SignalTrace V2 — Run Instructions

Requirements

Python 3.10 or newer.

Installation

Install dependencies:

python -m pip install -r requirements.txt

Gemini API Setup

Create a .env file in the project directory:

GEMINI_API_KEY=YOUR_GEMINI_API_KEY

Do not share or submit your actual API key.

Run Offline Mode

python main.py \
  --payments data/challenge/payments.csv \
  --shipments data/challenge/shipments.jsonl \
  --complaints data/challenge/complaints.jsonl \
  --extractions data/challenge/extractions.json \
  --output result_offline.json

Offline mode uses supplied extraction fixtures and makes no LLM API requests.

Run Live Gemini Mode

python main.py \
  --payments data/sample/payments.csv \
  --shipments data/sample/shipments.jsonl \
  --complaints data/sample/complaints.jsonl \
  --output result_live.json

The default live model is gemini-3.5-flash-lite.

You can select another model using --model MODEL_NAME.

Output

Both modes generate JSON containing:

* Input validation statistics
* Number of LLM errors
* Investigation cases
* Validated issue and order ID
* Evidence-based verdict
* Supporting evidence IDs