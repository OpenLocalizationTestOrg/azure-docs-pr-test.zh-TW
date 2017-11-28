---
title: "Azure Cosmos DB 的索引鍵 aaaAzure CLI 指令碼取得帳戶 |Microsoft 文件"
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
ms.openlocfilehash: d6462b3eebc8bc6935a6fa07dcae37a33e5f382e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-account-keys-for-azure-cosmos-db-using-hello-azure-cli"></a><span data-ttu-id="cb90d-103">取得使用 Azure CLI hello Azure Cosmos DB 中的帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="cb90d-103">Get account keys for Azure Cosmos DB using hello Azure CLI</span></span>

<span data-ttu-id="cb90d-104">這個範例會取得任何一種 Azure Cosmos DB 帳戶的帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="cb90d-104">This sample gets account keys for any kind of Azure Cosmos DB account.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="cb90d-105">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="cb90d-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="cb90d-106">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="cb90d-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="cb90d-107">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="cb90d-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="cb90d-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="cb90d-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-get-account-key/secure-cosmosdb-get-account-key.sh?highlight=22-25 "Get Azure Cosmos DB account keys")]

## <a name="clean-up-deployment"></a><span data-ttu-id="cb90d-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="cb90d-109">Clean up deployment</span></span>

<span data-ttu-id="cb90d-110">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="cb90d-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="cb90d-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="cb90d-111">Script explanation</span></span>

<span data-ttu-id="cb90d-112">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="cb90d-112">This script uses hello following commands.</span></span> <span data-ttu-id="cb90d-113">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="cb90d-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="cb90d-114">命令</span><span class="sxs-lookup"><span data-stu-id="cb90d-114">Command</span></span> | <span data-ttu-id="cb90d-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="cb90d-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cb90d-116">az group create</span><span class="sxs-lookup"><span data-stu-id="cb90d-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="cb90d-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="cb90d-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cb90d-118">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="cb90d-118">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="cb90d-119">更新 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cb90d-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="cb90d-120">az cosmosdb list-keys</span><span class="sxs-lookup"><span data-stu-id="cb90d-120">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="cb90d-121">建立主機 hello SQL Database 邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="cb90d-121">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="cb90d-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="cb90d-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="cb90d-123">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="cb90d-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cb90d-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cb90d-124">Next steps</span></span>

<span data-ttu-id="cb90d-125">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="cb90d-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="cb90d-126">其他 Azure Cosmos DB CLI 指令碼範例可以在 hello [Azure Cosmos DB CLI 文件](../cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="cb90d-126">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
