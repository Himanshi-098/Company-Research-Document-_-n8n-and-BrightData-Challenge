# Sales-Ready Company Research Automation using n8n & Bright Data 

## Overview

The automation creates clean and detailed sales-ready research document of you lead and their company in under 12-15 minutes. This automation helps you research the company and generate a detailed report containing company details, financial information, recent developments, technology focus, and executive biography. 

---

## Features

- **Automated Lead Qualification**: Determines if leads are worth pursuing based on website scrapability and data availability
- **Company Data Enrichment**: Pulls revenue, employee count, industry, and founding information via Apollo.io
- **Website and Link Categorization**: Categorizes and scrapes relevant pages (About Us, Services, Financial Information)
- **News & Development Tracking**: Finds and summarizes recent company news and growth updates
- **Executive Research**: Locates and extracts LinkedIn profiles and their professional backgrounds
- **Document Generation**: Creates structured and professional Google Docs with all research compiled
- **Slack Integration**: Sends qualification status with green/red flags analysis of each lead

---

## How it works (high level)

1. **Trigger (Part 3 - Main Automation)**
- Lead submits form
- Google Sheets is updated with name, email, website, call time 
- Kick off the main n8n flow

2. **Part 1 (Automation 1) — URL Health & Enrichment**
- Check website health (robots, status, HTML fetch).
- If **scrapable**: enrich with Apollo (revenue, headcount, industry, founded, keywords).
- Scrape homepage via Bright Data; then AI agent auto-categorize links (About / Products & Services / Financials).
- AI picks the **best** link per category; BrightData scrape & AI summarize each.
- If **not scrapable**: try the email domain. If still blocked: create a Disqualified doc + Slack note with reason and stop.

3. **Part 2 (Automation 2) — News, Financials, LinkedIn** *(only for qualified leads)*
- Find **recent news** & **financial sources** via Bright Data Google search. AI agent selects the most relevant and BrightData scrape, followed by AI summarization.
- Find **person’s LinkedIn**; if found, run Bright Data batch extraction and summarizes the exec bio.

**Back to Main Automation (Part 3)** - Finally the AI agent composes a polished **Google Doc** and a **Slack update** content and automation updates the document in Google Drive link and updates the Slack message (Qualified/Disqualified + flags + doc link).

---

## Tools & Integrations

- **n8n**: Workflow automation platform
- **Apollo.io**: Company data enrichment
- **BrightData**: Web scraping and data extraction
- **Google Sheets**: Form data and email content storage
- **Google Drive**: Document generation and storage
- **Slack**: Team notifications
- **AI Agents**: Content analysis and selection

---

## Output Document Includes

- **Company Overview**: Basic company information and background
- **Financial Data**: Revenue, funding, and growth metrics
- **Recent Developments**: Latest news, partnerships, and company updates
- **Technology Focus**: Tech stack, industry positioning, and innovation areas
- **Executive Biography**: Key decision-maker profiles and professional background

**Slack Output**
-  Qualification Status: Lead assessment with green and red flags

---

## Prerequisites

- N8n instance with appropriate nodes installed
- Apollo.io API access
- BrightData account with scraping capabilities
- Google Workspace account (Sheets, Drive, Docs API)
- Slack workspace and bot permissions
- AI service integration (OpenAI, Claude, etc.)

## Configuration

1. Set up Google Sheets form integration
2. Configure Apollo.io API credentials
3. Set up BrightData scraping parameters
4. Configure Google Drive API permissions
5. Set up Slack bot and channel integrations
6. Configure AI agent parameters and prompts

## Performance Metrics

- **Processing Time**: Under 20 minutes per lead
- **Data Quality**: Comprehensive research equivalent to 2+ hours of manual work

## Error Handling

- Website health checks prevent processing failures
- Fallback mechanisms for non-scrapable primary websites
- Clear disqualification reasons provided
- Graceful handling of missing LinkedIn profiles or news

---
##  Demo / Live Access

Demo Video: https://youtu.be/wQQpV7MnlCE

---

##  Architecture Diagram

**n8n workflows**: 

<img width="1654" height="789" alt="image" src="https://github.com/user-attachments/assets/f3f12af2-2363-49c5-b30e-263096f44d46" />

---

<img width="1488" height="842" alt="image" src="https://github.com/user-attachments/assets/02babe7b-ac13-439b-9013-a08065e821e1" />

---

<img width="1068" height="545" alt="image" src="https://github.com/user-attachments/assets/c0a3ad63-8176-48ba-bc17-8dd0786c6317" />

---

**Slack Output**: 

<img width="1194" height="338" alt="image" src="https://github.com/user-attachments/assets/5774ce45-e62c-4ab3-a0dc-5676b9161a69" />

