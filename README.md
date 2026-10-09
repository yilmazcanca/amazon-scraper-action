# Amazon Scraper & Price Monitor Action

Automated Amazon product extraction, real-time BuyBox monitoring, and pricing alert action powered by [Chaldia Labs](https://chaldialabs.com).

Bypasses Amazon WAF, bot blocks, and CAPTCHAs natively inside your GitHub Actions pipelines.

---

## Usage

Add this step to any GitHub Workflow (e.g., `.github/workflows/price-monitor.yml`):

```yaml
name: Monitor Amazon BuyBox

on:
  schedule:
    - cron: '0 */6 * * *' # Runs every 6 hours
  workflow_dispatch:

jobs:
  track:
    runs-on: ubuntu-latest
    steps:
      - name: Fetch Amazon Product
        id: amazon
        uses: chaldialabs/amazon-scraper-action@v1
        with:
          asin: 'B0FPXGC6YG'
          domain: 'com.tr'
          api_key: ${{ secrets.CHALDIA_API_KEY }}

      - name: Inspect Extracted Data
        run: |
          echo "Product: ${{ steps.amazon.outputs.title }}"
          echo "Current Price: ${{ steps.amazon.outputs.price }} ${{ steps.amazon.outputs.currency }}"
          echo "In Stock: ${{ steps.amazon.outputs.in_stock }}"
```

---

## Inputs

| Name | Required | Default | Description |
| :--- | :--- | :--- | :--- |
| `asin` | **Yes** | - | 10-character Amazon ASIN code. |
| `domain` | No | `com` | Target Amazon domain (`com`, `com.tr`, `de`, `co.uk`, etc.). |
| `api_key` | No | - | Your Chaldia Labs API key for high-volume requests. |

---

## Outputs

| Output | Description |
| :--- | :--- |
| `title` | Product title. |
| `price` | Extracted numerical price. |
| `currency` | Currency symbol/code (e.g., USD, EUR, TRY). |
| `in_stock` | Boolean string (`true`/`false`). |
| `raw_json` | Full structured JSON response payload. |

---

## Get an API Key

Get your free API key at [Chaldia Labs](https://chaldia-labs.vercel.app/).

## License

MIT © [Chaldia Labs](https://chaldia-labs.vercel.app/)
