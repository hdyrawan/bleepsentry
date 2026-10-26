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
