# Setup & Configuration

1. **Import** `workflow/whatsapp-agent.sanitized.json` into n8n.
2. **Add credentials:** WhatsApp Business Cloud (access token and business account ID) on the three send nodes; WhatsApp OAuth on the trigger; Anthropic on the chat model; Google Sheets on the booking node.
3. **Create the Google Sheet** with a tab named `Bookings` and the headers listed in [`integrations.md`](integrations.md). Paste its ID into the Google Sheets node (`YOUR_GOOGLE_SHEET_ID`).
4. **Edit `CONFIG`** at the top of the *Normalize* node:
   - `staffPhones` (digits only, with country code)
   - `staleAfterSeconds` (300), `maxMessagesPerHour` (40), `humanPauseHours` (2)
5. **Replace placeholders** in the AI Agent system prompt (phone numbers `0XXXXXXXXXX`, email `info@example.org`) and confirm prices and programmes are current.
6. **Activate** the workflow, copy the Production URL of the WhatsApp Trigger into Meta → WhatsApp → Configuration (webhook), and subscribe to `messages`.
7. **Test** with a personal number before announcing the line.

## Operational notes
- Staff alerts are free-text WhatsApp messages. Meta delivers them only if the staff number messaged the business number within the last 24 hours. The sheet is the permanent record.
- Memory and dedupe use in-memory/static data. Use Postgres or Redis chat memory if restarts must preserve context.
- Static data persists only while the workflow is active.
