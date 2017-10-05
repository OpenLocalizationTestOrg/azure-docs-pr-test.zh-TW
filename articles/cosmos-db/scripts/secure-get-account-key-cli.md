---
title: "Azure CLI 指令碼 - 取得 Azure Cosmos DB 的帳戶金鑰 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 取得 Azure Cosmos DB 的帳戶金鑰"
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
ms.openlocfilehash: 3df211cdc8878033c8b792da00cce9773ae57a36
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="get-account-keys-for-azure-cosmos-db-using-the-azure-cli"></a><span data-ttu-id="74f78-103">使用 Azure CLI 取得 Azure Cosmos DB 的帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="74f78-103">Get account keys for Azure Cosmos DB using the Azure CLI</span></span>

<span data-ttu-id="74f78-104">這個範例會取得任何一種 Azure Cosmos DB 帳戶的帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="74f78-104">This sample gets account keys for any kind of Azure Cosmos DB account.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="74f78-105">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="74f78-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="74f78-106">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="74f78-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="74f78-107">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="74f78-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="74f78-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="74f78-108">Sample script</span></span>

<span data-ttu-id="74f78-109">[!code-azurecli-interactive[主要](../../../cli_scripts/cosmosdb/scale-cosmosdb-get-account-key/secure-cosmosdb-get-account-key.sh?highlight=22-25 "取得 Azure Cosmos DB 帳戶金鑰")]</span><span class="sxs-lookup"><span data-stu-id="74f78-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-get-account-key/secure-cosmosdb-get-account-key.sh?highlight=22-25 "Get Azure Cosmos DB account keys")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="74f78-110">清除部署</span><span class="sxs-lookup"><span data-stu-id="74f78-110">Clean up deployment</span></span>

<span data-ttu-id="74f78-111">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="74f78-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="74f78-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="74f78-112">Script explanation</span></span>

<span data-ttu-id="74f78-113">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="74f78-113">This script uses the following commands.</span></span> <span data-ttu-id="74f78-114">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="74f78-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="74f78-115">命令</span><span class="sxs-lookup"><span data-stu-id="74f78-115">Command</span></span> | <span data-ttu-id="74f78-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="74f78-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="74f78-117">az group create</span><span class="sxs-lookup"><span data-stu-id="74f78-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="74f78-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="74f78-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="74f78-119">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="74f78-119">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="74f78-120">更新 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="74f78-120">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="74f78-121">az cosmosdb list-keys</span><span class="sxs-lookup"><span data-stu-id="74f78-121">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="74f78-122">建立主控 SQL Database 的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="74f78-122">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="74f78-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="74f78-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="74f78-124">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="74f78-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="74f78-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="74f78-125">Next steps</span></span>

<span data-ttu-id="74f78-126">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="74f78-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="74f78-127">您可以在 [Azure Cosmos DB CLI 文件](../cli-samples.md)中找到其他 Azure Cosmos DB CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="74f78-127">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
