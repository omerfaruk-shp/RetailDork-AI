# Ultimate Price & Link Scraper

A bot that finds the cheapest price for any product on Turkish shopping sites, saves everything to an Excel file, and optionally asks an AI to analyze the results for you.

## What This Bot Does

1. You type a product name (e.g. "iPhone 15" or "Samsung TV")
2. It opens Google and searches 12 different Turkish shopping sites automatically
3. It collects product names, prices, and clickable links
4. It filters out second-hand items and accessories automatically
5. It saves everything into a clean Excel file sorted by price (cheapest first)
6. Optionally, it sends the data to a local AI and prints a plain Turkish summary

---

## Installation (Step by Step)

### 1. Install Python 3

Make sure you have Python 3.9 or newer installed:

```bash
python3 --version
```

If you don't have Python, download it from [python.org](https://www.python.org/downloads/).

### 2. Install Required Libraries

Open a terminal and run these commands one by one:

```bash
pip install playwright
pip install pandas
pip install beautifulsoup4
pip install openpyxl
pip install ascii_magic
pip install openai
```

After that, install the Chromium browser that Playwright needs:

```bash
playwright install chromium
```

> **Troubleshooting:** If `pip` doesn't work (e.g. on macOS), try `pip3` instead. If you get permission errors, add `--user` at the end.

### 3. (Optional) Install Ollama for AI Analysis

The bot can ask an AI to analyze the prices. This step is **optional** — the Excel file will be generated either way.

**What is Ollama?** It's a free program that lets you run AI models on your own computer (no internet needed, no monthly fees).

**Installation:**

- Go to [ollama.com](https://ollama.com)
- Click "Download" and choose your operating system
- Install it like any normal program
- After installation, open a terminal and run:

```bash
ollama pull gemma4:12b
```

This downloads the AI model (about 7GB). It may take a while depending on your internet speed.

> ⚠️ Make sure Ollama is **running in the background** before you start the scraper. On macOS/Linux, just leave the terminal window open after installing. On Windows, Ollama runs as a system service automatically.

---

## Usage

```bash
python3 scraper.py
```

### What Happens When You Run It:

1. **ASCII Art** – A picture shows up in the terminal (requires `meliodas.jpg` in the same folder). After a few seconds, the screen clears.
2. **Product Prompt** – You will see:

   ```
   Aratılacak Ürün / Model:
   ```

   Type the product you want to search for (e.g. `Samsung Galaxy S24`) and press Enter.

3. **Browser Opens** – A Google Chrome window will open automatically. This is normal.

4. **CAPTCHA Check** – The program pauses and waits for you. Look at the browser window:
   - If there is a "I am not a robot" checkbox → click it and solve any puzzles
   - If the page looks normal → just go back to the terminal

5. **Press Enter** – Once you are ready, go back to the terminal and press Enter. The scraping begins.

6. **Watch It Work** – The terminal shows live progress:
   ```
   🔍 [DORK TARAMA] Akakçe -> 'site:akakce.com "Samsung Galaxy S24"'
      ↳ 3 valid links and prices found.
   🛒 [GOOGLE SHOPPING FEED] Scanning...
      ↳ Page 1: 5 products added.
   ```

7. **Excel File** – When done, you will see:
   ```
   📊 EXCEL FILE SUCCESSFULLY CREATED!
   📦 Products Found: 23
   📁 File Path: /Users/yourname/samsung_galaxy_s24_ucuz_fiyat_listesi.xlsx
   ```

8. **AI Report** – If Ollama is installed, a short price analysis is printed in the terminal.

---

## Output: The Excel File

The file is saved in the same folder where you ran the script.

**File name format:** `{product_name}_ucuz_fiyat_listesi.xlsx`

Example: `samsung_galaxy_s24_ucuz_fiyat_listesi.xlsx`

**What's inside:**

| Column | What it means |
|---|---|
| Platform / Satıcı | The website or seller name (e.g. Trendyol, Akakçe) |
| Ürün Başlığı | The full product title from the listing |
| Fiyat | The price in TL |
| Puan | Source type ("Web İlanı" or "Alışveriş Sekmesi") |
| Ürün Linki | A clickable link that says "Tıkla & Git 🔗" |

Rows are sorted from cheapest to most expensive.

---

## How the Filtering Works

The bot blocks listings that contain these keywords (unless your search term also contains them):

`kılıf`, `kaplama`, `çanta`, `koruyucu`, `sticker`, `yedek parça`, `tamir`, `kablo`, `ikinci el`, `kullanılmış`, `teşhir`, `outlet`, etc.

This means accessories, cases, repair parts, and second-hand items are automatically excluded so you only see new products.

---

## Configuration Details for Developers

### Target Sites

You can edit the `self.target_sites` list inside the `__init__` method to add or remove platforms.

### Noise Keywords

The `self.noise_keywords` list controls which words trigger a listing to be filtered out. Customize it for your needs.

### AI Model

The bot uses `gemma4:12b` by default. If you want to use a different model:

```python
response = client.chat.completions.create(
    model="llama3",  # change this
    ...
)
```

### Browser Settings

The bot runs in **visible mode** (`headless=False`) because Google often blocks headless browsers. You can change this in `run_scraper()`:

```python
browser = await p.chromium.launch(headless=True)  # invisible mode (may get blocked)
```

---

## Troubleshooting

| Problem | Solution |
|---|---|
| `ModuleNotFoundError: No module named 'playwright'` | Run `pip install playwright` and `playwright install chromium` |
| Browser opens but does nothing | Check for CAPTCHA and solve it, then press Enter |
| "No results found" for every site | Google may be blocking automated searches. Try a different VPN or wait a few hours |
| `FileNotFoundError: meliodas.jpg` | Either place an image named `meliodas.jpg` in the folder, or remove the `ascii_art_work()` call |
| AI analysis prints an error | Make sure Ollama is running (`ollama list` in terminal). If not, run `ollama serve` |
| Excel file has no clickable links | Make sure the URLs in the scraped results start with `http://` or `https://` |

---

## Known Limitations

- Google may show CAPTCHA, requiring manual interaction
- If Google updates its HTML structure, the CSS selectors may stop working and need updating
- Price extraction only works with TL/₺ formatted prices
- The AI model must be downloaded beforehand (~7GB for `gemma4:12b`)
