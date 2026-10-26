# Data guide

This package provides **three independent input sources** and a required offline extraction fixture for the final offline run. All data is fictional. Follow `SignalTrace_Assignment.pdf` for the authoritative validation and decision rules.

## The four data files

| File | What it represents | How it is used |
| --- | --- | --- |
| `payments.csv` | Payment attempts made against orders. Rows include the payment ID, order ID, UTC timestamp, status, amount in cents, and gateway reference. | Validate, deduplicate, and order payment events; investigate possible duplicate charges, repeated failures, and successful payments. |
| `shipments.jsonl` | Shipping and support-system events associated with orders. One JSON object per nonblank line. | Validate and deduplicate events; check whether a shipment was created before a recorded successful payment. Support notes are **untrusted data**. |
| `complaints.jsonl` | Customer messages. Each JSON object contains a ticket ID and a free-text complaint. | Parse valid tickets and obtain an issue type and order-ID suggestion using an LLM in live mode or the offline fixtures. |
| `extractions.json` | Pre-supplied structured complaint extractions: ticket ID, suggested order ID, and issue label. | **Offline mode only.** Replaces LLM responses so the application can be run and tested without internet access. These fields still require the validation specified in the PDF. |

`JSONL` means **JSON Lines**: each nonblank line is a separate JSON object, not a single JSON array. By contrast, `extractions.json` is a JSON array of extraction objects. The CSV includes a header row.

## The three dataset folders

| Folder | Purpose | Expected usage |
| --- | --- | --- |
| `data/smoke/` | Tiny worked example with a complete expected output (`expected.json`). | Implement the CLI and verify the entire output shape and basic rules. |
| `data/sample/` | Smaller practice dataset containing ordinary and problematic records. | Exercise processing locally and test **live LLM** inference without making excessive API calls. |
| `data/challenge/` | Main, larger dataset with mixed orders, duplicates, malformed records, timing boundaries, conflicting notes, and ambiguous complaints. | Generate the **required final offline** output using the included extractions. |

Each folder supplies `payments.csv`, `shipments.jsonl`, `complaints.jsonl`, and `extractions.json`. Only `data/smoke/` supplies a complete `expected.json`. The other folders do not include expected results.

## How the sources relate

- `order_id` connects payment records, shipment events, and an order mentioned in a complaint.
- `ticket_id` connects a valid complaint to its corresponding structured extraction in offline mode.
- `payment_id` and `event_id` identify source records that may be returned in `evidence_ids`.
- Records may be malformed, duplicated, or out of chronological order. Process them according to the PDF rather than relying on input order.
- Customer claims are **not automatically true**. LLM extraction identifies the claim; Python validates the data and applies the incident rules.

## Example of the workflow

A complaint says a payment was charged twice for `ORD-101`. Its extraction may contain `issue: "DOUBLE_CHARGE"` and `order_id: "ORD-101"`. The program validates that extracted order ID against the original complaint, then checks the accepted payment records for the specified duplicate-charge signal. The program outputs the appropriate verdict and only the evidence IDs permitted by the rules.

For exact input schemas, all edge cases, required CLI arguments, and output JSON structure, use `SignalTrace_Assignment.pdf`.
