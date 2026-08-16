# Fiesta ST Head Unit Build — Master Cutting List (v4)

2017 Fiesta ST (Sony panel, Sync 1 + factory sat nav, factory reverse camera) + C5 Android unit (8-core, 8G+256G, 1280x720, wireless CarPlay/AA, 4G slot unused, AHD 1080p camera)

Repo: github.com/JCDM123/fiesta-st-build — visual dash design lives in the repo renders; this sheet is the mechanical/build side.

---

## 1. Shopping / hardware
- [x] C5 head unit — customs cleared, expected early next week
- [x] Reverse camera cable — ARRIVED
- [x] Bench power — spare 12V 3.5A brick, meter-verified 12.4V true (42W headroom). Barrel tip cut, wires stripped, polarity re-verified and tape-marked
- [x] 256GB SSD in enclosure — already owned, mounting under the coin tray
- [ ] ALDI Mobile PAYG SIM ($2 starter, 365-day expiry, pay-as-you-go top-ups) — standard calls+SMS+data, NOT their dedicated data-only product, so the theft auto-call can use native dialling rather than leaning on an app
- [ ] Samsung SmartTag2 — theft tracker, hide deep in car (can do any time)
- [ ] Slim 4-port USB 2.0 squid/pigtail hub — squid style preferred (flexible tails survive vibration better than rigid sockets)
- [ ] 64GB+ high-endurance USB stick for DVR loop — consider stepping up to 256GB+ high-endurance flash or a small USB SSD (bigger = longer loop before overwrite + less wear/year); NOT a spinning HDD (vibration risk, power draw)
- [ ] Push-to-open magnetic touch latch — for the coin-tray SSD concealment panel (rated for the panel's weight, road-test before permanent fit)
- [ ] Slim disc magnet pairs (round, not bar) — for securing the DVR stick and music stick in the dash cavity; high-temp glue/VHB/epoxy for any mount point in direct sun, standard hot glue fine in shade
- [ ] Windscreen sunshade + UV/heat-rejecting window tint — protects the unit from cabin heat (biggest lever = reducing radiant load at the source)
- [ ] USB-C OTG adapter for A56 — wired RealDash audition (optional)
- [ ] External 3.5mm mic — ONLY if inbuilt fails the Signal call test
- [ ] Wago lever nuts (assorted sizes) — bench-wiring the unit's own loom to the brick
- Ruled out: TPMS kit, FORScan Lite on unit, boot password, OBD splitter, parked-surveillance battery pack, spinning hard drive for DVR

## 2. Before the old unit comes out — SETTINGS SWEEP ritual
- [ ] Walk EVERY Sync menu and set every preference to taste while the old screen works (persists in the BCM/modules forever): Vehicle settings (ESC, Hill start, Rain sensor, Mirrors, Indicator, Ambient light, Chimes), Audio, Clock, Display
- [ ] Final Deflation Detect (TPMS) reset at correct pressures — last act before removal
- [ ] MASTER RESET (SYNC Set. menu) — wipes phonebook/pairings before boxing the old unit
- [ ] Confirm A56 Emergency SOS is configured (Settings > Safety and emergency) — manual multi-press trigger, dials local emergency number + alerts contacts w/ location

## 3. Arrival day (box on the floor)
- [ ] Film unboxing start to finish; photograph everything generously (no rigid numbering needed)
- [ ] Check for loose mic + note its plug type; measure camera barrel
- [ ] Identify the unit's OWN wiring loom (bare colour-coded tails) separately from the finished quadlock plug

## 4. Bench era (maximal build)
- [ ] Power on bench: bridge loom red+yellow (fake ignition-on), black to ground, joined to the brick via Wago lever nuts
- [ ] Factory menu (Car Settings > Factory, pwd 000000): confirm CarType; check whether Car Settings exposes a Deflation Detect entry
- [ ] Photograph firmware/MCU; ADB full backup before debloating; no OTA updates unless broken
- [ ] Camera bench test; DVR settings: audio OFF, ENABLE TIMESTAMP OVERLAY (GPS/network-synced), check speed/GPS overlay option
- [ ] KEY-TEST every panel + wheel button via ADB logcat — build the button map from what actually forwards; confirm the unit's Android version allows Tasker to auto-place a phone call cleanly (needed for the theft alert)
- [ ] Choose and set a SLEEP MODE (no sleep/2hr/1day/3day) for ignition-off standby vs cold boot
- [ ] Burner Google account; guest wifi; Private DNS; NetGuard default-deny whitelist (RealDash, Maps, FuelCheck, Syncthing, Signal, Claude, Mega, DMSS, streams)
- [ ] Install: Poweramp, Mega app (both directions — music pull-down + guardian log push-up, wifi-only to protect hotspot data EXCEPT allow the SIM connection through for guardian logs specifically so theft trip data can still leave the car away from home wifi), Syncthing (DVR clips + logs to workstation, LAN-speed for the big files), Signal, Claude app, AJN stream, FuelCheck P98, Waze/Maps, DMSS, FUTO keyboard
- [ ] Point Poweramp's library scan at the Mega-synced music folder so new tracks appear automatically
- [ ] RealDash: install, load BOTH drive-page styles as swipe neighbours, set as launcher + autostart; enable background-keep-alive + battery-optimisation exemption; custom ST boot logo
- [ ] Confirm whether RealDash can render a real map (streets/tiles) for the in-car trip review, or whether that stays PC-side only — genuine open question, test on real hardware
- [ ] Wireless ADB + scrcpy paired with the workstation (not the Lenovo — see section 11)
- [ ] Driveway hybrid test: car's OBD cabled to the bench unit, RealDash reads live data pre-install
- [ ] Gear-ratio calibration: log one drive through all 6 gears once mobile (need VSS ticked — see section 12) → derive the RPM/speed math channel for GEAR
- [ ] Build the derived math channels: CLUTCH SLIP (RPM sustained above what speed predicts under load, high confidence in 3rd+, patient in 1st/2nd), turbo wastegate-duty TREND (rising WGATE% for the same boost = early leak/wear warning), software TPMS proxy (persistent inter-wheel speed disagreement in a straight line)
- [ ] Build Tasker automations: dashcam snapshot (CD key), save-clip (EJECT key), page teleports + speed-dial (number pad), wheel voice short/long press, LENDING MODE toggle (spare number-pad slot — suppresses the theft alert for that session while logging continues normally), THEFT ALERT (Bluetooth-absence-at-ignition → native phone call + simultaneous Signal message with time/context), NEAR-MISS bookmark (brake switch + sub-crash deceleration spike auto-tags dashcam footage), crash-alert (dashcam G-sensor spike → cancel countdown → auto-dial 000/contact)
- [ ] Build the CHECK NOW voice pipeline: on-unit Claude API call comparing today's data to a cached baselines file, TTS response + on-screen toast, wake-word OFF everywhere (button-press-only activation), Tasker cooldown against a stuck/double-press
- [ ] Build the auto-generated trip-map HTML script (Leaflet.js + OpenStreetMap, reads the CSV log's lat/long/speed, outputs a per-trip file next to the source log)
- [ ] Set your own number as a priority/emergency-bypass contact on your phone, so the theft-alert call rings through even on silent/DND
- [ ] Mark that calling number as priority/bypass on your OWN phone too

## 5. Install weekend (hardware only)
- [ ] Battery disconnect first → expect KAM relearn wobble after
- [ ] Wiring: quadlock to canbus box, radio antenna Fakra, factory reverse camera → Fakra-to-RCA adapter → unit camera input. Cable 2 (wide ~24-pin connector) does NOT get connected — confirmed from the seller's own instruction sheet
- [ ] Label THREE aerial plugs: radio antenna / reverse camera Fakra / factory GPS (leave GPS dormant)
- [ ] OBD junction: dedicated tail, quick-release joint at knee height, strain relief
- [ ] USB hub wiring: DVR stick + gearstick-socket lead (may need re-terminating) + 2 spare
- [ ] Mount the 256GB SSD under the coin tray behind the magnetic latch; anchor firmly, confirm clear of knee/pedal space, give the cable a service loop
- [ ] Secure the DVR stick and music stick with paired disc magnets in the dash cavity, no dangling cables
- [ ] Pod trimming: electronics proven first, then trim to fit
- [ ] Canbus init: Factory > CarType > canbus BRAND then Ford Fiesta
- [ ] Everything zip-tied, nothing hangs by its own plug
- [ ] Test: SWC + panel keys, camera trigger, aircon popup, handbrake signal
- [ ] Audio sweep before trim goes back
- [ ] Old Sync unit + pod + screen BOXED forever
- [ ] One-line note to insurer
- [ ] Fit the sunshade + confirm the window tint is done

## 6. First weeks in car
- [ ] Signal call test at highway speed → inbuilt mic verdict
- [ ] DSP/EQ session
- [ ] Test the theft alert deliberately (start the car without your phone nearby, in a controlled way) to confirm the call + Signal message actually fire
- [ ] Test the trip-map HTML generation on a real drive
- [ ] Live with it; annoyance list = design fuel; driver's-seat verdict on the two Drive-page styles as swipe neighbours

## 7. Interface (see repo for full visual spec)
Page set: Warm-up, Cruise (the calm daily companion — clock, now-playing, guardian whisper, zero performance content), Drive, Data (adjacent to Drive), Music, Maps, Performance, Guardian, Stats, Trip Review. Cruise recommended as the default post-warmup landing page.
- [ ] Music + Maps page concepts still to design
- [ ] Wheel close-up photo → confirm exact button layout
- [ ] Confirm remaining number-pad slots (long-6 father Signal, long-9 emergency dial, long-0 "on my way" message, short-*/# screen/mute) and Lending Mode's exact key

## 8. Input layer — button map (full detail in repo)
Wheel: voice short=Claude hands-free voice mode, long=Signal memo. Panel: NAV/MAP/MENU/SOUND/HOME/PHONE natural; CD=snapshot, EJECT=save clip, TRAFFIC=cameras, INFO=guardian, CLOCK=parking timer, AUX=source cycle. Number pad short=page teleport, long=speed-dial (1=wife mobile, 2=wife Signal, 3=son mobile, 4=son Signal, 5=father mobile). Rotary dial LEFT/RIGHT arrows proposed for page-swipe (freed from Sync's old menu-scroll job).

## 9. Theft detection + security system
- [ ] Bluetooth-absence-at-ignition trigger: engine starts without his phone's Bluetooth in range → Tasker fires a native phone call (harder to miss than a text) + simultaneous Signal message with time/context
- [ ] LENDING MODE toggle: press before handing over keys → suppresses the alert for that session, keeps GPS/speed logging running normally underneath for later review
- [ ] Guardian log Mega sync widened to also ride the car's own SIM (not just wifi) — a stolen car will never reach home wifi again, so this is what gets the actual route data out afterward, not just the initial alert
- [ ] SmartTag2 remains the anywhere-tracking backbone regardless (crowd-sourced Bluetooth network, never needs the car's own internet)
- [ ] TRIP REVIEW / SECURITY REVIEW: same feature, same map — colour-coded route by speed, stop markers with duration, max/avg speed + distance + duration stat cards; reviewable via the auto-generated per-trip HTML file (real OpenStreetMap tiles) sitting next to each day's log

## 10. Derived diagnostics (new math channels, no new PIDs)
- [ ] GEAR — RPM/speed ratio bands (needs VSS logged, which RealDash already does)
- [ ] CLUTCH SLIP — RPM sustained above what speed predicts under load; high confidence in 3rd gear+, patient trend-watching in 1st/2nd (wheelspin confound)
- [ ] Wastegate-duty TREND — rising TURBO_WGATE% to hold the same boost target = early leak/wear warning
- [ ] Software TPMS proxy — persistent inter-wheel speed disagreement in a straight line
- [ ] DRPMIS-based misfire/rough-running alert (factory channel, no derivation needed)
- [ ] Near-miss bookmark — brake switch + sub-crash deceleration spike auto-tags dashcam footage
- [ ] Non-engine watch list: BRK_FLUID (brake fluid level), EPAS_MOTOR_CUR trend (steering wear), door/window status check before walking away

## 11. Guardian system
- [ ] CHECK NOW: self-contained on the unit, calls Claude API directly over hotspot/SIM, compares against a cached baselines file, responds via TTS voice + on-screen toast
- [ ] Weekly deep-dive + baseline-refresh runs on the real WORKSTATION (not the Lenovo, which is his toy/tinkering machine) — Syncthing points to both, Lenovo keeps casual ADB/scrcpy duty
- [ ] Archive file organisation: top-level folders by type (guardian-logs/, dashcam-clips/, weekly-reports/), Year/Month subfolders, ISO-date filenames for auto-sorting
- [ ] Locked dashcam clips + guardian logs both push direct to Mega from the car (offsite backup independent of any PC being on)
- [ ] RealDash dashboards + Tasker profile exports also backed up to Mega (the build itself, not car data — fast restore if the unit ever dies)
- [ ] System updates flow via Mega too: future dashboard/Tasker revisions drop into the synced folder and pull down automatically — Tasker auto-triggers RealDash's import

## 12. Still open
- [ ] Next FORScan LAPTOP session (if one happens): remember to tick VSS alongside RPM — none of the existing profiles have it, though this does NOT affect guardian, which gets speed by default
- [ ] Father's SIM/Signal network preference for the speed-dial pattern
- [ ] Confirm whether RealDash can render real map tiles in-car or whether Trip Review stays PC/web-side only
- [ ] Thermal mods (thermal paste, aftermarket heatsink, airflow check) — optional, deferred, revisit only if real symptoms show up (trivial to reopen: fascia + 2 screws)
- [ ] Lufi retires when dash goes live (no splitter, one screen is enough)
