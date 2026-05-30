# ProShotClock

A free, full-screen basketball **shot clock** that runs in any web browser — no
download, no sign-up. Built as a single static HTML page and deployed via GitHub
Pages.

🔗 **Live:** [proshotclock.com](https://proshotclock.com)

## Features

- **Two configurable reset presets** — default 24 / 14 (NBA/FIBA), with one-tap
  presets for NCAA (30 / 20) and high school (35) in Settings
- **Custom times** from 0.1 to 60.0 seconds for drills
- **External full-screen display** (`display.html`) for a second monitor or
  projector, kept in sync live via the `BroadcastChannel` API
- **End-of-clock buzzer** (`siren.mp3`) when the timer hits zero
- **Color states** as time runs down — green while running, amber under 10s, red
  under 5s, switching to **tenths of a second** for the final stretch
- **Recall** to undo an accidental reset
- **Blank display** toggle for use between possessions
- **Customizable keyboard shortcuts**, saved in the browser
- Settings (presets, shortcuts, display options) **persist** via `localStorage`
- Collapsible donation sidebar (Buy Me a Coffee, PayPal, Satispay, Ethereum)

### Keyboard shortcuts

Defaults (all remappable in **Settings**):

| Key | Action |
| --- | --- |
| `Space` | Start / stop the clock |
| `→` | Reset to preset 1 (default 24) |
| `←` | Reset to preset 2 (default 14) |
| `↑` | Blank the display |
| `Enter` | Focus the custom-time input |

## External display

The control page is the operator console; `display.html` is a separate
full-screen LED view for the audience.

1. Click **🖥 Open display** on the main page — it opens in a new window.
2. Drag it to your second monitor / projector and double-click it for full screen.
3. Click once on the display to enable its buzzer (browsers block autoplay until
   a user gesture).

The console broadcasts its state on every tick over the `BroadcastChannel` API
(same browser, same origin), with `localStorage` providing the initial state when
a display window opens. You can open multiple display windows; each one syncs
independently. If you run the display on the same machine, enable **Mute this
page's buzzer** in Settings so the horn only sounds once.

## Settings

Open **⚙ Settings** on the main page to configure:

- **Reset presets** (Reset 1 / Reset 2), with quick presets for NBA/FIBA, NCAA
  and high school
- **Display options** — show tenths under 5s, FIBA blank-at-full, mute the
  console buzzer
- **Keyboard shortcuts** — click a field and press the key to remap it

All settings are saved to `localStorage` and persist across sessions (per
browser).

## Pages

| Path | Description |
| --- | --- |
| `/` (`index.html`) | Main shot clock (operator console) + below-the-fold rules guide and FAQ |
| `/display.html` | External full-screen LED display for a second screen (`noindex`) |
| `/pieni` (`pieni/index.html`) | "Empty / Full" display variant — shows whole seconds (rounded up) instead of tenths |

The two pages are intentionally different in how the countdown renders and are
kept that way; don't unify their display logic.

## Project structure

```
.
├── index.html        # Main app / operator console + SEO/guide content
├── display.html      # External full-screen LED display (synced via BroadcastChannel)
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
