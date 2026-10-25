# Changelog

All notable changes to the comma.ai Home Assistant integration will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2026-10-25

### Added
- Road camera (outside) and driver camera (inside) entities, using comma connect's WebRTC live stream
  - Streams start on demand and stop after 30 seconds without viewers
  - Snapshot and MJPEG support
  - `last_error` attribute explaining why a stream could not start
- Car battery voltage sensor and car running binary sensor, read live from the device via athena (polled every 5 minutes, since it uses the device's own connection) (bscholer/home-assistant-comma-ai#7, thanks @georgegebbett)
- Reauth flow: an expired JWT token now prompts to re-authenticate instead of failing setup (bscholer/home-assistant-comma-ai#7)

### Changed
- Requires Home Assistant 2025.12 or newer (for aiortc's PyAV requirement)

### Fixed
- Distance sensors were 1.6x too low: comma's stats API reports miles, not kilometers. They now follow the Home Assistant unit system instead of always showing miles (bscholer/home-assistant-comma-ai#4). Existing installs keep their current display unit; change it in the entity settings if you want km
- API errors raised inside the coordinator's task group are now reported correctly (bscholer/home-assistant-comma-ai#7)
- Accounts without a username fall back to email or user ID for the entry title (bscholer/home-assistant-comma-ai#7)
- Removed the deprecated `battery_level` override from the device tracker, unsupported from Home Assistant 2027.7 (bscholer/home-assistant-comma-ai#5, bscholer/home-assistant-comma-ai#6)

## [1.0.0] - 2025-10-26

### Added
- Initial release
- Device tracker for GPS location tracking
- Device information sensors (type, openpilot version, Prime status)
- GPS data sensors (speed, bearing, accuracy)
- Last ping and GPS update timestamp sensors
- All-time driving statistics (distance, time, routes)
- Weekly driving statistics (distance, time, routes)
- Config flow for easy setup via UI
- **JWT token reconfiguration** - Easy token renewal through UI when tokens expire (90 day expiry)
- JWT token authentication
- HACS compatibility
- Automatic unit conversion (km to miles, m/s to mph)
- Device grouping in Home Assistant UI
- 60-second update interval
- Graceful handling of offline devices
- Timezone-aware timestamp sensors
- Energy dashboard compatibility for distance tracking

### Technical
- Uses comma.ai public API v1 and v1.1
- Async implementation with proper coordinators
- Type hints throughout codebase
- Proper error handling
- Translation support (English)
- Home Assistant 2024.1.0+ compatibility
- Reconfigure flow for token updates

## [Unreleased]

### Planned
- Historical route visualization
- Navigation destination setting
- Saved locations management
- Binary sensors (is_driving, is_online)
- Services for advanced operations
- Multi-language translations
- Automatic token expiration warnings

