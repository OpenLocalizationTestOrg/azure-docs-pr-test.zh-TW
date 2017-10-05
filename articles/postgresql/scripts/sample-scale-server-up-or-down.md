---
title: "Azure CLI 指令碼 - 調整適用於 PostgreSQL 的 Azure 資料庫 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 在查詢計量之後，將「適用於 PostgreSQL 的 Azure 資料庫」伺服器調整為不同的效能等級。"
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: b847abb336cce5dd5516469dca58002d3ba265f0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a><span data-ttu-id="d46f5-103">使用 Azure CLI 監視和調整單一 PostgreSQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="d46f5-103">Monitor and scale a single PostgreSQL server using Azure CLI</span></span>
<span data-ttu-id="d46f5-104">此範例 CLI 指令碼會在查詢計量之後，將單一「適用於 PostgreSQL 的 Azure 資料庫」伺服器調整為不同的效能等級。</span><span class="sxs-lookup"><span data-stu-id="d46f5-104">This sample CLI script scales a single Azure Database for PostgreSQL server to a different performance level after querying the metrics.</span></span> 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d46f5-105">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d46f5-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d46f5-106">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="d46f5-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="d46f5-107">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="d46f5-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="d46f5-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="d46f5-108">Sample script</span></span>
<span data-ttu-id="d46f5-109">在此範例指令碼中，請變更醒目提示的命令列以自訂系統管理員使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="d46f5-109">In this sample script, change the highlighted lines to customize the admin username and password.</span></span> <span data-ttu-id="d46f5-110">請將 az monitor 命令中使用的訂用帳戶識別碼取代為您自己的訂用帳戶識別碼。[!code-azurecli-interactive[主要](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "建立適用於 PostgreSQL 的 Azure 資料庫並調整其大小。")]</span><span class="sxs-lookup"><span data-stu-id="d46f5-110">Replace the subscription id used in the az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d46f5-111">清除部署</span><span class="sxs-lookup"><span data-stu-id="d46f5-111">Clean up deployment</span></span>
<span data-ttu-id="d46f5-112">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="d46f5-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="d46f5-113">[!code-azurecli-interactive[主要](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "刪除資源群組。")]</span><span class="sxs-lookup"><span data-stu-id="d46f5-113">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="d46f5-114">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="d46f5-114">Script explanation</span></span>
<span data-ttu-id="d46f5-115">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="d46f5-115">This script uses the following commands.</span></span> <span data-ttu-id="d46f5-116">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="d46f5-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d46f5-117">**命令**</span><span class="sxs-lookup"><span data-stu-id="d46f5-117">**Command**</span></span> | <span data-ttu-id="d46f5-118">**注意事項**</span><span class="sxs-lookup"><span data-stu-id="d46f5-118">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="d46f5-119">az group create</span><span class="sxs-lookup"><span data-stu-id="d46f5-119">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="d46f5-120">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d46f5-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d46f5-121">az postgres server create</span><span class="sxs-lookup"><span data-stu-id="d46f5-121">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="d46f5-122">建立主控資料庫的 PostgreSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d46f5-122">Creates a PostgreSQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="d46f5-123">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="d46f5-123">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="d46f5-124">列出資源的度量值。</span><span class="sxs-lookup"><span data-stu-id="d46f5-124">List the metric value for the resources.</span></span> |
| [<span data-ttu-id="d46f5-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="d46f5-125">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="d46f5-126">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="d46f5-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d46f5-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d46f5-127">Next steps</span></span>
- <span data-ttu-id="d46f5-128">了解 Azure CLI 的詳細資訊：[Azure CLI 文件](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="d46f5-128">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="d46f5-129">嘗試其他指令碼：[「適用於 PostgreSQL 的 Azure 資料庫」的 Azure CLI 範例](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="d46f5-129">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="d46f5-130">了解調整的詳細資訊：[服務層](../concepts-service-tiers.md)及[計算單位和儲存單位](../concepts-compute-unit-and-storage.md)</span><span class="sxs-lookup"><span data-stu-id="d46f5-130">Read more information on scaling: [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md)</span></span>
