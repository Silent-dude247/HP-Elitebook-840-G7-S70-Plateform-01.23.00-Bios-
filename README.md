[Inquiry] HP EliteBook 840 G7 (S70) – Seeking Pre-Plundervolt BIOS for MSR 0xE2 & FIVR Unlock
The Objective
I am working to reclaim thermal headroom and performance on an HP EliteBook 840 G7 (Comet Lake). The end goal is to enable undervolting (FIVR control) and unlock MSR 0xE2 (CFG Lock) for native power management. However, I’ve hit the notorious HP "Security Wall."

Hardware/Software Environment
Model: HP EliteBook 840 G7

Platform ID: S70 / S73

board ID: 8723

CPU: Intel Core i5-10310U (10th Gen)

Current BIOS: v01.23.00 (2025/2026 release)

Primary OS: Arch (Linux) / Windows 11 Dual-Boot

The Current Block (Technical Analysis)
I have attempted to modify the UEFI variables via EFI Shell/Scripting, but the system is hardware-locked.

CFG Lock Target: IntelTechnologiesOptions @ Offset 0x0F.

Failure: (modGRUBShell:) setup_var_cv returns Error: 0x000000000000f. (RU.efi:) Attempts to write to 0x0F result in a Write Protect / Access Denied (0x8) error.

The Problem: It appears the Protected Range Registers (PRR) are initialized early in the boot sequence (PEI/DXE phase), rendering the variable store read-only for any software-level tools.

Missing Offsets for v01.23.00
While the CFG Lock offset is known, I have not yet successfully mapped the Overclocking/FIVR variables for this specific firmware version. I am looking for the IFR-confirmed Variable Store (likely CpuSetup) and Offsets for:

Overclocking Lock (To permit voltage modification).

FIVR Control / XTU Interface (To expose voltage sliders).

BIOS Lock (To potentially allow FPT writing).

If anyone has a PE32/IFR dump for S70 v01.23.00, your confirmation on these offsets would be invaluable to prevent a blind-write brick.

The "Golden Version" Request and My Last Option
I am seeking a specific SoftPaq (older BIOS)—ideally from late 2020 or early 2021—that was released prior to the aggressive SVN (Security Version Number) jumps and Plundervolt mitigations.

Does anyone have the SoftPaq ID or a verified .bin for a version that:

Accepts setup_var / RU.efi writes without PRR interference.

Does not have a locked SVN that triggers a signature failure during rollback.

Is verified to bypass the "excluded" status even with "Unrestricted Rollback" enabled in the BIOS menu.

I have a 16MB SPI dump of my current region for recovery purposes, but I am looking for the last version that treats the owner as the administrator.

Has anyone successfully rolled back an S70-platform EliteBook to a version where undervolting is functional? Any leads on specific SoftPaq numbers for older would be greatly appreciated.
