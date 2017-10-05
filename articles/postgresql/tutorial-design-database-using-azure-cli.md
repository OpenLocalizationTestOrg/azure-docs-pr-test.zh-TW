---
title: "使用 Azure CLI 來設計您第一個適用於 PostgreSQL 的 Azure 資料庫 | Microsoft Docs"
description: "本教學課程說明如何使用 Azure CLI 來設計您的第一個「適用於 PostgreSQL 的 Azure 資料庫」。"
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
ms.openlocfilehash: cf536fce8925f9173b541b845af25a8d8c38eabd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a><span data-ttu-id="3b288-103">使用 Azure CLI 來設計您第一個適用於 PostgreSQL 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="3b288-103">Design your first Azure Database for PostgreSQL using Azure CLI</span></span> 
<span data-ttu-id="3b288-104">在本教學課程中，您將使用 Azure CLI (命令列介面) 及其他公用程式來學習如何：</span><span class="sxs-lookup"><span data-stu-id="3b288-104">In this tutorial, you use Azure CLI (command-line interface) and other utilities to learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="3b288-105">建立適用於 PostgreSQL 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="3b288-105">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="3b288-106">設定伺服器防火牆</span><span class="sxs-lookup"><span data-stu-id="3b288-106">Configure the server firewall</span></span>
> * <span data-ttu-id="3b288-107">使用 [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) 公用程式來建立資料庫</span><span class="sxs-lookup"><span data-stu-id="3b288-107">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="3b288-108">載入範例資料</span><span class="sxs-lookup"><span data-stu-id="3b288-108">Load sample data</span></span>
> * <span data-ttu-id="3b288-109">查詢資料</span><span class="sxs-lookup"><span data-stu-id="3b288-109">Query data</span></span>
> * <span data-ttu-id="3b288-110">更新資料</span><span class="sxs-lookup"><span data-stu-id="3b288-110">Update data</span></span>
> * <span data-ttu-id="3b288-111">還原資料</span><span class="sxs-lookup"><span data-stu-id="3b288-111">Restore data</span></span>

<span data-ttu-id="3b288-112">您可以在瀏覽器中使用 Azure Cloud Shell 或在自己的電腦上[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli) 以執行本教學課程中的程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="3b288-112">You may use the Azure Cloud Shell in the browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer to run the code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3b288-113">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="3b288-113">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3b288-114">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="3b288-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="3b288-115">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="3b288-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="3b288-116">如果您有多個訂用帳戶，請選擇資源所在或作為計費對象的適當訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3b288-116">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="3b288-117">使用 [az account set](/cli/azure/account#set) 命令來選取您帳戶底下的特定訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="3b288-117">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="3b288-118">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="3b288-118">Create a resource group</span></span>
<span data-ttu-id="3b288-119">使用 [az group create](../azure-resource-manager/resource-group-overview.md) 命令建立 [Azure 資源群組](/cli/azure/group#create)。</span><span class="sxs-lookup"><span data-stu-id="3b288-119">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="3b288-120">資源群組是在其中以群組方式部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="3b288-120">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="3b288-121">下列範例會在 `westus` 位置建立名為 `myresourcegroup` 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3b288-121">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="3b288-122">建立適用於 PostgreSQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="3b288-122">Create an Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="3b288-123">使用 [az postgres server create](/cli/azure/postgres/server#create) 命令來建立[適用於 PostgreSQL 的 Azure 資料庫伺服器](overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3b288-123">Create an [Azure Database for PostgreSQL server](overview.md) using the [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="3b288-124">一個伺服器會包含一組以群組方式管理的資料庫。</span><span class="sxs-lookup"><span data-stu-id="3b288-124">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="3b288-125">下列範例會使用伺服器管理員登入 `mylogin` 在資源群組 `myresourcegroup` 中建立名為 `mypgserver-20170401` 的伺服器。</span><span class="sxs-lookup"><span data-stu-id="3b288-125">The following example creates a server called `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="3b288-126">伺服器的名稱會與 DNS 名稱對應，因此在 Azure 中必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="3b288-126">Name of a server maps to DNS name and is thus required to be globally unique in Azure.</span></span> <span data-ttu-id="3b288-127">將 `<server_admin_password>` 替換成您自己的值。</span><span class="sxs-lookup"><span data-stu-id="3b288-127">Substitute the `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="3b288-128">需要伺服器系統管理員登入以及您在此處指定的密碼，稍後才能在本快速入門中登入伺服器及其資料庫。</span><span class="sxs-lookup"><span data-stu-id="3b288-128">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="3b288-129">請記住或記錄此資訊，以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="3b288-129">Remember or record this information for later use.</span></span>

<span data-ttu-id="3b288-130">根據預設，**postgres** 資料庫會建立在您的伺服器底下。</span><span class="sxs-lookup"><span data-stu-id="3b288-130">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="3b288-131">[postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) 資料庫是要供使用者、公用程式及第三方應用程式使用的預設資料庫。</span><span class="sxs-lookup"><span data-stu-id="3b288-131">The [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="3b288-132">設定伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="3b288-132">Configure a server-level firewall rule</span></span>

<span data-ttu-id="3b288-133">使用 [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) 命令來建立 Azure PostgreSQL 伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="3b288-133">Create an Azure PostgreSQL server-level firewall rule with the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="3b288-134">伺服器層級防火牆規則可允許外部應用程式 (例如 [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) 或 [PgAdmin](https://www.pgadmin.org/)) 穿過 Azure PostgreSQL 服務防火牆連線到您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="3b288-134">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) to connect to your server through the Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="3b288-135">您可以設定一個防火牆規則，來涵蓋能夠從您網路連線的 IP 範圍。</span><span class="sxs-lookup"><span data-stu-id="3b288-135">You can set a firewall rule that covers an IP range to be able to connect from your network.</span></span> <span data-ttu-id="3b288-136">下列範例使用 [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) 來建立某個 IP 位址範圍的防火牆規則 `AllowAllIps`。</span><span class="sxs-lookup"><span data-stu-id="3b288-136">The following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) to create a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="3b288-137">若要開啟所有 IP 位址，請使用 0.0.0.0 作為起始 IP 位址，並使用 255.255.255.255 作為結束位址。</span><span class="sxs-lookup"><span data-stu-id="3b288-137">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="3b288-138">Azure PostgreSQL 伺服器會透過連接埠 5432 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="3b288-138">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="3b288-139">當您從公司網路內進行連線時，網路的防火牆可能不允許透過連接埠 5432 的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="3b288-139">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="3b288-140">請要求您的 IT 部門開啟連接埠 5432，以連線至 Azure SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="3b288-140">Have your IT department open port 5432 to connect to your Azure SQL Database server.</span></span>
>

## <a name="get-the-connection-information"></a><span data-ttu-id="3b288-141">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="3b288-141">Get the connection information</span></span>

<span data-ttu-id="3b288-142">若要連線到您的伺服器，您必須提供主機資訊和存取認證。</span><span class="sxs-lookup"><span data-stu-id="3b288-142">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="3b288-143">結果會採用 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="3b288-143">The result is in JSON format.</span></span> <span data-ttu-id="3b288-144">請記下 **administratorLogin** 和 **fullyQualifiedDomainName**。</span><span class="sxs-lookup"><span data-stu-id="3b288-144">Make a note of the **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-to-azure-database-for-postgresql-database-using-psql"></a><span data-ttu-id="3b288-145">使用 psql 來連線到適用於 PostgreSQL 資料庫的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="3b288-145">Connect to Azure Database for PostgreSQL database using psql</span></span>
<span data-ttu-id="3b288-146">如果您的用戶端電腦已安裝 PostgreSQL，您可以使用 [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) 的本機執行個體，或 Azure 雲端主控台來連線到 Azure PostgreSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="3b288-146">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), or the Azure Cloud Console to connect to an Azure PostgreSQL server.</span></span> <span data-ttu-id="3b288-147">現在我們將使用 psql 命令列公用程式來連線到「適用於 PostgreSQL 的 Azure 資料庫」伺服器。</span><span class="sxs-lookup"><span data-stu-id="3b288-147">Let's now use the psql command-line utility to connect to the Azure Database for PostgreSQL server.</span></span>

1. <span data-ttu-id="3b288-148">執行下列 psql 命令以連線到「適用於 PostgreSQL 的 Azure 資料庫」伺服器</span><span class="sxs-lookup"><span data-stu-id="3b288-148">Run the following psql command to connect to an Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="3b288-149">例如，下列命令會使用存取認證，連線到 PostgreSQL 伺服器 **mypgserver-20170401.postgres.database.azure.com** 上名為 **postgres** 的預設資料庫。</span><span class="sxs-lookup"><span data-stu-id="3b288-149">For example, the following command connects to the default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="3b288-150">系統提示輸入密碼時，請輸入您選擇的 `<server_admin_password>`。</span><span class="sxs-lookup"><span data-stu-id="3b288-150">Enter the `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  <span data-ttu-id="3b288-151">連線到伺服器後，請在提示字元建立空白資料庫。</span><span class="sxs-lookup"><span data-stu-id="3b288-151">Once you are connected to the server, create a blank database at the prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="3b288-152">在提示字元，執行下列命令以將連線切換到新建立的資料庫 **mypgsqldb**：</span><span class="sxs-lookup"><span data-stu-id="3b288-152">At the prompt, execute the following command to switch connection to the newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="3b288-153">在資料庫中建立資料表</span><span class="sxs-lookup"><span data-stu-id="3b288-153">Create tables in the database</span></span>
<span data-ttu-id="3b288-154">既然您已知道如何連線到「適用於 PostgreSQL 的 Azure 資料庫」，我們可以了解一下如何完成一些基本工作。</span><span class="sxs-lookup"><span data-stu-id="3b288-154">Now that you know how to connect to the Azure Database for PostgreSQL, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="3b288-155">首先，我們可以建立資料表並在其中載入一些資料。</span><span class="sxs-lookup"><span data-stu-id="3b288-155">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="3b288-156">我們將建立一個追蹤清查資訊的資料表。</span><span class="sxs-lookup"><span data-stu-id="3b288-156">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="3b288-157">您現在可以輸入下列命令來查看資料表清單中新建立的資料表：</span><span class="sxs-lookup"><span data-stu-id="3b288-157">You can see the newly created table in the list of tables now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="3b288-158">將資料載入到資料表</span><span class="sxs-lookup"><span data-stu-id="3b288-158">Load data into the tables</span></span>
<span data-ttu-id="3b288-159">既然我們已有資料表，我們可以在其中插入一些資料。</span><span class="sxs-lookup"><span data-stu-id="3b288-159">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="3b288-160">在開啟的命令提示字元視窗，執行下列查詢以插入幾列資料</span><span class="sxs-lookup"><span data-stu-id="3b288-160">At the open command prompt window, run the following query to insert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="3b288-161">您現在已將兩列範例資料插入到先前建立的資料表。</span><span class="sxs-lookup"><span data-stu-id="3b288-161">You have now two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="3b288-162">查詢並更新資料表中的資料</span><span class="sxs-lookup"><span data-stu-id="3b288-162">Query and update the data in the tables</span></span>
<span data-ttu-id="3b288-163">執行下列查詢，以從資料庫資料表中擷取資訊。</span><span class="sxs-lookup"><span data-stu-id="3b288-163">Execute the following query to retrieve information from the database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="3b288-164">您也可以更新資料表中的資料</span><span class="sxs-lookup"><span data-stu-id="3b288-164">You can also update the data in the tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="3b288-165">當您擷取資料時，資料列會相應地更新。</span><span class="sxs-lookup"><span data-stu-id="3b288-165">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="3b288-166">將資料庫還原至先前的時間點</span><span class="sxs-lookup"><span data-stu-id="3b288-166">Restore a database to a previous point in time</span></span>
<span data-ttu-id="3b288-167">假設您不小心刪除了資料表。</span><span class="sxs-lookup"><span data-stu-id="3b288-167">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="3b288-168">這是您無法輕易復原的情況。</span><span class="sxs-lookup"><span data-stu-id="3b288-168">This is something you cannot easily recover from.</span></span> <span data-ttu-id="3b288-169">「適用於 PostgreSQL 的 Azure 資料庫」可讓您返回到任何時間點 (最長可達過去 7 天 (基本) 和 35 天 (標準))，並將此時間點還原到新資料庫。</span><span class="sxs-lookup"><span data-stu-id="3b288-169">Azure Database for PostgreSQL allows you to go back to any point-in-time (in the last up to 7 days (Basic) and 35 days (Standard)) and restore this point-in-time to a new server.</span></span> <span data-ttu-id="3b288-170">您可以使用這個新的伺服器來復原已刪除的資料。</span><span class="sxs-lookup"><span data-stu-id="3b288-170">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="3b288-171">下列步驟會將範例伺服器還原到新增資料表之前的時間點。</span><span class="sxs-lookup"><span data-stu-id="3b288-171">The following steps restore the sample server to a point before the table was added.</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="3b288-172">`az postgres server restore` 命令需要下列參數：</span><span class="sxs-lookup"><span data-stu-id="3b288-172">The `az postgres server restore` command needs the following parameters:</span></span>
| <span data-ttu-id="3b288-173">設定</span><span class="sxs-lookup"><span data-stu-id="3b288-173">Setting</span></span> | <span data-ttu-id="3b288-174">建議的值</span><span class="sxs-lookup"><span data-stu-id="3b288-174">Suggested value</span></span> | <span data-ttu-id="3b288-175">說明</span><span class="sxs-lookup"><span data-stu-id="3b288-175">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="3b288-176">--resource-group</span><span class="sxs-lookup"><span data-stu-id="3b288-176">--resource-group</span></span> |  <span data-ttu-id="3b288-177">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3b288-177">myResourceGroup</span></span> |  <span data-ttu-id="3b288-178">來源伺服器所在的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3b288-178">The resource group in which the source server exists.</span></span>  |
| <span data-ttu-id="3b288-179">--name</span><span class="sxs-lookup"><span data-stu-id="3b288-179">--name</span></span> | <span data-ttu-id="3b288-180">mypgserver-restored</span><span class="sxs-lookup"><span data-stu-id="3b288-180">mypgserver-restored</span></span> | <span data-ttu-id="3b288-181">還原命令所建立之新伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="3b288-181">The name of the new server that is created by the restore command.</span></span> |
| <span data-ttu-id="3b288-182">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="3b288-182">restore-point-in-time</span></span> | <span data-ttu-id="3b288-183">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="3b288-183">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="3b288-184">選取所要還原的時間點。</span><span class="sxs-lookup"><span data-stu-id="3b288-184">Select a point-in-time to restore to.</span></span> <span data-ttu-id="3b288-185">這個日期和時間必須在來源伺服器的備份保留期限內。</span><span class="sxs-lookup"><span data-stu-id="3b288-185">This date and time must be within the source server's backup retention period.</span></span> <span data-ttu-id="3b288-186">請使用 ISO8601 日期和時間格式。</span><span class="sxs-lookup"><span data-stu-id="3b288-186">Use ISO8601 date and time format.</span></span> <span data-ttu-id="3b288-187">例如，您可能會使用您自己的本地時區，例如 `2017-04-13T05:59:00-08:00`，或使用 UTC Zulu 格式 `2017-04-13T13:59:00Z`。</span><span class="sxs-lookup"><span data-stu-id="3b288-187">For example, you may use your own local timezone, such as `2017-04-13T05:59:00-08:00`, or use UTC Zulu format `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="3b288-188">--source-server</span><span class="sxs-lookup"><span data-stu-id="3b288-188">--source-server</span></span> | <span data-ttu-id="3b288-189">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="3b288-189">mypgserver-20170401</span></span> | <span data-ttu-id="3b288-190">要進行還原的來源伺服器之名稱或識別碼。</span><span class="sxs-lookup"><span data-stu-id="3b288-190">The name or ID of the source server to restore from.</span></span> |

<span data-ttu-id="3b288-191">將伺服器還原至時間點可建立新的伺服器，自指定的時間點起複製作為原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="3b288-191">Restoring a server to a point-in-time creates a new server, copying as the original server as of the point in time you specify.</span></span> <span data-ttu-id="3b288-192">還原伺服器的位置與定價層值與來源伺服器相同。</span><span class="sxs-lookup"><span data-stu-id="3b288-192">The location and pricing tier values for the restored server are the same as the source server.</span></span>

<span data-ttu-id="3b288-193">命令是同步的，將會在伺服器還原之後傳回。</span><span class="sxs-lookup"><span data-stu-id="3b288-193">The command is synchronous, and will return after the server is restored.</span></span> <span data-ttu-id="3b288-194">一旦還原完成時，找出所建立的新伺服器。</span><span class="sxs-lookup"><span data-stu-id="3b288-194">Once the restore finishes, locate the new server that was created.</span></span> <span data-ttu-id="3b288-195">請確認資料已如預期般還原。</span><span class="sxs-lookup"><span data-stu-id="3b288-195">Verify the data was restored as expected.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3b288-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3b288-196">Next steps</span></span>
<span data-ttu-id="3b288-197">在本教學課程中，您已了解如何使用 Azure CLI (命令列介面) 及其他公用程式來：</span><span class="sxs-lookup"><span data-stu-id="3b288-197">In this tutorial, you learned how to use Azure CLI (command-line interface) and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="3b288-198">建立適用於 PostgreSQL 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="3b288-198">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="3b288-199">設定伺服器防火牆</span><span class="sxs-lookup"><span data-stu-id="3b288-199">Configure the server firewall</span></span>
> * <span data-ttu-id="3b288-200">使用 [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) 公用程式來建立資料庫</span><span class="sxs-lookup"><span data-stu-id="3b288-200">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="3b288-201">載入範例資料</span><span class="sxs-lookup"><span data-stu-id="3b288-201">Load sample data</span></span>
> * <span data-ttu-id="3b288-202">查詢資料</span><span class="sxs-lookup"><span data-stu-id="3b288-202">Query data</span></span>
> * <span data-ttu-id="3b288-203">更新資料</span><span class="sxs-lookup"><span data-stu-id="3b288-203">Update data</span></span>
> * <span data-ttu-id="3b288-204">還原資料</span><span class="sxs-lookup"><span data-stu-id="3b288-204">Restore data</span></span>

<span data-ttu-id="3b288-205">接著，了解如何使用 Azure 入口網站來執行類似的工作，請檢閱此教學課程：[使用 Azure 入口網站來設計您第一個適用於 PostgreSQL 的 Azure 資料庫](tutorial-design-database-using-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="3b288-205">Next, learn how to use the Azure portal to do similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using the Azure portal](tutorial-design-database-using-azure-portal.md)</span></span>
