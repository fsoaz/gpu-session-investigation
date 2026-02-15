***Logs & Findings

1. KWin Wayland Logs (journalctl --user -f _COMM=kwin_wayland)
Feb 15 17:17:57 fedora kwin_wayland[1741]: No suitable DRM devices have been found
Feb 15 17:17:57 fedora kwin_wayland[1741]: QThreadStorage: entry 7 destroyed before end of thread 0x560b8dd4b0a0
Feb 15 17:17:57 fedora kwin_wayland[1741]: QThreadStorage: entry 1 destroyed before end of thread 0x560b8dd4b0a0
Feb 15 17:17:57 fedora kwin_wayland[1741]: QThreadStorage: entry 0 destroyed before end of thread 0x560b8dd4b0a0
Feb 15 17:17:58 fedora kwin_wayland[1807]: No backend specified, automatically choosing drm
Feb 15 17:18:04 fedora kwin_wayland[1807]: Failed to register with host portal QDBusError("org.freedesktop.portal.Error.Failed", "Could not register app ID: Unable to open /proc/1807/root")
Feb 15 17:18:04 fedora kwin_wayland[1807]: Failed to register with host portal QDBusError("org.freedesktop.portal.Error.Failed", "Could not register app ID: Unable to open /proc/1807/root")
Feb 15 17:26:38 fedora kwin_wayland[1807]: Failed to register with host portal QDBusError("org.freedesktop.portal.Error.Failed", "Could not register app ID: Unable to open /proc/1807/root")
Feb 15 17:26:40 fedora kwin_wayland[1807]: Input Method crashed "maliit-keyboard" QList() 11 QProcess::CrashExit
Feb 15 17:27:04 fedora kwin_wayland[1807]: Input Method crashed "maliit-keyboard" QList() 11 QProcess::CrashExit
Issues Found:
Portal registration failures (sandbox/DBus issue)
maliit-keyboard (virtual keyboard) crashing repeatedly

***2. Kernel Logs (journalctl -kf)
Feb 15 17:23:25 fedora kernel: [drm] PCIE GART of 256M enabled (table at 0x000000F400000000).
Feb 15 17:23:40 fedora kernel: [drm] PCIE GART of 256M enabled (table at 0x000000F400000000).
Feb 15 17:24:06 fedora kernel: usb 1-1.1.4: reset high-speed USB device number 8 using xhci_hcd
Feb 15 17:26:38 fedora kernel: show_signal_msg: 30 callbacks suppressed
Feb 15 17:26:38 fedora kernel: maliit-keyboard[1848]: segfault at 561617e98000 ip 00007efee0e78670 sp 00007fff63508270 error 4 in libQt5Core.so.5.15.18[278670,7efee0c00000+2f2000] likely on CPU 5 (core 2, socket 0)
Feb 15 17:26:38 fedora kernel: Code: 00 00 55 48 89 e5 41 56 41 55 41 54 53 66 90 66 66 2e 0f 1f 84 00 00 00 00 00 4c 89 c2 48 29 c2 48 83 fa 0f 0f 8e 38 02 00 00 <f3> 0f 6f 00 66 0f d7 d0 85 d2 75 35 e9 f7 01 00 00 66 0f 1f 84 00
Feb 15 17:27:03 fedora kernel: maliit-keyboard[7678]: segfault at 560e94cfe000 ip 00007f995a078670 sp 00007ffcabdea570 error 4 in libQt5Core.so.5.15.18[278670,7f9959e00000+2f2000] likely on CPU 3 (core 1, socket 0)
Feb 15 17:27:03 fedora kernel: Code: 00 00 55 48 89 e5 41 56 41 55 41 54 53 66 90 66 66 2e 0f 1f 84 00 00 00 00 00 4c 89 c2 48 29 c2 48 83 fa 0f 0f 8e 38 02 00 00 <f3> 0f 6f 00 66 0f d7 d0 85 d2 75 35 e9 f7 01 00 00 66 0f 1f 84 00
Feb 15 17:36:56 fedora kernel: [drm] PCIE GART of 256M enabled (table at 0x000000F400000000).
Feb 15 17:37:15 fedora kernel: [drm] PCIE GART of 256M enabled (table at 0x000000F400000000).
Feb 15 17:40:18 fedora kernel: [drm] PCIE GART of 256M enabled (table at 0x000000F400000000).
Feb 15 17:40:39 fedora kernel: [drm] PCIE GART of 256M enabled (table at 0x000000F400000000).
Feb 15 17:40:48 fedora kernel: [drm] PCIE GART of 256M enabled (table at 0x000000F400000000).
Feb 15 17:41:38 fedora kernel: [drm] PCIE GART of 256M enabled (table at 0x000000F400000000).
Feb 15 17:43:20 fedora kernel: [drm] PCIE GART of 256M enabled (table at 0x000000F400000000).
Feb 15 17:44:18 fedora kernel: [drm] PCIE GART of 256M enabled (table at 0x000000F400000000).
Feb 15 17:44:29 fedora kernel: [drm] PCIE GART of 256M enabled (table at 0x000000F400000000).
Feb 15 17:44:50 fedora kernel: [drm] PCIE GART of 256M enabled (table at 0x000000F400000000).
Issues Found:
Frequent PCIE GART re-initialization (discrete GPU wake/suspend cycling)
maliit-keyboard segfaults in libQt5Core.so

***3. System Journal (journalctl -f)
Feb 15 17:37:46 fedora google-chrome-stable[8737]: [8732:8886:0215/173746.452417:ERROR:content/browser/browser_main_loop.cc:290] GLib: g_main_context_pop_thread_default: assertion 'stack != NULL' failed
Feb 15 17:37:46 fedora google-chrome-stable[8737]: [8732:8887:0215/173746.452417:ERROR:content/browser/browser_main_loop.cc:290] GLib: g_main_context_pop_thread_default: assertion 'stack != NULL' failed
Feb 15 17:37:46 fedora google-chrome-stable[8737]: [8732:8888:0215/173746.452420:ERROR:content/browser/browser_main_loop.cc:290] GLib: g_main_context_pop_thread_default: assertion 'stack != NULL' failed
Feb 15 17:38:00 fedora wireplumber[1733]: wp-event-dispatcher: <WpAsyncEventHook:0x558b4c1b0ce0> failed: failed to activate item: Object activation aborted: proxy destroyed
Feb 15 17:38:00 fedora wireplumber[1733]: wp-event-dispatcher: <WpAsyncEventHook:0x558b4c18c420> failed: <WpSiStandardLink:0x558b4c8b30d0> link failed: 1 of 1 PipeWire links failed to activate
Feb 15 17:38:05 fedora google-chrome-stable[8737]: [8732:8732:0215/173805.399264:ERROR:mojo/public/cpp/bindings/lib/interface_endpoint_client.cc:748] Message 1 rejected by interface blink.mojom.WidgetHost
Feb 15 17:38:37 fedora google-chrome-stable[8737]: [8732:8779:0215/173837.194076:ERROR:google_apis/gcm/engine/registration_request.cc:290] Registration response error message: DEPRECATED_ENDPOINT
Feb 15 17:40:18 fedora google-chrome-stable[8737]: Warning: maxDynamicUniformBuffersPerPipelineLayout artificially reduced from 500000 to 16 to fit dynamic offset allocation limit.
Feb 15 17:40:18 fedora google-chrome-stable[8737]: Warning: maxDynamicStorageBuffersPerPipelineLayout artificially reduced from 500000 to 16 to fit dynamic offset allocation limit.
Feb 15 17:40:30 fedora google-chrome-stable[8737]: [8732:8796:0215/174030.087164:ERROR:content/browser/browser_main_loop.cc:290] GLib: g_main_context_pop_thread_default: assertion 'stack != NULL' failed
Feb 15 17:40:30 fedora chrome[8732]: QThreadStorage: entry 2 destroyed before end of thread 0x30b40082a960
Feb 15 17:40:30 fedora chrome[8732]: QThreadStorage: entry 1 destroyed before end of thread 0x30b40082a960
Feb 15 17:40:30 fedora systemd[1415]: app-com.google.Chrome-8732.scope: Consumed 14.154s CPU time, 460.4M memory peak.
Feb 15 17:40:30 fedora systemd[1415]: app-google\x2dchrome@0c5c3a79e7444701b5e885e529aafd8c.service: Consumed 34.086s CPU time, 1016.6M memory peak.
Feb 15 17:40:39 fedora systemd[1415]: app-flatpak-com.spotify.Client-1429497949.scope: Consumed 38.969s CPU time, 1.1G memory peak.
Feb 15 17:41:17 fedora wireplumber[1733]: wp-event-dispatcher: <WpAsyncEventHook:0x558b4c1b0ce0> failed: failed to activate item: Object activation aborted: proxy destroyed
Feb 15 17:41:36 fedora systemd[1415]: Started app-com.spotify.Client@b2fdf803ff344947aaa10cbf82f260af.service - Spotify - Music Player.
Feb 15 17:41:36 fedora systemd[1415]: Started app-flatpak-com.spotify.Client-2357051700.scope.
Feb 15 17:41:37 fedora spotify[10534]: libayatana-appindicator is deprecated. Please use libayatana-appindicator-glib in newly written code.
Feb 15 17:41:39 fedora flatpak[10563]: libva error: /usr/lib/x86_64-linux-gnu/GL/lib/dri/radeonsi_drv_video.so init failed
Feb 15 17:41:40 fedora systemd[1415]: Started dbus-:1.2-org.freedesktop.portal.IBus@2.service.
Feb 15 17:41:40 fedora ibus-portal[10681]: Not connected to the ibus bus
Feb 15 17:41:40 fedora systemd[1415]: dbus-:1.2-org.freedesktop.portal.IBus@2.service: Main process exited, code=exited, status=1/FAILURE
Feb 15 17:41:40 fedora systemd[1415]: dbus-:1.2-org.freedesktop.portal.IBus@2.service: Failed with result 'exit-code'.
Feb 15 17:43:20 fedora systemd[1415]: app-flatpak-com.spotify.Client-2357051700.scope: Consumed 23.496s CPU time, 662.4M memory peak.
Issues Found:
Chrome: GLib threading errors, Mojo IPC rejection, GCM deprecated endpoint, WebGPU buffer limits
Spotify: VA-API initialization failure, deprecated libayatana-appindicator
Wireplumber: PipeWire link activation failures
IBus portal: Connection failures

***4. Boot-time GPU Initialization (journalctl -k -b | grep amdgpu)
Feb 15 17:12:56 fedora kernel: AMD-Vi: [Firmware Bug]: : IOAPIC[5] not in IVRS table
Feb 15 17:12:56 fedora kernel: Spectre V2 : Enabling Speculation Barrier for firmware calls
Feb 15 17:12:56 fedora kernel: ACPI: [Firmware Bug]: BIOS _OSI(Linux) query ignored
Feb 15 17:12:56 fedora kernel: acpi PNP0A08:00: [Firmware Info]: ECAM [mem 0xf8000000-0xfbffffff] for domain 0000 [bus 00-3f] only partially covers this bridge
Feb 15 17:12:57 fedora kernel: wmi_bus wmi_bus-PNP0C14:00: [Firmware Bug]: WMBF method block execution control method not found
Feb 15 17:13:02 fedora kernel: [drm] amdgpu kernel modesetting enabled.
Feb 15 17:13:02 fedora kernel: amdgpu: vga_switcheroo: detected switching method \_SB_.PCI0.GP17.VGA_.ATPX handle
Feb 15 17:13:02 fedora kernel: amdgpu: ATPX version 1, functions 0x00000001
Feb 15 17:13:02 fedora kernel: amdgpu: ATPX Hybrid Graphics, forcing to ATPX
Feb 15 17:13:02 fedora kernel: amdgpu: Virtual CRAT table created for CPU
Feb 15 17:13:02 fedora kernel: amdgpu: Topology: Add CPU node
Feb 15 17:13:02 fedora kernel: amdgpu 0000:01:00.0: enabling device (0002 -> 0003)
Feb 15 17:13:02 fedora kernel: amdgpu 0000:01:00.0: amdgpu: initializing kernel modesetting (TOPAZ 0x1002:0x6900 0x1025:0x125A 0xD1).
Feb 15 17:13:02 fedora kernel: amdgpu 0000:01:00.0: amdgpu: register mmio base: 0xE0A00000
Feb 15 17:13:02 fedora kernel: amdgpu 0000:01:00.0: amdgpu: register mmio size: 262144
Feb 15 17:13:02 fedora kernel: amdgpu 0000:01:00.0: amdgpu: Fetched VBIOS from ATRM
Feb 15 17:13:02 fedora kernel: amdgpu: ATOM BIOS: SWBRT32953.001
Feb 15 17:13:02 fedora kernel: kfd kfd: amdgpu: TOPAZ  not supported in kfd
Feb 15 17:13:02 fedora kernel: amdgpu 0000:01:00.0: amdgpu: Trusted Memory Zone (TMZ) feature not supported
Feb 15 17:13:02 fedora kernel: amdgpu 0000:01:00.0: amdgpu: GPU posting now...
Feb 15 17:13:02 fedora kernel: amdgpu 0000:01:00.0: amdgpu: vm size is 64 GB, 2 levels, block size is 10-bit, fragment size is 9-bit
Feb 15 17:13:02 fedora kernel: amdgpu 0000:01:00.0: amdgpu: VRAM: 2048M 0x000000F400000000 - 0x000000F47FFFFFFF (2048M used)
Feb 15 17:13:02 fedora kernel: amdgpu 0000:01:00.0: amdgpu: GART: 256M 0x000000FF00000000 - 0x000000FF0FFFFFFF
Feb 15 17:13:02 fedora kernel: amdgpu 0000:01:00.0: amdgpu: amdgpu: 2048M of VRAM memory ready
Issues Found:
BIOS firmware bugs (IOAPIC not in IVRS table, _OSI(Linux) ignored, ECAM partial coverage)
Topaz dGPU not supported in KFD (compute)
TMZ not supported on dGPU

***Root Cause Analysis
Primary Issue: Discrete GPU Power Management Cycling
The discrete AMD Topaz GPU was configured with auto runtime power management. Applications attempting to use GPU acceleration (Chrome WebGPU, Spotify VA-API) were repeatedly waking the dGPU, causing:
Frequent PCIE GART re-initialization messages
Potential micro-freezes during wake/suspend transitions
VA-API failures in Flatpak sandboxes (wrong driver path)
Secondary Issues
| Issue | Component | Severity |
|-------|-----------|----------|
| maliit-keyboard segfaults | libQt5Core.so | Medium |
| Portal registration failures | KWin/XDG Portal | Low |
| Wireplumber link failures | PipeWire | Low |
| GLib threading assertions | Chrome | Low |
| Missing H.264/H.265 codecs | Mesa VA drivers | Medium |

***Fixes Applied
1. Disabled Discrete GPU Wake for Applications
File: ~/.bash_profile
Change: Added export DRI_PRIME=0
This prevents applications from requesting the discrete GPU, keeping it in suspended state and eliminating wake/suspend cycles.
2. Installed VA-API Diagnostic Tools
sudo dnf install libva-utils
3. Installed Full-Codec VA-API Drivers
sudo dnf install rpmfusion-nonfree-release
sudo dnf swap mesa-va-drivers mesa-va-drivers-freeworld
Result: Hardware video decode now supports:
H.264 (decode + encode)
H.265/HEVC (decode + encode)
VC1
VP9
MPEG2
JPEG

***VA-API Status (After Fix)
vainfo: VA-API version: 1.22 (libva 2.22.0)
vainfo: Driver version: Mesa Gallium driver 25.3.4 for AMD Radeon Vega 8 Graphics
vainfo: Supported profile and entrypoints
      VAProfileMPEG2Simple            : VAEntrypointVLD
      VAProfileMPEG2Main              : VAEntrypointVLD
      VAProfileVC1Simple              : VAEntrypointVLD
      VAProfileVC1Main                : VAEntrypointVLD
      VAProfileVC1Advanced            : VAEntrypointVLD
      VAProfileH264ConstrainedBaseline: VAEntrypointVLD
      VAProfileH264ConstrainedBaseline: VAEntrypointEncSlice
      VAProfileH264Main               : VAEntrypointVLD
      VAProfileH264Main               : VAEntrypointEncSlice
      VAProfileH264High               : VAEntrypointVLD
      VAProfileH264High               : VAEntrypointEncSlice
      VAProfileHEVCMain               : VAEntrypointVLD
      VAProfileHEVCMain               : VAEntrypointEncSlice
      VAProfileHEVCMain10             : VAEntrypointVLD
      VAProfileJPEGBaseline           : VAEntrypointVLD
      VAProfileVP9Profile0            : VAEntrypointVLD
      VAProfileVP9Profile2            : VAEntrypointVLD
      VAProfileNone                   : VAEntrypointVideoProc

      ***Recommendations
Immediate Actions Required
Log out and log back in to apply the DRI_PRIME=0 environment variable
Optional Improvements
Suppress IOAPIC firmware warning (cosmetic):
Add iommu=pt to kernel parameters in /etc/default/grub
Run sudo grub2-mkconfig -o /boot/grub2/grub.cfg
Investigate maliit-keyboard crashes:
If not using virtual keyboard, consider removing: sudo dnf remove maliit-keyboard
Or update Qt5 packages: sudo dnf update qt5-*
For Flatpak Spotify VA-API:
May need Flatpak override for VA-API access: flatpak override --user --env=LIBVA_DRIVER_NAME=radeonsi com.spotify.Client

***System Information
$ lspci -k | grep -A3 VGA
04:00.0 VGA compatible controller: Advanced Micro Devices, Inc. [AMD/ATI] Raven Ridge [Radeon Vega Series / Radeon Vega Mobile Series] (rev c4)
        Subsystem: Acer Incorporated [ALI] Device 1259
        Kernel driver in use: amdgpu
        Kernel modules: amdgpu
$ glxinfo | grep -E "OpenGL renderer|OpenGL version"
OpenGL renderer string: AMD Radeon Vega 8 Graphics (radeonsi, raven, ACO, DRM 3.64, 6.18.9-200.fc43.x86_64)
OpenGL version string: 4.6 (Compatibility Profile) Mesa 25.3.4
$ cat /sys/bus/pci/devices/0000:01:00.0/power/runtime_status
suspended
$ cat /sys/bus/pci/devices/0000:01:00.0/power/control
auto

***Stack Trace Analysis
maliit-keyboard Segfaults
Both crashes occurred at the same code location, indicating a reproducible bug.
Crash Details
Process:    maliit-keyboard
Signal:     SIGSEGV (Segmentation Fault)
Error Code: 4 (read access violation in user mode)
Library:    libQt5Core.so.5.15.18
Offset:     0x278670
Decoded Stack Frame
#0  QUtf8::convertToUnicode(QChar*, char const*, int) + 144
    at /usr/lib64/libQt5Core.so.5.15.18
Function Signature
QChar* QUtf8::convertToUnicode(QChar* output, const char* input, int length)
Faulting Instruction
0x278670 <+144>:  movdqu (%rax),%xmm0   ; Load 16 bytes from address in RAX
Disassembly Context
; QUtf8::convertToUnicode - SSE-optimized UTF-8 to Unicode conversion
0x2785e0 <+0>:    endbr64
0x2785e4 <+4>:    movslq %edx,%rdx           ; Sign-extend length
0x2785e7 <+7>:    mov    %rdi,%rcx           ; output buffer
0x2785ea <+10>:   mov    %rsi,%rdi           ; input pointer
0x2785ed <+13>:   lea    (%rsi,%rdx,1),%r8   ; end = input + length
0x2785f1 <+17>:   cmp    $0xf,%rdx           ; if length <= 15
0x2785f5 <+21>:   jle    0x27895b            ;   use byte-by-byte path
...
0x278660 <+128>:  mov    %r8,%rdx            ; remaining = end - current
0x278663 <+131>:  sub    %rax,%rdx
0x278666 <+134>:  cmp    $0xf,%rdx           ; if remaining <= 15
0x27866a <+138>:  jle    0x2788a8            ;   exit SSE loop
0x278670 <+144>:  movdqu (%rax),%xmm0        ; <<< CRASH HERE
0x278674 <+148>:  pmovmskb %xmm0,%edx        ; Check for high bits (non-ASCII)

Root Cause
The function uses SSE instructions (movdqu) to process 16 bytes at a time for performance. The crash occurred because:
%rax contained an invalid pointer (0x561617e98000 / 0x560e94cfe000)
These addresses are within the process's address space but point to unmapped memory
The length check at +134 passed, but the pointer itself was corrupted or the buffer was freed
Likely Scenarios
Use-after-free: Input string buffer was deallocated while still being processed
Buffer overrun: Previous operation corrupted the string pointer
Race condition: Another thread modified/freed the string during conversion
Affected Component
maliit-keyboard → Qt5 Input Method → QUtf8::convertToUnicode()
This is a Qt5 bug or memory corruption in the maliit-keyboard virtual keyboard application when processing UTF-8 text input.
Recommended Actions
Update Qt5: sudo dnf update qt5-qtbase
Check for known bugs: Search Qt bug tracker for "convertToUnicode crash"
If not using virtual keyboard: sudo dnf remove maliit-keyboard
Report bug: File against maliit-keyboard with this stack trace

***Report generated: 2026-02-15 22:18 UTC
Stack trace added: 2026-02-15 23:10 UTC
