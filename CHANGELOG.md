# Changelog

All notable changes to this fork will be documented in this file.

## [3.0.16.0] — 2026-10-01

First community-maintained release of this fork. Based on the v3 line
([Bonasort-HA](https://github.com/Bonasort-HA/alarmdotcom) v3.0.14.5), merged
with upstream v3.0.15 and nulledy v3.0.15.2.

### Fixed

- **Auth/reconfigure crash** on HA 2025.12+ ("Unknown error" in reauth flow):
  replaced removed `async_set_unique_id()` entry resolution with
  `_get_reauth_entry()` (port of upstream PR #546).
- **All entities fail with `AttributeError: '_friendly_name_internal'`** on
  HA 2026.2+: private Entity helper replaced with public APIs (Bonasort).
- **`No module named 'bs4._typing'`** on HA 2026.8+: `beautifulsoup4` pin
  raised to `>=4.13.4` so stale installs force-upgrade (manifest previously
  allowed a 4.10.x that predates the `_typing` split).
- **`async_timeout` import error** breaking integration setup on HA 2026.9+:
  package is no longer an HA core dependency; replaced with stdlib
  `asyncio.timeout()` (found via clean-venv install-check).
- **Options flow crash** on HA 2025.12+ (`OptionsFlow.config_entry` made
  read-only) and config-entry migration via `version=` kwarg (Bonasort).
- **Websocket teardown** on messages for unknown/blacklisted devices —
  real-time push stays alive (forked `pyalarmdotcomajax` v0.5.13.2).
- **Panel state reporting** migrated to the supported `AlarmControlPanelState`
  API; includes upstream v3.0.15 desired-state corrections.
- **Thermostat writes** restored on the v3 line (color-mode/feature migration).

### Changed

- `pyalarmdotcomajax` requirement pinned to this fork's copy
  (@ v0.5.13.2) instead of the stale upstream beta.
- Minimum Home Assistant floor set to 2026.2 (hacs.json).
- Arm/disarm without a panel code is permitted (nulledy v3.0.15.2).