# Google Search Scraper & API

Webová aplikace, která pro zadané klíčové slovo stáhne výsledky z vyhledávače Google a vrátí je jako JSON soubor. Postavená na **FastAPI** a **Selenium**, spustitelná lokálně i v Dockeru.

Projekt vznikl jako zadání ve výběrovém řízení.

## Co umí
- Jednoduchý formulář v prohlížeči: zadáš dotaz, dostaneš soubor `results_google.json` (název a odkaz každého výsledku).
- Selenium běží v headless režimu a odklikne cookie lištu.
- Sám pozná, jestli běží v Linuxu/Dockeru (použije systémový Chromium), nebo lokálně (stáhne ChromeDriver).
- Ukázkový výstup je v [`results_google.json`](results_google.json).

## Technologie
Python 3.10+, FastAPI, Uvicorn, Selenium, Jinja2, Docker, pytest

## Spuštění lokálně
Potřebuješ Python 3.10+ a nainstalovaný Google Chrome.

```bash
git clone https://github.com/daniel-becher/google-search-scraper.git
cd google-search-scraper
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
python google_test.py
```

Pak otevři http://localhost:8000.

## Spuštění v Dockeru
```bash
docker compose up --build
```

Aplikace poběží na http://localhost:8000.

## Testy
```bash
pytest unit_tests.py
```

Pozor: test `test_google_scrape_returns_data` volá skutečný Google, takže potřebuje internet a může občas selhat, když Google zobrazí CAPTCHA.

## Struktura
```
google_test.py       # FastAPI aplikace a scraping logika
templates/index.html # formulář
unit_tests.py        # testy
Dockerfile           # obraz s Pythonem a Chromiem
docker-compose.yml   # spuštění jedním příkazem
```
