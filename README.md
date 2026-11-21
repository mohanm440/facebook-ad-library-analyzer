\# Facebook Ad Library Analyzer



An n8n workflow that scrapes Facebook Ad Library ads for a given search term, extracts the hook/body/CTA from each ad using Google Gemini, scores them against a weighted creative rubric, and identifies the strongest ad in the list.



\## How it works



1\. \*\*Scrape\*\* — Apify actor pulls live ads from Meta's Facebook Ad Library based on a search query

2\. \*\*Extract\*\* — Each ad's text is sent to Gemini to extract Hook, Body, and CTA

3\. \*\*Compare\*\* — All extracted ads are sent together to Gemini with a weighted scoring rubric

4\. \*\*Output\*\* — Returns the best ad with a full score breakdown and reasoning



\## Scoring rubric (100 points)



\- Hook Strength — 30 pts

\- CTA Clarity — 20 pts

\- Value Proposition — 20 pts

\- Message Clarity — 15 pts

\- Audience Relevance — 15 pts



\## Design decisions



\- Used Apify instead of the official Meta Ad Library API for faster setup without developer app review

\- Scoring is based on creative content only — no performance data (CTR, ROAS) is available or claimed

\- Free-tier Gemini API has a 5 requests/minute and 20 requests/day limit, so batch processing with a delay was added to avoid rate limit errors



\## Known limitations



\- Doesn't yet handle video ad transcription separately from text ads

\- Limited by free-tier API quotas during testing



\## Challenges faced



\- Hit Gemini's 429 "too many requests" error at both per-minute and per-day limits while testing with larger ad counts — resolved with batch delay and reduced test runs

\- Fixed a malformed Apify request URL and rotated an exposed API token during setup

