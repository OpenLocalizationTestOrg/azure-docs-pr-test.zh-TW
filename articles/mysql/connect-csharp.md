---
title: "用於從 C# 的 MySQL 連接 tooAzure 資料庫 |Microsoft 文件"
description: "本快速入門提供的 C# (.NET) 的程式碼範例可以使用 tooconnect 並查詢資料從 Azure 資料庫的 MySQL。"
services: MySQL
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: MySQL-database
ms.custom: mvc
ms.devlang: csharp
ms.topic: hero-article
ms.date: 07/10/2017
ms.openlocfilehash: 0dca98186199a40ef9cc592b93c3b2e815260273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-net-c-tooconnect-and-query-data"></a><span data-ttu-id="fc1e7-103">Azure 資料庫的 MySQL： 使用.NET (C#) tooconnect 和查詢資料</span><span class="sxs-lookup"><span data-stu-id="fc1e7-103">Azure Database for MySQL: Use .NET (C#) tooconnect and query data</span></span>
<span data-ttu-id="fc1e7-104">本快速入門示範如何 tooconnect tooan Azure 資料庫的 MySQL 使用 C# 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a C# application.</span></span> <span data-ttu-id="fc1e7-105">它會顯示 toouse SQL 陳述式 tooquery，如何插入、 更新和刪除 hello 資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="fc1e7-106">hello 本文章中的步驟假設您已熟悉開發使用 C# 中，且新 tooworking 與 MySQL 的 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-106">hello steps in this article assume that you are familiar with developing using C#, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc1e7-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="fc1e7-107">Prerequisites</span></span>
<span data-ttu-id="fc1e7-108">本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：</span><span class="sxs-lookup"><span data-stu-id="fc1e7-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="fc1e7-109">使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="fc1e7-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="fc1e7-110">使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="fc1e7-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="fc1e7-111">您也需要：</span><span class="sxs-lookup"><span data-stu-id="fc1e7-111">You also need to:</span></span>
- <span data-ttu-id="fc1e7-112">安裝 [.NET](https://www.microsoft.com/net/download)。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-112">Install [.NET](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="fc1e7-113">請遵循 hello hello 連結文章 tooinstall.NET 特別為您的平台 （Windows、 Ubuntu Linux 或 macOS） 中的步驟。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-113">Follow hello steps in hello linked article tooinstall .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="fc1e7-114">安裝 [Visual Studio](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-114">Install [Visual Studio](https://www.visualstudio.com/downloads/).</span></span>
- <span data-ttu-id="fc1e7-115">安裝 [ODBC Driver for MySQL](https://dev.mysql.com/downloads/connector/odbc/)。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-115">Install [ODBC Driver for MySQL](https://dev.mysql.com/downloads/connector/odbc/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="fc1e7-116">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="fc1e7-116">Get connection information</span></span>
<span data-ttu-id="fc1e7-117">取得 MySQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-117">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="fc1e7-118">您需要 hello 完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-118">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="fc1e7-119">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-119">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fc1e7-120">在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，並搜尋您已經建立，例如 hello 伺服器**myserver4demo**。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-120">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="fc1e7-121">按一下 hello 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-121">Click hello server name.</span></span>
4. <span data-ttu-id="fc1e7-122">選取 hello 伺服器**屬性**頁面。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-122">Select hello server's **Properties** page.</span></span> <span data-ttu-id="fc1e7-123">請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-123">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="fc1e7-124">![Azure Database for MySQL 伺服器名稱](./media/connect-csharp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="fc1e7-124">![Azure Database for MySQL server name](./media/connect-csharp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="fc1e7-125">如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-125">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="fc1e7-126">連線、建立資料表及插入資料</span><span class="sxs-lookup"><span data-stu-id="fc1e7-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="fc1e7-127">使用 hello 下列程式碼 tooconnect 並載入 hello 資料使用**CREATE TABLE**和**INSERT INTO** SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-127">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="fc1e7-128">hello 程式碼會使用 ODBC 類別具有方法[open （)](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish 連接 tooMySQL。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-128">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="fc1e7-129">然後，hello 程式碼會使用方法[CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx)管理員、 設定 hello CommandText 屬性，並呼叫方法[executenonquery （)](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello 資料庫命令。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-129">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets hello CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello database commands.</span></span> 

<span data-ttu-id="fc1e7-130">取代 hello 值，指定當您建立 hello 伺服器和資料庫中的 hello 主機、 DBName、 使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-130">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MySql.Data;
using System.Data.Odbc;

namespace driver
{
    class MySQLCreate
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "DROP TABLE IF EXISTS inventory;";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished dropping table (if existed)");

            command.CommandText = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished creating table");

            command.CommandText =
                String.Format(
                    @"INSERT INTO inventory (name, quantity) VALUES ({0}, {1});
                    INSERT INTO inventory (name, quantity) VALUES ({2}, {3});
                    INSERT INTO inventory (name, quantity) VALUES ({4}, {5});",
                    "\'banana\'", 150,
                    "\'orange\'", 154,
                    "\'apple\'", 100
                    );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows inserted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }

    }
}

```

## <a name="read-data"></a><span data-ttu-id="fc1e7-131">讀取資料</span><span class="sxs-lookup"><span data-stu-id="fc1e7-131">Read data</span></span>

<span data-ttu-id="fc1e7-132">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**選取**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-132">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="fc1e7-133">hello 程式碼會使用 ODBC 類別具有方法[open （)](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish 連接 tooMySQL。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-133">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="fc1e7-134">然後，hello 程式碼會使用方法[CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx)和方法[executereader （)](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) toorun hello 資料庫命令。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-134">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) and method [ExecuteReader()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) toorun hello database commands.</span></span> <span data-ttu-id="fc1e7-135">接下來 hello 程式碼使用[read](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) tooadvance toohello hello 結果記錄。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-135">Next hello code uses [Read()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) tooadvance toohello records in hello results.</span></span> <span data-ttu-id="fc1e7-136">然後 hello 程式碼會使用 GetInt32 和 GetString tooparse hello 值 hello 記錄中。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-136">Then hello code uses GetInt32 and GetString tooparse hello values in hello record.</span></span>

<span data-ttu-id="fc1e7-137">取代 hello 值，指定當您建立 hello 伺服器和資料庫中的 hello 主機、 DBName、 使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-137">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MySql.Data;
using System.Data.Odbc;


namespace driver
{
    class MySQLRead
    {

        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "SELECT * FROM inventory;";

            var reader = command.ExecuteReader();
            while (reader.Read())
            {
                Console.WriteLine(
                    string.Format(
                        "Reading from table=({0}, {1}, {2})",
                        reader.GetInt32(0).ToString(),
                        reader.GetString(1),
                        reader.GetInt32(2).ToString()
                        )
                    );
            }

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}


```

## <a name="update-data"></a><span data-ttu-id="fc1e7-138">更新資料</span><span class="sxs-lookup"><span data-stu-id="fc1e7-138">Update data</span></span>
<span data-ttu-id="fc1e7-139">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**更新**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-139">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="fc1e7-140">hello 程式碼會使用 ODBC 類別具有方法[open （)](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish 連接 tooMySQL。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-140">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="fc1e7-141">然後，hello 程式碼會使用方法[CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx)管理員、 設定 hello CommandText 屬性，並呼叫方法[executenonquery （)](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello 資料庫命令。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-141">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets hello CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello database commands.</span></span>

<span data-ttu-id="fc1e7-142">取代 hello 值，指定當您建立 hello 伺服器和資料庫中的 hello 主機、 DBName、 使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-142">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.Odbc;

namespace driver
{
    class MySQLUpdate
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
            String.Format("UPDATE inventory SET quantity = {0} WHERE name = {1};",
                200,
                "\'banana\'"
                );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows updated={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}



```


## <a name="delete-data"></a><span data-ttu-id="fc1e7-143">刪除資料</span><span class="sxs-lookup"><span data-stu-id="fc1e7-143">Delete data</span></span>
<span data-ttu-id="fc1e7-144">使用 hello 下列程式碼 tooconnect 並刪除 hello 資料使用**刪除**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-144">Use hello following code tooconnect and delete hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="fc1e7-145">hello 程式碼會使用 ODBC 類別具有方法[open （)](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish 連接 tooMySQL。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-145">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="fc1e7-146">然後，hello 程式碼會使用方法[CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx)管理員、 設定 hello CommandText 屬性，並呼叫方法[executenonquery （)](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello 資料庫命令。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-146">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets hello CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello database commands.</span></span>

<span data-ttu-id="fc1e7-147">取代 hello 值，指定當您建立 hello 伺服器和資料庫中的 hello 主機、 DBName、 使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="fc1e7-147">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.Odbc;

namespace driver
{
    class MySQLDelete
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
                String.Format("DELETE FROM inventory WHERE name = {0};",
                    "\'orange\'");
            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows deleted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}

```

## <a name="next-steps"></a><span data-ttu-id="fc1e7-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc1e7-148">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="fc1e7-149">用於使用傾印和還原 MySQL 移轉您的 MySQL 資料庫 tooAzure 資料庫</span><span class="sxs-lookup"><span data-stu-id="fc1e7-149">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
