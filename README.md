# TechStore – AI Sales & Support Bot

A Telegram bot built with **n8n** that answers customer questions for a fictional online store (TechStore), takes orders, tracks existing orders and hands complex cases to a human.

> Personal learning project, built solo during an AI Automation & AI Agents course (Aug 2026).

## What it does

- **Understands each message** with a Text Classifier that sorts it into 8 intents: Product Inquiry, FAQ, Complaint, Order Support, Create Order, Human Support, Greeting and Other.
- **Answers as an AI Agent** (Groq, Llama 3.3 70B) with conversation memory, so customers do not repeat themselves.
- **Stays accurate**: the agent answers only from the company information in its prompt (4 products, shipping, returns, payment, support hours) and says "I don't have that information" instead of inventing prices or policies.
- **Takes orders** through a chat conversation and saves them in Google Sheets.
- **Tracks orders** by order number (for example `ORD-1001`) by looking it up in Google Sheets.
- **Escalates to a human** by sending a Telegram alert to the support person when the customer asks for it or the case is complex.

## Tech stack

n8n, Groq Chat Model (Llama 3.3 70B), Telegram Bot API, Google Sheets, n8n Simple Memory.

## How it works

1. A Telegram message triggers the workflow.
2. The Text Classifier decides the intent.
3. The message is routed to the matching branch: AI Agent answer, order creation, order tracking or human escalation.
4. Orders and tickets are written to Google Sheets.

## Run it yourself

1. Import `workflow/techstore-ai-support-bot.json` into n8n (Workflows > Import from file).
2. Create your own credentials in n8n: Telegram bot (from @BotFather), Groq API key, Google Sheets.
3. Create a Google Sheet for orders and set its ID where the nodes show `YOUR_GOOGLE_SHEET_ID`.
4. Put your support person's chat ID where you see `YOUR_TELEGRAM_CHAT_ID`.
5. Activate the workflow and message your bot.

The export contains no passwords, API keys or tokens.

## What I learned

- Building an AI automation is more than calling an LLM: you also design how the system understands intent, chooses a path, handles data and knows when a human must step in.
- A strict prompt ("use only the information provided") reduces made-up answers.

## Author

Manar Saeed Ibrahim – [LinkedIn](https://www.linkedin.com/in/manar-s-836718242)
