# AGENTS.md

## Project overview
This repository contains a Python web scraper that crawls e-commerce category pages, extracts product data, and exports it as a UTF-8 CSV file named `products.csv`.

The implementation is intentionally lightweight and centered in [uniclerkpyme.py](uniclerkpyme.py). There is no app framework, no test suite, and no separate package layout.

## Key files
- [uniclerkpyme.py](uniclerkpyme.py): main scraper logic; prompts for category URL, start page, page count, and product limit
- [requirements.txt](requirements.txt): Python dependencies
- [README.md](README.md): project documentation and usage notes

## Working conventions
- Keep changes small and focused; this project is a single-file script with direct side effects.
- Prefer updating the existing script rather than introducing a full framework or new package structure.
- Preserve the current CSV export contract: columns are `Image, Name, SKU, Category, Price, Cost, Stock, Barcode`.
- When changing scraping logic, keep browser automation behavior simple and deterministic; Playwright waits and selectors are part of the product logic.

## Commands
Run the project from the repository root:

```bash
python .\uniclerkpyme.py
```

Install dependencies:

```bash
python -m venv venv
.\venv\Scripts\activate
pip install -r requirements.txt
playwright install
```

## Important behavior and pitfalls
- The script is interactive: it asks for a category URL, start page, number of pages, and max products at startup.
- It uses Playwright in `headless=True` mode and depends on the browser runtime being installed.
- Product detection assumes URLs contain `/product/` patterns, so changes to site structure may require selector or URL-matching updates.
- Price extraction is intentionally heuristic and can fail on highly protected or JavaScript-heavy sites; preserve fallback logic carefully.
- The script writes output to the current working directory as `products.csv`.

## Safety and scope
This project scrapes external websites. When changing crawling behavior, avoid aggressive scraping patterns or unnecessary request amplification. Respect website terms of service and keep changes conservative.

## Contribution guidance
- If you need to modify scraping behavior, read the helper functions and extraction flow in [uniclerkpyme.py](uniclerkpyme.py) before patching.
- If documentation needs to be updated, prefer small, repo-specific additions to [README.md](README.md) rather than duplicating large sections in this file.
- Do not add a broad complex architecture unless the repository genuinely grows beyond a single script.
