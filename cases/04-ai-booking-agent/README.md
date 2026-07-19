# AI Booking Agent for a Fitness Studio

> A VK/Telegram agent that books, reschedules and cancels sessions in a
> real CRM (Altegio) through natural conversation — built for a stretching
> studio and driven by an LLM router wrapped in a state machine.

## Problem
A boutique fitness studio lives and dies by its booking flow. Clients write
at any hour — "can I move tomorrow's class?", "what's free on Friday?" —
and every unanswered message is a lost visit. Hiring an admin to cover
evenings and weekends doesn't fit a small studio's economics. I founded
this studio, so I've felt this from the owner's chair.

## Solution
An AI agent in Telegram/VK that handles the full booking lifecycle. An LLM
understands the request, but a state machine decides what happens next —
the model routes, the workflow acts. The agent checks real slots in Altegio,
books, reschedules or cancels, and keeps conversation state in Google
Sheets, so the dialog survives restarts and never loses context.

## Key features
- **Natural-language booking** — clients write like they'd write to a human
- **State machine over LLM routing** — the model classifies intent, but
  every CRM action goes through explicit, deterministic states; no
  hallucinated bookings
- **Full lifecycle** — new booking, reschedule, cancellation, slot lookup
- **Real CRM integration** — live slot availability via Altegio API
- **Persistent dialog state** — Google Sheets as a lightweight state store

## How it works
- A Telegram/VK message triggers the workflow
- The LLM classifies intent and extracts entities (date, time, service)
- The state machine picks the branch: book / reschedule / cancel / clarify
- The workflow calls Altegio for real availability and executes the action
- Dialog state is written to Google Sheets after every step
- The client gets a confirmation in the same chat

## Stack
- n8n (self-hosted, Docker)
- Altegio API
- Telegram Bot API, VK API
- LLM (intent routing + entity extraction)
- Google Sheets API (state persistence)

## Outcome
The studio answers booking requests 24/7 without an admin on shift.
Reschedules and cancellations — the biggest time sink — run end to end
with no human in the loop.

## Screenshots
![Workflow in n8n](screenshots/workflow.png)
![Dialog in Telegram](screenshots/telegram-demo.png)
![State in Google Sheets](screenshots/sheet-state.png)
