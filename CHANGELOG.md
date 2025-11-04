# Changelog

All notable changes to this project will be documented in this file.

## [2.0.0] - 2024-11-04

### Changed
- **BREAKING**: Updated to use OBS 30.x API exclusively - no longer compatible with OBS 29.x
- Replaced deprecated `obs_sceneitem_get_info()` and `obs_sceneitem_set_info()` with individual getter/setter functions
- Replaced `obs.obs_transform_info()` with manual structure creation using individual API calls

### Fixed
- Fixed "attempt to call field 'obs_sceneitem_get_info' (a nil value)" error in OBS 30.x
- Fixed bug where `obs_sceneitem_get_info` was called instead of `obs_sceneitem_set_info` when restoring transform

### Technical Details
OBS 30.x removed the deprecated scene item transform functions. The new API uses:
- `obs_sceneitem_get_pos()` / `obs_sceneitem_set_pos()`
- `obs_sceneitem_get_scale()` / `obs_sceneitem_set_scale()`
- `obs_sceneitem_get_bounds()` / `obs_sceneitem_set_bounds()`
- `obs_sceneitem_get_rot()` / `obs_sceneitem_set_rot()`
- `obs_sceneitem_get_alignment()` / `obs_sceneitem_set_alignment()`
- `obs_sceneitem_get_bounds_type()` / `obs_sceneitem_set_bounds_type()`
- `obs_sceneitem_get_bounds_alignment()` / `obs_sceneitem_set_bounds_alignment()`

---

## [1.0.3] - 2024-11-04

### Fixed
- **Version parsing improvements**: Rewrote version detection to properly handle OBS 30.x and later versions
  - Changed from parsing version as "XX.Y" format to properly extracting major, minor, and patch numbers
  - Fixed version comparison logic using integer math (major * 100 + minor) instead of floating-point arithmetic
  - Now correctly handles version strings like "30.0.0", "30.0", "30.2.1-beta1", etc.
  - Avoids floating-point precision issues in version comparisons

- **macOS compatibility**: Fixed screen_capture detection for OBS 29.1+ and OBS 30+
  - Updated version check from `major > 29.0` to `version_number >= 2901` (integer comparison)
  - Ensures proper source type selection on modern OBS versions

- **Script cleanup**: Fixed version check in script_unload function
  - Now properly compares version numbers using integers for safe cleanup in OBS 29.1.3+
  - Prevents crashes on script reload/unload

### Changed
- Updated version to 1.0.3
- Improved debug logging to show full parsed version information
- Better version comparison using calculated version_number (integer-based)

### Technical Details
The main issue was in how version numbers were parsed and compared:
- **Old**: `major` was set to something like "29.1" or "30.0" (as a string matched pattern), comparisons used floating-point
- **New**: `major`, `minor`, `patch` are proper integer values, with `version_number = major * 100 + minor` for comparisons

This ensures compatibility with:
- OBS Studio 30.x (latest versions)
- OBS Studio 29.x (all versions)
- Future OBS releases (31.x, 32.x, etc.)

---

## [1.0.2] - Original

Original version from BlankSourceCode's repository.
Built for OBS v29.1.3 with support for Windows, Linux, and macOS.
