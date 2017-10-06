---
title: "aaaAzure PowerShell 指令碼範例-調整 web 應用程式與高可用性架構全球 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 - 透過高可用性架構將 Web 應用程式調整為全球可用"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 470f0129-1efe-462c-a029-5c66e04158a8
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1fcda23250efe4966d63c5dfa744b76c26f3762a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a>透過高可用性架構將 Web 應用程式調整為全球可用

在此案例中，您會建立一個資源群組、兩個 App Service 方案、兩個 Web 應用程式、一個流量管理員設定檔和兩個流量管理員端點。 一旦完成 hello 練習會有高可用性的架構可讓提供全域 hello 最低的網路延遲為基礎的 web 應用程式的可用性。

如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](/powershell/azure/overview)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。

## <a name="sample-script"></a>範例指令碼

[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]

## <a name="clean-up-deployment"></a>清除部署 

Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組、 web 應用程式和所有相關的資源。

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令的 hello。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | 建立用來存放所有資源的資源群組。 |
| [New-AzureRMTrafficManagerProfile](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | 建立流量管理員設定檔。 |
| [New-AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | 建立 App Service 方案。 |
| [New-AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | 建立 Web 應用程式。 |
| [New-AzureRMTrafficManagerEndpoint](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | 在流量管理員設定檔中建立端點。 |

## <a name="next-steps"></a>後續步驟

如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。

Azure App Service Web 應用程式的其他 Azure Powershell 範例可以在 hello [Azure PowerShell 範例](../app-service-powershell-samples.md)。
