# Roadmap

One device (Seeed XIAO MG24 Sense), three mounts:

- **Foot** – shoe/laces → running cadence (RSC), cycling cadence from the shoe (CSC crank)
- **Cadence** – crank arm → cycling cadence (CSC crank)
- **Speed** – wheel hub → wheel speed and distance (CSC wheel)

Each stage ends with something that works and is kept – no throwaway prototypes.
Stages are done in order; a stage is finished when its **Done when** box is ticked.

## Progress

- [ ] Stage 1 – Project skeleton
- [ ] Stage 2 – BLE compatibility test (go / no-go)
- [ ] Stage 3 – IMU driver and data logger
- [ ] Stage 4 – Shared core algorithm
- [ ] Stage 5 – Foot mode
- [ ] Stage 6 – Cadence mode (crank)
- [ ] Stage 7 – Speed mode (hub)
- [ ] Stage 8 – Power optimisation
- [ ] Stage 9 – Adapters and enclosure

## Key design decisions

| Topic | Decision |
|---|---|
| Toolchain | VS Code + PlatformIO, Arduino framework (`platform-seeedboards`, board `seeed-xiao-mg24`) |
| Cadence algorithm | One shared estimator of the **cycle frequency f** (band-pass ~0.4–3.5 Hz + autocorrelation on acceleration magnitude, with a confidence threshold). Running: cadence = 2·f steps/min. Cycling: +1 crank revolution per cycle |
| Mode detection | Determined by adapter geometry: each adapter fixes the rotation axis relative to the IMU (crank → Z, hub → X/Y, shoe → no full rotation). Fallback: mode set via a BLE characteristic |
| BLE identity | Each mode advertises with its own name and address (`Hejnas Foot` / `Hejnas Cadence` / `Hejnas Speed`), so the watch pairs it as three separate sensors |
| Hub mode | Accelerometer only (gravity rotation). The gyro saturates at ±2000 dps ≈ 42–46 km/h |
| IMU power | LSM6DS3TR-C powered via PD5; gyro off unless recordings prove it necessary |
| Battery | Voltage via PD3 (divider enable) / PD4 (ADC), exposed as Battery Service |
| License | MIT (code), CC0 (3D models) |

## Stage 1 – Project skeleton
- [ ] PlatformIO project with `src/`, `lib/`, `test/` layout
- [ ] Blink + serial log on the board
- [ ] GitHub Actions: build firmware + run native unit tests on every push/PR
- [ ] **Done when:** CI is green and the firmware runs on the board

## Stage 2 – BLE compatibility test (go / no-go)
- [ ] RSC service with fake cadence (`Hejnas Foot`)
- [ ] CSC service with fake crank data (`Hejnas Cadence`)
- [ ] CSC service with fake wheel data (`Hejnas Speed`)
- [ ] Battery and Device Information services
- [ ] Pairing test: Suunto Peak Pro
- [ ] Pairing test: Suunto Vertical
- [ ] Check how the watch handles cadence-only RSC (speed absent/zero)
- [ ] **Done when:** all three sensors pair and show plausible values in run and bike activities

> If it fails: add simple speed estimation (cadence × calibrated stride length) or adjust the BLE approach before writing any algorithm.

## Stage 3 – IMU driver and data logger
- [ ] LSM6DS3TR-C power-up via PD5, ODR, FIFO, wake-up interrupt
- [ ] Record raw accel + gyro to the on-board 4 MB flash
- [ ] Dump recordings over USB
- [ ] Python tool to download and plot recordings
- [ ] Recordings – running: flat, trail, downhill
- [ ] Recordings – shoe on bike
- [ ] Recordings – crank: road, rough terrain, coasting
- [ ] Recordings – hub: road, rough terrain
- [ ] **Done when:** a labelled set of recordings is stored in the repo

## Stage 4 – Shared core algorithm
- [ ] Platform-independent C++ library: filtering
- [ ] Cycle-frequency estimator with confidence
- [ ] Rotation-axis / mode detection
- [ ] Native unit tests on the recordings (`pio test -e native`)
- [ ] Coasting on rough terrain gives cadence 0
- [ ] **Done when:** all recordings pass with error below ±2 %

## Stage 5 – Foot mode
- [ ] Real running cadence in RSC
- [ ] Cycling cadence from the shoe in CSC
- [ ] Field tests: treadmill, road, trail
- [ ] **Done when:** cadence matches Suunto wrist cadence in all field tests

## Stage 6 – Cadence mode (crank)
- [ ] Crank revolutions in CSC
- [ ] Field tests: road, rough terrain, coasting
- [ ] **Done when:** cadence is correct in all field tests

## Stage 7 – Speed mode (hub)
- [ ] Wheel revolutions in CSC (wheel circumference set in the watch)
- [ ] Field tests: distance compared with GPS / known route
- [ ] **Done when:** distance error below ±2 % on a known route

## Stage 8 – Power optimisation
- [ ] Auto-sleep after inactivity
- [ ] Wake-on-motion from the IMU
- [ ] Current measurement (shunt resistor + oscilloscope)
- [ ] **Done when:** average current and battery life with 210 mAh LiPo are documented

## Stage 9 – Adapters and enclosure
- [ ] Shoe adapter (laces)
- [ ] Crank adapter
- [ ] Hub adapter
- [ ] Assembly guide with photos
- [ ] **Done when:** all adapters are printable (CC0) and each fixes the board orientation required by mode detection

## Later
- [ ] Running speed and distance (stride-length calibration, then gyro-based ZUPT)
- [ ] OTA firmware updates
- [ ] Configuration via BLE (calibration, mode override)
