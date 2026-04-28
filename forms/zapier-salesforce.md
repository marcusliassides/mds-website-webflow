# Form integration — Zapier → Salesforce

The contact form on `/contact` is wired to Salesforce via Zapier. The press inquiry CTA on `/press-kit` follows the same pattern with a different topic value.

## Webflow side

1. **Form name** in Designer: `MDS Contact` (data attribute: `data-name="MDS Contact"`).
2. **Required fields**: `name`, `email`, `topic`, `message`.
3. **Honeypot**: a hidden `name="website"` field. Keep it out of the focus order and accessibility tree; Zapier filters out submissions where this is non-empty.
4. **Success / fail states**: keep the default Webflow success message; customise copy in Designer to match brand voice.

## Environment, privacy, and cutover

- Build and test the Zap against a Salesforce sandbox first. Switch to production only after the final launch checklist pass.
- Confirm Salesforce ownership (`MDS Inbound`), Slack notifications, and optional email senders with the Mattel teams that own those systems.
- Form copy must link to Mattel's privacy policy and match the fields sent to Salesforce (`name`, `email`, `company`, `topic`, `message`).
- If visitors from regulated regions are in scope, confirm retention and lawful-basis language with Legal before launch.

## Zapier side

**Trigger** — `Webflow → New Form Submission`. Select the published site and the `MDS Contact` form.

**Step 1 — Filter (block bots)**
- Continue only if `website` field is empty.
- Continue only if `email` matches a basic email regex.

**Step 2 — Lookup or Create Lead in Salesforce**
- Search by email; if exists, update; otherwise create.
- Map fields:

  | Webflow field | Salesforce field          |
  |---------------|---------------------------|
  | name          | LastName (split on space) |
  | email         | Email                     |
  | company       | Company (default "Unknown")|
  | topic         | Lead_Source__c            |
  | message       | Description               |

- Set `LeadSource = "MDS Website"`.
- Set `Status = "New"`.
- Owner: round-robin queue `MDS Inbound`.

**Step 3 — Notify Slack**
- Channel: `#mds-inbound`.
- Message:
  > New `{{topic}}` from `{{name}}` ({{email}}) at `{{company}}`. Auto-routed to MDS Inbound queue.

**Step 4 — Confirmation email (optional)**
- From: `press@digitalstudios.mattel.com` (or `partnerships@…`).
- Reply-to: same.
- Verify the sender domain in the mail provider before enabling this step.
- Body: short acknowledgement, two-business-day SLA.

## Press inquiry CTA

The "Press inquiry" button on `/press-kit` opens a `mailto:press@digitalstudios.mattel.com` link rather than a separate form. Keep it that way — press teams strongly prefer email threads to form submissions.

## Testing

Before launch, submit a test entry from the staging URL and confirm:

- [ ] Lead appears in Salesforce within 60 seconds.
- [ ] Slack notification fires in `#mds-inbound`.
- [ ] Honeypot rejects a synthetic submission with `website=test`.
- [ ] Confirmation email lands in the test inbox.
- [ ] Form success message renders correctly on light AND dark mode.
