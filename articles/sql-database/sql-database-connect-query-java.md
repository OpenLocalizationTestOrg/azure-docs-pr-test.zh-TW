---
title: "Azure SQL Database 的 aaaUse Java tooquery |Microsoft 文件"
description: "本主題說明如何 toouse Java toocreate 連接 tooan Azure SQL Database 和查詢使用 TRANSACT-SQL 陳述式的程式。"
services: sql-database
documentationcenter: 
author: ajlam
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: andrela
ms.openlocfilehash: f014edbe38ca0e7b6e43f4eb4d2e53d3561bf3e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-java-tooquery-an-azure-sql-database"></a><span data-ttu-id="8362f-103">使用 Java tooquery Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="8362f-103">Use Java tooquery an Azure SQL database</span></span>

<span data-ttu-id="8362f-104">本快速入門示範如何 toouse [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) tooconnect tooan Azure SQL 資料庫，然後將 TRANSACT-SQL 陳述式 tooquery 資料。</span><span class="sxs-lookup"><span data-stu-id="8362f-104">This quick start demonstrates how toouse [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) tooconnect tooan Azure SQL database and then use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8362f-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="8362f-105">Prerequisites</span></span>

<span data-ttu-id="8362f-106">toocomplete 此快速入門教學課程，請確定您擁有 hello 下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="8362f-106">toocomplete this quick start tutorial, make sure you have hello following prerequisites:</span></span>

- <span data-ttu-id="8362f-107">Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="8362f-107">An Azure SQL database.</span></span> <span data-ttu-id="8362f-108">本快速入門會使用 hello 資源建立在其中一個這些快速入門：</span><span class="sxs-lookup"><span data-stu-id="8362f-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="8362f-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="8362f-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="8362f-110">建立 DB - CLI</span><span class="sxs-lookup"><span data-stu-id="8362f-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="8362f-111">建立 DB - PowerShell</span><span class="sxs-lookup"><span data-stu-id="8362f-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="8362f-112">A[伺服器層級防火牆規則](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)您使用此快速入門教學課程中的 hello 電腦 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8362f-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="8362f-113">您已安裝適用於您作業系統的 JAVA 和相關軟體。</span><span class="sxs-lookup"><span data-stu-id="8362f-113">You have installed Java and related software for your operating system.</span></span>

    - <span data-ttu-id="8362f-114">**MacOS**：安裝 Homebrew 和 JAVA，然後再安裝 Maven。</span><span class="sxs-lookup"><span data-stu-id="8362f-114">**MacOS**: Install Homebrew and Java, and then install Maven.</span></span> <span data-ttu-id="8362f-115">請參閱[步驟 1.2 和 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/)。</span><span class="sxs-lookup"><span data-stu-id="8362f-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span></span>
    - <span data-ttu-id="8362f-116">**Ubuntu**： 安裝 hello Java Development Kit，並安裝 Maven。</span><span class="sxs-lookup"><span data-stu-id="8362f-116">**Ubuntu**:  Install hello Java Development Kit, and install Maven.</span></span> <span data-ttu-id="8362f-117">請參閱[步驟 1.2、1.3 和 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/)。</span><span class="sxs-lookup"><span data-stu-id="8362f-117">See [Step 1.2, 1.3, and 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span></span>
    - <span data-ttu-id="8362f-118">**Windows**: hello Java Development Kit 和 Maven 安裝。</span><span class="sxs-lookup"><span data-stu-id="8362f-118">**Windows**: Install hello Java Development Kit, and Maven.</span></span> <span data-ttu-id="8362f-119">請參閱[步驟 1.2 和 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/)。</span><span class="sxs-lookup"><span data-stu-id="8362f-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="8362f-120">SQL Server 連線資訊</span><span class="sxs-lookup"><span data-stu-id="8362f-120">SQL server connection information</span></span>

<span data-ttu-id="8362f-121">收到 hello 連線所需的資訊 tooconnect toohello Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="8362f-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="8362f-122">您需要 hello 完整的伺服器名稱、 資料庫名稱，以及 hello 下一個程序中的登入資訊。</span><span class="sxs-lookup"><span data-stu-id="8362f-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="8362f-123">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="8362f-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8362f-124">選取**SQL 資料庫**從 hello 左側功能表中，按一下您的資料庫上 hello **SQL 資料庫**頁面。</span><span class="sxs-lookup"><span data-stu-id="8362f-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="8362f-125">在 hello**概觀**為您的資料庫頁面上，檢閱 hello 完整的伺服器名稱，如 hello 下列影像所示： 您可以將滑鼠停留在 hello 伺服器名稱 toobring 向上 hello**按一下 toocopy**選項。</span><span class="sxs-lookup"><span data-stu-id="8362f-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image: You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="8362f-127">如果您忘記您的伺服器登入資訊，請瀏覽 toohello SQL 資料庫伺服器頁面 tooview hello 伺服器管理員的名稱。</span><span class="sxs-lookup"><span data-stu-id="8362f-127">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span>  <span data-ttu-id="8362f-128">如有需要，重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="8362f-128">If necessary, reset hello password.</span></span>     

## <a name="create-maven-project-and-dependencies"></a><span data-ttu-id="8362f-129">**建立 Maven 專案和相依性**</span><span class="sxs-lookup"><span data-stu-id="8362f-129">**Create Maven project and dependencies**</span></span>
1. <span data-ttu-id="8362f-130">從終端機 hello，建立新的 Maven 專案，稱為**sqltest**。</span><span class="sxs-lookup"><span data-stu-id="8362f-130">From hello terminal, create a new Maven project called **sqltest**.</span></span> 

   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=sqltest" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```

2. <span data-ttu-id="8362f-131">在出現提示時按下 Y 鍵 。</span><span class="sxs-lookup"><span data-stu-id="8362f-131">Enter **Y** when prompted.</span></span>
3. <span data-ttu-id="8362f-132">將目錄變更為太**sqltest**並開啟***pom.xml***與慣用的文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="8362f-132">Change directory too**sqltest** and open ***pom.xml*** with your favorite text editor.</span></span>  <span data-ttu-id="8362f-133">新增 hello **Microsoft JDBC Driver for SQL Server** tooyour 專案相依性使用 hello 下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="8362f-133">Add hello **Microsoft JDBC Driver for SQL Server** tooyour project's dependencies using hello following code:</span></span>

   ```xml
   <dependency>
       <groupId>com.microsoft.sqlserver</groupId>
       <artifactId>mssql-jdbc</artifactId>
       <version>6.2.1.jre8</version>
   </dependency>
   ```

4. <span data-ttu-id="8362f-134">此外，在***pom.xml***，新增下列內容 tooyour 專案 hello。</span><span class="sxs-lookup"><span data-stu-id="8362f-134">Also in ***pom.xml***, add hello following properties tooyour project.</span></span>  <span data-ttu-id="8362f-135">如果您沒有屬性區段，您可以將它在 hello 相依性後面。</span><span class="sxs-lookup"><span data-stu-id="8362f-135">If you don't have a properties section, you can add it after hello dependencies.</span></span>

   ```xml
   <properties>
       <maven.compiler.source>1.8</maven.compiler.source>
       <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```

5. <span data-ttu-id="8362f-136">儲存並關閉 pom.xml。</span><span class="sxs-lookup"><span data-stu-id="8362f-136">Save and close ***pom.xml***.</span></span>

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="8362f-137">插入程式碼 tooquery SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="8362f-137">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="8362f-138">您的 Maven 專案中應該已經有名為 App.java 的檔案，位於：\sqltest\src\main\java\com\sqlsamples\App.java</span><span class="sxs-lookup"><span data-stu-id="8362f-138">You should already have a file called ***App.java*** in your Maven project located at:  ..\sqltest\src\main\java\com\sqlsamples\App.java</span></span>

2. <span data-ttu-id="8362f-139">開啟 hello 檔案，並取代其內容與 hello 下列程式碼並新增值 hello 適當伺服器、 資料庫、 使用者及密碼。</span><span class="sxs-lookup"><span data-stu-id="8362f-139">Open hello file and replace its contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.DriverManager;

   public class App {

    public static void main(String[] args) {
    
        // Connect toodatabase
           String hostName = "your_server.database.windows.net";
           String dbName = "your_database";
           String user = "your_username";
           String password = "your_password";
           String url = String.format("jdbc:sqlserver://%s:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", hostName, dbName, user, password);
           Connection connection = null;

           try {
                   connection = DriverManager.getConnection(url);
                   String schema = connection.getSchema();
                   System.out.println("Successful connection - Schema: " + schema);

                   System.out.println("Query data example:");
                   System.out.println("=========================================");

                   // Create and execute a SELECT SQL statement.
                   String selectSql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName " 
                       + "FROM [SalesLT].[ProductCategory] pc "  
                       + "JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid";
                
                   try (Statement statement = connection.createStatement();
                       ResultSet resultSet = statement.executeQuery(selectSql)) {

                           // Print results from select statement
                           System.out.println("Top 20 categories:");
                           while (resultSet.next())
                           {
                               System.out.println(resultSet.getString(1) + " "
                                   + resultSet.getString(2));
                           }
                    connection.close();
                   }                   
           }
           catch (Exception e) {
                   e.printStackTrace();
           }
       }
   }
   ```

## <a name="run-hello-code"></a><span data-ttu-id="8362f-140">執行 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="8362f-140">Run hello code</span></span>

1. <span data-ttu-id="8362f-141">在 hello 命令提示字元中執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="8362f-141">At hello command prompt, run hello following commands:</span></span>

   ```bash
   mvn package
   mvn -q exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```

2. <span data-ttu-id="8362f-142">請確認 hello 前 20 個資料列會傳回，，然後關閉 hello 應用程式視窗。</span><span class="sxs-lookup"><span data-stu-id="8362f-142">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8362f-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8362f-143">Next steps</span></span>
- [<span data-ttu-id="8362f-144">設計您的第一個 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="8362f-144">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="8362f-145">Microsoft JDBC Driver for SQL Server</span><span class="sxs-lookup"><span data-stu-id="8362f-145">Microsoft JDBC Driver for SQL Server</span></span>](https://github.com/microsoft/mssql-jdbc)
- [<span data-ttu-id="8362f-146">回報問題/發問</span><span class="sxs-lookup"><span data-stu-id="8362f-146">Report issues/ask questions</span></span>](https://github.com/microsoft/mssql-jdbc/issues)

