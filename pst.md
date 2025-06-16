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

 
---

## PowerShell Coding Standards

### PowerShell Coding Standards for Automated Testing  
**Description:** Provide a concise description of the standards purpose & objective.  
**Guidelines:** Outline the specific guidelines, best practices, or requirements related to the standards.  
**Implementation:** Offer guidance on how to implement the standard effectively.  
**Compliance:** Explain how compliance with the standard will be measured or assessed.  
**Environment Considerations:** If the standard is different by environment, include those details.  

| Column 1 | Column 2 | Column 3 | Column 4 |
| -------- | -------- | -------- | -------- |

### Error Handling and Output  
**Description:** Provide a concise description of the standards purpose & objective.  
**Guidelines:** Outline the specific guidelines, best practices, or requirements related to the standards.  
**Implementation:** Offer guidance on how to implement the standard effectively.  
**Compliance:** Explain how compliance with the standard will be measured or assessed.  
**Environment Considerations:** If the standard is different by environment, include those details.  

| Column 1 | Column 2 | Column 3 | Column 4 |
| -------- | -------- | -------- | -------- |

### Advanced PowerShell Language Features  
**Description:** Provide a concise description of the standards purpose & objective.  
**Guidelines:** Outline the specific guidelines, best practices, or requirements related to the standards.  
**Implementation:** Offer guidance on how to implement the standard effectively.  
**Compliance:** Explain how compliance with the standard will be measured or assessed.  
**Environment Considerations:** If the standard is different by environment, include those details.  

| Column 1 | Column 2 | Column 3 | Column 4 |
| -------- | -------- | -------- | -------- |

---

## References
- [Pester Documentation](https://pester.dev)
- [PowerShell Best Practices](https://docs.microsoft.com/en-us/powershell/scripting)
- [Azure DevOps Pipelines](https://learn.microsoft.com/en-us/azure/devops/pipelines/)
- [PowerShell ScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer)
