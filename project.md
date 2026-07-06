---
layout: page
title: Projects
subtitle: What I've built
---

### Stock Intelligence Pipeline

AI-powered daily stock screening and paper trading system. Claude analyzes 2,700+ stocks every morning, picks swing trades, and tracks performance with real money simulation.

**Live:** [kai-ion.github.io/stock-intelligence](https://kai-ion.github.io/stock-intelligence/)
**Code:** [github.com/kai-ion/stock-intelligence](https://github.com/kai-ion/stock-intelligence)

- Screens 2,700+ US stocks daily using NASDAQ API + yfinance with S&P 500 priority coverage
- Claude (via AWS Bedrock) generates a daily brief with top picks, entry/exit targets, and market analysis
- Paper trading simulator tracks P&L with automated position management (fibonacci targets, stop losses)
- Short screener identifies bearish setups with entry/cover/stop levels
- Automated EC2 pipeline: screener → Claude analysis → email → blog publish (Jekyll + GitHub Pages)
- **Tech:** Python, AWS (EC2, Bedrock, SES, S3, EventBridge), yfinance, Jekyll, GitHub Actions

---

### Sports Betting Analysis

AI-powered prop betting picks for NBA, WNBA, and MLB with quantitative edge scoring and Claude validation.

**Live:** [kai-ion.github.io/sports-betting](https://kai-ion.github.io/sports-betting/)
**Code:** [github.com/kai-ion/sports-betting](https://github.com/kai-ion/sports-betting)

- Fetches player props from BettingPros + Underdog Fantasy, projects stats from ESPN game logs
- Quantitative edge scoring (weighted L5/L10/season averages) identifies value bets
- Claude validates top edges and assigns confidence scores
- Enforces 50/50 OVER/UNDER balance for diversified picks
- Smart scheduling: checks ESPN scoreboard daily, skips offseason sports automatically
- Daily email + automated blog publish via GitHub Pages
- **Tech:** Python, AWS Bedrock, ESPN API, BettingPros, Playwright, Jekyll, GitHub Actions

---

### Job Application Tracker

Automatically tracks job applications and rejections from Gmail into a Google Sheet using Apps Script.

**Code:** [github.com/kai-ion/job-tracker](https://github.com/kai-ion/job-tracker)
**Try it:** [Make a copy](https://docs.google.com/spreadsheets/d/1FFnhnMLu72CPy3UhypF7zin0r7JleOVKXGBP7aPQhYs/copy)

- Scans Gmail every 5 minutes for application confirmations and rejection emails
- Extracts company name, role, and source (LinkedIn, Indeed, Greenhouse, Lever, etc.)
- Detects rejections even in threaded replies with fuzzy company matching
- Handles multiple applications to the same company (different roles)
- Supports multi-word companies (Weights & Biases, Goldman Sachs) and ATS platforms (Greenhouse, iCIMS, Lever)
- Notion database integration available as alternative backend
- **Tech:** Google Apps Script, Gmail API, Google Sheets, clasp CLI

---

### Previous Projects

**Slack AI Chatbot** (2025) — [GitHub](https://github.com/kai-ion)
- AI chatbot with Django + Defy AI for real-time interactions on web and Slack
- Deployed on AWS (EC2, Lambda, API Gateway, S3, PostgreSQL, NGINX, Docker)

**Stock Prediction WebApp** (2024) — [Demo](https://kaiion-stock-prediction-webapp.streamlit.app/) | [GitHub](https://github.com/kai-ion/Stock-Prediction-WebApp)
- SVR model trained on Google Finance data to predict stock prices
- Sentiment analysis of real-time stock tweets (85% accuracy) using Tweepy and TextBlob

**Odin Project** — [GitHub](https://github.com/kai-ion/Odin-Project)
- [Odin Recipes](https://kai-ion.github.io/odin-recipes/)
- [Odin Landing Page](https://kai-ion.github.io/odin-landing-page/)
