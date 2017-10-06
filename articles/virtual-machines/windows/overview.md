---
title: "aaaWindows 虛擬機器概觀 |Microsoft 文件"
description: "了解在 Azure 中建立及管理 Windows 虛擬機器。"
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: fbae9c8e-2341-4ed0-bb20-fd4debb2f9ca
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 8015b1aa4bcdaac2e721f25d85a5bc995a22f0f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-windows-virtual-machines-in-azure"></a>Azure 中的 Windows 虛擬機器概觀

Azure 虛擬機器 (VM) 是由 Azure 所提供的[隨選且可調整的數種運算資源](../../app-service-web/choose-web-site-cloud-service-vm.md)類型之一。 一般而言，當您需要更充分掌控 hello 運算環境比 hello 其他選項提供選擇 VM。 本文提供您在建立 VM 之前應該的事項、建立方式及管理方式的相關資訊。

Azure VM 可讓您無須 toobuy hello 的虛擬化彈性和維護 hello 實體硬體執行它。 不過，您仍然需要 toomaintain hello VM 上執行工作，例如設定、 修補，以及安裝在其執行的 hello 軟體。

Azure 虛擬機器可用於許多用途。 部分範例如下：

* **開發和測試**– Azure Vm 提供快速而輕鬆 toocreate 使用特定組態的電腦所需 toocode 和測試應用程式。
* **Hello 雲端中的應用程式**– 應用程式的需求可以變動，因為它可能會使經濟的意義上 toorun 它在 Azure 中的 VM 上。 當您需要 VM 時便支付額外的 VM，而當您不需要時便關閉這些 VM。
* **擴充資料中心**– Azure 虛擬網路中的虛擬機器可以輕鬆地連接的 tooyour 組織的網路。

應用程式所使用的 Vm 的 hello 數目可以向上延展和 toowhatever 是必要的 toomeet 您的需求。

## <a name="what-do-i-need-toothink-about-before-creating-a-vm"></a>我需要什麼 toothink 有關之前建立的 VM？
當您在 Azure 中建置應用程式基礎結構時，總是會有許多[設計考量](/architecture/reference-architectures/virtual-machines-linux?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 這些層面，VM 會都重要 toothink 有關開始之前：

* 您的應用程式資源 hello 名稱
* hello 儲存 hello 資源的位置
* hello 的 hello VM 的大小
* hello 可以建立的 Vm 數目上限
* 執行 hello hello VM 作業系統
* hello VM 在啟動之後的 hello 組態
* hello 相關聯的資源 VM 需要該 hello

### <a name="naming"></a>命名
虛擬機器具有[名稱](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)指派的 tooit 且有電腦名稱設定為 hello 作業系統的一部分。 VM 的 hello 名稱可以是 too15 字元組成。

如果您使用 Azure toocreate hello 作業系統磁碟，hello 電腦名稱，而且 hello 虛擬機器名稱是 hello 相同。 如果您[上傳並使用自己的映像](upload-generalized-managed.md)，包含先前設定的作業系統，並用它 toocreate 虛擬機器，hello 名稱可以不同。 我們建議您上傳您自己的映像檔，當您進行 hello hello 作業系統中的電腦名稱和 hello 相同的 hello 虛擬機器名稱。

### <a name="locations"></a>位置
在 Azure 中建立的所有資源都分散於多個[地理區域](https://azure.microsoft.com/regions/)hello 世界各地。 Hello 區域通常稱為**位置**當您建立 VM。 針對 VM，hello 位置會指定 hello 虛擬硬碟的儲存位置。

下表顯示一些 hello 方式，您可以取得一份可用的位置。

| 方法 | 說明 |
| --- | --- |
| Azure 入口網站 |當您建立 VM 時，請從 hello 清單中選取的位置。 |
| Azure PowerShell |使用 hello [Get AzureRmLocation](/powershell/module/azurerm.resources/get-azurermlocation)命令。 |
| REST API |使用 hello[列出位置](https://docs.microsoft.com/rest/api/resources/subscriptions#Subscriptions_ListLocations)作業。 |

### <a name="vm-size"></a>VM 大小
hello[大小](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)hello 您使用的 VM 由 hello 工作負載的 toorun。 您選擇的 hello 大小然後決定因素，例如處理能力、 記憶體和儲存體容量。 Azure 提供各種不同的大小 toosupport 許多類型的用法。

Azure 會收費[每小時價格](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)hello VM 的大小和作業系統為基礎。 部分的時數，Azure 只費用 hello 分鐘使用。 儲存體是個別定價與收費。

### <a name="vm-limits"></a>VM 限制
您的訂用帳戶具有預設[配額限制](../../azure-subscription-service-limits.md)就地可能會影響 hello 部署許多 Vm 為您的專案。 每個訂用帳戶為基礎的 hello 目前限制為 20 的 Vm，每個區域。 只要提出支援票證來要求增加，即可提高配額限制。

### <a name="operating-system-disks-and-images"></a>作業系統磁碟和映像
虛擬機器使用[虛擬硬碟 (Vhd)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toostore 其作業系統 (OS) 和資料。 Vhd 也可用於 hello 映像，您可以選擇從 tooinstall OS。 

Azure 提供了許多[marketplace 映像](https://azure.microsoft.com/marketplace/virtual-machines/)toouse 與各種版本和 Windows Server 作業系統的類型。 Marketplace 映像是依映像發行者、優惠、SKU 和版本 (版本通常會指定為最新版本) 來識別。 

下表顯示一些您可以找到映像的 hello 資訊的方法。

| 方法 | 說明 |
| --- | --- |
| Azure 入口網站 |當您選取映像 toouse hello 值會自動指定為您。 |
| Azure PowerShell |[Get-AzureRMVMImagePublisher](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/get-azurermvmimagepublisher) -Location "location"<BR>[Get-AzureRMVMImageOffer](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/get-azurermvmimageoffer) -Location "location" -Publisher "publisherName"<BR>[Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) -Location "location" -Publisher "publisherName" -Offer "offerName" |
| REST API |[列出映像發行者](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publishers)<BR>[列出映像優惠](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offers)<BR>[列出映像 SKU](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offer-skus) |

您可以選擇在太[上傳並使用自己的映像](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)並執行動作時，不使用 hello 發行者名稱、 提供項目，以及 sku。

### <a name="extensions"></a>擴充功能
VM [擴充](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)會透過 post 部署設定及自動化工作為您的 VM 提供其他功能。

可以使用擴充功能來完成這些常見工作︰

* **執行自訂指令碼**– hello[自訂指令碼延伸](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)可協助您設定 hello VM 上的工作負載，藉由 hello 佈建 VM 時，執行您的指令碼。
* **部署和管理設定**– hello [PowerShell 預期狀態設定 (DSC) 的延伸模組](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)可協助您設定在 VM toomanage DSC 組態和環境。
* **收集診斷資料**– hello [Azure 診斷延伸模組](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)能協助您設定 hello VM toocollect 診斷資料可以使用的 toomonitor hello 應用程式的健全狀況。

### <a name="related-resources"></a>相關資源
此表格中的 hello 資源所使用的 hello VM 和需要 tooexist 或 hello VM 建立時建立。

| 資源 | 必要 | 說明 |
| --- | --- | --- |
| [資源群組](../../azure-resource-manager/resource-group-overview.md) |是 |hello VM 必須包含在資源群組。 |
| [儲存體帳戶](../../storage/common/storage-create-storage-account.md) |是 |hello VM 需要 hello 儲存體帳戶 toostore 其虛擬硬碟。 |
| [虛擬網路](../../virtual-network/virtual-networks-overview.md) |是 |hello VM 必須是虛擬網路的成員。 |
| [公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) |否 |hello VM 可以存取公用 IP 位址指派 tooit tooremotely。 |
| [網路介面](../../virtual-network/virtual-network-network-interface.md) |是 |hello VM 需要 hello 網路介面 toocommunicate hello 網路中。 |
| [資料磁碟](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |否 |hello VM 可以包含資料磁碟 tooexpand 儲存體功能。 |

## <a name="how-do-i-create-my-first-vm"></a>如何建立第一個 VM？
有幾個選擇可供您建立 VM。 hello 選擇您的項目取決於您是在 hello 環境。 

下表提供資訊 tooget 您開始建立您的 VM。

| 方法 | 文章 |
| --- | --- |
| Azure 入口網站 |[建立執行 Windows 的 hello 入口網站的虛擬機器](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| 範本 |[利用 Resource Manager 範本建立 Windows 虛擬機器](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Azure PowerShell |[使用 PowerShell 建立 Windows VM](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| 用戶端 SDK |[使用 C# 部署 Azure 資源](csharp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| REST API |[建立或更新 VM](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-create-or-update) |

您希望它絕對不會發生，但偶爾會發生錯誤。 如果這種情況發生 tooyou，請查看中的 hello 資訊[部署問題疑難排解資源管理員在 Azure 中建立 Windows 虛擬機器](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

## <a name="how-do-i-manage-hello-vm-that-i-created"></a>如何管理 hello 我建立的 VM？
可以使用以瀏覽器為基礎的入口網站、支援指令碼處理的命令列工具，或直接透過 API 管理 VM。 一些您可能需要執行的一般管理工作會取得 VM 的相關資訊登入 tooa VM 管理可用性，並進行備份。

### <a name="get-information-about-a-vm"></a>取得 VM 的相關資訊
下表顯示您部分 hello 的方式，您可以取得 VM 的相關資訊。

| 方法 | 說明 |
| --- | --- |
| Azure 入口網站 |在 hello 中樞功能表中，按一下 **虛擬機器**，然後從 hello 清單中選取 hello VM。 Hello VM hello 刀鋒視窗，您必須存取 toooverview 資訊、 設定值，以及監視的度量。 |
| Azure PowerShell |如需使用 PowerShell toomanage Vm，請參閱[建立及管理 Windows Vm hello Azure PowerShell 模組](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 |
| REST API |使用 hello[取得 VM 資訊](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get)VM 作業 tooget 資訊。 |
| 用戶端 SDK |如需使用 C# toomanage Vm，請參閱[管理 Azure 虛擬機器使用 Azure 資源管理員和 C#](csharp-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 |

### <a name="log-on-toohello-vm"></a>登入 toohello VM
您使用 hello 連接 按鈕 hello Azure 入口網站中太[啟動遠端桌面 (RDP) 工作階段](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 可能有時發生錯誤時嘗試 toouse 遠端連線。 如果 tooyou 發生這種狀況，請參閱中的 hello 說明資訊[疑難排解遠端桌面連線 tooan Azure 虛擬機器執行 Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

### <a name="manage-availability"></a>管理可用性
重要的是您 toounderstand 如何太[確保高可用性](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)應用程式。 這項設定包括建立至少一個正在執行的多個 Vm tooensure。

在您的部署 tooqualify 我們 99.95 VM 的服務等級協定的順序，您需要 toodeploy 執行您的工作負載內的兩個或多個 Vm[可用性設定組](tutorial-availability-sets.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 此組態可確保您的 VM 會分散多個容錯網域，且部署至具有不同維護期間的主機。 完整的 hello [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/)說明 hello 保證整個 Azure 的可用性。

### <a name="back-up-hello-vm"></a>備份 hello VM
A[復原服務保存庫](../../backup/backup-introduction-to-azure-backup.md)是使用的 tooprotect 資料和 Azure 備份和 Azure Site Recovery 服務中的資產。 您也可以使用復原服務保存庫[部署和管理的資源管理員部署的 Vm 使用 PowerShell 備份](../../backup/backup-azure-vms-automation.md)。 

## <a name="next-steps"></a>後續步驟
* 如果您的意圖 toowork 使用 Linux Vm，請查看在[Azure 與 Linux](../linux/overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
* 深入了解 hello 指導方針設定您的基礎結構在 hello[範例 Azure 基礎結構的逐步解說](infrastructure-example.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
