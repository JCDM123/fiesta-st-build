# Fiesta ST Head Unit Build — Master Cutting List (v2)

2017 Fiesta ST (Sony panel, Sync 1 + factory sat nav, factory reverse camera) + C5 Android unit (8-core, 8G+256G, 1280x720, wireless CarPlay/AA, 4G slot unused, AHD 1080p camera)

Repo: github.com/JCDM123/fiesta-st-build

---

## 1. Shopping / hardware
- [x] C5 head unit — ordered, shipping
- [x] Fakra Z to RCA adapter pair — ordered
- [ ] Samsung SmartTag2 — theft tracker, hide deep in car (can do any time)
- [ ] Slim 4-port USB 2.0 squid/pigtail hub — dash cavity port expansion (with camera-era shopping)
- [ ] 64GB high-endurance USB stick or SD — DVR loop storage (when dashcam goes live)
- [ ] USB-C OTG adapter for A56 — wired RealDash audition (optional)
- [ ] External 3.5mm mic — ONLY if inbuilt fails the Signal call test (A-pillar, ear height; unit takes one mic OR the other)
- [x] Bench power — 12V wall brick from his collection (SCA charger FAILED multimeter check: probing output, 16V spikes — never direct). Verify brick steady 12V + polarity before unit connects
- Ruled out: TPMS kit, SIM plan (slot empty), FORScan Lite on unit, boot password

## 2. Before the old unit comes out
- [ ] Final TPMS baseline reset through the Sync 1 menu at correct pressures — LAST act before removal (reset lives in Sync screen; succession = canbus Car Settings app if present, else FORScan via OBD junction)
- [ ] Check A56 Settings > Safety and emergency for SOS/crash features (Emergency Assistance retires with Sync)

## 3. Arrival day (box on the floor)
- [ ] Film the unboxing start to finish (dispute evidence)
- [ ] Photograph: unit label (verify 8G+256G), canbus box brand label, every connector face + profile, fascia, camera, USB tails, mic, paperwork
- [ ] Check for external mic in box; note MIC tail plug type
- [ ] Measure camera barrel dimensions
- [ ] Upload photos to repo → custom install guide gets written

## 4. Bench era (maximal build — ~90% of system before install)
- [ ] Power on bench (12V brick, B+ + ACC twisted to +, GND to −); rest unit on box foam
- [ ] Factory menu (Car Settings > Factory, pwd 000000): confirm Ford Fiesta in CarType list for shipped canbus brand
- [ ] Photograph firmware/MCU versions; ADB full backup BEFORE debloating; standing rule: NO OTA updates unless broken
- [ ] ADB package dump → debloat list + NetGuard whitelist written from it
- [ ] Guided menu screenshot walk (adb screencap) → menu atlas to repo
- [ ] Check Car Settings app for a TPMS/TPS reset entry (succession question)
- [ ] Camera bench test: picture, baked-in guide lines, mirroring — note snip loops; DVR settings: audio OFF, storage target
- [ ] Burner Google account; guest wifi; Private DNS; permissions audit
- [ ] NetGuard default-deny; whitelist: RealDash, Waze/Maps, FuelCheck, Syncthing (local), Signal, Claude, DMSS, streams
- [ ] Apps: Poweramp + music library via USB stick (copy to internal 256GB), Syncthing (music down / logs + dashcam clips + photos up), Signal linked (Molly if link refused; passphrase lock), Claude, AJN stream (sideload, lowest bitrate), FuelCheck P98, Waze/Maps, DMSS, FUTO keyboard + voice input, BOM radar / parking timer / traffic cams / Linkt buttons later
- [ ] Tasker + AutoInput: Signal voice-memo automation (press 1 = locked recording via slide-up gesture, press 2 = send; contact picked on screen) — build + teach coordinates on bench
- [ ] Dashcam snapshot button automation (DVR snapshot tap, or timestamp-marker + PC frame-extract fallback)
- [ ] RealDash: install, restore licence, load dashboards, set as launcher + autostart; custom ST boot logo (Factory menu, badge from repo)
- [ ] Wireless ADB + scrcpy paired with Lenovo (future maintenance = couch sessions; wireless debugging auto-offs on reboot)
- [ ] Driveway hybrid test: car's OBD port cabled to bench unit — RealDash reads live engine data pre-install
- [ ] Glovebox library: manuals/wiring/receipts as PDFs on unit

## 5. Install weekend (hardware only — brain arrives finished)
- [ ] Battery disconnect first → expect KAM relearn wobble after (known dance, not a fault)
- [ ] Dash strip; identify cable model A or B from back of Sync unit
- [ ] Wiring: quadlock (1), SKIP cable 2, radio antenna Fakra (3), old-screen feed (4), canbus box
- [ ] Label THREE aerial plugs with tape: radio antenna / reverse camera Fakra / factory GPS (leave GPS dormant — new puck on dash top)
- [ ] Factory reverse camera → Fakra-to-RCA adapter → unit camera input
- [ ] OBD junction: FORScan USB cable → quick-release joint at knee height, velcro anchor, strain relief on unit side
- [ ] USB allocation: tail 1 = OBD direct; tail 2 = squid hub (DVR stick + glovebox lead + spare) — hub later is fine
- [ ] Pod trimming: electronics proven FIRST, then cut internal ribs small, test fit, repeat
- [ ] Canbus init: Factory > CarType > canbus BRAND first, then Ford, then Fiesta
- [ ] Everything zip-tied, nothing hangs by its plug (bobcat suspension doctrine)
- [ ] Test: SWC + Sony panel keys (key-test screen), camera trigger on reverse (fallback pin 05), aircon popup, handbrake signal
- [ ] Audio sweep: balance + fader all four corners BEFORE trim goes back
- [ ] Old Sync unit + pod + screen BOXED forever (reversion + resale)
- [ ] One-line note to insurer

## 6. First weeks in car
- [ ] Signal call test at highway speed → inbuilt mic verdict (A-pillar external is the $10 fix)
- [ ] DSP/EQ session parked (driver-seat time alignment — sound quality lives here per owner reports)
- [ ] Signal Telecom toggle on A56 + Android Auto → Signal calls as real call cards
- [ ] Live with it; annoyance list = design session fuel

## 7. Interface build (designs = DRAFTS, style not locked yet — proper design sessions to come)
Page concepts (content firm, looks open): 0 Warm-up (coolant arc, music sync progress, guardian tile) / 1 Drive (dial + shift lights) / 2 Music / 3 Maps / 4 Data (sweep bar + cards) / 5 Performance (0-100, splits, G) / 6 Guardian (health, trends, watch list, weekly report synced back into car) / 7 Stats (records + history)
- [ ] Music + Maps concepts; full style direction session; enriched pass candidate (depth, glows, honeycomb) liked but unconfirmed
- [ ] Status-bar badges: warming (amber→green: coolant ≥85°C AND ~5 min runtime), ESP mode (ABS TC_SYS_STAT: white/amber/red), CRUISE (captures speed at engage — no cruise PIDs exist on this car)
- [ ] Smart cooldown overlay: handbrake + recent-load trigger, EXT.T falling + weighted countdown (no oil temp sensor on ST180)
- [ ] Low-fuel floating popup: FLI-triggered, amber 1/4 tank, red at factory light, range from real burn, one-tap cheapest 98 (treat indicated 0 as 0)
- [ ] Service bar cards: blue counting down → amber due soon → red OVERSHOT past interval
- [ ] Button map: wheel short/long press + Sony panel keys; long-press-mute menu trick noted
- [ ] Day/night skins auto-switch with headlights (canbus)
- [ ] Stretch: custom ABS PIDs (real G, steer angle, brake pressure, wheel speeds); custom parking graphic from LRI_DIST/LRO_DIST(mm) if canbus popup is poor
- Boost PID names CONFIRMED from harvest: MAP(kPa), BARO(kPa), EQ_RAT11, EQRAT11_CMD + TURBO_WGATE(%), TURBO_BYP_MES(%); GPS_SPEED/LAT/LONG also on bus

## 8. Front dashcam (someday afternoon)
- [ ] DECIDED: hidden windscreen mount behind mirror / beside City Stop shroud (audition both spots on live view) — dashcam only, no parking view needed (9 yrs, reverse parks)
- [ ] Keep clear of City Stop sensor window; cable up headliner + A-pillar
- [ ] Snip loops as needed (lines off, mirror correct); flip in software if hung upside down
- [ ] DVR loop to dedicated stick, G-sensor clip locking, audio OFF; locked clips auto-backup via Syncthing
- [ ] Snapshot button live

## 9. Guardian system (last phase — after logging proves reliable)
- [ ] RealDash logs → Syncthing → PC; weekly summariser → Claude API (2017 ST180, Stage 1, Sydney; odometer baselined live from TOTAL_DIST PID) → email
- [ ] Guardian page gets the weekly verdict synced back into the car
- [ ] Service tracker: oil km/months, plugs, fluids by age, timing BELT ~2027 (10 yr — belt/tensioner/water pump)
- [ ] Trend watch: trims drift, cold-start V + BATT_SOC, fuel economy (FLI), ACT heat
- [ ] Software TPMS: wheel-speed ratio trending flags a deflating corner
- [ ] Music-sync bridge widget; FuelCheck API card; TPMS-reset-via-ELM science project
- Future option (parked): 365-day prepaid SIM, NetGuard-restricted to guardian/tracking only

## 10. Connectivity + security (settled)
- Road: A56 hotspot (25GB) • Driveway: home GUEST wifi (strong password + client isolation) • Theft: SmartTag2 + Signal remote-unlink • SIM slot empty • No home address on device (landmark trick) • No boot password; Molly passphrase only • Wipe-safe: flash storage keeps everything through power loss; never cut power mid-reset/firmware-write

## 11. Still open
- [ ] Commit this file to repo (the one upload that matters)
- [ ] Music + Maps page concepts
- [ ] Next FORScan drive log: tick MAP, BARO, EQ_RAT11, TURBO_WGATE, TURBO_BYP_MES + one pull past 6000 RPM (harvest complete — no PID re-export needed)
- [ ] OEM vs Stage 1 back-to-back log (warm weather, flexible)
- [ ] Lufi future: Y-splitter vs honourable retirement once dash is live
- [ ] Next service: reseat purge hose end, trim long section
