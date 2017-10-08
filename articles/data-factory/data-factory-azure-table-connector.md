---
title: "aaaMove 資料從 Azure 資料表的 / |Microsoft 文件"
description: "深入了解如何從 Azure 資料表儲存體，使用 Azure Data Factory 的/toomove 資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 3dc3da6d88854674a9108b600534bc5d07575f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-table-using-azure-data-factory"></a>移動資料 tooand 使用 Azure Data Factory 的 Azure 資料表
本文說明如何 toouse hello Azure Data Factory toomove 資料從 Azure 資料表儲存體中的複製活動。 它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。 

您可以從任何支援的來源資料儲存 tooAzure 資料表儲存體，或從 Azure 資料表儲存體支援 tooany 接收資料存放區來複製資料。 如需支援做為來源或接收器 hello 複製活動的資料存放區的清單，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。 

## <a name="getting-started"></a>開始使用
您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出「Azure 資料表儲存體」。

最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。 請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。

您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。 

無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello: 

1. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。
2. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。 
3. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。 

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。  如需使用的 toocopy 資料至 azure 或從 Azure 資料表儲存體的 Data Factory 實體的 JSON 定義的範例，請參閱[JSON 範例](#json-examples)本文一節。 

hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooAzure 資料表儲存體的 JSON 屬性的詳細資料： 

## <a name="linked-service-properties"></a>連結服務屬性
有兩種類型的連結服務中，您可以使用 toolink Azure blob 儲存體 tooan Azure data factory。 它們是：**AzureStorage** 連結服務和 **AzureStorageSas** 連結服務。 hello Azure 儲存體連結服務提供 hello 與全域存取 toohello Azure 儲存體的資料處理站。 而 hello Azure 儲存體 SAS （共用存取簽章） 連結的限制/時間繫結存取 toohello Azure 儲存體的 hello data factory 提供服務。 這兩個連結服務之間沒有其他差異。 選擇符合您需求的 hello 連結服務。 hello 下列各節提供更多詳細資料這兩個連結的服務。

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>資料集屬性
區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。 資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。

hello typeProperties 章節是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置的相關資訊。 hello **typeProperties** hello 資料集的類型 > 一節**AzureTable**具有下列屬性的 hello。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |參照的連結服務的 hello Azure 資料表的資料庫執行個體中的 hello 資料表的名稱。 |是。 當 tableName azureTableSourceQuery 沒有指定時，hello 資料表內的所有記錄都會複製的 toohello 目的地。 如果同時指定 azureTableSourceQuery，滿足 hello 查詢的 hello 資料表內的記錄將會複製的 toohello 目的地。 |

### <a name="schema-by-data-factory"></a>Data factory 的結構描述
若是無結構描述的資料存放區，例如 Azure 資料表，hello Data Factory 服務會推斷 hello 結構描述，其中一種 hello 下列方式：

1. 如果您指定資料的 hello 結構使用 hello**結構**hello 資料集定義，hello Data Factory 服務中的屬性會接受此結構做為 hello 結構描述。 在此情況下，如果資料列的資料行沒有值，系統就會為它提供 null 值。
2. 如果您未指定資料的 hello 結構使用 hello**結構**hello 資料集定義，Data Factory 中的屬性會推斷 hello 結構描述使用 hello 資料中的 hello 第一個資料列。 在此情況下，如果 hello 第一個資料列不包含 hello 完整結構描述，某些資料行缺少 hello 的複製作業的結果中。

因此，對於無結構描述的資料來源，hello 最佳作法是使用 hello 資料 toospecify hello 結構**結構**屬性。

## <a name="copy-activity-properties"></a>複製活動屬性
區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。 屬性 (例如名稱、描述、輸入和輸出資料集，以及原則) 適用於所有類型的活動。

屬性中的 hello hello 活動 hello typeProperties 區段可用另一方面會隨每個活動類型。 複製活動它們而異的來源與接收的 hello 類型。

**AzureTableSource**支援下列屬性 typeProperties > 一節中的 hello:

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| AzureTableSourceQuery |使用自訂查詢 tooread hello 的資料。 |Azure 資料表查詢字串。 請參閱 hello 下一節中的範例。 |否。 當 tableName azureTableSourceQuery 沒有指定時，hello 資料表內的所有記錄都會複製的 toohello 目的地。 如果同時指定 azureTableSourceQuery，滿足 hello 查詢的 hello 資料表內的記錄將會複製的 toohello 目的地。 |
| azureTableSourceIgnoreTableNotFound |指出是否壓抑 hello 的資料表不存在例外狀況。 |TRUE<br/>FALSE |否 |

### <a name="azuretablesourcequery-examples"></a>azureTableSourceQuery 範例
如果 Azure 資料表資料行是字串類型：

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

如果 Azure 資料表資料行是日期時間類型：

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

**AzureTableSink**支援下列屬性 typeProperties > 一節中的 hello:

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |預設資料分割索引鍵值，可供 hello 接收。 |字串值。 |否 |
| azureTablePartitionKeyName |指定的值用做為資料分割索引鍵的 hello 資料行的名稱。 如果未指定，azuretabledefaultpartitionkeyvalue 會做為 hello 資料分割索引鍵。 |資料行名稱。 |否 |
| azureTableRowKeyName |指定的資料行值用做為資料列索引鍵的 hello 資料行的名稱。 如果未指定，則會針對每個資料列使用 GUID。 |資料行名稱。 |否 |
| azureTableInsertType |hello 模式 tooinsert 資料插入 Azure 資料表。<br/><br/>這個屬性控制與相符的資料分割和資料列的索引鍵的 hello 輸出資料表中的現有資料列是否具有取代或合併其值。 <br/><br/>toolearn 有關這些設定 （「 合併 」 和 「 取代 」） 的運作方式，請參閱[插入或合併實體](https://msdn.microsoft.com/library/azure/hh452241.aspx)和[插入或取代實體](https://msdn.microsoft.com/library/azure/hh452242.aspx)主題。 <br/><br> 此設定適用於在 hello 資料列層級，不 hello 資料表層級，和這兩個選項會刪除 hello 輸出資料表不存在於 hello 輸入的資料列。 |合併 (預設值)<br/>取代 |否 |
| writeBatchSize |Hello 叫用 writeBatchSize 或 writeBatchTimeout 時，請將資料插入至 hello Azure 資料表中。 |整數 (資料列數目) |否 (預設值：10000) |
| writeBatchTimeout |用戶端 hello 叫用 writeBatchSize 或 writeBatchTimeout 時，將資料插入 hello Azure 資料表 |時間範圍<br/><br/>範例：“00:20:00” (20 分鐘) |否 （預設 toostorage 用戶端預設逾時值 90 秒） |

### <a name="azuretablepartitionkeyname"></a>azureTablePartitionKeyName
對應的來源資料行 tooa 目的地資料行之前您可以使用 hello 目的地資料行，如 hello azureTablePartitionKeyName 使用 hello 轉譯程式的 JSON 屬性。

下列範例的 hello，來源資料行 DivisionID 就是對應的 toohello 目的地資料行： DivisionID。  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
hello DivisionID 已指定為 hello 資料分割索引鍵。

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a>JSON 範例
hello 下列範例會提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。 它們會顯示如何從 Azure 資料表儲存體和 Azure Blob Database toocopy 資料 tooand。 不過，資料可以複製**直接**從任何支援的 hello 接收的 hello 來源 tooany。 如需詳細資訊，請參閱"支援資料存放區和格式 」 「 hello 」 一節中[使用複製活動移動資料](data-factory-data-movement-activities.md)。

## <a name="example-copy-data-from-azure-table-tooazure-blob"></a>範例： 將資料從 Azure 資料表 tooAzure Blob 複製
下列範例會示範 hello:

1. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 類型的連結服務 (同時用於資料表和 Blob)。
2. [AzureTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
3. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
4. hello[管線](data-factory-create-pipelines.md)與使用複製活動[AzureTableSource](#activity-properties)和[BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)。

hello 範例會將屬於 toohello Azure 資料表 tooa blob 中的預設資料分割的每個小時的資料。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

**Azure 儲存體連結服務：**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
Azure Data Factory 支援兩種類型的 Azure 儲存體連結服務：**AzureStorage** 和 **AzureStorageSas**。 如 hello 第一個、 指定 hello 連接字串，包含 hello 帳戶金鑰和 hello 更新版本，您可以指定 hello 共用存取簽章 (SAS) Uri。 請參閱 [連結服務](#linked-service-properties) 章節以取得詳細資料。  

**Azure 資料表輸入資料集：**

hello 範例假設您有 Azure 資料表中建立資料表"MyTable"。

設定"external":"true"會通知 hello Data Factory 服務的 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時。

```JSON
{
  "name": "AzureTableInput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
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

**Azure Blob 輸出資料集：**

資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。 hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**具有 AzureTableSource 和 BlobSink 的管線中複製活動：**

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**AzureTableSource**和**接收**類型設定得**BlobSink**。 使用指定的 hello SQL 查詢**AzureTableSourceQuery**屬性選取 hello 資料 hello 預設分割區從每個小時 toocopy。

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
                "typeProperties": {
                      "source": {
                        "type": "AzureTableSource",
                        "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },                
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
            }
         ]    
    }
}
```

## <a name="example-copy-data-from-azure-blob-tooazure-table"></a>範例： 從 Azure Blob tooAzure 資料表複製資料
下列範例會示範 hello:

1. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 類型的連結服務 (同時用於資料表和 Blob)
2. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
3. [AzureTable](#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
4. hello[管線](data-factory-create-pipelines.md)與使用複製活動[BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties)和[AzureTableSink](#copy-activity-properties)。

hello 範例從 Azure blob tooan Azure 資料表複製時間序列資料的每小時。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

**Azure 儲存體 (同時適用於 Azure 資料表和 Blob) 連結服務：**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

Azure Data Factory 支援兩種類型的 Azure 儲存體連結服務：**AzureStorage** 和 **AzureStorageSas**。 如 hello 第一個、 指定 hello 連接字串，包含 hello 帳戶金鑰和 hello 更新版本，您可以指定 hello 共用存取簽章 (SAS) Uri。 請參閱 [連結服務](#linked-service-properties) 章節以取得詳細資料。

**Azure Blob 輸入資料集：**

每小時從新的 Blob 挑選資料 (頻率：小時，間隔：1)。 hello 資料夾路徑和檔案名稱 hello blob 會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 年、 月和日的部分 hello 開始時間，會使用 hello 資料夾路徑和檔案名稱會使用 hello hello 開始時間的小時部分。 "external":"true"的設定會在該 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時通知 hello Data Factory 服務。

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
      ],
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

**Azure 資料表輸出資料集：**

hello 範例會將名為"MyTable"Azure 資料表中的資料 tooa 資料表複製。 建立 Azure 資料表具有如預期般 hello Blob CSV 檔案 toocontain hello 相同數目的資料行。 新的資料列會加入 toohello 資料表的每個小時。

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**具有 BlobSource 和 AzureTableSink 的管線中複製活動：**

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**BlobSource**和**接收**類型設定得**AzureTableSink**。

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "AzureTableSink",
            "writeBatchSize": 100,
            "writeBatchTimeout": "01:00:00"
          }
        },
        "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },                        
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```
## <a name="type-mapping-for-azure-table"></a>Azure 資料表的類型對應
Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)發行項，複製活動會執行自動類型轉換來源類型 toosink 類型以下列兩種方法的 hello。

1. 從原生的來源類型 too.NET 類型轉換
2. 從.NET 型別 toonative 接收器類型轉換

移動資料時太 & 從 Azure 資料表，hello 遵循[Azure 表格服務所定義的對應](https://msdn.microsoft.com/library/azure/dd179338.aspx)可用從 Azure 資料表 OData 類型 too.NET 型別，反之亦然。

| OData 資料類型 | .NET 類型 | 詳細資料 |
| --- | --- | --- |
| Edm.Binary |byte[] |向上 too64 KB 的位元組陣列。 |
| Edm.Boolean |布林 |布林值。 |
| Edm.DateTime |DateTime |以國際標準時間 (UTC) 表示的 64 位元值。 hello 支援日期時間範圍是從午夜 12:00，1601年西元 1 (C.E.), UTC. hello 範圍會在年 12 月 31 日結束 9999。 |
| Edm.Double |double |64 位元的浮點值。 |
| Edm.Guid |Guid |128 位元的全域唯一識別碼。 |
| Edm.Int32 |Int32 |32 位元的整數。 |
| Edm.Int64 |Int64 |64 位元的整數。 |
| Edm.String |String |UTF 16 編碼值。 字串值可能是 up too64 KB。 |

### <a name="type-conversion-sample"></a>類型轉換範例
下列範例中的 hello 適用於資料複製到 Azure Blob tooAzure 資料表使用類型轉換。

假設 hello Blob 資料集的 CSV 格式，而且包含三個資料行。 其中一個方法是使用 hello 星期幾的縮寫法文名稱的自訂日期時間格式的 datetime 資料行。

定義 hello Blob 來源的資料集以及 hello 資料行的類型定義，如下所示。

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
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
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
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
從 Azure 資料表 OData 類型 too.NET 類型指定 hello 類型對應，您會定義 hello 資料表 Azure 資料表中以 hello 遵循結構描述。

**Azure 資料表結構描述：**

| 資料行名稱 | 類型 |
| --- | --- |
| userid |Edm.Int64 |
| 名稱 |Edm.String |
| lastlogindate |Edm.DateTime |

接下來，定義 hello Azure 資料表的資料集，如下所示。 由於 hello 基礎資料存放區中已經指定 hello 型別資訊，因此不需要 toospecify hello 類型資訊的 「 結構 」 一節。

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

在此情況下，Data Factory 自動類型轉換包括 hello Datetime 欄位與 hello 自訂 datetime 格式移動資料，從 Blob tooAzure 資料表時，使用 hello 「 fr-fr 」 文化特性。

> [!NOTE]
> toomap 資料行從來源資料集 toocolumns 從接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。

## <a name="performance-and-tuning"></a>效能和微調
關於金鑰 toolearn 因素影響效能的 Azure Data Factory 和各種方式 toooptimize 中的資料移動 （複製活動），請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)。
