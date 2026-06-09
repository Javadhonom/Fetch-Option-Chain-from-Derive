A Python client for the Derive (Lyra Finance) REST API that fetches live option chain data and displays it in a structured table format — mirroring the layout of the Derive web interface.

Features

Fetches all active option instruments for any supported currency (BTC, ETH, SOL, …)
Displays a full option chain table with Calls on the left, Puts on the right, grouped by strike
Shows bid, ask, mark price, implied volatility (IV), delta, and open interest (OI) for every strike
Supports filtering by a specific expiry date or viewing all expiries at once
Optionally exports each expiry to a .csv file
No API key required — uses public endpoints only


Requirements

Python 3.10+
Dependencies:

bashpip install requests pandas tabulate

Usage
In Jupyter Notebook
Paste the full script into a cell and run it, then in a new cell:
python# BTC options, all expiries
run_once("BTC")

# ETH options
run_once("ETH")

# Specific expiry
run_once("BTC", expiry="20250627")
From the terminal
bash# BTC options, all expiries
python derive_option_chain.py

# ETH options
python derive_option_chain.py --currency ETH

# Specific expiry
python derive_option_chain.py --currency BTC --expiry 20250627

# Save each expiry to a CSV file
python derive_option_chain.py --currency BTC --csv

Output Format
────────────────────────────────────────────────────────────────────────────────
  BTC OPTIONS  │  Expiry: 27 JUN 2025  │  Spot: $105,420.00
────────────────────────────────────────────────────────────────────────────────
         ──── CALLS ────                STRIKE        ──── PUTS ────
  C Bid   C Ask  C Mark   C IV  C Delta  C OI  Strike  P Bid   P Ask  P Mark ...
  1,240   1,310  1,275   62.3%   0.682    45   95,000    80      95     88   ...
  ...
────────────────────────────────────────────────────────────────────────────────
  Columns: Bid | Ask | Mark | IV | Delta | OI

API Reference
This project uses two public Derive REST endpoints — no authentication needed:
EndpointPurposePOST /public/get_instrumentsList all active option contractsPOST /public/get_tickersFetch bid/ask, IV, greeks, OI per expiryPOST /public/get_currencyFetch current spot price
Base URL: https://api.lyra.finance
Full documentation: docs.derive.xyz

Project Structure
derive-option-chain/
├── derive_option_chain.py   # main script
└── README.md

Disclaimer
This project is for informational purposes only. It does not constitute financial advice. Options trading involves significant risk of loss. Always do your own research before trading.
