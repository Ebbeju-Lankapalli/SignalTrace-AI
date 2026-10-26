# LLM API setup

Before running the application in live mode, verify that a model inference request works with an authorized account. Provider quotas and available models may change; select a currently supported model.

- Gemini: https://aistudio.google.com/apikey and https://ai.google.dev/gemini-api/docs
- Groq: https://console.groq.com/keys and https://console.groq.com/docs/api-reference
- NVIDIA: https://build.nvidia.com/ (optional; confirm availability)

Store credentials in environment variables such as `GEMINI_API_KEY` or `GROQ_API_KEY`. Do not place keys in code or submitted files.

Free API access is not guaranteed. The application must also support the specified offline `--extractions` mode. If live inference is unavailable, record the HTTP status or error class in `NOTES.md` and provide the tested offline output.

LLM inference requests made by the running application and AI-assisted development tools are allowed. Verify and understand the code you submit, and never expose your API credentials.
