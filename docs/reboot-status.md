# Boot, reboot recovery and reversible operation — P104, CMP 70HX and P102

The phrase **"reboot-able unlock"** can describe two different achievements:
1. The same environment can boot safely, then a user can deliberately reapply the unlock and verify operation.
2. An unlock activates and validates **automatically** every time the system boots without human intervention.

Neither case requires that the GPU retains modified volatile registers physically through a power cycle. The data below keeps these meanings distinct.

| GPU | Evidence of unlock after a fresh boot | Post-driver proof | Automatic start proven? |
|---|---|---|---|
| **NVIDIA P104-100 8 GB** | **YES.** A real WD Linux reboot returned the GPU to Gen1 ×4, then a guarded manual one-shot activation restored physical Gen2 ×4. A new 8 MiB ×5 CUDA copy benchmark passed at H2D 1.544 / D2H 1.669 GB/s. | Raw link status 0x1042 confirmed again after CUDA initialization; temporary kernel hook removed and original driver file on disk retained. | **NO.** The systemd unit is intentionally manual/static. |
| **NVIDIA CMP 70HX 8 GB** | **YES, for independent boot reproduction.** The upstream Zagitta kernel procedure reported successful unlock on an original Lexar Linux boot and again on a distinct SanDisk Linux boot. | On SanDisk with NVIDIA proprietary driver 580.178.04 and CUDA initialized and GSP turned off, **PLM=FFFFFFFF, SS0=88888888, SS1=00000008** matched the intended unlocked state in independent read-only checks. Real BF16/FP16 tensor calculations and Qwen3 inference passed. | **NOT TESTED.** Automatic reactivation after every restart, and same-media repeat after a controlled fresh power cycle, were not separately accepted as test gates. |

| **NVIDIA P102-100 10 GB** | **Windows live stop/reactivation verified.** Fresh-reboot end-to-end validation remains a separate gate. | Endpoint and root read Gen2 x4 before stopping; median pinned H2D/D2H fell to 0.797/0.841 GB/s after stopping and recovered to 1.546/1.680 GB/s after reactivation, without reboot. Integrity passed; post-stop link register was not separately read. GTA V and Godot rendered on the P102 through the GT 1030. | **NOT YET VERIFIED.** Logon startup registration was recorded; automatic successful recovery through a fresh boot with measured transfers and rendering still requires confirmation. |

## Project-wide recovery standard

Our engineering objective is not a one-time unlock: it is a usable, reversible configuration that can be restored safely after restarting. The owner reports working Windows and Linux installations on both Dino and Harry. That is distinct from proving every unlock in both operating systems. For each card and OS, record a clean boot, driver initialization, baseline, activation, hardware readback where available, integrity-checked workload, and a subsequent restart/recovery. Where live stop and reactivation are supported, document them separately. Do not assume a safe live transition during an active GPU workload. Publish exact versions, rollback guidance and evidence of any required manual step. Use “may be a first” only as a qualified hypothesis, never an established global precedence claim.

## Later owner-confirmed recovery milestones — 27 November 2026

The owner confirms that Harry's CMP 70HX tensor unlock automatically returns on Linux reboot and remains usable, that Dino's P104 Gen2 unlock is recoverable after Linux reboot, and that Queen now has a rebootable Windows unlock configuration. These are later operational reports, distinct from the earlier captured benchmarks in the table. A dated automatic-start log and post-reboot workload/readback sequence for Harry and Queen should accompany a formal independent replication. The earlier measured Windows live stop/reactivation sequence is already documented. We may be among the first to combine these capabilities across these specific configurations; global precedence remains unverified.

## Important interpretation

**P104:** Proven *manual after-reboot reactivation*, not a permanently fused or auto-started link upgrade.

**CMP 70HX:** Proven independent successful unlock procedures on two different Linux boots, and later confirmed hardware selector state plus functional tensor compute after the driver loaded. That demonstrates working target state, but does not measure the benefit against a *locked* 70HX, nor prove automatic power-cycle restoration.

The PCIe and tensor unlocks are not the same mechanism. Do not use P104 Gen2 scripts on CMP70HX; do not infer CMP70HX Gen2 from tensor selector changes.

The underlying methods were developed by [mai1346/p104-gen2](https://github.com/mai1346/p104-gen2) and [Zagitta/gpu-unlock](https://github.com/Zagitta/gpu-unlock); our reports are independent reproductions and measurements on our own cards.

*Research series updated: 27 November 2026.*
