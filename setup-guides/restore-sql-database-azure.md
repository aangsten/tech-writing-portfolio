# Restoring SQL Database in Azure Portal

## Introduction

This guide describes how to restore a SQL Database using the Azure Portal. It covers selecting the correct subscription and database, performing a restore, configuring the database, and optionally moving the restored database into an elastic pool.

## Prerequisites

- Access to the Azure Portal with permissions to restore databases.
- Knowledge of the production database name (for example `xyz_prod`).

## Restore procedure

1. Sign in to the Azure Portal
   - Open: `https://portal.azure.com/#home`

2. Open SQL Databases
   - From Home, select **SQL Databases**.

3. Change subscription
   - If needed, switch the subscription to **XYZ Production**.

4. Locate the production database
   - Search for the company name (for example: `XYZ`) and open the production database (for example: `xyz_prod`).

5. Start a restore
   - Click **Restore** on the database blade.

6. Set restore point and time adjustments
   - Choose the backup/restore point you need.
   - If the restore time crosses a daylight savings boundary:
     - For fall (clocks back): set the UTC offset to **+6** hours (based on Central Time).
     - For spring (clocks forward): set the UTC offset to **+5** hours (based on Central Time).

7. Name the restored database
   - Remove any timestamp from the suggested name and add a identifying suffix (for example: `_andrew` or `_dr`).

8. Configure compute and storage
   - Service tier: **Standard**
   - DTUs: **400**
   - Backup storage redundancy: **Locally-redundant backup storage**

9. Review and create
   - Click **Review + Create**, verify settings, then **Create**.
   - Wait until deployment completes.

10. Open the restored resource
    - Click **Go to resource** once deployment finishes.

11. (Optional) Copy or rename for data restore workflows
    - From the restored database **Overview**, use **Copy** if you need a separate copy.
    - Append `dr` (or another suffix) to indicate a data-restore copy.

12. Select restore server
    - Example target server: `restoresql01` (East US 2).
    - Confirm backup storage redundancy is set to **Locally-redundant**.

13. Move the database into an elastic pool (optional)
    - Open the server (for example: `restoresql01.database.windows.net`).
    - Under **SQL elastic pool**, select `restoresql01_ep01` → **Configure** → **Databases** → **Add databases**.
    - Check the newly restored database and click **Apply**, then **Save**.

14. Clean up / delete old or test databases (if required)
    - From **SQL Databases**, select the database to delete.
    - Follow the delete confirmation steps:
      - Type your name when prompted.
      - Check the database (for example: `xyz_prod_andrew`) and click **Delete**.
      - Type `delete` to confirm.

These steps provide a comprehensive guide to restoring a SQL database in the Azure Portal, ensuring proper configurations and necessary adjustments are made throughout the process.
