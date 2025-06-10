**Introduction**

Pester is the ubiquitous testing framework for PowerShell, designed to help you verify that your scripts, functions, and modules behave as expected. With Pester you can:

* Write **unit tests** to validate individual functions in isolation.
* Create **integration tests** that exercise multiple components together.
* Generate **code coverage** reports to identify untested code paths.
* Integrate seamlessly into CI/CD pipelines (Azure DevOps, GitHub Actions, etc.) to enforce quality gates.

By adopting Pester, teams achieve greater confidence in change, faster feedback on defects, and a culture of test-driven development (TDD) in PowerShell.

---

## PowerShell (for Pester)

To write effective Pester tests, you need to understand key PowerShell features that influence how your code emits data and how Pester captures it.

### 1. Streams

PowerShell has **six streams** for different kinds of output. Pester can intercept or verify many of these:

| Stream          | Purpose                                           |
| --------------- | ------------------------------------------------- |
| **1. Output**   | Main data objects (e.g. custom objects, strings). |
| **2. Error**    | Non-terminating error messages.                   |
| **3. Warning**  | Informational warnings.                           |
| **4. Verbose**  | Detailed operational messages (–Verbose).         |
| **5. Debug**    | Debugging messages (–Debug).                      |
| **6. Progress** | Progress bars during long operations.             |

> **Tip:** Use `Should -Throw` to assert errors on the Error stream, and the `–Verbose` switch with `–PassThru` in your test runs to inspect verbose/debug output when diagnosing failures.

### 2. Outputs and Pipelines

* **Objects, not text**: PowerShell pipelines pass rich objects between commands. Your functions should emit structured objects (e.g. custom classes or PSCustomObject) rather than unparsed text, enabling Pester to inspect properties directly.
* **Return vs. Write-Host**:

  * Use `return` or write objects to the **Output** stream.
  * Avoid `Write-Host` in code you plan to test, as it writes directly to the console and bypasses standard streams.

### 3. Functions

* **Signature**: Declare parameter types and add `[CmdletBinding()]` to support common parameters (e.g. `–Verbose`, `–ErrorAction`), which Pester can leverage in tests.
* **Parameter validation**: Use `ValidateSet`, `ValidatePattern`, etc., to guard your inputs—tests should cover both valid and invalid parameters.
* **Output design**: Favor returning objects; testing properties becomes trivial:

  ```powershell
  function Get-User {
    [CmdletBinding()]
    param([string]$Name)
    return [PSCustomObject]@{ Name = $Name; Exists = $true }
  }
  ```

### 4. Modules

* **Module scope**: Encapsulate functions into modules (`.psm1` + module manifest `.psd1`) to keep code organized.

* **Dot-sourcing vs. Import-Module**: In tests, import the module under test:

  ```powershell
  BeforeAll { Import-Module "$PSScriptRoot/../MyModule.psm1" }
  ```

* **TestDrive**: Use Pester’s `TestDrive` (a temporary, isolated file system) for tests that write files:

  ```powershell
  Context "File-based operations" {
    BeforeEach { Set-Location TestDrive:\ }
    It "Creates the expected file" { … }
  }
  ```

---

## Pester Tests

Pester tests are PowerShell scripts (commonly `.Tests.ps1`) structured around *Describe*, *Context*, and *It* blocks.

### 1. Structure

```powershell
Describe "MyFunction" {
  
  Context "When called with valid input" {
    It "Returns the expected object" {
      $result = MyFunction -Param 'Value'
      $result | Should -BeOfType PSCustomObject
      $result.Property | Should -Be 'Expected'
    }
  }

  Context "When called with invalid input" {
    It "Throws a parameter validation error" {
      { MyFunction -Param $null } | Should -Throw
    }
  }

}
```

* **Describe**: Top-level grouping, usually named after your function or feature.
* **Context**: (Optional) Sub-grouping to clarify preconditions or scenario.
* **It**: Individual test case; contains one or more `Should` assertions.

### 2. Assertions: `Should`

Pester’s core assertion syntax follows `Should <Operator>`:

| Operator             | Example        | Use case                     |                           |
| -------------------- | -------------- | ---------------------------- | ------------------------- |
| `-Be`                | \`\$x          | Should -Be 42\`              | Exact value match         |
| `-BeOfType`          | \`\$o          | Should -BeOfType Hashtable\` | Type checking             |
| `-BeTrue`/`-BeFalse` | \`\$flag       | Should -BeTrue\`             | Boolean checks            |
| `-BeInRange`         | \`\$num        | Should -BeInRange 1,10\`     | Numeric range             |
| `-Match`             | \`\$s          | Should -Match '^Hello'\`     | Regex match               |
| `-Throw`             | \`{ Do-Thing } | Should -Throw }\`            | Expect an exception       |
| `-Contain`           | \`\$list       | Should -Contain 'Item'\`     | Membership in collections |
| `-HaveCount`         | \`\$a          | Should -HaveCount 3\`        | Collection size           |

### 3. Lifecycle Blocks

* **BeforeAll / AfterAll**: Run once per Describe (e.g. import module).
* **BeforeEach / AfterEach**: Run before/after each `It` block (e.g. set up test data, clean up).

### 4. Mocking

When your code calls external commands or services, use `Mock` to intercept and simulate behavior:

```powershell
Mock Get-Service { return @{ Status = 'Running' } }

It "Restarts service if not running" {
  Restart-ServiceIfStopped -Name 'Spooler'
  Assert-MockCalled Get-Service -Exactly 1 -Scope It
}
```

* **Mock** replaces the real command in the current scope.
* **Assert-MockCalled** verifies the mock was invoked as expected.

### 5. Organizing & Naming

* **File layout**:

  ```
  /Module
    MyModule.psm1
    MyModule.Tests.ps1
  ```
* **Naming conventions**:

  * Test files: `<ModuleName>.Tests.ps1`
  * Describe blocks: match function or class names.
  * It blocks: describe expected behavior in plain English.

### 6. Running Tests

* **Interactively**:

  ```powershell
  Invoke-Pester -Path .\MyModule.Tests.ps1 -Verbose
  ```
* **Code coverage**:

  ```powershell
  Invoke-Pester -CodeCoverage .\MyModule.psm1
  ```
* **CI Integration**: In Azure DevOps YAML:

  ```yaml
  - task: PowerShell@2
    displayName: 'Run Pester Tests'
    inputs:
      script: 'Invoke-Pester -Output Detailed'
  ```

### 7. Best Practices

* **TDD approach**: Write tests before code; drive your implementation.
* **Single assertion** per `It` where feasible—makes failures clearer.
* **Mock external dependencies** to isolate units under test.
* **Use TestDrive** for file-system or registry tests to avoid side-effects.
* **Keep tests fast**: avoid long waits or heavy integration steps in unit tests; reserve those for separate integration suites.
* **Review coverage reports**: aim for at least 80% coverage on critical modules.

---

By leveraging PowerShell’s rich streams and object model, structuring your code as modular functions, and applying Pester’s clear DSL (Describe/Context/It, Should, Mocks), you can build a robust suite of automated tests. This not only safeguards your scripts against regression but also accelerates development by providing immediate feedback on code changes.

---

## Streams

### Overview

PowerShell’s streams isolate message types so that piped commands only receive the Success (Output) stream by default ([devblogs.microsoft.com][2]).

* **Output (Success)**: Main data objects; use `Write-Output` or simply emit values ([learn.microsoft.com][1]).
* **Error**: Non-terminating errors via `Write-Error`; stored in `$Error` and can be made terminating with `-ErrorAction Stop` ([learn.microsoft.com][1]).
* **Warning**: Informational warnings with `Write-Warning` to signal deprecations or recoverable issues ([learn.microsoft.com][1]).
* **Verbose**: Detailed trace messages via `Write-Verbose` when `-Verbose` is specified ([learn.microsoft.com][1]).
* **Debug**: Developer-centric debug info via `Write-Debug` when `-Debug` is enabled ([learn.microsoft.com][1]).
* **Information**: General host messages with `Write-Information`, introduced in PowerShell 5 to replace unscriptable host output ([petri.com][7]).
* **Progress**: Progress bars via `Write-Progress`; not captured by pipelines or assignments ([learn.microsoft.com][1]).

### When to Use Each Stream

* **`Write-Output`** for returning objects your tests will assert on: it ensures the value flows through pipelines or assignments ([devblogs.microsoft.com][2]).
* **`Write-Error`** for recoverable errors that shouldn’t halt the function by default; your callers or tests can override with `-ErrorAction Stop` ([learn.microsoft.com][5]).
* **`throw`** when you need a **terminating error**—tests using `{ ... } | Should -Throw` will catch it, and execution stops immediately ([learn.microsoft.com][5]).
* **`Write-Warning`** to signal potential issues without affecting control flow; tests can assert on warnings with `Should -Throw` (if promoted) or by capturing the Warning stream ([learn.microsoft.com][1]).
* **`Write-Verbose`** and **`Write-Debug`** for detailed logs that only appear when explicitly requested, keeping normal test runs clean ([learn.microsoft.com][1]).
* **`Write-Information`** for general host messages that you don’t want treated as errors or verbose logs ([petri.com][7]).
* **`Write-Progress`** in long-running functions to display progress bars; avoid in unit-tested code unless you redirect or suppress it ([learn.microsoft.com][1]).

```powershell
function Get-Data {
  [CmdletBinding()]
  param([string]$Id)
  if (-not $Id) {
    throw "Id is required"                   # terminating error for invalid input :contentReference[oaicite:19]{index=19}
  }
  Write-Verbose "Fetching data for $Id"       # detailed log, shown only with -Verbose :contentReference[oaicite:20]{index=20}
  try {
    # Simulate fetch
    $result = @{ Id = $Id; Value = 42 }
    Write-Output $result                      # pass object to pipeline :contentReference[oaicite:21]{index=21}
  } catch {
    Write-Error "Fetch failed: $_"            # non-terminating by default :contentReference[oaicite:22]{index=22}
  }
}
```

---

## Functions

### Why Create Functions

1. **Reusability**: Encapsulate discrete operations to avoid copy/paste and ensure consistency across scripts ([learn.microsoft.com][4]).
2. **Testability**: Small, focused functions make it easy to write precise Pester tests using `Describe`/`It` blocks ([devblogs.microsoft.com][2]).
3. **Parameter Validation**: Built-in attributes (`ValidateSet`, `ValidatePattern`) guard inputs, and Pester tests can cover both valid and invalid cases ([learn.microsoft.com][3]).
4. **Pipeline Support**: Functions return objects that flow through pipelines, enabling composition and simple assertions ([devblogs.microsoft.com][8]).
5. **Maintainability**: Logical separation of concerns and modules (`.psm1` + `.psd1`) improves readability and CI integration ([learn.microsoft.com][1]).

### Advanced Functions & CmdletBinding

Applying `[CmdletBinding()]` elevates a function to an **advanced function**, automatically adding common parameters like `-Verbose`, `-Debug`, and `-ErrorAction` ([learn.microsoft.com][3]). You can also leverage methods on the `$PSCmdlet` object (e.g., `ShouldProcess`, `ThrowTerminatingError`) for granular control over processing and error reporting ([learn.microsoft.com][9]).

```powershell
function Remove-ItemSafely {
  [CmdletBinding(SupportsShouldProcess=$true)]
  param([string]$Path)
  if ($PSCmdlet.ShouldProcess($Path, 'Remove')) {
    if (Test-Path $Path) {
      Remove-Item $Path -ErrorAction Stop    # will throw terminating errors on failure :contentReference[oaicite:30]{index=30}
    } else {
      Write-Warning "Path not found: $Path"  # non-terminating warning :contentReference[oaicite:31]{index=31}
    }
  }
}
```

---

## Throw vs. Output

* **`throw`** generates a **terminating error** that halts execution immediately (unless caught), ideal for input validation failures or unrecoverable issues ([learn.microsoft.com][5]).
* **`Write-Error`** emits a **non-terminating error** to the Error stream; execution continues, and `$Error` is updated. Use `-ErrorAction Stop` to convert it into a terminating error if needed ([learn.microsoft.com][5]).
* **`Write-Output`** (or implicit output) writes to the **Success stream**, ensuring values flow through pipelines or assignments without interrupting control flow ([devblogs.microsoft.com][2]).

```powershell
function Test-Input {
  param([int]$Number)
  if ($Number -lt 0) {
    throw "Negative numbers are not allowed"           # halts execution :contentReference[oaicite:35]{index=35}
  } elseif ($Number -eq 0) {
    Write-Error "Zero is not useful" -ErrorAction Continue  # logs error but continues :contentReference[oaicite:36]{index=36}
  } else {
    Write-Output "You passed $Number"                   # normal output :contentReference[oaicite:37]{index=37}
  }
}
```

By mastering these streams and function patterns, your Pester tests can precisely target expected outputs, errors, and side-effects—resulting in robust, maintainable PowerShell code.

[1]: https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_output_streams?view=powershell-7.5&utm_source=chatgpt.com "about_Output_Streams - PowerShell | Microsoft Learn"
[2]: https://devblogs.microsoft.com/scripting/understanding-streams-redirection-and-write-host-in-powershell/?utm_source=chatgpt.com "Understanding Streams, Redirection, and Write-Host in PowerShell"
[3]: https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_functions_advanced?view=powershell-7.5&utm_source=chatgpt.com "about_Functions_Advanced - PowerShell | Microsoft Learn"
[4]: https://learn.microsoft.com/en-us/powershell/scripting/learn/ps101/09-functions?view=powershell-7.5&utm_source=chatgpt.com "Functions - PowerShell | Microsoft Learn"
[5]: https://learn.microsoft.com/en-us/powershell/scripting/learn/deep-dives/everything-about-exceptions?view=powershell-7.5&utm_source=chatgpt.com "Everything you wanted to know about exceptions - PowerShell"
[6]: https://sqljana.wordpress.com/2017/05/16/thoughts-on-when-to-use-write-host-write-output-write-debug-write-warning-write-verbose-write-errorthrow/?utm_source=chatgpt.com "Thoughts On When To Use – Write-Host, Write-Output, Write-Debug ..."
[7]: https://petri.com/understanding-how-streams-work-in-powershell-7/?utm_source=chatgpt.com "Understanding How Streams Work in PowerShell 7"
[8]: https://devblogs.microsoft.com/scripting/incorporating-pipelined-input-into-powershell-functions/?utm_source=chatgpt.com "Incorporating Pipelined Input into PowerShell Functions"
[9]: https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_functions_advanced_methods?view=powershell-7.5&utm_source=chatgpt.com "about_Functions_Advanced_Met..."
