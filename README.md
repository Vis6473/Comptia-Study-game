# Net+ Patch Bay

A browser study game for the **CompTIA Network+ (N10-009)** exam. It is a single HTML file with no build step and no dependencies apart from Google Fonts.

## Modes

- **Exam Quiz:** 10-question rounds drawn from 85 practice questions across all five exam domains, with an explanation after every answer. Press 1–4 to answer and Enter to continue.
- **Port Blitz:** 60 seconds of matching services and port numbers. Each wrong answer costs 3 seconds. Includes a port reference table.
- **OSI Stack:** put devices, protocols and PDUs on the correct OSI layer, 12 items per round.
- **Subnet Sprint:** endless random subnetting problems (network and broadcast address, host range, host count, mask) with a worked binary breakdown after each one.
- **Review:** every question you miss goes into a queue until you answer it correctly.

The home screen shows your accuracy in each domain next to that domain's exam weight. It also tracks XP, levels, a daily streak and your best scores.

## Run it

Open `index.html` in any browser, or serve the folder:

```bash
python3 -m http.server 8000
```

To publish it, enable GitHub Pages (Settings → Pages → deploy from the `main` branch, root folder).

## Notes

- Progress is stored in your browser's `localStorage`, so it stays on the device and browser you use.
- The questions are original practice items written against the N10-009 objectives, not real exam questions.
