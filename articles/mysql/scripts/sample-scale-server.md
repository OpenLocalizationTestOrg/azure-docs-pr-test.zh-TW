---
title: "調整「適用於 MySQL 的 Azure 資料庫」伺服器的 Azuer CLI 範例 | Microsoft Docs"
description: "此範例 CLI 指令碼會在查詢計量之後，將「適用於 MySQL 的 Azure 資料庫」伺服器調整為不同的效能等級。"
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
ms.openlocfilehash: 33316ff3db382d25a444d55772c6ee4d7b7ac418
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="e72f2-103">使用 Azure CLI 監視和調整適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="e72f2-103">Monitor and scale an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="e72f2-104">此範例 CLI 指令碼會在查詢計量之後，將單一「適用於 MySQL 的 Azure 資料庫」伺服器調整為不同的效能等級。</span><span class="sxs-lookup"><span data-stu-id="e72f2-104">This sample CLI script scales a single Azure Database for MySQL server to a different performance level after querying the metrics.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e72f2-105">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="e72f2-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e72f2-106">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="e72f2-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="e72f2-107">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="e72f2-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e72f2-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="e72f2-108">Sample script</span></span>
<span data-ttu-id="e72f2-109">在此範例指令碼中，請變更醒目提示的命令列以自訂系統管理員使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="e72f2-109">In this sample script, change the highlighted lines to customize the admin username and password.</span></span> <span data-ttu-id="e72f2-110">請將 az monitor 命令中使用的訂用帳戶識別碼取代為您自己的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="e72f2-110">Replace the subscription id used in the az monitor commands with your own subscription id.</span></span>
<span data-ttu-id="e72f2-111">[!code-azurecli-interactive[主要](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "建立適用於 MySQL 的 Azure 資料庫並調整其大小。")]</span><span class="sxs-lookup"><span data-stu-id="e72f2-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="e72f2-112">清除部署</span><span class="sxs-lookup"><span data-stu-id="e72f2-112">Clean up deployment</span></span>
<span data-ttu-id="e72f2-113">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="e72f2-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="e72f2-114">[!code-azurecli-interactive[主要](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "刪除資源群組。")]</span><span class="sxs-lookup"><span data-stu-id="e72f2-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="e72f2-115">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="e72f2-115">Script explanation</span></span>
<span data-ttu-id="e72f2-116">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="e72f2-116">This script uses the following commands.</span></span> <span data-ttu-id="e72f2-117">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="e72f2-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e72f2-118">**命令**</span><span class="sxs-lookup"><span data-stu-id="e72f2-118">**Command**</span></span> | <span data-ttu-id="e72f2-119">**注意事項**</span><span class="sxs-lookup"><span data-stu-id="e72f2-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="e72f2-120">az group create</span><span class="sxs-lookup"><span data-stu-id="e72f2-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="e72f2-121">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="e72f2-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e72f2-122">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="e72f2-122">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="e72f2-123">建立主控資料庫的 MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="e72f2-123">Creates a MySQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="e72f2-124">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="e72f2-124">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="e72f2-125">列出資源的度量值。</span><span class="sxs-lookup"><span data-stu-id="e72f2-125">List the metric value for the resources.</span></span> |
| [<span data-ttu-id="e72f2-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="e72f2-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="e72f2-127">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="e72f2-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e72f2-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e72f2-128">Next steps</span></span>
- <span data-ttu-id="e72f2-129">了解 Azure CLI 的詳細資訊：[Azure CLI 文件](/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="e72f2-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="e72f2-130">嘗試其他指令碼：[「適用於 MySQL 的 Azure 資料庫」的 Azure CLI 範例](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="e72f2-130">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="e72f2-131">如需有關調整的詳細資訊，請參閱[服務層](../concepts-service-tiers.md)及[計算單位和儲存體單位](../concepts-compute-unit-and-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="e72f2-131">For more information on scaling, see [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md).</span></span>
