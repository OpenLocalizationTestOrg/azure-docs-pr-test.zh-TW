---
title: "aaaCLI 範例移動 Azure SQL database-SQL 彈性集區 |Microsoft 文件"
description: "Azure CLI 範例指令碼 toomove SQL 彈性集區中的 SQL 資料庫"
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
ms.date: 07/05/2017
ms.author: janeng
ms.openlocfilehash: 841eb57d2d49612c3fadd3a6424a2b0309c69719
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomove-an-azure-sql-database-in-a-sql-elastic-pool"></a><span data-ttu-id="74398-103">SQL 彈性集區中使用 CLI toomove Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="74398-103">Use CLI toomove an Azure SQL database in a SQL elastic pool</span></span>

<span data-ttu-id="74398-104">此 Azure CLI 指令碼範例會建立兩個彈性集區和從一個 SQL 彈性集區的 Azure SQL database 移到另一個 SQL 彈性集區，並且再移動 hello 資料庫超出彈性集區 tooa 單一 Azure 資料庫效能層級。</span><span class="sxs-lookup"><span data-stu-id="74398-104">This Azure CLI script example creates two elastic pools and moves an Azure SQL database from one SQL elastic pool into another SQL elastic pool, and then moves hello database out of elastic pool tooa single Azure database performance level.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="74398-105">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="74398-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="74398-106">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="74398-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="74398-107">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="74398-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="74398-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="74398-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="74398-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="74398-109">Clean up deployment</span></span>

<span data-ttu-id="74398-110">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="74398-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="74398-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="74398-111">Script explanation</span></span>

<span data-ttu-id="74398-112">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="74398-112">This script uses hello following commands.</span></span> <span data-ttu-id="74398-113">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="74398-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="74398-114">命令</span><span class="sxs-lookup"><span data-stu-id="74398-114">Command</span></span> | <span data-ttu-id="74398-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="74398-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="74398-116">az group create</span><span class="sxs-lookup"><span data-stu-id="74398-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="74398-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="74398-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="74398-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="74398-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="74398-119">建立主機資料庫或彈性集區的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="74398-119">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="74398-120">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="74398-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="74398-121">建立 hello 邏輯伺服器內的彈性集區。</span><span class="sxs-lookup"><span data-stu-id="74398-121">Creates an elastic pool within hello logical server.</span></span> |
| [<span data-ttu-id="74398-122">az sql db create</span><span class="sxs-lookup"><span data-stu-id="74398-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="74398-123">在邏輯伺服器中將資料庫建立為單一或集區的資料庫。</span><span class="sxs-lookup"><span data-stu-id="74398-123">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="74398-124">az sql db update</span><span class="sxs-lookup"><span data-stu-id="74398-124">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="74398-125">更新資料庫屬性，或將資料庫移入、移出彈性集區或在彈性集區之間移動資料庫。</span><span class="sxs-lookup"><span data-stu-id="74398-125">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="74398-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="74398-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="74398-127">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="74398-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="74398-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="74398-128">Next steps</span></span>

<span data-ttu-id="74398-129">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="74398-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="74398-130">其他的 SQL 資料庫 CLI 指令碼範例可以在 hello [Azure SQL Database 文件](../sql-database-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="74398-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>


