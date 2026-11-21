# Contributing reproducible mining GPU evidence

Reports should include:
1. Exact public GPU model and PCI ID (no personal serial numbers).
2. OS/kernel/driver/toolchain versions.
3. Conditions: initial link, fan/temperature/power baseline and workload description.
4. Repetitions; raw values; correctness check; separate H2D/D2H and memory-local tests.
5. A truly matched baseline whenever claiming a causal speed improvement.
6. Safe recovery notes and explicit untested boundaries.
7. Links to original authors and prior art.

Open-source attribution is required; world-first claims must not rest only on failing to find an earlier result.

Do not publish: IP addresses, host keys, credentials, private chat logs, personal device identifiers, copyrighted NVIDIA binary blobs or third-party model files.

This repository intentionally does not provide a universal VBIOS or PCIe flashing script.
