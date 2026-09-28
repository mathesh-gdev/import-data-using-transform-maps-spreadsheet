# Import Data Using Transform Maps (Spreadsheet)

[![Platform: Naan Mudhalvan - SkillWallet](https://img.shields.io/badge/Platform-Naan%20Mudhalvan%20%7C%20SkillWallet-0056D2?style=for-the-badge)](https://skillwallet.naanmudhalvan.tn.gov.in/)
[![Track: ServiceNow System Administrator](https://img.shields.io/badge/Track-ServiceNow%20System%20Administrator-81B5A1?style=for-the-badge&logo=servicenow)](https://www.servicenow.com/)
[![GitHub: Repository](https://img.shields.io/badge/GitHub-Repository-181717?style=for-the-badge&logo=github)](https://github.com/mathesh-gdev/import-data-using-transform-maps-spreadsheet)
[![Progress: 45% (Milestones 1 & 2 Complete)](https://img.shields.io/badge/Progress-45%25%20Completed-2ea44f?style=for-the-badge)](#)
[![Scope: Global](https://img.shields.io/badge/Scope-Global-blueviolet?style=for-the-badge)](#)

---

## 📌 Executive Summary & Project Overview

This repository documents the implementation of the ServiceNow capstone project: **"Import Data using Transform Maps (Spreadsheet)"**, developed under the **Naan Mudhalvan / SkillWallet** ServiceNow System Administrator program.

The project demonstrates automated enterprise data migration into ServiceNow Personal Developer Instance (PDI) using **Import Sets** and **Transform Maps**. This report captures the completed foundation phases (**Milestone 1 & Milestone 2 - 45% Project Progress**), covering source data authoring, target database architecture, staging table ingestion, and field mapping configuration.

---

## 👥 Team Work Breakdown Structure (Current Progress)

| Member | Role | Milestone | SkillWallet Stories | Status |
| :--- | :--- | :--- | :--- | :---: |
| **Daniel Jeewins J** | Schema & System Specialist | **Milestone 1:** Foundation & Target Schema | • Story 1: Creation Of Spreadsheet<br>• Story 2: Creation of Tables | `COMPLETED` ✅ |
| **Vishal K** | Import Set & Mapping Specialist | **Milestone 2:** Staging & Transform Mapping | • Story 3: Create Importset Table<br>• Story 4: Create Transform Map | `COMPLETED` ✅ |
| **Mathesh G** *(Lead)* | Team Lead & Integration Specialist | **Milestone 3:** Execution & Coalesce Testing | • Story 5: Transform Data & Validate<br>• Story 6: Enable Coalesce<br>• Story 7: Inserting New Data | `IN PROGRESS` ⏳ |
| **Manikandan S** | Analytics & Dashboard Specialist | **Milestone 4:** Reporting Suite & Dashboard | • Story 8: Report 1 (3 Analytics Reports)<br>• Story 9: Adding Reports to Dashboard | `UPCOMING` ⏳ |

---

## 🏗️ Architecture Workflow (Milestones 1 & 2)

```mermaid
flowchart LR
    A["Raw Excel Dataset<br/>(Sample Spreadsheet.xlsx)<br/>[10 Employee Records]"] -->|System Import Sets > Load Data| B["Staging Table<br/>[u_employee_import]<br/>(10 Rows Staged / 0 Errors)"]
    B -->|Transform Map Definition<br/>[Sample Spreadsheet Import]| C["Field Mapping Engine<br/>• Auto Map Matching Fields<br/>• Mapping Assist (u_first_name -> u_employee_name)"]
    C -->|Target Schema Ready| D["Custom Target Table<br/>[u_employee_test]<br/>(5 Custom String Attributes)"]
```

---

## 📂 Active Repository Structure

```text
.
├── README.md                           # Project documentation (Milestones 1 & 2 complete)
├── .gitignore                          # Clean ignore rules for temporary & OS files
├── ServiceNow_Transform_Maps_Project_Playbook.docx # Official project playbook & team guide
├── dataset/
│   ├── Sample Spreadsheet.xlsx         # Milestone 1 baseline dataset (10 employee records)
│   └── Updated_Sample_Spreadsheet.xlsx # Milestone 3 stress-test dataset (ready for next phase)
└── screenshots/
    ├── 01_custom_table_schema.png      # Milestone 1: Target table schema (u_employee_test)
    ├── 02_form_layout_fields.png       # Milestone 1: Form view layout configuration
    ├── 03_load_data_import_set.png     # Milestone 2: Staging table creation & loaded rows
    └── 04_transform_map_field_mapping.png # Milestone 2: Transform Map & field mapping
```

---

## 📑 Completed Milestone Implementations

### Milestone 1: Foundation & Target Schema
**Owner:** `Daniel Jeewins J` | **SkillWallet Stories:** `Creation Of Spreadsheet`, `Creation of Tables`

#### 1. Baseline Dataset Construction (`Sample Spreadsheet.xlsx`)
- Created [`dataset/Sample Spreadsheet.xlsx`](dataset/Sample%20Spreadsheet.xlsx) with 10 structured employee records.
- Standardized header row: `Employee ID` | `First Name` | `Last Name` | `Email` | `Department` | `Location`.

#### 2. Target Table Architecture (`u_employee_test`)
- **Navigation:** System Definition > Tables (`sys_db_object.list`) > New.
- **Table Label:** `Employee Test`
- **Table Name:** `u_employee_test`
- **Application Scope:** Global (`global`)
- Created 5 custom columns in the table dictionary:

| Column Label | Column Name | Data Type | Max Length | Mandatory | System Purpose |
| :--- | :--- | :--- | :---: | :---: | :--- |
| **Employee ID** | `u_employee_id` | String | 40 | Yes | Unique corporate employee identifier |
| **Employee Name** | `u_employee_name` | String | 100 | Yes | Full employee display name |
| **Email** | `u_email` | String | 100 | No | Corporate communication address |
| **Department** | `u_department` | String | 100 | No | Operational business unit |
| **Location** | `u_location` | String | 100 | No | Primary office branch location |

![Target Table Schema](screenshots/01_custom_table_schema.png)
*Figure 1.1: Target table dictionary schema showing all 5 custom string columns.*

#### 3. Form Design & Layout Configuration
- Custom form layout configured via **Configure > Form Design** on `u_employee_test`.
- Positioned primary identifiers (`Employee ID`, `Employee Name`) at the top, followed by `Email`, `Department`, and `Location` in a structured dual-column format.

![Form Layout](screenshots/02_form_layout_fields.png)
*Figure 1.2: Form view layout displaying all 5 custom attributes on the main form view.*

---

### Milestone 2: Staging Table & Transform Mapping
**Owner:** `Vishal K` | **SkillWallet Stories:** `Create Importset Table`, `Create Transform Map`

#### 1. Import Set Ingestion (`u_employee_import`)
- **Navigation:** System Import Sets > Load Data.
- Uploaded [`dataset/Sample Spreadsheet.xlsx`](dataset/Sample%20Spreadsheet.xlsx) to create a new staging table:
  - **Staging Table Label:** `Employee Import`
  - **Staging Table Name:** `u_employee_import`
  - **Header Row:** 1 | **Sheet Number:** 1
- **Ingestion Result:** 10 records loaded into the staging table with 0 errors.

![Load Data Completion](screenshots/03_load_data_import_set.png)
*Figure 2.1: Load Data confirmation displaying 10 records loaded into staging table u_employee_import.*

#### 2. Transform Map Configuration (`Sample Spreadsheet Import`)
- **Navigation:** System Import Sets > Administration > Transform Maps > New.
- **Transform Map Name:** `Sample Spreadsheet Import`
- **Source Table:** `Employee Import` [`u_employee_import`]
- **Target Table:** `Employee Test` [`u_employee_test`]
- **Field Mapping Methodology:**
  - Automated matching generated via **Auto Map Matching Fields**.
  - Reconciled field name divergence using **Mapping Assist** to bridge source `u_first_name` directly to target `u_employee_name`.

| # | Source Field (`u_employee_import`) | Target Field (`u_employee_test`) | Mapping Method | Initial Coalesce |
| :-: | :--- | :--- | :--- | :-: |
| 1 | `u_employee_id` | `u_employee_id` | Auto Map Matching Fields | False |
| 2 | `u_first_name` | `u_employee_name` | Mapping Assist | False |
| 3 | `u_email` | `u_email` | Auto Map Matching Fields | False |
| 4 | `u_department` | `u_department` | Auto Map Matching Fields | False |
| 5 | `u_location` | `u_location` | Auto Map Matching Fields | False |

![Field Mapping Configuration](screenshots/04_transform_map_field_mapping.png)
*Figure 2.2: Field Maps list displaying complete field relationship definitions.*

---

## ⏳ Upcoming Milestones (Roadmap)

- **Milestone 3 (Mathesh G - Lead):**
  - Execute initial transform into `u_employee_test` (10 inserts).
  - Enable `Coalesce = true` on `u_employee_id`.
  - Ingest [`dataset/Updated_Sample_Spreadsheet.xlsx`](dataset/Updated_Sample_Spreadsheet.xlsx) to validate 2 inserts, 2 updates, and idempotency (4 ignored).
- **Milestone 4 (Manikandan S):**
  - Build 3 analytics reports (Department Pie Chart, Location Bar Chart, List Report).
  - Embed reports on executive dashboard `Employee Analytics Dashboards`.

---

## 🔗 Project Resources & References

| Resource | Link |
| :--- | :--- |
| 💻 **GitHub Repository** | [mathesh-gdev/import-data-using-transform-maps-spreadsheet](https://github.com/mathesh-gdev/import-data-using-transform-maps-spreadsheet) |
| 📊 **Source Dataset (v1)** | [dataset/Sample Spreadsheet.xlsx](dataset/Sample%20Spreadsheet.xlsx) |
| 📘 **Project Playbook Guide** | [ServiceNow_Transform_Maps_Project_Playbook.docx](ServiceNow_Transform_Maps_Project_Playbook.docx) |

---
*Created for the **Naan Mudhalvan - SkillWallet** Initiative \| ServiceNow System Administrator Track*
