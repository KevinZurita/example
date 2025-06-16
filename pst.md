# Testing Framework Configuration and Setup

## Table of Contents

- [Overview](#overview)  
  - [Introduction](#introduction)  
  - [Definitions](#definitions)  
  - [Scope](#scope)  
  - [Value](#value)  
  - [Stakeholders](#stakeholders)  
- [Testing Framework Components & Configuration](#testing-framework-components--configuration)  
  - [Testing Framework Components](#testing-framework-components)  
  - [Framework Configuration](#framework-configuration)  
  - [Testing Modalities](#testing-modalities)  
- [Pester Testing Standards](#pester-testing-standards)  
  - [Pester Test Workflow and Syntax](#pester-test-workflow-and-syntax)  
  - [Authentication](#authentication)  
  - [Test Structure and Examples](#test-structure-and-examples)  
  - [Functions](#functions)  
  - [Modules](#modules)  
  - [Test Coverage](#test-coverage)  
  - [Adding Tests for New and Existing Scripts](#adding-tests-for-new-and-existing-scripts)  
- [PowerShell Coding Standards](#powershell-coding-standards)  
  - [PowerShell Coding Standards for Automated Testing](#powershell-coding-standards-for-automated-testing)  
  - [Error Handling and Output](#error-handling-and-output)  
  - [Advanced PowerShell Language Features](#advanced-powershell-language-features)  
- [References](#references)

---

## Overview

### Introduction
This document provides standardized guidance for configuring and setting up automated testing frameworks for PowerShell in NM Cloud Operations. It covers prerequisites, installation, configuration, CI/CD integration, best practices, and troubleshooting, with a focus on Pester and Azure DevOps compatibility.

To achieve these goals, NM Cloud Operations has developed an Automated Testing Framework with the following objectives:
- Ensure early detection of bugs and regressions through comprehensive automated testing.
- Promote consistent, high-quality PowerShell code by enforcing documentation and code quality standards.
- Streamline CI/CD processes by providing reusable pipeline templates and automation scripts.
- Increase developer confidence and productivity by enabling rapid feedback and safe refactoring.
  
The framework consists of:
- A reusable YAML pipeline template for standardized CI/CD test execution.
- A centralized `TestExecutionScript.ps1` for orchestrating and running all Pester tests.
- Dedicated scripts for code quality and documentation validation, ensuring every script meets organizational standards.
- A dedicated Azure Agent Pool that provides consistent compute resources for pipeline execution.

Together, these components provide a robust, scalable, and maintainable approach to automated testing, supporting best practices throughout the PowerShell development lifecycle at NM. The scope of this document is to detail the Standards for PowerShell automated testing using Pester. Automated testing is essential for modern software development, providing early bug detection, improved code quality, faster feedback, and increased developer productivity.

### Definitions
Include key terms, acronyms, and abbreviations used in the document. Example:

| Term   | Definition                       |
| ------ | -------------------------------- |
| Term 1 | This is my definition for Term 1 |
| Term 2 | This is my definition for Term 2 |

### Scope

This standard applies to all PowerShell scripts, modules, and automation maintained or developed by NM Cloud Operations, especially those integrated into Azure DevOps pipelines. It covers all stages of development with this testing framework, CI/CD execution, error handling, test structure, and code organization.

### Value

Automated tests are essential for modern software development, providing significant value throughout the development lifecycle:
- **Early Bug Detection & Prevention:** Automated unit and regression tests catch issues early, reducing the cost and effort of fixes and preventing regressions as code evolves.
- **Improved Code Quality & Maintainability:** Test-driven development (TDD) and comprehensive test suites encourage modular, well-structured, and maintainable code, while serving as living documentation for intended behavior.
- **Faster Feedback & Debugging:** Automated tests in CI/CD pipelines provide rapid feedback on code changes, enabling quick identification and resolution of issues, and streamlining debugging.
- **Developer Productivity & Safe Refactoring:** Reliable tests empower developers to make changes and refactor code with confidence, knowing that defects will be caught automatically.
- **Efficiency, Scalability & Cost Savings:** Automation reduces manual testing effort, accelerates delivery, scales with application complexity, and lowers long-term costs by catching issues early.
- **Collaboration & Continuous Improvement:** Shared test suites foster better communication between teams, and test metrics drive ongoing process improvement and resource optimization.

In summary, automated testing is a critical investment that ensures software quality, reliability, and agility at scale.


### Stakeholders
- NM Cloud Operations Team

---

## Testing Framework Components & Configuration

### Testing Framework Components  
**Description:** Provide a concise description of the standards purpose & objective.  
**Guidelines:** Outline the specific guidelines, best practices, or requirements related to the standards.  
**Implementation:** Offer guidance on how to implement the standard effectively.  
**Compliance:** Explain how compliance with the standard will be measured or assessed.  
**Environment Considerations:** If the standard is different by environment, include those details.  

| Column 1 | Column 2 | Column 3 | Column 4 |
| -------- | -------- | -------- | -------- |

### Framework Configuration  
**Description:** Provide a concise description of the standards purpose & objective.  
**Guidelines:** Outline the specific guidelines, best practices, or requirements related to the standards.  
**Implementation:** Offer guidance on how to implement the standard effectively.  
**Compliance:** Explain how compliance with the standard will be measured or assessed.  
**Environment Considerations:** If the standard is different by environment, include those details.  

| Column 1 | Column 2 | Column 3 | Column 4 |
| -------- | -------- | -------- | -------- |

### Testing Modalities  
**Description:** Provide a concise description of the standards purpose & objective.  
**Guidelines:** Outline the specific guidelines, best practices, or requirements related to the standards.  
**Implementation:** Offer guidance on how to implement the standard effectively.  
**Compliance:** Explain how compliance with the standard will be measured or assessed.  
**Environment Considerations:** If the standard is different by environment, include those details.  

| Column 1 | Column 2 | Column 3 | Column 4 |
| -------- | -------- | -------- | -------- |

---
## Pester Testing Standards

### Pester Test Workflow and Syntax

**Description:**
Defines the workflow, syntax, and best practices for writing and organizing Pester tests in PowerShell projects. Covers file placement, naming conventions, test discovery, execution, test file structure, setup/teardown, mocking, and the use of tags for test selection.

**Guidelines:**

* **File Placement & Naming:**

  * Place test files in a dedicated `Tests/` directory or adjacent to the scripts/modules under test.
  * Test filenames must end in `.Tests.ps1` (e.g., `MyScript.Tests.ps1`).

* **Test Discovery & Execution:**

  * Pester automatically discovers `.Tests.ps1` files using `Invoke-Pester`.
  * Run with specific tags or paths as needed:

    ```powershell
    Invoke-Pester -Path ./Tests -Tag 'Unit'
    ```

* **Test File Structure:**

  * Use `BeforeAll` for global setup and `AfterAll` for cleanup.
  * Use `Describe` to group related tests.
  * Use `Context` to define specific conditions.
  * Use `It` blocks for individual assertions.

* **Mocking:**

  * Use `Mock` to simulate external dependencies.
  * Avoid mocking core commands unnecessarily.
  * Validate mock usage with `Assert-MockCalled`.

* **Tags:**

  * Define test purpose with tags for filtering:

    ```powershell
    Describe 'Unit Test' -Tag 'Unit' { ... }
    ```

**Test Types:**

| Test Type   | Tag         | Purpose                      | Example Reference                 |
| ----------- | ----------- | ---------------------------- | --------------------------------- |
| Unit        | Unit        | Test individual functions    | `Describe ... -Tag 'Unit'`        |
| Integration | Integration | Validate integration points  | `Describe ... -Tag 'Integration'` |
| EndToEnd    | EndToEnd    | Validate full execution flow | `Describe ... -Tag 'EndToEnd'`    |
| Quality     | Quality     | Style, lint, documentation   | `Describe ... -Tag 'Quality'`     |

**Implementation Template:**

```powershell
BeforeAll {
    # Set up reusable variables or mocks
}

Describe 'MyFunction' -Tag 'Unit' {
    Context 'When called with valid input' {
        It 'should return expected output' {
            MyFunction -Param 'value' | Should -Be 'expected'
        }
    }
}

AfterAll {
    # Cleanup logic
}
```

**Compliance:**

* All scripts must include `.Tests.ps1` files.
* Every exported function must have test coverage for normal, edge, and error conditions.
* Tags must be appropriately applied to each `Describe` block.

**Environment Considerations:**

* Local dev may rely on interactive login.
* CI/CD must use service principals or managed identity for non-interactive runs.

---

### Common Pester Assertions

| Assertion               | Use Case                 | Example        | Notes                       |                                  |
| ----------------------- | ------------------------ | -------------- | --------------------------- | -------------------------------- |
| `Should -Be`            | Exact value match        | \`\$x          | Should -Be 5\`              | Simple value assertion           |
| `Should -Match`         | Regex match              | \`\$str        | Should -Match 'error'\`     | Useful for log content           |
| `Should -Contain`       | Collection contains item | \`\$arr        | Should -Contain 'admin'\`   | Array or hashtable keys          |
| `Should -Throw`         | Error expected           | \`{ Do-Thing } | Should -Throw\`             | Always wrap in script block      |
| `Should -BeExactly`     | Case-sensitive match     | \`\$name       | Should -BeExactly 'Admin'\` | Rarely needed                    |
| `Should -BeGreaterThan` | Numeric comparison       | \`10           | Should -BeGreaterThan 5\`   | Intuitive for counters or limits |

---

### Authentication

**Description:**
Outlines how to implement and test authentication logic that works both interactively (local dev) and non-interactively (CI/CD).

**Guidelines:**

* Use interactive methods (e.g., `Connect-AzAccount`) only for local dev.
* Design all automation scripts to use service principals, managed identity, or credential parameters.
* Store credentials in pipeline variables or a secure vault.
* Refactor scripts to support `-ServicePrincipalSecret`, `-NonInteractive`, or similar parameters.

**Implementation:**

```powershell
$SecurePW = $env:AZURE_SECRET | ConvertTo-SecureString -AsPlainText -Force
Connect-AzAccount -ServicePrincipal -Tenant $Tenant -Credential (New-Object PSCredential($AppId, $SecurePW))
```

**Authentication Table:**

| Method          | Use Case          | Example                               | Notes                               |
| --------------- | ----------------- | ------------------------------------- | ----------------------------------- |
| Interactive     | Local development | `Connect-AzAccount`                   | Avoid in automation scripts         |
| Non-Interactive | CI/CD             | `Connect-AzAccount -ServicePrincipal` | Use in pipeline and test setups     |
| Reusable Module | Standardization   | `ConnectToServices.psm1`              | Centralizes logic and reduces drift |

**Compliance:**

* All automated tests must use non-interactive authentication.
* CI/CD logs must not contain secrets or prompts.

---

### Pester Test Structure Examples

| Block       | Purpose                  | Example                             | Notes                               |
| ----------- | ------------------------ | ----------------------------------- | ----------------------------------- |
| `BeforeAll` | Global setup             | Variable init, authentication setup | Runs once per `Describe` block      |
| `Describe`  | Group related test cases | `Describe 'Get-Report' {}`          | Apply tags here                     |
| `Context`   | Sub-scenario group       | `Context 'With null input' {}`      | Optional for complex tests          |
| `It`        | Single test expectation  | `It 'Should return X' { ... }`      | Must contain at least one assertion |
| `AfterAll`  | Global teardown          | Clean up resources or temp files    | Runs once after all tests           |

---

### Functions in Tests

**Best Practices:**

* Functions should be written with testability in mind.
* Each function should be imported and tested in isolation.
* Avoid reliance on global or script scope variables.

**Implementation Tips:**

* Use `param()` to inject dependencies.
* Return values instead of writing to output stream.
* Import functions using dot-sourcing or `Import-Module`:

```powershell
. "$PSScriptRoot\..\MyModule.psm1"
```

**Function Test Table:**

| Practice        | Rationale             | Example          | Notes                           |
| --------------- | --------------------- | ---------------- | ------------------------------- |
| `param()` usage | Dependency injection  | `param($key)`    | Supports mock inputs            |
| Return values   | Test-friendly results | `return $result` | Avoid `Write-Host`              |
| Imports         | Load target function  | `Import-Module`  | Use module versioning if needed |

---

### Writing Tests for New and Existing Scripts

**Standards:**

* All new scripts must come with `.Tests.ps1` files.
* Existing scripts should be refactored over time to include test coverage.
* Focus test additions on high-risk or frequently modified scripts.

**Compliance Expectations:**

| Script Type | Test Standard        | Notes                          |
| ----------- | -------------------- | ------------------------------ |
| New         | Full compliance      | Must follow test standards     |
| Existing    | Incremental adoption | Prioritize based on usage/risk |

---

### Coverage Requirements

**Description:**
Defines expectations for coverage, including what counts as adequate coverage for PowerShell scripts.

**Requirements:**

* At least one test for each:

  * Expected success case (valid return value)
  * Expected failure or `throw`
  * Expected stream output (e.g., verbose, error)

**Examples:**

```powershell
It 'Should throw on bad input' {
    { Do-Thing -BadParam } | Should -Throw
}

It 'Should return value on success' {
    Do-Thing -GoodParam | Should -Be 42
}
```

**Coverage Table:**

| Requirement       | Rationale                | Test Type   | Example Reference               |
| ----------------- | ------------------------ | ----------- | ------------------------------- |
| Throws on error   | Fail-fast on invalid use | Unit        | `Should -Throw`                 |
| Expected output   | Returns correct result   | Unit        | `Should -Be`, `Should -Contain` |
| Stream validation | Validates logging format | Integration | `Should -Match 'VERBOSE:'`      |

---

For additional syntax, see the official [Pester documentation](https://pester.dev).

---
## Pester Testing Standards
### Pester Test Workflow and Syntax  
**Description:** Defines the workflow, syntax, and best practices for writing and organizing Pester tests in PowerShell projects. Covers file placement, naming conventions, test discovery, execution, test file structure, setup/teardown, mocking, and the use of tags for test selection.

**Guidelines:**

**File Placement & Naming:** Place all test files in a dedicated `Tests` directory or alongside the scripts/modules they test. Name test files with the `.Tests.ps1` suffix (e.g., `MyScript.Tests.ps1`).
**Discovery & Run:** Pester automatically discovers test files ending with `.Tests.ps1`. Use a consistent structure for test files to enable easy discovery and execution in CI/CD.
**Test File Structure:** Use `BeforeAll` and `AfterAll` blocks for setup and teardown. Organize tests using `Describe`, `Context`, and `It` blocks for clarity and maintainability.
**Mocking:** Use `Mock` to simulate dependencies and isolate units of code. Only mock external dependencies or side effects, not the code under test.
**Tags:** Use tags (e.g., `Unit`, `EndToEnd`, `Integration`, `Quality`) to categorize tests. Tags enable selective test execution in pipelines (see `azure-pipelines.yml` and `pester-tests.yml`).

**Test Types:**

- **Unit Tests:** Test individual functions or logic, using mocks as needed. Should cover all expected results (throws, outputs, returns).
- **EndToEnd Tests:** Validate full script execution, including resource creation and teardown. Use tags like `EndToEnd` for these.
  
** Implementation** :
- Place your test files in the appropriate directory and follow the naming convention.
- Use the following template for structuring your tests:
**Compliance:**
  
- All new scripts must include corresponding `.Tests.ps1` files following this structure.
- Tests must be tagged appropriately and cover all major code paths.
- Code reviews and CI/CD pipelines will enforce compliance.

**Environment Considerations:**
- Local development may use interactive authentication; CI/CD must use non-interactive methods.
- Ensure secrets and credentials are handled securely in all environments.
  
**Sample Table Formatting:**
| Test Type   | Tag         | Purpose                      | Example/Reference                 |
| ----------- | ----------- | ---------------------------- | --------------------------------- |
| Unit        | Unit        | Test individual functions    | `Describe ... -Tag "Unit"`        |
| EndToEnd    | EndToEnd    | Full script execution        | `Describe ... -Tag "EndToEnd"`    |
| Integration | Integration | Test integration points      | `Describe ... -Tag "Integration"` |
| Quality     | Quality     | Code/documentation standards | `Describe ... -Tag "Quality"`     |

 

---

 

### Authentication
**Description:** Explains the difference between interactive and non-interactive authentication methods in PowerShell testing, and why non-interactive authentication is required for automated tests in CI/CD environments.

**Guidelines:**
- **Interactive Authentication:** Typically uses prompts or device login. Suitable for local development but not for automation. 
- **Non-Interactive Authentication:** Uses service principals, managed identities, or stored credentials. Required for CI/CD and automated testing.
- **Best Practice:** Always design scripts and tests to support non-interactive authentication for automation. Use secure methods to pass secrets (e.g., pipeline variables, Azure Key Vault).
- **Reusable Modules:** Leverage shared authentication modules (e.g., `ConnectToServices.psm1`) to standardize and simplify authentication logic across scripts and tests.
**Implementation:**
- Refactor scripts to accept credentials or secrets as parameters (e.g., `-ServicePrincipalSecret`).
- In test setup (`BeforeAll`), convert secrets to `SecureString` and pass to scripts under test.
- Use pipeline variables or Azure Key Vault for secret management in CI/CD.
- Example:
    ```powershell

    $SecurePW = $ServicePrincipalSecret | ConvertTo-SecureString -AsPlainText -Force

    . $RunScript -ServicePrincipalSecret $SecurePW -NonInteractive

    ```

**Compliance:**

- All scripts and tests intended for automation must support non-interactive authentication.
- Code reviews and pipeline runs will verify that no interactive prompts are present in automated tests.
**Environment Considerations:**

- Local development may use interactive authentication for convenience.
- CI/CD and shared environments must use non-interactive authentication for security and reliability.
 
**Authentication Table:**

| Method          | Use Case          | Example/Reference                     | Notes                                   |
| --------------- | ----------------- | ------------------------------------- | --------------------------------------- |
| Interactive     | Local development | `Connect-AzAccount`                   | Not for automation                      |
| Non-Interactive | CI/CD, automation | `Connect-AzAccount -ServicePrincipal` | Use in all automated test scenarios     |
| Module-based    | Shared logic      | `ConnectToServices.psm1`              | Use for consistency and maintainability |
 

### Pester Test Structure & Examples
**Description:** Provides design decisions, rationale, and a template for structuring Pester tests, including setup, teardown, and best practices for maintainable and effective test suites.

**Guidelines:**
- Use `BeforeAll` for test setup and `AfterAll` for cleanup.
- Organize tests using `Describe`, `Context`, and `It` blocks.
- Use `Mock` to isolate units and simulate dependencies.
- Ensure each function or module has at least one unit test for every expected result (throw, output, return value).
- End-to-end tests should validate full script execution and resource cleanup.
  
**Implementation:**
- Follow the provided template for new test files.
- Use tags to categorize tests and enable selective execution in CI/CD.
Example:

**Compliance:**
- All new scripts must have corresponding tests following this structure.
- Tests must cover all major code paths and expected results.
- Code reviews and CI/CD will enforce compliance.
  
**Environment Considerations:**
- Ensure tests are environment-agnostic and do not rely on interactive input.
- Use mocks and cleanup logic to avoid side effects in shared environments.
  
**Sample Table Formatting:**

| Block     | Purpose              | Example/Reference            | Notes                       |
| --------- | -------------------- | ---------------------------- | --------------------------- |
| BeforeAll | Setup                | Test variable initialization | Runs once before all tests  |
| Describe  | Group related tests  | `Describe ...`               | Use tags for test selection |
| It        | Individual test case | `It "Should ..." { ... }`    | One per expected result     |
| AfterAll  | Cleanup              | Resource deletion            | Runs once after all tests   |

###Functions

**Description:** Explains the importance of writing functions in PowerShell scripts, how to write them, and how to import them for testing.

**Guidelines:**

- Write reusable, single-responsibility functions for all logic.
- Use `param` blocks to define inputs and support testability.
- Export functions from modules for easy import and testing.
- Avoid global variables; use local scope within functions.
  
**Implementation:**
- Refactor scripts into functions and modules where possible.
- Import functions in test files using `Import-Module` or dot-sourcing.
  
**Compliance:**
- All new scripts should be function-based for testability.
- Code reviews will check for function structure and test coverage.
  
**Environment Considerations:**
- Functions should not rely on environment-specific state.
- Use parameters for all external dependencies.
  
**Sample Table Formatting:**

| Practice       | Rationale          | Example/Reference      | Notes                       |
| -------------- | ------------------ | ---------------------- | --------------------------- |
| Function-based | Testability, reuse | `function ... { ... }` | Use in all new scripts      |
| Param blocks   | Input validation   | `param([string]$Name)` | Required for test injection |
| Exported       | Import for testing | `Export-ModuleMember`  | For modules                 |

### Modules
**Description:** TODO: Describes the benefits of using modules for PowerShell code and testing, and how to structure and import them. The best practices for creating modules.

**Guidelines:**
- Organize related functions into modules (`.psm1` files).
- Use modules to encapsulate logic and dependencies.
- Export only public functions; keep helpers private.
- Place module tests in corresponding `.Tests.ps1` files.

**Implementation:**

- Create a module for each major domain or service.
- Use `Import-Module` in test files to load modules for testing.

Example:

**Compliance:**
- All new code should be organized into modules where practical.
- Tests must cover all exported functions.

**Environment Considerations:**
- Modules should be portable and not rely on environment-specific state.
- Use parameters for configuration.

**Sample Table Formatting:**

| Practice      | Rationale            | Example/Reference     | Notes                          |
| ------------- | -------------------- | --------------------- | ------------------------------ |
| Module-based  | Encapsulation, reuse | `.psm1` files         | Use for all major code domains |
| Exported only | Testability          | `Export-ModuleMember` | Only export public functions   |

### Adequate Testing Coverage
**Description:** Details the minimum requirements for test coverage, including unit and end-to-end tests, and how to ensure all code paths are tested.
**Guidelines:**
- Every function must have at least one unit test for each expected result (throw, output, return value).
- End-to-end tests should validate complete script execution and resource cleanup.
- Use mocks to isolate units and avoid side effects.
**Implementation:**
- Review all functions and ensure corresponding tests exist.
- Use code coverage tools or manual review to identify gaps.

- Example:
    ```powershell
    It "Should throw on invalid input" { { MyFunction -BadInput } | Should -Throw }

    It "Should return expected value" { MyFunction -GoodInput | Should -Be 42 }

  ```
**Compliance:**
- Code reviews and CI/CD pipelines will enforce coverage requirements.
- Test results and coverage reports should be reviewed regularly.

**Environment Considerations:**
- Tests should be environment-agnostic and not rely on external state.
- Use mocks and cleanup logic to avoid persistent changes.

**Sample Table Formatting:**
| Requirement            | Rationale           | Example/Reference              | Notes                   |
| ---------------------- | ------------------- | ------------------------------ | ----------------------- |
| Unit test per function | Ensures correctness | `It "Should ..." { ... }`      | One per expected result |
| End-to-end test        | Validates workflow  | `Describe ... -Tag "EndToEnd"` | Covers full execution   |

### Writing Tests For New Scripts and Existing Scripts
**Description:** Explains the expectations for new scripts to follow these standards, and guidance for refactoring existing scripts.
**Guidelines:**
- All new scripts must adhere strictly to these standards.
- Existing scripts in production should be refactored as time and resources allow, prioritizing high-impact or frequently changed scripts.
- Developers have discretion for legacy code, but are encouraged to improve testability and structure over time.
**Implementation:**
- Use this standard as a checklist for all new development.
- Plan refactoring of legacy scripts as part of technical debt management.
**Compliance:**
- New scripts will be reviewed for full compliance.
- Existing scripts should show progress toward compliance over time.
**Environment Considerations:**
- Refactoring should not disrupt production operations.
- Prioritize test coverage for critical or high-risk scripts.
**Sample Table Formatting:**

| Script Type | Standard Applied     | Example/Reference          | Notes                          |
| ----------- | -------------------- | -------------------------- | ------------------------------ |
| New         | Full compliance      | Follows all sections above | Required for all new scripts   |
| Existing    | Refactor as feasible | Incremental improvements   | Prioritize high-impact scripts |

 ## Mocking and Integration in Pester

### Mocking Strategy

**Purpose:** Enable reliable, isolated testing of PowerShell functions and modules by substituting external dependencies.

**Best Practices:**

* Use `Mock` to replace external functions or commands during test execution.
* Always test the behavior, not the implementation details.
* Limit the scope of mocks using `-ModuleName` or script scope.
* Avoid mocking internal functions unnecessarily.

**✅ Do:**

```powershell
Describe 'Get-DataFromAPI' {
    Mock Invoke-RestMethod { return @{ Name = 'Test' } }

    It 'should return a Name property' {
        (Get-DataFromAPI).Name | Should -Be 'Test'
    }
}
```

**🚫 Avoid:**

```powershell
Mock Write-Output { "forced" }  # Unnecessary mocking of core cmdlets
```

**Implementation Tips:**

* Mock `Start-Job`, `Invoke-RestMethod`, `Get-ChildItem`, or any filesystem/network interaction.
* Validate mocks were called using `Assert-MockCalled`.

---

### Integration with CI/CD Pipelines

**Goal:** Ensure tests run consistently in build pipelines and failures are surfaced early.

**Implementation Steps:**

* Install Pester in the agent or container.
* Run tests using:

```powershell
Invoke-Pester -Path "./Tests" -Output Detailed -CI
```

* Export results for reporting:

```powershell
Invoke-Pester -Path "./Tests" -OutputFormat NUnitXml -OutputFile "TestResults.xml"
```

* In Azure DevOps, publish results with:

```yaml
- task: PublishTestResults@2
  inputs:
    testResultsFiles: '**/TestResults.xml'
    testResultsFormat: 'NUnit'
```

---

### Recommended Folder Layout

```text
ProjectRoot/
│
├── Modules/
│   ├── MyModule/
│   │   ├── Public/
│   │   ├── Private/
│   │   ├── MyModule.psd1
│   │   └── MyModule.psm1
│
├── Tests/
│   ├── MyModule.Tests.ps1
│   └── MockData/
│
└── azure-pipelines.yml
```

---

## PowerShell Coding Standards

### PowerShell Coding Standards for Automated Testing

**Description:**
This standard defines the structure, practices, and expectations for writing PowerShell code that supports automated testing using Pester. Its objective is to create consistent, maintainable, and testable PowerShell code across all scripts and modules used in CI/CD pipelines and production workloads.

**Guidelines:**

* **Function-First Design:** Encapsulate all logic in advanced functions with `CmdletBinding`. Avoid inline script logic.

  **✅ Do:**

  ```powershell
  function Get-UserData {
      [CmdletBinding()]
      param([string]$UserName)
      return "Data for $UserName"
  }
  ```

  **🚫 Avoid:**

  ```powershell
  $UserName = 'Kevin'
  Write-Output "Data for $UserName"
  ```

* **Single Responsibility Principle:** Each function should perform one specific task. Split logic into units.

* **Comment-Based Help:** All functions must include help blocks with synopsis, description, and examples.

* **Avoid Global State:** Avoid `$global:` or shared variables.

* **Naming Conventions:** Use PascalCase for functions, camelCase for local variables.

* **Approved Verbs:** Stick to verbs from `Get-Verb`.

* **Validation Attributes:** Use parameter validation where applicable.

* **Modular Structure:** Prefer modules over monolithic scripts.

**Implementation:**
Adopt a module-based structure with `Public/`, `Private/`, and `Tests/` folders. Use PSScriptAnalyzer:

```powershell
Invoke-ScriptAnalyzer -Path ./Scripts -Recurse -Settings PSGallery
```

**Compliance:**

* PSScriptAnalyzer must pass.
* All exported functions must have unit tests.
* Violations surfaced in pull requests.

**Environment Considerations:**

* Relaxed in local/dev, stricter in CI/prod.

| Topic           | Standard Requirement | Example/Tool            | Notes                      |
| --------------- | -------------------- | ----------------------- | -------------------------- |
| Naming          | Verb-Noun            | `Get-Report`            | Use `Get-Verb`             |
| Help Comments   | Required             | `<# .SYNOPSIS ... #>`   | Use `New-HelpComment` tool |
| Script Analyzer | Mandatory            | `Invoke-ScriptAnalyzer` | CI integrated              |
| Structure       | Module-Based         | `Public/Private/Tests`  | Scaffold with `Plaster`    |

---

### Error Handling and Output

**Description:**
Defines how errors and output streams must be handled in PowerShell code to ensure testability, consistency, and clarity in diagnostics.

**Guidelines:**

* Use `throw` to indicate logic errors you want your tests to assert.
* Use `Write-Error` for runtime errors that might allow continued execution.
* Use `Write-Verbose` for developer insights.
* Use `Write-Warning` to alert non-fatal conditions.
* Avoid `Write-Host` as it bypasses streams.
* Use `Write-Output` when the function is returning data to another command or for Pester assertions.
* Use `Write-Information` for user-facing runtime logs that can be captured explicitly.

**✅ Do:**

```powershell
function Connect-Service {
    [CmdletBinding()]
    param()
    try {
        Do-Connect -ErrorAction Stop
    } catch {
        throw "Connection failed: $_"
    }
}
```

**🚫 Avoid:**

```powershell
function Connect-Service {
    Write-Host "Attempting connection..."
    Do-Connect
    if (!$?) { Write-Host "Failed" }
}
```

**Implementation:**
Enable `$ErrorActionPreference = 'Stop'`. Capture streams in tests:

```powershell
{ Get-Thing -BadParam } | Should -Throw
```

Stream handling:

```powershell
Write-Output "output"         # Passes to pipeline
Write-Verbose "debug"         # Use for dev visibility
Write-Information "log"       # Capturable in CI logs
Write-Warning "warning"       # Alerts user, non-fatal
Write-Error "failure"         # Error stream, avoid if `throw` is better
```

**Compliance:**

* All outputs must be testable.
* Stream misuse is flagged in reviews.
* Logs should never leak secrets.

**Environment Considerations:**

* Verbose and information logs may be disabled in production unless explicitly enabled.

| Stream      | Use Case                   | ✅ Use Case Example  | 🚫 Anti-Pattern                |
| ----------- | -------------------------- | ------------------- | ------------------------------ |
| Output      | Primary return values      | `return $result`    | `Write-Host $result`           |
| Error       | Script-breaking conditions | `throw "Error"`     | `Write-Error` for logic errors |
| Warning     | Alert but continue         | `Write-Warning`     | Using error instead            |
| Verbose     | Developer diagnostics      | `Write-Verbose`     | Hardcoded log messages         |
| Information | Operational logs           | `Write-Information` | Overusing `Write-Output`       |

---

### Advanced PowerShell Language Features

**Description:**
Guidance on when and how to apply advanced features like classes, script blocks, dynamic params, and streaming logic to make code more testable and modular.

**Guidelines:**

* **Classes:** Use for internal stateful modeling (e.g., job objects), but avoid unless necessary.
* **Script Blocks:** Use for deferred logic or `Invoke-Command`. Avoid overly complex inline blocks.
* **Dynamic Parameters:** Use when parameter availability depends on external context. Avoid when static params suffice.
* **Pipeline Support:** Ensure you handle piped input correctly using `process {}` blocks.
* **Closures:** Script blocks can be passed to functions for mockable behavior.

**✅ Do:**

```powershell
function Get-Name {
    [CmdletBinding()]
    param([string[]]$InputObject)
    process {
        foreach ($name in $InputObject) {
            [PSCustomObject]@{ Name = $name }
        }
    }
}
```

**🚫 Avoid:**

```powershell
function Get-Name {
    param($InputObject)
    foreach ($name in $InputObject) {
        Write-Output $name
    }
}
```

**Implementation:**

* Use `Export-ModuleMember` for module scope control.
* Test class behavior via method calls and assert internal state.
* Test pipeline functions with arrays and piped input:

  ```powershell
  @("one","two") | Get-Name | Should -HaveCount 2
  ```

**Compliance:**

* Any dynamic parameter or class must include justification and tests.
* Streaming functions must work with single and multiple items.

**Environment Considerations:**

* Classes are only supported in PowerShell 5+ and PowerShell Core.
* Pipeline logic must work cross-platform and in non-interactive shells.

| Feature       | Use Case             | ✅ Preferred              | 🚫 Avoid                       |
| ------------- | -------------------- | ------------------------ | ------------------------------ |
| Class         | Model reusable data  | `class Task {}`          | Overengineering                |
| Script Block  | Reusable logic       | `{ param($x) $x + 1 }`   | Complex inline logic           |
| Pipeline      | Stream data          | `process {}`             | Collecting all then outputting |
| Dynamic Param | Conditional behavior | `$PSCmdlet.MyInvocation` | Confusing interfaces           |

---

## References

* [Pester Documentation](https://pester.dev)
* [PowerShell Script Analyzer](https://github.com/PowerShell/PSScriptAnalyzer)
* [Approved Verbs for PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/developer/cmdlet/approved-verbs-for-cmdlets)
* [PowerShell Best Practices and Style Guide](https://poshcode.gitbook.io/powershell-practice-and-style/)
* [Test-Driven Development in PowerShell](https://leanpub.com/pesterbook)
* [PowerShell Classes](https://learn.microsoft.com/en-us/powershell/scripting/developer/help/powershell-classes)

