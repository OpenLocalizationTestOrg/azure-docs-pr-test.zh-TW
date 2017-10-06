---
title: "用於從 c + + 的 MySQL 連接 tooAzure 資料庫 |Microsoft 文件"
description: "本快速入門會提供您可以使用 tooconnect 和查詢資料從 Azure 資料庫的 MySQL 的 c + + 程式碼範例。"
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
ms.openlocfilehash: d027597bf02b1eacab9b8808957399f6e54e63cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-connectorc-tooconnect-and-query-data"></a><span data-ttu-id="6c20b-103">Azure 資料庫的 MySQL： 使用連接器/c + + tooconnect 和查詢資料</span><span class="sxs-lookup"><span data-stu-id="6c20b-103">Azure Database for MySQL: Use Connector/C++ tooconnect and query data</span></span>
<span data-ttu-id="6c20b-104">本快速入門示範如何 tooconnect tooan Azure 資料庫的 MySQL 使用 c + + 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c20b-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a C++ application.</span></span> <span data-ttu-id="6c20b-105">它會顯示 toouse SQL 陳述式 tooquery，如何插入、 更新和刪除 hello 資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="6c20b-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="6c20b-106">hello 本文章中的步驟假設您已熟悉開發使用 c + +，且新 tooworking 與 MySQL 的 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6c20b-106">hello steps in this article assume that you are familiar with developing using C++, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c20b-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="6c20b-107">Prerequisites</span></span>
<span data-ttu-id="6c20b-108">本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：</span><span class="sxs-lookup"><span data-stu-id="6c20b-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="6c20b-109">使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="6c20b-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="6c20b-110">使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="6c20b-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="6c20b-111">您也需要：</span><span class="sxs-lookup"><span data-stu-id="6c20b-111">You also need to:</span></span>
- <span data-ttu-id="6c20b-112">安裝 [.NET Framework](https://www.microsoft.com/net/download)</span><span class="sxs-lookup"><span data-stu-id="6c20b-112">Install [.NET Framework](https://www.microsoft.com/net/download)</span></span>
- <span data-ttu-id="6c20b-113">安裝 [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="6c20b-113">Install [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
- <span data-ttu-id="6c20b-114">安裝 [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span><span class="sxs-lookup"><span data-stu-id="6c20b-114">Install [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span></span> 
- <span data-ttu-id="6c20b-115">安裝 [Boost](http://www.boost.org/)</span><span class="sxs-lookup"><span data-stu-id="6c20b-115">Install [Boost](http://www.boost.org/)</span></span>

## <a name="install-visual-studio-and-net"></a><span data-ttu-id="6c20b-116">安裝 Visual Studio 和 .NET</span><span class="sxs-lookup"><span data-stu-id="6c20b-116">Install Visual Studio and .NET</span></span>
<span data-ttu-id="6c20b-117">本節中的 hello 步驟假設您已經熟悉使用.NET 開發。</span><span class="sxs-lookup"><span data-stu-id="6c20b-117">hello steps in this section assume that you are familiar with developing using .NET.</span></span>

### <a name="windows"></a><span data-ttu-id="6c20b-118">**Windows**</span><span class="sxs-lookup"><span data-stu-id="6c20b-118">**Windows**</span></span>
1. <span data-ttu-id="6c20b-119">安裝 Visual Studio 2017 Community，這是功能完整且可擴充的免費 IDE，用以建立適用於 Android、iOS、Windows 以及 Web 和資料庫應用程式和雲端服務的新式應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c20b-119">Install Visual Studio 2017 Community, which is a full featured, extensible, free IDE for creating modern applications for Android, iOS, Windows, as well as web & database applications and cloud services.</span></span> <span data-ttu-id="6c20b-120">您可以安裝 hello 完整.NET Framework，或是只.NET Core。</span><span class="sxs-lookup"><span data-stu-id="6c20b-120">You can install either hello full .NET Framework or just .NET Core.</span></span> <span data-ttu-id="6c20b-121">hello hello 快速入門工作使用中的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="6c20b-121">hello code snippets in hello Quickstart work with either.</span></span> <span data-ttu-id="6c20b-122">如果您已安裝在電腦上安裝的 Visual Studio，請略過 hello 下面兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="6c20b-122">If you already have Visual Studio installed on your machine, skip hello next two steps.</span></span>
   - <span data-ttu-id="6c20b-123">下載 hello [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15)。</span><span class="sxs-lookup"><span data-stu-id="6c20b-123">Download hello [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span></span> 
   - <span data-ttu-id="6c20b-124">執行 hello 安裝程式並遵循 hello 安裝提示 toocomplete hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="6c20b-124">Run hello installer and follow hello installation prompts toocomplete hello installation.</span></span>

### <a name="configure-visual-studio"></a><span data-ttu-id="6c20b-125">**設定 Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="6c20b-125">**Configure Visual Studio**</span></span>
1. <span data-ttu-id="6c20b-126">在 Visual Studio 的專案屬性 > 組態屬性 > C/c + + > 連結器 > 一般 > 其他程式庫目錄新增 hello lib\opt 目錄 (也就是： C:\Program Files (x86) \MySQL\MySQL 連接器 c + + 1.1.9\lib\opt) 的 hello c + +連接器。</span><span class="sxs-lookup"><span data-stu-id="6c20b-126">From Visual Studio, project property > configuration properties > C/C++ > linker > general > additional library directories, add hello lib\opt directory (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) of hello c++ connector.</span></span>
2. <span data-ttu-id="6c20b-127">從 Visual Studio 的專案屬性 > 組態屬性 > C/C++ > 一般 > 其他 include 目錄</span><span class="sxs-lookup"><span data-stu-id="6c20b-127">From Visual Studio, project property > configuration properties > C/C++ > general > additional include directories</span></span>
   - <span data-ttu-id="6c20b-128">新增 c++ 連接器的 include/ 目錄 (也就是 C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span><span class="sxs-lookup"><span data-stu-id="6c20b-128">Add include/ directory of c++ connector (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span></span>
   - <span data-ttu-id="6c20b-129">新增 Boost 程式庫的根目錄 (也就是 C:\boost_1_64_0\)</span><span class="sxs-lookup"><span data-stu-id="6c20b-129">Add Boost library's root directory (i.e.: C:\boost_1_64_0\)</span></span>
3. <span data-ttu-id="6c20b-130">在 Visual Studio 的專案屬性 > 組態屬性 > C/c + + > 連結器 > 輸入 > 其他相依性，新增 mysqlcppconn.lib hello 文字欄位</span><span class="sxs-lookup"><span data-stu-id="6c20b-130">From Visual Studio, project property > configuration properties > C/C++ > linker > Input > Additional Dependencies, add mysqlcppconn.lib into hello text field</span></span>
4. <span data-ttu-id="6c20b-131">Hello c + + 連接器程式庫資料夾中步驟 3 toohello 任一複本 mysqlcppconn.dll hello 應用程式可執行檔相同的目錄或將它加入 toohello 環境變數，讓您的應用程式可以找到它。</span><span class="sxs-lookup"><span data-stu-id="6c20b-131">Either copy mysqlcppconn.dll from hello c++ connector library folder in step 3 toohello same directory as hello application executable or add it toohello environment variable so your application can find it.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="6c20b-132">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="6c20b-132">Get connection information</span></span>
<span data-ttu-id="6c20b-133">取得 MySQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6c20b-133">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="6c20b-134">您需要 hello 完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="6c20b-134">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="6c20b-135">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="6c20b-135">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6c20b-136">在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，並搜尋您已經建立，例如 hello 伺服器**myserver4demo**。</span><span class="sxs-lookup"><span data-stu-id="6c20b-136">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="6c20b-137">按一下 hello 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="6c20b-137">Click hello server name.</span></span>
4. <span data-ttu-id="6c20b-138">選取 hello 伺服器**屬性**頁面。</span><span class="sxs-lookup"><span data-stu-id="6c20b-138">Select hello server's **Properties** page.</span></span> <span data-ttu-id="6c20b-139">請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。</span><span class="sxs-lookup"><span data-stu-id="6c20b-139">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="6c20b-140">![Azure Database for MySQL 伺服器名稱](./media/connect-cpp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="6c20b-140">![Azure Database for MySQL server name](./media/connect-cpp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="6c20b-141">如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="6c20b-141">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="6c20b-142">連線、建立資料表及插入資料</span><span class="sxs-lookup"><span data-stu-id="6c20b-142">Connect, create table, and insert data</span></span>
<span data-ttu-id="6c20b-143">使用 hello 下列程式碼 tooconnect 並載入 hello 資料使用**CREATE TABLE**和**INSERT INTO** SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="6c20b-143">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="6c20b-144">hello 程式碼會使用與 hello connect （) 方法 tooestablish 連接 tooMySQL sql::Driver 類別。</span><span class="sxs-lookup"><span data-stu-id="6c20b-144">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="6c20b-145">然後 hello 程式碼會使用方法 createStatement() 和 execute （） toorun hello 資料庫的命令。</span><span class="sxs-lookup"><span data-stu-id="6c20b-145">Then hello code uses method createStatement() and execute() toorun hello database commands.</span></span> 

<span data-ttu-id="6c20b-146">取代 hello 值，指定當您建立 hello 伺服器和資料庫中的 hello 主機、 DBName、 使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="6c20b-146">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
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

## <a name="read-data"></a><span data-ttu-id="6c20b-147">讀取資料</span><span class="sxs-lookup"><span data-stu-id="6c20b-147">Read data</span></span>

<span data-ttu-id="6c20b-148">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**選取**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="6c20b-148">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="6c20b-149">hello 程式碼會使用與 hello connect （) 方法 tooestablish 連接 tooMySQL sql::Driver 類別。</span><span class="sxs-lookup"><span data-stu-id="6c20b-149">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="6c20b-150">然後 hello 程式碼會使用方法 prepareStatement() 和 executeQuery() toorun hello 選取命令。</span><span class="sxs-lookup"><span data-stu-id="6c20b-150">Then hello code uses method prepareStatement() and executeQuery() toorun hello select commands.</span></span> <span data-ttu-id="6c20b-151">最後 hello 程式碼會使用 next （） tooadvance toohello 記錄 hello 結果中。</span><span class="sxs-lookup"><span data-stu-id="6c20b-151">Finally hello code uses next() tooadvance toohello records in hello results.</span></span> <span data-ttu-id="6c20b-152">然後 hello 程式碼會使用 getInt() 和 Sr tooparse hello 值 hello 記錄中。</span><span class="sxs-lookup"><span data-stu-id="6c20b-152">Then hello code uses getInt() and getString() tooparse hello values in hello record.</span></span>

<span data-ttu-id="6c20b-153">取代 hello 值，指定當您建立 hello 伺服器和資料庫中的 hello 主機、 DBName、 使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="6c20b-153">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
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

## <a name="update-data"></a><span data-ttu-id="6c20b-154">更新資料</span><span class="sxs-lookup"><span data-stu-id="6c20b-154">Update data</span></span>
<span data-ttu-id="6c20b-155">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**更新**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="6c20b-155">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="6c20b-156">hello 程式碼會使用與 hello connect （) 方法 tooestablish 連接 tooMySQL sql::Driver 類別。</span><span class="sxs-lookup"><span data-stu-id="6c20b-156">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="6c20b-157">然後 hello 程式碼會使用方法 prepareStatement() 和 executeQuery() toorun hello 更新命令。</span><span class="sxs-lookup"><span data-stu-id="6c20b-157">Then hello code uses method prepareStatement() and executeQuery() toorun hello update commands.</span></span> 

<span data-ttu-id="6c20b-158">取代 hello 值，指定當您建立 hello 伺服器和資料庫中的 hello 主機、 DBName、 使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="6c20b-158">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
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


## <a name="delete-data"></a><span data-ttu-id="6c20b-159">刪除資料</span><span class="sxs-lookup"><span data-stu-id="6c20b-159">Delete data</span></span>
<span data-ttu-id="6c20b-160">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**刪除**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="6c20b-160">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="6c20b-161">hello 程式碼會使用與 hello connect （) 方法 tooestablish 連接 tooMySQL sql::Driver 類別。</span><span class="sxs-lookup"><span data-stu-id="6c20b-161">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="6c20b-162">然後 hello 程式碼會使用方法 prepareStatement() 且 executeQuery() toorun hello 刪除命令。</span><span class="sxs-lookup"><span data-stu-id="6c20b-162">Then hello code uses method prepareStatement() and executeQuery() toorun hello delete commands.</span></span>

<span data-ttu-id="6c20b-163">取代 hello 值，指定當您建立 hello 伺服器和資料庫中的 hello 主機、 DBName、 使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="6c20b-163">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
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

## <a name="next-steps"></a><span data-ttu-id="6c20b-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c20b-164">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="6c20b-165">用於使用傾印和還原 MySQL 移轉您的 MySQL 資料庫 tooAzure 資料庫</span><span class="sxs-lookup"><span data-stu-id="6c20b-165">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
