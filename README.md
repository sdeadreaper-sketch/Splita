# Household Ledger — Rent Splitter (web version)

A browser front end for the original `main_rent_split.py` CLI script.
Same math, same validation rules — now driven from an HTML/CSS/JS page
served by a small Flask app, instead of the terminal.

## Run it locally

1. Open a terminal in this folder.
2. Install the one dependency:
   ```
   pip install -r requirements.txt
   ```
3. Start the server:
   ```
   python app.py
   ```
4. Open your browser to:
   ```
   http://127.0.0.1:5000
   ```

Stop the server with `Ctrl+C` in the terminal.

## How it's put together

- `app.py` — Flask app. `calculate_split()` reproduces the exact
  calculations from the original script (fair split vs. proportional
  split, income-limit warnings, totals). It's exposed as a JSON API at
  `POST /api/calculate`.
- `templates/index.html` — the page structure: split-mode picker, bill
  inputs, a dynamic roommate roster, and a results area.
- `static/style.css` — the visual design (a household-ledger/receipt
  theme).
- `static/script.js` — builds the roommate rows, sends the form data to
  `/api/calculate`, and renders the returned results as a receipt.

## Notes

- All validation (positive numbers, 0–100% limits, non-empty names)
  happens both in the browser (for instant feedback) and again on the
  server (so the API can't be fed bad data).
- Nothing is saved between requests — each calculation is stateless,
  just like the original script.
