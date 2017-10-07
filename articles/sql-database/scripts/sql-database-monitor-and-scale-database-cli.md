---
title: "aaaCLI 範例監視器位小數位數單一 Azure SQL 資料庫 |Microsoft 文件"
description: "Azure CLI 範例指令碼 toomonitor 和小數位數單一 Azure SQL 資料庫"
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
ms.openlocfilehash: 36031ddd46a947a80fe37884858a84eb66217270
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomonitor-and-scale-a-single-sql-database"></a><span data-ttu-id="a2d9d-103">使用 CLI toomonitor 並縮放單一的 SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="a2d9d-103">Use CLI toomonitor and scale a single SQL database</span></span>

<span data-ttu-id="a2d9d-104">此 Azure CLI 指令碼範例會調整單一 Azure SQL database tooa 不同的效能層級之後查詢 hello hello 資料庫大小資訊。</span><span class="sxs-lookup"><span data-stu-id="a2d9d-104">This Azure CLI script example scales a single Azure SQL database tooa different performance level after querying hello size information of hello database.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a2d9d-105">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a2d9d-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a2d9d-106">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="a2d9d-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a2d9d-107">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="a2d9d-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a2d9d-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="a2d9d-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a2d9d-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="a2d9d-109">Clean up deployment</span></span>

<span data-ttu-id="a2d9d-110">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="a2d9d-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="a2d9d-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="a2d9d-111">Script explanation</span></span>

<span data-ttu-id="a2d9d-112">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="a2d9d-112">This script uses hello following commands.</span></span> <span data-ttu-id="a2d9d-113">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="a2d9d-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a2d9d-114">命令</span><span class="sxs-lookup"><span data-stu-id="a2d9d-114">Command</span></span> | <span data-ttu-id="a2d9d-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="a2d9d-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a2d9d-116">az group create</span><span class="sxs-lookup"><span data-stu-id="a2d9d-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a2d9d-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a2d9d-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a2d9d-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="a2d9d-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="a2d9d-119">建立主機資料庫的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="a2d9d-119">Creates a logical server that hosts a database.</span></span> |
| [<span data-ttu-id="a2d9d-120">az sql db show-usage</span><span class="sxs-lookup"><span data-stu-id="a2d9d-120">az sql db show-usage</span></span>](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | <span data-ttu-id="a2d9d-121">顯示資料庫的 hello 大小使用量資訊。</span><span class="sxs-lookup"><span data-stu-id="a2d9d-121">Shows hello size usage information for a database.</span></span> |
| [<span data-ttu-id="a2d9d-122">az sql db update</span><span class="sxs-lookup"><span data-stu-id="a2d9d-122">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="a2d9d-123">更新資料庫屬性 （例如 hello 服務層或效能層級），或將資料庫移入、 登出或彈性集區之間。</span><span class="sxs-lookup"><span data-stu-id="a2d9d-123">Updates database properties (such as hello service tier or performance level) or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="a2d9d-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="a2d9d-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="a2d9d-125">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="a2d9d-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="a2d9d-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a2d9d-126">Next steps</span></span>

<span data-ttu-id="a2d9d-127">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="a2d9d-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a2d9d-128">其他的 SQL 資料庫 CLI 指令碼範例可以在 hello [Azure SQL Database 文件](../sql-database-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="a2d9d-128">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
