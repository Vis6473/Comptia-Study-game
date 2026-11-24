# Cyber Zombie Attack

A browser study game for CompTIA exams, with a tower-defense game ("the outpost") built into the quizzes. It covers Network+ (N10-009) and Security+ (SY0-701). The owner studies with it daily. It was called Net+ Patch Bay until the owner renamed it. The GitHub repo is `Vis6473/Comptia-Study-game` (renamed from `net-plus-study-game`; the local folder may still use the old name).

## How it's built

- Everything is in **`index.html`**: HTML, CSS and one script wrapped in an IIFE. There is no build step, no framework and no dependencies except Google Fonts (Chakra Petch, IBM Plex Sans, IBM Plex Mono).
- Open the file in a browser to run it, or serve the folder: `python3 -m http.server 8000`.
- Hash routing. Global views: `#menu` (the title screen, and the default with no hash), `#scores` (High Scores), `#settings`. Exam views: `#home`, `#quiz` (Quick Exams), `#mock`, `#review`, plus each exam's mini-games (`#ports`, `#osi` and `#subnet` for Network+; `#ports`, `#control` and `#attack` for Security+). `GLOBAL_VIEWS` and `VIEWS` map hashes to view functions. An exam view with no exam chosen sends you to the menu, and a mini-game the current exam doesn't have falls back to home. A click on a link to the current hash re-runs `route()`.
- **Exams:** `EXAMS` (the `Exams` section, just before Boot) registers each exam: name, code, pass mark, `DOMAINS`, `Q`, `OBJ`, `GUIDE`, `TIER`, `MOCK_SPLIT`, armory (`UPG`, `WPN`) and mini-game list (`games`, keys of `GAMES`). Network+ content is defined as `NET_*` constants. `setExam(id)` points the shared names (`EX`, `P`, `DOMAINS`, `Q`, `OBJ`, `GUIDE`, `TIER`, `MOCK_SPLIT`, `PASS`, `UPG`, `WPN`) at one exam, so most code just uses those names. An exam with `ready:false` shows as coming soon on the menu. Security+ content is the `SEC_*` constants (`SEC_Q`, `SEC_OBJ`, `SEC_GUIDE`, `SEC_UPG`, `SEC_WPN`) in the `Security+ content` section, and `SEC_DOMAINS` and `GAMES` sit in the `Exams` section.
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
| Mini games | Port Blitz, OSI Stack, Subnet Sprint (Network+); Control Sort and Attack Match (Security+), with data in `CTRL_CATS`, `CTRL_TYPES`, `CONTROLS` and `ATTACKS` |
| Exams | `SEC_DOMAINS`, `GAMES`, `EXAMS`, and the `let` bindings that `setExam` sets |

## Question bank rules

Each question is one line in `Q`:

```js
[domain, "question", "correct answer", ["wrong", "wrong", "wrong"], "explanation", "objective"]
// e.g. [5, "Which tool ...?", "OTDR", ["Toner probe", "Loopback plug", "Multimeter"], "An optical ...", "5.5"]
```

- Each exam has its own bank (`NET_Q`, `SEC_Q`), and `Q` points at the current one. Indexes are per bank.
- **Append new questions to the end of the bank.** Never insert in the middle or reorder.** Saved progress (`S.qs`, `S.review`, `S.reviewHits`, `S.missedEver`, mock exam state) refers to questions by array index. Inserting earlier in the list shifts every later question and scrambles saved progress. This already happened once, when 10 domain 2 and 3 questions were inserted mid-list in commit `eeac48e`. Since then, new questions only go at the end.
- The objective tag must be a key of `OBJ` and must start with the question's domain number.
- Write explanations that teach: give the right answer, then why the distractors are wrong or how they differ.
- Questions are original practice items, never copied from real exams or third-party question banks.
- `MOCK_SPLIT` must stay fillable from the bank: each domain needs at least that many questions.
- Network+ bank: 365 questions. Domain 1: 102, domain 2: 61, domain 3: 65, domain 4: 58, domain 5: 79. Every objective has at least 10 questions. Questions 147–218 were written to fill the gaps a coverage check against the Network+ study guide found, especially 1.2 and 2.4, which had none. Questions 219–266 added domain 2 and 4 subtopics from the guide's chapter openings, 267–317 did the same for domains 3 and 5, and 318–364 for domain 1.
- Security+ bank: 338 questions. Domain 1: 46, domain 2: 61, domain 3: 47, domain 4: 97, domain 5: 87, with at least 9 per objective. Questions 174–217 filled domain 3 and 5 subtopics that had no questions, 218–263 did the same for domains 1 and 2, 264–307 for domain 4, and 308–337 for domain 5. Its mock split is 11/20/16/25/18 and the pass mark is 750. They were written from the subtopic lists in the owner's Security+ books, never copied from them.

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
- `GUIDE` maps each objective to the chapters that cover it in the owner's Network+ study guide, with each chapter's book page and PDF page. It comes from the book's objective map plus the chapter openings. The study plan lists those chapters, and the Quick Exams explanation line names them. Chapter links into the PDF (`#page=N`) appear only when the PDF is reachable: when the app is opened from a local checkout, or served from the repo with the LFS file present. Everywhere else, such as the Artifact preview, the chapters show as plain text.

## Outpost defense (`D` module)

- Each Quick Exam is one night. `startQuiz` calls `D.mount()` and `D.newRound()`. Each question calls `D.wave(i,total)`, which starts the endless spawning. A correct answer calls `D.correct(reward,streak)` (adds ammo). A wrong answer calls `D.wrong()` (adds a brute). `quizResult` calls `D.final()`.
- **Focus mode:** `startQuiz` adds `body.focus-mode`, which hides the cable stripe, header, tabs and footer so only the quiz and the dock show. `route()` removes it on any navigation.
- **Pause:** `setPause(v)` in `D` freezes the fight, shows the `#dPauseMenu` overlay (Resume, Restart exam, Armory, Quit to home), dims the quiz with `body.exam-paused` and sets `#app.inert` so it can't be clicked or tabbed into. P toggles and Esc resumes (`onPauseKey`), and the quiz's own key handler checks `D.isPaused()`. Restart calls the function `startQuiz` registers with `D.setRestart`, which reruns the same question pool with a fresh night. `unmount` and `newRound` always clear the pause.
- The horde spawns without end until the last question is answered. Then `final()` launches a bomber that clears the field, and `win()` advances `S.base.night`. If the wall falls first, the night is lost and the player retries it. Status values are `live`, `air`, `won` and `lost`.
- Zombie variants: `spawn()` sets `e.v`. Network+ uses `walker` and `brute`. Security+ uses `bot` (a walker with an antenna), `worm` (60% hp, 1.7× speed, drawn by `drawWorm`) and `ransom` (a brute that wipes 3 ammo a second at the wall). `e.t` (`w` or `b`) still decides size, health bars and scrap. Security+ tracers are cyan.
- Economy:
  - Ammo per correct answer depends on the domain tier: Standard (domains 1 and 3) +20; Hard (domains 2 and 4) +25 and 10 scrap; Elite (domain 5) +30 and 15 scrap. Three correct in a row adds 5 bonus scrap.
  - Scrap buys `UPG` base upgrades and weapon upgrades.
  - **XP is spendable currency.** Available XP is `S.xp - S.base.xpSpent`; level still uses total `S.xp`. XP unlocks `WPN` weapons: flame bunker, tesla coil, mortar pit, railgun.
  - `SUPPLY` sells ammo: crate 40 rounds for 15 scrap, pallet 150 for 50 scrap, airdrop 200 for 60 XP. Ammo bought during a night goes straight to the guns; otherwise it goes to `S.base.stock` for the next night.
- The dock is a deliberately single-theme dark "tech-punk" style (`.tp` tokens: cyan, magenta, amber, hazard stripes, scanlines). The rest of the app supports light and dark themes through `:root` tokens.

## Mock exam

90 questions, 90 minutes, split 21/18/17/13/21 by the domain weights (Security+: 11/20/16/25/18, pass 750), with no feedback until submitting. The user can flag questions and jump between them. The score is an estimate, `100 + 800 × percent`, with a pass mark of 720. CompTIA's real scaling isn't public, so keep calling the score an estimate. Unanswered questions count as wrong.

- **Full screen:** `runMock` adds `body.focus-mode` and Start calls `enterFullscreen()` (the browser Fullscreen API, optional and allowed to fail). Submitting or quitting removes focus mode and calls `exitFullscreen()`.
- **Pause:** `M.pausedAt` marks a paused exam. Resuming adds the paused time to `M.ends` and `M.pausedTotal`, so time used excludes pauses. A paused exam is never auto-submitted. The `.mpause` overlay sits outside `#app`, which is made `inert` and dimmed with `body.exam-paused`. P or Esc pauses and resumes.
- **Leaving erases the exam:** quitting from the pause menu or the submit panel, or any hash change while the exam runs (caught by the router's `leaveGuard`), opens a confirmation that leaving erases the exam's progress. "Quit and erase" sets `P.mock = null` and continues to wherever the user was going. `leaveGuard` is cleared in the mock's `cleanup`.
- **Closing or reloading:** a `pagehide` handler sets `pausedAt`, so the exam comes back paused rather than erased. The in-app warning can't run on page unload.

## Saved state

`localStorage["netplus-patch-bay-v1"]`. Every read and write is wrapped in try/catch, and `load()` merges onto `freshState()`. When you add fields, add defaults to `freshState()` or `exFresh()` and merge nested objects in `load()` so older saves still work. Never rename `KEY`, or users lose their progress.

- **Per exam** (`S.ex.net`, `S.ex.sec`, made by `exFresh()`; the current one is `P`): `qs`, `dom`, `review`, `reviewHits`, `missedEver`, `mock`, `mockLast`, `mockHistory`, `best` (`ports`, `osi`, `subnet`, `quick`, `control`, `attack`, `mock`), `missedPorts`, `answered`. Use `P.<field>` in exam code, never `S.<field>`.
- **Shared:** `xp`, `streak`, `lastDay`, `exam` (last chosen exam), `settings`, and `base` (scrap, night, bestNight, xpSpent, stock, kills, bestKills). Upgrade levels are per exam in `S.base.up.net` and `S.base.up.sec`.
- **Migration:** saves from before the exam split kept Network+ progress at the top level with flat `base.up`. `load()` moves them into `S.ex.net` and `S.base.up.net`, and fills `best.mock` from mock history.
- Don't name a local variable `P`; it hides the current exam's progress. Subnet Sprint's problem variable is `pr` for this reason.

## Keeping things in sync

- **README.md** describes every mode and the economy. Update it with every feature change.
- **Artifact copy:** a hosted preview lives at https://claude.ai/artifact/QwEmVjoMpUWVVaMmCt8Nsb (private to the owner). It is built from `index.html` by removing the `<!doctype>`, `<html>`, `<head>` and `<body>` wrapper and the charset and viewport meta tags, then adding `<meta name="claude:viewport-fit-sides" content="cover">` after the `<title>`. Republish it after changes if the session has the Artifact tool.
- Commits go to `main`, but only when the owner asks. The owner has asked for a push after each round of changes so far.

## Testing

- **Syntax:** extract the `<script>` body and run `node --check` on it.
- **Behavior:** Playwright with Chromium. The script is an IIFE, so test against a copy that exposes internals before boot. For example, replace `renderHud();route();\n})();` with `Object.defineProperty(window,'S',{get:()=>S});Object.defineProperty(window,'P',{get:()=>P});\nrenderHud();route();\n})();`. The app opens on the menu, so pick an exam (click `.ocard[data-ex="net"]`) before testing exam views. Test old-format saves still load when you touch `load()`.
- Check for page errors, horizontal overflow at 390px width, and the flows you changed.

## Planned next

- **Security+ books:** the Sybex *CompTIA Security+ Study Guide, Ninth Edition* (17 chapters) and *Security+ Practice Tests, Third Edition* (one chapter per domain, answers in an appendix). Both PDFs are scanned images with no text layer, so reading them needs OCR (`apt-get install tesseract-ocr`, render pages with `pdftoppm -r 150 -gray`, run `tesseract` with `OMP_THREAD_LIMIT=1` and several processes in parallel, which takes about 0.6 s a page). `SEC_GUIDE` holds the study guide chapter map (from its objective map) and, in `practice`, each domain's question and answer pages in the practice tests book. Never copy the practice tests' questions into the app.
- **Study guides:** the Network+ guide is the Sybex *CompTIA Network+ Study Guide, Sixth Edition* (N10-009), a scanned 1,000-page PDF with searchable text, so `pdftotext -layout` works on it. Its PDF page numbers run about 41–50 pages ahead of the printed page numbers, and the gap grows in later chapters. The coverage check is done (see the bank note above). The owner's PDFs are in `guides/`, stored with Git LFS (see `.gitattributes`): a CompTIA Network+ Study Guide (561 MB), a Security+ SY0-701 Study Guide, Ninth Edition (189 MB), and Security+ SY0-701 Practice Tests, Third Edition (48 MB). Fetch only the file you need with `git lfs pull --include "<path>"`, not all of them. A plain clone gives small pointer files, not PDFs. Use the guides to check the bank's coverage of the objectives, find weak spots, and link questions to chapters. They are copyrighted books: the repo must stay private, and the app's questions and explanations must be written fresh, never copied or closely paraphrased from the books or their practice tests.
- **Security+ is complete** (phases 1–3: menu, settings, high scores, the Security+ track, and Control Sort and Attack Match). OSI Stack and Control Sort are scavenging missions: `scavenge(game,n,haul)` pays `SCAV[game]` scrap and XP for each correct answer as it happens (OSI 6 scrap and 4 XP; Control Sort 4 scrap and 2 XP per correct pick), and `haulLine` shows the total at the end. Control Sort only uses controls whose category and type are well established; leave out ones that sources classify differently, such as security guards. Next ideas: a full Security+ check against the practice tests' subtopic lists, like the Network+ coverage check.
