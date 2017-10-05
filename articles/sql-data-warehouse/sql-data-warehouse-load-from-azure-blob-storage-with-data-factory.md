---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: "從 Azure blob 儲存體將資料載入 Azure SQL 資料倉儲 (Azure Data Factory) | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 載入資料"
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 689fb02e-eb98-4f7c-81e6-6c1d22d53901
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: barbkess
ms.custom: loading
ms.openlocfilehash: ca8bdfc21582253e8709a33eb624547fed4461d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-azure-blob-storage-into-azure-sql-data-warehouse-azure-data-factory"></a>從 Azure blob 儲存體將資料載入 Azure SQL 資料倉儲 (Azure Data Factory)
> [!div class="op_single_selector"]
> * [Data Factory](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [PolyBase](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

 本教學課程說明如何在 Azure Data Factory 中建立管線，將資料從 Azure 儲存體 Blob 移至 SQL 資料倉儲。 使用下列步驟，您將：

* 在 Azure 儲存體 Blob 中設定範例資料。
* 將資源連接到 Azure Data Factory。
* 建立管線來將資料從儲存體 Blob 移至 SQL 資料倉儲。

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a>開始之前
若要熟悉 Azure Data Factory，請參閱 [Azure Data Factory 簡介][Introduction to Azure Data Factory]。

### <a name="create-or-identify-resources"></a>建立或識別資源
開始進行本教學課程之前，您需要有下列資源。

* **Azure 儲存體 Blob**：本教學課程使用 Azure 儲存體 Blob 做為 Azure Data Factory 管線的資料來源，因此您需要有此資源來儲存範例資料。 如果您沒有此資源，請了解如何[建立儲存體帳戶][Create a storage account]。
* **SQL 資料倉儲**：本教學課程會將資料從 Azure 儲存體 Blob 移至 SQL 資料倉儲，因此需要有線上的資料倉儲且已載入 AdventureWorksDW 範例資料。 如果您還沒有資料倉儲，請了解如何[佈建資料倉儲][Create a SQL Data Warehouse]。 如果您有資料倉儲，但尚未佈建範例資料，您可以[手動載入範例資料][Load sample data into SQL Data Warehouse]。
* **Azure Data Factory**：Azure Data Factory 將會完成實際載入，因此您需要有此資源來建置資料移動管線。如果您還沒有此資源，請從[開始使用 Azure Data Factory (Data Factory 編輯器)][Get started with Azure Data Factory (Data Factory Editor)] 的步驟 1 了解如何建立此資源。
* **AZCopy**：您需要有 AZCopy 將本機用戶端的範例資料複製到您的 Azure 儲存體 Blob。 如需安裝指示，請參閱 [AZCopy 文件][AZCopy documentation]。

## <a name="step-1-copy-sample-data-to-azure-storage-blob"></a>步驟 1：將範例資料複製到 Azure 儲存體 Blob
一切就緒時，您就可以開始將範例資料複製到您的 Azure 儲存體 Blob。

1. [下載範例資料][Download sample data]。 這項資料會將另外三年份的銷售資料加入至 AdventureWorksDW 範例資料。
2. 使用此 AZCopy 命令，將三年份的資料複製到您的 Azure 儲存體 Blob。

````
AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
````


## <a name="step-2-connect-resources-to-azure-data-factory"></a>步驟 2：將資源連接到 Azure Data Factory
既然已備妥資料，我們可以開始建立 Azure Data Factory 管線，將資料從 Azure Blob 儲存體移至 SQL 資料倉儲。

首先，請開啟 [Azure 入口網站][Azure portal]，從左側功能表中選取您的 Data Factory。

### <a name="step-21-create-linked-service"></a>步驟 2.1：建立連結服務
將您的 Azure 儲存體帳戶和 SQL 資料倉儲連結到您的 Data Factory。  

1. 首先，按一下 Data Factory 的 [連結服務] 區段來開始註冊程序，然後按一下 [新資料存放區]。 選擇要用來註冊 Azure 儲存體的名稱、選取 Azure 儲存體做為類型，然後輸入您的帳戶名稱和帳戶金鑰。
2. 若要註冊 SQL 資料倉儲，請瀏覽至 [編寫及部署] 區段，選取 [新資料存放區]，然後選取 [Azure SQL 資料倉儲]。 複製並貼上此範本，然後填入您的特定資訊。

```JSON
{
    "name": "<Linked Service Name>",
    "properties": {
        "description": "",
        "type": "AzureSqlDW",
        "typeProperties": {
             "connectionString": "Data Source=tcp:<server name>.database.windows.net,1433;Initial Catalog=<server name>;Integrated Security=False;User ID=<user>@<servername>;Password=<password>;Connect Timeout=30;Encrypt=True"
         }
    }
}
```

### <a name="step-22-define-the-dataset"></a>步驟 2.2：定義資料集
建立連結服務之後，我們必須定義資料集。  在這裡，此舉表示將定義要從儲存體移至資料倉儲的資料結構。  您可以閱讀如何建立的相關資訊。

1. 若要開始此程序，請瀏覽至 Data Factory 的 [作者與部署] 區段。
2. 依序按一下 [新增資料集] 和 [Azure Blob 儲存體]，以將儲存體連結至 Data Factory。  您可以使用以下指令碼，在 Azure Blob 儲存體中定義您的資料：

```JSON
{
    "name": "<Dataset Name>",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "<linked storage name>",
        "typeProperties": {
            "folderPath": "<containter name>",
            "fileName": "FactInternetSales.csv",
            "format": {
            "type": "TextFormat",
            "columnDelimiter": ",",
            "rowDelimiter": "\n"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
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


1. 現在，我們也會對 SQL 資料倉儲定義我們的資料集。  我們以相同方式開始，即依序按一下 [新增資料集] 和 [Azure SQL 資料倉儲]。

```JSON
{
    "name": "DWDataset",
    "properties": {
        "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "FactInternetSales"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

## <a name="step-3-create-and-run-your-pipeline"></a>步驟 3：建立和執行管線
最後，我們將在 Azure Data Factory 中安裝並執行管線。  這是將完成實際資料移動的作業。  您可以在[這裡][Move data to and from Azure SQL Data Warehouse using Azure Data Factory]完整檢視使用 SQL 資料倉儲和 Azure Data Factory 可以完成的作業。

現在。在 [作者與部署] 區段中。依序按一下 [其他命令] 和 [新增管線]。  建立管線之後，您可以使用以下程式碼，將資料傳送到資料倉儲：

```JSON
{
    "name": "<Pipeline Name>",
    "properties": {
        "description": "<Description>",
        "activities": [
          {
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "skipHeaderLineCount": 1
                },
                "sink": {
                    "type": "SqlDWSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:10"
                }
            },
            "inputs": [
              {
                "name": "<Storage Dataset>"
              }
            ],
            "outputs": [
              {
                "name": "<Data Warehouse Dataset>"
              }
            ],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Sample Copy",
            "description": "Copy Activity"
          }
        ],
        "start": "<Date YYYY-MM-DD>",
        "end": "<Date YYYY-MM-DD>",
        "isPaused": false
    }
}
```

## <a name="next-steps"></a>後續步驟
若要深入了解，首先請檢視：

* [Azure Data Factory 的學習路徑][Azure Data Factory learning path]。
* [Azure SQL 資料倉儲連接器][Azure SQL Data Warehouse Connector]。 這是搭配使用 Azure Data Factory 與 Azure SQL 資料倉儲的核心參考主題。

這些主題提供 Azure Data Factory 的詳細資訊。 其中討論 Azure SQL Database 或 HDinsight，但資訊也適用於 Azure SQL 資料倉儲。

* [教學課程：開始使用 Azure Data Factory][Tutorial: Get started with Azure Data Factory] 這是使用 Azure Data Factory 處理資料的核心教學課程。 在本教學課程中，您將建置第一個管線，在每個月使用 HDInsight 來轉換及分析 Web 記錄檔。 請注意，本教學課程中沒有複製的活動。
* [教學課程：將資料從 Azure 儲存體 Blob 複製到 Azure SQL Database][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database]。 在本教學課程中，您將在 Azure Data Factory 中建立管線，將資料從 Azure 儲存體 Blob 複製到 Azure SQL Database。

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction to Azure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data to and from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
