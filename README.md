# Superstore Sales: Power BI Dashboard and AI Chat

An end-to-end analytics project: a Power BI report on a Superstore sales dataset, a Supabase database with read-only access, and a chat page that answers questions from that data and shows the SQL behind every answer. The project also tracks answer accuracy, sends an AI monitoring summary of any answers marked wrong, and uses Power Automate to deliver daily updates.

**Live chat:** https://uday027.github.io/superstore-chat/

## Screenshots

| Overview | Trends |
|---|---|
| ![Overview](docs/screenshots/01-overview.png) | ![Trends](docs/screenshots/02-trends.png) |

| Chat with SQL | Supabase security |
|---|---|
| ![Chat](docs/screenshots/03-chat-sql.png) | ![RLS](docs/screenshots/04-supabase-rls.png) |

## Architecture

![Architecture](docs/screenshots/05-architecture.png)

- **Data:** Kaggle Superstore sample, loaded into Supabase.
- **Database:** Supabase (PostgreSQL) with Row Level Security. Visitors have read-only access.
- **Chat page:** built with an AI artifact and hosted on GitHub Pages. It answers questions from Supabase and shows the SQL for each answer.
- **Accuracy tracking:** each answer is counted as right, wrong, or off-topic, and the totals appear on the page.
- **AI monitoring:** a daily summary of any answer marked wrong, including the question, the answer given, and the visitor's explanation.
- **Dashboard:** Power BI Desktop, imported from Supabase data.
- **Automation:** a Power Automate flow sends the previous day's raw data every morning at 9:00 AM.

## What it does

- **Executive Overview:** total sales, profit, margin, orders, quantity, sales by region and category.
- **Sales Trends:** quarterly sales and profit, margin over time, seasonality, and a year-by-year performance table with sparklines, progress bars, and growth indicators.
- **Ask a question:** type a question in plain English. The page answers from the database and shows the SQL it ran.
- **Report a wrong answer:** visitors can mark an answer as wrong and explain why. The report is saved, and the AI monitoring summary sends it to the project owner.
- **Daily updates:** Power Automate delivers the previous day's raw data every morning.

## Questions the chat answers

- What was the total sales?
- Which region has the highest profit?
- Which sub-categories are making a loss?
- What is the profit margin by category?
- In the East region, which 5 products have the lowest sales?

Each answer shows the SQL it ran. You can copy it and run it in the Supabase SQL Editor.

## Power BI report

Open `report/superstore_dashboard.pbix` in Power BI Desktop (free). It uses the public sample data stored in the file, so no database connection is needed.

Pages: Overview, Trends, and Products and losses.

## Automation

A Power Automate flow runs every morning at 9:00 AM. It runs a query on the Power BI dataset, creates a CSV of the previous day's raw data, and emails it.

![Power Automate flow](docs/screenshots/06-powerautomate.png)

## Security

- Visitors have read-only access to the sales data. They can add records only to the accuracy and report tables.
- Row Level Security is enabled on every table.
- The chat uses fixed query functions, so visitors cannot run their own SQL.
- No customer names or IDs are included in the data.

## Data notes

- The dataset is a public Superstore sample.
- Order dates were adjusted to 2017 to 2026 for this project, so year and quarter results differ from the original file.
- 2026 covers January to September.

## Limitations

- The chat understands common questions in plain English. For best results, try the example questions above, or phrase your question the way they're written.

## Tools

Power BI Desktop, Supabase, PostgreSQL, SQL, DAX, AI artifacts, AI monitoring, GitHub Pages, Power Automate.

## Author

Uday Kumar
