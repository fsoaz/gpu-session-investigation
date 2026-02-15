# System Bug Reports: GPU & Session Freeze Investigation

This repository contains detailed bug reports and system crash analyses intended to support upstream open-source projects by providing clear reproduction data, impact assessment, and technical context.

---

## Reports

| Component | Description | Status | Severity |
|-----------|-------------|--------|----------|
| AMD Topaz GPU | Discrete GPU wake/suspend cycling causing session micro-freezes | Active | High |
| Maliit Keyboard | SIGSEGV crash on Wayland input method | Active | Medium |
| Chrome | GLib threading errors, WebGPU warnings | Active | Low |
| Spotify (Flatpak) | VA-API initialization failures | Active | Medium |
| Wireplumber | PipeWire link activation failures | Active | Low |

---

### AMD Topaz GPU Session Freeze Report

Frequent wake/suspend transitions of the discrete AMD Topaz GPU under Wayland/KWin led to micro-freezes and VA-API failures in Flatpak applications. This issue is exacerbated by hybrid graphics configuration and auto runtime power management.

**Status:** Active  
**Severity:** High  
**Impact:**  
- Session freezes during application use (Chrome, Spotify)  
- VA-API hardware video decoding unavailable in Flatpaks  

**Mitigations Applied:**  
- Disabled discrete GPU wake via `DRI_PRIME=0`  
- Installed full VA-API driver stack (`mesa-va-drivers-freeworld`)  
- Validated hardware decoding support via `vainfo`

---

### Maliit Keyboard Crash Report

Recurring SIGSEGV crashes in `maliit-keyboard` affecting Wayland input method functionality.

**Status:** Active  
**Severity:** Medium  
**Impact:** On-screen keyboard unusable after crash  

**Workarounds:**  
- Remove maliit-keyboard if not needed: `sudo dnf remove maliit-keyboard`  
- Update Qt5 packages: `sudo dnf update qt5-*`

---

## Repository Structure

Each report in this repository includes:

- Crash details and stack traces  
- Environment information  
- Reproduction steps  
- Impact analysis  
- Suggested workarounds and mitigations  

---

## Audience

- Open-source maintainers  
- QA engineers  
- Linux desktop developers  

---

## License

Documentation only – public domain.
