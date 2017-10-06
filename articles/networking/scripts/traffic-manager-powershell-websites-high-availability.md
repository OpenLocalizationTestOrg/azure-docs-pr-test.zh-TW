---
title: "PowerShell 指令碼範例應用程式的高可用性的路由傳送流量 aaaAzure |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 - 路由傳送流量以達到應用程式的高可用性"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: georgewallace
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 11d15780403b4ed79e85d7b3495bc5d674bfdaee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a>路由傳送流量以達到應用程式的高可用性

這個指令碼會建立一個資源群組、兩個 App Service 方案、兩個 Web 應用程式、一個流量管理員設定檔和兩個流量管理員端點。 Hello hello 主要區域中的應用程式無法使用時，traffic Manager 將導向流量 toohello 應用程式與 hello 主要區域中，一個區域及 toohello 次要區域。 在執行之前 hello 指令碼，您必須變更 hello MyWebApp，MyWebAppL1 和 MyWebAppL2 值 toounique 值在整個 Azure。 執行 hello 指令碼之後, 您可以存取與 hello URL mywebapp.trafficmanager.net hello 主要區域中的 hello 應用程式。

如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]


執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate 資源群組、 web 應用程式、 流量管理員設定檔，hello 和所有相關聯的資源。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | 建立用來存放所有資源的資源群組。 |
| [New-AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | 建立 App Service 方案。 這就像是 Azure Web 應用程式的伺服器陣列。 |
| [New-AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | 建立 Azure web 應用程式內 hello 應用程式服務方案。 |
| [Set-AzureRmResource](/powershell/module/azurerm.resources/new-azurermresource) | 建立 Azure web 應用程式內 hello 應用程式服務方案。 |
| [New-AzureRmTrafficManagerProfile](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | 建立 Azure 流量管理員設定檔。 |
| [New-AzureRmTrafficManagerEndpoint](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | 加入端點 tooan Azure 流量管理員設定檔。 |

## <a name="next-steps"></a>後續步驟

如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](https://docs.microsoft.com/powershell/azure/overview)。

其他網路的 PowerShell 指令碼範例可以在 hello [Azure 網路概觀文件](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)。
