# Ultimate Price & Link Scraper

A Google Shopping and Google Web Dork-based price comparison bot that scrapes Turkish e-commerce platforms to identify the lowest prices for a given product and exports structured results to a formatted Excel workbook with optional local LLM analysis.

## Features

- **Google Web Dork Scraping** – Performs `site:` restricted searches across 12 Turkish e-commerce domains (Akakçe, Cimri, Trendyol, Hepsiburada, Amazon TR, N11, PttAVM, Pazarama, Çiçeksepeti, Teknosa, Vatan Bilgisayar, Epey)
- **Google Shopping Feed Scraping** – Queries the Google Shopping tab (`udm=28`) with pagination support
- **Noise Filtering** – Automatically excludes second-hand listings, accessories, cases, replacement parts, and other irrelevant results via keyword blacklist
- **Price Parsing** – Extracts TL/₺ formatted prices using regex and sorts results numerically
- **Excel Export** – Generates a professionally formatted `.xlsx` file with sorted prices, clickable hyperlinks, styled headers, and auto-sized columns
- **Local AI Analysis** – Sends top results to a local Gemma model via Ollama for natural language price/performance recommendations

## Requirements

```bash
pip install playwright pandas beautifulsoup4 openpyxl ascii_magic openai
playwright install chromium
```

Optional – local AI analysis:
- [Ollama](https://ollama.com) must be running
- Pull the model: `ollama pull gemma4:12b`

## Usage

```bash
python scraper.py
```

The program will:
1. Display an ASCII art splash screen from `meliodas.jpg`
2. Prompt for the target product name
3. Open a visible Chromium browser window for CAPTCHA/manual verification
4. Wait for the user to press Enter to begin scraping
5. Execute site-specific dork searches and Google Shopping feed scans
6. Export deduplicated, price-sorted results to Excel
7. Optionally generate an AI analysis report via the local Ollama endpoint

## Output

- File: `{product_slug}_ucuz_fiyat_listesi.xlsx`
- Sheet: `Fiyat Listesi` (Price List)
- Sorted ascending by parsed numeric price
- Hyperlinked product URLs with "Tıkla & Git 🔗" label
- Dark blue header row with white bold text
- Auto-adjusted column widths (capped at 50 characters)

## Architecture

```text
┌──────────────────────────────────────────────────┐
│  UltimatePriceAndLinkScraper                     │
│  ┌───────────────────────────────────────────┐   │
│  │ Google Web Dorks (12 sites)               │   │
│  │   └─ site:akakce.com "product"            │   │
│  │   └─ site:trendyol.com "product"          │   │
│  │   └─ ...                                  │   │
│  ├───────────────────────────────────────────┤   │
│  │ Google Shopping Feed (udm=28, 3 pages)    │   │
│  ├───────────────────────────────────────────┤   │
│  │ Noise Filter → Price Parser → Dedup       │   │
│  ├───────────────────────────────────────────┤   │
│  │ Excel Export (openpyxl)                   │   │
│  │ AI Analysis (Ollama / OpenAI-compatible)  │   │
│  └───────────────────────────────────────────┘   │
└──────────────────────────────────────────────────┘
```

## Target Platforms

| Platform | Domain |
|---|---|
| Akakçe (Best Price) | akakce.com |
| Cimri (Best Price) | cimri.com |
| Epey | epey.com |
| Trendyol | trendyol.com |
| Hepsiburada | hepsiburada.com |
| Amazon TR | amazon.com.tr |
| N11 | n11.com |
| PttAVM | pttavm.com |
| Pazarama | pazarama.com |
| Çiçeksepeti | ciceksepeti.com |
| Teknosa | teknosa.com |
| Vatan Bilgisayar | vatanbilgisayar.com |

## Configuration

The `LOCAL_API_URL` defaults to `http://localhost:11434/v1` (Ollama). Update the `model` parameter in `analyze_with_local_ai()` to match your downloaded model.

The `noise_keywords` list in `__init__` controls which listing types are filtered out. Extend or modify for domain-specific requirements.

## Limitations

- Google CAPTCHA may require manual intervention (browser runs in non-headless mode)
- CSS selectors are tied to Google's current DOM structure and may require updates over time
- Price extraction accuracy depends on consistent TL/₺ formatting in search snippets
- AI analysis requires Ollama to be installed and running separately
