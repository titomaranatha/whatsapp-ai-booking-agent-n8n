# Workflow: trigger to completion

1. **Trigger:** a WhatsApp `messages` webhook arrives.
2. **Normalize** drops the message (no output) if it is:
   - a delivery/read status update (no message),
   - a duplicate message ID (Meta retries; last 200 IDs kept),
   - older than 300 seconds,
   - from a staff number (staff commands `/bot on|off <number>` are processed, then nothing is sent),
   - from a customer currently paused,
   - over 40 messages in an hour from that customer,
   - empty after text extraction.

   Otherwise it builds the customer context: number, WhatsApp name, text (max 1,500 characters; non-text messages become a bracketed note), and a booking reference `KIL-` plus 5 characters.
3. **AI Agent** receives the text with the system prompt (current time in Africa/Lagos, customer details, reference) and 12-message memory. It returns JSON: `reply`, `booking`, `escalate`.
4. **Parse Reply** extracts the JSON. If parsing fails or `reply` is empty, a fallback message with contact options is used. It also strips markdown bold/headings, caps length, and:
   - builds a booking row only if `full_name` and `programme` are present and the same customer/programme was not booked in the last 15 minutes,
   - builds an escalation only if the same customer/reason was not escalated in the last 30 minutes.
5. **Send Reply** sends the message to the customer.
6. **Branches** (both run after Send Reply):
   - **Booking:** append a row to the `Bookings` sheet, then alert staff.
   - **Escalation:** alert staff.

## Booking conversation rules (from the prompt)
Collect one item at a time: full name, programme, category, preferred start month, optional payment preference, and child age for youth programmes. Read back, wait for explicit confirmation, submit once, give the reference, and state that the team will confirm.

## Escalation reasons
`custom_pricing`, `instalment`, `partnership`, `nysc_ppa`, `refund`, `complaint`, `human_requested`, `payment_proof`, `other`.

## Automation level
| Operation | Level |
|---|---|
| Answering enquiries, collecting booking details | Automated |
| Saving bookings, alerting staff | Automated |
| Confirming a seat, payment details, custom pricing, instalment plans, refunds, complaints | Manual (staff) |
| Pausing the bot for a customer | Manual (staff command) |
| Updating prices or programme info | Manual (edit the system prompt) |
