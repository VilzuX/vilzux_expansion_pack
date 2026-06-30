# VilzuX Expansion Pack — Master Planning Document

**Base:** Football Life 2026 (FL26) — currently in research/prototype phase. Final database implementation deferred to FL27 (expected ~Oct 2026, unconfirmed — watch SmokePatch's site).
**Last updated:** 2026-06-20

---

## Open decisions (pending your input — update this section as you decide)

- [ ] Sandbox FL26 copy set up for safe testing, separate from your main install?
- [ ] Existing kit/badge/logo assets for any of the 12 leagues — which, if any?
- [x] Round-robin formats → **decided by precedent**: every non-standard format encountered (10 of 11 leagues) has been approximated as a straight double round-robin throughout this document. Flag now if you want to revisit this for any specific league before we move to DB wiring.
- [ ] Roster accuracy target — exact current 2026 table, or "close enough" if a specific club is hard to source?

---

## Known engine limitations to design around

**Format limitations — final tally across all 11 researched leagues:**

1. **Split-season formats (5 of 11 leagues): Finland, Serbia, Czech Republic, Slovakia, Romania.** Regular season followed by a mid-season table split into championship/relegation groups, with points carried forward (often halved/rounded). PES's competition engine is built around fixed round-robin or group+knockout — a mid-season table split is not natively supported. **Standing rule: implement all five as a straight double round-robin**, using just the regular-season fixture count (drop the extra group-stage matches). This is now the majority pattern in our pack, not an exception — treat it as a default, not a per-league judgment call.
2. **Quadruple round-robin (2 of 11 leagues): Croatia, Slovenia.** Both are our smallest leagues (10 clubs each) and independently arrived at the same fix for a thin domestic pool — each pair of clubs meets 4 times (36 matches/team) instead of 2. **Standing rule: implement as a standard double round-robin (18 matches/team)**, accepting the reduced fixture count.
3. **Asymmetric triple round-robin (1 of 11 leagues): Hungary.** Each pair of clubs meets 3 times, with the third match's venue dynamically assigned based on which stadium hosted the second — producing an uneven home/away split per pairing (33 matches/team total). The most structurally unusual format in the pack; no native engine support exists for this anywhere we're aware of. **Standing rule: implement as a standard double round-robin (22 matches/team).**
4. **Leagues needing no format workaround at all (3 of 11): Sweden, Norway, Poland.** Clean double round-robin natively. These are the simplest implementations in the whole pack and good candidates for an early pilot if you want a confidence-building win before tackling a split-format league.

**Other limitations:**

5. **Competition menu fragility.** SmokePatch's own FL25 release notes mention a newly-added league being pulled from the menu "due to multiple issues" until it could be re-added safely. Treat any new competition slot as fragile until heavily tested.
6. **Continental competition format.** FL26 still uses the pre-2024 group-stage + knockout UEFA format, not the real-world Swiss league-phase model. Our Conference League build should target old-format realism, not a Swiss-model emulation.
7. **Database edits are unsupported by SmokePatch.** They may be overwritten by future updates. Always keep backups; expect to redo ID bindings after major version changes (e.g. FL26 → FL27).
8. **Roster/roster-adjacent uncertainty flagged during research — reconfirm closer to FL27 launch:** Serbia's 16→14 team contraction; Czech Republic's Karviná match-fixing appeal (15 vs 16 teams); Slovakia's exact 2026–27 relegation picture; Slovenia's Domžale mid-season dissolution and unconfirmed replacement; Romania's exact relegation/play-off cutoffs in the bottom group; Hungary's exact 2026–27 bottom-two relegation.
9. **Branding/naming flag:** Romania's FCSB carries an active, recently-resolved-against-them legal dispute over use of the "Steaua" name and history (CSA Steaua București is a separate legal entity). Use "FCSB" branding for the current club; verify any downloaded asset pack isn't using outdated "Steaua" naming by accident.

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
| 9 | Niké Liga | Slovakia | ✅ | ⏳ (post-FL27) | ⏳ | ⏳ | Research complete |
| 10 | PrvaLiga | Slovenia | ✅ | ⏳ (post-FL27) | ⏳ | ⏳ | Research complete |
| 11 | SuperLiga | Romania | ✅ | ⏳ (post-FL27) | ⏳ | ⏳ | Research complete |
| 12 | NB I | Hungary | ✅ | ⏳ (post-FL27) | ⏳ | ⏳ | Research complete |

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

---

### 9. Slovakia — Niké Liga (Slovak First Football League) ✅

**Tier & size:** Top tier, **12 clubs**. Format unchanged since the 2017–18 season.

**2025–26 season:** Champions were **Slovan Bratislava** — their 8th consecutive Niké Liga title (24th Slovak title overall, counting both pre-war/Czechoslovak-era and modern titles). Slovan are historically significant beyond domestic football: they're the only Slovak (or former Czechoslovak) club ever to win a European trophy, lifting the 1969 European Cup Winners' Cup against Barcelona.

**2026–27 clubs (confirmed changes):**
- IN: Dukla Banská Bystrica (2. Liga champions, automatically promoted, returning after a 1-season absence).
- OUT: Tatran Prešov (relegated — had only just returned to the top flight in 2025–26 after a 7-season absence, went straight back down).
- ⚠️ The exact mechanics of the final relegation/play-off picture for 2025–26 involve a dramatic final-day match between Tatran Prešov and Komárno (1–0, with a 92nd-minute equalizer disallowed). Komárno appear to have retained their top-flight place via the standard play-off route. Treat this as broadly reliable but **reconfirm the exact final 2026–27 roster closer to FL27 launch** — this is exactly the kind of granular mid-table detail worth double-checking against a primary source before locking in team IDs.

**Season format: ⚠️ SPLIT FORMAT — fourth instance in our pack** (after Finland, Serbia, Czech Republic).
- Regular season: double round-robin, all 12 teams play each other home and away = **22 matches** per team.
- Table then splits into a **Championship Group (top 6)** and a **Relegation Group (bottom 6)**, each playing the other 5 teams in their group home and away = **10 more matches**, points carried forward.
- Total: ~32 matches per club.
- Same engine limitation as the other three split-format leagues. **Implement as a straight 22-match double round-robin.** This is now confirmed in 4 of 9 researched leagues so far — strongly suggests the split-round-robin approximation should just be treated as a standing rule for this whole project rather than a per-league exception.

**Promotion/relegation:**
- Bottom-placed team in the Relegation Group (12th overall) automatically relegated.
- 11th-placed team enters a two-legged play-off against the 2nd-placed team from the 2. Liga (2nd tier) for the final spot.
- 2. Liga champion is automatically promoted.
- 2nd tier: **2. Liga** (Slovak second division).

**Domestic cup:** Slovak Cup (Slovenský pohár).

**UEFA qualification:**
- Champion → Champions League qualifying.
- 2nd and 3rd place → Conference League qualifying.
- Slovak Cup winner → Conference League qualifying (cascades to 4th place if the cup winner already qualified via league position).
- Total: **1 CL + 3 ECL = 4 UEFA slots.**
- Slovakia's UEFA coefficient currently sits in the low-20s among European leagues (reconfirm exact ranking closer to implementation), built largely on Slovan Bratislava's recent run of consistent European participation, including a Champions League league-phase campaign.

**Derbies to include:**
- **Tradičné derby (Traditional Derby / West-Slovakia Derby): Slovan Bratislava vs Spartak Trnava** — the marquee fixture, explicitly described as the most prestigious match in the Slovak football calendar, between the two most successful clubs in the country's history. History of serious incidents: a 2021 pitch invasion and fight between both clubs' ultras groups led to the match being abandoned, a multi-game fan ban for Trnava, and a heavy fine for Slovan; an earlier 2009 fixture was played behind closed doors following a pyrotechnics incident. Maximum rival weight justified.
- **Slovan Bratislava vs DAC Dunajská Streda** — per Slovan's own club records, this is considered the second most prestigious fixture in Slovak football after the Traditional Derby. Worth noting for context: DAC represents the Hungarian-speaking minority region of southern Slovakia and has strong ties to Hungarian club Ferencváros — a meaningful identity/regional dimension worth being aware of, separate from matchday rivalry intensity.
- ⚠️ Secondary regional derbies exist (e.g. a Mid-Slovakian derby involving Dukla Banská Bystrica vs Žilina, an historic East-Slovakian derby between Tatran Prešov and MFK Košice) but **most sourcing for these is outdated or the clubs' current divisional status is uncertain** — Tatran Prešov specifically is confirmed relegated for 2026–27, so that derby would not be active in the top flight. Re-verify current rosters before wiring any of these secondary rivalries.

**Stadiums:**
- Tehelné pole — Slovan Bratislava, Bratislava (~22,500 cap, largest in the league).
- Štadión Antona Malatinského — Spartak Trnava, Trnava (~18,200 cap).
- MOL Aréna — DAC Dunajská Streda, Dunajská Streda (~12,700 cap).
- Not yet cross-checked against FL26's default list — pending Asset Inventory pass.

**Kits/badges:** Not yet sourced — pending your input on existing assets. Slovan Bratislava, as Slovakia's most recognisable club, likely has community kit packs available; smaller clubs may require more searching.

---

---

### 10. Slovenia — PrvaLiga (Prva liga Telemach) ✅

**Tier & size:** Top tier, **10 clubs**. Established 1991 after Slovenian independence from Yugoslavia.

**2025–26 season:** **Celje** won their third PrvaLiga title, beating defending champions Olimpija Ljubljana (who had just won their fourth title the season before). As champions, Celje qualify for the second qualifying round of the 2026–27 Champions League.

⚠️ **MAJOR DISRUPTION — mid-season club dissolution:** Two-time former champions **Domžale withdrew from the league after 18 rounds during the 2025–26 season due to financial insolvency and were subsequently dissolved.** This is a serious structural event — a founding-era club going under mid-competition. It closely echoes the fate of the *original* NK Olimpija, which also dissolved due to financial collapse in 2005 (see Eternal Derby note below) — financial instability has precedent at the top of Slovenian football.

**2026–27 roster uncertainty:** I have **not been able to confirm** which club fills Domžale's vacated slot for 2026–27 — this is exactly the kind of detail I won't guess at per your project rules. What's confirmed: Aluminij and Primorje were *already* promoted into the 2025–26 season (replacing relegated Nafta 1903 and Rogaška) — that's a separate, already-resolved transition. The *Domžale* replacement is a distinct, more recent question that needs reconfirming closer to FL27 launch from a primary source (Slovenian FA or PrvaLiga official site).

**Season format: ⚠️ QUADRUPLE ROUND-ROBIN — second instance in our pack (after Croatia).**
Each of the 10 clubs plays every other club **four times** (twice home, twice away) = **36 matches per team**, 180 total league matches. This format has been in place since 2005 specifically because the league is so small (10 clubs) — same underlying reason as Croatia's HNL.

Same engine limitation as Croatia: PES's competition engine supports double round-robin natively, not quadruple. **Recommended implementation: standard double round-robin (18 matches per team)**, same approach as Croatia. Worth noting as a *pattern*: both of our two smallest leagues (Croatia and Slovenia, 10 clubs each) independently arrived at the same quadruple-fixture solution to a thin domestic player pool — useful context, not just a coincidence to dismiss.

**Promotion/relegation:**
- Bottom-placed team (10th) automatically relegated.
- 9th-placed team enters a two-legged play-off against the runner-up of the 2. SNL (second tier) — winner plays PrvaLiga next season.
- 2. SNL champion is automatically promoted.
- 2nd tier: 2. SNL (Slovenian Second League).

**Domestic cup:** Slovenian Football Cup (Pokal Slovenije).

**UEFA qualification:**
- Champion → Champions League qualifying. ⚠️ Entry round has shifted recently: the 2024–25 champion (Olimpija) entered at the **first** qualifying round, but the 2025–26 champion (Celje) enters at the **second** qualifying round for 2026–27 — suggesting Slovenia's coefficient is improving. Reconfirm the exact entry round at implementation time rather than assuming it's fixed.
- Runner-up and 3rd place → Conference League second qualifying round.
- Slovenian Cup winner → Conference League second qualifying round (cascades to next-best unqualified league team if the cup winner already qualified via league position).
- Total: **1 CL + up to 3 ECL = up to 4 UEFA slots.**
- Slovenia's UEFA coefficient ranking sits around 22nd in Europe per recent figures (worth reconfirming closer to implementation, as these shift yearly) — modest but meaningfully ahead of where it sat a decade ago, boosted by recent European qualifying runs from Celje and Olimpija.

**Derbies to include:**
- **Večni derbi (Eternal Derby): NK Maribor vs NK Olimpija Ljubljana** — the unambiguous headline fixture, dating to 1962 in the Yugoslav era. Geographic/cultural framing: Ljubljana (capital, traditionally wealthier, west) vs Maribor (industrial Styria region, traditionally working-class, east) — a divide that has faded somewhat in recent decades but still colors the rivalry's identity. Maribor's ultras are **Viole Maribor**; Olimpija's are the **Green Dragons**. Real history of serious incidents, including a fan stabbing after a match in 2010 (no football-related fatalities in Slovenia to date). 
  ⚠️ Important continuity note: the *original* Olimpija dissolved due to financial collapse in 2005; a phoenix club (eventually renamed NK Olimpija Ljubljana) was founded weeks later, inherited the fanbase and ultras, and is broadly treated as the rivalry's continuation by media and fans — though not the legal successor per the Slovenian FA. Worth knowing this context even though, practically, the in-game derby just needs "Maribor vs Olimpija Ljubljana" wired at maximum rival weight.
- **Štajerski derbi (Styrian derby): Maribor vs Celje** — regional rivalry between Styria's two clubs, sharpened by Celje's current champion status (2025–26) directly denying Maribor the title race.
- **Štajirsko-prekmurski derbi (Styria–Prekmurje derby): Maribor vs Mura** — regional rivalry with a recent serious incident: in 2024, a stun grenade thrown by a Maribor ultra injured six Mura players and a teenage ball boy, resulting in a €25,000 fine, the match awarded 3–0 to Mura, and a four-match stadium closure for Maribor. Worth including as an active, currently-tense rivalry.

**Stadiums:**
- Stožice Stadium — Olimpija Ljubljana, Ljubljana (~16,000 cap, largest in the league; also hosts the Slovenia national team).
- Ljudski vrt — Maribor, Maribor.
- Not yet cross-checked against FL26's default stadium list — pending Asset Inventory pass.

**Kits/badges:** Not yet sourced — pending your input on existing assets. Maribor and Olimpija are the most internationally visible Slovenian clubs (both have played UEFA group-stage football); kit packs for them are more likely to already exist in the community than for the smaller clubs.

---

---

### 11. Romania — SuperLiga (Liga I) ✅

**Tier & size:** Top tier, **16 clubs**, the largest league in our pack alongside Poland. Established 1909 — one of the oldest national competitions in our entire list. Currently ranked **25th in UEFA's league coefficient standings** (consistent across two independent sources).

**2025–26 season result:** **Universitatea Craiova** won the title — their first in **35 years** — and also won the Cupa României (Romanian Cup), completing a double. FCSB had been two-time defending champions entering the season.

**2026–27 roster:** 16 teams = 13 returning + 2 promoted directly from Liga II + 1 promoted via play-off (Csíkszereda Miercurea Ciuc confirmed as one of the promoted sides). Exact full 16-club list for 2026-27 not yet compiled — straightforward to pull from LPF's official site closer to implementation.

⚠️ **CRITICAL BRANDING/NAMING ISSUE — verify before any club-naming or badge work:**
Bucharest's most successful club operates under serious, currently-unresolved legal disputes over its name and history:
- **FCSB** (the club playing in Liga I right now, owned by Gigi Becali) was formerly called "Steaua București" but lost the legal right to that name in 2014.
- **CSA Steaua București** is a separate, legally distinct club that the Romanian courts have recognized as the rightful holder of the original Steaua identity and honours (including the 1986 European Cup win).
- **This is not settled history — it's an active legal case.** A Constitutional Court verdict came down around 1 April 2026, and FCSB **lost** that case, exhausting national legal remedies; the club's owner has stated intent to escalate to the European Court of Human Rights.
- Practical implication for the mod: **the club currently in SuperLiga must be represented and named as "FCSB"**, not "Steaua," to reflect the current legal and competitive reality — even though most kit packs, badges, and older PES/FL community assets may still be labeled "Steaua" from years before the renaming. Double-check any asset pack's naming before importing it.

**Season format: ⚠️ SPLIT FORMAT — fifth instance in our pack** (after Finland, Serbia, Czech Republic, Slovakia).
- Regular season: double round-robin, 16 teams × 15 opponents × 2 = **30 matches per team**.
- Table then splits:
  - **Championship group (top 6):** round-robin against each other twice more (10 matches), points from the regular season halved and rounded up, carried forward. Decides the champion and UEFA qualification places. Final standings = overall positions 1–6.
  - **Relegation group/play-out (bottom 10):** single round-robin among themselves (9 matches), also with halved/rounded points carried forward. Final standings = overall positions 7–16.
- ⚠️ The exact relegation cutoffs and play-off mechanics within the bottom group are described slightly inconsistently across my sources (some figures suggest direct relegation happens around positions 9–10 overall, others suggest it's the bottom of the 10-team group specifically, i.e. positions 15–16). There's also an unusual extra mechanism: the top two finishers within the relegation group reportedly get a shot at one more Conference League berth via a special play-off. **Don't lock in the exact relegation/play-off numbers until cross-checked against LPF's official regulations** — this is more an example of the rule being genuinely intricate than of me being unable to find it.
- Same engine limitation as the other four split-format leagues. **Implement as a straight 30-match double round-robin.** This is now the majority pattern across our 11 leagues (5 of 11 use a split format) — strongly reinforces treating round-robin approximation as a standing project-wide rule rather than a per-league judgment call.

**Promotion/relegation:** 2nd tier is **Liga II**. Bottom of the relegation/play-out group drops down; some mid-table sides in that group face two-legged play-offs against Liga II's top finishers. (See verification flag above before finalizing exact numbers.)

**Domestic cup:** Cupa României.

**UEFA qualification:**
- Champion → Champions League second qualifying round.
- Cup winner → Europa League first qualifying round (cascades to the next-best unqualified league side if the cup winner already qualified via league position — exactly what happened in 2025–26, since Craiova won both).
- Runner-up → Conference League qualifying (exact round varies by source; reconfirm before implementation).
- 3rd place → Conference League qualifying.
- Possible additional ECL berth via the relegation-group play-off winner (see format note above) — an unusual feature worth knowing about even if not modeled directly.
- Total: roughly **1 CL + 1 EL + 2–3 ECL = 4–5 UEFA slots.**
- ⚠️ Licensing caveat: in 2025–26, **UTA Arad and Oțelul Galați were ineligible for European play-off spots because they lacked a UEFA license**, despite results — a real-world constraint that doesn't need modeling in-game, but good context for why final tables and European participants don't always match perfectly.

**Derbies to include:**
- **Eternul derby (Eternal Derby): FCSB vs Dinamo București** — the headline fixture, first played 1948, 190+ official meetings. Rooted in a Cold War-era institutional rivalry: FCSB's predecessor represented the Romanian Army, Dinamo represented the Ministry of Internal Affairs (police/security services) — a genuine police-vs-army rivalry baked into the clubs' DNA. Regularly marred by serious hooliganism. Maximum rival weight justified — this is comparable in stature to the Red Star/Partizan and Sparta/Slavia fixtures already logged for this pack.
- **FCSB vs Rapid București** — the second-most significant Bucharest rivalry, 140+ meetings, intensified further by a 2005-06 UEFA Cup all-Romanian clash.
- **Dinamo vs Rapid București** — third leg of Bucharest's three-way club rivalry triangle (FCSB / Dinamo / Rapid), rooted in Rapid's pre-communist, railway-workers identity versus Dinamo's post-1948 state-security origin.
- ⚠️ Note Bucharest functions like Stockholm/Gothenburg in our Sweden dossier — three major clubs sharing a city creates a genuine rivalry web, not just one isolated derby. Worth wiring all three relationships rather than just the headline fixture, if the engine's rivalry slots allow it.

**Stadiums:**
- Arena Națională — FCSB's home ground, ~55,634 capacity, the largest stadium in our entire 11-league pack.
- Stadionul Dinamo (Ștefan cel Mare) — Dinamo's traditional home, though the club has been using Arena Națională for major fixtures amid ongoing renovations — verify current matchday venue before implementation.
- Not yet cross-checked against FL26's default stadium list — pending Asset Inventory pass.

**Kits/badges:** Not yet sourced. ⚠️ Given the FCSB/Steaua naming dispute above, **explicitly verify any downloaded kit/badge pack uses current "FCSB" branding** rather than outdated "Steaua" branding, unless you deliberately want the historical identity for flavor reasons — your call, but it should be a deliberate choice, not an accident from using an old asset pack.

---

---

### 12. Hungary — NB I (Nemzeti Bajnokság I / OTP Bank Liga) ✅

**Tier & size:** Top tier, **12 clubs**, 127th season as of 2025–26 — one of the oldest leagues in our entire pack.

**2025–26 season result:** **ETO FC Győr won their 5th national title**, ending **Ferencváros's 7-year (7-title) reign** as champions — confirmed directly: Ferencváros finished runner-up in 2025–26. Ferencváros did, however, win the **Magyar Kupa** (Hungarian Cup), beating Zalaegerszeg 1–0 on 9 May 2026, and had a genuinely strong European campaign that season — reaching the Europa League quarter-finals before losing to Braga. Worth knowing: Ferencváros's title streak being broken is the headline story of this league's season, similar in significance to Craiova's 35-year wait in Romania or Celje's win in Slovenia.

**2026–27 roster:** Confirmed for the *2025–26* season (i.e. one cycle back from FL27's likely launch data): Kisvárda and Kazincbarcika promoted, replacing Fehérvár (relegated after 25 years in the top flight) and Kecskemét (after 3 years). I have **not confirmed** which two clubs finish bottom of 2025–26 to determine the actual 2026–27 roster — flagging for verification closer to FL27 launch rather than guessing.

⚠️ **Notable infrastructure quirk:** Kazincbarcika's own stadium doesn't meet NB I's facility requirements, so for 2025–26 they ground-shared — playing "home" games at Mezőkövesd for the first 18 rounds, then at Diósgyőri Stadion in Miskolc for the rest. Worth keeping in mind for the stadium-assignment phase: not every club's "home ground" in real life is actually their own — some smaller-league clubs play designated home matches at a borrowed venue, which is a small but real authenticity detail.

**Season format: ⚠️ NEW ENGINE LIMITATION — sixth pattern type, and the most structurally unusual one yet.**
NB I doesn't use a clean round-robin multiple at all. Each of the 12 clubs plays every other club **three times**: once at each club's home ground, and then a **third match played at whichever of the two stadiums did *not* host the second match** — i.e. the venue for match 3 is determined dynamically by the sequence of the first two, producing an inherently asymmetric home/away split per pairing (one club nets 2 home games against a given rival, the other only 1, presumably alternating fairness across seasons). Total: 33 matches per team.

This is structurally distinct from both limitations found earlier: it's not a clean even multiple like Croatia/Slovenia's quadruple round-robin, and it's not a mid-season table split like the five split-format leagues. It's an odd-numbered, dynamically-assigned-venue format that **no engine I'm aware of, including PES/Sider's most flexible scheduling tools, can natively replicate.** 

**Recommended implementation: standard double round-robin (22 matches per team)** — same fallback principle applied to every other format anomaly in this project. This keeps the whole 11-league pack internally consistent and stable.

**Promotion/relegation:** Refreshingly simple compared to several other leagues in this pack — **no split, no play-off chain.** Bottom two clubs are relegated directly to Nemzeti Bajnokság II; NB II's champion and runner-up are promoted directly in return. 2nd tier: Nemzeti Bajnokság II.

**Domestic cup:** Magyar Kupa (Hungarian Cup).

**UEFA qualification:**
- Champion → Champions League qualifying.
- Runner-up and 3rd place → Conference League qualifying.
- Magyar Kupa winner → Europa League qualifying (cascades down if the cup winner already qualified via league position — exactly what happened this cycle, since Ferencváros were both cup winners *and* league runners-up, so they take the better EL slot and the ECL spot they'd otherwise have held passes to 4th place).
- Total: roughly **1 CL + 1 EL + up to 2 ECL = 4 UEFA slots.**

**Derbies to include:**
- **The Derby (Derbi): Ferencváros vs Újpest** — Hungary's biggest, most intense rivalry, **120+ years old** (first played 1905). Deep social roots: Ferencváros founded by Christian Swabian immigrants with strong working-class/national identity; Újpest founded by a Jewish-Hungarian industrialist and historically tied to Budapest's Jewish community — a genuine ethnic/religious dimension layered onto the football rivalry, later complicated further by Communist-era politics (Újpest renamed "Újpesti Dózsa," administered by the Ministry of Interior; Ferencváros seen as the club of political opposition). Matches feature large-scale tifo choreography, pyrotechnics, and heavy policing — Budapest's metro authority runs dedicated police-controlled service on derby days. Ferencváros currently dominant (16 consecutive derby wins as of the most recent confirmed streak). Maximum rival weight justified — comparable in cultural weight to the other "marquee" derbies already logged across this pack (Belgrade, Zagreb, Prague).
- **Örökrangadó (Eternal Derby): Ferencváros vs MTK Budapest** — actually Hungary's *oldest* top-flight rivalry, predating the Derby by decades; the two clubs jointly monopolized the league 1904–1930. Both clubs confirmed currently in NB I — safe to wire in alongside the Derby, though MTK is no longer the football powerhouse it once was, so treat this as a historically rich but currently secondary rivalry rather than co-equal with Ferencváros–Újpest.
- ⚠️ Other regional rivalries exist (Debreceni VSC vs Diósgyőri VTK in eastern Hungary; the Fejér County derby between Fehérvár and Puskás Akadémia) but **need current divisional verification** — notably, **Fehérvár was just relegated** after 25 years in NB I, meaning the Fejér County derby is **not currently active at top-flight level** for the 2025–26/2026–27 cycle. Don't wire it in without rechecking, same caution applied to similar cases in Sweden and Slovakia.

**Stadiums:**
- Groupama Aréna — Ferencváros, Budapest (built on/near the historic Üllői út site).
- Szusza Ferenc Stadion — Újpest, Budapest.
- Not yet cross-checked against FL26's default stadium list — pending Asset Inventory pass.

**Kits/badges:** Not yet sourced — pending your input on existing assets. Ferencváros, as Hungary's most internationally recognized club (regular European qualifier with a deep 2025–26 Europa League run), is the most likely to already have community kit packs available.

---

## ✅ All 11 league dossiers complete (Denmark excluded — already in FL26)

This closes out the research phase you asked to prioritize "now." Every league has a documented season format, promotion/relegation chain, domestic cup, UEFA qualification path, derby list, and stadium starting point — all version-agnostic, all still valid no matter what FL27's eventual database looks like.
