# SignalTrace V2 — Candidate Instructions

**Start here:** Open `SignalTrace_Assignment.pdf` and read it completely. It contains the authoritative requirements, validation and incident rules, examples, and submission instructions. **Time limit: 120 minutes.**

## What is provided

```text
SignalTrace_Assignment.pdf       Full task instructions and output specification
README.md                        This start guide
DATA_GUIDE.md                    What each data file means and how the folders differ
API_SETUP.md                     LLM API setup and offline-mode instructions
NOTES_TEMPLATE.md                Optional outline for the required NOTES.md
.env.example                     Example environment variable names (no API keys)
data/
  smoke/
    payments.csv                 Tiny payment input
    shipments.jsonl              Tiny shipment input
    complaints.jsonl             Tiny complaint input
    extractions.json             Pre-supplied offline complaint extractions
    expected.json                Exact expected smoke-test result
  sample/
    payments.csv
    shipments.jsonl
    complaints.jsonl
    extractions.json             Smaller practice inputs for live LLM mode
  challenge/
    payments.csv
    shipments.jsonl
    complaints.jsonl
    extractions.json             Larger inputs for the required final offline result
```

**No application source code is provided. Create and implement `main.py` and any supporting Python files.** The input files and offline extractions are data, not solutions. The three datasets serve different purposes: `smoke` demonstrates expected behavior, `sample` supports smaller live API calls, and `challenge` is the required final offline run.

## What to do, in order

1. Read `SignalTrace_Assignment.pdf`, then `DATA_GUIDE.md`. Review the data files.
2. **Write** `main.py` to accept the required command-line flags, load and validate inputs, implement the Python evidence rules, and write the specified JSON output.
3. Implement `--extractions` offline mode first. It reads the supplied extraction JSON and **must not call an LLM API**.
4. Run the small smoke example and compare the JSON values with `data/smoke/expected.json`.
5. Run offline mode on `data/challenge/` and save `result_offline.json`.
6. Implement live LLM extraction. Test it with the smaller `data/sample/` inputs and save `result_live.json`, or describe an actual provider access failure in `NOTES.md`.
7. Submit a ZIP containing the Python source, dependency instructions, required outputs, and `NOTES.md` (maximum 250 words). Never submit API keys.

## Required example commands

**Smoke test (offline):**

```bash
python main.py --payments data/smoke/payments.csv --shipments data/smoke/shipments.jsonl --complaints data/smoke/complaints.jsonl --extractions data/smoke/extractions.json --output smoke_result.json
```

**Final dataset (offline, required):**

```bash
python main.py --payments data/challenge/payments.csv --shipments data/challenge/shipments.jsonl --complaints data/challenge/complaints.jsonl --extractions data/challenge/extractions.json --output result_offline.json
```

**LLM API mode (smaller dataset):**

```bash
python main.py --payments data/sample/payments.csv --shipments data/sample/shipments.jsonl --complaints data/sample/complaints.jsonl --output result_live.json
```

In live mode, configure an LLM API credential in an environment variable. A frontend is not required. Browser research, AI development assistants, and API inference are permitted. Complete the work individually, and be prepared to explain any code submitted.

If this README and the PDF appear inconsistent, follow the PDF.
