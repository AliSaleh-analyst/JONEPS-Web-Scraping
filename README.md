# JONEPS Pharmaceutical Tender Tracker

Automated daily scraper that monitors the **Jordan Government Procurement Portal (JONEPS)** for pharmaceutical tenders and keeps them organized in an Excel file updated every day without any manual effort.


<img width="1440" height="508" alt="image" src="https://github.com/user-attachments/assets/c2645fcd-7bd4-4e19-bf4b-b22be0118b9f" />

---

## What It Does

- Visits the JONEPS website daily via GitHub Actions
- Scrapes all tender listings and filters **pharmaceutical-related tenders only**
- Appends new tenders to `JONEPS-Tenders.xlsx`, no duplicates, no overwrites
- Stops early once it detects no new tenders, keeping runtime minimal
- Commits the updated Excel file back to this repository automatically

---

## Output

The file `JONEPS-Tenders.xlsx` contains:

| Column | Description |
|--------|-------------|
| `Tender_no` | Unique tender reference number |
| `Title` | Full tender title (Arabic) |
| `Closing_date` | Last date to submit a bid |

---

## How It Works

GitHub Actions (daily 9:00 AM Jordan Time)
↓
Opens JONEPS website via headless Chrome
↓
Scrapes tender listings page by page
↓
Filters pharmaceutical tenders by keyword
↓
Skips already-recorded tenders
↓
Appends new rows to JONEPS-Tenders.xlsx
↓
Commits & pushes updated file to repo



---

## Tech Stack

- **Python** — core scraping logic
- **Selenium** — browser automation
- **openpyxl** — Excel read/write
- **GitHub Actions** — daily scheduled execution

---

## Pharma Keywords Used

English: `pharma`, `medicine`, `drug`, `medical`, `hospital`, `clinic`

Arabic: `دواء`, `دوائي`, `صيدل`, `مستشفى`, `طبي`, `أدوية`, `صحة`

---

## Running Manually

You can trigger the scraper anytime without waiting for the daily schedule:

1. Go to the **Actions** tab in this repository
2. Click **JONEPS Daily Scrape**
3. Click **Run workflow**

---

## Setup

No configuration needed — the workflow runs automatically using GitHub's built-in token.

To adjust the schedule, edit `.github/workflows/scrape.yml` and change the cron expression:

```yaml
cron: '0 6 * * *'  # 6:00 AM UTC = 9:00 AM Jordan Time
Data Source
Jordan Government Procurement Portal — JONEPS
