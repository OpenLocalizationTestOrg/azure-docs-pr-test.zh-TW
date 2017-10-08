---
title: "aaaDifferences 和 Azure 堆疊中的虛擬機器的考量 |Microsoft 文件"
description: "了解使用 Azure Stack 中虛擬機器時的差異與考量。"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/4/2017
ms.author: sngun
ms.openlocfilehash: cee03e3e83b54efabaecd2647ec7defe371ee870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="considerations-for-virtual-machines-in-azure-stack"></a>Azure Stack 中虛擬機器的考量

虛擬機器是 Azure Stack 所提供的隨選、可調整計算資源。 當您使用虛擬機器時，您必須了解有可用在 Azure 中的 hello 功能與 Azure 堆疊之間的差異。 本文提供 hello 虛擬機器和其功能在 Azure 堆疊中的唯一考量事項的概觀。 toolearn 高階 Azure 堆疊與 Azure 之間的差異，請參閱 「 hello[金鑰考量](azure-stack-considerations.md)主題。

## <a name="cheat-sheet-virtual-machine-differences"></a>速查表：虛擬機器差異

| 功能 | Azure (全域) | Azure Stack |
| --- | --- | --- |
| 虛擬機器映像 | hello Azure Marketplace 包含您可以使用 toocreate 虛擬機器的映像。 請參閱 hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) hello Azure Marketplace 中可用的映像頁面 tooview hello 清單。 | 根據預設，沒有任何映像 hello Azure 堆疊 marketplace 中。 hello Azure 堆疊雲端系統管理員應該[發行](azure-stack-add-default-image.md)或[下載映像](azure-stack-download-azure-marketplace-item.md)toohello 堆疊 Azure marketplace 的使用者才能使用它們。 |
| 虛擬機器大小 | Azure 支援各種不同的虛擬機器大小。 toolearn 有關 hello 可用大小和選項，請參閱 toohello [Windows 虛擬機器大小](../virtual-machines/virtual-machines-windows-sizes.md)和[Linux 虛擬機器大小](../virtual-machines/linux/sizes.md)主題。 | Azure Stack 支援 Azure 中一部分可用的虛擬機器大小。 tooview hello 清單支援的大小，請參閱 toohello[虛擬機器大小](#virtual-machine-sizes)本文一節。 |
| 虛擬機器配額 | [配額限制](../azure-subscription-service-limits.md#service-specific-limits)由 Microsoft 設定 | hello Azure 堆疊雲端系統管理員必須[指派配額](azure-stack-setting-quotas.md)提供了虛擬機器 tootheir 使用者之前。 |
| 虛擬機器擴充功能 |Azure 支援各種不同的虛擬機器擴充功能。 toolearn hello 可用擴充功能，請參閱 toohello[虛擬機器擴充功能和功能](../virtual-machines/windows/extensions-features.md)主題。| Azure 堆疊支援在 Azure 中可用擴充功能的子集，且 hello 延伸模組的每個有特定的版本。 hello Azure 堆疊雲端系統管理員可以選擇哪些擴充功能 toobe 進行可用 toofor 他們的使用者。 tooview hello 清單支援的延伸模組，請參閱 toohello[虛擬機器擴充功能](#virtual-machine-extensions)本文一節。 |
| 虛擬機器網路 | 透過網際網路 hello 指派 tootenant 虛擬機器的公用 IP 位址都可存取的。<br><br><br>Azure 虛擬機器有固定的 DNS 名稱 | 指派 tooa 租用戶虛擬機器的公用 IP 位址是只 hello Azure 堆疊開發套件的環境中存取。 使用者必須擁有存取 toohello Azure 堆疊 Development Kit 透過[RDP](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop)或[VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)建立 Azure 堆疊中的 tooconnect tooa 虛擬機器。<br><br>特定的 Azure 堆疊執行個體內建立的虛擬機器有根據 hello 值 hello 雲端系統管理員所設定的 DNS 名稱。 |
| 虛擬機器儲存體 | 支援[受控磁碟](../virtual-machines/windows/managed-disks-overview.md)。 | Azure Stack 尚未支援受控磁碟。 |
| API 版本 | Azure 一律會有所有的 hello 虛擬機器功能的 hello 最新 API 版本。 | Azure Stack 支援特定的 Azure 服務及這些服務的特定 API 版本。 tooview hello 清單支援的 API 版本，請參閱 toohello [API 版本](#api-versions)本文一節。 |
|虛擬機器可用性設定組|多個容錯網域 (每一區域 2 或 3 個)<br>多個更新網域<br>受控磁碟支援|單一容錯網域<br>單一更新網域<br>無受控磁碟支援|
|虛擬機器擴展集|支援自動調整|不支援自動調整。<br>新增執行個體 tooa 小數位數組使用 hello 入口網站中，資源管理員範本或 PowerShell。

## <a name="virtual-machine-sizes"></a>虛擬機器大小 

hello Azure 堆疊開發套件支援下列大小 hello: 

| 類型 | 大小 | 支援的大小範圍 |
| --- | --- | --- |
|一般用途 |基本 A|A0-A4|
|一般用途 |標準 A|A0-A7|
|一般用途 |標準 D|D1-D4|
|一般用途 |標準 Dv2|D1v2-D5v2|
|記憶體最佳化|D 系列|D11-D14|
|記憶體最佳化 |Dv2 系列|D11v2-D14v2|

Azure 堆疊和 Azure 中的虛擬機器大小會一致 hello 記憶體、 CPU 核心數、 網路頻寬、 磁碟效能，以及定義 hello 大小的其他因素方面。 例如，hello 標準 D 大小在 Azure 和 Azure 堆疊中的虛擬機器是一致的。 

## <a name="virtual-machine-extensions"></a>虛擬機器擴充功能 

 hello Azure 堆疊開發套件支援下列虛擬機器擴充功能版本 hello:

![VM 擴充功能](media/azure-stack-vm-considerations/vm-extensions.png)

使用下列 PowerShell 指令碼 tooget hello 清單中的 Azure 堆疊環境中的虛擬機器擴充功能的 hello:

```powershell 
Get-AzureRmVmImagePublisher -Location local | `
  Get-AzureRmVMExtensionImageType | `
  Get-AzureRmVMExtensionImage | `
  Select Type, Version | `
  Format-Table -Property * -AutoSize 
```

## <a name="api-versions"></a>API 版本 

Azure 堆疊開發套件中的虛擬機器功能都支援下列 API 版本的 hello:

![VM 資源類型](media/azure-stack-vm-considerations/vm-resoource-types.png)

您可以使用下列 PowerShell 指令碼 tooget hello API 版本 hello Azure 堆疊環境中的虛擬機器功能的 hello:

```powershell 
Get-AzureRmResourceProvider | `
  Select ProviderNamespace -Expand ResourceTypes | `
  Select * -Expand ApiVersions | `
  Select ProviderNamespace, ResourceTypeName, @{Name="ApiVersion"; Expression={$_}} | `
  where-Object {$_.ProviderNamespace -like “Microsoft.compute”}
```
支援資源類型的 hello 清單和應用程式開發介面版本可能會不同，如果 hello 雲端運算子會更新您 Azure 堆疊環境 tooa 較新版本。

## <a name="next-steps"></a>後續步驟

[在 Azure Stack 中使用 PowerShell 來建立 Windows 虛擬機器](azure-stack-quick-create-vm-powershell.md)
