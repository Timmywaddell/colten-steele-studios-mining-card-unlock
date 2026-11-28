# Queen: P102-100 Windows gaming, Godot and 27B local AI on 8 GB RAM

**Colten Steele Studios — research release, 28 November 2026**

Old hardware. New possibilities. Your own AI game studio.

A second-hand mining GPU can become a useful Windows workstation for 1080p gaming, original game development and modern local AI. Queen combines a P102-100 10 GB with a GT 1030 2 GB display and speech GPU. **We might be among the first to document this exact combination**; global priority is unverified. The underlying unlock and AI technologies are credited below.

## What we achieved

- Full Ternary Bonsai 2.5 27B PTQ1_0, configured for 32,768 tokens, on the P102.
- Persistent CUDA Whisper on the GT 1030 while the main model remains loaded. Both local servers were observed running simultaneously.
- One-time idle working-set reclamation without unloading GPU weights. Approximately 5.5 GiB of available system RAM in a later co-resident snapshot.
- 3,049 physical PCIe endpoint/root Gen2 x4 observations across 2 h 36 min during the current AI session. Earlier runs experienced real Gen1 downshifts; sampling cannot exclude shorter events between observations.
- A native assistant with voice mode, streamed text and sentence speech, memory, research evidence and job-draft workflows. Earlier V25 voice conversation was owner-tested. V33 natural interruption is implemented but not fully live-qualified.
- One recovery/workload controller, with GTA V, Racing Kit Builder and Steele City desktop shortcuts routed through it. A prior Racing Kit Builder AI-to-game-to-AI switch passed. The newest full-system reboot and GTA/City switching tests remain open.

## Version-pinned system

| Component | Configuration |
|---|---|
| CPU | Intel Core i3-9100F, 4 cores / 4 threads |
| Motherboard | ASRock B365 Pro4, AMI P1.00 |
| System RAM | 8 GB DDR4, approximately 7.93 GiB usable |
| Main GPU | P102-100, 10,240 MiB, GP102, SM 6.1 |
| Display / speech GPU | GT 1030, 2,048 MiB, SM 6.1 |
| OS | Windows 10 Pro build 19045 |
| GPU driver | NVIDIA 582.78, both WDDM |
| Storage | Toshiba 512 GB NVMe, SATA HDD, 16 GiB NVMe page file |
| Gaming | Game-local DXVK 2.6.2, GT 1030 display output |
| LLM | PrismML fork prism-b12178, CUDA 12.4 |
| Model | Ternary-Bonsai-2.5-27B-PTQ1_0.gguf, 5,993,834,848 bytes |
| Speech | whisper.cpp v1.7.6 CUDA 12.4, multilingual base model |
| Cooling | 70% fan targets; AI thermal stop 70 C; factory P102 250 W limit, no overclock |
| Recorded cash cost | $42 P102; $198 project expenditure including reused/free parts (not full retail replacement value) |

All prices are approximate US-dollar equivalents of historical recorded spending, converted using the 27 November 2026 closing exchange rate. Rounded amounts may not sum exactly; reused/free components are not assigned a retail value.

## Evidence and results

Download the [complete sanitized physical-link trace](../data/queen-physical-pcie-20261128.csv) and [measurement summary](../data/queen-ai-20261128.csv).

| Result | Evidence classification |
|---|---|
| Windows GTA V at 1920 x 1080 | Owner-observed 70–75 FPS, very-high/ultra-oriented graphics mix; not all settings maxed or controlled average |
| Original Godot city | Owner-observed 50–60 FPS with drops at speed, FSR 0.85; Vulkan and traffic functionality verified |
| Windows reboot recovery (27 Nov) | 1.542–1.551 GB/s H2D and 1.669–1.673 GB/s D2H; transfer integrity PASS; 32 arithmetic values, zero errors |
| Bonsai plain decoding, 32K configured | 18.94 tokens/s; 162 generated tokens in 8.50063 s, 76 prompt tokens at 37.13 t/s, total 10.54740 s; truncated=0 |
| Longer response | 18.37 tokens/s, 799 generated tokens in 43.43358 s; truncated=0 |
| Idle working-set trim | 5,451,182,080 bytes before, 360,448 immediately after; same running process |
| Later co-resident snapshot | 5,787,112 KiB available RAM (~5.52 GiB); P102 8,245 MiB VRAM; GT 1030 712 MiB VRAM |
| Physical PCIe trace, 28 Nov UTC | 10:32:38.5293010 to 13:09:00.8379313; 3,049/3,049 Gen2 x4 sampled; peak sampled P102 temperature 60 C |
| Official MTP candidate | 6,232,818,944 bytes; SHA-256 e0fc5f3d47b9c926d52677d303b19df356a2376614b3e1cb9973865fc04ca431 matched expected. Not activated or speed-tested. |

These are studio records, not independent peer review. Windows mapped pages can be reclaimed and later faulted back: trimming the working set is not freeing all committed memory or reducing model parameters. The 32K setting is not a demonstrated 32K-filled recall benchmark. Separate GPU workloads do not pool VRAM. Blender is a planned quantitative production benchmark, not a measured Queen result.

## Replication recipe

Use an isolated test installation, legitimate games and upstream software, preserve a known-good backup and rollback, and leave system security protections intact. This is a version-pinned verification recipe, not a universal installer; the exact adapted Windows driver and game-specific library-loading fix are not redistributed.

1. Record hardware, BIOS/VBIOS, OS, driver and PCIe endpoint/root status. Connect the monitor to the display GPU, verify both adapters and cooling, and capture baseline transfer measurements.
2. Review the original [KODAMA P102 Gen2 project](https://github.com/KODAMA-TECHNOLOGY/P102-PCIE2.0ULOCKER) for compatible configurations. Follow the existing [Windows gaming guide](../cards/p102-100.md#reproduce-the-windows-dual-gpu-approach) and [reboot evidence](reboot-status.md). Do not mix P104 or CMP methods. Verify both PCI endpoints, transfer integrity and arithmetic after initialization. NVIDIA management link reporting may disagree with physical status. Do not retrain during active workloads.
3. Obtain the official [Bonsai model](https://huggingface.co/prism-ml/Ternary-Bonsai-2.5-27B-GGUF) and compatible [PrismML runtime](https://github.com/PrismML-Eng/Bonsai-demo). Confirm Pascal SM 6.1 support, PTQ1_0 format, and official SHA-256. The Queen model file hash is 929560EC9D37CF3CADD4B00CC87B51C570082A628DD830B4692DC0B2ED18DBBE. Confirm the runtime flags with its help and GPU order with its device listing. Use locally chosen paths and a newly generated private key file, never expose the server or copy someone else's secrets.

Measured Queen LLM command (PowerShell; define your local paths first):

```powershell
& $LlamaServer -m $Model -c 32768 -ctk f16 -ctv f16 -dev CUDA0 -ngl 99 -fit off -sm none -fa off -t 3 -tb 3 -b 64 -ub 32 --load-mode mmap --lazy-mode on --no-warmup -np 1 --host 127.0.0.1 --port 19931 --no-webui --cache-ram 0 --reasoning-format deepseek --reasoning-effort xhigh --api-key-file $PrivateKeyFile
```

4. Check readiness and actual inference, then record finish reason, timing, RAM, VRAM, page-file use and temperatures. The same model at 16,384 context is a validated fallback. Keep one slot. One idle-only working-set trim can reclaim mapped resident pages; use [Microsoft's EmptyWorkingSet documentation](https://learn.microsoft.com/en-us/windows/win32/api/psapi/nf-psapi-emptyworkingset). This is optional, not a universal memory requirement. Measure page faults and subsequent latency; never repeatedly trim during inference.
5. Obtain [whisper.cpp v1.7.6](https://github.com/ggml-org/whisper.cpp/releases/tag/v1.7.6) compatible CUDA 12.4 build and multilingual base model from upstream. Confirm device ordering first; index 1 is specific to Queen. In a separate PowerShell process:

```powershell
$env:CUDA_DEVICE_ORDER = 'PCI_BUS_ID'
$env:CUDA_VISIBLE_DEVICES = '1'
& $WhisperServer -m $WhisperBase --host 127.0.0.1 --port 8178 -t 2 -l en -nt -nc -bo 5 -bs 5
```

The multilingual model supports other languages with appropriate request settings. Isolate or clear device-selection environment variables before starting other GPU programs. Keep CPU fallback. Compare identical audio samples and warm latency; cold GPU startup did not demonstrate a speed advantage on Queen.
6. Stop the verified idle AI workload before starting games, check VRAM release, log settings, renderer, FPS and frame times, exit the game normally and restore the assistant. Never force-close a game. Keep original launchers available. The current custom controller and full native assistant are not yet distributed as a portable package.
7. Restart with rollback available. Verify cooling, physical endpoint/root, CUDA integrity, a single LLM and speech server and restored conversation. One earlier automatic Windows unlock restart passed; the complete latest integrated stack has not yet passed a fresh reboot.

## Community challenge and next tests

Can anyone reproduce the same combination, or show an earlier documented example? Please share exact hardware and driver, baseline and after measurements, complete prompt/decode timings, physical PCIe traces, voice latency, controlled 1080p FPS and frame times, restart outcome, and failures as well as successes. Remove private paths, IPs, device serials, credentials and personal data. [Open a replication report or correction](https://github.com/Timmywaddell/colten-steele-studios-mining-card-unlock/issues).

Remaining: independent replication; controlled matched Gen1/Gen2 gaming and Blender benchmarks; 32K-filled recall; warm speech and human barge-in; measured MTP; latest whole-stack reboot/game recovery; actual authorized account automation. No automatic external applications or email sending is claimed.

## Attribution

[KODAMA Technology](https://github.com/KODAMA-TECHNOLOGY/P102-PCIE2.0ULOCKER) for P102 Gen2, [DXVK](https://github.com/doitsujin/dxvk) for graphics translation, [PrismML](https://github.com/PrismML-Eng/Bonsai-demo) for Bonsai, [llama.cpp](https://github.com/ggml-org/llama.cpp) and [whisper.cpp](https://github.com/ggml-org/whisper.cpp) contributors. Our contribution is the card-specific integration, measurements, memory and workload orchestration and original game-development research. No proprietary binaries or private logs are redistributed.

[Project home](../README.md) · [Windows gaming and Godot report](../cards/p102-100.md) · [Studio website](https://headless-fzilvlsgnve-timmywaddell1-140d.wix-site-host.com)
