---
title: "Azure Stack 中虛擬機器的差異與考量 | Microsoft Docs"
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
ms.openlocfilehash: f97433d7db5811c69851002e459eb01b6e97a722
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="considerations-for-virtual-machines-in-azure-stack"></a>Azure Stack 中虛擬機器的考量

虛擬機器是 Azure Stack 所提供的隨選、可調整計算資源。 當您使用虛擬機器時，必須了解 Azure 與 Azure Stack 中所提供功能之間的差異。 此文章提供 Azure Stack 中虛擬機器及其功能的獨特考量概觀。 若要深入了解 Azure Stack 與 Azure 之間的大致差異，請參閱[主要考量](azure-stack-considerations.md)主題。

## <a name="cheat-sheet-virtual-machine-differences"></a>速查表：虛擬機器差異

| 功能 | Azure (全域) | Azure Stack |
| --- | --- | --- |
| 虛擬機器映像 | Azure Marketplace 包含您可用來建立虛擬機器的映像。 若要檢視 Azure Marketplace 中可用的映像清單，請參閱 [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) 頁面。 | Azure Stack 市集中預設沒有提供任何映像。 Azure Stack 雲端系統管理員應該先將映像[發行](azure-stack-add-default-image.md)或[下載](azure-stack-download-azure-marketplace-item.md)到 Azure Stack 市集，使用者才能使用這些映像。 |
| 虛擬機器大小 | Azure 支援各種不同的虛擬機器大小。 若要了解可用的大小和選項，請參考 [Windows 虛擬機器大小](../virtual-machines/virtual-machines-windows-sizes.md)和 [Linux 虛擬機器大小](../virtual-machines/linux/sizes.md)主題。 | Azure Stack 支援 Azure 中一部分可用的虛擬機器大小。 若要檢視支援的大小清單，請參考此文章的[虛擬機器大小](#virtual-machine-sizes)一節。 |
| 虛擬機器配額 | [配額限制](../azure-subscription-service-limits.md#service-specific-limits)由 Microsoft 設定 | Azure Stack 雲端系統管理員在提供虛擬機器給其使用者之前，必須先[指派配額](azure-stack-setting-quotas.md)。 |
| 虛擬機器擴充功能 |Azure 支援各種不同的虛擬機器擴充功能。 若要了解可用的擴充功能，請參考[虛擬機器擴充功能和功能](../virtual-machines/windows/extensions-features.md)主題。| Azure Stack 支援 Azure 中一部分可用的擴充功能，且每個擴充功能都有特定的版本。 Azure Stack 雲端系統管理員可以選擇要將哪些擴充功能提供給其使用者使用。 若要檢視支援的擴充功能清單，請參考此文章的[虛擬機器擴充功能](#virtual-machine-extensions)一節。 |
| 虛擬機器網路 | 指派給租用戶虛擬機器的公用 IP 位址可透過網際網路存取。<br><br><br>Azure 虛擬機器有固定的 DNS 名稱 | 指派給租用戶虛擬機器的公用 IP 位址時，只能在「Azure Stack 開發套件」環境內存取。 使用者必須能夠透過 [RDP](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop) 或 [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) 存取「Azure Stack 開發套件」，才能連線到在 Azure Stack 中建立的虛擬機器。<br><br>在特定 Azure Stack 執行個體內建立之虛擬機器的 DNS 名稱會以雲端系統管理員所設定的值為基礎。 |
| 虛擬機器儲存體 | 支援[受控磁碟](../virtual-machines/windows/managed-disks-overview.md)。 | Azure Stack 尚未支援受控磁碟。 |
| API 版本 | Azure 一律會有所有虛擬機器功能的最新 API 版本。 | Azure Stack 支援特定的 Azure 服務及這些服務的特定 API 版本。 若要檢視支援的 API 版本清單，請參考此文章的 [API 版本](#api-versions)一節。 |
|虛擬機器可用性設定組|多個容錯網域 (每一區域 2 或 3 個)<br>多個更新網域<br>受控磁碟支援|單一容錯網域<br>單一更新網域<br>無受控磁碟支援|
|虛擬機器擴展集|支援自動調整|不支援自動調整。<br>使用入口網站、Resource Manager 範本或 PowerShell 將更多執行個體新增到擴展集。

## <a name="virtual-machine-sizes"></a>虛擬機器大小 

「Azure Stack 開發套件」支援下列大小： 

| 類型 | 大小 | 支援的大小範圍 |
| --- | --- | --- |
|一般用途 |基本 A|A0-A4|
|一般用途 |標準 A|A0-A7|
|一般用途 |標準 D|D1-D4|
|一般用途 |標準 Dv2|D1v2-D5v2|
|記憶體最佳化|D 系列|D11-D14|
|記憶體最佳化 |Dv2 系列|D11v2-D14v2|

Azure 堆疊和 Azure 中的虛擬機器大小會一致記憶體、 CPU 核心數、 網路頻寬、 磁碟效能，以及定義大小的其他因素方面。 例如，標準 D 大小的虛擬機器，在 Azure 和 Azure 堆疊中是一致的。 

## <a name="virtual-machine-extensions"></a>虛擬機器擴充功能 

 「Azure Stack 開發套件」支援下列虛擬機器擴充功能版本：

![VM 擴充功能](media/azure-stack-vm-considerations/vm-extensions.png)

使用下列 PowerShell 指令碼，來取得您 Azure Stack 環境中所提供虛擬機器擴充功能的清單：

```powershell 
Get-AzureRmVmImagePublisher -Location local | `
  Get-AzureRmVMExtensionImageType | `
  Get-AzureRmVMExtensionImage | `
  Select Type, Version | `
  Format-Table -Property * -AutoSize 
```

## <a name="api-versions"></a>API 版本 

「Azure Stack 開發套件」中的虛擬機器功能支援下列 API 版本：

![VM 資源類型](media/azure-stack-vm-considerations/vm-resoource-types.png)

您可以使用下列 PowerShell 指令碼，來取得您 Azure Stack 環境中所提供虛擬機器功能的 API 版本：

```powershell 
Get-AzureRmResourceProvider | `
  Select ProviderNamespace -Expand ResourceTypes | `
  Select * -Expand ApiVersions | `
  Select ProviderNamespace, ResourceTypeName, @{Name="ApiVersion"; Expression={$_}} | `
  where-Object {$_.ProviderNamespace -like “Microsoft.compute”}
```
如果雲端操作員將您的 Azure Stack 環境更新成較新的版本，所支援資源類型和 API 版本的清單可能會有所不同。

## <a name="next-steps"></a>後續步驟

[在 Azure Stack 中使用 PowerShell 來建立 Windows 虛擬機器](azure-stack-quick-create-vm-powershell.md)
