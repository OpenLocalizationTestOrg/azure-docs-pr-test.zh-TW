---
title: "第一個 Azure 資料庫的 MySQL 資料庫-Azure CLI aaaDesign |Microsoft 文件"
description: "本教學課程說明如何 toocreate 和管理 Azure 資料庫的 MySQL 伺服器資料庫從 hello 命令列使用 Azure CLI 2.0。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 6339913c2af58e0e4c4eabb69097a5c9c245781c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="cbcf5-103">設計您第一個適用於 MySQL 資料庫的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="cbcf5-103">Design your first Azure Database for MySQL database</span></span>

<span data-ttu-id="cbcf5-104">Azure 的 MySQL 資料庫是關聯式資料庫中的服務 hello Microsoft 雲端式 MySQL Community Edition 資料庫引擎上。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-104">Azure Database for MySQL is a relational database service in hello Microsoft cloud based on MySQL Community Edition database engine.</span></span> <span data-ttu-id="cbcf5-105">在此教學課程中，您使用 Azure CLI （命令列介面） 和其他公用程式 toolearn 如何以：</span><span class="sxs-lookup"><span data-stu-id="cbcf5-105">In this tutorial, you use Azure CLI (command-line interface) and other utilities toolearn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cbcf5-106">建立適用於 MySQL 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="cbcf5-106">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="cbcf5-107">Hello 伺服器防火牆設定</span><span class="sxs-lookup"><span data-stu-id="cbcf5-107">Configure hello server firewall</span></span>
> * <span data-ttu-id="cbcf5-108">使用[mysql 命令列工具](https://dev.mysql.com/doc/refman/5.6/en/mysql.html)toocreate 資料庫</span><span class="sxs-lookup"><span data-stu-id="cbcf5-108">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate a database</span></span>
> * <span data-ttu-id="cbcf5-109">載入範例資料</span><span class="sxs-lookup"><span data-stu-id="cbcf5-109">Load sample data</span></span>
> * <span data-ttu-id="cbcf5-110">查詢資料</span><span class="sxs-lookup"><span data-stu-id="cbcf5-110">Query data</span></span>
> * <span data-ttu-id="cbcf5-111">更新資料</span><span class="sxs-lookup"><span data-stu-id="cbcf5-111">Update data</span></span>
> * <span data-ttu-id="cbcf5-112">還原資料</span><span class="sxs-lookup"><span data-stu-id="cbcf5-112">Restore data</span></span>

<span data-ttu-id="cbcf5-113">您可以使用在 hello 瀏覽器中的 hello Azure 雲端殼層或[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)在本教學課程中您自己電腦 toorun hello 程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-113">You may use hello Azure Cloud Shell in hello browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer toorun hello code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="cbcf5-114">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="cbcf5-115">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="cbcf5-116">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="cbcf5-117">如果您有多個訂閱，選擇適當 hello 訂閱 hello 資源存在或已支付。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-117">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="cbcf5-118">使用 [az account set](/cli/azure/account#set) 命令來選取您帳戶底下的特定訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-118">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="cbcf5-119">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="cbcf5-119">Create a resource group</span></span>
<span data-ttu-id="cbcf5-120">使用 [az group create](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) 命令來建立 [Azure 資源群組](https://docs.microsoft.com/cli/azure/group#create)。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-120">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) with [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="cbcf5-121">資源群組是在其中以群組方式部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-121">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="cbcf5-122">hello 下列範例會建立名為的資源群組`mycliresource`在 hello`westus`位置。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-122">hello following example creates a resource group named `mycliresource` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="cbcf5-123">建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="cbcf5-123">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="cbcf5-124">建立 Azure 資料庫的 MySQL 伺服器 hello az mysql 伺服器建立命令。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-124">Create an Azure Database for MySQL server with hello az mysql server create command.</span></span> <span data-ttu-id="cbcf5-125">一部伺服器可以管理多個資料庫。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-125">A server can manage multiple databases.</span></span> <span data-ttu-id="cbcf5-126">一般而言，每個專案或每個使用者會使用個別的資料庫。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-126">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="cbcf5-127">hello 下列範例會建立 Azure 資料庫的 MySQL 伺服器位於`westus`hello 資源群組中`mycliresource`名稱`mycliserver`。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-127">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `mycliresource` with name `mycliserver`.</span></span> <span data-ttu-id="cbcf5-128">hello 伺服器具有系統管理員記錄檔中名為`myadmin`和密碼`Password01!`。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-128">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="cbcf5-129">hello 伺服器會透過**基本**效能層和**50** hello 伺服器中的所有 hello 資料庫之間共用的單位。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-129">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="cbcf5-130">您可以個別調整運算和儲存體向上或向下視 hello 應用程式需求而定。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-130">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="cbcf5-131">設定防火牆規則</span><span class="sxs-lookup"><span data-stu-id="cbcf5-131">Configure firewall rule</span></span>
<span data-ttu-id="cbcf5-132">建立 Azure 資料庫與 hello az mysql 伺服器防火牆規則的 MySQL 伺服器層級防火牆規則建立命令。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-132">Create an Azure Database for MySQL server-level firewall rule with hello az mysql server firewall-rule create command.</span></span> <span data-ttu-id="cbcf5-133">伺服器層級防火牆規則允許外部應用程式，例如**mysql**命令列工具或 MySQL Workbench tooconnect tooyour 伺服器透過 hello Azure MySQL 服務防火牆。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-133">A server-level firewall rule allows an external application, such as **mysql** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="cbcf5-134">hello 下列範例會建立預先定義的位址範圍的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-134">hello following example creates a firewall rule for a predefined address range.</span></span> <span data-ttu-id="cbcf5-135">此範例會顯示 hello 整個可能的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-135">This example shows hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a><span data-ttu-id="cbcf5-136">取得 hello 的連接資訊</span><span class="sxs-lookup"><span data-stu-id="cbcf5-136">Get hello connection information</span></span>

<span data-ttu-id="cbcf5-137">tooconnect tooyour 伺服器，您需要 tooprovide 主機資訊和存取認證。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-137">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

<span data-ttu-id="cbcf5-138">hello 結果是以 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-138">hello result is in JSON format.</span></span> <span data-ttu-id="cbcf5-139">請記下 hello **fullyQualifiedDomainName**和**administratorLogin**。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-139">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mycliserver.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mycliresource/providers/Microsoft.DBforMySQL/servers/mycliserver",
  "location": "westus",
  "name": "mycliserver",
  "resourceGroup": "mycliresource",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-toohello-server-using-mysql"></a><span data-ttu-id="cbcf5-140">使用 mysql toohello 伺服器連接</span><span class="sxs-lookup"><span data-stu-id="cbcf5-140">Connect toohello server using mysql</span></span>
<span data-ttu-id="cbcf5-141">使用[mysql 命令列工具](https://dev.mysql.com/doc/refman/5.6/en/mysql.html)tooestablish MySQL 伺服器的連線 tooyour Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-141">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish a connection tooyour Azure Database for MySQL server.</span></span> <span data-ttu-id="cbcf5-142">在此範例中，hello 命令為：</span><span class="sxs-lookup"><span data-stu-id="cbcf5-142">In this example, hello command is:</span></span>
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="cbcf5-143">建立空白資料庫</span><span class="sxs-lookup"><span data-stu-id="cbcf5-143">Create a blank database</span></span>
<span data-ttu-id="cbcf5-144">一旦您已連線的 toohello 伺服器，建立一個空白資料庫。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-144">Once you’re connected toohello server, create a blank database.</span></span>
```sql
mysql> CREATE DATABASE mysampledb;
```

<span data-ttu-id="cbcf5-145">在 hello 提示字元中執行下列命令 tooswitch hello 連線 toothis 新建資料庫的 hello:</span><span class="sxs-lookup"><span data-stu-id="cbcf5-145">At hello prompt, run hello following command tooswitch hello connection toothis newly created database:</span></span>
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="cbcf5-146">Hello 資料庫中建立資料表</span><span class="sxs-lookup"><span data-stu-id="cbcf5-146">Create tables in hello database</span></span>
<span data-ttu-id="cbcf5-147">您現在知道如何 tooconnect toohello Azure 資料庫的 MySQL 資料庫，我們可能會超出如何 toocomplete 某些基本工作。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-147">Now that you know how tooconnect toohello Azure Database for MySQL database, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="cbcf5-148">首先，我們可以建立資料表並在其中載入一些資料。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-148">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="cbcf5-149">我們將建立一個儲存清查資訊的資料表。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-149">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="cbcf5-150">資料載入至 hello 資料表</span><span class="sxs-lookup"><span data-stu-id="cbcf5-150">Load data into hello tables</span></span>
<span data-ttu-id="cbcf5-151">既然我們已有資料表，我們可以在其中插入一些資料。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-151">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="cbcf5-152">在 hello 開啟命令提示字元視窗中，請執行下列查詢 tooinsert hello 某些資料列的資料。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-152">At hello open command prompt window, run hello following query tooinsert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="cbcf5-153">現在您有兩個資料列範例資料插入 hello 您稍早建立的資料表。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-153">Now you have two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="cbcf5-154">查詢和更新 hello 資料表中的 hello 資料</span><span class="sxs-lookup"><span data-stu-id="cbcf5-154">Query and update hello data in hello tables</span></span>
<span data-ttu-id="cbcf5-155">執行 hello hello 資料庫資料表中的下列查詢 tooretrieve 資訊。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-155">Execute hello following query tooretrieve information from hello database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="cbcf5-156">您也可以更新 hello hello 資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-156">You can also update hello data in hello tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="cbcf5-157">當您擷取資料時，取得據以更新 hello 資料列。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-157">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="cbcf5-158">還原資料庫 tooa 前一個點的時間</span><span class="sxs-lookup"><span data-stu-id="cbcf5-158">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="cbcf5-159">想像一下您不小心刪除了這個資料表。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-159">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="cbcf5-160">這是您無法輕易復原的情況。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-160">This is something you cannot easily recover from.</span></span> <span data-ttu-id="cbcf5-161">Azure 的 MySQL 資料庫可讓您 toogo 後 tooany 點時間 hello 上次向上 too35 天並還原時間 tooa 新的伺服器中的這一點。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-161">Azure Database for MySQL allows you toogo back tooany point in time in hello last up too35 days and restore this point in time tooa new server.</span></span> <span data-ttu-id="cbcf5-162">您可以使用這個新的伺服器 toorecover 刪除的資料。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-162">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="cbcf5-163">hello 加入 hello 資料表之前，請遵循步驟還原 hello 範例伺服器 tooa 點。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-163">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

<span data-ttu-id="cbcf5-164">Hello 還原您需要下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="cbcf5-164">For hello Restore you need hello following information:</span></span>

- <span data-ttu-id="cbcf5-165">還原點： 選取在時間點所發生之前 hello 伺服器已變更。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-165">Restore point: Select a point-in-time that occurs before hello server was changed.</span></span> <span data-ttu-id="cbcf5-166">必須大於或等於 toohello 來源資料庫的最舊的備份值。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-166">Must be greater than or equal toohello source database's Oldest backup value.</span></span>
- <span data-ttu-id="cbcf5-167">目標伺服器： 提供新的伺服器名稱，您想要 toorestore</span><span class="sxs-lookup"><span data-stu-id="cbcf5-167">Target server: Provide a new server name you want toorestore to</span></span>
- <span data-ttu-id="cbcf5-168">來源伺服器： 提供您想要從 toorestore 的 hello 伺服器 hello 名稱</span><span class="sxs-lookup"><span data-stu-id="cbcf5-168">Source server: Provide hello name of hello server you want toorestore from</span></span>
- <span data-ttu-id="cbcf5-169">位置： 您無法選取 hello 區域，依預設它是與 hello 來源伺服器相同</span><span class="sxs-lookup"><span data-stu-id="cbcf5-169">Location: You cannot select hello region, by default it is same as hello source server</span></span>

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

<span data-ttu-id="cbcf5-170">toorestore hello 伺服器和[還原 tooa 時間點](./howto-restore-server-portal.md)hello 資料表已刪除之前。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-170">toorestore hello server and [restore tooa point-in-time](./howto-restore-server-portal.md) before hello table was deleted.</span></span> <span data-ttu-id="cbcf5-171">還原伺服器 tooa 不同點時間建立重複的新伺服器與 hello 原始伺服器在您指定的時間點 hello，前提是它在 hello 的保留期限內是您[服務層](./concepts-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="cbcf5-171">Restoring a server tooa different point in time creates a duplicate new server as hello original server as of hello point in time you specify, provided that it is within hello retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbcf5-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cbcf5-172">Next Steps</span></span>
<span data-ttu-id="cbcf5-173">在本教學課程中，您已了解：</span><span class="sxs-lookup"><span data-stu-id="cbcf5-173">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="cbcf5-174">建立適用於 MySQL 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="cbcf5-174">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="cbcf5-175">Hello 伺服器防火牆設定</span><span class="sxs-lookup"><span data-stu-id="cbcf5-175">Configure hello server firewall</span></span>
> * <span data-ttu-id="cbcf5-176">使用[mysql 命令列工具](https://dev.mysql.com/doc/refman/5.6/en/mysql.html)toocreate 資料庫</span><span class="sxs-lookup"><span data-stu-id="cbcf5-176">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate a database</span></span>
> * <span data-ttu-id="cbcf5-177">載入範例資料</span><span class="sxs-lookup"><span data-stu-id="cbcf5-177">Load sample data</span></span>
> * <span data-ttu-id="cbcf5-178">查詢資料</span><span class="sxs-lookup"><span data-stu-id="cbcf5-178">Query data</span></span>
> * <span data-ttu-id="cbcf5-179">更新資料</span><span class="sxs-lookup"><span data-stu-id="cbcf5-179">Update data</span></span>
> * <span data-ttu-id="cbcf5-180">還原資料</span><span class="sxs-lookup"><span data-stu-id="cbcf5-180">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cbcf5-181">適用於 MySQL 的 Azure 資料庫 - Azuer CLI 範例</span><span class="sxs-lookup"><span data-stu-id="cbcf5-181">Azure Database for MySQL - Azure CLI samples</span></span>](./sample-scripts-azure-cli.md)
