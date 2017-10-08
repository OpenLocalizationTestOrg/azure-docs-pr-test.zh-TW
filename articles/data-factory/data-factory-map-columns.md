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
# <a name="map-source-dataset-columns-toodestination-dataset-columns"></a>將來源資料集資料行 toodestination 資料集資料行對應
資料行對應可以使用的 toospecify hello 「 結構 」 的來源資料表對應 toocolumns 中指定資料行如何在 hello 「 結構 」 的接收資料表中指定。 hello **columnMapping**屬性位於 hello **typeProperties** hello 複製活動的區段。

資料行對應支援下列案例的 hello:

* Hello 來源資料集結構中的所有資料行都對應的 tooall hello 接收資料集結構中的資料行。
* Hello hello 來源資料集結構中的資料行的子集是對應的 tooall hello 接收資料集結構中的資料行。

hello 下面是錯誤條件會造成例外狀況：

* 較少的資料行或中 hello 「 結構 」 的接收資料表比 hello 對應中指定的資料行。
* 重複的對應。
* SQL 查詢結果並沒有指定 hello 對應中的資料行名稱。

> [!NOTE]
> hello 下列範例是針對 SQL Azure 和 Azure Blob 但支援矩形的資料集的適用 tooany 資料存放區。 調整資料集和範例 toopoint toodata hello 相關的資料來源中的連結的服務定義。

## <a name="sample-1--column-mapping-from-azure-sql-tooazure-blob"></a>範例 1 – 資料行對應從 Azure SQL tooAzure blob
在此範例中，hello 輸入的資料表的結構和它所指 tooa SQL 資料表中 Azure SQL database。

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

在此範例中，hello 輸出資料表的結構和它所指 tooa blob 在 Azure blob 儲存體中。

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

下列 JSON hello 定義複製活動在管線中。 hello 來源資料行對應中接收 toocolumns (**columnMappings**) 使用 hello**轉譯程式**屬性。

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
**資料行對應流程：**

![資料行對應流程](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-tooazure-blob"></a>範例 2 – 資料行對應 SQL 查詢從 Azure SQL tooAzure blob
在此範例中，SQL 查詢會是使用的 tooextract Azure SQL 資料，而不是只需指定 「 結構 」 一節中的 hello 資料表名稱和 hello 資料行名稱。 

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
在此情況下，hello 查詢結果會在 「 結構 」 的來源中指定的第一個對應的 toocolumns。 接下來，hello 來源 「 結構 」 的資料行的對應的 toocolumns 中接收 「 結構 」 在 columnMappings 中指定的規則。  假設 hello 查詢會傳回 5 個資料行、 兩個資料行多於 hello 「 結構 」 的來源中所指定。

**資料行對應流程**

![資料行對應流程 -2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a>後續步驟
如需使用複製活動的教學課程，請參閱 hello 文章： 

- [從 Blob 儲存體 tooSQL 資料庫複製資料](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
