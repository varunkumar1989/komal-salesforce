# 05 — Integration, transactional messaging and deployment

## Goal

Connect SFMC safely to external systems, trigger the right message at the right event, and release changes without creating customer-impacting errors.

## Integration foundations

An integration needs four explicit decisions:

1. **Source:** which system sends or receives data?
2. **Identity:** which identifier joins the records?
3. **Contract:** what fields, data types, timing and failure behaviour are expected?
4. **Owner:** who monitors and fixes failures?

Never treat an API connection as “done” just because authentication works. A reliable integration includes limits, retries, logging, monitoring and a documented recovery path.

## Installed packages and API access

Use an Installed Package to obtain the appropriate API integration. Apply least privilege: grant only the scopes and business-unit access needed. Store credentials in approved secure locations, rotate them as required, and never embed secrets inside Content Builder or CloudPages code.

## Triggered and transactional messaging

| Pattern | Use when | Key guardrail |
|---|---|---|
| Batch campaign | A planned audience receives a message together | Frequency, suppression and approval controls |
| Triggered send | A system event should send a defined email | Idempotency and error logging |
| Transactional Journey | A customer action requires a timely, personalised message flow | Event schema, consent policy and operational SLA |
| API event | An external application injects an event into a journey | Authentication, schema validation and replay handling |

### Event design example

A transactional “order shipped” event might contain:

```json
{
  "eventId": "ship_84721",
  "contactKey": "C-10294",
  "orderId": "O-55081",
  "shipmentDate": "2026-10-27T09:00:00Z",
  "trackingUrl": "https://example.com/track/O-55081"
}
```

The `eventId` should make replay handling clear. If the source retries, the system should not send the same customer five shipment confirmations.

## Deployment and release management

Treat SFMC changes as releases:

1. Describe the change and acceptance criteria.
2. Separate development, test and production where the account design supports it.
3. Export or package assets using the approved deployment method.
4. Re-map data extensions, folders, sender profiles and references for the target environment.
5. Run a test send or test event.
6. Activate only after approval.
7. Monitor the release and retain rollback instructions.

### Release checklist

- [ ] Credentials and package scopes reviewed.
- [ ] Sender, domain and unsubscribe settings correct.
- [ ] Target data extension is populated and deduplicated.
- [ ] Journey entry and re-entry settings are intentional.
- [ ] Dynamic content branches have a test contact.
- [ ] Error and retry behaviour is documented.
- [ ] Owner and escalation route are known.
- [ ] Rollback method is prepared.

## Explain it in an interview

> “I design SFMC integration as a data contract, not a connector. I define the identifier, schema, timing, failure mode and monitoring first. For transactional messaging, I use an event identifier and test replay behaviour. For deployment, I treat every activation as a release with dependencies, approvals and a rollback plan.”

## Practice

Complete Lab 9 and Lab 10 in [practice-labs.md](practice-labs.md).
