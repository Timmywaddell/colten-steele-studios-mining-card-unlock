# P104-100 Linux gaming — GTA V final results (22 Nov 2026)

**Colten Steele Studios Mining Card Unlock Project — owner-approved final gaming update.**

## Directly captured FPS from the DXVK overlay

| Real GTA V scene | Captured FPS |
|---|---:|
| Outdoor city driving in traffic | **39.9** |
| Outdoor parking area | **51.7** |
| Driving through a tunnel | **115.8** |

The owner additionally observed **up to 135 FPS in enclosed spaces** and close to 60 FPS while walking or stopped. The 135 FPS figure is an owner report, not an independently captured frame. The owner reported running at 720p with maximum Advanced Graphics settings; the captured Linux game window was 1366×768 and exact individual graphics-menu toggles were not independently audited. The three captured FPS numbers are **different scenes**, not a matched performance comparison or overall average, and no 1%-low FPS was recorded.

## Independently verified environment

NVIDIA P104-100 8GB GP104 on ASUS B250 Mining Expert / i5-7500 / 8GB host RAM. WD Ubuntu 24.04.5 experimental Linux, NVIDIA 580.196.07, Intel HD630 physical display with NVIDIA PRIME render offload, UMU-Proton-11.0-2e, owner-supplied standalone GTA V. Genuine playable Story Mode and a working DXVK FPS overlay verified. Real physical PCIe **Gen2 ×4** (`LNKSTA=0x1042`) remained active during testing.

At the **115.8 FPS** tunnel screenshot, P104 GPU was approximately **68°C**, **86% utilized**, and using **4.58 GB VRAM**. A separate passive 3-minute telemetry capture collected **37 GPU samples and 13 screenshots**, with average GPU temperature **62.3°C**, utilization **61.6%**, VRAM **4.45 GB**, power **109.3 W**, and raw Gen2 ×4 throughout.

## Reversible tuning and limitations

Experimental CPU scheduling (`nice -2`), CPU performance governor and 2 GB LZ4 zram were tested on the WD Linux system. The owner reported better general FPS. **No controlled identical-scene A/B** was conducted, so we cannot assign a numeric FPS gain to these optimizations, nor claim Gen2 doubled game FPS. The earlier 57.6 XDamage updates/sec measurement is window-content updates, not exact rendered frames; the DXVK overlay provides direct FPS observations.

**GTA V gaming test closed at owner's request.** Next development: private Blender, Godot and CUDA workload compatibility, performance and reproducible per-card setups. No new Blender/Godot results are claimed.

Original upstream Gen2 work credited to [mai1346/p104-gen2](https://github.com/mai1346/p104-gen2). No VBIOS flash, extra lanes, extra cores or Gen3 unlock is claimed.
