---
title: "Azure Vm tooManaged 磁碟 aaaMigrate |Microsoft 文件"
description: "移轉使用未受管理的磁碟儲存體帳戶 toouse 受管理磁碟中建立的 Azure 虛擬機器。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 29420f13c4ffd5b25726e0ef1aafe89347286a89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-vms-toomanaged-disks-in-azure"></a>將 Azure 中的 Azure Vm tooManaged 磁碟移轉

藉由移除 hello 需要 azure 受管理的磁碟可簡化的存放裝置管理 tooseparately 管理儲存體帳戶。  您也可以移轉現有的 Azure Vm tooManaged 磁碟 toobenefit 從更佳的可靠性的可用性設定組的 Vm。 它會確保 hello 磁碟的可用性設定組不同的 Vm 將會從每個其他 tooavoid 單點失敗充分的隔離性。 自動將不同的 Vm 磁碟置於可用性設定組中不同的存放裝置延展單位 （戳記） 這會限制 hello toohardware 和軟體的失敗原因造成單一的儲存體延展單位故障的影響力。
根據您的需求，您可選擇兩種類型的儲存體選項︰

- [進階受控磁碟](../../storage/common/storage-premium-storage.md)是固態硬碟 (SSD) 式儲存媒體，可針對執行大量 I/O 工作負載的虛擬機器，提供高效能、低延遲的磁碟支援。 您可以利用的 hello 速度與這些磁碟移轉 tooPremium 管理磁碟的效能。

- [標準管理磁碟](../../storage/common/storage-standard-storage.md)使用硬碟機 (HDD) 基礎儲存媒體，而且最適合用來開發/測試和其他不頻繁存取工作負載的敏感性較低的 tooperformance 變化性。

您可以移轉下列案例中的 tooManaged 磁碟：

| 移轉...                                            | 文件連結                                                                                                                                                                                                                                                                  |
|----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 在 可用性集 toomanaged 磁碟轉換獨立 Vm 和 Vm   | [將 Vm toouse 管理磁碟轉換](convert-unmanaged-to-managed-disks.md) |
| 在受管理的磁碟上的傳統 tooResource 管理員從單一 VM     | [移轉單一 VM](migrate-single-classic-to-resource-manager.md)  | 
| 從受管理的磁碟上的傳統 tooResource 管理員 vNet 中的所有 hello Vm     | [從傳統 tooResource Manager 移轉 IaaS 資源](migration-classic-resource-manager-ps.md)然後[將 VM 轉換從 unmanaged 的磁碟 toomanaged 磁碟](convert-unmanaged-to-managed-disks.md) | 






## <a name="plan-for-hello-conversion-toomanaged-disks"></a>規劃 hello 轉換 tooManaged 磁碟

本節可協助您 toomake hello 最佳決定 VM 和磁碟類型。


## <a name="location"></a>位置

挑選 Azure 受控磁碟可用的位置。 如果您要移動 tooPremium 管理磁碟，也請高階儲存體可在您規劃要 toomove hello 區域中。 如需可使用 Azure 服務之地點的最新資訊，請參閱[依區域提供的 Azure 服務](https://azure.microsoft.com/regions/#services)。

## <a name="vm-sizes"></a>VM 大小

如果您要移轉 tooPremium 管理磁碟，您會有 hello VM 所在的區域中的 hello VM tooPremium 可用儲存體能夠大小 tooupdate hello 大小。 檢閱可支援進階儲存體 hello VM 大小。 hello Azure VM 大小規格中所列[虛擬機器的大小](sizes.md)。
檢閱 hello 使用進階儲存體和選擇 hello 最適當的 VM 大小最適合您的工作負載的虛擬機器的效能特性。 請確定有足夠的頻寬可用的 VM toodrive hello 磁碟流量。

## <a name="disk-sizes"></a>磁碟大小

**進階受控磁碟**

有七種型別的進階受控磁碟可以搭配 VM 使用，而且每種都有特定的 IOP 和輸送量限制。 請考量這些限制時選擇 hello VM 的高階磁碟類型根據 hello 產能、 效能、 延展性方面的應用程式需求和尖峰負載。

| 進階磁碟類型  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| 磁碟大小           | 128 GB| 512 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| 每一磁碟的 IOPS       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| 每一磁碟的輸送量 | 每秒 25 MB  | 每秒 50 MB  | 每秒 100 MB | 每秒 150 MB | 每秒 200 MB | 每秒 250 MB | 每秒 250 MB |

**標準受控磁碟**

有七種型別的標準受控磁碟可搭配 VM 使用。 每種類型的容量各不相同，但其 IOPS 和輸送量限制相同。 選擇 hello 根據 hello 容量需求的應用程式的標準管理磁碟類型。

| 標準磁碟類型  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| 磁碟大小           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   | 2048 GB (2TB)    | 4095 GB (4 TB)   | 
| 每一磁碟的 IOPS       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| 每一磁碟的輸送量 | 每秒 60 MB | 每秒 60 MB | 每秒 60 MB | 每秒 60 MB | 每秒 60 MB | 每秒 60 MB | 每秒 60 MB | 

## <a name="disk-caching-policy"></a>磁碟快取原則

**進階受控磁碟**

根據預設，快取原則的磁碟是*唯讀*針對所有 hello 高階資料磁碟，和*讀寫*hello Premium 作業系統磁碟附加 toohello VM。 此組態設定，建議您使用 IOs 應用程式的 tooachieve hello 達到最佳效能。 對於頻繁寫入或唯寫的資料磁碟 (例如 SQL Server 記錄檔)，停用磁碟快取可獲得更佳的應用程式效能。

## <a name="pricing"></a>價格

檢閱 hello[定價管理磁碟](https://azure.microsoft.com/en-us/pricing/details/managed-disks/)。 定價的高階管理磁碟是與 hello 高階 Unmanaged 磁碟相同。 但標準受控磁碟與標準非受控磁碟的價格不同。



## <a name="next-steps"></a>後續步驟

- 深入了解[受控磁碟](managed-disks-overview.md)
