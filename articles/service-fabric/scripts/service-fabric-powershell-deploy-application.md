---
title: "aaaAzure PowerShell 指令碼範例-將部署應用程式 tooa 叢集 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例-部署應用程式 tooa Service Fabric 叢集。"
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
ms.openlocfilehash: b417c9908c72f016e930c43ff2d13e0cc5451f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a>部署應用程式 tooa Service Fabric 叢集

這個範例指令碼複製應用程式封裝 tooa 叢集映像存放區、 hello 叢集中註冊 hello 應用程式類型和建立應用程式執行個體從 hello 應用程式類型。  如果任何預設的服務定義 hello hello 目標應用程式類型應用程式資訊清單中，此時會建立這些服務。 視需要自訂 hello 參數。 

如有需要安裝 hello Service Fabric PowerShell 模組以 hello [Service Fabric SDK](../service-fabric-get-started.md)。 

## <a name="sample-script"></a>範例指令碼

[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a>清除部署 

Hello 指令碼範例執行後，hello 中的指令碼[移除應用程式](service-fabric-powershell-remove-application.md)可以是使用的 tooremove hello 應用程式執行個體、 取消註冊 hello 應用程式類型，並從 hello 映像存放區刪除 hello 應用程式套件。

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令的 hello。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | 複製應用程式封裝 toohello 叢集映像存放區。  |
|[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| 註冊應用程式類型和 hello 叢集上的版本。 |
|[New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| 從註冊的應用程式類型建立應用程式。 |

## <a name="next-steps"></a>後續步驟

如需有關 hello Service Fabric PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/service-fabric/?view=azureservicefabricps)。

可以在 hello 中找到其他的 Powershell 範例，讓 Azure Service Fabric [Azure PowerShell 範例](../service-fabric-powershell-samples.md)。
