# Architecture

| Node | Type | Role |
|---|---|---|
| WhatsApp Trigger | WhatsApp Trigger | Receives `messages` webhooks from Meta |
| Normalize | Code | Dedupe, stale guard, staff commands, pause, rate limit, text extraction, booking reference |
| AI Agent | LangChain Agent | Prompted with the system message; max 3 iterations |
| Anthropic Chat Model | Chat model | `claude-sonnet-4-5`, 700 max tokens |
| Window Buffer Memory | Memory | Last 12 messages, keyed by customer number |
| Parse Reply | Code | Parses JSON, applies fallback, dedupes bookings and escalations, builds payloads |
| Send Reply | WhatsApp | Sends the reply to the customer |
| Is Booking? / Needs Escalation? | IF | Branch on `isBooking` / `isEscalation` |
| Save Booking (Google Sheets) | Google Sheets | Appends a row to `Bookings` |
| Notify Staff - Booking / Escalation | WhatsApp | Alerts the staff number |
| Setup notes | Sticky note | Setup instructions inside the workflow |

## Design choices
- **Structured output:** the model returns one JSON object; code, not the model, decides whether to save or alert.
- **Guards before the model:** abusive or duplicate traffic is dropped before any AI cost.
- **Human override:** staff messages are never answered by the bot and can pause it per customer.
- **Sheet as system of record:** staff alerts are best-effort; the sheet is permanent.

Diagrams: [`../architecture/system-architecture.mmd`](../architecture/system-architecture.mmd), [`../architecture/workflow-diagram.mmd`](../architecture/workflow-diagram.mmd)
