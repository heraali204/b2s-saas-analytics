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

