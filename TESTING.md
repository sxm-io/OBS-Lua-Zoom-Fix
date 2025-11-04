# Testing Guide

This guide helps you test the OBS Zoom to Mouse script to ensure it works correctly with your OBS version.

## Quick Test Checklist

Use this checklist to verify basic functionality:

- [ ] Script loads without errors in OBS Scripts window
- [ ] Display Capture source appears in Zoom Source dropdown
- [ ] Zoom hotkey triggers zoom in animation
- [ ] Zoom centers on mouse cursor position
- [ ] Mouse tracking works while zoomed in
- [ ] Zoom out hotkey returns to normal view
- [ ] No errors in OBS log

## Detailed Testing Procedures

### 1. Version Detection Test

**Purpose**: Verify the script correctly detects your OBS version.

**Steps**:
1. Open OBS Studio
2. Go to **Help** → **About** - Note your OBS version (e.g., "30.0.0")
3. Open **Tools** → **Scripts**
4. Select the "OBS Zoom to Mouse" script
5. Check "Enable debug logging"
6. Click "More Info" button
7. Go to **Help** → **Log Files** → **View Current Log**
8. Search for "OBS Version:" in the log

**Expected Result**:
```
OBS Version: 30.0.0 (parsed as 30.0.0)
```

**Pass Criteria**: Version is correctly parsed with all three numbers (major.minor.patch)

---

### 2. Script Loading Test

**Purpose**: Ensure the script loads without errors.

**Steps**:
1. Open **Tools** → **Scripts**
2. Remove the script if already loaded (select it and click **-**)
3. Click **+** and add `obs-zoom-to-mouse.lua`
4. Check the script appears in the list
5. Check **Help** → **Log Files** → **View Current Log** for errors

**Expected Result**:
- Script appears in list
- No error messages in log
- Settings panel shows on right side

**Pass Criteria**: No errors, script settings visible

---

### 3. Source Detection Test

**Purpose**: Verify the script can find your Display Capture sources.

**Steps**:
1. Create a new scene if needed
2. Add a **Display Capture** source
3. In Scripts window, select "OBS Zoom to Mouse"
4. Click "Refresh zoom sources"
5. Check the "Zoom Source" dropdown

**Expected Result**:
- Your Display Capture source appears in dropdown
- `<None>` option is available

**Pass Criteria**: All Display Capture sources are listed

---

### 4. Basic Zoom Test

**Purpose**: Test basic zoom in/out functionality.

**Steps**:
1. Select your Display Capture in "Zoom Source" dropdown
2. Set Zoom Factor to `2.0`
3. Set Zoom Speed to `0.06`
4. Go to **File** → **Settings** → **Hotkeys**
5. Assign a hotkey to "Toggle zoom to mouse" (e.g., `F1`)
6. Click **OK**
7. Return to OBS main view
8. Move mouse to specific location on screen
9. Press zoom hotkey
10. Observe zoom animation
11. Press hotkey again to zoom out

**Expected Result**:
- Smooth zoom animation towards mouse position
- View centers on where mouse was when hotkey pressed
- Smooth zoom out animation back to normal

**Pass Criteria**: Zoom works smoothly in both directions

---

### 5. Mouse Tracking Test

**Purpose**: Verify auto-follow mouse functionality.

**Steps**:
1. Enable "Auto follow mouse"
2. Set Follow Speed to `0.25`
3. Set Follow Border to `8`
4. Zoom in using hotkey
5. Wait for zoom animation to complete
6. Keep mouse still for 1 second
7. Slowly move mouse to edge of visible area
8. Observe view following mouse

**Expected Result**:
- View has "safe zone" in center where mouse can move freely
- When mouse approaches edge, view starts following
- Smooth tracking motion
- View locks when mouse stops moving

**Pass Criteria**: Tracking follows mouse at edges, stops in center

---

### 6. Multi-Monitor Test

**Purpose**: Test with multiple monitor setups (if applicable).

**Steps**:
1. Set up OBS with multiple monitors
2. Create Display Capture for second monitor
3. Select it as Zoom Source
4. Zoom in on second monitor
5. Move mouse around second monitor

**Expected Result**:
- Zoom works correctly on second monitor
- Mouse position is accurate
- No offset or alignment issues

**Pass Criteria**: Zoom centers correctly on mouse cursor position

---

### 7. Platform-Specific Tests

#### Windows Test
- Display Capture source type should be `monitor_capture`
- Mouse position should be accurate
- Multi-monitor support should work

#### Linux Test
- XSHM display capture should work automatically
- Pipewire sources work with manual position setup
- Mouse position is correct

#### macOS Test (OBS 29.1+)
- Script should use `screen_capture` source type
- Check log shows: "screen_capture" for OBS 29.1+
- Mouse position is correct (Y-axis may be inverted)

---

### 8. Transform Compatibility Test

**Purpose**: Verify script handles different transform settings.

**Test Cases**:

**Case A: Bounding Box = None**
1. Set Display Capture transform to "No bounds"
2. Reload script
3. Try zooming

Expected: Script auto-converts to Scale Inner bounds

**Case B: Transform Crop**
1. Add crop to transform (e.g., Top: 100)
2. Reload script  
3. Try zooming

Expected: Script auto-converts crop to Crop/Pad filter

**Case C: Existing Crop Filter**
1. Add Crop/Pad filter manually
2. Set some crop values
3. Try zooming

Expected: Zoom accounts for existing crop

---

### 9. Hotkey Conflict Test

**Purpose**: Ensure hotkeys work and don't conflict.

**Steps**:
1. Set zoom hotkey to something common (e.g., `Ctrl+Z`)
2. Test in OBS
3. Try in other applications
4. Change to different hotkey
5. Test again

**Expected Result**:
- Hotkey works reliably in OBS
- Doesn't interfere with other OBS hotkeys
- Can be changed without issues

---

### 10. Performance Test

**Purpose**: Verify script doesn't cause performance issues.

**Steps**:
1. Open OBS Stats (View → Stats)
2. Note CPU and FPS before enabling zoom
3. Zoom in and out multiple times
4. Move mouse around while zoomed
5. Check stats again

**Expected Result**:
- Minimal CPU impact (<1% on modern systems)
- No FPS drops
- Smooth animation throughout

---

## Regression Testing

After any updates to the script, test these scenarios:

1. **Clean Install**: Remove and re-add script
2. **Settings Persistence**: Change settings, restart OBS, verify they persist
3. **Scene Switching**: Zoom in, switch scenes, switch back
4. **Source Rename**: Rename Display Capture source while zoomed
5. **Script Reload**: Use "Reload Scripts" while zoomed in

## Common Issues and Solutions

### Issue: Script loads but zoom doesn't work
**Check**:
- Zoom Source is selected (not `<None>`)
- Hotkey is assigned
- Display Capture is in current scene
- Transform settings are compatible

### Issue: Zoom position is offset
**Check**:
- Transform alignment is "Top Left"
- Crop is set to all zeros (or using Crop/Pad filter)
- Monitor settings in OS haven't changed
- Try "Set manual source position" for multi-monitor

### Issue: Mouse tracking doesn't work
**Check**:
- "Auto follow mouse" is enabled OR
- "Toggle follow" hotkey is pressed after zoom
- Follow Border is not 0
- Mouse is moving to edge of zoom area

### Issue: Script causes OBS to crash
**Check**:
- OBS version (should be 29.1.3+ for safe cleanup)
- Debug log shows version correctly
- Try disabling and re-enabling script
- Report issue with OBS version and log

## Reporting Test Results

When reporting issues, include:

```
OBS Version: [e.g., 30.0.0]
Operating System: [e.g., Windows 11, Ubuntu 22.04, macOS 14]
Script Version: [from CHANGELOG.md]

Test Results:
- Version Detection: [Pass/Fail]
- Script Loading: [Pass/Fail]
- Source Detection: [Pass/Fail]
- Basic Zoom: [Pass/Fail]
- Mouse Tracking: [Pass/Fail]

Error Messages (if any):
[Paste relevant log lines]

Steps to Reproduce:
1. 
2. 
3. 

Expected vs Actual:
Expected: 
Actual: 
```

## Automated Testing Notes

This script cannot be easily unit tested because it requires:
- OBS Studio environment
- OBS Lua API
- FFI library access
- Platform-specific mouse APIs

All testing must be done manually in a live OBS environment.

## Success Criteria

The script is considered working if:
- ✓ All 10 detailed tests pass
- ✓ No errors in OBS log
- ✓ Performance impact is negligible
- ✓ Works on target platform (Windows/Linux/macOS)
- ✓ Compatible with OBS 29.1.3 through latest version

---

Happy Testing! 🧪
