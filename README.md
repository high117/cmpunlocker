# cmpunlocker

Unlock tool for the NVIDIA CMP 170HX (GA100) mining card. Restores full SM compute throughput and unlocked HBM2e memory geometry that are restricted in firmware/OTP configuration.

---
## Provenance & Attribution

**This is a personal fork of [cmpunlocker](https://github.com/amoghmunikote/cmpunlocker) by [Amogh Munikote](https://github.com/amoghmunikote), maintained for personal use. No upstream code is claimed as the fork owner's work.**

- Original project: [amoghmunikote/cmpunlocker](https://github.com/amoghmunikote/cmpunlocker) — original author Amogh Munikote. All upstream code remains the work of its respective authors.
- Contributor work is included under its original authorship; see [CREDITS.md](CREDITS.md) (MeatKO — DKMS removal; asm64-hooligan — full BAR1 64GB; armand0e — late PMA extension, keep the high reserved region reserved for WPR2, upstream PR #32).
- The patches in `driver/patches/` are applied to NVIDIA `open-gpu-kernel-modules` sources, which remain under their own license/copyright.
- The project `LICENSE` (GNU GPL v2) applies and is unchanged.
- **AI-assisted work:** modifications made in this fork (including this notice) were produced with AI/LLM tooling assistance.


**[Join our Discord community](https://discord.gg/CdHSakKSFv)** for support and discussions.

---
## Proof of Concept

Below are memory and performance results after applying the unlock:

### Memory Unlock Results

<img alt="memory unlock" src="https://github.com/user-attachments/assets/ae062bd8-e3a7-4e73-b9a4-fbcde53f3c7b" width="100%" style="max-width: 900px;" />

### Performance Benchmarks ([OpenCL-Benchmark](https://github.com/ProjectPhysX/OpenCL-Benchmark))

<img alt="performance benchmarks" src="https://github.com/user-attachments/assets/2501506d-420f-4014-9574-b1bd0290eb60" width="100%" style="max-width: 900px;" />

---

## Requirements

- Linux (x86-64)
- Root access
- NVIDIA CMP 170HX
- **nvidia-open 610.43.0x already installed** (libs + firmware)
- Kernel headers matching the running kernel (`linux-headers-$(uname -r)` / `kernel-devel`)
- Secure Boot disabled (patched modules are unsigned)
- Network access on first install (downloads matching stock `open-gpu-kernel-modules` sources)
- Python 3 (used at build time to select 8GB/10GB geometry)

---

## Install

To install cmpunlocker, run the following command:

```bash
sudo ./install.sh
```

To force a certain memory profile, use the `--profile` option:

```bash
sudo ./install.sh --profile=8gb    # 8GB card → 64GB unlock
sudo ./install.sh --profile=10gb   # 10GB card → 40GB unlock
```

Then perform a cold reboot (full power off, then boot).

## What Gets Unlocked

| Feature | Status |
|---|---|
| Full SM compute throughput (SS0/SS1) | Working ✓ |
| Memory geometry (64GB on 8GB cards, 40GB on 10GB cards) | Working ✓ |
| PCIe Gen 2 speeds | Working ✓ |
| Full BAR1 Size (64GB) | Working ✓ |
| JTAG (Host2Jtag register access) | Working ✓ |
| Persistence across reboot (patched modules) | Working ✓ |

---

## Uninstall

To uninstall cmpunlocker, run the following command:

```bash
sudo ./uninstall.sh --yes
```

Then perform a cold reboot (full power off, then boot).

## Support & Community

Having issues? Need help? Join our [Discord community](https://discord.gg/CdHSakKSFv) to discuss with other users and get support.
