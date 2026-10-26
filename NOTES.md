SignalTrace V2 — Implementation Notes

Approach

I developed a Python command-line application to investigate customer complaints using payment transactions, shipment events, and structured AI extractions.

The application loads CSV and JSONL files, validates required fields, removes duplicate records, and sorts accepted events chronologically.

For complaint understanding, I integrated Google’s Gemini API. Gemini extracts the issue category and order ID, while Python independently validates the extracted information against the original complaint.

Three deterministic investigation rules detect potential duplicate charges, repeated payment failures within 10 minutes, and shipments created without an earlier successful payment.

The application supports offline fixture-based processing without network requests and live processing using Gemini. Results are exported as structured JSON with verdicts and supporting evidence IDs.

Testing

* Verified the offline smoke dataset against the supplied expected JSON: PASS.
* Processed 46 accepted complaints from the challenge dataset.
* Successfully processed 15 sample complaints using Gemini.
* Confirmed zero LLM errors in the final live test.

Known Limitations

The investigation depends on the completeness and accuracy of the supplied records. Missing transactions may affect the verdict. Live extraction also depends on Gemini API availability and model responses.

Technical Risk

Customer complaints may contain misleading instructions or ambiguous information. To reduce this risk, the application treats complaints as untrusted input, validates extracted order IDs, and prevents the LLM from making final investigation decisions.