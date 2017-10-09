---
title: "建立 Azure 資料庫，使用 Azure CLI hello PostgreSQL |Microsoft 文件"
description: "快速啟動指南 toocreate 並管理 PostgreSQL 伺服器使用 Azure CLI （命令列介面） 的 Azure 資料庫。"
services: postgresql
author: sanagama
ms.author: sanagama
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 06/13/2017
ms.openlocfilehash: 946aa3cbf5ff9f5ac4e51248412d3da5d718141e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-using-hello-azure-cli"></a><span data-ttu-id="26efb-103">建立 Azure 資料庫，使用 Azure CLI hello PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="26efb-103">Create an Azure Database for PostgreSQL using hello Azure CLI</span></span>
<span data-ttu-id="26efb-104">Azure PostgreSQL 資料庫是受管理的服務，可讓您 toorun、 管理及調整 hello 雲端中的高可用性 PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="26efb-104">Azure Database for PostgreSQL is a managed service that enables you toorun, manage, and scale highly available PostgreSQL databases in hello cloud.</span></span> <span data-ttu-id="26efb-105">hello Azure CLI 會使用的 toocreate 和管理 Azure 資源，從 hello 命令列或指令碼中。</span><span class="sxs-lookup"><span data-stu-id="26efb-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="26efb-106">本快速入門示範如何 toocreate Azure 資料庫中的 PostgreSQL 伺服器[Azure 資源群組](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)使用 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="26efb-106">This quickstart shows you how toocreate an Azure Database for PostgreSQL server in an [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) using hello Azure CLI.</span></span>

<span data-ttu-id="26efb-107">如果您沒有 Azure 訂用帳戶，請在開始前建立[免費帳戶](https://azure.microsoft.com/free/) 。</span><span class="sxs-lookup"><span data-stu-id="26efb-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="26efb-108">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="26efb-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="26efb-109">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="26efb-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="26efb-110">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="26efb-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="26efb-111">如果您有多個訂閱，請選擇 計費 hello 資源 hello 適當訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="26efb-111">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource will be billed.</span></span> <span data-ttu-id="26efb-112">使用 [az account set](/cli/azure/account#set) 命令來選取您帳戶底下的特定訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="26efb-112">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="26efb-113">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="26efb-113">Create a resource group</span></span>

<span data-ttu-id="26efb-114">建立[Azure 資源群組](../azure-resource-manager/resource-group-overview.md)使用 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="26efb-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="26efb-115">資源群組是在其中以群組方式部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="26efb-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="26efb-116">hello 下列範例會建立名為的資源群組`myresourcegroup`在 hello`westus`位置。</span><span class="sxs-lookup"><span data-stu-id="26efb-116">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="26efb-117">建立適用於 PostgreSQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="26efb-117">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="26efb-118">建立[PostgreSQL server 的 Azure 資料庫](overview.md)使用 hello [az postgres 伺服器建立](/cli/azure/postgres/server#create)命令。</span><span class="sxs-lookup"><span data-stu-id="26efb-118">Create an [Azure Database for PostgreSQL server](overview.md) using hello [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="26efb-119">一個伺服器會包含一組以群組方式管理的資料庫。</span><span class="sxs-lookup"><span data-stu-id="26efb-119">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="26efb-120">hello 下列範例會建立一個名為伺服器`mypgserver-20170401`資源群組中`myresourcegroup`與伺服器系統管理員登入`mylogin`。</span><span class="sxs-lookup"><span data-stu-id="26efb-120">hello following example creates a server named `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="26efb-121">伺服器 hello 名稱 tooDNS 名稱對應，因此在 Azure 中全域唯一的必要的 toobe。</span><span class="sxs-lookup"><span data-stu-id="26efb-121">hello name of a server maps tooDNS name and is thus required toobe globally unique in Azure.</span></span> <span data-ttu-id="26efb-122">替代 hello`<server_admin_password>`與您自己的值。</span><span class="sxs-lookup"><span data-stu-id="26efb-122">Substitute hello `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="26efb-123">hello 伺服器系統管理員登入和密碼，您在此處指定為 toohello server 中的必要的 toolog 和其資料庫，稍後在這個快速入門。</span><span class="sxs-lookup"><span data-stu-id="26efb-123">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="26efb-124">請記住或記錄此資訊，以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="26efb-124">Remember or record this information for later use.</span></span>

<span data-ttu-id="26efb-125">根據預設，**postgres** 資料庫會建立在您的伺服器底下。</span><span class="sxs-lookup"><span data-stu-id="26efb-125">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="26efb-126">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html)資料庫是適用於由使用者、 公用程式及協力廠商應用程式的預設資料庫。</span><span class="sxs-lookup"><span data-stu-id="26efb-126">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="26efb-127">設定伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="26efb-127">Configure a server-level firewall rule</span></span>

<span data-ttu-id="26efb-128">建立 Azure PostgreSQL 伺服器層級防火牆規則以 hello [az postgres 伺服器防火牆規則建立](/cli/azure/postgres/server/firewall-rule#create)命令。</span><span class="sxs-lookup"><span data-stu-id="26efb-128">Create an Azure PostgreSQL server-level firewall rule with hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="26efb-129">伺服器層級防火牆規則允許外部應用程式，例如[psql](https://www.postgresql.org/docs/9.2/static/app-psql.html)或[PgAdmin](https://www.pgadmin.org/) tooconnect tooyour 伺服器透過 hello Azure PostgreSQL 服務防火牆。</span><span class="sxs-lookup"><span data-stu-id="26efb-129">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server through hello Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="26efb-130">您可以設定防火牆規則，它涵蓋了 IP 範圍 toobe 無法 tooconnect 從您的網路。</span><span class="sxs-lookup"><span data-stu-id="26efb-130">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span> <span data-ttu-id="26efb-131">hello 下列範例會使用[az postgres 伺服器防火牆規則建立](/cli/azure/postgres/server/firewall-rule#create)toocreate 防火牆規則`AllowAllIps`ip 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="26efb-131">hello following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) toocreate a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="26efb-132">tooopen 所有 IP 位址，都作為 hello 起始 IP 位址和 255.255.255.255 hello 結束位址為 0.0.0.0。</span><span class="sxs-lookup"><span data-stu-id="26efb-132">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="26efb-133">Azure PostgreSQL 伺服器會透過連接埠 5432 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="26efb-133">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="26efb-134">當您從公司網路內進行連線時，網路的防火牆可能不允許透過連接埠 5432 的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="26efb-134">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="26efb-135">具有您開啟通訊埠 5432 tooconnect tooyour Azure SQL Database 伺服器的 IT 部門。</span><span class="sxs-lookup"><span data-stu-id="26efb-135">Have your IT department open port 5432 tooconnect tooyour Azure SQL Database server.</span></span>

## <a name="get-hello-connection-information"></a><span data-ttu-id="26efb-136">取得 hello 的連接資訊</span><span class="sxs-lookup"><span data-stu-id="26efb-136">Get hello connection information</span></span>

<span data-ttu-id="26efb-137">tooconnect tooyour 伺服器，您需要 tooprovide 主機資訊和存取認證。</span><span class="sxs-lookup"><span data-stu-id="26efb-137">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="26efb-138">hello 結果是以 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="26efb-138">hello result is in JSON format.</span></span> <span data-ttu-id="26efb-139">請記下 hello **administratorLogin**和**fullyQualifiedDomainName**。</span><span class="sxs-lookup"><span data-stu-id="26efb-139">Make a note of hello **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-toopostgresql-database-using-psql"></a><span data-ttu-id="26efb-140">連接使用 psql tooPostgreSQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="26efb-140">Connect tooPostgreSQL database using psql</span></span>

<span data-ttu-id="26efb-141">如果您的用戶端電腦已安裝的 PostgreSQL，您可以使用的本機執行個體[psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="26efb-141">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL server.</span></span> <span data-ttu-id="26efb-142">我們現在使用 hello psql 命令列公用程式 tooconnect toohello Azure PostgreSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="26efb-142">Let's now use hello psql command-line utility tooconnect toohello Azure PostgreSQL server.</span></span>

1. <span data-ttu-id="26efb-143">執行下列 psql 命令 tooconnect tooan Azure Database PostgreSQL 伺服器 hello</span><span class="sxs-lookup"><span data-stu-id="26efb-143">Run hello following psql command tooconnect tooan Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="26efb-144">比方說，下列命令的 hello 連接 toohello 預設資料庫呼叫**postgres** PostgreSQL 伺服器上**mypgserver 20170401.postgres.database.azure.com**使用存取認證。</span><span class="sxs-lookup"><span data-stu-id="26efb-144">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="26efb-145">輸入 hello`<server_admin_password>`您選擇當系統提示您輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="26efb-145">Enter hello `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  <span data-ttu-id="26efb-146">一旦您已連線的 toohello 伺服器，建立一個空白資料庫在 hello 提示字元。</span><span class="sxs-lookup"><span data-stu-id="26efb-146">Once you are connected toohello server, create a blank database at hello prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="26efb-147">在 hello 提示字元中執行下列命令 tooswitch 連線 toohello 新建資料庫的 hello **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="26efb-147">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="connect-toopostgresql-database-using-pgadmin"></a><span data-ttu-id="26efb-148">連接使用 pgAdmin tooPostgreSQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="26efb-148">Connect tooPostgreSQL database using pgAdmin</span></span>

<span data-ttu-id="26efb-149">使用 hello GUI 工具 tooconnect tooAzure PostgreSQL 伺服器_pgAdmin_</span><span class="sxs-lookup"><span data-stu-id="26efb-149">tooconnect tooAzure PostgreSQL server using hello GUI tool _pgAdmin_</span></span>
1.  <span data-ttu-id="26efb-150">啟動 hello _pgAdmin_應用程式用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="26efb-150">Launch hello _pgAdmin_ application on your client computer.</span></span> <span data-ttu-id="26efb-151">您可以從 http://www.pgadmin.org/ 安裝 _pgAdmin_。</span><span class="sxs-lookup"><span data-stu-id="26efb-151">You can install _pgAdmin_ from http://www.pgadmin.org/.</span></span>
2.  <span data-ttu-id="26efb-152">選擇**新增伺服器**從 hello**快速連結**功能表。</span><span class="sxs-lookup"><span data-stu-id="26efb-152">Choose **Add New Server** from hello **Quick Links** menu.</span></span>
3.  <span data-ttu-id="26efb-153">在 hello**建立-伺服器**對話方塊**一般**索引標籤上，輸入 hello 伺服器的唯一易記名稱。</span><span class="sxs-lookup"><span data-stu-id="26efb-153">In hello **Create - Server** dialog box **General** tab, enter a unique friendly Name for hello server.</span></span> <span data-ttu-id="26efb-154">例如 **Azure PostgreSQL 伺服器**。</span><span class="sxs-lookup"><span data-stu-id="26efb-154">Say **Azure PostgreSQL Server**.</span></span>
 <span data-ttu-id="26efb-155">![pgAdmin 工具 - 建立 - 伺服器](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span><span class="sxs-lookup"><span data-stu-id="26efb-155">![pgAdmin tool - create - server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span></span>
4.  <span data-ttu-id="26efb-156">在 [hello**建立-伺服器**對話方塊中，**連接**] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="26efb-156">In hello **Create - Server** dialog box, **Connection** tab:</span></span>
    - <span data-ttu-id="26efb-157">輸入 hello 完整的伺服器名稱 (例如， **mypgserver 20170401.postgres.database.azure.com**) 在 hello**主機名稱 / 位址**方塊。</span><span class="sxs-lookup"><span data-stu-id="26efb-157">Enter hello fully qualified server name (for example, **mypgserver-20170401.postgres.database.azure.com**) in hello **Host Name/ Address** box.</span></span> 
    - <span data-ttu-id="26efb-158">輸入連接埠 5432 hello**連接埠**方塊。</span><span class="sxs-lookup"><span data-stu-id="26efb-158">Enter port 5432 into hello **Port** box.</span></span> 
    - <span data-ttu-id="26efb-159">輸入 hello **Server 系統管理員登入 (user@mypgserver)**稍早在此快速入門和您建立 hello hello 伺服器時輸入的密碼取得**Username**和**密碼**方塊中分別。</span><span class="sxs-lookup"><span data-stu-id="26efb-159">Enter hello **Server admin login (user@mypgserver)** obtained earlier in this quickstart and password you entered when you created hello server into hello **Username** and **Password** boxes, respectively.</span></span>
    - <span data-ttu-id="26efb-160">將 [SSL 模式] 選取為 [必要]。</span><span class="sxs-lookup"><span data-stu-id="26efb-160">Select **SSL Mode** as **Require**.</span></span> <span data-ttu-id="26efb-161">根據預設，所有的 Azure PostgreSQL 伺服器建立時都會開啟強制使用 SSL。</span><span class="sxs-lookup"><span data-stu-id="26efb-161">By default, all Azure PostgreSQL servers are created with SSL enforcing turned ON.</span></span> <span data-ttu-id="26efb-162">tooturn 關閉 SSL 強制執行，請參閱詳細資料中的[強制 SSL](./concepts-ssl-connection-security.md)。</span><span class="sxs-lookup"><span data-stu-id="26efb-162">tooturn OFF SSL enforcing, see details in [Enforcing SSL](./concepts-ssl-connection-security.md).</span></span>

    ![pgAdmin - 建立 - 伺服器](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  <span data-ttu-id="26efb-164">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="26efb-164">Click **Save**.</span></span>
6.  <span data-ttu-id="26efb-165">Hello 瀏覽器左窗格中，展開 hello**伺服器群組**。</span><span class="sxs-lookup"><span data-stu-id="26efb-165">In hello Browser left pane, expand hello **Server Groups**.</span></span> <span data-ttu-id="26efb-166">選擇您的伺服器 [Azure PostgreSQL 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="26efb-166">Choose your server **Azure PostgreSQL Server**.</span></span>
7.  <span data-ttu-id="26efb-167">選擇 hello**伺服器**您連線到，並選擇 **資料庫**其下。</span><span class="sxs-lookup"><span data-stu-id="26efb-167">Choose hello **Server** you connected to, and then choose **Databases** under it.</span></span> 
8.  <span data-ttu-id="26efb-168">以滑鼠右鍵按一下**資料庫**tooCreate 資料庫。</span><span class="sxs-lookup"><span data-stu-id="26efb-168">Right-click on **Databases** tooCreate a Database.</span></span>
9.  <span data-ttu-id="26efb-169">選擇資料庫名稱**mypgsqldb**和 hello 擁有者，做為伺服器系統管理員登入**mylogin**。</span><span class="sxs-lookup"><span data-stu-id="26efb-169">Choose a database name **mypgsqldb** and hello owner for it as server admin login **mylogin**.</span></span>
10. <span data-ttu-id="26efb-170">按一下**儲存**toocreate 空白資料庫。</span><span class="sxs-lookup"><span data-stu-id="26efb-170">Click **Save** toocreate a blank database.</span></span>
11. <span data-ttu-id="26efb-171">在 hello**瀏覽器**，依序展開 hello**伺服器**群組。</span><span class="sxs-lookup"><span data-stu-id="26efb-171">In hello **Browser**, expand hello **Servers** group.</span></span> <span data-ttu-id="26efb-172">展開您所建立的 hello 伺服器，並查看 hello 資料庫**mypgsqldb**其下。</span><span class="sxs-lookup"><span data-stu-id="26efb-172">Expand hello server you created, and see hello database **mypgsqldb** under it.</span></span>
 <span data-ttu-id="26efb-173">![pgAdmin - 建立 - 資料庫](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span><span class="sxs-lookup"><span data-stu-id="26efb-173">![pgAdmin - Create - Database](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="26efb-174">清除資源</span><span class="sxs-lookup"><span data-stu-id="26efb-174">Clean up resources</span></span>

<span data-ttu-id="26efb-175">清除您要建立 hello 快速入門中刪除 hello 的所有資源[Azure 資源群組](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="26efb-175">Clean up all resources you created in hello quickstart by deleting hello [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!TIP]
> <span data-ttu-id="26efb-176">此集合中的其他快速入門會以本快速入門為基礎。</span><span class="sxs-lookup"><span data-stu-id="26efb-176">Other quickstarts in this collection build upon this quick start.</span></span> <span data-ttu-id="26efb-177">如果您計劃與後續 toowork toocontinue 快速入門，無法清除不要 hello 建立本快速入門的資源。</span><span class="sxs-lookup"><span data-stu-id="26efb-177">If you plan toocontinue on toowork with subsequent quickstarts, do not clean up hello resources created in this quickstart.</span></span> <span data-ttu-id="26efb-178">如果您不打算 toocontinue，使用下列步驟 toodelete hello 本快速入門中 hello Azure CLI 所建立的所有資源。</span><span class="sxs-lookup"><span data-stu-id="26efb-178">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quickstart in hello Azure CLI.</span></span>

```azurecli-interactive
az group delete --name myresourcegroup
```

<span data-ttu-id="26efb-179">如果您想要 toodelete hello 一個新建立的伺服器，您可以執行[az postgres 伺服器刪除](/cli/azure/postgres/server#delete)命令。</span><span class="sxs-lookup"><span data-stu-id="26efb-179">If you just would like toodelete hello one newly created server, you can run [az postgres server delete](/cli/azure/postgres/server#delete) command.</span></span>
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a><span data-ttu-id="26efb-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="26efb-180">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="26efb-181">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="26efb-181">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
