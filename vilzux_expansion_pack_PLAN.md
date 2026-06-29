# VilzuX Expansion Pack — Master Planning Document

**Base:** Football Life 2026 (FL26) — currently in research/prototype phase. Final database implementation deferred to FL27 (expected ~Oct 2026, unconfirmed — watch SmokePatch's site).
**Last updated:** 2026-06-20

---

## Open decisions (pending your input — update this section as you decide)

- [ ] Sandbox FL26 copy set up for safe testing, separate from your main install?
- [ ] Existing kit/badge/logo assets for any of the 12 leagues — which, if any?
- [ ] Split-season leagues (see limitation #1 below) → approximate as round-robin (recommended) or attempt advanced Sider scripting?
- [ ] Roster accuracy target — exact current 2026 table, or "close enough" if a specific club is hard to source?

---

## Known engine limitations to design around

1. **Split-season formats.** Several target leagues split into championship/relegation groups partway through the season (confirmed so far: Finland). PES's competition engine is built around fixed round-robin or group+knockout — a mid-season table split is very unlikely to be natively supported. Default plan: implement as a straight round-robin unless proven otherwise during testing.
2. **Competition menu fragility.** SmokePatch's own FL25 release notes mention a newly-added league being pulled from the menu "due to multiple issues" until it could be re-added safely. Treat any new competition slot as fragile until heavily tested.
3. **Continental competition format.** FL26 still uses the pre-2024 group-stage + knockout UEFA format, not the real-world Swiss league-phase model. Our Conference League build should target old-format realism, not a Swiss-model emulation.
4. **Database edits are unsupported by SmokePatch.** They may be overwritten by future updates. Always keep backups; expect to redo ID bindings after major version changes (e.g. FL26 → FL27).

---

## League rollout order & status

| # | League | Country | Research | IDs Found | DB Wired | Cosmetics | Status |
|---|--------|---------|----------|-----------|----------|-----------|--------|
| 1 | Veikkausliiga | Finland | ✅ | ⏳ (post-FL27) | ⏳ | ⏳ | Research complete |
| 2 | Allsvenskan | Sweden | ✅ | ⏳ (post-FL27) | ⏳ | ⏳ | Research complete |
| 3 | Eliteserien | Norway | ⏳ | ⏳ | ⏳ | ⏳ | Not started |
| 4 | Superliga | Denmark | ⏳ | ⏳ | ⏳ | ⏳ | Not started |
| 5 | SuperLiga | Serbia | ⏳ | ⏳ | ⏳ | ⏳ | Not started |
| 6 | HNL | Croatia | ⏳ | ⏳ | ⏳ | ⏳ | Not started |
| 7 | Ekstraklasa | Poland | ⏳ | ⏳ | ⏳ | ⏳ | Not started |
| 8 | Chance Liga | Czech Republic | ⏳ | ⏳ | ⏳ | ⏳ | Not started |
| 9 | Niké Liga | Slovakia | ⏳ | ⏳ | ⏳ | ⏳ | Not started |
| 10 | PrvaLiga | Slovenia | ⏳ | ⏳ | ⏳ | ⏳ | Not started |
| 11 | SuperLiga | Romania | ⏳ | ⏳ | ⏳ | ⏳ | Not started |
| 12 | NB I | Hungary | ⏳ | ⏳ | ⏳ | ⏳ | Not started |

Tracked separately once dossiers are far enough along: UEFA Conference League integration, domestic cup wiring, rivalry/derby data entry, kit/badge/stadium asset pass.

---

## League Dossiers

### 1. Finland — Veikkausliiga ✅

**Tier & size:** Top tier, 12 clubs.

**Season format:** Double round-robin regular season (22 rounds), then the table splits into a 6-team Championship Round and a 6-team Relegation Round, each playing one more round-robin (5 rounds), carrying points forward. ~27 rounds / ~162 total matches league-wide.
⚠️ Split format — see engine limitation #1.

**Promotion/relegation:**
- Bottom-placed team (12th) is automatically relegated.
- 11th-placed team plays a relegation/promotion play-off against a representative from Ykkösliiga (2nd tier); winner keeps/gains the Veikkausliiga spot.
- Ykkösliiga's champion is automatically promoted.
- 2nd tier: Ykkösliiga, 10 clubs.

**Domestic cup:** Finnish Cup (Suomen Cup).

**UEFA qualification (most recently confirmed cycle):**
- 1st place → UEFA Champions League qualifying.
- 2nd place → UEFA Conference League qualifying.
- In practice, three teams entered Conference League qualifying for the 2025→2026 cycle (2nd–4th placed), alongside the champion in the Champions League path. Budget for **roughly 4 total UEFA slots (1 CL + 3 ECL)**, but recheck UEFA's official access list before finalizing — allocations shift with coefficient rankings.

**Derbies to include:**
- **Stadin derby (Helsinki derby): HJK vs HIFK** — the marquee one. Rivalry traces to 1909, originally tied to Finnish- vs Swedish-speaking communities, now played at Bolt Arena.
- Turku derby: TPS vs Inter Turku
- Pirkanmaan derby: Haka vs Ilves
- Metroderby: HJK/HIFK vs FC Honka
- ⚠️ Other historically-named derbies (vs Tampere United, OPS, KPV) involve clubs not currently in Veikkausliiga — verify current division before wiring rivalry data.

**Stadiums:** Not yet cross-checked against FL26's default stadium list — pending the Asset Inventory pass.

**Kits/badges:** Not yet sourced — pending your input on existing assets.

---

### 2. Sweden — Allsvenskan ✅

**Tier & size:** Top tier, 16 clubs (since 2008).

**Season format:** Single round-robin home/away, no split — every club plays every other club twice (30 matches each, 240 league-wide). Simpler than Finland; no engine workaround needed here.

**Promotion/relegation:**
- Bottom two (15th, 16th) automatically relegated.
- 14th-placed team plays a two-legged relegation/promotion play-off against Superettan's 3rd-placed team (Allsvenskan side hosts the second leg).
- Superettan's top two are automatically promoted; its 3rd-placed team gets the play-off shot above.
- 2nd tier: Superettan, 16 clubs, also double round-robin (30 games each).

**Domestic cup:** Svenska Cupen.

**UEFA qualification:**
- Champion → Champions League qualifying.
- Runner-up (2nd) and 3rd place → Conference League qualifying.
- Svenska Cupen winner → Europa League qualifying.
- Fallback: if the cup winner already qualified via league position, the spare Conference League spot passes to the 4th-placed league team.
- Tidy total: **1 CL + 1 EL + 2 ECL = 4 UEFA slots.**

**Derbies to include:**
- **Tvillingderbyt (the Twinderby): AIK vs Djurgården** — the marquee one, "biggest derby in Sweden/Scandinavia," rivalry dating to 1891 (both clubs founded three weeks apart).
- Other Stockholm clashes: Hammarby vs AIK, Hammarby vs Djurgården — Stockholm currently has 4 clubs in Allsvenskan (AIK, Djurgården, Hammarby, Brommapojkarna) for 2026, so the derby calendar is unusually busy this season.
- **Göteborgsklassikern: IFK Göteborg vs Örgryte IS** — historic, holds the all-time Allsvenskan attendance record (52,194 in 1959).
- IFK Göteborg vs GAIS — the other major Gothenburg derby; Gothenburg also has 4 clubs in the 2026 top flight (IFK Göteborg, GAIS, BK Häcken, Örgryte).
- **Västderby ("El Västico"): IF Elfsborg vs IFK Göteborg.**
- **Mesta mästarmötet: IFK Göteborg vs Malmö FF** — clash of Sweden's two most-titled clubs.
- ⚠️ Skånederbyt (Malmö FF vs Helsingborgs IF) is historically significant but currently **inactive at top-flight level** — Helsingborg isn't in Allsvenskan this season. Hold off wiring it in as an active derby unless/until they're promoted; re-check before implementation.

**Stadiums:** Not yet cross-checked against FL26's default list — pending Asset Inventory pass.

**Kits/badges:** Not yet sourced — pending your input on existing assets.

---

*(Leagues 3–12 to be added one at a time, same format, as we work through the list.)*
