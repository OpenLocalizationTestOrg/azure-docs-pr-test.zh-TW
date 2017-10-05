---
title: "Azure PowerShell︰建立 SQL Database | Microsoft Docs"
description: "了解如何在 Azure 入口網站中，建立 SQL Database 邏輯伺服器、伺服器層級防火牆規則和資料庫。"
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
ms.devlang: PowerShell
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: 44ed4a603977617c898315c4fc0b2d3dd3a8f16a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a><span data-ttu-id="14249-104">使用 PowerShell 建立單一 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="14249-104">Create a single Azure SQL database using PowerShell</span></span>

<span data-ttu-id="14249-105">PowerShell 可用來從命令列或在指令碼中建立和管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="14249-105">PowerShell is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="14249-106">本指南詳述如何使用 PowerShell 在 [Azure SQL Database 邏輯伺服器](sql-database-features.md)的 [Azure 資源群組](../azure-resource-manager/resource-group-overview.md)中部署 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="14249-106">This guide details using PowerShell to deploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="14249-107">如果您沒有 Azure 訂用帳戶，請在開始前建立[免費帳戶](https://azure.microsoft.com/free/) 。</span><span class="sxs-lookup"><span data-stu-id="14249-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

<span data-ttu-id="14249-108">本教學課程需要 Azure PowerShell 模組 4.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="14249-108">This tutorial requires the Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="14249-109">執行 ` Get-Module -ListAvailable AzureRM` 找出版本。</span><span class="sxs-lookup"><span data-stu-id="14249-109">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="14249-110">如果您需要安裝或升級，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="14249-110">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

## <a name="log-in-to-azure"></a><span data-ttu-id="14249-111">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="14249-111">Log in to Azure</span></span>

<span data-ttu-id="14249-112">使用 [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) 命令登入 Azure 訂用帳戶並遵循畫面上的指示。</span><span class="sxs-lookup"><span data-stu-id="14249-112">Log in to your Azure subscription using the [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command and follow the on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a><span data-ttu-id="14249-113">建立變數</span><span class="sxs-lookup"><span data-stu-id="14249-113">Create variables</span></span>

<span data-ttu-id="14249-114">定義變數以便使用於本快速入門中的指令碼。</span><span class="sxs-lookup"><span data-stu-id="14249-114">Define variables for use in the scripts in this quick start.</span></span>

```powershell
# The data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# The logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# The login information for the server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# The ip address range that you want to allow to access your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.0"
# The database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="14249-115">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="14249-115">Create a resource group</span></span>

<span data-ttu-id="14249-116">使用 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 命令建立 [Azure 資源群組](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="14249-116">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="14249-117">資源群組是在其中以群組方式部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="14249-117">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="14249-118">下列範例會在 `westeurope` 位置建立名為 `myResourceGroup` 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="14249-118">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span></span>

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="14249-119">建立邏輯伺服器</span><span class="sxs-lookup"><span data-stu-id="14249-119">Create a logical server</span></span>

<span data-ttu-id="14249-120">使用 [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) 命令建立 [Azure SQL Database 邏輯伺服器](sql-database-features.md)。</span><span class="sxs-lookup"><span data-stu-id="14249-120">Create an [Azure SQL Database logical server](sql-database-features.md) using the [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) command.</span></span> <span data-ttu-id="14249-121">邏輯伺服器包含一組當作群組管理的資料庫。</span><span class="sxs-lookup"><span data-stu-id="14249-121">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="14249-122">下列範例會使用名為 `ServerAdmin` 的系統管理員登入和密碼 `ChangeYourAdminPassword1` 在資源群組中建立隨機命名的伺服器。</span><span class="sxs-lookup"><span data-stu-id="14249-122">The following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="14249-123">視需要取代這些預先定義的值。</span><span class="sxs-lookup"><span data-stu-id="14249-123">Replace these pre-defined values as desired.</span></span>

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="14249-124">設定伺服器防火牆規則</span><span class="sxs-lookup"><span data-stu-id="14249-124">Configure a server firewall rule</span></span>

<span data-ttu-id="14249-125">使用 [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) 命令建立 [Azure SQL Database 伺服器層級防火牆規則](sql-database-firewall-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="14249-125">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using the [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) command.</span></span> <span data-ttu-id="14249-126">伺服器層級防火牆規則可讓外部應用程式 (例如 SQL Server Management Studio 或 SQLCMD 公用程式) 穿過 SQL Database 服務防火牆連線到 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="14249-126">A server-level firewall rule allows an external application, such as SQL Server Management Studio or the SQLCMD utility to connect to a SQL database through the SQL Database service firewall.</span></span> <span data-ttu-id="14249-127">在下列範例中，只會針對其他 Azure 資源開啟防火牆。</span><span class="sxs-lookup"><span data-stu-id="14249-127">In the following example, the firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="14249-128">若要啟用外部連線，請將 IP 位址變更為適合您環境的地址。</span><span class="sxs-lookup"><span data-stu-id="14249-128">To enable external connectivity, change the IP address to an appropriate address for your environment.</span></span> <span data-ttu-id="14249-129">若要開啟所有 IP 位址，請使用 0.0.0.0 做為起始 IP 位址，並使用 255.255.255.255 做為結束位址。</span><span class="sxs-lookup"><span data-stu-id="14249-129">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> <span data-ttu-id="14249-130">SQL Database 會透過連接埠 1433 通訊。</span><span class="sxs-lookup"><span data-stu-id="14249-130">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="14249-131">如果您嘗試從公司網路進行連線，您網路的防火牆可能不允許透過連接埠 1433 的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="14249-131">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="14249-132">若是如此，除非 IT 部門開啟連接埠 1433，否則將無法連線至 Azure SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="14249-132">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-the-server-with-sample-data"></a><span data-ttu-id="14249-133">在伺服器中建立資料庫與範例資料</span><span class="sxs-lookup"><span data-stu-id="14249-133">Create a database in the server with sample data</span></span>

<span data-ttu-id="14249-134">在伺服器中使用 [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) 命令來建立 [S0 效能等級](sql-database-service-tiers.md)的資料庫。</span><span class="sxs-lookup"><span data-stu-id="14249-134">Create a database with an [S0 performance level](sql-database-service-tiers.md) in the server using the [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) command.</span></span> <span data-ttu-id="14249-135">下列範例會建立名為 `mySampleDatabase` 的資料庫，並將 AdventureWorksLT 範例資料載入此資料庫。</span><span class="sxs-lookup"><span data-stu-id="14249-135">The following example creates a database called `mySampleDatabase` and loads the AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="14249-136">視需要取代這些預先定義的值 (本集合中的其他快速入門會建置在本快速入門中的值)。</span><span class="sxs-lookup"><span data-stu-id="14249-136">Replace these predefined values as desired (other quick starts in this collection build upon the values in this quick start).</span></span>

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a><span data-ttu-id="14249-137">清除資源</span><span class="sxs-lookup"><span data-stu-id="14249-137">Clean up resources</span></span>

<span data-ttu-id="14249-138">此集合中的其他快速入門會建置在本快速入門。</span><span class="sxs-lookup"><span data-stu-id="14249-138">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="14249-139">如果您打算繼續進行後續的快速入門，請勿清除在此快速入門中建立的資源。</span><span class="sxs-lookup"><span data-stu-id="14249-139">If you plan to continue on to work with subsequent quick starts, do not clean up the resources created in this quick start.</span></span> <span data-ttu-id="14249-140">如果您不打算繼續，請使用下列步驟，在 Azure 入口網站中刪除本快速入門所建立的所有資源。</span><span class="sxs-lookup"><span data-stu-id="14249-140">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span></span>
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="14249-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="14249-141">Next steps</span></span>

<span data-ttu-id="14249-142">您現在具有資料庫，您可使用最愛的工具進行連線和查詢。</span><span class="sxs-lookup"><span data-stu-id="14249-142">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="14249-143">選擇下列工具來深入了解︰</span><span class="sxs-lookup"><span data-stu-id="14249-143">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="14249-144">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="14249-144">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="14249-145">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="14249-145">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="14249-146">.NET</span><span class="sxs-lookup"><span data-stu-id="14249-146">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="14249-147">PHP</span><span class="sxs-lookup"><span data-stu-id="14249-147">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="14249-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="14249-148">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="14249-149">Java</span><span class="sxs-lookup"><span data-stu-id="14249-149">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="14249-150">Python</span><span class="sxs-lookup"><span data-stu-id="14249-150">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="14249-151">Ruby</span><span class="sxs-lookup"><span data-stu-id="14249-151">Ruby</span></span>](sql-database-connect-query-ruby.md)

