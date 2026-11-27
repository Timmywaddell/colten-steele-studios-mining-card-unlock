# Boot, reboot recovery and reversible operation — P104, CMP 70HX and P102

The phrase **"reboot-able unlock"** can describe two different achievements:
1. The same environment can boot safely, then a user can deliberately reapply the unlock and verify operation.
2. An unlock activates and validates **automatically** every time the system boots without human intervention.

Neither case requires that the GPU retains modified volatile registers physically through a power cycle. The data below keeps these meanings distinct.

| GPU | Evidence of unlock after a fresh boot | Post-driver proof | Automatic start proven? |
|---|---|---|---|
| **NVIDIA P104-100 8 GB** | **YES.** A real WD Linux reboot returned the GPU to Gen1 ×4, then a guarded manual one-shot activation restored physical Gen2 ×4. A new 8 MiB ×5 CUDA copy benchmark passed at H2D 1.544 / D2H 1.669 GB/s. | Raw link status 0x1042 confirmed again after CUDA initialization; temporary kernel hook removed and original driver file on disk retained. | **NO.** The systemd unit is intentionally manual/static. |
| **NVIDIA CMP 70HX 8 GB** | **YES, for independent boot reproduction.** The upstream Zagitta kernel procedure reported successful unlock on an original Lexar Linux boot and again on a distinct SanDisk Linux boot. | On SanDisk with NVIDIA proprietary driver 580.178.04 and CUDA initialized and GSP turned off, **PLM=FFFFFFFF, SS0=88888888, SS1=00000008** matched the intended unlocked state in independent read-only checks. Real BF16/FP16 tensor calculations and Qwen3 inference passed. | **NOT TESTED.** Automatic reactivation after every restart, and same-media repeat after a controlled fresh power cycle, were not separately accepted as test gates. |
| **NVIDIA P102-100 10 GB** | **YES: automatic recovery after a real Windows restart/sign-in on 27 November 2026.** Earlier live stop/reactivation also verified. | Fresh endpoint and root Gen2 ×4, training=false; five pinned trials H2D 1.542–1.551 and D2H 1.669–1.673 GB/s; pageable/pinned integrity PASS; CUDA arithmetic zero errors. | **YES, one measured restart.** Existing logon task automatically recovered and validated the link. Owner confirmed usability. Cold power-cycle, repeated-cycle endurance and new controlled gaming benchmarks remain open. |


## Project-wide recovery standard

Our engineering objective is not a one-time unlock: it is a usable, reversible configuration that can be restored safely after restarting. The owner reports working Windows and Linux installations on both Dino and Harry. That is distinct from proving every unlock in both operating systems. For each card and OS, record a clean boot, driver initialization, baseline, activation, hardware readback where available, integrity-checked workload, and a subsequent restart/recovery. Where live stop and reactivation are supported, document them separately. Do not assume a safe live transition during an active GPU workload. Publish exact versions, rollback guidance and evidence of any required manual step. Use “may be a first” only as a qualified hypothesis, never an established global precedence claim.

## Later owner-confirmed recovery milestones — 27 November 2026

The owner confirms that Harry's CMP 70HX tensor unlock automatically returns on Linux reboot and remains usable, that Dino's P104 Gen2 unlock is recoverable after Linux reboot, and that Queen now has a rebootable Windows unlock configuration. These are later operational reports, distinct from the earlier captured benchmarks in the table. Queen's later dated automatic-start, PCI readback and CUDA sequence is now recorded below. Harry's automatic-recovery claim remains owner-reported pending its separate dated evidence. The earlier measured Windows live stop/reactivation sequence is already documented. We may be among the first to combine these capabilities across these specific configurations; global precedence remains unverified.

## Verified Windows reboot recovery — 27 November 2026

**SUCCESS: Queen automatically restored PCIe Gen2 ×4 after a real Windows restart and user sign-in.** This is measured automatic recovery on this configuration, not physical retention of volatile GPU settings.

The recorded boot was 05:39:24 PST (13:39:24 UTC). The scheduled recovery completed at 05:40:29 PST; a separate live read at 05:40:55 PST confirmed fresh status, both endpoint and root port at Gen2 ×4, and training=false. No manual post-reboot activation was needed in this acceptance run.

| Post-reboot check | Result |
|---|---|
| Endpoint and root port | Gen2 ×4 at both ends; training=false |
| Pinned CUDA H2D, five trials | 1.548, 1.551, 1.542, 1.548, 1.542 GB/s |
| Pinned CUDA D2H, five trials | 1.672, 1.673, 1.673, 1.669, 1.673 GB/s |
| Transfer integrity | Pageable and pinned PASS |
| CUDA arithmetic | 32 values, zero errors |
| Display drivers | NVIDIA 582.78 unchanged on both adapters |
| Owner acceptance | Owner confirmed everything working after restart |

The existing Windows logon task waits 30 seconds, checks the recovery wrapper's hash, starts the exact existing driver services when stopped, invokes the original community launcher once, verifies fresh PCI status, runs CUDA transfer and arithmetic checks, and verifies PCI state again. It refuses recovery during an active game and logs failures instead of repeatedly launching. This describes the validated sequence; it is not a portable installer or a reason to apply Queen's configuration to other hardware. Credit for the upstream P102 method remains with [KODAMA Technology](https://github.com/KODAMA-TECHNOLOGY/P102-PCIE2.0ULOCKER).

**Scope:** one measured Windows restart/sign-in recovery on Queen. Cold power-cycle and repeated-cycle endurance remain to be tested. The short CUDA check is not sustained stability qualification. Post-reboot usability is owner-confirmed; no new controlled FPS, AI throughput or independent graphics capture is claimed. The earlier live stop/reactivation measurements remain valid as a separate experiment.

## Important interpretation

**P104:** Proven *manual after-reboot reactivation*, not a permanently fused or auto-started link upgrade.

**CMP 70HX:** Proven independent successful unlock procedures on two different Linux boots, and later confirmed hardware selector state plus functional tensor compute after the driver loaded. That demonstrates working target state, but does not measure the benefit against a *locked* 70HX, nor prove automatic power-cycle restoration.

The PCIe and tensor unlocks are not the same mechanism. Do not use P104 Gen2 scripts on CMP70HX; do not infer CMP70HX Gen2 from tensor selector changes.

The underlying methods were developed by [mai1346/p104-gen2](https://github.com/mai1346/p104-gen2) and [Zagitta/gpu-unlock](https://github.com/Zagitta/gpu-unlock); our reports are independent reproductions and measurements on our own cards.

*Research series updated: 27 November 2026.*
