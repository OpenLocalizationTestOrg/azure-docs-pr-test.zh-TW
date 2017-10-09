---
title: "aaaImplement 地理分散的 Azure SQL Database 方案 |Microsoft 文件"
description: "了解的 tooconfigure 您的 Azure SQL Database 和應用程式的容錯移轉 tooa 複寫資料庫，並測試容錯移轉。"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 9295d33c669405108a1a64ef1e7cb77f582773a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-geo-distributed-database"></a><span data-ttu-id="7608d-103">實作異地分散資料庫</span><span class="sxs-lookup"><span data-stu-id="7608d-103">Implement a geo-distributed database</span></span>

<span data-ttu-id="7608d-104">在本教學課程中，您設定 Azure SQL database 與容錯移轉 tooa 遠端區域的應用程式，然後測試您的容錯移轉計劃。</span><span class="sxs-lookup"><span data-stu-id="7608d-104">In this tutorial, you configure an Azure SQL database and application for failover tooa remote region, and then test your failover plan.</span></span> <span data-ttu-id="7608d-105">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="7608d-105">You learn how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="7608d-106">建立資料庫使用者並授與其權限</span><span class="sxs-lookup"><span data-stu-id="7608d-106">Create database users and grant them permissions</span></span>
> * <span data-ttu-id="7608d-107">設定資料庫層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="7608d-107">Set up a database-level firewall rule</span></span>
> * <span data-ttu-id="7608d-108">建立[異地複寫容錯移轉群組](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7608d-108">Create a [geo-replication failover group](sql-database-geo-replication-overview.md)</span></span>
> * <span data-ttu-id="7608d-109">建立及編譯 Java 應用程式 tooquery Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="7608d-109">Create and compile a Java application tooquery an Azure SQL database</span></span>
> * <span data-ttu-id="7608d-110">執行災害復原演練</span><span class="sxs-lookup"><span data-stu-id="7608d-110">Perform a disaster recovery drill</span></span>

<span data-ttu-id="7608d-111">如果您沒有 Azure 訂用帳戶，請在開始之前先[建立免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="7608d-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7608d-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="7608d-112">Prerequisites</span></span>

<span data-ttu-id="7608d-113">toocomplete 完成本教學課程，請確定 hello 下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="7608d-113">toocomplete this tutorial, make sure hello following prerequisites are completed:</span></span>

- <span data-ttu-id="7608d-114">最新安裝的 hello [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs)。</span><span class="sxs-lookup"><span data-stu-id="7608d-114">Installed hello latest [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span></span> 
- <span data-ttu-id="7608d-115">已安裝 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="7608d-115">Installed an Azure SQL database.</span></span> <span data-ttu-id="7608d-116">本教學課程使用 hello 有提供 AdventureWorksLT 範例資料庫的名稱與**mySampleDatabase**其中一個這些快速入門：</span><span class="sxs-lookup"><span data-stu-id="7608d-116">This tutorial uses hello AdventureWorksLT sample database with a name of **mySampleDatabase** from one of these quick starts:</span></span>

   - [<span data-ttu-id="7608d-117">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="7608d-117">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="7608d-118">建立 DB - CLI</span><span class="sxs-lookup"><span data-stu-id="7608d-118">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="7608d-119">建立 DB - PowerShell</span><span class="sxs-lookup"><span data-stu-id="7608d-119">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="7608d-120">已識別方法 tooexecute SQL 對資料庫的指令碼，您可以使用其中一個 hello 遵循查詢工具：</span><span class="sxs-lookup"><span data-stu-id="7608d-120">Have identified a method tooexecute SQL scripts against your database, you can use one of hello following query tools:</span></span>
   - <span data-ttu-id="7608d-121">hello 查詢編輯器中 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="7608d-121">hello query editor in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7608d-122">如需有關使用 hello Azure 入口網站中的 hello 查詢編輯器的詳細資訊，請參閱[連接和查詢中使用查詢編輯器](sql-database-get-started-portal.md#query-the-sql-database)。</span><span class="sxs-lookup"><span data-stu-id="7608d-122">For more information on using hello query editor in hello Azure portal, see [Connect and query using Query Editor](sql-database-get-started-portal.md#query-the-sql-database).</span></span>
   - <span data-ttu-id="7608d-123">hello 最新版本的[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)，這是用於管理任何 SQL 基礎結構，從 SQL Server tooSQL 資料庫的 Microsoft Windows 整合式的環境。</span><span class="sxs-lookup"><span data-stu-id="7608d-123">hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), which is an integrated environment for managing any SQL infrastructure, from SQL Server tooSQL Database for Microsoft Windows.</span></span>
   - <span data-ttu-id="7608d-124">hello 最新版本的[Visual Studio Code](https://code.visualstudio.com/docs)、 圖形化的程式碼編輯器 for Linux，macOS，且可支援擴充功能，包括 Windows hello [mssql 延伸](https://aka.ms/mssql-marketplace)查詢 Microsoft SQL ServerAzure SQL Database 和 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="7608d-124">hello newest version of [Visual Studio Code](https://code.visualstudio.com/docs), which is a graphical code editor for Linux, macOS, and Windows that supports extensions, including hello [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="7608d-125">如需搭配使用此工具與 Azure SQL Database 的詳細資訊，請參閱[使用 VS Code 連線及查詢](sql-database-connect-query-vscode.md)。</span><span class="sxs-lookup"><span data-stu-id="7608d-125">For more information on using this tool with Azure SQL Database, see [Connect and query with VS Code](sql-database-connect-query-vscode.md).</span></span> 

## <a name="create-database-users-and-grant-permissions"></a><span data-ttu-id="7608d-126">建立資料庫使用者並授與權限</span><span class="sxs-lookup"><span data-stu-id="7608d-126">Create database users and grant permissions</span></span>

<span data-ttu-id="7608d-127">連接 tooyour 資料庫，並建立使用者帳戶，使用下列查詢工具 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="7608d-127">Connect tooyour database and create user accounts using one of hello following query tools:</span></span>

- <span data-ttu-id="7608d-128">hello hello Azure 入口網站中的查詢編輯器</span><span class="sxs-lookup"><span data-stu-id="7608d-128">hello Query editor in hello Azure portal</span></span>
- <span data-ttu-id="7608d-129">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="7608d-129">SQL Server Management Studio</span></span>
- <span data-ttu-id="7608d-130">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7608d-130">Visual Studio Code</span></span>

<span data-ttu-id="7608d-131">這些使用者帳戶自動複寫 tooyour 次要伺服器，並保持同步。</span><span class="sxs-lookup"><span data-stu-id="7608d-131">These user accounts replicate automatically tooyour secondary server (and be kept in sync).</span></span> <span data-ttu-id="7608d-132">toouse SQL Server Management Studio 或 Visual Studio 程式碼，您可能需要 tooconfigure 防火牆規則，如果您從在您有尚未設定防火牆的 IP 位址的用戶端連接。</span><span class="sxs-lookup"><span data-stu-id="7608d-132">toouse SQL Server Management Studio or Visual Studio Code, you may need tooconfigure a firewall rule if you are connecting from a client at an IP address for which you have not yet configured a firewall.</span></span> <span data-ttu-id="7608d-133">如需詳細步驟，請參閱[建立伺服器層級防火牆規則](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)。</span><span class="sxs-lookup"><span data-stu-id="7608d-133">For detailed steps, see [Create a server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>

- <span data-ttu-id="7608d-134">在查詢視窗中，執行下列查詢 toocreate 兩個使用者帳戶資料庫中的 hello。</span><span class="sxs-lookup"><span data-stu-id="7608d-134">In a query window, execute hello following query toocreate two user accounts in your database.</span></span> <span data-ttu-id="7608d-135">此指令碼授與**db_owner**權限 toohello **app_admin**帳戶並授與**選取**和**更新**toohello 權限**app_user**帳戶。</span><span class="sxs-lookup"><span data-stu-id="7608d-135">This script grants **db_owner** permissions toohello **app_admin** account and grants **SELECT** and **UPDATE** permissions toohello **app_user** account.</span></span> 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user toodb_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission tooSalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product tooapp_user;
   ```

## <a name="create-database-level-firewall"></a><span data-ttu-id="7608d-136">建立資料庫層級防火牆</span><span class="sxs-lookup"><span data-stu-id="7608d-136">Create database-level firewall</span></span>

<span data-ttu-id="7608d-137">為 SQL Database 建立[資料庫層級防火牆規則](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)。</span><span class="sxs-lookup"><span data-stu-id="7608d-137">Create a [database-level firewall rule](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) for your SQL database.</span></span> <span data-ttu-id="7608d-138">此資料庫層級防火牆規則會自動複寫 toohello 您在本教學課程中建立的次要伺服器。</span><span class="sxs-lookup"><span data-stu-id="7608d-138">This database-level firewall rule replicates automatically toohello secondary server that you create in this tutorial.</span></span> <span data-ttu-id="7608d-139">（在本教學課程） 為了簡單起見，使用 hello 公用電腦的 IP 位址 hello 執行 hello 本教學課程中的步驟。</span><span class="sxs-lookup"><span data-stu-id="7608d-139">For simplicity (in this tutorial), use hello public IP address of hello computer on which you are performing hello steps in this tutorial.</span></span> <span data-ttu-id="7608d-140">toodetermine hello IP 位址用於 hello 伺服器層級防火牆規則，針對您目前的電腦，請參閱[建立伺服器層級防火牆](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)。</span><span class="sxs-lookup"><span data-stu-id="7608d-140">toodetermine hello IP address used for hello server-level firewall rule for your current computer, see [Create a server-level firewall](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>  

- <span data-ttu-id="7608d-141">在您開啟查詢視窗中，取代 hello 下列查詢，以您的環境的 hello 適當 IP 位址取代 hello IP 位址中的 hello 上一個查詢。</span><span class="sxs-lookup"><span data-stu-id="7608d-141">In your open query window, replace hello previous query with hello following query, replacing hello IP addresses with hello appropriate IP addresses for your environment.</span></span>  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a><span data-ttu-id="7608d-142">建立作用中異地複寫自動容錯移轉群組</span><span class="sxs-lookup"><span data-stu-id="7608d-142">Create an active geo-replication auto failover group</span></span> 

<span data-ttu-id="7608d-143">使用 Azure PowerShell，建立[作用中地理複寫自動容錯移轉群組](sql-database-geo-replication-overview.md)之間現有的 Azure SQL server 和新的 hello 清空 Azure SQL server 的 Azure 地區，並將範例資料庫 toohello 容錯移轉群組。</span><span class="sxs-lookup"><span data-stu-id="7608d-143">Using Azure PowerShell, create an [active geo-replication auto failover group](sql-database-geo-replication-overview.md) between your existing Azure SQL server and hello new empty Azure SQL server in an Azure region, and then add your sample database toohello failover group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7608d-144">這些 Cmdlet 需要 Azure PowerShell 4.0。</span><span class="sxs-lookup"><span data-stu-id="7608d-144">These cmdlets require Azure PowerShell 4.0.</span></span> [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. <span data-ttu-id="7608d-145">填入您的 PowerShell 指令碼使用您現有的伺服器和範例資料庫 hello 值的變數，並提供容錯移轉群組名稱的全域唯一值。</span><span class="sxs-lookup"><span data-stu-id="7608d-145">Populate variables for your PowerShell scripts using hello values for your existing server and sample database, and provide a globally unique value for failover group name.</span></span>

   ```powershell
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   $myresourcegroupname = "<your resource group name>"
   $mylocation = "<your resource group location>"
   $myservername = "<your existing server name>"
   $mydatabasename = "mySampleDatabase"
   $mydrlocation = "<your disaster recovery location>"
   $mydrservername = "<your disaster recovery server name>"
   $myfailovergroupname = "<your unique failover group name>"
   ```

2. <span data-ttu-id="7608d-146">在容錯移轉區域中建立空的備份伺服器。</span><span class="sxs-lookup"><span data-stu-id="7608d-146">Create an empty backup server in your failover region.</span></span>

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. <span data-ttu-id="7608d-147">建立 hello 兩部伺服器之間容錯移轉群組。</span><span class="sxs-lookup"><span data-stu-id="7608d-147">Create a failover group between hello two servers.</span></span>

   ```powershell
   $myfailovergroup = New-AzureRMSqlDatabaseFailoverGroup `
      –ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -PartnerServerName $mydrservername  `
      –FailoverGroupName $myfailovergroupname `
      –FailoverPolicy Automatic `
      -GracePeriodWithDataLossHours 2
   $myfailovergroup   
   ```

4. <span data-ttu-id="7608d-148">加入您的資料庫 toohello 容錯移轉群組。</span><span class="sxs-lookup"><span data-stu-id="7608d-148">Add your database toohello failover group.</span></span>

   ```powershell
   $myfailovergroup = Get-AzureRmSqlDatabase `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -DatabaseName $mydatabasename | `
    Add-AzureRmSqlDatabaseToFailoverGroup `
      -ResourceGroupName $myresourcegroupname ` `
      -ServerName $myservername `
      -FailoverGroupName $myfailovergroupname
   $myfailovergroup   
   ```

## <a name="install-java-software"></a><span data-ttu-id="7608d-149">安裝 Java 軟體</span><span class="sxs-lookup"><span data-stu-id="7608d-149">Install Java software</span></span>

<span data-ttu-id="7608d-150">本節中的 hello 步驟假設您熟悉開發使用 Java，並使用新 tooworking 使用 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="7608d-150">hello steps in this section assume that you are familiar with developing using Java and are new tooworking with Azure SQL Database.</span></span> 

### <a name="mac-os"></a><span data-ttu-id="7608d-151">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="7608d-151">**Mac OS**</span></span>
<span data-ttu-id="7608d-152">開啟您的終端機，並瀏覽 tooa 想建立 Java 專案的目錄。</span><span class="sxs-lookup"><span data-stu-id="7608d-152">Open your terminal and navigate tooa directory where you plan on creating your Java project.</span></span> <span data-ttu-id="7608d-153">安裝**brew**和**Maven**輸入 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="7608d-153">Install **brew** and **Maven** by entering hello following commands:</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

<span data-ttu-id="7608d-154">如需安裝及設定 Java 和 Maven 環境的詳細指引，請移至 hello[建置應用程式使用 SQL Server](https://www.microsoft.com/sql-server/developer-get-started/)，選取**Java**，選取**MacOS**，然後依照hello 詳細設定 Java 和 Maven 步驟 1.2 和 1.3 中的指示。</span><span class="sxs-lookup"><span data-stu-id="7608d-154">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **MacOS**, and then follow hello detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="7608d-155">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="7608d-155">**Linux (Ubuntu)**</span></span>
<span data-ttu-id="7608d-156">開啟您的終端機，並瀏覽 tooa 想建立 Java 專案的目錄。</span><span class="sxs-lookup"><span data-stu-id="7608d-156">Open your terminal and navigate tooa directory where you plan on creating your Java project.</span></span> <span data-ttu-id="7608d-157">安裝**Maven**輸入 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="7608d-157">Install **Maven** by entering hello following commands:</span></span>

```bash
sudo apt-get install maven
```

<span data-ttu-id="7608d-158">如需安裝及設定 Java 和 Maven 環境的詳細指引，請移至 hello[建置應用程式使用 SQL Server](https://www.microsoft.com/sql-server/developer-get-started/)，選取**Java**，選取**Ubuntu**，然後依照hello 詳細的步驟 1.2、 1.3 和 1.4 中設定 Java 和 Maven 的指示。</span><span class="sxs-lookup"><span data-stu-id="7608d-158">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **Ubuntu**, and then follow hello detailed instructions for configuring Java and Maven in step 1.2, 1.3, and 1.4.</span></span>

### <a name="windows"></a><span data-ttu-id="7608d-159">**Windows**</span><span class="sxs-lookup"><span data-stu-id="7608d-159">**Windows**</span></span>
<span data-ttu-id="7608d-160">安裝[Maven](https://maven.apache.org/download.cgi)使用 hello 官方安裝程式。</span><span class="sxs-lookup"><span data-stu-id="7608d-160">Install [Maven](https://maven.apache.org/download.cgi) using hello official installer.</span></span> <span data-ttu-id="7608d-161">使用的 Maven toohelp 管理相依性、 建置、 測試及執行您的 Java 專案。</span><span class="sxs-lookup"><span data-stu-id="7608d-161">Use Maven toohelp manage dependencies, build, test, and run your Java project.</span></span> <span data-ttu-id="7608d-162">如需安裝及設定 Java 和 Maven 環境的詳細指引，請移至 hello[建置應用程式使用 SQL Server](https://www.microsoft.com/sql-server/developer-get-started/)，選取**Java**選取視窗，然後依照 hello 詳細指示設定 Java 和 Maven 中的步驟 1.2 和 1.3。</span><span class="sxs-lookup"><span data-stu-id="7608d-162">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select Windows, and then follow hello detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

## <a name="create-sqldbsample-project"></a><span data-ttu-id="7608d-163">建立 SqlDbSample 專案</span><span class="sxs-lookup"><span data-stu-id="7608d-163">Create SqlDbSample project</span></span>

1. <span data-ttu-id="7608d-164">在 hello 命令主控台 （例如 Bash) 中，建立 Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="7608d-164">In hello command console (such as Bash), create a Maven project.</span></span> 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. <span data-ttu-id="7608d-165">鍵入 **Y**，然後按一下 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="7608d-165">Type **Y** and click **Enter**.</span></span>
3. <span data-ttu-id="7608d-166">將目錄變更為新建立的專案。</span><span class="sxs-lookup"><span data-stu-id="7608d-166">Change directories into your newly created project.</span></span>

   ```bash
   cd SqlDbSamples
   ```

4. <span data-ttu-id="7608d-167">使用您最愛的編輯器，開啟您的專案資料夾中的 hello pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="7608d-167">Using your favorite editor, open hello pom.xml file in your project folder.</span></span> 

5. <span data-ttu-id="7608d-168">新增 hello Microsoft JDBC Driver for SQL Server 相依性 tooyour Maven 專案開啟慣用的文字編輯器，然後複製並貼上 hello 到 pom.xml 檔案下列行。</span><span class="sxs-lookup"><span data-stu-id="7608d-168">Add hello Microsoft JDBC Driver for SQL Server dependency tooyour Maven project by opening your favorite text editor and copying and pasting hello following lines into your pom.xml file.</span></span> <span data-ttu-id="7608d-169">不要覆寫 hello 預先填入 hello 檔案中的現有值。</span><span class="sxs-lookup"><span data-stu-id="7608d-169">Do not overwrite hello existing values prepopulated in hello file.</span></span> <span data-ttu-id="7608d-170">hello JDBC 相依性必須 hello 較大 「 相依性 」 一節 （） 內貼上動作。</span><span class="sxs-lookup"><span data-stu-id="7608d-170">hello JDBC dependency must be pasted within hello larger “dependencies” section ( ).</span></span>   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. <span data-ttu-id="7608d-171">加入 hello hello 「 相依性 」 一節之後，到 hello pom.xml 檔案遵循 < 屬性 > 一節，以指定針對 Java toocompile hello 專案 hello 版本。</span><span class="sxs-lookup"><span data-stu-id="7608d-171">Specify hello version of Java toocompile hello project against by adding hello following “properties” section into hello pom.xml file after hello "dependencies" section.</span></span> 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. <span data-ttu-id="7608d-172">新增 hello 下列 「 建置 」 一節到 hello pom.xml 檔案之後 hello < 屬性 > 一節 toosupport 資訊清單檔案中 （每瓶）。</span><span class="sxs-lookup"><span data-stu-id="7608d-172">Add hello following "build" section into hello pom.xml file after hello "properties" section toosupport manifest files in jars.</span></span>       

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.apache.maven.plugins</groupId>
         <artifactId>maven-jar-plugin</artifactId>
         <version>3.0.0</version>
         <configuration>
           <archive>
             <manifest>
               <mainClass>com.sqldbsamples.App</mainClass>
             </manifest>
           </archive>
        </configuration>
       </plugin>
     </plugins>
   </build>
   ```
8. <span data-ttu-id="7608d-173">儲存並關閉 hello pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="7608d-173">Save and close hello pom.xml file.</span></span>
9. <span data-ttu-id="7608d-174">開啟 hello App.java 檔案 (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java)，並以下列內容的 hello 取代 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="7608d-174">Open hello App.java file (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) and replace hello contents with hello following contents.</span></span> <span data-ttu-id="7608d-175">Hello 容錯移轉群組名稱取代 hello 容錯移轉群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="7608d-175">Replace hello failover group name with hello name for your failover group.</span></span> <span data-ttu-id="7608d-176">如果您已變更的 hello 資料庫名稱、 使用者或密碼的 hello 值，變更以及這些值。</span><span class="sxs-lookup"><span data-stu-id="7608d-176">If you have changed hello values for hello database name, user, or password, change those values as well.</span></span>

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.Timestamp;
   import java.sql.DriverManager;
   import java.util.Date;
   import java.util.concurrent.TimeUnit;

   public class App {

      private static final String FAILOVER_GROUP_NAME = "myfailovergroupname";
  
      private static final String DB_NAME = "mySampleDatabase";
      private static final String USER = "app_user";
      private static final String PASSWORD = "ChangeYourPassword1";

      private static final String READ_WRITE_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);
      private static final String READ_ONLY_URL = String.format("jdbc:sqlserver://%s.secondary.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);

      public static void main(String[] args) {
         System.out.println("#######################################");
         System.out.println("## GEO DISTRIBUTED DATABASE TUTORIAL ##");
         System.out.println("#######################################");
         System.out.println(""); 

         int highWaterMark = getHighWaterMarkId();

         try {
            for(int i = 1; i < 1000; i++) {
                //  loop will run for about 1 hour
                System.out.print(i + ": insert on primary " + (insertData((highWaterMark + i))?"successful":"failed"));
                TimeUnit.SECONDS.sleep(1);
                System.out.print(", read from secondary " + (selectData((highWaterMark + i))?"successful":"failed") + "\n");
                TimeUnit.SECONDS.sleep(3);
            }
         } catch(Exception e) {
            e.printStackTrace();
      }
   }

   private static boolean insertData(int id) {
      // Insert data into hello product table with a unique product name that we can use toofind hello product again later
      String sql = "INSERT INTO SalesLT.Product (Name, ProductNumber, Color, StandardCost, ListPrice, SellStartDate) VALUES (?,?,?,?,?,?);";

      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         pstmt.setInt(2, 200989 + id + 10000);
         pstmt.setString(3, "Blue");
         pstmt.setDouble(4, 75.00);
         pstmt.setDouble(5, 89.99);
         pstmt.setTimestamp(6, new Timestamp(new Date().getTime()));
         return (1 == pstmt.executeUpdate());
      } catch (Exception e) {
         return false;
      }
   }

   private static boolean selectData(int id) {
      // Query hello data that was previously inserted into hello primary database from hello geo replicated database
      String sql = "SELECT Name, Color, ListPrice FROM SalesLT.Product WHERE Name = ?";

      try (Connection connection = DriverManager.getConnection(READ_ONLY_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         try (ResultSet resultSet = pstmt.executeQuery()) {
            return resultSet.next();
         }
      } catch (Exception e) {
         return false;
      }
   }

   private static int getHighWaterMarkId() {
      // Query hello high water mark id that is stored in hello table toobe able toomake unique inserts 
      String sql = "SELECT MAX(ProductId) FROM SalesLT.Product";
      int result = 1;
        
      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              Statement stmt = connection.createStatement();
              ResultSet resultSet = stmt.executeQuery(sql)) {
         if (resultSet.next()) {
             result =  resultSet.getInt(1);
            }
         } catch (Exception e) {
          e.printStackTrace();
         }
         return result;
      }
   }
   ```
6. <span data-ttu-id="7608d-177">儲存並關閉 hello App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="7608d-177">Save and close hello App.java file.</span></span>

## <a name="compile-and-run-hello-sqldbsample-project"></a><span data-ttu-id="7608d-178">編譯並執行 hello SqlDbSample 專案</span><span class="sxs-lookup"><span data-stu-id="7608d-178">Compile and run hello SqlDbSample project</span></span>

1. <span data-ttu-id="7608d-179">在 hello 命令主控台中，執行 toofollowing 命令。</span><span class="sxs-lookup"><span data-stu-id="7608d-179">In hello command console, execute toofollowing command.</span></span>

   ```bash
   mvn package
   ```
2. <span data-ttu-id="7608d-180">完成後，請執行下列命令 toorun hello 應用程式 （它的執行約 1 小時除非您手動將它停止） 的 hello:</span><span class="sxs-lookup"><span data-stu-id="7608d-180">When finished, execute hello following command toorun hello application (it runs for about 1 hour unless you stop it manually):</span></span>

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a><span data-ttu-id="7608d-181">執行災害復原鑽研</span><span class="sxs-lookup"><span data-stu-id="7608d-181">Perform disaster recovery drill</span></span>

1. <span data-ttu-id="7608d-182">呼叫容錯移轉群組的手動容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="7608d-182">Call manual failover of failover group.</span></span> 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. <span data-ttu-id="7608d-183">在容錯移轉期間觀察 hello 應用程式的結果。</span><span class="sxs-lookup"><span data-stu-id="7608d-183">Observe hello application results during failover.</span></span> <span data-ttu-id="7608d-184">某些插入失敗時 hello DNS 快取重新整理。</span><span class="sxs-lookup"><span data-stu-id="7608d-184">Some inserts fail while hello DNS cache refreshes.</span></span>     

3. <span data-ttu-id="7608d-185">找出災害復原伺服器正在執行的角色。</span><span class="sxs-lookup"><span data-stu-id="7608d-185">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. <span data-ttu-id="7608d-186">容錯回復。</span><span class="sxs-lookup"><span data-stu-id="7608d-186">Failback.</span></span>

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. <span data-ttu-id="7608d-187">在容錯回復期間觀察 hello 應用程式的結果。</span><span class="sxs-lookup"><span data-stu-id="7608d-187">Observe hello application results during failback.</span></span> <span data-ttu-id="7608d-188">某些插入失敗時 hello DNS 快取重新整理。</span><span class="sxs-lookup"><span data-stu-id="7608d-188">Some inserts fail while hello DNS cache refreshes.</span></span>     

6. <span data-ttu-id="7608d-189">找出災害復原伺服器正在執行的角色。</span><span class="sxs-lookup"><span data-stu-id="7608d-189">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a><span data-ttu-id="7608d-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7608d-190">Next steps</span></span> 

<span data-ttu-id="7608d-191">如需詳細資訊，請參閱[作用中異地複寫和容錯移轉群組](sql-database-geo-replication-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7608d-191">For more information, see [Active geo-replication and failover groups](sql-database-geo-replication-overview.md).</span></span>
