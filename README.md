# 🔬 USB Microscope Viewer

A web-based viewer for USB microscopes with real-time filters, zoom/pan, and snapshot capture. Designed for electronics work — inspecting solder joints, PCBs, and components.

![License](https://img.shields.io/badge/license-MIT-blue.svg)

## Features

- **Freeze Detection & Auto-Reconnect** — Detects when USB camera freezes (common when moving the camera) and auto-restarts it
- **Smooth Zoom & Pan** — Mouse wheel to zoom, drag to pan around the image
- **Real-time Image Filters** — Apply filters without freezing:
  - 🔧 **Sharpen** — Enhance fine details
  - 📐 **Edges** — Edge detection for traces
  - 🔄 **Invert** — Invert colors
  - ⚡ **Solder Mode** — Optimized for shiny solder joints, adds blue tint for copper contrast
  - ⚫ **Mono** — Grayscale
  - **Contrast, Brightness, Saturation** sliders
- **One-Click Snapshots** — Press Space or click button, auto-downloads full-res JPEG
- **Keyboard Shortcuts** — Quick filter toggles (1-5), R to reset, Space for snapshot
- **Gallery** — Sidebar with captured snapshots history

## Quick Start

```bash
# Clone the repo
git clone https://github.com/Akku-21/usb-microscope-viewer.git
cd usb-microscope-viewer

# Start a local server
python3 -m http.server 8888

# Open in browser
xdg-open http://localhost:8888/microscope.html
```

Or just open `microscope.html` directly in your browser (some browsers restrict camera access for local files).

## Usage

1. **Start Camera** — Click the button and allow camera access
2. **Zoom** — Scroll mouse wheel (0.5x to 5x)
3. **Pan** — Click and drag to move around
4. **Filters** — Use toolbar buttons or press 1-5:
   - `1` — Sharpen
   - `2` — Edges  
   - `3` — Invert
   - `4` — Solder Mode (recommended for PCB work)
   - `5` — Mono
5. **Snapshot** — Press `Space` or click 📷 button
6. **Reset** — Press `R` to reset zoom and filters

## For Solder Joint Inspection

Recommended settings:
- Enable **Solder Mode** (button or press `4`)
- Increase **Contrast** slightly (+10 to +30)
- Position microscope close to joint (10-20mm)
- Use side lighting from a desk lamp instead of ring LED
- Take snapshots and zoom in for detail

## Freeze Detection & Auto-Reconnection

**Problem:** When you move the USB microscope, the image often freezes due to USB bandwidth interruption.

**Solution:** The app now detects freezes automatically and attempts to reconnect:

1. **Automatic Detection** — Monitors frame delivery; if no frame for 1.5 seconds, declares "frozen"
2. **Auto-Reconnect** — Stops and restarts the camera automatically (up to 5 attempts)
3. **Visual Feedback** — Orange border + overlay shows "FROZEN" or "RECONNECTING" status
4. **Manual Override** — Click the 🔄 **Reconnect** button to force reconnection

The status bar shows:
- **Live** — Camera working normally
- **FROZEN** — Frame delivery stopped, attempting auto-reconnect
- **RECONNECTING...** — Actively restarting the camera

## Requirements

- Modern browser with WebRTC support (Chrome, Firefox, Edge)
- USB microscope accessible as video device (`/dev/video0` on Linux)
- Local web server (for camera permissions)

## Camera Selection

The app auto-selects the last video device (typically the microscope if you have a webcam). To use a specific device, modify the `deviceId` in the `startCamera()` function.

## License

MIT License — feel free to use, modify, distribute.

## Credits

Built for electronics hobbyists and repair work. Inspired by frustration with buggy native microscope apps.
