---
title: "aaaGet 入門 （垂直資料分割） 的跨資料庫查詢 |Microsoft 文件"
description: "如何使用 toouse 彈性資料庫查詢垂直資料分割資料庫"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: e5b44b10-c432-4f96-b20e-08615ff4d5dd
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: torsteng
ms.openlocfilehash: 9e6183268e8bf87e3ac28f502711fcc05a7a3f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a>開始使用跨資料庫查詢 (垂直資料分割) (預覽)
Azure SQL Database 的彈性資料庫查詢 （預覽） 可讓您跨越多個資料庫使用單一連接點的 toorun T-SQL 查詢。 本主題適用於太[垂直資料分割資料庫](sql-database-elastic-query-vertical-partitioning.md)。  

完成時，您將： 了解如何 tooconfigure 與使用 Azure SQL Database tooperform 查詢該跨越多個相關的資料庫。 

如需有關 hello 彈性資料庫查詢功能的詳細資訊，請參閱[Azure SQL Database 彈性資料庫查詢概觀](sql-database-elastic-query-overview.md)。 

## <a name="prerequisites"></a>必要條件

您必須具備 ALTER ANY EXTERNAL DATA SOURCE 權限。 此權限會包含 hello ALTER DATABASE 權限。 ALTER ANY EXTERNAL DATA SOURCE 權限是必要的 toorefer toohello 基礎資料來源。

## <a name="create-hello-sample-databases"></a>建立 hello 範例資料庫
與 toostart，我們需要 toocreate 兩個資料庫，**客戶**和**訂單**，有兩種 hello 相同或不同的邏輯伺服器。   

執行下列查詢在 hello hello**訂單**資料庫 toocreate hello **OrderInformation**資料表和輸入 hello 範例資料。 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

現在，執行下列查詢在 hello**客戶**資料庫 toocreate hello **CustomerInformation**資料表和輸入 hello 範例資料。 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a>建立資料庫物件
### <a name="database-scoped-master-key-and-credentials"></a>資料庫範圍的主要金鑰和認證
1. 在 Visual Studio 中開啟 SQL Server Management Studio 或 SQL Server Data Tools
2. 連接 toohello Orders 資料庫，並執行下列 T-SQL 命令 hello:
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    hello 「 使用者名稱 」 和 「 密碼 」 應 hello 使用者名稱，而且使用 toologin hello 客戶資料庫密碼。
    目前不支援使用 Azure Active Directory 與彈性查詢進行驗證。

### <a name="external-data-sources"></a>外部資料來源
toocreate 外部資料來源，執行下列命令在 hello Orders 資料庫上的 hello: 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a>外部資料表
Hello Orders 資料庫符合 hello hello CustomerInformation 資料表定義上建立外部資料表：

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>執行範例彈性資料庫 T-SQL 查詢
定義外部資料來源和外部資料表之後，您現在可以使用 T-SQL tooquery 外部資料表。 Hello Orders 資料庫上執行下列查詢： 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a>成本
目前，hello 彈性資料庫查詢功能併入您的 Azure SQL Database 的 hello 成本。  

如需價格資訊，請參閱 [SQL Database 價格](https://azure.microsoft.com/pricing/details/sql-database)。 

## <a name="next-steps"></a>後續步驟

* 如需彈性查詢的概觀，請參閱[彈性查詢概觀](sql-database-elastic-query-overview.md)。
* 如需垂直資料分割之資料的語法和範例查詢，請參閱[查詢垂直資料分割的資料](sql-database-elastic-query-vertical-partitioning.md)
* 如需水平資料分割 (分區化) 教學課程，請參閱[開始使用彈性查詢進行水平資料分割 (分區化)](sql-database-elastic-query-getting-started.md)。
* 如需水平資料分割之資料的語法和範例查詢，請參閱[查詢水平資料分割的資料](sql-database-elastic-query-horizontal-partitioning.md)
* 如需會在單一遠端 Azure SQL Database 或一組在水平資料分割配置中作為分區之資料庫上執行 Transact-SQL 陳述式的預存程序，請參閱 [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714)。