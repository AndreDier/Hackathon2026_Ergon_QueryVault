# QueryVault — Ergon Hackathon Challenge 2026

> **1st Place** — University of Mississippi Hackathon 2026 · Ergon QueryVault Challenge
> 
> A 24-hour hackathon build by a team of 4.

---

## What Is QueryVault?

QueryVault is a Salesforce-native application built for **Ergon**, the challenge sponsor, to solve a real internal pain point: their team was managing a growing library of useful SOQL queries in a spreadsheet, relying on Ctrl+F to find what they needed day to day.

QueryVault replaces that workflow with a clean, searchable, centralized library — built entirely on Salesforce using **Lightning Web Components (LWC)** and **Apex** — where queries can be created, validated, browsed, and reused with a single click.

---

## The Challenge

The hackathon brief asked teams to build a full CRED (Create, Read, Edit, Delete) application on Salesforce that:

- Stored reusable SOQL queries tied to Salesforce objects
- Validated SOQL syntax before saving, with safety guardrails
- Provided a searchable and filterable library UI
- Allowed users to copy queries instantly for reuse
- Was seeded with realistic demo data across multiple Salesforce objects

We had a little less than **24 hours**, and none of us had ever written a line of Apex or LWC before.

---

## The Team

A team of 4 University of Mississippi students — none of us with prior Salesforce development experience. We used AI tools extensively to generate and iterate on code, then worked to integrate everything into a cohesive, functioning application.

My personal role was **integration and debugging** — figuring out how the AI-generated pieces my teammates contributed fit together architecturally, identifying where things were breaking, and patching the gaps to get a working whole.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Platform | Salesforce |
| Frontend | Lightning Web Components (LWC) |
| Backend | Apex (Controllers, SOQL validation) |
| IDE | Agentforce Vibes (Salesforce's AI-assisted IDE) |
| Data Model | Custom Object: `UsefulQuery__c` |
| Deployment | Salesforce Metadata API via IDE |

---

## What We Built

### Data Model
- Custom object `UsefulQuery__c` with fields for Name, Description, SOQL query text, and SObject API Name
- SObject API Name stored as a picklist populated dynamically from Salesforce's Schema — no hardcoded object names

### Library UI (Browse + Search)
- Searchable, filterable datatable listing all saved queries
- Filter by SObject type
- Row actions for viewing, editing, and deleting records

### Query Editor (Create + Edit)
- Form-based editor for creating and updating query records
- All required fields validated before submission
- SObject selection via dynamic dropdown — no freehand API name entry

### SOQL Validation
- Dedicated **Validate** button checks SOQL syntax before a record can be saved
- Validation is guardrailed: enforces a row limit so no unbounded queries can execute
- Clear error messaging surfaced to the user on failure

### Full CRED
- **Create** — New queries added through the LWC editor
- **Read** — View full query details; one-click **Copy** button for reuse
- **Edit** — Modify existing records with re-validation on SOQL or SObject changes
- **Delete** — Confirmation-gated delete to prevent accidental removal

### Seed Data
- 10+ sample `UsefulQuery__c` records spanning multiple objects (Account, Case, Contact, Contract, etc.)
- Loaded via Salesforce Data Import Wizard from the provided Excel template

---

## What We Didn't Complete

- **Permission Sets (S1):** We did not implement the role-based access control requirement (Viewer vs. Editor permission sets) within the 24-hour window. Everything else from the MVP checklist was delivered.

---

## Repository Structure

```
/
├── force-app/
│   └── main/
│       └── default/
│           ├── classes/          # Apex controllers
│           ├── lwc/              # Lightning Web Components
│           └── objects/          # Custom object metadata
├── docs/
│   ├── CHALLENGE.md              # Full challenge brief
│   └── RESOURCES.md              # Salesforce learning resources
└── README.md
```

---

## How to Use the App

### Finding and Copying a Query
1. Open the **QueryVault** app from the Salesforce App Launcher.
2. Use the search bar to find a query by name or description, or filter by SObject.
3. Click the row action menu to show all usable actions per query.
4. Hit the **Copy** button to copy the SOQL text to your clipboard — ready to paste anywhere.

### Creating a New Query
1. Navigate to the top of the page.
2. Fill in Name, Description, SObject (select from the dropdown), and the SOQL query body.
3. Click **Validate** to check your SOQL syntax. Fix any errors surfaced.
4. Once validated, click **Save** to add the query to the library.

### Editing or Deleting a Query
- Use the row action menu on any library entry to **Edit** or **Delete**.
- Delete requires confirmation before the record is removed.

---

## Seed Data

To re-insert the sample records:

1. Open `salesforce_useful_queries.xlsx`
2. In Salesforce: **Setup → Data Import Wizard → Launch Wizard**
3. Select **Custom Objects → UsefulQuery__c** → **Add new records**
4. Upload the file and map columns:
   - Name → `Name`
   - SObjectName → `SObjectAPIName__c`
   - Query → `SOQLField__c`
   - Description → `DescriptionField__c`
5. Click **Start Import**

---

## Reflections

This project was a genuine crash course — 24 hours to learn a new platform, two new languages, a new IDE, and ship something functional for a real sponsor. Leaning on AI to accelerate unfamiliar territory was intentional and effective, but the hardest part wasn't generating code: it was understanding how the pieces fit together well enough to debug what was broken and make confident architectural decisions under time pressure.

We came in **1st place** for the Ergon QueryVault challenge.

---

## Links

- **GitHub Repository:** [https://github.com/AndreDier/Hackathon2026_Ergon_QueryVault](https://github.com/AndreDier/Hackathon2026_Ergon_QueryVault)
- **Salesforce LWC Docs:** [developer.salesforce.com](https://developer.salesforce.com/docs/platform/lightning-component-reference/guide/components.html)
- **Apex Reference:** [Apex Reference Docs](https://developer.salesforce.com/docs/atlas.en-us.apexref.meta/apexref/apex_ref_guide.htm)
