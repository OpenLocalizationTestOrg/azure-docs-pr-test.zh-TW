---
title: "Azure CLI：建立 SQL Database | Microsoft Docs"
description: "了解如何使用 Azure CLI 建立 SQL Database 邏輯伺服器、伺服器層級防火牆規則和資料庫。"
keywords: "sql database 教學課程, 建立 sql database"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: a735f7e6aa65ac36dc4e5a49c5a9a834be43d71a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-single-azure-sql-database-using-the-azure-cli"></a><span data-ttu-id="d63f9-104">使用 Azure CLI 建立單一 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d63f9-104">Create a single Azure SQL database using the Azure CLI</span></span>

<span data-ttu-id="d63f9-105">Azure CLI 可用來從命令列或在指令碼中建立和管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="d63f9-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="d63f9-106">本指南詳述如何使用 Azure CLI 在 [Azure SQL Database 邏輯伺服器](sql-database-features.md)的 [Azure 資源群組](../azure-resource-manager/resource-group-overview.md)中部署 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="d63f9-106">This guide details using the Azure CLI to deploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="d63f9-107">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="d63f9-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d63f9-108">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d63f9-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d63f9-109">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="d63f9-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="d63f9-110">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="d63f9-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="define-variables"></a><span data-ttu-id="d63f9-111">定義變數</span><span class="sxs-lookup"><span data-stu-id="d63f9-111">Define variables</span></span>

<span data-ttu-id="d63f9-112">定義變數以便使用於本快速入門中的指令碼。</span><span class="sxs-lookup"><span data-stu-id="d63f9-112">Define variables for use in the scripts in this quick start.</span></span>

```azurecli-interactive
# The data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# The logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# The ip address range that you want to allow to access your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# The database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a><span data-ttu-id="d63f9-113">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="d63f9-113">Create a resource group</span></span>

<span data-ttu-id="d63f9-114">使用 [az group create](../azure-resource-manager/resource-group-overview.md) 命令建立 [Azure 資源群組](/cli/azure/group#create)。</span><span class="sxs-lookup"><span data-stu-id="d63f9-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d63f9-115">資源群組是在其中以群組方式部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="d63f9-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="d63f9-116">下列範例會在 `westeurope` 位置建立名為 `myResourceGroup` 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d63f9-116">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span></span>

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="d63f9-117">建立邏輯伺服器</span><span class="sxs-lookup"><span data-stu-id="d63f9-117">Create a logical server</span></span>

<span data-ttu-id="d63f9-118">使用 [az sql server create](/cli/azure/sql/server#create) 命令建立 [Azure SQL Database 邏輯伺服器](sql-database-features.md)。</span><span class="sxs-lookup"><span data-stu-id="d63f9-118">Create an [Azure SQL Database logical server](sql-database-features.md) using the [az sql server create](/cli/azure/sql/server#create) command.</span></span> <span data-ttu-id="d63f9-119">邏輯伺服器包含一組當作群組管理的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d63f9-119">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="d63f9-120">下列範例會使用名為 `ServerAdmin` 的系統管理員登入和密碼 `ChangeYourAdminPassword1` 在資源群組中建立隨機命名的伺服器。</span><span class="sxs-lookup"><span data-stu-id="d63f9-120">The following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="d63f9-121">視需要取代這些預先定義的值。</span><span class="sxs-lookup"><span data-stu-id="d63f9-121">Replace these pre-defined values as desired.</span></span>

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="d63f9-122">設定伺服器防火牆規則</span><span class="sxs-lookup"><span data-stu-id="d63f9-122">Configure a server firewall rule</span></span>

<span data-ttu-id="d63f9-123">使用 [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) 命令建立 [Azure SQL Database 伺服器層級防火牆規則](sql-database-firewall-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="d63f9-123">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using the [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) command.</span></span> <span data-ttu-id="d63f9-124">伺服器層級防火牆規則可讓外部應用程式 (例如 SQL Server Management Studio 或 SQLCMD 公用程式) 穿過 SQL Database 服務防火牆連線到 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="d63f9-124">A server-level firewall rule allows an external application, such as SQL Server Management Studio or the SQLCMD utility to connect to a SQL database through the SQL Database service firewall.</span></span> <span data-ttu-id="d63f9-125">在下列範例中，只會針對其他 Azure 資源開啟防火牆。</span><span class="sxs-lookup"><span data-stu-id="d63f9-125">In the following example, the firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="d63f9-126">若要啟用外部連線，請將 IP 位址變更為適合您環境的地址。</span><span class="sxs-lookup"><span data-stu-id="d63f9-126">To enable external connectivity, change the IP address to an appropriate address for your environment.</span></span> <span data-ttu-id="d63f9-127">若要開啟所有 IP 位址，請使用 0.0.0.0 做為起始 IP 位址，並使用 255.255.255.255 做為結束位址。</span><span class="sxs-lookup"><span data-stu-id="d63f9-127">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> <span data-ttu-id="d63f9-128">SQL Database 會透過連接埠 1433 通訊。</span><span class="sxs-lookup"><span data-stu-id="d63f9-128">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="d63f9-129">如果您嘗試從公司網路進行連線，您網路的防火牆可能不允許透過連接埠 1433 的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="d63f9-129">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="d63f9-130">若是如此，除非 IT 部門開啟連接埠 1433，否則將無法連線至 Azure SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d63f9-130">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-the-server-with-sample-data"></a><span data-ttu-id="d63f9-131">在伺服器中建立資料庫與範例資料</span><span class="sxs-lookup"><span data-stu-id="d63f9-131">Create a database in the server with sample data</span></span>

<span data-ttu-id="d63f9-132">使用 [az sql db create](/cli/azure/sql/db#create) 命令在伺服器中建立具有 [S0 效能等級](sql-database-service-tiers.md)的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d63f9-132">Create a database with an [S0 performance level](sql-database-service-tiers.md) in the server using the [az sql db create](/cli/azure/sql/db#create) command.</span></span> <span data-ttu-id="d63f9-133">下列範例會建立名為 `mySampleDatabase` 的資料庫，並將 AdventureWorksLT 範例資料載入此資料庫。</span><span class="sxs-lookup"><span data-stu-id="d63f9-133">The following example creates a database called `mySampleDatabase` and loads the AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="d63f9-134">視需要取代這些預先定義的值 (本集合中的其他快速入門會建置在本快速入門中的值)。</span><span class="sxs-lookup"><span data-stu-id="d63f9-134">Replace these predefined values as desired (other quick starts in this collection build upon the values in this quick start).</span></span>

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a><span data-ttu-id="d63f9-135">清除資源</span><span class="sxs-lookup"><span data-stu-id="d63f9-135">Clean up resources</span></span>

<span data-ttu-id="d63f9-136">此集合中的其他快速入門會建置在本快速入門。</span><span class="sxs-lookup"><span data-stu-id="d63f9-136">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="d63f9-137">如果您打算繼續進行後續的快速入門，請勿清除在此快速入門中建立的資源。</span><span class="sxs-lookup"><span data-stu-id="d63f9-137">If you plan to continue on to work with subsequent quick starts, do not clean up the resources created in this quick start.</span></span> <span data-ttu-id="d63f9-138">如果您不打算繼續，請使用下列步驟，在 Azure 入口網站中刪除本快速入門所建立的所有資源。</span><span class="sxs-lookup"><span data-stu-id="d63f9-138">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span></span>
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="d63f9-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d63f9-139">Next steps</span></span>

<span data-ttu-id="d63f9-140">您現在具有資料庫，您可使用最愛的工具進行連線和查詢。</span><span class="sxs-lookup"><span data-stu-id="d63f9-140">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="d63f9-141">選擇下列工具來深入了解︰</span><span class="sxs-lookup"><span data-stu-id="d63f9-141">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="d63f9-142">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="d63f9-142">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="d63f9-143">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d63f9-143">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="d63f9-144">.NET</span><span class="sxs-lookup"><span data-stu-id="d63f9-144">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="d63f9-145">PHP</span><span class="sxs-lookup"><span data-stu-id="d63f9-145">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="d63f9-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="d63f9-146">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="d63f9-147">Java</span><span class="sxs-lookup"><span data-stu-id="d63f9-147">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="d63f9-148">Python</span><span class="sxs-lookup"><span data-stu-id="d63f9-148">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="d63f9-149">Ruby</span><span class="sxs-lookup"><span data-stu-id="d63f9-149">Ruby</span></span>](sql-database-connect-query-ruby.md)

