---
title: "aaaAzure CLI 指令碼範例-建立 ACS DC/OS 叢集 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 建立 ACS DC/OS 叢集"
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
ms.openlocfilehash: 35213fd615b2145642add908dfc48516c33ff332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="92100-104">建立 Azure Container Service DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="92100-104">Create an Azure Container Service DC/OS Cluster</span></span>

<span data-ttu-id="92100-105">這個範例會建立執行 DCOS 的 Azure Container Service 叢集。</span><span class="sxs-lookup"><span data-stu-id="92100-105">This sample creates an Azure Container Service cluster running DCOS.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="92100-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="92100-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="92100-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="92100-107">Clean up deployment</span></span> 

<span data-ttu-id="92100-108">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="92100-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="92100-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="92100-109">Script explanation</span></span>

<span data-ttu-id="92100-110">此指令碼會使用下列命令 toocreate hello 部署的 hello。</span><span class="sxs-lookup"><span data-stu-id="92100-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="92100-111">Hello 資料表中的每個項目連結 toocommand 特定文件。</span><span class="sxs-lookup"><span data-stu-id="92100-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="92100-112">命令</span><span class="sxs-lookup"><span data-stu-id="92100-112">Command</span></span> | <span data-ttu-id="92100-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="92100-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="92100-114">az group create</span><span class="sxs-lookup"><span data-stu-id="92100-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="92100-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="92100-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="92100-116">az acs create</span><span class="sxs-lookup"><span data-stu-id="92100-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="92100-117">建立 ACS 叢集。</span><span class="sxs-lookup"><span data-stu-id="92100-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="92100-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="92100-118">Next steps</span></span>

<span data-ttu-id="92100-119">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="92100-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="92100-120">其他 Azure 容器服務 CLI 指令碼範例可以在 hello [Azure 容器服務文件](../cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="92100-120">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>
