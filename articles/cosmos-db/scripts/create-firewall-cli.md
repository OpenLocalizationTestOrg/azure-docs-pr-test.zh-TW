---
title: "CLI 指令碼建立的 Azure Cosmos DB 防火牆 aaaAzure |Microsoft 文件"
description: "Azure CLI 指令碼範例：建立 Azure Cosmos DB 的防火牆"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: sammvcple
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: d4bee4f37906033c96826b9662d2ba396325c792
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-firewall-using-hello-azure-cli"></a><span data-ttu-id="476f0-103">Azure Cosmos DB： 建立使用 Azure CLI hello 的防火牆</span><span class="sxs-lookup"><span data-stu-id="476f0-103">Azure Cosmos DB: Create a firewall using hello Azure CLI</span></span>

<span data-ttu-id="476f0-104">這個範例 CLI 指令碼會建立適用於任何種類 Azure Cosmos DB 帳戶的防火牆原則。</span><span class="sxs-lookup"><span data-stu-id="476f0-104">This sample CLI script creates a firewall policy for any kind of Azure Cosmos DB account.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="476f0-105">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="476f0-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="476f0-106">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="476f0-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="476f0-107">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="476f0-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="476f0-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="476f0-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-create-firewall/secure-cosmosdb-create-firewall.sh?highlight=38-42 "Create an Azure Cosmos DB firewall")]

## <a name="clean-up-deployment"></a><span data-ttu-id="476f0-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="476f0-109">Clean up deployment</span></span>

<span data-ttu-id="476f0-110">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="476f0-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="476f0-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="476f0-111">Script explanation</span></span>

<span data-ttu-id="476f0-112">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="476f0-112">This script uses hello following commands.</span></span> <span data-ttu-id="476f0-113">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="476f0-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="476f0-114">命令</span><span class="sxs-lookup"><span data-stu-id="476f0-114">Command</span></span> | <span data-ttu-id="476f0-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="476f0-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="476f0-116">az group create</span><span class="sxs-lookup"><span data-stu-id="476f0-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="476f0-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="476f0-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="476f0-118">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="476f0-118">az cosmosdb create</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#create) | <span data-ttu-id="476f0-119">建立 Azure CosmosDB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="476f0-119">Creates an Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="476f0-120">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="476f0-120">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="476f0-121">更新 Azure CosmosDB 帳戶 tooinclude 防火牆設定。</span><span class="sxs-lookup"><span data-stu-id="476f0-121">Updates an Azure CosmosDB account tooinclude firewall settings.</span></span> |
| [<span data-ttu-id="476f0-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="476f0-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="476f0-123">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="476f0-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="476f0-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="476f0-124">Next steps</span></span>

<span data-ttu-id="476f0-125">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="476f0-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="476f0-126">其他 Azure Cosmos DB CLI 指令碼範例可以在 hello [Azure Cosmos DB CLI 文件](../cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="476f0-126">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
