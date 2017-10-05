---
title: "使用 Java 連線至 Azure Database for PostgreSQL | Microsoft Docs"
description: "本快速入門提供 Java 程式碼範例，您可用於從 Azure Database for PostgreSQL 連線及查詢資料。"
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
ms.openlocfilehash: 730a3f464b4437c260d09abc026a186a0e26293c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-java-to-connect-and-query-data"></a><span data-ttu-id="30ecf-103">Azure Database for PostgreSQL︰使用 Java 連線及查詢資料</span><span class="sxs-lookup"><span data-stu-id="30ecf-103">Azure Database for PostgreSQL: Use Java to connect and query data</span></span>
<span data-ttu-id="30ecf-104">本快速入門示範如何使用 Java 應用程式來連線到 Azure Database for PostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="30ecf-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a Java application.</span></span> <span data-ttu-id="30ecf-105">它會顯示如何使用 SQL 陳述式來查詢、插入、更新和刪除資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="30ecf-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="30ecf-106">本文中的步驟假設您已熟悉使用 Java 進行開發，但不熟悉 Azure Database for PostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="30ecf-106">The steps in this article assume that you are familiar with developing using Java, and that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30ecf-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="30ecf-107">Prerequisites</span></span>
<span data-ttu-id="30ecf-108">本快速入門使用在以下任一指南中建立的資源作為起點︰</span><span class="sxs-lookup"><span data-stu-id="30ecf-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="30ecf-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="30ecf-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="30ecf-110">建立 DB - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="30ecf-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="30ecf-111">您也需要：</span><span class="sxs-lookup"><span data-stu-id="30ecf-111">You also need to:</span></span>
- <span data-ttu-id="30ecf-112">下載符合您 Java 和 Java Development Kit 版本的 [PostgreSQL JDBC 驅動程式](https://jdbc.postgresql.org/download.html)。</span><span class="sxs-lookup"><span data-stu-id="30ecf-112">Download the [PostgreSQL JDBC Driver](https://jdbc.postgresql.org/download.html) matching your version of Java and the Java Development Kit.</span></span>
- <span data-ttu-id="30ecf-113">在您的應用程式 classpath 中納入 PostgreSQL JDBC jar 檔案 (例如 postgresql-42.1.1.jar)。</span><span class="sxs-lookup"><span data-stu-id="30ecf-113">Include the PostgreSQL JDBC jar file (for example postgresql-42.1.1.jar) in your application classpath.</span></span> <span data-ttu-id="30ecf-114">如需詳細資訊，請參閱 [classpath 詳細資料](https://jdbc.postgresql.org/documentation/head/classpath.html)。</span><span class="sxs-lookup"><span data-stu-id="30ecf-114">For more information, see [classpath details](https://jdbc.postgresql.org/documentation/head/classpath.html).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="30ecf-115">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="30ecf-115">Get connection information</span></span>
<span data-ttu-id="30ecf-116">取得連線到 Azure Database for PostgreSQL 所需的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="30ecf-116">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="30ecf-117">您需要完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="30ecf-117">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="30ecf-118">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="30ecf-118">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="30ecf-119">從 Azure 入口網站的左側功能表中，按一下 [所有資源]，然後搜尋您所建立的伺服器，例如 **mypgserver-20170401**。</span><span class="sxs-lookup"><span data-stu-id="30ecf-119">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="30ecf-120">按一下伺服器名稱 [mypgserver-20170401]。</span><span class="sxs-lookup"><span data-stu-id="30ecf-120">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="30ecf-121">選取伺服器的 [概觀] 頁面。</span><span class="sxs-lookup"><span data-stu-id="30ecf-121">Select the server's **Overview** page.</span></span> <span data-ttu-id="30ecf-122">記下 [伺服器名稱] 和 [伺服器管理員登入名稱]。</span><span class="sxs-lookup"><span data-stu-id="30ecf-122">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="30ecf-123">![Azure Database for PostgreSQL - 伺服器管理員登入](./media/connect-java/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="30ecf-123">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-java/1-connection-string.png)</span></span>
5. <span data-ttu-id="30ecf-124">如果您忘記伺服器登入資訊，請瀏覽至 [概觀] 頁面來檢視伺服器管理員登入名稱，並視需要重設密碼。</span><span class="sxs-lookup"><span data-stu-id="30ecf-124">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="30ecf-125">連線、建立資料表及插入資料</span><span class="sxs-lookup"><span data-stu-id="30ecf-125">Connect, create table, and insert data</span></span>
<span data-ttu-id="30ecf-126">使用函式搭配 **INSERT** SQL 陳述式，利用下列程式碼來連線和載入資料。</span><span class="sxs-lookup"><span data-stu-id="30ecf-126">Use the following code to connect and load the data using the function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="30ecf-127">[getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html)、[createStatement()](https://jdbc.postgresql.org/documentation/head/query.html) 和 [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) 方法用來連線、置放及建立資料表。</span><span class="sxs-lookup"><span data-stu-id="30ecf-127">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used to connect, drop, and create the table.</span></span> <span data-ttu-id="30ecf-128">[prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) 物件用來建置 insert 命令，並以 setString() 和 setInt() 繫結參數值。</span><span class="sxs-lookup"><span data-stu-id="30ecf-128">The [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) object is used to build the insert commands, with setString() and setInt() to bind the parameter values.</span></span> <span data-ttu-id="30ecf-129">[executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) 方法會針對每組參數執行此命令。</span><span class="sxs-lookup"><span data-stu-id="30ecf-129">Method [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) runs the command for each set of parameters.</span></span> 

<span data-ttu-id="30ecf-130">以建立自己的伺服器和資料庫時所指定的值，取代主機、資料庫、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="30ecf-130">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

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

        // check that the driver is installed
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
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
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
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
    
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="read-data"></a><span data-ttu-id="30ecf-131">讀取資料</span><span class="sxs-lookup"><span data-stu-id="30ecf-131">Read data</span></span>
<span data-ttu-id="30ecf-132">使用下列程式碼搭配 **SELECT** SQL 陳述式來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="30ecf-132">Use the following code to read the data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="30ecf-133">[getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html)、[createStatement()](https://jdbc.postgresql.org/documentation/head/query.html) 和 [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) 方法用來連線、建立和執行 select 陳述式。</span><span class="sxs-lookup"><span data-stu-id="30ecf-133">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used to connect, create, and run the select statement.</span></span> <span data-ttu-id="30ecf-134">結果會使用 [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html) 物件進行處理。</span><span class="sxs-lookup"><span data-stu-id="30ecf-134">The results are processed using a [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html) object.</span></span> 

<span data-ttu-id="30ecf-135">以建立自己的伺服器和資料庫時所指定的值，取代主機、資料庫、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="30ecf-135">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

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

        // check that the driver is installed
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
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
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
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}

```

## <a name="update-data"></a><span data-ttu-id="30ecf-136">更新資料</span><span class="sxs-lookup"><span data-stu-id="30ecf-136">Update data</span></span>
<span data-ttu-id="30ecf-137">使用下列程式碼搭配 **UPDATE** SQL 陳述式來變更資料。</span><span class="sxs-lookup"><span data-stu-id="30ecf-137">Use the following code to change the data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="30ecf-138">[getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html)、[prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html) 和 [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) 方法用來連線、準備及執行 update 陳述式。</span><span class="sxs-lookup"><span data-stu-id="30ecf-138">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used to connect, prepare, and run the update statement.</span></span> 

<span data-ttu-id="30ecf-139">以建立自己的伺服器和資料庫時所指定的值，取代主機、資料庫、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="30ecf-139">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

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

        // check that the driver is installed
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
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Modify some data in table.
                int nRowsUpdated = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?;");
                preparedStatement.setInt(1, 200);
                preparedStatement.setString(2, "banana");
                nRowsUpdated += preparedStatement.executeUpdate();
                System.out.println(String.format("Updated %d row(s) of data.", nRowsUpdated));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```
## <a name="delete-data"></a><span data-ttu-id="30ecf-140">刪除資料</span><span class="sxs-lookup"><span data-stu-id="30ecf-140">Delete data</span></span>
<span data-ttu-id="30ecf-141">使用下列程式碼搭配 **DELETE** SQL 陳述式來移除資料。</span><span class="sxs-lookup"><span data-stu-id="30ecf-141">Use the following code to remove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="30ecf-142">[getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html)、[prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html) 和 [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) 方法用來連線、準備及執行 delete 陳述式。</span><span class="sxs-lookup"><span data-stu-id="30ecf-142">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used to connect, prepare, and run the delete statement.</span></span> 

<span data-ttu-id="30ecf-143">以建立自己的伺服器和資料庫時所指定的值，取代主機、資料庫、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="30ecf-143">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

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

        // check that the driver is installed
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
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Delete some data from table.
                int nRowsDeleted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("DELETE FROM inventory WHERE name = ?;");
                preparedStatement.setString(1, "orange");
                nRowsDeleted += preparedStatement.executeUpdate();
                System.out.println(String.format("Deleted %d row(s) of data.", nRowsDeleted));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="30ecf-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="30ecf-144">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="30ecf-145">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="30ecf-145">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
