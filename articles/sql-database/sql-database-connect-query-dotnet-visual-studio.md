---
title: "使用 Visual Studio 和 .NET 查詢 Azure SQL Database | Microsoft Docs"
description: "本主題說明如何使用 Visual Studio 來建立連線到 Azure SQL Database 的程式，並使用 Transact-SQL 陳述式查詢。"
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
ms.openlocfilehash: 105dab17823a7e7f6957a604833f4ecad35c14bd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-net-c-with-visual-studio-to-connect-and-query-an-azure-sql-database"></a><span data-ttu-id="16028-103">使用 .NET (C#) 搭配 Visual Studio 連線及查詢 Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="16028-103">Use .NET (C#) with Visual Studio to connect and query an Azure SQL database</span></span>

<span data-ttu-id="16028-104">此快速入門教學課程示範如何使用 [.NET 架構](https://www.microsoft.com/net/)搭配 Visual Studio 來建立 C# 程式以連線至 Azure SQL 資料庫，並使用 Transact-SQL 陳述式來查詢資料。</span><span class="sxs-lookup"><span data-stu-id="16028-104">This quick start tutorial demonstrates how to use the [.NET framework](https://www.microsoft.com/net/) to create a C# program with Visual Studio to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16028-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="16028-105">Prerequisites</span></span>

<span data-ttu-id="16028-106">若要完成本快速入門教學課程，請確定您具有下列項目︰</span><span class="sxs-lookup"><span data-stu-id="16028-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="16028-107">Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="16028-107">An Azure SQL database.</span></span> <span data-ttu-id="16028-108">本快速入門使用其中一個快速入門建立的資源︰</span><span class="sxs-lookup"><span data-stu-id="16028-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="16028-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="16028-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="16028-110">建立 DB - CLI</span><span class="sxs-lookup"><span data-stu-id="16028-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="16028-111">建立 DB - PowerShell</span><span class="sxs-lookup"><span data-stu-id="16028-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="16028-112">在此快速入門教學課程中，您所使用電腦的公用 IP 位址[伺服器層級防火牆規則](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)。</span><span class="sxs-lookup"><span data-stu-id="16028-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="16028-113">安裝 [Visual Studio Community 2017、Visual Studio Professional 2017 或 Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="16028-113">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="16028-114">SQL Server 連線資訊</span><span class="sxs-lookup"><span data-stu-id="16028-114">SQL server connection information</span></span>

<span data-ttu-id="16028-115">取得連線到 Azure SQL Database 所需的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="16028-115">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="16028-116">您在下一個程序中需要完整的伺服器名稱、資料庫名稱和登入資訊。</span><span class="sxs-lookup"><span data-stu-id="16028-116">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="16028-117">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="16028-117">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="16028-118">從左側功能表中選取 [SQL Database]，按一下 [SQL Database]頁面上您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="16028-118">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="16028-119">在您資料庫的 [概觀] 頁面上，檢閱如下圖所示的完整伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="16028-119">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="16028-120">您可以將滑鼠移至伺服器名稱上，以帶出 [按一下以複製] 選項。</span><span class="sxs-lookup"><span data-stu-id="16028-120">You can hover over the server name to bring up the **Click to copy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="16028-122">如果您忘記 Azure SQL Database 伺服器登入資訊，請瀏覽至 [SQL Database 伺服器] 頁面來檢視伺服器系統管理員名稱。</span><span class="sxs-lookup"><span data-stu-id="16028-122">If you forget your Azure SQL Database server login information, navigate to the SQL Database server page to view the server admin name.</span></span> <span data-ttu-id="16028-123">如有必要，您可以重設密碼。</span><span class="sxs-lookup"><span data-stu-id="16028-123">You can reset the password if necessary.</span></span>

5. <span data-ttu-id="16028-124">按一下 [顯示資料庫連接字串]。</span><span class="sxs-lookup"><span data-stu-id="16028-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="16028-125">檢閱完整的 **ADO.NET** 連接字串。</span><span class="sxs-lookup"><span data-stu-id="16028-125">Review the complete **ADO.NET** connection string.</span></span>

    ![ADO.NET 連接字串](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="16028-127">在您執行本教學課程的電腦上，公用 IP 位址必須有防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="16028-127">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="16028-128">如果您在不同電腦上或有不同的公用 IP 位址，請建立[使用 Azure 入口網站的伺服器層級防火牆規則](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)。</span><span class="sxs-lookup"><span data-stu-id="16028-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-visual-studio-project"></a><span data-ttu-id="16028-129">建立新的 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="16028-129">Create a new Visual Studio project</span></span>

1. <span data-ttu-id="16028-130">在 Visual Studio 中，選擇 [檔案]、[新增]、[專案]。</span><span class="sxs-lookup"><span data-stu-id="16028-130">In Visual Studio, choose **File**, **New**, **Project**.</span></span> 
2. <span data-ttu-id="16028-131">在 [新增專案] 對話方塊中，展開 [Visual C#]。</span><span class="sxs-lookup"><span data-stu-id="16028-131">In the **New Project** dialog, and expand **Visual C#**.</span></span>
3. <span data-ttu-id="16028-132">選取 [主控台應用程式] 並輸入 sqltest 作為專案名稱。</span><span class="sxs-lookup"><span data-stu-id="16028-132">Select **Console App** and enter *sqltest* for the project name.</span></span>
4. <span data-ttu-id="16028-133">按一下 [確定] 以在 Visual Studio 中建立並開啟新專案</span><span class="sxs-lookup"><span data-stu-id="16028-133">Click **OK** to create and open the new project in Visual Studio</span></span>
4. <span data-ttu-id="16028-134">在 [方案總管] 中，以滑鼠右鍵按一下 [sqltest]，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="16028-134">In Solution Explorer, right-click **sqltest** and click **Manage NuGet Packages**.</span></span> 
5. <span data-ttu-id="16028-135">在 [瀏覽] 上，搜尋 ```System.Data.SqlClient```，並在找到後選取它。</span><span class="sxs-lookup"><span data-stu-id="16028-135">On the **Browse**, search for ```System.Data.SqlClient``` and, when found, select it.</span></span>
6. <span data-ttu-id="16028-136">在 **System.Data.SqlClient** 頁面上，按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="16028-136">In the **System.Data.SqlClient** page, click **Install**.</span></span>
7. <span data-ttu-id="16028-137">當安裝完成時，檢閱所做的變更，然後按一下 [確定] 來關閉 [預覽] 視窗。</span><span class="sxs-lookup"><span data-stu-id="16028-137">When the install completes, review the changes and then click **OK** to close the **Preview** window.</span></span> 
8. <span data-ttu-id="16028-138">如果 [授權接受] 視窗出現時，按一下 [我接受]。</span><span class="sxs-lookup"><span data-stu-id="16028-138">If a **License Acceptance** window appears, click **I Accept**.</span></span>

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="16028-139">插入程式碼以查詢 SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="16028-139">Insert code to query SQL database</span></span>
1. <span data-ttu-id="16028-140">切換到 (或視需要開啟) **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="16028-140">Switch to (or open if necessary) **Program.cs**</span></span>

2. <span data-ttu-id="16028-141">使用下列程式碼取代 **Program.cs**的內容，並為您的伺服器、資料庫、使用者和密碼新增適當的值。</span><span class="sxs-lookup"><span data-stu-id="16028-141">Replace the contents of **Program.cs** with the following code and add the appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-the-code"></a><span data-ttu-id="16028-142">執行程式碼</span><span class="sxs-lookup"><span data-stu-id="16028-142">Run the code</span></span>

1. <span data-ttu-id="16028-143">按 **F5** 鍵執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="16028-143">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="16028-144">請確認前 20 個資料列已傳回，然後關閉應用程式視窗。</span><span class="sxs-lookup"><span data-stu-id="16028-144">Verify that the top 20 rows are returned and then close the application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16028-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="16028-145">Next steps</span></span>

- <span data-ttu-id="16028-146">了解如何在 Windows/Linux/macOS 中[使用 .NET Core 來連線及查詢 Azure SQL 資料庫](sql-database-connect-query-dotnet-core.md)。</span><span class="sxs-lookup"><span data-stu-id="16028-146">Learn how to [connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="16028-147">了解 [使用命令列以開始使用在 Windows/Linux/macOS 上的 .NET Core](/dotnet/core/tutorials/using-with-xplat-cli)。</span><span class="sxs-lookup"><span data-stu-id="16028-147">Learn about [Getting started with .NET Core on Windows/Linux/macOS using the command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="16028-148">深入了解如何[使用 SSMS 設計您的第一個 Azure SQL 資料庫](sql-database-design-first-database.md)或[使用 .NET 設計您的第一個 Azure SQL 資料庫](sql-database-design-first-database-csharp.md)。</span><span class="sxs-lookup"><span data-stu-id="16028-148">Learn how to [Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="16028-149">如需 .NET 的詳細資訊，請參閱 [.NET 文件](https://docs.microsoft.com/dotnet/)。</span><span class="sxs-lookup"><span data-stu-id="16028-149">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
