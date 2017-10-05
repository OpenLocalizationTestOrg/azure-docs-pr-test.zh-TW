---
title: "從 C++ 連線到 Azure Database for MySQL | Microsoft Docs"
description: "本快速入門提供 C++ 程式碼範例，您可用於從 Azure Database for MySQL 連線及查詢資料。"
services: mysql
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: C++
ms.topic: hero-article
ms.date: 08/03/2017
ms.openlocfilehash: 63388b83b913d95136140fa4c56af0dbebbdad81
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-database-for-mysql-use-connectorc-to-connect-and-query-data"></a><span data-ttu-id="d779c-103">Azure Database for MySQL︰使用 Connector/C++ 來連線及查詢資料</span><span class="sxs-lookup"><span data-stu-id="d779c-103">Azure Database for MySQL: Use Connector/C++ to connect and query data</span></span>
<span data-ttu-id="d779c-104">本快速入門示範如何使用 C++ 應用程式來連線到 Azure Database for MySQL。</span><span class="sxs-lookup"><span data-stu-id="d779c-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a C++ application.</span></span> <span data-ttu-id="d779c-105">它會顯示如何使用 SQL 陳述式來查詢、插入、更新和刪除資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="d779c-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="d779c-106">本文中的步驟假設您已熟悉使用 C++ 進行開發，但不熟悉 Azure Database for MySQL。</span><span class="sxs-lookup"><span data-stu-id="d779c-106">The steps in this article assume that you are familiar with developing using C++, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d779c-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="d779c-107">Prerequisites</span></span>
<span data-ttu-id="d779c-108">本快速入門使用在以下任一指南中建立的資源作為起點︰</span><span class="sxs-lookup"><span data-stu-id="d779c-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="d779c-109">使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="d779c-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="d779c-110">使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="d779c-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="d779c-111">您也需要：</span><span class="sxs-lookup"><span data-stu-id="d779c-111">You also need to:</span></span>
- <span data-ttu-id="d779c-112">安裝 [.NET Framework](https://www.microsoft.com/net/download)</span><span class="sxs-lookup"><span data-stu-id="d779c-112">Install [.NET Framework](https://www.microsoft.com/net/download)</span></span>
- <span data-ttu-id="d779c-113">安裝 [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="d779c-113">Install [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
- <span data-ttu-id="d779c-114">安裝 [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span><span class="sxs-lookup"><span data-stu-id="d779c-114">Install [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span></span> 
- <span data-ttu-id="d779c-115">安裝 [Boost](http://www.boost.org/)</span><span class="sxs-lookup"><span data-stu-id="d779c-115">Install [Boost](http://www.boost.org/)</span></span>

## <a name="install-visual-studio-and-net"></a><span data-ttu-id="d779c-116">安裝 Visual Studio 和 .NET</span><span class="sxs-lookup"><span data-stu-id="d779c-116">Install Visual Studio and .NET</span></span>
<span data-ttu-id="d779c-117">本節中的步驟假設您已熟悉使用 .NET 進行開發。</span><span class="sxs-lookup"><span data-stu-id="d779c-117">The steps in this section assume that you are familiar with developing using .NET.</span></span>

### <a name="windows"></a><span data-ttu-id="d779c-118">**Windows**</span><span class="sxs-lookup"><span data-stu-id="d779c-118">**Windows**</span></span>
1. <span data-ttu-id="d779c-119">安裝 Visual Studio 2017 Community，這是功能完整且可擴充的免費 IDE，用以建立適用於 Android、iOS、Windows 以及 Web 和資料庫應用程式和雲端服務的新式應用程式。</span><span class="sxs-lookup"><span data-stu-id="d779c-119">Install Visual Studio 2017 Community, which is a full featured, extensible, free IDE for creating modern applications for Android, iOS, Windows, as well as web & database applications and cloud services.</span></span> <span data-ttu-id="d779c-120">您可以安裝完整的 .NET Framework 或只安裝 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="d779c-120">You can install either the full .NET Framework or just .NET Core.</span></span> <span data-ttu-id="d779c-121">快速入門中的程式碼片段均可搭配使用。</span><span class="sxs-lookup"><span data-stu-id="d779c-121">The code snippets in the Quickstart work with either.</span></span> <span data-ttu-id="d779c-122">如果您已在電腦上安裝 Visual Studio，請略過後續兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="d779c-122">If you already have Visual Studio installed on your machine, skip the next two steps.</span></span>
   - <span data-ttu-id="d779c-123">下載 [Visual Studio 2017 安裝程式](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15)。</span><span class="sxs-lookup"><span data-stu-id="d779c-123">Download the [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span></span> 
   - <span data-ttu-id="d779c-124">執行安裝程式並依照安裝提示來完成安裝。</span><span class="sxs-lookup"><span data-stu-id="d779c-124">Run the installer and follow the installation prompts to complete the installation.</span></span>

### <a name="configure-visual-studio"></a><span data-ttu-id="d779c-125">**設定 Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="d779c-125">**Configure Visual Studio**</span></span>
1. <span data-ttu-id="d779c-126">從 Visual Studio 的專案屬性 > 組態屬性 > C/C++ > 連結器 > 一般 > 其他 library 目錄，新增 c++ 連接器的 lib\opt 目錄 (也就是 C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt)。</span><span class="sxs-lookup"><span data-stu-id="d779c-126">From Visual Studio, project property > configuration properties > C/C++ > linker > general > additional library directories, add the lib\opt directory (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) of the c++ connector.</span></span>
2. <span data-ttu-id="d779c-127">從 Visual Studio 的專案屬性 > 組態屬性 > C/C++ > 一般 > 其他 include 目錄</span><span class="sxs-lookup"><span data-stu-id="d779c-127">From Visual Studio, project property > configuration properties > C/C++ > general > additional include directories</span></span>
   - <span data-ttu-id="d779c-128">新增 c++ 連接器的 include/ 目錄 (也就是 C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span><span class="sxs-lookup"><span data-stu-id="d779c-128">Add include/ directory of c++ connector (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span></span>
   - <span data-ttu-id="d779c-129">新增 Boost 程式庫的根目錄 (也就是 C:\boost_1_64_0\)</span><span class="sxs-lookup"><span data-stu-id="d779c-129">Add Boost library's root directory (i.e.: C:\boost_1_64_0\)</span></span>
3. <span data-ttu-id="d779c-130">從 Visual Studio 的專案屬性 > 組態屬性 > C/C++ > 連結器 > 輸入 > 其他相依性，將 mysqlcppconn.lib 新增到文字欄位中</span><span class="sxs-lookup"><span data-stu-id="d779c-130">From Visual Studio, project property > configuration properties > C/C++ > linker > Input > Additional Dependencies, add mysqlcppconn.lib into the text field</span></span>
4. <span data-ttu-id="d779c-131">從步驟 3 的 c++ 連接器程式庫資料夾將 mysqlcppconn.dll 複製到與應用程式可執行檔相同的目錄，或將它新增至環境變數，您的應用程式便可找到它。</span><span class="sxs-lookup"><span data-stu-id="d779c-131">Either copy mysqlcppconn.dll from the c++ connector library folder in step 3 to the same directory as the application executable or add it to the environment variable so your application can find it.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="d779c-132">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="d779c-132">Get connection information</span></span>
<span data-ttu-id="d779c-133">取得連線到 Azure Database for MySQL 所需的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="d779c-133">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="d779c-134">您需要完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="d779c-134">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="d779c-135">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="d779c-135">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d779c-136">從 Azure 入口網站的左側功能表中，按一下 [所有資源]，然後搜尋您所建立的伺服器，例如 **myserver4demo**。</span><span class="sxs-lookup"><span data-stu-id="d779c-136">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="d779c-137">按一下伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="d779c-137">Click the server name.</span></span>
4. <span data-ttu-id="d779c-138">選取伺服器的 [屬性] 頁面。</span><span class="sxs-lookup"><span data-stu-id="d779c-138">Select the server's **Properties** page.</span></span> <span data-ttu-id="d779c-139">記下 [伺服器名稱] 和 [伺服器管理員登入名稱]。</span><span class="sxs-lookup"><span data-stu-id="d779c-139">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="d779c-140">![Azure Database for MySQL 伺服器名稱](./media/connect-cpp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="d779c-140">![Azure Database for MySQL server name](./media/connect-cpp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="d779c-141">如果您忘記伺服器登入資訊，請瀏覽至 [概觀] 頁面來檢視伺服器管理員登入名稱，並視需要重設密碼。</span><span class="sxs-lookup"><span data-stu-id="d779c-141">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="d779c-142">連線、建立資料表及插入資料</span><span class="sxs-lookup"><span data-stu-id="d779c-142">Connect, create table, and insert data</span></span>
<span data-ttu-id="d779c-143">使用下列程式碼搭配 **CREATE TABLE** 和 **INSERT INTO** SQL 陳述式來連線和載入資料。</span><span class="sxs-lookup"><span data-stu-id="d779c-143">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="d779c-144">此程式碼使用 sql::Driver 類別搭配 connect() 方法來建立 MySQL 連線。</span><span class="sxs-lookup"><span data-stu-id="d779c-144">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="d779c-145">然後，程式碼會使用 createStatement() 和 execute() 方法來執行資料庫命令。</span><span class="sxs-lookup"><span data-stu-id="d779c-145">Then the code uses method createStatement() and execute() to run the database commands.</span></span> 

<span data-ttu-id="d779c-146">以建立伺服器和資料庫時所指定的值，取代主機、資料庫名稱、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="d779c-146">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```c++
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::Statement *stmt;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }

    stmt = con>createStatement();
    stmt>execute("DROP TABLE IF EXISTS inventory");
    cout << "Finished dropping table (if existed)" << endl;
    stmt>execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
    cout << "Finished creating table" << endl;
    delete stmt;

    pstmt = con>prepareStatement("INSERT INTO inventory(name, quantity) VALUES(?,?)");
    pstmt>setString(1, "banana");
    pstmt>setInt(2, 150);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "orange");
    pstmt>setInt(2, 154);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "apple");
    pstmt>setInt(2, 100);
    pstmt>execute();
    cout << "One row inserted." << endl;
    
    delete pstmt;   
    delete con;
    system("pause");
    return 0;

```

## <a name="read-data"></a><span data-ttu-id="d779c-147">讀取資料</span><span class="sxs-lookup"><span data-stu-id="d779c-147">Read data</span></span>

<span data-ttu-id="d779c-148">使用下列程式碼搭配 **SELECT** SQL 陳述式來連線和讀取資料。</span><span class="sxs-lookup"><span data-stu-id="d779c-148">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="d779c-149">此程式碼使用 sql::Driver 類別搭配 connect() 方法來建立 MySQL 連線。</span><span class="sxs-lookup"><span data-stu-id="d779c-149">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="d779c-150">然後，程式碼會使用 prepareStatement() 和 executeQuery() 方法來執行 select 命令。</span><span class="sxs-lookup"><span data-stu-id="d779c-150">Then the code uses method prepareStatement() and executeQuery() to run the select commands.</span></span> <span data-ttu-id="d779c-151">程式碼最後會使用 next() 前往結果中的記錄。</span><span class="sxs-lookup"><span data-stu-id="d779c-151">Finally the code uses next() to advance to the records in the results.</span></span> <span data-ttu-id="d779c-152">接下來程式碼會使用 getInt() 和 getString() 來剖析記錄中的值。</span><span class="sxs-lookup"><span data-stu-id="d779c-152">Then the code uses getInt() and getString() to parse the values in the record.</span></span>

<span data-ttu-id="d779c-153">以建立伺服器和資料庫時所指定的值，取代主機、資料庫名稱、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="d779c-153">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

//  select  
    pstmt = con>prepareStatement("SELECT * FROM inventory;");
    result = pstmt>executeQuery();  
    
    while (result>next())
        printf("Reading from table=(%d, %s, %d)\n", result>getInt(1), result>getString(2).c_str(), result>getInt(3));   
    
    delete result;
    delete pstmt;   
    delete con;
    system("pause");
    return 0;
}
```

## <a name="update-data"></a><span data-ttu-id="d779c-154">更新資料</span><span class="sxs-lookup"><span data-stu-id="d779c-154">Update data</span></span>
<span data-ttu-id="d779c-155">使用下列程式碼搭配 **UPDATE** SQL 陳述式來連線和讀取資料。</span><span class="sxs-lookup"><span data-stu-id="d779c-155">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="d779c-156">此程式碼使用 sql::Driver 類別搭配 connect() 方法來建立 MySQL 連線。</span><span class="sxs-lookup"><span data-stu-id="d779c-156">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="d779c-157">然後，程式碼會使用 prepareStatement() 和 executeQuery() 方法來執行 update 命令。</span><span class="sxs-lookup"><span data-stu-id="d779c-157">Then the code uses method prepareStatement() and executeQuery() to run the update commands.</span></span> 

<span data-ttu-id="d779c-158">以建立伺服器和資料庫時所指定的值，取代主機、資料庫名稱、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="d779c-158">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

    //update
    pstmt = con>prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?");
    pstmt>setInt(1, 200);
    pstmt>setString(2, "banana");
    pstmt>executeQuery();
    printf("Row updated\n");
    
    delete con;
    delete pstmt;
    system("pause");
    return 0;
}
```


## <a name="delete-data"></a><span data-ttu-id="d779c-159">刪除資料</span><span class="sxs-lookup"><span data-stu-id="d779c-159">Delete data</span></span>
<span data-ttu-id="d779c-160">使用下列程式碼搭配 **DELETE** SQL 陳述式來連線和讀取資料。</span><span class="sxs-lookup"><span data-stu-id="d779c-160">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="d779c-161">此程式碼使用 sql::Driver 類別搭配 connect() 方法來建立 MySQL 連線。</span><span class="sxs-lookup"><span data-stu-id="d779c-161">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="d779c-162">然後，程式碼會使用 prepareStatement() 和 executeQuery() 方法來執行 update 命令。</span><span class="sxs-lookup"><span data-stu-id="d779c-162">Then the code uses method prepareStatement() and executeQuery() to run the delete commands.</span></span>

<span data-ttu-id="d779c-163">以建立伺服器和資料庫時所指定的值，取代主機、資料庫名稱、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="d779c-163">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }
        
    //delete
    pstmt = con>prepareStatement("DELETE FROM inventory WHERE name = ?");
    pstmt>setString(1, "orange");
    result = pstmt>executeQuery();
    printf("Row deleted\n");    
    
    delete pstmt;
    delete con;
    delete result;
    system("pause");
    return 0;
}
```

## <a name="next-steps"></a><span data-ttu-id="d779c-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d779c-164">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d779c-165">使用傾印和還原來將 MySQL 資料庫移轉至適用於 MySQL 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="d779c-165">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
