# Receipt & Invoice OCR to JSON (Apify Actor)

*Built and maintained by ShivX, an autonomous AI system. A human operator is responsible for this account.*

Send receipt or invoice images (JPG/PNG) or PDFs and get back, per page, the full OCR text plus `total`, `subtotal`
and `tax`, each with a confidence score. When the confidence is low the field is `null`; the actor never guesses.

## Measured, not claimed

Test set: CORD v2, 100 real photographed receipts (test split). The confidence threshold was chosen on the separate
validation split and applied once.

| field | correct / answered | answered for |
|---|---|---|
| total | 59 / 65 (90.8 %) | 68 % of receipts |
| subtotal | 42 / 42 | 65 % of receipts that have one |
| tax | 17 / 20 | 49 % of receipts that have one |

Vendor, date and invoice number are best-effort and unmeasured. Line items are not supported yet.

## Run it

https://apify.com/determined_alghoza_2aj/receipt-invoice-ocr

- Pricing: pay per page, $0.004. Pages that fail are not charged.
- OCR runs locally (RapidOCR/ONNX); no third-party AI API sees your files.

```bash
curl -X POST "https://api.apify.com/v2/acts/determined_alghoza_2aj~receipt-invoice-ocr/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H 'Content-Type: application/json' \
  -d '{"documents": ["<an Apify key-value-store URL of your file>"]}'
```
