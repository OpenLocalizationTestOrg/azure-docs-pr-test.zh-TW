---
title: "aaaMapping Azure Data Factory 中的資料集資料行 |Microsoft 文件"
description: "了解如何 toomap 來源資料行 toodestination 資料行。"
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
ms.openlocfilehash: 8f78d4af675bec0a70e5f6e83ec1ffb511408b5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="map-source-dataset-columns-toodestination-dataset-columns"></a><span data-ttu-id="087dc-103">將來源資料集資料行 toodestination 資料集資料行對應</span><span class="sxs-lookup"><span data-stu-id="087dc-103">Map source dataset columns toodestination dataset columns</span></span>
<span data-ttu-id="087dc-104">資料行對應可以使用的 toospecify hello 「 結構 」 的來源資料表對應 toocolumns 中指定資料行如何在 hello 「 結構 」 的接收資料表中指定。</span><span class="sxs-lookup"><span data-stu-id="087dc-104">Column mapping can be used toospecify how columns specified in hello “structure” of source table map toocolumns specified in hello “structure” of sink table.</span></span> <span data-ttu-id="087dc-105">hello **columnMapping**屬性位於 hello **typeProperties** hello 複製活動的區段。</span><span class="sxs-lookup"><span data-stu-id="087dc-105">hello **columnMapping** property is available in hello **typeProperties** section of hello Copy activity.</span></span>

<span data-ttu-id="087dc-106">資料行對應支援下列案例的 hello:</span><span class="sxs-lookup"><span data-stu-id="087dc-106">Column mapping supports hello following scenarios:</span></span>

* <span data-ttu-id="087dc-107">Hello 來源資料集結構中的所有資料行都對應的 tooall hello 接收資料集結構中的資料行。</span><span class="sxs-lookup"><span data-stu-id="087dc-107">All columns in hello source dataset structure are mapped tooall columns in hello sink dataset structure.</span></span>
* <span data-ttu-id="087dc-108">Hello hello 來源資料集結構中的資料行的子集是對應的 tooall hello 接收資料集結構中的資料行。</span><span class="sxs-lookup"><span data-stu-id="087dc-108">A subset of hello columns in hello source dataset structure is mapped tooall columns in hello sink dataset structure.</span></span>

<span data-ttu-id="087dc-109">hello 下面是錯誤條件會造成例外狀況：</span><span class="sxs-lookup"><span data-stu-id="087dc-109">hello following are error conditions that result in an exception:</span></span>

* <span data-ttu-id="087dc-110">較少的資料行或中 hello 「 結構 」 的接收資料表比 hello 對應中指定的資料行。</span><span class="sxs-lookup"><span data-stu-id="087dc-110">Either fewer columns or more columns in hello “structure” of sink table than specified in hello mapping.</span></span>
* <span data-ttu-id="087dc-111">重複的對應。</span><span class="sxs-lookup"><span data-stu-id="087dc-111">Duplicate mapping.</span></span>
* <span data-ttu-id="087dc-112">SQL 查詢結果並沒有指定 hello 對應中的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="087dc-112">SQL query result does not have a column name that is specified in hello mapping.</span></span>

> [!NOTE]
> <span data-ttu-id="087dc-113">hello 下列範例是針對 SQL Azure 和 Azure Blob 但支援矩形的資料集的適用 tooany 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="087dc-113">hello following samples are for Azure SQL and Azure Blob but are applicable tooany data store that supports rectangular datasets.</span></span> <span data-ttu-id="087dc-114">調整資料集和範例 toopoint toodata hello 相關的資料來源中的連結的服務定義。</span><span class="sxs-lookup"><span data-stu-id="087dc-114">Adjust dataset and linked service definitions in examples toopoint toodata in hello relevant data source.</span></span>

## <a name="sample-1--column-mapping-from-azure-sql-tooazure-blob"></a><span data-ttu-id="087dc-115">範例 1 – 資料行對應從 Azure SQL tooAzure blob</span><span class="sxs-lookup"><span data-stu-id="087dc-115">Sample 1 – column mapping from Azure SQL tooAzure blob</span></span>
<span data-ttu-id="087dc-116">在此範例中，hello 輸入的資料表的結構和它所指 tooa SQL 資料表中 Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="087dc-116">In this sample, hello input table has a structure and it points tooa SQL table in an Azure SQL database.</span></span>

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

<span data-ttu-id="087dc-117">在此範例中，hello 輸出資料表的結構和它所指 tooa blob 在 Azure blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="087dc-117">In this sample, hello output table has a structure and it points tooa blob in an Azure blob storage.</span></span>

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

<span data-ttu-id="087dc-118">下列 JSON hello 定義複製活動在管線中。</span><span class="sxs-lookup"><span data-stu-id="087dc-118">hello following JSON defines a copy activity in a pipeline.</span></span> <span data-ttu-id="087dc-119">hello 來源資料行對應中接收 toocolumns (**columnMappings**) 使用 hello**轉譯程式**屬性。</span><span class="sxs-lookup"><span data-stu-id="087dc-119">hello columns from source mapped toocolumns in sink (**columnMappings**) by using hello **Translator** property.</span></span>

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
<span data-ttu-id="087dc-120">**資料行對應流程：**</span><span class="sxs-lookup"><span data-stu-id="087dc-120">**Column mapping flow:**</span></span>

![資料行對應流程](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-tooazure-blob"></a><span data-ttu-id="087dc-122">範例 2 – 資料行對應 SQL 查詢從 Azure SQL tooAzure blob</span><span class="sxs-lookup"><span data-stu-id="087dc-122">Sample 2 – column mapping with SQL query from Azure SQL tooAzure blob</span></span>
<span data-ttu-id="087dc-123">在此範例中，SQL 查詢會是使用的 tooextract Azure SQL 資料，而不是只需指定 「 結構 」 一節中的 hello 資料表名稱和 hello 資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="087dc-123">In this sample, a SQL query is used tooextract data from Azure SQL instead of simply specifying hello table name and hello column names in “structure” section.</span></span> 

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
<span data-ttu-id="087dc-124">在此情況下，hello 查詢結果會在 「 結構 」 的來源中指定的第一個對應的 toocolumns。</span><span class="sxs-lookup"><span data-stu-id="087dc-124">In this case, hello query results are first mapped toocolumns specified in “structure” of source.</span></span> <span data-ttu-id="087dc-125">接下來，hello 來源 「 結構 」 的資料行的對應的 toocolumns 中接收 「 結構 」 在 columnMappings 中指定的規則。</span><span class="sxs-lookup"><span data-stu-id="087dc-125">Next, hello columns from source “structure” are mapped toocolumns in sink “structure” with rules specified in columnMappings.</span></span>  <span data-ttu-id="087dc-126">假設 hello 查詢會傳回 5 個資料行、 兩個資料行多於 hello 「 結構 」 的來源中所指定。</span><span class="sxs-lookup"><span data-stu-id="087dc-126">Suppose hello query returns 5 columns, two more columns than those specified in hello “structure” of source.</span></span>

<span data-ttu-id="087dc-127">**資料行對應流程**</span><span class="sxs-lookup"><span data-stu-id="087dc-127">**Column mapping flow**</span></span>

![資料行對應流程 -2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a><span data-ttu-id="087dc-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="087dc-129">Next steps</span></span>
<span data-ttu-id="087dc-130">如需使用複製活動的教學課程，請參閱 hello 文章：</span><span class="sxs-lookup"><span data-stu-id="087dc-130">See hello article for a tutorial on using Copy Activity:</span></span> 

- [<span data-ttu-id="087dc-131">從 Blob 儲存體 tooSQL 資料庫複製資料</span><span class="sxs-lookup"><span data-stu-id="087dc-131">Copy data from Blob Storage tooSQL Database</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
