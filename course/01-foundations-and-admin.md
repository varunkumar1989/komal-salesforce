# 01 — Foundations and administration

## What you will be able to do

Explain what SFMC does, organise a safe business unit, distinguish contacts from subscribers, and choose the correct data container for a campaign.

## Core concepts

### CRM and Salesforce Marketing Cloud

A CRM stores and manages relationships with customers. Salesforce Marketing Cloud is a marketing-engagement platform: it uses customer data to deliver, automate and measure messages across channels. In a simple explanation: **CRM helps you know the customer; SFMC helps you communicate with the customer at scale.**

### Account, business unit and user

- **Account:** the overall SFMC organisation.
- **Business Unit (BU):** a separated workspace for a brand, market, region or team.
- **User:** a person who signs in and receives only the permissions needed for their role.
- **Role / permission:** the actions a user is allowed to perform.

Use a BU when different teams need separate branding, data access or sending governance. Use least-privilege permissions; never use an administrator account for daily campaign work.

### Contact, Subscriber and ContactKey

- **Contact:** a person or entity represented across SFMC channels.
- **Subscriber:** an email-addressable record for email sending.
- **ContactKey:** the stable identifier that ties a person to data and channel activity.

A useful rule: choose one durable ContactKey such as CRM Contact ID or customer ID. Do not change it to an email address just because an email address changes.

### Lists and Data Extensions

| Container | Best for | Avoid when |
|---|---|---|
| List | Simple, email-centred audience management | You need multiple fields, relationships or high-scale modelling |
| Data Extension (DE) | Structured data, segmentation, automations and journeys | You do not know the row grain or key |
| Publication list | Optional communications by topic | You need to bypass global unsubscribe rules |
| Suppression / exclusion | People who must not receive a send | You need to model campaign eligibility |

Before creating a DE, write its **data grain**: “one row per customer,” “one row per order,” or “one row per preference.” Mixing grains creates duplicate sends and inaccurate reporting.

## Mini build: a safe subscriber model

Create a sendable DE called `Customer_Master`:

| Field | Type | Key? | Notes |
|---|---|---:|---|
| ContactKey | Text | Yes | Stable customer identifier |
| EmailAddress | EmailAddress | No | Send relationship field |
| FirstName | Text | No | Optional personalisation |
| CountryCode | Text | No | Segmentation |
| ConsentStatus | Text | No | Track permission source and state |
| LastUpdated | Date | No | Audit field |

Then create a second DE called `Order_Summary` with one row per order. Relate both through `ContactKey`; do not put many orders into one customer row.

## Administration checklist

- [ ] Name BUs, DEs, automations and journeys consistently.
- [ ] Use roles rather than shared credentials.
- [ ] Identify the owner of every production send.
- [ ] Document the ContactKey and data grain.
- [ ] Confirm consent and suppression logic before activation.
- [ ] Review access when a team member changes role.

## Explain it in an interview

> “I treat SFMC as a governed engagement layer. I start with a stable ContactKey and clear data grain, then isolate brands or regions in business units and give users only the permissions required for their job. That reduces duplicate messaging, data leakage and avoidable send errors.”

## Practice

Complete Lab 1 and Lab 2 in [practice-labs.md](practice-labs.md).
