# Real Estate Cold Outreach Automation (n8n)

This repository contains an **n8n workflow** that automates end-to-end cold outreach for real estate professionals.  
It scrapes real estate businesses from Google Maps, extracts and verifies email addresses, sends personalized cold emails via Gmail, and logs all outreach activity into Google Sheets.

The workflow is designed with **rate limiting, deduplication, email validation, and error handling** to support safe and scalable outbound campaigns.

---

## 🚀 What This Workflow Does

**High-level flow:**

1. Accepts keywords via webhook (e.g. real estate niches or Instagram-style keywords)
2. Scrapes real estate businesses from **Google Maps** using Apify
3. Extracts business contact emails
4. Deduplicates emails to avoid repeats
5. Validates emails using an email verification API
6. Filters out invalid, disposable, blocked, or undeliverable emails
7. Sends cold emails via **Gmail**
8. Logs all processed leads and outreach data into **Google Sheets**
9. Applies wait times and batching to prevent rate limits

---

## 🧠 Key Features

- Google Maps lead scraping via Apify
- Keyword-based prospecting
- Email deduplication
- Email validation (deliverable, non-disposable, non-blocked)
- Gmail cold email sending
- Google Sheets lead & outreach logging
- Batch processing with delays
- Webhook-triggered execution
- Designed for scalable outbound campaigns

---

## 🛠️ Tools & Services Used

- **n8n**
- **Apify (Google Maps Scraper)**
- **Gmail API**
- **Google Sheets API**
- **Email Verification API**
- Webhooks

---

## 🔁 Workflow Breakdown

### 1. Webhook Trigger
- Receives a POST request with `instagramKeywords`
- Keywords are split into an array and cleaned

### 2. Google Maps Scraping
- Uses Apify's Google Maps scraper
- Filters results to real estate–related businesses
- Scrapes emails, phone numbers, addresses, and websites

### 3. Deduplication & Limits
- Removes duplicate email addresses
- Limits the number of processed leads per run

### 4. Email Validation
- Verifies each email address
- Only allows emails that are:
  - Valid
  - Deliverable
  - Not disposable
  - Not blocked

### 5. Cold Email Sending
- Sends a predefined cold email via Gmail
- Dynamically injects city/location data
- Applies wait times between sends to protect deliverability

### 6. Logging & Tracking
- Saves all outreach data to Google Sheets:
  - Business name
  - Phone
  - Website
  - Email
  - Address
  - Email subject
  - Email body

---

## 📩 Cold Email Example

The workflow sends a personalized outreach email focused on helping real estate teams generate off-market listings, investors, and motivated sellers through direct outbound conversations.

Email personalization includes:
- City
- Business context
- Non-promotional, conversational tone

---

## ⚙️ Setup Instructions

### Requirements

- n8n (self-hosted or cloud)
- Apify account
- Google Workspace (Gmail + Sheets)
- Email verification API key

### Steps

1. Import the workflow JSON into n8n
2. Configure credentials:
   - Apify API
   - Gmail OAuth
   - Google Sheets OAuth
   - Email verification API key
3. Update:
   - Target location (default: New York, USA)
   - Email copy (optional)
   - Google Sheet destination
4. Activate the workflow
5. Trigger via webhook with keywords

---

## 🧪 Webhook Payload Example

```json
{
  "instagramKeywords": "real estate agent, real estate broker, property consultant"
}
