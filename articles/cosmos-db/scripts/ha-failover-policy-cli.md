---
title: "Azure CLI 指令碼 - 建立高可用性的容錯移轉原則 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 建立高可用性的容錯移轉原則"
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
ms.openlocfilehash: 96083d66cc1a2ef179f9313c1b3ed04162c1c048
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-failover-policy-for-high-availability-using-the-azure-cli"></a><span data-ttu-id="0388b-103">使用 Azure CLI 建立高可用性的容錯移轉原則</span><span class="sxs-lookup"><span data-stu-id="0388b-103">Create a failover policy for high availability using the Azure CLI</span></span>

<span data-ttu-id="0388b-104">此範例 CLI 指令碼會建立 Azure Cosmos DB 帳戶，然後將它設定為高可用性。</span><span class="sxs-lookup"><span data-stu-id="0388b-104">This sample CLI script creates an Azure Cosmos DB account, and then configures it for high availability.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0388b-105">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="0388b-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0388b-106">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="0388b-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="0388b-107">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="0388b-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="0388b-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="0388b-108">Sample script</span></span>

<span data-ttu-id="0388b-109">[!code-azurecli-interactive[主要](../../../cli_scripts/cosmosdb/high-availability-cosmosdb-configure-failover/high-availability-cosmosdb-configure-failover.sh?highlight=23-27 "建立 Azure Cosmos DB 容錯移轉原則")]</span><span class="sxs-lookup"><span data-stu-id="0388b-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/high-availability-cosmosdb-configure-failover/high-availability-cosmosdb-configure-failover.sh?highlight=23-27 "Create an Azure Cosmos DB failover policy")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="0388b-110">清除部署</span><span class="sxs-lookup"><span data-stu-id="0388b-110">Clean up deployment</span></span>

<span data-ttu-id="0388b-111">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="0388b-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="0388b-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="0388b-112">Script explanation</span></span>

<span data-ttu-id="0388b-113">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="0388b-113">This script uses the following commands.</span></span> <span data-ttu-id="0388b-114">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="0388b-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0388b-115">命令</span><span class="sxs-lookup"><span data-stu-id="0388b-115">Command</span></span> | <span data-ttu-id="0388b-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="0388b-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0388b-117">az group create</span><span class="sxs-lookup"><span data-stu-id="0388b-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="0388b-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="0388b-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0388b-119">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="0388b-119">az cosmosdb create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="0388b-120">建立 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0388b-120">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="0388b-121">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="0388b-121">az cosmosdb update</span></span>](/cli/azure/cosmosdb#update) | <span data-ttu-id="0388b-122">更新 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0388b-122">Updates Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="0388b-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="0388b-123">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="0388b-124">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="0388b-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0388b-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0388b-125">Next steps</span></span>

<span data-ttu-id="0388b-126">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="0388b-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0388b-127">您可以在 [Azure Cosmos DB CLI 文件](../cli-samples.md)中找到其他 Azure Cosmos DB CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="0388b-127">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
