---
title: "Azure CLI 指令碼 - Azure Cosmos DB 的多區域複寫 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - Azure Cosmos DB 的多區域複寫"
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
ms.openlocfilehash: ab716c28b88412438d0cea80377f9f0f40dc8bd6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-the-azure-cli"></a><span data-ttu-id="21586-103">使用 Azure CLI 複寫多個區域中的 Azure Cosmos DB 資料庫帳戶和設定容錯移轉優先順序</span><span class="sxs-lookup"><span data-stu-id="21586-103">Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using the Azure CLI</span></span>

<span data-ttu-id="21586-104">此範例會使用 Azure CLI 複寫多個區域中的任何一種 Azure Cosmos DB 資料庫帳戶，並設定容錯移轉優先順序。</span><span class="sxs-lookup"><span data-stu-id="21586-104">This sample replicates any kind of Azure Cosmos DB database account in multiple regions and configures failover priorities using the Azure CLI.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="21586-105">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="21586-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="21586-106">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="21586-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="21586-107">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="21586-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="21586-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="21586-108">Sample script</span></span>

<span data-ttu-id="21586-109">[!code-azurecli-interactive[主要](../../../cli_scripts/cosmosdb/scale-cosmosdb-replicate-multiple-regions/scale-cosmosdb-replicate-multiple-regions.sh?highlight=21-31 "將 Azure Cosmos DB 擴展至多個區域")]</span><span class="sxs-lookup"><span data-stu-id="21586-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-replicate-multiple-regions/scale-cosmosdb-replicate-multiple-regions.sh?highlight=21-31 "Scale Azure Cosmos DB into multiple regions")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="21586-110">清除部署</span><span class="sxs-lookup"><span data-stu-id="21586-110">Clean up deployment</span></span>

<span data-ttu-id="21586-111">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="21586-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="21586-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="21586-112">Script explanation</span></span>

<span data-ttu-id="21586-113">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="21586-113">This script uses the following commands.</span></span> <span data-ttu-id="21586-114">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="21586-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="21586-115">命令</span><span class="sxs-lookup"><span data-stu-id="21586-115">Command</span></span> | <span data-ttu-id="21586-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="21586-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="21586-117">az group create</span><span class="sxs-lookup"><span data-stu-id="21586-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="21586-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="21586-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="21586-119">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="21586-119">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="21586-120">更新 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="21586-120">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="21586-121">az group delete</span><span class="sxs-lookup"><span data-stu-id="21586-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="21586-122">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="21586-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="21586-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="21586-123">Next steps</span></span>

<span data-ttu-id="21586-124">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="21586-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="21586-125">您可以在 [Azure Cosmos DB CLI 文件](../cli-samples.md)中找到其他 Azure Cosmos DB CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="21586-125">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
