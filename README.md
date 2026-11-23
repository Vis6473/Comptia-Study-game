# Net+ Patch Bay

A browser study game for the **CompTIA Network+ (N10-009)** exam. It is a single HTML file with no build step and no dependencies apart from Google Fonts.

## Modes

- **Exam Quiz + Outpost Defense:** 10-question rounds drawn from 114 practice questions across all five exam domains, with an explanation after every answer. Each quiz is also a night of defense in the bottom half of the screen. Undead waves march on your walled base, and correct answers resupply its guns. Press 1–4 to answer and Enter to continue.
- **Port Blitz:** 60 seconds of matching services and port numbers. Each wrong answer costs 3 seconds. Includes a port reference table.
- **OSI Stack:** put devices, protocols and PDUs on the correct OSI layer, 12 items per round.
- **Subnet Sprint:** endless random subnetting problems (network and broadcast address, host range, host count, mask) with a worked binary breakdown after each one.
- **Review:** every question you miss goes into a review queue and stays there until you answer it correctly twice in a row. You can also practice every question you've ever missed, as often as you like.

## Outpost Defense

- **Ammo:** every correct answer sends ammo to the wall. Domains are rated by difficulty, and harder ones also send scrap:

  | Domain | Tier | Reward per correct answer |
  |---|---|---|
  | 1.0 Networking Concepts | Standard | +20 ammo |
  | 3.0 Network Operations | Standard | +20 ammo |
  | 2.0 Network Implementation | Hard | +25 ammo, +10 scrap |
  | 4.0 Network Security | Hard | +25 ammo, +10 scrap |
  | 5.0 Network Troubleshooting | Elite | +30 ammo, +15 scrap |

- **Wrong answers** draw a brute into the fight. Three correct answers in a row earn bonus scrap.
- **Scrap** buys base upgrades (heavy caliber, autoloader, extra turret mounts, wall plating, ammo cache) and weapon upgrades. You also earn scrap from kills, survived nights, Port Blitz, OSI Stack and Subnet Sprint.
- **Ammo supplies:** buy ammo crates and pallets with scrap, or an airdrop with XP. During a night the ammo goes straight to the guns. Otherwise it's stockpiled for your next night.
- **XP is currency:** spend it in the Armory to attach new weapons to the base: Flame bunker (150 XP), Tesla coil (300), Mortar pit (450) and Railgun (650). Your level still counts all the XP you've ever earned.
- **Nights:** survive the final wave to advance to the next night, where the horde gets bigger and tougher.

The home screen shows your accuracy in each domain next to that domain's exam weight. It also tracks XP, levels, a daily streak and your best scores.

## Abbreviations

Questions, explanations, the port table and OSI items spell out abbreviations the first time they appear, for example "UDP (User Datagram Protocol)". A setting on the quiz screen turns this off for the answer choices, so you can test yourself on what they stand for.

## Run it

Open `index.html` in any browser, or serve the folder:

```bash
python3 -m http.server 8000
```

To publish it, enable GitHub Pages (Settings → Pages → deploy from the `main` branch, root folder).

## Notes

- Progress is stored in your browser's `localStorage`, so it stays on the device and browser you use.
- The questions are original practice items written against the N10-009 objectives, not real exam questions.
