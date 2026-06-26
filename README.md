# WinPE Drivers

Minimal, ready‑to‑inject driver packages for Windows Preinstallation Environment (WinPE) and Windows Recovery Environment (WinRE).

## Purpose
These driver packs are used by the WinRE management script to add critical hardware support – such as Intel VMD storage – to the recovery image without bloating it. Only the essential files are included (`.inf`, `.sys`, `.cat`), keeping the injected image as small as possible.

## Structure
WinPEDrivers/
├── IntelVMD/
│ ├── 11thGen.zip (for 11th–13th Gen Intel Core platforms)
│ └── 14thGen.zip (for 14th Gen and newer Intel Core platforms)
└── ... (future additions e.g., touchpad, network)

Each `.zip` archive contains the bare driver files at its root – ready for `DISM /Add-Driver`.

## Usage
1. Download the appropriate `.zip` from this repository.
2. Mount the target WinPE/WinRE image with DISM.
3. Inject the driver:  
   `DISM /Image:<mount_path> /Add-Driver /Driver:<path_to_extracted_zip>`
4. Commit and export the image.

This process is automated by the WinRE deployment script; manual injection is also fully supported.

## Source & Updates
- **Intel VMD 11th–13th Gen** extracted from Intel RST VMD F6 driver package, version 19.5.x.  
- **Intel VMD 14th Gen+** extracted from Intel RST VMD F6 driver package, version 20.x.  

These packs are updated when Intel releases a new VMD driver that requires matching hardware IDs or fixes. Check the repository’s commit history for version changes.

## Licensing
These driver files are redistributed under their original equipment manufacturer or Intel’s license terms.  
All rights remain with the respective copyright holders. Redistribution is intended solely for recovery and preinstallation purposes on properly licensed Windows systems.
