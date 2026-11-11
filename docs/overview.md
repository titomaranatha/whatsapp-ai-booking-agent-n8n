# Overview

## Purpose
Handle first-line WhatsApp enquiries for a training centre and convert confirmed interest into structured booking requests, with humans handling anything uncertain.

## Intended users
- **Customers:** prospective students, parents, SIWES/NYSC participants, career-switchers.
- **Staff:** receive booking and escalation alerts and keep the Bookings sheet.

## What the agent does
- Answers about programmes, price list, how to join, location, and hours, using only facts in its system prompt.
- Collects booking details one question at a time, reads them back, and submits only after explicit customer confirmation.
- Escalates custom pricing, instalment plans, partnerships, refunds, complaints, payment proof, requests for a human, and anything not covered.

## What it deliberately does not do
- Quote prices or dates not in its prompt, or invent discounts and payment details.
- Collect card numbers, PINs, or passwords.
- Guarantee a seat: a booking is a *request* the team confirms.
- Open images, documents, or voice notes.
