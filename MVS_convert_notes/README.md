# Neo Geo MVS — Mask ROM → EPROM Replacement Reference

Which EPROM replaces which mask ROM on Neo Geo MVS cartridges, with a **confidence rating** and **sources** attached to every claim.

> [!IMPORTANT]
> This is compiled community knowledge, not an SNK document. Chip markings, PCB revisions and jumper settings vary between carts. Verify against **your own board** before ordering or burning anything. No ROM images are included or linked.

| | |
|---|---|
| **Scope** | MVS game cartridges (PROG + CHA boards) and the motherboard BIOS chip. AES carts share many parts but were not researched. |
| **Compiled** | September 2026 |
| **Data basis** | Mask ROM part numbers from MAME's Neo Geo driver (283 ROM sets parsed), plus wiki pages, repair write-ups, forum threads and five manufacturer datasheets |
| **Companion files** | [BOARDS.md](BOARDS.md): PROG and CHA board per game (also as [mvs_boards.csv](mvs_boards.csv)) |

## Contents

1. [How to read the confidence ratings](#1-how-to-read-the-confidence-ratings)
2. [The replacement chips at a glance](#2-the-replacement-chips-at-a-glance)
3. [PROG board: P and V ROMs](#3-prog-board-p-and-v-roms)
4. [CHA board: C, S1 and M1 ROMs](#4-cha-board-c-s1-and-m1-roms)
5. [Gotchas](#5-gotchas)
6. [Board notes](#6-board-notes)
7. [Worked examples](#7-worked-examples)
8. [Programmable parts already seen on real carts](#8-programmable-parts-already-seen-on-real-carts)
9. [Datasheet cross-check](#9-datasheet-cross-check)
10. [Motherboard BIOS](#10-motherboard-bios)
11. [Data quality and open questions](#11-data-quality-and-open-questions)
12. [Sources](#12-sources)
13. [Appendix: how the MAME data was extracted](#appendix-how-the-mame-data-was-extracted)

---

## 1. How to read the confidence ratings

| Badge | Meaning |
|---|---|
| 🟢 **High** | Two or more independent sources agree, or a hands-on conversion/repair reports it working. |
| 🟡 **Medium** | One credible source; or MAME's community-written chip notes alone; or a capacity-based inference that is consistent with sourced rows. |
| 🔴 **Low** | My own inference, a claim I could not re-verify, or a design its author calls untested. |
| ❔ **Unknown** | Looked; found nothing reliable. |

- Citations look like **[S5]** and point to the [Sources](#12-sources) table. **[S1]** is MAME's driver, analysed by me (see the [appendix](#appendix-how-the-mame-data-was-extracted)).
- Counts like *(38)* mean "38 MAME sets (parents, clones and bootlegs) list this part in their ROM notes". They show how common a part is, not production volumes.
- MAME's part numbers describe the chip printed on the dumped cart. They are community-written and not audited.

---

## 2. The replacement chips at a glance

Nine EPROM families cover every mask ROM that has a one-chip equivalent. Two cases have no one-chip answer.

| EPROM | Pins | Organisation | Replaces (mask ROM) | Used for | Confidence |
|---|---|---|---|---|---|
| **27C1024** | 40 | 64K × 16 (1 Mbit) | TC531024 | Motherboard BIOS; small "P2" on early carts | 🟢 BIOS · 🟡 P2 |
| **27C400** | 40 | 256K × 16 or 512K × 8 (4 Mbit) | TC534200 family | P 512 KB; C 512 KB; V 512 KB (40-pin originals) | 🟢 P · 🟡 C, V |
| **27C800** | 42 | 512K × 16 or 1M × 8 (8 Mbit) | TC538200 family | P, C, V at 1 MB (V in byte mode) | 🟢 |
| **27C160** | 42 | 1M × 16 or 2M × 8 (16 Mbit) | TC5316200 family | P, C, V at 2 MB; two per 32 Mbit V ROM | 🟢 |
| **27C322** | 42 | 2M × 16, word mode only (32 Mbit) | TC5332205 / -202, KM23C32000 | P and C at 4 MB. **Never V.** | 🟢 |
| **27C1000 / 27C301** | 32, non-JEDEC | 128K × 8 | TC531000 family | S1 on non-encrypted boards; M1 if the CHA jumpers allow | 🟢 |
| **27C010 / 27C1001** | 32, JEDEC | 128K × 8 | TC531001 family | M1 | 🟢 |
| **27C2001** (= 27C020) | 32, JEDEC | 256K × 8 | TC532000, MB832000 | M1 at 256 KB | 🟡 |
| **27C4001** (= 27C040; Macronix sells the footprint as MX27C4000) | 32, JEDEC | 512K × 8 | TC534000 | M1 at 512 KB; possibly V at 512 KB | 🟡 M1 · 🔴 V |
| *no single chip* | — | — | TC5332204 / -201, TC533204 (32 Mbit **V**) | **2 × 27C160** per original chip | 🟢 |
| *no equivalent* | — | — | TC5364205 (64 Mbit) | Split across smaller EPROMs on a board with enough sockets | 🟢 |

Sources: [S2] [S5] [S6] [S7] [S16] [S17] [S24] [S30] [S32] [S35] [S36]. Pin counts and organisations for 27C400/800/160/322 come from [S16]; the 27C1024 pin count and the 27C010/1001 JEDEC 32-pin package are standard datasheet facts I did not cite separately.

**Rule of thumb** 🟢 [S5]: for Toshiba mask ROMs, drop the `TC53` prefix and read the density.

| Mask ROM | → | EPROM |
|---|---|---|
| TC531001 | 1001 | 27C1001 or 27C010 |
| TC531000 | 1000 | 27C1000 or 27C301 |
| TC534200 | 4200 | 27C400 |
| TC538200 | 8200 | 27C800 |
| TC5316200 | 16200 | 27C160 |
| KM23C32000 (Samsung) | — | 27C322 (not for V ROMs) |
| TC5364205 | — | none |

For other makers (Fujitsu `MB83…`, Sony `CXK38…`, Hitachi `HN62…`, and house-marked `VIC9…`/`UM…` parts) I matched by density and package family. That is 🟡, not verified part by part.

---

## 3. PROG board: P and V ROMs

### P ROM — 68000 program, 16-bit

| Capacity | Mask ROMs in MAME notes | EPROM | Conf. | Sources |
|---|---|---|---|---|
| 1 Mbit × 16 (128 KB, the small "P2" on early carts, e.g. `alpham2`, `kotm`, `sengoku`, `gpilots`, `fatfury1`) | TC531024 (9) | 27C1024 | 🟡 | [S1] [S24] |
| 4 Mbit (512 KB) | TC534200 (38) · MB834200 (8) · CXK384500 (3) · HN62434 (2) · HN62422PC (1) · UM8303B (1) | 27C400 | 🟢 | [S2] [S5] [S16] [S17] |
| 8 Mbit (1 MB) | TC538200 (80) · VIC940800 (2) · CXK388000 (1) · CXK388002 (1) | 27C800 | 🟢 | [S2] [S5] [S9] |
| 16 Mbit (2 MB) | TC5316200 (57) · plus four `kof98*` sets noted only as "16mbit" | 27C160 | 🟢 | [S2] [S5] [S6] |
| 32 Mbit (4 MB) | TC5332205 (47) · TC5332202 (2) | 27C322 | 🟢 | [S2] [S5] [S14] |
| 64 Mbit (8 MB) | TC5364205 (1: `rotd`, Rage of the Dragons) | none | 🟢 | [S5] [S16] |
| 256 KB inside the NEO-SMA chip | "stored in the custom chip": `kof99` (+`h` `e` `k`), `garou` (+`h` `ha`), `kof2000` | cannot be replaced by an EPROM | 🟡 | [S1] |

The 2 MB P ROMs on the SMA carts `garou`, `garouha` and `kof99e` are noted in MAME as four **M27C160** chips, i.e. already EPROMs (see [section 8](#8-programmable-parts-already-seen-on-real-carts)).

### V ROM — ADPCM samples, 8-bit bus

| Capacity | Mask ROMs in MAME notes | EPROM | Conf. | Sources |
|---|---|---|---|---|
| 4 Mbit (512 KB), `…4200` series | TC534200 (8) · MB834200 (1) | 27C400 | 🟡 | [S5] [S16] |
| 4 Mbit (512 KB), `…4000` series (probably 32-pin) | MB834000 (9) · TC534000 (5) · CXK384000 (1) · CXK384001 (1) · UM8302 (1) | 27C4001 / 27C040, pinout unverified | 🔴 | [S22] |
| 8 Mbit (1 MB) | TC538200 (58) · CXK388000 (4) · HN62408 (2) · VIC930800 (2) · HN62308BPC (1) · MB838000 (1) | 27C800, byte mode | 🟢 | [S2] [S5] [S11] |
| 16 Mbit (2 MB) | TC5316200 (93) · VIC931600 (2) · CXK381600 (1) | 27C160, byte mode | 🟢 | [S2] [S6] [S11] |
| 32 Mbit (4 MB) | TC5332204 (83) · TC5332201 (11) · TC533204 (1) | **2 × 27C160** per chip. Never 27C322. | 🟢 | [S2] [S5] [S7] [S13] |
| 64 Mbit (8 MB) | TC5364205 (25), e.g. `mslug4` `mslug5` `kof2002` `kof2003` `svc` `matrim` `samsho5` `rotd` | none | 🟡 | [S1] [S5] |

> [!WARNING]
> **V ROMs are read in 8-bit mode.** Original mask ROMs could output bytes. The 27C322 is word-only and physically lacks the /BYTE pin, so it cannot replace a V ROM. Details in [gotchas 1–2](#5-gotchas).

Ways people have tackled 32 Mbit V ROMs beyond "two 27C160":

- Splitting a V ROM's address space across two chips with on-board decoding (Twinkle Star Sprites build) — 🟡 [S13]
- V-ROM emulation modules described as in development — 🔴 [S12]
- A 29F160-to-27C160/322 flash adapter board whose own page calls it untested — 🔴 [S29]

---

## 4. CHA board: C, S1 and M1 ROMs

### C ROM — sprite graphics, 16-bit, used in pairs

C ROMs are wired as pairs of 16-bit devices [S3].

| Capacity | Mask ROMs in MAME notes | EPROM | Conf. | Sources |
|---|---|---|---|---|
| 4 Mbit (512 KB) | TC534200 (23) · MB834200 (7) · CXK384000 (2) | 27C400 | 🟡 | [S5] [S16] |
| 8 Mbit (1 MB) | TC538200 (53) · CXK388000 (4) · HN62408 (2) · HN62408PD (1) · MB838200 (1) | 27C800 | 🟢 | [S5] [S10] |
| 16 Mbit (2 MB) | TC5316200 (62) · VIC931600 (2) · CXK381600 (1) · UMT301B (1) · UMT302B (1) | 27C160 | 🟢 | [S5] [S6] |
| 32 Mbit (4 MB) | TC5332205 (52) · TC5332202 (11). Samsung KM23C32000 also reported on some carts. | 27C322 | 🟢 | [S5] [S6] [S7] [S13] |
| 64 Mbit (8 MB) | TC5364205 (73), from about `zupapa` / `kof97` / `lastblad` onward. `garou` uses eight of them. | none. Split into 2 × 27C322 (or 4 × 27C160) on a board with enough sockets | 🟢 | [S1] [S3] [S5] [S6] |

### S1 — fix-layer tiles, 8-bit

| Capacity | Mask ROMs in MAME notes | EPROM | Conf. | Sources |
|---|---|---|---|---|
| 1 Mbit × 8 (128 KB; 233 of 283 sets list an S1) | TC531000 (152) · MB831000 (7) · CXK381000 (5) · HN62321 (2) · TC531000DP (2) · VIC930100 (2) · HN62321BP (1) · T531000 (1) · UMK300 (1) | **27C1000 or 27C301 (non-JEDEC)**. A 27C010/27C1001 only works with pins 2 and 24 swapped. | 🟢 | [S5] [S6] [S19] [S20] [S21] |

> [!NOTE]
> **Encrypted (NEO-CMC) boards have no S1 chip.** MAME's comment says their fix-layer data comes from the C ROMs. 48 of the 283 entries list no S1: the `neogeo` BIOS entry, the `mvstemp` test set, and 46 games/bootlegs from `zupapa` onward (`kof99`, `garou`, `mslug3`, `kof2000`, `svc`, `kof2003` and so on). 🟡 [S1]; related: the CMC scrambles C and S1 data together [S4].

### M1 — Z80 sound program, 8-bit

| Capacity | Mask ROMs in MAME notes | EPROM | Conf. | Sources |
|---|---|---|---|---|
| 1 Mbit (128 KB) | TC531001 (152) · TC531001DP (6) · CXK381003 (4) · HN62321A (2) · T531001 (2) · VIC930100 (2) · CXK381003A (1) · HN62321AP (1) · UML359 (1) | 27C010 or 27C1001 (JEDEC) | 🟢 | [S5] [S6] [S15] [S28] [S35] |
| 2 Mbit (256 KB) | TC532000 (14) · MB832000 (9) | 27C2001 (= 27C020) | 🟡 | [S1] [S6] [S30] |
| 4 Mbit (512 KB) | TC534000 (16) | 27C4001 (= 27C040; MX27C4000 has the same 32-pin footprint) | 🟡 | [S1] [S6] [S30] [S36] |

The 256 KB and 512 KB rows are 🟡 because [S6] only says newer games need 2 or 4 Mbit M ROMs; the EPROM choice follows from capacity. MAME notes name 27C2000, 27C040 and M27C4001 on real dumps ([section 8](#8-programmable-parts-already-seen-on-real-carts)). Pinouts of the EPROM side are checked against datasheets in [section 9](#9-datasheet-cross-check).

MAME's header adds that many M1 chips (IDs 0001–0045 and 0267–0272) hold mirrored 64 KB or 128 KB data, that the smallest M1 on SNK carts is 1 Mbit and the largest 4 Mbit, and that all S1 ROMs are 1 Mbit. So an image can be smaller than the chip it came from. 🟡 [S1]

---

## 5. Gotchas

| # | Gotcha | Conf. | Sources |
|---|---|---|---|
| 1 | **V ROMs are read in 8-bit mode.** The 42-pin 27C322 is word-only, so it cannot replace a V ROM. Use 27C160 (byte-capable): two per 32 Mbit chip, with jumpers set for 16 Mbit V ROMs. A Blazing Star conversion only produced correct sound after switching to four 27C160s. | 🟢 | [S2] [S5] [S7] [S13] |
| 2 | **/BYTE must be low.** On the boards documented, V-ROM sockets are wired for byte mode: the PROG-GSC schematic ties /BYTE to ground, and PROGBK1 uses jumpers. Set the jumpers for the EPROM size you fitted. | 🟢 | [S2] [S11] |
| 3 | **Two different 1 Mbit pinouts.** S1 is always non-JEDEC (27C1000/27C301). M1 can be JEDEC (27C010/27C1001) or non-JEDEC depending on CHA jumpers. A 27C301 differs from a 27C010 by two swapped pins (2 and 24; in the JEDEC 27C010, pin 2 is A16 and pin 24 is OE), so programming needs an adapter or pin swap. | 🟢 | [S5] [S6] [S19] [S35] |
| 4 | **"27C1000" is not one pinout.** ST made both variants and Macronix's part is JEDEC. Prefer ST or AMD, check the datasheet, and test-read a known chip. | 🟢 | [S6] [S20] |
| 5 | **Newer games need bigger M1 ROMs** (2 or 4 Mbit) than the 1 Mbit parts on most carts. | 🟢 | [S6] |
| 6 | **4 Mbit × 16 mask ROMs use the 27C400-family pinout, not the 27C4096 pinout.** Adapters exist precisely to translate between them. Some MAME sets list 27C4096-family EPROMs (`HN27C4096HG`, `M27C4002`, `27C240`), so match your board instead of assuming. | 🟡 | [S1] [S16] [S17] |
| 7 | **64 Mbit mask ROMs have no EPROM equivalent.** Split the image across smaller EPROMs. The CHA256 board tops out at 32 MiB of sprite data. | 🟢 | [S3] [S5] [S6] |
| 8 | **Protection chips.** NEO-CMC scrambles S1 and C data (M1 too in the later "050" version) and has never been reproduced. Like-for-like repairs burn the same dump. Moving a game onto a different protection setup is not a simple EPROM swap (my inference). | 🟢 CMC facts · 🔴 inference | [S4] |
| 9 | **Programming.** Use a programmer or adapter that handles 40/42-pin 16-bit EPROMs. With a TL866 plus adapter: select the 27C4096 device, disable the ID check, use a ~50 µs pulse delay and write in 512 KB chunks. Set Vpp per the datasheet: one builder killed a 27C160 with the wrong programming voltage and had another chip programmed at 13 V that still verified but could no longer be erased. | 🟡 | [S6] [S16] [S18] |
| 10 | **Verify twice**, after writing and again before soldering. UniBIOS's cart CRC check reportedly covers program ROMs only, so it will not catch a bad C or S ROM. | 🟡 | [S6] [S9] |
| 11 | **Speed grade and fakes.** For 1 Mbit EPROMs, 150 ns or faster is the common advice. Be wary of listings claiming "new" old EPROMs (may be relabelled slower parts or fakes). | 🟡 | [S15] [S28] |
| 12 | **Order the right package.** For a 2.54 mm DIP42 socket, ST's M27C160 comes as `F` (windowed, UV-erasable) or `B` (plastic DIP42). The `S` suffix is a shrink DIP with 1.78 mm pitch, and `K` and `M` are PLCC44 and SO44. | 🟢 | [S32] |
| 13 | **OTP parts cannot be erased.** The Atmel AT27C010/L and the Macronix MX27C4000 are one-time programmable, so a bad burn means a new chip. Windowed ST parts (`F`) can be UV-erased. | 🟢 | [S32] [S35] [S36] |
| 14 | **Never program an MX29F1615 with an EPROM profile.** Its BYTE/VPP pin is rated −0.5 to 10.5 V, and EPROM programming puts 12.5 V there. Use the flash device profile, and check that your programmer lists it. | 🟢 datasheets · 🔴 programmer support | [S32] [S33] |

---

## 6. Board notes

### PROGBK1 🟢 [S2]

- P1 can be 4, 8 or 16 Mbit (27C400 / 27C800 / 27C160).
- P2 is bankswitched with a 74LS74 and can hold the same types plus 27C322. It is only available if P1 is 4 or 8 Mbit.
- Up to four V ROMs of 8, 16 or 32 Mbit (27C800 / 27C160 / 27C322), 16 MiB total, but see [gotcha 1](#5-gotchas): 27C322 is unusable for V.
- A 4 Mbit V ROM is allowed only if there is exactly one and it sits in the last used slot.
- Jumper groups select /OE, /CE and size for P1, P2 and each V ROM. See the wiki tables.

### CHA256 / CHA256B

- C1–C8 sockets. An added 74LS74 extends C ROM capacity from 8 MiB to 32 MiB (256 Mbit). 🟢 [S3]
- CHA256 and CHA256B are different boards with different jumper settings. 🟢 [S6]
- M1 can be set for JEDEC or non-JEDEC parts by jumper. 🟢 [S6]
- For the C1/C2 pair, one expert's table says: jumper J11 closed and R1 open for 27C322, the opposite for smaller parts. The same thread shows a builder finding board scans and photos that disagree with it. 🔴 Check your own board's scans. [S6]

### PROGTOP

- A PROGTOP P2 socket (Top Hunter) took an M27C800 in place of a TC538200. 🟢 [S9]
- Ironclad was built on PROGTOP + CHA256: 3 × 27C160 (V1, V2, P1). 🟢 [S6]
- A Blazing Star build on PROGTOP is documented, using 27C322 for P1 and SP2 with data repeated to fill 4 MB and problems addressing the upper 1 MB of SP2. I read only part of that thread, so treat its jumper notes as 🔴 until you read how it was resolved. [S14]

### Which PROG/CHA pair does a game use?

See **[BOARDS.md](BOARDS.md)** (also as [mvs_boards.csv](mvs_boards.csv)) for a per-game list of PROG and CHA boards covering 150 MVS entries. Each row carries a confidence badge from cross-checking MAME's header comments [S1], Mike McBike's table [S8] and the JNX board-code list [S37]: 148 rows are 🟢 and 2 are 🟡. `PROGBK1` is the most-used PROG board and `CHA256` the most-used CHA board; the largest family is `PROGBK1` + `CHA256` with 25 games. Donor and target boards must match in size, bankswitching and protection.

---

## 7. Worked examples

| Build | Boards | EPROMs used | Outcome | Conf. | Source |
|---|---|---|---|---|---|
| **Ironclad** | PROGTOP + CHA256 | 3 × 27C160 (V1, V2, P1) · 4 × 27C322 (C1–C4) · 27C1000 (S1) · 27C1001 (M1). V1 file split across two 27C160s. | Booted on the first attempt | 🟢 | [S6] |
| **Pulstar** | PROGBK1 + CHA256 | 27C160 (SP2) · 27C800 (P1) · 4 × 27C160 (V1–V4, striped write) · 6 × 27C322 (C1–C6) · 2 × 27C160 (C7, C8) · 27C1000 (S1) · 27C1001 (M1) | Plan reviewed as sound by an experienced converter. The builder's first attempt showed scrambled sprites, traced partly to bad writes on C1–C3. Final result not shown. | 🟡 | [S6] |
| **Blazing Star** | PROGBK1 + CHA512Y (Neo Geo Cup '98 donor) | 27C322 for C ROMs · **4 × 27C160** for V ROMs · added 74LS74, 4.7 kΩ resistor and jumpers | Sound fixed by moving V ROMs to 27C160 in byte mode; write-up ends with a finished cart | 🟢 | [S7] |
| **Top Hunter** (repair) | PROGTOP | M27C800 replacing a bad TC538200 P2 (046-p2) | Graphic glitches fixed | 🟢 | [S9] |
| **MVS cartridge repair** | CHA board (C8) | 27C800 replacing a 1 MB C8 | Replacement demonstrated; outcome not visible in the excerpt I read | 🟡 | [S10] |
| **Twinkle Star Sprites** (from scratch) | board type not confirmed in the excerpt I read | C ROMs all 27C322 (data duplicated to fill smaller sockets) · S1 and M1 as EPROMs · V1 split across two chips using the board's address decoding | Documented in a blog post | 🟡 | [S13] |
| **Pochi & Nyaa** | (16 Mbit C sockets) | 64 Mbit C ROMs split into four parts each | Described second-hand; I did not read that thread | 🟡 | [S6] |

Parts a builder ordered for Pulstar/Ironclad (reviewed by twistedsymphony) 🟢 [S6]: `M27C160-100F1`, `M27C800-100F1`, `M27C322-100F1`, `M27C1000-12F1`, `M27C1001-10F1`. Mike McBike's Pulstar used a Hitachi `HN27C301G-17` for S1.

---

## 8. Programmable parts already seen on real carts

Everything here is 🟡: it comes from MAME's ROM-set notes and was not independently verified. "Named" means the part is what MAME's comment says; a few comments are ambiguous.

| Function | Part named in MAME notes | Sets |
|---|---|---|
| P, 4 Mbit | M27C4002 | `aof2a` `fatfurspa` `kof95a` `rbff1a` `rbff1ka` `samsho3` |
| P, 4 Mbit | AM27C400 | `vliner` `vliner6e` `vliner7e` |
| P, 4 Mbit | D27C4000 | `roboarmya` `wh1` `wh1ha` |
| P, 4 Mbit | TC574200 (Toshiba EPROM/OTP family) | `2020bba` `eightman` |
| P, 4 Mbit | 27C240 · HN27C4096HG | `pbobblen` · `sbp` |
| P, 8 Mbit | M27C800 · M27C160 (1 MB image) | `jockeygpa` · `jockeygp` |
| P, 16 Mbit | M27C160 (×4 on the SMA carts, ×2 on `kof98a`) | `garou` `garouha` `kof99e` `kof98a` |
| P, 32 Mbit | "EPROM" (type unspecified) | `samsho5a` |
| V, 32 Mbit | M27C322 | `sbp` |
| C, 16 Mbit | M27C160 | `sbp` |
| S1 | M27C4001 (128 KB image on a 4 Mbit part) · HN27C301 (Mike McBike's Pulstar, [S6]) | `sbp` |
| M1, 128 KB | TC541000 · TC54H1000 · M27C1001 · "27c010" | `eightman` `roboarmy` `roboarmya` · `2020bb*` `wh1` · `pbobblen` `zupapa` · `rotd*` |
| M1, 256 KB | 27C2000 | `kof98ka` |
| M1, 512 KB | M27C4001 · "27c040" | `jockeygp*` `sbp` · `samsho5*` |

Notes:

- `sbp` is an **unlicensed 2004 release by Vektorlogic**, not an SNK production cart [S1]. Its EPROMs show the parts work, not what SNK shipped.
- The Toshiba `TC54`/`TC57` prefixes denote EPROM/OTP families, not mask ROM 🟡 [S23].
- `M27C…` is ST, `AM27C…` is AMD, `D27C…` is NEC, `HN27C…` is Hitachi. This matters for [gotcha 4](#5-gotchas).
- The MAME comment for the **Ghost Lop prototype** (`ghostlop`) says the location-test version used socketed EPROMs on the PROG board, flash chips on adapter boards for the C ROMs and EPROMs for M1 and S1 [S1].

### Flash instead of EPROM

The **Metal Slug 5 "clear cart" bootleg** (`mslug5b`) is all erasable flash, on custom logic instead of SNK's protection chips [S1] 🟡:

| Position | Flash part |
|---|---|
| P1 (1 MB) | MX29F1615PC-10 |
| P2 and V (4 MB) | LH28F320BJD-TTL80 (3.3 V) |
| C (8 MB) | M59PW064 64 Mbit (SO44, 3.3 V) |
| C (2 MB) | LH28F160BJD-TTL80 (DIP, 3.3 V) |
| S1 | W29C011A-15 |
| M1 | W29EE011-15 |

MAME's note: the PROG board has no V encryption and uses a PLCC EPM7096LC84-15 for PCM, with 16-bit V ROMs decoded by two 74HC245; the CHA board has no C/M encryption and uses a PALCE16V8 for ZMC and five 74HC273A latches in place of NEO-273. The MX29F1615 has the same DIP42 pinout as the M27C160 at every pin: 🟢 [S32] [S33], details in [section 9](#9-datasheet-cross-check).

---

## 9. Datasheet cross-check

Five manufacturer datasheets were supplied as PDFs: ST M27C160 [S32], Macronix MX29F1615 [S33], ST M27C512 [S34], Atmel AT27C010/L [S35] and Macronix MX27C4000 [S36]. They are copies from datasheet aggregators, so check the manufacturer's site for newer revisions. Pin numbers below were read from the datasheets' pin diagrams. Chip and output enables are active low on all of these parts.

### M27C160 vs MX29F1615 (DIP42)

**Verdict: 🟢 the two parts have the same DIP42 pinout at every pin.** For reading, the MX29F1615 behaves like an EPROM: it powers up in read mode and needs no command, `BYTE/VPP` low gives 8-bit output (with `Q15/A-1` as the lowest address bit) and high gives 16-bit output, exactly as the M27C160's `BYTEVPP` does. [S32] [S33]

| Pin(s) | M27C160 (ST) | MX29F1615 (Macronix) |
|---|---|---|
| 1–2 | A18, A17 | A18, A17 |
| 3–10 | A7 … A0 | A7 … A0 |
| 11 | E | CE |
| 12 and 31 | VSS | GND |
| 13 | G | OE |
| 14–21 | Q0 Q8 Q1 Q9 Q2 Q10 Q3 Q11 | same |
| 22 | VCC | VCC |
| 23–29 | Q4 Q12 Q5 Q13 Q6 Q14 Q7 | same |
| 30 | Q15A–1 | Q15/A-1 |
| 32 | BYTEVPP | BYTE/VPP |
| 33–41 | A16 A15 A14 A13 A12 A11 A10 A9 A8 | same |
| 42 | A19 | A19 |

What differs, from the two datasheets:

| Item | M27C160 (ST) | MX29F1615 (Macronix) | Why it matters | Conf. |
|---|---|---|---|---|
| Memory type | UV EPROM (`F`) or OTP (`B`, `S`, `K`, `M`) | Flash, rated 100 program/erase cycles | Rewritable, but with low endurance | 🟢 |
| Read timing, 100 ns grade | Address, CE 100 ns; OE 50 ns; output float 40 ns max | Address, CE 100 ns; OE 50 ns; output float 35 ns max | Equivalent | 🟢 |
| Input-high level (VIH) | 2.0 V min | 2.4 V min | Could matter only if an address line is driven by an LS/TTL output, which guarantees just 2.4 V high. HC and CMOS drivers are fine. My inference, untested. | 🔴 |
| Output drive | VOH 2.4 V at −400 µA; VOL 0.4 V at 2.1 mA | VOH 2.4 V at −2 mA; VOL 0.45 V at 2.1 mA | Comparable | 🟢 |
| Pin 32 voltage limits | −2 to 14 V; programmed at 12.5 V | −0.5 to 10.5 V; about 10 V enables writes | Do not use an EPROM programming profile on the flash | 🟢 |
| Byte/word switching | Switching timing is specified | Keep the pin static high or low; dynamic switching is not recommended | Fine: Neo Geo boards hard-wire or jumper it | 🟢 |
| Programming | VCC 6.25 V, VPP 12.5 V, 50 µs pulses | 5 V; command sequences (64-word page program, chip erase) | Needs a programmer with an MX29F1615 profile; I did not check which programmers have one | 🟢 method · 🔴 support |
| Device ID | 20h / B1h | C2h / 6Bh | Auto-detect tells them apart | 🟢 |
| Packages | FDIP42W, PDIP42, SDIP42, PLCC44, SO44 | PDIP42 (600 mil) only | Buy `F` or `B` for a DIP42 socket | 🟢 |
| Datasheet status | Rev. -04, Jan 2002 | **Preliminary** rev. 1.2, Nov 2002 | Look for the latest Macronix revision | 🟢 |

**In a Neo Geo socket.** A MX29F1615PC-10 fits where an M27C160-100 fits, including 8-bit V-ROM sockets that hold the byte pin static (pin level 🟢 [S32] [S33]). MAME records one as P1 in a bootleg cart ([section 8](#8-programmable-parts-already-seen-on-real-carts)), which is the only in-circuit evidence I have: 🟡 [S1]. Test any flash part in a spare cart before trusting it.

### 1 Mbit, 4 Mbit and 512 Kbit parts

| Part | Datasheet facts | Neo Geo relevance | Conf. |
|---|---|---|---|
| **AT27C010/L** (Atmel) | 128K × 8, one-time programmable. 32-pin PDIP, PLCC or TSOP. JEDEC pinout: pin 1 VPP, pin 2 A16, pin 22 CE, pin 24 OE, pin 30 NC, pin 31 PGM, pin 32 VCC. In read mode PGM and VPP may be at either logic level. Grades from 45 ns to 150 ns. | The JEDEC side of the 27C010 vs 27C301 difference: A16 on pin 2 and OE on pin 24, which a non-JEDEC 27C301 swaps [S19]. Suits a JEDEC M1. | 🟢 [S35] |
| **MX27C4000** (Macronix) | 512K × 8, one-time programmable, plastic packages only. 32-pin PDIP, PLCC, SOP or TSOP. Pin 1 VPP, pin 2 A16, pin 30 A17, pin 31 A18, pin 32 VCC, no PGM pin. | The same 32-pin layout as the 27C010 except pins 30–31 (A17 and A18 instead of NC and PGM), i.e. the 27C040 footprint [S30]. Fits the 512 KB M1 row. Whether a TC534000 socket is wired for it is still unverified. Name trap: `27C4000` (32-pin, ×8) is not `27C400` (40-pin, ×16 or ×8). | 🟢 pinout · 🟡 M1 use · 🔴 V-ROM use [S36] |
| **M27C512** (ST) | 64K × 8, 28-pin (FDIP28W or PDIP28; PLCC32 and TSOP28 also exist). A0–A15, pin 22 is G/VPP, VPP 12.75 V. | Not needed for SNK's own carts, whose M1 and S1 are at least 1 Mbit. MAME lists a 64 KB M1 for the V-Liner sets (`vliner*`) and the `mvstemp` test set, and a 64 KB S1 for the homebrew `lasthope`. I found no source for how those originals are packaged. It is not a drop-in for a 32-pin 1 Mbit socket. | 🟢 pinout · ❔ use [S34] [S1] |

---

## 10. Motherboard BIOS

| Item | Finding | Conf. | Sources |
|---|---|---|---|
| Stock BIOS on MV1FZ-class boards | Toshiba `TC531024P-15` (128 KB × 16). **27C1024** is the EPROM replacement. | 🟢 | [S24] [S31] |
| UniBIOS adapters | NeoBiosMasta Deck is sold as compatible with 27C1024 chips | 🟢 | [S26] |
| Larger 27C4096-class chips | A forum member notes a 27C240/27C4096 is four times the capacity and has two extra pins that must be tied off. How to fill the extra space is not stated (repeating the image four times is common practice but **unsourced** here). | 🟡 pin tie · 🔴 image fill | [S25] |
| MV1B / MV1C | NeoBiosMasta targets both boards [S26]; the MV1C BIOS is surface-mounted [S27]. MAME lists a 512 KB "MV1C mask ROM" BIOS (`sp-45.sp1`, `sp-j3.sp1`). | 🟡 | [S1] [S26] [S27] |
| SM1 / SFIX / LO system ROMs | Listed at 128 KB each in MAME. I found no reliable replacement-chip information. | ❔ | — |

---

## 11. Data quality and open questions

**How complete is the chip data?**

- 283 ROM sets parsed; **192** have a part number for every chip, **91** have at least one chip with no note (mostly bootlegs, prototypes and hacks).
- **52** distinct mask ROM part numbers appear. Counts are sets, not carts.

**Inconsistencies in MAME's notes**

- `kizuna` and `kizuna4p`: 2 MB C7/C8 images noted as TC538200, which is an 8 Mbit part.
- `zedblade`: a 512 KB P1 image noted as TC538200.
- Four `kof98*` sets note P1 only as "mask rom 16mbit"; `samsho5a` notes P as "EPROM".
- `flipshot` M1 reads "TC 531001" (normalised in the counts).
- M1 notes "mask rom 27c010" (`rotd*`) and "mask rom 27c040" (`samsho5*`) are ambiguous: a chip marked like an EPROM but recorded as the M1 ROM.

**Assumptions I could not verify**

- Toshiba density digits (…4200 = 512K×8 or 256K×16, …4000 = 512K×8, …1024 = 64K×16, …16200 = 2M×8 or 1M×16) come from Elnec's decoder, which says it may not be valid for every chip 🟡 [S23].
- Package and pinout of the …4000-series 4 Mbit ×8 mask ROMs are unverified. The MX27C4000 datasheet [S36] confirms the EPROM side (a 27C040 footprint) but not the mask-ROM side, and some 4 Mbit ×8 mask ROMs use non-JEDEC pinouts (an example from other arcade boards is in [S22]).
- Non-Toshiba parts are matched to EPROMs by density and family.
- Which programmers support the MX29F1615 is unchecked 🔴.
- The original packaging of the 64 KB parts in the V-Liner M1 and the Last Hope S1 is undocumented in my sources.

**Not covered or not usable**

- AES carts; SM1/SFIX/LO system ROMs; per-board socket maps beyond PROGBK1 and part of CHA256.
- These pages blocked automated access and were **not used**: a 68kmla.org cross-reference thread, `smitdogg.mameworld.info/du/romref.txt` (the cross-reference table that [S6] cites), and wiki.neogeodev.org `index.php?title=` URLs.
- Community advice ages: [S5] is from 2018 and [S6] from 2021. Check newer threads before committing money.
- The five datasheets [S32]–[S36] are user-supplied PDFs from aggregator sites (the Macronix MX29F1615 copy is watermarked iiic.cc and marked PRELIMINARY).
- The NeoGeo Dev Wiki's *Cartridge ROM arrangements* page (per-game boards and sizes) blocked automated access; only its search snippet was seen.

---

## 12. Sources

| ID | Source | Used for | Type |
|---|---|---|---|
| S1 | [MAME `neogeo.cpp`](https://github.com/mamedev/mame/blob/master/src/mame/snk/neogeo.cpp) (raw: [file](https://raw.githubusercontent.com/mamedev/mame/master/src/mame/snk/neogeo.cpp)) | Mask ROM part numbers, sizes, EPROM/flash parts seen, BIOS notes. **My analysis**, see appendix | Emulator source comments |
| S2 | [NeoGeo Dev Wiki: PROGBK1](https://wiki.neogeodev.org/index.php/PROGBK1) | P/V ROM sizes and EPROM types, 27C322 unusable for V | Wiki |
| S3 | [NeoGeo Dev Wiki: NEO-273](https://wiki.neogeodev.org/index.php/NEO-273) | CHA256 32 MiB capacity, paired 16-bit C ROMs | Wiki |
| S4 | [NeoGeo Dev Wiki: NEO-CMC](https://wiki.neogeodev.org/index.php/NEO-CMC) | Encryption scope; no reproduction of the chip | Wiki |
| S5 | [arcade-projects: "Options for Conversion of this MVS Boot?"](https://www.arcade-projects.com/threads/options-for-conversion-of-this-mvs-boot.6544/) (twistedsymphony, Aug 2018) | Mask ROM → EPROM mapping rule; V-ROM caveat; 64 Mbit has no equivalent. The author says he had original and converted carts on the bench. | Forum, expert |
| S6 | [arcade-projects: "Pulstar and Ironclad conversions help"](https://www.arcade-projects.com/threads/pulstar-and-ironclad-conversions-help.17078/) (2021) | EPROM lists, S1/M1 pinout rules, splitting, programming and verify advice, Ironclad result | Forum, hands-on |
| S7 | [Mike McBike: Blazing Star conversion](http://www.wolfgangrobel.de/mvs/blazingstar.htm) | 27C322 for C ROMs; V ROMs need 4 × 27C160 | Hands-on write-up |
| S8 | [Mike McBike: Neo Geo cartridges](http://www.wolfgangrobel.de/mvs/neogeogames.htm) | Per-game PROG/CHA pair (transcribed for [BOARDS.md](BOARDS.md)) | Reference table |
| S9 | [Retrostuff: Top Hunter MVS cartridge repair](https://retrostuff.org/2021/01/10/top-hunter-mvs-cartridge-repair/) | TC538200 → M27C800 on PROGTOP; UniBIOS CRC check | Hands-on repair |
| S10 | [arcade-projects: MVS cartridge repair walkthrough](https://www.arcade-projects.com/posts/464016) | 1 MB C8 → 27C800; warning that M1/S1 use different pinouts | Forum, hands-on |
| S11 | [arcade-projects: PROG-GSC V ROMs](https://www.arcade-projects.com/goto/post?id=378792) | /BYTE hard-wired low on the PROG-GSC schematic | Forum |
| S12 | [arcade-projects: Blazing Star conversion thread, page 2](https://www.arcade-projects.com/threads/neogeo-conversions-for-fun-and-no-profit-blazing-star-complete-documented.30476/page-2) | 32 Mbit V ROMs and 27C322; custom V-ROM modules | Forum |
| S13 | [abzman2k: Synthesizing a Neo Geo game from scratch](https://abzman2k.wordpress.com/2021/04/13/synthesizing-a-neo-geo-game-from-scratch-ish/) | TC5332204 is byte-mode only; C ROMs as 27C322; V1 split across two chips | Blog, hands-on |
| S14 | [arcade-projects: Blazing Star on PROGTOP](https://www.arcade-projects.com/threads/neogeo-blazing-star-conversion-on-progtop-board-issue-almost-there-solved.18009/) | PROGTOP P-ROM notes (partly read) | Forum |
| S15 | [r/neogeo: "Blazing star mvs no sound"](https://lr.in.psf.lt/r/neogeo/comments/1b9025l/blazing_star_mvs_no_sound) (Mar 2024, mirror) | M1 → 27C010 (AMD/ST/TI, ≥150 ns) | Forum advice |
| S16 | [Keir Fraser: EPROM Adapter](https://github.com/keirf/pcb-projects/wiki/EPROM-Adapter) | 27C400/800/160/322 pins and organisation; pinout differs from 27C4096 | Project docs |
| S17 | [DigicoolThings: 27C400/800/160/322 adapter](https://digicoolthings.com/?p=97) | This EPROM family uses mask-ROM-compatible pinouts | Vendor page |
| S18 | [mafe72: 27C160 TL866 adapter](https://github.com/mafe72/27c160-tl866-adapter) | TL866 workflow (512 KB chunks, device choice, pulse delay) | Project docs |
| S19 | [justinpaulin.com: 27C301 → 27C010 adapter](https://justinpaulin.com/?p=304) | 27C301 is non-JEDEC with two swapped pins | Hands-on (Game Boy context) |
| S20 | [arcade-projects post 80642](https://www.arcade-projects.com/goto/post?id=80642) | ST "27C1000" exists in JEDEC and non-JEDEC forms | Forum (non-Neo Geo board) |
| S21 | [Dataman forum: NEC D23C1000 mask ROM](https://forum.dataman.com/viewtopic.php?p=2725) | 1 Mbit mask ROM pinout matches 27C301 | Forum |
| S22 | [NESdev forum: mask ROM pinout reference](https://nesdev.nes.science/f9/t16494.xhtml) | Example of a non-JEDEC 4 Mbit ×8 mask ROM (HN62304) | Forum (non-Neo Geo) |
| S23 | [Elnec: Toshiba part-number decoder](https://www.elnec.com//device/Toshiba/TC54H1001A+%5BSOP32%5D) | TC54/57 = EPROM; density digits | Vendor reference |
| S24 | [arcade-projects: "Neo Geo Bios Chip replacement"](https://www.arcade-projects.com/goto/post?id=85368) | TC531024P-15 → 27C1024 | Forum |
| S25 | [arcade-projects: "Neo-geo MVS Universe Bios problem"](https://www.arcade-projects.com/goto/post?id=175339) | 27C240/27C4096 extra pins | Forum |
| S26 | [Arcade Xpress: NeoBiosMasta Deck](https://www.arcadexpress.com/en/superguns-mvs-snk/1214-neobiosmasta-deck-for-unibios-40-chip-snk-neo-geo.html) | MV1B/MV1C adapter for 27C1024 | Vendor page |
| S27 | [arcade-projects: MV1C Unibios / NeoBiosMasta install](https://www.arcade-projects.com/threads/mv1c-unibios-neobiosmasta-install-troubleshooting.32707) | MV1C BIOS is surface-mounted | Forum |
| S28 | [jwestfall69/neogeo-diag-mvs-cha](https://github.com/jwestfall69/neogeo-diag-mvs-cha) | Diag CHA board uses 27C1001/27C010, ≥150 ns; warning on "new" EPROM sellers | Project docs |
| S29 | [OSH Park: 29F160 → 27C160/322 adapter](https://oshpark.com/shared_projects/hnFhCQrA) | Flash adapter for V-ROM use; author says untested | Project page |
| S30 | [NESdev forum: 27C2001 = 27C020 naming](https://nesdev.nes.science/f10/t1201.xhtml) | 27C1001=27C010, 27C2001=27C020, 27C4001=27C040 | Forum |
| S31 | [arcade-projects post 252184](https://www.arcade-projects.com/goto/post?id=252184) | Diag BIOS burned to a 27C1024 to replace the BIOS | Forum |
| S32 | ST M27C160 datasheet, rev. -04, January 2002 (user-supplied PDF) | DIP42 pinout, byte/word modes, timing, programming, packages, OTP vs UV | Manufacturer datasheet |
| S33 | Macronix MX29F1615 datasheet, PRELIMINARY rev. 1.2, 21 November 2002 (user-supplied PDF) | DIP42 pinout, read behaviour, voltage limits, command-based programming | Manufacturer datasheet (preliminary) |
| S34 | ST M27C512 datasheet, rev. 2.0, November 2004 (user-supplied PDF) | 28-pin 64K × 8 pinout | Manufacturer datasheet |
| S35 | Atmel AT27C010/L datasheet (user-supplied PDF) | JEDEC 32-pin 27C010 pinout, OTP | Manufacturer datasheet |
| S36 | Macronix MX27C4000 datasheet, rev. 3.8, 26 August 2003 (user-supplied PDF) | 32-pin 512K × 8 pinout, OTP | Manufacturer datasheet |
| S37 | [JNX: Neo-Geo MVS Cart Board Codes](http://www.jamma-nation-x.com/jammax/mvsboardcodes.html) | Per-game PROG/CHA pair, 149 rows (transcribed for [BOARDS.md](BOARDS.md)) | Community reference table |

Further reading (pointers only, not used as evidence): [MVS Scans](http://mvs.gotwalls.com/index.php/Main_Page) for PCB photos and the [NeoGeo Dev Wiki cartridge index](https://wiki.neogeodev.org/index.php/Cartridges).

---

## Appendix: how the MAME data was extracted

- **Input:** `src/mame/snk/neogeo.cpp` from MAME's master branch, retrieved during this research session. 795,545 bytes, SHA-256 `77324df687d4cf49c6874a9f83d6253a69f7db59404b878a51685850207afc97`, containing 284 `ROM_START` blocks (283 with parseable chip entries).
- **Method:** for each set, read every `ROM_LOAD*`, `NEO_SFIX_*` and `NEO_BIOS_AUDIO_*` entry, assign a function (P, V, C, S1, M1) from the ROM region, merge `ROM_CONTINUE` lines into the preceding chip, and collect the `/* … */` comments that name the part. Parts starting with `27C`/`M27C`/`AM27C`/`D27C`/`HN27C`/`TC54`/`TC57`/`W29`/`MX29`/`LH28`/`M59PW` are treated as programmable or flash; everything else as mask ROM.
- **Limits:** sizes are the dumped image sizes, which normally equal chip capacity but not always (see [section 10](#11-data-quality-and-open-questions)). Clones, bootlegs and prototypes are counted as sets.

<details>
<summary>Script (Python 3.8+, no dependencies)</summary>

```python
#!/usr/bin/env python3
"""Extract ROM chip part numbers from the comments in MAME's Neo Geo driver.

Usage: python3 mame_chips.py neogeo.cpp
Reports, per ROM function and capacity, how many MAME sets list each part.
"""
import re, sys, collections

SRC = sys.argv[1] if len(sys.argv) > 1 else "neogeo.cpp"
KB = 1024
MACROS = {  # macros that imply role + size
    "NEO_SFIX_64K": ("S1", 64*KB),  "NEO_SFIX_128K": ("S1", 128*KB),
    "NEO_BIOS_AUDIO_64K": ("M1", 64*KB),  "NEO_BIOS_AUDIO_128K": ("M1", 128*KB),
    "NEO_BIOS_AUDIO_256K": ("M1", 256*KB), "NEO_BIOS_AUDIO_512K": ("M1", 512*KB),
    "NEO_BIOS_AUDIO_ENCRYPTED_128K": ("M1", 128*KB),
    "NEO_BIOS_AUDIO_ENCRYPTED_256K": ("M1", 256*KB),
    "NEO_BIOS_AUDIO_ENCRYPTED_512K": ("M1", 512*KB),
}
def role_of(region):
    r = region.lower()
    if "maincpu" in r: return "P"
    if "audiocpu" in r or "audiocrypt" in r: return "M1"
    if "fixed" in r and "bios" not in r: return "S1"
    if "adpcm" in r: return "V"
    if "sprites" in r: return "C"
def to_int(s): return int(s, 16) if s.startswith("0x") else int(s)

roms = collections.defaultdict(list)      # set -> [[role, size, [comments]]]
cur = region = None
for line in open(SRC, encoding="utf-8", errors="replace"):
    if (m := re.match(r"\s*ROM_START\(\s*(\w+)\s*\)", line)):
        cur, region = m.group(1), None; continue
    if re.match(r"\s*ROM_END", line): cur = None; continue
    if cur is None: continue
    if (m := re.match(r'\s*ROM_REGION(?:16_BE)?\(\s*\S+\s*,\s*"([^"]+)"', line)):
        region = m.group(1); continue
    notes = [n.strip() for n in re.findall(r"/\*\s*(.*?)\s*\*/", line)
             if not n.lower().startswith("plane")]
    macro = re.match(r"\s*(NEO_\w+)\(", line)
    if macro and macro.group(1) in MACROS:
        role, size = MACROS[macro.group(1)]
        roms[cur].append([role, size, notes]); continue
    if (m := re.match(r"\s*(ROM_LOAD\w*|ROM_CONTINUE)\(\s*(?:\"[^\"]+\"\s*,\s*)?"
                      r"(0x[0-9a-fA-F]+|\d+)\s*,\s*(0x[0-9a-fA-F]+|\d+)", line)) and region:
        role = role_of(region)
        if not role: continue
        if m.group(1) == "ROM_CONTINUE" and roms[cur]:
            roms[cur][-1][1] += to_int(m.group(3))     # same chip, second half
        else:
            roms[cur].append([role, to_int(m.group(3)), notes])

PROGRAMMABLE = re.compile(r"^(M?27C|AM27C|D27C|HN27C|TC57|TC54|W29|MX29|LH28|M59PW)", re.I)
def clean(n): return re.sub(r"^mask rom\s*", "", re.sub(r"\s+", " ", n), flags=re.I)

table = collections.defaultdict(set)      # (role,size,kind,part) -> sets
for name, entries in roms.items():
    for role, size, notes in entries:
        for n in map(clean, notes):
            if n.lower() in ("unused",) or n.lower().startswith("stored in"): continue
            kind = "programmable" if PROGRAMMABLE.match(n) else "mask"
            table[(role, size, kind, n)].add(name)

for kind in ("mask", "programmable"):
    print(f"\n===== {kind.upper()} =====")
    for role in ("P", "V", "C", "S1", "M1"):
        print(f"--- {role}")
        by_size = collections.defaultdict(list)
        for (r, size, k, part), s in table.items():
            if r == role and k == kind: by_size[size].append((part, len(s)))
        for size in sorted(by_size):
            parts = ", ".join(f"{p} ({n})" for p, n in sorted(by_size[size], key=lambda x: (-x[1], x[0])))
            print(f"  {size//KB:>5} KB : {parts}")
print("\nSets parsed:", len(roms))
```

</details>
