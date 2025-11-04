# Installation Guide

This guide will help you install and configure the OBS Zoom to Mouse script.

## Prerequisites

- **OBS Studio**: Version 29.0 or later (tested with OBS 30.x)
  - Download from: https://obsproject.com/
- **Operating System**: Windows, Linux, or macOS
- **Display Capture Source**: At least one display capture source in your OBS scene

## Step-by-Step Installation

### 1. Download the Script

**Option A: Clone the Repository**
```bash
git clone https://github.com/sxm-io/OBS-Lua-Zoom-Fix.git
```

**Option B: Download Directly**
1. Visit https://github.com/sxm-io/OBS-Lua-Zoom-Fix
2. Click on `obs-zoom-to-mouse.lua`
3. Click "Raw" button
4. Right-click and "Save As..." to download

### 2. Install in OBS Studio

1. **Launch OBS Studio**

2. **Open the Scripts Panel**
   - Go to **Tools** → **Scripts**
   - The Scripts window will open

3. **Add the Script**
   - Click the **+** (plus) button at the bottom left
   - Navigate to where you saved `obs-zoom-to-mouse.lua`
   - Select the file and click **Open**

4. **Verify Installation**
   - You should see "OBS Zoom to Mouse" in the scripts list
   - The right panel should show script settings

### 3. Set Up Your Display Capture Source

If you don't have a Display Capture source yet:

1. In OBS main window, click **+** under Sources
2. Select **Display Capture**
3. Give it a name and click **OK**
4. Select your monitor and click **OK**

### 4. Configure Recommended Settings

For the best zoom experience, configure your Display Capture source:

1. **Right-click** your Display Capture source → **Transform**
   - Set **Positional Alignment** to `Top Left`
   - Set **Bounding Box Type** to `Scale to inner bounds`
   - Set **Alignment in Bounding Box** to `Top Left`

2. **Right-click** your Display Capture source → **Transform** → **Edit Transform**
   - Set all Crop values to **0** (Left: 0, Top: 0, Right: 0, Bottom: 0)

3. **If you need to crop**, add a filter instead:
   - Right-click Display Capture → **Filters**
   - Click **+** under Effect Filters
   - Select **Crop/Pad**
   - Set **Relative** to `False` (unchecked)
   - Adjust Left, Top, Width, Height as needed

### 5. Configure Script Settings

In the Scripts window:

1. **Select Zoom Source**
   - From the "Zoom Source" dropdown, select your Display Capture source
   - If it's not listed, click "Refresh zoom sources"

2. **Basic Settings** (recommended defaults):
   - Zoom Factor: `2.0` (zoom in 2x)
   - Zoom Speed: `0.06` (smooth animation)
   - Auto follow mouse: `✓` (checked)
   - Follow Speed: `0.25`
   - Follow Border: `8%`

3. **Click "Apply"** or just change to another settings tab

### 6. Set Up Hotkeys

1. In OBS, go to **File** → **Settings** → **Hotkeys**

2. Scroll down to find:
   - **Toggle zoom to mouse** - Set a hotkey (e.g., `Ctrl+Z` or `Middle Mouse Button`)
   - **Toggle follow mouse during zoom** - Optional, for manual control

3. Click **OK** to save

## Testing the Installation

1. **Test the zoom**:
   - Make sure your scene with the Display Capture is active
   - Press your zoom hotkey
   - The display should zoom in smoothly to where your mouse cursor is

2. **Test mouse tracking**:
   - While zoomed in, move your mouse around
   - The view should follow your cursor (if auto-follow is enabled)

3. **Zoom out**:
   - Press the zoom hotkey again
   - The view should smoothly zoom back out

## Troubleshooting

### Script not appearing in Scripts list
- Make sure you selected the `.lua` file, not a folder
- Try restarting OBS Studio
- Check the OBS log for any error messages

### Zoom source not listed
- Make sure you have a Display Capture source in your current scene
- Click "Refresh zoom sources" button
- Try enabling "Allow any zoom source" (requires manual position setup)

### Zoom position is wrong
- Verify your Display Capture transform settings (see Step 4)
- If using multiple monitors, try enabling "Set manual source position"
- Check that monitor settings haven't changed in your OS

### Script works but zoom is choppy
- Increase "Zoom Speed" value (0.1-0.2 for faster animation)
- Increase "Follow Speed" value
- Check your PC performance/OBS resource usage

### Linux: Mouse position incorrect
- Install X11 libraries: `sudo apt-get install libx11-6`
- For Pipewire sources, enable "Set manual source position"

### macOS: Script not working
- Make sure you're using OBS 29.1 or later
- The script should auto-detect and use `screen_capture`
- Check Script Log for version detection messages

## Platform-Specific Notes

### Windows
- Works with all Display Capture sources
- No additional setup required

### Linux
- Requires X11 libraries (usually pre-installed)
- For XSHM sources: Install xserver-xorg
- For Pipewire: Requires manual position setup

### macOS
- OBS 29.1+: Uses `screen_capture` automatically
- OBS 29.0 and below: Uses legacy `display_capture`
- May require screen recording permissions in System Preferences

## Advanced Configuration

See the [README.md](README.md) for advanced options like:
- Manual source position override
- Remote mouse tracking (dual machine setup)
- Custom follow behavior
- Debug logging

## Getting Help

If you encounter issues:

1. **Enable debug logging**:
   - In Scripts window, check "Enable debug logging"
   - Reproduce your issue
   - Check the OBS Script Log (Help → Log Files → View Current Log)

2. **Report issues**:
   - Create an issue on GitHub
   - Include your OBS version, OS, and relevant log messages

3. **Check original project**:
   - Many issues may be documented at: https://github.com/BlankSourceCode/obs-zoom-to-mouse

## Next Steps

- Experiment with different Zoom Factor and Speed settings
- Try different Follow Border and Lock Sensitivity values
- Set up multiple hotkeys for different zoom levels
- Explore the script settings for advanced customization

Enjoy your new zoom capabilities! 🎥
