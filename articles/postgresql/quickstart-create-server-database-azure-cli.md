---
title: "使用 Azure CLI 建立 Azure Database for PostgreSQL | Microsoft Docs"
description: "本快速入門指南說明如何使用 Azure CLI (命令列介面) 建立及管理 Azure Database for PostgreSQL 伺服器。"
services: postgresql
author: sanagama
ms.author: sanagama
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 06/13/2017
ms.openlocfilehash: d78243abc140c7b3f0b99bdf56821b7920568550
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-database-for-postgresql-using-the-azure-cli"></a><span data-ttu-id="1a2f5-103">使用 Azure CLI 建立 Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1a2f5-103">Create an Azure Database for PostgreSQL using the Azure CLI</span></span>
<span data-ttu-id="1a2f5-104">Azure Database for PostgreSQL 是一個受管理的服務，可讓您在雲端執行、管理及調整高可用性 PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-104">Azure Database for PostgreSQL is a managed service that enables you to run, manage, and scale highly available PostgreSQL databases in the cloud.</span></span> <span data-ttu-id="1a2f5-105">Azure CLI 可用來從命令列或在指令碼中建立和管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="1a2f5-106">本快速入門說明如何使用 Azure CLI 在 [Azure 資源群組](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)中建立 Azure Database for PostgreSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-106">This quickstart shows you how to create an Azure Database for PostgreSQL server in an [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) using the Azure CLI.</span></span>

<span data-ttu-id="1a2f5-107">如果您沒有 Azure 訂用帳戶，請在開始前建立[免費帳戶](https://azure.microsoft.com/free/) 。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1a2f5-108">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="1a2f5-109">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="1a2f5-110">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="1a2f5-111">如果您有多個訂用帳戶，請選擇資源計費的適當訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-111">If you have multiple subscriptions, choose the appropriate subscription in which the resource will be billed.</span></span> <span data-ttu-id="1a2f5-112">使用 [az account set](/cli/azure/account#set) 命令在您的帳戶之下選取特定訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-112">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="1a2f5-113">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="1a2f5-113">Create a resource group</span></span>

<span data-ttu-id="1a2f5-114">使用 [az group create](../azure-resource-manager/resource-group-overview.md) 命令建立 [Azure 資源群組](/cli/azure/group#create)。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="1a2f5-115">資源群組是在其中以群組方式部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="1a2f5-116">下列範例會在 `westus` 位置建立名為 `myresourcegroup` 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-116">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="1a2f5-117">建立適用於 PostgreSQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="1a2f5-117">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="1a2f5-118">使用 [az postgres server create](/cli/azure/postgres/server#create) 命令來建立[適用於 PostgreSQL 的 Azure 資料庫伺服器](overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-118">Create an [Azure Database for PostgreSQL server](overview.md) using the [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="1a2f5-119">一個伺服器包含一組當作群組管理的資料庫。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-119">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="1a2f5-120">下列範例會使用伺服器管理員登入 `mylogin` 在 `myresourcegroup` 資源群組中建立名為 `mypgserver-20170401` 的伺服器。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-120">The following example creates a server named `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="1a2f5-121">伺服器的名稱會對應至 DNS 名稱，因此必須是 Azure 中全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-121">The name of a server maps to DNS name and is thus required to be globally unique in Azure.</span></span> <span data-ttu-id="1a2f5-122">將 `<server_admin_password>` 替換成您自己的值。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-122">Substitute the `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="1a2f5-123">需要伺服器系統管理員登入以及您在此處指定的密碼，稍後才能在本快速入門中登入伺服器及其資料庫。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-123">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="1a2f5-124">請記住或記錄此資訊，以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-124">Remember or record this information for later use.</span></span>

<span data-ttu-id="1a2f5-125">根據預設，**postgres** 資料庫會建立在您的伺服器底下。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-125">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="1a2f5-126">[postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) 資料庫是要供使用者、公用程式及第三方應用程式使用的預設資料庫。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-126">The [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="1a2f5-127">設定伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="1a2f5-127">Configure a server-level firewall rule</span></span>

<span data-ttu-id="1a2f5-128">使用 [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) 命令來建立 Azure PostgreSQL 伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-128">Create an Azure PostgreSQL server-level firewall rule with the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="1a2f5-129">伺服器層級防火牆規則可允許外部應用程式 (例如 [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) 或 [PgAdmin](https://www.pgadmin.org/)) 穿過 Azure PostgreSQL 服務防火牆連線到您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-129">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) to connect to your server through the Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="1a2f5-130">您可以設定一個防火牆規則，來涵蓋能夠從您網路連線的 IP 範圍。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-130">You can set a firewall rule that covers an IP range to be able to connect from your network.</span></span> <span data-ttu-id="1a2f5-131">下列範例使用 [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) 來建立某個 IP 位址範圍的防火牆規則 `AllowAllIps`。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-131">The following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) to create a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="1a2f5-132">若要開啟所有 IP 位址，請使用 0.0.0.0 作為起始 IP 位址，並使用 255.255.255.255 作為結束位址。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-132">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="1a2f5-133">Azure PostgreSQL 伺服器會透過連接埠 5432 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-133">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="1a2f5-134">當您從公司網路內進行連線時，網路的防火牆可能不允許透過連接埠 5432 的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-134">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="1a2f5-135">請要求您的 IT 部門開啟連接埠 5432，以連線至 Azure SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-135">Have your IT department open port 5432 to connect to your Azure SQL Database server.</span></span>

## <a name="get-the-connection-information"></a><span data-ttu-id="1a2f5-136">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="1a2f5-136">Get the connection information</span></span>

<span data-ttu-id="1a2f5-137">若要連線到您的伺服器，您必須提供主機資訊和存取認證。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-137">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="1a2f5-138">結果會採用 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-138">The result is in JSON format.</span></span> <span data-ttu-id="1a2f5-139">請記下 **administratorLogin** 和 **fullyQualifiedDomainName**。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-139">Make a note of the **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-to-postgresql-database-using-psql"></a><span data-ttu-id="1a2f5-140">使用 psql 連線到 PostgreSQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="1a2f5-140">Connect to PostgreSQL database using psql</span></span>

<span data-ttu-id="1a2f5-141">如果您的用戶端電腦已安裝 PostgreSQL，您可以使用 [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) 的本機執行個體來連線到 Azure PostgreSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-141">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) to connect to an Azure PostgreSQL server.</span></span> <span data-ttu-id="1a2f5-142">現在我們將使用 psql 命令列公用程式來連線到 Azure PostgreSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-142">Let's now use the psql command-line utility to connect to the Azure PostgreSQL server.</span></span>

1. <span data-ttu-id="1a2f5-143">執行下列 psql 命令以連線到「適用於 PostgreSQL 的 Azure 資料庫」伺服器</span><span class="sxs-lookup"><span data-stu-id="1a2f5-143">Run the following psql command to connect to an Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="1a2f5-144">例如，下列命令會使用存取認證，連線到 PostgreSQL 伺服器 **mypgserver-20170401.postgres.database.azure.com** 上名為 **postgres** 的預設資料庫。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-144">For example, the following command connects to the default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="1a2f5-145">系統提示輸入密碼時，請輸入您選擇的 `<server_admin_password>`。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-145">Enter the `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  <span data-ttu-id="1a2f5-146">連線到伺服器後，請在提示字元建立空白資料庫。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-146">Once you are connected to the server, create a blank database at the prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="1a2f5-147">在提示字元，執行下列命令，將連線切換到新建立的資料庫 **mypgsqldb**：</span><span class="sxs-lookup"><span data-stu-id="1a2f5-147">At the prompt, execute the following command to switch connection to the newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="connect-to-postgresql-database-using-pgadmin"></a><span data-ttu-id="1a2f5-148">使用 pgAdmin 連線到 PostgreSQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="1a2f5-148">Connect to PostgreSQL database using pgAdmin</span></span>

<span data-ttu-id="1a2f5-149">若要使用 GUI 工具_pgAdmin_ 連線到 Azure PostgreSQL 伺服器：</span><span class="sxs-lookup"><span data-stu-id="1a2f5-149">To connect to Azure PostgreSQL server using the GUI tool _pgAdmin_</span></span>
1.  <span data-ttu-id="1a2f5-150">在您的用戶端電腦上啟動 _pgAdmin_ 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-150">Launch the _pgAdmin_ application on your client computer.</span></span> <span data-ttu-id="1a2f5-151">您可以從 http://www.pgadmin.org/ 安裝 _pgAdmin_。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-151">You can install _pgAdmin_ from http://www.pgadmin.org/.</span></span>
2.  <span data-ttu-id="1a2f5-152">從 [快速連結] 功能表選擇 [新增伺服器]。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-152">Choose **Add New Server** from the **Quick Links** menu.</span></span>
3.  <span data-ttu-id="1a2f5-153">在 [建立 - 伺服器] 對話方塊的 [一般] 索引標籤上，輸入伺服器的唯一易記名稱。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-153">In the **Create - Server** dialog box **General** tab, enter a unique friendly Name for the server.</span></span> <span data-ttu-id="1a2f5-154">例如 **Azure PostgreSQL 伺服器**。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-154">Say **Azure PostgreSQL Server**.</span></span>
 <span data-ttu-id="1a2f5-155">![pgAdmin 工具 - 建立 - 伺服器](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span><span class="sxs-lookup"><span data-stu-id="1a2f5-155">![pgAdmin tool - create - server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span></span>
4.  <span data-ttu-id="1a2f5-156">在 [建立 - 伺服器] 對話方塊的 [連線] 索引標籤︰</span><span class="sxs-lookup"><span data-stu-id="1a2f5-156">In the **Create - Server** dialog box, **Connection** tab:</span></span>
    - <span data-ttu-id="1a2f5-157">在 [主機名稱/位址] 方塊中輸入完整的伺服器名稱 (例如，**mypgserver-20170401.postgres.database.azure.com**)。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-157">Enter the fully qualified server name (for example, **mypgserver-20170401.postgres.database.azure.com**) in the **Host Name/ Address** box.</span></span> 
    - <span data-ttu-id="1a2f5-158">在 [連接埠] 方塊中輸入連接埠 5432。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-158">Enter port 5432 into the **Port** box.</span></span> 
    - <span data-ttu-id="1a2f5-159">在 [使用者名稱] 和 [密碼] 方塊中，分別輸入稍早在此快速入門中取得的**伺服器管理員登入 (user@mypgserver)** 以及在您建立伺服器時所輸入的密碼。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-159">Enter the **Server admin login (user@mypgserver)** obtained earlier in this quickstart and password you entered when you created the server into the **Username** and **Password** boxes, respectively.</span></span>
    - <span data-ttu-id="1a2f5-160">將 [SSL 模式] 選取為 [必要]。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-160">Select **SSL Mode** as **Require**.</span></span> <span data-ttu-id="1a2f5-161">根據預設，建立所有 Azure PostgreSQL 伺服器時都會開啟 SSL 強制執行。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-161">By default, all Azure PostgreSQL servers are created with SSL enforcing turned ON.</span></span> <span data-ttu-id="1a2f5-162">若要關閉 SSL 強制執行，請參閱[強制 SSL](./concepts-ssl-connection-security.md) 中的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-162">To turn OFF SSL enforcing, see details in [Enforcing SSL](./concepts-ssl-connection-security.md).</span></span>

    ![pgAdmin - 建立 - 伺服器](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  <span data-ttu-id="1a2f5-164">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-164">Click **Save**.</span></span>
6.  <span data-ttu-id="1a2f5-165">在左側的 [Browser (瀏覽器)] 窗格中，展開 [Server Groups (伺服器群組)]。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-165">In the Browser left pane, expand the **Server Groups**.</span></span> <span data-ttu-id="1a2f5-166">選擇您的伺服器 [Azure PostgreSQL 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-166">Choose your server **Azure PostgreSQL Server**.</span></span>
7.  <span data-ttu-id="1a2f5-167">選擇您連線到的 [Server (伺服器)]，然後選擇其下的 [Databases (資料庫)]。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-167">Choose the **Server** you connected to, and then choose **Databases** under it.</span></span> 
8.  <span data-ttu-id="1a2f5-168">以滑鼠右鍵按一下 [Databases (資料庫)] 以建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-168">Right-click on **Databases** to Create a Database.</span></span>
9.  <span data-ttu-id="1a2f5-169">選擇資料庫名稱 **mypgsqldb** 以及其擁有者作為伺服器管理員登入 **mylogin**。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-169">Choose a database name **mypgsqldb** and the owner for it as server admin login **mylogin**.</span></span>
10. <span data-ttu-id="1a2f5-170">按一下 [儲存] 以建立空白資料庫。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-170">Click **Save** to create a blank database.</span></span>
11. <span data-ttu-id="1a2f5-171">在 [瀏覽器] 中展開 [伺服器] 群組。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-171">In the **Browser**, expand the **Servers** group.</span></span> <span data-ttu-id="1a2f5-172">展開您所建立的伺服器，並請參閱其下的資料庫 **mypgsqldb**。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-172">Expand the server you created, and see the database **mypgsqldb** under it.</span></span>
 <span data-ttu-id="1a2f5-173">![pgAdmin - 建立 - 資料庫](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span><span class="sxs-lookup"><span data-stu-id="1a2f5-173">![pgAdmin - Create - Database](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="1a2f5-174">清除資源</span><span class="sxs-lookup"><span data-stu-id="1a2f5-174">Clean up resources</span></span>

<span data-ttu-id="1a2f5-175">刪除 [Azure 資源群組](../azure-resource-manager/resource-group-overview.md)以清除您在快速入門中建立的所有資源。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-175">Clean up all resources you created in the quickstart by deleting the [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!TIP]
> <span data-ttu-id="1a2f5-176">此集合中的其他快速入門會以本快速入門為基礎。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-176">Other quickstarts in this collection build upon this quick start.</span></span> <span data-ttu-id="1a2f5-177">如果您打算繼續進行後續的快速入門，請勿清除在此快速入門中建立的資源。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-177">If you plan to continue on to work with subsequent quickstarts, do not clean up the resources created in this quickstart.</span></span> <span data-ttu-id="1a2f5-178">如果您不打算繼續，請使用下列步驟，在 Azure CLI 中刪除本快速入門所建立的所有資源。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-178">If you do not plan to continue, use the following steps to delete all resources created by this quickstart in the Azure CLI.</span></span>

```azurecli-interactive
az group delete --name myresourcegroup
```

<span data-ttu-id="1a2f5-179">如果您只想要刪除一個新建立的伺服器，您可以執行 [az postgres server delete](/cli/azure/postgres/server#delete) 命令。</span><span class="sxs-lookup"><span data-stu-id="1a2f5-179">If you just would like to delete the one newly created server, you can run [az postgres server delete](/cli/azure/postgres/server#delete) command.</span></span>
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a><span data-ttu-id="1a2f5-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1a2f5-180">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="1a2f5-181">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="1a2f5-181">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
