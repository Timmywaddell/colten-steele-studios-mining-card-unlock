# Colten Steele Studios Mining Card Unlock Project

**Two verified experimental mining-GPU unlock milestones:** the P104-100 physically regained PCIe Gen2 ×4 after reboot through a guarded manual reactivation, while the CMP 70HX reproduced a GA104 tensor-unlock procedure across two Linux USB boots, retained the intended unlocked selector values after NVIDIA/CUDA initialization, and performed real BF16/FP16 tensor calculations and AI inference.

**Public research site:** [Colten Steele Studios Mining Card Unlock Project](https://headless-fzilvlsgnve-timmywaddell1-140d.wix-site-host.com)

This repository is organized **by card and by test**. We distinguish an upstream method we reproduced from a method we invented, a functional unlock-state observation from a proven performance gain, and direct PCIe bandwidth from application performance. **See the [reboot and restart evidence table](docs/reboot-status.md)** for the precise difference between P104's verified manual after-reboot activation and CMP 70HX's successful unlock reproduction on separate boot media.

## Latest update — 27 November 2026

**Project Queen:** a ฿1,430 P102-100 mining GPU is rendering GTA V at 1080p under Windows and powering our original Godot city development environment. See the [Windows gaming and Godot report](cards/p102-100.md) for observed frame rates, measured PCIe transfers, limitations and our upcoming local AI research. Independent reproductions and studio development collaborations are welcome.

## Research index

| Card | Research status | Evidence | Report |
|---|---|---|---|
| NVIDIA P104-100 8 GB (GP104) | **Reproduced:** real PCIe Gen1 x4 → Gen2 x4; repeated after reboot/manual activation | Raw PCIe LNKSTA, CUDA pinned host-transfer rates, checksum-safe test | [Research note 01](cards/p104-100.md) |
| NVIDIA CMP 70HX 8 GB (GA104) | **Unlocked state and tensor compute verified:** Zagitta method completed on two separate Linux USB boots; intended selector values read back after driver/CUDA; BF16/FP16 and Qwen3 work | Independent read-only PLM/SS0/SS1 values, BF16/FP16 CUDA arithmetic, Qwen3 inference. **No factory-locked-vs-unlocked speed gain measured** | [Research note 02](cards/cmp-70hx.md) |
| NVIDIA P102-100 10 GB (GP102) | **Windows GTA V and Godot rendering verified**; manual Gen2 transfer recovery measured | ~70–75 FPS GTA V at 1080p (owner observed); ~1.54 GB/s H2D and ~1.70 GB/s D2H; Godot Vulkan city and traffic functional | [Research note 03](cards/p102-100.md) |
| Other CMP/P-series | Planned | No result | [Test queue](ROADMAP.md) |

## Key measured achievement: P104-100

| Stage | PCIe link | Pinned host→device | Pinned device→host |
|---|---|---:|---:|
| Original | Gen1 x4 | 0.784 GB/s | 0.830 GB/s |
| First validated Gen2 | Gen2 x4 | 1.544 GB/s | 1.665 GB/s |
| Independent Gen2 repeat | Gen2 x4 | 1.536 GB/s | 1.672 GB/s |
| Reboot + manual reactivation | Gen2 x4 | 1.544 GB/s | 1.669 GB/s |

**Interpretation:** approximately 1.97x H2D and 2.01x D2H *PCIe transfer* bandwidth. Not 2x tokens/s, FPS, tensor arithmetic or GPU VRAM bandwidth. Read the [measurement method](docs/methodology.md) and [CSV](data/p104-gen2-bandwidth.csv).

## CMP 70HX is a different experiment

**The CMP 70HX tensor unlock is a confirmed working experimental result**, not merely a kernel message: the prior-art [Zagitta gpu-unlock](https://github.com/Zagitta/gpu-unlock) procedure succeeded on two independent Linux USB boots (Lexar and SanDisk), then read-only hardware-register checks after NVIDIA driver and CUDA initialization on the SanDisk setup matched all intended PLM/SS0/SS1 unlocked selector values with GSP disabled. BF16/FP16 tensor calculations and real Qwen3 local inference completed. **The missing element is a matched factory-locked performance baseline**; that prevents us quantifying an unlock-caused speedup or claiming a world-first invention. We have also not demonstrated automatic reactivation after every reboot. The CMP's PCIe remained Gen1 x4. See [CMP 70HX observed performance](data/cmp70hx-observed.csv) and [the three independently read back unlocked feature selectors](data/cmp70hx-unlocked-selectors.csv).

## Attribution

The original P104 Linux Gen2 method was developed by [mai1346/p104-gen2](https://github.com/mai1346/p104-gen2), building on earlier work including [WJNKAC](https://github.com/WJNKAC) and [skbskhud/p104-unlock-v3](https://github.com/skbskhud/p104-unlock-v3). The GA104 tensor-unlock implementation belongs to [Zagitta/gpu-unlock](https://github.com/Zagitta/gpu-unlock). Additional mining-card graphics work exists in [Icyoung/cmpunlocker](https://github.com/Icyoung/cmpunlocker). Their upstream work is not our invention.

Our own contribution is **independent test evidence**, including an ASUS B250 + Linux 7.0/NVIDIA 580.196.07 P104 reproduction, fan-safe manual reactivation after reboot, repeated measurements, and specific local CMP 70HX observations with explicit limitations.

## Experimental caution

These are high-risk, version-specific hardware experiments, not universal installation instructions. Changing PCIe registers, rebinding a GPU, or modifying NVIDIA driver modules can hang a machine. **Do not run upstream installers unchanged on different GPUs, drivers or PCI addresses.** We are not publishing private host credentials, device serial numbers, personal screenshots or raw Office logs.

No original driver blobs, firmware dumps, third-party copyrighted files, passwords or private keys are included. The absence of a dedicated license means that reuse permissions beyond ordinary GitHub viewing and forking have not been granted; the project owner can choose licenses later.

*Colten Steele Studios · First publication 21 November 2026*

