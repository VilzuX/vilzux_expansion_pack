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
| 6 | HNL | Croatia | ✅ | ⏳ (post-FL27) | ⏳ | ⏳ | Research complete |
| 7 | Ekstraklasa | Poland | ✅ | ⏳ (post-FL27) | ⏳ | ⏳ | Research complete |
| 8 | Chance Liga | Czech Republic | ✅ | ⏳ (post-FL27) | ⏳ | ⏳ | Research complete |
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

---

### 6. Croatia — HNL (SuperSport Hrvatska nogometna liga) ✅

**Tier & size:** Top tier, **10 clubs** — the smallest league in our entire expansion pack. This has important engine implications (see format note below).

**2025–26 clubs (confirmed 10-team roster):**
GNK Dinamo Zagreb, HNK Hajduk Split, HNK Rijeka, NK Osijek, NK Lokomotiva Zagreb, NK Varaždin, HNK Gorica, NK Slaven Belupo (Koprivnica), NK Istra 1961, NK Vukovar 1991 (promoted for first time in club history).
Defending champions: GNK Dinamo Zagreb (2025–26 title, their 25th HNL title overall).

**Season format: ⚠️ NEW ENGINE LIMITATION — QUADRUPLE round-robin.**
With only 10 teams, each club plays every opponent **4 times** (twice home, twice away) = **36 matches per team**. This is how the HNL compensates for having so few clubs — it fills the calendar with extra fixtures rather than expanding the number of teams.

The PES competition engine supports double round-robin (home + away = 2 matches per opponent) natively. A quadruple format almost certainly cannot be configured in the standard engine without advanced Sider scripting — and there's no confirmed community workaround for this.

**Recommended implementation approach:** Implement as a standard **double round-robin (18 matches per team)**, accepting the reduced match count. The fixture count difference is noticeable but unavoidable without the quadruple round-robin. Make a note in the mod's documentation. This is the cleanest stable option. Do NOT try to add extra rounds — this risks instability.

**Promotion/relegation:**
- 10th place automatically relegated to Prva NL (2nd tier).
- 9th place enters a two-legged playoff against 3rd place from the Prva NL — winner stays/enters HNL.
- Prva NL champion is automatically promoted.
- 2nd tier: Prva NL (SuperSport Prva Nogometna Liga).

**Domestic cup:** Croatian Football Cup (Hrvatski nogometni kup).

**UEFA qualification:**
- Champion → CL second qualifying round (champions path).
- Runner-up (2nd) and 3rd → Conference League qualifying.
- Croatian Cup winner → Europa League second qualifying round.
- Cascade rule: if Cup winner already qualified via league position, the EL spot moves to 2nd place, and the spare ECL spot moves to 4th place.
- Total: **1 CL + 1 EL + 2 ECL = 4 UEFA slots** (subject to cascade).

**Derbies to include:**
- **Vječni derbi / Eternal Derby: Dinamo Zagreb vs Hajduk Split** — the Croatian equivalent of the Eternal Derby in Serbia. Part of the historic Yugoslav "Big Four" alongside Red Star and Partizan. The rivalry traces to the 1920s, intensified post-independence in 1991. Dinamo's ultras are the Bad Blue Boys (BBB); Hajduk's are the Torcida — one of the oldest ultras groups in Europe (founded 1950, older than most Italian groups). Hajduk have 100,000+ members, making them one of Europe's largest fan-owned clubs. Classified as a high-risk event by police; over 100 fans detained in 2025 before a fixture in Split. Maximum rival weight in-game.
- **Dinamo Zagreb vs Rijeka** — secondary but growing rivalry, especially fierce during the 2010s when Rijeka challenged Dinamo's dominance. Rijeka won their first Croatian title in 2016–17, breaking years of Dinamo/Hajduk hegemony. Worth including as a second-tier rivalry.
- ⚠️ Note that Dinamo Zagreb is also historically rival with Serbian clubs Red Star and Partizan from the Yugoslav era — not relevant for domestic implementation, but worth knowing when wiring cross-competition encounters in the Conference League/Europa League later.

**Stadiums:**
- Stadion Maksimir — Dinamo Zagreb, Zagreb (capacity ~35,000).
- Stadion Poljud — Hajduk Split, Split (capacity ~33,987). Record HNL attendance: 38,000 for a Dinamo vs Hajduk match.
- Not yet cross-checked against FL26's default list — pending Asset Inventory pass. Maksimir and Poljud are among the most recognisable grounds in the Balkans; community stadium packs likely exist for both.

**Kits/badges:** Not yet sourced — pending your input on existing assets. Dinamo and Hajduk are well-known clubs with widely available kit packs.

---

---

### 7. Poland — Ekstraklasa ✅

**Tier & size:** Top tier, **18 clubs** — the largest league in our entire expansion pack alongside Romania. Also the most historically deep, with the 2025–26 season being the **100th season of the Polish Football Championship**.

**2025–26 clubs (18 confirmed):**
Lech Poznań, Jagiellonia Białystok, Górnik Zabrze, Legia Warsaw, Raków Częstochowa, Pogoń Szczecin, Zagłębie Lubin, Widzew Łódź, Cracovia, GKS Katowice, Radomiak Radom, Ruch Chorzów, Korona Kielce, Piast Gliwice, Wisła Płock, Arka Gdynia, Bruk-Bet Termalica Nieciecza, Lechia Gdańsk.
2025–26 champions: **Lech Poznań** (second consecutive title, their 10th overall).

**2026–27 clubs (confirmed changes for FL27 data):**
IN: Wisła Kraków (promoted after 4-year absence), Śląsk Wrocław (promoted after 1 year), Wieczysta Kraków (promoted for the first time in club history — will be in Ekstraklasa for the first time ever).
OUT: Bruk-Bet Termalica Nieciecza, Arka Gdynia, Lechia Gdańsk (all relegated).
⚠️ Notable: For 2026–27, Kraków will have **three clubs in the top flight** simultaneously (Wisła, Cracovia, Wieczysta) — the first time since 1994–95. This is historically significant and means the Kraków Holy War derby will be active again at Ekstraklasa level when FL27 launches.

**Season format:** Standard double round-robin — **34 matches per team**, 18 clubs × 17 opponents × 2 = 306 total league matches. No split format (they used one from 2013–2020 but reverted to a single table). Clean, straightforward engine implementation — the largest slot we'll need to fill but no format complications.

**Promotion/relegation:**
- Bottom three (16th, 17th, 18th) automatically relegated to I liga.
- I liga: Top two automatically promoted; 3rd–6th place enter a mini-playoff for a third promotion spot.
- 2nd tier: Betclic I liga (18 clubs, also double round-robin).

**Domestic cup:** Polish Cup (Puchar Polski).

**UEFA qualification:**
- Champion (1st) → Champions League qualifying.
- 2nd and 3rd → Conference League qualifying.
- Polish Cup winner → additional UEFA slot (typically ECL or EL depending on coefficient).
- If the Cup winner already qualified via league, the spot cascades down the table.
- Total: **1 CL + up to 3 ECL = roughly 4 UEFA slots.** Poland's coefficient is rising sharply — in 2025–26 four Polish clubs represented in major European competition simultaneously for the first time since 2002–03, and Jagiellonia Białystok and Legia Warsaw both reached Conference League quarter-finals.

**Derbies to include:**
- **Derby of Poland: Legia Warsaw vs Lech Poznań** — the headline national rivalry. Poland's two most successful clubs from rival cities (Warsaw vs Poznań), each representing contrasting identities. Notoriously violent fixture history; flares on pitch, multiple bans. Both clubs consistently in Ekstraklasa.
- **Święta Wojna (Holy War): Wisła Kraków vs Cracovia** — considered the fiercest and oldest derby in Poland, first contested in 1908. 200+ official encounters. Described as one of the most intense in Central Europe. Deeply rooted in Kraków's cultural and social history. ✅ **Both clubs are confirmed in 2026–27 Ekstraklasa** — actively wire this at maximum intensity.
- **Great Silesian Derby: Górnik Zabrze vs Ruch Chorzów** — most frequently contested Polish derby (120+ official matches). Upper Silesian regional identity, mining community roots. Both clubs in 2025–26; verify Ruch's status for 2026–27 before wiring.
- **Łódź Derby: ŁKS Łódź vs Widzew Łódź** — fierce central-Poland industrial rivalry. Check both clubs' divisional status for 2026–27 before wiring (ŁKS currently in I liga).
- ⚠️ Wieczysta Kraków's first-ever Ekstraklasa season in 2026–27 will create a brand-new derby dynamic with both Wisła and Cracovia in the same city. Worth noting for atmosphere/rival assignment even if Wieczysta has no historic rivalry weight yet.

**Stadiums:**
- Stadion Wojska Polskiego (Polish Army Stadium) — Legia Warsaw (~31,800 cap).
- INEA Stadion — Lech Poznań (~41,609 cap, largest stadium in our entire expansion pack and one of the biggest in Central Europe).
- Synerise Arena Kraków — Wisła Kraków (~33,130).
- Not yet cross-checked against FL26's default list — pending Asset Inventory pass.

**Kits/badges:** Not yet sourced — pending your input on existing assets. Legia and Lech are well-known internationally; community kit packs widely available. Wisła Kraków kits should also be findable.

---

---

### 8. Czech Republic — Chance Liga (Czech First League) ✅

**Tier & size:** Top tier, **16 clubs**. One of the strongest leagues in our expansion pack by UEFA coefficient — Czech Republic currently ranked **10th in Europe** out of 55 associations.

**2025–26 clubs (16 confirmed):**
Slavia Prague, Sparta Prague, Viktoria Plzeň, Baník Ostrava, Sigma Olomouc, Bohemians 1905, Mladá Boleslav, FK Jablonec, Slovan Liberec, Slovácko, FK Zbrojovka Brno, Dukla Prague, MFK Karviná, FC Fastav Zlín, and others.
2025–26 champions: **Slavia Prague** (consecutive title; also current titleholders heading into 2026–27).

**2026–27 clubs (confirmed changes):**
- IN: FC Zbrojovka Brno (2025–26 second division champions, returning after 3-year absence).
- OUT: FK Dukla Prague (relegated to second division).
- ⚠️ **MFK Karviná — administrative relegation:** On 15 June 2026, Karviná were administratively relegated by the Czech FA Ethics Committee for alleged match-fixing, despite having won the 2025–26 Czech Cup. They announced an appeal — if confirmed before the season starts, another club replaces them; if not resolved in time, the 2026–27 league runs with only **15 teams**. Monitor this situation before implementing — it directly affects slot count.

**Season format:** ⚠️ **SPLIT FORMAT — third instance in our pack.**
- Regular season: double round-robin = **30 matches** per team.
- Then table splits into **three groups:**
  - Championship group (positions 1–6): single round-robin of 5 extra matches, carrying points forward. Compete for title and European spots.
  - Middle/Placement group (positions 7–12): single round-robin of 5 extra matches.
  - Relegation group (positions 13–16): single round-robin of 3 extra matches. 16th directly relegated; 14th and 15th enter play-outs.
- Total matches for top teams: ~35 per club.

Same engine limitation as Finland and Serbia. **Implement as straight 30-match double round-robin.** The championship/placement/relegation group phase cannot be natively replicated in PES. This is now a confirmed pattern across 3 of our 8 researched leagues — worth adding to the master limitations section.

**Promotion/relegation:**
- 16th place automatically relegated to Czech National Football League (second tier).
- 14th and 15th place enter two-legged play-outs against 2nd and 3rd from the second division.
- Second division champion is automatically promoted.
- 2nd tier: Chance Národní Liga (Czech National Football League), 16 clubs.

**Domestic cup:** Czech Cup (Pohár FAČR / MOL Cup). Cup winner qualifies for ECL qualifying rounds.

**UEFA qualification:**
- Champion → Champions League second qualifying round.
- Runner-up → Europa League qualifying.
- 3rd place → Conference League qualifying.
- Cup winner → additional ECL qualifying slot (cascades if already qualified via league).
- Total: roughly **1 CL + 1 EL + 1–2 ECL = 3–4 UEFA slots.** Exact stages depend on coefficient ranking at time of implementation — Czech Republic's 10th position gives strong entry points.

**Derbies to include:**
- **Prague Derby (Pražské derby / Derby pražských S): Sparta Prague vs Slavia Prague** — the standout fixture of Czech football and one of Central Europe's defining rivalries. First played 29 March 1896 — over 300 competitive encounters. Often compared to the Scottish Old Firm in terms of cultural weight. Sparta (working class identity, red strip, historically right-leaning fanbase) vs Slavia (academic/bourgeois roots, red-and-white, left-leaning). Both founded in the 1890s less than 1km apart in Prague.
  ⚠️ **Live context (May 2026):** In their most recent derby, Slavia fans stormed the pitch in the 97th minute (Slavia leading 3–2) and attacked multiple Sparta players. Match abandoned. Slavia's North Stand closed indefinitely, two Slavia players (including top scorer Tomáš Chorý) suspended for the rest of the season and transfer-listed. Disciplinary proceedings ongoing. This is the most intense active situation of any derby in our entire pack — maximum rival weight absolutely justified.
- **Sparta vs Baník Ostrava** — secondary rivalry, Prague vs the industrial north-east. Worth including as a lower-weight rival pair.
- ⚠️ Bohemians 1905 (the "Kangaroo" club) have minor derby standing with both Prague clubs — notable for atmosphere, lower intensity than the main Prague derby.

**Stadiums:**
- Epet Arena (Eden Arena) — Slavia Prague, Prague (~19,370 cap).
- Fortuna Arena (Letná) — Sparta Prague, Prague (~18,887 cap).
- Doosan Arena — Viktoria Plzeň, Plzeň (~11,700 cap).
- Not yet cross-checked against FL26's default list — pending Asset Inventory pass. Both Prague stadiums are modern, well-documented, and community stadium packs likely exist.

**Kits/badges:** Not yet sourced. Slavia, Sparta and Plzeň are all UEFA-regulars — kit packs widely available in the PES/FL community.

---

*(Leagues 9–12 to be added one at a time, same format, as we work through the list.)*
