---
title: "Azure SQL Database 的 aaaUse.NET Core tooquery |Microsoft 文件"
description: "本主題會示範如何 toouse.NET 核心 toocreate 連接 tooan Azure SQL Database 的程式，及查詢使用 TRANSACT-SQL 陳述式。"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 2d10c407f44f43b6baa3bf337cdd1173d9c9c35f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-c-tooquery-an-azure-sql-database"></a><span data-ttu-id="8c089-103">使用.NET Core (C#) tooquery Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="8c089-103">Use .NET Core (C#) tooquery an Azure SQL database</span></span>

<span data-ttu-id="8c089-104">本快速入門教學課程示範如何 toouse [.NET Core](https://www.microsoft.com/net/)上 Windows/Linux/macOS toocreate C# 程式 tooconnect tooan Azure SQL 資料庫，並使用 Transact SQL 陳述式 tooquery 資料。</span><span class="sxs-lookup"><span data-stu-id="8c089-104">This quick start tutorial demonstrates how toouse [.NET Core](https://www.microsoft.com/net/) on Windows/Linux/macOS toocreate a C# program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c089-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="8c089-105">Prerequisites</span></span>

<span data-ttu-id="8c089-106">toocomplete 此快速入門教學課程，請確定您擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="8c089-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="8c089-107">Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="8c089-107">An Azure SQL database.</span></span> <span data-ttu-id="8c089-108">本快速入門會使用 hello 資源建立在其中一個這些快速入門：</span><span class="sxs-lookup"><span data-stu-id="8c089-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="8c089-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="8c089-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="8c089-110">建立 DB - CLI</span><span class="sxs-lookup"><span data-stu-id="8c089-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="8c089-111">建立 DB - PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c089-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="8c089-112">A[伺服器層級防火牆規則](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)您使用此快速入門教學課程中的 hello 電腦 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8c089-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="8c089-113">您已安裝[適用於您作業系統的 .NET Core](https://www.microsoft.com/net/core)。</span><span class="sxs-lookup"><span data-stu-id="8c089-113">You have installed [.NET Core for your operating system](https://www.microsoft.com/net/core).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="8c089-114">SQL Server 連線資訊</span><span class="sxs-lookup"><span data-stu-id="8c089-114">SQL server connection information</span></span>

<span data-ttu-id="8c089-115">收到 hello 連線所需的資訊 tooconnect toohello Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="8c089-115">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="8c089-116">您需要 hello 完整的伺服器名稱、 資料庫名稱，以及 hello 下一個程序中的登入資訊。</span><span class="sxs-lookup"><span data-stu-id="8c089-116">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="8c089-117">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="8c089-117">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8c089-118">選取**SQL 資料庫**從 hello 左側功能表中，按一下您的資料庫上 hello **SQL 資料庫**頁面。</span><span class="sxs-lookup"><span data-stu-id="8c089-118">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="8c089-119">在 hello**概觀**頁面為您的資料庫檢閱 hello 完整伺服器名稱 hello 下列影像所示。</span><span class="sxs-lookup"><span data-stu-id="8c089-119">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="8c089-120">您可以將滑鼠停留在 hello 伺服器名稱 toobring 向上 hello**按一下 toocopy**選項。</span><span class="sxs-lookup"><span data-stu-id="8c089-120">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="8c089-122">如果您忘記您的 Azure SQL Database 伺服器登入資訊，請瀏覽 toohello SQL 資料庫伺服器頁面 tooview hello 伺服器管理員的名稱。</span><span class="sxs-lookup"><span data-stu-id="8c089-122">If you forget your Azure SQL Database server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span> <span data-ttu-id="8c089-123">如有必要，您可以將 hello 密碼重設。</span><span class="sxs-lookup"><span data-stu-id="8c089-123">You can reset hello password if necessary.</span></span>

5. <span data-ttu-id="8c089-124">按一下 [顯示資料庫連接字串]。</span><span class="sxs-lookup"><span data-stu-id="8c089-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="8c089-125">完成檢閱 hello **ADO.NET**連接字串。</span><span class="sxs-lookup"><span data-stu-id="8c089-125">Review hello complete **ADO.NET** connection string.</span></span>

    ![ADO.NET 連接字串](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="8c089-127">防火牆規則必須可供您執行本教學課程中的 hello 電腦的 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8c089-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="8c089-128">如果您在不同電腦上或有不同的公用 IP 位址，建立[伺服器層級防火牆規則使用 hello Azure 入口網站](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)。</span><span class="sxs-lookup"><span data-stu-id="8c089-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-net-project"></a><span data-ttu-id="8c089-129">建立新的 .NET 專案</span><span class="sxs-lookup"><span data-stu-id="8c089-129">Create a new .NET project</span></span>

1. <span data-ttu-id="8c089-130">開啟命令提示字元，並建立名為 sqltest 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="8c089-130">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="8c089-131">瀏覽您建立並執行下列命令的 hello toohello 資料夾：</span><span class="sxs-lookup"><span data-stu-id="8c089-131">Navigate toohello folder you created and run hello following command:</span></span>

    ```
    dotnet new console
    ```

2. <span data-ttu-id="8c089-132">開啟***sqltest.csproj***與慣用的文字編輯器將 System.Data.SqlClient 新增為相依性，使用下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="8c089-132">Open ***sqltest.csproj*** with your favorite text editor and add System.Data.SqlClient as a dependency using hello following code:</span></span>

    ```xml
    <ItemGroup>
        <PackageReference Include="System.Data.SqlClient" Version="4.3.0" />
    </ItemGroup>
    ```

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="8c089-133">插入程式碼 tooquery SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="8c089-133">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="8c089-134">在您的開發環境或慣用的文字編輯器中開啟 Program.cs</span><span class="sxs-lookup"><span data-stu-id="8c089-134">In your development environment or favorite text editor open **Program.cs**</span></span>

2. <span data-ttu-id="8c089-135">以下列程式碼並新增值 hello 適當伺服器、 資料庫、 使用者及密碼的 hello 取代 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="8c089-135">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```csharp
using System;
using System.Data.SqlClient;
using System.Text;

namespace sqltest
{
    class Program
    {
        static void Main(string[] args)
        {
            try 
            { 
                SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                builder.DataSource = "your_server.database.windows.net"; 
                builder.UserID = "your_user";            
                builder.Password = "your_password";     
                builder.InitialCatalog = "your_database";

                using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                {
                    Console.WriteLine("\nQuery data example:");
                    Console.WriteLine("=========================================\n");
                    
                    connection.Open();       
                    StringBuilder sb = new StringBuilder();
                    sb.Append("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName ");
                    sb.Append("FROM [SalesLT].[ProductCategory] pc ");
                    sb.Append("JOIN [SalesLT].[Product] p ");
                    sb.Append("ON pc.productcategoryid = p.productcategoryid;");
                    String sql = sb.ToString();

                    using (SqlCommand command = new SqlCommand(sql, connection))
                    {
                        using (SqlDataReader reader = command.ExecuteReader())
                        {
                            while (reader.Read())
                            {
                                Console.WriteLine("{0} {1}", reader.GetString(0), reader.GetString(1));
                            }
                        }
                    }                    
                }
            }
            catch (SqlException e)
            {
                Console.WriteLine(e.ToString());
            }
            Console.ReadLine();
        }
    }
}
```

## <a name="run-hello-code"></a><span data-ttu-id="8c089-136">執行 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="8c089-136">Run hello code</span></span>

1. <span data-ttu-id="8c089-137">在 hello 命令提示字元中執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="8c089-137">At hello command prompt, run hello following commands:</span></span>

   ```csharp
   dotnet restore
   dotnet run
   ```

2. <span data-ttu-id="8c089-138">請確認 hello 前 20 個資料列會傳回，，然後關閉 hello 應用程式視窗。</span><span class="sxs-lookup"><span data-stu-id="8c089-138">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8c089-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8c089-139">Next steps</span></span>

- <span data-ttu-id="8c089-140">[開始使用 Windows/Linux/macOS 使用 hello 命令列上的.NET Core](/dotnet/core/tutorials/using-with-xplat-cli)。</span><span class="sxs-lookup"><span data-stu-id="8c089-140">[Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="8c089-141">了解如何太[連接及查詢 Azure SQL database 使用 hello.NET framework 和 Visual Studio](sql-database-connect-query-dotnet-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="8c089-141">Learn how too[connect and query an Azure SQL database using hello .NET framework and Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span></span>  
- <span data-ttu-id="8c089-142">了解如何太[設計第一個 Azure SQL database 使用 SSMS](sql-database-design-first-database.md)或[設計第一個 Azure SQL database 使用.NET](sql-database-design-first-database-csharp.md)。</span><span class="sxs-lookup"><span data-stu-id="8c089-142">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="8c089-143">如需 .NET 的詳細資訊，請參閱 [.NET 文件](https://docs.microsoft.com/dotnet/)。</span><span class="sxs-lookup"><span data-stu-id="8c089-143">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
