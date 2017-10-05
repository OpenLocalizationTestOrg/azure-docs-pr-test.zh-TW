---
title: "從 C# 連線至 Azure Database for PostgreSQL | Microsoft Docs"
description: "本快速入門提供 C# (.NET) 程式碼範例，可讓您連線至 Azure Database for PostgreSQL 來查詢資料。"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: csharp
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 91e0269e310688dc88d139430ccf386a1d26a61c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-net-c-to-connect-and-query-data"></a><span data-ttu-id="eec42-103">Azure Database for PostgreSQL︰使用 .NET (C#) 連線及查詢資料</span><span class="sxs-lookup"><span data-stu-id="eec42-103">Azure Database for PostgreSQL: Use .NET (C#) to connect and query data</span></span>
<span data-ttu-id="eec42-104">本快速入門示範如何使用 C# 應用程式來連線到 Azure Database for PostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="eec42-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a C# application.</span></span> <span data-ttu-id="eec42-105">它會顯示如何使用 SQL 陳述式來查詢、插入、更新和刪除資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="eec42-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="eec42-106">本文中的步驟假設您已熟悉使用 C# 進行開發，但不熟悉 Azure Database for PostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="eec42-106">The steps in this article assume that you are familiar with developing using C#, and that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eec42-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="eec42-107">Prerequisites</span></span>
<span data-ttu-id="eec42-108">本快速入門使用在以下任一指南中建立的資源作為起點︰</span><span class="sxs-lookup"><span data-stu-id="eec42-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="eec42-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="eec42-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="eec42-110">建立 DB - CLI</span><span class="sxs-lookup"><span data-stu-id="eec42-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="eec42-111">您也需要：</span><span class="sxs-lookup"><span data-stu-id="eec42-111">You also need to:</span></span>
- <span data-ttu-id="eec42-112">安裝 [.NET Framework](https://www.microsoft.com/net/download)。</span><span class="sxs-lookup"><span data-stu-id="eec42-112">Install [.NET Framework](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="eec42-113">請依照連結文章中的步驟，特別為您的平台 (Windows、Ubuntu Linux 或 macOS) 安裝 .NET。</span><span class="sxs-lookup"><span data-stu-id="eec42-113">Follow the steps in the linked article to install .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="eec42-114">安裝 [Visual Studio](https://www.visualstudio.com/downloads/) 或 Visual Studio Code 以輸入及編輯程式碼。</span><span class="sxs-lookup"><span data-stu-id="eec42-114">Install [Visual Studio](https://www.visualstudio.com/downloads/) or Visual Studio Code to type and edit code.</span></span>
- <span data-ttu-id="eec42-115">安裝 [Npgsql](http://www.npgsql.org/doc/index.html) 程式庫，如下所述。</span><span class="sxs-lookup"><span data-stu-id="eec42-115">Install [Npgsql](http://www.npgsql.org/doc/index.html) library as described below.</span></span>

## <a name="install-npgsql-references-into-your-visual-studio-solution"></a><span data-ttu-id="eec42-116">將 Npgsql 參考安裝在 Visual Studio 解決方案中</span><span class="sxs-lookup"><span data-stu-id="eec42-116">Install Npgsql references into your Visual Studio solution</span></span>
<span data-ttu-id="eec42-117">若要從 C# 應用程式連線到 PostgreSQL，請使用稱為 Npgsql 的開放原始碼 ADO.NET 程式庫。</span><span class="sxs-lookup"><span data-stu-id="eec42-117">To connect from the C# application to PostgreSQL, use the open source ADO.NET library called Npgsql.</span></span> <span data-ttu-id="eec42-118">NuGet 有助於輕鬆下載和管理參考。</span><span class="sxs-lookup"><span data-stu-id="eec42-118">NuGet helps download and manage the references easily.</span></span>

1. <span data-ttu-id="eec42-119">建立新的 C# 解決方案或開啟現有解決方案：</span><span class="sxs-lookup"><span data-stu-id="eec42-119">Create a new C# solution, or open an existing one:</span></span> 
   - <span data-ttu-id="eec42-120">在 Visual Studio 中，按一下 [檔案] 功能表的 [新增] > [專案]，以建立解決方案。</span><span class="sxs-lookup"><span data-stu-id="eec42-120">Within Visual Studio, create a solution, by clicking File menu **New** > **Project**.</span></span>
   - <span data-ttu-id="eec42-121">在 [新增專案] 對話方塊中，展開 [範本] > [Visual C#]。</span><span class="sxs-lookup"><span data-stu-id="eec42-121">In the New Project dialogue, expand **Templates** > **Visual C#**.</span></span> 
   - <span data-ttu-id="eec42-122">選擇適當的範本，例如 [主控台應用程式 (.NET Core)]。</span><span class="sxs-lookup"><span data-stu-id="eec42-122">Choose an appropriate template such as **Console App (.NET Core)**.</span></span>

2. <span data-ttu-id="eec42-123">使用 Nuget 套件管理員來安裝 Npgsql：</span><span class="sxs-lookup"><span data-stu-id="eec42-123">Use the Nuget Package Manager to install Npgsql:</span></span>
   - <span data-ttu-id="eec42-124">按一下 [工具] 功能表 > [Nuget 套件管理員] > [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="eec42-124">Click the **Tools** menu > **NuGet Package Manager** > **Package Manager Console**.</span></span>
   - <span data-ttu-id="eec42-125">在 [套件管理員主控台] 中，輸入 `Install-Package Npgsql`</span><span class="sxs-lookup"><span data-stu-id="eec42-125">In the **Package Manager Console**, type `Install-Package Npgsql`</span></span>
   - <span data-ttu-id="eec42-126">安裝命令會下載 Npgsql.dll 和相關組件，並將它們新增為解決方案中的相依性。</span><span class="sxs-lookup"><span data-stu-id="eec42-126">The install command downloads the Npgsql.dll and related assemblies and adds them as dependencies in the solution.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="eec42-127">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="eec42-127">Get connection information</span></span>
<span data-ttu-id="eec42-128">取得連線到 Azure Database for PostgreSQL 所需的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="eec42-128">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="eec42-129">您需要完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="eec42-129">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="eec42-130">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="eec42-130">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="eec42-131">從 Azure 入口網站的左側功能表中，按一下 [所有資源]，然後搜尋您所建立的伺服器，例如 **mypgserver-20170401**。</span><span class="sxs-lookup"><span data-stu-id="eec42-131">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="eec42-132">按一下伺服器名稱 [mypgserver-20170401]。</span><span class="sxs-lookup"><span data-stu-id="eec42-132">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="eec42-133">選取伺服器的 [概觀] 頁面。</span><span class="sxs-lookup"><span data-stu-id="eec42-133">Select the server's **Overview** page.</span></span> <span data-ttu-id="eec42-134">記下 [伺服器名稱] 和 [伺服器管理員登入名稱]。</span><span class="sxs-lookup"><span data-stu-id="eec42-134">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="eec42-135">![Azure Database for PostgreSQL - 伺服器管理員登入](./media/connect-csharp/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="eec42-135">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-csharp/1-connection-string.png)</span></span>
5. <span data-ttu-id="eec42-136">如果您忘記伺服器登入資訊，請瀏覽至 [概觀] 頁面來檢視伺服器管理員登入名稱，並視需要重設密碼。</span><span class="sxs-lookup"><span data-stu-id="eec42-136">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="eec42-137">連線、建立資料表及插入資料</span><span class="sxs-lookup"><span data-stu-id="eec42-137">Connect, create table, and insert data</span></span>
<span data-ttu-id="eec42-138">使用下列程式碼搭配 **CREATE TABLE** 和 **INSERT INTO** SQL 陳述式來連線和載入資料。</span><span class="sxs-lookup"><span data-stu-id="eec42-138">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="eec42-139">此程式碼使用 NpgsqlCommand 類別搭配 [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) 方法來建立 PostgreSQL 連線。</span><span class="sxs-lookup"><span data-stu-id="eec42-139">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="eec42-140">然後，程式碼會使用 [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) 方法，設定 CommandText 屬性，並呼叫 [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) 方法來執行資料庫命令。</span><span class="sxs-lookup"><span data-stu-id="eec42-140">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets the CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) to run the database commands.</span></span> 

<span data-ttu-id="eec42-141">以建立伺服器和資料庫時所指定的值，取代主機、資料庫名稱、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="eec42-141">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresCreate
    {
        // Obtain connection string information from the portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4}; SSL Mode=Prefer; Trust Server Certificate=true",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

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
                    @"
                                INSERT INTO inventory (name, quantity) VALUES ({0}, {1});
                                INSERT INTO inventory (name, quantity) VALUES ({2}, {3});
                                INSERT INTO inventory (name, quantity) VALUES ({4}, {5});
                            ",
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

## <a name="read-data"></a><span data-ttu-id="eec42-142">讀取資料</span><span class="sxs-lookup"><span data-stu-id="eec42-142">Read data</span></span>
<span data-ttu-id="eec42-143">使用下列程式碼搭配 **SELECT** SQL 陳述式來連線和讀取資料。</span><span class="sxs-lookup"><span data-stu-id="eec42-143">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="eec42-144">此程式碼使用 NpgsqlCommand 類別搭配 [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) 方法來建立 PostgreSQL 連線。</span><span class="sxs-lookup"><span data-stu-id="eec42-144">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="eec42-145">然後，程式碼會使用 [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) 和 [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) 方法來執行資料庫命令。</span><span class="sxs-lookup"><span data-stu-id="eec42-145">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) and method [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) to run the database commands.</span></span> <span data-ttu-id="eec42-146">接下來程式碼會使用 [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) 前往結果中的記錄。</span><span class="sxs-lookup"><span data-stu-id="eec42-146">Next the code uses [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) to advance to the records in the results.</span></span> <span data-ttu-id="eec42-147">接下來程式碼會使用 [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) 和 [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) 來剖析記錄中的值。</span><span class="sxs-lookup"><span data-stu-id="eec42-147">Then the code uses [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) and [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) to parse the values in the record.</span></span>

<span data-ttu-id="eec42-148">以建立伺服器和資料庫時所指定的值，取代主機、資料庫名稱、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="eec42-148">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresRead
    {
        // Obtain connection string information from the portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

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


## <a name="update-data"></a><span data-ttu-id="eec42-149">更新資料</span><span class="sxs-lookup"><span data-stu-id="eec42-149">Update data</span></span>
<span data-ttu-id="eec42-150">使用下列程式碼搭配 **UPDATE** SQL 陳述式來連線和讀取資料。</span><span class="sxs-lookup"><span data-stu-id="eec42-150">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="eec42-151">此程式碼使用 NpgsqlCommand 類別搭配 [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) 方法來建立 PostgreSQL 連線。</span><span class="sxs-lookup"><span data-stu-id="eec42-151">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="eec42-152">然後，程式碼會使用 [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) 方法，設定 CommandText 屬性，並呼叫 [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) 方法來執行資料庫命令。</span><span class="sxs-lookup"><span data-stu-id="eec42-152">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets the CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) to run the database commands.</span></span>

<span data-ttu-id="eec42-153">以建立伺服器和資料庫時所指定的值，取代主機、資料庫名稱、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="eec42-153">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresUpdate
    {
        // Obtain connection string information from the portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

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


## <a name="delete-data"></a><span data-ttu-id="eec42-154">刪除資料</span><span class="sxs-lookup"><span data-stu-id="eec42-154">Delete data</span></span>
<span data-ttu-id="eec42-155">使用下列程式碼搭配 **DELETE** SQL 陳述式來連線和讀取資料。</span><span class="sxs-lookup"><span data-stu-id="eec42-155">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="eec42-156">此程式碼使用 NpgsqlCommand 類別搭配 [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) 方法來建立 PostgreSQL 連線。</span><span class="sxs-lookup"><span data-stu-id="eec42-156">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="eec42-157">然後，程式碼會使用 [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) 方法，設定 CommandText 屬性，並呼叫 [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) 方法來執行資料庫命令。</span><span class="sxs-lookup"><span data-stu-id="eec42-157">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets the CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) to run the database commands.</span></span>

<span data-ttu-id="eec42-158">以建立伺服器和資料庫時所指定的值，取代主機、資料庫名稱、使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="eec42-158">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresDelete
    {
        // Obtain connection string information from the portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

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

## <a name="next-steps"></a><span data-ttu-id="eec42-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eec42-159">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="eec42-160">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="eec42-160">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
