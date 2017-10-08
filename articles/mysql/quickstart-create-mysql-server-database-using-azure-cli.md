---
title: "快速入門：建立 Azure Database for MySQL 伺服器 - Azuer CLI | Microsoft Docs"
description: "本快速入門說明如何 toouse 會 hello Azure CLI toocreate Azure 資源群組中的 MySQL server Azure 資料庫。"
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
ms.openlocfilehash: 708d0cce12e812cb464adcf7e83e6f85c196bafe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="19192-103">使用 Azure CLI 建立 Azure Database for MySQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="19192-103">Create an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="19192-104">本快速入門說明如何 toouse hello Azure CLI toocreate Azure 資源群組中的 MySQL server Azure 資料庫在五分鐘內。</span><span class="sxs-lookup"><span data-stu-id="19192-104">This quickstart describes how toouse hello Azure CLI toocreate an Azure Database for MySQL server in an Azure resource group in about five minutes.</span></span> <span data-ttu-id="19192-105">hello Azure CLI 會使用的 toocreate 和管理 Azure 資源，從 hello 命令列或指令碼中。</span><span class="sxs-lookup"><span data-stu-id="19192-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span>

<span data-ttu-id="19192-106">如果您沒有 Azure 訂用帳戶，請在開始前建立[免費帳戶](https://azure.microsoft.com/free/) 。</span><span class="sxs-lookup"><span data-stu-id="19192-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="19192-107">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="19192-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="19192-108">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="19192-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="19192-109">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="19192-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="19192-110">如果您有多個訂閱，選擇適當 hello 訂閱 hello 資源存在或已支付。</span><span class="sxs-lookup"><span data-stu-id="19192-110">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="19192-111">使用 [az account set](/cli/azure/account#set) 命令來選取您帳戶底下的特定訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="19192-111">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="19192-112">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="19192-112">Create a resource group</span></span>
<span data-ttu-id="19192-113">建立[Azure 資源群組](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview)使用 hello [az 群組建立](https://docs.microsoft.com/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="19192-113">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) using hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="19192-114">資源群組是在其中以群組方式部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="19192-114">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="19192-115">hello 下列範例會建立名為的資源群組`myresourcegroup`在 hello`westus`位置。</span><span class="sxs-lookup"><span data-stu-id="19192-115">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="19192-116">建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="19192-116">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="19192-117">建立 MySQL 伺服器的 Azure 資料庫以 hello **az mysql 伺服器建立**命令。</span><span class="sxs-lookup"><span data-stu-id="19192-117">Create an Azure Database for MySQL server with hello **az mysql server create** command.</span></span> <span data-ttu-id="19192-118">一部伺服器可以管理多個資料庫。</span><span class="sxs-lookup"><span data-stu-id="19192-118">A server can manage multiple databases.</span></span> <span data-ttu-id="19192-119">一般而言，每個專案或每個使用者會使用個別的資料庫。</span><span class="sxs-lookup"><span data-stu-id="19192-119">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="19192-120">hello 下列範例會建立 Azure 資料庫的 MySQL 伺服器位於`westus`hello 資源群組中`myresourcegroup`名稱`myserver4demo`。</span><span class="sxs-lookup"><span data-stu-id="19192-120">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `myresourcegroup` with name `myserver4demo`.</span></span> <span data-ttu-id="19192-121">hello 伺服器具有系統管理員記錄檔中名為`myadmin`和密碼`Password01!`。</span><span class="sxs-lookup"><span data-stu-id="19192-121">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="19192-122">hello 伺服器會透過**基本**效能層和**50** hello 伺服器中的所有 hello 資料庫之間共用的單位。</span><span class="sxs-lookup"><span data-stu-id="19192-122">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="19192-123">您可以個別調整運算和儲存體向上或向下視 hello 應用程式需求而定。</span><span class="sxs-lookup"><span data-stu-id="19192-123">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="19192-124">設定防火牆規則</span><span class="sxs-lookup"><span data-stu-id="19192-124">Configure firewall rule</span></span>
<span data-ttu-id="19192-125">建立 Azure 資料庫的 MySQL 伺服器層級防火牆規則使用 hello **az mysql 伺服器防火牆規則建立**命令。</span><span class="sxs-lookup"><span data-stu-id="19192-125">Create an Azure Database for MySQL server-level firewall rule using hello **az mysql server firewall-rule create** command.</span></span> <span data-ttu-id="19192-126">伺服器層級防火牆規則可讓外部應用程式，例如 hello **mysql.exe**命令列工具或 MySQL Workbench tooconnect tooyour 伺服器透過 hello Azure MySQL 服務防火牆。</span><span class="sxs-lookup"><span data-stu-id="19192-126">A server-level firewall rule allows an external application, such as hello **mysql.exe** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="19192-127">hello 下列範例會建立的預先定義的位址範圍，在此範例中是 hello 整個可能的 IP 位址範圍的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="19192-127">hello following example creates a firewall rule for a predefined address range, which in this example is hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a><span data-ttu-id="19192-128">進行 SSL 設定</span><span class="sxs-lookup"><span data-stu-id="19192-128">Configure SSL settings</span></span>
<span data-ttu-id="19192-129">預設會強制執行您的伺服器與用戶端應用程式之間的 SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="19192-129">By default, SSL connections between your server and client applications are enforced.</span></span>  <span data-ttu-id="19192-130">這可確保安全性的 「 移動 」 透過加密 hello 資料流資料 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="19192-130">This ensures security of "in-motion" data by encrypting hello data stream over hello internet.</span></span>  <span data-ttu-id="19192-131">此快速入門更容易 toomake，我們停用您伺服器的 SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="19192-131">toomake this quick start easier, we disable SSL connections for your server.</span></span>  <span data-ttu-id="19192-132">不建議對生產伺服器這麼做。</span><span class="sxs-lookup"><span data-stu-id="19192-132">This is not recommended for production servers.</span></span>  <span data-ttu-id="19192-133">如需詳細資訊，請參閱[設定 SSL 連接，您的應用程式 toosecurely 所連接的 MySQL tooAzure 資料庫](./howto-configure-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="19192-133">For more information, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span>

<span data-ttu-id="19192-134">hello 下列範例會停用強制執行您的 MySQL 伺服器上的 SSL。</span><span class="sxs-lookup"><span data-stu-id="19192-134">hello following example disables enforcing SSL on your MySQL server.</span></span>
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a><span data-ttu-id="19192-135">取得 hello 的連接資訊</span><span class="sxs-lookup"><span data-stu-id="19192-135">Get hello connection information</span></span>

<span data-ttu-id="19192-136">tooconnect tooyour 伺服器，您需要 tooprovide 主機資訊和存取認證。</span><span class="sxs-lookup"><span data-stu-id="19192-136">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

<span data-ttu-id="19192-137">hello 結果是以 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="19192-137">hello result is in JSON format.</span></span> <span data-ttu-id="19192-138">請記下 hello **fullyQualifiedDomainName**和**administratorLogin**。</span><span class="sxs-lookup"><span data-stu-id="19192-138">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
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

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a><span data-ttu-id="19192-139">使用命令列工具的 hello mysql.exe toohello 伺服器連接</span><span class="sxs-lookup"><span data-stu-id="19192-139">Connect toohello server using hello mysql.exe command-line tool</span></span>
<span data-ttu-id="19192-140">使用 hello tooyour 伺服器連接**mysql.exe**命令列工具。</span><span class="sxs-lookup"><span data-stu-id="19192-140">Connect tooyour server using hello **mysql.exe** command-line tool.</span></span> <span data-ttu-id="19192-141">您可以從[這裡](https://dev.mysql.com/downloads/)下載 MySQL，再將它安裝於電腦上。</span><span class="sxs-lookup"><span data-stu-id="19192-141">You can download MySQL from [here](https://dev.mysql.com/downloads/) and install it on your computer.</span></span> <span data-ttu-id="19192-142">而您也可以按一下 hello**試試**程式碼範例，按鈕或 hello`>_`按鈕 hello 上方右側的工具列中 hello Azure 入口網站，並啟動 hello **Azure 雲端殼層**。</span><span class="sxs-lookup"><span data-stu-id="19192-142">Instead you may also click hello **Try It** button on code samples, or hello  `>_` button from hello upper right toolbar in hello Azure portal, and launch hello **Azure Cloud Shell**.</span></span>

<span data-ttu-id="19192-143">輸入 hello 下一個命令：</span><span class="sxs-lookup"><span data-stu-id="19192-143">Type hello next commands:</span></span> 

1. <span data-ttu-id="19192-144">連接伺服器所使用的 toohello **mysql**命令列工具：</span><span class="sxs-lookup"><span data-stu-id="19192-144">Connect toohello server using **mysql** command-line tool:</span></span>
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. <span data-ttu-id="19192-145">檢視伺服器狀態：</span><span class="sxs-lookup"><span data-stu-id="19192-145">View server status:</span></span>
```sql
 mysql> status
```
<span data-ttu-id="19192-146">如果一切順利，hello 命令列工具應該輸出 hello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="19192-146">If everything goes well, hello command-line tool should output hello following text:</span></span>

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome toohello MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.

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
> <span data-ttu-id="19192-147">如需其他命令，請參閱 [MySQL 5.7 參考手冊 - 第 4.5.1 章](https://dev.mysql.com/doc/refman/5.7/en/mysql.html)。</span><span class="sxs-lookup"><span data-stu-id="19192-147">For additional commands, see [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span></span>

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a><span data-ttu-id="19192-148">使用 hello MySQL Workbench GUI 工具 toohello 伺服器連接</span><span class="sxs-lookup"><span data-stu-id="19192-148">Connect toohello server using hello MySQL Workbench GUI tool</span></span>
1.  <span data-ttu-id="19192-149">啟動 hello MySQL Workbench 用戶端電腦上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="19192-149">Launch hello MySQL Workbench application on your client computer.</span></span> <span data-ttu-id="19192-150">您可以從[這裡](https://dev.mysql.com/downloads/workbench/)下載並安裝 MySQL Workbench。</span><span class="sxs-lookup"><span data-stu-id="19192-150">You can download and install MySQL Workbench from [here](https://dev.mysql.com/downloads/workbench/).</span></span>

2.  <span data-ttu-id="19192-151">在 [hello**設定新連線**對話方塊方塊中，輸入下列資訊 hello**參數**] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="19192-151">In hello **Setup New Connection** dialog box, enter hello following information on **Parameters** tab:</span></span>

   ![設定新連線](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| <span data-ttu-id="19192-153">**設定**</span><span class="sxs-lookup"><span data-stu-id="19192-153">**Setting**</span></span> | <span data-ttu-id="19192-154">**建議的值**</span><span class="sxs-lookup"><span data-stu-id="19192-154">**Suggested Value**</span></span> | <span data-ttu-id="19192-155">**說明**</span><span class="sxs-lookup"><span data-stu-id="19192-155">**Description**</span></span> |
|---|---|---|
|   <span data-ttu-id="19192-156">連線名稱</span><span class="sxs-lookup"><span data-stu-id="19192-156">Connection Name</span></span> | <span data-ttu-id="19192-157">我的連線</span><span class="sxs-lookup"><span data-stu-id="19192-157">My Connection</span></span> | <span data-ttu-id="19192-158">指定此連線的標籤 (這可以是任何項目)</span><span class="sxs-lookup"><span data-stu-id="19192-158">Specify a label for this connection (this can be anything)</span></span> |
| <span data-ttu-id="19192-159">連線方式</span><span class="sxs-lookup"><span data-stu-id="19192-159">Connection Method</span></span> | <span data-ttu-id="19192-160">選擇標準 (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="19192-160">choose Standard (TCP/IP)</span></span> | <span data-ttu-id="19192-161">用於 MySQL 的 TCP/IP 通訊協定 tooconnect tooAzure 資料庫 ></span><span class="sxs-lookup"><span data-stu-id="19192-161">Use TCP/IP protocol tooconnect tooAzure Database for MySQL></span></span> |
| <span data-ttu-id="19192-162">主機名稱</span><span class="sxs-lookup"><span data-stu-id="19192-162">Hostname</span></span> | <span data-ttu-id="19192-163">myserver4demo.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="19192-163">myserver4demo.mysql.database.azure.com</span></span> | <span data-ttu-id="19192-164">您先前記下的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="19192-164">Server name you previously noted.</span></span> |
| <span data-ttu-id="19192-165">連接埠</span><span class="sxs-lookup"><span data-stu-id="19192-165">Port</span></span> | <span data-ttu-id="19192-166">3306</span><span class="sxs-lookup"><span data-stu-id="19192-166">3306</span></span> | <span data-ttu-id="19192-167">會使用 MySQL 的 hello 預設通訊埠。</span><span class="sxs-lookup"><span data-stu-id="19192-167">hello default port for MySQL is used.</span></span> |
| <span data-ttu-id="19192-168">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="19192-168">Username</span></span> | myadmin@myserver4demo | <span data-ttu-id="19192-169">hello server 系統管理員登入您先前所述。</span><span class="sxs-lookup"><span data-stu-id="19192-169">hello server admin login you previously noted.</span></span> |
| <span data-ttu-id="19192-170">密碼</span><span class="sxs-lookup"><span data-stu-id="19192-170">Password</span></span> | **** | <span data-ttu-id="19192-171">使用您先前設定的 hello 系統管理員帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="19192-171">Use hello admin account password you configured earlier.</span></span> |

<span data-ttu-id="19192-172">按一下**測試連接**tootest 如果已正確設定所有參數。</span><span class="sxs-lookup"><span data-stu-id="19192-172">Click **Test Connection** tootest if all parameters are correctly configured.</span></span>
<span data-ttu-id="19192-173">現在，您可以按一下 hello 連接 toosuccessfully toohello 伺服器連接。</span><span class="sxs-lookup"><span data-stu-id="19192-173">Now, you can click hello connection toosuccessfully connect toohello server.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="19192-174">清除資源</span><span class="sxs-lookup"><span data-stu-id="19192-174">Clean up resources</span></span>
<span data-ttu-id="19192-175">如果您不需要這些資源，另一個快速入門/教學課程中，您可以刪除它們，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="19192-175">If you don't need these resources for another quickstart/tutorial, you can delete them by doing hello following command:</span></span> 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a><span data-ttu-id="19192-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="19192-176">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="19192-177">使用 Azure CLI 設計 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="19192-177">Design a MySQL Database with Azure CLI</span></span>](./tutorial-design-database-using-cli.md)
