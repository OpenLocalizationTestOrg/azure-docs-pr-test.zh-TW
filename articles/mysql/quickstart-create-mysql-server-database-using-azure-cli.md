---
title: "快速入門：建立 Azure Database for MySQL 伺服器 - Azuer CLI | Microsoft Docs"
description: "本快速入門說明如何使用 Azure CLI 在 Azure 資源群組中建立 Azure Database for MySQL 伺服器。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: hero-article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 04fc441aee7a4c8adc4f02d5e51b2d9e64400f55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="fd5ce-103">使用 Azure CLI 建立 Azure Database for MySQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="fd5ce-103">Create an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="fd5ce-104">本快速入門說明如何使用 Azure CLI，在大約 5 分鐘內於 Azure 資源群組中建立 Azure Database for MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-104">This quickstart describes how to use the Azure CLI to create an Azure Database for MySQL server in an Azure resource group in about five minutes.</span></span> <span data-ttu-id="fd5ce-105">Azure CLI 可用來從命令列或在指令碼中建立和管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span>

<span data-ttu-id="fd5ce-106">如果您沒有 Azure 訂用帳戶，請在開始前建立[免費帳戶](https://azure.microsoft.com/free/) 。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fd5ce-107">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-107">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="fd5ce-108">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="fd5ce-109">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="fd5ce-110">如果您有多個訂用帳戶，請選擇資源所在或作為計費對象的適當訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-110">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="fd5ce-111">使用 [az account set](/cli/azure/account#set) 命令來選取您帳戶底下的特定訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-111">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="fd5ce-112">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="fd5ce-112">Create a resource group</span></span>
<span data-ttu-id="fd5ce-113">使用 [az group create](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) 命令建立 [Azure 資源群組](https://docs.microsoft.com/cli/azure/group#create)。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-113">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) using the [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="fd5ce-114">資源群組是在其中以群組方式部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-114">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="fd5ce-115">下列範例會在 `westus` 位置建立名為 `myresourcegroup` 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-115">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="fd5ce-116">建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="fd5ce-116">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="fd5ce-117">使用 **az mysql server create** 命令建立 Azure Database for MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-117">Create an Azure Database for MySQL server with the **az mysql server create** command.</span></span> <span data-ttu-id="fd5ce-118">一部伺服器可以管理多個資料庫。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-118">A server can manage multiple databases.</span></span> <span data-ttu-id="fd5ce-119">一般而言，每個專案或每個使用者會使用個別的資料庫。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-119">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="fd5ce-120">下列範例會在資源群組 `myresourcegroup` 的 `westus` 中建立名稱為 `myserver4demo` 的「適用於 MySQL 的 Azure 資料庫」伺服器。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-120">The following example creates an Azure Database for MySQL server located in `westus` in the resource group `myresourcegroup` with name `myserver4demo`.</span></span> <span data-ttu-id="fd5ce-121">此伺服器具有一個名為 `myadmin` 且密碼為 `Password01!` 的系統管理員登入。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-121">The server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="fd5ce-122">建立的伺服器為 [基本] 效能層級，並有 **50** 個計算單位在伺服器中的所有資料庫之間共用。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-122">The server is created with **Basic** performance tier and **50** compute units shared between all the databases in the server.</span></span> <span data-ttu-id="fd5ce-123">您可以視應用程式需求而定，相應增加或減少計算和儲存體規模。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-123">You can scale compute and storage up or down depending on the application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="fd5ce-124">設定防火牆規則</span><span class="sxs-lookup"><span data-stu-id="fd5ce-124">Configure firewall rule</span></span>
<span data-ttu-id="fd5ce-125">使用 **az mysql server firewall-rule create** 命令建立 Azure Database for MySQL 伺服器層級的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-125">Create an Azure Database for MySQL server-level firewall rule using the **az mysql server firewall-rule create** command.</span></span> <span data-ttu-id="fd5ce-126">伺服器層級的防火牆規則允許外部應用程式 (例如 **mysql.exe** 命令列工具或 MySQL Workbench) 穿過 Azure MySQL 服務防火牆連線到您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-126">A server-level firewall rule allows an external application, such as the **mysql.exe** command-line tool or MySQL Workbench to connect to your server through the Azure MySQL service firewall.</span></span> 

<span data-ttu-id="fd5ce-127">下列範例會建立適用於預先定義之位址範圍的防火牆規則，在此範例中，這是整個可能的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-127">The following example creates a firewall rule for a predefined address range, which in this example is the entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a><span data-ttu-id="fd5ce-128">進行 SSL 設定</span><span class="sxs-lookup"><span data-stu-id="fd5ce-128">Configure SSL settings</span></span>
<span data-ttu-id="fd5ce-129">預設會強制執行您的伺服器與用戶端應用程式之間的 SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-129">By default, SSL connections between your server and client applications are enforced.</span></span>  <span data-ttu-id="fd5ce-130">這可藉由加密透過網際網路的資料流，確保「移動中」資料的安全性。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-130">This ensures security of "in-motion" data by encrypting the data stream over the internet.</span></span>  <span data-ttu-id="fd5ce-131">為了讓本快速入門更容易進行，我們停用了您伺服器的 SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-131">To make this quick start easier, we disable SSL connections for your server.</span></span>  <span data-ttu-id="fd5ce-132">不建議對生產伺服器這麼做。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-132">This is not recommended for production servers.</span></span>  <span data-ttu-id="fd5ce-133">如需詳細資訊，請參閱[在您的應用程式中設定 SSL 連線能力，以安全地連線至適用於 MySQL 的 Azure 資料庫](./howto-configure-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-133">For more information, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](./howto-configure-ssl.md).</span></span>

<span data-ttu-id="fd5ce-134">下列範例會停用在 MySQL 伺服器上強制執行 SSL。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-134">The following example disables enforcing SSL on your MySQL server.</span></span>
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-the-connection-information"></a><span data-ttu-id="fd5ce-135">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="fd5ce-135">Get the connection information</span></span>

<span data-ttu-id="fd5ce-136">若要連線到您的伺服器，您必須提供主機資訊和存取認證。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-136">To connect to your server, you need to provide host information and access credentials.</span></span>

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

<span data-ttu-id="fd5ce-137">結果會採用 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-137">The result is in JSON format.</span></span> <span data-ttu-id="fd5ce-138">請記下 **fullyQualifiedDomainName** 和 **administratorLogin**。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-138">Make a note of the **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "myserver4demo.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforMySQL/servers/myserver4demo",
  "location": "westus",
  "name": "myserver4demo",
  "resourceGroup": "myresourcegroup",
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

## <a name="connect-to-the-server-using-the-mysqlexe-command-line-tool"></a><span data-ttu-id="fd5ce-139">使用 mysql.exe 命令列工具連線到伺服器</span><span class="sxs-lookup"><span data-stu-id="fd5ce-139">Connect to the server using the mysql.exe command-line tool</span></span>
<span data-ttu-id="fd5ce-140">使用 **mysql.exe** 命令列工具連線到伺服器。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-140">Connect to your server using the **mysql.exe** command-line tool.</span></span> <span data-ttu-id="fd5ce-141">您可以從[這裡](https://dev.mysql.com/downloads/)下載 MySQL，再將它安裝於電腦上。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-141">You can download MySQL from [here](https://dev.mysql.com/downloads/) and install it on your computer.</span></span> <span data-ttu-id="fd5ce-142">相反地，您也可以按一下程式碼範例上的 [試用] 按鈕，或是 Azure 入口網站右上角工具列的 `>_` 按鈕，並啟動 **Azure Cloud Shell**。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-142">Instead you may also click the **Try It** button on code samples, or the  `>_` button from the upper right toolbar in the Azure portal, and launch the **Azure Cloud Shell**.</span></span>

<span data-ttu-id="fd5ce-143">輸入下一個命令：</span><span class="sxs-lookup"><span data-stu-id="fd5ce-143">Type the next commands:</span></span> 

1. <span data-ttu-id="fd5ce-144">使用 **mysql** 命令列工具連線到伺服器︰</span><span class="sxs-lookup"><span data-stu-id="fd5ce-144">Connect to the server using **mysql** command-line tool:</span></span>
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. <span data-ttu-id="fd5ce-145">檢視伺服器狀態：</span><span class="sxs-lookup"><span data-stu-id="fd5ce-145">View server status:</span></span>
```sql
 mysql> status
```
<span data-ttu-id="fd5ce-146">如果一切順利，命令列工具應輸出下列文字︰</span><span class="sxs-lookup"><span data-stu-id="fd5ce-146">If everything goes well, the command-line tool should output the following text:</span></span>

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> status
--------------
mysql  Ver 14.14 Distrib 5.6.35, for Win64 (x86_64)

Connection id:          65512
Current database:
Current user:           myadmin@116.230.243.143
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.6.26.0 MySQL Community Server (GPL)
Protocol version:       10
Connection:             myserver4demo.mysql.database.azure.com via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 2 days 9 hours 47 min 20 sec

Threads: 4  Questions: 34833  Slow queries: 2  Opens: 84  Flush tables: 4  Open tables: 1  Queries per second avg: 0.167
--------------

mysql>
```

> [!TIP]
> <span data-ttu-id="fd5ce-147">如需其他命令，請參閱 [MySQL 5.7 參考手冊 - 第 4.5.1 章](https://dev.mysql.com/doc/refman/5.7/en/mysql.html)。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-147">For additional commands, see [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span></span>

## <a name="connect-to-the-server-using-the-mysql-workbench-gui-tool"></a><span data-ttu-id="fd5ce-148">使用 MySQL Workbench GUI 工具連線到伺服器</span><span class="sxs-lookup"><span data-stu-id="fd5ce-148">Connect to the server using the MySQL Workbench GUI tool</span></span>
1.  <span data-ttu-id="fd5ce-149">在您的用戶端電腦上啟動 MySQL Workbench 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-149">Launch the MySQL Workbench application on your client computer.</span></span> <span data-ttu-id="fd5ce-150">您可以從[這裡](https://dev.mysql.com/downloads/workbench/)下載並安裝 MySQL Workbench。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-150">You can download and install MySQL Workbench from [here](https://dev.mysql.com/downloads/workbench/).</span></span>

2.  <span data-ttu-id="fd5ce-151">在 [設定新連線] 對話方塊的 [參數] 索引標籤上輸入下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="fd5ce-151">In the **Setup New Connection** dialog box, enter the following information on **Parameters** tab:</span></span>

   ![設定新連線](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| <span data-ttu-id="fd5ce-153">**設定**</span><span class="sxs-lookup"><span data-stu-id="fd5ce-153">**Setting**</span></span> | <span data-ttu-id="fd5ce-154">**建議的值**</span><span class="sxs-lookup"><span data-stu-id="fd5ce-154">**Suggested Value**</span></span> | <span data-ttu-id="fd5ce-155">**說明**</span><span class="sxs-lookup"><span data-stu-id="fd5ce-155">**Description**</span></span> |
|---|---|---|
|   <span data-ttu-id="fd5ce-156">連線名稱</span><span class="sxs-lookup"><span data-stu-id="fd5ce-156">Connection Name</span></span> | <span data-ttu-id="fd5ce-157">我的連線</span><span class="sxs-lookup"><span data-stu-id="fd5ce-157">My Connection</span></span> | <span data-ttu-id="fd5ce-158">指定此連線的標籤 (這可以是任何項目)</span><span class="sxs-lookup"><span data-stu-id="fd5ce-158">Specify a label for this connection (this can be anything)</span></span> |
| <span data-ttu-id="fd5ce-159">連線方式</span><span class="sxs-lookup"><span data-stu-id="fd5ce-159">Connection Method</span></span> | <span data-ttu-id="fd5ce-160">選擇標準 (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="fd5ce-160">choose Standard (TCP/IP)</span></span> | <span data-ttu-id="fd5ce-161">使用 TCP/IP 通訊協定來連線到 MySQL> 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="fd5ce-161">Use TCP/IP protocol to connect to Azure Database for MySQL></span></span> |
| <span data-ttu-id="fd5ce-162">主機名稱</span><span class="sxs-lookup"><span data-stu-id="fd5ce-162">Hostname</span></span> | <span data-ttu-id="fd5ce-163">myserver4demo.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="fd5ce-163">myserver4demo.mysql.database.azure.com</span></span> | <span data-ttu-id="fd5ce-164">您先前記下的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-164">Server name you previously noted.</span></span> |
| <span data-ttu-id="fd5ce-165">連接埠</span><span class="sxs-lookup"><span data-stu-id="fd5ce-165">Port</span></span> | <span data-ttu-id="fd5ce-166">3306</span><span class="sxs-lookup"><span data-stu-id="fd5ce-166">3306</span></span> | <span data-ttu-id="fd5ce-167">會使用 MySQL 的預設連接埠。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-167">The default port for MySQL is used.</span></span> |
| <span data-ttu-id="fd5ce-168">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="fd5ce-168">Username</span></span> | myadmin@myserver4demo | <span data-ttu-id="fd5ce-169">先前記下的伺服器管理員登入。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-169">The server admin login you previously noted.</span></span> |
| <span data-ttu-id="fd5ce-170">密碼</span><span class="sxs-lookup"><span data-stu-id="fd5ce-170">Password</span></span> | **** | <span data-ttu-id="fd5ce-171">使用您稍早設定的管理帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-171">Use the admin account password you configured earlier.</span></span> |

<span data-ttu-id="fd5ce-172">按一下 [測試連線] 以測試所有參數是否都已設定正確。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-172">Click **Test Connection** to test if all parameters are correctly configured.</span></span>
<span data-ttu-id="fd5ce-173">您現在可以按一下連線，以成功連線到伺服器。</span><span class="sxs-lookup"><span data-stu-id="fd5ce-173">Now, you can click the connection to successfully connect to the server.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="fd5ce-174">清除資源</span><span class="sxs-lookup"><span data-stu-id="fd5ce-174">Clean up resources</span></span>
<span data-ttu-id="fd5ce-175">如果您不需要這些資源來進行其他快速入門/教學課程，可以執行下列命令加以刪除︰</span><span class="sxs-lookup"><span data-stu-id="fd5ce-175">If you don't need these resources for another quickstart/tutorial, you can delete them by doing the following command:</span></span> 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a><span data-ttu-id="fd5ce-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd5ce-176">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fd5ce-177">使用 Azure CLI 設計 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="fd5ce-177">Design a MySQL Database with Azure CLI</span></span>](./tutorial-design-database-using-cli.md)
