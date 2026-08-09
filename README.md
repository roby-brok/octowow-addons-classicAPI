# My OctoWoW Addon Setup — ClassicAPI Edition

The addons and client mods I run on [OctoWoW](https://octowow.st) (WoW 1.12.1 client),
**rebuilt around [ClassicAPI](https://github.com/brues-code/ClassicAPI)**.

This repository is **a list, not a mirror.** No addon code is hosted here — every entry links to the
author's own repository, which is where you should download it from. All credit belongs to the
people who wrote these; I just use them and occasionally fix something.

Maintained by **Roby_Brok**.

> ### Status: private / not released
>
> This setup depends on **[brues-code](https://github.com/brues-code)'s** work — ClassicAPI itself,
> plus his ClassicAPI editions of pfUI and pfQuest. I only found the project in August 2026 and
> ported my fixes onto it. **This list stays private until he's had a chance to look at it**, out of
> courtesy — it's his project the whole thing rests on.
>
> My **[legacy setup](https://github.com/roby-brok/octowow-addons)** is the public one and does not
> need ClassicAPI. Nothing there is going away.

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

| Mod | Version | Source |
|---|---|---|
| **ClassicAPI** | — | **https://github.com/brues-code/ClassicAPI** — required, everything below assumes it |
| SuperWoW | 2.2 | https://github.com/balakethelock/SuperWoW |
| Nampower | 4.6.2 | https://github.com/Emyrk/nampower |
| UnitXP SP3 | — | https://codeberg.org/konaka/UnitXP_SP3 |

---

## Interface

| Addon | Version | Source |
|---|---|---|
| pfUI | ClassicAPI | **[my fork](https://github.com/roby-brok/pfui-classicAPI)** of **[brues-code's ClassicAPI Edition](https://github.com/brues-code/pfUI)** — original by [Shagu](https://github.com/shagu/pfUI). His edition is the substantial work; mine adds ~45 fixes on top, listed in its `CHANGES-octo.md` |
| pfUI [Addon Skinner] | 0.5 | **[my fork](https://github.com/roby-brok/pfUI-addonskinner)** of [jrc13245's](https://github.com/jrc13245/pfUI-addonskinner) — originals by [dein0s](https://gitlab.com/dein0s_wow_vanilla/pfUI-addonskinner) and [RoadBlock](https://github.com/Road-block/). Adds a skin for Mik's Scrolling Battle Text's options window; upstream invites PRs for new skins, so this should land there eventually |
| pfUI [Better Totems] | 1.0 | **[my fork](https://github.com/roby-brok/pfUI-bettertotems)** — original by [Bombg](https://github.com/Bombg/pfUI-bettertotems) |
| AtlasLoot | 3.4.4 | https://github.com/Otari98/AtlasLoot — ⚠️ **use this fork.** "AtlasLoot TW Edition v1.0.2" works but cannot be skinned by pfUI-addonskinner, and fails for none of the obvious reasons |
| Modern Map Markers [Octo] | 2.4 | https://github.com/paokkerkir/ModernMapMarkers-octo — an OctoWoW fork of [tilare's original](https://github.com/tilare/ModernMapMarkers) |
| LevelRange [Turtle] | 2.2.0 | https://github.com/Spartelfant/LevelRange-Turtle |
| Atlas-TW (Atlas-CFM) | 1.60 | https://github.com/byCFM2/Atlas-TW |
| PizzaSlices | 1.5.2 | by Pizzahawaii — [mirror](https://github.com/roby-brok/octowow-addon-mirrors) |
| Turtle_General / Turtle_GroupUI | — | *bundled with the client* |

## Quests & world

| Addon | Version | Source |
|---|---|---|
| pfQuest | ClassicAPI | **[my fork](https://github.com/roby-brok/pfquest-classicAPI)** of **[brues-code's edition](https://github.com/brues-code/pfQuest)** — original by [Shagu](https://github.com/shagu/pfQuest), continued by [The Kludge Bureau](https://github.com/The-Kludge-Bureau/pfQuest). His edition reads quest IDs from `C_QuestLog` rather than matching quest text, which removes a whole class of lookup failures |
| pfQuest [Octo DB] | 1.0.3 | **[my pack](https://github.com/roby-brok/pfQuest-octo)** — [The Kludge Bureau's](https://github.com/The-Kludge-Bureau/pfQuest-turtle) TurtleWoW database with [paokkerkir's](https://github.com/paokkerkir/pfQuest-octo) Octo pack folded in. Replaces both — do not install them alongside it. Works unchanged on the ClassicAPI edition |
| pfExtend | 1.0.6 | **[my fork](https://github.com/roby-brok/pfExtend)** — original by [Cliencer](https://github.com/Cliencer/pfExtend) and TinyStick. ⚠️ While its QuestHelper browser is open it resets pfQuest's tracker and route on every refresh. Not currently installed on my setup for that reason |
| FlightMap | 1.12-1 | by Dhask — [mirror](https://github.com/roby-brok/octowow-addon-mirrors) |

## Combat

| Addon | Version | Source |
|---|---|---|
| BigWigs | 2.0.0 | https://github.com/pepopo978/BigWigs |
| OWThreat | 1.4.0 | **[my fork](https://github.com/roby-brok/OWThreat)** — original ([TWThreat](https://github.com/MarcelineVQ/TWThreat)) by Xerron/Er. Speaks the same threat API, so it works alongside stock TWThreat users — but do not install both |
| ShaguDPS | 3.0.1 | https://github.com/shagu/ShaguDPS |
| DoiteAuras | 1.8.7 | https://github.com/Player-Doite/DoiteAuras |
| Mik's Scrolling Battle Text | 4.43 | by Mik — [mirror](https://github.com/roby-brok/octowow-addon-mirrors) |
| Aegis: RallyPower | 1.1.0 | https://github.com/Torchlite-bit/Aegis_RallyPower |
| Aegis: Single Button Rotation | 1.1.4 | https://github.com/Torchlite-bit/Aegis_SBR — already ClassicAPI-native (`C_Spell`, `C_UnitAuras`, `C_Timer`, `C_EncodingUtil`) |

## Macros & API

| Addon | Version | Source |
|---|---|---|
| SuperCleveRoidMacros | 2.4 | https://github.com/jrc13245/SuperCleveRoidMacros — **still required.** ClassicAPI gives macros better *inputs* (real unit tokens, spell IDs, focus) but has no conditional parser; `[@mouseover,help]` is entirely CleveRoids' |
| SuperAPI | — | https://github.com/balakethelock/SuperAPI |
| Nampower Settings | — | https://github.com/Dusk-92/NampowerSettings |
| UnitXP SP3 Addon | — | https://github.com/whtmst/UnitXP_SP3_Addon |

## Items, bags & characters

| Addon | Version | Source |
|---|---|---|
| aux-addon | — | https://github.com/OldManAlpha/aux-addon |
| BetterCharacterStats | 1.15.3 | https://github.com/pepopo978/BetterCharacterStats |
| StatCompare | 2.0.0 Beta | by slashboy, updated by Provocateur@turtlewow — [mirror](https://github.com/roby-brok/octowow-addon-mirrors) |
| OctoMail | 1.5.0 | **[my fork](https://github.com/roby-brok/OctoMail)** of [TurtleMail](https://github.com/sica42/TurtleMail) by [shirsig](https://github.com/shirsig) and [sica42](https://github.com/sica42) |
| PizzaWorldBuffs | 2.0.0 | https://github.com/acid9000/PizzaWorldBuffs |

---

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

**The forks** exist only to carry fixes I hit while playing. Each one's README explains what was
changed and why. Use the originals unless you specifically want those fixes — and if an upstream
author wants a change, it's theirs to take.

## Thanks

To everyone whose work is listed above. To **Shagu**, whose pfUI and pfQuest are the backbone of
this setup, and to **[brues-code](https://github.com/brues-code)**, whose ClassicAPI and its pfUI
and pfQuest editions are what this entire list is built on.
