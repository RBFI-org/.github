<div align="center">
  <kbd>
    <img src="./rbfi_logo.png" width="150" alt="RBFI" />
  </kbd>
</div>


# RBFI org
### Raw Boot Firmware Interface — Open-Source Bare-Metal Firmware
</div>

---

## About RBFI

**RBFI (Raw Boot Firmware Interface)** is a lightweight, transparent, zero-bloat bare-metal firmware written in pure assembly. Designed as a direct, high-speed bridge from the CPU reset vector (`0xFFFFFFF0`) straight to 64-bit operating system kernels without the overhead of legacy BIOS or multi-megabyte UEFI stacks.

### Core Principles
* **Zero Bloat & Full Transparency:** Every instruction is hand-crafted and auditable — no opaque binary blobs, no heavy DXE abstractions
* **Direct 64-Bit Handoff:** Initializes Cache-As-RAM (CAR), DRAM controllers, PCIe buses, USB, and static **ACPI 2.0+** tables, handing off cleanly to the OS kernel in Long Mode
* **Hardware Freedom:** Built to support native bare-metal booting across Intel platforms (Sandy Bridge, Ivy Bridge, Haswell, Broadwell, Bay Trail)

---

## Repositories & Ecosystem

* **[RBFI](https://github.com/RBFI-org/RBFI)** — Core x86_64 bare-metal firmware source (`RBFI_x86.nas`), ACPI 2.0+ builder, and Boot ABI specification.

---

## RBFI Boot ABI (Quick Reference)
* **Kernel Load Address:** `0x00100000`
* **Magic Signature:** `"longmode"` (`8 bytes` at `0x00100000`)
* **64-Bit Entry Pointer:** `[0x00100008]`
* **ACPI 2.0+ RSDP Pointer:** Passed in `RDI` (`0x0009E000`)
* **Memory Map:** 4GB Identity Paging (2MB pages) with uncached (`PCD + PWT`) MMIO regions (`0xD0000000+`)

