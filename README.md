# Teardown of some Chinese Neo Geo MVS bootlegs / repros

## Disclaimer
- I do not own these bootleg cartridges, because piracy is bad, very very bad. Don't do this.
- Everything written here is for documentation only. You do whatever you want with it, not my concern. I did this because this is precisely the kind of information I was searching on internet without finding it.
- Any reuse of original content present here must be credited anyway (in other word, cite the source / author). It's not because it's about piracy that you can reuse content without credits.

## Summary
- Tests were made with sound going out from a [SmallCab deluxe V2 supergun](https://www.smallcab.net/supergun-deluxe-p-2166.html) equipped with a [dummy load](https://github.com/Raphael-Boichot/Neogeo-MVS-one-slot-stereo-mod#do-you-want-to-try-a-non-destructive-and-easy-mod-before-). This is clearly not the absolute way to experience the amazing sound quality of a Neo-Geo MVS but the author has distinguished between sound glitches caused by his specific setup and those caused by the repro cartridges being tested, by comparing them with original games.
- Repros shown here rely on rerouting (not exact copies) of genuine PCBs ([PROGBK1](https://wiki.neogeodev.org/index.php?title=PROGBK1), [PROGBK2](https://wiki.neogeodev.org/index.php?title=PROGBK2), [CHA512Y](https://wiki.neogeodev.org/index.php?title=CHA512Y), [PROG-EP](https://wiki.neogeodev.org/index.php/PROG-EP), [CHA32G](https://wiki.neogeodev.org/index.php/CHA42G), for example). They looks like official MVS releases from 2003 but are not (no matching with existing genuine cartridges). This is the only part always new in these cartridges. Quality is always super good (gold plating, slikscreen, solder masks, irreproachables).
- Shells can be new or refurbished. The new shells are harder to put together because the tolerances are a bit off with screws but they are still heavy and sturdy.
- Not a single chip on these board is brand new. 100% are recycled and present signs of prior use / storage without care like left stickers, traces of old stickers, scratches, unreadable marking due to wear or sanding, etc. Most of them are obsolete and probably just e-waste but also frequently 5V / 5V tolerant !
- The 161-in-1 in "version 2" / black shell shown here looks [exactly like the 161 in 1 in "version 3"](https://wiki.neogeodev.org/index.php?title=161-in-1_Series_1), same design. My guess is that "version 3" / blue shell is now (2026) just a Chinese scam to pocket the added value of a potential ["all-in-one" or Vortex convert](https://github.com/xvortex/VTXCart) made by the buyer without taking any risk for the vendor who just sells stocks of a very particular "version 2", reshelled / restamped. Some are even stamped "all-in-one compatible" to confirm the scam. There is no small profit. The chronological evolutions of the 161-in-1 revisions follows exactly the [chronological discussions](https://www.neogeo-system.com/t7269-tuto-modification-mvs-cartouche-161in1-v2) on western forums about how to "improve it" (including the snake oil). [Reported glitches](https://wiki.neogeodev.org/index.php?title=161-in-1_Series_1) are ALWAYS the same. The said multicart is more or less [reverse-engineered](https://www.arcade-projects.com/threads/reverse-engineering-161-in-1-cartridge-to-change-rom-games.15069/) now.
- There is a mixture of 5V, 3.3V (5V tolerant) and 3.3V chips on these cartridges. Apart from the fact that this is half-ass job (there is plenty of room on the PCB to add serious bus transcievers for outgoing signals), the long term effect of this level mismatch is just inexistant for the MVS motherboard as even in the worst case scenario, 3.3V signals sent back to the MVS motherboard, it stays in the [tolerance margin of the 5V TTL chips of the Neo-Geo](https://retrosix.wiki/wiki/digital-logic-levels). For the cartridges in the other hand, Each time a pure 3.3V (not 5V tolerant) chip is used, there is a 3.3V voltage regulator somewhere close.
- Most games passing the Unibios 4.0 checksum with success work without major glitches (or glitches are fixable). For the other ones, depends... There is probably a mix of botched hacks and issue with delay tolerances of the flash chips used. My guess is that some particular way of programming the Neo-Geo sound chip (most of the glitches are sound artifacts) always induces bugs in the repros whatever the bootleg PCB configuration. Sound glitches go from barely noticeable to frankly irritating when you're used to play the genuine games.
- The value for money remains excellent for playing and spending quality time with friends. These are clearly not collectible items but they perfectly do the entertainment job for the price you can touch them in 2026 (around 60€ shippment included outside China, less inside).
- As far as I understand / see on internet, all cartridges from different suppliers / vendors have the same glitches for a given game. They probably all originates from common ancestor bootlegs never updated because nobody cares of minor glitches in China. Discussing technical details with the sellers is anyway useless. Whether they act stupid or are stupid, they won't pass on any worthwhile information. A possible explanation is that they now apply old recipes without having any idea of why or how there bootlegs work. Whatever the reason, you're on you own to fix / modify these cartridges.

## Forewords: Neo Geo game structure in chips / ROM in a nutshell

| ROM chip | Hardware Target | Functionality |
| :--- | :--- | :--- |
| **P (Program)** | 68000 CPU | Main logic, game states, AI, and collision detection. |
| **C (Character)** | Video Processor | Graphics data; split into interleaved banks for the sprite engine. |
| **S (System)** | Fix Layer | The "Fix" layer (static HUD, text, menus) sitting on top of gameplay. |
| **M (Music)** | Z80 CPU | The audio sub-processor that handles music commands. |
| **V (Voice)** | ADPCM Chip | Compressed audio samples for sound effects and speech. |

## Electrical tests, or will repros fry your precious Neo Geo MVS ?

| Neo Geo Game Name | Conditions of test | Cumulated current | Test time | Raw current @5V | Cartridge only @5V |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **MV1FZS BIOS (Unibios 4.0)** | Crosshatch, no input | 2875 mA.h | 93 min | 1855 mA | 0 mA |
| **Pop'n Bounce (UVPROMs on original PCB)** | Playthrough | 791 mA.h | 23 min | 2063 mA | 209 mA |
| **World Heroes 2 (original, mask ROMs)** | Attract mode | 1757 mA.h | 50 min | 2108 mA | 254 mA |
| **King of the Monsters 2 (repro shown here)** | Attract mode | 1418 mA.h | 40 min | 2127 mA | 272 mA |
| **Sengoku 2 (repro shown here)** | Attract mode | 2503 mA.h | 70 min | 2145 mA | 291 mA |
| **Magician Lord (repro shown here)** | Playthrough | 1523 mA.h | 40 min | 2285 mA | 430 mA |
| **Xenocrisis (repro shown here)** | Playthrough | 2790 mA.h | 71 min | 2358 mA | 503 mA |
| **King of Fighters 98 (original, mask ROMs)** | Playthrough | 1674 mA.h | 40 min | 2511 mA | 656 mA |
| **Metal Slug 5 (repro shown here)** | Playthrough | 1738 mA.h | 40 min | 2607 mA | 752 mA |
| **161-in-1 V2 (repro shown here)** | PICKnMIX rolling mode | 3083 mA.h | 60 min | 3083 mA | 1228 mA |

Measurements of the 5V line were conducted using a modified USB power meter. Due to highly unstable instantaneous current draw, values were averaged over several dozen minutes using cumulative current. 

While standard cartridges and reproductions exhibit similar power profiles — following a 'the bigger the game, the more power-hungry' trend — the 161-in-1 multicart is a significant outlier, requiring a stable 5V supply of at least 3A. Many consolized MVS units may fail to meet this threshold.

# Combo PROGBK2 / CHA512Y

## Xenocrisis repro
- Test setup: MV1FZS recapped from fresh, beefy enough arcade power supply (5.00V during all tests), good quality sound amplifier after a High/Low impedance adapter.
- Supplier: [Kuqi - Vintage Arcade Store Store](https://www.aliexpress.com/store/1103076414), May 2026.
- Unibios 4.0 verdict: unknwon game (of course)
- Glitches: none after hours of playing.  Game itself is a good Smash TV clone for Genesis. Cartridge owner was expecting more "Neo Geo signature effects" like massive shrinking sprites. And Cthulhu as a random boss in a game that has nothing Lovecraftian, such a lack of taste. Shit, they were charging 350 bucks for it!
- The cartridge uses 3 chips not reported as 5V tolerant but having their own 3.3V voltage regulator.

**Sticker**
![](/Pictures/Xenocrisis_Sticker.JPG)

**PRG board top**
![](/Pictures/Xenocrisis_PRG_top.JPG)

PCM2 is an ALTERA MAX EPM3256ATC144-10N ([ALTERA MAX 3000A family](/Datasheets/ALTERA_MAX_3000A.pdf)). P1 is a [Macronix 2 MBytes Flash memory](/Datasheets/Macronix%20MX29F1615PC-10.pdf) and V2 is a [ST 16 MBytes Flash memory](/Datasheets/ST%20M59PW1282.PDF). KM23C3200 refers to a 4 MBytes maskROM. MX23C3210 refers to another [Macronix 4 MBytes maskROM](/Macronix%20MX23C3210.pdf).

**PRG board bottom**
![](/Pictures/Xenocrisis_PRG_bottom.JPG)

**CHA board top**
![](/Pictures/Xenocrisis_CHA_top.JPG)

NEO 273 is an ALTERA MAX EPM7128STC100-15 ([ALTERA MAX 7000 family](/Datasheets/ALTERA_MAX_7000.pdf)). C1 and C2 are [Macronix 8 MBytes Flash memory](/Datasheets/Macronix%20MX26L6420.PDF). M1 and S1 are [Winbond 128kBytes Flash memory](/Datasheets/Winbond%20W27C010.PDF). KM23C3200 refers to a 4 MBytes maskROM.

**CHA board bottom**
![](/Pictures/Xenocrisis_CHA_bottom.JPG)

## Metal Slug 5 repro
- Test setup: MV1FZS recapped from fresh, beefy enough arcade power supply (5.00V during all tests), good quality sound amplifier after a High/Low impedance adapter.
- Supplier: [Guangzhou San Star Online Shop](https://www.aliexpress.com/store/202692), March 2026.
- Unibios 4.0 verdict: Checksum NG 
- Glitches: No graphical glitches - sound glitches like scratchy sound during some explosions, some oversaturated sound effects (similar to Metal Slug 4 on the 161 in 1). Adding 47 pF ceramic capacitors to SDRMPX, SDPMPX, SDROE and SDPOE does not change anything.
- This board was clearly modified at some point (scratches, traces of desoldering)

**Sticker**
![](/Pictures/Metal_Slug5_Sticker.JPG)

**PRG board top**
![](/Pictures/Metal_Slug5_PRG_top.JPG)

PCM2 is an ALTERA MAX EPM3256ATC144-10N ([ALTERA MAX 3000A family](/Datasheets/ALTERA_MAX_3000A.pdf)). P1 is a [Macronix 1 MBytes Flash memory](/Datasheets/Macronix%20MX27C8100.PDF). V2 is a [ST 16 MBytes Flash memory](/Datasheets/ST%20M59PW1282.PDF). P2 is a [ST 4 MBytes Flash memory](/Datasheets/ST%20M27C322.PDF). KM23C3200 refers to a 4 MBytes maskROM. MX23C3210 refers to another [Macronix 4 MBytes maskROM](/Macronix%20MX23C3210.pdf).

**PRG board bottom**
![](/Pictures/Metal_Slug5_PRG_bottom.JPG)

**CHA board top**
![](/Pictures/Metal_Slug5_CHA_top.JPG)

NEO 273 is an ALTERA MAX EPM7128STC100-7 ([ALTERA MAX 7000 family](/Datasheets/ALTERA_MAX_7000.pdf)). C1, C2, C3 and C4 are beefy [ST 16 MBytes Flash memory](/Datasheets/ST%20M59PW1282.PDF). M1 and S1 are [Winbond 128 kBytes Flash memory](/Datasheets/Winbond%20W27C010.PDF). KM23C3200 refers to a 4 MBytes maskROM. 

**CHA board bottom**
![](/Pictures/Metal_Slug5_CHA_bottom.JPG)

# Combo PROGBK1 / CHA512Y

## King of the Monsters 2 repro
- Test setup: MV1FZS recapped from fresh, beefy enough arcade power supply (5.00V during all tests), good quality sound amplifier after a High/Low impedance adapter.
- Supplier: [Vintage Video Game Family Accessories Store](https://www.aliexpress.com/store/1102921377), April 2026.
- Unibios 4.0 verdict: Checksum OK
- Glitches: none after hours of playing

**Sticker**
![](/Pictures/KOTM2_Sticker.JPG)

**PRG board top**
![](/Pictures/KOTM2_PRG_top.JPG)

PCM is a LATTICE LC4128ZE ([ispMACH 4000ZE Family](/Datasheets/Lattice_4000ZE_family.pdf)). P1 is a [SKY(?) 2 MBytes Flash memory](/Datasheets/Macronix%20MX29F1615PC-10.pdf). V1 is a [Macronix 4 Mbytes EPROM](/Datasheets/Macronix%20MX29LV320E.pdf). KM23C3200 refers to a 4 MBytes maskROM. MX23C3210 refers to another [Macronix 4 MBytes maskROM](/Macronix%20MX23C3210.pdf).

**PRG board bottom**
![](/Pictures/KOTM2_PRG_bottom.JPG)

**CHA board top**
![](/Pictures/KOTM2_CHA_top.JPG)

NEO 273 is an ALTERA MAX EPM7128STC100-7 ([ALTERA MAX 7000 family](/Datasheets/ALTERA_MAX_7000.pdf)). C5 and C6 are [ST 4 MBytes OTP (one time programmable) memory chips](/Datasheets/ST%20M27C322.PDF). M1 and S1 are [Winbond 128 kBytes Flash memory](/Datasheets/Winbond%20W27C010.PDF).

**CHA board bottom**
![](/Pictures/KOTM2_CHA_bottom.JPG)

## Sengoku 2 repro
- Test setup: MV1FZS recapped from fresh, beefy enough arcade power supply (5.00V during all tests), good quality sound amplifier after a High/Low impedance adapter.
- Supplier: [Kuqi - Vintage Arcade Store Store](https://www.aliexpress.com/store/1103076414), January 2026.
- Unibios 4.0 verdict: Checksum OK
- Glitches: none after hours of playing

**Sticker**
![](/Pictures/Sengoku2_Sticker.JPG)

**PRG board top**
![](/Pictures/Sengoku2_PRG_top.JPG)

PCM is a LATTICE LC4128ZE ([ispMACH 4000ZE Family](/Datasheets/Lattice_4000ZE_family.pdf)). P1 is a [Macronix 2 MBytes Flash memory](/Datasheets/Macronix%20MX29F1615PC-10.pdf). V1 is readable with grazing light, it's a [Macronix 4 MBytes Flash memory](/Datasheets/Macronix%20MX29LV320E.pdf). KM23C3200 refers to a 4 MBytes maskROM. MX23C3210 refers to another [Macronix 4 MBytes maskROM](/Macronix%20MX23C3210.pdf).

**PRG board bottom**
![](/Pictures/Sengoku2_PRG_bottom.JPG)

**CHA board top**
![](/Pictures/Sengoku2_CHA_top.JPG)

NEO 273 is an ALTERA MAX EPM7128STC100-7 ([ALTERA MAX 7000 family](/Datasheets/ALTERA_MAX_7000.pdf)). C1 and C2 are [Macronix 8 MBytes Flash memory](/Datasheets/Macronix%20MX26L6420.PDF). M1 and S1 are [Winbond 128 kBytes Flash memory](/Datasheets/Winbond%20W27C010.PDF). KM23C3200 refers to a 4 MBytes maskROM. 

**CHA board bottom**
![](/Pictures/Sengoku2_CHA_bottom.JPG)

# Combo PROG-EP / CHA32G

## Magician Lord repro
- Test setup: MV1FZS recapped from fresh, beefy enough arcade power supply (5.00V during all tests), good quality sound amplifier after a High/Low impedance adapter.
- Supplier: [Kuqi - Vintage Arcade Store Store](https://www.aliexpress.com/store/1103076414), May 2026.
- Unibios 4.0 verdict: Checksum OK 
- Glitches: No graphical glitches - sound glitches like saturated sound levels that jumpscares you. **These sound artifacts are easily fixable** (see next), so get ready to fire up the soldering iron!

**Sticker**
![](/Pictures/Magician_Lord_sticker.JPG)

**PRG board top**
![](/Pictures/Magician_Lord_PRG_top.JPG)

PCM is an ALTERA MAX EPM7128STC100-6 ([ALTERA MAX 7000 family](/Datasheets/ALTERA_MAX_7000.pdf)). The PRG board uses [Macronix 2 MBytes Flash memory](/Datasheets/Macronix%20MX29F1615PC-10.pdf) for V1, V2 and P1. There is enough room on P1 to [cram the two sets](https://www.youtube.com/watch?v=kXWZlWuGljk) of program ROMS of this game with a switch. The double slots for P1 and V1 / V2 are probably meant to populate the board with whatever SOP-44, 5V tolerant 2MBytes or more flash memory chips (I do not find any possible reference though). Marking [below P1](/Magician_Lord_hacks/Hacking_Magician_Lord_01.jpg) is TC5316200, which is the [mask ROM counterpart](/Datasheets/Toshiba%20TC5316200.pdf).

**PRG board bottom**
![](/Pictures/Magician_Lord_PRG_bottom.JPG)

**CHA board top**
![](/Pictures/Magician_Lord_CHA_top.JPG)

CPLD is an ALTERA MAX (no marking on PCB) EPM7128STC100-6 ([ALTERA MAX 7000 family](/Datasheets/ALTERA_MAX_7000.pdf)). The CHA board uses [Macronix 2 MBytes Flash memory](/Datasheets/Macronix%20MX29F1615PC-10.pdf) for C1 and C2, and [Winbond 128 kBytes Flash memory](/Datasheets/Winbond%20W27C010.PDF) for M1 and S1. Marking [below S1](/Magician_Lord_hacks/Hacking_Magician_Lord_01.jpg) is TC531001, which is the [mask ROM counterpart](/Datasheets/Toshiba%20TC531001.pdf).

**CHA board bottom**
![](/Pictures/Magician_Lord_CHA_bottom.JPG)

**Fixing sound glitches of Magician lord**
![](/Pictures/Magician_Lord_sound_fixing.png)

I simply follow the guide proposed [here](https://www.neogeo-system.com/t6458-tuto-corriger-problemes-de-pcm-bruitages-satures-sur-conversion-mvs-mvs-ou-autres) which is derived from older guides to fix the 161-in-1 sound. Beware, the mod shown in the link has a pinout error so follow the [right pinout from neogeodev](https://wiki.neogeodev.org/index.php/MVS_cartridge_pinout) or the schematic here. I used  microscopic 0603 CMD ceramic capacitors because I like suffering. **This modification completely fixes any sound glitch with this bootleg!**

**Modifying the cartridge to boot with set 1 or set 2 of the game**
![](/Magician_Lord_hacks/AES_MVS_hack.png)

Follow the [guide](/Magician_Lord_hacks/README.md). These cartridges are super easy to modify !

# Custom design

## 161-in-1 "Series 2" bootleg
- Test setup: MV1FZS recapped from fresh, beefy enough arcade power supply (5.00V during all tests), good quality sound amplifier after a High/Low impedance adapter.
- Supplier: [Random Taobao supplier](https://www.taobao.com/) from within mainland China, December 2025.
- Unibios 4.0 verdict: Checksum NG for all games, supports the Pick'n Mix
- Bugs: rare graphical glitches all documented - some sound glitches (also well documented). Overall, **always the same glitches whatever the alledged PCB revisions.** The cartridge tends to mess up the calendar and the book keeping in test mode (but not always), but it goes back to normal with a genuine cartridge. Very irritating with the factory MVS bios where it can trigger calendar errors and oblige you to play with the dip switches to erase backup RAM. So the advice: **always use the 161-in-1 WITH the Unibios**.
- [list of games](/Datasheets/MVS_161_in_1_GL.pdf) (always the same, too many KOFs and crap hacks, not enough early games).

The owner of the cartridge (not me) has tried many "improvements" found on the internet to fix the sound issues (see next sections) without any success, so his conclusion: **"any fix to sound glitches of the 161-in-1 proposed on the internet is just bullshit or yet implemented in late revisions"**.

**Sticker**
![](/Pictures/161in1v2_sticker.JPG)

**PRG board top**
![](/Pictures/161in1v2_PRG_top.JPG)

CP1 and PCM2 are ([ALTERA MAX 3000](/Datasheets/ALTERA_MAX_3000A.pdf)) with marking EPM3256ATC144-10N. PCM2 is sanded for unknown reason but the chip is the same as CP1 after some more investigation with grazing light.

The resistor ladders A103J, 9 pins (RP1, RP2, RP3) and the 470 µF electrolytic capacitors (instead of 100 µF from factory) were added by the cartridge owner post factory as (unsucessful) [attempt to fix sound glitches](https://www.neogeo-system.com/t7269-tuto-modification-mvs-cartouche-161in1-v2). This board also present signs of modifications to add or modify ceramic capacitors on [SDRMPX, SDPMPX, SDROE, SDPOE](https://www.neo-geo.com/forums/index.php?threads/pcm-sound-stability-fixes-multicarts-120-in-1-138-in-1-161-in-1-and-others.242857/) (22 to 47 pF), without making any difference.

U2 is a 8-bit [STC11F08XE](/Datasheets/STC11-10xx_Series_MCU.pdf) microcontroller. Function is unclear to me in the presence of 3 beefy ALTERA CPLDs.

Each board has its own voltage regulator (AMS1117) capable to produce 1A each at 3.3V, much enough to power the whole set of chips. The cartridge itself consumes about 1200 mA (at 5V), versus about 500 mA (at 5V, on average) for a regular MVS cartridge. Nothing that’s going to fry your MVS slot as this noticeable increase of current is sucked directly on the 5V rail. To my knowledge, arcade power supplies are perfectly able to handles this.

**PRG board bottom**
![](/Pictures/161in1v2_PRG_bottom.JPG)

The F0095H0 are humongus [1 Gigabyte NOR Flash Memory](https://www.arcade-projects.com/threads/reverse-engineering-161-in-1-cartridge-to-change-rom-games.15069/page-4) chips with unusual, non-standard BGA/LGA package, so the small orange sub-board/daughterboard which is meant to adapt those custom pins to standard, edge-soldered pins. 4 chips = 4 Gigabytes but much room is lost due to ROM alignement so the uncompressed fullset would not fit as it in any case.

The yellow sticker indicates a chip refurbished from a pachinslot machine based on [Sabu to Ichi Torimonohikae](https://en.wikipedia.org/wiki/Sabu_to_Ichi_Torimono_Hikae) theme, containing "effects/cutscene data 2", from [NewGin Company](https://en.wikipedia.org/wiki/NewGin).

Some ceramic decoupling caps were missing, without any pattern, then populated by 100 nF by the owner who is educated enough to make the good choice.

**CHA board top**
![](/Pictures/161in1v2_CHA_top.JPG)

The white sticker on the F0095H0 indicates a chip refurbished from a pachinslot based on [Seibu Keisatsu](https://en.wikipedia.org/wiki/Seibu_Keisatsu) theme, containing "effects/cutscene data 2", from [NewGin Company](https://en.wikipedia.org/wiki/NewGin). The show was popular in 2004, so the chip is probably about 20 years old.

U2 is another ([ALTERA MAX 3000](/Datasheets/ALTERA_MAX_3000A.pdf)) with marking EPM3256ATC144-10N. S1 is a beefy [Macronix 32 MBytes Flash memory](/Datasheets/Macronix%20MX29GL256F.pdf). M1 is a Micron Technology 64 MBytes Parallel NOR Flash memory chip, similar to a [Macronix MX29GLXXX series](/Datasheets/Migrate%20M29EW%20to%20Macronix%20MX29GL_F.pdf). Basically manufacturer just took the e-waste available on shelves.

**CHA board bottom**
![](/Pictures/161in1v2_CHA_bottom.JPG)

Some ceramic decoupling caps were also missing for no reason, populated by 100 nF by the owner just in case. Does not change anything.

Overall, this cartridge was more than OK for the $60 it was sold before the prices went crazy with the VERTEX mod. New customers: fly away any price up to 80€, try TaoBao directly if you have local contacts, second hand units or wait for the next version, if any. Fun fact: this cartridge fell from waist height onto a tiled floor and still works like a charm. It’s built to last!

# Teardown of some converts / repairs

## Puzzle de Pon convert
- Test setup: MV1FZS recapped from fresh, beefy enough arcade power supply (5.00V during all tests), good quality sound amplifier after a High/Low impedance adapter.
- Supplier: Vinted (Europe), september 2026.
- Unibios 4.0 verdict: Checksum OK
- Glitches: some slight graphical glitches
- Original cartridge: World Heroes for CHA, unknown for PROG

**Sticker**
![](/Pictures/Puzzle_de_Pon_Sticker.JPG)

**PRG board top**
![](/Pictures/Puzzle_de_Pon_PRG_top.JPG)

PCM is a LATTICE LC4128ZE ([ispMACH 4000ZE Family](/Datasheets/Lattice_4000ZE_family.pdf)). P1 is a [SKY(?) 2 MBytes Flash memory](/Datasheets/Macronix%20MX29F1615PC-10.pdf). V1 is a [Macronix 4 Mbytes EPROM](/Datasheets/Macronix%20MX29LV320E.pdf). KM23C3200 refers to a 4 MBytes maskROM. MX23C3210 refers to another [Macronix 4 MBytes maskROM](/Macronix%20MX23C3210.pdf).

**PRG board bottom**
![](/Pictures/Puzzle_de_Pon_PRG_bottom.JPG)

**CHA board top**
![](/Pictures/Puzzle_de_Pon_CHA_top.JPG)

NEO 273 is an ALTERA MAX EPM7128STC100-7 ([ALTERA MAX 7000 family](/Datasheets/ALTERA_MAX_7000.pdf)). C5 and C6 are [ST 4 MBytes OTP (one time programmable) memory chips](/Datasheets/ST%20M27C322.PDF). M1 and S1 are [Winbond 128 kBytes Flash memory](/Datasheets/Winbond%20W27C010.PDF).

**CHA board bottom**
![](/Pictures/Puzzle_de_Pon_CHA_bottom.JPG)

