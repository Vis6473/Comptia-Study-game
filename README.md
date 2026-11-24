# Cyber Zombie Attack

A browser study game for **CompTIA Network+ (N10-009)** and **CompTIA Security+ (SY0-701)**. You answer exam questions to keep a zombie horde off your outpost. It is a single HTML file with no build step and no dependencies apart from Google Fonts.

## Main menu, settings and high scores

- **Main menu:** the title screen where you pick the exam to study. Each exam card shows your accuracy, questions seen, review queue and best mock score. Use **Menu** in the tabs, or the logo, to switch exams.
- **Settings:** turn spelled-out abbreviations in answer choices on or off, and reset Network+ progress, Security+ progress, the outpost, or everything. Each reset asks you to confirm first.
- **High scores:** the outpost's records (highest night, most undead in one night, total kills, level) and, for each exam, the best mock score, best quick exam, mini-game records and recent mock attempts.
- **Progress:** each exam keeps its own stats, review queue, mock exams and high scores. XP, your level, your streak and the outpost are shared, but each exam has its own base upgrades and weapons.

## Network+ modes

- **Quick Exams + Outpost Defense:** 10-question rounds drawn from 219 practice questions across all five exam domains, with an explanation after every answer. Every question is tagged with its N10-009 objective. Each quick exam is also a night of defense in the bottom half of the screen. The undead spawn without end until you answer the last question, and correct answers resupply the guns. Then a bomber flies over, clears the field, and the next night begins. Press 1–4 to answer and Enter to continue.
- **Mock Exam:** a timed 90-question, 90-minute exam split by the N10-009 domain weights (21/18/17/13/21 questions). You get no feedback until you submit. You can flag questions, jump around with the question grid, and close the page and resume, since the clock keeps running. Results show an estimated 100–900 score (pass at 720), a breakdown by domain, and every missed question with its explanation. Misses go into your review queue.
- **Port Blitz:** 60 seconds of matching services and port numbers. Each wrong answer costs 3 seconds. Includes a port reference table.
- **OSI Stack:** a scavenging mission. Put devices, protocols and PDUs on the correct OSI layer, 12 items per round. Each correct layer brings back 6 scrap and 4 XP straight away.
- **Subnet Sprint:** endless random subnetting problems (network and broadcast address, host range, host count, mask) with a worked binary breakdown after each one.
- **Review:** every question you miss goes into a review queue and stays there until you answer it correctly twice in a row. You can also practice every question you've ever missed. A study plan lists the exam objectives you're weakest on, with the key facts from the questions you missed, the chapters and pages that cover it in the Network+ study guide in `guides/`, links to Professor Messer's videos and CompTIA's exam objectives, and a button to practice just that objective. When you open the app from a checkout of this repo with the PDFs downloaded, the chapter links open the guide at the right page.

## Security+ modes

- **Quick Exams + Outpost Defense:** 10-question rounds from 264 original Security+ questions covering all 28 SY0-701 objectives, with at least 9 per objective. Security+ nights bring their own zombies (see below).
- **Mock Exam:** 90 questions in 90 minutes, split 11/20/16/25/18 across the five domains by their exam weights (12/22/18/28/20%). The pass mark is 750 on the 100–900 scale.
- **Port Blitz:** the same port drill as Network+, with its own high score.
- **Control Sort:** classify 10 security controls by category (technical, managerial, operational, physical) and by type (preventive, deterrent, detective, corrective, compensating, directive). Each correct pick is a point, out of 20, and a scavenging mission that brings back 4 scrap and 2 XP straight away.
- **Attack Match:** 60 seconds to name the attack behind each indicator or scenario, such as password spraying, an evil twin or a logic bomb. A wrong answer costs 3 seconds, and the attacks you missed are listed at the end.
- **Review:** the same review queue and study plan as Network+. Each weak objective links to its chapters in the Security+ Study Guide and to that domain's chapter in the Security+ Practice Tests book, with the question and answer pages.

## Outpost Defense

- **Ammo:** every correct answer sends ammo to the wall. Domains are rated by difficulty, and harder ones also send scrap:

  | Domain | Tier | Reward per correct answer |
  |---|---|---|
  | 1.0 Networking Concepts | Standard | +20 ammo |
  | 3.0 Network Operations | Standard | +20 ammo |
  | 2.0 Network Implementation | Hard | +25 ammo, +10 scrap |
  | 4.0 Network Security | Hard | +25 ammo, +10 scrap |
  | 5.0 Network Troubleshooting | Elite | +30 ammo, +15 scrap |

- **Security+ rewards:**

  | Domain | Tier | Reward per correct answer |
  |---|---|---|
  | 1.0 General Security Concepts | Standard | +20 ammo |
  | 3.0 Security Architecture | Standard | +20 ammo |
  | 2.0 Threats, Vulnerabilities, and Mitigations | Hard | +25 ammo, +10 scrap |
  | 5.0 Security Program Management and Oversight | Hard | +25 ammo, +10 scrap |
  | 4.0 Security Operations | Elite | +30 ammo, +15 scrap |

- **Zombies:** Network+ nights bring walkers and brutes. Security+ nights bring botnet zombies, fast fragile worms and ransomware brutes, which encrypt (wipe) 3 rounds of ammo every second they stay at the wall.
- **Wrong answers** draw an extra brute into the fight (a ransomware brute in Security+). Three correct answers in a row earn bonus scrap.
- **Scrap** is shared by both exams. It buys base upgrades (heavy caliber, autoloader, extra turret mounts, wall plating, ammo cache) and weapon upgrades. You also earn scrap from kills, survived nights and the mini-games.
- **Ammo supplies:** buy ammo crates and pallets with scrap, or an airdrop of 200 rounds with XP. During a night the ammo goes straight to the guns. Otherwise it's stockpiled for your next night.
- **XP is currency:** spend it in the Armory to attach new weapons to the base. Each exam has its own upgrades and weapons. Network+ has Flame bunker (150 XP), Tesla coil (300), Mortar pit (450) and Railgun (650). Security+ has the Sandbox trap, EDR pulse, Honeypot mine and Kill switch at the same prices, and its base upgrades are Patch level, Threat feed, Sensor node, Hardened firewall and Backup cache. Your level still counts all the XP you've ever earned.
- **Pause:** the Pause button (or P) freezes the horde and puts the quick exam on hold: the exam dims and ignores clicks and keys, and a pause menu over the horde shows the question, hostiles, wall and ammo. From there you can resume (or press Esc), restart the quick exam from question 1 with a fresh night, open the armory, or quit to home. Answers already given stay recorded.
- **Nights:** keep the wall standing until the bomber clears the field to advance to the next night, where the horde gets bigger and tougher.

The home screen shows your accuracy in each domain next to that domain's exam weight. It also tracks XP, levels, a daily streak and your best scores.

## Abbreviations

Questions, explanations, the port table and OSI items spell out abbreviations the first time they appear, for example "UDP (User Datagram Protocol)". When a question tests what a term means (its correct answer is an abbreviation), the answer choices stay abbreviated until you answer, so the full name does not give the answer away. A setting on the quiz screen and in Settings turns spelled-out choices off entirely.

## Study guides

The `guides/` folder holds PDF study guides to read alongside the game:

| Exam | Guide | Size |
|---|---|---|
| Network+ | [CompTIA Network+ Study Guide](guides/Network%2B/CompTIA%20Network%2B%20Study%20Guide.pdf) | 561 MB |
| Security+ (SY0-701) | [Security+ Study Guide, Ninth Edition](guides/Security%2B/Security%2B%20SY0-701%20Study%20Guide/09102025_Security%2B%C2%AE%20Study%20Guide%20Ninth%20Edition.pdf) | 189 MB |
| Security+ (SY0-701) | [Security+ Practice Tests, Third Edition](guides/Security%2B/Security%2B%20Practice%20Tests%20SY0-701/09102025_Security%2B%20Practice%20Tests%20Exam%20SYO-701%20Third%20Edition.pdf) | 48 MB |

The PDFs are stored with [Git LFS](https://git-lfs.com). Install it before you clone (`brew install git-lfs`, then `git lfs install`), or the files download as small text pointers instead of the PDFs. These are copyrighted books, so keep this repository private.

## Run it

Open `index.html` in any browser, or serve the folder:

```bash
python3 -m http.server 8000
```

To publish it, enable GitHub Pages (Settings → Pages → deploy from the `main` branch, root folder).

## Notes

- Progress is stored in your browser's `localStorage`, so it stays on the device and browser you use.
- The questions are original practice items written against the official CompTIA exam objectives, not real exam questions.
