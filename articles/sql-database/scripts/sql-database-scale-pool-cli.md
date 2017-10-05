---
title: "CLI 範例 - 調整 SQL 彈性集區 - Azure SQL Database | Microsoft Docs"
description: "在 Azure SQL Database 中調整 SQL 彈性集區的 Azure CLI 範例指令碼"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 888d2b7b7c118fede82d39881570a3b3d7b09961
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="use-cli-to-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="6eff9-103">使用 CLI 在 Azure SQL Database 中調整 SQL 彈性集區</span><span class="sxs-lookup"><span data-stu-id="6eff9-103">Use CLI to scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="6eff9-104">此 Azure CLI 指令碼範例會建立 SQL 彈性集區、移動集區資料庫，以及變更彈性集區的效能等級。</span><span class="sxs-lookup"><span data-stu-id="6eff9-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6eff9-105">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6eff9-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6eff9-106">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="6eff9-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="6eff9-107">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="6eff9-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6eff9-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="6eff9-108">Sample script</span></span>

<span data-ttu-id="6eff9-109">[!code-azurecli-interactive[主要](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "在集區之間移動資料庫")]</span><span class="sxs-lookup"><span data-stu-id="6eff9-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6eff9-110">清除部署</span><span class="sxs-lookup"><span data-stu-id="6eff9-110">Clean up deployment</span></span>

<span data-ttu-id="6eff9-111">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="6eff9-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6eff9-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="6eff9-112">Script explanation</span></span>

<span data-ttu-id="6eff9-113">此指令碼使用下列命令來建立資源群組、邏輯伺服器、SQL Database 和防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="6eff9-113">This script uses the following commands to create a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="6eff9-114">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="6eff9-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6eff9-115">命令</span><span class="sxs-lookup"><span data-stu-id="6eff9-115">Command</span></span> | <span data-ttu-id="6eff9-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="6eff9-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6eff9-117">az group create</span><span class="sxs-lookup"><span data-stu-id="6eff9-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6eff9-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6eff9-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6eff9-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="6eff9-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="6eff9-120">建立主控 SQL Database 的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="6eff9-120">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="6eff9-121">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="6eff9-121">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="6eff9-122">在邏輯伺服器內建立彈性資料庫集區。</span><span class="sxs-lookup"><span data-stu-id="6eff9-122">Creates an elastic database pool within the logical server.</span></span> |
| [<span data-ttu-id="6eff9-123">az sql db create</span><span class="sxs-lookup"><span data-stu-id="6eff9-123">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="6eff9-124">在邏輯伺服器中建立 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="6eff9-124">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="6eff9-125">az sql elastic-pools update</span><span class="sxs-lookup"><span data-stu-id="6eff9-125">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="6eff9-126">更新彈性資料庫集區，在此範例中是變更指派的 eDTU。</span><span class="sxs-lookup"><span data-stu-id="6eff9-126">Updates an elastic database pool, in this example changes the assigned eDTU.</span></span> |
| [<span data-ttu-id="6eff9-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="6eff9-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="6eff9-128">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="6eff9-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6eff9-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6eff9-129">Next steps</span></span>

<span data-ttu-id="6eff9-130">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="6eff9-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6eff9-131">其他的 SQL Database CLI 指令碼範例可於 [Azure SQL Database 文件](../sql-database-cli-samples.md)中找到。</span><span class="sxs-lookup"><span data-stu-id="6eff9-131">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
