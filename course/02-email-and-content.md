# 02 — Email Studio and Content Builder

## Goal

Build an accessible, personalised, responsive email that renders safely in common clients and is tested before a live send.

## Email Studio essentials

- **All Subscribers:** account-level email subscription record.
- **Send classification:** bundles commercial/transactional intent, sender profile and delivery profile.
- **Sender profile:** display name and from address.
- **Delivery profile:** delivery settings such as header/footer and IP behaviour.
- **Exclusion / suppression:** people who must not receive the message.

A practical sequence: define the audience → select a compliant send classification → build in Content Builder → preview personalisation → test across email clients → send or activate.

## Content Builder essentials

Use Content Builder for reusable content blocks, templates, dynamic content and asset management.

### Personalisation

A personalisation string inserts a value from the send context, for example:

```
Hello %%FirstName%%,
```

Always provide a fallback. A blank greeting is better than exposing a broken token, but a deliberate fallback is best:

```
%%[ IF EMPTY(@FirstName) THEN SET @FirstName = "there" ENDIF ]%%
Hello %%=v(@FirstName)=%%
```

### Dynamic content

Use dynamic content when the message changes based on a field such as language, lifecycle stage or product category. Keep the rule small and test every branch; complex logic is easier to audit in a documented data field than inside a single content block.

## Responsive email pattern

Email clients are inconsistent. Build the core layout with tables and inline CSS, then enhance it for supported clients.

```html
<table role="presentation" width="100%" cellspacing="0" cellpadding="0" border="0">
  <tr>
    <td align="center">
      <table role="presentation" width="600" class="container" cellspacing="0" cellpadding="0" border="0">
        <tr><td style="padding:24px; font-family:Arial, sans-serif;">...</td></tr>
      </table>
    </td>
  </tr>
</table>
<style>
  @media screen and (max-width: 600px) {
    .container { width: 100% !important; }
    .stack { display: block !important; width: 100% !important; }
  }
</style>
```

### Outlook rendering

Classic Windows Outlook uses a Microsoft Word rendering engine. Prefer table layouts, explicit widths, inline CSS, and tested fallbacks. Avoid relying only on modern CSS such as flexbox, grid, background images or unsupported web fonts. Use VML only when it is necessary and fully tested, for example for a critical background-image fallback.

### Dark mode

You cannot reliably force every email client to preserve your design. Protect readability instead:

- Use high text-to-background contrast.
- Avoid putting essential text only inside images.
- Use transparent PNGs carefully because some clients alter background colours.
- Test both light and dark environments.
- Place a visible border around light modules that could disappear on a light background.

## Pre-send QA checklist

- [ ] Subject line and preheader are complete.
- [ ] From name, reply address and send classification are correct.
- [ ] Every personalisation field has a fallback.
- [ ] Links include the correct UTM naming and work on mobile.
- [ ] Unsubscribe and preference-centre links work.
- [ ] Copy is scannable and accessible; image alt text is meaningful.
- [ ] Desktop Outlook, Gmail, Apple Mail and a mobile client are checked.
- [ ] Dark-mode readability is checked.
- [ ] A seed-list or test audience confirms data and dynamic branches.

## Explain it in an interview

> “I treat email as a constrained front end. I use a table-first structure for broad rendering, progressive enhancement for mobile, and client testing for Outlook and dark mode. In SFMC, I also test the data layer — personalisation, dynamic content, sender profile and suppression — because a visually correct email can still be operationally wrong.”

## Practice

Complete Lab 3 and Lab 4 in [practice-labs.md](practice-labs.md).
