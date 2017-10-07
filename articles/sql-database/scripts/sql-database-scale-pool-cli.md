---
title: "aaaCLI 範例調整 SQL 彈性集區-Azure SQL 資料庫 |Microsoft 文件"
description: "Azure CLI 範例指令碼 tooscale Azure SQL Database 中的 SQL 彈性集區"
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
ms.openlocfilehash: 436128b8183213f78b9abc2ec46efe2a3ed3c37c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-tooscale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="ef60f-103">使用 CLI tooscale Azure SQL Database 中的 SQL 彈性集區</span><span class="sxs-lookup"><span data-stu-id="ef60f-103">Use CLI tooscale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="ef60f-104">此 Azure CLI 指令碼範例會建立 SQL 彈性集區、移動集區資料庫，以及變更彈性集區的效能等級。</span><span class="sxs-lookup"><span data-stu-id="ef60f-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ef60f-105">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ef60f-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ef60f-106">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="ef60f-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ef60f-107">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="ef60f-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ef60f-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="ef60f-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ef60f-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="ef60f-109">Clean up deployment</span></span>

<span data-ttu-id="ef60f-110">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="ef60f-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ef60f-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="ef60f-111">Script explanation</span></span>

<span data-ttu-id="ef60f-112">此指令碼會使用下列命令 toocreate 資源群組中，邏輯伺服器，SQL Database 和防火牆規則的 hello。</span><span class="sxs-lookup"><span data-stu-id="ef60f-112">This script uses hello following commands toocreate a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="ef60f-113">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="ef60f-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ef60f-114">命令</span><span class="sxs-lookup"><span data-stu-id="ef60f-114">Command</span></span> | <span data-ttu-id="ef60f-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="ef60f-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ef60f-116">az group create</span><span class="sxs-lookup"><span data-stu-id="ef60f-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ef60f-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ef60f-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ef60f-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="ef60f-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="ef60f-119">建立主機 hello SQL Database 邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="ef60f-119">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="ef60f-120">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="ef60f-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="ef60f-121">建立 hello 邏輯伺服器內的彈性資料庫集區。</span><span class="sxs-lookup"><span data-stu-id="ef60f-121">Creates an elastic database pool within hello logical server.</span></span> |
| [<span data-ttu-id="ef60f-122">az sql db create</span><span class="sxs-lookup"><span data-stu-id="ef60f-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="ef60f-123">建立 hello 邏輯伺服器中的 hello SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ef60f-123">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="ef60f-124">az sql elastic-pools update</span><span class="sxs-lookup"><span data-stu-id="ef60f-124">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="ef60f-125">更新的彈性資料庫集區，在此範例變更 hello 分派 eDTU。</span><span class="sxs-lookup"><span data-stu-id="ef60f-125">Updates an elastic database pool, in this example changes hello assigned eDTU.</span></span> |
| [<span data-ttu-id="ef60f-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="ef60f-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="ef60f-127">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="ef60f-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ef60f-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ef60f-128">Next steps</span></span>

<span data-ttu-id="ef60f-129">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="ef60f-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ef60f-130">其他的 SQL 資料庫 CLI 指令碼範例可以在 hello [Azure SQL Database 文件](../sql-database-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="ef60f-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
