---
title: "aaaAzure PowerShell 指令碼範例從叢集移除應用程式 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 - 從 Service Fabric 叢集移除應用程式。"
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
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 3fe2082c2fbeffbff1622f206021d4d907197d19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>從 Service Fabric 叢集移除應用程式

這個範例指令碼刪除正在執行的 Service Fabric 應用程式執行個體、 取消登錄的應用程式類型和版本從 hello 叢集和從 hello 叢集映像存放區刪除 hello 應用程式套件。  正在刪除 hello 應用程式執行個體也會刪除所有 hello 執行該應用程式相關聯的服務執行個體。 視需要自訂 hello 參數。 

如有需要安裝 hello Service Fabric PowerShell 模組以 hello [Service Fabric SDK](../service-fabric-get-started.md)。 

## <a name="sample-script"></a>範例指令碼

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令的 hello。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | 移除 hello 叢集正在執行的 Service Fabric 應用程式執行個體。  |
| [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | 取消註冊 Service Fabric 應用程式類型和從 hello 叢集的版本。 |
| [Remove-ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | Service Fabric 應用程式套件移除 hello 映像存放區。|

## <a name="next-steps"></a>後續步驟

如需有關 hello Service Fabric PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/service-fabric/?view=azureservicefabricps)。

可以在 hello 中找到其他的 Powershell 範例，讓 Azure Service Fabric [Azure PowerShell 範例](../service-fabric-powershell-samples.md)。
