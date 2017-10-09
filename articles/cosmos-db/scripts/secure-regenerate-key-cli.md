---
title: "aaaAzure CLI 指令碼重新產生 Azure Cosmos DB 帳戶金鑰 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 重新產生 Azure Cosmos DB 帳戶金鑰"
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
ms.openlocfilehash: ca77e05039775c90d7541899eeffc45a76d60657
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="regenerate-an-azure-cosmos-db-account-key-using-hello-azure-cli"></a><span data-ttu-id="e8b5b-103">重新產生使用 Azure CLI hello Azure Cosmos DB 帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="e8b5b-103">Regenerate an Azure Cosmos DB account key using hello Azure CLI</span></span>

<span data-ttu-id="e8b5b-104">這個範例會重新產生的任何一種使用 Azure CLI hello Azure Cosmos DB 帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="e8b5b-104">This sample regenerates any kind of Azure Cosmos DB account key using hello Azure CLI.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e8b5b-105">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="e8b5b-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e8b5b-106">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="e8b5b-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e8b5b-107">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="e8b5b-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e8b5b-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="e8b5b-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-regenerate-keys/secure-cosmosdb-regenerate-keys.sh?highlight=27-31 "Regenerate Azure Cosmos DB account keys")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e8b5b-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="e8b5b-109">Clean up deployment</span></span>

<span data-ttu-id="e8b5b-110">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="e8b5b-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e8b5b-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="e8b5b-111">Script explanation</span></span>

<span data-ttu-id="e8b5b-112">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="e8b5b-112">This script uses hello following commands.</span></span> <span data-ttu-id="e8b5b-113">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="e8b5b-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e8b5b-114">命令</span><span class="sxs-lookup"><span data-stu-id="e8b5b-114">Command</span></span> | <span data-ttu-id="e8b5b-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="e8b5b-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e8b5b-116">az group create</span><span class="sxs-lookup"><span data-stu-id="e8b5b-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="e8b5b-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="e8b5b-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e8b5b-118">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="e8b5b-118">az cosmosdb create</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#create) | <span data-ttu-id="e8b5b-119">更新 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e8b5b-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="e8b5b-120">az cosmosdb regenerate-key</span><span class="sxs-lookup"><span data-stu-id="e8b5b-120">az cosmosdb regenerate-key</span></span>](/cli/azure/cosmosdb/regenerate-key) | <span data-ttu-id="e8b5b-121">重新產生 Azure Cosmos DB 帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="e8b5b-121">Regeneratates Azure Cosmos DB account keys.</span></span> |
| [<span data-ttu-id="e8b5b-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="e8b5b-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="e8b5b-123">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="e8b5b-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e8b5b-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e8b5b-124">Next steps</span></span>

<span data-ttu-id="e8b5b-125">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="e8b5b-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e8b5b-126">其他 Azure Cosmos DB CLI 指令碼範例可以在 hello [Azure Cosmos DB CLI 文件](../cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="e8b5b-126">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
