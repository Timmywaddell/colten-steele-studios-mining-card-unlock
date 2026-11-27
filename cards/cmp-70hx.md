# Research note 02 — CMP 70HX selector readback and functional CUDA

**Status: working tensor unlock state confirmed after NVIDIA/CUDA initialization, including successful execution of the upstream procedure on two separate Linux USB boots. A factory-locked-to-unlocked speedup has NOT been quantified.**

## Hardware

- Palit NVIDIA CMP 70HX 8 GB (GA104), PCI 10DE:248A
- Intel i7-6700 / Gigabyte Z270X Ultra Gaming / 16 GB system RAM
- Experimental USB Ubuntu 24.04.5, kernel 7.0.0-31-generic
- NVIDIA proprietary 580.178.04; both CMP 70HX and GTX1660 Super recognized

## Recorded build expenditure

Harry's second-hand Core i7-6700, Gigabyte Z270X Ultra Gaming, 16 GB DDR4 and Cooler Master Hyper TX3 EVO cooler bundle cost ฿3,288 delivered. The owner confirms that the CMP 70HX cost ฿1,400 delivered. **Recorded combined expenditure: ฿4,688.** The GTX 1660 Super and Thermaltake 1650 W PSU were previously owned; this subtotal does not represent the replacement cost of a complete system. Other costs remain unverified.

## What succeeded

The upstream [Zagitta gpu-unlock v2.0.0](https://github.com/Zagitta/gpu-unlock) procedure succeeded on **two separate experimental Linux USB boots**: first Lexar, then SanDisk. A later independent, read-only BAR observation on the SanDisk Linux session, **after the NVIDIA driver and CUDA initialized with GSP OFF**, confirmed the expected unlocked feature values:

- PLM = `0xFFFFFFFF`
- SS0 = `0x88888888`
- SS1 = `0x00000008`

**All three values matched the unlock's intended hardware state after driver/CUDA initialization**. This is machine-readable in the [selector evidence CSV](../data/cmp70hx-unlocked-selectors.csv); no write was performed for the readback. Bounded BF16/FP16 tensor computations passed numerical accuracy checks, and Qwen3 inference worked. This confirms a functional unlock-state and compute milestone. The two successes occurred on separate USB Linux boots; the specific distinction between this repeated procedure and **automatic post-reboot activation or retention across an unattended power cycle** is documented in the [boot and restart evidence table](../docs/reboot-status.md). Without a matched factory-locked benchmark, the throughput gain caused by the unlock cannot be quantified.

## Measured, not causally attributed to the unlock

| Workload | GSP ON | GSP OFF |
|---|---:|---:|
| BF16 GEMM 4096 | 37.518 TFLOPS | 35.045 TFLOPS |
| FP16 GEMM 4096 | 34.554 TFLOPS | 34.345 TFLOPS |
| Qwen3-1.7B single-stream decode | 36.54 tok/s | 36.37 tok/s |
| Qwen3-1.7B eight-stream *aggregate* decode | 300.84 tok/s | 295.25 tok/s |

The initial GSP-off comparison did not show a meaningful speed increase. These are post-unlock GSP-mode tests, **not a factory-locked versus unlocked comparison**. See [CSV](../data/cmp70hx-observed.csv).

A separate Qwen3-30B-A3B IQ3_XXS model at 4096 context generated a short reply at 31.8 tok/s. **It used both the CMP 70HX and GTX1660 Super**, so it is not a single-GPU result and cannot prove unlock speedup.

A 512 MiB GPU-local copy test reported 562.24 GB/s combined read+write, corresponding to about 281.12 GB/s payload-copy throughput. It is **not PCIe bandwidth**. The observed PCIe link remained Gen1 x4; Gen2 has not been demonstrated on the 70HX.

## What remains unknown

- No same-card matched original locked/unlocked comparison.
- No quantified speedup that can be ascribed to the unlock itself.
- No 70HX Gen2, extra VRAM, unlocked rasterization or universal 70HX compatibility proof.
- No established first-in-the-world precedence: public [Zagitta supported-ID discussions](https://github.com/Zagitta/gpu-unlock/issues/168) and [Icyoung CMP graphics unlock work](https://github.com/Icyoung/cmpunlocker) already exist.

This report does not expose proprietary GPU dumps, installation secrets, local private paths, host keys or individual device serial numbers. Prior work is clearly attributed.

**Experiment dates:** 19–20 November 2026. **Public research-series inclusion:** 21 November 2026.
