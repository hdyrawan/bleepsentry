## 0.3

- Added sweep mode: long-press OK calibrates a baseline/threshold across all
  four frequencies in sequence, then continuously cycles through them
  (dwell-watch), alerting and logging independently per frequency. This is
  the actual multi-band TSCM sweep workflow; the single-frequency Watch mode
  (short-press OK) remains for red-team monitoring of one known frequency.
- Up/Down now preserves any previously-calibrated baseline per frequency
  instead of discarding it on every switch.
- Builds clean against SDK API 88.2. Not yet tested on physical hardware.

## 0.2

- Pivoted from BLE passive scanning to Sub-GHz RF anomaly sentry. The public
  Flipper SDK's BLE stack exposes peripheral/advertiser functions only; there
  is no central/observer scan API available to apps, so the original concept
  was not buildable. Verified against SDK headers (`bt.h`, `gap.h`,
  `furi_hal_bt.h`) before pivoting.
- Implemented core RSSI-threshold alert engine: frequency selection (300,
  433.92, 868.35, 915 MHz), baseline calibration, live RSSI bar, vibration
  alert on threshold breach.
- Builds clean against SDK API 88.2. Not yet tested on physical hardware.

## 0.1

- Initial scaffold via `ufbt create`.
