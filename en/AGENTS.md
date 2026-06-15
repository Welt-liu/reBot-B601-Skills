# B601-RS Robotic Arm User Guide

> This document applies only to the **B601-RS robotic arm**.
> Except for commands that require explicit user permission, all steps are executed by the agent with your consent. In non-exceptional cases, do not ask the user to handle things manually in the terminal.
> Do not use motorbridge-cli commands not mentioned in this document, as they may start the motors and cause unexpected behavior.

## Quick Start

Please confirm which form of robotic arm you have:

| Form | Description | Starting Step |
|------|-------------|---------------|
| Kit (unassembled) | Requires user assembly | Start from Step 1 |
| Assembled | Pre-assembled and ready to use | Jump to Step 3 |

---

## Step 1: Environment Initialization

See [Environment Setup Reference](https://github.com/Welt-liu/reBot-B601-RS-Skills/blob/main/en/references/setup-environment.md) to complete the following:

- [ ] Python environment setup (Miniforge or existing Python)
- [ ] motorbridge installation
- [ ] Platform-specific configuration (Linux: configure can0, Windows: install PCAN-USB driver)

After completion, verify motorbridge-cli is available:

```bash
motorbridge-cli --help
```

> **Windows users**: Use Miniforge to create a conda environment — do not use system Python directly. No can0 configuration needed. See [Environment Setup Reference](https://github.com/Welt-liu/reBot-B601-RS-Skills/blob/main/en/references/setup-environment.md) for details.

---

## Step 2: Write Motor IDs

See [Write Motor ID Reference](https://github.com/Welt-liu/reBot-B601-RS-Skills/blob/main/en/references/write-motor-id.md)

This reference guides you through:

1. **Identify the USB-CAN adapter** (PCAN-USB; Linux: configure `can0` at bitrate `1000000`, Windows: driver auto-detects)
2. **Set motor IDs one by one** (7 motors total, ID range 1–7)
   - Connect only one motor at a time
   - Scan to confirm the current motor ID (default: 127, some batches pre-set to 1–7)
   - Modify to the user-specified target ID
   - > **Note**: robstride `id-set` may report `store_parameters failed` timeout error — the ID is actually written, verify by scanning
3. **Final verification** — Scan to confirm all motor IDs (1–7) are correctly written

---

## Step 3: Zero Calibration

See the [Zero Calibration Reference](references/write-motor-zero.md).

This reference guides you through:

1. **Start motorbridge-gateway** (bound to `127.0.0.1:9002`, using `can0`)
2. **Guide the user to open Motorbridge Studio** to complete zero calibration

---

## Reference Documents Status

| Reference | File | Status |
|-----------|------|--------|
| Environment Setup | `references/setup-environment.md` | Completed |
| Write Motor ID | `references/write-motor-id.md` | Completed |
| Zero Calibration | `references/write-motor-zero.md` | Completed |
