# Gaming note 01 — GTA V on NVIDIA P104-100, Linux, PCIe Gen2 x4

**Colten Steele Studios Mining Card Unlock Project — 21 November 2026**

## Owner-observed gameplay result

On Dino's NVIDIA **P104-100 8 GB**, the owner reports playing **Grand Theft Auto V at 720p, with the Advanced Graphics settings maxed out, at 60 FPS**. This is a direct user-reported in-game experience, not a captured GPU per-frame benchmark or an independent test of every graphics-option toggle. The exact standard graphics menu settings, anti-aliasing, population settings and whether the frame rate remained at 60 throughout every scene have not been recorded.

## Independently verified Linux setup

- ASUS B250 Mining Expert / i5-7500 / 8 GB system RAM / NVIDIA P104-100 8 GB GP104
- Experimental Ubuntu 24.04.5 Linux, NVIDIA 580.196.07
- Physical Intel HD630 HDMI display; P104-100 NVIDIA PRIME render offload
- Actual negotiated PCIe **Gen2 x4**, raw `LNKSTA=0x1042`, following guarded manual unlock; GPU fan held at 60%
- UMU launcher 1.4.4 + pinned UMU-Proton-11.0-2e, standalone owner-supplied GTA V files on an internal storage volume, dedicated game prefix
- Full checksum comparison passed for **215 immutable source files**; three changing mod/loader logs excluded and documented
- Verified genuine GTA V Story Mode 3D gameplay, character/HUD/minimap and functional desktop launcher

## Independent live-window measurement

A passive XDamage monitor observed the running GTA V window while the owner was playing. This is **window-content update frequency**, not a direct rendered-FPS counter.

| Sample | Duration | Window updates | Average updates/sec |
|---|---:|---:|---:|
| First | 25 sec | 1,430 | 57.2 |
| Second | 20 sec | 1,162 | 58.1 |
| Combined | 45 sec | 2,592 | **57.6** |

The active display was **1366x768 at 59.79 Hz** during this earlier measurement. The owner's subsequent **720p / 60 FPS** account is a separate gameplay observation and must not be misrepresented as a 720p instrumented FPS trace.

A stronger MangoHud benchmark launcher is prepared for a future normal game launch, but there is **no accepted per-frame CSV, 1%-low or sustained 720p max-advanced trace** in this publication.

## Why this matters for the unlock project

The mining-only P104-100 ran an actual Windows DirectX game through Proton on Linux with NVIDIA graphics offload while its physical PCIe link was in the verified Gen2 x4 state. This demonstrates **functional multipurpose graphics use**, alongside separate native CUDA 12.9 SM61 compute testing and PCIe host-transfer improvements.

**Causality limit:** no matched Gen1-versus-Gen2 GTA V FPS A/B has been recorded. Do not claim the Gen2 unlock doubled game FPS. No other card's gaming performance is inferred.

## Next engineering goal (not yet achieved)

Create a reversible, version-pinned, card-specific Linux setup profile with validated GPU driver/compute, graphics/Proton, safe one-shot unlock reactivation, hardware checks, rollback and documented tests. Keep the original working drives and software intact. The P102-100 10 GB remains an untested candidate, not a P104-compatible unlock by assumption.

*Attribution: the original P104 Linux PCIe Gen2 method was developed by [mai1346/p104-gen2](https://github.com/mai1346/p104-gen2). Our contribution is independent reproduction and the above gaming/compute evidence. No world-first invention claim.*
