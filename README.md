💹 Financial Ratio Explanation Tutor — Backend (FastAPI)
📘 Overview

The Financial Ratio Explanation Tutor is an intelligent financial analysis backend built using FastAPI.
It processes uploaded Balance Sheets and Profit & Loss Statements (P&L), calculates key financial ratios,
and provides AI-powered explanations using Google Gemini 2.5 Flash.

It serves as the backend engine for the Streamlit Frontend, powering features such as:

Automated ratio computation 📊

AI-driven ratio explanations 🤖

Financial health summary generation 💬

Interactive Q&A with Gemini Chat 💡

🧠 Key Features
Feature	Description
📄 CSV Upload Support	Accepts single combined CSV or separate Balance Sheet and P&L files.
📊 Automated Ratio Computation	Calculates common financial ratios like Gross Margin, Net Profit Margin, Current Ratio, Debt-Equity, and DSCR.
🧮 Smart Data Parsing	Extracts financial fields dynamically (works with slightly varied column names).
🤖 AI-Powered Explanations	Uses Gemini API to explain each ratio in plain English.
💬 Chat Interface	Allows interactive Q&A — users can ask “What is DSCR?” or “Why is my current ratio low?”
🧾 Detailed JSON Response	Returns clean JSON outputs for frontend integration.
⚙️ Tech Stack
Component	Technology
Language	Python 3.10+
Framework	FastAPI
AI Model	Google Gemini 2.5 Flash
Server	Uvicorn
Libraries	pandas, python-dotenv, google-generativeai, uvicorn, fastapi, pydantic
Environment	Local or Cloud (e.g., Render, Railway, AWS EC2)
🧱 Folder & File Structure
📦 backend
│
├── main.py                     # FastAPI main app
├── financial_parser.py         # Handles CSV parsing & ratio calculations
├── requirements.txt            # Dependencies
├── .env.example                # Template for your Gemini API key
├── sample_financials.csv       # Example input file for testing
└── README.md                   # Project documentation

🧩 Key Backend Endpoints
Endpoint	Method	Description	Input	Output
/	GET	Health check	—	{ "message": "Financial Ratio Tutor Backend is running!" }
/analyze/	POST	Upload and analyze a single combined CSV	file: CSV	JSON (ratios + explanations)
/analyze_dual/	POST	Upload separate Balance Sheet and P&L CSVs	balance.csv, pnl.csv	JSON (ratios + explanations)
/explain/	POST	Get AI-generated explanations for ratios	{ "ratios": {...} }	{ "explanation": "..." }
/chat/	POST	Chat-style interface with Gemini AI	{ "message": "...", "ratios": {...} }	{ "reply": "..." }
🧮 Supported Financial Ratios
Ratio	Formula	Description
Gross Margin	(Revenue − COGS) / Revenue	Measures core profitability before expenses.
Net Profit Margin	Net Profit / Revenue	Indicates how much profit remains from revenue.
Current Ratio	Current Assets / Current Liabilities	Shows liquidity and short-term financial health.
Debt-Equity Ratio	Total Debt / Shareholder Equity	Evaluates financial leverage.
DSCR (Debt Service Coverage Ratio)	Operating Income / Debt Obligations	Measures ability to cover debt payments.
🔐 Environment Variables

Create a .env file (from .env.example) in your backend directory:

GEMINI_API_KEY=your_google_gemini_api_key_here


You can get your key from the Google AI Studio
.

🚀 How to Run Locally
1️⃣ Clone the Project
git clone https://github.com/yourusername/financial-ratio-tutor.git
cd financial-ratio-tutor/backend

2️⃣ Install Dependencies
pip install -r requirements.txt


If you’re missing FastAPI or Uvicorn, install them manually:

pip install fastapi uvicorn google-generativeai python-dotenv pandas

3️⃣ Configure API Key

Copy .env.example → .env and update:

GEMINI_API_KEY=your_actual_gemini_key

4️⃣ Run the FastAPI Server
uvicorn main:app --reload


✅ Backend URL: http://127.0.0.1:8000

✅ Docs URL: http://127.0.0.1:8000/docs

🔍 Sample Test (Using sample_financials.csv)
curl -X POST "http://127.0.0.1:8000/analyze/" \
-F "file=@sample_financials.csv"


Expected Output:

{
  "ratios": {
    "Gross Margin": 0.45,
    "Net Profit Margin": 0.25,
    "Current Ratio": 2.3,
    "Debt-Equity Ratio": 0.4,
    "DSCR": 5.2
  },
  "status": {
    "Gross Margin": "good",
    "Net Profit Margin": "good"
  },
  "explanations": {
    "Gross Margin": "Healthy margin — indicates efficient production and strong pricing."
  }
}

🧠 How the AI Explanation Works
Step	Action
1️⃣	User uploads CSVs (either single or dual).
2️⃣	Backend parses financial data via financial_parser.py.
3️⃣	Ratios are computed and validated for missing/invalid data.
4️⃣	Results are sent to the Gemini API with a custom financial prompt.
5️⃣	Gemini generates explanations and insights in natural language.
6️⃣	JSON response is sent back to the frontend.
🧰 Example Prompt Sent to Gemini
You are a financial tutor. Explain the meaning and interpretation of these financial ratios in simple terms:
Gross Margin: 0.40
Net Profit Margin: 0.35
Current Ratio: 2.5
Debt-Equity Ratio: 0.3
DSCR: 10.2

Provide one paragraph per ratio, ending with actionable improvement suggestions.

🧾 Example AI Output
Gross Margin (0.40): A 40% margin shows strong control over production costs...
Net Profit Margin (0.35): Indicates excellent profitability...
Current Ratio (2.5): Suggests the company has ample liquidity...
Debt-Equity Ratio (0.3): Low leverage, implying a stable capital structure...
DSCR (10.2): The company can easily cover its debt obligations...

🧩 API Documentation

After running the backend, you can explore:

Docs Type	URL
Swagger UI	http://127.0.0.1:8000/docs

ReDoc	http://127.0.0.1:8000/redoc

Both provide an interface to test APIs interactively.

🧑‍💻 Developer Notes

This backend is designed to integrate seamlessly with the Streamlit frontend.

Handles both single and dual file uploads.

Built to be extensible — more ratios or AI models can be added easily.

Ideal for hackathons, financial education apps, or enterprise dashboards.

🏁 Future Enhancements

✅ Add support for Cash Flow Ratios
✅ Implement trend analysis (multi-year comparison)
✅ Add industry benchmarking using public datasets
✅ Deploy via Render / Railway / AWS

👨‍💻 Contributors

Team 150

SB Solutions Hackathon 2025

🏆 Acknowledgments

Special thanks to Sairajsri Business Solutions Pvt. Ltd.
for hosting the SB Solutions Hackathon 2025 and inspiring innovative AI-based financial tools.
