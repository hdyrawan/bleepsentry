# Bleepsentry

Passive Bluetooth Low Energy (BLE) recon and census tool for Flipper Zero, built for two audiences:

- **Red team / physical pentest**: passive site survey, multi-session presence correlation ("did this device follow me between two locations"), target tagging with silent re-entry alerts, dwell-time/schedule analytics.
- **TSCM (counter-surveillance)**: pre/post baseline-diff bug sweeps, known-bug/tracker signature matching, stationary-signature triage to separate planted devices from people carrying phones.

Bleepsentry only **listens**. It never transmits advertisements or connects to devices in passive mode. GATT enumeration (a later, explicitly separate mode) is the only feature that connects to a target device, and only when you select one.

## Status

Early development. Current build is the scaffold only — no scanning logic yet.

## Hardware

Stock Flipper Zero only. No add-on boards required (BLE radio is on-board).

## Intended use

This tool is built for authorized security engagements (penetration tests, red team exercises, TSCM/bug sweeps under contract) and for sweeping your own devices/spaces. Fingerprinting and cross-session correlation features can re-identify devices despite BLE MAC randomization — use only where you have authorization to observe the people/assets in range.

## Build

```
pip install ufbt
ufbt
ufbt launch   # with a Flipper connected over USB
```
