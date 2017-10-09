---
title: "Azure CLI：建立 SQL Database | Microsoft Docs"
description: "了解 toocreate SQL Database 邏輯伺服器，伺服器層級防火牆規則，並使用資料庫 hello Azure CLI。"
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
ms.openlocfilehash: 9b1ffb17eabeb70a000ff0c997128832b07aa4fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-hello-azure-cli"></a><span data-ttu-id="75ef1-104">建立單一的 Azure SQL database，使用 Azure CLI hello</span><span class="sxs-lookup"><span data-stu-id="75ef1-104">Create a single Azure SQL database using hello Azure CLI</span></span>

<span data-ttu-id="75ef1-105">hello Azure CLI 會使用的 toocreate 和管理 Azure 資源，從 hello 命令列或指令碼中。</span><span class="sxs-lookup"><span data-stu-id="75ef1-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="75ef1-106">此指南使用 hello Azure CLI toodeploy 詳細資料中的 Azure SQL database [Azure 資源群組](../azure-resource-manager/resource-group-overview.md)中[Azure SQL Database 邏輯伺服器](sql-database-features.md)。</span><span class="sxs-lookup"><span data-stu-id="75ef1-106">This guide details using hello Azure CLI toodeploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="75ef1-107">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="75ef1-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="75ef1-108">如果您選擇 tooinstall，並在本機上使用 hello CLI，這個主題需要執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="75ef1-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="75ef1-109">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="75ef1-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="75ef1-110">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="75ef1-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="define-variables"></a><span data-ttu-id="75ef1-111">定義變數</span><span class="sxs-lookup"><span data-stu-id="75ef1-111">Define variables</span></span>

<span data-ttu-id="75ef1-112">在這個快速入門中的 hello 指令碼中定義使用的變數。</span><span class="sxs-lookup"><span data-stu-id="75ef1-112">Define variables for use in hello scripts in this quick start.</span></span>

```azurecli-interactive
# hello data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# hello ip address range that you want tooallow tooaccess your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# hello database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a><span data-ttu-id="75ef1-113">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="75ef1-113">Create a resource group</span></span>

<span data-ttu-id="75ef1-114">建立[Azure 資源群組](../azure-resource-manager/resource-group-overview.md)使用 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="75ef1-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="75ef1-115">資源群組是在其中以群組方式部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="75ef1-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="75ef1-116">hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`westeurope`位置。</span><span class="sxs-lookup"><span data-stu-id="75ef1-116">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location.</span></span>

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="75ef1-117">建立邏輯伺服器</span><span class="sxs-lookup"><span data-stu-id="75ef1-117">Create a logical server</span></span>

<span data-ttu-id="75ef1-118">建立[Azure SQL Database 邏輯伺服器](sql-database-features.md)使用 hello [az sql server 建立](/cli/azure/sql/server#create)命令。</span><span class="sxs-lookup"><span data-stu-id="75ef1-118">Create an [Azure SQL Database logical server](sql-database-features.md) using hello [az sql server create](/cli/azure/sql/server#create) command.</span></span> <span data-ttu-id="75ef1-119">邏輯伺服器包含一組當作群組管理的資料庫。</span><span class="sxs-lookup"><span data-stu-id="75ef1-119">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="75ef1-120">hello 下列範例會建立隨機命名的伺服器資源群組中具有系統管理員登入名為`ServerAdmin`且密碼為`ChangeYourAdminPassword1`。</span><span class="sxs-lookup"><span data-stu-id="75ef1-120">hello following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="75ef1-121">視需要取代這些預先定義的值。</span><span class="sxs-lookup"><span data-stu-id="75ef1-121">Replace these pre-defined values as desired.</span></span>

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="75ef1-122">設定伺服器防火牆規則</span><span class="sxs-lookup"><span data-stu-id="75ef1-122">Configure a server firewall rule</span></span>

<span data-ttu-id="75ef1-123">建立[Azure SQL Database 伺服器層級防火牆規則](sql-database-firewall-configure.md)使用 hello [az sql server 防火牆建立](/cli/azure/sql/server/firewall-rule#create)命令。</span><span class="sxs-lookup"><span data-stu-id="75ef1-123">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using hello [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) command.</span></span> <span data-ttu-id="75ef1-124">伺服器層級防火牆規則可讓外部應用程式，例如 SQL Server Management Studio 或 hello SQLCMD 公用程式 tooconnect tooa SQL database 透過 hello SQL Database 服務防火牆。</span><span class="sxs-lookup"><span data-stu-id="75ef1-124">A server-level firewall rule allows an external application, such as SQL Server Management Studio or hello SQLCMD utility tooconnect tooa SQL database through hello SQL Database service firewall.</span></span> <span data-ttu-id="75ef1-125">在下列範例的 hello，hello 開啟防火牆會僅針對其他 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="75ef1-125">In hello following example, hello firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="75ef1-126">tooenable 外部連線，變更 hello IP 位址 tooan 適當的位址，為您的環境。</span><span class="sxs-lookup"><span data-stu-id="75ef1-126">tooenable external connectivity, change hello IP address tooan appropriate address for your environment.</span></span> <span data-ttu-id="75ef1-127">tooopen 所有 IP 位址，都作為 hello 起始 IP 位址和 255.255.255.255 hello 結束位址為 0.0.0.0。</span><span class="sxs-lookup"><span data-stu-id="75ef1-127">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> <span data-ttu-id="75ef1-128">SQL Database 會透過連接埠 1433 通訊。</span><span class="sxs-lookup"><span data-stu-id="75ef1-128">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="75ef1-129">如果您嘗試 tooconnect 從公司網路內，由您的網路防火牆可能不允許透過通訊埠 1433年的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="75ef1-129">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="75ef1-130">如果是的話，就能 tooconnect tooyour Azure SQL Database 伺服器除非您的 IT 部門會開啟通訊埠 1433年。</span><span class="sxs-lookup"><span data-stu-id="75ef1-130">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a><span data-ttu-id="75ef1-131">以範例資料的 hello 伺服器中建立資料庫</span><span class="sxs-lookup"><span data-stu-id="75ef1-131">Create a database in hello server with sample data</span></span>

<span data-ttu-id="75ef1-132">建立與資料庫[S0 的效能層級](sql-database-service-tiers.md)hello 伺服器使用 hello [az sql 資料庫建立](/cli/azure/sql/db#create)命令。</span><span class="sxs-lookup"><span data-stu-id="75ef1-132">Create a database with an [S0 performance level](sql-database-service-tiers.md) in hello server using hello [az sql db create](/cli/azure/sql/db#create) command.</span></span> <span data-ttu-id="75ef1-133">hello 下列範例會建立一個稱為資料庫`mySampleDatabase`和載入 hello 有提供 AdventureWorksLT 範例資料到此資料庫。</span><span class="sxs-lookup"><span data-stu-id="75ef1-133">hello following example creates a database called `mySampleDatabase` and loads hello AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="75ef1-134">這些預先定義的取代值，則為所需 （在這個快速入門中的 hello 值的這個集合組建中其他快速開始）。</span><span class="sxs-lookup"><span data-stu-id="75ef1-134">Replace these predefined values as desired (other quick starts in this collection build upon hello values in this quick start).</span></span>

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a><span data-ttu-id="75ef1-135">清除資源</span><span class="sxs-lookup"><span data-stu-id="75ef1-135">Clean up resources</span></span>

<span data-ttu-id="75ef1-136">此集合中的其他快速入門會建置在本快速入門。</span><span class="sxs-lookup"><span data-stu-id="75ef1-136">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="75ef1-137">如果您計劃 toocontinue toowork 與後續的快速入門，請不要清除 hello 資源建立在這個快速開始。</span><span class="sxs-lookup"><span data-stu-id="75ef1-137">If you plan toocontinue on toowork with subsequent quick starts, do not clean up hello resources created in this quick start.</span></span> <span data-ttu-id="75ef1-138">如果您不打算 toocontinue，使用 hello 本快速入門 hello Azure 入口網站中的下列步驟 toodelete 建立所有資源。</span><span class="sxs-lookup"><span data-stu-id="75ef1-138">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quick start in hello Azure portal.</span></span>
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="75ef1-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="75ef1-139">Next steps</span></span>

<span data-ttu-id="75ef1-140">您現在具有資料庫，您可使用最愛的工具進行連線和查詢。</span><span class="sxs-lookup"><span data-stu-id="75ef1-140">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="75ef1-141">選擇下列工具來深入了解︰</span><span class="sxs-lookup"><span data-stu-id="75ef1-141">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="75ef1-142">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="75ef1-142">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="75ef1-143">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="75ef1-143">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="75ef1-144">.NET</span><span class="sxs-lookup"><span data-stu-id="75ef1-144">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="75ef1-145">PHP</span><span class="sxs-lookup"><span data-stu-id="75ef1-145">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="75ef1-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="75ef1-146">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="75ef1-147">Java</span><span class="sxs-lookup"><span data-stu-id="75ef1-147">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="75ef1-148">Python</span><span class="sxs-lookup"><span data-stu-id="75ef1-148">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="75ef1-149">Ruby</span><span class="sxs-lookup"><span data-stu-id="75ef1-149">Ruby</span></span>](sql-database-connect-query-ruby.md)

