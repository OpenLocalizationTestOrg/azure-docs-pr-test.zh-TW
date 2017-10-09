---
title: "從 AWS 和其他平台 tooManaged aaaMigrate 磁碟在 Azure 中 |Microsoft 文件"
description: "在 Azure 中使用從其他雲端 (如 AWS) 或其他虛擬化平台上傳的 VHD 建立 VM，並充分利用 Azure 受控磁碟。"
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
ms.date: 02/07/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 66c3912397ab905aafb3910e13ac711befb8f502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-amazon-web-services-aws-and-other-platforms-toomanaged-disks-in-azure"></a>從 Amazon Web Services (AWS) 和其他平台 tooManaged 磁碟在 Azure 中的移轉

您可以上傳 VHD 檔案從 AWS 或內部部署虛擬化解決方案 tooAzure toocreate 利用管理磁碟的 Vm。 Azure 受管理的磁碟移除 hello 需要 toomanaging 儲存體帳戶的 Azure IaaS Vm。 您有 tooonly 指定 hello 類型 （高階或標準），以及在需要時，磁碟大小，而且 Azure 將會建立並為您管理 hello 磁碟。 

您可以上傳一般化和特製化 VHD。 
- **一般化 VHD** - 已使用 Sysprep 將您所有的個人帳戶資訊移除。 
- **特製化 VHD** -維護 hello 使用者帳戶、 應用程式及其他狀態資料從您的原始 VM。 

> [!IMPORTANT]
> 上傳任何 VHD tooAzure 之前, 您應該遵循[準備 Windows VHD 或 VHDX tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
>
>


| 案例                                                                                                                         | 文件                                                                                                                       |
|----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| 您有現有的 AWS EC2 執行個體，您可能想 toomigrate tooAzure 受管理磁碟                                     | [從 Amazon Web Services (AWS) tooAzure 移動 VM](aws-to-azure.md)                           |
| 從 VM 和您想要做為映像 toocreate toouse toouse 其他虛擬化平台，您有多個 Azure Vm。 | [一般化的 VHD 上傳，並在 Azure 中使用 toocreate 新的 Vm](upload-generalized-managed.md) |
| 您有唯一的自訂您想要在 Azure 中的 toorecreate VM。                                                      | [上傳特製化的 VHD tooAzure 並建立新的 VM](create-vm-specialized.md)         |


## <a name="overview-of-managed-disks"></a>受控磁碟概觀

Azure 受管理的磁碟藉由移除 hello 需要 toomanage 儲存體帳戶，簡化管理 VM。 受控磁碟也受惠於可用性設定組中更佳的 VM 可靠性。 它會確保 hello 磁碟的可用性設定組不同的 Vm 將會從每個其他 tooavoid 單點失敗充分的隔離性。 自動將不同的 Vm 磁碟置於可用性設定組中不同的存放裝置延展單位 （戳記） 這會限制 hello toohardware 和軟體的失敗原因造成單一的儲存體延展單位故障的影響力。 根據您的需求，您可選擇兩種類型的儲存體選項︰ 
 
- [進階受控磁碟](../../storage/common/storage-premium-storage.md)是固態硬碟 (SSD) 式儲存媒體，可針對執行大量 I/O 工作負載的虛擬機器，提供高效能、低延遲的磁碟支援。 您可以利用的 hello 速度與這些磁碟移轉 tooPremium 管理磁碟的效能。  

- [標準管理磁碟](../../storage/common/storage-standard-storage.md)使用硬碟機 (HDD) 基礎儲存媒體，而且最適合用來開發/測試和其他不頻繁存取工作負載的敏感性較低的 tooperformance 變化性。  

## <a name="plan-for-hello-migration-toomanaged-disks"></a>規劃移轉 hello tooManaged 磁碟

本節可協助您 toomake hello 最佳決定 VM 和磁碟類型。


### <a name="location"></a>位置

挑選 Azure 受控磁碟可用的位置。 如果您正在移轉 tooPremium 管理磁碟，也請確定高階儲存體可用規劃至 toomigrate hello 區域中。 如需可使用 Azure 服務之地點的最新資訊，請參閱[依區域提供的 Azure 服務](https://azure.microsoft.com/regions/#services)。

### <a name="vm-sizes"></a>VM 大小

如果您要移轉 tooPremium 管理磁碟，您會有 hello VM 所在的區域中的 hello VM tooPremium 可用儲存體能夠大小 tooupdate hello 大小。 檢閱可支援進階儲存體 hello VM 大小。 hello Azure VM 大小規格中所列[虛擬機器的大小](sizes.md)。
檢閱 hello 使用進階儲存體和選擇 hello 最適當的 VM 大小最適合您的工作負載的虛擬機器的效能特性。 請確定有足夠的頻寬可用的 VM toodrive hello 磁碟流量。

### <a name="disk-sizes"></a>磁碟大小

**進階受控磁碟**

有三種類型的進階受控磁碟可以搭配您的 VM 使用，而且每種都有特定的 IOP 和輸送量限制。 當您選擇 hello VM 的高階磁碟類型根據 hello 產能、 效能、 延展性方面的應用程式需求和尖峰負載時，請考慮這些限制。

| 進階磁碟類型  | P10               | P20               | P30               |
|---------------------|-------------------|-------------------|-------------------|
| 磁碟大小           | 128 GB            | 512 GB            | 1024 GB (1 TB)    |
| 每一磁碟的 IOPS       | 500               | 2300              | 5000              |
| 每一磁碟的輸送量 | 每秒 100 MB | 每秒 150 MB | 每秒 200 MB |

**標準受控磁碟**

有五種類型的標準受控磁碟可搭配您的 VM 使用。 每種類型的容量各不相同，但其 IOPS 和輸送量限制相同。 選擇 hello 根據 hello 容量需求的應用程式的標準管理磁碟類型。

| 標準磁碟類型  | S4               | S6               | S10              | S20              | S30              |
|---------------------|------------------|------------------|------------------|------------------|------------------|
| 磁碟大小           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   |
| 每一磁碟的 IOPS       | 500              | 500              | 500              | 500              | 500              |
| 每一磁碟的輸送量 | 每秒 60 MB | 每秒 60 MB | 每秒 60 MB | 每秒 60 MB | 每秒 60 MB |

### <a name="disk-caching-policy"></a>磁碟快取原則 

**進階受控磁碟**

根據預設，快取原則的磁碟是*唯讀*針對所有 hello 高階資料磁碟，和*讀寫*hello Premium 作業系統磁碟附加 toohello VM。 此組態設定，建議您使用 IOs 應用程式的 tooachieve hello 達到最佳效能。 對於頻繁寫入或唯寫的資料磁碟 (例如 SQL Server 記錄檔)，停用磁碟快取可獲得更佳的應用程式效能。

### <a name="pricing"></a>價格

檢閱 hello[定價管理磁碟](https://azure.microsoft.com/en-us/pricing/details/managed-disks/)。 定價的高階管理磁碟是與 hello 高階 Unmanaged 磁碟相同。 但標準受控磁碟與標準非受控磁碟的價格不同。


## <a name="next-steps"></a>後續步驟

- 上傳任何 VHD tooAzure 之前, 您應該遵循[準備 Windows VHD 或 VHDX tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
