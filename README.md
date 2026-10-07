# Ai-resume-assistant-
# 📄 ATS Resume Checker

Upload your resume (PDF, DOCX or TXT), optionally paste a job description, and get:

- An overall **ATS score** (0-100) and a per-section breakdown
- Strengths of your resume
- Prioritised, actionable **improvements** (High / Medium / Low)
- **Keywords** found and missing (matched against the job description if you add one)
- Formatting issues that can trip up ATS parsers

Built with **Streamlit** and **Google Gemini Flash**.

> The score is an AI estimate, not the output of a real ATS. Use it as guidance.

---

## Run locally

```bash
# 1. clone / download the project, then:
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt

# 2. set your Gemini API key (free key: https://aistudio.google.com/apikey)
export GEMINI_API_KEY="your-key-here"     # Windows PowerShell: $env:GEMINI_API_KEY="your-key-here"

# 3. run
streamlit run app.py
```

You can also skip step 2 and paste the key into the sidebar when the app opens.

## Configuration

| Name | Where | Purpose |
|------|-------|---------|
| `GEMINI_API_KEY` | env var or Streamlit secret | Your Gemini API key (required) |
| `MODEL_NAME` | env var or Streamlit secret | Optional. Defaults to `gemini-3.5-flash` |

For local secrets you can create `.streamlit/secrets.toml`:

```toml
GEMINI_API_KEY = "your-key-here"
```

**Never commit this file or your key to GitHub.**

## Deploy on Streamlit Community Cloud

1. Push this project to a GitHub repo (`app.py`, `requirements.txt`, `README.md` in the root).
2. Go to https://share.streamlit.io and sign in with GitHub.
3. Click **Create app** > **Deploy a public app from GitHub**.
4. Choose your repo, branch `main`, main file path `app.py`.
5. Open **Advanced settings**, pick Python 3.11 or 3.12, and in **Secrets** paste:
   ```toml
   GEMINI_API_KEY = "your-key-here"
   ```
6. Click **Deploy**.

## Project structure

```
app.py             # Streamlit app + Gemini call
requirements.txt   # Python dependencies
README.md          # This file
```

## Troubleshooting

- **"Almost no text could be extracted"**: your resume is probably a scanned image. Export a text-based PDF or DOCX.
- **"Model not found"**: set `MODEL_NAME` to a current Gemini Flash model name.
- **"Rate limit or quota reached"**: the free tier has limits, wait a minute and retry.
