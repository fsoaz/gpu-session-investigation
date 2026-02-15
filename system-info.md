# System Information & Observed Behavior

## System
- Fedora Linux 43 (x86_64)
- Kernel: 6.18.9-200.fc43.x86_64
- Session: KDE Plasma (Wayland)
- GPU:
  - AMD Topaz (Discrete, 2GB, amdgpu, auto PM)
  - AMD Raven Ridge Vega 8 (Integrated, shared VRAM, primary)

## Problem
The entire Wayland session freezes (mouse, screen, compositor stops responding).  
Requires hard reboot.

## Observed Behavior
- Frequent "[drm] PCIE GART re-initialization" messages
- VA-API failure: `radeonsi_drv_video.so init failed`
- Occurs when running multiple Electron/Chromium-based applications:
  - Google Chrome
  - Warp terminal
  - Spotify (Flatpak)
  - Obsidian

## After Reboot
Previous boot logs show:
```bash
journalctl -b -1 -k | grep -Ei 'amdgpu|drm|ring|timeout|reset'
