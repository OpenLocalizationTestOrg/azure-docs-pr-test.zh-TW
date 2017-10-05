---
title: "從 C# 連線到 Azure Database for MySQL | Microsoft Docs"
description: "本快速入門提供 C# (.NET) 程式碼範例，您可用於從 Azure Database for MySQL 連線及查詢資料。"
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
ms.openlocfilehash: f1488f6b4a240165c71c95f759af73d6b9fd7bfe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-database-for-mysql-use-net-c-to-connect-and-query-data"></a><span data-ttu-id="c8815-103">Azure Database for MySQL︰使用 .NET (C#) 來連線及查詢資料</span><span class="sxs-lookup"><span data-stu-id="c8815-103">Azure Database for MySQL: Use .NET (C#) to connect and query data</span></span>
<span data-ttu-id="c8815-104">本快速入門示範如何使用 C# 應用程式來連線到 Azure Database for MySQL。</span><span class="sxs-lookup"><span data-stu-id="c8815-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a C# application.</span></span> <span data-ttu-id="c8815-105">它會顯示如何使用 SQL 陳述式來查詢、插入、更新和刪除資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="c8815-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="c8815-106">本文中的步驟假設您已熟悉使用 C# 進行開發，但不熟悉 Azure Database for MySQL。</span><span class="sxs-lookup"><span data-stu-id="c8815-106">The steps in this article assume that you are familiar with developing using C#, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8815-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="c8815-107">Prerequisites</span></span>
<span data-ttu-id="c8815-108">本快速入門使用在以下任一指南中建立的資源作為起點︰</span><span class="sxs-lookup"><span data-stu-id="c8815-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="c8815-109">使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="c8815-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="c8815-110">使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="c8815-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="c8815-111">您也需要：</span><span class="sxs-lookup"><span data-stu-id="c8815-111">You also need to:</span></span>
- <span data-ttu-id="c8815-112">安裝 [.NET](https://www.microsoft.com/net/download)。</span><span class="sxs-lookup"><span data-stu-id="c8815-112">Install [.NET](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="c8815-113">請依照連結文章中的步驟，特別為您的平台 (Windows、Ubuntu Linux 或 macOS) 安裝 .NET。</span><span class="sxs-lookup"><span data-stu-id="c8815-113">Follow the steps in the linked article to install .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="c8815-114">安裝 [Visual Studio](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="c8815-114">Install [Visual Studio](https://www.visualstudio.com/downloads/).</span></span>
- <span data-ttu-id="c8815-115">安裝 [ODBC Driver for MySQL](https://dev.mysql.com/downloads/connector/odbc/)。</span><span class="sxs-lookup"><span data-stu-id="c8815-115">Install [ODBC Driver for MySQL](https://dev.mysql.com/downloads/connector/odbc/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="c8815-116">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="c8815-116">Get connection information</span></span>
<span data-ttu-id="c8815-117">取得連線到 Azure Database for MySQL 所需的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="c8815-117">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="c8815-118">您需要完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="c8815-118">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="c8815-119">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="c8815-119">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c8815-120">從 Azure 入口網站的左側功能表中，按一下 [所有資源]，然後搜尋您所建立的伺服器，例如 **myserver4demo**。</span><span class="sxs-lookup"><span data-stu-id="c8815-120">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="c8815-121">按一下伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="c8815-121">Click the server name.</span></span>
4. <span data-ttu-id="c8815-122">選取伺服器的 [屬性] 頁面。</span><span class="sxs-lookup"><span data-stu-id="c8815-122">Select the server's **Properties** page.</span></span> <span data-ttu-id="c8815-123">記下 [伺服器名稱] 和 [伺服器管理員登入名稱]。</span><span class="sxs-lookup"><span data-stu-id="c8815-123">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="c8815-124">![Azure Database for MySQL 伺服器名稱](./media/connect-csharp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="c8815-124">![Azure Database for MySQL server name](./media/connect-csharp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="c8815-125">如果您忘記伺服器登入資訊，請瀏覽至 [概觀] 頁面來檢視伺服器管理員登入名稱，並視需要重設密碼。</span><span class="sxs-lookup"><span data-stu-id="c8815-125">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="c8815-126">連線、建立資料表及插入資料</span><span class="sxs-lookup"><span data-stu-id="c8815-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="c8815-127">使用下列程式碼搭配 **CREATE TABLE** 和 **INSERT INTO** SQL 陳述式來連線和載入資料。</span><span class="sxs-lookup"><span data-stu-id="c8815-127">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="c8815-128">此程式碼使用 ODBC 類別搭配 [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) 方法來建立 MySQL 連線。</span><span class="sxs-lookup"><span data-stu-id="c8815-128">The code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) to establish a connection to MySQL.</span></span> <span data-ttu-id="c8815-129">然後，程式碼會使用 [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) 方法，設定 CommandText 屬性，並呼叫 [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) 方法來執行資料庫命令。</span><span class="sxs-lookup"><span data-stu-id="c8815-129">Then the code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets the CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) to run the database commands.</span></span> 

<span data-ttu-id="c8815-130">以建立伺服器和資料庫時所指定的值，取代主機、資料庫名稱、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="c8815-130">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

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

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }

    }
}

```

## <a name="read-data"></a><span data-ttu-id="c8815-131">讀取資料</span><span class="sxs-lookup"><span data-stu-id="c8815-131">Read data</span></span>

<span data-ttu-id="c8815-132">使用下列程式碼搭配 **SELECT** SQL 陳述式來連線和讀取資料。</span><span class="sxs-lookup"><span data-stu-id="c8815-132">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="c8815-133">此程式碼使用 ODBC 類別搭配 [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) 方法來建立 MySQL 連線。</span><span class="sxs-lookup"><span data-stu-id="c8815-133">The code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) to establish a connection to MySQL.</span></span> <span data-ttu-id="c8815-134">然後，程式碼會使用 [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) 和 [ExecuteReader()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) 方法來執行資料庫命令。</span><span class="sxs-lookup"><span data-stu-id="c8815-134">Then the code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) and method [ExecuteReader()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) to run the database commands.</span></span> <span data-ttu-id="c8815-135">接下來程式碼會使用 [Read()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) 前往結果中的記錄。</span><span class="sxs-lookup"><span data-stu-id="c8815-135">Next the code uses [Read()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) to advance to the records in the results.</span></span> <span data-ttu-id="c8815-136">接下來程式碼會使用 GetInt32 和 GetString 來剖析記錄中的值。</span><span class="sxs-lookup"><span data-stu-id="c8815-136">Then the code uses GetInt32 and GetString to parse the values in the record.</span></span>

<span data-ttu-id="c8815-137">以建立伺服器和資料庫時所指定的值，取代主機、資料庫名稱、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="c8815-137">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

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

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}


```

## <a name="update-data"></a><span data-ttu-id="c8815-138">更新資料</span><span class="sxs-lookup"><span data-stu-id="c8815-138">Update data</span></span>
<span data-ttu-id="c8815-139">使用下列程式碼搭配 **UPDATE** SQL 陳述式來連線和讀取資料。</span><span class="sxs-lookup"><span data-stu-id="c8815-139">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="c8815-140">此程式碼使用 ODBC 類別搭配 [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) 方法來建立 MySQL 連線。</span><span class="sxs-lookup"><span data-stu-id="c8815-140">The code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) to establish a connection to MySQL.</span></span> <span data-ttu-id="c8815-141">然後，程式碼會使用 [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) 方法，設定 CommandText 屬性，並呼叫 [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) 方法來執行資料庫命令。</span><span class="sxs-lookup"><span data-stu-id="c8815-141">Then the code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets the CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) to run the database commands.</span></span>

<span data-ttu-id="c8815-142">以建立伺服器和資料庫時所指定的值，取代主機、資料庫名稱、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="c8815-142">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

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

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}



```


## <a name="delete-data"></a><span data-ttu-id="c8815-143">刪除資料</span><span class="sxs-lookup"><span data-stu-id="c8815-143">Delete data</span></span>
<span data-ttu-id="c8815-144">使用下列程式碼搭配 **DELETE** SQL 陳述式來連線和刪除資料。</span><span class="sxs-lookup"><span data-stu-id="c8815-144">Use the following code to connect and delete the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="c8815-145">此程式碼使用 ODBC 類別搭配 [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) 方法來建立 MySQL 連線。</span><span class="sxs-lookup"><span data-stu-id="c8815-145">The code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) to establish a connection to MySQL.</span></span> <span data-ttu-id="c8815-146">然後，程式碼會使用 [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) 方法，設定 CommandText 屬性，並呼叫 [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) 方法來執行資料庫命令。</span><span class="sxs-lookup"><span data-stu-id="c8815-146">Then the code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets the CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) to run the database commands.</span></span>

<span data-ttu-id="c8815-147">以建立伺服器和資料庫時所指定的值，取代主機、資料庫名稱、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="c8815-147">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

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

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}

```

## <a name="next-steps"></a><span data-ttu-id="c8815-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c8815-148">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="c8815-149">使用傾印和還原來將 MySQL 資料庫移轉至適用於 MySQL 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="c8815-149">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
