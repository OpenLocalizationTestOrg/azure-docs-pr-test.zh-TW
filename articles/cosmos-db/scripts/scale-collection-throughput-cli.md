---
title: "Azure CLI 指令碼 - 調整 Azure Cosmos DB 容器輸送量 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 調整 Azure Cosmos DB 容器輸送量"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: f08733cd4074c7144b20a0592522423e729e6f1d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="scale-azure-cosmos-db-container-throughput-using-the-azure-cli"></a><span data-ttu-id="6d77b-103">使用 Azure CLI 調整 Azure Cosmos DB 容器輸送量</span><span class="sxs-lookup"><span data-stu-id="6d77b-103">Scale Azure Cosmos DB container throughput using the Azure CLI</span></span>

<span data-ttu-id="6d77b-104">此範例會調整任何一種 Azure Cosmos DB 容器的容器輸送量。</span><span class="sxs-lookup"><span data-stu-id="6d77b-104">This sample scales container throughput for any kind of Azure Cosmos DB container.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6d77b-105">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6d77b-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6d77b-106">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="6d77b-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="6d77b-107">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="6d77b-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6d77b-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="6d77b-108">Sample script</span></span>

<span data-ttu-id="6d77b-109">[!code-azurecli-interactive[主要](../../../cli_scripts/cosmosdb/scale-cosmosdb-throughput/scale-cosmosdb-throughput.sh?highlight=40-46 "調整 Azure Cosmos DB 輸送量")]</span><span class="sxs-lookup"><span data-stu-id="6d77b-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-throughput/scale-cosmosdb-throughput.sh?highlight=40-46 "Scale Azure Cosmos DB throughput")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6d77b-110">清除部署</span><span class="sxs-lookup"><span data-stu-id="6d77b-110">Clean up deployment</span></span>

<span data-ttu-id="6d77b-111">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="6d77b-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6d77b-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="6d77b-112">Script explanation</span></span>

<span data-ttu-id="6d77b-113">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="6d77b-113">This script uses the following commands.</span></span> <span data-ttu-id="6d77b-114">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="6d77b-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6d77b-115">命令</span><span class="sxs-lookup"><span data-stu-id="6d77b-115">Command</span></span> | <span data-ttu-id="6d77b-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="6d77b-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6d77b-117">az group create</span><span class="sxs-lookup"><span data-stu-id="6d77b-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="6d77b-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6d77b-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6d77b-119">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="6d77b-119">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="6d77b-120">更新 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d77b-120">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="6d77b-121">az group delete</span><span class="sxs-lookup"><span data-stu-id="6d77b-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="6d77b-122">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="6d77b-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6d77b-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6d77b-123">Next steps</span></span>

<span data-ttu-id="6d77b-124">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="6d77b-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6d77b-125">您可以在 [Azure Cosmos DB CLI 文件](../cli-samples.md)中找到其他 Azure Cosmos DB CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="6d77b-125">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
