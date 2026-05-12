# Job Tracker - n8n Automation

Automated job scraping and tracking workflow built with n8n (self-hosted via Docker).

## What It Does
- Scrapes job listings from multiple sources via RapidAPI (JSearch)
- Searches 50 job titles across 5 priority tiers
- Rotates keyword groups daily to stay within free API limits
- Filters results to British Columbia only
- Detects location mismatches (e.g., job says BC but description says Toronto)
- Flags remote positions
- Deduplicates against existing Google Sheet entries
- Appends new jobs to Google Sheets with priority and tier tags
- Sends daily HTML email digest grouped by priority

## Tech Stack
- n8n (self-hosted, Docker)
- Google Sheets (job database)
- RapidAPI JSearch (job scraping)
- Gmail (email digest)
- Ollama (planned, AI scoring)

## Workflow Nodes
1. Schedule Trigger (daily 7 AM PST)
2. Build Search Queries (keyword rotation across 12 groups)
3. Fetch Jobs from API (HTTP Request with batching)
4. Normalize and Prioritize (parse, filter BC, detect mismatches)
5. Read Existing Jobs (Google Sheets)
6. Filter Duplicates (URL comparison)
7. Any New Jobs? (IF node)
8. Append New Jobs (Google Sheets)
9. Build Email Digest (HTML email builder)
10. Send Email Digest (Gmail) - in progress

## Setup
1. Docker Desktop with WSL 2 on Windows 11
2. n8n running at localhost:5678
3. Google Cloud project with Sheets, Drive, and Gmail APIs enabled
4. RapidAPI account with JSearch subscription (free tier)

## Status
- [x] Schedule Trigger
- [x] Search query builder with rotation
- [x] API fetching with rate limit batching
- [x] Data normalization and BC filtering
- [x] Location mismatch detection
- [x] Remote job detection
- [x] Google Sheets read
- [x] Deduplication
- [x] Google Sheets append
- [ ] Email digest
- [ ] Ollama AI scoring