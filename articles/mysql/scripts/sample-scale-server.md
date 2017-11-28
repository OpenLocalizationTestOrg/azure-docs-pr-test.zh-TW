---
title: "aaaAzure CLI 範例 tooscale Azure 資料庫的 MySQL 伺服器 |Microsoft 文件"
description: "這個範例 CLI 指令碼會縮放 Azure 資料庫的 MySQL server tooa 不同效能層級之後查詢 hello 度量。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: sample
ms.custom: mvc
ms.date: 05/31/2017
ms.openlocfilehash: 721ef9db35a5f3be7a38438c1abb724187b18b75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="78321-103">使用 Azure CLI 監視和調整適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="78321-103">Monitor and scale an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="78321-104">這個範例 CLI 指令碼之後查詢 hello 度量縮放單一 Azure 資料庫的 MySQL server tooa 不同效能層級。</span><span class="sxs-lookup"><span data-stu-id="78321-104">This sample CLI script scales a single Azure Database for MySQL server tooa different performance level after querying hello metrics.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="78321-105">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="78321-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="78321-106">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="78321-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="78321-107">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="78321-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="78321-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="78321-108">Sample script</span></span>
<span data-ttu-id="78321-109">在這個範例指令碼中，變更反白顯示 hello 行 toocustomize hello 管理員使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="78321-109">In this sample script, change hello highlighted lines toocustomize hello admin username and password.</span></span> <span data-ttu-id="78321-110">取代您自己的訂用帳戶 id 與 hello az 監視器命令中使用的 hello 訂用帳戶 id。[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span><span class="sxs-lookup"><span data-stu-id="78321-110">Replace hello subscription id used in hello az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="78321-111">清除部署</span><span class="sxs-lookup"><span data-stu-id="78321-111">Clean up deployment</span></span>
<span data-ttu-id="78321-112">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="78321-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="78321-113">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="78321-113">Script explanation</span></span>
<span data-ttu-id="78321-114">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="78321-114">This script uses hello following commands.</span></span> <span data-ttu-id="78321-115">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="78321-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="78321-116">**命令**</span><span class="sxs-lookup"><span data-stu-id="78321-116">**Command**</span></span> | <span data-ttu-id="78321-117">**注意事項**</span><span class="sxs-lookup"><span data-stu-id="78321-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="78321-118">az group create</span><span class="sxs-lookup"><span data-stu-id="78321-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="78321-119">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="78321-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="78321-120">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="78321-120">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="78321-121">建立裝載 hello 資料庫的 MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="78321-121">Creates a MySQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="78321-122">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="78321-122">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="78321-123">列出 hello 資源 hello 公制值。</span><span class="sxs-lookup"><span data-stu-id="78321-123">List hello metric value for hello resources.</span></span> |
| [<span data-ttu-id="78321-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="78321-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="78321-125">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="78321-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="78321-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="78321-126">Next steps</span></span>
- <span data-ttu-id="78321-127">閱讀更多有關 hello Azure CLI: [Azure CLI 文件](/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="78321-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="78321-128">嘗試其他指令碼：[「適用於 MySQL 的 Azure 資料庫」的 Azure CLI 範例](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="78321-128">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="78321-129">如需有關調整的詳細資訊，請參閱[服務層](../concepts-service-tiers.md)及[計算單位和儲存體單位](../concepts-compute-unit-and-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="78321-129">For more information on scaling, see [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md).</span></span>
