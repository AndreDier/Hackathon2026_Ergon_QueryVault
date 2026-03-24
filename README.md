# QueryVault
### University of Mississippi Hackathon 2026 — Ergon Challenge

> A centralized, searchable library of reusable SOQL queries built on Salesforce for Ergon, developed in 24 hours by a team of 4.

---

## About the Hackathon

This project was built during the **University of Mississippi Hackathon 2026**, a 24-hour event in which our team tackled the **Ergon QueryVault Challenge**, sponsored by **Ergon**, a Mississippi-based energy and specialty chemicals company. Our team of four was tasked with solving a real internal pain point: Ergon's developers, admins, and QA engineers had no centralized place to store and reuse their most valuable SOQL queries — they were living in a spreadsheet.

We had no prior experience with Salesforce development, Lightning Web Components (LWC), or Apex going into this challenge.

---

## The Problem

Ergon's team relied on a shared spreadsheet to track frequently used SOQL queries. Finding the right query meant scrolling and using Ctrl+F. There was no validation, no structure, and no easy way to copy and reuse queries safely. The challenge asked us to replace that workflow with a proper application.

---

## Our Solution

We built **QueryVault** — an LWC-based CRED (Create, Read, Edit, Delete) application embedded in Salesforce that allows users to:

- **Browse and search** a library of saved SOQL queries by name, description, or SObject
- **Create and edit** query records with a structured form UI
- **Validate SOQL syntax** before saving, with guardrails to prevent unbounded or harmful query execution
- **Copy queries** to the clipboard with a single button click
- **Delete records** with a confirmation step to prevent accidental loss

All queries are stored in a custom Salesforce object (`UsefulQuery__c`) and surfaced through a Lightning Web Component interface built directly into the Salesforce platform.

---

## Tech Stack

| Technology | Purpose |
|---|---|
| **Salesforce LWC** | Frontend UI components |
| **Apex** | Backend logic, SOQL validation, data operations |
| **AgentForce Vibes IDE** | Salesforce development environment |
| **Salesforce Data Import Wizard** | Seed data loading |
| **GitHub** | Version control and collaboration |

> **Note:** None of our team members had used LWC, Apex, or Salesforce development tools prior to this hackathon. We leveraged AI-assisted development throughout the process and learned these technologies on the fly during the 24-hour window.

---

## Data Model

### `UsefulQuery__c` (Custom Object)

| Field | API Name | Type | Description |
|---|---|---|---|
| Name | `Name` | Text | Human-readable query title |
| SOQL Query | `SOQLField__c` | Long Text Area | The full SOQL query text |
| Description | `DescriptionField__c` | Long Text Area | Usage notes and context |
| SObject API Name | `SObjectAPIName__c` | Picklist | The Salesforce object the query targets |

SObject options were populated dynamically from Salesforce schema — no hardcoded object names.

---

## What We Built (MVP Checklist)

- [x] Custom object `UsefulQuery__c` with all required fields
- [x] LWC library view with search and SObject filtering
- [x] LWC create/edit form with required field validation
- [x] Dynamic SObject selection (no freehand API name entry)
- [x] SOQL syntax validation before save with a dedicated Validate button
- [x] Safety guardrails on validation (row limits enforced)
- [x] Full CRED functionality (Create, Read, Edit, Delete)
- [x] Delete confirmation to prevent accidental deletion
- [x] Copy-to-clipboard button on query view
- [x] 10+ seed data records spanning multiple Salesforce objects
- [x] "How to Use" documentation
- [ ] Permission sets / role-based access control *(not completed within the time limit)*

---

## How to Use

### Finding a Query
1. Open the **QueryVault** app from the Salesforce App Launcher.
2. Browse the query library or use the search bar to filter by name or description.
3. Use the SObject dropdown to narrow results to a specific Salesforce object.
4. Click a query row to open its detail view.

### Copying a Query
- From the detail view, click the **Copy** button to copy the SOQL text to your clipboard.

### Creating a Query
1. Click **New Query** from the library view.
2. Fill in the Name, Description, SObject, and SOQL fields.
3. Click **Validate** to check your SOQL syntax. You must pass validation before saving.
4. Click **Save** to store the record.

### Editing or Deleting a Query
- Use the row action buttons in the library table to **Edit** or **Delete** a record.
- Deletion requires confirmation before the record is removed.

### Validation Notes
- Validation checks SOQL syntax before allowing a save — invalid queries will be rejected with an error message.
- Validation is constrained to a safe row limit to prevent performance issues.
- You cannot save a query until it has been validated successfully.

---

## Seed Data

Sample records are included and can be re-loaded using the Salesforce Data Import Wizard:

1. Open `salesforce_useful_queries.xlsx`
2. Go to **Setup → Data Import Wizard → Launch Wizard**
3. Select **Custom Objects → UsefulQuery__c** → **Add new records**
4. Map columns as follows and start the import:
   - `Name` → Name
   - `Query` → SOQLField__c
   - `Description` → DescriptionField__c
   - `SObjectName` → SObjectAPIName__c

---

## Team

Built by a team of 4 University of Mississippi students in 24 hours at the Ergon Hackathon 2026. We came in with no Salesforce experience and shipped a working application end-to-end.

**Repository:** [github.com/AndreDier/Hackathon2026_Ergon_QueryVault](https://github.com/AndreDier/Hackathon2026_Ergon_QueryVault/blob/main/docs/CHALLENGE.md)

---

## Challenge Reference

The full problem statement is available in [`docs/CHALLENGE.md`](./docs/CHALLENGE.md).

---

*Built with curiosity, caffeine, and a lot of AI-assisted debugging at Ole Miss — 2026.*
