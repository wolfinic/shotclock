# ProShotClock

A free, full-screen basketball **shot clock** that runs in any web browser — no
download, no sign-up. Built as a single static HTML page and deployed via GitHub
Pages.

🔗 **Live:** [proshotclock.com](https://proshotclock.com)

## Features

- **24-second** NBA/FIBA shot clock with a quick **14-second** reset
- **Custom times** from 0.1 to 24.0 seconds for drills
- **End-of-clock buzzer** (`siren.mp3`) when the timer hits zero
- **Color states** as time runs down — green while running, amber under 10s, red
  under 5s, switching to **tenths of a second** for the final stretch
- **Blank display** toggle for use between possessions
- **Keyboard shortcuts** for live operation
- Collapsible donation sidebar (Buy Me a Coffee, PayPal, Satispay, Ethereum)

### Keyboard shortcuts

| Key | Action |
| --- | --- |
| `Space` | Start / stop the clock |
| `→` | Reset to 24 |
| `←` | Reset to 14 |
| `↑` | Blank the display |
| `Enter` | Focus the custom-time input |

## Pages

| Path | Description |
| --- | --- |
| `/` (`index.html`) | Main shot clock + below-the-fold rules guide and FAQ |
| `/pieni` (`pieni/index.html`) | "Empty / Full" display variant — shows whole seconds (rounded up) instead of tenths |

The two pages are intentionally different in how the countdown renders and are
kept that way; don't unify their display logic.

## Project structure

```
.
├── index.html        # Main app + SEO/guide content
├── pieni/
│   └── index.html    # Empty/Full display variant
├── siren.mp3         # End-of-clock buzzer
├── robots.txt        # Crawler rules (incl. AI/answer-engine bots)
├── sitemap.xml       # XML sitemap
├── llms.txt          # Summary for LLM/AI crawlers
├── CNAME             # Custom domain for GitHub Pages (proshotclock.com)
└── README.md
```

## Local development

It's a static site with no build step. Either open the file directly:

```bash
open index.html
```

…or serve the folder so that the `/pieni` route and `siren.mp3` resolve cleanly:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deployment

Hosted on **GitHub Pages** from the `main` branch with the custom domain in
`CNAME`. Any push to `main` publishes automatically:

```bash
git add -A
git commit -m "Describe your change"
git push origin main
```

## SEO

`index.html` includes Open Graph / Twitter cards and JSON-LD structured data
(`WebApplication` + `FAQPage`). `robots.txt`, `sitemap.xml`, and `llms.txt`
support both traditional search engines and AI answer engines.

## License

© Niccolò Bevacqua. All rights reserved.
