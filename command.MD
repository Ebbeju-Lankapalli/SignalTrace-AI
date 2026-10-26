## Offline Testing

python main.py \
  --payments data/challenge/payments.csv \
  --shipments data/challenge/shipments.jsonl \
  --complaints data/challenge/complaints.jsonl \
  --extractions data/challenge/extractions.json \
  --output result_offline.json

## Online Testing

python main.py \
  --payments data/sample/payments.csv \
  --shipments data/sample/shipments.jsonl \
  --complaints data/sample/complaints.jsonl \
  --output result_live.json