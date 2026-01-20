# Source Map

## Salesforce (CRM)

### Tables

#### salesforce_account
- Description: Represents an organization/company record in Salesforce CRM. This table is the CRM “account” entity used to group contacts and opportunities, and it may include both active customers and non-customer prospects depending on how the business uses Salesforce.
- Primary key:`Id`
- Important timestamps: CreatedDate (when the account record was created in Salesforce; not necessarily when the customer started paying)
- Grain: 1 row per Salesforce account (`Id`)
- Notes / assumptions:
    - Accounts may exist without Stripe billing records (prospects, churned customers, or missing mappings).
    - `IsDeleted` exists → deleted accounts may still appear in extracts and need filtering rules later.
    - CRM “account created date” can be misleading for lifecycle metrics; revenue start should come from billing, not this field.
 
#### salesforce_contact
- Description: Represents an individual person associated with a Salesforce account. Contacts are CRM records used to store people-related information (e.g., decision-makers, stakeholders, billing contacts) and do not necessarily represent active product users.
- Primary key: `Id`
- Important timestamps: `CreatedDate` (when the contact record was created in Salesforce; not necessarily when the relationship with the organization began)
- Grain: 1 row per Salesforce contact (`Id`)
- Notes / assumptions:
  - Multiple contacts can be associated with a single Salesforce account.
  - Contacts may represent various roles (e.g., decision-maker, finance contact) and are not guaranteed to be the primary or active point of contact.
  - `IsDeleted` exists, meaning deleted contacts may still appear in historical extracts and require filtering in downstream models.
  - Contacts are not directly linked to product users and should not be assumed to represent product activity.

#### salesforce_opportunity
- Description: Represents a sales deal attempt associated with a Salesforce account. An opportunity captures sales intent and the potential value of a deal, which may be open, won, or lost, and does not guarantee realized revenue.
- Primary key: `Id`
- Important timestamps:
  - `CreatedDate` (when the opportunity was created in Salesforce)
  - `CloseDate` (when the opportunity was marked as closed; may be null for open deals)
- Grain: 1 row per Salesforce opportunity (`Id`)
- Notes / assumptions:
  - An account can have multiple opportunities over time (e.g., new business, expansions, renewals).
  - `Amount` represents expected deal value, not guaranteed or recognized revenue.
  - Opportunity status is derived from fields such as `StageName`, `IsClosed`, and `IsWon`.
  - Closed opportunities may not directly correspond to Stripe billing records and should be reconciled carefully with invoicing data.

## Stripe
