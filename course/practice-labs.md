# SFMC practice labs

Build each lab in a training or sandbox environment where possible. Do not use real customer data without approval and a documented purpose.

## Lab 1 — Business unit and role design

**Task:** Draft a business-unit structure for a company with an India retail brand and a B2B brand.

**Deliverable:** One diagram and a permission matrix.

**Acceptance criteria:**

- Each BU has a clear business purpose.
- An administrator is not used as a normal sender.
- Permissions follow least privilege.
- The ownership of customer data is documented.

## Lab 2 — Customer data model

**Task:** Create `Customer_Master`, `Order_Summary` and `Preference` Data Extensions.

**Deliverable:** A data dictionary showing field, type, key and row grain.

**Acceptance criteria:**

- ContactKey is consistent across relationship tables.
- Primary keys prevent unintended duplicates.
- Each DE describes one row type.
- Consent can be audited.

## Lab 3 — Responsive email

**Task:** Build a single-column welcome email and a two-column product module that stacks on mobile.

**Deliverable:** Content Builder asset plus screenshots from desktop and mobile clients.

**Acceptance criteria:**

- The content remains readable at 320px wide.
- Essential text is live HTML, not only an image.
- Outlook fallback is checked.
- Alt text and unsubscribe are present.

## Lab 4 — Personalisation and dynamic content

**Task:** Send a campaign with a greeting fallback and two content branches based on `CustomerTier`.

**Deliverable:** Test evidence for Gold, Standard and missing-name contacts.

**Acceptance criteria:**

- Every branch renders correctly.
- Missing values do not expose broken syntax.
- The audience is excluded if consent is missing.

## Lab 5 — SQL audience

**Task:** Build an “inactive buyers” audience using customer and order tables.

**Deliverable:** SQL query, target DE and row-count validation note.

**Acceptance criteria:**

- The business definition is written in plain language.
- ContactKey appears once in the target DE.
- Query results are reconciled against a known sample.
- The automation has an error notification.

## Lab 6 — Welcome journey

**Task:** Create a three-step welcome journey with an entry source, decision split, wait and exit rules.

**Deliverable:** Screenshot of the journey canvas plus a measurement plan.

**Acceptance criteria:**

- Re-entry is intentional.
- Suppression or unsubscribe can exit the journey.
- The decision field has a documented source.
- A success metric is defined.

## Lab 7 — CloudPage form

**Task:** Build a landing page that captures email, first name and consent.

**Deliverable:** Page URL in the training environment, field map and test records.

**Acceptance criteria:**

- Required fields are validated.
- A confirmation and error state exist.
- Consent timestamp/source is recorded.
- No secret is visible in page code.

## Lab 8 — Preference centre

**Task:** Create a page allowing a customer to select product updates and event invitations.

**Deliverable:** Preference schema, page screenshot and test contact outcome.

**Acceptance criteria:**

- Global unsubscribe behaviour is not overridden.
- Each preference can be audited.
- The user sees a clear confirmation.

## Lab 9 — Transactional event contract

**Task:** Define an event for “order shipped.”

**Deliverable:** JSON schema, field definitions and duplicate-event rule.

**Acceptance criteria:**

- Event ID supports safe retries.
- ContactKey is stable.
- Required fields are validated.
- Monitoring owner is named.

## Lab 10 — Release checklist

**Task:** Simulate promoting an email, automation and journey to production.

**Deliverable:** Release checklist, dependencies list, test evidence and rollback plan.

**Acceptance criteria:**

- Dependencies are mapped.
- A test event or seed send passes.
- Activation owner is named.
- Rollback steps are specific and feasible.

## Portfolio evidence template

For each lab, write five sentences:

1. **Problem:** What customer or operations issue did the build solve?
2. **Data:** Which fields and source system were involved?
3. **Method:** What did you configure or code?
4. **Validation:** How did you test it?
5. **Limitation:** What would you improve in production?
