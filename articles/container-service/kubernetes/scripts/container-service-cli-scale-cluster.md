---
title: "Azure CLI 指令碼範例 - 調整 ACS 叢集 | Microsoft Docs"
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
ms.openlocfilehash: 14e9f9d85bc0c1428240f15831632eafe2a0f80e
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="9e97e-104">調整 Azure Container Service 叢集</span><span class="sxs-lookup"><span data-stu-id="9e97e-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="9e97e-105">此範例會調整 Azure Container Service。</span><span class="sxs-lookup"><span data-stu-id="9e97e-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9e97e-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="9e97e-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="9e97e-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="9e97e-107">Clean up deployment</span></span> 

<span data-ttu-id="9e97e-108">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="9e97e-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9e97e-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="9e97e-109">Script explanation</span></span>

<span data-ttu-id="9e97e-110">此指令碼會使用下列命令來建立部署。</span><span class="sxs-lookup"><span data-stu-id="9e97e-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="9e97e-111">下表中的每個項目都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="9e97e-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9e97e-112">命令</span><span class="sxs-lookup"><span data-stu-id="9e97e-112">Command</span></span> | <span data-ttu-id="9e97e-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="9e97e-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9e97e-114">az acs scale</span><span class="sxs-lookup"><span data-stu-id="9e97e-114">az acs scale</span></span>](/cli/azure/acs#scale) | <span data-ttu-id="9e97e-115">調整 ACS 叢集的規模。</span><span class="sxs-lookup"><span data-stu-id="9e97e-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9e97e-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9e97e-116">Next steps</span></span>

<span data-ttu-id="9e97e-117">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="9e97e-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9e97e-118">您可以在 [Azure Container Service 文件](../cli-samples.md)中找到其他的 Azure Container Service CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="9e97e-118">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>

