# Next mining-card test queue

This is a list of intended experiments, **not published achievements**.

## P102-100 — 10 GB variant (owner reported)
Confirm PCI ID, exact VRAM with nvidia-smi, cooling and Linux graphics support. Then measure on the same fixed workloads: CUDA correctness, real PCIe link, pinned H2D/D2H, GTA V actual FPS/frametimes, Blender read-only test, and AI inference. The specific P104 link-retrain procedure is NOT validated for P102 and must not be copied directly.

## P104-100 follow-up
Add actual in-engine FPS and 1% lows with a frame-time tool, and a stable, reproducible, temperature-guarded AI inference test. Separate those results from the existing Gen2 host transfer finding. The initial GTA V observation was near 60 *window updates per second* on 59.79 Hz display; this is not direct engine FPS and is excluded from the claim.

## CMP 70HX
Obtain a defensible same-hardware locked/unlocked A/B only if doing so can preserve the working Linux/Windows environment with owner authorization and recovery. Further measure sustained CUDA GEMM, repeatable Qwen3 prefill/decode, power/clock/thermal conditions, and independent review of prior art. Never call the unpaired 37.5 TFLOPS figure a 2x gain.

## Future devices
Specific 30HX, P106 and other mining GPUs must get their own hardware IDs and tests. No extrapolated claims, no unverified x16/Gen3/VRAM/shader unlock promises.
