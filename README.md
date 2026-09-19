# Portfolio-Tracker
This is a project to build a stock portfolio tracker that pulls live market data and tracks performance over time.

## What this project does
- Pulls live stock prices from the Finnhub API
- Adds and views stock holdings with live pricing
- Calculates cost basis, current value, and gain/loss (per holding and portfolio-wide)
- Saves and loads portfolios to/from JSON files
- Tracks portfolio value over time and plots growth as a line chart
- Handles invalid tickers and bad input 

## Methodology
The project is built around two classes:

- **`Holding`** — represents a single stock holding (ticker, shares, purchase price). Handles its own cost basis, live value, and gain/loss calculations once a current price is attached.
- **`Portfolio`** — holds a collection of `Holding` objects. Aggregates totals across all holdings (total cost basis, total current value, total gain/loss) and manages adding new positions.

Live prices are fetched via `requests` from the Finnhub API and attached to each holding individually, so gain/loss can be calculated by comparing purchase price against current market price.

Portfolios are saved and loaded using JSON — each `Holding`/`Portfolio` is converted to a plain dictionary (`to_dict()`) before saving, since JSON can't store custom Python objects directly, then reconstructed back into real objects on load.

Every time a portfolio is saved, its total value is also logged (with a date) to a separate history file, building a time-series dataset used to plot portfolio growth over time.

The whole thing is wrapped in a command-line menu loop, with error handling for invalid tickers and non-numeric input.

## What this project demonstrates
- Object-oriented programming (classes, methods, `self`)
- REST API integration (`requests`, JSON parsing)
- File I/O and data persistence (JSON)
- Error handling (`try`/`except`)
- Environment variable management for API key security
- Data visualisation (`matplotlib`)
