# tc-profit-tracker

A tool for hobby tissue culture growers: pick a plant, see what it costs to clone it, what it sells for, how much profit is left after the price drops, and whether demand for it is steady over time.

**Status:** idea stage. Nothing is built yet beyond a working spreadsheet model.

## What's here
| Path | What it is |
|---|---|
| [docs/idea-brief.md](docs/idea-brief.md) | The idea brief: audience, cost model, price data sources, price tracking, legal issues, MVP, open questions |
| [spreadsheet/tc-profit-calculator.xlsx](spreadsheet/tc-profit-calculator.xlsx) | Working calculator for 20 starter plants plus a price log tab |
| [scripts/build_spreadsheet.py](scripts/build_spreadsheet.py) | Regenerates the spreadsheet template (`python3 scripts/build_spreadsheet.py`, needs `openpyxl`) |

## The spreadsheet
- **Settings:** shared defaults like labor rate, contamination and acclimatization loss, fees and batch size.
- **Calculator:** one row per plant. Blue cells are inputs, grey cells are calculated: cycles and months to sellable, labor and media cost, cost per sellable plant, expected sale price after price decay, and profit per plant and per batch.
- **Price Log:** one row per listing or sale you see. Sold rows feed the calculator's "sold last 30 days" and "average sold price" columns, so you can see which plants have steady demand.

Starting prices, multiplication rates and decay rates are rough estimates, not checked against live listings. Replace them as the price log fills in. The model also assumes the whole batch sells at once, so check sales volume before trusting the batch profit.

## Decided so far
- Audience: hobbyists and small sellers.
- Format: a calculator first, with price tracking for demand over time.
- Approach: prove the model in the spreadsheet, then build a simple web page.

## Next steps
1. Start logging prices weekly for the 20 plants, since eBay only shows about 90 days of sold listings.
2. Refine the cost defaults with real hobbyist numbers.
3. Build the first static web page version of the calculator.

Not legal advice: many named cultivars are patented or protected, and selling clones of them may need a license.
