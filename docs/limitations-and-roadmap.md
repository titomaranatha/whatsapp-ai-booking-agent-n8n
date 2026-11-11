# Limitations & Roadmap

## Status
- Workflow exported as **inactive**; setup flag `templateCredsSetupCompleted` is false. No production metrics are claimed.

## Limitations (observed from the workflow design)
- **In-memory state:** memory, dedupe, pause list, and rate limits are lost on restart or when the workflow is deactivated.
- **Staff alert delivery:** limited by Meta's 24-hour window; there are no WhatsApp message templates.
- **Chained dependency:** the booking and escalation branches run after *Send Reply*. If sending to the customer fails, no sheet row or staff alert is produced for that message.
- **No error workflow:** failures in Sheets, WhatsApp, or the AI call are not routed to an alert.
- **Single staff number:** alerts go to the first entry in `staffPhones`.
- **Static knowledge:** prices and programmes live in the prompt and need manual updates.
- **Text only:** attachments and voice notes are not processed.
- **Single booking per submission:** the agent submits one booking object per confirmed request.

## Roadmap
- [ ] Persistent memory (Postgres or Redis) and persistent dedupe
- [ ] Error-handling workflow with admin alerts
- [ ] WhatsApp message templates for reliable staff alerts
- [ ] Decouple sheet saving from the send step
- [ ] Knowledge base outside the prompt (sheet or database)
- [ ] Voice-note transcription and attachment handling
- [ ] Booking status updates and reminders
- [ ] Conversation quality review and evaluation set
