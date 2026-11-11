# Security & Privacy

- **No secrets in the repo.** Credentials are stored in n8n. The export contains `REPLACE_ME` placeholders; `.gitignore` blocks raw exports so only the sanitized file is committed.
- **Redacted data.** Staff and office phone numbers and the contact email in the export were replaced with placeholders. Re-check before sharing any updated export.
- **Customer data.** Conversations and bookings contain personal data (names, phone numbers, children's ages). Keep the Google Sheet private, restrict access, and do not commit exports or logs.
- **Children's data.** Youth bookings include a child's age. Collect only what is needed and follow applicable Nigerian data-protection rules (NDPA).
- **Payment safety.** The agent never requests card numbers, PINs, or passwords and holds no payment details.
- **Abuse control.** Rate limiting, dedupe, and stale-message checks reduce spam and AI cost; staff can pause the bot per customer.
- **Prompt-injection resistance.** Prompt instructions plus code-level validation; see `agent-design.md`.
- **Webhook exposure.** Keep the n8n instance updated and the Production URL private to Meta.
- **Transparency.** The agent discloses it is an AI assistant when asked.
