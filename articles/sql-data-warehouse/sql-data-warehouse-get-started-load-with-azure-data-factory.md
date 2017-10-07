---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: "使用 Azure Data Factory aaaLoad 資料 |Microsoft 文件"
description: "了解使用 Azure Data Factory tooload 資料"
services: sql-data-warehouse
documentationcenter: NA
author: twounder
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: ac7ddaa7-a3a5-4e15-b3cf-c696d2d105df
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 10/31/2016
ms.author: mausher;barbkess
ms.custom: loading
ms.openlocfilehash: 4186bd88d14be33f90130a41e8df06ce1d7cbab2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-azure-data-factory"></a>使用 Azure Data Factory 載入資料
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)  
> 
> 

本教學課程示範如何 toocreate Azure Data Factory toomove 資料從 Azure 儲存體 Blob tooAzure SQL 資料倉儲中的管線。 以下列的步驟將會看到 hello:

* 在 Azure 儲存體 Blob 中設定範例資料。
* 連接資源 tooAzure Data Factory。
* 從儲存體 Blob tooSQL 資料倉儲中建立管線 toomove 資料。

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a>開始之前
toofamiliarize 自己與 Azure Data Factory，請參閱[簡介 tooAzure Data Factory][Introduction tooAzure Data Factory]。

### <a name="create-or-identify-resources"></a>建立或識別資源
開始之前本教學課程，您需要 toohave hello 下列資源：

* **Azure 儲存體 Blob**： 本教學課程使用 Azure 儲存體 Blob 做 hello 資料來源 hello Azure Data Factory 管線，並因此您需要 toohave 一個可用 toostore hello 範例資料。 如果您還沒有已經，了解如何太[建立儲存體帳戶][Create a storage account]。
* **SQL 資料倉儲**： 此教學課程移 hello 資料從 Azure 儲存體 Blob 太 SQL 資料倉儲，因此需要 toohave 的資料倉儲線上 hello AdventureWorksDW 範例資料會載入。 如果您已經沒有資料倉儲，了解如何太[佈建一個][Create a SQL Data Warehouse]。 如果您有資料倉儲，但未以佈建它 hello 範例資料，您可以[手動載入][Load sample data into SQL Data Warehouse]。
* **Azure Data Factory**: Azure Data Factory 完成 hello 實際負載，因此您需要 toohave 其中一個，您可以使用 toobuild hello 資料移動管線。 如果您還沒有已經，了解如何 toocreate 其中一個步驟 1 中的[開始使用 Azure Data Factory （Data Factory 編輯器）][Get started with Azure Data Factory (Data Factory Editor)]。
* **AZCopy**： 您需要從您的本機用戶端 tooyour Azure 儲存體 Blob 的 AZCopy toocopy hello 範例資料。 安裝指示，請參閱 hello [AZCopy 文件][AZCopy documentation]。

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a>步驟 1： 複製範例資料 tooAzure 儲存體 Blob
準備的所有 hello 片段之後，您就準備好 toocopy 範例資料 tooyour Azure 儲存體 Blob。

1. [下載範例資料][Download sample data]。 這項資料將加入另一個的三年的銷售資料 tooyour AdventureWorksDW 範例資料。
2. 使用此 AZCopy 命令 toocopy hello 三年的資料 tooyour Azure 儲存體 Blob。
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-tooazure-data-factory"></a>步驟 2： 連接資源 tooAzure Data Factory
現在已 hello 資料就地我們可以從 Azure blob 儲存體中建立 hello Azure Data Factory 管線 toomove hello 資料到 SQL 資料倉儲。

啟動 tooget，開啟 hello [Azure 入口網站][ Azure portal]從 hello 左側功能表中選取您的 data factory。

### <a name="step-21-create-linked-service"></a>步驟 2.1：建立連結服務
連結您的 Azure 儲存體帳戶和 SQL 資料倉儲 tooyour 資料 factory。  

1. 首先，您的 data factory hello '連結服務' 區段，即可開始 hello 註冊程序，然後按一下'新建資料存放區。' 選擇名稱 tooregister 下選取的 Azure 儲存體做為您的類型，您 azure 儲存體，然後輸入您的帳戶名稱和帳戶金鑰。
2. tooregister SQL 資料倉儲瀏覽 toohello '作者及部署' 區段，選取 新增資料存放區，' 然後 ' Azure SQL 資料倉儲 '。 複製並貼上此範本，然後填入您的特定資訊。
   
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

### <a name="step-22-define-hello-dataset"></a>步驟 2.2： 定義 hello 資料集
建立 hello 連結的服務之後，我們必須 toodefine hello 資料集。  以下這表示定義 hello 已從您的儲存體 tooyour 資料倉儲移 hello 資料結構。  您可以閱讀如何建立的相關資訊。

1. 開始此程序瀏覽的 data factory toohello 「 作者和部署 」 一節。
2. '新的資料集' 按一下，然後按一下Azure Blob 儲存體' toolink 您的儲存體 tooyour data factory。  您可以使用下列指令碼 toodefine hello 您的資料，在 Azure Blob 儲存體：
   
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
3. 現在，我們要對 SQL 資料倉儲定義我們的資料集。 我們一開始在 hello 同樣地，按一下 新的資料集' ' Azure SQL 資料倉儲 '。
   
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
最後，我們會設定並執行 Azure Data Factory 中的 hello 管線。  這是完成 hello 實際的資料移動的 hello 作業。  您可以找到您可完成 SQL 資料倉儲與 Azure Data Factory 的 hello 作業的完整檢視[這裡][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]。

在 hello '作者與部署' 區段中，按一下 '更命令' 然後 ' 新管線 '。  建立 hello 管線之後，您可以使用下列程式碼 tootransfer hello 資料 tooyour 資料倉儲的 hello:

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
藉由檢視詳細資訊，開始 toolearn:

* [Azure Data Factory 的學習路徑][Azure Data Factory learning path]。
* [Azure SQL 資料倉儲連接器][Azure SQL Data Warehouse Connector]。 這是適用於使用 Azure SQL 資料倉儲中的 Azure Data Factory 的 hello 核心參考主題。

這些主題提供 Azure Data Factory 的詳細資訊。 他們討論 Azure SQL Database 或 HDInsight，但 hello 資訊也適用於 tooAzure SQL 資料倉儲。

* [教學課程： 開始使用 Azure Data Factory] [ Tutorial: Get started with Azure Data Factory]這是 hello 核心教學課程來處理資料與 Azure Data Factory。 在本教學課程中，您會建置您使用 HDInsight tootransform 的第一個管線，並分析每月為基礎的網站記錄檔。 請注意，本教學課程中沒有複製的活動。
* [教學課程： 將資料從 Azure 儲存體 Blob tooAzure SQL Database 中複製][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]。 在本教學課程中，您可以建立在 Azure Data Factory toocopy 資料管線從 Azure 儲存體 Blob tooAzure SQL 資料庫。

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction tooAzure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
