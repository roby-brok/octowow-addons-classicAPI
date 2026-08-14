# My OctoWoW Addon Setup — ClassicAPI Edition

The addons and client mods I run on [OctoWoW](https://octowow.st) (WoW 1.12.1 client),
**rebuilt around [ClassicAPI](https://github.com/brues-code/ClassicAPI)**.

This repository is **a list, not a mirror.** No addon code is hosted here — every entry links to the
author's own repository, which is where you should download it from. All credit belongs to the
people who wrote these; I just use them and occasionally fix something.

Maintained by **Roby_Brok**. *Last synced against the actual install: **2026-08-14**.*

> ### Status
>
> This setup depends on **[brues-code](https://github.com/brues-code)'s** work — ClassicAPI itself,
> plus his ClassicAPI editions of pfUI and pfQuest. I found the project in August 2026, switched my
> whole install to it, and ported my fixes onto his trees. It is his project that everything here
> rests on.
>
> **ClassicAPI is not part of the stock Octo client** — the launcher does not install it for you.
> Grab the release from [brues' repo](https://github.com/brues-code/ClassicAPI), then add it via
> the launcher's *MODS → Your DLL mods → Add DLL* (or drop it next to `WoW.exe` and add a
> `ClassicAPI.dll` line to `dlls.txt` by hand — same thing). **SuperWoW is added the same way** —
> the launcher does not ship it either. Without the ClassicAPI DLL, nothing on this list that
> says "ClassicAPI" will run.
>
> My pfUI and pfQuest trees are **real GitHub forks** of his repositories — they sit in his network
> and the fixes that belong upstream go to him as focused PRs (two are already merged in pfUI).
>
> This describes **my particular install** — treat it as a reference, not something to copy
> wholesale. My **[legacy setup](https://github.com/roby-brok/octowow-addons)** does not need
> ClassicAPI and keeps working the classic way, with shipped data tables. Nothing there is going
> away.

---

## What ClassicAPI changes

[ClassicAPI](https://github.com/brues-code/ClassicAPI) is a DLL that backports a large slice of the
modern Blizzard Lua API to 1.12 — `C_Spell`, `C_UnitAuras`, `C_NamePlate`, `C_Container`,
`C_EquipmentSet`, `C_Timer`, a real `focus` unit, and about 500 functions besides. Addons built on
it can ask the client for data instead of shipping hand-maintained tables.

For this setup that meant three things:

- **Nameplates stopped stuttering.** pfUI's old nameplate code walked every `WorldFrame` child every
  frame. The ClassicAPI edition is event-driven with real per-plate unit tokens and GUIDs. This was
  the single biggest change in day-to-day feel.
- **Two addons became redundant** and are no longer in the list below — see *Dropped*.
- **Everything hard-depends on the DLL.** No ClassicAPI, no pfUI. Keep a copy of the legacy build if
  that worries you.

---

## Client mods (DLLs)

Loaded by [VanillaFixes](https://github.com/hexblade/VanillaFixes) and listed in `dlls.txt`. These
are not addons — most of what follows depends on them.

The launcher ships nampower and UnitXP itself (MODS tab); **SuperWoW and ClassicAPI it does
not** — add both via *MODS → Your DLL mods → Add DLL*.

| Mod | Version | Source |
|---|---|---|
| **ClassicAPI** | — | **https://github.com/brues-code/ClassicAPI** — required, everything below assumes it |
| SuperWoW | 2.2 | https://github.com/balakethelock/SuperWoW |
| Nampower | 4.6.2 | https://github.com/Emyrk/nampower |
| UnitXP SP3 | v90 | https://github.com/brues-code/UnitXP_SP3 — his build of [konaka's original](https://codeberg.org/konaka/UnitXP_SP3), adds a background-FPS cap and reworked crit animation |

---

## Interface

| Addon | Version | Source |
|---|---|---|
| pfUI | ClassicAPI | **[my fork](https://github.com/roby-brok/pfUI-classicAPI)** of **[brues-code's ClassicAPI Edition](https://github.com/brues-code/pfUI)** — original by [Shagu](https://github.com/shagu/pfUI). His edition is the substantial work; mine adds preferences and polish on top — nearly all bug fixes found here are **already merged upstream** (PRs #39/#40). What remains is listed briefly in its README and fully in `CHANGES-octo.md` |
| pfUI [Addon Skinner] | 0.5 | **[my fork](https://github.com/roby-brok/pfUI-addonskinner)** of [jrc13245's](https://github.com/jrc13245/pfUI-addonskinner) — originals by [dein0s](https://gitlab.com/dein0s_wow_vanilla/pfUI-addonskinner) and [RoadBlock](https://github.com/Road-block/). Adds a skin for Mik's Scrolling Battle Text's options window; upstream invites PRs for new skins, so this should land there eventually |
| pfUI [Better Totems] | 1.0 | **[my fork](https://github.com/roby-brok/pfUI-bettertotems)** — original by [Bombg](https://github.com/Bombg/pfUI-bettertotems) |
| AtlasLoot | 3.4.4 | https://github.com/Otari98/AtlasLoot — ⚠️ **use this fork.** "AtlasLoot TW Edition v1.0.2" works but cannot be skinned by pfUI-addonskinner, and fails for none of the obvious reasons |
| Atlas-TW (Atlas-CFM) | 1.60 | https://github.com/byCFM2/Atlas-TW |
| PizzaSlices | 1.5.2 | by Pizzahawaii — [mirror](https://github.com/roby-brok/octowow-addon-mirrors) |
| Turtle_General / Turtle_GroupUI | — | *bundled with the client* |

## Quests & world

| Addon | Version | Source |
|---|---|---|
| pfQuest | ClassicAPI | **[my fork](https://github.com/roby-brok/pfQuest-classicAPI)** of **[brues-code's edition](https://github.com/brues-code/pfQuest)** — original by [Shagu](https://github.com/shagu/pfQuest), continued by [The Kludge Bureau](https://github.com/The-Kludge-Bureau/pfQuest). His edition reads quest IDs from `C_QuestLog` rather than matching quest text, which removes a whole class of lookup failures. The fork's `[Translate]` repair is offered upstream as [PR #2](https://github.com/brues-code/pfQuest/pull/2) |
| pfQuest [Octo DB] | 1.0.13 | **[my pack](https://github.com/roby-brok/pfQuest-octo)** — [The Kludge Bureau's](https://github.com/The-Kludge-Bureau/pfQuest-turtle) TurtleWoW database with [paokkerkir's](https://github.com/paokkerkir/pfQuest-octo) Octo pack folded in. Replaces both — do not install them alongside it. Works unchanged on the ClassicAPI edition |
| pfExtend | 1.0.8 | **[my fork](https://github.com/roby-brok/pfExtend)** — original by [Cliencer](https://github.com/Cliencer/pfExtend) and TinyStick. ⚠️ While its QuestHelper browser is open it resets pfQuest's tracker and route on every refresh — close it when done |

## Combat

| Addon | Version | Source |
|---|---|---|
| GreedMeter | 1.2.5 | https://github.com/iGreed1993/GreedMeter — damage **and threat** meter with **GUID attribution** through SuperWoW's raw combat log, the accuracy leap chat-parsing meters can't make. Its threat mode replaced OWThreat in this setup (2026-08-14); the early drag-crash was fixed upstream in 1.2.2 after [issue #1](https://github.com/iGreed1993/GreedMeter/issues/1) |
| Mik's Scrolling Battle Text | v5.0-octo | **[my fork](https://github.com/roby-brok/MikScrollingBattleText)** — original by Mik; now rebased onto **[brues-code's continuation](https://github.com/brues-code/Vanilla_MikScrollingBattleText)** (the living branch of the family), which also drops the Babble-Spell library by resolving names through Nampower. My three fixes ride on top: it no longer silently switches combat logging to disk on (269 MB found), the combat-log parser gets a cheap literal-prefix reject, and the negative icon cache is honoured. Needs the stock `MikScrollingBattleTextOptions` alongside it, unmodified — that folder ships in [jrc13245/Vanilla_MikScrollingBattleText](https://github.com/jrc13245/Vanilla_MikScrollingBattleText), so you don't have to hunt for it |
| Aegis: RallyPower | 1.1.0 | https://github.com/Torchlite-bit/Aegis_RallyPower |
| Aegis: Single Button Rotation | 1.1.8 | https://github.com/Torchlite-bit/Aegis_SBR — already ClassicAPI-native (`C_Spell`, `C_UnitAuras`, `C_Timer`, `C_EncodingUtil`) |

## Macros & API

| Addon | Version | Source |
|---|---|---|
| SuperCleveRoidMacros | 2.4+ | **[brues-code's fork](https://github.com/brues-code/SuperCleveRoidMacros)** of [jrc13245's](https://github.com/jrc13245/SuperCleveRoidMacros) — built to pair with his pfUI (shared cast tracking, no redundant mouseover hooks) and adds `#showtooltip spell:<id>` / `item:<id>`. **Still required:** ClassicAPI gives macros better *inputs* but has no conditional parser; `[@mouseover,help]` is entirely CleveRoids' |
| SuperAPI | — | https://github.com/balakethelock/SuperAPI |
| Nampower Settings | — | https://github.com/Emyrk/nampowersettings — the companion settings addon from the nampower maintainer |
| OctoCVars | 0.2.1 | **[my addon](https://github.com/roby-brok/OctoCVars)** — cvar browser for this stack. 1.12 can't enumerate cvars, so it ships a curated list (stock + Nampower `NP_*` + SuperWoW) and probes it at login: only cvars your client actually has are shown. Search, changed-from-default filter, edit with hints, reset. `/cvars` |
| UnitXP SP3 Addon | v90 | https://github.com/brues-code/UnitXP_SP3_Addon — paired with his v90 DLL below; degrades with a clear message instead of erroring when the DLL is older |

## Items, bags & characters

| Addon | Version | Source |
|---|---|---|
| Aegis: Exchange | 1.8.0 | https://github.com/Torchlite-bit/Aegis_Exchange — auction house helper |
| StatCompare | 2.0.0 Beta | by slashboy, updated by Provocateur@turtlewow — [mirror](https://github.com/roby-brok/octowow-addon-mirrors) |
| Aegis: Courier | 1.0.4 | https://github.com/Torchlite-bit/Aegis_Courier — mailbox companion |
| PizzaWorldBuffs | 2.0.0 | https://github.com/acid9000/PizzaWorldBuffs |

---

## Rotated out on 2026-08-10

Removed from the install, so removed from the list — nothing wrong with any of them:
**ShaguDPS** (GreedMeter trial), **OctoMail** (Aegis: Courier), **aux-addon** (Aegis:
Exchange), and **BigWigs, BetterCharacterStats, DoiteAuras, FlightMap, LevelRange-Turtle,
ModernMapMarkers-octo** — out of the ClassicAPI loadout for now; most remain on the
[legacy list](https://github.com/roby-brok/octowow-addons).

**OWThreat** followed on 2026-08-14 — GreedMeter's threat mode covers it now. The fork
stays maintained at [roby-brok/OWThreat](https://github.com/roby-brok/OWThreat), speaks
the same threat API as stock TWThreat, and remains on the legacy list.

## Dropped — now native

Not a criticism of either addon. The functionality simply moved into the client mod or into pfUI.

| Addon | Replaced by |
|---|---|
| **ItemRack** | pfUI's built-in **Equipment Manager**, backed by `C_EquipmentSet`. Engine-side and GUID-tracked, so it tells apart duplicate and enchanted copies of the same item — which name-and-slot matching cannot |
| **SuperMacro** | ClassicAPI supplies `C_Macro.CreateMacro` / `EditMacro`, `GetMacroSpell` and the macro-icon lookups. I had no super macros defined and it threw a load error at every login |

**SortBags** ([shirsig](https://github.com/shirsig/SortBags)) is also largely superseded — pfUI now
sorts bags and bank through `C_Container.MoveItem`, which is instant rather than a cursor
pickup-and-drop loop, with an auto-sort-on-open option. Still perfectly fine to keep.

---

## Notes

**Entries marked *mirror* have no live upstream I could find.** Those copies are re-uploaded
unmodified to [octowow-addon-mirrors](https://github.com/roby-brok/octowow-addon-mirrors), which
makes clear they are not my work and lists each author. If you know the real home for one, open an
issue and I will link it and delete the copy.

**Installing from a GitHub ZIP:** the green *Code → Download ZIP* button unpacks as
`Name-main` or `Name-master`. The game (and pfUI's addon integrations) only recognize the
addon if the folder inside `Interface\AddOns` is named **exactly** the addon's own name
(`pfUI`, `OWThreat`, …) — rename it after unzipping, or use `git clone` instead.

**The forks** exist only to carry fixes I hit while playing. Each one's README explains what was
changed and why. Use the originals unless you specifically want those fixes — and if an upstream
author wants a change, it's theirs to take.

## Thanks

To everyone whose work is listed above. To **Shagu**, whose pfUI and pfQuest are the backbone of
this setup, and to **[brues-code](https://github.com/brues-code)**, whose ClassicAPI and its pfUI
and pfQuest editions are what this entire list is built on.
