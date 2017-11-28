---
title: "aaaCreate 及管理 Azure 資料庫使用 Azure CLI PostgreSQL 防火牆規則 |Microsoft 文件"
description: "本文說明如何 toocreate 及 PostgreSQL 防火牆規則，使用 Azure CLI 命令列管理 Azure 資料庫。"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 06e34c9e3996c2ec3df63191d794bc34d0ca0cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a><span data-ttu-id="bf856-103">使用 Azure CLI 建立和管理適用於 PostgreSQL 的 Azure 資料庫防火牆規則</span><span class="sxs-lookup"><span data-stu-id="bf856-103">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="bf856-104">伺服器層級防火牆規則可讓系統管理員 toomanage 存取 tooan Azure Database PostgreSQL 伺服器從特定的 IP 位址或 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="bf856-104">Server-level firewall rules enable administrators toomanage access tooan Azure Database for PostgreSQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="bf856-105">您可以使用方便 Azure CLI 命令，來建立、 更新、 刪除、 清單，並顯示您的伺服器防火牆規則 toomanage。</span><span class="sxs-lookup"><span data-stu-id="bf856-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules toomanage your server.</span></span> <span data-ttu-id="bf856-106">如需「適用於 PostgreSQL 的 Azure 資料庫」防火牆的概觀，請參閱[適用於 PostgreSQL 的 Azure 資料庫伺服器防火牆規則](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="bf856-106">For an overview of Azure Database for PostgreSQL firewalls, see [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf856-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="bf856-107">Prerequisites</span></span>
<span data-ttu-id="bf856-108">透過這個方式 tooguide toostep，您需要：</span><span class="sxs-lookup"><span data-stu-id="bf856-108">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="bf856-109">[「適用於 PostgreSQL 的 Azure 資料庫」伺服器和資料庫](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="bf856-109">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="bf856-110">安裝[Azure CLI 2.0](/cli/azure/install-azure-cli)命令列公用程式或使用 hello Azure 雲端殼層 hello 瀏覽器中的。</span><span class="sxs-lookup"><span data-stu-id="bf856-110">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a><span data-ttu-id="bf856-111">設定「適用於 PostgreSQL 的 Azure 資料庫」的防火牆規則</span><span class="sxs-lookup"><span data-stu-id="bf856-111">Configure firewall rules for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="bf856-112">hello [az postgres 伺服器防火牆規則](/cli/azure/postgres/server/firewall-rule)命令會使用的 tooconfigure 防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="bf856-112">hello [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) commands are used tooconfigure firewall rules.</span></span>

## <a name="list-firewall-rules"></a><span data-ttu-id="bf856-113">列出防火牆規則</span><span class="sxs-lookup"><span data-stu-id="bf856-113">List firewall rules</span></span> 
<span data-ttu-id="bf856-114">toolist hello 現有伺服器防火牆規則 hello 在伺服器上，執行 hello [az postgres 伺服器防火牆規則清單](/cli/azure/postgres/server/firewall-rule#list)命令。</span><span class="sxs-lookup"><span data-stu-id="bf856-114">toolist hello existing server firewall rules on hello server, run hello [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="bf856-115">如果依預設，在 JSON 中的任何格式，hello 輸出會列出 hello 規則。</span><span class="sxs-lookup"><span data-stu-id="bf856-115">hello output lists hello rules if any, by default in JSON format.</span></span> <span data-ttu-id="bf856-116">您可以使用 hello 交換器`--output table`更容易閱讀的表格格式做為 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="bf856-116">You may use hello switch `--output table` for a more readable table format as hello output.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a><span data-ttu-id="bf856-117">建立防火牆規則</span><span class="sxs-lookup"><span data-stu-id="bf856-117">Create firewall rule</span></span>
<span data-ttu-id="bf856-118">新的防火牆規則 hello 在伺服器上，執行 hello toocreate [az postgres 伺服器防火牆規則建立](/cli/azure/postgres/server/firewall-rule#create)命令。</span><span class="sxs-lookup"><span data-stu-id="bf856-118">toocreate a new firewall rule on hello server, run hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> 

<span data-ttu-id="bf856-119">這個範例允許所有 IP 位址 tooaccess hello 伺服器範圍**mypgserver 20170401.postgres.database.azure.com**</span><span class="sxs-lookup"><span data-stu-id="bf856-119">This example allows a range of all IP addresses tooaccess hello server **mypgserver-20170401.postgres.database.azure.com**</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
<span data-ttu-id="bf856-120">tooallow 單數的 IP 位址 tooaccess，提供 hello 起始 IP 和結束 IP，如此範例所示為 hello 相同的位址。</span><span class="sxs-lookup"><span data-stu-id="bf856-120">tooallow a singular IP address tooaccess, provide hello same address as hello Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
<span data-ttu-id="bf856-121">成功時，hello 命令輸出會列出您已建立，根據預設，在 JSON 格式的 hello 防火牆規則的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="bf856-121">Upon success, hello command output lists hello details of hello firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="bf856-122">如果失敗，hello 改為輸出 showserror 訊息文字。</span><span class="sxs-lookup"><span data-stu-id="bf856-122">If there is a failure, hello output showserror message text instead.</span></span>

## <a name="update-firewall-rule"></a><span data-ttu-id="bf856-123">更新防火牆規則</span><span class="sxs-lookup"><span data-stu-id="bf856-123">Update firewall rule</span></span> 
<span data-ttu-id="bf856-124">更新現有防火牆規則上 hello 伺服器使用[az postgres 伺服器防火牆規則更新](/cli/azure/postgres/server/firewall-rule#update)命令。</span><span class="sxs-lookup"><span data-stu-id="bf856-124">Update an existing firewall rule on hello server using [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) command.</span></span> <span data-ttu-id="bf856-125">提供 hello 做為輸入，而且 hello 起始 IP 和結束 IP 屬性 tooupdate hello 現有防火牆規則名稱。</span><span class="sxs-lookup"><span data-stu-id="bf856-125">Provide hello name of hello existing firewall rule as input, and hello start IP and end IP attributes tooupdate.</span></span>
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
<span data-ttu-id="bf856-126">成功時，hello 命令輸出會列出您已更新，根據預設，在 JSON 格式的 hello 防火牆規則的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="bf856-126">Upon success, hello command output lists hello details of hello firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="bf856-127">如果失敗，hello 改為輸出 showserror 訊息文字。</span><span class="sxs-lookup"><span data-stu-id="bf856-127">If there is a failure, hello output showserror message text instead.</span></span>
> [!NOTE]
> <span data-ttu-id="bf856-128">如果 hello 防火牆規則不存在，它取得建立 hello 更新命令。</span><span class="sxs-lookup"><span data-stu-id="bf856-128">If hello firewall rule does not exist, it gets created by hello update command.</span></span>

## <a name="show-firewall-rule-details"></a><span data-ttu-id="bf856-129">顯示防火牆規則詳細資料</span><span class="sxs-lookup"><span data-stu-id="bf856-129">Show firewall rule details</span></span>
<span data-ttu-id="bf856-130">您也可以顯示 hello 現有防火牆規則的詳細資料的伺服器執行[az postgres 伺服器防火牆規則顯示](/cli/azure/postgres/server/firewall-rule#show)命令。</span><span class="sxs-lookup"><span data-stu-id="bf856-130">You can also show hello existing firewall rule details for a server by running [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="bf856-131">成功時，hello 命令輸出會列出您已指定，預設會在 JSON 格式的 hello 防火牆規則的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="bf856-131">Upon success, hello command output lists hello details of hello firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="bf856-132">如果失敗，hello 改為輸出 showserror 訊息文字。</span><span class="sxs-lookup"><span data-stu-id="bf856-132">If there is a failure, hello output showserror message text instead.</span></span>

## <a name="delete-firewall-rule"></a><span data-ttu-id="bf856-133">刪除防火牆規則</span><span class="sxs-lookup"><span data-stu-id="bf856-133">Delete firewall rule</span></span>
<span data-ttu-id="bf856-134">IP 範圍從 hello 伺服器 toorevoke 存取刪除現有的防火牆規則執行 hello [az postgres 伺服器防火牆規則刪除](/cli/azure/postgres/server/firewall-rule#delete)命令。</span><span class="sxs-lookup"><span data-stu-id="bf856-134">toorevoke access for an IP range from hello server, delete an existing firewall rule by executing hello [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) command.</span></span> <span data-ttu-id="bf856-135">提供 hello hello 現有防火牆規則名稱。</span><span class="sxs-lookup"><span data-stu-id="bf856-135">Provide hello name of hello existing firewall rule.</span></span>
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="bf856-136">成功時，沒有任何輸出。</span><span class="sxs-lookup"><span data-stu-id="bf856-136">Upon success, there is no output.</span></span> <span data-ttu-id="bf856-137">在發生錯誤時，會傳回 hello 錯誤訊息文字。</span><span class="sxs-lookup"><span data-stu-id="bf856-137">Upon failure, hello error message text is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf856-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bf856-138">Next steps</span></span>
- <span data-ttu-id="bf856-139">同樣地，您可以使用網頁瀏覽器太[建立及管理 Azure 資料庫使用 hello Azure 入口網站的 PostgreSQL 防火牆規則](howto-manage-firewall-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="bf856-139">Similarly, you can use a web browser too[Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal](howto-manage-firewall-using-portal.md)</span></span>
- <span data-ttu-id="bf856-140">進一步了解[適用於 PostgreSQL 的 Azure 資料庫伺服器防火牆規則](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="bf856-140">Understand more about [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>
- <span data-ttu-id="bf856-141">連線 PostgreSQL 伺服器 tooan Azure 資料庫的說明，請參閱[PostgreSQL 的 Azure 資料庫的連接程式庫](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="bf856-141">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
