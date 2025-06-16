Gmail	Kevin Zurita <kevinezuritap@gmail.com>
Pester Docs
Zurita, Kevin <kevin.zurita@nm.org>	Mon, Jun 16, 2025 at 4:16 PM
To: Kevin Zurita <kevinezuritap@gmail.com>
# Testing Framework Configuration and Setup

 

 

 

---

 

 

 

## Table of Contents

 

 

 

- [Testing Framework Configuration and Setup](#testing-framework-configuration-and-setup)

 

  - [Table of Contents](#table-of-contents)

 

  - [Overview](#overview)

 

    - [Introduction](#introduction)

 

    - [Definitions](#definitions)

 

    - [Scope](#scope)

 

    - [Value](#value)

 

    - [Stakeholders](#stakeholders)

 

  - [Testing Framework Components \& Configuration](#testing-framework-components--configuration)

 

    - [Testing Framework Components](#testing-framework-components)

 

    - [Framework Configuration](#framework-configuration)

 

    - [Testing Modalities](#testing-modalities)

 

  - [Pester Testing Standards](#pester-testing-standards)

 

    - [Pester Testing Workflow and Syntax](#pester-testing-workflow-and-syntax)

 

  - [Implementation:](#implementation)

 

    - [Authentication](#authentication)

 

    - [Pester Test Structure \& Examples](#pester-test-structure--examples)

 

    - [Functions](#functions)

 

    - [Modules](#modules)

 

    - [Adequate Testing Coverage](#adequate-testing-coverage)

 

    - [New Scripts and Existing Scripts](#new-scripts-and-existing-scripts)

 

  - [PowerShell Coding Standards](#powershell-coding-standards)

 

    - [PowerShell Coding Standards for Automated Testing](#powershell-coding-standards-for-automated-testing)

 

- [Guidelines](#guidelines)

 

    - [Implementation](#implementation-1)

 

    - [Compliance](#compliance)

 

    - [Environment Considerations](#environment-considerations)

 

  - [Error Handling and Output Streams](#error-handling-and-output-streams)

 

    - [**Write-Output:**](#write-output)

 

    - [**Write-Error:**](#write-error)

 

    - [**throw:**](#throw)

 

    - [**Write-Warning:**](#write-warning)

 

    - [**Write-Verbose:**](#write-verbose)

 

    - [**Write-Information:**](#write-information)

 

    - [**Write-Host:**](#write-host)

 

    - [Error Handling Best Practices:](#error-handling-best-practices)

 

    - [Comments and Documentation:](#comments-and-documentation)

 

    - [Streams and Testing](#streams-and-testing)

 

  - [PowerShell Output Streams](#powershell-output-streams)

 

    - [Advanced PowerShell Language Features](#advanced-powershell-language-features)

 

    - [Examples for Each Guideline](#examples-for-each-guideline)

 

 

 

---

 

 

 

## Overview

 

 

 

---

 

 

 

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

 

 

 

---

 

 

 

### Definitions

 

 

 

Include key terms, acronyms, and abbreviations used in the document. Example:

 

 

 

| Term   | Definition                       |

 

| ------ | -------------------------------- |

 

| Term 1 | This is my definition for Term 1 |

 

| Term 2 | This is my definition for Term 2 |

 

 

 

---

 

 

 

### Scope

 

 

 

This standard applies to all PowerShell scripts, modules, and automation maintained or developed by NM Cloud Operations, especially those integrated into Azure DevOps pipelines. It covers all stages of development with this testing framework, CI/CD execution, error handling, test structure, and code organization.

 

 

 

---

 

 

 

### Value

 

 

 

Automated tests are essential for modern software development, providing significant value throughout the development lifecycle:

 

 

 

- **Early Bug Detection & Prevention:** Automated unit and regression tests catch issues early, reducing the cost and effort of fixes and preventing regressions as code evolves.

 

 

 

- **Improved Code Quality & Maintainability:** Test-driven development (TDD) and comprehensive test suites encourage modular, well-structured, and maintainable code, while serving as living documentation for intended behavior.

 

 

 

- **Faster Feedback & Debugging:** Automated tests in CI/CD pipelines provide rapid feedback on code changes, enabling quick identification and resolution of issues, and streamlining debugging.

 

 

 

- **Developer Productivity & Safe Refactoring:** Reliable tests empower developers to make changes and refactor code with confidence, knowing that defects will be caught automatically.

 

 

 

- **Efficiency, Scalability & Cost Savings:** Automation reduces manual testing effort, accelerates delivery, scales with application complexity, and lowers long-term costs by catching issues early.

 

 

 

- **Collaboration & Continuous Improvement:** Shared test suites foster better communication between teams, and test metrics drive ongoing process improvement and resource optimization.

 

 

 

In summary, automated testing is a critical investment that ensures software quality, reliability, and agility at scale.

 

 

 

---

 

 

 

### Stakeholders

 

 

 

- NM Cloud Operations Team

 

 

 

---

 

 

 

## Testing Framework Components & Configuration

 

 

 

---

 

 

 

### Testing Framework Components

 

 

 

**Description:** Provide a concise description of the standards purpose & objective.

 

 

 

**Guidelines:** Outline the specific guidelines, best practices, or requirements related to the standards.

 

 

 

**Implementation:** Offer guidance on how to implement the standard effectively.

 

 

 

**Compliance:** Explain how compliance with the standard will be measured or assessed.

 

 

 

**Environment Considerations:** If the standard is different by environment, include those details.

 

 

 

| Column 1           | Column 2                                                                                    | Column 3 | Column 4 |

 

| ------------------ | ------------------------------------------------------------------------------------------- | -------- | -------- |

 

| Components         | {ADO Library, Agent Pool Dependencies, VS Code, Pipeline and configuration, Introduce Tags} |          |          |

 

| Configurations     | Yaml, linter script, pipeline flags, compute resources, setting secrets, flags.             |          |          |

 

| Testing modalities | Local Testing vs Testing in the Pipeline. VS code extensions. Dot sourcing                  |          |          |

 

 

 

---

 

 

 

### Framework Configuration

 

 

 

**Description:** Provide a concise description of the standards purpose & objective.

 

 

 

**Guidelines:** Outline the specific guidelines, best practices, or requirements related to the standards.

 

 

 

**Implementation:** Offer guidance on how to implement the standard effectively.

 

 

 

**Compliance:** Explain how compliance with the standard will be measured or assessed.

 

 

 

**Environment Considerations:** If the standard is different by environment, include those details.

 

 

 

| Column 1 | Column 2 | Column 3 | Column 4 |

 

| -------- | -------- | -------- | -------- |

 

 

 

---

 

 

 

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

 

 

 

---

 

 

 

### Pester Testing Workflow and Syntax

 

 

 

**Description:** Defines the workflow, syntax, and best practices for writing and organizing Pester tests in PowerShell projects. Covers file placement, naming conventions, test discovery, execution, test file structure, setup/teardown, mocking, and the use of tags for test selection.

 

 

 

**Guidelines:**

 

 

 

- **File Placement & Naming:** Place all test files in a dedicated `Tests` directory or alongside the scripts/modules they test. Name test files with the `.Tests.ps1` suffix (e.g., `MyScript.Tests.ps1`).

 

 

 

- **Discovery & Run:** Pester automatically discovers test files ending with `.Tests.ps1`. Use a consistent structure for test files to enable easy discovery and execution in CI/CD.

 

 

 

- **Test File Structure:** Use `BeforeAll` and `AfterAll` blocks for setup and teardown. Organize tests using `Describe`, `Context`, and `It` blocks for clarity and maintainability.

 

 

 

- **Mocking:** Use `Mock` to simulate dependencies and isolate units of code. Only mock external dependencies or side effects, not the code under test.

 

 

 

- **Tags:** Use tags (e.g., `Unit`, `EndToEnd`, `Integration`, `Quality`) to categorize tests. Tags enable selective test execution in pipelines (see `azure-pipelines.yml` and `pester-tests.yml`).

 

 

 

 **Test Types:**

 

 - **Unit Tests:** Test individual functions or logic, using mocks as needed. Should cover all expected results (throws, outputs, returns).

 

- **EndToEnd Tests:** Validate full script execution, including resource creation and teardown. Use tags like `EndToEnd` for these.

 

 

 

## Implementation:

 

 

 

- Place your test files in the appropriate directory and follow the naming convention.

 

 

 

- Use the following template for structuring your tests:

 

 

 

    ```powershell

 

 

 

    BeforeAll {

 

 

 

        # Setup test variables and secrets

 

 

 

        $testSub    = "<YourSubscription>"

 

 

 

        $testRG     = "<YourResourceGroup>"

 

 

 

        $testServer = "<YourSqlServer>"

 

 

 

        $testDB     = "<YourDatabase>"

 

 

 

        $testOffset = 1

 

 

 

        $SecurePW   = $ServicePrincipalSecret | ConvertTo-SecureString -AsPlainText -Force

 

 

 

        $RunScript = $PSCommandPath.Replace('.Tests.ps1', '.ps1')

 

 

 

        . $RunScript -Sub $testSub -RGName $testRG -SQLServerName $testServer `

 

 

 

            -SourceDatabaseName $testDB -PITR_Hours_Offset $testOffset `

 

 

 

            -Test -PesterTesting -NonInteractive -ServicePrincipalSecret $SecurePW

 

 

 

    }

 

 

 

    Describe "<ScriptUnderTest> | Unit Tests" -Tag "Unit" {

 

 

 

        It "Should fail with a clear error if the resource group does not exist" {

 

 

 

            { . "$PSScriptRoot\<ScriptUnderTest>.ps1" -Sub $testSub -RGName "doesnotexist-rg" `

 

 

 

                -SQLServerName $testServer -SourceDatabaseName $testDB -PITR_Hours_Offset $testOffset `

 

 

 

                -Test -NonInteractive -ServicePrincipalSecret $SecurePW } |

 

 

 

                Should -Throw "ERROR: Resource Group doesnotexist-rg does not exist."

 

 

 

        }

 

 

 

        # Additional unit tests...

 

 

 

    }

 

 

 

    Describe "<ScriptUnderTest> | End-to-End Test" -Tag "EndToEnd" {

 

 

 

        It "Should return the expected output lines or expected error" {

 

 

 

            try {

 

 

 

                $result = . "$PSScriptRoot\<ScriptUnderTest>.ps1" -Sub $testSub -RGName $testRG -SQLServerName $testServer `

 

 

 

                    -SourceDatabaseName $testDB -PITR_Hours_Offset $testOffset -NonInteractive -ServicePrincipalSecret $SecurePW

 

 

 

                $resultString = $result -join "`n"

 

 

 

                $resultString | Should -Match "Expected output line"

 

 

 

            }

 

 

 

            catch {

 

 

 

                $_.Exception.Message | Should -Match "ERROR: .*"

 

 

 

            }

 

 

 

        }

 

 

 

    }

 

 

 

    AfterAll {

 

 

 

        # Cleanup resources created during the tests

 

 

 

        # Remove-Resource -Name "<ResourceName>" -Force -ErrorAction SilentlyContinue

 

 

 

    }

 

 

 

    ```

 

 

 

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

 

 

 

---

 

 

 

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

 

 

 

- Example:

 

 

 

    ```powershell

 

 

 

    BeforeAll {

 

 

 

        # Setup test variables and secrets

 

 

 

        ...

 

 

 

    }

 

 

 

    Describe "<ScriptUnderTest> | Unit Tests" -Tag "Unit" {

 

 

 

        It "Should ..." { ... }

 

 

 

    }

 

 

 

    Describe "<ScriptUnderTest> | End-to-End Test" -Tag "EndToEnd" {

 

 

 

        It "Should ..." { ... }

 

 

 

    }

 

 

 

    AfterAll {

 

 

 

        # Cleanup

 

 

 

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

 

| It        | Individual test case | `It "Should ..." { ... }`    | One per expected result     |

 

| AfterAll  | Cleanup              | Resource deletion            | Runs once after all tests   |

 

 

 

---

 

 

 

### Functions

 

 

 

**Description:** Explains the importance of writing functions in PowerShell scripts, how to write them, and how to import them for testing.

 

 

 

**Guidelines:**

 

 

 

- Write reusable, single-responsibility functions for all logic.

 

 

 

- Use `param` blocks to define inputs and support testability.

 

 

 

- Export functions from modules for easy import and testing.

 

 

 

- Avoid global variables; use local scope within functions.

 

 

 

**Implementation:**

 

 

 

- Refactor scripts into functions and modules where possible.

 

 

 

- Import functions in test files using `Import-Module` or dot-sourcing.

 

 

 

- Example:

 

 

 

    ```powershell

 

 

 

    function Get-Example {

 

 

 

        param([string]$Name)

 

 

 

        if (-not $Name) { throw "Name is required" }

 

 

 

        return "Hello, $Name"

 

 

 

    }

 

 

 

    # In test file:

 

 

 

    . ./MyScript.ps1

 

 

 

    It "Should return greeting" { Get-Example -Name "World" | Should -Be "Hello, World" }

 

 

 

    ```

 

 

 

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

 

 

 

---

 

 

 

### Modules

 

 

 

**Description:** TODO: Describes the benefits of using modules for PowerShell code and testing, and how to structure and import them.

 

 

 

**Guidelines:**

 

 

 

- Organize related functions into modules (`.psm1` files).

 

 

 

- Use modules to encapsulate logic and dependencies.

 

 

 

- Export only public functions; keep helpers private.

 

 

 

- Place module tests in corresponding `.Tests.ps1` files.

 

 

 

**Implementation:**

 

 

 

- Create a module for each major domain or service.

 

 

 

- Use `Import-Module` in test files to load modules for testing.

 

 

 

- Example:

 

 

 

    ```powershell

 

 

 

    # MyModule.psm1

 

 

 

    function Get-Thing { ... }

 

 

 

    Export-ModuleMember -Function Get-Thing

 

 

 

    # MyModule.Tests.ps1

 

 

 

    Import-Module ./MyModule.psm1

 

 

 

    It "Should ..." { Get-Thing | Should -Be ... }

 

 

 

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

 

 

 

---

 

 

 

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

 

 

 

---

 

 

 

### New Scripts and Existing Scripts

 

 

 

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

 

 

 

---

 

 

 

## PowerShell Coding Standards

 

 

 

---

 

 

 

### PowerShell Coding Standards for Automated Testing

 

 

 

---

 

 

 

**Description**

 

 

 

These standards define how to write clear, maintainable, secure, and testable PowerShell code for NM Cloud Operations. The objective is to ensure all scripts and modules are easy to understand, robust, and ready for automation and testing, supporting both local and CI/CD environments.

 

 

 

---

 

 

 

# Guidelines

 

 

 

**Readability & Maintainability:**

 

- Use functions and modules to encapsulate logic. Each function should do one thing well.

 

- Limit variable scope using `param`, `local:`, or within functions. Avoid global variables.

 

- Use 4-space indentation and blank lines to separate logical blocks. Add spaces around operators for clarity.

 

- Use block comments for function headers and inline comments to explain non-obvious logic. Avoid restating code in comments.

 

 

 

**File and Function Organization:**

 

- Start every `.ps1` or `.psm1` file with a comment-based help prolog (`<# ... #>`), including synopsis, description, parameters, and examples.

 

- Place related functions in modules (`.psm1`). Organize files by domain, not type.

 

- Name functions using Verb-Noun (PascalCase), parameters in camelCase, and constants in UPPER_SNAKE_CASE. Use approved PowerShell verbs.

 

 

 

**Error Handling & Testing:**

 

- Use `throw` for terminating errors and `try/catch` for handling exceptions. Set `$ErrorActionPreference = 'Stop'` in automation.

 

- Write Pester tests for every function and script. Use `Describe`, `Context`, and `It` blocks. Use `Mock` to isolate dependencies.

 

- Assert on outputs, side effects, and error handling. Use tags to organize tests (e.g., Unit, EndToEnd, Quality).

 

 

 

**Variables & Expressions:**

 

- Declare one variable per line. Add types if helpful (e.g., `[int]$retryCount = 3`).

 

- Use parentheses for complex logic. Avoid using `$_` outside short pipelines.

 

 

 

**Control Flow:**

 

-  Never rely on implicit scope.

 

 -  Refactor if nesting exceeds two levels.

 

-  Prefer early returns.

 

 

 

**Performance & Portability:**

 

 

 

- Avoid unnecessary `Write-Host`; use `Write-Output` or structured logging. Use `Measure-Command` for profiling. Avoid `Select-Object -First` in tight loops. Design for cross-platform compatibility if using PowerShell Core.

 

 

 

**Directory & File Standards:**

 

- Use `.psm1` for modules, `.ps1` for scripts. Organize by domain (e.g., `/Modules/ResourceGroups/ResourceGroup.psm1`).

 

 

 

---

 

 

 

### Implementation

 

 

 

- Use comment-based help in every script/module for discoverability and documentation.

 

 

 

- Refactor scripts into functions and modules for testability and reuse.

 

 

 

- Use Pester for all testing. Place test files alongside scripts or in a `/Tests` directory, using the `.Tests.ps1` suffix.

 

 

 

- Use `Mock` in Pester to simulate dependencies and isolate units under test.

 

 

 

- Use pipeline variables or secure vaults for secrets in automation. Always support non-interactive authentication for CI/CD.

 

 

 

- Use code analyzers (e.g., `Invoke-ScriptAnalyzer`) to enforce style and best practices.

 

 

 

---

 

 

 

### Compliance

 

 

 

- Code reviews will check for adherence to these standards, including naming, structure, error handling, and test coverage.

 

 

 

- CI/CD pipelines will run Pester and ScriptAnalyzer tests. Failures or warnings must be addressed before merging.

 

 

 

- All new scripts must be fully compliant. Existing scripts should be refactored as time allows, prioritizing high-impact code.

 

 

 

---

 

 

 

### Environment Considerations

 

 

 

- Local development may use interactive authentication and manual testing. CI/CD must use non-interactive authentication and automated tests.

 

 

 

- Use environment-agnostic code and avoid hardcoding environment-specific values. Use parameters and configuration files where possible.

 

 

 

- Ensure cleanup logic in tests to avoid resource leaks in shared or production environments.

 

 

 

---

 

 

 

## Error Handling and Output Streams

 

 

 

---

 

PowerShell provides several output streams for handling different types of messages and errors. Understanding and using these streams appropriately is essential for writing robust, maintainable scripts and for enabling effective testing and automation.

 

 

 

### **Write-Output:**

 

 

 

  - Use for returning data/results from functions and scripts. This is the default output stream and is used for passing objects down the pipeline.

 

 

 

  - Avoid using `Write-Output` for status or error messages; reserve it for actual data your function is designed to return.

 

 

 

  Example:

 

```powershell

 

 

 

    function Get-UserName {

 

 

 

        param([string]$UserId)

 

 

 

        # ... logic ...

 

 

 

        Write-Output $userName

 

 

 

    }

 

 

 

```

 

 

 

### **Write-Error:**

 

 

 

  - Use for non-terminating errors that should be visible to the user or calling process but do not necessarily stop script execution.

 

 

 

  - Supports structured error records and can be caught with `try/catch` if `-ErrorAction Stop` is used.

 

 

 

  Example:

 

 

 

```powershell

 

 

 

    if (-not (Test-Path $file)) {

 

 

 

        Write-Error "File not found: $file"

 

 

 

        return

 

 

 

    }

 

 

 

```

 

 

 

### **throw:**

 

 

 

  - Use for terminating errors that should immediately stop execution and be caught by a `try/catch` block.

 

 

 

  - Use `throw` for critical failures, invalid arguments, or when a function cannot continue.

 

 

 

  Example:

 

 

 

```powershell

 

 

 

    function Remove-ImportantFile {

 

 

 

        param([string]$Path)

 

 

 

        if (-not (Test-Path $Path)) {

 

 

 

            throw "File does not exist: $Path"

 

 

 

        }

 

 

 

        Remove-Item $Path

 

 

 

    }

 

 

 

```

 

 

 

### **Write-Warning:**

 

 

 

  - Use to alert users to potential issues that are not errors but may require attention.

 

 

 

Example:

 

 

 

 ```powershell

 

 

 

    if ($diskSpace -lt 10) {

 

 

 

        Write-Warning "Disk space is low: $diskSpace GB remaining."

 

 

 

    }

 

 

 

```

 

 

 

### **Write-Verbose:**

 

 

 

  - Use for detailed diagnostic output, enabled by the `-Verbose` common parameter.

 

 

 

  Example:

 

 

 

```powershell

 

 

 

    Write-Verbose "Starting backup operation..."

 

 

 

```

 

 

 

### **Write-Information:**

 

 

 

  - Use for informational messages that can be selectively displayed or logged.

 

 

 

  Example:

 

 

 

```powershell

 

 

 

    Write-Information "Backup completed successfully."

 

 

 

```

 

 

 

### **Write-Host:**

 

 

 

  - Avoid in production scripts. Use only for interactive scripts where direct console output is required and not needed for automation or logging.

 

 

 

### Error Handling Best Practices:

 

 

 

- Always validate parameters and inputs at the start of a function. Use `throw` for invalid arguments.

 

 

 

- Use `try/catch` to handle errors from cmdlets or functions that may fail. In the `catch` block, use `Write-Error` or `throw` as appropriate.

 

 

 

- Set `$ErrorActionPreference = 'Stop'` in CI/CD or automation scripts to ensure all errors are caught and handled.

 

 

 

- Provide clear, actionable error messages. Include context such as parameter values or operation details.

 

 

 

- Use custom error types or error records for advanced scenarios.

 

 

 

### Comments and Documentation:

 

 

 

- Use block comments (`<# ... #>`) for file/module headers and function documentation. Include synopsis, description, parameters, and examples.

 

 

 

- Use inline comments (`# ...`) to explain complex logic, assumptions, or non-obvious decisions.

 

 

 

- Avoid restating the code; comments should add value and context.

 

 

 

- Keep comments up to date as code changes.

 

 

 

-Example:

 

 

 

```powershell

 

 

 

  <#

 

 

 

  .SYNOPSIS

 

 

 

  Removes a user from the system.

 

 

 

  .DESCRIPTION

 

 

 

  This function removes a user and all associated resources.

 

 

 

  .PARAMETER UserId

 

 

 

  The ID of the user to remove.

 

 

 

  .EXAMPLE

 

 

 

  Remove-User -UserId 12345

 

 

 

  #>

 

 

 

  function Remove-User {

 

 

 

      param([int]$UserId)

 

 

 

      # Validate input

 

 

 

      if ($UserId -le 0) {

 

 

 

          throw "UserId must be positive."

 

 

 

      }

 

 

 

      # ...

 

 

 

  }

 

 

 

```

 

 

 

### Streams and Testing

 

 

 

- Use the appropriate stream for each type of output to enable precise assertions in Pester tests.

 

 

 

- In tests, use `Should -Throw`, `Should -Be`, and `Should -Match` to assert on errors, outputs, and messages.

 

 

 

- Redirect or capture streams in tests to verify warnings, verbose output, or errors as needed.

 

 

 

- Example:

 

 

 

```powershell

 

 

 

  It "Should write a warning if disk space is low" {

 

 

 

      { Check-DiskSpace -DiskSpace 5 } | Should -ThrowOrWriteWarning "Disk space is low"

 

 

 

  }

 

 

 

```

 

 

 

---

 

 

 

## PowerShell Output Streams

 

PowerShell supports multiple output streams, each with a specific purpose and stream number:

 

 

 

| Stream      | Number | Purpose                     | Cmdlet/Keyword     | When to Use                              |

 

| ----------- | ------ | --------------------------- | ------------------ | ---------------------------------------- |

 

| Output      | 1      | Data/results                | Write-Output       | Return data from functions/scripts       |

 

| Error       | 2      | Non-terminating/terminating | Write-Error, throw | Report or stop on errors                 |

 

| Warning     | 3      | Potential issues            | Write-Warning      | Alert user to non-critical problems      |

 

| Verbose     | 4      | Diagnostic info             | Write-Verbose      | Debugging, detailed process info         |

 

| Debug       | 5      | Debugging info              | Write-Debug        | Step-by-step troubleshooting             |

 

| Information | 6      | Informational messages      | Write-Information  | General info, logging                    |

 

| Host        | N/A    | Console-only output         | Write-Host         | Interactive scripts only (avoid in prod) |

 

 

 

You can redirect or capture these streams using `*>`, `2>`, `3>`, etc. For example, `command 2> error.log` captures errors.

 

Example:

 

```PowerShell

 

  TODO add example here.

 

```

 

---

 

 

 

### Advanced PowerShell Language Features

 

PowerShell offers rich language features to support robust, maintainable, and testable code.

 

 

 

**CmdletBinding and Advanced Functions:**

 

 

 

  - Use `[CmdletBinding()]` to enable common parameters (`-Verbose`, `-ErrorAction`, etc.) and advanced function features.

 

 

 

  Example:

 

 

 

```powershell

 

 

 

    function Get-Example {

 

 

 

        [CmdletBinding()]

 

 

 

        param([Parameter(Mandatory)] [string]$Name)

 

 

 

        Write-Output "Hello, $Name"

 

 

 

    } 

 

```

 

 

 

**Parameter Validation:**

 

 

 

  - Use attributes like `[Parameter(Mandatory)]`, `[ValidateSet()]`, `[ValidateNotNullOrEmpty()]` to enforce input rules.

 

 

 

  Example:

 

 

 

```powershell

 

 

 

    param(

 

 

 

        [Parameter(Mandatory)]

 

 

 

        [ValidateSet('Start','Stop')]

 

 

 

        [string]$Action

 

 

 

    )

 

 

 

```

 

 

 

**Pipeline Support:**

 

 

 

  - Design functions to accept pipeline input using `ValueFromPipeline` and process each item with `process {}`.

 

 

 

  - Example:

 

 

 

```powershell

 

 

 

    function Get-UpperCase {

 

 

 

        [CmdletBinding()]

 

 

 

        param([Parameter(ValueFromPipeline)] [string]$Text)

 

 

 

        process {

 

 

 

            $Text.ToUpper()

 

 

 

        }

 

 

 

    }

 

 

 

    'foo','bar' | Get-UpperCase

 

 

 

```

 

 

 

**Modules and Importing:**

 

 

 

  - Use modules (`.psm1`) to group related functions. Export only public functions.

 

 

 

  - Example:

 

  ```powershell

 

 

 

    # MyModule.psm1

 

 

 

    function Get-Thing { ... }

 

 

 

    Export-ModuleMember -Function Get-Thing

 

 

 

    # Import in script

 

 

 

    Import-Module ./MyModule.psm1

 

 

 

```

 

 

 

**Splatting:**

 

 

 

  - Use splatting to pass parameter sets as a hashtable or array for cleaner code.

 

 

 

 Example:

 

 

 

```powershell

 

 

 

    $params = @{ Path = 'file.txt'; Force = $true }

 

 

 

    Remove-Item @params

 

 

 

```

 

 

 

**ErrorAction and ErrorVariable:**

 

 

 

  - Control error handling at the cmdlet level with `-ErrorAction` and capture errors with `-ErrorVariable`.

 

 

 

  - Example:

 

 

 

```powershell

 

 

 

    Remove-Item 'missing.txt' -ErrorAction SilentlyContinue -ErrorVariable myErr

 

 

 

    if ($myErr) { Write-Warning "File not found." }

 

 

 

```

 

 

 

**Try/Catch/Finally:**

 

 

 

  - Use `try/catch/finally` for robust error handling and cleanup.

 

 

 

  - Example:

 

```powershell

 

 

 

    try {

 

 

 

        # risky operation

 

 

 

    } catch {

 

 

 

        Write-Error $_

 

 

 

    } finally {

 

 

 

        # cleanup

 

 

 

    }

 

 

 

```

 

 

 

**Script and Module Scope:**

 

 

 

  - Use `script:` and `module:` scope modifiers to control variable/function visibility.

 

 

 

  - Example:

 

 

 

```powershell

 

 

 

    $script:counter = 0

 

 

 

    function Increment {

 

 

 

        $script:counter++

 

 

 

    }

 

 

 

```

 

 

 

**Data Files and Configuration:**

 

 

 

  - Use JSON, CSV, or XML files for configuration and data-driven scripts.

 

 

 

  Example:

 

 

 

```powershell

 

 

 

    $config = Get-Content 'config.json' | ConvertFrom-Json

 

 

 

```

 

 

 

**Testing Features:**

 

 

 

  - Use Pester's `Mock`, `Should`, and tagging features for comprehensive, isolated tests.

 

 

 

  - Example:

 

 

 

```powershell

 

 

 

    Mock Get-Date { '2025-01-01' }

 

 

 

    It "Should use mocked date" { (Get-Date) | Should -Be '2025-01-01' }

 

 

 

```

 

 

 

---

 

 

 

### Examples for Each Guideline

 

 

 

**Encapsulation & Scope:**

 

 

 

```powershell

 

 

 

  function Add-Numbers {

 

 

 

      param([int]$A, [int]$B)

 

 

 

      $sum = $A + $B

 

 

 

      return $sum

 

 

 

  }

 

 ```

 

 

 

**Whitespace:**

 

```powershell

 

 

 

  # Good

 

 

 

  $a = 1

 

 

 

  $b = 2

 

 

 

  $sum = $a + $b

 

 

 

 

 

  # Bad

 

 

 

  $a=1;$b=2;$sum=$a+$b

 

 

 

```

 

 

 

**Comments:**

 

 

 

```powershell

 

 

 

  <#

 

 

 

  .SYNOPSIS

 

 

 

  Adds two numbers.

 

 

 

  .DESCRIPTION

 

 

 

  Returns the sum of two integers.

 

 

 

  #>

 

 

 

  function Add-Numbers { ... }

 

 

 

  # Inline comment: Add the numbers

 

 

 

  $sum = $a + $b

 

 

 

```

 

 

 

**Error Handling:**

 

 

 

```powershell

 

 

 

  function Remove-File {

 

 

 

      param([string]$Path)

 

 

 

      if (-not (Test-Path $Path)) {

 

 

 

          Write-Error "File not found: $Path"

 

 

 

          return

 

 

 

      }

 

 

 

      try {

 

 

 

          Remove-Item $Path -ErrorAction Stop

 

 

 

      } catch {

 

 

 

          throw "Failed to remove file: $Path"

 

 

 

      }

 

 

 

  }

 

 

 

```

 

 

 

**Testing:**

 

 

 

```powershell

 

 

 

  # MyScript.ps1

 

 

 

  function Get-Greeting {

 

 

 

      param([string]$Name)

 

 

 

      return "Hello, $Name!"

 

 

 

  }

 

 

 

  # MyScript.Tests.ps1

 

 

 

  . ./MyScript.ps1

 

 

 

  Describe "Get-Greeting" {

 

 

 

      It "Should greet by name" {

 

 

 

          Get-Greeting -Name 'World' | Should -Be 'Hello, World!'

 

 

 

      }

 

 

 

  }

 

 

 

```

 

 

 

**Performance:**

 

 

 

```powershell

 

 

 

  Measure-Command { Get-Process }

 

 

 

  ```

 

 

 

- **Portability:**

 

 

 

  ```powershell

 

 

 

  if ($IsWindows) {

 

 

 

      # Windows-specific logic

 

 

 

  } elseif ($IsLinux) {

 

 

 

      # Linux-specific logic

 

 

 

  }

 

 

 

```

Table of Contents

Overview

Introduction

Definitions

Scope

Value

Stakeholders

Testing Framework Components & Configuration

Testing Framework Components

Framework Configuration

Testing Modalities

Pester Testing Standards

Pester Test Workflow and Syntax

Authentication

Test Structure and Examples

Functions

Modules

Test Coverage

Adding Tests for New and Existing Scripts

PowerShell Coding Standards

PowerShell Coding Standards for Automated Testing

Error Handling and Output

Advanced PowerShell Language Features

References

 

 

 

Kevin Zurita
Cloud Engineer Associate
Digital Operations
Northwestern Memorial Healthcare

541 N. Fairbanks Ct,
Chicago, Illinois 60611
kevin.zurita@nm.org



 


Northwestern Medicine is anchored by Northwestern Memorial Hospital, nationally ranked in 11 specialties and one of only three hospitals in the nation rated high performing in all procedures and conditions by U.S. News & World Report, 2024 – 2025.

This message and any included attachments are intended only for the addressee. The information contained in this message is confidential and may constitute proprietary or non-public information under international, federal, or state laws. Unauthorized forwarding, printing, copying, distribution, or use of such information is strictly prohibited and may be unlawful. If you are not the addressee, please promptly delete this message and notify the sender of the delivery error by email.

		image001.png
3K View Download
Chat

New Conversation

🤓 Explain a complex thing

Explain Artificial Intelligence so that I can explain it to my six-year-old child.


🧠 Get suggestions and create new ideas

Please give me the best 10 travel ideas around the world


💭 Translate, summarize, fix grammar and more…

Translate "I love you" French


GPT-4o Mini
Hello, how can I help you today?
GPT-4o Mini
coin image
10
Upgrade




# Testing Framework Configuration and Setup

 

 

 

---

 

 

 

## Table of Contents

 

 

 

- [Testing Framework Configuration and Setup](#testing-framework-configuration-and-setup)

 

  - [Table of Contents](#table-of-contents)

 

  - [Overview](#overview)

 

    - [Introduction](#introduction)

 

    - [Definitions](#definitions)

 

    - [Scope](#scope)

 

    - [Value](#value)

 

    - [Stakeholders](#stakeholders)

 

  - [Testing Framework Components \& Configuration](#testing-framework-components--configuration)

 

    - [Testing Framework Components](#testing-framework-components)

 

    - [Framework Configuration](#framework-configuration)

 

    - [Testing Modalities](#testing-modalities)

 

  - [Pester Testing Standards](#pester-testing-standards)

 

    - [Pester Testing Workflow and Syntax](#pester-testing-workflow-and-syntax)

 

  - [Implementation:](#implementation)

 

    - [Authentication](#authentication)

 

    - [Pester Test Structure \& Examples](#pester-test-structure--examples)

 

    - [Functions](#functions)

 

    - [Modules](#modules)

 

    - [Adequate Testing Coverage](#adequate-testing-coverage)

 






Powered by AITOPIA 
Chat
Ask
Search
Write
Image
ChatFile
Vision
Full Page
