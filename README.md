# 📰 AI News Summarizer Agent

A fast, lightweight, and automated news-research workflow powered by **LangGraph**, **OpenAI**, and the **News API**.
Give it a topic, and it turns the noisy chaos of online news into clean, bulleted summaries.

## 📜 License

Released under the **MIT License**.

```
THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT...
```

## 🌐 Overview

This project is a Python-based intelligent news-summarization agent. It stitches together multiple tools to behave like a structured human researcher:

• Generates optimized search queries based on your prompt
• Pulls news metadata via **News API V2**
• Scrapes full articles using **BeautifulSoup**
• Filters and selects the most relevant sources
• Produces tight, bulleted *TL;DR* summaries using **GPT-4o-mini**

Everything is orchestrated through **LangGraph**, which handles the step-by-step workflow logic.

## ⚙️ Installation

You can install dependencies via **pip** or **poetry**.

### Prerequisites

Your `.env` file must include:

```
OPENAI_API_KEY=
NEWS_API_KEY=
TAVILY_API_KEY=      # optional (for the internet search variant)
```

### Install with pip

```
pip install langgraph langchain-openai newsapi-python beautifulsoup4 requests python-dotenv
```

### Install with poetry

```
poetry install
```

## 🚀 Usage

The workflow runs asynchronously—ideal for Jupyter notebooks or asyncio-based scripts.

### Import the runner

```python
from main import run_workflow
```

### Run a query

```python
import asyncio

query = "Apple iPhone 15"
result = await run_workflow(query, num_articles_tldr=3)

print(result)
```

The agent will return a structured summary of the top articles matching the query.

## 🔧 Workflow Nodes

The system’s internal **GraphState** moves through a small chain of carefully designed nodes. Each reflects a stage a real researcher would follow.

### 1. Generate Params

Creates optimized search parameters based on the query and past interactions.
`generate_newsapi_params(state)`

### 2. Retrieve Metadata

Queries News API and collects article metadata.
`retrieve_article_metadata(state)`

### 3. Scrape & Filter

Scrapes each URL, extracts readable text, and selects the most relevant articles.
`select_top_urls(state)`

### 4. Summarize

Runs multiple LLM summarization calls in parallel.
`summarize_articles_parallel(state)`

The result is a clean, tightly focused set of summaries tailored to your prompt.

## 🪟 Windows Terminal Notes

Windows CMD/PowerShell may choke on non-ASCII characters (smart quotes, emojis, etc.), producing:

```
UnicodeEncodeError: 'charmap' codec can't encode character '\u2019'
```

Fixes include:

• Set `PYTHONIOENCODING=utf-8`
• Install `win-unicode-console`:
`py -m pip install win-unicode-console`
• Run scripts under the unicode console wrapper.

Avoid forcing your terminal to always use UTF-8 globally—it can cause unrelated tools to behave oddly.

## 🤝 Support

Suggestions, improvements, and feedback are welcome.