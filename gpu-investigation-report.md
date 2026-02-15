
---

### **gpu-investigation-report.md**

```markdown
# GPU & Session Freeze Investigation Report

**Date:** 2026-02-15  
**System:** Fedora Linux 43  
**Kernel:** 6.18.9-200.fc43.x86_64  
**Session Type:** Wayland (KWin)

---

## 1️⃣ System Overview

**GPU Configuration (Hybrid Graphics)**

| GPU | PCI Slot | Type | VRAM | Driver | Status |
|-----|----------|------|------|--------|--------|
| AMD Topaz | 0000:01:00.0 | Discrete | 2GB | amdgpu | Suspended (auto PM) |
| AMD Raven Ridge (Vega 8) | 0000:04:00.0 | Integrated APU | Shared | amdgpu | Active (primary) |

**Graphics Stack:**  
- Mesa: 25.3.4  
- OpenGL: 4.6 (Compatibility Profile)  
- DRM: 3.64  
- GPU Switching: ATPX (vga_switcheroo)

---

## 2️⃣ Target Applications

- Spotify (Flatpak)  
- Google Chrome  
- Obsidian  

---

## 3️⃣ Logs & Findings

### a) KWin Wayland Logs
(journalctl --user -f _COMM=kwin_wayland)

**Findings:**  
- Portal registration failures (`QDBusError("org.freedesktop.portal.Error.Failed")`)  
- Repeated virtual keyboard crashes (`maliit-keyboard`)  

### b) Kernel Logs
(journalctl -kf)

**Findings:**  
- Frequent PCIE GART re-initialization (discrete GPU wake/suspend cycling)  
- `maliit-keyboard` segfaults in libQt5Core.so  

### c) System Journal

**Chrome:**  
- GLib threading errors: `g_main_context_pop_thread_default`  
- Mojo IPC rejection: `blink.mojom.WidgetHost`  
- GCM deprecated endpoint warning  
- WebGPU buffer limits warnings  

**Spotify (Flatpak):**  
- VA-API initialization failed (`radeonsi_drv_video.so`)  
- Deprecated libayatana-appindicator  

**Wireplumber:**  
- PipeWire link activation failures  

**IBus Portal:**  
- Connection failures  

### d) Boot-time GPU Initialization

**Issues Found:**  
- BIOS firmware warnings (IOAPIC not in IVRS table, `_OSI(Linux)` ignored)  
- Topaz dGPU not supported in KFD (compute)  
- Trusted Memory Zone (TMZ) not supported  
- Hybrid GPU (ATPX) power management cycling causing freezes
