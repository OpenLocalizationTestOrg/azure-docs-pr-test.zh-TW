---
title: "Azure PowerShell︰建立 SQL Database | Microsoft Docs"
description: "了解 toocreate SQL Database 邏輯伺服器、 伺服器層級防火牆規則和資料庫中的 hello Azure 入口網站。"
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
ms.openlocfilehash: e89f68b44083a3b64e61f95117dbbedfa6647ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a><span data-ttu-id="293a0-104">使用 PowerShell 建立單一 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="293a0-104">Create a single Azure SQL database using PowerShell</span></span>

<span data-ttu-id="293a0-105">PowerShell 是使用的 toocreate，並從 hello 命令列或指令碼中管理的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="293a0-105">PowerShell is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="293a0-106">此指南使用 PowerShell toodeploy 詳細資料中的 Azure SQL database [Azure 資源群組](../azure-resource-manager/resource-group-overview.md)中[Azure SQL Database 邏輯伺服器](sql-database-features.md)。</span><span class="sxs-lookup"><span data-stu-id="293a0-106">This guide details using PowerShell toodeploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="293a0-107">如果您沒有 Azure 訂用帳戶，請在開始前建立[免費帳戶](https://azure.microsoft.com/free/) 。</span><span class="sxs-lookup"><span data-stu-id="293a0-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

<span data-ttu-id="293a0-108">本教學課程需要 hello Azure PowerShell 模組版本 4.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="293a0-108">This tutorial requires hello Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="293a0-109">執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="293a0-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="293a0-110">如果您需要 tooinstall 或升級，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="293a0-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

## <a name="log-in-tooazure"></a><span data-ttu-id="293a0-111">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="293a0-111">Log in tooAzure</span></span>

<span data-ttu-id="293a0-112">登入 tooyour Azure 訂用帳戶使用 hello[新增 AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount)命令，並遵循螢幕上指示 hello。</span><span class="sxs-lookup"><span data-stu-id="293a0-112">Log in tooyour Azure subscription using hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command and follow hello on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a><span data-ttu-id="293a0-113">建立變數</span><span class="sxs-lookup"><span data-stu-id="293a0-113">Create variables</span></span>

<span data-ttu-id="293a0-114">在這個快速入門中的 hello 指令碼中定義使用的變數。</span><span class="sxs-lookup"><span data-stu-id="293a0-114">Define variables for use in hello scripts in this quick start.</span></span>

```powershell
# hello data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# hello login information for hello server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# hello ip address range that you want tooallow tooaccess your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.0"
# hello database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="293a0-115">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="293a0-115">Create a resource group</span></span>

<span data-ttu-id="293a0-116">建立[Azure 資源群組](../azure-resource-manager/resource-group-overview.md)使用 hello[新增 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)命令。</span><span class="sxs-lookup"><span data-stu-id="293a0-116">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="293a0-117">資源群組是在其中以群組方式部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="293a0-117">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="293a0-118">hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`westeurope`位置。</span><span class="sxs-lookup"><span data-stu-id="293a0-118">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location.</span></span>

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="293a0-119">建立邏輯伺服器</span><span class="sxs-lookup"><span data-stu-id="293a0-119">Create a logical server</span></span>

<span data-ttu-id="293a0-120">建立[Azure SQL Database 邏輯伺服器](sql-database-features.md)使用 hello[新增 AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver)命令。</span><span class="sxs-lookup"><span data-stu-id="293a0-120">Create an [Azure SQL Database logical server](sql-database-features.md) using hello [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) command.</span></span> <span data-ttu-id="293a0-121">邏輯伺服器包含一組當作群組管理的資料庫。</span><span class="sxs-lookup"><span data-stu-id="293a0-121">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="293a0-122">hello 下列範例會建立隨機命名的伺服器資源群組中具有系統管理員登入名為`ServerAdmin`且密碼為`ChangeYourAdminPassword1`。</span><span class="sxs-lookup"><span data-stu-id="293a0-122">hello following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="293a0-123">視需要取代這些預先定義的值。</span><span class="sxs-lookup"><span data-stu-id="293a0-123">Replace these pre-defined values as desired.</span></span>

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="293a0-124">設定伺服器防火牆規則</span><span class="sxs-lookup"><span data-stu-id="293a0-124">Configure a server firewall rule</span></span>

<span data-ttu-id="293a0-125">建立[Azure SQL Database 伺服器層級防火牆規則](sql-database-firewall-configure.md)使用 hello[新增 AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule)命令。</span><span class="sxs-lookup"><span data-stu-id="293a0-125">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using hello [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) command.</span></span> <span data-ttu-id="293a0-126">伺服器層級防火牆規則可讓外部應用程式，例如 SQL Server Management Studio 或 hello SQLCMD 公用程式 tooconnect tooa SQL database 透過 hello SQL Database 服務防火牆。</span><span class="sxs-lookup"><span data-stu-id="293a0-126">A server-level firewall rule allows an external application, such as SQL Server Management Studio or hello SQLCMD utility tooconnect tooa SQL database through hello SQL Database service firewall.</span></span> <span data-ttu-id="293a0-127">在下列範例的 hello，hello 開啟防火牆會僅針對其他 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="293a0-127">In hello following example, hello firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="293a0-128">tooenable 外部連線，變更 hello IP 位址 tooan 適當的位址，為您的環境。</span><span class="sxs-lookup"><span data-stu-id="293a0-128">tooenable external connectivity, change hello IP address tooan appropriate address for your environment.</span></span> <span data-ttu-id="293a0-129">tooopen 所有 IP 位址，都作為 hello 起始 IP 位址和 255.255.255.255 hello 結束位址為 0.0.0.0。</span><span class="sxs-lookup"><span data-stu-id="293a0-129">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> <span data-ttu-id="293a0-130">SQL Database 會透過連接埠 1433 通訊。</span><span class="sxs-lookup"><span data-stu-id="293a0-130">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="293a0-131">如果您嘗試 tooconnect 從公司網路內，由您的網路防火牆可能不允許透過通訊埠 1433年的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="293a0-131">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="293a0-132">如果是的話，就能 tooconnect tooyour Azure SQL Database 伺服器除非您的 IT 部門會開啟通訊埠 1433年。</span><span class="sxs-lookup"><span data-stu-id="293a0-132">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a><span data-ttu-id="293a0-133">以範例資料的 hello 伺服器中建立資料庫</span><span class="sxs-lookup"><span data-stu-id="293a0-133">Create a database in hello server with sample data</span></span>

<span data-ttu-id="293a0-134">建立與資料庫[S0 的效能層級](sql-database-service-tiers.md)hello 伺服器使用 hello[新增 AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)命令。</span><span class="sxs-lookup"><span data-stu-id="293a0-134">Create a database with an [S0 performance level](sql-database-service-tiers.md) in hello server using hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) command.</span></span> <span data-ttu-id="293a0-135">hello 下列範例會建立一個稱為資料庫`mySampleDatabase`和載入 hello 有提供 AdventureWorksLT 範例資料到此資料庫。</span><span class="sxs-lookup"><span data-stu-id="293a0-135">hello following example creates a database called `mySampleDatabase` and loads hello AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="293a0-136">這些預先定義的取代值，則為所需 （在這個快速入門中的 hello 值的這個集合組建中其他快速開始）。</span><span class="sxs-lookup"><span data-stu-id="293a0-136">Replace these predefined values as desired (other quick starts in this collection build upon hello values in this quick start).</span></span>

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a><span data-ttu-id="293a0-137">清除資源</span><span class="sxs-lookup"><span data-stu-id="293a0-137">Clean up resources</span></span>

<span data-ttu-id="293a0-138">此集合中的其他快速入門會建置在本快速入門。</span><span class="sxs-lookup"><span data-stu-id="293a0-138">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="293a0-139">如果您計劃 toocontinue toowork 與後續的快速入門，請不要清除 hello 資源建立在這個快速開始。</span><span class="sxs-lookup"><span data-stu-id="293a0-139">If you plan toocontinue on toowork with subsequent quick starts, do not clean up hello resources created in this quick start.</span></span> <span data-ttu-id="293a0-140">如果您不打算 toocontinue，使用 hello 本快速入門 hello Azure 入口網站中的下列步驟 toodelete 建立所有資源。</span><span class="sxs-lookup"><span data-stu-id="293a0-140">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quick start in hello Azure portal.</span></span>
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="293a0-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="293a0-141">Next steps</span></span>

<span data-ttu-id="293a0-142">您現在具有資料庫，您可使用最愛的工具進行連線和查詢。</span><span class="sxs-lookup"><span data-stu-id="293a0-142">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="293a0-143">選擇下列工具來深入了解︰</span><span class="sxs-lookup"><span data-stu-id="293a0-143">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="293a0-144">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="293a0-144">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="293a0-145">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="293a0-145">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="293a0-146">.NET</span><span class="sxs-lookup"><span data-stu-id="293a0-146">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="293a0-147">PHP</span><span class="sxs-lookup"><span data-stu-id="293a0-147">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="293a0-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="293a0-148">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="293a0-149">Java</span><span class="sxs-lookup"><span data-stu-id="293a0-149">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="293a0-150">Python</span><span class="sxs-lookup"><span data-stu-id="293a0-150">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="293a0-151">Ruby</span><span class="sxs-lookup"><span data-stu-id="293a0-151">Ruby</span></span>](sql-database-connect-query-ruby.md)

