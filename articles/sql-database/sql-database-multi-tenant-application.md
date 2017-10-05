---
title: "使用 Azure SQL Database 實作多租用戶 SaaS 應用程式 | Microsoft Docs"
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
ms.openlocfilehash: 0aea69d86a51c38c99a72f46737de1eea27bef83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a><span data-ttu-id="e1076-103">使用 Azure SQL Database 實作多租用戶 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="e1076-103">Implement a multi-tenant SaaS application using Azure SQL Database</span></span>

<span data-ttu-id="e1076-104">多租用戶應用程式是指雲端環境中裝載的應用程式，可將同一組服務提供給不共用或看不到彼此資料的數百或數千個租用戶。</span><span class="sxs-lookup"><span data-stu-id="e1076-104">A multi-tenant application is an application hosted in a cloud environment and that provides the same set of services to hundreds or thousands of tenants who do not share or see each other’s data.</span></span> <span data-ttu-id="e1076-105">例如，提供服務給雲端裝載環境中租用戶的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1076-105">An example is an SaaS application that provides services to tenants in a cloud-hosted environment.</span></span> <span data-ttu-id="e1076-106">此模型會隔離每個租用戶的資料，並且針對成本最佳化資源的分配。</span><span class="sxs-lookup"><span data-stu-id="e1076-106">This model isolates the data for each tenant and optimizes the distribution of resources for cost.</span></span> 

<span data-ttu-id="e1076-107">本教學課程示範如何使用 Azure SQL Database 建立多租用戶 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1076-107">This tutorial demonstrates how to create a multi-tenant SaaS application using Azure SQL Database.</span></span>

<span data-ttu-id="e1076-108">在本教學課程中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="e1076-108">In this tutorial, you will learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="e1076-109">使用每個租用戶一個資料庫的模式設定資料庫環境來支援多租用戶 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="e1076-109">Set up a database environment to support a multi-tenant SaaS application, using the Database-per-tenant pattern</span></span>
> * <span data-ttu-id="e1076-110">建立租用戶目錄</span><span class="sxs-lookup"><span data-stu-id="e1076-110">Create a tenant catalog</span></span>
> * <span data-ttu-id="e1076-111">佈建租用戶資料庫並在租用戶目錄中註冊</span><span class="sxs-lookup"><span data-stu-id="e1076-111">Provision a tenant database and register it in the tenant catalog</span></span>
> * <span data-ttu-id="e1076-112">設定範例 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="e1076-112">Set up a sample Java application</span></span> 
> * <span data-ttu-id="e1076-113">使用簡單的 Java 主控台應用程式存取租用戶資料庫</span><span class="sxs-lookup"><span data-stu-id="e1076-113">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="e1076-114">刪除租用戶</span><span class="sxs-lookup"><span data-stu-id="e1076-114">Delete a tenant</span></span>

<span data-ttu-id="e1076-115">如果您沒有 Azure 訂用帳戶，請在開始之前先[建立免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="e1076-115">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1076-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="e1076-116">Prerequisites</span></span>

<span data-ttu-id="e1076-117">若要完成本教學課程，請確定您具有下列項目︰</span><span class="sxs-lookup"><span data-stu-id="e1076-117">To complete this tutorial, make sure you have:</span></span>

* <span data-ttu-id="e1076-118">已安裝最新版本的 PowerShell 和[最新的 Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="e1076-118">Installed the newest version of PowerShell and the [latest Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span></span>

* <span data-ttu-id="e1076-119">已安裝最新版本的 [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。</span><span class="sxs-lookup"><span data-stu-id="e1076-119">Installed the latest version of [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> <span data-ttu-id="e1076-120">安裝 SQL Server Management Studio 時亦會安裝最新版本的 SQLPackage，此命令列公用程式可用於自動化處理資料庫開發工作的範圍。</span><span class="sxs-lookup"><span data-stu-id="e1076-120">Installing SQL Server Management Studio also installs the latest version of SQLPackage, a command-line utility that can be used to automate a range of database development tasks.</span></span>

* <span data-ttu-id="e1076-121">已在電腦上安裝 [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) \(英文\)，以及[最新的 JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="e1076-121">Installed the [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) and the [latest JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span> 

* <span data-ttu-id="e1076-122">已安裝 [Apache Maven](https://maven.apache.org/download.cgi) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="e1076-122">Installed [Apache Maven](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="e1076-123">Maven 將用來協助管理相依性、建置、測試及執行範例 Java 專案。</span><span class="sxs-lookup"><span data-stu-id="e1076-123">Maven will be used to help manage dependencies, build, test and run the sample Java project</span></span>

## <a name="set-up-data-environment"></a><span data-ttu-id="e1076-124">設定資料環境</span><span class="sxs-lookup"><span data-stu-id="e1076-124">Set up data environment</span></span>

<span data-ttu-id="e1076-125">您將為每個租用戶佈建一個資料庫。</span><span class="sxs-lookup"><span data-stu-id="e1076-125">You will be provisioning a database per tenant.</span></span> <span data-ttu-id="e1076-126">每個租用戶一個資料庫的模型，只需一點 DevOps 成本，即可提供租用戶之間最高程度的隔離。</span><span class="sxs-lookup"><span data-stu-id="e1076-126">The database-per-tenant model provides the highest degree of isolation between tenants, with little DevOps cost.</span></span> <span data-ttu-id="e1076-127">若要最佳化雲端資源的成本，您也要將租用戶資料庫佈建到彈性集區，讓您能最佳化一組資料庫的價格效能。</span><span class="sxs-lookup"><span data-stu-id="e1076-127">To optimize the cost of cloud resources, you will also be provisioning the tenant databases into an elastic pool which allows you to optimize the price performance for a group of databases.</span></span> <span data-ttu-id="e1076-128">若要了解其他資料庫佈建模型，請[參閱此處](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models)。</span><span class="sxs-lookup"><span data-stu-id="e1076-128">To learn about other database provisioning models [see here](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span></span>

<span data-ttu-id="e1076-129">遵循下列步驟來建立 SQL 伺服器和裝載所有租用戶資料庫的彈性集區。</span><span class="sxs-lookup"><span data-stu-id="e1076-129">Follow these steps to create a SQL server and an elastic pool that will host all your tenant databases.</span></span> 

1. <span data-ttu-id="e1076-130">建立變數來儲存將用於本教學課程其餘部分的值。</span><span class="sxs-lookup"><span data-stu-id="e1076-130">Create variables to store values that will be used in the rest of the tutorial.</span></span> <span data-ttu-id="e1076-131">確定修改 IP 位址變數修改以包含您的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="e1076-131">Make sure to modify the IP address variable to include your IP address</span></span> 
   
   ```PowerShell 
   # Set an admin login and password for your database
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   
   # Create random unique names for logical server and tenants
   $servername = "server-$(Get-Random)"
   $tenant1 = "geolamice"
   $tenant2 = "ranplex"
   
   # Store current client IP address (modify to include your IP address)
   $startIpAddress = 0.0.0.0 
   $endIpAddress = 0.0.0.0
   ```
   
2. <span data-ttu-id="e1076-132">登入 Azure 並建立 SQL 伺服器和彈性集區</span><span class="sxs-lookup"><span data-stu-id="e1076-132">Login to Azure and create a SQL server and elastic pool</span></span> 
   
   ```PowerShell
   # Login to Azure 
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
   
## <a name="create-tenant-catalog"></a><span data-ttu-id="e1076-133">建立租用戶目錄</span><span class="sxs-lookup"><span data-stu-id="e1076-133">Create tenant catalog</span></span> 

<span data-ttu-id="e1076-134">在多租用戶 SaaS 應用程式中，請務必了解租用戶的資訊儲存在何處。</span><span class="sxs-lookup"><span data-stu-id="e1076-134">In a multi-tenant SaaS application, it’s important to know where information for a tenant is stored.</span></span> <span data-ttu-id="e1076-135">此資訊通常儲存在目錄資料庫中。</span><span class="sxs-lookup"><span data-stu-id="e1076-135">This is commonly stored in a catalog database.</span></span> <span data-ttu-id="e1076-136">目錄資料庫用來保留租用戶與儲存該租用戶資料的資料庫之間的對應。</span><span class="sxs-lookup"><span data-stu-id="e1076-136">The catalog database is used to hold a mapping between a tenant and a database in which that tenant’s data is stored.</span></span>  <span data-ttu-id="e1076-137">無論使用多租用戶或單一租用戶資料庫，都適用基本模式。</span><span class="sxs-lookup"><span data-stu-id="e1076-137">The basic pattern applies whether a multi-tenant or a single-tenant database is used.</span></span>

<span data-ttu-id="e1076-138">遵循下列步驟來建立範例 SaaS 應用程式的目錄資料庫。</span><span class="sxs-lookup"><span data-stu-id="e1076-138">Follow these steps to create a catalog database for the sample SaaS application.</span></span>

```PowerShell
# Create empty database in pool
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "tenantCatalog" `
    -ElasticPoolName "myElasticPool"

# Create table to track mapping between tenants and their databases
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

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a><span data-ttu-id="e1076-139">佈建 'tenant1' 的資料庫，並在租用戶目錄中註冊</span><span class="sxs-lookup"><span data-stu-id="e1076-139">Provision database for 'tenant1' and register in tenant catalog</span></span> 
<span data-ttu-id="e1076-140">使用 PowerShell 佈建新租用戶 'tenant1' 的資料庫，並在目錄中註冊此租用戶。</span><span class="sxs-lookup"><span data-stu-id="e1076-140">Use Powershell to provision a database for a new tenant 'tenant1' and register this tenant in the catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant1'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into the table 
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

# Register 'tenant1' in the tenant catalog 
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

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a><span data-ttu-id="e1076-141">佈建 'tenant2' 的資料庫，並在租用戶目錄中註冊</span><span class="sxs-lookup"><span data-stu-id="e1076-141">Provision database for 'tenant2' and register in tenant catalog</span></span>
<span data-ttu-id="e1076-142">使用 PowerShell 佈建新租用戶 'tenant2' 的資料庫，並在目錄中註冊此租用戶。</span><span class="sxs-lookup"><span data-stu-id="e1076-142">Use Powershell to provision a database for a new tenant 'tenant2' and register this tenant in the catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant2'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant2 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into the table 
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

# Register tenant 'tenant2' in the tenant catalog 
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

## <a name="set-up-sample-java-application"></a><span data-ttu-id="e1076-143">設定範例 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="e1076-143">Set up sample Java application</span></span> 

1. <span data-ttu-id="e1076-144">建立 Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="e1076-144">Create a maven project.</span></span> <span data-ttu-id="e1076-145">在命令提示字元視窗中輸入下列命令︰</span><span class="sxs-lookup"><span data-stu-id="e1076-145">Type the following in a command prompt window:</span></span>
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. <span data-ttu-id="e1076-146">在 pom.xml 檔案中新增此相依性、語言等級以及支援 jars 中資訊清單檔案的建置選項︰</span><span class="sxs-lookup"><span data-stu-id="e1076-146">Add this dependency, language level, and build option to support manifest files in jars to the pom.xml file:</span></span>
   
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

3. <span data-ttu-id="e1076-147">在 App.java 檔案中新增下列內容︰</span><span class="sxs-lookup"><span data-stu-id="e1076-147">Add the following into the App.java file:</span></span>

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
   
   System.out.println(" " + CMD_QUIT + " - quit the application\n");
   
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
   
   // List all tenants that currently exist in the system
   
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
   
   // Query the data that was previously inserted into the primary database from the geo replicated database
   
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

4. <span data-ttu-id="e1076-148">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="e1076-148">Save the file.</span></span>

5. <span data-ttu-id="e1076-149">移至命令主控台並執行</span><span class="sxs-lookup"><span data-stu-id="e1076-149">Go to command console and execute</span></span>

   ```bash
   mvn package
   ```

6. <span data-ttu-id="e1076-150">完成時，執行下列命令以執行應用程式</span><span class="sxs-lookup"><span data-stu-id="e1076-150">When finished, execute the following to run the application</span></span> 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
<span data-ttu-id="e1076-151">如果執行成功，輸出會看起來像這樣︰</span><span class="sxs-lookup"><span data-stu-id="e1076-151">The output will look like this if it runs successfully:</span></span>

```
############################

## SAAS DATABASE TUTORIAL ##

############################

OPTIONS

LIST - list tenants

QUERY <NAME> - connect and tenant query tenant <NAME>

QUIT - quit the application

* List the tenants

* Query tenants you created
```

## <a name="delete-first-tenant"></a><span data-ttu-id="e1076-152">刪除第一個租用戶</span><span class="sxs-lookup"><span data-stu-id="e1076-152">Delete first tenant</span></span> 
<span data-ttu-id="e1076-153">使用 PowerShell 刪除第一個租用戶的租用戶資料庫與目錄項目。</span><span class="sxs-lookup"><span data-stu-id="e1076-153">Use PowerShell to delete the tenant database and catalog entry for the first tenant.</span></span>

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

<span data-ttu-id="e1076-154">使用 Java 應用程式嘗試連線到 'tenant1'。</span><span class="sxs-lookup"><span data-stu-id="e1076-154">Try connecting to 'tenant1' using the Java application.</span></span> <span data-ttu-id="e1076-155">您會收到租用戶不存在的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="e1076-155">You will get an error stating that the tenant does not exist.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1076-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e1076-156">Next steps</span></span> 

<span data-ttu-id="e1076-157">在本教學課程中，您了解：</span><span class="sxs-lookup"><span data-stu-id="e1076-157">In this tutorial, you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="e1076-158">使用每個租用戶一個資料庫的模式設定資料庫環境來支援多租用戶 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="e1076-158">Set up a database environment to support a multi-tenant SaaS application, using the Database-per-tenant pattern</span></span>
> * <span data-ttu-id="e1076-159">建立租用戶目錄</span><span class="sxs-lookup"><span data-stu-id="e1076-159">Create a tenant catalog</span></span>
> * <span data-ttu-id="e1076-160">佈建租用戶資料庫並在租用戶目錄中註冊</span><span class="sxs-lookup"><span data-stu-id="e1076-160">Provision a tenant database and register it in the tenant catalog</span></span>
> * <span data-ttu-id="e1076-161">設定範例 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="e1076-161">Set up a sample Java application</span></span> 
> * <span data-ttu-id="e1076-162">使用簡單的 Java 主控台應用程式存取租用戶資料庫</span><span class="sxs-lookup"><span data-stu-id="e1076-162">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="e1076-163">刪除租用戶</span><span class="sxs-lookup"><span data-stu-id="e1076-163">Delete a tenant</span></span>

* <span data-ttu-id="e1076-164">如需一般工作的 PowerShell 範例，請參閱 [SQL Database PowerShell 範例](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span><span class="sxs-lookup"><span data-stu-id="e1076-164">PowerShell samples for common tasks, see [SQL Database PowerShell samples](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span></span>

* <span data-ttu-id="e1076-165">如需多租用戶 SaaS 應用程式的模式，請參閱[設計模式](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span><span class="sxs-lookup"><span data-stu-id="e1076-165">Design patterns for multi-tenant SaaS applications see [Design patterns](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span></span>

* <span data-ttu-id="e1076-166">如需一般 Azure 的工作的 Java 範例，請參閱 [Java 開發人員中心](https://azure.microsoft.com/develop/java/)</span><span class="sxs-lookup"><span data-stu-id="e1076-166">Java samples for common Azure tasks, see [Java Developer Center](https://azure.microsoft.com/develop/java/)</span></span>



