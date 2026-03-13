# ARB · OMX Stockholm Arbitrage Monitor

A free, self-contained arbitrage spread monitor for **OMX Stockholm A/B share pairs**, deployable on GitHub Pages with zero backend.

## Features

- **35 pre-loaded OMX Stockholm pairs** — all companies with dual share classes (A/B or A/C)
- **Smart learning** — the app remembers which pairs have shown opportunities and ranks them by frequency (stored in browser localStorage)
- **Hot pairs heat bar** — most profitable pairs surface to the top automatically over time
- **Live prices** — fetched from Yahoo Finance every 30s–10min (configurable)
- **Sparkline history** — visual spread chart for the current session
- **Profit calculator** — enter your share count, courtage, and safety margin. The app tells you exactly whether a trade is profitable _after all costs_
- **Event log** — timestamped log of every price fetch and opportunity

## Deploy to GitHub Pages (Free, 24/7)

### Option A — GitHub UI (easiest)

1. Create a new GitHub repository (e.g. `arb-monitor`)
2. Upload `index.html` via **Add file → Upload files**
3. Go to **Settings → Pages**
4. Under *Source*, select **Deploy from a branch** → `main` → `/ (root)`
5. Save. Your app will be live at `https://YOUR_USERNAME.github.io/arb-monitor/` within ~60 seconds.

### Option B — Git CLI

```bash
git init arb-monitor
cd arb-monitor
cp /path/to/index.html .
git add index.html
git commit -m "Initial deploy"
git remote add origin https://github.com/YOUR_USERNAME/arb-monitor.git
git push -u origin main
```
Then enable GitHub Pages in Settings → Pages as above.

## How It Works

### Arbitrage Logic

For an A/B pair, a profitable arbitrage trade means:

```
Net Profit = |Price_A − Price_B| × NumShares
           − Courtage × 2              (buy + sell legs)
           − Safety Margin %           (buffer against slippage)
```

The app signals **GO** only when Net Profit > 0.

### Learning System

Every time a pair is monitored, the app stores in your browser:
- Number of times monitored
- Number of times an opportunity was detected
- Maximum spread ever seen
- Last observed spread

Pairs are sorted by opportunity count — so over time, the most profitable pairs automatically rise to the top of the dropdown.

### Pair Database

| Company | A-share | B/C-share | Cap |
|---|---|---|---|
| Atlas Copco | ATCO-A.ST | ATCO-B.ST | Large |
| Ericsson | ERIC-A.ST | ERIC-B.ST | Large |
| Handelsbanken | SHB-A.ST | SHB-B.ST | Large |
| Husqvarna | HUSQ-A.ST | HUSQ-B.ST | Large |
| Industrivärden | INDU-A.ST | INDU-C.ST | Large |
| Investor | INVE-A.ST | INVE-B.ST | Large |
| Kinnevik | KINV-A.ST | KINV-B.ST | Large |
| NCC | NCC-A.ST | NCC-B.ST | Large |
| NIBE Industrier | NIBE-A.ST | NIBE-B.ST | Large |
| SCA | SCA-A.ST | SCA-B.ST | Large |
| Securitas | SECU-A.ST | SECU-B.ST | Large |
| Skanska | SKA-A.ST | SKA-B.ST | Large |
| SKF | SKF-A.ST | SKF-B.ST | Large |
| SSAB | SSAB-A.ST | SSAB-B.ST | Large |
| Sweco | SWEC-A.ST | SWEC-B.ST | Large |
| Tele2 | TEL2-A.ST | TEL2-B.ST | Large |
| Trelleborg | TREL-A.ST | TREL-B.ST | Large |
| Volvo | VOLV-A.ST | VOLV-B.ST | Large |
| Wallenstam | WALL-A.ST | WALL-B.ST | Large |
| Addlife | ALIF-A.ST | ALIF-B.ST | Mid |
| Addtech | ADDT-A.ST | ADDT-B.ST | Mid |
| Elanders | ELAN-A.ST | ELAN-B.ST | Mid |
| Getinge | GETI-A.ST | GETI-B.ST | Mid |
| Hufvudstaden | HUFV-A.ST | HUFV-C.ST | Mid |
| Latour | LATO-A.ST | LATO-B.ST | Mid |
| Lundbergföretagen | LUND-A.ST | LUND-B.ST | Mid |
| Nolato | NOLA-A.ST | NOLA-B.ST | Mid |
| Peab | PEAB-A.ST | PEAB-B.ST | Mid |
| Ratos | RATO-A.ST | RATO-B.ST | Mid |
| Sagax | SAGA-A.ST | SAGA-B.ST | Mid |
| Sdiptech | SDIP-A.ST | SDIP-B.ST | Small |
| Vitec Software | VITS-A.ST | VITS-B.ST | Small |
| Xano Industri | XANO-A.ST | XANO-B.ST | Small |

## Notes

- Prices are fetched via **Yahoo Finance** through a CORS proxy — no API key required
- All learning data is stored in **your browser's localStorage** — nothing leaves your device
- The app works best kept open in a dedicated browser tab
- Ticker symbols follow Yahoo Finance format with `.ST` suffix for Stockholm

## License

MIT — free to use, modify, and deploy.
