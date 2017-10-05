---
title: "使用 Azure CLI 建立和管理適用於 PostgreSQL 的 Azure 資料庫防火牆規則 | Microsoft Docs"
description: "本文說明如何使用 Azure CLI 命令列，建立和管理適用於 PostgreSQL 的 Azure 資料庫防火牆規則。"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 6f081416dd7d78f0153b3fda21a340a8c1a70c5f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a><span data-ttu-id="4ea74-103">使用 Azure CLI 建立和管理適用於 PostgreSQL 的 Azure 資料庫防火牆規則</span><span class="sxs-lookup"><span data-stu-id="4ea74-103">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="4ea74-104">伺服器等級防火牆規則可讓系統管理員從特定的 IP 位址或 IP 位址範圍，管理和存取適用於 PostgreSQL 的 Azure 資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="4ea74-104">Server-level firewall rules enable administrators to manage access to an Azure Database for PostgreSQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="4ea74-105">透過方便的 Azure CLI 命令，您可以建立、更新、刪除、列出及顯示防火牆規則，以管理您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="4ea74-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules to manage your server.</span></span> <span data-ttu-id="4ea74-106">如需「適用於 PostgreSQL 的 Azure 資料庫」防火牆的概觀，請參閱[適用於 PostgreSQL 的 Azure 資料庫伺服器防火牆規則](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="4ea74-106">For an overview of Azure Database for PostgreSQL firewalls, see [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ea74-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="4ea74-107">Prerequisites</span></span>
<span data-ttu-id="4ea74-108">若要逐步執行本作法指南，您需要︰</span><span class="sxs-lookup"><span data-stu-id="4ea74-108">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="4ea74-109">[「適用於 PostgreSQL 的 Azure 資料庫」伺服器和資料庫](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="4ea74-109">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="4ea74-110">安裝 [Azure CLI 2.0](/cli/azure/install-azure-cli) 命令列公用程式，或在瀏覽器中使用 Azure Cloud Shell。</span><span class="sxs-lookup"><span data-stu-id="4ea74-110">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a><span data-ttu-id="4ea74-111">設定「適用於 PostgreSQL 的 Azure 資料庫」的防火牆規則</span><span class="sxs-lookup"><span data-stu-id="4ea74-111">Configure firewall rules for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="4ea74-112">[az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) 命令可用於設定防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="4ea74-112">The [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) commands are used to configure firewall rules.</span></span>

## <a name="list-firewall-rules"></a><span data-ttu-id="4ea74-113">列出防火牆規則</span><span class="sxs-lookup"><span data-stu-id="4ea74-113">List firewall rules</span></span> 
<span data-ttu-id="4ea74-114">若要列出伺服器上現有的伺服器防火牆規則，請執行 [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) 命令。</span><span class="sxs-lookup"><span data-stu-id="4ea74-114">To list the existing server firewall rules on the server, run the [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="4ea74-115">輸出會列出規則 (若有的話)，預設為 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="4ea74-115">The output lists the rules if any, by default in JSON format.</span></span> <span data-ttu-id="4ea74-116">您可以使用參數 `--output table`，以更容易閱讀的資料表格式呈現輸出。</span><span class="sxs-lookup"><span data-stu-id="4ea74-116">You may use the switch `--output table` for a more readable table format as the output.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a><span data-ttu-id="4ea74-117">建立防火牆規則</span><span class="sxs-lookup"><span data-stu-id="4ea74-117">Create firewall rule</span></span>
<span data-ttu-id="4ea74-118">若要在伺服器上建立新的防火牆規則，請執行 [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) 命令。</span><span class="sxs-lookup"><span data-stu-id="4ea74-118">To create a new firewall rule on the server, run the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> 

<span data-ttu-id="4ea74-119">此範例允許所有 IP 位址範圍存取伺服器 **mypgserver-20170401.postgres.database.azure.com**</span><span class="sxs-lookup"><span data-stu-id="4ea74-119">This example allows a range of all IP addresses to access the server **mypgserver-20170401.postgres.database.azure.com**</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
<span data-ttu-id="4ea74-120">若要允許單一 IP 位址進行存取，請提供相同的位址作為起始 IP 和結束 IP，如這個範例所示。</span><span class="sxs-lookup"><span data-stu-id="4ea74-120">To allow a singular IP address to access, provide the same address as the Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
<span data-ttu-id="4ea74-121">成功時，命令輸出會列出您已建立之防火牆規則的詳細資料，預設為 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="4ea74-121">Upon success, the command output lists the details of the firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="4ea74-122">如果失敗，輸出就會改為顯示錯誤訊息文字。</span><span class="sxs-lookup"><span data-stu-id="4ea74-122">If there is a failure, the output showserror message text instead.</span></span>

## <a name="update-firewall-rule"></a><span data-ttu-id="4ea74-123">更新防火牆規則</span><span class="sxs-lookup"><span data-stu-id="4ea74-123">Update firewall rule</span></span> 
<span data-ttu-id="4ea74-124">請使用 [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) 命令更新伺服器上現有的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="4ea74-124">Update an existing firewall rule on the server using [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) command.</span></span> <span data-ttu-id="4ea74-125">提供現有防火牆規則的名稱作為輸入，以及要更新的起始 IP 和結束 IP 屬性。</span><span class="sxs-lookup"><span data-stu-id="4ea74-125">Provide the name of the existing firewall rule as input, and the start IP and end IP attributes to update.</span></span>
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
<span data-ttu-id="4ea74-126">成功時，命令輸出會列出您已更新之防火牆規則的詳細資料，預設為 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="4ea74-126">Upon success, the command output lists the details of the firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="4ea74-127">如果失敗，輸出就會改為顯示錯誤訊息文字。</span><span class="sxs-lookup"><span data-stu-id="4ea74-127">If there is a failure, the output showserror message text instead.</span></span>
> [!NOTE]
> <span data-ttu-id="4ea74-128">如果防火牆規則不存在，更新命令則會相關規則。</span><span class="sxs-lookup"><span data-stu-id="4ea74-128">If the firewall rule does not exist, it gets created by the update command.</span></span>

## <a name="show-firewall-rule-details"></a><span data-ttu-id="4ea74-129">顯示防火牆規則詳細資料</span><span class="sxs-lookup"><span data-stu-id="4ea74-129">Show firewall rule details</span></span>
<span data-ttu-id="4ea74-130">您也可以執行 [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) 命令，以顯示伺服器現有的防火牆規則詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4ea74-130">You can also show the existing firewall rule details for a server by running [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="4ea74-131">成功時，命令輸出會列出您已指定之防火牆規則的詳細資料，預設為 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="4ea74-131">Upon success, the command output lists the details of the firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="4ea74-132">如果失敗，輸出就會改為顯示錯誤訊息文字。</span><span class="sxs-lookup"><span data-stu-id="4ea74-132">If there is a failure, the output showserror message text instead.</span></span>

## <a name="delete-firewall-rule"></a><span data-ttu-id="4ea74-133">刪除防火牆規則</span><span class="sxs-lookup"><span data-stu-id="4ea74-133">Delete firewall rule</span></span>
<span data-ttu-id="4ea74-134">若要從伺服器撤銷 IP 範圍的存取，請執行 [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) 命令以刪除現有防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="4ea74-134">To revoke access for an IP range from the server, delete an existing firewall rule by executing the [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) command.</span></span> <span data-ttu-id="4ea74-135">提供現有防火牆規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ea74-135">Provide the name of the existing firewall rule.</span></span>
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="4ea74-136">成功時，沒有任何輸出。</span><span class="sxs-lookup"><span data-stu-id="4ea74-136">Upon success, there is no output.</span></span> <span data-ttu-id="4ea74-137">發生錯誤時，就會傳回錯誤訊息文字。</span><span class="sxs-lookup"><span data-stu-id="4ea74-137">Upon failure, the error message text is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ea74-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ea74-138">Next steps</span></span>
- <span data-ttu-id="4ea74-139">同樣地，您可以透過網頁瀏覽器，[使用 Azure 入口網站建立和管理適用於 PostgreSQL 的 Azure 資料庫防火牆規則](howto-manage-firewall-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="4ea74-139">Similarly, you can use a web browser to [Create and manage Azure Database for PostgreSQL firewall rules using the Azure portal](howto-manage-firewall-using-portal.md)</span></span>
- <span data-ttu-id="4ea74-140">進一步了解[適用於 PostgreSQL 的 Azure 資料庫伺服器防火牆規則](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="4ea74-140">Understand more about [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>
- <span data-ttu-id="4ea74-141">如需連線至「適用於 PostgreSQL 的 Azure 資料庫」伺服器的說明，請參閱[「適用於 PostgreSQL 的 Azure 資料庫」的連線庫](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="4ea74-141">For help in connecting to an Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
