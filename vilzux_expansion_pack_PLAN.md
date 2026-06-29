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
| 3 | Eliteserien | Norway | ✅ | ⏳ (post-FL27) | ⏳ | ⏳ | Research complete |
| 4 | Superliga | Denmark | ✅ N/A | N/A | N/A | N/A | **Already in FL26 — skip** |
| 5 | SuperLiga | Serbia | ✅ | ⏳ (post-FL27) | ⏳ | ⏳ | Research complete |
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

### 3. Norway — Eliteserien ✅

**Tier & size:** Top tier, 16 clubs (season runs March–December, unusually long to accommodate Scandinavian winter).

**2026 clubs (confirmed):**
Aalesunds FK, SK Brann, FK Bodø/Glimt, Fredrikstad FK, HamKam, KFUM Oslo, Kristiansund BK, Lillestrøm SK, Molde FK, Rosenborg BK, Sandefjord Fotball, Sarpsborg 08, IK Start, Tromsø IL, Vålerenga IF, Viking FK.
Defending champions: Viking FK (2025 title).

**Season format:** Straight double round-robin — 30 matches each, 240 league-wide. No split format. Straightforward engine implementation — same as Allsvenskan.

**Promotion/relegation:**
- Bottom two (15th, 16th) automatically relegated to the Norwegian First Division.
- 14th-placed team plays a two-legged playoff against the runner-up of the First Division promotion playoffs — winner stays/enters Eliteserien.
- Top two from the First Division are automatically promoted.
- 2nd tier: Norwegian First Division (also known as OBOS-ligaen for sponsorship reasons).

**Domestic cup:** Norwegian Football Cup (Norges Fotballcup). 
⚠️ The cup winner earns the title of "Norwegian Champions" — distinct from the league winner — a cultural detail worth noting even if the in-game implementation can't reflect it directly.

**UEFA qualification (confirmed from ESPN/Sofascore for current cycle):**
- 1st and 2nd → Champions League qualifying.
- 3rd → Europa League qualifying.
- 4th → Conference League qualifying.
- Norwegian Cup winner likely also earns a UEFA slot (verify exact path before final implementation).
- Total: roughly **4 UEFA slots (2 CL + 1 EL + 1 ECL)** — notably more CL slots than Finland/Sweden, reflecting Norway's stronger UEFA coefficient.

**Derbies to include:**
- **Rosenborg vs Molde** — "Marathon of the North," the headline rivalry of the modern era. Rosenborg (Trondheim) vs Molde; both consistent title contenders since the 2010s.
- **Vålerenga vs Lillestrøm** — fierce Oslo-area derby. Strong supporter culture on both sides; Vålerenga ultras famously beheaded a statue of a Lillestrøm legend at some point (noted as a detail of the intensity, not to celebrate). Both clubs in Eliteserien 2026.
- **KFUM Oslo vs Vålerenga** — both in the 2026 season, making the Oslo derby an active fixture this year.
- **Rosenborg vs Vålerenga** — inter-city rivalry between Norway's most-titled club (26 championships) and the capital's biggest club.
- ⚠️ Brann (Bergen) vs Vålerenga (Oslo) also carries rivalry weight — geographically a west/east clash — worth including if both stay top-flight long-term.

**Stadiums:** Not yet cross-checked against FL26's default list — pending Asset Inventory pass. Notable grounds: Lerkendal Stadion (Rosenborg, ~21,400 cap), Brann Stadion (~17,700), Intility Arena (Vålerenga), Aspmyra Stadion (Bodø/Glimt, ~8,000 — intimate atmosphere, consistently unsettles opponents at home).

**Kits/badges:** Not yet sourced — pending your input on existing assets.

---

---

### 5. Serbia — SuperLiga ✅

**Tier & size:** Top tier. **⚠️ CRITICAL — League is actively shrinking:**
- 2025–26 season: **16 teams** (current season)
- 2026–27 season: **14 teams** (four relegated from 2025-26, two promoted)
- 2027–28 season: **12 teams** (planned further reduction)

Since FL27 launches around October 2026, it will almost certainly ship with the **2026-27 season data — 14 teams, not 16**. Plan the implementation around 14 teams. Do not build a 16-team slot and expect it to match real-world data.

**2025–26 clubs (16, current season — for reference):**
Red Star Belgrade, Partizan, Vojvodina, Radnički Niš, TSC Bačka Topola, OFK Beograd, Spartak Subotica, Čukarički, Mladost Lučani, FK Novi Pazar, Napredak Kruševac, Radnički 1923, Kolubara, FK Inđija, Radnik Surdulica, Javor-Matis.
⚠️ For the 2026-27 14-team list, pull fresh data once FL27 launches — four clubs will have been relegated.

**Season format:** Double round-robin regular season (30 games each), then **split** into two groups of 8: a Championship Round (top 8, playing for title and UEFA spots) and a Relegation Round (bottom 8, playing to avoid drop). Points carried forward from the regular season.
⚠️ This is the second split-season format we've encountered after Finland. Same engine limitation applies — implement as straight round-robin unless proven otherwise. When the league reduces to 14 the format may also change; re-check before implementing.

**Promotion/relegation (2026-27 structure, 14 teams):**
- Bottom two automatically relegated.
- 13th and 14th enter play-offs against 3rd and 4th from the Serbian First League.
- Serbian First League's top two automatically promoted.
- 2nd tier: Serbian First League (Prva Liga Srbije).

**Domestic cup:** Serbian Cup (Kup Srbije).

**UEFA qualification:**
- Champion → Champions League qualifying (playoff round — strong entry point).
- Runner-up → Champions League qualifying (second qualifying round).
- 3rd place → Conference League qualifying (third qualifying round).
- 4th place → Conference League qualifying (second qualifying round).
- Serbian Cup winner → Europa League qualifying (playoff round).
- Total: **2 CL + 1 EL + 2 ECL = 5 UEFA slots** — the most generous allocation of any league in our list so far, reflecting Serbia's historically strong UEFA coefficient (currently ranked 13th in Europe out of 55 leagues).

**Derbies to include:**
- **Večiti derbi (The Eternal Derby): Red Star Belgrade vs Partizan Belgrade** — unambiguously one of the most intense derbies in world football. Both clubs formed in 1945, stadiums less than 1km apart in south Belgrade, have won every Serbian SuperLiga title since 1992 bar one. Red Star's ultras are called the Delije; Partizan's are the Grobari (Gravediggers). Described as "one of European football's most bitter rivalries" — ranked in multiple global top-10 lists. This is the headline fixture of the entire expansion pack; maximum rival weight in-game.
- ⚠️ Other Serbian derbies (e.g. Vojvodina vs Spartak Subotica — Vojvodinian derby) exist but are secondary and regional. Wire them only if both clubs are in the 14-team setup at implementation time.

**Stadiums:**
- Rajko Mitić Stadium ("Marakana") — Red Star Belgrade, one of the most recognisable grounds in Eastern Europe.
- Partizan Stadium — Partizan Belgrade, located under 1km from Marakana.
- Not yet cross-checked against FL26's default list — pending Asset Inventory pass.

**Kits/badges:** Not yet sourced — pending your input on existing assets. Note: Red Star and Partizan are well-known clubs — community kit packs for both are widely available.

---

*(Leagues 6–12 to be added one at a time, same format, as we work through the list.)*
