# Bleepsentry

Passive RF anomaly sentry for Flipper Zero, built for two audiences:

- **Red team / physical pentest**: passive monitoring of a target frequency (e.g. a garage/gate remote) to detect unexpected transmissions — flags possible replay-attack activity or unauthorized transmitters during an engagement.
- **TSCM (counter-surveillance)**: a live RSSI meter across common ISM sub-GHz bands, used the way a professional bug sweeper uses a spectrum analyzer — establish a quiet baseline in a room, then get an alert the moment something starts transmitting above that baseline. Many covert bugs/transmitters operate in exactly this 300–928 MHz range.

## Why Sub-GHz, not Bluetooth

This project started as a BLE passive-scanning tool. During development I checked the actual Flipper Zero SDK headers (not assumptions) and confirmed the public SDK's BLE stack (`bt.h`, `gap.h`, `furi_hal_bt.h`) only exposes **peripheral/advertiser** functionality — starting/stopping advertising, GATT profiles, extra-beacon transmission. There is no GAP central/observer scan API, no advertisement-received event, and no raw HCI passthrough exposed to apps. Passive BLE device scanning is not buildable against the official, catalog-eligible Flipper firmware today. Rather than ship something that can't work, the project pivoted to Sub-GHz (CC1101), where `furi_hal_subghz` genuinely exposes RSSI readout and async RX — the same APIs every existing capture/spectrum app in the catalog already relies on.

## How it works

Two modes, both logging every alert to `/data/log.csv` (timestamp, frequency, baseline, threshold, peak RSSI, duration):

- **Watch mode** (short-press OK): calibrates a baseline on the *current* frequency only, then continuously monitors just that one frequency. Built for red-team use — watching one known frequency (e.g. a garage/gate remote) for replay-attack-style activity.
- **Sweep mode** (long-press OK): calibrates a baseline on *every* frequency in sequence, then continuously cycles through all of them, alerting and logging independently per frequency. This is the actual multi-band TSCM bug-sweep workflow.

Controls:
- **Up/Down**: switch to a specific frequency manually (drops out of Sweep mode; keeps any previously-calibrated baseline for that frequency)
- **OK (short)**: calibrate + watch the current frequency
- **OK (long)**: calibrate + sweep all frequencies
- **Back**: exit

## Status

Early development. Core RSSI-threshold alert engine and multi-frequency sweep mode are implemented and build clean against SDK API 88.2 (uFBT, release channel). **Not yet tested on physical hardware** — no Flipper was connected during this development session; on-device behavior (radio timing, RSSI readings, GUI responsiveness) is unverified until that happens.

Planned next: baseline-diff sweep comparison (pre/post meeting), on-device CSV browsing, icon/screenshots for catalog submission.

## Hardware

Stock Flipper Zero only. No add-on boards required (CC1101 radio is on-board).

## Intended use

Built for authorized security engagements (penetration tests, red team exercises, TSCM/bug sweeps under contract) and for sweeping your own spaces. It only listens — it never transmits.

## Build

```
pip install ufbt
ufbt
ufbt launch   # with a Flipper connected over USB
```
