---
title: "PowerShell 指令碼範例-aaaAzure 升級 Service Fabric 應用程式 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 - 升級 Service Fabric 應用程式。"
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 4f4777607bd6b35a76029e09ddb441006565d4cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-service-fabric-application"></a>升級 Service Fabric 應用程式

這個範例指令碼升級執行 Service Fabric 應用程式執行個體 tooversion 1.3.0。 hello 指令碼複製 hello 新應用程式封裝 toohello 叢集映像存放區、 註冊 hello 應用程式類型、 開始進行監視的升級，和 hello 升級完成或回復之前會持續檢查 hello 升級狀態。 視需要自訂 hello 參數。 

如有需要安裝 hello Service Fabric PowerShell 模組以 hello [Service Fabric SDK](../service-fabric-get-started.md)。 

## <a name="sample-script"></a>範例指令碼

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令的 hello。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | 取得 hello Service Fabric 叢集中的所有 hello 應用程式或特定應用程式。  |
| [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | 取得 hello Service Fabric 應用程式升級狀態。 |
| [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | 取得 hello 註冊 hello Service Fabric 叢集上的 Service Fabric 應用程式類型。 |
| [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | 取消註冊 Service Fabric 應用程式類型。  |
| [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | 複製 Service Fabric 應用程式套件 toohello 映像存放區。  |
| [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | 註冊 Service Fabric 應用程式類型。 |
| [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | 升級 Service Fabric 應用程式 toohello 指定的應用程式類型版本。 |


## <a name="next-steps"></a>後續步驟

如需有關 hello Service Fabric PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/service-fabric/?view=azureservicefabricps)。

可以在 hello 中找到其他的 Powershell 範例，讓 Azure Service Fabric [Azure PowerShell 範例](../service-fabric-powershell-samples.md)。
