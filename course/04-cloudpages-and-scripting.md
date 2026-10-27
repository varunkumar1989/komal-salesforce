# 04 — CloudPages, AMPscript and SSJS

## Goal

Create a useful customer-facing page that captures data safely, honours consent and handles errors gracefully.

## CloudPages

CloudPages hosts landing pages, forms, preference centres and lightweight interactive experiences within SFMC. A good page has a single purpose, a defined data contract, clear consent language and a testable thank-you/error state.

### Page checklist

- Define the audience and the page's one action.
- Capture only fields that are needed.
- Validate required inputs on both client and server sides.
- Store consent time, source and policy version where relevant.
- Show a user-friendly confirmation or error.
- Protect secrets and do not expose credentials in page code.
- Test on mobile and with realistic data.

## AMPscript

AMPscript is SFMC's personalisation and data-access scripting language. Use it for controlled data lookup, display and simple writes.

```
%%[
VAR @email, @result
SET @email = RequestParameter("email")

IF NOT EMPTY(@email) THEN
  SET @result = UpsertData(
    "Lead_Capture_DE", 1,
    "EmailAddress", @email,
    "Source", "CloudPage"
  )
ENDIF
]%%
```

The snippet is only a learning example. In production, validate the field, record consent appropriately, handle errors and ensure the Data Extension is secured.

## SSJS

Server-Side JavaScript (SSJS) gives JavaScript-style control for server-side SFMC tasks. Use it when the logic is clearer in JavaScript or when an SFMC server-side API requires it. Prefer the smallest possible code path, structured logging and predictable error handling.

### AMPscript or SSJS?

| Need | Prefer |
|---|---|
| Personalise a content block or email | AMPscript |
| Simple lookup or conditional content | AMPscript |
| Complex server-side flow or API interaction | SSJS, with reviewed error handling |
| Client-side visual interaction | HTML/CSS/JavaScript, with server-side validation |

## Preference centres and unsubscribe

A preference centre lets a customer choose communication topics or frequency. It does **not** replace a mandatory unsubscribe process. Do not build logic that silently overwrites a global unsubscribe state.

Record at minimum:

- ContactKey
- preference type
- preference value
- source page / campaign
- timestamp
- consent text or policy version, where applicable

## Explain it in an interview

> “I use CloudPages as a secure touchpoint between the customer and SFMC data. I keep the form purpose narrow, validate before write, preserve consent evidence and design a clear failure state. AMPscript handles personalisation and simple data tasks; SSJS is reserved for logic that benefits from server-side JavaScript and deliberate error handling.”

## Practice

Complete Lab 7 and Lab 8 in [practice-labs.md](practice-labs.md).
