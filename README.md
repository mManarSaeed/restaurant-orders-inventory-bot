# Restaurant Orders & Inventory Management

A Telegram ordering system built with **n8n** for a small restaurant. It takes orders, checks that the ingredients are available, updates the stock and sends the manager a daily report.

> Personal learning project, built solo during an AI Automation & AI Agents course (Aug 2026).

## What it does

The workflow has **35 nodes** and **5 flows**, selected by a Switch node:

| Flow | What happens |
|---|---|
| New Order | Checks every ingredient of the meal against the recipe sheet. If something is missing the order is refused. Otherwise the order is saved and sent to the admin with **Done / Cancel** buttons. |
| Callback Button | When the admin presses Done, the stock is deducted (only once) and the customer receives an invoice with the total. Pressing the button twice does not process the order twice. |
| Cancel Order | Cancels the order without touching the stock. |
| Stock Update | The admin updates a stock item by message, for example `update Burger 50`. |
| Help Message | Shows the available commands. |

Extras:

- **Low-stock alert** when an ingredient falls to the threshold (5).
- **Daily report** on a schedule: number of orders, completed and cancelled orders, total revenue and the best-selling meal.

## Tech stack

n8n, Telegram Bot API, Google Sheets (tabs: `Stock`, `Orders`, `Recipe_Mapping`), n8n Code nodes for the business logic.

## Run it yourself

1. Import `workflow/restaurant-orders-inventory-bot.json` into n8n.
2. Create a Telegram bot with @BotFather and add its credential in n8n.
3. Create a Google Sheet with the three tabs above and set its ID where the nodes show `YOUR_GOOGLE_SHEET_ID`.
4. Put the admin chat ID where you see `YOUR_TELEGRAM_CHAT_ID`.
5. Activate the workflow.

The export contains no passwords, API keys or tokens.

## What I learned

- Adding nodes is not enough: you must understand the data moving from one node to the next.
- Testing edge cases made the system reliable: an ingredient that is out of stock, an admin pressing Done twice, a cancelled order, and low stock.

## Author

Manar Saeed Ibrahim – [LinkedIn](https://www.linkedin.com/in/manar-s-836718242)
