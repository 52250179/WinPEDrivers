# WinPE Drivers

Minimal, ready‑to‑inject driver packages for Windows Preinstallation Environment (WinPE) and Windows Recovery Environment (WinRE).

## Purpose
These driver packs provide critical hardware support – such as Intel VMD storage – without bloating the recovery image. Only the essential files are included (`.inf`, `.sys`, `.cat`), keeping the injected image as small as possible.

## Structure
WinPEDrivers/
├── Storage/
│ └── Intel/
│ └── VMD/
│ ├── v19.7z (v19.5.x base – Intel 11th, 12th, and 13th Gen)
│ └── v20.7z (v20.x base – Intel 14th Gen and newer)
└── ... (future: Network, Chipset, Touchpad, etc.)

Each `.zip` archive contains the bare driver files at its root – ready for `DISM /Add-Driver`.

## Usage
1. Identify the required driver from the manifest.
2. Download the `.zip` from the corresponding path in this repository.
3. Mount the target WinPE/WinRE image with DISM.
4. Inject the driver:  
   `DISM /Image:<mount_path> /Add-Driver /Driver:<path_to_extracted_zip>`
5. Commit and export the image.

This process is automated by the WinRE deployment script; manual injection is also fully supported.

## Source & Versions
- **Intel VMD v19** (`Storage/Intel/VMD/v19.zip`)  
  Based on Intel RST VMD F6 driver package, **version 19.5.x**.  
  Covers Intel 11th Gen (Tiger Lake), 12th Gen (Alder Lake), and 13th Gen (Raptor Lake).
- **Intel VMD v20** (`Storage/Intel/VMD/v20.zip`)  
  Based on Intel RST VMD F6 driver package, **version 20.x**.  
  Covers Intel 14th Gen (Meteor Lake), 15th Gen (Arrow Lake), and is expected to support future iterations.

These packs are updated when Intel releases a new VMD driver that changes the required hardware IDs or introduces a breaking change. Check the repository’s commit history for version updates.

## Licensing
These driver files are redistributed under their original equipment manufacturer or Intel’s license terms.  
All rights remain with the respective copyright holders. Redistribution is intended solely for recovery and preinstallation purposes on properly licensed Windows systems.
