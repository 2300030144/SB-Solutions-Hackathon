Financial Ratio Explanation Tutor — Backend
1. Overview

This backend is the analytical engine for the Financial Ratio Explanation Tutor project.
It processes uploaded financial data (single or dual CSVs), computes financial ratios, and generates AI-based explanations using Google Gemini.
The backend exposes multiple endpoints that can be consumed by a frontend client (Streamlit in this case).

2. Objectives

Parse balance sheet and profit & loss (P&L) data.

Compute essential financial ratios from raw CSV files.

Use AI (Gemini) to generate human-understandable explanations.

Expose REST endpoints for analysis, explanation, and chat interaction.

Support both single combined and dual (separate) CSV upload workflows.

3. Architecture Overview

The backend is built on a modular architecture using FastAPI.
Each major process is divided into separate functional modules:

Layer	Function
main.py	FastAPI application entry point and API routing
financial_parser.py	Handles CSV data extraction and ratio calculations
requirements.txt	Dependencies
.env	Environment variable for Gemini API key
sample_financials.csv	Example test data

Data flow between modules:

Client Upload → FastAPI Endpoint → CSV Parser → Ratio Calculator → Gemini Explanation → JSON Response

4. Technologies Used
Component	Technology
Language	Python 3.10+
Framework	FastAPI
AI Model	Google Gemini 2.5 Flash
Libraries	pandas, python-dotenv, google-generativeai, uvicorn
Server	Uvicorn (ASGI)
Output Format	JSON
5. API Endpoints
5.1 /

Method: GET
Purpose: Health check endpoint.
Response:

{"message": "Financial Ratio Tutor Backend is running!"}

5.2 /analyze/

Method: POST
Purpose: Analyze a single combined financial CSV.
Input: file (CSV file)
Output:

{
  "ratios": {"Gross Margin": 0.45, "Net Profit Margin": 0.20, ...},
  "status": {"Gross Margin": "good", ...},
  "explanations": {"Gross Margin": "Healthy margin ..."}
}

5.3 /analyze_dual/

Method: POST
Purpose: Analyze separate P&L and Balance Sheet CSV files.
Input:

pnl: Profit & Loss CSV

balance: Balance Sheet CSV
Output: Same as /analyze/.

5.4 /explain/

Method: POST
Purpose: Request Gemini to explain ratios.
Input:

{"ratios": {"Gross Margin": 0.4, "Current Ratio": 2.5}}


Output:

{"explanation": "Gross Margin indicates strong pricing efficiency..."}

5.5 /chat/

Method: POST
Purpose: Allow Q&A-style interaction with Gemini (for ratio terms or insights).
Input:

{"message": "What is DSCR?", "ratios": {"DSCR": 12.2}}


Output:

{"reply": "DSCR measures the company's ability to service its debt."}

6. Key Ratios Computed
Ratio	Formula	Significance
Gross Margin	(Revenue - COGS) / Revenue	Profitability before expenses
Net Profit Margin	Net Profit / Revenue	Overall profitability
Current Ratio	Current Assets / Current Liabilities	Liquidity measure
Debt-Equity Ratio	Total Debt / Shareholder Equity	Leverage and financial stability
DSCR	Operating Income / Debt Obligations	Debt service capacity
7. Environment Configuration
.env File
GEMINI_API_KEY=your_google_gemini_api_key_here


Obtain an API key from Google AI Studio
.

8. Installation and Setup
Step 1: Install dependencies
pip install -r requirements.txt

Step 2: Run the FastAPI server
uvicorn main:app --reload

Step 3: Verify the server

Visit:

API root → http://127.0.0.1:8000

Docs → http://127.0.0.1:8000/docs

9. Data Flow

File Upload
User uploads either:

One combined financial CSV

Two separate CSVs (P&L and Balance Sheet)

File Processing
The parser:

Reads CSVs using pandas

Normalizes column names

Extracts key metrics (revenue, COGS, current assets, liabilities, etc.)

Ratio Calculation
Mathematical operations performed for all key ratios.
Invalid or missing values are handled gracefully with "—" placeholders.

AI Explanation
Ratios are formatted into a prompt and sent to Gemini.
Gemini returns plain-language explanations and improvement suggestions.

Response Formation
The results (ratios, statuses, explanations) are bundled into a structured JSON response.

Frontend Consumption
Streamlit frontend displays the data in cards, charts, and text sections.

10. Future Extensions

Add trend-based ratio comparison (multi-year analysis).

Include cash flow and efficiency ratios.

Integrate external financial benchmarks.

Enable database persistence for uploaded reports.

Support user authentication and API tokens.
