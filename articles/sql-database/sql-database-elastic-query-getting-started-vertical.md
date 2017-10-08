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
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a><span data-ttu-id="68295-103">開始使用跨資料庫查詢 (垂直資料分割) (預覽)</span><span class="sxs-lookup"><span data-stu-id="68295-103">Get started with cross-database queries (vertical partitioning) (preview)</span></span>
<span data-ttu-id="68295-104">Azure SQL Database 的彈性資料庫查詢 （預覽） 可讓您跨越多個資料庫使用單一連接點的 toorun T-SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="68295-104">Elastic database query (preview) for Azure SQL Database allows you toorun T-SQL queries that span multiple databases using a single connection point.</span></span> <span data-ttu-id="68295-105">本主題適用於太[垂直資料分割資料庫](sql-database-elastic-query-vertical-partitioning.md)。</span><span class="sxs-lookup"><span data-stu-id="68295-105">This topic applies too[vertically partitioned databases](sql-database-elastic-query-vertical-partitioning.md).</span></span>  

<span data-ttu-id="68295-106">完成時，您將： 了解如何 tooconfigure 與使用 Azure SQL Database tooperform 查詢該跨越多個相關的資料庫。</span><span class="sxs-lookup"><span data-stu-id="68295-106">When completed, you will: learn how tooconfigure and use an Azure SQL Database tooperform queries that span multiple related databases.</span></span> 

<span data-ttu-id="68295-107">如需有關 hello 彈性資料庫查詢功能的詳細資訊，請參閱[Azure SQL Database 彈性資料庫查詢概觀](sql-database-elastic-query-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="68295-107">For more information about hello elastic database query feature, please see  [Azure SQL Database elastic database query overview](sql-database-elastic-query-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="68295-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="68295-108">Prerequisites</span></span>

<span data-ttu-id="68295-109">您必須具備 ALTER ANY EXTERNAL DATA SOURCE 權限。</span><span class="sxs-lookup"><span data-stu-id="68295-109">You must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="68295-110">此權限會包含 hello ALTER DATABASE 權限。</span><span class="sxs-lookup"><span data-stu-id="68295-110">This permission is included with hello ALTER DATABASE permission.</span></span> <span data-ttu-id="68295-111">ALTER ANY EXTERNAL DATA SOURCE 權限是必要的 toorefer toohello 基礎資料來源。</span><span class="sxs-lookup"><span data-stu-id="68295-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="create-hello-sample-databases"></a><span data-ttu-id="68295-112">建立 hello 範例資料庫</span><span class="sxs-lookup"><span data-stu-id="68295-112">Create hello sample databases</span></span>
<span data-ttu-id="68295-113">與 toostart，我們需要 toocreate 兩個資料庫，**客戶**和**訂單**，有兩種 hello 相同或不同的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="68295-113">toostart with, we need toocreate two databases, **Customers** and **Orders**, either in hello same or different logical servers.</span></span>   

<span data-ttu-id="68295-114">執行下列查詢在 hello hello**訂單**資料庫 toocreate hello **OrderInformation**資料表和輸入 hello 範例資料。</span><span class="sxs-lookup"><span data-stu-id="68295-114">Execute hello following queries on hello **Orders** database toocreate hello **OrderInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

<span data-ttu-id="68295-115">現在，執行下列查詢在 hello**客戶**資料庫 toocreate hello **CustomerInformation**資料表和輸入 hello 範例資料。</span><span class="sxs-lookup"><span data-stu-id="68295-115">Now, execute following query on hello **Customers** database toocreate hello **CustomerInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a><span data-ttu-id="68295-116">建立資料庫物件</span><span class="sxs-lookup"><span data-stu-id="68295-116">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="68295-117">資料庫範圍的主要金鑰和認證</span><span class="sxs-lookup"><span data-stu-id="68295-117">Database scoped master key and credentials</span></span>
1. <span data-ttu-id="68295-118">在 Visual Studio 中開啟 SQL Server Management Studio 或 SQL Server Data Tools</span><span class="sxs-lookup"><span data-stu-id="68295-118">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="68295-119">連接 toohello Orders 資料庫，並執行下列 T-SQL 命令 hello:</span><span class="sxs-lookup"><span data-stu-id="68295-119">Connect toohello Orders database and execute hello following T-SQL commands:</span></span>
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    <span data-ttu-id="68295-120">hello 「 使用者名稱 」 和 「 密碼 」 應 hello 使用者名稱，而且使用 toologin hello 客戶資料庫密碼。</span><span class="sxs-lookup"><span data-stu-id="68295-120">hello "username" and "password" should be hello username and password used toologin into hello Customers database.</span></span>
    <span data-ttu-id="68295-121">目前不支援使用 Azure Active Directory 與彈性查詢進行驗證。</span><span class="sxs-lookup"><span data-stu-id="68295-121">Authentication using Azure Active Directory with elastic queries is not currently supported.</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="68295-122">外部資料來源</span><span class="sxs-lookup"><span data-stu-id="68295-122">External data sources</span></span>
<span data-ttu-id="68295-123">toocreate 外部資料來源，執行下列命令在 hello Orders 資料庫上的 hello:</span><span class="sxs-lookup"><span data-stu-id="68295-123">toocreate an external data source, execute hello following command on hello Orders database:</span></span> 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a><span data-ttu-id="68295-124">外部資料表</span><span class="sxs-lookup"><span data-stu-id="68295-124">External tables</span></span>
<span data-ttu-id="68295-125">Hello Orders 資料庫符合 hello hello CustomerInformation 資料表定義上建立外部資料表：</span><span class="sxs-lookup"><span data-stu-id="68295-125">Create an external table on hello Orders database, which matches hello definition of hello CustomerInformation table:</span></span>

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="68295-126">執行範例彈性資料庫 T-SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="68295-126">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="68295-127">定義外部資料來源和外部資料表之後，您現在可以使用 T-SQL tooquery 外部資料表。</span><span class="sxs-lookup"><span data-stu-id="68295-127">Once you have defined your external data source and your external tables you can now use T-SQL tooquery your external tables.</span></span> <span data-ttu-id="68295-128">Hello Orders 資料庫上執行下列查詢：</span><span class="sxs-lookup"><span data-stu-id="68295-128">Execute this query on hello Orders database:</span></span> 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a><span data-ttu-id="68295-129">成本</span><span class="sxs-lookup"><span data-stu-id="68295-129">Cost</span></span>
<span data-ttu-id="68295-130">目前，hello 彈性資料庫查詢功能併入您的 Azure SQL Database 的 hello 成本。</span><span class="sxs-lookup"><span data-stu-id="68295-130">Currently, hello elastic database query feature is included into hello cost of your Azure SQL Database.</span></span>  

<span data-ttu-id="68295-131">如需價格資訊，請參閱 [SQL Database 價格](https://azure.microsoft.com/pricing/details/sql-database)。</span><span class="sxs-lookup"><span data-stu-id="68295-131">For pricing information see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="68295-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="68295-132">Next steps</span></span>

* <span data-ttu-id="68295-133">如需彈性查詢的概觀，請參閱[彈性查詢概觀](sql-database-elastic-query-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="68295-133">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="68295-134">如需垂直資料分割之資料的語法和範例查詢，請參閱[查詢垂直資料分割的資料](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="68295-134">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="68295-135">如需水平資料分割 (分區化) 教學課程，請參閱[開始使用彈性查詢進行水平資料分割 (分區化)](sql-database-elastic-query-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="68295-135">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="68295-136">如需水平資料分割之資料的語法和範例查詢，請參閱[查詢水平資料分割的資料](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="68295-136">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="68295-137">如需會在單一遠端 Azure SQL Database 或一組在水平資料分割配置中作為分區之資料庫上執行 Transact-SQL 陳述式的預存程序，請參閱 [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714)。</span><span class="sxs-lookup"><span data-stu-id="68295-137">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>