# Azure Purview / Data Governance Cataloguing Exercise

## Project
**24CC3046-P061 — Azure Purview or Data Governance Cataloguing Exercise**

### Use cases
1. Catalogue and classify data across five sources.
2. Identify sensitive data locations.

### Important
All sample data in this package is synthetic. Do not upload real personal, financial, password, or confidential data into a student/demo environment.

## Suggested five-source design

| Source | Example source type | Demo content |
|---|---|---|
| Source 1 | Azure Blob Storage | customers.csv |
| Source 2 | ADLS Gen2 | employees.csv |
| Source 3 | Azure SQL Database | transactions table |
| Source 4 | Azure Data Explorer | products table |
| Source 5 | Power BI / another supported source | support_tickets data |

If your lab account does not provide one of these source types, use another source supported by your Purview environment and document the substitution.

## Procedure

### 1. Create/open Microsoft Purview
1. Sign in to the Azure portal.
2. Open your Microsoft Purview account.
3. Select **Open Microsoft Purview governance portal**.
4. Go to **Data Map**.

### 2. Create a collection
1. Open **Data Map > Collections**.
2. Create a collection such as `P061-DataGovernance`.
3. Give your team the required Data Source Admin/Data Curator permissions according to your lab instructions.

### 3. Prepare the five sources
Create or identify five supported data sources. For a simple student demo:
- Upload `customers.csv` to Azure Blob Storage.
- Upload `employees.csv` to ADLS Gen2.
- Create an Azure SQL table named `transactions` using `transactions.csv`.
- Create a small Azure Data Explorer table named `products` using `products.csv`.
- Load `support_tickets.csv` into Power BI or another supported source available in your account.

### 4. Register each source
For each source:
1. Go to **Data Map > Data sources**.
2. Select **Register**.
3. Select the source type.
4. Enter the source name/account details.
5. Select the collection.
6. Register the source.

Use names such as:
- `P061-Blob-Customers`
- `P061-ADLS-Employees`
- `P061-AzureSQL-Transactions`
- `P061-ADX-Products`
- `P061-PBI-Support`

### 5. Configure authentication
For each source, create/select an allowed credential.

Preferred option where supported: **Microsoft Purview managed identity**. Other sources may require a service principal, account key, SQL authentication, or another supported authentication method.

If your team cannot obtain credentials, record:
- source name
- credential/authentication required
- who owns the credential
- exact error message
- screenshot of the failed connection test

Do NOT put passwords, keys, or secrets in the Git repository.

### 6. Create and run scans
For each registered source:
1. Select the source in **Data Map**.
2. Select **New scan**.
3. Enter a scan name, for example `P061-Scan-Blob`.
4. Select the required credential.
5. Select the collection.
6. Select **Test connection**.
7. Choose the folders/tables/assets to scan.
8. Select the system/default scan rule set, or create a custom rule set.
9. Enable relevant classifications.
10. Run the scan once for the lab.
11. Wait for the scan to complete.

### 7. Classify sensitive data
After the scan:
1. Open the discovered asset.
2. Review the **Schema/Classifications** information.
3. Record detected sensitive data.
4. If needed, create a custom classification/rule for a business-specific field.
5. Do not blindly accept every automated result; business validation is required.

Example mapping:
- Email → personal/contact information
- Phone → personal/contact information
- Name → person information
- CardLast4 → financial/payment-related information
- Salary → employee/financial information

### 8. Identify sensitive-data locations
Create a table in your report:

| Source | Asset | Sensitive field | Classification | Validation |
|---|---|---|---|---|
| Blob | customers.csv | Email | Personal/contact | Pending/Validated |
| ADLS | employees.csv | WorkEmail | Personal/contact | Pending/Validated |
| Azure SQL | transactions | CardLast4 | Financial/payment | Pending/Validated |
| ADX | products | SupplierEmail | Personal/contact | Pending/Validated |
| Power BI/other | support_tickets | ContactEmail | Personal/contact | Pending/Validated |

Replace the example classifications with the classifications actually returned by your Purview scan.

### 9. Business validation
A student/team member should review the automated classifications:
- Confirm whether the field really contains sensitive information.
- Mark false positives.
- Record the reason for accepting/rejecting a classification.
- Capture a screenshot of the final catalog/asset page.

### 10. Final evidence to submit
Capture screenshots of:
1. Purview account/governance portal.
2. Collection.
3. Five registered sources.
4. Each scan configuration.
5. Successful scan results.
6. Asset/schema metadata.
7. Classification results.
8. Sensitive-data locations.
9. Business validation table.
10. Any credential/connection bottleneck.

## Bottleneck handling

### Problem: Scanning requires credentials
Do not use or request another person's password. Ask the source owner/instructor for the approved credential method. If unavailable, document the blocker and show the registration/configuration screen plus the failed test connection.

### Problem: Classification needs business validation
Automated classification is not the final business decision. Record the detected classification, have the team validate it, and document accepted/rejected results.

### Problem: Network/firewall blocks the scan
Check whether the source is publicly reachable and whether the selected integration runtime is appropriate. For private/network-restricted sources, use the integration runtime/authentication method supported by that source and your lab policy.

## Expected outcome
At the end of the exercise, the Purview Data Map should contain five registered sources, scanned assets/metadata, classification results, and a documented list of locations containing sensitive data.

## Submission structure

```text
P061-Azure-Purview/
├── documentation/
│   ├── PROJECT_PROCEDURE.md
│   ├── FINAL_REPORT_TEMPLATE.md
│   └── EVIDENCE_CHECKLIST.md
├── sample_data/
│   ├── customers.csv
│   ├── employees.csv
│   ├── transactions.csv
│   ├── products.csv
│   └── support_tickets.csv
├── classification/
│   └── classification-mapping.csv
└── architecture/
    └── architecture.mmd
```
