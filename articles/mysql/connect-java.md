---
title: "使用 Java 連線到 Azure Database for MySQL | Microsoft Docs"
description: "本快速入門提供 Java 程式碼範例，您可用於從 Azure Database for MySQL 資料庫連線及查詢資料。"
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.devlang: java
ms.date: 06/20/2017
ms.openlocfilehash: 6ffcf3b38a3d868dfa10ea2e2a9d097441387d4f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-database-for-mysql-use-java-to-connect-and-query-data"></a><span data-ttu-id="617f2-103">Azure Database for MySQL︰使用 Java 來連線及查詢資料</span><span class="sxs-lookup"><span data-stu-id="617f2-103">Azure Database for MySQL: Use Java to connect and query data</span></span>
<span data-ttu-id="617f2-104">本快速入門示範如何使用 Java 應用程式來連線到 Azure Database for MySQL。</span><span class="sxs-lookup"><span data-stu-id="617f2-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a Java application.</span></span> <span data-ttu-id="617f2-105">它會顯示如何使用 SQL 陳述式來查詢、插入、更新和刪除資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="617f2-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="617f2-106">本文中的步驟假設您已熟悉使用 Java 進行開發，但不熟悉 Azure Database for MySQL。</span><span class="sxs-lookup"><span data-stu-id="617f2-106">The steps in this article assume that you are familiar with developing using Java, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="617f2-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="617f2-107">Prerequisites</span></span>
<span data-ttu-id="617f2-108">本快速入門使用在以下任一指南中建立的資源作為起點︰</span><span class="sxs-lookup"><span data-stu-id="617f2-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="617f2-109">使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="617f2-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="617f2-110">使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="617f2-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="617f2-111">您也需要：</span><span class="sxs-lookup"><span data-stu-id="617f2-111">You also need to:</span></span>
- <span data-ttu-id="617f2-112">下載 JDBC 驅動程式 [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)</span><span class="sxs-lookup"><span data-stu-id="617f2-112">Download the JDBC driver [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)</span></span>
- <span data-ttu-id="617f2-113">將 JDBC jar 檔案 (例如 mysql-connector-java-5.1.42-bin.jar) 包含在您的應用程式 classpath 中。</span><span class="sxs-lookup"><span data-stu-id="617f2-113">Include the JDBC jar file (for example mysql-connector-java-5.1.42-bin.jar) into your application classpath.</span></span> <span data-ttu-id="617f2-114">如果您在這方面有問題，請參閱環境文件以取得類別路徑的詳細資訊，例如 [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) 或 [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span><span class="sxs-lookup"><span data-stu-id="617f2-114">If you have trouble with this, please consult your environment's documentation for class path specifics, such as [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) or [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span></span>
- <span data-ttu-id="617f2-115">開啟防火牆並針對您的應用程式調整 SSL 設定，以確保 Azure Database for MySQL 連線安全性，進而連線成功。</span><span class="sxs-lookup"><span data-stu-id="617f2-115">Ensure your Azure Database for MySQL connection security is configured with the firewall opened and SSL settings adjusted for your application to connect successfully.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="617f2-116">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="617f2-116">Get connection information</span></span>
<span data-ttu-id="617f2-117">取得連線到 Azure Database for MySQL 所需的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="617f2-117">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="617f2-118">您需要完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="617f2-118">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="617f2-119">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="617f2-119">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="617f2-120">在左側窗格中，按一下 [所有資源]，然後搜尋您所建立的伺服器 (例如 **myserver4demo**)。</span><span class="sxs-lookup"><span data-stu-id="617f2-120">In the left pane, click **All resources**, and then search for the server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="617f2-121">按一下伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="617f2-121">Click the server name.</span></span>
4. <span data-ttu-id="617f2-122">選取伺服器的 [屬性] 頁面。</span><span class="sxs-lookup"><span data-stu-id="617f2-122">Select the server's **Properties** page.</span></span> <span data-ttu-id="617f2-123">記下 [伺服器名稱] 和 [伺服器管理員登入名稱]。</span><span class="sxs-lookup"><span data-stu-id="617f2-123">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="617f2-124">![Azure Database for MySQL 伺服器名稱](./media/connect-java/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="617f2-124">![Azure Database for MySQL server name](./media/connect-java/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="617f2-125">如果您忘記伺服器登入資訊，請瀏覽至 [概觀] 頁面來檢視伺服器管理員登入名稱，並視需要重設密碼。</span><span class="sxs-lookup"><span data-stu-id="617f2-125">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="617f2-126">連線、建立資料表及插入資料</span><span class="sxs-lookup"><span data-stu-id="617f2-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="617f2-127">使用函式搭配 **INSERT** SQL 陳述式，利用下列程式碼來連線和載入資料。</span><span class="sxs-lookup"><span data-stu-id="617f2-127">Use the following code to connect and load the data using the function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="617f2-128">[getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) 方法用來連線到 MySQL。</span><span class="sxs-lookup"><span data-stu-id="617f2-128">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span> <span data-ttu-id="617f2-129">[createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) 和 execute() 方法用來置放和建立資料表。</span><span class="sxs-lookup"><span data-stu-id="617f2-129">Methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and execute() are used to drop and create the table.</span></span> <span data-ttu-id="617f2-130">prepareStatement 物件用來建置 insert 命令，並以 setString() 和 setInt() 繫結參數值。</span><span class="sxs-lookup"><span data-stu-id="617f2-130">The prepareStatement object is used to build the insert commands, with setString() and setInt() to bind the parameter values.</span></span> <span data-ttu-id="617f2-131">executeUpdate() 方法會針對每組要插入值的參數執行此命令。</span><span class="sxs-lookup"><span data-stu-id="617f2-131">Method executeUpdate() runs the command for each set of parameters to insert the values.</span></span> 

<span data-ttu-id="617f2-132">以建立自己的伺服器和資料庫時所指定的值，取代主機、資料庫、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="617f2-132">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class CreateTableInsertRows {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

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

## <a name="read-data"></a><span data-ttu-id="617f2-133">讀取資料</span><span class="sxs-lookup"><span data-stu-id="617f2-133">Read data</span></span>
<span data-ttu-id="617f2-134">使用下列程式碼搭配 **SELECT** SQL 陳述式來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="617f2-134">Use the following code to read the data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="617f2-135">[getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) 方法用來連線到 MySQL。</span><span class="sxs-lookup"><span data-stu-id="617f2-135">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span> <span data-ttu-id="617f2-136">[createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) 和 executeQuery() 方法用來連線和執行 select 陳述式。</span><span class="sxs-lookup"><span data-stu-id="617f2-136">The methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and executeQuery() are used to connect and run the select statement.</span></span> <span data-ttu-id="617f2-137">結果會使用 [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) 物件進行處理。</span><span class="sxs-lookup"><span data-stu-id="617f2-137">The results are processed using a [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) object.</span></span> 

<span data-ttu-id="617f2-138">以建立自己的伺服器和資料庫時所指定的值，取代主機、資料庫、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="617f2-138">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class ReadTable {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database", e);
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
                throw new SQLException("Encountered an error when executing given sql statement", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database."); 
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="update-data"></a><span data-ttu-id="617f2-139">更新資料</span><span class="sxs-lookup"><span data-stu-id="617f2-139">Update data</span></span>
<span data-ttu-id="617f2-140">使用下列程式碼搭配 **UPDATE** SQL 陳述式來變更資料。</span><span class="sxs-lookup"><span data-stu-id="617f2-140">Use the following code to change the data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="617f2-141">[getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) 方法用來連線到 MySQL。</span><span class="sxs-lookup"><span data-stu-id="617f2-141">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span> <span data-ttu-id="617f2-142">[prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) 和 executeUpdate() 方法用來準備及執行 update 陳述式。</span><span class="sxs-lookup"><span data-stu-id="617f2-142">The methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used to prepare and run the update statement.</span></span> 

<span data-ttu-id="617f2-143">以建立自己的伺服器和資料庫時所指定的值，取代主機、資料庫、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="617f2-143">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class UpdateTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }
        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

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

## <a name="delete-data"></a><span data-ttu-id="617f2-144">刪除資料</span><span class="sxs-lookup"><span data-stu-id="617f2-144">Delete data</span></span>
<span data-ttu-id="617f2-145">使用下列程式碼搭配 **DELETE** SQL 陳述式來移除資料。</span><span class="sxs-lookup"><span data-stu-id="617f2-145">Use the following code to remove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="617f2-146">[getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) 方法用來連線到 MySQL。</span><span class="sxs-lookup"><span data-stu-id="617f2-146">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span>  <span data-ttu-id="617f2-147">[prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) 和 executeUpdate() 方法用來準備及執行 update 陳述式。</span><span class="sxs-lookup"><span data-stu-id="617f2-147">The methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used to prepare and run the update statement.</span></span> 

<span data-ttu-id="617f2-148">以建立自己的伺服器和資料庫時所指定的值，取代主機、資料庫、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="617f2-148">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class DeleteTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";
        
        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database", e);
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

## <a name="next-steps"></a><span data-ttu-id="617f2-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="617f2-149">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="617f2-150">使用傾印和還原來將 MySQL 資料庫移轉至適用於 MySQL 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="617f2-150">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
