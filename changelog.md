## 0.4

- Extracted pure logic (threshold math, alert state transition, frequency
  index wrap, CSV line formatting) into `bleepsentry_logic.c/.h`, free of
  any Flipper SDK dependency, with a host-side unit test suite in `tests/`
  that runs on a normal machine (no device needed) and is wired into CI.
  This does NOT substitute for on-device testing of GUI/radio/timing
  behavior, but it does prove the math and formatting are correct.
- Explicitly excluded `tests/` from the embedded build via `sources` in
  `application.fam` -- the default source glob is recursive and was
  pulling the host test file (and its `<assert.h>`/`<math.h>` includes)
  into the actual .fap binary. Caught via a clean rebuild, fixed before
  any hardware testing could have surfaced it.
- Ran `ufbt lint`/`ufbt format` (clang-format) for the first time; fixed
  all violations.

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
