---
title: "CLI 指令碼範例-aaaAzure 調整為 ACS 叢集 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 調整 ACS 叢集"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 容器, 微服務, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: nepeters
ms.openlocfilehash: 1e07518fc2ca67476d9ef64bb22d75f848a37e43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="59613-104">調整 Azure Container Service 叢集</span><span class="sxs-lookup"><span data-stu-id="59613-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="59613-105">此範例會調整 Azure Container Service。</span><span class="sxs-lookup"><span data-stu-id="59613-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="59613-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="59613-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="59613-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="59613-107">Clean up deployment</span></span> 

<span data-ttu-id="59613-108">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="59613-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="59613-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="59613-109">Script explanation</span></span>

<span data-ttu-id="59613-110">此指令碼會使用下列命令 toocreate hello 部署的 hello。</span><span class="sxs-lookup"><span data-stu-id="59613-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="59613-111">Hello 資料表中的每個項目連結 toocommand 特定文件。</span><span class="sxs-lookup"><span data-stu-id="59613-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="59613-112">命令</span><span class="sxs-lookup"><span data-stu-id="59613-112">Command</span></span> | <span data-ttu-id="59613-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="59613-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="59613-114">az acs scale</span><span class="sxs-lookup"><span data-stu-id="59613-114">az acs scale</span></span>](/cli/azure/acs#scale) | <span data-ttu-id="59613-115">調整 ACS 叢集的規模。</span><span class="sxs-lookup"><span data-stu-id="59613-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="59613-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="59613-116">Next steps</span></span>

<span data-ttu-id="59613-117">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="59613-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="59613-118">其他 Azure 容器服務 CLI 指令碼範例可以在 hello [Azure 容器服務文件](../cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="59613-118">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>

