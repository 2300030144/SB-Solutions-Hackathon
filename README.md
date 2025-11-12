# 💹 Financial Ratio Explanation Tutor (Backend)

## 📘 Overview
This project analyzes financial statements and explains key financial ratios using Google Gemini AI.  
It acts as a financial tutor — computing ratios like Gross Margin, Net Profit Margin, Current Ratio, DSCR, etc.,  
and explaining what they mean in simple language.

---

## ⚙️ Tech Stack
- **Language:** Python
- **Framework:** FastAPI
- **Libraries:** pandas, python-dotenv, google-generativeai, uvicorn
- **Model:** Google Gemini 2.5 Flash (via API)
- **Environment:** Local

---

## 🧱 Files
| File | Purpose |
|------|----------|
| `main.py` | FastAPI app — endpoints for upload, analysis, and chat |
| `financial_parser.py` | Handles data extraction & ratio computation |
| `requirements.txt` | List of dependencies |
| `.env.example` | Placeholder for your API key |
| `sample_financials.csv` | Example test data |

---

## 🚀 How to Run Locally
1. Install dependencies:
   ```bash
   pip install -r requirements.txt
