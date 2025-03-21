# Automated Web Scraper and Summarizer

## Overview

This Python program is designed to automate the process of searching for a topic on Google, scraping the top search results, generating summaries using the Groq Large Language Model (LLM), and sending the final summarized content via email. It is tailored for researchers, content creators, or anyone who needs to quickly gather and summarize information from the web.

## Accessing the Code

The code is available on Kaggle: [Automated Web Scraper and Summarizer](https://www.kaggle.com/code/neerazpatel/automated-web-scraper-and-summarizer).

## Running the Script

To execute the script, simply download the iPython file and run the cells. Note that scraping websites may take some time.

## Initialization

The script begins by importing necessary libraries:
- **requests**: For making HTTP requests.
- **firecrawl**: For scraping web content.
- **Groq**: For generating text summaries.

It initializes the Groq LLM with a specified model and API key.

## Fetching Search Results

The `fetch_search_results` function queries Google via SerpAPI. It constructs a URL with the search query and API key, makes a GET request to retrieve the search results, and extracts the top 10 organic results (excluding ads).

## Scraping and Summarizing Content

### 1. Scraping

- The `scrape_urls` function iterates over the list of URLs retrieved from the search results.
- Each URL is scraped using the FirecrawlApp instance to extract the main content.
- The content is cleaned to remove unnecessary data like images, URLs, and excessive whitespace.

### 2. Chunking and Summarizing

- The cleaned content is split into manageable chunks to handle large texts.
- Each chunk is processed by the Groq model to generate a summary.
- The summaries are combined into a final summary.

### 3. Final Summary

- A final summarization prompt is created to generate a structured output:
  - **Title**
  - **Introduction**
  - **Five subtopic titles**
  - **Conclusion**
- The result is printed and returned.

## Sending the Final Summary via Email

The `send_email_mailjet` function uses the Mailjet REST API to send the summarized content via email. The email includes both text and HTML versions for compatibility with different email clients.

## Error Handling

The script handles rate limits by SerpAPI and Firecrawl by pausing execution when a 429 HTTP error (Too Many Requests) is encountered. Other errors are logged and can be further expanded for more robust error handling.

## Environment Variables

To secure API keys and sensitive data, it is recommended to use environment variables. The keys used in this project include:

| Environment Variable | Description |
|-----------------------|-------------|
| **GROQ_API_KEY**      | API key for Groq LLM. |
| **SERPAPI_API_KEY**   | API key for SerpAPI. |
| **MAILJET_API_KEY**   | API key for Mailjet. |
| **MAILJET_API_SECRET**| API secret for Mailjet. |
| **FIRECRAWL_API_KEY** | API key for Firecrawl. |

These can be set in your shell's environment or within a `.env` file for local development.

