---
title: "Azure CLI 指令碼 - 建立適用於 PostgreSQL 的 Azure 資料庫 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 建立「適用於 PostgreSQL 的 Azure 資料庫」伺服器，並設定伺服器等級防火牆規則。"
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: e545b568cd57fdcf28ab33a5ebfa34a495111c7f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-the-azure-cli"></a><span data-ttu-id="6eb3d-103">使用 Azure CLI 建立「適用於 PostgreSQL 的 Azure 資料庫」伺服器並設定防火牆規則</span><span class="sxs-lookup"><span data-stu-id="6eb3d-103">Create an Azure Database for PostgreSQL server and configure a firewall rule using the Azure CLI</span></span>
<span data-ttu-id="6eb3d-104">此範例 CLI 指令碼會建立「適用於 PostgreSQL 的 Azure 資料庫」伺服器，並設定伺服器等級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="6eb3d-104">This sample CLI script creates an Azure Database for PostgreSQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="6eb3d-105">成功執行指令碼後，即可從所有 Azure 服務和已設定的 IP 位址存取 PostgreSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6eb3d-105">Once the script has been successfully run, the PostgreSQL server can be accessed from all Azure services and the configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6eb3d-106">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6eb3d-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6eb3d-107">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="6eb3d-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="6eb3d-108">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="6eb3d-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6eb3d-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="6eb3d-109">Sample script</span></span>
<span data-ttu-id="6eb3d-110">在此範例指令碼中，請編輯醒目提示的命令列以自訂系統管理員使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="6eb3d-110">In this sample script, edit the highlighted lines to customize the admin username and password.</span></span>
<span data-ttu-id="6eb3d-111">[!code-azurecli-interactive[主要](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "建立適用於 PostgreSQL 的 Azure 資料庫，以及伺服器層級防火牆規則。")]</span><span class="sxs-lookup"><span data-stu-id="6eb3d-111">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6eb3d-112">清除部署</span><span class="sxs-lookup"><span data-stu-id="6eb3d-112">Clean up deployment</span></span>
<span data-ttu-id="6eb3d-113">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="6eb3d-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="6eb3d-114">[!code-azurecli-interactive[主要](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "刪除資源群組。")]</span><span class="sxs-lookup"><span data-stu-id="6eb3d-114">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="6eb3d-115">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="6eb3d-115">Script explanation</span></span>
<span data-ttu-id="6eb3d-116">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="6eb3d-116">This script uses the following commands.</span></span> <span data-ttu-id="6eb3d-117">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="6eb3d-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6eb3d-118">**命令**</span><span class="sxs-lookup"><span data-stu-id="6eb3d-118">**Command**</span></span> | <span data-ttu-id="6eb3d-119">**注意事項**</span><span class="sxs-lookup"><span data-stu-id="6eb3d-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="6eb3d-120">az group create</span><span class="sxs-lookup"><span data-stu-id="6eb3d-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="6eb3d-121">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6eb3d-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6eb3d-122">az postgres server create</span><span class="sxs-lookup"><span data-stu-id="6eb3d-122">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="6eb3d-123">建立主控資料庫的 PostgreSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6eb3d-123">Creates a PostgreSQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="6eb3d-124">az postgres server firewall create</span><span class="sxs-lookup"><span data-stu-id="6eb3d-124">az postgres server firewall create</span></span>](/cli/azure/postgres/server/firewall-rule#create) | <span data-ttu-id="6eb3d-125">建立防火牆規則以允許從輸入的 IP 位址範圍存取伺服器及其之下的資料庫。</span><span class="sxs-lookup"><span data-stu-id="6eb3d-125">Creates a firewall rule to allow access to the server and databases under it from the entered IP address range.</span></span> |
| [<span data-ttu-id="6eb3d-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="6eb3d-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="6eb3d-127">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="6eb3d-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6eb3d-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6eb3d-128">Next steps</span></span>
- <span data-ttu-id="6eb3d-129">了解 Azure CLI 的詳細資訊：[Azure CLI 文件](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="6eb3d-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="6eb3d-130">嘗試其他指令碼：[「適用於 PostgreSQL 的 Azure 資料庫」的 Azure CLI 範例](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="6eb3d-130">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
