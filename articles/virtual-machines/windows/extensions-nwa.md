---
title: "aaaAzure 網路監看員的代理程式適用於 Windows 的虛擬機器擴充功能 |Microsoft 文件"
description: "部署 Windows 虛擬機器使用虛擬機器擴充功能上的 hello 網路監看員的代理程式。"
services: virtual-machines-windows
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 27e46af7-2150-45e8-b084-ba33de8c5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 21298706e462ff32c4d314f9a1ad127074ddf481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a>適用於 Windows 的網路監看員代理程式虛擬機器擴充功能

## <a name="overview"></a>概觀

[Azure 網路監看員](https://review.docs.microsoft.com/en-us/azure/network-watcher/)是網路效能的監視、診斷和分析服務，可讓您監視 Azure 網路。 hello 網路監看員的代理程式的虛擬機器擴充功能是某些 hello Azure 虛擬機器上的網路監看員功能的需求。 這包括擷取隨選網路流量和其他進階功能。

此文件詳細資料 hello 支援平台和部署選項 hello 網路監看員的代理程式的虛擬機器擴充功能的 Windows。

## <a name="prerequisites"></a>必要條件

### <a name="operating-system"></a>作業系統

hello 網路監看員的代理程式擴充功能的 Windows 可執行 Windows Server 2008 R2、 2012年、 2012 R2、 及 2016年釋放。 請注意，hello Nano Server 不支援這一次。

### <a name="internet-connectivity"></a>網際網路連線

某些 hello 網路監看員的代理程式的功能要求該 hello 目標虛擬機器必須連接的 toohello 網際網路。 不使用 hello 能力 tooestablish 傳出連線的一些 hello 網路監看員的代理程式功能可能故障，或變成無法使用。 如需詳細資訊，請參閱 hello[網路監看員文件](../../network-watcher/network-watcher-monitoring-overview.md)。

## <a name="extension-schema"></a>擴充功能結構描述

hello 下列 JSON 顯示 hello 網路監看員的代理程式延伸模組的 hello 結構描述。 hello 延伸模組都不需要也不支援任何使用者提供的設定，這次並依賴其預設設定。

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentWindows",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a>屬性值

| 名稱 | 值 / 範例 |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.Azure.NetworkWatcher |
| 類型 | NetworkWatcherAgentWindows |
| typeHandlerVersion | 1.4 |


## <a name="template-deployment"></a>範本部署

也可以使用 Azure Resource Manager 範本部署 Azure VM 擴充功能。 hello hello 前一節中詳細的 JSON 結構描述可用於 Azure Resource Manager 範本 toorun hello 網路監看員的代理程式擴充功能，在 Azure 資源管理員範本部署期間。

## <a name="powershell-deployment"></a>PowerShell 部署

hello`Set-AzureRmVMExtension`命令可以是使用的 toodeploy hello 網路監看員的代理程式的虛擬機器擴充功能 tooan 現有的虛擬機器。

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a>疑難排解和支援

### <a name="troubleshooting"></a>疑難排解

從 hello Azure 入口網站，並使用 hello Azure PowerShell 模組，可以擷取有關 hello 部署狀態的延伸模組的資料。 toosee hello 部署狀態的延伸模組指定的 vm 時，執行下列命令所使用的 hello hello Azure PowerShell 模組。

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

延伸模組執行輸出 hello 中找到的記錄的 toofiles 之後，目錄：

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a>支援

如果您需要更多說明，在本文中的任何時間點，您可以參閱 toohello 網路監看員使用者指南 》 文件，或連絡 hello Azure 專家發表 hello [MSDN Azure 和堆疊溢位論壇](https://azure.microsoft.com/en-us/support/forums/)。 或者，您可以提出 Azure 支援事件。 移 toohello [Azure 支援服務網站](https://azure.microsoft.com/en-us/support/options/)並選取 取得支援。 使用 Azure 所支援的相關資訊，請參閱 hello [Microsoft Azure 支援常見問題集](https://azure.microsoft.com/en-us/support/faq/)。
