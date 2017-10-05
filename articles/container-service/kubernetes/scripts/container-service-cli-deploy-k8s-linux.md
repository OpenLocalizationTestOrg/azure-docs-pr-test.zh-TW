---
title: "Azure CLI 指令碼範例 - 建立 ACS Linux Kubernetes 叢集 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 建立 ACS Linux Kubernetes 叢集"
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
ms.openlocfilehash: c6a392217f84f549f2cae3c68fed85b9f888db77
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="create-an-azure-container-service-kubernetes-linux-cluster"></a><span data-ttu-id="103e7-104">建立 Azure Container Service Kubernetes Linux 叢集</span><span class="sxs-lookup"><span data-stu-id="103e7-104">Create an Azure Container Service Kubernetes Linux Cluster</span></span>

<span data-ttu-id="103e7-105">這個範例會針對以 Linux 為基礎的容器建立執行 Kubernetes 的 Azure Container Service 叢集。</span><span class="sxs-lookup"><span data-stu-id="103e7-105">This sample creates an Azure Container Service cluster running Kubernetes for Linux based containers.</span></span>

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="103e7-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="103e7-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type kubernetes \
  --resource-group myResourceGroup \
  --name myK8SCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="103e7-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="103e7-107">Clean up deployment</span></span> 

<span data-ttu-id="103e7-108">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="103e7-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="103e7-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="103e7-109">Script explanation</span></span>

<span data-ttu-id="103e7-110">此指令碼會使用下列命令來建立部署。</span><span class="sxs-lookup"><span data-stu-id="103e7-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="103e7-111">下表中的每個項目都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="103e7-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="103e7-112">命令</span><span class="sxs-lookup"><span data-stu-id="103e7-112">Command</span></span> | <span data-ttu-id="103e7-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="103e7-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="103e7-114">az group create</span><span class="sxs-lookup"><span data-stu-id="103e7-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="103e7-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="103e7-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="103e7-116">az acs create</span><span class="sxs-lookup"><span data-stu-id="103e7-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="103e7-117">建立 ACS 叢集。</span><span class="sxs-lookup"><span data-stu-id="103e7-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="103e7-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="103e7-118">Next steps</span></span>

<span data-ttu-id="103e7-119">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="103e7-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="103e7-120">您可以在 [Azure Container Service 文件](../cli-samples.md)中找到其他的 Azure Container Service CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="103e7-120">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>

