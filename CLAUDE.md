# Cyber Zombie Attack

A browser study game for CompTIA exams, with a tower-defense game ("the outpost") built into the quizzes. It covers Network+ (N10-009), Security+ (SY0-701), A+ Core 1 (220-1201) and A+ Core 2 (220-1202). A+ is two separate exams in the app, with ids `a1` and `a2`. The owner studies with it daily. It was called Net+ Patch Bay until the owner renamed it. The GitHub repo is `Vis6473/Comptia-Study-game` (renamed from `net-plus-study-game`; the local folder may still use the old name).

## How it's built

- Everything is in **`index.html`**: HTML, CSS and one script wrapped in an IIFE. There is no build step, no framework and no dependencies except Google Fonts (Chakra Petch, IBM Plex Sans, IBM Plex Mono).
- Open the file in a browser to run it, or serve the folder: `python3 -m http.server 8000`.
- Hash routing. Global views: `#menu` (the title screen, and the default with no hash), `#scores` (High Scores), `#settings`. Exam views: `#home`, `#quiz` (Quick Exams), `#mock`, `#review`, plus each exam's mini-games (`#ports`, `#osi` and `#subnet` for Network+; `#ports`, `#control` and `#attack` for Security+; `#ports` and `#hardware` for A+ Core 1; `#command` and `#wintool` for A+ Core 2). `GLOBAL_VIEWS` and `VIEWS` map hashes to view functions. An exam view with no exam chosen sends you to the menu, and a mini-game the current exam doesn't have falls back to home. A click on a link to the current hash re-runs `route()`.
- **Exams:** `EXAMS` (the `Exams` section, just before Boot) registers each exam: name, code, pass mark, `DOMAINS`, `Q`, `OBJ`, `GUIDE`, `TIER`, `MOCK_SPLIT`, armory (`UPG`, `WPN`) and mini-game list (`games`, keys of `GAMES`). Network+ content is defined as `NET_*` constants. `setExam(id)` points the shared names (`EX`, `P`, `DOMAINS`, `Q`, `OBJ`, `GUIDE`, `TIER`, `MOCK_SPLIT`, `PASS`, `UPG`, `WPN`) at one exam, so most code just uses those names. An exam with `ready:false` shows as coming soon on the menu. Security+ content is the `SEC_*` constants (`SEC_Q`, `SEC_OBJ`, `SEC_GUIDE`, `SEC_UPG`, `SEC_WPN`) in the `Security+ content` section, and `SEC_DOMAINS` and `GAMES` sit in the `Exams` section. A+ content is the `A1_*` and `A2_*` constants (`A1_DOMAINS`, `A1_OBJ`, `A1_UPG`, `A1_WPN`, `A1_Q`, and the same for `A2_`) plus the match-game data `HARDWARE`, `COMMANDS` and `WINTOOLS`, in the `A+ content` section just before `Exams`. `EXAM_IDS` (in the State section) lists every exam id in menu order; menus, settings, high scores, the score card and saved state all loop over it, so a new exam goes in `EXAM_IDS` and `EXAMS`. A+ has no study guide yet, so its `GUIDE` is `null` and the study plan and explanation footer skip the book chapters. Domain counts differ per exam (A+ Core 2 has four, CISSP eight), so never hardcode five domains.
- **CISSP (ISC2)** (`cissp`): content is the `CISSP_*` constants (`CISSP_OBJ`, `CISSP_UPG`, `CISSP_WPN`, `CISSP_Q`) plus `CONCEPTS` (Concept Match) in the `CISSP content` section, and `CISSP_DOMAINS` (2024 outline weights 16/10/13/13/13/12/13/10) in the Exams section. `ORG:"ISC2"` switches the study links (`isISC2()`): a CISSP video search and isc2.org instead of Professor Messer and CompTIA. `badge` is the label shown above the name on the menu, High Scores and score card. Games: `concept` and `attack`. Zombies: `insider`, `spy` (80% hp, 1.4× speed) and `apt` (a brute that heals 3% of max health a second). The objective titles were written from memory of the 2024 outline, like A+'s, so check them against ISC2's outline when available. An exam with `ready:false` shows as Arriving soon on the menu, and Settings, High Scores and the score card skip it.
- The menu, Settings and High Scores are global (`body.menu-mode` hides the header and tabs on the menu; `body.global-mode` hides the tabs). The menu is a deliberately dark title screen with an animated horde on a canvas, which stays still when the device asks for reduced motion.
- Every view that adds timers or key listeners sets the global `cleanup`. `route()` calls it and also calls `D.unmount()`.

### Main sections of the script (in order)

| Section | What it holds |
|---|---|
| Content | `NET_DOMAINS` (name, exam weight %, color), `NET_Q` (question bank), `PORTS`, `LAYERS`, `OSI_ITEMS` |
| State | `KEY`, `exFresh()`, `freshState()`, `mergeEx()`, `load()`, `save()`, `award(xp)` |
| Abbreviations | `GL` glossary, `expand(text)`, `isTermQ(answer)`, `choice(option)` |
| Outpost economy | `NET_TIER`/`TIERS` (rewards per domain), `NET_UPG` (scrap upgrades), `NET_WPN` (XP weapons), `SUPPLY` (ammo), shop HTML |
| Outpost defense | `D`, a canvas tower-defense module in a fixed bottom dock |
| Quiz | `startQuiz(pool,label,again)`, `showQ`, `quizResult`, `recordAnswer(id,ok)` |
| Objectives | `OBJ` (N10-009 objective titles plus a video search topic), `SRC` (study links), study plan in `viewReview` |
| Mock exam | `MOCK_SPLIT`, `buildMock`, `runMock`, `submitMock`, `mockResults` |
| Menu, Settings, High Scores | `viewMenu`, `menuHorde`, `viewSettings`, `resetPart`, `viewScores` |
| Router | `VIEWS`, `GLOBAL_VIEWS`, `route()`, `renderChrome()` (header subtitle and tabs) |
| Mini games | Port Blitz, OSI Stack, Subnet Sprint (Network+); Control Sort (Security+), with data in `CTRL_CATS`, `CTRL_TYPES` and `CONTROLS`; match games (`MATCH`, `viewMatch`, `runMatch`): Attack Match (`ATTACKS`, Security+), Hardware Match (Core 1), Command Match and Tool Match (Core 2). Port Blitz drills `portList()`: the exam's `ports` list if it has one, otherwise every port not marked A+ only |
| A+ content | `A1_*`, `A2_*`, `HARDWARE`, `COMMANDS`, `WINTOOLS` |
| Exams | `SEC_DOMAINS`, `GAMES`, `EXAMS`, and the `let` bindings that `setExam` sets |

## Question bank rules

Each question is one line in `Q`:

```js
[domain, "question", "correct answer", ["wrong", "wrong", "wrong"], "explanation", "objective"]
// e.g. [5, "Which tool ...?", "OTDR", ["Toner probe", "Loopback plug", "Multimeter"], "An optical ...", "5.5"]
```

- Each exam has its own bank (`NET_Q`, `SEC_Q`, `A1_Q`, `A2_Q`, `CISSP_Q`), and `Q` points at the current one. Indexes are per bank.
- **Append new questions to the end of the bank.** Never insert in the middle or reorder.** Saved progress (`S.qs`, `S.review`, `S.reviewHits`, `S.missedEver`, mock exam state) refers to questions by array index. Inserting earlier in the list shifts every later question and scrambles saved progress. This already happened once, when 10 domain 2 and 3 questions were inserted mid-list in commit `eeac48e`. Since then, new questions only go at the end.
- The objective tag must be a key of `OBJ` and must start with the question's domain number.
- Write explanations that teach: give the right answer, then why the distractors are wrong or how they differ.
- Questions are original practice items, never copied from real exams or third-party question banks.
- `MOCK_SPLIT` must stay fillable from the bank: each domain needs at least that many questions.
- Network+ bank: 365 questions. Domain 1: 102, domain 2: 61, domain 3: 65, domain 4: 58, domain 5: 79. Every objective has at least 10 questions. Questions 147–218 were written to fill the gaps a coverage check against the Network+ study guide found, especially 1.2 and 2.4, which had none. Questions 219–266 added domain 2 and 4 subtopics from the guide's chapter openings, 267–317 did the same for domains 3 and 5, and 318–364 for domain 1.
- Security+ bank: 338 questions. Domain 1: 46, domain 2: 61, domain 3: 47, domain 4: 97, domain 5: 87, with at least 9 per objective. Questions 174–217 filled domain 3 and 5 subtopics that had no questions, 218–263 did the same for domains 1 and 2, 264–307 for domain 4, and 308–337 for domain 5. Its mock split is 11/20/16/25/18 and the pass mark is 750. They were written from the subtopic lists in the owner's Security+ books, never copied from them.
- A+ Core 1 bank (`A1_Q`): 216 questions. Domain 1: 24, domain 2: 64, domain 3: 56, domain 4: 16, domain 5: 56, at least 8 per objective (questions 144–215 brought every objective up to 8). Mock split 12/21/22/10/25 (weights 13/23/25/11/28%), pass mark 675.
- CISSP bank (`CISSP_Q`): 313 questions. Domains 60/30/50/18/30/25/75/25, at least 5 per objective (62 objectives). Questions 185–312 brought every objective up to 5. Mock split 16/10/13/13/13/12/13/10. `SOC` in `GL` means security operations center, so write out System and Organization Controls for audit reports.
- A+ Core 2 bank (`A2_Q`): 246 questions. Domain 1: 68, domain 2: 70, domain 3: 39, domain 4: 69, with at least 6 per objective. Questions 130–185 added domains 3 and 4, and 186–245 domains 1 and 2. `AD` in `GL` means administrative distance, so write out Active Directory. Mock split 25/25/21/19 (weights 28/28/23/21%), pass mark 700.
- The A+ objective titles in `A1_OBJ` and `A2_OBJ` were written from memory of the 220-1201/1202 objectives, because the owner has no A+ books and the cloud session couldn't reach comptia.org. Check them against the official objectives PDF when one is available, and do a coverage check like the Network+ one.

## Abbreviation behavior (requested by the owner)

- `expand()` spells out the first use of each `GL` abbreviation in a block of text, for example "UDP (User Datagram Protocol)". Questions and explanations always use it.
- Answer choices are expanded only if `S.settings.expandChoices` is on (the default) **and** the question is not a terminology question.
- `isTermQ(correctAnswer)`: if the correct answer contains an abbreviation, the question is testing that term. Its choices stay abbreviated until the user answers, then they are spelled out. This keeps the full name from giving the answer away. Apply the same rule anywhere answer choices are shown, including the mock exam.
- When you add questions that use new abbreviations, add them to `GL`. Check that the question text doesn't reveal the answer once it's expanded.
- `GL` maps each abbreviation to one meaning. PDU means protocol data unit, so power questions spell out "power distribution unit" instead of using PDU. A plural "IPs" is never expanded, because it means IP addresses.

## Review rules

- A missed question goes into `S.review` and `S.missedEver`. It leaves the review queue only after `REVIEW_CLEAR` (2) correct answers in a row, in any mode.
- All answer bookkeeping goes through `recordAnswer(id, ok)`. Use it for any new mode that asks bank questions.
- The Review tab offers the review queue, everything ever missed, and a study plan. The study plan lists weak objectives, meaning those with questions in review or under 70% correct over at least 3 answers. For each it shows key facts from missed questions, links, and per-objective practice.
- Study links are search URLs (YouTube search for "Professor Messer N10-009 <objective> <topic>", and a web search for the CompTIA objectives PDF) plus the two sites' home pages. The cloud environment could not reach professormesser.com or comptia.org, so deep links were never verified. Don't add guessed deep URLs. The objective titles in `OBJ` match the objective map in the Network+ study guide.
- `GUIDE` maps each objective to the chapters that cover it in the owner's Network+ study guide, with each chapter's book page and PDF page. It comes from the book's objective map plus the chapter openings. The study plan lists those chapters as plain text with book page numbers, and the Quick Exams explanation line names them. The PDF page numbers kept in `ch` are unused since the PDFs were removed from the repo.

## Outpost defense (`D` module)

- Each Quick Exam is one night. `startQuiz` calls `D.mount()` and `D.newRound()`. Each question calls `D.wave(i,total)`, which starts the endless spawning. A correct answer calls `D.correct(reward,streak)` (adds ammo). A wrong answer calls `D.wrong()` (adds a brute). `quizResult` calls `D.final()`.
- **Focus mode:** `startQuiz` adds `body.focus-mode`, which hides the cable stripe, header, tabs and footer so only the quiz and the dock show. `route()` removes it on any navigation.
- **Pause:** `setPause(v)` in `D` freezes the fight, shows the `#dPauseMenu` overlay (Resume, Restart exam, Armory, Quit to home), dims the quiz with `body.exam-paused` and sets `#app.inert` so it can't be clicked or tabbed into. P toggles and Esc resumes (`onPauseKey`), and the quiz's own key handler checks `D.isPaused()`. Restart calls the function `startQuiz` registers with `D.setRestart`, which reruns the same question pool with a fresh night. `unmount` and `newRound` always clear the pause.
- The horde spawns without end until the last question is answered. Then `final()` launches a bomber that clears the field, and `win()` advances `S.base.night`. If the wall falls first, the night is lost and the player retries it. Status values are `live`, `air`, `won` and `lost`.
- Zombie variants: `spawn()` picks from `VARIANTS[exam]` ([walker, 30% variant, brute]) and `mkFoe()` applies `FOE` multipliers; `PAL` and `EYE` color them and `TRC` sets tracer colors. A+ Core 1 uses `spark`, `surge` (70% hp, 1.5× speed) and `chassis` (a brute with 130% hp). A+ Core 2 uses `phish`, `rootkit` (125% hp, flickers) and `trojan` (a brute that releases two phishers when killed). Network+ uses `walker` and `brute`. Security+ uses `bot` (a walker with an antenna), `worm` (60% hp, 1.7× speed, drawn by `drawWorm`) and `ransom` (a brute that wipes 3 ammo a second at the wall). `e.t` (`w` or `b`) still decides size, health bars and scrap. Security+ tracers are cyan.
- Economy:
  - Ammo per correct answer depends on the domain tier: Standard (domains 1 and 3) +20; Hard (domains 2 and 4) +25 and 10 scrap; Elite (domain 5) +30 and 15 scrap. Three correct in a row adds 5 bonus scrap.
  - Scrap buys `UPG` base upgrades and weapon upgrades.
  - **XP is spendable currency.** Available XP is `S.xp - S.base.xpSpent`; level still uses total `S.xp`. XP unlocks `WPN` weapons: flame bunker, tesla coil, mortar pit, railgun.
  - `SUPPLY` sells ammo: crate 40 rounds for 15 scrap, pallet 150 for 50 scrap, airdrop 200 for 60 XP. Ammo bought during a night goes straight to the guns; otherwise it goes to `S.base.stock` for the next night.
- The dock is a deliberately single-theme dark "tech-punk" style (`.tp` tokens: cyan, magenta, amber, hazard stripes, scanlines). The rest of the app supports light and dark themes through `:root` tokens.

## Mock exam

90 questions, 90 minutes, split 21/18/17/13/21 by the domain weights (Security+: 11/20/16/25/18, pass 750), with no feedback until submitting. CompTIA mocks open with performance-based questions, like the real exams: `EX.PBQ` lists `PBQ_LIB` generators (matching tasks from existing data, such as `portList()`, `OSI_ITEMS`, `ATTACKS`, `CONTROLS`, `HARDWARE`, `COMMANDS`, `WINTOOLS`, and ordering tasks from `NET_STEPS`, `A1_STEPS`, `MALWARE_STEPS`, `IR_STEPS`). They take the place of multiple-choice questions (trimmed from the largest domains), so the total stays at 90. Each PBQ is worth `PBQ_W` (3) questions, with partial credit per row. `M.pbq[i].sel` holds the chosen option index per row, `M.flag` covers PBQs plus multiple choice, and `M.cur` counts across both, with PBQs first. CISSP sets `CAT:{min,max}`: the mock follows the adaptive exam's rules (no going back, skipping or flagging, `M.done` answered so far) and `catDecision()` ends it after `min` once a 95% confidence interval on percent correct clears the pass percentage, or at `max`; time running out before `min` fails. An exam can override the length, time and scale with `MOCK_N`, `MOCK_MIN`, `SCALE` and `ORG` (read through `MOCK_N()`, `MOCK_MS()`, `SCALE()`, `scaleTxt()` and `passPct()`), plus `mockNote` for the intro. CISSP uses `CAT:{min:100,max:150}`, `MOCK_N:150` (questions built), `MOCK_MIN:180` and a 0–1000 scale with a pass mark of 700. The user can flag questions and jump between them. The score is an estimate, `100 + 800 × percent`, with a pass mark of 720. CompTIA's real scaling isn't public, so keep calling the score an estimate. Unanswered questions count as wrong.

- **Full screen:** `runMock` adds `body.focus-mode` and Start calls `enterFullscreen()` (the browser Fullscreen API, optional and allowed to fail). Submitting or quitting removes focus mode and calls `exitFullscreen()`.
- **Pause:** `M.pausedAt` marks a paused exam. Resuming adds the paused time to `M.ends` and `M.pausedTotal`, so time used excludes pauses. A paused exam is never auto-submitted. The `.mpause` overlay sits outside `#app`, which is made `inert` and dimmed with `body.exam-paused`. P or Esc pauses and resumes.
- **Leaving erases the exam:** quitting from the pause menu or the submit panel, or any hash change while the exam runs (caught by the router's `leaveGuard`), opens a confirmation that leaving erases the exam's progress. "Quit and erase" sets `P.mock = null` and continues to wherever the user was going. `leaveGuard` is cleared in the mock's `cleanup`.
- **Closing or reloading:** a `pagehide` handler sets `pausedAt`, so the exam comes back paused rather than erased. The in-app warning can't run on page unload.
- **Rewards:** `mockRewards()` runs on a pass: `MOCK_REWARD` (150 scrap, 200 ammo to `S.base.stock`) every time, plus each newly unlocked achievement's bonus. `achievementList()` builds the achievements (`pass_<exam>`, `dist_<exam>` at 85% or better, `sweep`), and `S.ach` stores unlocked ones with a date. `load()` grants `pass_<exam>` (marked `retro`) for mocks passed before achievements existed. High Scores shows them with `achPanel()`, and the score card shows the count.

## Saved state

`localStorage["netplus-patch-bay-v1"]`. Every read and write is wrapped in try/catch, and `load()` merges onto `freshState()`. When you add fields, add defaults to `freshState()` or `exFresh()` and merge nested objects in `load()` so older saves still work. Never rename `KEY`, or users lose their progress.

- **Per exam** (`S.ex.net`, `S.ex.sec`, `S.ex.a1`, `S.ex.a2`, `S.ex.cissp`, made by `exFresh()`; the current one is `P`): `qs`, `dom`, `review`, `reviewHits`, `missedEver`, `mock`, `mockLast`, `mockHistory`, `best` (`ports`, `osi`, `subnet`, `quick`, `control`, `attack`, `hardware`, `command`, `wintool`, `concept`, `mock`), `missedPorts`, `answered`. Use `P.<field>` in exam code, never `S.<field>`.
- **Shared:** `xp`, `streak`, `lastDay`, `exam` (last chosen exam), `settings`, `ach` (achievements), and `base` (scrap, night, bestNight, xpSpent, stock, kills, bestKills). Upgrade levels are per exam in `S.base.up.<exam id>`.
- **Migration:** saves from before the exam split kept Network+ progress at the top level with flat `base.up`. `load()` moves them into `S.ex.net` and `S.base.up.net`, and fills `best.mock` from mock history. Saves from before A+ get fresh `a1` and `a2` progress and empty upgrade sets.
- `settings.admin` (`{xp, scrap}`) holds the Settings > Admin switches. Read them through `infXP()` and `infScrap()`. Spend through `spendXP()` and `spendScrap()`, check prices with `hasScrap()` (and `xpAvail()`, which returns `Infinity` when infinite), and show balances with `xpTxt()` and `scrapTxt()` (∞ when on), so any new shop or display respects the switches.
- `settings.playerName` is the optional name on the High Scores score card (`drawScoreCard`, `setupScoreCard`). Shared online high scores were discussed and put on hold; scores stay in localStorage.
- Don't name a local variable `P`; it hides the current exam's progress. Subnet Sprint's problem variable is `pr` for this reason.

## Keeping things in sync

- **README.md** describes every mode and the economy. Update it with every feature change.
- **Artifact copy:** a hosted preview lives at https://claude.ai/artifact/QwEmVjoMpUWVVaMmCt8Nsb (private to the owner). It is built from `index.html` by removing the `<!doctype>`, `<html>`, `<head>` and `<body>` wrapper and the charset and viewport meta tags, then adding `<meta name="claude:viewport-fit-sides" content="cover">` after the `<title>`. Republish it after changes if the session has the Artifact tool. It declares the `downloads` capability so the score card's Save button works there (`claude.use("downloads")`); omit `capabilities` on republish to keep it.
- **Game changes need the owner's approval first.** The owner is playtesting the game side. Before changing anything strictly about the game, such as the outpost defense, zombies, the armory, weapons and upgrades, the economy and rewards, nights and difficulty, or the mini-games' mechanics, describe the proposed change and wait for the owner to approve it. Study content (questions, objectives, study links, mock exam rules) doesn't need this. When unsure which side a change falls on, ask.
- Commits go to `main`. The owner has given standing permission to push working builds to `main` without asking: push once a change passes the syntax check and the relevant browser tests. Don't push builds that fail tests, and still ask before anything destructive, such as force-pushing or rewriting history.

## Testing

- **Syntax:** extract the `<script>` body and run `node --check` on it.
- **Behavior:** Playwright with Chromium. The script is an IIFE, so test against a copy that exposes internals before boot. For example, replace `renderHud();route();\n})();` with `Object.defineProperty(window,'S',{get:()=>S});Object.defineProperty(window,'P',{get:()=>P});\nrenderHud();route();\n})();`. The app opens on the menu, so pick an exam (click `.ocard[data-ex="net"]`) before testing exam views. Test old-format saves still load when you touch `load()`.
- Check for page errors, horizontal overflow at 390px width, and the flows you changed.

## Planned next

- **Books (no longer in the repo):** the owner asked for the study guide PDFs to be removed, so `guides/` and Git LFS are gone (they remain in Git history). The chapter maps in `NET_GUIDE` and `SEC_GUIDE` were built from the Sybex *CompTIA Network+ Study Guide, Sixth Edition*, the *CompTIA Security+ Study Guide, Ninth Edition* and *Security+ Practice Tests, Third Edition* (`SEC_GUIDE.practice` holds each domain's question and answer pages). The Network+ coverage check is done. The planned full Security+ check against the practice tests' subtopic lists would need the owner to provide that PDF again. Questions and explanations must always be written fresh, never copied or closely paraphrased from any book or practice test.
- **Security+ is complete** (phases 1–3: menu, settings, high scores, the Security+ track, and Control Sort and Attack Match). OSI Stack and Control Sort are scavenging missions: `scavenge(game,n,haul)` pays `SCAV[game]` scrap and XP for each correct answer as it happens (OSI 6 scrap and 4 XP; Control Sort 4 scrap and 2 XP per correct pick), and `haulLine` shows the total at the end. Control Sort only uses controls whose category and type are well established; leave out ones that sources classify differently, such as security guards. Next ideas: more A+ questions for the thin objectives, and an A+ coverage check once the owner has the official objectives or a study guide.
