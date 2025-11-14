<h1><b>PhishGuard</b></h1>
<h3>An AI-Powered Real-Time Phishing Detection System for Safe Web Browsing</h3>

<p>
Detecting phishing after the breach is too late — <b>PhishGuard</b> protects you before you click.<br>
PhishGuard introduces an intelligent Chrome extension that combines <b>Large Language Models (LLMs)</b>, <b>VirusTotal threat intelligence</b>, and <b>real-time web analysis</b> to identify malicious websites with streaming AI-powered assessments.
</p>

<p>
  <img src="https://img.shields.io/badge/Status-Production%20Ready-brightgreen?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Python-3.10+-skyblue?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Chrome-Extension-orange?style=for-the-badge&logo=googlechrome"/>
  <img src="https://img.shields.io/badge/AI-Powered-purple?style=for-the-badge&logo=openai"/>
  <img src="https://img.shields.io/badge/License-MIT-blue?style=for-the-badge"/>
</p>

---

## Overview

PhishGuard answers a critical cybersecurity question:

> **"How do we detect sophisticated phishing attacks in real-time before users submit their credentials?"**

Using advanced AI models and multi-source threat intelligence, this project:

- Analyzes webpage content using <b>NVIDIA Llama 3.3 Nemotron Super 49B</b>
- Cross-references threats with <b>VirusTotal's crowd-sourced database</b>
- Provides <b>streaming real-time risk assessments</b> with confidence scores
- Detects <b>brand impersonation, credential harvesting, and domain spoofing</b>
- Delivers <b>instant visual alerts</b> with color-coded risk indicators
- Operates seamlessly as a <b>Chrome browser extension</b>

This project is **production-ready**, **AI-native**, and designed for real-world cybersecurity protection.

---

## Key Features

| Category                  | Description                                                              |
| ------------------------- | ------------------------------------------------------------------------ |
| **AI Analysis**           | Dual LLM pipeline with NVIDIA Llama 3.3 (49B) + Llama 3.1 (405B)        |
| **Threat Intelligence**   | VirusTotal API v3 integration for malware detection                      |
| **Real-Time Detection**   | Streaming NDJSON responses with live status updates                      |
| **Multi-Criteria Scoring**| Brand accuracy, credential harvesting, URL manipulation, CTA patterns    |
| **Risk Categorization**   | Safe (<25%), Suspicious (25-60%), Dangerous (>60%)                       |
| **User Experience**       | One-click analysis, auto-scan, Chrome notifications, scan history        |
| **Performance**           | Local caching (1-hour validity), processes 120K characters of HTML       |

---

## Architecture

<p>
<a href="https://github.com/cse543-project/ai-based-phishing-detection">
  <img src="https://img.shields.io/badge/GitHub-Repository-blue?style=for-the-badge&logo=github" />
</a>
</p>

**Multi-Stage AI Pipeline:**

```
User Browser (Chrome Extension)
    ↓
popup.js / background.js (Manifest V3)
    ↓
FastAPI Backend (localhost:8000)
    ↓
LangGraph Workflow State Machine
    ├── Stage 1: extract_urls → Playwright HTML Scraping
    ├── Stage 2: process_with_llm → Content Analysis (Llama 3.3)
    ├── Stage 3: phishing_prediction → Initial Risk Scoring (Llama 3.1)
    ├── Stage 4: get_vt_result → VirusTotal API Threat Check
    ├── Stage 5: output → Score Aggregation
    └── Stage 6: final → Confidence Percentage Extraction
    ↓
Streaming Response (NDJSON Format)
    ↓
Visual Risk Display (Color-Coded Alerts)
```

---

## Detection Pipeline

<table>
<tr>
<td width="50%" valign="top">

### **1. Content Extraction**
- Headless browser automation (Playwright)
- Full HTML content capture
- JavaScript execution support
- HTTP status code validation

</td>
<td width="50%" valign="top">

### **2. AI Analysis**
- Brand impersonation detection
- Credential harvesting patterns
- Call-to-action urgency analysis
- URL manipulation identification

</td>
</tr>

<tr>
<td width="50%" valign="top">

### **3. Threat Intelligence**
- VirusTotal database lookup
- Malicious/suspicious vote aggregation
- Historical threat correlation
- Community flagging verification

</td>
<td width="50%" valign="top">

### **4. Risk Scoring**
- Multi-source score aggregation
- Confidence percentage (0-100%)
- Detailed reasoning extraction
- Real-time streaming results

</td>
</tr>
</table>

---

## AI Models & Analysis

### **Primary AI Models**

| Model | Purpose | Parameters | Temperature |
|-------|---------|------------|-------------|
| **NVIDIA Llama 3.3 Nemotron Super 49B** | HTML Content Analysis | 49 Billion | 0.6 |
| **Meta Llama 3.1 405B Instruct** | Phishing Prediction | 405 Billion | 0.3 |

### **Phishing Detection Criteria**

The AI evaluates websites across **5 critical dimensions**:

1. **Brand Accuracy (0-10 scale)**
   - Detects impersonation of legitimate brands
   - Analyzes logo usage, color schemes, typography
   - Flags domain name mismatches

2. **Credential Harvesting**
   - Identifies suspicious form fields
   - Detects requests for sensitive information
   - Analyzes input field patterns

3. **Call-to-Action Patterns**
   - Spots urgency tactics ("Act Now!", "Limited Time")
   - Flags threatening language
   - Identifies social engineering techniques

4. **URL Manipulation**
   - Detects typosquatting
   - Identifies homograph attacks
   - Flags subdomain spoofing

5. **VirusTotal Intelligence**
   - Cross-checks with 70+ security vendors
   - Aggregates malicious/suspicious flags
   - Validates community reports

---

## Risk Classification System

### **Three-Tier Risk Model**

| Risk Level | Score Range | Visual Indicator | Action |
|-----------|-------------|------------------|--------|
| **Safe** | 0-24% | 🟢 Green Badge | No action required |
| **Suspicious** | 25-60% | 🟡 Yellow Badge | Proceed with caution |
| **Dangerous** | 61-100% | 🔴 Red Badge | Block + Chrome notification |

---

## Extension Features

<table>
<tr>
<td width="50%" valign="top">

### **User Interface**
- One-click analysis from toolbar
- Real-time streaming status updates
- Color-coded risk visualization
- Detailed reasoning display
- Scan history (last 100 results)

</td>
<td width="50%" valign="top">

### **Smart Configuration**
- Auto-scan on page load (toggle)
- Chrome notification alerts (toggle)
- Adjustable risk thresholds
- 1-hour result caching
- Background service worker

</td>
</tr>
</table>

---

## Performance Characteristics

| Metric | Value | Description |
|--------|-------|-------------|
| **Max HTML Processing** | 120,000 characters | Full page analysis capability |
| **Cache Duration** | 1 hour | Reduces API load for repeat visits |
| **Scan History** | Last 100 results | Persistent local storage |
| **VirusTotal Delay** | 10 seconds | Analysis completion wait time |
| **Response Format** | NDJSON Streaming | Real-time progressive updates |
| **LLM Temperature** | 0.3-0.6 | Balanced creativity/determinism |
| **Max Tokens** | 16-4096 | Context-dependent generation |

---

## Tech Stack

<p>
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" height="45" />
<img src="https://fastapi.tiangolo.com/img/logo-margin/logo-teal.png" height="45" />
<img src="https://playwright.dev/img/playwright-logo.svg" height="45" />
<img src="https://raw.githubusercontent.com/langchain-ai/langgraph/main/docs/static/img/langgraph.png" height="45" />
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-original.svg" height="45" />
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/chrome/chrome-original.svg" height="45" />
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/git/git-original.svg" height="45" />
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/github/github-original.svg" height="45" />
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/vscode/vscode-original.svg" height="45" />
</p>

### **Backend Stack**
- **FastAPI** - High-performance async web framework
- **LangGraph** - Multi-agent AI workflow orchestration
- **LangChain** - LLM framework and prompt management
- **Playwright** - Headless browser automation
- **BeautifulSoup** - HTML parsing and extraction
- **OpenAI SDK** - NVIDIA AI endpoint integration
- **Uvicorn** - ASGI server for production deployment

### **Frontend Stack**
- **Chrome Extension Manifest V3** - Modern extension API
- **Vanilla JavaScript** - Lightweight, framework-free
- **CSS3 Custom Properties** - Themeable design system
- **NDJSON Streaming** - Progressive real-time updates

### **External APIs**
- **NVIDIA AI Endpoints** - Llama 3.3 Nemotron Super 49B inference
- **VirusTotal API v3** - Crowd-sourced threat intelligence

---

## Installation & Setup

### **Prerequisites**
```bash
Python 3.10+
Chrome Browser
NVIDIA API Key
VirusTotal API Key
```

### **Backend Setup**
```bash
cd ai-based-phishing-detection

# Install dependencies
pip install fastapi uvicorn langchain langgraph playwright beautifulsoup4 openai

# Install Playwright browsers
playwright install chromium

# Configure API keys (see Security Note below)
# Edit backend_api.py and add your keys to environment variables

# Start the API server
python backend_api.py
```

### **Chrome Extension Setup**
1. Open Chrome and navigate to `chrome://extensions/`
2. Enable **Developer mode** (top-right toggle)
3. Click **Load unpacked**
4. Select the `ai-based-phishing-detection` directory
5. Pin the PhishGuard extension to your toolbar

### **Security Note**
⚠️ **API keys are currently hardcoded in source files.** Before deployment, migrate to environment variables:

```python
import os
NVIDIA_API_KEY = os.getenv("NVIDIA_API_KEY")
VIRUSTOTAL_API_KEY = os.getenv("VIRUSTOTAL_API_KEY")
```

---

## Usage

### **Manual Analysis**
1. Navigate to any website
2. Click the PhishGuard icon in your toolbar
3. Click **"Analyze This Page"**
4. Watch the real-time streaming analysis
5. Review the risk score and reasoning

### **Auto-Scan Mode**
1. Click the PhishGuard icon
2. Enable **"Auto-scan on page load"**
3. Browse normally — PhishGuard automatically analyzes new pages
4. Receive Chrome notifications for high-risk sites

### **Configuration Options**
- **Auto-scan**: Toggle automatic background scanning
- **Notifications**: Enable/disable Chrome desktop alerts
- **High Risk Threshold**: Default 75% (configurable)
- **Medium Risk Threshold**: Default 50% (configurable)

---

## Research Directions

- **Federated learning** for privacy-preserving model updates
- **Browser fingerprinting** for advanced bot detection
- **OCR integration** for screenshot-based phishing analysis
- **Real-time URL reputation scoring** via blockchain consensus
- **Behavioral analysis** of form submission patterns
- **Multi-language phishing detection** with multilingual LLMs
- **Zero-day phishing detection** using anomaly-based ML
- **Integration with password managers** for credential protection
- **Enterprise deployment** with centralized threat dashboards

---

## Project Team

This project was developed by an 8-person team:

1. Sai Teja Alasyam
2. Akash Sateesha
3. Vishal Lakshmi Narayanan
4. Aarya Choudhary
5. Aditya Rallapalli
6. Ajita Bhardwaj
7. Lekshman Babu Devendra Babu
8. Maanesh Mohanraj

---

## Acknowledgements

**AI Models:**
- NVIDIA AI Endpoints (Llama 3.3 Nemotron Super 49B)
- Meta AI (Llama 3.1 405B Instruct)

**Threat Intelligence:**
- VirusTotal API v3 (Google Chronicle)

**Inspiration:**
Research inspired by cybersecurity best practices, phishing defense strategies, and real-time AI-powered threat detection systems.

---

## License

MIT License - See LICENSE file for details

---

## Contributing

Contributions are welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

---

## Citation

If you use PhishGuard in your research, please cite:

```bibtex
@software{phishguard2024,
  title = {PhishGuard: AI-Powered Real-Time Phishing Detection},
  author = {Alasyam, Sai Teja and Sateesha, Akash and Narayanan, Vishal Lakshmi and
            Choudhary, Aarya and Rallapalli, Aditya and Bhardwaj, Ajita and
            Babu, Lekshman Babu Devendra and Mohanraj, Maanesh},
  year = {2024},
  url = {https://github.com/cse543-project/ai-based-phishing-detection}
}
```

---

<p
