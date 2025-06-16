I can help you enhance the provided document by adding more comprehensive information on getting started with Pester, PowerShell, and automated tests, including better examples with edge cases and more Pester documentation details.

Here's the expanded document:

-----

# Testing Framework Configuration and Setup

## Table of Contents

  - [Overview](https://www.google.com/search?q=%23overview)
      - [Introduction](https://www.google.com/search?q=%23introduction)
      - [Definitions](https://www.google.com/search?q=%23definitions)
      - [Scope](https://www.google.com/search?q=%23scope)
      - [Value](https://www.google.com/search?q=%23value)
      - [Stakeholders](https://www.google.com/search?q=%23stakeholders)
  - [Getting Started with Pester and Automated Testing](https://www.google.com/search?q=%23getting-started-with-pester-and-automated-testing)
      - [Pester Installation and Basic Usage](https://www.google.com/search?q=%23pester-installation-and-basic-usage)
      - [First Pester Test](https://www.google.com/search?q=%23first-pester-test)
      - [Key Pester Concepts Revisited](https://www.google.com/search?q=%23key-pester-concepts-revisited)
  - [Testing Framework Components & Configuration](https://www.google.com/search?q=%23testing-framework-components--configuration)
      - [Testing Framework Components](https://www.google.com/search?q=%23testing-framework-components)
      - [Framework Configuration](https://www.google.com/search?q=%23framework-configuration)
      - [Testing Modalities](https://www.google.com/search?q=%23testing-modalities)
  - [Pester Testing Standards](https://www.google.com/search?q=%23pester-testing-standards)
      - [Pester Test Workflow and Syntax](https://www.google.com/search?q=%23pester-test-workflow-and-syntax)
      - [Common Pester Assertions](https://www.google.com/search?q=%23common-pester-assertions)
      - [Authentication](https://www.google.com/search?q=%23authentication)
      - [Pester Test Structure & Examples](https://www.google.com/search?q=%23pester-test-structure--examples)
      - [Functions in Tests](https://www.google.com/search?q=%23functions-in-tests)
      - [Modules](https://www.google.com/search?q=%23modules)
      - [Adequate Testing Coverage](https://www.google.com/search?q=%23adequate-testing-coverage)
      - [Writing Tests For New Scripts and Existing Scripts](https://www.google.com/search?q=%23writing-tests-for-new-scripts-and-existing-scripts)
  - [Mocking and Integration in Pester](https://www.google.com/search?q=%23mocking-and-integration-in-pester)
      - [Mocking Strategy](https://www.google.com/search?q=%23mocking-strategy)
      - [Integration with CI/CD Pipelines](https://www.google.com/search?q=%23integration-with-cicd-pipelines)
      - [Recommended Folder Layout](https://www.google.com/search?q=%23recommended-folder-layout)
  - [PowerShell Coding Standards](https://www.google.com/search?q=%23powershell-coding-standards)
      - [PowerShell Coding Standards for Automated Testing](https://www.google.com/search?q=%23powershell-coding-standards-for-automated-testing)
      - [Error Handling and Output](https://www.google.com/search?q=%23error-handling-and-output)
      - [Advanced PowerShell Language Features](https://www.google.com/search?q=%23advanced-powershell-language-features)
  - [References](https://www.google.com/search?q=%23references)

-----

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

-----

## Getting Started with Pester and Automated Testing

This section provides a practical guide to installing Pester and writing your first automated tests.

### Pester Installation and Basic Usage

Pester is a behavior-driven development (BDD) based testing framework for PowerShell. It's an essential tool for ensuring the quality and reliability of your PowerShell scripts and modules.

**Installation:**
Pester is available on the PowerShell Gallery and can be easily installed using `Install-Module`. For most environments, installing it for all users is recommended.

```powershell
# To install Pester for the current user
Install-Module -Name Pester -Scope CurrentUser

# To install Pester for all users (requires administrative privileges)
Install-Module -Name Pester -Scope AllUsers
```

**Verification:**
After installation, verify that Pester is correctly installed by checking its version.

```powershell
Get-Module -Name Pester -ListAvailable
```

**Basic Usage:**
The primary cmdlet for running Pester tests is `Invoke-Pester`. By default, `Invoke-Pester` searches for files ending with `.Tests.ps1` in the current directory and its subdirectories.

```powershell
# Run all tests in the current directory and subdirectories
Invoke-Pester

# Run tests in a specific path
Invoke-Pester -Path './MyModule/Tests'

# Run tests with a specific tag (e.g., 'Unit')
Invoke-Pester -Tag 'Unit'

# Run tests in a specific file
Invoke-Pester -Path './MyScript.Tests.ps1'
```

### First Pester Test

Let's create a simple PowerShell function and then write a Pester test for it.

**1. Create a PowerShell Function (e.g., `Calculator.ps1`):**

```powershell
# Calculator.ps1
function Add-Numbers {
    [CmdletBinding()]
    param(
        [Parameter(Mandatory=$true)]
        [int]$Number1,

        [Parameter(Mandatory=$true)]
        [int]$Number2
    )

    Write-Verbose "Adding $Number1 and $Number2"
    return ($Number1 + $Number2)
}

function Subtract-Numbers {
    [CmdletBinding()]
    param(
        [Parameter(Mandatory=$true)]
        [int]$Number1,

        [Parameter(Mandatory=$true)]
        [int]$Number2
    )

    Write-Verbose "Subtracting $Number2 from $Number1"
    return ($Number1 - $Number2)
}
```

**2. Create a Pester Test File (e.g., `Calculator.Tests.ps1`):**

Place this file in a `Tests` directory or alongside `Calculator.ps1`.

```powershell
# Calculator.Tests.ps1
BeforeAll {
    # Dot-source the script to make its functions available in the test session
    . "$PSScriptRoot\Calculator.ps1"
}

Describe 'Add-Numbers Function' -Tag 'Unit' {
    Context 'When adding two positive numbers' {
        It 'should return the correct sum' {
            (Add-Numbers -Number1 5 -Number2 3) | Should -Be 8
        }
    }

    Context 'When adding a positive and a negative number' {
        It 'should return the correct sum' {
            (Add-Numbers -Number1 10 -Number2 -5) | Should -Be 5
        }
    }

    Context 'When passing zero as one of the numbers' {
        It 'should return the other number' {
            (Add-Numbers -Number1 7 -Number2 0) | Should -Be 7
        }
    }

    Context 'When input is invalid (non-integer)' {
        It 'should throw an error' {
            { Add-Numbers -Number1 'abc' -Number2 1 } | Should -Throw
        }
    }

    Context 'When Verbose preference is set' {
        It 'should write verbose output' {
            # Mock Write-Verbose to capture its output
            Mock Write-Verbose { param($Message) $script:VerboseOutput = $Message }
            $script:VerboseOutput = "" # Reset verbose output

            # Set VerbosePreference to Continue for the test to capture verbose output
            Add-Numbers -Number1 1 -Number2 1 -Verbose:$true

            $script:VerboseOutput | Should -Match "Adding 1 and 1"
        }
    }
}

Describe 'Subtract-Numbers Function' -Tag 'Unit' {
    Context 'When subtracting two positive numbers' {
        It 'should return the correct difference' {
            (Subtract-Numbers -Number1 10 -Number2 4) | Should -Be 6
        }
    }

    Context 'When subtracting a larger number from a smaller one' {
        It 'should return a negative result' {
            (Subtract-Numbers -Number1 3 -Number2 7) | Should -Be -4
        }
    }

    Context 'When input is invalid (missing parameter)' {
        It 'should throw a parameter binding error' {
            { Subtract-Numbers -Number1 5 } | Should -Throw -ErrorType 'ParameterBindingException'
        }
    }
}
```

**3. Run the Tests:**

Navigate to the directory containing your `Calculator.ps1` and `Calculator.Tests.ps1` (or their parent directory if `Tests` is a subdirectory) in PowerShell and run:

```powershell
Invoke-Pester
```

You should see output indicating the number of passed and failed tests.

### Key Pester Concepts Revisited

As seen in the first example, Pester tests are structured using a specific vocabulary. Understanding these core concepts is crucial for writing effective tests.

  * **`Describe` block:** This is the top-level container for a group of related tests. It defines a test suite and often represents a function, module, or major feature. You can apply tags to `Describe` blocks for selective execution.

    ```powershell
    Describe 'Feature Name' -Tag 'Category' {
        # ... tests for this feature
    }
    ```

  * **`Context` block (Optional):** Used to group `It` blocks under a specific condition or scenario within a `Describe` block. This helps to make your tests more readable and organized, especially for edge cases.

    ```powershell
    Context 'When condition X is met' {
        # ... tests for this specific condition
    }
    ```

  * **`It` block:** This defines an individual test case, representing a single expectation or assertion. The string after `It` should describe the expected behavior in a clear, concise manner. Each `It` block should contain at least one Pester assertion.

    ```powershell
    It 'should perform action Y correctly' {
        # ... test logic and assertions
    }
    ```

  * **`BeforeAll` and `AfterAll` blocks:**

      * **`BeforeAll`:** Code within this block runs *once* before *all* `Describe` blocks (or `Context` blocks if used at that level) in a given test file. It's ideal for setting up reusable variables, importing modules, or performing one-time setup tasks like creating temporary directories.
      * **`AfterAll`:** Code within this block runs *once* after *all* `Describe` blocks (or `Context` blocks) have completed. It's primarily used for cleanup tasks, such as removing temporary files or disconnecting from services.

    <!-- end list -->

    ```powershell
    BeforeAll {
        # One-time setup
    }

    Describe 'My Feature' {
        # Tests
    }

    AfterAll {
        # One-time cleanup
    }
    ```

  * **`BeforeEach` and `AfterEach` blocks:**

      * **`BeforeEach`:** Code within this block runs *before each* `It` block within its scope. Useful for setting up a clean state for every individual test.
      * **`AfterEach`:** Code within this block runs *after each* `It` block within its scope. Useful for cleaning up resources specific to each test.

    <!-- end list -->

    ```powershell
    Describe 'My Feature' {
        BeforeEach {
            # Setup for each 'It' block
        }

        It 'should do X' { ... }
        It 'should do Y' { ... }

        AfterEach {
            # Cleanup for each 'It' block
        }
    }
    ```

  * **`Mock`:** Pester's `Mock` cmdlet is incredibly powerful for isolating the code under test from its external dependencies. When you `Mock` a command, Pester temporarily replaces the original command with your defined script block for the duration of the mock. This allows you to control the output or behavior of dependencies, preventing side effects and making your tests faster and more reliable.

    ```powershell
    Describe 'Processing user data' {
        It 'should get data from API' {
            # Mock Invoke-RestMethod to prevent actual API call
            Mock Invoke-RestMethod { return @{ Name = 'TestUser'; Id = 123 } }

            $userData = Get-UserData
            $userData.Name | Should -Be 'TestUser'

            # Assert that Invoke-RestMethod was called
            Assert-MockCalled -CommandName Invoke-RestMethod -Times 1
        }
    }
    ```

-----

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

-----

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

    <!-- end list -->

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

    <!-- end list -->

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
    # Set up reusable variables or mocks. This runs once before all tests in this file.
    # E.g., dot-source your script or import your module here.
    . "$PSScriptRoot\..\MyScript.ps1"
}

Describe 'MyFunction' -Tag 'Unit' {
    # BeforeEach and AfterEach can be used here for per-It block setup/cleanup
    BeforeEach {
        # E.g., reset a global variable or create a new mock for each test
    }

    Context 'When called with valid input' {
        It 'should return expected output' {
            MyFunction -Param 'value' | Should -Be 'expected'
        }

        It 'should handle integer input correctly' {
            (MyFunction -Number 10) | Should -Be 20 # Example: if MyFunction doubles the number
        }
    }

    Context 'When called with edge case input' {
        It 'should handle empty string gracefully' {
            (MyFunction -Param '') | Should -Be 'default' # Assuming default behavior
        }

        It 'should handle large numbers without overflow' {
            (MyFunction -Number 1000000) | Should -Be 2000000
        }
    }

    Context 'When input causes an error' {
        It 'should throw a specific error for invalid parameter' {
            { MyFunction -InvalidParam } | Should -Throw -ErrorType 'ParameterBindingException'
        }

        It 'should throw a custom error for business logic failure' {
            Mock Get-ExternalServiceData { throw 'Service Unavailable' }
            { MyFunction -RequiresService } | Should -Throw -Message 'Service Unavailable'
        }
    }

    Context 'When interacting with external systems (mocked)' {
        It 'should call an external API' {
            Mock Invoke-RestMethod { return 'Success' }
            MyFunction -CallApi
            Assert-MockCalled -CommandName Invoke-RestMethod -Times 1
        }

        It 'should log verbose information when -Verbose is used' {
            Mock Write-Verbose { param($Message) $script:VerboseLog += $Message }
            $script:VerboseLog = '' # Reset log for this test
            MyFunction -Verbose
            $script:VerboseLog | Should -Match 'Performing operation'
        }
    }

    AfterEach {
        # E.g., clean up test-specific data
    }
}

AfterAll {
    # Cleanup logic that runs once after all tests in this file.
    # E.g., remove temporary files created by BeforeAll.
}
```

**Compliance:**

  * All scripts must include `.Tests.ps1` files.
  * Every exported function must have test coverage for normal, edge, and error conditions.
  * Tags must be appropriately applied to each `Describe` block.

**Environment Considerations:**

  * Local dev may rely on interactive login.
  * CI/CD must use service principals or managed identity for non-interactive runs.

-----

### Common Pester Assertions

Pester provides a rich set of assertions (using the `Should` keyword) to validate the behavior of your code. Here are some of the most commonly used ones:

| Assertion               | Use Case                                   | Example                                       | Notes                                                                           |
| :---------------------- | :----------------------------------------- | :-------------------------------------------- | :------------------------------------------------------------------------------ |
| `Should -Be`            | Exact value match                          | `5 | Should -Be 5`                                | Simple value assertion for primitives, strings, and objects.                    |
| `Should -BeExactly`     | Case-sensitive and type-sensitive exact match | `'Admin' | Should -BeExactly 'Admin'`                  | Stricter than `-Be`, useful when type or case is critical. Rarely needed for general use. |
| `Should -Match`         | Regex match (for strings)                  | `('Error occurred: 123' | Should -Match 'Error occurred: \d+'` | Powerful for validating log messages, file content, or complex string patterns. |
| `Should -NotMatch`      | Regex does not match                       | `('Success' | Should -NotMatch 'Error')`                 | Ensures a string does *not* contain a specific pattern.                         |
| `Should -Contain`       | Collection contains item                   | `(1, 2, 3 | Should -Contain 2)`                        | Checks if an array, list, or hash table (by key) contains a specified item.    |
| `Should -NotContain`    | Collection does not contain item           | `(1, 2, 3 | Should -NotContain 4)`                     | Ensures a collection does *not* contain a specific item.                        |
| `Should -Throw`         | Error expected                             | `{ Do-Thing -BadInput } | Should -Throw`            | Always wrap the code that is expected to throw an error in a script block. Can be specific about error type/message. |
| `Should -NotThrow`      | No error expected                          | `{ Do-Thing -GoodInput } | Should -NotThrow`         | Ensures a piece of code executes without throwing an unhandled exception.       |
| `Should -BeGreaterThan` | Numeric comparison (greater than)          | `10 | Should -BeGreaterThan 5`                    | Intuitive for counters, limits, or sizes. Also `-BeGreaterThanOrEqual`.       |
| `Should -BeLessThan`    | Numeric comparison (less than)             | `5 | Should -BeLessThan 10`                    | Also `-BeLessThanOrEqual`.                                                      |
| `Should -Exist`         | Path exists                                | `(Test-Path 'C:\temp\myfile.txt') | Should -Exist` | For validating file or directory creation/existence.                           |
| `Should -NotBe`         | Value is not equal                         | `5 | Should -NotBe 10`                         | Opposite of `-Be`.                                                              |
| `Should -BeNull`        | Value is null                              | `($null | Should -BeNull)`                       | Checks if a variable or expression evaluates to `$null`.                        |
| `Should -NotBeNull`     | Value is not null                          | `('value' | Should -NotBeNull)`                | Ensures a variable or expression is not `$null`.                                |
| `Should -BeTrue`        | Value is `$true`                           | `($true | Should -BeTrue)`                       | For boolean checks.                                                             |
| `Should -BeFalse`       | Value is `$false`                          | `($false | Should -BeFalse)`                      | For boolean checks.                                                             |
| `Should -BeEmpty`       | Collection is empty                        | `(@() | Should -BeEmpty)`                        | Checks if an array, string, or collection is empty.                             |
| `Should -HaveCount`     | Collection has specific number of items    | `(1, 2, 3 | Should -HaveCount 3)`              | Useful for verifying the number of returned objects.                            |

-----

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
# Example of non-interactive authentication in a script being tested
# The script should have parameters like -ServicePrincipalId, -ServicePrincipalSecret, -TenantId
function Invoke-MyAzureOperation {
    [CmdletBinding()]
    param(
        [Parameter(Mandatory=$true)]
        [string]$ServicePrincipalId,

        [Parameter(Mandatory=$true)]
        [securestring]$ServicePrincipalSecret,

        [Parameter(Mandatory=$true)]
        [string]$TenantId
    )

    try {
        Write-Verbose "Attempting to connect to Azure via Service Principal..."
        $cred = New-Object System.Management.Automation.PSCredential($ServicePrincipalId, $ServicePrincipalSecret)
        Connect-AzAccount -ServicePrincipal -Tenant $TenantId -Credential $cred -ErrorAction Stop
        Write-Verbose "Successfully connected to Azure."

        # Perform Azure operations
        # ...
    }
    catch {
        Write-Error "Failed to connect or perform Azure operation: $($_.Exception.Message)"
        throw $_.Exception
    }
}

# In your Pester test file (e.g., MyAzureOperation.Tests.ps1)
Describe 'Invoke-MyAzureOperation' -Tag 'Integration' {
    # Use BeforeAll for one-time setup of test credentials
    BeforeAll {
        # For CI/CD, these would come from pipeline variables or Key Vault
        # For local testing, you might load them from a local secure file or environment variables
        $script:TestServicePrincipalId = $env:TEST_SPN_ID
        $script:TestServicePrincipalSecret = ($env:TEST_SPN_SECRET | ConvertTo-SecureString -AsPlainText -Force)
        $script:TestTenantId = $env:TEST_TENANT_ID

        if (-not $script:TestServicePrincipalId) {
            # Provide a way to skip integration tests if credentials are not available
            Write-Warning "Skipping integration tests: Azure Service Principal credentials not found."
            $TestTarget = Get-Pester -Pipeline | Where-Object Path -EQ $PesterInfo.Path
            $TestTarget.Tests | Where-Object Tags -Contains 'Integration' | ForEach-Object { $_.Skip = $true }
        }

        # Dot-source the script containing the function to make it available
        . "$PSScriptRoot\..\MyAzureOperation.ps1"
    }

    Context 'When connecting with valid service principal credentials' {
        It 'should connect to AzAccount successfully' {
            if ($script:TestServicePrincipalId) { # Only run if credentials are present
                # Mock Connect-AzAccount to prevent actual connection during unit tests,
                # or allow it to run for true integration tests if credentials are valid.
                # For a true integration test, you might not mock Connect-AzAccount
                # but ensure you have a dedicated test Azure subscription/resource group.
                Mock Connect-AzAccount {
                    param($ServicePrincipal, $Tenant, $Credential, $ErrorAction)
                    # Simulate successful connection
                    Write-Verbose "Mocked Connect-AzAccount called successfully."
                }

                # Mock any other Azure cmdlets that Invoke-MyAzureOperation calls
                Mock Get-AzResourceGroup { return @{ ResourceGroupName = 'TestRG' } }

                {
                    Invoke-MyAzureOperation `
                        -ServicePrincipalId $script:TestServicePrincipalId `
                        -ServicePrincipalSecret $script:TestServicePrincipalSecret `
                        -TenantId $script:TestTenantId
                } | Should -NotThrow

                Assert-MockCalled -CommandName Connect-AzAccount -Times 1
            }
        }
    }

    Context 'When connecting with invalid service principal credentials' {
        It 'should throw an authentication error' {
            if ($script:TestServicePrincipalId) { # Only run if credentials are present
                Mock Connect-AzAccount {
                    param($ServicePrincipal, $Tenant, $Credential, $ErrorAction)
                    # Simulate authentication failure
                    throw "Authentication failed: Invalid credentials"
                }

                {
                    Invoke-MyAzureOperation `
                        -ServicePrincipalId "invalid-id" `
                        -ServicePrincipalSecret (ConvertTo-SecureString "invalid-secret" -AsPlainText -Force) `
                        -TenantId "invalid-tenant"
                } | Should -Throw -Message 'Authentication failed: Invalid credentials'
            }
        }
    }
}
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

-----

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

**Example: Advanced Test Structure for a `Process-LogFile` Function**

Imagine a function `Process-LogFile` that reads a log file, filters entries, and writes summarized output.

```powershell
# MyLogProcessor.ps1
function Process-LogFile {
    [CmdletBinding(DefaultParameterSetName='Default')]
    param(
        [Parameter(Mandatory=$true, ParameterSetName='Default')]
        [string]$Path,

        [Parameter(Mandatory=$false)]
        [string]$Filter = '*',

        [Parameter(Mandatory=$false)]
        [switch]$ShowErrorsOnly
    )

    Write-Verbose "Processing log file: $Path with filter '$Filter'."
    if (-not (Test-Path $Path)) {
        throw "Log file not found: $Path"
    }

    $logContent = Get-Content -Path $Path

    $filteredContent = $logContent | Where-Object { $_ -like "*$Filter*" }

    if ($ShowErrorsOnly) {
        $filteredContent = $filteredContent | Where-Object { $_ -match 'ERROR|FAILURE' }
    }

    # Simulate parsing and returning structured data
    $results = @()
    foreach ($line in $filteredContent) {
        if ($line -match '^(?<Timestamp>[\d-]+ [\d:]+)\s+\[(?<Level>\w+)\]\s+(?<Message>.*)$') {
            $results += [PSCustomObject]@{
                Timestamp = $Matches.Timestamp
                Level     = $Matches.Level
                Message   = $Matches.Message
            }
        }
    }
    return $results
}
```

```powershell
# MyLogProcessor.Tests.ps1
BeforeAll {
    # Dot-source the function script
    . "$PSScriptRoot\..\MyLogProcessor.ps1"
}

Describe 'Process-LogFile Function' -Tag 'Unit' {
    # Test Setup: Create a temporary log file for each test
    BeforeEach {
        $script:tempLogFilePath = Join-Path (Get-TempPath) "temp_log_$(New-Guid).log"
        $script:logContent = @(
            "2023-01-01 10:00:00 [INFO] User logged in."
            "2023-01-01 10:01:00 [DEBUG] Debug message."
            "2023-01-01 10:02:00 [WARN] Disk space low."
            "2023-01-01 10:03:00 [ERROR] Database connection failed."
            "2023-01-01 10:04:00 [INFO] Report generated."
            "2023-01-01 10:05:00 [ERROR] File access denied."
        )
        $script:logContent | Set-Content -Path $script:tempLogFilePath -Encoding UTF8
    }

    # Test Teardown: Remove the temporary log file after each test
    AfterEach {
        Remove-Item -Path $script:tempLogFilePath -Force -ErrorAction SilentlyContinue
    }

    Context 'When processing a valid log file without filters' {
        It 'should return all log entries' {
            $result = Process-LogFile -Path $script:tempLogFilePath
            $result | Should -HaveCount $script:logContent.Count
            $result[0].Message | Should -Be "User logged in."
        }
    }

    Context 'When filtering by a specific keyword' {
        It 'should return only entries matching the filter' {
            $result = Process-LogFile -Path $script:tempLogFilePath -Filter 'Disk'
            $result | Should -HaveCount 1
            $result[0].Message | Should -Be "Disk space low."
        }

        It 'should be case-insensitive for filters' {
            $result = Process-LogFile -Path $script:tempLogFilePath -Filter 'disk'
            $result | Should -HaveCount 1
            $result[0].Message | Should -Be "Disk space low."
        }
    }

    Context 'When ShowErrorsOnly switch is used' {
        It 'should return only error/failure entries' {
            $result = Process-LogFile -Path $script:tempLogFilePath -ShowErrorsOnly
            $result | Should -HaveCount 2 # Two ERROR entries
            $result[0].Message | Should -Be "Database connection failed."
            $result[1].Message | Should -Be "File access denied."
        }

        It 'should combine with keyword filter if both are used' {
            $result = Process-LogFile -Path $script:tempLogFilePath -ShowErrorsOnly -Filter 'Database'
            $result | Should -HaveCount 1
            $result[0].Message | Should -Be "Database connection failed."
        }
    }

    Context 'When log file does not exist' {
        It 'should throw an error' {
            { Process-LogFile -Path "NonExistentLog.log" } | Should -Throw -Message "Log file not found: NonExistentLog.log"
        }
    }

    Context 'When log file is empty' {
        BeforeEach {
            # Overwrite the temp log file with empty content for this specific context
            "" | Set-Content -Path $script:tempLogFilePath -Encoding UTF8
        }

        It 'should return an empty collection' {
            $result = Process-LogFile -Path $script:tempLogFilePath
            $result | Should -BeEmpty
            $result | Should -HaveCount 0
        }
    }

    Context 'When Get-Content throws an access denied error (mocked)' {
        It 'should propagate the error' {
            # Mock Get-Content to simulate an access denied error
            Mock Get-Content {
                param($Path, $ErrorAction)
                throw [System.UnauthorizedAccessException]"Access denied to $Path"
            }

            { Process-LogFile -Path $script:tempLogFilePath } | Should -Throw -ErrorType 'UnauthorizedAccessException'
        }
    }

    Context 'When verbose logging is enabled' {
        It 'should write verbose output' {
            # Mock Write-Verbose to capture output for assertion
            Mock Write-Verbose { param($Message) $script:VerboseMessages += $Message }
            $script:VerboseMessages = @() # Reset captured messages for this test

            Process-LogFile -Path $script:tempLogFilePath -Verbose

            $script:VerboseMessages | Should -HaveCount 1
            $script:VerboseMessages[0] | Should -Match "Processing log file: .* with filter '\*'."
        }
    }
}

# An example of an Integration Test (hypothetical, as this function doesn't interact externally)
# This would involve actual file system operations beyond just Test-Path/Get-Content,
# or interactions with network resources.
Describe 'Process-LogFile Integration' -Tag 'Integration' {
    # Setup a new, distinct temporary file for integration tests if needed
    BeforeAll {
        $script:integrationLogPath = Join-Path (Get-TempPath) "integration_log_$(New-Guid).log"
        "Line 1" | Add-Content -Path $script:integrationLogPath -Encoding UTF8
    }

    AfterAll {
        Remove-Item -Path $script:integrationLogPath -Force -ErrorAction SilentlyContinue
    }

    Context 'When processing a real file' {
        It 'should read content from a physical file' {
            $result = Process-LogFile -Path $script:integrationLogPath
            $result | Should -HaveCount 1
            $result[0].Message | Should -Be "Line 1"
        }
    }
}
```

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
| Context   | Sub-scenario group   | `Context ...`                | Optional for complex tests  |
| It        | Individual test case | `It "Should ..." { ... }`    | One per expected result     |
| AfterAll  | Cleanup              | Resource deletion            | Runs once after all tests   |

-----

### Functions in Tests

**Description:** Explains the importance of writing functions in PowerShell scripts, how to write them, and how to import them for testing.

**Guidelines:**

  * Write reusable, single-responsibility functions for all logic.
  * Use `param` blocks to define inputs and support testability.
  * Export functions from modules for easy import and testing.
  * Avoid global variables; use local scope within functions.

**Implementation Tips:**

  * **Dot-sourcing:** For individual `.ps1` script files containing functions, use dot-sourcing in your `BeforeAll` block to load the functions into the current Pester session.

    ```powershell
    BeforeAll {
        # Assuming MyFunction.ps1 is in the parent directory of the Tests directory
        . "$PSScriptRoot\..\MyFunction.ps1"
    }
    ```

    This makes the functions defined in `MyFunction.ps1` available directly within your test script.

  * **Importing Modules:** If your functions are part of a PowerShell module (`.psm1` file), import the module. This is the preferred method for larger projects.

    ```powershell
    BeforeAll {
        Import-Module -Name 'MyModuleName' -Force -ErrorAction Stop
        # If the module is not in a PSModulePath, you might need to specify the path:
        # Import-Module -Name "$PSScriptRoot\..\MyModule\MyModuleName.psm1" -Force -ErrorAction Stop
    }
    ```

  * **Injecting Dependencies with `param()`:** Design your functions to accept all necessary inputs and dependencies via parameters. This makes it easy to pass mock data or specific test values during testing, rather than relying on external state.

    ```powershell
    # MyServiceFunction.ps1
    function Get-ServiceStatus {
        [CmdletBinding()]
        param(
            [Parameter(Mandatory=$true)]
            [string]$ServiceName,

            # Inject a function/scriptblock for getting actual service status
            # This allows mocking Test-Service in tests.
            [scriptblock]$TestServiceFunc = { param($Name) (Get-Service -Name $Name -ErrorAction SilentlyContinue).Status }
        )

        Write-Verbose "Checking status of $ServiceName..."
        $status = & $TestServiceFunc -Name $ServiceName

        if ($status -eq 'Running') {
            return 'Online'
        } else {
            return 'Offline'
        }
    }
    ```

    ```powershell
    # MyServiceFunction.Tests.ps1
    BeforeAll { . "$PSScriptRoot\..\MyServiceFunction.ps1" }

    Describe 'Get-ServiceStatus' -Tag 'Unit' {
        Context 'When service is running' {
            It 'should return Online' {
                # Mock the injected TestServiceFunc for this specific test
                $mockTestServiceFunc = { param($Name) 'Running' }
                (Get-ServiceStatus -ServiceName 'MyService' -TestServiceFunc $mockTestServiceFunc) | Should -Be 'Online'
            }
        }

        Context 'When service is stopped' {
            It 'should return Offline' {
                $mockTestServiceFunc = { param($Name) 'Stopped' }
                (Get-ServiceStatus -ServiceName 'AnotherService' -TestServiceFunc $mockTestServiceFunc) | Should -Be 'Offline'
            }
        }

        Context 'When service does not exist' {
            It 'should return Offline (as Test-Service would return $null or error)' {
                $mockTestServiceFunc = { param($Name) $null } # Simulate service not found
                (Get-ServiceStatus -ServiceName 'NonExistentService' -TestServiceFunc $mockTestServiceFunc) | Should -Be 'Offline'
            }
        }
    }
    ```

**Compliance:**

  - All new scripts should be function-based for testability.
  - Code reviews will check for function structure and test coverage.

**Environment Considerations:**

  - Functions should not rely on environment-specific state.
  - Use parameters for all external dependencies.

**Function Test Table:**

| Practice        | Rationale             | Example/Reference      | Notes                           |
| --------------- | --------------------- | ---------------------- | ------------------------------- |
| Function-based  | Testability, reuse    | `function ... { ... }` | Use in all new scripts          |
| Param blocks    | Input validation      | `param([string]$Name)` | Required for test injection     |
| Return values   | Test-friendly results | `return $result`       | Avoid `Write-Host` or `Write-Output` for primary return values that are not part of the pipeline. |
| Imports         | Load target function  | `Import-Module`        | Use module versioning if needed |

-----

### Modules

**Description:** Describes the benefits of using modules for PowerShell code and testing, and how to structure and import them. The best practices for creating modules.

**Guidelines:**

  - Organize related functions into modules (`.psm1` files).
  - Use modules to encapsulate logic and dependencies.
  - Export only public functions; keep helpers private.
  - Place module tests in corresponding `.Tests.ps1` files.

**Implementation:**

  * **Module Structure:** A typical module structure, as outlined in the "Recommended Folder Layout" section, includes:

      * `MyModule.psm1`: The main module file, containing both public and private functions.
      * `MyModule.psd1`: The module manifest, which defines module properties, exported functions, and dependencies.
      * `Public/`: Directory for public functions (exported).
      * `Private/`: Directory for helper functions (not exported).

  * **Exporting Functions:** Use `Export-ModuleMember` in your `.psm1` file to explicitly declare which functions are public and available for import. This improves clarity and prevents unintended access to helper functions.

    ```powershell
    # MyModule.psm1
    # Dot-source all public functions
    . "$PSScriptRoot\Public\Get-PublicFunction.ps1"
    . "$PSScriptRoot\Public\Set-AnotherPublicFunction.ps1"

    # Dot-source all private (helper) functions
    . "$PSScriptRoot\Private\Get-HelperFunction.ps1"

    # Export only the public functions
    Export-ModuleMember -Function 'Get-PublicFunction', 'Set-AnotherPublicFunction'
    ```

  * **Importing for Testing:** In your module's test file, use `Import-Module` to load the module.

    ```powershell
    # MyModule.Tests.ps1
    BeforeAll {
        # Import the module. If it's not in a PSModulePath, provide the full path.
        Import-Module -Name "$PSScriptRoot\..\MyModule\MyModule.psm1" -Force -ErrorAction Stop
    }

    Describe 'Get-PublicFunction' -Tag 'Unit' {
        Context 'When called with valid parameters' {
            It 'should return expected value' {
                (Get-PublicFunction -Param 'Value') | Should -Be 'Expected'
            }
        }
    }

    Describe 'Private Helper Function (Get-HelperFunction)' -Tag 'Unit' {
        # You might need to dot-source private functions directly for testing if not exported
        BeforeAll {
            . "$PSScriptRoot\..\MyModule\Private\Get-HelperFunction.ps1"
        }
        It 'should produce correct intermediate result' {
            (Get-HelperFunction -InternalParam 'Data') | Should -Be 'ProcessedData'
        }
    }
    ```

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

-----

### Adequate Testing Coverage

**Description:** Details the minimum requirements for test coverage, including unit and end-to-end tests, and how to ensure all code paths are tested.

**Requirements:**

  * At least one test for each:
      * Expected success case (valid return value)
      * Expected failure or `throw` condition
      * Expected stream output (e.g., verbose, error, warning, information)
  * For functions with conditional logic (e.g., `if/else`, `switch`), ensure tests cover each branch.
  * For loops (`foreach`, `for`, `while`), ensure tests cover zero iterations, one iteration, and multiple iterations.
  * For functions interacting with external systems, use mocks extensively for unit tests and consider dedicated integration tests for actual interaction.

**Examples:**

```powershell
# Assuming a function: function Convert-StringToInteger { param([string]$Value) ... }

It 'Should convert a valid positive integer string' {
    (Convert-StringToInteger -Value '123') | Should -Be 123
}

It 'Should convert a valid negative integer string' {
    (Convert-StringToInteger -Value '-45') | Should -Be -45
}

It 'Should throw an error for non-integer string input' {
    { Convert-StringToInteger -Value 'abc' } | Should -Throw
}

It 'Should return zero for an empty string input' {
    # Assuming this is the desired behavior for an empty string
    (Convert-StringToInteger -Value '') | Should -Be 0
}

It 'Should write verbose output when -Verbose is specified' {
    Mock Write-Verbose { param($Message) $script:VerboseMessages += $Message }
    $script:VerboseMessages = @()
    Convert-StringToInteger -Value '10' -Verbose
    $script:VerboseMessages | Should -Contain "Converting '10' to integer."
}

It 'Should write a warning if input is too large (edge case)' {
    Mock Write-Warning { param($Message) $script:WarningMessages += $Message }
    $script:WarningMessages = @()
    Convert-StringToInteger -Value '999999999999999999999999999999999' # Value exceeding int type
    $script:WarningMessages | Should -Contain "Input value '9999...' might be too large."
}
```

**Compliance:**

  - Code reviews and CI/CD pipelines will enforce coverage requirements.
  - Test results and coverage reports should be reviewed regularly. While Pester doesn't have built-in line coverage reporting like some other frameworks, the structured guidelines and comprehensive examples here help achieve high functional coverage. Tools like `PesterCoverage` (a community module) can be used for more formal code coverage metrics.

**Environment Considerations:**

  - Tests should be environment-agnostic and not rely on external state.
  - Use mocks and cleanup logic to avoid persistent changes.

**Coverage Table:**

| Requirement       | Rationale                | Test Type   | Example Reference               |
| ----------------- | ------------------------ | ----------- | ------------------------------- |
| Throws on error   | Fail-fast on invalid use | Unit        | `Should -Throw`                 |
| Expected output   | Returns correct result   | Unit        | `Should -Be`, `Should -Contain` |
| Stream validation | Validates logging format | Unit        | `Should -Match 'VERBOSE:'`      |
| Edge cases        | Ensures robustness       | Unit        | Empty input, max/min values     |
| Branch coverage   | Exercises all logic paths| Unit        | `if/else` conditions            |
| Loop iterations   | Tests loop behaviors     | Unit        | Zero, one, many iterations      |

-----

### Writing Tests For New Scripts and Existing Scripts

**Description:** Explains the expectations for new scripts to follow these standards, and guidance for refactoring existing scripts.

**Guidelines:**

  - All new scripts must adhere strictly to these standards from their inception. This includes:
      - Designing for testability (functions, parameters, avoiding global state).
      - Creating comprehensive `.Tests.ps1` files alongside the script/module.
      - Ensuring all public functions have adequate unit test coverage.
      - Applying appropriate Pester tags.
  - Existing scripts in production should be refactored over time to include test coverage. This is often an iterative process:
      - Prioritize high-risk or frequently modified scripts. These are most likely to introduce regressions.
      - Identify critical paths or core logic within legacy scripts and write tests for those first.
      - When modifying an existing script, commit to writing new tests for the changes and adding tests for any previously uncovered areas touched by the modification.
      - Developers have discretion for legacy code but are strongly encouraged to improve testability and structure over time. Even simple "smoke tests" for legacy scripts can provide value.

**Implementation:**

  - Use this standard as a checklist for all new development.
  - Integrate Pester tests into the CI/CD pipeline for new scripts immediately.
  - Plan refactoring of legacy scripts as part of technical debt management. This can be tracked through backlog items, technical debt sprints, or dedicated refactoring tasks.
  - For existing scripts, consider a phased approach:
    1.  **Add basic smoke tests:** Quickly verify primary functionality.
    2.  **Add regression tests:** For any bugs found, write a test that fails with the bug and passes once fixed.
    3.  **Refactor and add unit tests:** Break down monolithic scripts into smaller, testable functions, then add comprehensive unit tests for these new functions.

**Compliance:**

  - New scripts will be reviewed for full compliance with all sections of this document. Any pull request for a new script without corresponding tests following these guidelines will be rejected.
  - Existing scripts should show continuous progress toward compliance over time, as evidenced by increasing test coverage and adherence to coding standards during refactoring efforts. Metrics (e.g., code coverage reports, number of new tests added to legacy code) can be used to track this progress.

**Environment Considerations:**

  - Refactoring should not disrupt production operations. All changes, especially to existing scripts, must be thoroughly tested in non-production environments before deployment.
  - Prioritize test coverage for critical or high-risk scripts that directly impact business operations or are frequently updated.

**Sample Table Formatting:**

| Script Type | Standard Applied     | Example/Reference          | Notes                          |
| ----------- | -------------------- | -------------------------- | ------------------------------ |
| New         | Full compliance      | Follows all sections above | Required for all new scripts   |
| Existing    | Refactor as feasible | Incremental improvements   | Prioritize high-impact scripts |

-----

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
    # Mocking Invoke-RestMethod to simulate an API response without actual network call
    Mock Invoke-RestMethod {
        param($Uri)
        if ($Uri -like "*users*") {
            return @{ Name = 'Test'; Id = 123 }
        } elseif ($Uri -like "*products*") {
            return @{ Product = 'Laptop'; Price = 1200 }
        }
        return $null
    }

    It 'should return a Name property when getting user data' {
        # Assuming Get-DataFromAPI calls Invoke-RestMethod with a URI containing "users"
        (Get-DataFromAPI -Endpoint 'users').Name | Should -Be 'Test'
    }

    It 'should return a Product property when getting product data' {
        # Assuming Get-DataFromAPI calls Invoke-RestMethod with a URI containing "products"
        (Get-DataFromAPI -Endpoint 'products').Product | Should -Be 'Laptop'
    }

    It 'should assert Invoke-RestMethod was called for user data' {
        Get-DataFromAPI -Endpoint 'users'
        Assert-MockCalled -CommandName Invoke-RestMethod -Times 1 -ParameterFilter @{ Uri = '*/users*' }
    }

    It 'should assert Invoke-RestMethod was not called if logic prevents it' {
        # Assuming Get-DataFromAPI has a condition to not call API
        Get-DataFromAPI -Endpoint 'local-data' # This call doesn't trigger API call in the function
        Assert-MockCalled -CommandName Invoke-RestMethod -Times 0
    }
}
```

**🚫 Avoid:**

```powershell
# Avoid mocking core cmdlets like Write-Output unless absolutely necessary for specific stream validation.
# Mocking simple cmdlets can hide underlying issues and make tests brittle.
Mock Write-Output { "forced" }
```

**Implementation Tips:**

  * Mock common cmdlets that interact with external systems: `Start-Job`, `Invoke-RestMethod`, `Get-ChildItem` (for file system), `Get-Service`, `Read-Host`, etc.
  * **Deep Mocks:** For complex scenarios, you might mock deeper, e.g., mocking a specific method of a .NET object if your PowerShell code directly uses .NET classes.
  * **Validating Mock Calls:** Use `Assert-MockCalled` to ensure that your code under test interacts with its dependencies as expected (e.g., how many times a certain command was called, with what parameters). This is crucial for verifying interactions.

-----

### Integration with CI/CD Pipelines

**Goal:** Ensure tests run consistently in build pipelines and failures are surfaced early.

**Implementation Steps:**

1.  **Install Pester in the agent or container:** In your Azure DevOps pipeline definition (e.g., `azure-pipelines.yml`), ensure Pester is installed on the build agent. This can be done via a PowerShell task.

    ```yaml
    - task: PowerShell@2
      displayName: 'Install Pester'
      inputs:
        targetType: 'inline'
        script: |
          Install-Module -Name Pester -Force -Scope CurrentUser -Repository PSGallery
    ```

2.  **Run tests using `Invoke-Pester`:** Execute your tests using `Invoke-Pester`. The `-CI` switch ensures Pester runs in a Continuous Integration friendly mode (e.g., minimal output, no interactive prompts).

    ```powershell
    Invoke-Pester -Path "./Tests" -Output Detailed -CI
    ```

3.  **Export results for reporting:** To visualize test results in Azure DevOps, Pester can export results in various formats, such as NUnitXml or JUnitXml.

    ```powershell
    Invoke-Pester -Path "./Tests" -OutputFormat NUnitXml -OutputFile "TestResults.xml" -CI
    ```

4.  **Publish results in Azure DevOps:** Use the `PublishTestResults@2` task to upload the generated XML report to Azure DevOps, allowing you to see test summaries, individual test results, and track trends over time.

    ```yaml
    - task: PublishTestResults@2
      displayName: 'Publish Test Results'
      inputs:
        testResultsFiles: '**/TestResults.xml' # Path to your Pester test results XML file
        testResultsFormat: 'NUnit' # Or 'JUnit', depending on your Pester output format
        mergeTestResults: true # Merges results from multiple test run files
        testRunTitle: 'Pester Tests'
    ```

**Example Azure DevOps Pipeline Snippet (`azure-pipelines.yml`):**

```yaml
# Starter pipeline for PowerShell project with Pester tests
trigger:
- main

pool:
  vmImage: 'windows-latest' # Or your dedicated Azure Agent Pool

steps:
- task: PowerShell@2
  displayName: 'Install Pester Module'
  inputs:
    targetType: 'inline'
    script: |
      Write-Host "Installing Pester module..."
      Install-Module -Name Pester -Force -Scope CurrentUser -Repository PSGallery
      Write-Host "Pester installation complete."

- task: PowerShell@2
  displayName: 'Run Pester Tests and Generate Report'
  inputs:
    targetType: 'inline'
    script: |
      Write-Host "Running Pester tests..."
      $PesterArgs = @{
          Path        = "$(System.DefaultWorkingDirectory)/Tests" # Adjust path as needed
          OutputFormat= 'NUnitXml'
          OutputFile  = "$(Build.ArtifactStagingDirectory)/TestResults.xml"
          CI          = $true # Enable CI mode for cleaner output
          # Tag         = 'Unit' # Uncomment to run specific tags
      }
      Invoke-Pester @PesterArgs
      Write-Host "Pester test run complete."
    # ContinueOnError: true # Set to true if you want the pipeline to continue even if tests fail

- task: PublishTestResults@2
  displayName: 'Publish Pester Test Results'
  inputs:
    testResultsFiles: '$(Build.ArtifactStagingDirectory)/TestResults.xml'
    testResultsFormat: 'NUnit'
    testRunTitle: 'PowerShell Pester Test Results - $(Build.BuildId)'
    # Always run this task, even if previous tasks fail, to get test results
    condition: succeededOrFailed()
```

-----

### Recommended Folder Layout

A well-structured project layout makes it easier to manage code, tests, and configurations, especially for larger PowerShell projects or modules.

```text
ProjectRoot/
│
├── Modules/                  # Root for all PowerShell modules in this project
│   └── MyModule/             # Specific module directory
│       ├── Public/           # Contains public functions (exported from .psm1)
│       │   └── Get-PublicFunction.ps1
│       ├── Private/          # Contains private (helper) functions (not exported)
│       │   └── Get-PrivateHelper.ps1
│       ├── MyModule.psd1     # Module manifest file
│       └── MyModule.psm1     # Main module script (loads Public/Private functions, defines exports)
│
├── Scripts/                  # Directory for standalone scripts (not part of a module)
│   ├── MyScript.ps1
│   └── UtilityScript.ps1
│
├── Tests/                    # Root for all Pester test files
│   ├── Modules/              # Tests specific to modules
│   │   └── MyModule.Tests.ps1 # Tests for MyModule
│   ├── Scripts/              # Tests specific to standalone scripts
│   │   └── MyScript.Tests.ps1 # Tests for MyScript
│   ├── TestData/             # Optional: Contains test-specific data files (e.g., mock JSON, CSV)
│   │   └── mock-api-response.json
│   └── IntegrationTests.ps1  # Optional: For broader integration or end-to-end tests
│
├── docs/                     # Project documentation
│
├── .vscode/                  # VSCode settings (e.g., recommended extensions, settings.json)
│
├── .gitignore                # Git ignore file
│
└── azure-pipelines.yml       # Azure DevOps pipeline definition
```

-----

## PowerShell Coding Standards

### PowerShell Coding Standards for Automated Testing

**Description:**
This standard defines the structure, practices, and expectations for writing PowerShell code that supports automated testing using Pester. Its objective is to create consistent, maintainable, and testable PowerShell code across all scripts and modules used in CI/CD pipelines and production workloads.

**Guidelines:**

  * **Function-First Design:** Encapsulate all logic in advanced functions with `CmdletBinding()`. Avoid inline script logic, as it's harder to test in isolation.

    **✅ Do:**

    ```powershell
    function Get-UserData {
        [CmdletBinding()]
        param(
            [Parameter(Mandatory=$true)]
            [string]$UserName
        )
        Write-Verbose "Retrieving data for user: $UserName"
        # Simulate data retrieval
        return "Data for $UserName"
    }
    ```

    **🚫 Avoid:**

    ```powershell
    $UserName = 'Kevin'
    # Direct script logic that is hard to isolate and test
    Write-Output "Data for $UserName"
    ```

  * **Single Responsibility Principle:** Each function should perform one specific task. Split complex logic into smaller, testable units. For example, a function that "gets data, processes it, and saves it" should be broken into `Get-Data`, `Process-Data`, and `Save-Data`.

  * **Comment-Based Help:** All public functions must include robust comment-based help blocks with `.`SYNOPSIS` ,  `.`DESCRIPTION`, `.`PARAMETER` , and  `.`EXAMPLE` sections. This is crucial for documentation and usability. Tools like `New-HelpComment` can assist.

  * **Avoid Global State:** Minimize reliance on global (`$global:`) or script (`$script:`) scope variables. Pass necessary data as parameters or return values. This makes functions more predictable and easier to test independently.

  * **Naming Conventions:** Adhere to PowerShell's standard naming conventions:

      * **Functions:** Use PascalCase (e.g., `Get-Report`, `Set-Configuration`) with approved verbs from `Get-Verb`.
      * **Variables:** Use camelCase (e.g., `$userName`, `$outputPath`).
      * **Parameters:** Use PascalCase (e.g., `-ComputerName`, `-Credential`).

  * **Approved Verbs:** Always use cmdlets from the [Approved Verbs for PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/developer/cmdlet/approved-verbs-for-cmdlets). This ensures consistency and predictability across your cmdlets.

  * **Validation Attributes:** Use parameter validation attributes (e.g., `[ValidateNotNullOrEmpty()]`, `[ValidateSet()]`, `[ValidateRange()]`, `[ValidatePattern()]`) to enforce input constraints. This shifts validation logic from the function body to the parameter definition, making the function cleaner and validation implicitly tested by parameter binding.

    ```powershell
    function Set-LogLevel {
        [CmdletBinding()]
        param(
            [Parameter(Mandatory=$true)]
            [ValidateSet('Verbose', 'Information', 'Warning', 'Error', 'None')]
            [string]$Level
        )
        # ... logic
    }
    ```

  * **Modular Structure:** Prefer organizing related functions into PowerShell modules (`.psm1` files) over monolithic scripts. Modules facilitate reuse, encapsulation, and easier testing.

**Implementation:**

  * Adopt a module-based structure with `Public/`, `Private/`, and `Tests/` folders as recommended.

  * Utilize **PSScriptAnalyzer** as a static code analysis tool. Integrate it into your CI/CD pipeline to automatically check for style guide violations, common errors, and best practice adherence.

    ```powershell
    # To run PSScriptAnalyzer locally on your scripts directory
    Invoke-ScriptAnalyzer -Path './Scripts' -Recurse -Settings PSGallery # Uses the default PSGallery rules
    # Or for custom rules:
    # Invoke-ScriptAnalyzer -Path './Scripts' -Recurse -Settings './.PSScriptAnalyzerSettings.psd1'
    ```

**Compliance:**

  * All code must pass **PSScriptAnalyzer** checks with configured rules.
  * All exported functions must have comprehensive unit tests as per the "Adequate Testing Coverage" section.
  * Violations surfaced in pull requests (e.g., by PSScriptAnalyzer or manual review) must be addressed before merging.

**Environment Considerations:**

  * While coding standards should ideally be consistent, some flexibility might be allowed for rapid prototyping in local/development environments. However, strict adherence is mandatory for code committed to version control and deployed via CI/CD.

| Topic           | Standard Requirement | Example/Tool            | Notes                      |
| :-------------- | :------------------- | :---------------------- | :------------------------- |
| Naming          | Verb-Noun            | `Get-Report`            | Use `Get-Verb`             |
| Help Comments   | Required             | `<# .SYNOPSIS ... #>`   | Use `New-HelpComment` tool |
| Script Analyzer | Mandatory            | `Invoke-ScriptAnalyzer` | CI integrated              |
| Structure       | Module-Based         | `Public/Private/Tests`  | Scaffold with `Plaster`    |
| Parameters      | Validation           | `[ValidateNotNullOrEmpty()]`| Improves robustness        |

-----

### Error Handling and Output

**Description:**
Defines how errors and output streams must be handled in PowerShell code to ensure testability, consistency, and clarity in diagnostics.

**Guidelines:**

  * Use `throw` to indicate **terminating errors** (logic errors, invalid state) that you want your script to stop on and that you will explicitly assert in tests.
  * Use `Write-Error` for **non-terminating errors** (runtime issues that might allow continued execution, or for reporting errors in pipeline functions that should not stop the entire pipeline). `Write-Error` writes to the error stream.
  * Use `Write-Verbose` for detailed developer insights during execution, often used for debugging. This stream is typically only shown when `-Verbose` is specified.
  * Use `Write-Warning` to alert non-fatal conditions or potential issues that don't warrant stopping execution.
  * **Avoid `Write-Host`**: This cmdlet writes directly to the console and bypasses all PowerShell output streams, making it untestable and uncapturable by other cmdlets or automated systems. It should be used *only* for specific interactive user prompts or highly transient console messages.
  * Use `Write-Output` when the function is returning data to another command in the pipeline or for Pester assertions that check the function's primary return value.
  * Use `Write-Information` for structured, user-facing runtime logs that can be captured explicitly by `*-Information` cmdlets or within CI/CD systems.

**✅ Do:**

```powershell
function Process-Data {
    [CmdletBinding(SupportsShouldProcess=$true, ConfirmImpact='High')]
    param(
        [Parameter(Mandatory=$true)]
        [string]$DataInput,
        [switch]$SimulateFailure
    )

    if ($SimulateFailure) {
        Write-Error "Simulated failure processing data '$DataInput'." -ErrorId 'SimulatedFailure' -Category 'InvalidOperation'
        # OR for a terminating error:
        # throw "Simulated failure processing data: $DataInput"
        return $false # Or exit, depending on whether it's terminating or non-terminating
    }

    if (-not $DataInput) {
        throw "Input data cannot be null or empty." # Terminating error for invalid input
    }

    if ($PSCmdlet.ShouldProcess("data '$DataInput'", "process")) {
        Write-Verbose "Starting processing for '$DataInput'."
        # ... actual processing ...
        Write-Information "Successfully processed data '$DataInput'." -Tags @('DataProcessing', 'Success')
        return $true
    } else {
        Write-Warning "Operation for '$DataInput' was cancelled by user."
        return $false
    }
}
```

**🚫 Avoid:**

```powershell
function Process-DataBad {
    param($DataInput)
    Write-Host "Processing $DataInput..." # Untestable
    if (-not $DataInput) {
        Write-Host "Error: Input is empty!" # Untestable error
        return
    }
    # ... logic
}
```

**Implementation:**

  * Enable `$ErrorActionPreference = 'Stop'` at the top of your scripts or within specific `try/catch` blocks to ensure that non-terminating errors from cmdlets (like `Get-Item -Path NonExistent`) are elevated to terminating errors, allowing `try/catch` to handle them.

  * **Capturing Streams in Tests:** Pester provides mechanisms to capture output and error streams for assertion.

    ```powershell
    # Example: Asserting on a terminating error (throw)
    It 'Should throw on bad input' {
        { Process-Data -DataInput $null } | Should -Throw -Message "Input data cannot be null or empty."
    }

    # Example: Asserting on a non-terminating error (Write-Error)
    It 'Should write an error when simulating failure' {
        # Redirect the error stream to capture it for assertion
        $errorRecord = (Process-Data -DataInput 'test' -SimulateFailure 2>$null) | Select-Object -ExpandProperty Exception
        $errorRecord.Message | Should -Match "Simulated failure"
        $errorRecord.Category | Should -Be 'InvalidOperation'
    }

    # Example: Asserting on Verbose output
    It 'Should write verbose output when enabled' {
        # Use Pester's built-in stream redirection for verbose
        $verboseOutput = ""
        Measure-Command {
            Process-Data -DataInput 'value' -Verbose 4>&1 | Out-String | ForEach-Object { $verboseOutput += $_ }
        }
        $verboseOutput | Should -Match "Starting processing for 'value'."
    }

    # Example: Asserting on Information stream output
    It 'Should write information output on success' {
        $infoOutput = @()
        Measure-Command {
            Process-Data -DataInput 'success' -InformationAction Continue 6>&1 | Where-Object { $_ -is [System.Management.Automation.InformationRecord] } | ForEach-Object { $infoOutput += $_.MessageData }
        }
        $infoOutput | Should -HaveCount 1
        $infoOutput[0] | Should -Be "Successfully processed data 'success'."
    }
    ```

**Compliance:**

  * All outputs intended for programmatic consumption or logging must be directed to appropriate PowerShell streams and be testable.
  * Misuse of streams (e.g., `Write-Host` for data output) is flagged in code reviews and PSScriptAnalyzer.
  * Logs generated must never leak sensitive information or credentials.

**Environment Considerations:**

  * Verbose and information logs may be disabled by default in production environments unless explicitly enabled for troubleshooting. Configure your logging to respect `$VerbosePreference` and `$InformationPreference`.

| Stream      | Use Case                   | ✅ Use Case Example  | 🚫 Anti-Pattern                |
| :---------- | :------------------------- | :------------------- | :----------------------------- |
| Output      | Primary return values      | `return $result`     | `Write-Host $result`           |
| Error       | Script-breaking conditions | `throw "Error"`      | `Write-Error` for logic errors (when `throw` is more appropriate) |
| Warning     | Alert but continue         | `Write-Warning`      | Using `Write-Error` for non-fatal conditions |
| Verbose     | Developer diagnostics      | `Write-Verbose`      | Hardcoded log messages         |
| Information | Operational logs           | `Write-Information`  | Overusing `Write-Output` for unstructured logging |

-----

### Advanced PowerShell Language Features

**Description:**
Guidance on when and how to apply advanced features like classes, script blocks, dynamic parameters, and streaming logic to make code more testable and modular.

**Guidelines:**

  * **Classes:** Use PowerShell classes (`class MyClass {}`) for internal stateful modeling (e.g., representing complex data structures, job objects, or custom configurations). Avoid overengineering; use classes only when a simple `PSCustomObject` is insufficient, or when you need methods, properties, inheritance, or strong typing for internal objects. Test class behavior via method calls and assert internal state.

    ```powershell
    # Example: Defining a class for a custom log entry
    class LogEntry {
        [string]$Timestamp
        [string]$Level
        [string]$Message

        LogEntry([string]$timestamp, [string]$level, [string]$message) {
            $this.Timestamp = $timestamp
            $this.Level = $level
            $this.Message = $message
        }

        [string]ToString() {
            return "$($this.Timestamp) [$($this.Level)] $($this.Message)"
        }
    }

    # In tests:
    It 'should create a LogEntry object correctly' {
        $entry = [LogEntry]::new("2023-01-01 12:00:00", "INFO", "Test message")
        $entry.Level | Should -Be "INFO"
        $entry.ToString() | Should -Match "\[INFO\] Test message"
    }
    ```

  * **Script Blocks:** Use script blocks (`{ param($x) $x + 1 }`) for deferred logic, callback functions, or when passing code to be executed by another function (e.g., for custom filtering, sorting, or execution contexts like `Invoke-Command`). Avoid overly complex inline blocks; if a script block becomes large or reusable, define it as a named function.

    ```powershell
    function Invoke-CustomAction {
        [CmdletBinding()]
        param(
            [Parameter(Mandatory=$true)]
            [scriptblock]$Action
        )
        Write-Verbose "Executing custom action..."
        & $Action # Execute the script block
    }

    # In tests:
    It 'should execute the provided script block' {
        $mockActionCalled = $false
        $mockAction = { $mockActionCalled = $true }
        Invoke-CustomAction -Action $mockAction
        $mockActionCalled | Should -BeTrue
    }
    ```

  * **Dynamic Parameters:** Use dynamic parameters when a parameter's availability or validation depends on external context (e.g., retrieving valid choices from a service). Avoid when static parameters suffice, as dynamic parameters add complexity to the cmdlet definition and can be harder to discover or test exhaustively.

    ```powershell
    # Example: A dynamic parameter that lists available Azure regions
    function Get-AzureResourceGroupLocation {
        [CmdletBinding()]
        param(
            [Parameter(Mandatory=$true)]
            [string]$ResourceGroupName
        )
        DynamicParam {
            $paramDictionary = [System.Management.Automation.RuntimeDefinedParameterDictionary]::new()
            $parameterAttributes = [System.Management.Automation.Collection`1[System.Attribute]]::new()

            $validateSetAttribute = [System.Management.Automation.ValidateSetAttribute]::new("eastus", "westus", "centralus")
            $parameterAttributes.Add($validateSetAttribute)

            $locationParam = [System.Management.Automation.RuntimeDefinedParameter]::new("Location", [string], $parameterAttributes)
            $paramDictionary.Add("Location", $locationParam)

            return $paramDictionary
        }
        # ... logic that uses $Location
    }

    # In tests: Test expected behavior when -Location is provided
    # Testing discovery of dynamic params is more complex and might involve
    # reflecting on the cmdlet or using integration tests.
    ```

  * **Pipeline Support (`process {}` blocks):** Ensure your functions correctly handle piped input (`ValueFromPipeline` and `ValueFromPipelineByPropertyName`). This makes your functions composable and idiomatic PowerShell. Always process input within the `process {}` block. Avoid collecting all pipeline input in `begin {}` and then processing; stream data through.

    ```powershell
    function Convert-TextToUppercase {
        [CmdletBinding()]
        param(
            [Parameter(ValueFromPipeline=$true)]
            [string]$InputText
        )
        process {
            Write-Output ($InputText.ToUpper())
        }
    }

    # In tests:
    It 'Should convert single piped string to uppercase' {
        ('hello' | Convert-TextToUppercase) | Should -Be 'HELLO'
    }

    It 'Should convert multiple piped strings to uppercase' {
        @('hello', 'world') | Convert-TextToUppercase | Should -Be @('HELLO', 'WORLD')
    }

    It 'Should handle empty piped input' {
        (@() | Convert-TextToUppercase) | Should -BeEmpty
    }
    ```

  * **Closures:** Script blocks can create closures, capturing variables from their enclosing scope. This can be useful for creating parameterized callbacks or functions. Be mindful of variable scope when using closures to avoid unexpected side effects, especially in tests.

**Implementation:**

  * Use `Export-ModuleMember` for precise control over what functions, variables, or aliases are exposed from a module, thus defining its public interface.
  * Test class behavior by instantiating objects, calling methods, and asserting property values.
  * Test pipeline functions comprehensively with various input types: single items, arrays, and actual piped input to ensure correct streaming behavior.

**Compliance:**

  * Any use of advanced language features like dynamic parameters or classes must include clear justification in documentation and be accompanied by robust tests that validate their behavior and error conditions.
  * Streaming functions must correctly work with single objects, arrays, and true pipeline input (e.g., `Get-Item | MyFunction`).

**Environment Considerations:**

  * PowerShell classes are only supported in PowerShell 5.0+ and PowerShell Core/7+. Ensure your target execution environment supports the features you use.
  * Pipeline logic and general PowerShell scripting should work cross-platform and in non-interactive shells for CI/CD compatibility.

| Feature       | Use Case             | ✅ Preferred              | 🚫 Avoid                       |
| :------------ | :------------------- | :------------------------ | :----------------------------- |
| Class         | Model reusable data  | `class Task {}`          | Overengineering for simple data structures |
| Script Block  | Reusable logic       | `{ param($x) $x + 1 }`   | Complex inline logic that should be a named function |
| Pipeline      | Stream data          | `process {}`             | Collecting all then outputting in `end {}` (unless justified for aggregation) |
| Dynamic Param | Conditional behavior | `$PSCmdlet.MyInvocation` | Confusing interfaces or over-use when static params suffice |

-----

## References

  * [Pester Documentation](https://pester.dev)
  * [PowerShell Script Analyzer](https://github.com/PowerShell/PSScriptAnalyzer)
  * [Approved Verbs for PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/developer/cmdlet/approved-verbs-for-cmdlets)
  * [PowerShell Best Practices and Style Guide](https://poshcode.gitbook.io/powershell-practice-and-style/)
  * [Test-Driven Development in PowerShell](https://leanpub.com/pesterbook)
  * [PowerShell Classes](https://learn.microsoft.com/en-us/powershell/scripting/developer/help/powershell-classes)
