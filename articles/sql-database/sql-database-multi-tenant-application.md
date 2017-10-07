---
title: "使用 Azure SQL Database 的 aaaImplement 多租用戶 SaaS 應用程式 |Microsoft 文件"
description: "使用 Azure SQL Database 實作多租用戶 SaaS 應用程式。"
services: sql-database
documentationcenter: 
author: AyoOlubeko
manager: jhubbard
editor: monicar
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/08/2017
ms.author: AyoOlubek
ms.openlocfilehash: b87b8f296e2c20a8f674b56375f43fdc92df76d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a><span data-ttu-id="28c5e-103">使用 Azure SQL Database 實作多租用戶 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="28c5e-103">Implement a multi-tenant SaaS application using Azure SQL Database</span></span>

<span data-ttu-id="28c5e-104">多租用戶應用程式是裝載在雲端環境中的應用程式，以及提供的 hello 相同設定的服務 toohundreds 或數千個租用戶共用或檢視彼此的資料。</span><span class="sxs-lookup"><span data-stu-id="28c5e-104">A multi-tenant application is an application hosted in a cloud environment and that provides hello same set of services toohundreds or thousands of tenants who do not share or see each other’s data.</span></span> <span data-ttu-id="28c5e-105">範例會提供在雲端裝載環境中的服務 tootenants 的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="28c5e-105">An example is an SaaS application that provides services tootenants in a cloud-hosted environment.</span></span> <span data-ttu-id="28c5e-106">此模型中每個租用戶隔離 hello 資料，並能最佳化 hello 資源分配的成本。</span><span class="sxs-lookup"><span data-stu-id="28c5e-106">This model isolates hello data for each tenant and optimizes hello distribution of resources for cost.</span></span> 

<span data-ttu-id="28c5e-107">本教學課程示範如何 toocreate 多租用戶 SaaS 應用程式使用 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="28c5e-107">This tutorial demonstrates how toocreate a multi-tenant SaaS application using Azure SQL Database.</span></span>

<span data-ttu-id="28c5e-108">在本教學課程中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="28c5e-108">In this tutorial, you will learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="28c5e-109">設定資料庫環境 toosupport 多租用戶 SaaS 應用程式，使用 hello 資料庫每個租用戶模式</span><span class="sxs-lookup"><span data-stu-id="28c5e-109">Set up a database environment toosupport a multi-tenant SaaS application, using hello Database-per-tenant pattern</span></span>
> * <span data-ttu-id="28c5e-110">建立租用戶目錄</span><span class="sxs-lookup"><span data-stu-id="28c5e-110">Create a tenant catalog</span></span>
> * <span data-ttu-id="28c5e-111">佈建租用戶資料庫並將其註冊 hello 租用戶目錄中</span><span class="sxs-lookup"><span data-stu-id="28c5e-111">Provision a tenant database and register it in hello tenant catalog</span></span>
> * <span data-ttu-id="28c5e-112">設定範例 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="28c5e-112">Set up a sample Java application</span></span> 
> * <span data-ttu-id="28c5e-113">使用簡單的 Java 主控台應用程式存取租用戶資料庫</span><span class="sxs-lookup"><span data-stu-id="28c5e-113">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="28c5e-114">刪除租用戶</span><span class="sxs-lookup"><span data-stu-id="28c5e-114">Delete a tenant</span></span>

<span data-ttu-id="28c5e-115">如果您沒有 Azure 訂用帳戶，請在開始之前先[建立免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="28c5e-115">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28c5e-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="28c5e-116">Prerequisites</span></span>

<span data-ttu-id="28c5e-117">toocomplete 此教學課程，請確定您有：</span><span class="sxs-lookup"><span data-stu-id="28c5e-117">toocomplete this tutorial, make sure you have:</span></span>

* <span data-ttu-id="28c5e-118">已安裝的 hello 最新版本的 PowerShell 和 hello[最新的 Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="28c5e-118">Installed hello newest version of PowerShell and hello [latest Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span></span>

* <span data-ttu-id="28c5e-119">已安裝的 hello 最新版本的[SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。</span><span class="sxs-lookup"><span data-stu-id="28c5e-119">Installed hello latest version of [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> <span data-ttu-id="28c5e-120">安裝 SQL Server Management Studio 也會安裝 hello SQLPackage，可以是使用的 tooautomate 範圍內的資料庫開發工作的命令列公用程式最新版本。</span><span class="sxs-lookup"><span data-stu-id="28c5e-120">Installing SQL Server Management Studio also installs hello latest version of SQLPackage, a command-line utility that can be used tooautomate a range of database development tasks.</span></span>

* <span data-ttu-id="28c5e-121">已安裝的 hello [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html)和 hello[最新的 JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="28c5e-121">Installed hello [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) and hello [latest JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span> 

* <span data-ttu-id="28c5e-122">已安裝 [Apache Maven](https://maven.apache.org/download.cgi) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="28c5e-122">Installed [Apache Maven](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="28c5e-123">將使用 maven toohelp 管理相依性、 建置、 測試及執行 hello 範例 Java 專案</span><span class="sxs-lookup"><span data-stu-id="28c5e-123">Maven will be used toohelp manage dependencies, build, test and run hello sample Java project</span></span>

## <a name="set-up-data-environment"></a><span data-ttu-id="28c5e-124">設定資料環境</span><span class="sxs-lookup"><span data-stu-id="28c5e-124">Set up data environment</span></span>

<span data-ttu-id="28c5e-125">您將為每個租用戶佈建一個資料庫。</span><span class="sxs-lookup"><span data-stu-id="28c5e-125">You will be provisioning a database per tenant.</span></span> <span data-ttu-id="28c5e-126">hello 資料庫每個租用戶模型提供 hello 高程度的租用戶，較小的 DevOps 成本之間的隔離。</span><span class="sxs-lookup"><span data-stu-id="28c5e-126">hello database-per-tenant model provides hello highest degree of isolation between tenants, with little DevOps cost.</span></span> <span data-ttu-id="28c5e-127">雲端資源的 toooptimize hello 成本，您將也會佈建 hello 租用戶資料庫到彈性集區可讓您 toooptimize hello 價格效能群組的資料庫。</span><span class="sxs-lookup"><span data-stu-id="28c5e-127">toooptimize hello cost of cloud resources, you will also be provisioning hello tenant databases into an elastic pool which allows you toooptimize hello price performance for a group of databases.</span></span> <span data-ttu-id="28c5e-128">有關其他佈建模型的資料庫 toolearn[此處](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models)。</span><span class="sxs-lookup"><span data-stu-id="28c5e-128">toolearn about other database provisioning models [see here](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span></span>

<span data-ttu-id="28c5e-129">請遵循這些步驟 toocreate，SQL server 和將裝載所有租用戶資料庫的彈性集區。</span><span class="sxs-lookup"><span data-stu-id="28c5e-129">Follow these steps toocreate a SQL server and an elastic pool that will host all your tenant databases.</span></span> 

1. <span data-ttu-id="28c5e-130">建立變數 toostore 值將用於在 hello hello 教學課程的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="28c5e-130">Create variables toostore values that will be used in hello rest of hello tutorial.</span></span> <span data-ttu-id="28c5e-131">請確定 toomodify hello IP 位址變數 tooinclude 您的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="28c5e-131">Make sure toomodify hello IP address variable tooinclude your IP address</span></span> 
   
   ```PowerShell 
   # Set an admin login and password for your database
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   
   # Create random unique names for logical server and tenants
   $servername = "server-$(Get-Random)"
   $tenant1 = "geolamice"
   $tenant2 = "ranplex"
   
   # Store current client IP address (modify tooinclude your IP address)
   $startIpAddress = 0.0.0.0 
   $endIpAddress = 0.0.0.0
   ```
   
2. <span data-ttu-id="28c5e-132">登入 tooAzure 並建立 SQL server 和彈性集區</span><span class="sxs-lookup"><span data-stu-id="28c5e-132">Login tooAzure and create a SQL server and elastic pool</span></span> 
   
   ```PowerShell
   # Login tooAzure 
   Login-AzureRmAccount
   
   # Create resource group 
   New-AzureRmResourceGroup -Name "myResourceGroup" -Location "northcentralus"
   
   # Create logical SQL Server with firewall rules 
   New-AzureRmSqlServer -ResourceGroupName "myResourceGroup" `
       -ServerName $servername `
       -Location "northcentralus" `
       -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   
   New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
       -ServerName $servername `
       -FirewallRuleName "singleAddress" -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
   
   # Create elastic pool 
   New-AzureRmSqlElasticPool -ResourceGroupName "myResourceGroup"
       -ServerName $servername `
       -ElasticPoolName "myElasticPool" `
       -Edition "Standard" `
       -Dtu 50 `
       -DatabaseDtuMin 10 `
       -DatabaseDtuMax 20
   ```
   
## <a name="create-tenant-catalog"></a><span data-ttu-id="28c5e-133">建立租用戶目錄</span><span class="sxs-lookup"><span data-stu-id="28c5e-133">Create tenant catalog</span></span> 

<span data-ttu-id="28c5e-134">在多租用戶 SaaS 應用程式中，很重要的 tooknow 租用戶的資訊儲存在何處。</span><span class="sxs-lookup"><span data-stu-id="28c5e-134">In a multi-tenant SaaS application, it’s important tooknow where information for a tenant is stored.</span></span> <span data-ttu-id="28c5e-135">此資訊通常儲存在目錄資料庫中。</span><span class="sxs-lookup"><span data-stu-id="28c5e-135">This is commonly stored in a catalog database.</span></span> <span data-ttu-id="28c5e-136">hello 類別目錄資料庫是使用的 toohold 租用戶和租用戶的資料儲存所在的資料庫之間的對應。</span><span class="sxs-lookup"><span data-stu-id="28c5e-136">hello catalog database is used toohold a mapping between a tenant and a database in which that tenant’s data is stored.</span></span>  <span data-ttu-id="28c5e-137">hello 基本模式適用於多租用戶是否，或使用單一租用戶資料庫。</span><span class="sxs-lookup"><span data-stu-id="28c5e-137">hello basic pattern applies whether a multi-tenant or a single-tenant database is used.</span></span>

<span data-ttu-id="28c5e-138">請遵循這些步驟 toocreate hello 範例 SaaS 應用程式類別目錄資料庫。</span><span class="sxs-lookup"><span data-stu-id="28c5e-138">Follow these steps toocreate a catalog database for hello sample SaaS application.</span></span>

```PowerShell
# Create empty database in pool
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "tenantCatalog" `
    -ElasticPoolName "myElasticPool"

# Create table tootrack mapping between tenants and their databases
$commandText = "
CREATE TABLE Tenants
(
   TenantId         INT IDENTITY PRIMARY KEY,
   TenantName       NVARCHAR(128) NOT NULL,
   TenantDatabase   NVARCHAR(128) NOT NULL
);

CREATE INDEX IX_TenantName ON Tenants (TenantName);"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a><span data-ttu-id="28c5e-139">佈建 'tenant1' 的資料庫，並在租用戶目錄中註冊</span><span class="sxs-lookup"><span data-stu-id="28c5e-139">Provision database for 'tenant1' and register in tenant catalog</span></span> 
<span data-ttu-id="28c5e-140">使用 Powershell tooprovision 資料庫新租用戶的 '租用戶 1' 與註冊此租用戶 hello 目錄中。</span><span class="sxs-lookup"><span data-stu-id="28c5e-140">Use Powershell tooprovision a database for a new tenant 'tenant1' and register this tenant in hello catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant1'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant1');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant1 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register 'tenant1' in hello tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant1', '$tenant1');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a><span data-ttu-id="28c5e-141">佈建 'tenant2' 的資料庫，並在租用戶目錄中註冊</span><span class="sxs-lookup"><span data-stu-id="28c5e-141">Provision database for 'tenant2' and register in tenant catalog</span></span>
<span data-ttu-id="28c5e-142">使用 Powershell tooprovision 資料庫新租用戶 'tenant2' 與註冊此租用戶 hello 目錄中。</span><span class="sxs-lookup"><span data-stu-id="28c5e-142">Use Powershell tooprovision a database for a new tenant 'tenant2' and register this tenant in hello catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant2'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant2 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant2');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant2 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register tenant 'tenant2' in hello tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant2', '$tenant2');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="set-up-sample-java-application"></a><span data-ttu-id="28c5e-143">設定範例 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="28c5e-143">Set up sample Java application</span></span> 

1. <span data-ttu-id="28c5e-144">建立 Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="28c5e-144">Create a maven project.</span></span> <span data-ttu-id="28c5e-145">命令提示字元 視窗中輸入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="28c5e-145">Type hello following in a command prompt window:</span></span>
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. <span data-ttu-id="28c5e-146">新增此相依性、 語言層級，並建置選項 toosupport （每瓶） toohello pom.xml 檔案中的資訊清單檔案：</span><span class="sxs-lookup"><span data-stu-id="28c5e-146">Add this dependency, language level, and build option toosupport manifest files in jars toohello pom.xml file:</span></span>
   
   ```XML
   <dependency>
         <groupId>com.microsoft.sqlserver</groupId>
         <artifactId>mssql-jdbc</artifactId>
         <version>6.1.0.jre8</version>
   </dependency>
   
   <properties>
         <maven.compiler.source>1.8</maven.compiler.source>
         <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   
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

3. <span data-ttu-id="28c5e-147">加入下列 hello hello App.java 檔案：</span><span class="sxs-lookup"><span data-stu-id="28c5e-147">Add hello following into hello App.java file:</span></span>

   ```java 
   package com.sqldbsamples;
   
   import java.util.Map;
   
   import java.util.HashMap;
   
   import java.io.BufferedReader;
   
   import java.io.InputStreamReader;
   
   import java.sql.Connection;
   
   import java.sql.Statement;
   
   import java.sql.PreparedStatement;
   
   import java.sql.ResultSet;
   
   import java.sql.DriverManager;
   
   public class App {
   
   private static final String SERVER_NAME = "your-server-name";
   
   private static final String CATALOG_DB_NAME = "tenantCatalog";
   
   private static final String USER = "ServerAdmin";
   
   private static final String PASSWORD = "ChangeYourAdminPassword1";
   
   private static final String CATALOG_DB_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, CATALOG_DB_NAME, USER, PASSWORD);
   
   private static final String CMD_LIST = "LIST";

   private static final String CMD_QUERY = "QUERY";

   private static final String CMD_QUIT = "QUIT";
   
   public static void main(String[] args) {
   
   System.out.println("\n############################");
   
   System.out.println("## SAAS DATABASE TUTORIAL ##");
   
   System.out.println("############################\n");
   
   System.out.println("OPTIONS");
   
   System.out.println(" " + CMD_LIST + " - list tenants");
   
   System.out.println(" " + CMD_QUERY + " <NAME> - connect and tenant query tenant <NAME>");
   
   System.out.println(" " + CMD_QUIT + " - quit hello application\n");
   
   try (BufferedReader br = new BufferedReader(new InputStreamReader(System.in))) {
   
   while(true) {
   
   String[] input = br.readLine().split("\\s");
   
   if (null != input && input.length > 0) {
   
   if (input[0].equalsIgnoreCase(CMD_LIST)) {
   
   listTenants();
   
   } else if (input[0].toLowerCase().startsWith(CMD_QUERY.toLowerCase()) && input.length == 2) {
   
   queryTenant(input[1].trim());
   
   } else if (input[0].equalsIgnoreCase(CMD_QUIT)) {
   
   break;
   
   } else {
   
   System.out.println(" -> Command not supported");
   
   }
   
   }
   
   System.out.println("");
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void listTenants() {
   
   // List all tenants that currently exist in hello system
   
   String sql = "SELECT TenantName FROM Tenants";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   Statement stmt = connection.createStatement();
   
   ResultSet resultSet = stmt.executeQuery(sql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void queryTenant(String name) {
   
   // Query hello data that was previously inserted into hello primary database from hello geo replicated database
   
   String url = null;
   
   String sql = "SELECT TenantDatabase FROM Tenants WHERE TenantName = ?";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   PreparedStatement pstmt = connection.prepareStatement(sql)) {
   
   pstmt.setString(1, name);
   
   try (ResultSet resultSet = pstmt.executeQuery()) {
   
   if (resultSet.next()) {
   
   url = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, resultSet.getString(1), USER, PASSWORD);
   
   }
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   if (null != url) {
   
   String tenantSql = "SELECT TenantName FROM WhoAmI";
   
   try (Connection connection = DriverManager.getConnection(url);
   
   Statement stmt = connection.createStatement();

   ResultSet resultSet = stmt.executeQuery(tenantSql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> Entry in table WhoAmI in tenant " + name + " is: " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   } else {
   
   System.out.println(" -> Tenant " + name + " not found");
   
   }
   
   }
   
   }
   ```

4. <span data-ttu-id="28c5e-148">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="28c5e-148">Save hello file.</span></span>

5. <span data-ttu-id="28c5e-149">請移 toocommand 主控台並執行</span><span class="sxs-lookup"><span data-stu-id="28c5e-149">Go toocommand console and execute</span></span>

   ```bash
   mvn package
   ```

6. <span data-ttu-id="28c5e-150">完成後，請執行下列 toorun hello 應用程式的 hello</span><span class="sxs-lookup"><span data-stu-id="28c5e-150">When finished, execute hello following toorun hello application</span></span> 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
<span data-ttu-id="28c5e-151">如果已順利執行，hello 輸出看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="28c5e-151">hello output will look like this if it runs successfully:</span></span>

```
############################

## SAAS DATABASE TUTORIAL ##

############################

OPTIONS

LIST - list tenants

QUERY <NAME> - connect and tenant query tenant <NAME>

QUIT - quit hello application

* List hello tenants

* Query tenants you created
```

## <a name="delete-first-tenant"></a><span data-ttu-id="28c5e-152">刪除第一個租用戶</span><span class="sxs-lookup"><span data-stu-id="28c5e-152">Delete first tenant</span></span> 
<span data-ttu-id="28c5e-153">使用 PowerShell toodelete hello 租用戶資料庫與類別目錄項目 hello 第一個租用戶。</span><span class="sxs-lookup"><span data-stu-id="28c5e-153">Use PowerShell toodelete hello tenant database and catalog entry for hello first tenant.</span></span>

```PowerShell
# Remove 'tenant1' from catalog 
$commandText = "DELETE FROM Tenants WHERE TenantName = '$tenant1';"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Delete database 
Remove-AzureRmSqlDatabase -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1
```

<span data-ttu-id="28c5e-154">請再次嘗試連線太 '租用戶 1' 使用 hello Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="28c5e-154">Try connecting too'tenant1' using hello Java application.</span></span> <span data-ttu-id="28c5e-155">您會收到錯誤，指出該 hello 租用戶不存在。</span><span class="sxs-lookup"><span data-stu-id="28c5e-155">You will get an error stating that hello tenant does not exist.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28c5e-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="28c5e-156">Next steps</span></span> 

<span data-ttu-id="28c5e-157">在本教學課程中，您了解：</span><span class="sxs-lookup"><span data-stu-id="28c5e-157">In this tutorial, you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="28c5e-158">設定資料庫環境 toosupport 多租用戶 SaaS 應用程式，使用 hello 資料庫每個租用戶模式</span><span class="sxs-lookup"><span data-stu-id="28c5e-158">Set up a database environment toosupport a multi-tenant SaaS application, using hello Database-per-tenant pattern</span></span>
> * <span data-ttu-id="28c5e-159">建立租用戶目錄</span><span class="sxs-lookup"><span data-stu-id="28c5e-159">Create a tenant catalog</span></span>
> * <span data-ttu-id="28c5e-160">佈建租用戶資料庫並將其註冊 hello 租用戶目錄中</span><span class="sxs-lookup"><span data-stu-id="28c5e-160">Provision a tenant database and register it in hello tenant catalog</span></span>
> * <span data-ttu-id="28c5e-161">設定範例 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="28c5e-161">Set up a sample Java application</span></span> 
> * <span data-ttu-id="28c5e-162">使用簡單的 Java 主控台應用程式存取租用戶資料庫</span><span class="sxs-lookup"><span data-stu-id="28c5e-162">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="28c5e-163">刪除租用戶</span><span class="sxs-lookup"><span data-stu-id="28c5e-163">Delete a tenant</span></span>

* <span data-ttu-id="28c5e-164">如需一般工作的 PowerShell 範例，請參閱 [SQL Database PowerShell 範例](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span><span class="sxs-lookup"><span data-stu-id="28c5e-164">PowerShell samples for common tasks, see [SQL Database PowerShell samples](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span></span>

* <span data-ttu-id="28c5e-165">如需多租用戶 SaaS 應用程式的模式，請參閱[設計模式](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span><span class="sxs-lookup"><span data-stu-id="28c5e-165">Design patterns for multi-tenant SaaS applications see [Design patterns](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span></span>

* <span data-ttu-id="28c5e-166">如需一般 Azure 的工作的 Java 範例，請參閱 [Java 開發人員中心](https://azure.microsoft.com/develop/java/)</span><span class="sxs-lookup"><span data-stu-id="28c5e-166">Java samples for common Azure tasks, see [Java Developer Center](https://azure.microsoft.com/develop/java/)</span></span>



