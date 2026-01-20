# B2B SaaS Analytics Engineering Project

This repository simulates a **real-world analytics engineering workflow** for a B2B SaaS company, covering **sales, billing, and product analytics** across multiple source systems.

The project is designed to demonstrate professional-level skills in:
- SQL transformations
- Dimensional modeling (facts & dimensions)
- Schema alignment across tools
- Handling late-arriving data and backfills
- Managing migrations and refactors
- Analytics documentation and data quality testing

---

## Business Context

The company is a fictional **B2B SaaS platform** with:
- A sales team using **Salesforce**
- A billing system powered by **Stripe**
- Product analytics collected via **Segment**

Stakeholders rely on analytics to answer questions around:
- Revenue growth, churn, and retention
- Sales pipeline health and deal velocity
- Product usage, engagement, and feature adoption
- The relationship between product behavior and revenue

---

## Source Systems

### Salesforce (CRM)
- Accounts
- Contacts
- Opportunities
- Opportunity stage history

Used to model:
- Sales pipeline
- Win rates
- Deal lifecycle and timing

### Stripe (Billing)
- Customers
- Subscriptions
- Invoices
- Invoice line items
- Charges and refunds
- Coupons and plans

Used to model:
- MRR / ARR
- Invoice and payment status
- Discounts and revenue adjustments
- Late payments and backfilled charges

### Segment (Product Analytics)
- Users and account mappings
- Sessions
- Events

Used to model:
- Product engagement
- Feature adoption
- Account-level activity
- Event taxonomy changes and late-arriving events

---

## Data Architecture

This project follows a **modern analytics engineering architecture**:

`Raw Sources → Staging → Intermediate → Marts`

### Raw
- Vendor-extracted data (CSV + SQLite)
- No transformations applied
- Includes imperfect, messy, real-world data

### Staging
- Column renaming and type casting
- Standardized naming conventions
- Source-specific cleanup only

### Intermediate
- Business logic
- Schema alignment across sources
- Canonical event naming
- Subscription and account history models

### Marts
- Analytics-ready fact and dimension tables
- Stable schemas for BI and reporting
- Clear table grain and metric definitions

---

## Project Structure
```md
b2b-analytics-engineering/
├── README.md
├── warehouse/
│   ├── raw_sources.sqlite
│   └── raw_sources_delta.sqlite
├── models/
│   ├── sources/
│   ├── staging/
│   ├── intermediate/
│   └── marts/
│       ├── finance/
│       ├── sales/
│       ├── product/
│       └── dimensions/
├── tests/
├── macros/
├── snapshots/
└── docs/
```

---

## Tools & Technologies Used

This project uses a modern analytics engineering toolset commonly found in production environments.

### Data Storage
- **SQLite**
  - Used to simulate a cloud data warehouse locally
  - Stores raw source data and delta (backfill) batches

### Transformation & Modeling
- **SQL**
  - Primary language for data transformations
  - Used across staging, intermediate, and mart layers
- **dbt-style project structure**
  - Source definitions
  - Staging models
  - Intermediate business logic
  - Analytics marts
  - Tests and documentation

### Version Control
- **Git / GitHub**
  - Project versioning
  - Documentation-first workflow
  - Incremental development and refactors

### Data Quality & Testing
- **Schema tests**
  - Primary key uniqueness
  - Not-null constraints
  - Accepted values
- **Custom business logic tests**
  - Revenue sanity checks
  - Payment and invoice reconciliation

### Documentation
- **YAML-based source documentation**
- **Markdown**
  - Source maps
  - Metric definitions
  - Data dictionary

---

## Key Analytics Concepts Covered

### Dimensional Modeling
- Explicit fact vs dimension separation
- Clearly defined table grain
- Account, customer, user, and plan dimensions

### SQL Transformations
- Multi-source joins
- Deduplication logic
- Time-based aggregations
- Currency normalization

### Schema Alignment
- Event naming consistency across versions
- Unified account identity across Salesforce, Stripe, and Segment

### Backfills
- Late-arriving product events
- Late-arriving invoice payments
- Reconciliation of historical metrics

### Migrations
- Event taxonomy changes
- Subscription plan changes and upgrades
- Forward-compatible modeling patterns

### Refactors
- Separation of concerns between staging, logic, and marts
- Introduction of canonical intermediate models
- Incremental improvements without breaking downstream models

---

## Data Quality & Testing

The project includes:
- Primary key uniqueness tests
- Not-null constraints
- Accepted value tests
- Relationship tests between facts and dimensions
- Custom business logic validations (e.g. revenue non-negativity)

---

## Documentation

Supporting documentation lives in `/docs`, including:
- Source maps
- Metric definitions
- Data dictionary
- Modeling assumptions and known limitations

---
### Optional Extensions (Future Work)
- dbt Core or dbt Cloud
- DuckDB / BigQuery / Snowflake
- BI tools (Looker, Power BI, Tableau)
- Orchestration (Airflow)

---
## Disclaimer

All data in this repository is **synthetic** and generated for learning and demonstration purposes only.  
No real customer or company data is used.

---

## Why This Project Exists

This project is intentionally scoped to reflect **what analytics engineers actually do at work**, rather than toy examples:
- Messy inputs
- Changing schemas
- Business-driven modeling decisions
- Tradeoffs between correctness, performance, and usability
