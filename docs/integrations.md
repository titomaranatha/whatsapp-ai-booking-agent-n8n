# Integrations

| Service | Use | Credential in n8n |
|---|---|---|
| WhatsApp Business Cloud API (Meta) | Receive messages (webhook), send replies and staff alerts | WhatsApp OAuth (trigger); WhatsApp Business Cloud (send nodes) |
| Anthropic API | LLM for the AI Agent (`claude-sonnet-4-5`) | Anthropic API key |
| Google Sheets | Booking records, `Bookings` tab | Google Sheets OAuth2 |
| n8n | Workflow runtime, static data, memory | n/a |

The exported workflow contains credential placeholders only.

## Bookings sheet columns (row 1)
Reference, Date, Customer WhatsApp, WhatsApp Name, Full Name, Programme, Category, Preferred Start, Payment, Child Age, Notes, Status

New rows are created with `Status = New`.
