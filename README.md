# Colten Steele Studios Mining Card Unlock Project

**Three documented experimental mining-GPU milestones:** Queen's P102-100 automatically recovered Gen2 ×4 after a Windows restart/sign-in with passing PCI and CUDA checks;  the P104-100 physically regained PCIe Gen2 ×4 after reboot through a guarded manual reactivation, while the CMP 70HX reproduced a GA104 tensor-unlock procedure across two Linux USB boots, retained the intended unlocked selector values after NVIDIA/CUDA initialization, and performed real BF16/FP16 tensor calculations and AI inference.

**Public research site:** [Colten Steele Studios Mining Card Unlock Project](https://headless-fzilvlsgnve-timmywaddell1-140d.wix-site-host.com)

This repository is organized **by card and by test**. We distinguish an upstream method we reproduced from a method we invented, a functional unlock-state observation from a proven performance gain, and direct PCIe bandwidth from application performance. **See the [reboot and restart evidence table](docs/reboot-status.md)** for the precise difference between P104's verified manual after-reboot activation and CMP 70HX's successful unlock reproduction on separate boot media.

## Latest update — 28 November 2026: Project Queen, from mining GPU to local AI workstation

**Full 27B reasoning on a THB 1,430 mining GPU.** Queen now runs Bonsai 2.5 27B with 32K configured context on the P102-100, plus persistent CUDA Whisper on a separate GT 1030, on Windows with only 8 GB RAM. Measured decode: 18.94 tokens/s. A later snapshot retained ~5.5 GiB available RAM with both engines resident. The current run recorded 3,049/3,049 sampled physical Gen2 x4 observations across 2 h 36 min.

- [Queen Windows AI: measured results, exact configuration and replication recipe](docs/queen-windows-ai.md)
- [Measurement CSV](data/queen-ai-20261128.csv) · [Complete 3,049-row sanitized PCIe trace](data/queen-physical-pcie-20261128.csv)
- [Replicate, report a failure or correct our findings](https://github.com/Timmywaddell/colten-steele-studios-mining-card-unlock/issues)

We might be among the first to document this particular Windows mining-GPU gaming, Godot and dual-GPU AI configuration; worldwide precedence is unverified. No MTP speed claim, full-context recall claim, or measured Blender performance yet. The complete new AI/game reboot sequence still needs fresh acceptance.

## Earlier update — 27 November 2026

**Project Queen:** a ฿1,430 P102-100 mining GPU is rendering GTA V at 1080p under Windows and powering our original Godot city development environment. See the [Windows gaming and Godot report](cards/p102-100.md) for observed frame rates, measured PCIe transfers, limitations and the new [local AI research](docs/queen-windows-ai.md). Independent reproductions and studio development collaborations are welcome.

**Reboot success — 27 November:** automatic Windows logon recovery restored Gen2 ×4 at both PCI ends; five pinned CUDA trials passed at 1.542–1.551 GB/s H2D and 1.669–1.673 GB/s D2H, with zero arithmetic errors. The owner confirmed everything working after reboot. [Read the measured acceptance record](docs/reboot-status.md#verified-windows-reboot-recovery--27-november-2026).

## Budget gaming and local AI workstations — three systems, ฿23,261 in recorded spending

| Workstation | Mining GPU | GPU purchase | Recorded system/project cost | Demonstrated work |
|---|---|---:|---:|---|
| Dino | P104-100 8 GB | ฿800 | ฿6,260 | Linux gaming, PCIe research |
| Harry | CMP 70HX 8 GB | ฿1,400 | ฿10,288 | Tensor compute and local AI inference |
| Queen | P102-100 10 GB | ฿1,430 | ฿6,713 | Windows gaming, Godot, 27B local AI + GPU speech |
| **Total** | | | **฿23,261** | |

**Dino:** motherboard with 8 GB RAM and cooler ฿1,000; CPU ฿1,400; P104 ฿800; SSD ฿580; PSU ฿1,400; three fans ฿80; case ฿1,000. Mechanical drives, cabling and remaining components supplied free.

**Harry:** motherboard, CPU, 16 GB RAM and cooler bundle ฿3,288; CMP 70HX ฿1,400; case ฿1,200; GTX 1660 Super ฿3,200; PSU ฿1,200.

**Queen:** earlier project spending ฿5,200, updated committed total ฿6,713 including NVMe, delivery and a ฿190 Studio replacement PSU. GT 1030, fans, mechanical drives, keyboard and mouse supplied free.

Prices are owner-confirmed historical Thai baht expenditure, with Queen's total supported by the project ledger; not independently audited receipts or current retail replacement costs. Reused/free equipment is not valued at market price. Queen's AI measurements are now [published separately](docs/queen-windows-ai.md).

## Reversible, restart-recoverable research — our engineering standard

Our goal is working solutions that survive ordinary use, with documented recovery after restart rather than one-off demonstrations. Dino and Harry have working Windows and Linux installations according to the owner; their Linux unlock evidence is documented separately. Dino demonstrated manual Gen2 recovery after reboot, Harry reproduced tensor unlocking on two Linux boot environments, and Queen demonstrated reversible Gen2 transfer behavior during a Windows session alongside GTA V and Godot rendering. The owner subsequently confirms automatic Linux tensor-unlock recovery on Harry, Linux Gen2 recovery on Dino, and a rebootable Windows unlock setup on Queen. Queen has now passed that gate for one Windows restart/sign-in: fresh endpoint/root Gen2 ×4, transfer integrity PASS and zero CUDA arithmetic errors. Repeated-cycle and cold-power-cycle qualification remain open; Harry's automatic recovery retains its separate owner-reported classification. We may be among the first to document this particular combination, but global priority is unverified. See the [recovery evidence matrix](docs/reboot-status.md) for exactly what each card has demonstrated.

## Research index

| Card | Research status | Evidence | Report |
|---|---|---|---|
| NVIDIA P104-100 8 GB (GP104) | **Reproduced:** real PCIe Gen1 x4 → Gen2 x4; repeated after reboot/manual activation | Raw PCIe LNKSTA, CUDA pinned host-transfer rates, checksum-safe test | [Research note 01](cards/p104-100.md) |
| NVIDIA CMP 70HX 8 GB (GA104) | **Unlocked state and tensor compute verified:** Zagitta method completed on two separate Linux USB boots; intended selector values read back after driver/CUDA; BF16/FP16 and Qwen3 work | Independent read-only PLM/SS0/SS1 values, BF16/FP16 CUDA arithmetic, Qwen3 inference. **No factory-locked-vs-unlocked speed gain measured** | [Research note 02](cards/cmp-70hx.md) |
| NVIDIA P102-100 10 GB (GP102) | **Windows automatic Gen2 reboot recovery verified**, alongside GTA V, Godot rendering and new 27B AI evidence | ~70–75 FPS GTA V at 1080p (owner observed); ~1.54 GB/s H2D and ~1.70 GB/s D2H; Godot Vulkan city and traffic functional | [Research note 03](cards/p102-100.md) |
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

## Replicate our budget mining GPU research

| Test system | Motherboard / BIOS | Operating system and driver |
|---|---|---|
| Dino / P104-100 | ASUS B250 Mining Expert; motherboard BIOS revision pending confirmation; GPU VBIOS 86.04.7A.00.19 | Ubuntu 24.04.5.1, kernel 7.0.0-31-generic, NVIDIA 580.196.07 |
| Harry / CMP 70HX | Gigabyte Z270X Ultra Gaming; motherboard BIOS revision pending confirmation | Ubuntu 24.04.5, kernel 7.0.0-31-generic, NVIDIA 580.178.04 for the post-bind selector test |
| Queen / P102-100 + GT 1030 | ASRock B365 Pro4; AMI P1.00 (live readback, 27 November) | Windows 10 Pro build 19045, NVIDIA 582.78 (32.0.15.8278), game-local DXVK 2.6.2 |

The [P104 recovery report](cards/p104-100.md), [CMP tensor report](cards/cmp-70hx.md), [Windows dual-GPU checklist](cards/p102-100.md#reproduce-the-windows-dual-gpu-approach) and [recovery evidence matrix](docs/reboot-status.md) describe the card-specific workflow. For independent replication: (1) record exact board, BIOS/VBIOS, OS, GPU and driver; (2) preserve a known-good backup and normal boot path; (3) capture baseline transfer or compute results; (4) follow the applicable upstream project's documented prerequisites and recovery guidance, not another card's procedure; (5) verify actual GPU identity, link state or functional tensor computation and numerical integrity; (6) verify restart recovery and repeat the same workload. Keep security protections intact; stop if the system becomes unstable. Queen's dated automatic restart sequence and results are documented in the recovery evidence matrix. A portable installer and independent reproduction on another machine are not yet released.

**Prior art and our contribution:** [mai1346/p104-gen2](https://github.com/mai1346/p104-gen2) and earlier P104 researchers established the Gen2 technique; [Zagitta/gpu-unlock](https://github.com/Zagitta/gpu-unlock) established the GA104 tensor method; [KODAMA Technology](https://github.com/KODAMA-TECHNOLOGY/P102-PCIE2.0ULOCKER) published P102 Gen2 work; [DXVK](https://github.com/doitsujin/dxvk) provides the graphics translation layer. Our contribution is the card-specific integration, guarded recovery, independently measured transfers, functional tensor tests, Windows dual-GPU GTA V and Godot demonstration, and budget build evidence. We may be among the first to document this particular combination; global priority is not established.

**Help the community:** [Submit a replication report or correction](https://github.com/Timmywaddell/colten-steele-studios-mining-card-unlock/issues). Include GPU and board models, BIOS/VBIOS, driver and OS/kernel versions, baseline and after-test measurements, restart outcome (manual or automatic), temperatures, and sanitized errors or logs. Include failures as well as successes. Remove credentials, private IPs, serial numbers, personal paths and payment details. Please do not upload copyrighted driver/game binaries or unreviewed kernel tools. We welcome independent reproductions and development collaborations.

## Attribution

The original P104 Linux Gen2 method was developed by [mai1346/p104-gen2](https://github.com/mai1346/p104-gen2), building on earlier work including [WJNKAC](https://github.com/WJNKAC) and [skbskhud/p104-unlock-v3](https://github.com/skbskhud/p104-unlock-v3). The GA104 tensor-unlock implementation belongs to [Zagitta/gpu-unlock](https://github.com/Zagitta/gpu-unlock). Additional mining-card graphics work exists in [Icyoung/cmpunlocker](https://github.com/Icyoung/cmpunlocker). Their upstream work is not our invention.

Our own contribution is **independent test evidence**, including an ASUS B250 + Linux 7.0/NVIDIA 580.196.07 P104 reproduction, fan-safe manual reactivation after reboot, repeated measurements, and specific local CMP 70HX observations with explicit limitations.

## Experimental caution

These are high-risk, version-specific hardware experiments, not universal installation instructions. Changing PCIe registers, rebinding a GPU, or modifying NVIDIA driver modules can hang a machine. **Do not run upstream installers unchanged on different GPUs, drivers or PCI addresses.** We are not publishing private host credentials, device serial numbers, personal screenshots or raw Office logs.

No original driver blobs, firmware dumps, third-party copyrighted files, passwords or private keys are included. The absence of a dedicated license means that reuse permissions beyond ordinary GitHub viewing and forking have not been granted; the project owner can choose licenses later.

*Colten Steele Studios · First publication 21 November 2026*

