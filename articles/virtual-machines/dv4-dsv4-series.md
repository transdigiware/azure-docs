---
title: Dv4 and Dsv4-series - Azure Virtual Machines
description: Specifications for the Dv4 and Dsv4-series VMs.
author: brbell
ms.author: brbell
ms.reviewer: cynthn
ms.custom: mimckitt
ms.service: virtual-machines
ms.subservice: vm-sizes-general
ms.topic: conceptual
ms.date: 06/08/2020
---

# Dv4 and Dsv4-series

The Dv4 and Dsv4-series runs on the Intel&reg; Xeon&reg; Platinum 8272CL (Cascade Lake) processors in a hyper-threaded configuration, providing a better value proposition for most general-purpose workloads. It features an all core Turbo clock speed of 3.4 GHz. 

> [!NOTE]
> For frequently asked questions, see [Azure VM sizes with no local temp disk](azure-vms-no-temp-disk.yml).

## Dv4-series

Dv4-series sizes run on the Intel&reg; Xeon&reg; Platinum 8272CL (Cascade Lake). The Dv4-series sizes offer a combination of vCPU, memory and remote storage options for most production workloads. Dv4-series VMs feature [Intel&reg; Hyper-Threading Technology](https://www.intel.com/content/www/us/en/architecture-and-technology/hyper-threading/hyper-threading-technology.html).

Remote Data disk storage is billed separately from virtual machines. To use premium storage disks, use the Dsv4 sizes. The pricing and billing meters for Dsv4 sizes are the same as Dv4-series.

> [!NOTE]
> After a restart, a file named *Data_loss_warning.txt* might be appear beside drive C (the first data disk attached from the Azure portal). In this scenario, despite the file name, no data loss has occurred on the disk. In general, the *Data_loss_warning.txt* file usually is copied on the temporary drive. If you're using a VM that doesn't have a temp drive, WindowsAzureGuestAgent incorrectly copies the file to the first drive letter. In v4 VMs, the first drive letter is a data disk.
>
> A resolution for this issue was applied in the latest version (version 2.7.41491.999) of the VM agent.

[ACU](acu.md): 195-210<br>
[Premium Storage](premium-storage-performance.md): Not Supported<br>
[Premium Storage caching](premium-storage-performance.md): Not Supported<br>
[Live Migration](maintenance-and-updates.md): Supported<br>
[Memory Preserving Updates](maintenance-and-updates.md): Supported<br>
[VM Generation Support](generation-2.md): Generation 1 and 2<br>
[Accelerated Networking](../virtual-network/create-vm-accelerated-networking-cli.md): Supported (*Requires a minimum of 4 vCPU*)<br>
[Ephemeral OS Disks](ephemeral-os-disks.md): Not Supported <br>
<br>

| Size | vCPU | Memory: GiB | Temp storage (SSD) GiB | Max data disks | Max NICs|Expected Network bandwidth (Mbps) |
|---|---|---|---|---|---|---|
| Standard_D2_v4 | 2 | 8 | Remote Storage Only | 4 | 2|1000 |
| Standard_D4_v4 | 4 | 16  | Remote Storage Only | 8 | 2|2000 |
| Standard_D8_v4 | 8 | 32 | Remote Storage Only | 16 | 4|4000 |
| Standard_D16_v4 | 16 | 64 | Remote Storage Only | 32 | 8|8000 |
| Standard_D32_v4 | 32 | 128 | Remote Storage Only | 32 | 8|16000 |
| Standard_D48_v4 | 48 | 192 | Remote Storage Only | 32 | 8|24000 |
| Standard_D64_v4 | 64 | 256 | Remote Storage Only | 32 | 8|30000 |

## Dsv4-series

Dsv4-series sizes run on the Intel&reg; Xeon&reg; Platinum 8272CL (Cascade Lake). The Dv4-series sizes offer a combination of vCPU, memory and remote storage options for most production workloads. Dsv4-series VMs feature [Intel&reg; Hyper-Threading Technology](https://www.intel.com/content/www/us/en/architecture-and-technology/hyper-threading/hyper-threading-technology.html). Remote Data disk storage is billed separately from virtual machines.

[ACU](acu.md): 195-210<br>
[Premium Storage](premium-storage-performance.md): Supported<br>
[Premium Storage caching](premium-storage-performance.md): Supported<br>
[Live Migration](maintenance-and-updates.md): Supported<br>
[Memory Preserving Updates](maintenance-and-updates.md): Supported<br>
[VM Generation Support](generation-2.md): Generation 1 and 2<br>
[Accelerated Networking](../virtual-network/create-vm-accelerated-networking-cli.md): Supported (*Requires a minimum of 4 vCPU*)<br>
[Ephemeral OS Disks](ephemeral-os-disks.md): Not Supported <br>
<br>

| Size | vCPU | Memory: GiB | Temp storage (SSD) GiB | Max data disks | Max uncached disk throughput: IOPS/MBps | Max burst uncached disk throughput: IOPS/MBps<sup>1</sup> | Max NICs|Expected Network bandwidth (Mbps) |
|---|---|---|---|---|---|---|---|---|
| Standard_D2s_v4 | 2 | 8  | Remote Storage Only | 4 | 3200/48 | 4000/200 |2|1000 |
| Standard_D4s_v4 | 4 | 16 | Remote Storage Only | 8 | 6400/96 | 8000/200 |2|2000 |
| Standard_D8s_v4 | 8 | 32 | Remote Storage Only | 16 | 12800/192 | 16000/400 |4|4000 |
| Standard_D16s_v4 | 16 | 64  | Remote Storage Only | 32 | 25600/384 | 32000/800 |8|8000 |
| Standard_D32s_v4 | 32 | 128 | Remote Storage Only | 32 | 51200/768 | 64000/1600 |8|16000 |
| Standard_D48s_v4 | 48 | 192 | Remote Storage Only | 32 | 76800/1152 | 80000/2000 |8|24000 |
| Standard_D64s_v4 | 64 | 256 | Remote Storage Only | 32 | 80000/1200 | 80000/2000 |8|30000 |

<sup>1</sup>  Dsv4-series VMs can [burst](./disk-bursting.md) their disk performance and get up to their bursting max for up to 30 minutes at a time.