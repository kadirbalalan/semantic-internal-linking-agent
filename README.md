🔗 Semantic Internal Linking Automation Agent
An automated SEO agent built with n8n that analyzes content clusters and intelligently injects semantic internal links. unlike basic plugins that just look for keyword matches, this workflow uses an LLM to understand the context of the page and decides whether to hyperlink an existing phrase or generate a new, contextually relevant bridge sentence.

🚀 The Problem
Internal linking is crucial for SEO (crawling and authority distribution), but doing it manually for hundreds of pages is:

Time-consuming: Requires reading both source and target pages.

Inconsistent: Hard to maintain a perfect silo structure manually.

Low Quality: Plugins often force links into unnatural keywords.

💡 The Solution
This workflow acts as an SEO Editor. It takes a list of URLs from a specific content cluster (Topic Silo) in a Google Sheet, scrapes their live content, and uses an LLM to cross-link them semantically.

Key Features
Hybrid Injection Strategy: The LLM decides the best linking method based on context:

Method A (Anchor Match): Finds an existing relevant phrase and wraps it in an href.

Method B (Bridge Sentence): If no relevant phrase exists, it writes a new, natural sentence containing the link and inserts it where it fits best.

Cluster-Based Logic: Designed to work within specific topic clusters (single sheet) to ensure topical authority is preserved.

Live Content Analysis: Scrapes the current live version of the page to ensure links are placed in the actual body content, ignoring navbars or footers.

CMS-Ready Output: Writes the final HTML output back to the Google Sheet, ready to be copy-pasted directly into WordPress or any CMS.

🛠️ Technical Architecture
The workflow consists of 4 main stages:

Ingestion & Filtering:

Fetches the content plan from Google Sheets.

Filters for rows that haven't been processed yet to save tokens.

Loops through each URL in the cluster.

Scraping & Parsing:

HTTP Request: Fetches the raw HTML of the target URL.

HTML Extractor: Cleans the DOM to isolate the main article body (removing scripts, styles, and boilerplate).

Semantic Processing:

OpenRouter / LLM Chain: The scraped content and the list of target internal links are fed into a Large Language Model.

Prompt Engineering: The model is instructed to find semantic opportunities for linking. It is strictly forbidden from hallucinating information and must maintain the original tone of the article.

Formatting & Update:

The code node formats the LLM's output.

Updates the specific row in Google Sheets with the "Optimized Content" ready for publishing.

⚙️ How to Use
Import: Import the .json file into your n8n instance.

Setup Google Sheets:

Create a sheet with columns: Target URL, Keyword, Current Content, Optimized Content (Output).

Configure Credentials:

Connect your Google Sheets OAuth2 credential.

Connect your OpenRouter API key (or OpenAI/Anthropic).

Run: Execute the workflow. It will process the cluster and populate the sheet with linked HTML.

📝 Example Output
Input (Raw Text):

"Marketing automation is essential for growing businesses. It helps you save time."

LLM Decision: Needs a link to the 'Email Marketing Guide'.

Output (Hybrid Injection):

"Marketing automation is essential for growing businesses. For example, using strategies from our Email Marketing Guide can significantly boost retention. It helps you save time."

⚠️ Prerequisite
Self-hosted n8n or n8n Cloud.

A valid API Key for an LLM provider (OpenRouter, OpenAI, etc.).

Google Cloud Console project with Sheets API enabled.
