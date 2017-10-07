---
title: "從 C# PostgreSQL 連接 tooAzure 資料庫 |Microsoft 文件"
description: "本快速入門提供的 C# (.NET) 程式碼範例可以使用 tooconnect 並查詢 PostgreSQL 從 Azure 資料庫的資料。"
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
ms.openlocfilehash: 5ba7426f8ad263193cdb208b3531da0ceff181dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-net-c-tooconnect-and-query-data"></a><span data-ttu-id="656c9-103">Azure PostgreSQL 資料庫： 使用.NET (C#) tooconnect 和查詢資料</span><span class="sxs-lookup"><span data-stu-id="656c9-103">Azure Database for PostgreSQL: Use .NET (C#) tooconnect and query data</span></span>
<span data-ttu-id="656c9-104">本快速入門示範如何 tooconnect tooan PostgreSQL 使用 C# 應用程式的 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="656c9-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a C# application.</span></span> <span data-ttu-id="656c9-105">它會顯示 toouse SQL 陳述式 tooquery，如何插入、 更新和刪除 hello 資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="656c9-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="656c9-106">hello 本文章中的步驟假設您已熟悉開發使用 C# 中，且新 tooworking Azure PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="656c9-106">hello steps in this article assume that you are familiar with developing using C#, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="656c9-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="656c9-107">Prerequisites</span></span>
<span data-ttu-id="656c9-108">本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：</span><span class="sxs-lookup"><span data-stu-id="656c9-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="656c9-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="656c9-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="656c9-110">建立 DB - CLI</span><span class="sxs-lookup"><span data-stu-id="656c9-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="656c9-111">您也需要：</span><span class="sxs-lookup"><span data-stu-id="656c9-111">You also need to:</span></span>
- <span data-ttu-id="656c9-112">安裝 [.NET Framework](https://www.microsoft.com/net/download)。</span><span class="sxs-lookup"><span data-stu-id="656c9-112">Install [.NET Framework](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="656c9-113">請遵循 hello hello 連結文章 tooinstall.NET 特別為您的平台 （Windows、 Ubuntu Linux 或 macOS） 中的步驟。</span><span class="sxs-lookup"><span data-stu-id="656c9-113">Follow hello steps in hello linked article tooinstall .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="656c9-114">安裝[Visual Studio](https://www.visualstudio.com/downloads/)或 Visual Studio Code tootype 和編輯程式碼。</span><span class="sxs-lookup"><span data-stu-id="656c9-114">Install [Visual Studio](https://www.visualstudio.com/downloads/) or Visual Studio Code tootype and edit code.</span></span>
- <span data-ttu-id="656c9-115">安裝 [Npgsql](http://www.npgsql.org/doc/index.html) 程式庫，如下所述。</span><span class="sxs-lookup"><span data-stu-id="656c9-115">Install [Npgsql](http://www.npgsql.org/doc/index.html) library as described below.</span></span>

## <a name="install-npgsql-references-into-your-visual-studio-solution"></a><span data-ttu-id="656c9-116">將 Npgsql 參考安裝在 Visual Studio 解決方案中</span><span class="sxs-lookup"><span data-stu-id="656c9-116">Install Npgsql references into your Visual Studio solution</span></span>
<span data-ttu-id="656c9-117">從 C# 應用程式 tooPostgreSQL，hello tooconnect 使用稱為 Npgsql 的 hello 開放原始碼 ADO.NET 程式庫。</span><span class="sxs-lookup"><span data-stu-id="656c9-117">tooconnect from hello C# application tooPostgreSQL, use hello open source ADO.NET library called Npgsql.</span></span> <span data-ttu-id="656c9-118">下載並輕鬆地管理 hello 參考，NuGet 可幫助。</span><span class="sxs-lookup"><span data-stu-id="656c9-118">NuGet helps download and manage hello references easily.</span></span>

1. <span data-ttu-id="656c9-119">建立新的 C# 解決方案或開啟現有解決方案：</span><span class="sxs-lookup"><span data-stu-id="656c9-119">Create a new C# solution, or open an existing one:</span></span> 
   - <span data-ttu-id="656c9-120">在 Visual Studio 中，按一下 [檔案] 功能表的 [新增] > [專案]，以建立解決方案。</span><span class="sxs-lookup"><span data-stu-id="656c9-120">Within Visual Studio, create a solution, by clicking File menu **New** > **Project**.</span></span>
   - <span data-ttu-id="656c9-121">在 hello 新增專案對話方塊中，展開**範本** > **Visual C#**。</span><span class="sxs-lookup"><span data-stu-id="656c9-121">In hello New Project dialogue, expand **Templates** > **Visual C#**.</span></span> 
   - <span data-ttu-id="656c9-122">選擇適當的範本，例如 [主控台應用程式 (.NET Core)]。</span><span class="sxs-lookup"><span data-stu-id="656c9-122">Choose an appropriate template such as **Console App (.NET Core)**.</span></span>

2. <span data-ttu-id="656c9-123">使用 Nuget 套件管理員 tooinstall Npgsql hello:</span><span class="sxs-lookup"><span data-stu-id="656c9-123">Use hello Nuget Package Manager tooinstall Npgsql:</span></span>
   - <span data-ttu-id="656c9-124">按一下 hello**工具**功能表 > **NuGet 套件管理員** > **Package Manager Console**。</span><span class="sxs-lookup"><span data-stu-id="656c9-124">Click hello **Tools** menu > **NuGet Package Manager** > **Package Manager Console**.</span></span>
   - <span data-ttu-id="656c9-125">在 hello **Package Manager Console**，類型`Install-Package Npgsql`</span><span class="sxs-lookup"><span data-stu-id="656c9-125">In hello **Package Manager Console**, type `Install-Package Npgsql`</span></span>
   - <span data-ttu-id="656c9-126">hello 安裝命令下載 hello Npgsql.dll 和相關的組件，並將它們加入做為 hello 方案中的相依性。</span><span class="sxs-lookup"><span data-stu-id="656c9-126">hello install command downloads hello Npgsql.dll and related assemblies and adds them as dependencies in hello solution.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="656c9-127">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="656c9-127">Get connection information</span></span>
<span data-ttu-id="656c9-128">取得 PostgreSQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="656c9-128">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="656c9-129">您需要 hello 完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="656c9-129">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="656c9-130">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="656c9-130">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="656c9-131">在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，並搜尋您已經建立，例如 hello 伺服器**mypgserver 20170401**。</span><span class="sxs-lookup"><span data-stu-id="656c9-131">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="656c9-132">按一下伺服器名稱，hello **mypgserver 20170401**。</span><span class="sxs-lookup"><span data-stu-id="656c9-132">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="656c9-133">選取 hello 伺服器**概觀**頁面。</span><span class="sxs-lookup"><span data-stu-id="656c9-133">Select hello server's **Overview** page.</span></span> <span data-ttu-id="656c9-134">請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。</span><span class="sxs-lookup"><span data-stu-id="656c9-134">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="656c9-135">![Azure Database for PostgreSQL - 伺服器管理員登入](./media/connect-csharp/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="656c9-135">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-csharp/1-connection-string.png)</span></span>
5. <span data-ttu-id="656c9-136">如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="656c9-136">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="656c9-137">連線、建立資料表及插入資料</span><span class="sxs-lookup"><span data-stu-id="656c9-137">Connect, create table, and insert data</span></span>
<span data-ttu-id="656c9-138">使用 hello 下列程式碼 tooconnect 並載入 hello 資料使用**CREATE TABLE**和**INSERT INTO** SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="656c9-138">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="656c9-139">hello 程式碼使用 NpgsqlCommand 類別具有方法[open （)](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish 連接 tooPostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="656c9-139">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="656c9-140">然後，hello 程式碼會使用方法[CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand)管理員、 設定 hello CommandText 屬性，並呼叫方法[executenonquery （)](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello 資料庫命令。</span><span class="sxs-lookup"><span data-stu-id="656c9-140">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span> 

<span data-ttu-id="656c9-141">取代 hello 值，指定當您建立 hello 伺服器和資料庫中的 hello 主機、 DBName、 使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="656c9-141">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        // Obtain connection string information from hello portal
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

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```

## <a name="read-data"></a><span data-ttu-id="656c9-142">讀取資料</span><span class="sxs-lookup"><span data-stu-id="656c9-142">Read data</span></span>
<span data-ttu-id="656c9-143">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**選取**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="656c9-143">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="656c9-144">hello 程式碼使用 NpgsqlCommand 類別具有方法[open （)](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish 連接 tooPostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="656c9-144">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="656c9-145">然後，hello 程式碼會使用方法[CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand)和方法[executereader （)](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) toorun hello 資料庫命令。</span><span class="sxs-lookup"><span data-stu-id="656c9-145">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) and method [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) toorun hello database commands.</span></span> <span data-ttu-id="656c9-146">接下來 hello 程式碼使用[read](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) tooadvance toohello hello 結果記錄。</span><span class="sxs-lookup"><span data-stu-id="656c9-146">Next hello code uses [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) tooadvance toohello records in hello results.</span></span> <span data-ttu-id="656c9-147">然後，hello 程式碼會使用[GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_)和[Sr](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) tooparse hello 記錄中的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="656c9-147">Then hello code uses [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) and [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) tooparse hello values in hello record.</span></span>

<span data-ttu-id="656c9-148">取代 hello 值，指定當您建立 hello 伺服器和資料庫中的 hello 主機、 DBName、 使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="656c9-148">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        // Obtain connection string information from hello portal
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

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```


## <a name="update-data"></a><span data-ttu-id="656c9-149">更新資料</span><span class="sxs-lookup"><span data-stu-id="656c9-149">Update data</span></span>
<span data-ttu-id="656c9-150">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**更新**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="656c9-150">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="656c9-151">hello 程式碼使用 NpgsqlCommand 類別具有方法[open （)](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish 連接 tooPostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="656c9-151">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="656c9-152">然後，hello 程式碼會使用方法[CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand)管理員、 設定 hello CommandText 屬性，並呼叫方法[executenonquery （)](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello 資料庫命令。</span><span class="sxs-lookup"><span data-stu-id="656c9-152">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span>

<span data-ttu-id="656c9-153">取代 hello 值，指定當您建立 hello 伺服器和資料庫中的 hello 主機、 DBName、 使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="656c9-153">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        // Obtain connection string information from hello portal
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

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```


## <a name="delete-data"></a><span data-ttu-id="656c9-154">刪除資料</span><span class="sxs-lookup"><span data-stu-id="656c9-154">Delete data</span></span>
<span data-ttu-id="656c9-155">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**刪除**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="656c9-155">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="656c9-156">hello 程式碼使用 NpgsqlCommand 類別具有方法[open （)](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish 連接 tooPostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="656c9-156">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="656c9-157">然後，hello 程式碼會使用方法[CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand)管理員、 設定 hello CommandText 屬性，並呼叫方法[executenonquery （)](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello 資料庫命令。</span><span class="sxs-lookup"><span data-stu-id="656c9-157">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span>

<span data-ttu-id="656c9-158">取代 hello 值，指定當您建立 hello 伺服器和資料庫中的 hello 主機、 DBName、 使用者和密碼參數。</span><span class="sxs-lookup"><span data-stu-id="656c9-158">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        // Obtain connection string information from hello portal
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

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="656c9-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="656c9-159">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="656c9-160">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="656c9-160">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
