# Secure LangChain Chatbot (chatbot.py) 🔐

This file documents `chatbot.py` — a Streamlit-based secure chat interface built with LangChain and OpenAI.

> Short: a small, safety-aware chatbot that uses a strict system prompt, prompt-injection detection, and output sanitization before showing LLM responses.

## Quick Features ✅

- Streamlit chat UI (`st.chat_input`, `st.chat_message`) with session-based history
- Prompt injection guard (`is_prompt_injection`) to block malicious inputs
- Response sanitization (`sanitize_output`) to redact sensitive phrases
- Uses `langchain_core.prompts.ChatPromptTemplate` for system/human templating
- Uses `langchain_openai.ChatOpenAI` (default: `gpt-3.5-turbo`) as the LLM
- Caches the LLM with `@st.cache_resource` for efficiency

## Requirements 🔧

Install dependencies listed in `requirements.txt`:

```bash
pip install -r requirements.txt
```

Make sure `python-dotenv` is available so `.env` is loaded.

## Setup ⚙️

1. Create a `.env` file in the repository root with your OpenAI key:

```env
OPENAI_API_KEY=sk-...
```

2. (Optional) Create and activate a virtual environment.

> Note: `chatbot.py` will raise a `ValueError` if `OPENAI_API_KEY` is not set.

## Run locally ▶️

Start the Streamlit app:

```bash
streamlit run chatbot.py
```

Open the displayed local URL (typically `http://localhost:8501`).


## Security & Safety 🔐

- `INJECTION_PATTERNS` contains typical prompt-injection signatures; matching input is blocked and a warning message is shown.
- `sanitize_output()` replaces phrases like "system prompt" and "internal rules" with `[redacted]` before display.

## Troubleshooting 🛠️

- If you see `ValueError: OPENAI_API_KEY not found`, ensure your `.env` contains `OPENAI_API_KEY` and that the app is launched from the repository root.
- If responses are missing or slow, check your API key limits and internet connectivity.

---
