---
title: "aaaSelect Windows VM 映像在 Azure 中 |Microsoft 文件"
description: "了解如何 toouse Azure PowerSHell toodetermine hello 發行者、 方案、 SKU 和 Marketplace 的 VM 映像的版本。"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a>Toofind Windows VM hello Azure powershell 的 Azure Marketplace 中的映像

本主題描述 toouse Azure PowerShell toofind VM hello Azure Marketplace 中的映像。 當您建立 Windows VM 時，請使用此資訊 toospecify Marketplace 映像。

請確定您已安裝，並最新設定 hello [Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。



## <a name="table-of-commonly-used-windows-images"></a>常用 Windows 映像表
| PublisherName | 提供項目 | SKU |
|:--- |:--- |:--- |:--- |
| MicrosoftWindowsServer |WindowsServer |2016-Datacenter |
| MicrosoftWindowsServer |WindowsServer |2016-Datacenter-Server-Core |
| MicrosoftWindowsServer |WindowsServer |2016-Datacenter-with-Containers |
| MicrosoftWindowsServer |WindowsServer |2016-Nano-Server |
| MicrosoftWindowsServer |WindowsServer |2012-R2-Datacenter |
| MicrosoftWindowsServer |WindowsServer |2008-R2-SP1 |
| MicrosoftDynamicsNAV |DynamicsNAV |2017 |
| MicrosoftSharePoint |MicrosoftSharePointServer |2016 |
| MicrosoftSQLServer |SQL2016-WS2016 |Enterprise |
| MicrosoftSQLServer |SQL2014SP2-WS2012R2 |Enterprise |
| MicrosoftWindowsServerHPCPack |WindowsServerHPCPack |2012R2 |
| MicrosoftWindowsServerEssentials |WindowsServerEssentials |WindowsServerEssentials |

## <a name="find-specific-images"></a>尋找特定映像


在建立新的虛擬機器與 Azure 資源管理員時，在某些情況下您需要 toospecify 映像具有下列映像屬性的 hello hello 組合：

* 發佈者
* 提供項目
* SKU

例如，使用這些值以 hello[組 AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet 或使用資源群組範本中，您必須指定建立的 VM toobe hello 型別。

如果您需要 toodetermine 這些值，您可以執行 hello [Get AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher)， [Get AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer)，和[Get AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlettoonavigate hello 映像。 您要判斷這些值：

1. 清單 hello 映像的發行者。
2. 針對指定的發行者，列出其提供項目。
3. 針對指定的提供項目，列出其 SKU。

首先，列出 hello 發行者以 hello 下列命令：

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

填入您所選的發行者的名稱，然後執行下列命令的 hello:

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

填入您所選的提供項目名稱，然後執行下列命令的 hello:

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

從 hello hello 輸出`Get-AzureRMVMImageSku`命令時，您會有新的虛擬機器所需 toospecify hello 映像的所有 hello 資訊。

hello 下列範例示範完整的範例：

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

輸出：

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

Hello"MicrosoftWindowsServer"發行者：

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

輸出：

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

Hello"WindowsServer 」 提供：

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

輸出：

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

從這個清單中，複製 hello 選擇 SKU 名稱，而且您擁有 hello 所有 hello 資訊`Set-AzureRMVMSourceImage`PowerShell cmdlet 或資源群組範本。

## <a name="next-steps"></a>後續步驟
現在您可以選擇明確地說 hello 映像您會想 toouse。 toocreate 虛擬機器，快速利用剛找到的 hello 映像資訊，請參閱[使用 PowerShell 建立 Windows 虛擬機器](quick-create-powershell.md)。
