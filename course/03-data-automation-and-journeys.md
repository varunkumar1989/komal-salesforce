# 03 — Data, Automation Studio and Journey Builder

## Goal

Turn source data into a governed audience, automate repeatable processing, and deliver a lifecycle journey that has clear entry, exit and measurement rules.

## Data Extensions and data modelling

A Data Extension is a table. Start with the question: **what does one row mean?**

| Example DE | Correct grain | Key |
|---|---|---|
| Customer_Master | one row per customer | ContactKey |
| Order_Summary | one row per order | OrderID |
| Product_Catalog | one row per product | ProductID |
| Preference | one row per customer and preference type | ContactKey + PreferenceType |

Use a shared ContactKey where relationships are needed. Store the original source identifier and avoid deriving a new identifier from a changeable email address.

## SQL Query Activity

A SQL Query Activity transforms or segments data. It writes to a target Data Extension. Use it for aggregation, joins, deduplication and audience creation.

```sql
SELECT
  c.ContactKey,
  c.EmailAddress,
  MAX(o.OrderDate) AS LastOrderDate,
  SUM(o.OrderValue) AS LifetimeValue
FROM Customer_Master c
INNER JOIN Order_Summary o
  ON c.ContactKey = o.ContactKey
WHERE c.ConsentStatus = 'OptedIn'
GROUP BY c.ContactKey, c.EmailAddress
```

Before activating a query:

1. Validate row counts against the source.
2. Check for duplicate ContactKeys.
3. Confirm the target DE schema and overwrite/update method.
4. Test with a small audience.
5. Document the business rule in plain language.

## Automation Studio

Automation Studio runs repeatable activities on a schedule or file trigger. A common flow:

1. File Transfer or import source data.
2. Data Extract or SQL Query Activity transforms it.
3. Filter or script applies business rules.
4. Verification alert notifies the owner.
5. Journey uses the prepared DE.

Design for re-runs: use idempotent logic where possible, record load date, and alert on failure. An automation that “usually works” without monitoring is not a reliable production process.

## Contact Builder and attribute groups

Contact Builder maps the relationships between contact data. An attribute group helps you relate customers, orders, preferences and other entities around the ContactKey.

Document:

- the contact model,
- relationship direction,
- cardinality (one-to-one / one-to-many),
- source owner,
- refresh schedule,
- and consent field.

## Journey Builder

A Journey Builder journey is a decision flow driven by a defined event or audience.

### Journey design canvas

| Component | Question to answer |
|---|---|
| Entry source | What event or audience starts the journey? |
| Entry rule | Can a contact enter again? |
| Decision split | What explicit data condition decides the branch? |
| Wait | Is the timing justified by customer intent? |
| Exit criterion | When should a contact stop receiving messages? |
| Goal / measurement | What behaviour means the journey worked? |

### Example: welcome journey

- Entry: a customer joins `Customer_Master` with `ConsentStatus = OptedIn`.
- Message 1: welcome email immediately.
- Wait: two days.
- Decision: if no site activity, send helpful product-discovery email; otherwise, send product education.
- Exit: unsubscribe, conversion, or account deletion.
- Measure: first purchase rate within 14 days versus an appropriate comparison group.

## Explain it in an interview

> “I build journeys on a clear data contract. Every Data Extension has a row grain and key, the automation is monitored and repeatable, and the journey makes entry, exit and frequency rules explicit. That allows marketing teams to move faster without losing control of customer experience.”

## Practice

Complete Lab 5 and Lab 6 in [practice-labs.md](practice-labs.md).
