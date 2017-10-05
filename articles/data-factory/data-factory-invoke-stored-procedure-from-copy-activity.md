---
title: "從 Azure Data Factory 複製活動叫用預存程序 | Microsoft Docs"
description: "了解如何從 Azure Data Factory 複製活動叫用 Azure SQL Database 或 SQL Server 中的預存程序。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: af6e4a57e726598c266ee766656aa2cc22e374e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a><span data-ttu-id="39209-103">從 Azure Data Factory 中的複製活動叫用預存程序</span><span class="sxs-lookup"><span data-stu-id="39209-103">Invoke stored procedure from copy activity in Azure Data Factory</span></span>
<span data-ttu-id="39209-104">將資料複製到 [SQL Server](data-factory-sqlserver-connector.md) 或 [Azure SQL Database](data-factory-azure-sql-connector.md) 時，您可以在複製活動中設定 **SqlSink** 以叫用預存程序。</span><span class="sxs-lookup"><span data-stu-id="39209-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure the **SqlSink** in copy activity to invoke a stored procedure.</span></span> <span data-ttu-id="39209-105">您可以使用預存程序來執行將資料插入到目的地資料表之前所需的任何額外處理 (合併資料行、查詢值、插入到多個資料表等)。</span><span class="sxs-lookup"><span data-stu-id="39209-105">You may want to use the stored procedure to perform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in to the destination table.</span></span> <span data-ttu-id="39209-106">此功能會利用[資料表值參數](https://msdn.microsoft.com/library/bb675163.aspx)。</span><span class="sxs-lookup"><span data-stu-id="39209-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span> 

<span data-ttu-id="39209-107">下列範例示範如何從 Data Factory 管線 (複製活動) 叫用 SQL Server 資料庫中的預存程序：</span><span class="sxs-lookup"><span data-stu-id="39209-107">The following sample shows how to invoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span></span>  

## <a name="output-dataset-json"></a><span data-ttu-id="39209-108">輸出資料集 JSON</span><span class="sxs-lookup"><span data-stu-id="39209-108">Output dataset JSON</span></span>
<span data-ttu-id="39209-109">在輸出資料集 JSON 中，將 **type** 設定為：**SqlServerTable**。</span><span class="sxs-lookup"><span data-stu-id="39209-109">In the output dataset JSON, set the **type** to: **SqlServerTable**.</span></span> <span data-ttu-id="39209-110">請將它設定為 **AzureSqlTable**，以與 Azure SQL Database 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="39209-110">Set it to **AzureSqlTable** to use with an Azure SQL database.</span></span> <span data-ttu-id="39209-111">**tableName** 屬性的值必須與預存程序第一個參數的名稱相符。</span><span class="sxs-lookup"><span data-stu-id="39209-111">The value for **tableName** property must match the name of first parameter of the stored procedure.</span></span>  

```json
{
  "name": "SqlOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlLinkedService",
    "typeProperties": {
      "tableName": "Marketing"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

## <a name="sqlsink-section-in-copy-activity-json"></a><span data-ttu-id="39209-112">複製活動 JSON 中的 SqlSink 區段</span><span class="sxs-lookup"><span data-stu-id="39209-112">SqlSink section in copy activity JSON</span></span>
<span data-ttu-id="39209-113">依下列方式，在複製活動 JSON 中定義 **SqlSink** 區段。</span><span class="sxs-lookup"><span data-stu-id="39209-113">Define the **SqlSink** section in the copy activity JSON as follows.</span></span> <span data-ttu-id="39209-114">若要在將資料插入到接收/目的地資料庫時叫用預存程序，請同時指定 **SqlWriterStoredProcedureName** 和 **SqlWriterTableType** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="39209-114">To invoke a stored procedure while inserting data into the sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span></span> <span data-ttu-id="39209-115">如需這些屬性的描述，請參閱 [SQL Server 連接器一文中的 SqlSink 一節](data-factory-sqlserver-connector.md#sqlsink)。</span><span class="sxs-lookup"><span data-stu-id="39209-115">For descriptions of these properties, see [SqlSink section in the SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span></span>

```json
"sink":
{
    "type": "SqlSink",
    "SqlWriterTableType": "MarketingType",
    "SqlWriterStoredProcedureName": "spOverwriteMarketing", 
    "storedProcedureParameters":
            {
                "stringData": 
                {
                    "value": "str1"     
                }
            }
}
```

## <a name="stored-procedure-definition"></a><span data-ttu-id="39209-116">預存程序定義</span><span class="sxs-lookup"><span data-stu-id="39209-116">Stored procedure definition</span></span> 
<span data-ttu-id="39209-117">在資料庫中，使用與 **SqlWriterStoredProcedureName** 相同的名稱來定義預存程序。</span><span class="sxs-lookup"><span data-stu-id="39209-117">In your database, define the stored procedure with the same name as **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="39209-118">預存程序會處理來自來源資料存放區的輸入資料，然後將資料插入到目的地資料庫的資料表中。</span><span class="sxs-lookup"><span data-stu-id="39209-118">The stored procedure handles input data from the source data store, and inserts data into a table in the destination database.</span></span> <span data-ttu-id="39209-119">預存程序第一個參數的名稱必須與資料集 JSON 中定義的 tableName (Marketing) 相符。</span><span class="sxs-lookup"><span data-stu-id="39209-119">The name of the first parameter of stored procedure must match the tableName defined in the dataset JSON (Marketing).</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a><span data-ttu-id="39209-120">資料表類型定義</span><span class="sxs-lookup"><span data-stu-id="39209-120">Table type definition</span></span>
<span data-ttu-id="39209-121">在資料庫中，使用與 **SqlWriterTableType** 相同的名稱來定義資料表類型。</span><span class="sxs-lookup"><span data-stu-id="39209-121">In your database, define the table type with the same name as **SqlWriterTableType**.</span></span> <span data-ttu-id="39209-122">資料表類型的結構描述必須與輸入資料集的結構描述相符。</span><span class="sxs-lookup"><span data-stu-id="39209-122">The schema of the table type must match the schema of the input dataset.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a><span data-ttu-id="39209-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="39209-123">Next steps</span></span>
<span data-ttu-id="39209-124">如需完整的 JSON 範例，請檢閱下列連接器文章：</span><span class="sxs-lookup"><span data-stu-id="39209-124">Review the following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="39209-125">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="39209-125">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="39209-126">SQL Server</span><span class="sxs-lookup"><span data-stu-id="39209-126">SQL Server</span></span>](data-factory-sqlserver-connector.md)
