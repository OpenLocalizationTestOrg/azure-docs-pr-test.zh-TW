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
# <a name="azure-database-for-mysql-use-connectorc-tooconnect-and-query-data"></a>Azure 資料庫的 MySQL： 使用連接器/c + + tooconnect 和查詢資料
本快速入門示範如何 tooconnect tooan Azure 資料庫的 MySQL 使用 c + + 應用程式。 它會顯示 toouse SQL 陳述式 tooquery，如何插入、 更新和刪除 hello 資料庫中的資料。 hello 本文章中的步驟假設您已熟悉開發使用 c + +，且新 tooworking 與 MySQL 的 Azure 資料庫。

## <a name="prerequisites"></a>必要條件
本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：
- [使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器](./quickstart-create-mysql-server-database-using-azure-cli.md)

您也需要：
- 安裝 [.NET Framework](https://www.microsoft.com/net/download)
- 安裝 [Visual Studio](https://www.visualstudio.com/downloads/)
- 安裝 [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/) 
- 安裝 [Boost](http://www.boost.org/)

## <a name="install-visual-studio-and-net"></a>安裝 Visual Studio 和 .NET
本節中的 hello 步驟假設您已經熟悉使用.NET 開發。

### <a name="windows"></a>**Windows**
1. 安裝 Visual Studio 2017 Community，這是功能完整且可擴充的免費 IDE，用以建立適用於 Android、iOS、Windows 以及 Web 和資料庫應用程式和雲端服務的新式應用程式。 您可以安裝 hello 完整.NET Framework，或是只.NET Core。 hello hello 快速入門工作使用中的程式碼片段。 如果您已安裝在電腦上安裝的 Visual Studio，請略過 hello 下面兩個步驟。
   - 下載 hello [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15)。 
   - 執行 hello 安裝程式並遵循 hello 安裝提示 toocomplete hello 安裝。

### <a name="configure-visual-studio"></a>**設定 Visual Studio**
1. 在 Visual Studio 的專案屬性 > 組態屬性 > C/c + + > 連結器 > 一般 > 其他程式庫目錄新增 hello lib\opt 目錄 (也就是： C:\Program Files (x86) \MySQL\MySQL 連接器 c + + 1.1.9\lib\opt) 的 hello c + +連接器。
2. 從 Visual Studio 的專案屬性 > 組態屬性 > C/C++ > 一般 > 其他 include 目錄
   - 新增 c++ 連接器的 include/ 目錄 (也就是 C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)
   - 新增 Boost 程式庫的根目錄 (也就是 C:\boost_1_64_0\)
3. 在 Visual Studio 的專案屬性 > 組態屬性 > C/c + + > 連結器 > 輸入 > 其他相依性，新增 mysqlcppconn.lib hello 文字欄位
4. Hello c + + 連接器程式庫資料夾中步驟 3 toohello 任一複本 mysqlcppconn.dll hello 應用程式可執行檔相同的目錄或將它加入 toohello 環境變數，讓您的應用程式可以找到它。

## <a name="get-connection-information"></a>取得連線資訊
取得 MySQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。 您需要 hello 完整的伺服器名稱和登入認證。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，並搜尋您已經建立，例如 hello 伺服器**myserver4demo**。
3. 按一下 hello 伺服器名稱。
4. 選取 hello 伺服器**屬性**頁面。 請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。
 ![Azure Database for MySQL 伺服器名稱](./media/connect-cpp/1_server-properties-name-login.png)
5. 如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。

## <a name="connect-create-table-and-insert-data"></a>連線、建立資料表及插入資料
使用 hello 下列程式碼 tooconnect 並載入 hello 資料使用**CREATE TABLE**和**INSERT INTO** SQL 陳述式。 hello 程式碼會使用與 hello connect （) 方法 tooestablish 連接 tooMySQL sql::Driver 類別。 然後 hello 程式碼會使用方法 createStatement() 和 execute （） toorun hello 資料庫的命令。 

取代 hello 值，指定當您建立 hello 伺服器和資料庫中的 hello 主機、 DBName、 使用者和密碼參數。 

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

## <a name="read-data"></a>讀取資料

使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**選取**SQL 陳述式。 hello 程式碼會使用與 hello connect （) 方法 tooestablish 連接 tooMySQL sql::Driver 類別。 然後 hello 程式碼會使用方法 prepareStatement() 和 executeQuery() toorun hello 選取命令。 最後 hello 程式碼會使用 next （） tooadvance toohello 記錄 hello 結果中。 然後 hello 程式碼會使用 getInt() 和 Sr tooparse hello 值 hello 記錄中。

取代 hello 值，指定當您建立 hello 伺服器和資料庫中的 hello 主機、 DBName、 使用者和密碼參數。 

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

## <a name="update-data"></a>更新資料
使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**更新**SQL 陳述式。 hello 程式碼會使用與 hello connect （) 方法 tooestablish 連接 tooMySQL sql::Driver 類別。 然後 hello 程式碼會使用方法 prepareStatement() 和 executeQuery() toorun hello 更新命令。 

取代 hello 值，指定當您建立 hello 伺服器和資料庫中的 hello 主機、 DBName、 使用者和密碼參數。 

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


## <a name="delete-data"></a>刪除資料
使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**刪除**SQL 陳述式。 hello 程式碼會使用與 hello connect （) 方法 tooestablish 連接 tooMySQL sql::Driver 類別。 然後 hello 程式碼會使用方法 prepareStatement() 且 executeQuery() toorun hello 刪除命令。

取代 hello 值，指定當您建立 hello 伺服器和資料庫中的 hello 主機、 DBName、 使用者和密碼參數。 

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

## <a name="next-steps"></a>後續步驟
> [!div class="nextstepaction"]
> [用於使用傾印和還原 MySQL 移轉您的 MySQL 資料庫 tooAzure 資料庫](concepts-migrate-dump-restore.md)
