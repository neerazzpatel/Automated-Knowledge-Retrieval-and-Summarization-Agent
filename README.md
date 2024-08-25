**Automated Web Scraper and Summarizer**


This Python program automates the process of searching for a topic on Google, scraping the top search results, generating summaries using the Groq LLM (Large Language Model), and sending the final summarized content via email. The script is designed for researchers, content creators, or anyone who needs to quickly gather and summarize information from the web.


**Initialization**

The script starts by importing necessary libraries, including requests for making HTTP requests, firecrawl for scraping web content, and Groq for generating text summaries. The script also initializes the Groq LLM with a specified model and API key.

**Fetching Search Results**

The fetch_search_results function is used to query Google via SerpAPI. The function constructs a URL with the search query and API key, then makes a GET request to retrieve the search results. The top 10 organic results (excluding ads) are extracted and returned.

**Scraping and Summarizing Content**

**1. Scraping:**
The scrape_urls function iterates over the list of URLs retrieved from the search results.
Each URL is scraped using the FirecrawlApp instance to extract the main content.
The content is then cleaned to remove unnecessary data like images, URLs, and excessive whitespace.

**2. Chunking and Summarizing:**
The cleaned content is split into manageable chunks to handle large texts.
Each chunk is processed by the Groq model to generate a summary.
The summaries are combined into a final summary.

**3. Final Summary:**
A final summarization prompt is created to generate a structured output: title, introduction, five subtopic titles, and a conclusion.
The result is printed and returned.
Sending the Final Summary via Email
The send_email_mailjet function uses the Mailjet REST API to send the summarized content via email. The email includes both text and HTML versions for compatibility with different email clients.


**Error Handling**

The script is equipped to handle rate limits by SerpAPI and Firecrawl by pausing the execution when a 429 HTTP error (Too Many Requests) is encountered. Other errors are logged and can be further expanded for more robust error handling.


**Environment Variables**

To keep your API keys and sensitive data secure, it is recommended to use environment variables. The keys used in this project include:


GROQ_API_KEY: API key for Groq LLM.

SERPAPI_API_KEY: API key for SerpAPI.

MAILJET_API_KEY: API key for Mailjet.

MAILJET_API_SECRET: API secret for Mailjet.

FIRECRAWL_API_KEY: API key for Firecrawl.

You can set these in your shell's environment or within a .env file for local development.
