# Quick Reference

## Installation (30 seconds)
1. Download `obs-zoom-to-mouse.lua`
2. OBS → Tools → Scripts → + (Add)
3. Select the file
4. Done!

## Setup (2 minutes)
1. In Scripts window, select your Display Capture from "Zoom Source" dropdown
2. Go to File → Settings → Hotkeys
3. Assign hotkey to "Toggle zoom to mouse" (e.g., F1)
4. Click OK

## Usage
- **Zoom In**: Press your hotkey (cursor zooms to mouse position)
- **Zoom Out**: Press hotkey again
- **Mouse Tracking**: Enabled automatically if "Auto follow mouse" is on

## Recommended Settings
```
Zoom Factor: 2.0
Zoom Speed: 0.06
Auto follow mouse: ✓
Follow Speed: 0.25
Follow Border: 8%
```

## Display Capture Transform (Important!)
Right-click source → Transform:
- Positional Alignment: Top Left
- Bounding Box Type: Scale to inner bounds  
- Alignment in Bounding Box: Top Left
- Crop: All zeros (0, 0, 0, 0)

For cropping, use Filter → Crop/Pad instead!

## Troubleshooting Quick Fixes

| Problem | Solution |
|---------|----------|
| Source not listed | Click "Refresh zoom sources" |
| Zoom position wrong | Check transform settings above |
| Mouse tracking not working | Enable "Auto follow mouse" |
| Script not loading | Check OBS version (need 29.0+) |

## Hotkey Ideas
- `F1` - Simple and accessible
- `Ctrl+Z` - Familiar "zoom" association  
- `Middle Mouse Button` - Quick access while presenting
- `Numpad 0` - Dedicated key

## File Locations

**Script File**:
- Windows: `C:\Program Files\obs-studio\data\obs-plugins\frontend-tools\scripts\`
- Linux: `~/.config/obs-studio/scripts/` or `/usr/share/obs/obs-plugins/frontend-tools/scripts/`
- macOS: `~/Library/Application Support/obs-studio/scripts/`

## Version Compatibility

| OBS Version | Status |
|-------------|--------|
| 29.x | ✓ Compatible |
| 30.x | ✓ Compatible |
| 31.x+ | ✓ Should work |

## More Information

- Full Install Guide: [INSTALL.md](INSTALL.md)
- Testing Guide: [TESTING.md](TESTING.md)
- Technical Details: [TECHNICAL.md](TECHNICAL.md)
- Change Log: [CHANGELOG.md](CHANGELOG.md)

## Getting Help

1. Enable "Enable debug logging" in script settings
2. Reproduce the issue
3. Check Help → Log Files → View Current Log
4. Report issue on GitHub with log excerpt

## Credits

Original by BlankSourceCode: https://github.com/BlankSourceCode/obs-zoom-to-mouse

---

**Quick Start Video**:
1. Add script
2. Set hotkey
3. Press hotkey to zoom
4. That's it! 🎉
