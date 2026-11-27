# Cyber Zombie Attack

A browser study game for **CompTIA Network+ (N10-009)**, **CompTIA Security+ (SY0-701)**, **CompTIA A+**, which is split into its two exams, **A+ Core 1 (220-1201)** and **A+ Core 2 (220-1202)**, and **ISC2 CISSP**. You answer exam questions to keep a zombie horde off your outpost. It is a single HTML file with no build step and no dependencies apart from Google Fonts.

## Main menu, settings and high scores

- **Main menu:** the title screen where you pick the exam to study. Each exam card shows your accuracy, questions seen, review queue and best mock score. Use **Menu** in the tabs, or the logo, to switch exams.
- **Exam home page:** the Exam domains card shows your overall accuracy, how much of the question bank you've covered, how many questions you've ever missed, and your mock exam count and best score. Under each domain's bar are its answers (right and wrong), questions seen out of the bank, questions never missed, a link to any of its questions in review, and its weakest objective.
- **Settings:** turn spelled-out abbreviations in answer choices on or off, and reset any one exam's progress, the outpost, or everything. Each reset asks you to confirm first.
- **High scores:** the outpost's records (highest night, most undead in one night, total kills, level) and, for each exam, the best mock score, best quick exam, mini-game records and recent mock attempts.
- **Score card:** High Scores draws a 1200×630 image of your records, with an optional name. Save it as a PNG, copy it, share it from a phone through the share sheet, or open a post on X with your scores as text and attach the image. Scores stay on your device; there is no online leaderboard yet.
- **Progress:** each exam keeps its own stats, review queue, mock exams and high scores. XP, your level, your streak and the outpost are shared, but each exam has its own base upgrades and weapons.

## Music

Relaxing 8-bit background music with a survival-horror mood plays while you study: slow minor-key loops like a safe room between fights, with a music-box melody, a low drone, a soft echo and the odd eerie note. Each mode has its own original tune: the menu screens (main menu, High Scores, Settings), your exam pages (home, Armory, Review), quick exam nights (with a faint heartbeat) and the mini-games. The mock exam is always silent.

During quick exam nights, very quiet sound effects play for the outpost and the horde: turret fire, rifles, tank cannons, mortars, explosions, tesla zaps, the flamethrower, the railgun and jets, plus zombie groans, squishes, thuds against the wall, spitters and the super boss's roar. Sounds are panned by where they happen on the field and limited so a busy night stays quiet.

Everything is synthesized in the browser, so there are no audio files. Sound starts after your first click or key press, because browsers don't allow it before that, and pauses while the tab is in the background. Settings has separate on/off switches and volume sliders for music and sound effects, and a night's pause menu has Music and Sounds buttons.

## Network+ modes

- **Quick Exams + Outpost Defense:** 10-question rounds drawn from 365 practice questions across all five exam domains, with an explanation after every answer. Every question is tagged with its N10-009 objective. Each quick exam is also a night of defense in the bottom half of the screen. The undead spawn without end until you answer the last question, and correct answers resupply the guns. Then a bomber makes a slow pass, dropping a bomb on each zombie it flies over, timed to land where that zombie will be. It also carpet-bombs the whole field with three rows of large cyan, magenta, yellow and black toner bombs. Once the field is clear, the next night begins. Press 1–4 to answer and Enter to continue.
- **Mock Exam:** a timed 90-question, 90-minute exam that runs like the real N10-009. It opens with 3 performance-based questions (matching ports, placing items on the OSI model, and ordering the troubleshooting steps), each worth 3 multiple-choice questions with partial credit, followed by 87 multiple-choice questions split by the domain weights. It opens full screen, with only the exam on screen, and also asks the browser for real full screen where that's allowed. You get no feedback until you submit. You can flag questions and jump around with the question grid. **Pause** (or P / Esc) stops the clock and covers the exam with a pause menu: resume, or quit. Quitting, or trying to leave the exam any other way, warns you first that leaving erases all of that exam's progress. Closing or reloading the page pauses the exam, so it's waiting for you, paused, when you come back. Results show an estimated 100–900 score (pass at 720), a breakdown by domain, your performance-based answers next to the correct ones, and every missed question with its explanation. Misses go into your review queue. Passing pays rewards and achievements (see below).
- **Port Blitz:** 60 seconds of matching services and port numbers. Each wrong answer costs 3 seconds. Includes a port reference table.
- **OSI Stack:** a scavenging mission. Put devices, protocols and PDUs on the correct OSI layer, 12 items per round. Each correct layer brings back 6 scrap and 4 XP straight away.
- **Subnet Sprint:** endless random subnetting problems (network and broadcast address, host range, host count, mask) with a worked binary breakdown after each one.
- **Answer feedback:** after you answer, the choices are replaced by the verdict (the correct answer, and what you picked if you were wrong), and the explanation fills the space above the outpost, with Next always in view.
- **Question selection:** each quick exam includes up to 3 questions from your review queue, then questions you haven't seen yet, then the ones you've seen, weakest first.
- **Review:** every question you miss goes into a review queue and stays there until you answer it correctly twice in a row. You can also practice every question you've ever missed. A study plan lists the exam objectives you're weakest on, with the key facts from the questions you missed, the chapters and page numbers that cover it in the Sybex CompTIA Network+ Study Guide, links to Professor Messer's videos and CompTIA's exam objectives, and a button to practice just that objective.

## Security+ modes

- **Quick Exams + Outpost Defense:** 10-question rounds from 338 original Security+ questions covering all 28 SY0-701 objectives, with at least 9 per objective. Security+ nights bring their own zombies (see below).
- **Mock Exam:** 90 questions in 90 minutes: 3 performance-based questions (identifying attacks, classifying control types, and ordering the incident response phases), then 87 multiple-choice questions split by the domain weights (12/22/18/28/20%). The pass mark is 750 on the 100–900 scale.
- **Port Blitz:** the same port drill as Network+, with its own high score.
- **Control Sort:** classify 10 security controls by category (technical, managerial, operational, physical) and by type (preventive, deterrent, detective, corrective, compensating, directive). Each correct pick is a point, out of 20, and a scavenging mission that brings back 4 scrap and 2 XP straight away.
- **Attack Match:** 60 seconds to name the attack behind each indicator or scenario, such as password spraying, an evil twin or a logic bomb. A wrong answer costs 3 seconds, and the attacks you missed are listed at the end.
- **Review:** the same review queue and study plan as Network+. Each weak objective links to its chapters in the Security+ Study Guide and to that domain's chapter in the Security+ Practice Tests book, with the question and answer pages.

## CISSP modes (ISC2)

- **Quick Exams + Outpost Defense:** 10-question rounds from 313 original questions covering all 62 objectives in the eight CISSP domains (2024 outline), with at least 5 per objective.
- **Mock Exam:** follows the real CISSP's adaptive rules: 100 to 150 questions in up to 3 hours, and you can't go back, skip or flag. After question 100 the exam ends as soon as your result is clear with 95% confidence; otherwise it runs to 150. Running out of time before question 100 is a fail. It can't pick questions by difficulty like the real exam, so it uses this statistical stopping rule instead. Scores are estimated on ISC2's 0–1000 scale, with a pass mark of 700.
- **Concept Match:** 60 seconds to name CISSP concepts from their descriptions: security models such as Bell-LaPadula and Biba, risk terms, access control models, federation, recovery sites, crypto attacks and more.
- **Attack Match:** the same attack drill as Security+, with its own high score.
- **Review:** the review queue and study plan, with a CISSP video search for each weak objective and a link to find ISC2's exam outline.

## A+ Core 1 modes (220-1201)

- **Quick Exams + Outpost Defense:** 10-question rounds from 216 original questions covering all 27 Core 1 objectives, with at least 8 per objective across mobile devices, networking, hardware, virtualization and cloud, and hardware and network troubleshooting.
- **Mock Exam:** 90 questions in 90 minutes: 3 performance-based questions (ports, hardware, and ordering the troubleshooting steps), then 87 multiple-choice questions split by the domain weights (13/23/25/11/28%). The pass mark is 675 on the 100–900 scale.
- **Port Blitz:** the port drill, limited to the 15 ports the A+ objectives list (including NetBIOS 137–139), with its own high score.
- **Hardware Match:** 60 seconds to name connectors, cables, components, printer parts and tools from their descriptions.
- **Review:** the same review queue and study plan, with Professor Messer and CompTIA objective links for each weak objective. There's no A+ study guide mapped yet, so no chapter references.

## A+ Core 2 modes (220-1202)

- **Quick Exams + Outpost Defense:** 10-question rounds from 246 original questions covering all 36 Core 2 objectives, with at least 6 per objective across operating systems, security, software troubleshooting and operational procedures.
- **Mock Exam:** 90 questions in 90 minutes: 3 performance-based questions (commands, Windows tools, and ordering the malware removal steps), then 87 multiple-choice questions split by the domain weights (28/28/23/21%). The pass mark is 700.
- **Command Match:** 60 seconds to pick the Windows or Linux command for each job, from ipconfig /flushdns to chmod.
- **Tool Match:** 60 seconds to pick the Windows tool or settings page for each job, such as Event Viewer, Disk Management or msconfig.
- **Review:** the same review queue and study plan as Core 1.

## Mock exam rewards and achievements

- **Every pass** pays 150 scrap and 200 rounds of ammo, stockpiled for your next night.
- **Achievements** pay a one-time bonus: passing each exam's mock (250 scrap, 300 ammo), passing with distinction at 85% or better (150 scrap, 150 ammo), and Clean sweep for passing every exam's mock (500 scrap, 500 ammo).
- High Scores lists every achievement, and the score card shows how many you've unlocked. Mocks you passed before achievements existed unlock their achievement without the bonus.
- **Weapon transfer:** passing a mock exam also lets you send one of that exam's unique weapons to another exam: Network+'s Tank bunker, Security+'s Drone depot, EDR pulse or Honeypot mine, A+ Core 1's Toner bomb jets, A+ Core 2's Cable bot or Disk wipe stun mortar, or CISSP's Incident response team or Cryptographic mine. It replaces the other exam's weapon in the same slot, at the level it has in its home exam (at least 1), and you keep upgrading it there. A borrowed weapon has a Send back button in the Armory, which returns it home and gives the exam its own weapon back. Each exam holds one borrowed weapon, and you get one pick per pass, so a later pass can swap it.

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

- **A+ rewards:** Core 1 pays Standard for 1.0 Mobile Devices and 4.0 Virtualization and Cloud Computing, Hard for 2.0 Networking and 3.0 Hardware, and Elite for 5.0 Hardware and Network Troubleshooting. Core 2 pays Standard for 4.0 Operational Procedures, Hard for 1.0 Operating Systems and 2.0 Security, and Elite for 3.0 Software Troubleshooting. CISSP pays Standard for domains 2, 5 and 6, Hard for 1, 4, 7 and 8, and Elite for 3.0 Security Architecture and Engineering.
- **Zombies:** Network+ nights bring walkers and brutes. Security+ nights bring botnet zombies, fast fragile worms and ransomware brutes, which encrypt (wipe) 3 rounds of ammo every second they stay at the wall. A+ Core 1 nights bring static-charged sparks, fast power surges and armored chassis brutes with 30% more health. A+ Core 2 nights bring phishers, rootkits that flicker half out of sight with extra health, and trojan brutes that release two phishers when they're destroyed. CISSP nights bring insiders in suits, fast spies, and APT brutes that heal 3% of their health every second unless you finish them off.
- **Wrong answers** draw an extra brute into the fight (a ransomware brute in Security+). Three correct answers in a row earn bonus scrap.
- **Scrap** is shared by every exam. It buys base upgrades (heavy caliber, autoloader, extra turret mounts, wall plating, ammo cache) and weapon upgrades. You also earn scrap from kills, survived nights and the mini-games.
- **Armory tab:** every exam has an Armory tab with your loadout (turrets, damage per round, fire rate, wall, starting and bonus ammo, and weapon levels), the full shop, and a horde guide showing each zombie's health, time to reach the wall and wall damage on your current night.
- **Ammo supplies:** buy ammo crates and pallets with scrap, or an airdrop of 200 rounds with XP. During a night the ammo goes straight to the guns. Otherwise it's stockpiled for your next night.
- **XP is currency:** spend it in the Armory to attach new weapons to the base. Each exam has its own upgrades and weapons. Network+ has Flame bunker (150 XP), Tesla coil (300), Tank bunker (450) and Railgun (650). Security+ has the Drone depot, EDR pulse, Honeypot mine and Kill switch at the same prices, and its base upgrades are Patch level, Threat feed, Sensor node, Hardened firewall and Backup cache. A+ Core 1 has the Overheat vent, ESD arc, Toner bomb and Laser printer beam, with Overclocked turrets, Liquid cooling, Expansion slot, Surge protector and RAM upgrade. A+ Core 2 has the Cable bot, Group Policy chain, Disk wipe charge and Safe Mode beam, with Admin rights, Task Scheduler, Remote session, BitLocker wall and Restore point. CISSP has the Incident response team, Kill chain breaker, Cryptographic mine and Zero Trust lance, with Defense in depth, Continuous monitoring, Security architecture, Hardened perimeter and Risk reserve. Your level still counts all the XP you've ever earned.
- **Each weapon fights differently**, and each gets its own structure at the base:
  - **Flame weapons** (Flame bunker and its equivalents) burn zombies near the wall continuously and set them on fire, so they keep burning for a couple of seconds. They carry 10 s of fuel at level 1, 15 s at level 2 and 20 s at level 3, used only while firing. An empty tank cools down to refuel (8 s at level 1, down to 5 s at level 3), and the recharge bar shows the fuel left.
  - **Cable bot** (A+ Core 2, replacing the Quarantine pit, upgrades to level 4): a small tracked bot drives out of the base and slowly strings coils of Ethernet barbed wire across the field between the 25 m and 150 m markers, in a staggered belt across three rows, nearest the wall first. Level 1 strings 4 fences of thin beige RJ11 with little plugs for barbs, level 2 6 fences of thicker blue-and-white twisted RJ45, level 3 8 fences of aqua fiber whose ends pulse slowly with light, and level 4 turns them into 8 laser fences. Each upgrade also lengthens every fence's cable: it covers 55% of its row at level 1, 75% at level 2, 95% at level 3 and 110% at level 4. Zombies in a fence move at 60%, 50%, 40% or 30% speed (bosses get half the slowdown) and take a very little damage (0.2 to 0.8 a second). Each fence has durability (40, 70, 110 or 160) that zombies wear down as they push through, shown by a bar over damaged fences. A cut fence disappears, and the bot comes back to rebuild it, or patches fences that drop below 60%. Zombies go after the bot: they veer toward it when it's just ahead of them and stop to attack it when they touch it. It has 30, 45, 60 or 80 health by level, and a destroyed bot has to be rebuilt in its shed, a second cooldown of 25, 20, 15 or 12 s, before it rolls out again. The base structure is a cable shed with spools, showing how many fences are up. Its first bar shows the fences' durability left, and its second shows the bot's health, or its rebuild progress with a countdown under the shed.
  - **Drone depot** (Security+, replacing the Sandbox trap): 5 suicide drones at level 1, 10 at level 2 and 15 at level 3. They launch from the depot on their own and hover in a line 25 m out. When a zombie comes within 100 m of the wall, the nearest hovering drone dives at it and blows up with splash damage. Each drone takes its own target, except brutes and bosses, which several drones can hit at once. Another 5 drones stay stockpiled on the launch pad, ready to replace a drone the moment it dives, and the depot shows how many are ready. The depot builds a replacement for each spent drone over time. It's drawn as a small factory. Robot arms weld new drones just inside the hangar door, with sparks flying. Finished drones roll out of the door onto a conveyor belt, ride it to a small launch pad and queue there until they take off. The drone on the pad refuels before it launches: a hose from a fuel post pulses with fuel, and a gauge over the pad fills until the next launch, then turns green. Each take-off kicks up a downwash ring and dust, and the drone rises straight off the pad before flying out.
  - **Exam boost:** every weapon on Security+ and A+ Core 2 deals 15% more damage, so those two exams can reach night 150 like the others.
  - **Incident response teams** (CISSP) are field squads of armored orbital drop troopers instead of a flame weapon. Each restock starts in the yard: a small shuttle lands on the launch pad, troopers run out of the command post and board it, and it blasts off the top of the screen. Then an orbital ship flies slowly across the top of the field and drops a pod for every open slot, so the ship's flight is the only wait. Pods land somewhere between the 0 m and 75 m markers, never in a row that already has a team, and a blinking marker shows each landing spot before the pod falls. The pod hits hard: a blast, a shockwave, a dust cloud and a crater shake the screen, and nearby zombies take damage and get thrown back. The team digs in behind a temporary sandbag bunker and shoots at zombies in front of it, out to 50 m at level 1, 75 m at level 2 and 100 m at level 3. Teams are the only units zombies can kill: any zombie that reaches a team stops and attacks it, and the team shrinks as it takes damage. Each team carries limited supplies, and a team that runs out is airlifted out by helicopter. Up to 5 teams can be in the field at once (6 with the level 4 upgrade, which also gives every team medics that heal 2 health a second, with a green cross while they work, and 160 rounds of supplies instead of 70), and a lost or extracted team is replaced on the ship's next pass. The helipad at the base shows how many are out.
  - **Tesla weapons** charge up, then arc lightning through several zombies and stun them, so they stop walking and stop hitting the wall.
  - **Mortar weapons** shell the densest pack. The blast knocks zombies back and leaves a crater.
  - **Tanks** (Network+'s Tank bunker, its unique weapon) replace the mortar pit: 2 tanks at level 1, 4 at level 2 and 6 at level 3, with a range of 60 m at level 1 up to 100 m at level 3. A fourth upgrade level, for tanks only, raises shell damage from 12 to 18 and the magazine from 8 to 12 shells. Each tank takes a lane no other tank holds, and tanks that end up sharing a lane spread out so they never stack. When a zombie ahead gets within about 25 m, a tank drives forward to meet it, firing on the move. It runs over any normal-sized zombie in its path, but it never steers toward zombies to crush them. Brutes and bosses are too big to run over, so they stop the tank, and it never goes past 100 m from the wall. They roll out through a gate in the wall to the busiest lane and fire splash shells at zombies in range. When a tank's magazine runs dry, it drives back to the bunker to reload, then heads out again. Reloading tanks park on a service apron above the bunker, one fuel pump per tank: a hose runs to the tank with fuel pulsing along it, the pump light blinks, a shell is lowered into the turret, and a gauge fills until the tank is ready. Destroyed tanks are rebuilt inside the bunker, which shows how many are being rebuilt. Zombies that reach a tank stop and attack it. A destroyed tank is rebuilt in the bunker (20 s at level 1, 10 s at level 3) and rolls out again.
  - **Railguns** slide slowly along the wall to the busiest lane, charge, then fire a beam that hits every zombie in that lane once they're lined up.
  - **EDR pulse** (Security+) only stuns. It deals no damage, but its stun lasts much longer (1.6 s at level 1, up to 2.4 s).
  - **Minefields:** Security+'s Honeypot mine and CISSP's Cryptographic mine are mines instead of a mortar, like a potato mine. The field holds 10 mines at level 1, 15 at level 2 and 20 at level 3. They're buried in the zombies' lanes. Once armed, each blows up under the first zombie to reach it with splash damage, then a new one is buried in another lane and slowly arms (20 s at level 1, down to 12 s).
  - **Toner jets:** A+ Core 1's Toner bomb sends a slow little jet over the busiest pack every few seconds. It flies anywhere on the field, past the max range line, aims toner bombs right at the zombies in its lane, and carpet-bombs the pack with a line of small cyan, magenta, yellow and black bomblets that splash the zombies and stain the ground.
  - **Stun mortar:** A+ Core 2's Disk wipe charge doesn't knock zombies back. It freezes every zombie in the blast for a second or more.
  - **Max range:** turrets and the long-range weapons only fire at zombies inside the first 60% of the field, marked with a dashed MAX RANGE line, so you see the horde before it's hit. The toner jets are the exception: they fly slowly over the whole field.
  - **Turrets start weak too:** the wall's autocannons start at 0.6 damage a round and 0.6 shots a second each, and reach 4.6 damage and 2.5 shots a second at upgrade level 5 (about 11.5 damage a second each). The final Turret mount upgrade (level 3) adds two turrets, for 6 on the wall. The final Heavy caliber upgrade (level 5) adds explosive rounds: each round bursts on impact, dealing half its damage to zombies around the target, and the blast gets around shields. The final Autoloader upgrade (level 5) adds armor-piercing rounds: they go straight through shields and hit brutes 50% harder. Both stack.
  - **Weapons start weak:** every weapon starts much weaker and slower at level 1 (for example a railgun hits for 7 every 9 s), and only reaches full strength at level 3 (21 every 3.1 s).
  - The Armory describes each weapon's exact damage, range and recharge at your level.
  - **Recharge bars:** every weapon except the wall turrets has a small bar under it that fills as it reloads and glows when it's ready. For minefields, the bar shows how many mines are armed.
- **Each exam has its own night counter:** your Network+ nights and your Security+ nights (and so on) advance separately. The menu shows each exam's current night, and High Scores lists them all.
- **Ammo carries over:** whatever ammo is left at the end of a night, won or lost, goes to the stockpile and is loaded into the guns at the start of your next night.
- **Bigger hordes over time:** each night, zombies spawn faster (up to about 1.6 a second), increasingly arrive in pairs or threes, and specials become more common (up to 45% of the horde).
- **Super bosses:** every 10th night (10, 20, 30 and so on), a super boss arrives 12 seconds in, with its own health bar across the top of the field. Each exam has its own: the Broadcast Behemoth (Network+), Botnet Overlord (Security+), Meltdown Titan (A+ Core 1), Bluescreen Colossus (A+ Core 2) and Nation-State Leviathan (CISSP). It has 12 brutes' worth of health, walks slowly at a fixed pace that doesn't speed up with later nights, can't be stunned or knocked back, summons three zombies every 12 seconds, and hits the wall four times as hard as a brute. Killing it pays 60 scrap and 30 XP.
- **Special zombies:** from night 3, about 1 in 8 zombies (rising each night, up to 3 in 10) is a special with its own ability. Every exam has five shared types plus one of its own:
  - **Spitter:** stops about 40 m out, or as soon as a team in its lane is in reach, and spits acid at the wall or the team.
  - **Shield bearer:** a zombie in SWAT gear (helmet with visor, tactical vest) behind a riot shield. The shield soaks up turret rounds, team rifles and railgun hits until it breaks. When it breaks, they drop it and start running at 2.2x speed. Flame, tesla, mines, bombs, explosive splash and armor-piercing rounds go around it.
  - **Burrower:** tunnels underground, where nothing can hit it, and surfaces about 18 m from the wall.
  - **Screamer:** zombies near it move 30% faster while it's alive.
  - **Bloater:** slow and swollen. It bursts when killed, hurting nearby teams, and the wall if it's close.
  - **Packet storm** (Network+): splits into three fast, fragile packets when destroyed.
  - **Social engineer** (Security+): looks harmless. Weapons won't target it until it's within 30 m of the wall or gets caught in splash damage.
  - **Overclocker** (A+ Core 1): speeds up as it takes damage, up to 2.5 times as fast.
  - **Keylogger** (A+ Core 2): steals a scrap every second while it's at the wall.
  - **Zero-day** (CISSP): shrugs off the first hit from each weapon type.
  - The Armory's horde guide lists the current exam's specials with their health, speed and wall damage.
- **The horde gets stronger:** zombies gain health, move 4% faster and deal 6% more wall damage every night up to night 10, then only every 5 nights after that (nights 15, 20, 25 and so on). Their speed growth stops at +40%. They keep spawning more often every night. A callout marks the start of each new night, and the Armory's horde guide shows the current night's numbers. All zombie growth (strength, spawn rate, packs, specials) stops at night 150, so later nights play like night 150.
- **The base:** behind the wall is a command post, ammo depot, barracks and generator, plus props for each exam. The old barracks is now an airstrip: every time you earn ammo from a right answer or buy it during a night, a small cargo plane flies in, lands, drops boxes of ammo beside the runway and takes off again. The number of boxes matches the delivery: 2 for a right answer, 1 for an ammo crate, 5 for an ammo pallet and 10 for an airdrop. A yellow cargo bot hauls them from the airstrip to the ammo station, two at a time. A small crew of soldiers and wheeled bots keeps the base busy, hauling supply crates from the ammo depot to the wall turrets and to each weapon you've unlocked, then heading back for more. The crew and the cargo bot follow paths around the buildings instead of walking over them, and each crew member keeps to its own lane so they don't walk over each other. The field has craters, tank traps and barbed wire. Upgrades show up too: the wall gets armor plates as you buy plating, and the turret barrels change with caliber and autoloader upgrades.
- **Focus mode:** while a quick exam (or review round) runs, only the exam and the outpost are on screen. The header, tabs and footer come back when you leave through the result screen or the pause menu.
- **Pause:** the Pause button (or P) freezes the horde and puts the quick exam on hold: the exam dims and ignores clicks and keys, and a pause menu over the horde shows the question, hostiles, wall and ammo. From there you can resume (or press Esc), restart the quick exam from question 1 with a fresh night, open the armory, or quit to home. Answers already given stay recorded.
- **Wall damage:** a zombie at the wall damages it every second, and each step up in size doubles the damage: fast zombies 2.25, walkers 4.5, brutes 9.
- **Turrets:** the wall's main guns are 30 mm autocannons. Each fires once a second on its own timer, so they shoot one after another, and every shot is a visible round that flies across the field and hits when it arrives. Autoloader upgrades make them fire faster.
- **Nights:** keep the wall standing until the bomber clears the field to advance to the next night, where the horde gets bigger and tougher. If the outpost is overrun, the banner lets you pause or restart the quick exam with a fresh night. You can also keep answering: correct answers still earn scrap and XP, but you stay on the night you lost and your next quick exam retries it. On night 1, walkers take about 38–50 seconds to reach the wall and brutes about 75, and the horde gets 4% faster each night.

The home screen shows your accuracy in each domain next to that domain's exam weight. It also tracks XP, levels, a daily streak and your best scores.

## Abbreviations

Questions, explanations, the port table and OSI items spell out abbreviations the first time they appear, for example "UDP (User Datagram Protocol)". When a question tests what a term means (its correct answer is an abbreviation), the answer choices stay abbreviated until you answer, so the full name does not give the answer away. A setting on the quiz screen and in Settings turns spelled-out choices off entirely.

## Study guides

The study plans name the chapters and page numbers that cover each weak objective in these books, so you can read along in your own copy:

- **Network+:** Sybex *CompTIA Network+ Study Guide, Sixth Edition* (N10-009)
- **Security+:** Sybex *CompTIA Security+ Study Guide, Ninth Edition* and *CompTIA Security+ Practice Tests, Third Edition* (SY0-701)

The books themselves aren't in this repository.

## Run it

Open `index.html` in any browser, or serve the folder:

```bash
python3 -m http.server 8000
```

To publish it, enable GitHub Pages (Settings → Pages → deploy from the `main` branch, root folder).

## Notes

- Progress is stored in your browser's `localStorage`, so it stays on the device and browser you use.
- The questions are original practice items written against the official CompTIA exam objectives, not real exam questions.
