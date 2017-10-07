---
title: "aaaAzure CLI 指令碼標尺 Azure Cosmos DB 容器輸送量 |Microsoft 文件"
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
ms.openlocfilehash: b1a60feaf43f555a9f6ba20e5e0617f73521c0a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-cosmos-db-container-throughput-using-hello-azure-cli"></a><span data-ttu-id="b3c02-103">使用 Azure CLI hello 向 Azure Cosmos DB 容器輸送量</span><span class="sxs-lookup"><span data-stu-id="b3c02-103">Scale Azure Cosmos DB container throughput using hello Azure CLI</span></span>

<span data-ttu-id="b3c02-104">此範例會調整任何一種 Azure Cosmos DB 容器的容器輸送量。</span><span class="sxs-lookup"><span data-stu-id="b3c02-104">This sample scales container throughput for any kind of Azure Cosmos DB container.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b3c02-105">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b3c02-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b3c02-106">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="b3c02-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b3c02-107">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="b3c02-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b3c02-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="b3c02-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-throughput/scale-cosmosdb-throughput.sh?highlight=40-46 "Scale Azure Cosmos DB throughput")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b3c02-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="b3c02-109">Clean up deployment</span></span>

<span data-ttu-id="b3c02-110">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="b3c02-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b3c02-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="b3c02-111">Script explanation</span></span>

<span data-ttu-id="b3c02-112">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="b3c02-112">This script uses hello following commands.</span></span> <span data-ttu-id="b3c02-113">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="b3c02-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b3c02-114">命令</span><span class="sxs-lookup"><span data-stu-id="b3c02-114">Command</span></span> | <span data-ttu-id="b3c02-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="b3c02-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b3c02-116">az group create</span><span class="sxs-lookup"><span data-stu-id="b3c02-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="b3c02-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b3c02-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b3c02-118">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="b3c02-118">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="b3c02-119">更新 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3c02-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="b3c02-120">az group delete</span><span class="sxs-lookup"><span data-stu-id="b3c02-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="b3c02-121">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="b3c02-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b3c02-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b3c02-122">Next steps</span></span>

<span data-ttu-id="b3c02-123">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="b3c02-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b3c02-124">其他 Azure Cosmos DB CLI 指令碼範例可以在 hello [Azure Cosmos DB CLI 文件](../cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="b3c02-124">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
