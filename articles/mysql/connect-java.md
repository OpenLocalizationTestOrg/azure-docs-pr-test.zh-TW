---
title: "使用 Java 的 MySQL 連接 tooAzure 資料庫 |Microsoft 文件"
description: "本快速入門提供您可以使用 tooconnect 與查詢資料從 Azure 資料庫的 MySQL 資料庫的 Java 程式碼範例。"
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
ms.openlocfilehash: d584b5491d29700b36fae26800c59d93ceb3e265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-java-tooconnect-and-query-data"></a>Azure 資料庫的 MySQL： 使用 Java tooconnect 和查詢資料
本快速入門示範如何 tooconnect tooan Azure 資料庫的 MySQL 使用 Java 應用程式。 它會顯示 toouse SQL 陳述式 tooquery，如何插入、 更新和刪除 hello 資料庫中的資料。 hello 本文章中的步驟假設您已熟悉開發使用 Java，且新 tooworking 與 MySQL 的 Azure 資料庫。

## <a name="prerequisites"></a>必要條件
本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：
- [使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器](./quickstart-create-mysql-server-database-using-azure-cli.md)

您也需要：
- 下載 hello JDBC driver [MySQL 連接器/J](https://dev.mysql.com/downloads/connector/j/)
- 將 hello JDBC jar 檔案 (例如 mysql-連接器-java-5.1.42-bin.jar) 包含您應用程式的 classpath。 如果您在這方面有問題，請參閱環境文件以取得類別路徑的詳細資訊，例如 [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) 或 [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)
- 請確定您的 Azure 資料庫的 MySQL 連線安全性已與 hello 防火牆開啟且 SSL 設定進行已成功調整應用程式 tooconnect。

## <a name="get-connection-information"></a>取得連線資訊
取得 MySQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。 您需要 hello 完整的伺服器名稱和登入認證。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. Hello 左窗格中，按一下 **所有資源**，然後搜尋您所建立的 hello server (例如， **myserver4demo**)。
3. 按一下 hello 伺服器名稱。
4. 選取 hello 伺服器**屬性**頁面。 請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。
 ![Azure Database for MySQL 伺服器名稱](./media/connect-java/1_server-properties-name-login.png)
5. 如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。

## <a name="connect-create-table-and-insert-data"></a>連線、建立資料表及插入資料
下列程式碼 tooconnect 和負載 hello 資料使用 hello 函式的使用 hello**插入**SQL 陳述式。 hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html)方法是使用的 tooconnect tooMySQL。 方法[createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html)和 execute （） 都使用的 toodrop 建立 hello 資料表。 hello prepareStatement 物件是使用的 toobuild hello insert 命令，使用 setString() 和 setInt() toobind hello 參數值。 方法 executeUpdate() 執行 hello 命令，針對每個參數 tooinsert hello 值集。 

您指定當您建立您自己的伺服器和資料庫的 hello 值取代 hello 主機、 資料庫、 使用者和密碼參數。

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

        // check that hello driver is installed
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

## <a name="read-data"></a>讀取資料
使用 hello 下列程式碼與 tooread hello 資料**選取**SQL 陳述式。 hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html)方法是使用的 tooconnect tooMySQL。 hello 方法[createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html)和 executeQuery() 都使用的 tooconnect 執行 hello select 陳述式。 使用處理 hello 結果[ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html)物件。 

您指定當您建立您自己的伺服器和資料庫的 hello 值取代 hello 主機、 資料庫、 使用者和密碼參數。

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

        // check that hello driver is installed
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
            throw new SQLException("Failed toocreate connection toodatabase", e);
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
                throw new SQLException("Encountered an error when executing given sql statement", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase."); 
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="update-data"></a>更新資料
使用 hello 下列程式碼與 toochange hello 資料**更新**SQL 陳述式。 hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html)方法是使用的 tooconnect tooMySQL。 hello 方法[prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html)和 executeUpdate() 都使用的 tooprepare 執行 hello update 陳述式。 

您指定當您建立您自己的伺服器和資料庫的 hello 值取代 hello 主機、 資料庫、 使用者和密碼參數。

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

        // check that hello driver is installed
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
            
            // set up hello connection properties
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

## <a name="delete-data"></a>刪除資料
使用 hello 下列程式碼與 tooremove 資料**刪除**SQL 陳述式。 hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html)方法是使用的 tooconnect tooMySQL。  hello 方法[prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html)和 executeUpdate() 都使用的 tooprepare 執行 hello update 陳述式。 

您指定當您建立您自己的伺服器和資料庫的 hello 值取代 hello 主機、 資料庫、 使用者和密碼參數。

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
        
        // check that hello driver is installed
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
            
            // set up hello connection properties
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
            throw new SQLException("Failed toocreate connection toodatabase", e);
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

## <a name="next-steps"></a>後續步驟
> [!div class="nextstepaction"]
> [用於使用傾印和還原 MySQL 移轉您的 MySQL 資料庫 tooAzure 資料庫](concepts-migrate-dump-restore.md)
