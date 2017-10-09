---
title: "使用 Azure CLI 來設計您第一個適用於 PostgreSQL 的 Azure 資料庫 | Microsoft Docs"
description: "本教學課程示範如何 tooDesign 第一次 Azure 資料庫，以獲得 PostgreSQL 使用 Azure CLI。"
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: tutorial
ms.date: 06/13/2017
ms.openlocfilehash: 7914925c090e0b6f3e7c8a999eedb0b2baf83d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a><span data-ttu-id="a9656-103">使用 Azure CLI 來設計您第一個適用於 PostgreSQL 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="a9656-103">Design your first Azure Database for PostgreSQL using Azure CLI</span></span> 
<span data-ttu-id="a9656-104">在此教學課程中，您使用 Azure CLI （命令列介面） 和其他公用程式 toolearn 如何以：</span><span class="sxs-lookup"><span data-stu-id="a9656-104">In this tutorial, you use Azure CLI (command-line interface) and other utilities toolearn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="a9656-105">建立適用於 PostgreSQL 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="a9656-105">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="a9656-106">Hello 伺服器防火牆設定</span><span class="sxs-lookup"><span data-stu-id="a9656-106">Configure hello server firewall</span></span>
> * <span data-ttu-id="a9656-107">使用[ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html)公用程式 toocreate 資料庫</span><span class="sxs-lookup"><span data-stu-id="a9656-107">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="a9656-108">載入範例資料</span><span class="sxs-lookup"><span data-stu-id="a9656-108">Load sample data</span></span>
> * <span data-ttu-id="a9656-109">查詢資料</span><span class="sxs-lookup"><span data-stu-id="a9656-109">Query data</span></span>
> * <span data-ttu-id="a9656-110">更新資料</span><span class="sxs-lookup"><span data-stu-id="a9656-110">Update data</span></span>
> * <span data-ttu-id="a9656-111">還原資料</span><span class="sxs-lookup"><span data-stu-id="a9656-111">Restore data</span></span>

<span data-ttu-id="a9656-112">您可以使用在 hello 瀏覽器中的 hello Azure 雲端殼層或[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)在本教學課程中您自己電腦 toorun hello 程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="a9656-112">You may use hello Azure Cloud Shell in hello browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer toorun hello code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a9656-113">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a9656-113">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a9656-114">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="a9656-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a9656-115">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="a9656-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="a9656-116">如果您有多個訂閱，選擇適當 hello 訂閱 hello 資源存在或已支付。</span><span class="sxs-lookup"><span data-stu-id="a9656-116">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="a9656-117">使用 [az account set](/cli/azure/account#set) 命令來選取您帳戶底下的特定訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="a9656-117">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="a9656-118">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="a9656-118">Create a resource group</span></span>
<span data-ttu-id="a9656-119">建立[Azure 資源群組](../azure-resource-manager/resource-group-overview.md)使用 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="a9656-119">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="a9656-120">資源群組是在其中以群組方式部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="a9656-120">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="a9656-121">hello 下列範例會建立名為的資源群組`myresourcegroup`在 hello`westus`位置。</span><span class="sxs-lookup"><span data-stu-id="a9656-121">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="a9656-122">建立適用於 PostgreSQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="a9656-122">Create an Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="a9656-123">建立[PostgreSQL server 的 Azure 資料庫](overview.md)使用 hello [az postgres 伺服器建立](/cli/azure/postgres/server#create)命令。</span><span class="sxs-lookup"><span data-stu-id="a9656-123">Create an [Azure Database for PostgreSQL server](overview.md) using hello [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="a9656-124">一個伺服器會包含一組以群組方式管理的資料庫。</span><span class="sxs-lookup"><span data-stu-id="a9656-124">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="a9656-125">hello 下列範例會建立名為伺服器`mypgserver-20170401`資源群組中`myresourcegroup`與伺服器系統管理員登入`mylogin`。</span><span class="sxs-lookup"><span data-stu-id="a9656-125">hello following example creates a server called `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="a9656-126">伺服器的名稱將 tooDNS 名稱對應，因此在 Azure 中全域唯一的必要的 toobe。</span><span class="sxs-lookup"><span data-stu-id="a9656-126">Name of a server maps tooDNS name and is thus required toobe globally unique in Azure.</span></span> <span data-ttu-id="a9656-127">替代 hello`<server_admin_password>`與您自己的值。</span><span class="sxs-lookup"><span data-stu-id="a9656-127">Substitute hello `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="a9656-128">hello 伺服器系統管理員登入和密碼，您在此處指定為 toohello server 中的必要的 toolog 和其資料庫，稍後在這個快速入門。</span><span class="sxs-lookup"><span data-stu-id="a9656-128">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="a9656-129">請記住或記錄此資訊，以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="a9656-129">Remember or record this information for later use.</span></span>

<span data-ttu-id="a9656-130">根據預設，**postgres** 資料庫會建立在您的伺服器底下。</span><span class="sxs-lookup"><span data-stu-id="a9656-130">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="a9656-131">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html)資料庫是適用於由使用者、 公用程式及協力廠商應用程式的預設資料庫。</span><span class="sxs-lookup"><span data-stu-id="a9656-131">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="a9656-132">設定伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="a9656-132">Configure a server-level firewall rule</span></span>

<span data-ttu-id="a9656-133">建立 Azure PostgreSQL 伺服器層級防火牆規則以 hello [az postgres 伺服器防火牆規則建立](/cli/azure/postgres/server/firewall-rule#create)命令。</span><span class="sxs-lookup"><span data-stu-id="a9656-133">Create an Azure PostgreSQL server-level firewall rule with hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="a9656-134">伺服器層級防火牆規則允許外部應用程式，例如[psql](https://www.postgresql.org/docs/9.2/static/app-psql.html)或[PgAdmin](https://www.pgadmin.org/) tooconnect tooyour 伺服器透過 hello Azure PostgreSQL 服務防火牆。</span><span class="sxs-lookup"><span data-stu-id="a9656-134">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server through hello Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="a9656-135">您可以設定防火牆規則，它涵蓋了 IP 範圍 toobe 無法 tooconnect 從您的網路。</span><span class="sxs-lookup"><span data-stu-id="a9656-135">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span> <span data-ttu-id="a9656-136">hello 下列範例會使用[az postgres 伺服器防火牆規則建立](/cli/azure/postgres/server/firewall-rule#create)toocreate 防火牆規則`AllowAllIps`ip 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="a9656-136">hello following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) toocreate a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="a9656-137">tooopen 所有 IP 位址，都作為 hello 起始 IP 位址和 255.255.255.255 hello 結束位址為 0.0.0.0。</span><span class="sxs-lookup"><span data-stu-id="a9656-137">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="a9656-138">Azure PostgreSQL 伺服器會透過連接埠 5432 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="a9656-138">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="a9656-139">當您從公司網路內進行連線時，網路的防火牆可能不允許透過連接埠 5432 的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="a9656-139">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="a9656-140">具有您開啟通訊埠 5432 tooconnect tooyour Azure SQL Database 伺服器的 IT 部門。</span><span class="sxs-lookup"><span data-stu-id="a9656-140">Have your IT department open port 5432 tooconnect tooyour Azure SQL Database server.</span></span>
>

## <a name="get-hello-connection-information"></a><span data-ttu-id="a9656-141">取得 hello 的連接資訊</span><span class="sxs-lookup"><span data-stu-id="a9656-141">Get hello connection information</span></span>

<span data-ttu-id="a9656-142">tooconnect tooyour 伺服器，您需要 tooprovide 主機資訊和存取認證。</span><span class="sxs-lookup"><span data-stu-id="a9656-142">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="a9656-143">hello 結果是以 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="a9656-143">hello result is in JSON format.</span></span> <span data-ttu-id="a9656-144">請記下 hello **administratorLogin**和**fullyQualifiedDomainName**。</span><span class="sxs-lookup"><span data-stu-id="a9656-144">Make a note of hello **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
```json
{
  "administratorLogin": "mylogin",
  "fullyQualifiedDomainName": "mypgserver-20170401.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforPostgreSQL/servers/mypgserver-20170401",
  "location": "westus",
  "name": "mypgserver-20170401",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "PGSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 51200,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": "9.6"
}
```

## <a name="connect-tooazure-database-for-postgresql-database-using-psql"></a><span data-ttu-id="a9656-145">連接 tooAzure 資料庫使用 psql PostgreSQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="a9656-145">Connect tooAzure Database for PostgreSQL database using psql</span></span>
<span data-ttu-id="a9656-146">如果您的用戶端電腦已安裝的 PostgreSQL，您可以使用的本機執行個體[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html)，或 hello Azure 雲端主控台 tooconnect tooan Azure PostgreSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a9656-146">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), or hello Azure Cloud Console tooconnect tooan Azure PostgreSQL server.</span></span> <span data-ttu-id="a9656-147">我們現在使用 hello psql 命令列公用程式 tooconnect toohello Azure Database PostgreSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a9656-147">Let's now use hello psql command-line utility tooconnect toohello Azure Database for PostgreSQL server.</span></span>

1. <span data-ttu-id="a9656-148">執行下列 psql 命令 tooconnect tooan Azure Database PostgreSQL 伺服器 hello</span><span class="sxs-lookup"><span data-stu-id="a9656-148">Run hello following psql command tooconnect tooan Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="a9656-149">比方說，下列命令的 hello 連接 toohello 預設資料庫呼叫**postgres** PostgreSQL 伺服器上**mypgserver 20170401.postgres.database.azure.com**使用存取認證。</span><span class="sxs-lookup"><span data-stu-id="a9656-149">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="a9656-150">輸入 hello`<server_admin_password>`您選擇當系統提示您輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="a9656-150">Enter hello `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  <span data-ttu-id="a9656-151">一旦您已連線的 toohello 伺服器，建立一個空白資料庫在 hello 提示字元。</span><span class="sxs-lookup"><span data-stu-id="a9656-151">Once you are connected toohello server, create a blank database at hello prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="a9656-152">在 hello 提示字元中執行下列命令 tooswitch 連線 toohello 新建資料庫的 hello **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="a9656-152">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="a9656-153">Hello 資料庫中建立資料表</span><span class="sxs-lookup"><span data-stu-id="a9656-153">Create tables in hello database</span></span>
<span data-ttu-id="a9656-154">您現在知道如何 tooconnect toohello PostgreSQL 的 Azure 資料庫，我們可能會超出如何 toocomplete 某些基本工作。</span><span class="sxs-lookup"><span data-stu-id="a9656-154">Now that you know how tooconnect toohello Azure Database for PostgreSQL, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="a9656-155">首先，我們可以建立資料表並在其中載入一些資料。</span><span class="sxs-lookup"><span data-stu-id="a9656-155">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="a9656-156">我們將建立一個追蹤清查資訊的資料表。</span><span class="sxs-lookup"><span data-stu-id="a9656-156">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="a9656-157">您可以看到新建立的資料表中的資料表的 hello 清單現在輸入 hello:</span><span class="sxs-lookup"><span data-stu-id="a9656-157">You can see hello newly created table in hello list of tables now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="a9656-158">資料載入至 hello 資料表</span><span class="sxs-lookup"><span data-stu-id="a9656-158">Load data into hello tables</span></span>
<span data-ttu-id="a9656-159">既然我們已有資料表，我們可以在其中插入一些資料。</span><span class="sxs-lookup"><span data-stu-id="a9656-159">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="a9656-160">在 hello 開啟命令提示字元視窗中，執行下列查詢 tooinsert hello 某些資料列的資料</span><span class="sxs-lookup"><span data-stu-id="a9656-160">At hello open command prompt window, run hello following query tooinsert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="a9656-161">您有範例資料插入您稍早建立的 hello 資料表現在包含兩個資料列。</span><span class="sxs-lookup"><span data-stu-id="a9656-161">You have now two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="a9656-162">查詢和更新 hello 資料表中的 hello 資料</span><span class="sxs-lookup"><span data-stu-id="a9656-162">Query and update hello data in hello tables</span></span>
<span data-ttu-id="a9656-163">執行 hello hello 資料庫資料表中的下列查詢 tooretrieve 資訊。</span><span class="sxs-lookup"><span data-stu-id="a9656-163">Execute hello following query tooretrieve information from hello database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="a9656-164">您也可以更新 hello 資料表中的 hello 資料</span><span class="sxs-lookup"><span data-stu-id="a9656-164">You can also update hello data in hello tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="a9656-165">當您擷取資料時，取得據以更新 hello 資料列。</span><span class="sxs-lookup"><span data-stu-id="a9656-165">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="a9656-166">還原資料庫 tooa 前一個點的時間</span><span class="sxs-lookup"><span data-stu-id="a9656-166">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="a9656-167">假設您不小心刪除了資料表。</span><span class="sxs-lookup"><span data-stu-id="a9656-167">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="a9656-168">這是您無法輕易復原的情況。</span><span class="sxs-lookup"><span data-stu-id="a9656-168">This is something you cannot easily recover from.</span></span> <span data-ttu-id="a9656-169">Azure PostgreSQL 資料庫可讓您 （在最後一個向上 too7 天 （基本） 則為 35 天 （標準） hello) 的 toogo 後 tooany 在時間點，並還原這個時間點 tooa 新的伺服器。</span><span class="sxs-lookup"><span data-stu-id="a9656-169">Azure Database for PostgreSQL allows you toogo back tooany point-in-time (in hello last up too7 days (Basic) and 35 days (Standard)) and restore this point-in-time tooa new server.</span></span> <span data-ttu-id="a9656-170">您可以使用這個新的伺服器 toorecover 刪除的資料。</span><span class="sxs-lookup"><span data-stu-id="a9656-170">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="a9656-171">hello 加入 hello 資料表之前，請遵循步驟還原 hello 範例伺服器 tooa 點。</span><span class="sxs-lookup"><span data-stu-id="a9656-171">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="a9656-172">hello`az postgres server restore`命令需要 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="a9656-172">hello `az postgres server restore` command needs hello following parameters:</span></span>
| <span data-ttu-id="a9656-173">設定</span><span class="sxs-lookup"><span data-stu-id="a9656-173">Setting</span></span> | <span data-ttu-id="a9656-174">建議的值</span><span class="sxs-lookup"><span data-stu-id="a9656-174">Suggested value</span></span> | <span data-ttu-id="a9656-175">說明</span><span class="sxs-lookup"><span data-stu-id="a9656-175">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="a9656-176">--resource-group</span><span class="sxs-lookup"><span data-stu-id="a9656-176">--resource-group</span></span> |  <span data-ttu-id="a9656-177">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a9656-177">myResourceGroup</span></span> |  <span data-ttu-id="a9656-178">資源群組中的 hello 來源伺服器已存在。</span><span class="sxs-lookup"><span data-stu-id="a9656-178">The resource group in which hello source server exists.</span></span>  |
| <span data-ttu-id="a9656-179">--name</span><span class="sxs-lookup"><span data-stu-id="a9656-179">--name</span></span> | <span data-ttu-id="a9656-180">mypgserver-restored</span><span class="sxs-lookup"><span data-stu-id="a9656-180">mypgserver-restored</span></span> | <span data-ttu-id="a9656-181">hello hello hello restore 命令所建立的新伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="a9656-181">hello name of hello new server that is created by hello restore command.</span></span> |
| <span data-ttu-id="a9656-182">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="a9656-182">restore-point-in-time</span></span> | <span data-ttu-id="a9656-183">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="a9656-183">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="a9656-184">選取以時間點 toorestore。</span><span class="sxs-lookup"><span data-stu-id="a9656-184">Select a point-in-time toorestore to.</span></span> <span data-ttu-id="a9656-185">這個日期和時間必須在 hello 來源伺服器的備份保留期限內。</span><span class="sxs-lookup"><span data-stu-id="a9656-185">This date and time must be within hello source server's backup retention period.</span></span> <span data-ttu-id="a9656-186">請使用 ISO8601 日期和時間格式。</span><span class="sxs-lookup"><span data-stu-id="a9656-186">Use ISO8601 date and time format.</span></span> <span data-ttu-id="a9656-187">例如，您可能會使用您自己的本地時區，例如 `2017-04-13T05:59:00-08:00`，或使用 UTC Zulu 格式 `2017-04-13T13:59:00Z`。</span><span class="sxs-lookup"><span data-stu-id="a9656-187">For example, you may use your own local timezone, such as `2017-04-13T05:59:00-08:00`, or use UTC Zulu format `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="a9656-188">--source-server</span><span class="sxs-lookup"><span data-stu-id="a9656-188">--source-server</span></span> | <span data-ttu-id="a9656-189">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="a9656-189">mypgserver-20170401</span></span> | <span data-ttu-id="a9656-190">hello 名稱或識別碼 hello 來源伺服器 toorestore 從。</span><span class="sxs-lookup"><span data-stu-id="a9656-190">hello name or ID of hello source server toorestore from.</span></span> |

<span data-ttu-id="a9656-191">還原伺服器 tooa 在時間點建立新的伺服器，做為 hello 原始伺服器 hello 點複製指定的時間。</span><span class="sxs-lookup"><span data-stu-id="a9656-191">Restoring a server tooa point-in-time creates a new server, copying as hello original server as of hello point in time you specify.</span></span> <span data-ttu-id="a9656-192">hello 位置及定價層 hello 還原伺服器的值為 hello 與 hello 來源伺服器相同。</span><span class="sxs-lookup"><span data-stu-id="a9656-192">hello location and pricing tier values for hello restored server are hello same as hello source server.</span></span>

<span data-ttu-id="a9656-193">hello 命令為同步，而且將 hello 伺服器恢復正常後傳回。</span><span class="sxs-lookup"><span data-stu-id="a9656-193">hello command is synchronous, and will return after hello server is restored.</span></span> <span data-ttu-id="a9656-194">一旦 hello 還原完成時，找出 hello 已建立的新伺服器。</span><span class="sxs-lookup"><span data-stu-id="a9656-194">Once hello restore finishes, locate hello new server that was created.</span></span> <span data-ttu-id="a9656-195">請確認資料已還原，如預期般的 hello。</span><span class="sxs-lookup"><span data-stu-id="a9656-195">Verify hello data was restored as expected.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a9656-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a9656-196">Next steps</span></span>
<span data-ttu-id="a9656-197">在本教學課程中，您學到如何 toouse Azure CLI （命令列介面） 和其他公用程式：</span><span class="sxs-lookup"><span data-stu-id="a9656-197">In this tutorial, you learned how toouse Azure CLI (command-line interface) and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="a9656-198">建立適用於 PostgreSQL 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="a9656-198">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="a9656-199">Hello 伺服器防火牆設定</span><span class="sxs-lookup"><span data-stu-id="a9656-199">Configure hello server firewall</span></span>
> * <span data-ttu-id="a9656-200">使用[ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html)公用程式 toocreate 資料庫</span><span class="sxs-lookup"><span data-stu-id="a9656-200">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="a9656-201">載入範例資料</span><span class="sxs-lookup"><span data-stu-id="a9656-201">Load sample data</span></span>
> * <span data-ttu-id="a9656-202">查詢資料</span><span class="sxs-lookup"><span data-stu-id="a9656-202">Query data</span></span>
> * <span data-ttu-id="a9656-203">更新資料</span><span class="sxs-lookup"><span data-stu-id="a9656-203">Update data</span></span>
> * <span data-ttu-id="a9656-204">還原資料</span><span class="sxs-lookup"><span data-stu-id="a9656-204">Restore data</span></span>

<span data-ttu-id="a9656-205">接下來，了解如何 toouse hello Azure 入口網站 toodo 類似的工作，請檢閱本教學課程： [PostgreSQL 使用 hello Azure 入口網站的設計您的第一個 Azure 資料庫](tutorial-design-database-using-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a9656-205">Next, learn how toouse hello Azure portal toodo similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using hello Azure portal](tutorial-design-database-using-azure-portal.md)</span></span>
