# Uni-Clerkpyme Scraper

A lightweight Python scraper for extracting product data from e-commerce category pages and exporting it to a CSV file for catalog, inventory, or POS workflows.

This project is built around a single script, [uniclerkpyme.py](uniclerkpyme.py), and uses Playwright to load pages, discover product links, extract pricing metadata, and export the final result as `products.csv`.

## Features

- Category-page crawling with configurable start page and page count
- Product link discovery from page HTML
- Multiple fallback strategies for price extraction
- Automatic generation of SKU, barcode, stock, and cost values
- UTF-8 CSV export with a POS-friendly column order
- Simple setup and minimal dependencies

## Project structure

- [uniclerkpyme.py](uniclerkpyme.py): main scraping workflow
- [requirements.txt](requirements.txt): project dependencies
- [README.md](README.md): usage and setup notes
- [AGENTS.md](AGENTS.md): repo instructions for coding agents

## Requirements

- Python 3.10+
- Playwright browser runtime
- pandas

## Installation

```bash
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
playwright install
```

## Usage

Run the scraper from the repository root:

```bash
python .\uniclerkpyme.py
```

The script will prompt for:

- Category URL
- Start page
- Number of pages to crawl
- Maximum number of products to export

## Output

The scraper writes a CSV file named `products.csv` with this column order:

| Column | Description |
| --- | --- |
| Image | Product image URL |
| Name | Product title |
| SKU | Generated SKU |
| Category | Category slug derived from the URL |
| Price | Parsed product price |
| Cost | Estimated cost based on price |
| Stock | Randomized stock count |
| Barcode | Generated barcode |

## How it works

1. Opens the category URL in Playwright.
2. Finds product links on the page.
3. Visits each product page and reads the available metadata.
4. Extracts price with fallback logic for dynamic or JavaScript-heavy storefronts.
5. Saves the cleaned output as a CSV file.

## Important notes

- The scraper assumes product URLs contain `/product/` segments.
- Price extraction is heuristic and may require adjustment for heavily protected or dynamic storefronts.
- Generated output files are local artifacts and should not be committed unless intentionally required.
- Respect the target website's terms of service and keep scraping volume conservative.

## Troubleshooting

### Playwright browser missing

```bash
playwright install
```

### Timeout or price extraction issues

- Increase wait times in the scraper if the page loads slowly.
- Check whether the site injects prices in scripts or JSON instead of the standard DOM.
- Confirm the target page structure still includes product URLs matching `/product/`.

## Contributing

Pull requests are welcome. For larger changes, open an issue first to discuss the proposed update.

## License

This project is provided as-is for internal or personal use. If you plan to distribute it publicly, add an explicit license file before publishing.
