# Net+ Patch Bay

A browser study game for the CompTIA Network+ exam (N10-009), with a tower-defense game ("the outpost") built into the quizzes. The owner studies with it daily and plans to add Security+ (SY0-701) as a second exam track.

## How it's built

- Everything is in **`index.html`**: HTML, CSS and one script wrapped in an IIFE. There is no build step, no framework and no dependencies except Google Fonts (Chakra Petch, IBM Plex Sans, IBM Plex Mono).
- Open the file in a browser to run it, or serve the folder: `python3 -m http.server 8000`.
- Hash routing: `#home`, `#quiz` (Quick Exams), `#mock`, `#ports`, `#osi`, `#subnet`, `#review`. `VIEWS` maps hashes to view functions. A click on a link to the current hash re-runs `route()`, so "Review" links work from the review screen.
- Every view that adds timers or key listeners sets the global `cleanup`. `route()` calls it and also calls `D.unmount()`.

### Main sections of the script (in order)

| Section | What it holds |
|---|---|
| Content | `DOMAINS` (name, exam weight %, color), `Q` (question bank), `PORTS`, `LAYERS`, `OSI_ITEMS` |
| State | `KEY`, `freshState()`, `load()`, `save()`, `award(xp)` |
| Abbreviations | `GL` glossary, `expand(text)`, `isTermQ(answer)`, `choice(option)` |
| Outpost economy | `TIER`/`TIERS` (rewards per domain), `UPG` (scrap upgrades), `WPN` (XP weapons), `SUPPLY` (ammo), shop HTML |
| Outpost defense | `D`, a canvas tower-defense module in a fixed bottom dock |
| Quiz | `startQuiz(pool,label,again)`, `showQ`, `quizResult`, `recordAnswer(id,ok)` |
| Objectives | `OBJ` (N10-009 objective titles plus a video search topic), `SRC` (study links), study plan in `viewReview` |
| Mock exam | `MOCK_SPLIT`, `buildMock`, `runMock`, `submitMock`, `mockResults` |
| Mini games | Port Blitz, OSI Stack, Subnet Sprint |

## Question bank rules

Each question is one line in `Q`:

```js
[domain, "question", "correct answer", ["wrong", "wrong", "wrong"], "explanation", "objective"]
// e.g. [5, "Which tool ...?", "OTDR", ["Toner probe", "Loopback plug", "Multimeter"], "An optical ...", "5.5"]
```

- **Append new questions to the end of `Q`. Never insert in the middle or reorder.** Saved progress (`S.qs`, `S.review`, `S.reviewHits`, `S.missedEver`, mock exam state) refers to questions by array index. Inserting earlier in the list shifts every later question and scrambles saved progress. This already happened once, when 10 domain 2 and 3 questions were inserted mid-list in commit `eeac48e`. Since then, new questions only go at the end.
- The objective tag must be a key of `OBJ` and must start with the question's domain number.
- Write explanations that teach: give the right answer, then why the distractors are wrong or how they differ.
- Questions are original practice items, never copied from real exams or third-party question banks.
- `MOCK_SPLIT` must stay fillable from the bank: each domain needs at least that many questions.
- Current bank: 147 questions. Domain 1: 22, domain 2: 21, domain 3: 20, domain 4: 35, domain 5: 49.

## Abbreviation behavior (requested by the owner)

- `expand()` spells out the first use of each `GL` abbreviation in a block of text, for example "UDP (User Datagram Protocol)". Questions and explanations always use it.
- Answer choices are expanded only if `S.settings.expandChoices` is on (the default) **and** the question is not a terminology question.
- `isTermQ(correctAnswer)`: if the correct answer contains an abbreviation, the question is testing that term. Its choices stay abbreviated until the user answers, then they are spelled out. This keeps the full name from giving the answer away. Apply the same rule anywhere answer choices are shown, including the mock exam.
- When you add questions that use new abbreviations, add them to `GL`. Check that the question text doesn't reveal the answer once it's expanded.

## Review rules

- A missed question goes into `S.review` and `S.missedEver`. It leaves the review queue only after `REVIEW_CLEAR` (2) correct answers in a row, in any mode.
- All answer bookkeeping goes through `recordAnswer(id, ok)`. Use it for any new mode that asks bank questions.
- The Review tab offers the review queue, everything ever missed, and a study plan. The study plan lists weak objectives, meaning those with questions in review or under 70% correct over at least 3 answers. For each it shows key facts from missed questions, links, and per-objective practice.
- Study links are search URLs (YouTube search for "Professor Messer N10-009 <objective> <topic>", and a web search for the CompTIA objectives PDF) plus the two sites' home pages. The cloud environment could not reach professormesser.com or comptia.org, so deep links were never verified. Don't add guessed deep URLs. The objective titles in `OBJ` were also written from memory, so check them against the official PDF when it's available.

## Outpost defense (`D` module)

- Each Quick Exam is one night. `startQuiz` calls `D.mount()` and `D.newRound()`. Each question calls `D.wave(i,total)`, which starts the endless spawning. A correct answer calls `D.correct(reward,streak)` (adds ammo). A wrong answer calls `D.wrong()` (adds a brute). `quizResult` calls `D.final()`.
- The horde spawns without end until the last question is answered. Then `final()` launches a bomber that clears the field, and `win()` advances `S.base.night`. If the wall falls first, the night is lost and the player retries it. Status values are `live`, `air`, `won` and `lost`.
- Economy:
  - Ammo per correct answer depends on the domain tier: Standard (domains 1 and 3) +20; Hard (domains 2 and 4) +25 and 10 scrap; Elite (domain 5) +30 and 15 scrap. Three correct in a row adds 5 bonus scrap.
  - Scrap buys `UPG` base upgrades and weapon upgrades.
  - **XP is spendable currency.** Available XP is `S.xp - S.base.xpSpent`; level still uses total `S.xp`. XP unlocks `WPN` weapons: flame bunker, tesla coil, mortar pit, railgun.
  - `SUPPLY` sells ammo: crate 40 rounds for 15 scrap, pallet 150 for 50 scrap, airdrop 200 for 60 XP. Ammo bought during a night goes straight to the guns; otherwise it goes to `S.base.stock` for the next night.
- The dock is a deliberately single-theme dark "tech-punk" style (`.tp` tokens: cyan, magenta, amber, hazard stripes, scanlines). The rest of the app supports light and dark themes through `:root` tokens.

## Mock exam

90 questions, 90 minutes, split 21/18/17/13/21 by the domain weights, with no feedback until submitting. The user can flag questions, jump between them, and resume later (state lives in `S.mock` and the clock keeps running). It auto-submits when time runs out. The score is an estimate, `100 + 800 × percent`, with a pass mark of 720. CompTIA's real scaling isn't public, so keep calling the score an estimate. Unanswered questions count as wrong.

## Saved state

`localStorage["netplus-patch-bay-v1"]`. Every read and write is wrapped in try/catch, and `load()` merges onto `freshState()`. When you add fields, add defaults to `freshState()` and merge nested objects in `load()` so older saves still work. Never rename `KEY`, or users lose their progress.

## Keeping things in sync

- **README.md** describes every mode and the economy. Update it with every feature change.
- **Artifact copy:** a hosted preview lives at https://claude.ai/artifact/QwEmVjoMpUWVVaMmCt8Nsb (private to the owner). It is built from `index.html` by removing the `<!doctype>`, `<html>`, `<head>` and `<body>` wrapper and the charset and viewport meta tags, then adding `<meta name="claude:viewport-fit-sides" content="cover">` after the `<title>`. Republish it after changes if the session has the Artifact tool.
- Commits go to `main`, but only when the owner asks. The owner has asked for a push after each round of changes so far.

## Testing

- **Syntax:** extract the `<script>` body and run `node --check` on it.
- **Behavior:** Playwright with Chromium. The script is an IIFE, so test against a copy that exposes internals before boot. For example, replace `renderHud();route();\n})();` with `window.Q=Q;window.expand=expand;Object.defineProperty(window,'S',{get:()=>S});\nrenderHud();route();\n})();`.
- Check for page errors, horizontal overflow at 390px width, and the flows you changed.

## Planned next

- **Study guides:** the owner's PDFs are in `guides/`, stored with Git LFS (see `.gitattributes`): a CompTIA Network+ Study Guide (561 MB), a Security+ SY0-701 Study Guide, Ninth Edition (189 MB), and Security+ SY0-701 Practice Tests, Third Edition (48 MB). Fetch only the file you need with `git lfs pull --include "<path>"`, not all of them. A plain clone gives small pointer files, not PDFs. Use the guides to check the bank's coverage of the objectives, find weak spots, and link questions to chapters. They are copyrighted books: the repo must stay private, and the app's questions and explanations must be written fresh, never copied or closely paraphrased from the books or their practice tests.
- **Security+ track:** add Security+ (SY0-701) as a second exam with an exam picker, its own domains, weights, objectives, question bank and mock split. The outpost, armory, XP and review should carry across both exams. Propose the design to the owner before building it.
