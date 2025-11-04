# Changelog

All notable changes to this project will be documented in this file.

## [1.0.3] - 2024-11-04

### Fixed
- **Version parsing improvements**: Rewrote version detection to properly handle OBS 30.x and later versions
  - Changed from parsing version as "XX.Y" format to properly extracting major, minor, and patch numbers
  - Fixed version comparison logic that was using floating-point arithmetic incorrectly
  - Now correctly handles version strings like "30.0.0", "30.2.1-beta1", etc.

- **macOS compatibility**: Fixed screen_capture detection for OBS 29.1+ and OBS 30+
  - Updated version check from `major > 29.0` to `version_number >= 29.1`
  - Ensures proper source type selection on modern OBS versions

- **Script cleanup**: Fixed version check in script_unload function
  - Now properly compares version numbers for safe cleanup in OBS 29.1.3+
  - Prevents crashes on script reload/unload

### Changed
- Updated version to 1.0.3
- Improved debug logging to show full parsed version information
- Better version comparison using calculated version_number

### Technical Details
The main issue was in how version numbers were parsed and compared:
- **Old**: `major` was set to something like "29.1" or "30.0" (as a string matched pattern)
- **New**: `major`, `minor`, `patch` are proper integer values, with `version_number` for comparisons

This ensures compatibility with:
- OBS Studio 30.x (latest versions)
- OBS Studio 29.x (all versions)
- Future OBS releases

---

## [1.0.2] - Original

Original version from BlankSourceCode's repository.
Built for OBS v29.1.3 with support for Windows, Linux, and macOS.
