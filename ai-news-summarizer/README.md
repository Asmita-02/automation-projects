# AI News Summarizer (n8n Workflow)

An automated [n8n](https://n8n.io) workflow that pulls the latest AI and technology headlines from RSS feeds, summarizes them with Google Gemini, and emails you a clean daily brief.

## What It Does

Every day at **10:00 AM**, the workflow:

1. Fetches the latest articles from two RSS feeds:
   - **AI Business** (`https://aibusiness.com/rss.xml`) for AI news
   - **TechCrunch** (`https://techcrunch.com/feed/`) for broader technology news
2. Merges and aggregates all items into a single dataset
3. Sends the data to **Google Gemini** with a prompt that selects up to 3 AI stories and up to 3 technology stories
4. Emails the formatted summary to you through **Gmail**

### Example Output

```
Hi there,
Here's your Tech Brief:

AI NEWS
=======
HEADLINE IN ALL CAPS
Short 1-2 sentence summary.
Link: https://...

TECHNOLOGY UPDATES
==================
HEADLINE IN ALL CAPS
Short 1-2 sentence summary.
Link: https://...
```

## Workflow Overview

```
Schedule Trigger (10 AM)
   ├── AI News Feed (RSS) ───────┐
   └── Tech Updates Feed (RSS) ──┴── Data Merger ── Data Aggregator
                                                          │
                              Google Gemini Chat Model ───┤
                                                          ▼
                                              AI Summarization Model
                                                          │
                                                          ▼
                                                Gmail: Send a message
```

## Requirements

- An n8n instance (self-hosted or n8n Cloud)
- A **Google Gemini API key** (free tier available from [Google AI Studio](https://aistudio.google.com/))
- A **Gmail account** connected to n8n via OAuth2

## Setup

1. **Import the workflow**
   In n8n, go to *Workflows → Import from File* and select `ai_news_summarizer_github_safe.json`.

2. **Add your Gemini credentials**
   Open the *Google Gemini Chat Model* node, create a new credential, and paste your API key.

3. **Connect Gmail**
   Open the *Send a message* node and connect your Google account using OAuth2.

4. **Set the recipient**
   In the *Send a message* node, replace `your-email@example.com` with the address that should receive the brief.

5. **Test it**
   Click *Execute Workflow* to run it once and check your inbox.

6. **Activate**
   Toggle the workflow to **Active** so it runs automatically every day.

## Customization

- **Change the schedule:** edit the *Schedule Trigger* node (the default is 10:00 AM daily).
- **Use different news sources:** swap the URLs in the two RSS Feed nodes for any RSS feed you like.
- **Adjust the summary style or number of stories:** edit the prompt in the *AI Summarization Model* node.
- **Switch the AI model:** replace the Gemini node with another chat model supported by n8n.

## Security Note

This repository contains **no API keys, tokens, or personal email addresses**. You must add your own credentials after importing. Never commit exported workflows that contain real credential IDs or recipient emails.

## Tech Stack

- n8n
- Google Gemini
- Gmail
- RSS

## License

Feel free to use and modify this workflow for your own projects.
