---
title: "PowerShell 指令碼範例-aaaAzure 建立 Service Fabric 叢集 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 - 建立 Service Fabric 叢集。"
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 12fdc201bd51688cb850cd456b1e00442b79c22d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster"></a>建立 Service Fabric 叢集

這個範例指令碼會建立 Service Fabric 叢集，這是使用 X.509 憑證保護的五節點叢集。  hello 命令會建立自我簽署的憑證，並將它上載 tooa 新的金鑰保存庫。 hello 憑證也是複製的 tooa 本機目錄。  設定 hello *-OS*參數 toochoose hello 版本的 Windows 或 Linux hello 叢集節點上執行。  視需要自訂 hello 參數。

如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](/powershell/azure/overview)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。 

## <a name="sample-script"></a>範例指令碼

[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]

## <a name="clean-up-deployment"></a>清除部署 

Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組、 叢集及所有相關的資源。

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令的 hello。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [New-AzureRmServiceFabricCluster](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | 建立新的 Service Fabric 叢集。 |

## <a name="next-steps"></a>後續步驟

如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。

適用於 Azure Service Fabric 的其他 Azure Powershell 範例可以在 hello [Azure PowerShell 範例](../service-fabric-powershell-samples.md)。
