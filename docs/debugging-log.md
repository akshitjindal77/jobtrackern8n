# Debugging Log

## 2026-05-11: Initial Build

### Issue: RapidAPI 429 Rate Limit
- Error: "The service is receiving too many requests from you"
- Cause: n8n fired all 4 HTTP requests simultaneously
- Fix: Added batching to HTTP Request node (Batch Size: 1, Interval: 2000ms)

### Issue: n8n Table Shows "empty" for Blank Fields
- Not a real problem. n8n displays empty strings as "empty" in the table view
- Google Sheets receives blank cells correctly

### Issue: False REMOTE OK Tags
- Cause: remote detection matched "remote" in phrases like "remote desktop" or "remote access"
- Fix: Changed to phrase-based matching (e.g., "work from home", "remote position", "location: remote")
- Also added title check for "(Remote)"

### Issue: Cloud Wiz Toronto Job Not Flagged
- Job listed as Langley BC but description said Downtown Toronto ON
- Root cause: full description contained a remote keyword, skipping mismatch check
- Fix: Tightened remote keyword matching (see above)

### Issue: Triple Eight Transport False Positive
- Job is legitimately in Abbotsford BC but company mentions Calgary/Edmonton terminals
- Accepted as minor false positive; AI scoring will handle this better

### Issue: Google Sheet Column Mismatch
- Headers had typos: "Data Posted" instead of "Date Posted", "Data Scrapped" instead of "Date Scraped"
- n8n created new columns at the end instead of writing to existing ones
- Fix: Corrected all header names to exactly match code output field names

### Issue: Filter Duplicates - "Referenced node doesn't exist"
- Cause: Node was named "Normalize and Priorites" (typo) but code referenced "Normalize and Prioritize"
- Fix: Renamed node to match the code string exactly