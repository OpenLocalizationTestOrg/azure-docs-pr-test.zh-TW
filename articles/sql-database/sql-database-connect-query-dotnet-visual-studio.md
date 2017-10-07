---
title: "aaaUse Visual Studio 和.NET tooquery Azure SQL Database |Microsoft 文件"
description: "本主題說明如何 toouse Visual Studio toocreate 連接 tooan Azure SQL Database 和查詢使用 TRANSACT-SQL 陳述式的程式。"
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
ms.openlocfilehash: 038cfb9c680217dfeea5a9996a0abed88cc80559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-c-with-visual-studio-tooconnect-and-query-an-azure-sql-database"></a>使用 Visual Studio tooconnect.NET (C#) 和查詢 Azure SQL database

本快速入門教學課程示範如何 toouse hello [.NET framework](https://www.microsoft.com/net/) toocreate C# 程式使用 Visual Studio tooconnect tooan Azure SQL database，並使用 Transact SQL 陳述式 tooquery 資料。

## <a name="prerequisites"></a>必要條件

toocomplete 此快速入門教學課程，請確定您擁有 hello 下列：

- Azure SQL Database。 本快速入門會使用 hello 資源建立在其中一個這些快速入門： 

   - [建立 DB - 入口網站](sql-database-get-started-portal.md)
   - [建立 DB - CLI](sql-database-get-started-cli.md)
   - [建立 DB - PowerShell](sql-database-get-started-powershell.md)

- A[伺服器層級防火牆規則](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)您使用此快速入門教學課程中的 hello 電腦 hello 公用 IP 位址。
- 安裝 [Visual Studio Community 2017、Visual Studio Professional 2017 或 Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/)。

## <a name="sql-server-connection-information"></a>SQL Server 連線資訊

收到 hello 連線所需的資訊 tooconnect toohello Azure SQL database。 您需要 hello 完整的伺服器名稱、 資料庫名稱，以及 hello 下一個程序中的登入資訊。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 選取**SQL 資料庫**從 hello 左側功能表中，按一下您的資料庫上 hello **SQL 資料庫**頁面。 
3. 在 hello**概觀**頁面為您的資料庫檢閱 hello 完整伺服器名稱 hello 下列影像所示。 您可以將滑鼠停留在 hello 伺服器名稱 toobring 向上 hello**按一下 toocopy**選項。 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. 如果您忘記您的 Azure SQL Database 伺服器登入資訊，請瀏覽 toohello SQL 資料庫伺服器頁面 tooview hello 伺服器管理員的名稱。 如有必要，您可以將 hello 密碼重設。

5. 按一下 [顯示資料庫連接字串]。

6. 完成檢閱 hello **ADO.NET**連接字串。

    ![ADO.NET 連接字串](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> 防火牆規則必須可供您執行本教學課程中的 hello 電腦的 hello 公用 IP 位址。 如果您在不同電腦上或有不同的公用 IP 位址，建立[伺服器層級防火牆規則使用 hello Azure 入口網站](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)。 
>
  
## <a name="create-a-new-visual-studio-project"></a>建立新的 Visual Studio 專案

1. 在 Visual Studio 中，選擇 [檔案]、[新增]、[專案]。 
2. 在 [hello**新專案**] 對話方塊中，展開**Visual C#**。
3. 選取**主控台應用程式**輸入*sqltest* hello 專案名稱。
4. 按一下**確定**toocreate 和 Visual Studio 中的開啟 hello 新專案
4. 在 [方案總管] 中，以滑鼠右鍵按一下 [sqltest]，然後按一下 [管理 NuGet 套件]。 
5. 在 hello**瀏覽**，搜尋```System.Data.SqlClient```，當找到，請選取。
6. 在 hello **System.Data.SqlClient**頁面上，按一下**安裝**。
7. Hello 安裝完成時，檢閱 hello 變更，然後按一下**確定**tooclose hello**預覽**視窗。 
8. 如果 [授權接受] 視窗出現時，按一下 [我接受]。

## <a name="insert-code-tooquery-sql-database"></a>插入程式碼 tooquery SQL 資料庫
1. 太切換 （或開啟如有必要） **Program.cs**

2. 取代 hello 內容**Program.cs**以 hello 下列程式碼並新增值 hello 適當伺服器、 資料庫、 使用者及密碼。

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

## <a name="run-hello-code"></a>執行 hello 程式碼

1. 按**F5** toorun hello 應用程式。
2. 請確認 hello 前 20 個資料列會傳回，，然後關閉 hello 應用程式視窗。

## <a name="next-steps"></a>後續步驟

- 了解如何太[連接及查詢 Azure SQL database 使用.NET core](sql-database-connect-query-dotnet-core.md) Windows/Linux/macOS 上。  
- 深入了解[開始使用 Windows/Linux/macOS 使用 hello 命令列上的.NET Core](/dotnet/core/tutorials/using-with-xplat-cli)。
- 了解如何太[設計第一個 Azure SQL database 使用 SSMS](sql-database-design-first-database.md)或[設計第一個 Azure SQL database 使用.NET](sql-database-design-first-database-csharp.md)。
- 如需 .NET 的詳細資訊，請參閱 [.NET 文件](https://docs.microsoft.com/dotnet/)。
