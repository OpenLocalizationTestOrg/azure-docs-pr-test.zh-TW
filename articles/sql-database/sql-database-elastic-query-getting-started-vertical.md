---
title: "開始使用跨資料庫查詢 (垂直資料分割) | Microsoft Docs"
description: "如何使用具有垂直分割資料庫的彈性資料庫查詢"
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
ms.openlocfilehash: 17158c4960e9ba9251524659c90af9aec1316774
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a><span data-ttu-id="d0c7f-103">開始使用跨資料庫查詢 (垂直資料分割) (預覽)</span><span class="sxs-lookup"><span data-stu-id="d0c7f-103">Get started with cross-database queries (vertical partitioning) (preview)</span></span>
<span data-ttu-id="d0c7f-104">Azure SQL Database 彈性資料庫查詢 (預覽) 可讓您執行使用單一連接點跨越多個資料庫的 T-SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="d0c7f-104">Elastic database query (preview) for Azure SQL Database allows you to run T-SQL queries that span multiple databases using a single connection point.</span></span> <span data-ttu-id="d0c7f-105">本主題適用於 [垂直分割的資料庫](sql-database-elastic-query-vertical-partitioning.md)。</span><span class="sxs-lookup"><span data-stu-id="d0c7f-105">This topic applies to [vertically partitioned databases](sql-database-elastic-query-vertical-partitioning.md).</span></span>  

<span data-ttu-id="d0c7f-106">完成時，您將：了解如何設定和使用 Azure SQL Database 以執行跨越多個相關資料庫的查詢。</span><span class="sxs-lookup"><span data-stu-id="d0c7f-106">When completed, you will: learn how to configure and use an Azure SQL Database to perform queries that span multiple related databases.</span></span> 

<span data-ttu-id="d0c7f-107">如需有關彈性資料庫查詢功能的詳細資訊，請參閱 [Azure SQL Database 彈性資料庫查詢概觀](sql-database-elastic-query-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d0c7f-107">For more information about the elastic database query feature, please see  [Azure SQL Database elastic database query overview](sql-database-elastic-query-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d0c7f-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="d0c7f-108">Prerequisites</span></span>

<span data-ttu-id="d0c7f-109">您必須具備 ALTER ANY EXTERNAL DATA SOURCE 權限。</span><span class="sxs-lookup"><span data-stu-id="d0c7f-109">You must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="d0c7f-110">這個權限包含在 ALTER DATABASE 權限中。</span><span class="sxs-lookup"><span data-stu-id="d0c7f-110">This permission is included with the ALTER DATABASE permission.</span></span> <span data-ttu-id="d0c7f-111">需有 ALTER ANY EXTERNAL DATA SOURCE 權限，才能參考基礎資料來源。</span><span class="sxs-lookup"><span data-stu-id="d0c7f-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="create-the-sample-databases"></a><span data-ttu-id="d0c7f-112">建立範例資料庫</span><span class="sxs-lookup"><span data-stu-id="d0c7f-112">Create the sample databases</span></span>
<span data-ttu-id="d0c7f-113">開始使用前，我們需要在相同或不同的邏輯伺服器中建立兩個資料庫 **Customers** 和 **Orders**。</span><span class="sxs-lookup"><span data-stu-id="d0c7f-113">To start with, we need to create two databases, **Customers** and **Orders**, either in the same or different logical servers.</span></span>   

<span data-ttu-id="d0c7f-114">在 **Orders** 資料庫上執行下列查詢，以建立 **OrderInformation** 資料表及輸入範例資料。</span><span class="sxs-lookup"><span data-stu-id="d0c7f-114">Execute the following queries on the **Orders** database to create the **OrderInformation** table and input the sample data.</span></span> 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

<span data-ttu-id="d0c7f-115">現在，在 **Customers** 資料庫上執行下列查詢，以建立 **CustomerInformation** 資料表及輸入範例資料。</span><span class="sxs-lookup"><span data-stu-id="d0c7f-115">Now, execute following query on the **Customers** database to create the **CustomerInformation** table and input the sample data.</span></span> 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a><span data-ttu-id="d0c7f-116">建立資料庫物件</span><span class="sxs-lookup"><span data-stu-id="d0c7f-116">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="d0c7f-117">資料庫範圍的主要金鑰和認證</span><span class="sxs-lookup"><span data-stu-id="d0c7f-117">Database scoped master key and credentials</span></span>
1. <span data-ttu-id="d0c7f-118">在 Visual Studio 中開啟 SQL Server Management Studio 或 SQL Server Data Tools</span><span class="sxs-lookup"><span data-stu-id="d0c7f-118">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="d0c7f-119">連接至 Orders 資料庫，並執行下列 T-SQL 命令：</span><span class="sxs-lookup"><span data-stu-id="d0c7f-119">Connect to the Orders database and execute the following T-SQL commands:</span></span>
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    <span data-ttu-id="d0c7f-120">"username" 和 "password" 應該是用來登入 Customers 資料庫的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="d0c7f-120">The "username" and "password" should be the username and password used to login into the Customers database.</span></span>
    <span data-ttu-id="d0c7f-121">目前不支援使用 Azure Active Directory 與彈性查詢進行驗證。</span><span class="sxs-lookup"><span data-stu-id="d0c7f-121">Authentication using Azure Active Directory with elastic queries is not currently supported.</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="d0c7f-122">外部資料來源</span><span class="sxs-lookup"><span data-stu-id="d0c7f-122">External data sources</span></span>
<span data-ttu-id="d0c7f-123">若要建立外部資料來源，請在 Orders 資料庫上執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="d0c7f-123">To create an external data source, execute the following command on the Orders database:</span></span> 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a><span data-ttu-id="d0c7f-124">外部資料表</span><span class="sxs-lookup"><span data-stu-id="d0c7f-124">External tables</span></span>
<span data-ttu-id="d0c7f-125">在符合 CustomerInformation 資料表定義的 Orders 資料庫上，建立外部資料表：</span><span class="sxs-lookup"><span data-stu-id="d0c7f-125">Create an external table on the Orders database, which matches the definition of the CustomerInformation table:</span></span>

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="d0c7f-126">執行範例彈性資料庫 T-SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="d0c7f-126">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="d0c7f-127">一旦您已定義外部資料來源和外部資料表，您現在即可使用 T-SQL 來查詢外部資料表。</span><span class="sxs-lookup"><span data-stu-id="d0c7f-127">Once you have defined your external data source and your external tables you can now use T-SQL to query your external tables.</span></span> <span data-ttu-id="d0c7f-128">在 Orders 資料庫上執行此查詢：</span><span class="sxs-lookup"><span data-stu-id="d0c7f-128">Execute this query on the Orders database:</span></span> 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a><span data-ttu-id="d0c7f-129">成本</span><span class="sxs-lookup"><span data-stu-id="d0c7f-129">Cost</span></span>
<span data-ttu-id="d0c7f-130">目前，彈性資料庫查詢功能算在 Azure SQL Database 的成本內。</span><span class="sxs-lookup"><span data-stu-id="d0c7f-130">Currently, the elastic database query feature is included into the cost of your Azure SQL Database.</span></span>  

<span data-ttu-id="d0c7f-131">如需價格資訊，請參閱 [SQL Database 價格](https://azure.microsoft.com/pricing/details/sql-database)。</span><span class="sxs-lookup"><span data-stu-id="d0c7f-131">For pricing information see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d0c7f-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d0c7f-132">Next steps</span></span>

* <span data-ttu-id="d0c7f-133">如需彈性查詢的概觀，請參閱[彈性查詢概觀](sql-database-elastic-query-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d0c7f-133">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="d0c7f-134">如需垂直資料分割之資料的語法和範例查詢，請參閱[查詢垂直資料分割的資料](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="d0c7f-134">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="d0c7f-135">如需水平資料分割 (分區化) 教學課程，請參閱[開始使用彈性查詢進行水平資料分割 (分區化)](sql-database-elastic-query-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="d0c7f-135">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="d0c7f-136">如需水平資料分割之資料的語法和範例查詢，請參閱[查詢水平資料分割的資料](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="d0c7f-136">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="d0c7f-137">如需會在單一遠端 Azure SQL Database 或一組在水平資料分割配置中作為分區之資料庫上執行 Transact-SQL 陳述式的預存程序，請參閱 [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714)。</span><span class="sxs-lookup"><span data-stu-id="d0c7f-137">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>