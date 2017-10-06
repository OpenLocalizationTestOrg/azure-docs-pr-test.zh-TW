---
title: "aaaInvoke 預存程序從 Azure 資料 Factory 複製活動 |Microsoft 文件"
description: "了解如何在 Azure SQL Database 或從 Azure Data Factory 的 SQL Server 中的預存程序 tooinvoke 複製活動。"
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
ms.openlocfilehash: 986377118afb8c08607c2325fcc3ab00b3de9268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a><span data-ttu-id="e4992-103">從 Azure Data Factory 中的複製活動叫用預存程序</span><span class="sxs-lookup"><span data-stu-id="e4992-103">Invoke stored procedure from copy activity in Azure Data Factory</span></span>
<span data-ttu-id="e4992-104">當將資料複製到[SQL Server](data-factory-sqlserver-connector.md)或[Azure SQL Database](data-factory-azure-sql-connector.md)，您可以設定 hello **SqlSink**在複製活動 tooinvoke 預存程序。</span><span class="sxs-lookup"><span data-stu-id="e4992-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure.</span></span> <span data-ttu-id="e4992-105">您可能想 toouse hello 預存程序 tooperform toohello 目的地資料表中插入資料之前，需要任何額外的處理 （合併資料行，查閱值，插入多個資料表等）。</span><span class="sxs-lookup"><span data-stu-id="e4992-105">You may want toouse hello stored procedure tooperform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in toohello destination table.</span></span> <span data-ttu-id="e4992-106">此功能會利用[資料表值參數](https://msdn.microsoft.com/library/bb675163.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e4992-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span> 

<span data-ttu-id="e4992-107">hello 下列範例顯示如何 tooinvoke 預存程序在 SQL Server 資料庫從 Data Factory 管線 （複製活動）：</span><span class="sxs-lookup"><span data-stu-id="e4992-107">hello following sample shows how tooinvoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span></span>  

## <a name="output-dataset-json"></a><span data-ttu-id="e4992-108">輸出資料集 JSON</span><span class="sxs-lookup"><span data-stu-id="e4992-108">Output dataset JSON</span></span>
<span data-ttu-id="e4992-109">在 hello 輸出資料集 JSON，設定 hello**類型**至： **SqlServerTable**。</span><span class="sxs-lookup"><span data-stu-id="e4992-109">In hello output dataset JSON, set hello **type** to: **SqlServerTable**.</span></span> <span data-ttu-id="e4992-110">設定得**AzureSqlTable** toouse 與 Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="e4992-110">Set it too**AzureSqlTable** toouse with an Azure SQL database.</span></span> <span data-ttu-id="e4992-111">hello 值**tableName**屬性必須符合 hello hello 預存程序之第一個參數的名稱。</span><span class="sxs-lookup"><span data-stu-id="e4992-111">hello value for **tableName** property must match hello name of first parameter of hello stored procedure.</span></span>  

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

## <a name="sqlsink-section-in-copy-activity-json"></a><span data-ttu-id="e4992-112">複製活動 JSON 中的 SqlSink 區段</span><span class="sxs-lookup"><span data-stu-id="e4992-112">SqlSink section in copy activity JSON</span></span>
<span data-ttu-id="e4992-113">定義 hello **SqlSink**區段 hello 複製活動 JSON 中，如下所示。</span><span class="sxs-lookup"><span data-stu-id="e4992-113">Define hello **SqlSink** section in hello copy activity JSON as follows.</span></span> <span data-ttu-id="e4992-114">tooinvoke 預存程序時將資料插入 hello 接收/目的地資料庫，指定兩個值**SqlWriterStoredProcedureName**和**SqlWriterTableType**屬性。</span><span class="sxs-lookup"><span data-stu-id="e4992-114">tooinvoke a stored procedure while inserting data into hello sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span></span> <span data-ttu-id="e4992-115">如需這些屬性的描述，請參閱[SqlSink hello SQL Server 連接器文件中的區段](data-factory-sqlserver-connector.md#sqlsink)。</span><span class="sxs-lookup"><span data-stu-id="e4992-115">For descriptions of these properties, see [SqlSink section in hello SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span></span>

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

## <a name="stored-procedure-definition"></a><span data-ttu-id="e4992-116">預存程序定義</span><span class="sxs-lookup"><span data-stu-id="e4992-116">Stored procedure definition</span></span> 
<span data-ttu-id="e4992-117">在資料庫中，定義 hello 預存程序，以做為名稱相同的 hello **SqlWriterStoredProcedureName**。</span><span class="sxs-lookup"><span data-stu-id="e4992-117">In your database, define hello stored procedure with hello same name as **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="e4992-118">hello 預存程序會處理從 hello 來源資料存放區輸入的資料，並將資料插入 hello 目的地資料庫中的資料表。</span><span class="sxs-lookup"><span data-stu-id="e4992-118">hello stored procedure handles input data from hello source data store, and inserts data into a table in hello destination database.</span></span> <span data-ttu-id="e4992-119">hello hello 預存程序的第一個參數名稱必須符合 hello tableName hello 資料集 JSON （行銷） 中定義。</span><span class="sxs-lookup"><span data-stu-id="e4992-119">hello name of hello first parameter of stored procedure must match hello tableName defined in hello dataset JSON (Marketing).</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a><span data-ttu-id="e4992-120">資料表類型定義</span><span class="sxs-lookup"><span data-stu-id="e4992-120">Table type definition</span></span>
<span data-ttu-id="e4992-121">在資料庫中，定義 hello 資料表類型，以做為名稱相同的 hello **SqlWriterTableType**。</span><span class="sxs-lookup"><span data-stu-id="e4992-121">In your database, define hello table type with hello same name as **SqlWriterTableType**.</span></span> <span data-ttu-id="e4992-122">hello hello 資料表類型的結構描述必須符合 hello 的 hello 輸入資料集的結構描述。</span><span class="sxs-lookup"><span data-stu-id="e4992-122">hello schema of hello table type must match hello schema of hello input dataset.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a><span data-ttu-id="e4992-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e4992-123">Next steps</span></span>
<span data-ttu-id="e4992-124">檢閱下列連接器的 hello 文件，如需完整的 JSON 範例：</span><span class="sxs-lookup"><span data-stu-id="e4992-124">Review hello following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="e4992-125">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e4992-125">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="e4992-126">SQL Server</span><span class="sxs-lookup"><span data-stu-id="e4992-126">SQL Server</span></span>](data-factory-sqlserver-connector.md)
