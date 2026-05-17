# Pdusen's SkyrimNet Knowledge Packs — Agent Instructions

## Repo overview

This repo distributes SkyrimNet Knowledge Packs (`.sknpack` JSON files) that give SkyrimNet's LLM-driven
NPCs awareness of locations and characters added by popular Skyrim SE/AE city and college overhauls. Each
pack lives in [`packs/`](packs/) and is intended to be paired with a specific set of upstream mods.

## Invariant: every pack must be documented in the README

For every `.sknpack` file present in [`packs/`](packs/), [README.md](README.md) must contain a matching
entry under the `## Included Packs` heading. When a pack is added, renamed, or removed, update the README
in the same change — never leave the two out of sync.

## Format for a pack entry

Each pack entry under `## Included Packs` follows this shape. Match it exactly so the README stays
consistent as packs are added.

```markdown
### [Pack Display Name](packs/Pack_File_Name.sknpack)

**Intended mod combination:** [Mod A](https://www.nexusmods.com/skyrimspecialedition/mods/NNNN) +
[Mod B](https://www.nexusmods.com/skyrimspecialedition/mods/NNNN) +
[Mod C](https://www.nexusmods.com/skyrimspecialedition/mods/NNNN). These mods **must** be combined using
the [Exact Patch Mod Name](https://www.nexusmods.com/skyrimspecialedition/mods/NNNN) mod — this pack is
built against the exact merged layout that patch produces, and other compatibility solutions may not
match.

Adds knowledge for <one-sentence summary of what the pack covers>: <comma-separated list of the locations
it adds> and the residents/faculty/etc. <comma-separated list of NPCs>. NPCs in the <relevant faction(s)>
will recognize these locations and people in conversation.
```

Rules for filling in the template:

- **Heading link text** — use a human-readable name for the pack (typically derived from the pack
  filename, with underscores replaced by spaces and "`-`" preserved where it appears).
- **Heading link target** — the literal relative path `packs/<filename>.sknpack`.
- **Intended mod combination** — list every upstream mod the pack assumes is installed. Link each one to
  its **correct** Nexus Mods page. If a specific version is required (e.g. "Great City of Winterhold v4"),
  call that out in bold inline text. If the mods must be merged via a specific patch mod, name and link
  that patch mod, and include the "this pack is built against the exact merged layout that patch
  produces…" caveat — other patches that combine the same base mods will not line up.
- **Summary paragraph** — describe what the pack adds in prose, not as a bullet list. Source the content
  from the pack's own JSON:
  - `skyrimnet_knowledge_pack.description` gives the high-level framing.
  - Each `entries[].display_name` with `type: "LOCATION"` is a location to mention.
  - Each `entries[].display_name` with `type: "RELATIONSHIP"` is an NPC to mention. Strip any `NPC:` /
    role-suffix scaffolding from the display name when listing the NPC by name in the summary (e.g.
    `"NPC: Thelsa Andalas - Alchemy Instructor"` → "Thelsa Andalas").
  - The faction in `entries[].condition_expr` (e.g. `CollegeofWinterholdFaction`,
    `TownWinterholdFaction`) determines which faction's NPCs will "recognize" the entries — name those
    factions in the closing sentence.

## When verifying Nexus links

Mod IDs in URLs are easy to get wrong from memory alone. Before recommending or committing a Nexus Mods
link, confirm the ID by searching the web for the mod name on `nexusmods.com` rather than guessing.

## Style

- Keep entries succinct — one short intended-mods paragraph and one short summary paragraph per pack. Do
  not introduce bullet lists, sub-headings, or feature tables inside an entry.
- Match the tone of existing entries: descriptive, neutral, and oriented around what an in-game NPC would
  plausibly know.
