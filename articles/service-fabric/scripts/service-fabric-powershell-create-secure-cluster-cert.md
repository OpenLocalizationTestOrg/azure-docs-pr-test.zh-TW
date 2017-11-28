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
# <a name="create-a-service-fabric-cluster"></a><span data-ttu-id="689fb-103">建立 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="689fb-103">Create a Service Fabric cluster</span></span>

<span data-ttu-id="689fb-104">這個範例指令碼會建立 Service Fabric 叢集，這是使用 X.509 憑證保護的五節點叢集。</span><span class="sxs-lookup"><span data-stu-id="689fb-104">This sample script creates a Service Fabric cluster a five-node cluster secured with an X.509 certificate.</span></span>  <span data-ttu-id="689fb-105">hello 命令會建立自我簽署的憑證，並將它上載 tooa 新的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="689fb-105">hello command creates a self-signed certificate and uploads it tooa new key vault.</span></span> <span data-ttu-id="689fb-106">hello 憑證也是複製的 tooa 本機目錄。</span><span class="sxs-lookup"><span data-stu-id="689fb-106">hello certificate is also copied tooa local directory.</span></span>  <span data-ttu-id="689fb-107">設定 hello *-OS*參數 toochoose hello 版本的 Windows 或 Linux hello 叢集節點上執行。</span><span class="sxs-lookup"><span data-stu-id="689fb-107">Set hello *-OS* parameter toochoose hello version of Windows or Linux that runs on hello cluster nodes.</span></span>  <span data-ttu-id="689fb-108">視需要自訂 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="689fb-108">Customize hello parameters as needed.</span></span>

<span data-ttu-id="689fb-109">如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](/powershell/azure/overview)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="689fb-109">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="689fb-110">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="689fb-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="689fb-111">清除部署</span><span class="sxs-lookup"><span data-stu-id="689fb-111">Clean up deployment</span></span> 

<span data-ttu-id="689fb-112">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組、 叢集及所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="689fb-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, cluster, and all related resources.</span></span>

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="689fb-113">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="689fb-113">Script explanation</span></span>

<span data-ttu-id="689fb-114">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="689fb-114">This script uses hello following commands.</span></span> <span data-ttu-id="689fb-115">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="689fb-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="689fb-116">命令</span><span class="sxs-lookup"><span data-stu-id="689fb-116">Command</span></span> | <span data-ttu-id="689fb-117">注意事項</span><span class="sxs-lookup"><span data-stu-id="689fb-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="689fb-118">New-AzureRmServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="689fb-118">New-AzureRmServiceFabricCluster</span></span>](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | <span data-ttu-id="689fb-119">建立新的 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="689fb-119">Creates a new Service Fabric cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="689fb-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="689fb-120">Next steps</span></span>

<span data-ttu-id="689fb-121">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="689fb-121">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="689fb-122">適用於 Azure Service Fabric 的其他 Azure Powershell 範例可以在 hello [Azure PowerShell 範例](../service-fabric-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="689fb-122">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
