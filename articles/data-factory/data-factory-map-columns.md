---
title: "在 Azure Data Factory 中對應資料集資料行 | Microsoft Docs"
description: "了解如何將來源資料行對應至目的地資料行。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: a50661b377cfbbff3f1f762342cb275d5da82cea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="map-source-dataset-columns-to-destination-dataset-columns"></a><span data-ttu-id="e15a8-103">將來源資料集資料行對應至目的地資料集資料行</span><span class="sxs-lookup"><span data-stu-id="e15a8-103">Map source dataset columns to destination dataset columns</span></span>
<span data-ttu-id="e15a8-104">資料行對應可用於指定將來源資料表「 結構 」中指定資料行對應至接收器資料表 「 結構 」 中指定資料行的方式。</span><span class="sxs-lookup"><span data-stu-id="e15a8-104">Column mapping can be used to specify how columns specified in the “structure” of source table map to columns specified in the “structure” of sink table.</span></span> <span data-ttu-id="e15a8-105">複製活動的 **typeProperties** 區段中可使用 **columnMapping** 屬性。</span><span class="sxs-lookup"><span data-stu-id="e15a8-105">The **columnMapping** property is available in the **typeProperties** section of the Copy activity.</span></span>

<span data-ttu-id="e15a8-106">資料行對應支援下列案例：</span><span class="sxs-lookup"><span data-stu-id="e15a8-106">Column mapping supports the following scenarios:</span></span>

* <span data-ttu-id="e15a8-107">來源資料集結構中的所有資料行對應至接收資料集結構中的所有資料行。</span><span class="sxs-lookup"><span data-stu-id="e15a8-107">All columns in the source dataset structure are mapped to all columns in the sink dataset structure.</span></span>
* <span data-ttu-id="e15a8-108">來源資料集結構中的資料行子集對應至接收資料集結構中的所有資料行。</span><span class="sxs-lookup"><span data-stu-id="e15a8-108">A subset of the columns in the source dataset structure is mapped to all columns in the sink dataset structure.</span></span>

<span data-ttu-id="e15a8-109">以下是會導致發生例外狀況的錯誤狀況：</span><span class="sxs-lookup"><span data-stu-id="e15a8-109">The following are error conditions that result in an exception:</span></span>

* <span data-ttu-id="e15a8-110">接收器資料表「結構」中的資料行數量多於或少於對應中所指定的數量。</span><span class="sxs-lookup"><span data-stu-id="e15a8-110">Either fewer columns or more columns in the “structure” of sink table than specified in the mapping.</span></span>
* <span data-ttu-id="e15a8-111">重複的對應。</span><span class="sxs-lookup"><span data-stu-id="e15a8-111">Duplicate mapping.</span></span>
* <span data-ttu-id="e15a8-112">SQL 查詢結果中沒有對應中所指定的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="e15a8-112">SQL query result does not have a column name that is specified in the mapping.</span></span>

> [!NOTE]
> <span data-ttu-id="e15a8-113">下列範例是針對 Azure SQL 和 Azure Blob，但是也適用於任何支援矩形資料集的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="e15a8-113">The following samples are for Azure SQL and Azure Blob but are applicable to any data store that supports rectangular datasets.</span></span> <span data-ttu-id="e15a8-114">請調整範例中的資料集和已連結服務定義，以指向相關資料來源中的資料。</span><span class="sxs-lookup"><span data-stu-id="e15a8-114">Adjust dataset and linked service definitions in examples to point to data in the relevant data source.</span></span>

## <a name="sample-1--column-mapping-from-azure-sql-to-azure-blob"></a><span data-ttu-id="e15a8-115">範例 1 – 從 Azure SQL 到 Azure Blob 的資料行對應</span><span class="sxs-lookup"><span data-stu-id="e15a8-115">Sample 1 – column mapping from Azure SQL to Azure blob</span></span>
<span data-ttu-id="e15a8-116">在此範例中，輸入資料表有一個結構，且指向 Azure SQL 資料庫中的 SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="e15a8-116">In this sample, the input table has a structure and it points to a SQL table in an Azure SQL database.</span></span>

```json
{
    "name": "AzureSQLInput",
    "properties": {
        "structure": 
         [
           { "name": "userid"},
           { "name": "name"},
           { "name": "group"}
         ],
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="e15a8-117">在此範例中，輸出資料表有一個結構，且指向 Azure Blob 儲存體中的 Blob。</span><span class="sxs-lookup"><span data-stu-id="e15a8-117">In this sample, the output table has a structure and it points to a blob in an Azure blob storage.</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
         "structure": 
          [
                { "name": "myuserid"},
                { "name": "myname" },
                { "name": "mygroup"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="e15a8-118">下列 JSON 定義了管線中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="e15a8-118">The following JSON defines a copy activity in a pipeline.</span></span> <span data-ttu-id="e15a8-119">來自來源的資料行是使用 **Translator** 屬性來對應至接收器中的資料行 (**columnMappings**)。</span><span class="sxs-lookup"><span data-stu-id="e15a8-119">The columns from source mapped to columns in sink (**columnMappings**) by using the **Translator** property.</span></span>

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "Copy",
    "inputs":  [ { "name": "AzureSQLInput"  } ],
    "outputs":  [ { "name": "AzureBlobOutput" } ],
    "typeProperties":    {
        "source":
        {
            "type": "SqlSource"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup, Name: MyName"
        }
    },
   "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
<span data-ttu-id="e15a8-120">**資料行對應流程：**</span><span class="sxs-lookup"><span data-stu-id="e15a8-120">**Column mapping flow:**</span></span>

![資料行對應流程](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-to-azure-blob"></a><span data-ttu-id="e15a8-122">範例 2 – 利用 SQL 查詢從 Azure SQL 至 Azure Blob 的資料行對應</span><span class="sxs-lookup"><span data-stu-id="e15a8-122">Sample 2 – column mapping with SQL query from Azure SQL to Azure blob</span></span>
<span data-ttu-id="e15a8-123">在此範例中，使用 SQL 查詢從 Azure SQL 擷取資料，而非只在 「 結構 」 區段中指定資料表名稱和資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="e15a8-123">In this sample, a SQL query is used to extract data from Azure SQL instead of simply specifying the table name and the column names in “structure” section.</span></span> 

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "CopyActivity",
    "inputs":  [ { "name": " AzureSQLInput"  } ],
    "outputs":  [ { "name": " AzureBlobOutput" } ],
    "typeProperties":
    {
        "source":
        {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartDateTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "Translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup,Name: MyName"
        }
    },
    "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
<span data-ttu-id="e15a8-124">在此情況下，查詢結果會先對應至來源「 結構 」 中所指定的資料行。</span><span class="sxs-lookup"><span data-stu-id="e15a8-124">In this case, the query results are first mapped to columns specified in “structure” of source.</span></span> <span data-ttu-id="e15a8-125">接下來，來源 「 結構 」 中的資料行會使用 columnMappings 中指定的規則對應至接收器 「 結構 」 中的資料行。</span><span class="sxs-lookup"><span data-stu-id="e15a8-125">Next, the columns from source “structure” are mapped to columns in sink “structure” with rules specified in columnMappings.</span></span>  <span data-ttu-id="e15a8-126">假設該查詢傳回 5 個資料行，比來源的 “structure” 中所指定的多 2 個資料行。</span><span class="sxs-lookup"><span data-stu-id="e15a8-126">Suppose the query returns 5 columns, two more columns than those specified in the “structure” of source.</span></span>

<span data-ttu-id="e15a8-127">**資料行對應流程**</span><span class="sxs-lookup"><span data-stu-id="e15a8-127">**Column mapping flow**</span></span>

![資料行對應流程 -2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a><span data-ttu-id="e15a8-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e15a8-129">Next steps</span></span>
<span data-ttu-id="e15a8-130">請參閱有關使用「複製活動」的教學課程文章：</span><span class="sxs-lookup"><span data-stu-id="e15a8-130">See the article for a tutorial on using Copy Activity:</span></span> 

- [<span data-ttu-id="e15a8-131">將資料從 Blob 儲存體複製到 SQL Database</span><span class="sxs-lookup"><span data-stu-id="e15a8-131">Copy data from Blob Storage to SQL Database</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
