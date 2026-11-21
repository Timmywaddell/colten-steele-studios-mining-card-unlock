# Measurement, evidence classification and limitations

## Claims and labels

- **Verified:** a named observation with an actual record, timestamp, device identity and repeatable commands/conditions.
- **Reproduced:** a technique proposed by others that worked on our independent hardware with recorded checks.
- **Preliminary:** a useful observation lacking a decisive control, repeat, or isolated cause.
- **Awaiting test:** no performance claim.

We do **not** claim first invention when method prior art exists. We do **not** infer speedups from GPU theoretical specifications, software support tables, an unlock success log, or unrelated benchmark configurations.

## P104 test

On a P104-100, exact PCI Link Status changed from `0x1041` (Gen1 x4) to `0x1042` (Gen2 x4) and Link Capability2 was `0x00000006`. Same hardware and 8 MiB host-pinned CUDA transfer workload ran five repetitions for H2D and D2H; data roundtrip was verified. Three Gen2 measurements, including one after reboot and manual reactivation, agreed closely. The original on-disk NVIDIA module was kept unchanged.

The P104 owner used separate manual fan controls to maintain 60% GPU fan and full chassis intake; unattended retrain was not certified.

## CMP 70HX test

We report observed feature-selector readback after driver initialization, bounded numerical-correctness checks for BF16/FP16 arithmetic, and sampled GSP mode performance comparisons. We explicitly **lack a locked control measurement on the same device**, so we cannot claim the percentage gain caused by the original feature-selector unlock.

Qwen3-30B result used two graphics cards; 512 MiB VRAM copy is not PCIe. The CMP link remained Gen1 x4. These are distinct from P104 observations.

## Reproducibility and safety

These experiments manipulate specific Nvidia and PCIe internals; errors can cause display loss or system hangs. Do not run third-party modules/patches with mismatched device IDs, kernel and driver versions, or without a recovery plan. Only public summary data is shipped; device serials, LAN IPs, credentials, user/private paths, copyrighted GPU blobs and private Office files are excluded. Refer to credited original project documentation for code, but treat its own warnings seriously.

Original upstream resources:
- https://github.com/mai1346/p104-gen2
- https://github.com/skbskhud/p104-unlock-v3
- https://github.com/Zagitta/gpu-unlock
- https://github.com/Zagitta/gpu-unlock/issues/168
- https://github.com/Icyoung/cmpunlocker

*No peer-reviewed or world-first claim is made.*
