---
title: "使用 Java PostgreSQL 連接 tooAzure 資料庫 |Microsoft 文件"
description: "本快速入門提供您可以使用 tooconnect 和查詢 PostgreSQL 資料從 Azure 資料庫的 Java 程式碼範例。"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: java
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 8f6e0a47a0d6dfebf29eb56c31ccccabd7c2b670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-java-tooconnect-and-query-data"></a><span data-ttu-id="297af-103">Azure PostgreSQL 資料庫： 使用 Java tooconnect 和查詢資料</span><span class="sxs-lookup"><span data-stu-id="297af-103">Azure Database for PostgreSQL: Use Java tooconnect and query data</span></span>
<span data-ttu-id="297af-104">本快速入門示範如何 tooconnect tooan PostgreSQL 使用 Java 應用程式的 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="297af-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a Java application.</span></span> <span data-ttu-id="297af-105">它會顯示 toouse SQL 陳述式 tooquery，如何插入、 更新和刪除 hello 資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="297af-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="297af-106">hello 本文章中的步驟假設您已熟悉開發使用 Java，且新 tooworking Azure PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="297af-106">hello steps in this article assume that you are familiar with developing using Java, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="297af-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="297af-107">Prerequisites</span></span>
<span data-ttu-id="297af-108">本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：</span><span class="sxs-lookup"><span data-stu-id="297af-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="297af-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="297af-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="297af-110">建立 DB - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="297af-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="297af-111">您也需要：</span><span class="sxs-lookup"><span data-stu-id="297af-111">You also need to:</span></span>
- <span data-ttu-id="297af-112">下載 hello [PostgreSQL JDBC 驅動程式](https://jdbc.postgresql.org/download.html)比對您的 Java 和 hello Java Development Kit 版本。</span><span class="sxs-lookup"><span data-stu-id="297af-112">Download hello [PostgreSQL JDBC Driver](https://jdbc.postgresql.org/download.html) matching your version of Java and hello Java Development Kit.</span></span>
- <span data-ttu-id="297af-113">Hello PostgreSQL JDBC jar 檔案 (例如 42.1.1.jar postgresql) 併入您的應用程式 classpath 中。</span><span class="sxs-lookup"><span data-stu-id="297af-113">Include hello PostgreSQL JDBC jar file (for example postgresql-42.1.1.jar) in your application classpath.</span></span> <span data-ttu-id="297af-114">如需詳細資訊，請參閱 [classpath 詳細資料](https://jdbc.postgresql.org/documentation/head/classpath.html)。</span><span class="sxs-lookup"><span data-stu-id="297af-114">For more information, see [classpath details](https://jdbc.postgresql.org/documentation/head/classpath.html).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="297af-115">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="297af-115">Get connection information</span></span>
<span data-ttu-id="297af-116">取得 PostgreSQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="297af-116">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="297af-117">您需要 hello 完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="297af-117">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="297af-118">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="297af-118">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="297af-119">在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，並搜尋您已經建立，例如 hello 伺服器**mypgserver 20170401**。</span><span class="sxs-lookup"><span data-stu-id="297af-119">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="297af-120">按一下伺服器名稱，hello **mypgserver 20170401**。</span><span class="sxs-lookup"><span data-stu-id="297af-120">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="297af-121">選取 hello 伺服器**概觀**頁面。</span><span class="sxs-lookup"><span data-stu-id="297af-121">Select hello server's **Overview** page.</span></span> <span data-ttu-id="297af-122">請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。</span><span class="sxs-lookup"><span data-stu-id="297af-122">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="297af-123">![Azure Database for PostgreSQL - 伺服器管理員登入](./media/connect-java/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="297af-123">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-java/1-connection-string.png)</span></span>
5. <span data-ttu-id="297af-124">如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="297af-124">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="297af-125">連線、建立資料表及插入資料</span><span class="sxs-lookup"><span data-stu-id="297af-125">Connect, create table, and insert data</span></span>
<span data-ttu-id="297af-126">下列程式碼 tooconnect 和負載 hello 資料使用 hello 函式的使用 hello**插入**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="297af-126">Use hello following code tooconnect and load hello data using hello function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="297af-127">hello 方法[getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html)， [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html)，和[executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html)會使用的 tooconnect，卸除，並建立 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="297af-127">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used tooconnect, drop, and create hello table.</span></span> <span data-ttu-id="297af-128">hello [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html)物件是使用的 toobuild hello insert 命令，使用 setString() 和 setInt() toobind hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="297af-128">hello [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) object is used toobuild hello insert commands, with setString() and setInt() toobind hello parameter values.</span></span> <span data-ttu-id="297af-129">方法[executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html)執行 hello 每個參數集的命令。</span><span class="sxs-lookup"><span data-stu-id="297af-129">Method [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) runs hello command for each set of parameters.</span></span> 

<span data-ttu-id="297af-130">您指定當您建立您自己的伺服器和資料庫的 hello 值取代 hello 主機、 資料庫、 使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="297af-130">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class CreateTableInsertRows {

    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Drop previous table of same name if one exists.
                Statement statement = connection.createStatement();
                statement.execute("DROP TABLE IF EXISTS inventory;");
                System.out.println("Finished dropping table (if existed).");
    
                // Create table.
                statement.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
                System.out.println("Created table.");
    
                // Insert some data into table.
                int nRowsInserted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("INSERT INTO inventory (name, quantity) VALUES (?, ?);");
                preparedStatement.setString(1, "banana");
                preparedStatement.setInt(2, 150);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "orange");
                preparedStatement.setInt(2, 154);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "apple");
                preparedStatement.setInt(2, 100);
                nRowsInserted += preparedStatement.executeUpdate();
                System.out.println(String.format("Inserted %d row(s) of data.", nRowsInserted));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
    
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="read-data"></a><span data-ttu-id="297af-131">讀取資料</span><span class="sxs-lookup"><span data-stu-id="297af-131">Read data</span></span>
<span data-ttu-id="297af-132">使用 hello 下列程式碼與 tooread hello 資料**選取**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="297af-132">Use hello following code tooread hello data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="297af-133">hello 方法[getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html)， [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html)，和[executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html)會使用的 tooconnect，建立及執行 hello select 陳述式。</span><span class="sxs-lookup"><span data-stu-id="297af-133">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used tooconnect, create, and run hello select statement.</span></span> <span data-ttu-id="297af-134">使用處理 hello 結果[ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html)物件。</span><span class="sxs-lookup"><span data-stu-id="297af-134">hello results are processed using a [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html) object.</span></span> 

<span data-ttu-id="297af-135">您指定當您建立您自己的伺服器和資料庫的 hello 值取代 hello 主機、 資料庫、 使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="297af-135">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class ReadTable {

    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
    
                Statement statement = connection.createStatement();
                ResultSet results = statement.executeQuery("SELECT * from inventory;");
                while (results.next())
                {
                    String outputString = 
                        String.format(
                            "Data row = (%s, %s, %s)",
                            results.getString(1),
                            results.getString(2),
                            results.getString(3));
                    System.out.println(outputString);
                }
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}

```

## <a name="update-data"></a><span data-ttu-id="297af-136">更新資料</span><span class="sxs-lookup"><span data-stu-id="297af-136">Update data</span></span>
<span data-ttu-id="297af-137">使用 hello 下列程式碼與 toochange hello 資料**更新**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="297af-137">Use hello following code toochange hello data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="297af-138">hello 方法[getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html)， [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html)，和[executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html)會使用的 tooconnect，準備和執行 hello update 陳述式。</span><span class="sxs-lookup"><span data-stu-id="297af-138">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used tooconnect, prepare, and run hello update statement.</span></span> 

<span data-ttu-id="297af-139">您指定當您建立您自己的伺服器和資料庫的 hello 值取代 hello 主機、 資料庫、 使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="297af-139">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class UpdateTable {
    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Modify some data in table.
                int nRowsUpdated = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?;");
                preparedStatement.setInt(1, 200);
                preparedStatement.setString(2, "banana");
                nRowsUpdated += preparedStatement.executeUpdate();
                System.out.println(String.format("Updated %d row(s) of data.", nRowsUpdated));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```
## <a name="delete-data"></a><span data-ttu-id="297af-140">刪除資料</span><span class="sxs-lookup"><span data-stu-id="297af-140">Delete data</span></span>
<span data-ttu-id="297af-141">使用 hello 下列程式碼與 tooremove 資料**刪除**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="297af-141">Use hello following code tooremove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="297af-142">hello 方法[getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html)， [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html)，和[executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html)會使用的 tooconnect，準備和執行 hello delete 陳述式。</span><span class="sxs-lookup"><span data-stu-id="297af-142">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used tooconnect, prepare, and run hello delete statement.</span></span> 

<span data-ttu-id="297af-143">您指定當您建立您自己的伺服器和資料庫的 hello 值取代 hello 主機、 資料庫、 使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="297af-143">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class DeleteTable {
    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Delete some data from table.
                int nRowsDeleted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("DELETE FROM inventory WHERE name = ?;");
                preparedStatement.setString(1, "orange");
                nRowsDeleted += preparedStatement.executeUpdate();
                System.out.println(String.format("Deleted %d row(s) of data.", nRowsDeleted));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="297af-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="297af-144">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="297af-145">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="297af-145">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
