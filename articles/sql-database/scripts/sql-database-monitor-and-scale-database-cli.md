---
title: "CLI 範例 - 監視 - 調整 - 單一 SQL Database | Microsoft Docs"
description: "監視和調整單一 Azure SQL Database 的 Azure CLI 範例指令碼"
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
ms.openlocfilehash: 01911b85268244a8fddb32aa726f8a870abbaf77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-monitor-and-scale-a-single-sql-database"></a><span data-ttu-id="8209f-103">使用 CLI 監視和調整單一 SQL Database</span><span class="sxs-lookup"><span data-stu-id="8209f-103">Use CLI to monitor and scale a single SQL database</span></span>

<span data-ttu-id="8209f-104">此 Azure CLI 指令碼範例會在查詢單一 Azure SQL Database 的大小資訊後，將其調整為不同的效能等級。</span><span class="sxs-lookup"><span data-stu-id="8209f-104">This Azure CLI script example scales a single Azure SQL database to a different performance level after querying the size information of the database.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8209f-105">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8209f-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8209f-106">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="8209f-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="8209f-107">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="8209f-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="8209f-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="8209f-108">Sample script</span></span>

<span data-ttu-id="8209f-109">[!code-azurecli-interactive[主要](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "監視和調整單一 SQL Database")]</span><span class="sxs-lookup"><span data-stu-id="8209f-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="8209f-110">清除部署</span><span class="sxs-lookup"><span data-stu-id="8209f-110">Clean up deployment</span></span>

<span data-ttu-id="8209f-111">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="8209f-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="8209f-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="8209f-112">Script explanation</span></span>

<span data-ttu-id="8209f-113">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="8209f-113">This script uses the following commands.</span></span> <span data-ttu-id="8209f-114">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="8209f-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8209f-115">命令</span><span class="sxs-lookup"><span data-stu-id="8209f-115">Command</span></span> | <span data-ttu-id="8209f-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="8209f-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8209f-117">az group create</span><span class="sxs-lookup"><span data-stu-id="8209f-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8209f-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8209f-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8209f-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="8209f-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="8209f-120">建立主機資料庫的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="8209f-120">Creates a logical server that hosts a database.</span></span> |
| [<span data-ttu-id="8209f-121">az sql db show-usage</span><span class="sxs-lookup"><span data-stu-id="8209f-121">az sql db show-usage</span></span>](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | <span data-ttu-id="8209f-122">顯示資料庫的大小使用量資訊。</span><span class="sxs-lookup"><span data-stu-id="8209f-122">Shows the size usage information for a database.</span></span> |
| [<span data-ttu-id="8209f-123">az sql db update</span><span class="sxs-lookup"><span data-stu-id="8209f-123">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="8209f-124">更新資料庫屬性 (例如服務層或效能等級)，或將資料庫移入、移出彈性集區或在彈性集區之間移動資料庫。</span><span class="sxs-lookup"><span data-stu-id="8209f-124">Updates database properties (such as the service tier or performance level) or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="8209f-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="8209f-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="8209f-126">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="8209f-126">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="8209f-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8209f-127">Next steps</span></span>

<span data-ttu-id="8209f-128">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="8209f-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8209f-129">其他的 SQL Database CLI 指令碼範例可於 [Azure SQL Database 文件](../sql-database-cli-samples.md)中找到。</span><span class="sxs-lookup"><span data-stu-id="8209f-129">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
