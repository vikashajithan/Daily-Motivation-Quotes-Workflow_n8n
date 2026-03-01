# Daily Motivation Quotes Workflow

## Overview

This n8n workflow automatically sends a **short, AI-generated motivational email** every morning at 6:00 AM (IST). It uses Groq's LLM to write a fresh, energetic message focused on discipline, consistency, and goal-setting — then delivers it straight to your inbox.

---

## Architecture

A simple 3-step linear pipeline:

**Schedule Trigger → LLM Chain → Gmail**

---

## Nodes & Components

| Node | Type | Purpose |
|------|------|---------|
| **Schedule Trigger** | Trigger | Fires every day at 6:00 AM (Asia/Kolkata timezone) |
| **Basic LLM Chain** | LLM Chain | Generates the motivational email content using a fixed prompt |
| **Groq Chat Model** | LLM | Powers the chain using `llama-3.1-8b-instant` via Groq |
| **Send a message** | Action | Sends the generated email to `vikashwork7@gmail.com` via Gmail |

---

## How It Works

1. Every morning at **6:00 AM IST**, the Schedule Trigger fires automatically
2. The **Basic LLM Chain** calls Groq with a fixed prompt instructing it to write a short motivational message covering:
   - An energetic greeting
   - Motivation around discipline and consistency
   - A reminder to focus on the main goal
   - A push to take action today
   - Signed off with the name **Vikash**
3. The generated text is sent as an email with the subject **"Daily motivation"** to the configured Gmail address

---

## Email Format

The AI produces a short, punchy email — not more than a few lines. Example structure:

```
Good morning! 🔥

Discipline beats motivation every single day. Show up, do the work,
and stay locked in on your goal. Today is your chance — take it.

— Vikash
```

---

## Configuration & Credentials

| Credential | Used By |
|-----------|---------|
| `Groq account` | Groq Chat Model |
| `Gmail account` | Send a message |

---

## Setup Instructions

1. **Groq**: Sign up at [groq.com](https://groq.com) and add your API key to the `Groq account` credential.
2. **Gmail**: Authenticate your Google account via OAuth2 in the `Gmail account` credential.
3. **Recipient email**: Update the `sendTo` field in the **Send a message** node if you want to change the destination address.
4. **Timezone**: The trigger is set to `Asia/Kolkata` (IST). Change it in workflow settings if needed.
5. The workflow is already **active** (`"active": true`) — it will run automatically once credentials are connected.

---

## Customization Tips

- **Change the name**: Replace `[vikash]` in the LLM prompt with your own name.
- **Change the time**: Edit the Schedule Trigger — currently set to `triggerAtHour: 6` (6:00 AM). Set any hour (0–23).
- **Upgrade the model**: Swap `llama-3.1-8b-instant` for a larger Groq model (e.g., `llama-3.3-70b-versatile`) for richer output.
- **Add more recipients**: Use Gmail's CC/BCC options in the Send a message node to include others.
- **Vary the prompt**: Add instructions like "include a quote from a famous person" or "add a daily challenge" to keep emails fresh.
