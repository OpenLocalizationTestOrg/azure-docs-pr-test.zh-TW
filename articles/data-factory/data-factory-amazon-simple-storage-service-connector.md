---
title: "使用 Data Factory 的 aaaMove 資料從 Amazon 簡單的儲存體服務 |Microsoft 文件"
description: "深入了解如何使用 Azure Data Factory 的 toomove 資料從 Amazon 簡單儲存體服務 (S3)。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a>使用 Azure Data Factory 從 Amazon Simple Storage Service 移動資料
本文說明如何 toouse hello 複製在 Azure Data Factory toomove 資料從 Amazon 簡單儲存體服務 (S3) 活動。 它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。

您可以從 Amazon S3 tooany 支援接收資料存放區複製資料。 取得一份資料存放區支援接收由 hello 複製活動時，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。 Data Factory 目前支援從 Amazon S3 tooother 資料存放區的唯一移動資料，但不是將資料從其他資料會儲存 tooAmazon S3。

## <a name="required-permissions"></a>所需的權限
toocopy 資料從 Amazon S3，請確定您已獲得下列權限的 hello:

* 適用於 Amazon S3 物件作業的 `s3:GetObject` 和 `s3:GetObjectVersion`。
* 適用於 Amazon S3 貯體作業的 `s3:ListBucket`。 如果您使用 Data Factory 複製精靈中，hello`s3:ListAllMyBuckets`也是必要欄位。

如需 hello 的 Amazon S3 權限的完整清單的詳細資訊，請參閱[原則中指定的權限](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html)。

## <a name="getting-started"></a>開始使用
您可以藉由使用不同的工具或 API，建立內含複製活動的管線，以從 Amazon S3 來源移動資料。

最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。 如需快速逐步解說，請參閱[教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md)。

您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 如需逐步指示 toocreate 具有複製活動的管線，請參閱 hello[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。

無論您是使用工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:

1. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。
2. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。
3. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用工具或 Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。 使用 Data Factory 實體的 Amazon S3 資料存放區中的使用的 toocopy 資料的 JSON 定義中的範例，請參閱 hello [JSON 範例： 將資料從 Amazon S3 tooAzure Blob 複製](#json-example-copy-data-from-amazon-s3-to-azure-blob)本文一節。

> [!NOTE]
> 如需有關針對複製活動支援的檔案和壓縮格式的詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)。

hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooAmazon S3 的 JSON 屬性的詳細資料。

## <a name="linked-service-properties"></a>連結服務屬性
連結的服務連結資料儲存區 tooa data factory。 您建立連結的服務型別的**AwsAccessKey** toolink Amazon S3 資料儲存 tooyour 資料 factory。 下表中的 hello 提供描述的 JSON 元素特定 tooAmazon S3 (AwsAccessKey) 連結服務。

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| accessKeyID |Hello 密碼的存取金鑰的識別碼。 |字串 |是 |
| secretAccessKey |hello 密碼存取金鑰本身。 |加密的密碼字串 |是 |

下列是一個範例：

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a>資料集屬性
資料集 toorepresent toospecify 輸入 Azure Blob 儲存體，hello 類型的屬性設定 hello 資料集的資料太**AmazonS3**。 設定 hello **linkedServiceName**連結服務的 hello Amazon S3 hello 資料集 toohello 名稱的內容。 如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)。 

所有資料集類型 (例如 SQL 資料庫、Azure Blob 及 Azure 資料表) 的結構、可用性及原則等區段都相似。 hello **typeProperties**章節是不同的每種類型的資料集，並提供 hello hello 資料存放區中的 hello 資料位置的相關資訊。 hello **typeProperties**類型的資料集區段**AmazonS3** （包括 hello Amazon S3 資料集） 具有下列屬性的 hello:

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| bucketName |hello S3 值區的名稱。 |String |是 |
| key |hello S3 物件索引鍵。 |String |否 |
| prefix |Hello S3 物件索引鍵的前置詞。 系統會選取索引鍵以此前置詞開頭的物件。 只有當索引鍵空白時才適用。 |string |否 |
| 版本 |hello 的 hello S3 物件，如果已啟用 S3 版本控制的版本。 |String |否 |
| format | 支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。 設定 hello**類型**下格式 tooone 這些值的屬性。 如需詳細資訊，請參閱 hello[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)， [JSON 格式](data-factory-supported-file-and-compression-formats.md#json-format)， [Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)， [Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)，和[Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)區段。 <br><br> 如果您想要為 toocopy 檔案-之間以檔案為基礎存放區 （二進位複製），略過 hello 格式 > 一節中這兩個輸入和輸出資料集定義。 |否 | |
| compression | 指定 hello 類型和層級的 hello 資料壓縮。 hello 支援型別： **GZip**， **Deflate**， **BZip2**，和**ZipDeflate**。 hello 支援層級為：**最佳**和**最快**。 如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。 |否 | |


> [!NOTE]
> **bucketName + 鍵**指定 hello hello S3 物件，其中值區是 hello S3 物件的根容器，而索引鍵是 hello 完整路徑 toohello S3 物件位置。

### <a name="sample-dataset-with-prefix"></a>prefix 的相關範例資料集

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a>範例資料集 (含版本)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a>S3 的動態路徑
hello 上述範例會使用固定的值為 hello**金鑰**和**bucketName** hello Amazon S3 資料集中的屬性。

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

您可以藉由使用系統變數 (例如 SliceStart)，讓 Data Factory 在執行階段動態地計算這些屬性。

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

您可以相同 hello hello**前置詞**Amazon S3 資料集的屬性。 如需支援的函式和變數清單，請參閱 [Data Factory 函式與系統變數](data-factory-functions-variables.md)。

## <a name="copy-activity-properties"></a>複製活動屬性
如需可用來定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)。 屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。 屬性用於 hello **typeProperties** hello 活動的區段會隨每個活動類型。 Hello 複製活動，根據 hello 類型的來源與接收屬性而有所不同。 Hello 複製活動中的來源時的型別**FileSystemSource** （包括 Amazon S3），下列屬性的 hello 位於**typeProperties** > 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| 遞迴 |指定是否 toorecursively 清單 S3 物件 hello 目錄下。 |true/false |否 |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a>JSON 範例： 從 Amazon S3 tooAzure Blob 儲存體複製資料
這個範例示範如何從 Azure Blob 儲存體的 Amazon S3 tooan toocopy 資料。 不過，資料可以複製直接太[任何支援的 hello 接收](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 Data Factory 中的 hello 複製活動。

hello 範例提供下列 Data Factory 實體的 hello 的 JSON 定義。 您可以使用這些定義 toocreate 管線 toocopy 資料從 Amazon S3 tooBlob 儲存體，使用 hello [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)， [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)，或[PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。   

* [AwsAccessKey](#linked-service-properties)類型的連結服務。
* [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
* [AmazonS3](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
* [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
* 具有使用 [FileSystemSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

hello 範例將資料從 Azure blob 的 Amazon S3 tooan 每小時。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

### <a name="amazon-s3-linked-service"></a>Amazon S3 已連結的服務

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a>Azure 儲存體連結服務

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

### <a name="amazon-s3-input-dataset"></a>Amazon S3 輸入資料集

設定**"external": true**通知 hello Data Factory 服務該 hello 資料集是外部 toohello 資料處理站。 設定此屬性 tootrue 上就不會產生 hello 管線中活動的輸入資料集。

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a>Azure Blob 輸出資料集

資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。 hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 hello 資料夾路徑會使用 hello 的 hello 開始時間的年、 月、 日和小時部分。

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a>具有 Amazon S3 來源和 Blob 接收器的管線中複製活動

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**FileSystemSource**，和**接收**類型設定得**BlobSink**。

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
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
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> 請參閱 < 從接收的資料集、 來源資料集 toocolumns toomap 資料行[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。


## <a name="next-steps"></a>後續步驟
請參閱下列文章 hello:

* 關於金鑰 toolearn 因素影響效能的 Data Factory 中的資料移動 （複製活動） 和各種方式 toooptimize 的請參閱 hello[複製活動效能及微調指南](data-factory-copy-activity-performance.md)。

* 複製活動與建立管線的逐步指示，請參閱 hello[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。
