# Cross-promo catalog

`catalog.json` lists the studio's games for the in-game "More games" button and the small card on
the won-level screen. Every game reads it through `createCrossPromo` in `@taninteractive/game-core`
(`platform/cross-promo`, rules in `pure/crossPromo`) and ships a snapshot of it in
`src/data/promoCatalog.json`, copied before each release build.

Served at `https://taninteractive.github.io/promo/catalog.json`. Games cache it for 24 h, so an edit
reaches players within a day, without an app update.

## Fields

| Field | Rule |
|---|---|
| `version` | Bump on **every** edit (a game's bundled snapshot newer than its cached copy wins) |
| `enabled` | `false` hides every suggestion in every game (kill switch) |
| `placements.<name>` | `false` hides that placement (`menu`, `result`); a missing name is on |
| `games[].id` | Studio slug, `[a-z0-9-]`, the game's `selfId` and the analytics `target` |
| `games[].name` | Card title per language, `en` required, ≤ 30 characters |
| `games[].tagline` | One line per language, `en` required, ≤ 60 characters; a missing language falls back to `en` |
| `games[].icon` | Relative to this folder (`<id>/icon-192.png`), 192×192 PNG from the game's 512 store icon |
| `games[].stores.google/amazon` | `package` and `live`. **`live: true` only when the game is public in that store**: Play production (never closed or open testing), Amazon live |
| `games[].weight` | Relative chance to be picked (default 1) |

An entry that breaks a rule is dropped by the games, never shown half-filled.

## When a game goes live in a store

1. Set `stores.<store>.live` to `true` and bump `version`.
2. Merge. Players see it within 24 h.

Status on 2026-10-29: Google Play production = Hungry Frog, Pillowhold, Mossbelly, Yardlight; Amazon live =
Hungry Frog, Blotsling, Mossbelly, Yardlight, Pillowhold (Tailwallop showed Live in the Amazon console on 2026-10-27, still `false` until the owner confirms the flip).

## Rules (Google Play policy and studio)

- Never reward a player for installing another game (incentivised installs are forbidden).
- Taglines: plain words, no ranking claims ("#1", "best"), no prices, no other companies' names.
- Icons are the games' own store icons only.
