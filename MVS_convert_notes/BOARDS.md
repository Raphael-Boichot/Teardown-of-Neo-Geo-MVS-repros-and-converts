# Neo Geo MVS — PROG and CHA board references per game

Which **PROG** board and which **CHA** board each MVS game cartridge uses, cross-checked across three independent listings. Companion to [README.md](README.md) (mask ROM → EPROM reference).

> [!IMPORTANT]
> A board pair tells you which PCB family a game ships on, not which chips are on it. Sockets, ROM sizes and jumpers vary by board revision, and some games were produced on more than one board set (see the *Also documented* column). Check the board code printed on your own PCBs.

| | |
|---|---|
| **Rows** | 150 (149 numbered MVS game IDs + 1 late release) |
| **Distinct board pairs** | 36 (23 PROG types, 11 CHA types) |
| **Confidence** | 🟢 148 · 🟡 2 |
| **Games with an alternate board set documented** | 39 |
| **Scope** | MVS cartridges only. AES cartridges use `NEO-AEG` boards with different revisions. |
| **Compiled** | September 2026 |

## Contents

1. [How to read this](#1-how-to-read-this)
2. [Board usage at a glance](#2-board-usage-at-a-glance)
3. [Games that share the same board pair](#3-games-that-share-the-same-board-pair)
4. [Per-game table](#4-per-game-table)
5. [Board and protection-chip glossary](#5-board-and-protection-chip-glossary)
6. [Data quality and limits](#6-data-quality-and-limits)
7. [Sources and method](#7-sources-and-method)

---

## 1. How to read this

| Badge | Meaning |
|---|---|
| 🟢 **High** | The pair is listed by every source that covers the game (at least two), and at least two of them name it as the standard pair. |
| 🟡 **Medium** | Only one source covers the game, or the sources disagree on which pair is the standard one. |
| 🔴 **Low** | Sources conflict with no overlap. *No game falls in this class.* |

- **Src** shows which sources list the pair: **M** = MAME's driver comments, **K** = Mike McBike's cartridge table, **J** = the JNX board-code list. Details in [section 7](#7-sources-and-method).
- Board names use MAME's spelling (for example `PROGBK1`, `CHA256`). Mike and JNX write the same boards as `BK1` and `256`.
- **MVS no.** is the SNK product number from MAME. `??M-` means the MVS number is unconfirmed; the digits are the game ID.
- **Also documented** lists other PROG + CHA pairs that at least one source gives for the same game, with the sources in brackets.
- **Notes** carries protection chips and board date codes recorded in MAME's header for the standard pair (for example `CMC 7042`, `SMA`, `PCM2`).

---

## 2. Board usage at a glance

Games per PROG board, using the standard pair from the table in section 4:

| PROG board | Games |
|---|---|
| `PROGBK1` | 56 |
| `PROG42G-1` | 15 |
| `PROGGSC` | 14 |
| `PROGTOP` | 13 |
| `PROG-EP` | 7 |
| `PROG 4096` | 6 |
| `PROGBK2` | 6 |
| `PROG42G` | 4 |
| `PROG16` | 4 |
| `PROGLBA` | 4 |
| `PROG-G2` | 3 |
| `PROG-HERO` | 2 |
| `PROG-8MB` | 2 |
| `PROG8M42` | 2 |
| `PROG42G-COM` | 2 |
| `PROG 4096 B` | 2 |
| `PROGBK3S` | 2 |
| `PROG-NAM` | 1 |
| `PROGSF1` | 1 |
| `PROGEOP` | 1 |
| `PROGBK3R` | 1 |
| `PROGBK2R` | 1 |
| `PROGBK2S` | 1 |

Games per CHA board:

| CHA board | Games |
|---|---|
| `CHA256` | 46 |
| `CHA42G-1` | 23 |
| `CHAFIO` | 22 |
| `CHA256B` | 13 |
| `CHA512Y` | 12 |
| `CHA-32` | 10 |
| `CHA42G-3B` | 8 |
| `CHA 42G-2` | 5 |
| `CHA42G` | 4 |
| `CHA-8M` | 4 |
| `CHA 42G-3` | 3 |

PROGBK1 is the most-used PROG board and CHA256 the most-used CHA board. This matches the statistics quoted in a search snippet of the NeoGeo Dev Wiki's *Cartridge ROM arrangements* page (the page itself blocked automated access).

---

## 3. Games that share the same board pair

Useful for choosing a donor cartridge for a conversion or a repair. Games on the same pair are the candidates; check ROM sizes and protection first.

| PROG | CHA | Games | Titles |
|---|---|---|---|
| `PROGBK1` | `CHA256` | 25 | Fatal Fury 3; King of Fighters '95; Samurai Shodown 3: Blades of Blood; Pulstar; Kabuki Klash; Neo Bomberman; Real Bout Fatal Fury; Art of Fighting 3: Path of the Warrior; Aero Fighters 3; Metal Slug; Quiz Chibi Marukochan Deluxe; Goal! Goal! Goal!; Over Top; King of Fighters '96; Super Sidekicks 4: The Ultimate 11; Ninja Master's; Ragnagard; Pleasure Goal 5-on-5 Street Soccer; Ironclad Brikinger; Stakes Winner 2; Magical Drop 3; Shock Troopers; Flip Shot; Bust-A-Move Again; Captain Tomaday |
| `PROG42G-1` | `CHA42G-1` | 15 | Mutation Nation; King of the Monsters; Last Resort; Eight Man; Legend of Success Joe; Super Baseball 2020; Soccer Brawl; Robo Army; Fatal Fury; Football Frenzy; Crossed Swords; Baseball Stars 2; Quiz Meitantei Neo & Geo; Ninja Commando; Windjammers |
| `PROGGSC` | `CHA256` | 11 | Quest of Jong Master; Art of Fighting 2; Spinmaster; World Heroes 2 Jet; Karnov's Revenge; Aero Fighters 2; Zed Blade; Street Hoop; Quiz King of Fighters; World Heroes Perfect; Ghost Lop (prototype / location test) |
| `PROGBK1` | `CHA256B` | 10 | Tecmo World Soccer '96; Neo Turf Masters; Super Dodge Ball; Neo Driftout; Magical Drop 2; Samurai Shodown 4: Amakusa's Revenge; Real Bout Fatal Fury Special; Twinkle Star Sprites; Waku Waku 7; Breakers |
| `PROGBK1` | `CHA512Y` | 10 | King of Fighters '97; Last Blade; Irritating Maze, The; Blazing Star; Real Bout Fatal Fury 2; Metal Slug 2; Last Blade 2; Neo Geo Cup '98; Breakers Revenge; Shock Troopers 2nd Squad |
| `PROGTOP` | `CHA256` | 9 | King of Fighters '94; Super Sidekicks 2; Samurai Shodown 2; Power Spikes 2; Panic Bomber; Galaxy Fight: Universal Warriors; Double Dragon; Bust-A-Move; Kizuna Encounter |
| `PROG-EP` | `CHA-32` | 7 | Baseball Stars Professional; Top Player's Golf; Mahjong Kyo Retsuden; Magician Lord; Ninja Combat; Cyber-Lip; Puzzled |
| `PROGBK1` | `CHAFIO` | 7 | Zupapa!; Ganryu; Strikers 1945 Plus; Prehistoric Isle 2; Bang Bead; Nightmare in the Dark; Sengoku 3 |
| `PROGBK2` | `CHAFIO` | 6 | King of Fighters 2001; Metal Slug 4; Rage of the Dragons; King of Fighters 2002; Matrimelee; Pochi & Nyaa |
| `PROG 4096` | `CHA 42G-2` | 4 | Sengoku 2; 3 Count Bout; Puzzle de Pon!; Puzzle de Pon! R |
| `PROG42G` | `CHA42G` | 4 | Alpha Mission 2; Sengoku; Burning Fight; Quiz Daisousa Sen |
| `PROGBK1` | `CHA42G-3B` | 4 | Stakes Winner; Voltage Fighter Gowcaizer; Neo Mr. Do!; Money Puzzle Exchanger |
| `PROGLBA` | `CHAFIO` | 4 | King of Fighters '99; Garou: Mark of the Wolves; Metal Slug 3; King of Fighters 2000 |
| `PROG16` | `CHA42G-1` | 3 | King of the Monsters 2; Andro Dunos; World Heroes |
| `PROG 4096 B` | `CHA 42G-3` | 2 | World Heroes 2; Savage Reign |
| `PROG-8MB` | `CHA-8M` | 2 | Super Spy, The; Minnasan no Okagesamadesu |
| `PROG-G2` | `CHA42G-1` | 2 | Fatal Fury 2; Viewpoint |
| `PROG-HERO` | `CHA-32` | 2 | Riding Hero; League Bowling |
| `PROG42G-COM` | `CHA42G-1` | 2 | Bakatonosama Mahjong Manyuki; Thrash Rally |
| `PROG8M42` | `CHA-8M` | 2 | Ghost Pilots; Blue's Journey |
| `PROGBK3S` | `CHAFIO` | 2 | Metal Slug 5; King of Fighters 2003 |
| `PROGTOP` | `CHA256B` | 2 | Top Hunter; Aggressors of Dark Kombat |
| `PROGTOP` | `CHA42G-3B` | 2 | Super Sidekicks 3 : The Next Glory; Master of Syougi |
| `PROG 4096` | `CHA42G-1` | 1 | Art of Fighting |
| `PROG 4096` | `CHA42G-3B` | 1 | Pop 'N Bounce |
| `PROG-G2` | `CHA 42G-2` | 1 | Super Sidekicks |
| `PROG-NAM` | `CHA-32` | 1 | NAM 1975 |
| `PROG16` | `CHA256` | 1 | Gururin |
| `PROGBK2R` | `CHAFIO` | 1 | Samurai Shodown 5 |
| `PROGBK2S` | `CHAFIO` | 1 | Samurai Shodown 5 Special |
| `PROGBK3R` | `CHAFIO` | 1 | SVC Chaos: SNK vs. Capcom |
| `PROGEOP` | `CHA512Y` | 1 | Metal Slug X |
| `PROGGSC` | `CHA 42G-3` | 1 | Samurai Shodown |
| `PROGGSC` | `CHA256B` | 1 | Fight Fever |
| `PROGGSC` | `CHA42G-3B` | 1 | Fatal Fury Special |
| `PROGSF1` | `CHA512Y` | 1 | King of Fighters '98 |

---

## 4. Per-game table

Sorted by game ID (the number in MAME's headers and in Mike's *NGH* column).

| ID | MVS no. | Game (MAME set) | Year | PROG | CHA | Also documented | Notes | Conf. | Src |
|---|---|---|---|---|---|---|---|---|---|
| 0001 | NGM-001 | NAM 1975 (`nam1975`) | 1990 | `PROG-NAM` | `CHA-32` | — | — | 🟢 | M K J |
| 0002 | NGM-002 | Baseball Stars Professional (`bstars`) | 1990 | `PROG-EP` | `CHA-32` | — | — | 🟢 | M K J |
| 0003 | NGM-003 | Top Player's Golf (`tpgolf`) | 1990 | `PROG-EP` | `CHA-32` | — | — | 🟢 | M K J |
| 0004 | NGM-004 | Mahjong Kyo Retsuden (`mahretsu`) | 1990 | `PROG-EP` | `CHA-32` | — | — | 🟢 | M K J |
| 0005 | NGM-005 | Magician Lord (`maglord`) | 1990 | `PROG-EP` | `CHA-32` | — | — | 🟢 | M K J |
| 0006 | NGM-006 | Riding Hero (`ridhero`) | 1990 | `PROG-HERO` | `CHA-32` | — | — | 🟢 | M K J |
| 0007 | NGM-007 | Alpha Mission 2 (`alpham2`) | 1991 | `PROG42G` | `CHA42G` | — | — | 🟢 | M K J |
| 0009 | NGM-009 | Ninja Combat (`ncombat`) | 1990 | `PROG-EP` | `CHA-32` | — | — | 🟢 | M K J |
| 0010 | NGM-010 | Cyber-Lip (`cyberlip`) | 1990 | `PROG-EP` | `CHA-32` | — | — | 🟢 | M K J |
| 0011 | NGM-011 | Super Spy, The (`superspy`) | 1990 | `PROG-8MB` | `CHA-8M` | — | — | 🟢 | M K J |
| 0014 | NGM-014 | Mutation Nation (`mutnat`) | 1992 | `PROG42G-1` | `CHA42G-1` | — | — | 🟢 | M K J |
| 0016 | NGM-016 | King of the Monsters (`kotm`) | 1991 | `PROG42G-1` | `CHA42G-1` | PROG42G + CHA42G (M) | — | 🟢 | M K J |
| 0017 | NGM-017 | Sengoku (`sengoku`) | 1991 | `PROG42G` | `CHA42G` | — | — | 🟢 | M K J |
| 0018 | NGM-018 | Burning Fight (`burningf`) | 1991 | `PROG42G` | `CHA42G` | PROG42G-1 + CHA42G-1 (M; MAME lists this as the standard pair) | Sources disagree: Mike/JNX give PROG42G + CHA42G; MAME gives 42G-1 as standard and mentions 42G only for boards seen 'manually patched up with wires and resistors' | 🟡 | M K J |
| 0019 | NGM-019 | League Bowling (`lbowling`) | 1990 | `PROG-HERO` | `CHA-32` | — | — | 🟢 | M K J |
| 0020 | NGM-020 | Ghost Pilots (`gpilots`) | 1991 | `PROG8M42` | `CHA-8M` | — | — | 🟢 | M K J |
| 0021 | NGM-021 | Puzzled (`joyjoy`) | 1990 | `PROG-EP` | `CHA-32` | — | — | 🟢 | M K J |
| 0022 | ALM-001 | Blue's Journey (`bjourney`) | 1990 | `PROG8M42` | `CHA-8M` | — | — | 🟢 | M K J |
| 0023 | NGM-023 | Quiz Daisousa Sen (`quizdais`) | 1991 | `PROG42G` | `CHA42G` | PROGTOP + CHA256 (M; Korean release) | — | 🟢 | M K J |
| 0024 | NGM-024 | Last Resort (`lresort`) | 1992 | `PROG42G-1` | `CHA42G-1` | PROG-EP + CHA-EPG (M; prototype); PROG42G-1 + CHA 42G-2 (K) | — | 🟢 | M K J |
| 0025 | NGM-025 | Eight Man (`eightman`) | 1991 | `PROG42G-1` | `CHA42G-1` | — | — | 🟢 | M K J |
| 0027 | MOM-001 | Minnasan no Okagesamadesu (`minasan`) | 1990 | `PROG-8MB` | `CHA-8M` | — | — | 🟢 | M K J |
| 0029 | ??M-029 | Legend of Success Joe (`legendos`) | 1991 | `PROG42G-1` | `CHA42G-1` | — | — | 🟢 | M K J |
| 0030 | NGM-030 | Super Baseball 2020 (`2020bb`) | 1991 | `PROG42G-1` | `CHA42G-1` | — | — | 🟢 | M K J |
| 0031 | NGM-031 | Soccer Brawl (`socbrawl`) | 1991 | `PROG42G-1` | `CHA42G-1` | — | — | 🟢 | M K J |
| 0032 | NGM-032 | Robo Army (`roboarmy`) | 1991 | `PROG42G-1` | `CHA42G-1` | PROG42G-COM + CHA42G-1 (M) | — | 🟢 | M K J |
| 0033 | NGM-033 | Fatal Fury (`fatfury1`) | 1991 | `PROG42G-1` | `CHA42G-1` | — | — | 🟢 | M K J |
| 0034 | NGM-034 | Football Frenzy (`fbfrenzy`) | 1992 | `PROG42G-1` | `CHA42G-1` | — | — | 🟢 | M K J |
| 0036 | MOM-002 | Bakatonosama Mahjong Manyuki (`bakatono`) | 1991 | `PROG42G-COM` | `CHA42G-1` | PROG42G-1 + CHA42G-1 (M) | — | 🟢 | M K J |
| 0037 | ALM-002 | Crossed Swords (`crsword`) | 1991 | `PROG42G-1` | `CHA42G-1` | — | — | 🟢 | M K J |
| 0038 | ALM-003 | Thrash Rally (`trally`) | 1991 | `PROG42G-COM` | `CHA42G-1` | — | — | 🟢 | M K J |
| 0039 | NGM-039 | King of the Monsters 2 (`kotm2`) | 1992 | `PROG16` | `CHA42G-1` | — | — | 🟢 | M K J |
| 0040 | NGM-040 | Sengoku 2 (`sengoku2`) | 1993 | `PROG 4096` | `CHA 42G-2` | — | — | 🟢 | M K J |
| 0041 | NGM-041 | Baseball Stars 2 (`bstars2`) | 1992 | `PROG42G-1` | `CHA42G-1` | — | — | 🟢 | M K J |
| 0042 | NGM-042 | Quiz Meitantei Neo & Geo (`quizdai2`) | 1992 | `PROG42G-1` | `CHA42G-1` | — | — | 🟢 | M K J |
| 0043 | NGM-043 | 3 Count Bout (`3countb`) | 1993 | `PROG 4096` | `CHA 42G-2` | PROG-G2 + CHA 42G-2 (M) | — | 🟢 | M K J |
| 0044 | NGM-044 | Art of Fighting (`aof`) | 1992 | `PROG 4096` | `CHA42G-1` | PROG16 + CHA42G-1 (M) | — | 🟢 | M K J |
| 0045 | NGM-045 | Samurai Shodown (`samsho`) | 1993 | `PROGGSC` | `CHA 42G-3` | — | — | 🟢 | M K J |
| 0046 | NGM-046 | Top Hunter (`tophuntr`) | 1994 | `PROGTOP` | `CHA256B` | — | — | 🟢 | M K J |
| 0047 | NGM-047 | Fatal Fury 2 (`fatfury2`) | 1992 | `PROG-G2` | `CHA42G-1` | PROG-G2 + CHA 42G-2 (M) | SNK-9201 | 🟢 | M K J |
| 0048 | ??M-048 | Quest of Jong Master (`janshin`) | 1994 | `PROGGSC` | `CHA256` | — | — | 🟢 | M K J |
| 0049 | NGM-049 | Andro Dunos (`androdun`) | 1992 | `PROG16` | `CHA42G-1` | — | — | 🟢 | M K J |
| 0050 | ALM-004 | Ninja Commando (`ncommand`) | 1992 | `PROG42G-1` | `CHA42G-1` | — | — | 🟢 | M K J |
| 0051 | AIM-051 | Viewpoint (`viewpoin`) | 1992 | `PROG-G2` | `CHA42G-1` | PROG 4096 + CHA 42G-2 (M) | — | 🟢 | M K J |
| 0052 | NGM-052 | Super Sidekicks (`ssideki`) | 1992 | `PROG-G2` | `CHA 42G-2` | — | SNK-9201 | 🟢 | M K J |
| 0053 | ALM-005 | World Heroes (`wh1`) | 1992 | `PROG16` | `CHA42G-1` | — | — | 🟢 | M K J |
| 0055 | NGM-055 | King of Fighters '94 (`kof94`) | 1994 | `PROGTOP` | `CHA256` | PROGTOP + CHA256B (M) | — | 🟢 | M K J |
| 0056 | NGM-056 | Art of Fighting 2 (`aof2`) | 1994 | `PROGGSC` | `CHA256` | — | — | 🟢 | M K J |
| 0057 | ALM-006 | World Heroes 2 (`wh2`) | 1993 | `PROG 4096 B` | `CHA 42G-3` | — | — | 🟢 | M K J |
| 0058 | NGM-058 | Fatal Fury Special (`fatfursp`) | 1993 | `PROGGSC` | `CHA42G-3B` | PROGGSC + CHA 42G-3 (M) | — | 🟢 | M K J |
| 0059 | NGM-059 | Savage Reign (`savagere`) | 1995 | `PROG 4096 B` | `CHA 42G-3` | PROGTOP + CHA256 (M) | — | 🟢 | M K J |
| 0060 | ??M-060 | Fight Fever (`fightfev`) | 1994 | `PROGGSC` | `CHA256B` | — | — | 🟢 | M K J |
| 0061 | NGM-061 | Super Sidekicks 2 (`ssideki2`) | 1994 | `PROGTOP` | `CHA256` | PROGGSC + CHA256 (M); PROGGSC + CHA256B (M); PROG 4096 B + CHA256 (M) | — | 🟢 | M K J |
| 0062 | DEM-001 | Spinmaster (`spinmast`) | 1993 | `PROGGSC` | `CHA256` | — | — | 🟢 | M K J |
| 0063 | NGM-063 | Samurai Shodown 2 (`samsho2`) | 1994 | `PROGTOP` | `CHA256` | — | — | 🟢 | M K J |
| 0064 | ADM-007 | World Heroes 2 Jet (`wh2j`) | 1994 | `PROGGSC` | `CHA256` | — | — | 🟢 | M K J |
| 0065 | DEM-002 | Windjammers (`wjammers`) | 1994 | `PROG42G-1` | `CHA42G-1` | — | — | 🟢 | M K J |
| 0066 | DEM-003 | Karnov's Revenge (`karnovr`) | 1994 | `PROGGSC` | `CHA256` | — | — | 🟢 | M K J |
| 0067 | ??M-067 | Gururin (`gururin`) | 1994 | `PROG16` | `CHA256` | PROG16 + CHA256B (M) | — | 🟢 | M K J |
| 0068 | NGM-068 | Power Spikes 2 (`pspikes2`) | 1994 | `PROGTOP` | `CHA256` | — | — | 🟢 | M K J |
| 0069 | NGM-069 | Fatal Fury 3 (`fatfury3`) | 1995 | `PROGBK1` | `CHA256` | — | — | 🟢 | M K J |
| 0070 | ??M-070 | Zupapa! (`zupapa`) | 2001 | `PROGBK1` | `CHAFIO` | — | date 1999.6.14; CMC 7042 | 🟢 | M K J |
| 0073 | ??M-073 | Panic Bomber (`panicbom`) | 1994 | `PROGTOP` | `CHA256` | — | — | 🟢 | M K J |
| 0074 | ADM-008 | Aggressors of Dark Kombat (`aodk`) | 1994 | `PROGTOP` | `CHA256B` | — | — | 🟢 | M K J |
| 0075 | NGM-075 | Aero Fighters 2 (`sonicwi2`) | 1994 | `PROGGSC` | `CHA256` | — | — | 🟢 | M K J |
| 0076 | ??M-076 | Zed Blade (`zedblade`) | 1994 | `PROGGSC` | `CHA256` | — | — | 🟢 | M K J |
| 0078 | NGM-078 | Galaxy Fight: Universal Warriors (`galaxyfg`) | 1995 | `PROGTOP` | `CHA256` | — | — | 🟢 | M K J |
| 0079 | DEM-004 | Street Hoop (`strhoop`) | 1994 | `PROGGSC` | `CHA256` | — | — | 🟢 | M K J |
| 0080 | SAM-080 | Quiz King of Fighters (`quizkof`) | 1995 | `PROGGSC` | `CHA256` | PROGTOP + CHA256 (M; Korean release) | — | 🟢 | M K J |
| 0081 | NGM-081 | Super Sidekicks 3 : The Next Glory (`ssideki3`) | 1995 | `PROGTOP` | `CHA42G-3B` | PROGTOP + CHA256 (M); PROG 4096 B + CHA 42G-3 (M); PROGBK1 + CHA256B (M) | — | 🟢 | M K J |
| 0082 | NGM-082 | Double Dragon (`doubledr`) | 1995 | `PROGTOP` | `CHA256` | PROGTOP + CHA 42G-3 (M); PROGBK1 + CHA256 (M); PROGTOP + CHA256B (M); PROG 4096 B + CHA 42G-3 (M); PROGGSC + CHA42G-3B (M) | — | 🟢 | M K J |
| 0083 | NGM-083 | Bust-A-Move (`pbobblen`) | 1994 | `PROGTOP` | `CHA256` | — | — | 🟢 | M K J |
| 0084 | NGM-084 | King of Fighters '95 (`kof95`) | 1995 | `PROGBK1` | `CHA256` | PROGSM + CHA256 (M) | — | 🟢 | M K J |
| 0086 | ??M-086 | Tecmo World Soccer '96 (`twsoc96`) | 1996 | `PROGBK1` | `CHA256B` | — | — | 🟢 | M K J |
| 0087 | NGM-087 | Samurai Shodown 3: Blades of Blood (`samsho3`) | 1995 | `PROGBK1` | `CHA256` | PROGSS3 + CHA256 (M) | — | 🟢 | M K J |
| 0088 | NGM-088 | Stakes Winner (`stakwin`) | 1995 | `PROGBK1` | `CHA42G-3B` | — | MAME header spells the CHA board 'CHA42-3B' (treated as 42G-3B) | 🟢 | M K J |
| 0089 | NGM-089 | Pulstar (`pulstar`) | 1995 | `PROGBK1` | `CHA256` | PROGBK1 + CHA256B (M) | — | 🟢 | M K J |
| 0090 | ADM-009 | World Heroes Perfect (`whp`) | 1995 | `PROGGSC` | `CHA256` | PROGTOP + CHA256 (M); PROGGSC + CHA256B (M); PROGBK1 + CHA256B (M) | — | 🟢 | M K J |
| 0092 | NGM-092 | Kabuki Klash (`kabukikl`) | 1995 | `PROGBK1` | `CHA256` | PROGTOP + CHA256 (M) | — | 🟢 | M K J |
| 0093 | ??M-093 | Neo Bomberman (`neobombe`) | 1997 | `PROGBK1` | `CHA256` | — | — | 🟢 | M K J |
| 0094 | NGM-094 | Voltage Fighter Gowcaizer (`gowcaizr`) | 1995 | `PROGBK1` | `CHA42G-3B` | — | — | 🟢 | M K J |
| 0095 | NGM-095 | Real Bout Fatal Fury (`rbff1`) | 1995 | `PROGBK1` | `CHA256` | — | — | 🟢 | M K J |
| 0096 | NGM-096 | Art of Fighting 3: Path of the Warrior (`aof3`) | 1996 | `PROGBK1` | `CHA256` | — | — | 🟢 | M K J |
| 0097 | NGM-097 | Aero Fighters 3 (`sonicwi3`) | 1995 | `PROGBK1` | `CHA256` | — | — | 🟢 | M K J |
| 0200 | NGM-200 | Neo Turf Masters (`turfmast`) | 1996 | `PROGBK1` | `CHA256B` | PROGBK1 + CHA256 (M) | — | 🟢 | M K J |
| 0201 | NGM-201 | Metal Slug (`mslug`) | 1996 | `PROGBK1` | `CHA256` | PROGBK1 + CHA256B (M) | — | 🟢 | M K J |
| 0202 | ??M-202 | Puzzle de Pon! (`puzzledp`) | 1995 | `PROG 4096` | `CHA 42G-2` | — | — | 🟢 | M K J |
| 0203 | ADM-010 | Master of Syougi (`moshougi`) | 1995 | `PROGTOP` | `CHA42G-3B` | — | — | 🟢 | M K J |
| 0206 | ??M-206 | Quiz Chibi Marukochan Deluxe (`marukodq`) | 1995 | `PROGBK1` | `CHA256` | — | — | 🟢 | M K J |
| 0207 | ??M-207 | Neo Mr. Do! (`neomrdo`) | 1996 | `PROGBK1` | `CHA42G-3B` | PROG 4096 + CHA42G-3B (M) | — | 🟢 | M K J |
| 0208 | ??M-208 | Super Dodge Ball (`sdodgeb`) | 1996 | `PROGBK1` | `CHA256B` | — | — | 🟢 | M K J |
| 0209 | ??M-209 | Goal! Goal! Goal! (`goalx3`) | 1995 | `PROGBK1` | `CHA256` | — | — | 🟢 | M K J |
| 0212 | ADM-011 | Over Top (`overtop`) | 1996 | `PROGBK1` | `CHA256` | — | — | 🟢 | M K J |
| 0213 | ??M-213 | Neo Driftout (`neodrift`) | 1996 | `PROGBK1` | `CHA256B` | — | — | 🟢 | M K J |
| 0214 | NGM-214 | King of Fighters '96 (`kof96`) | 1996 | `PROGBK1` | `CHA256` | PROGSS3 + CHA256 (M) | — | 🟢 | M K J |
| 0215 | NGM-215 | Super Sidekicks 4: The Ultimate 11 (`ssideki4`) | 1996 | `PROGBK1` | `CHA256` | — | — | 🟢 | M K J |
| 0216 | ??M-216 | Kizuna Encounter (`kizuna`) | 1996 | `PROGTOP` | `CHA256` | — | — | 🟢 | M K J |
| 0217 | ADM-012 | Ninja Master's (`ninjamas`) | 1996 | `PROGBK1` | `CHA256` | — | — | 🟢 | M K J |
| 0218 | NGM-218 | Ragnagard (`ragnagrd`) | 1996 | `PROGBK1` | `CHA256` | — | — | 🟢 | M K J |
| 0219 | NGM-219 | Pleasure Goal 5-on-5 Street Soccer (`pgoal`) | 1996 | `PROGBK1` | `CHA256` | — | — | 🟢 | M K J |
| 0220 | — | Ironclad Brikinger (`ironclad`) | 2014? | `PROGBK1` | `CHA256` | PROGTOP + CHA256B (K) | Single source (Mike); late/unlicensed release, MAME lists ID-0220 as a 1996 prototype | 🟡 | K |
| 0221 | NGM-221 | Magical Drop 2 (`magdrop2`) | 1996 | `PROGBK1` | `CHA256B` | PROGBK1 + CHA256 (M) | — | 🟢 | M K J |
| 0222 | NGM-222 | Samurai Shodown 4: Amakusa's Revenge (`samsho4`) | 1996 | `PROGBK1` | `CHA256B` | PROGBK1 + CHA256 (M) | — | 🟢 | M K J |
| 0223 | NGM-223 | Real Bout Fatal Fury Special (`rbffspec`) | 1996 | `PROGBK1` | `CHA256B` | — | — | 🟢 | M K J |
| 0224 | ADM-013 | Twinkle Star Sprites (`twinspri`) | 1996 | `PROGBK1` | `CHA256B` | — | — | 🟢 | M K J |
| 0225 | SUM-225 | Waku Waku 7 (`wakuwak7`) | 1996 | `PROGBK1` | `CHA256B` | — | — | 🟢 | M K J |
| 0227 | NGM-227 | Stakes Winner 2 (`stakwin2`) | 1996 | `PROGBK1` | `CHA256` | — | — | 🟢 | M K J |
| 0228 | — | Ghost Lop (prototype / location test) (`ghostlop`) | 1996 | `PROGGSC` | `CHA256` | — | Prototype / location-test cart; not in Mike's table | 🟢 | M J |
| 0230 | NGM-2300 | Breakers (`breakers`) | 1996 | `PROGBK1` | `CHA256B` | — | — | 🟢 | M K J |
| 0231 | ??M-2310 | Money Puzzle Exchanger (`miexchng`) | 1997 | `PROGBK1` | `CHA42G-3B` | — | — | 🟢 | M K J |
| 0232 | NGM-2320 | King of Fighters '97 (`kof97`) | 1997 | `PROGBK1` | `CHA512Y` | — | — | 🟢 | M K J |
| 0233 | NGM-2330 | Magical Drop 3 (`magdrop3`) | 1997 | `PROGBK1` | `CHA256` | PROGBK1 + CHA256B (M) | — | 🟢 | M K J |
| 0234 | NGM-2340 | Last Blade (`lastblad`) | 1997 | `PROGBK1` | `CHA512Y` | — | — | 🟢 | M K J |
| 0235 | ??M-2350 | Puzzle de Pon! R (`puzzldpr`) | 1997 | `PROG 4096` | `CHA 42G-2` | — | — | 🟢 | M K J |
| 0236 | ??M-2360 | Irritating Maze, The (`irrmaze`) | 1997 | `PROGBK1` | `CHA512Y` | — | — | 🟢 | M K J |
| 0237 | ??M-2370 | Pop 'N Bounce (`popbounc`) | 1997 | `PROG 4096` | `CHA42G-3B` | — | — | 🟢 | M K J |
| 0238 | ??M-2380 | Shock Troopers (`shocktro`) | 1997 | `PROGBK1` | `CHA256` | — | — | 🟢 | M K J |
| 0239 | NGM-2390 | Blazing Star (`blazstar`) | 1998 | `PROGBK1` | `CHA512Y` | — | — | 🟢 | M K J |
| 0240 | NGM-2400 | Real Bout Fatal Fury 2 (`rbff2`) | 1998 | `PROGBK1` | `CHA512Y` | — | — | 🟢 | M K J |
| 0241 | NGM-2410 | Metal Slug 2 (`mslug2`) | 1998 | `PROGBK1` | `CHA512Y` | PROGBK1 + CHA256 (M) | — | 🟢 | M K J |
| 0242 | NGM-2420 | King of Fighters '98 (`kof98`) | 1998 | `PROGSF1` | `CHA512Y` | PROGSF1E + CHA512Y (M); PROGBK1 + CHA512Y (M) | date 1998.6.17; protected board; PROGSF1/SF1E carry an Altera protection chip; a PROGBK1 variant is also listed | 🟢 | M K J |
| 0243 | NGM-2430 | Last Blade 2 (`lastbld2`) | 1998 | `PROGBK1` | `CHA512Y` | — | — | 🟢 | M K J |
| 0244 | ??M-2440 | Neo Geo Cup '98 (`neocup98`) | 1998 | `PROGBK1` | `CHA512Y` | — | — | 🟢 | M K J |
| 0245 | ??M-2450 | Breakers Revenge (`breakrev`) | 1998 | `PROGBK1` | `CHA512Y` | — | — | 🟢 | M K J |
| 0246 | NGM-2460 | Shock Troopers 2nd Squad (`shocktr2`) | 1998 | `PROGBK1` | `CHA512Y` | — | — | 🟢 | M K J |
| 0247 | ??M-2470 | Flip Shot (`flipshot`) | 1998 | `PROGBK1` | `CHA256` | — | — | 🟢 | M K J |
| 0248 | ??M-2480 | Bust-A-Move Again (`pbobbl2n`) | 1999 | `PROGBK1` | `CHA256` | — | — | 🟢 | M K J |
| 0249 | ??M-2490 | Captain Tomaday (`ctomaday`) | 1999 | `PROGBK1` | `CHA256` | PROGBK1 + CHA512Y (M) | — | 🟢 | M K J |
| 0250 | NGM-2500 | Metal Slug X (`mslugx`) | 1999 | `PROGEOP` | `CHA512Y` | — | date 1999.2.2 | 🟢 | M K J |
| 0251 | NGM-2510 | King of Fighters '99 (`kof99`) | 1999 | `PROGLBA` | `CHAFIO` | PROGBK1 + CHAFIO (M; non-SMA version) | SMA; date 1999.4.12; date 1999.6.14; CMC 7042; Primary = SMA-protected version | 🟢 | M K J |
| 0252 | ??M-2520 | Ganryu (`ganryu`) | 1999 | `PROGBK1` | `CHAFIO` | — | date 1999.6.14; CMC 7042 | 🟢 | M K J |
| 0253 | NGM-2530 | Garou: Mark of the Wolves (`garou`) | 1999 | `PROGLBA` | `CHAFIO` | — | date 1999.4.12; SMA; LBA-SUB; date 1999.6.14; CMC 7042 | 🟢 | M K J |
| 0254 | ??M-2540 | Strikers 1945 Plus (`s1945p`) | 1999 | `PROGBK1` | `CHAFIO` | — | date 1999.6.14; CMC 7042 | 🟢 | M K J |
| 0255 | ??M-2550 | Prehistoric Isle 2 (`preisle2`) | 1999 | `PROGBK1` | `CHAFIO` | — | date 1999.6.14; CMC 7042 | 🟢 | M K J |
| 0256 | NGM-2560 | Metal Slug 3 (`mslug3`) | 2000 | `PROGLBA` | `CHAFIO` | PROGBK1 + CHAFIO (M; non-SMA version) | date 1999.4.12; SMA; LBA-SUB; date 1999.6.14; CMC 7042; Primary = SMA-protected version | 🟢 | M K J |
| 0257 | NGM-2570 | King of Fighters 2000 (`kof2000`) | 2000 | `PROGLBA` | `CHAFIO` | PROGBK1 + CHAFIO (M; non-SMA version) | date 1999.4.12; SMA; LBA-SUB; date 1999.6.14; CMC 7050; Primary = SMA-protected version | 🟢 | M K J |
| 0259 | ??M-2590 | Bang Bead (`bangbead`) | 2000 | `PROGBK1` | `CHAFIO` | PROGTOP + CHA265B? (K) | date 1999.6.14; CMC 7042; Mike's alternate CHA reads '265B' (probably a typo for 256B) | 🟢 | M K J |
| 0260 | ??M-2600 | Nightmare in the Dark (`nitd`) | 2000 | `PROGBK1` | `CHAFIO` | PROGTOP + CHA512Y (K) | date 1999.6.14; CMC 7042 | 🟢 | M K J |
| 0261 | NGM-2610 | Sengoku 3 (`sengoku3`) | 2001 | `PROGBK1` | `CHAFIO` | — | date 1999.6.14; CMC 7042 | 🟢 | M K J |
| 0262 | NGM-262? | King of Fighters 2001 (`kof2001`) | 2001 | `PROGBK2` | `CHAFIO` | — | PCM2 SNK; REV1.0; CMC 7050 | 🟢 | M K J |
| 0263 | NGM-2630 | Metal Slug 4 (`mslug4`) | 2002 | `PROGBK2` | `CHAFIO` | — | PCM2 SNK; CMC 7050 | 🟢 | M K J |
| 0264 | NGM-264? | Rage of the Dragons (`rotd`) | 2002 | `PROGBK2` | `CHAFIO` | — | date 2000.3.21; PCM2 SNK; date 1999.6.14; CMC 7050 | 🟢 | M K J |
| 0265 | NGM-2650 | King of Fighters 2002 (`kof2002`) | 2002 | `PROGBK2` | `CHAFIO` | — | date 2000.3.21; PCM2 SNK; date 1999.6.14; CMC 7050 | 🟢 | M K J |
| 0266 | NGM-2660 | Matrimelee (`matrim`) | 2003 | `PROGBK2` | `CHAFIO` | — | date 2000.3.21; PCM2 SNK; date 1999.6.14; CMC 7050 | 🟢 | M K J |
| 0267 | ??M-2670 | Pochi & Nyaa (`pnyaa`) | 2003 | `PROGBK2` | `CHAFIO` | — | date 2000.3.21; PCM2 SNK; date 1999.6.14; CMC 7050 | 🟢 | M K J |
| 0268 | NGM-2680 | Metal Slug 5 (`mslug5`) | 2003 | `PROGBK3S` | `CHAFIO` | — | date 2003.10.1; PCM2 PLAYMORE; PVC; date 2003.7.24; CMC 7050 | 🟢 | M K J |
| 0269 | NGM-2690 | SVC Chaos: SNK vs. Capcom (`svc`) | 2003 | `PROGBK3R` | `CHAFIO` | — | date 2003.9.2; PCM2 SNKPLAYMORE; PVC; date 2003.7.24; CMC 7050 | 🟢 | M K J |
| 0270 | NGM-2700 | Samurai Shodown 5 (`samsho5`) | 2003 | `PROGBK2R` | `CHAFIO` | — | date 2003.8.26; PCM2 SNKPLAYMORE; date 2003.7.24; CMC 7050 | 🟢 | M K J |
| 0271 | NGM-2710 | King of Fighters 2003 (`kof2003`) | 2003 | `PROGBK3S` | `CHAFIO` | — | date 2003.10.1; PCM2 SNKPLAYMORE; PVC; date 2003.7.24; CMC 7050 | 🟢 | M K J |
| 0272 | NGM-2720 | Samurai Shodown 5 Special (`samsh5sp`) | 2004 | `PROGBK2S` | `CHAFIO` | — | date 2003.10.18; PCM2 SNKPLAYMORE; date 2003.7.24; CMC 7050 | 🟢 | M K J |

---

## 5. Board and protection-chip glossary

From the comments at the top of MAME's Neo Geo driver ([S1](README.md#12-sources) in the README).

**PROG boards** (program `P` ROMs and sample `V` ROMs)

`PROG-NAM` · `PROG-HERO` · `PROG-EP` · `PROG-8MB` · `PROGEP8M` · `PROG8M42` · `PROG16` · `PROG42G` · `PROG42G-COM` · `PROG42G-1` · `PROG-G2` · `PROG 4096` · `PROG 4096 B` · `PROGGSC` · `PROGSM` · `PROGSS3` · `PROGTOP` · `PROGSF1` (1998.6.17) · `PROGSF1E` (1998.6.18) · `PROGEOP` (1999.2.2) · `PROGLBA` (1999.4.12; `LBA-SUB` 2000.2.24) · `PROGBK1` (1994 and 2001 revisions) · `PROGBK2` (2000.3.21, with NEO-PCM2 SNK 1999 or PLAYMORE 2002; also a KOF 2001 REV1.0 and a 2002 Korea-made revision) · SNK Playmore: `PROGBK2R` (2003.8.26) · `PROGBK3R` (2003.9.2) · `PROGBK3S` (2003.10.1) · `PROGBK2S` (2003.10.18) · development board `PROGMC2`.

**CHA boards** (graphics `C` ROMs, fix-layer `S1` ROM and sound-driver `M1` ROM)

`CHA-32` · `CHA-8M` · `CHA42G` · `CHA42G-1` · `CHA 42G-2` · `CHA 42G-3` · `CHA42G-3B` · `CHA256` · `CHA256B` · `CHA512Y` · `CHAFIO` (1999.6.14, used with NEO-CMC 7042 or 7050; also a KOF 2001 REV1.0 and a 2002 Korea-made revision) · SNK Playmore `CHAFIO` (2003.7.24, NEO-CMC 7050 only) · development board `CHAMC2`.

**Custom and protection chips named in the headers**

| Chip | Board | Function (per MAME) |
|---|---|---|
| `NEO-273` | CHA | C and S ROM address latch |
| `NEO-CMC 7042 / 7050` | CHA | NEO-273 and NEO-ZMC logic, C ROM decryption (7050 also decrypts M1), C/S multiplexing, S ROM bankswitching |
| `NEO-ZMC / NEO-ZMC2` | CHA | Z80 memory controller (ZMC2 adds a tile serializer) |
| `PRO-CT0 / SNK-9201` | PROG-G2 | P ROM protection (Fatal Fury 2 and other G2 games); also on early AES CHA boards |
| `NEO-SMA` | PROGLBA | P ROM decryption and bankswitching, RNG, 256 KB of game data stored in the chip |
| `NEO-PCM2` | PROGBK2 / BK3 | PCM functionality, V ROM decryption, P ROM decoding and bankswitching |
| `NEO-PVC` | PROGBK3 | P ROM decryption and bankswitching, with RAM |
| `ALTERA EPM7128` | PROGSF1 / PROGEOP | P ROM protection (KOF '98, Metal Slug X) |
| `NEO-COMA` | PROG-HERO / 42G-COM | Microcontroller for Multi Play mode (Riding Hero, League Bowling, Thrash Rally) |
| `PCM` | PROG | ADPCM bus latches and V ROM multiplexer |

---

## 6. Data quality and limits

- **Agreement.** For 141 of the 150 rows every covering source names the same first-listed pair. In the other 9, MAME lists several boards and its first line differs from Mike and JNX (for example King of the Monsters, Art of Fighting, Savage Reign, Super Sidekicks 2, World Heroes Perfect), or only one source covers the game. The standard pair used here is the one at least two sources name first; the other sets appear under *Also documented*.
- **Burning Fight** is the one real disagreement. Mike and JNX give `PROG42G` + `CHA42G`; MAME gives `PROG42G-1` + `CHA42G-1` as standard and mentions the 42G pair only for boards "seen several times" that were hand-patched with wires and resistors.
- **Typos.** MAME's header for Stakes Winner reads `CHA42-3B` (treated as `CHA42G-3B`). Mike's alternate CHA for Bang Bead reads `265B`, probably `256B`; it is shown as written.
- **Ironclad Brikinger** appears only in Mike's table (year given as "2014?"). MAME files it as a 1996 prototype with no board line.
- **Ghost Lop** is a prototype/location-test cart. MAME and JNX agree on `PROGGSC` + `CHA256`; Mike's table does not list it.
- **Games with a Korean release** (Quiz Daisousa Sen, Quiz King of Fighters) list a second pair that MAME attributes to the Korean boards.
- **KOF '99, Metal Slug 3, KOF 2000** are listed on `PROGLBA` (SMA-protected version) by all sources. MAME also documents a non-SMA version on `PROGBK1`.
- **Production runs.** JNX itself warns that some games use more than one board set and that its list shows the most common. Treat every pair as "typical", not guaranteed.
- **Spot checks against hands-on builds** (from the README's worked examples): the Blazing Star write-up used a Neo Geo Cup '98 donor, and the table gives both games `PROGBK1` + `CHA512Y`; the Pulstar plan used `PROGBK1` + `CHA256`; the Ironclad build used `PROGTOP` + `CHA256` from a KOF '94 donor, and the table gives KOF '94 exactly that pair; Top Hunter's P ROM sits on a `PROGTOP`, as listed.
- **Not covered:** AES boards, bootlegs, homebrew, development boards (`CHAMC2`, `PROGMC2`), and the NeoGeo Dev Wiki's *Cartridge ROM arrangements* page, which blocked automated access.

---

## 7. Sources and method

| Key | Source | Contribution |
|---|---|---|
| **M** | [MAME `neogeo.cpp`](https://github.com/mamedev/mame/blob/master/src/mame/snk/neogeo.cpp) | Per-game header comments (`ID-xxxx`, `NGM-xxx`, `NEO-MVS PROGxxx / NEO-MVS CHAxxx`), titles and years from the `GAME()` rows. Parsed by script; 149 headers carry an MVS board line. Same file snapshot as the README (SHA-256 `77324df6…afc97`). |
| **K** | [Mike McBike @ Home: Neo Geo Cartridges](http://www.wolfgangrobel.de/mvs/neogeogames.htm) | Year, NGH number, developer, PROG and CHA per game; bold cells mark alternate boards. Transcribed by hand from the page. |
| **J** | [JNX: Neo-Geo MVS Cart Board Codes](http://www.jamma-nation-x.com/jammax/mvsboardcodes.html) | Game name, PROG and CHA per game (149 rows). Transcribed by hand from the page. |

**Method.** Board names from all three sources were normalised (hyphens and spaces removed; `BK3-R` = `PROGBK3R`; revision and date codes moved to notes). Games were joined on the game ID (MAME ↔ Mike) and on the title (JNX), with five manual title matches. For each game the standard pair is the one named first by at least two sources. A pair earns 🟢 only if every covering source lists it, either as its main pair or as a documented alternate.

No ROM data is included or linked.
