---
title: "設計您第一個適用於 MySQL 資料庫的 Azure 資料庫 - Azure CLI | Microsoft Docs"
description: "本教學課程說明如何使用 Azure CLI 2.0 從命令列建立和管理 Azure Database for MySQL 伺服器和資料庫。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 590cba6cb58d0c0eaedb9f122ac048c33988004d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="261bd-103">設計您第一個適用於 MySQL 資料庫的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="261bd-103">Design your first Azure Database for MySQL database</span></span>

<span data-ttu-id="261bd-104">「適用於 MySQL 的 Azure 資料庫」是 Microsoft 雲端中以 MySQL Community Edition 資料庫引擎為基礎的關聯式資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="261bd-104">Azure Database for MySQL is a relational database service in the Microsoft cloud based on MySQL Community Edition database engine.</span></span> <span data-ttu-id="261bd-105">在本教學課程中，您將使用 Azure CLI (命令列介面) 及其他公用程式來學習如何：</span><span class="sxs-lookup"><span data-stu-id="261bd-105">In this tutorial, you use Azure CLI (command-line interface) and other utilities to learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="261bd-106">建立適用於 MySQL 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="261bd-106">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="261bd-107">設定伺服器防火牆</span><span class="sxs-lookup"><span data-stu-id="261bd-107">Configure the server firewall</span></span>
> * <span data-ttu-id="261bd-108">使用 [mysql 命令列工具](https://dev.mysql.com/doc/refman/5.6/en/mysql.html)來建立資料庫</span><span class="sxs-lookup"><span data-stu-id="261bd-108">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to create a database</span></span>
> * <span data-ttu-id="261bd-109">載入範例資料</span><span class="sxs-lookup"><span data-stu-id="261bd-109">Load sample data</span></span>
> * <span data-ttu-id="261bd-110">查詢資料</span><span class="sxs-lookup"><span data-stu-id="261bd-110">Query data</span></span>
> * <span data-ttu-id="261bd-111">更新資料</span><span class="sxs-lookup"><span data-stu-id="261bd-111">Update data</span></span>
> * <span data-ttu-id="261bd-112">還原資料</span><span class="sxs-lookup"><span data-stu-id="261bd-112">Restore data</span></span>

<span data-ttu-id="261bd-113">您可以在瀏覽器中使用 Azure Cloud Shell 或在自己的電腦上[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli) 以執行本教學課程中的程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="261bd-113">You may use the Azure Cloud Shell in the browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer to run the code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="261bd-114">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="261bd-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="261bd-115">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="261bd-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="261bd-116">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="261bd-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="261bd-117">如果您有多個訂用帳戶，請選擇資源所在或作為計費對象的適當訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="261bd-117">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="261bd-118">使用 [az account set](/cli/azure/account#set) 命令來選取您帳戶底下的特定訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="261bd-118">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="261bd-119">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="261bd-119">Create a resource group</span></span>
<span data-ttu-id="261bd-120">使用 [az group create](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) 命令來建立 [Azure 資源群組](https://docs.microsoft.com/cli/azure/group#create)。</span><span class="sxs-lookup"><span data-stu-id="261bd-120">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) with [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="261bd-121">資源群組是在其中以群組方式部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="261bd-121">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="261bd-122">下列範例會在 `westus` 位置建立名為 `mycliresource` 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="261bd-122">The following example creates a resource group named `mycliresource` in the `westus` location.</span></span>

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="261bd-123">建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="261bd-123">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="261bd-124">使用 az mysql server create 命令來建立「適用於 MySQL 的 Azure 資料庫」伺服器。</span><span class="sxs-lookup"><span data-stu-id="261bd-124">Create an Azure Database for MySQL server with the az mysql server create command.</span></span> <span data-ttu-id="261bd-125">一部伺服器可以管理多個資料庫。</span><span class="sxs-lookup"><span data-stu-id="261bd-125">A server can manage multiple databases.</span></span> <span data-ttu-id="261bd-126">一般而言，每個專案或每個使用者會使用個別的資料庫。</span><span class="sxs-lookup"><span data-stu-id="261bd-126">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="261bd-127">下列範例會在資源群組 `mycliresource` 的 `westus` 中建立名稱為 `mycliserver` 的「適用於 MySQL 的 Azure 資料庫」伺服器。</span><span class="sxs-lookup"><span data-stu-id="261bd-127">The following example creates an Azure Database for MySQL server located in `westus` in the resource group `mycliresource` with name `mycliserver`.</span></span> <span data-ttu-id="261bd-128">此伺服器具有一個名為 `myadmin` 且密碼為 `Password01!` 的系統管理員登入。</span><span class="sxs-lookup"><span data-stu-id="261bd-128">The server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="261bd-129">建立的伺服器為 [基本] 效能層級，並有 **50** 個計算單位在伺服器中的所有資料庫之間共用。</span><span class="sxs-lookup"><span data-stu-id="261bd-129">The server is created with **Basic** performance tier and **50** compute units shared between all the databases in the server.</span></span> <span data-ttu-id="261bd-130">您可以視應用程式需求而定，相應增加或減少計算和儲存體規模。</span><span class="sxs-lookup"><span data-stu-id="261bd-130">You can scale compute and storage up or down depending on the application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="261bd-131">設定防火牆規則</span><span class="sxs-lookup"><span data-stu-id="261bd-131">Configure firewall rule</span></span>
<span data-ttu-id="261bd-132">使用 az mysql server firewall-rule create 命令來建立「適用於 MySQL 的 Azure 資料庫」伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="261bd-132">Create an Azure Database for MySQL server-level firewall rule with the az mysql server firewall-rule create command.</span></span> <span data-ttu-id="261bd-133">伺服器層級防火牆規則可允許外部應用程式 (例如 **mysql** 命令列工具或 MySQL Workbench) 穿過 Azure MySQL 服務防火牆連線到您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="261bd-133">A server-level firewall rule allows an external application, such as **mysql** command-line tool or MySQL Workbench to connect to your server through the Azure MySQL service firewall.</span></span> 

<span data-ttu-id="261bd-134">下列範例會針對一個預先定義的位址範圍建立防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="261bd-134">The following example creates a firewall rule for a predefined address range.</span></span> <span data-ttu-id="261bd-135">此範例會顯示整個可能的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="261bd-135">This example shows the entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-the-connection-information"></a><span data-ttu-id="261bd-136">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="261bd-136">Get the connection information</span></span>

<span data-ttu-id="261bd-137">若要連線到您的伺服器，您必須提供主機資訊和存取認證。</span><span class="sxs-lookup"><span data-stu-id="261bd-137">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

<span data-ttu-id="261bd-138">結果會採用 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="261bd-138">The result is in JSON format.</span></span> <span data-ttu-id="261bd-139">請記下 **fullyQualifiedDomainName** 和 **administratorLogin**。</span><span class="sxs-lookup"><span data-stu-id="261bd-139">Make a note of the **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
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

## <a name="connect-to-the-server-using-mysql"></a><span data-ttu-id="261bd-140">使用 mysql 來連線到伺服器</span><span class="sxs-lookup"><span data-stu-id="261bd-140">Connect to the server using mysql</span></span>
<span data-ttu-id="261bd-141">使用 [mysql 命令列工具](https://dev.mysql.com/doc/refman/5.6/en/mysql.html)來建立對「適用於 MySQL 的 Azure 資料庫」伺服器的連線。</span><span class="sxs-lookup"><span data-stu-id="261bd-141">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to establish a connection to your Azure Database for MySQL server.</span></span> <span data-ttu-id="261bd-142">在此範例中，命令是：</span><span class="sxs-lookup"><span data-stu-id="261bd-142">In this example, the command is:</span></span>
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="261bd-143">建立空白資料庫</span><span class="sxs-lookup"><span data-stu-id="261bd-143">Create a blank database</span></span>
<span data-ttu-id="261bd-144">連線到伺服器之後，請建立一個空白資料庫。</span><span class="sxs-lookup"><span data-stu-id="261bd-144">Once you’re connected to the server, create a blank database.</span></span>
```sql
mysql> CREATE DATABASE mysampledb;
```

<span data-ttu-id="261bd-145">在提示字元，執行下列命令以將連線切換到這個新建立的資料庫：</span><span class="sxs-lookup"><span data-stu-id="261bd-145">At the prompt, run the following command to switch the connection to this newly created database:</span></span>
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="261bd-146">在資料庫中建立資料表</span><span class="sxs-lookup"><span data-stu-id="261bd-146">Create tables in the database</span></span>
<span data-ttu-id="261bd-147">既然您已知道如何連線到「適用於 MySQL 資料庫的 Azure 資料庫」，我們可以了解一下如何完成一些基本工作。</span><span class="sxs-lookup"><span data-stu-id="261bd-147">Now that you know how to connect to the Azure Database for MySQL database, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="261bd-148">首先，我們可以建立資料表並在其中載入一些資料。</span><span class="sxs-lookup"><span data-stu-id="261bd-148">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="261bd-149">我們將建立一個儲存清查資訊的資料表。</span><span class="sxs-lookup"><span data-stu-id="261bd-149">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="261bd-150">將資料載入到資料表</span><span class="sxs-lookup"><span data-stu-id="261bd-150">Load data into the tables</span></span>
<span data-ttu-id="261bd-151">既然我們已有資料表，我們可以在其中插入一些資料。</span><span class="sxs-lookup"><span data-stu-id="261bd-151">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="261bd-152">在開啟的命令提示字元視窗，執行下列查詢以插入幾列資料。</span><span class="sxs-lookup"><span data-stu-id="261bd-152">At the open command prompt window, run the following query to insert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="261bd-153">您現在已將兩列範例資料插入到先前建立的資料表。</span><span class="sxs-lookup"><span data-stu-id="261bd-153">Now you have two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="261bd-154">查詢並更新資料表中的資料</span><span class="sxs-lookup"><span data-stu-id="261bd-154">Query and update the data in the tables</span></span>
<span data-ttu-id="261bd-155">執行下列查詢，以從資料庫資料表中擷取資訊。</span><span class="sxs-lookup"><span data-stu-id="261bd-155">Execute the following query to retrieve information from the database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="261bd-156">您也可以更新資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="261bd-156">You can also update the data in the tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="261bd-157">當您擷取資料時，資料列會相應地更新。</span><span class="sxs-lookup"><span data-stu-id="261bd-157">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="261bd-158">將資料庫還原至先前的時間點</span><span class="sxs-lookup"><span data-stu-id="261bd-158">Restore a database to a previous point in time</span></span>
<span data-ttu-id="261bd-159">想像一下您不小心刪除了這個資料表。</span><span class="sxs-lookup"><span data-stu-id="261bd-159">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="261bd-160">這是您無法輕易復原的情況。</span><span class="sxs-lookup"><span data-stu-id="261bd-160">This is something you cannot easily recover from.</span></span> <span data-ttu-id="261bd-161">「適用於 MySQL 的 Azure 資料庫」可讓您返回到最長可達過去 35 天內的任何時間點，並將此時間點還原到新伺服器。</span><span class="sxs-lookup"><span data-stu-id="261bd-161">Azure Database for MySQL allows you to go back to any point in time in the last up to 35 days and restore this point in time to a new server.</span></span> <span data-ttu-id="261bd-162">您可以使用這個新的伺服器來復原已刪除的資料。</span><span class="sxs-lookup"><span data-stu-id="261bd-162">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="261bd-163">下列步驟會將範例伺服器還原到新增資料表之前的時間點。</span><span class="sxs-lookup"><span data-stu-id="261bd-163">The following steps restore the sample server to a point before the table was added.</span></span>

<span data-ttu-id="261bd-164">若要進行還原，您需要下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="261bd-164">For the Restore you need the following information:</span></span>

- <span data-ttu-id="261bd-165">還原點：選取在變更伺服器之前的時間點。</span><span class="sxs-lookup"><span data-stu-id="261bd-165">Restore point: Select a point-in-time that occurs before the server was changed.</span></span> <span data-ttu-id="261bd-166">必須大於或等於來源資料庫的最舊備份值。</span><span class="sxs-lookup"><span data-stu-id="261bd-166">Must be greater than or equal to the source database's Oldest backup value.</span></span>
- <span data-ttu-id="261bd-167">目標伺服器︰提供要作為還原目的地的新伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="261bd-167">Target server: Provide a new server name you want to restore to</span></span>
- <span data-ttu-id="261bd-168">來源伺服器︰提供要作為還原來源的伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="261bd-168">Source server: Provide the name of the server you want to restore from</span></span>
- <span data-ttu-id="261bd-169">位置︰您無法選取區域，預設是與來源伺服器相同的區域</span><span class="sxs-lookup"><span data-stu-id="261bd-169">Location: You cannot select the region, by default it is same as the source server</span></span>

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

<span data-ttu-id="261bd-170">還原伺服器並[還原到刪除資料表之前的時間點](./howto-restore-server-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="261bd-170">To restore the server and [restore to a point-in-time](./howto-restore-server-portal.md) before the table was deleted.</span></span> <span data-ttu-id="261bd-171">如果將伺服器還原到不同的時間點，將會從您指定的時間點 (前提是此時間點在您[服務層](./concepts-service-tiers.md)的保留期限內) 開始，建立重複的新伺服器作為原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="261bd-171">Restoring a server to a different point in time creates a duplicate new server as the original server as of the point in time you specify, provided that it is within the retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="261bd-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="261bd-172">Next Steps</span></span>
<span data-ttu-id="261bd-173">在本教學課程中，您已了解：</span><span class="sxs-lookup"><span data-stu-id="261bd-173">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="261bd-174">建立適用於 MySQL 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="261bd-174">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="261bd-175">設定伺服器防火牆</span><span class="sxs-lookup"><span data-stu-id="261bd-175">Configure the server firewall</span></span>
> * <span data-ttu-id="261bd-176">使用 [mysql 命令列工具](https://dev.mysql.com/doc/refman/5.6/en/mysql.html)來建立資料庫</span><span class="sxs-lookup"><span data-stu-id="261bd-176">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to create a database</span></span>
> * <span data-ttu-id="261bd-177">載入範例資料</span><span class="sxs-lookup"><span data-stu-id="261bd-177">Load sample data</span></span>
> * <span data-ttu-id="261bd-178">查詢資料</span><span class="sxs-lookup"><span data-stu-id="261bd-178">Query data</span></span>
> * <span data-ttu-id="261bd-179">更新資料</span><span class="sxs-lookup"><span data-stu-id="261bd-179">Update data</span></span>
> * <span data-ttu-id="261bd-180">還原資料</span><span class="sxs-lookup"><span data-stu-id="261bd-180">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="261bd-181">適用於 MySQL 的 Azure 資料庫 - Azuer CLI 範例</span><span class="sxs-lookup"><span data-stu-id="261bd-181">Azure Database for MySQL - Azure CLI samples</span></span>](./sample-scripts-azure-cli.md)
