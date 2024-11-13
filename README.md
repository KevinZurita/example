# Database GoldenPath Deployment Guide

This guide is designed to assist **Database Administrators** in deploying new databases for Azure applications. It provides detailed instructions, standards, and best practices to ensure consistent, secure, and efficient database deployments within our Azure environment. Even if you're new to Azure, Azure DevOps, Git, or Terraform, this guide will walk you through each step of the process.

---

## Table of Contents

1. [Database Deployment Standards](#database-deployment-standards)
   - [Azure Cloud](#azure-cloud)
   - [Azure DevOps](#azure-devops)
   - [Git](#git)
   - [Terraform](#terraform)
   - [Deployment Procedure](#deployment-procedure)
2. [Database Management Standards](#database-management-standards)
   - [Database Scaling](#database-scaling)
   - [Database Deletion](#database-deletion)
   - [Alerts, Monitoring, and Performance Tuning](#alerts-monitoring-and-performance-tuning)
   - [Backups & Restores](#backups-restores)
   - [Security](#security)
   - [Permissions](#permissions)

---

## Database Deployment Standards

### Azure Cloud

**Description:**
Azure Cloud is Microsoft's cloud computing platform that provides a wide range of services, including hosting and managing databases and applications. It allows us to deploy scalable and reliable resources.

**Guidelines:**

- **Regions:** Azure has multiple data center regions worldwide. We primarily deploy databases in the **South Central US** region, identified by the number `2`. Each region has a specific code used in resource naming.

  - **Region Codes:**
    - **North Central US**: `1`
    - **South Central US**: `2` (Primary)
    - **Central US**: `3`
    - **East US 2**: `4`

- **Subscriptions:** Subscriptions are used to manage resources and costs in Azure. We have different subscriptions for each environment:

  - **`sbx`** - Sandbox: For experimentation and learning.
  - **`npd`** - Non-production: For development and testing.
  - **`stg`** - Staging: For pre-production testing, mirroring production.
  - **`prd`** - Production: For live applications and databases.

**Implementation:**

- When deploying resources, ensure you select the correct **region** and **subscription** that correspond to your environment.
- The **region code** is included in resource names to easily identify where they are deployed.

**Environment Considerations:**

- Resources in **staging** (`stg`) should closely replicate the **production** (`prd`) environment to ensure testing is accurate.
- **Sandbox** (`sbx`) and **non-production** (`npd`) environments are for development and should not impact production resources.

---

### Azure DevOps

**Description:**
Azure DevOps is a set of development tools provided by Microsoft that allows for source control, project management, and CI/CD pipelines. It helps teams collaborate on code and automate the deployment process.

**Guidelines:**

- All database deployment code is stored in the **Database Administration** project within Azure DevOps.
- We use specific repositories for each environment to keep code organized:

  - **Sandbox Repository:** `env-dba-sbx-db`
  - **Non-production Repository:** `env-dba-npd-db`
  - **Staging Repository:** `env-dba-stg-db`
  - **Production Repository:** `env-dba-prd-db`

**Implementation:**

- Access Azure DevOps through your web browser using your organizational credentials.
- Navigate to the **Database Administration** project and select the repository corresponding to your environment.

---

### Git

**Description:**
Git is a version control system that tracks changes in files and allows multiple people to collaborate on code. It helps manage code history and coordinate work among team members.

**Guidelines:**

- **Branching Strategy:**

  - Always create a new **branch** from the `main` branch for any changes you make.
  - **Branch Naming Convention:**
    - For new features: `feature/<your-feature-name>`
    - For bug fixes: `bugfix/<issue-description>`
    - Example: `feature/add-new-database`

- **Pull Requests:**

  - After making changes, submit a **pull request** to merge your branch back into `main`.
  - All changes must be reviewed and approved by the **Cloud Operations** team before they are merged.

**Implementation:**

- **Cloning the Repository:**

  - Use Git tools (like Git Bash, Git GUI, or integrated tools in Visual Studio Code) to clone the repository to your local machine.
  - Example command:
    ```
    git clone https://dev.azure.com/YourOrganization/DatabaseAdministration/_git/env-dba-sbx-db
    ```

- **Creating a Branch:**

  - Navigate to your repository directory.
  - Create a new branch:
    ```
    git checkout -b feature/add-new-database
    ```

- **Making Changes:**

  - Edit the necessary files, such as Terraform configurations.
  - Save your changes and commit them with a clear message:
    ```
    git add .
    git commit -m "Added new database for application X"
    ```

- **Pushing and Pull Request:**

  - Push your branch to the remote repository:
    ```
    git push origin feature/add-new-database
    ```
  - In Azure DevOps, create a pull request from your branch to `main`.
  - Add reviewers from the Cloud Operations team.

**Compliance:**

- **Do Not** push changes directly to `main` to prevent unreviewed code from being deployed.
- Ensure that all changes are made through the branching and pull request process for accountability and code quality.

---

### Terraform

**Description:**
Terraform is an open-source infrastructure as code (IaC) tool that allows you to define and provide data center infrastructure using a declarative configuration language. It manages your infrastructure's lifecycle and keeps track of resource dependencies.

**Guidelines:**

- Use the provided **custom Terraform module** for deploying SQL Databases to ensure consistency and compliance with organizational standards.
- Avoid making any changes directly in the Azure portal, as this can lead to configuration drift and inconsistencies.

**Implementation:**

- **Understanding the Terraform Module:**

  - The module simplifies the creation of SQL Databases by encapsulating standard configurations.
  - It includes default settings for monitoring, alerting, and compliance.

- **Module Usage Example:**

  ```hcl
  module "sql_database" {
    source            = "tfe.prd.nm.org/nm/sql-database/azure"
    version           = "1.0.16"
    enable_alert      = true
    environment       = "sbx"
    use_case          = "app"
    db_type           = "webapp"
    action            = "/subscriptions/00000-60600"
    cloudops_tags     = local.cloudops_tags
    sql_server_id     = "/subscriptions/your-subscription-id/resourceGroups/your-resource-group/providers/Microsoft.Sql/servers/your-sql-server"
    rg_name           = "your-resource-group"
    rg_location       = "South Central US"
  }
  ```

- **Key Variables Explained:**

  - `source`: Location of the Terraform module.
  - `version`: The version of the module to use.
  - `enable_alert`: When set to `true`, default alerts are configured.
  - `environment`: Your deployment environment (`sbx`, `npd`, `stg`, `prd`).
  - `use_case`: A short identifier for the database's purpose (e.g., `app`, `web`).
  - `db_type`: Type of the database (e.g., `webapp`).
  - `action`: The Azure Action Group ID for alert notifications.
  - `cloudops_tags`: Tags used for resource management and billing.
  - `sql_server_id`: The resource ID of the SQL Server where the database will reside.
  - `rg_name`: The name of the resource group.
  - `rg_location`: The Azure region where resources are deployed.

**Naming Conventions:**

- **Format:** `nma<RegionNumber>-<UseCase>-<Environment>-sqldb`
  - `nma`: Stands for "Northwestern Medicine Azure".
  - `<RegionNumber>`: The code for the Azure region.
  - `<UseCase>`: A three-letter code identifying the business use.
  - `<Environment>`: Environment identifier (`sbx`, `npd`, `stg`, `prd`).
  - `sqldb`: Indicates that the resource is a SQL Database.

- **Example:**
  - `nma2-app-sbx-sqldb` represents a SQL Database in South Central US (`2`), used for an application (`app`), in the sandbox environment (`sbx`).

**Compliance:**

- Ensure all configurations adhere to the naming conventions and standards.
- Keep your Terraform code updated and store it securely in the repository.

---

### Deployment Procedure

**Description:**
This section outlines the step-by-step process for deploying a new database using the tools and standards mentioned above.

**Guidelines:**

1. **Set Up Access:**

   - Make sure you have the necessary permissions to access Azure DevOps, Git repositories, and Azure subscriptions.
   - If you do not have access, contact the Cloud Operations team to request it.

2. **Prepare Your Local Environment:**

   - Install a code editor (e.g., Visual Studio Code) for editing files.
   - Install Git if it's not already installed.
   - No need to install Terraform locally since deployments are handled via Azure DevOps pipelines.

3. **Clone the Repository:**

   - Open your terminal or Git client.
   - Clone the repository for your environment:
     ```
     git clone https://dev.azure.com/YourOrganization/DatabaseAdministration/_git/env-dba-sbx-db
     ```

4. **Create a New Branch:**

   - Navigate into the repository directory:
     ```
     cd env-dba-sbx-db
     ```
   - Create a new branch for your work:
     ```
     git checkout -b feature/add-new-database
     ```

5. **Modify Terraform Configuration:**

   - Open the Terraform files in your code editor.
   - Add or update the module configuration for your new database.
   - Ensure all required variables are filled out correctly.
   - Follow the naming conventions strictly.

6. **Commit Your Changes:**

   - Save all changes in your code editor.
   - Stage and commit your changes with a clear message:
     ```
     git add .
     git commit -m "Added new database for application X in sandbox environment"
     ```

7. **Push Your Branch and Create a Pull Request:**

   - Push your branch to the remote repository:
     ```
     git push origin feature/add-new-database
     ```
   - In Azure DevOps, navigate to the repository and you should see a prompt to create a pull request.
   - Fill in the pull request details:
     - **Title:** Brief summary of changes.
     - **Description:** Detailed explanation of what you're adding or changing.
     - **Reviewers:** Add the Cloud Operations team or specific members.

8. **Review and Approval:**

   - The Cloud Operations team will review your pull request.
   - They may request changes or approve it as is.
   - Address any feedback by making additional commits to your branch.

9. **Merge and Deployment:**

   - Once approved, the pull request can be merged into `main`.
   - The Azure DevOps pipeline will automatically trigger, executing the Terraform `plan` and `apply` commands.
   - Monitor the pipeline's progress in Azure DevOps to ensure deployment succeeds.

10. **Verification:**

    - After deployment, verify that the database has been created in Azure.
    - Check that all configurations and settings are as expected.

**Compliance:**

- Always use the pull request process to ensure code quality and compliance.
- Do not attempt to run Terraform commands locally; rely on the automated pipeline for consistency and security.
- Document any deviations or special considerations in the pull request description.

---

## Database Management Standards

### Database Scaling

**Description:**
Scaling refers to adjusting the resources allocated to your database to meet performance requirements. This could mean increasing or decreasing compute power or storage based on usage patterns.

**Guidelines:**

- **Performance Optimization First:**
  - Before scaling, investigate if performance issues can be resolved through optimization.
  - Review query performance, indexes, and application code for inefficiencies.

- **Cost Considerations:**
  - Scaling up increases costs. Ensure it's necessary by analyzing performance metrics.
  - Aim for the most cost-effective solution that meets performance needs.

**Implementation:**

- **Adjusting Resources:**

  - Modify the Terraform configuration to change resource settings.
  - Key variables to adjust:
    - `pricing_tier`: Defines the compute size and performance level.
    - `max_size_gb`: Specifies the maximum storage size.

- **Process:**

  1. **Create a New Branch:**
     - For scaling changes, start a new Git branch as before.

  2. **Update Terraform Code:**
     - Edit the variables in the Terraform module to reflect new resource requirements.

  3. **Commit and Push Changes:**
     - Commit your changes with a message explaining why scaling is needed.
     - Push the branch and create a pull request.

  4. **Review and Approval:**
     - The Cloud Operations team will review the proposed changes.
     - Provide any necessary documentation or justification for the scaling.

  5. **Merge and Deployment:**
     - Once approved, merge the pull request.
     - The Azure DevOps pipeline will apply the changes.

**Compliance:**

- Document the reasons for scaling in the pull request.
- Ensure that scaling actions are approved and recorded.

---

### Database Deletion

**Description:**
When a database is no longer needed, it must be deleted carefully to avoid data loss or unintended consequences.

**Guidelines:**

- **Authorization:**
  - Obtain written approval from relevant stakeholders before proceeding.
  - Ensure that the deletion aligns with data retention policies.

- **Data Backup:**
  - Determine if a final backup is required.
  - Store backups securely according to retention guidelines.

- **Terraform Managed Deletion:**
  - Delete databases using Terraform to keep infrastructure state consistent.

**Implementation:**

- **Modify Terraform Configuration:**

  - In your Terraform code, remove or comment out the resource definition for the database.

- **Process:**

  1. **Create a New Branch:**
     - Start a new Git branch for the deletion changes.

  2. **Edit Terraform Code:**
     - Remove the module block that defines the database.

  3. **Commit and Push Changes:**
     - Commit with a message like "Removing database X as per request".

  4. **Create Pull Request:**
     - Explain why the database is being deleted.
     - Attach approval documentation if required.

  5. **Review and Approval:**
     - The Cloud Operations team will review to ensure compliance.

  6. **Merge and Deployment:**
     - Upon approval, merge the pull request.
     - The pipeline will execute and delete the database.

**Compliance:**

- Keep records of approvals and backup confirmations.
- Ensure deletion is compliant with data governance policies.

---

### Alerts, Monitoring, and Performance Tuning

**Description:**
Proactively monitoring databases helps detect and resolve issues before they impact users. Alerts notify the team of potential problems, and performance tuning optimizes database operations.

**Guidelines:**

- **Default Alerts to Configure:**

  - **High Deadlock Count:** Triggers when deadlocks exceed 50.
  - **High Failed Connections:** Triggers when failed connections exceed 50.
  - **High Storage Consumption:** Triggers when storage usage exceeds 90% of capacity.
  - **High Session Count:** Triggers when the average session count exceeds 90.

- **Monitoring Tools:**

  - Use Azure Monitor and Application Insights for tracking metrics.
  - Leverage the built-in configurations in the Terraform module.

**Implementation:**

- **Enable Alerts in Terraform:**

  - Ensure `enable_alert = true` in your module configuration.
  - Define the `action` variable with the appropriate Azure Action Group ID for notifications.

- **Configuring Action Groups:**

  - Action Groups specify who gets notified and how (email, SMS, etc.).
  - Work with the Cloud Operations team to set up or update Action Groups.

- **Performance Tuning:**

  - Regularly review performance metrics.
  - Identify slow queries, missing indexes, or resource bottlenecks.
  - Implement optimizations as needed.

**Compliance:**

- Regularly review and adjust alert thresholds if necessary.
- Document performance tuning activities and their outcomes.

---

### Backups & Restores

**Description:**
Backups ensure that data can be recovered in case of accidental deletion, corruption, or disasters. Regular testing of restore procedures validates the backup's effectiveness.

**Guidelines:**

- **Automated Backups:**

  - Azure SQL Databases have built-in automated backup features.
  - Retention policies should meet organizational requirements.

- **Restore Testing:**

  - Schedule periodic tests to restore databases from backups.
  - Document the procedures and results of these tests.

**Implementation:**

- **Verify Backup Settings:**

  - Check that the database's backup configuration aligns with standards.
  - Adjust retention periods and redundancy options as necessary.

- **Testing Restores:**

  - Use non-production environments to test restore processes.
  - Document each step and any issues encountered.

**Compliance:**

- Maintain logs of backup and restore activities.
- Ensure backup policies comply with regulatory requirements.

---

### Security

**Description:**
Securing databases is critical to protect sensitive information from unauthorized access and breaches.

**Guidelines:**

- **Principle of Least Privilege:**

  - Grant users and applications only the permissions they need.
  - Regularly review and adjust permissions.

- **Access Controls:**

  - Use **Azure Active Directory (AAD)** for authentication when possible.
  - Implement firewalls to restrict access to trusted networks.
  - Enable **Transparent Data Encryption (TDE)** to encrypt data at rest.

**Implementation:**

- **Configure Security Settings in Terraform:**

  - Define network rules and firewall settings.
  - Use variables to set security configurations.

- **Use Azure Key Vault:**

  - Store secrets, such as connection strings or passwords, securely.
  - Reference secrets in your applications without exposing them in code.

**Compliance:**

- Conduct regular security audits.
- Stay updated on Azure security best practices.

---

### Permissions

**Description:**
Proper management of permissions ensures that users have appropriate access while maintaining security.

**Guidelines:**

- **Role-Based Access Control (RBAC):**

  - Assign predefined roles to users based on their job functions.
  - Avoid using shared accounts.

- **Credential Management:**

  - Use managed identities for applications to access databases without storing credentials.
  - Rotate credentials regularly.

**Implementation:**

- **Define Roles and Permissions:**

  - In Terraform, configure database roles and assign users.
  - Use AAD groups to simplify permission management.

- **Integrate with Azure Services:**

  - Use **Managed Service Identities** for applications.
  - Leverage **Azure Policy** to enforce permission standards.

**Compliance:**

- Regularly review access logs.
- Remove access promptly when users change roles or leave the organization.

---

By following this comprehensive guide, even those new to Azure and related tools can successfully deploy and manage databases in compliance with organizational standards. Remember to leverage the support of the Cloud Operations team whenever you have questions or need assistance. Collaboration and adherence to these procedures ensure that our systems remain secure, efficient, and reliable.
