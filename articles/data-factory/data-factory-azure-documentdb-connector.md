---
title: "aaaMove 資料從 Azure Cosmos DB / |Microsoft 文件"
description: "了解如何使用 Azure Data Factory 從 Azure Cosmos DB 集合來回移動資料"
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a>從使用 Azure Data Factory 的 Azure Cosmos DB 移動資料 tooand
本文說明如何 toouse hello Azure Data Factory toomove 資料從 Azure Cosmos DB (DocumentDB API) 中的複製活動。 它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。 

您可以從任何支援的來源資料儲存 tooAzure Cosmos DB，或從 Azure Cosmos DB tooany 支援接收資料存放區來複製資料。 如需支援做為來源或接收器 hello 複製活動的資料存放區的清單，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。 

> [!IMPORTANT]
> Azure Cosmos DB 連接器只支援 DocumentDB API。

toocopy 資料當做-是要從/JSON 檔案或另一個 Cosmos DB 集合，請參閱[匯入/匯出 JSON 文件](#importexport-json-documents)。

## <a name="getting-started"></a>開始使用
您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出 Azure Cosmos DB。

最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。 請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。

您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。 

無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello: 

1. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。
2. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。 
3. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。 

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。  如需使用的 toocopy 資料，從 Cosmos DB 的 Data Factory 實體的 JSON 定義的範例，請參閱[JSON 範例](#json-examples)本文一節。 

hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooCosmos DB 的 JSON 屬性的詳細資料： 

## <a name="linked-service-properties"></a>連結服務屬性
下表中的 hello 提供 JSON 項目特定 tooAzure Cosmos 資料庫連結服務的描述。

| **屬性** | **說明** | **必要** |
| --- | --- | --- |
| 類型 |hello 類型屬性必須設定為： **DocumentDb** |是 |
| connectionString |指定所需 tooconnect tooAzure Cosmos DB 資料庫的資訊。 |是 |

範例：

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a>資料集屬性
如需區段和屬性可用來定義資料集的完整清單，請參閱 toohello[建立資料集](data-factory-create-datasets.md)發行項。 資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。

hello typeProperties 章節是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置的相關資訊。 hello typeProperties 區段 hello 資料集型別的**DocumentDbCollection**具有下列屬性的 hello。

| **屬性** | **說明** | **必要** |
| --- | --- | --- |
| collectionName |Hello Cosmos DB 文件集合的名稱。 |是 |

範例：

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a>Data factory 的結構描述
針對無結構描述的資料存放區，例如 Azure Cosmos DB，hello Data Factory 服務會推斷 hello 結構描述 hello 下列方式之一：  

1. 如果您指定資料的 hello 結構使用 hello**結構**hello 資料集定義，hello Data Factory 服務中的屬性會接受此結構做為 hello 結構描述。 在此情況下，如果資料列不包含資料行的值，則會使用 null 值。
2. 如果您未指定資料 hello 結構使用 hello**結構**hello 資料集定義，hello Data Factory 服務中的屬性會推斷 hello 結構描述使用 hello 資料中的 hello 第一個資料列。 在此情況下，如果 hello 第一個資料列不包含 hello 完整結構描述，某些資料行將會遺失在 hello 的複製作業的結果。

因此，對於無結構描述的資料來源，hello 最佳作法是使用 hello 資料 toospecify hello 結構**結構**屬性。

## <a name="copy-activity-properties"></a>複製活動屬性
如需區段和屬性可用來定義活動的完整清單，請參閱 toohello[建立管線](data-factory-create-pipelines.md)發行項。 屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。

> [!NOTE]
> hello 複製活動會採用只有 1 個輸入，並產生一個輸出。

屬性中的 hello hello 活動 hello typeProperties 區段可用另一方面改變與每個活動類型與它們的來源與接收的 hello 類型而異的複製活動發生。

當來源的類型時，複製活動發生**DocumentDbCollectionSource** hello 下列屬性可用於**typeProperties** > 一節：

| **屬性** | **說明** | **允許的值** | **必要** |
| --- | --- | --- | --- |
| query |指定 hello 查詢 tooread 資料。 |Azure Cosmos DB 所支援的查詢字串。 <br/><br/>範例： `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |否 <br/><br/>如果未指定，hello 執行的 SQL 陳述式：`select <columns defined in structure> from mycollection` |
| nestingSeparator |巢狀 hello 文件的特殊字元 tooindicate |任何字元。 <br/><br/>Azure Cosmos DB 是 JSON 文件的 NoSQL 存放區 (允許巢狀結構)。 Azure Data Factory 可讓使用者 toodenote 階層 nestingSeparator，也就是透過 「。 」 在上述範例 hello。 Hello 分隔符號 hello 複製活動會產生三個子系的元素與 hello"Name"物件第一個中間和最後一個、 相應 too"Name.First"，"Name.Middle"和"Name.Last"hello 在資料表定義。 |否 |

**DocumentDbCollectionSink**支援 hello 下列屬性：

| **屬性** | **說明** | **允許的值** | **必要** |
| --- | --- | --- | --- |
| nestingSeparator |需要 hello 來源資料行名稱 tooindicate 巢狀文件中的特殊字元。 <br/><br/>例如上述： `Name.First` hello 輸出資料表會產生下列 JSON 結構 hello Cosmos DB 文件中的 hello:<br/><br/>"Name": {<br/>    "First": "John"<br/>}, |為使用的 tooseparate 巢狀層級的字元。<br/><br/>預設值為 `.` (點)。 |為使用的 tooseparate 巢狀層級的字元。 <br/><br/>預設值為 `.` (點)。 |
| writeBatchSize |並行要求數目 tooAzure Cosmos DB 服務 toocreate 文件。<br/><br/>使用這個屬性來複製從 Cosmos DB 的資料時，您可以微調 hello 效能。 當您增加叫用 writeBatchSize，因為會傳送多個平行要求 tooCosmos DB 時，您可以預期更佳的效能。 不過，您必須先 tooavoid 節流，可擲回 hello 錯誤訊息: 「 要求率非常大 」。<br/><br/>節流是由許多因素所決定，包括文件大小、文件中的詞彙數目、目標集合的檢索原則等。複製作業，您可以使用較佳的集合 (例如 S3) toohave hello 大部分可用的輸送量 （2500 的要求單位/秒）。 |Integer |否 (預設值：5) |
| writeBatchTimeout |在逾時之前，請等待 hello 作業 toocomplete 時間。 |時間範圍<br/><br/> 範例：“00:30:00” (30 分鐘)。 |否 |

## <a name="importexport-json-documents"></a>匯入/匯出 JSON 文件
使用此 Cosmos DB 連接器，您可以輕鬆地

* 將 JSON 文件從各種來源匯入到 Cosmos DB，包括 Azure Blob、Azure Data Lake、內部部署的檔案系統，或 Azure Data Factory 所支援的其他檔案型存放區。
* 將 JSON 文件從 Cosmos DB 集合匯出至各種檔案型存放區。
* 在兩個 Cosmos DB 集合之間依原樣移轉資料。

tooachieve 複製這類結構描述無關， 
* 複製精靈時，請檢查 hello **」 匯出為-tooJSON 檔案或 Cosmos DB 集合"**選項。
* 當使用 JSON 編輯，請不要指定 hello 「 結構 」 一節中的 Cosmos DB 的資料集，也不 Cosmos DB 上的 「 nestingSeparator"屬性來源/接收器複製活動中。 從 tooimport / 匯出 tooJSON 檔案，資料集中 hello 檔案存放區格式類型指定為"JsonFormat，「 組態 」 filePattern 」 並略過 hello rest 格式設定，請參閱[JSON 格式](data-factory-supported-file-and-compression-formats.md#json-format)詳細資料 區段。

## <a name="json-examples"></a>JSON 範例
hello 下列範例會提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。 它們會顯示如何從 Azure Cosmos DB 和 Azure Blob 儲存體 toocopy 資料 tooand。 不過，資料可以複製**直接**從任何 hello 接收所述的 hello 來源 tooany[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a>範例： 將資料從 Azure Cosmos DB tooAzure Blob 複製
顯示 hello 以下的範例：

1. [DocumentDb](#linked-service-properties)類型的連結服務。
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
3. [DocumentDbCollection](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
5. 具有使用 [DocumentDbCollectionSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

hello 範例會在 Azure Cosmos DB tooAzure Blob 複製資料。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

**Azure Cosmos DB 連結服務︰**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
**Azure Blob 儲存體連結服務：**

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
**Azure DocumentDB 輸入資料集：**

hello 範例假設您擁有名為的集合**人員**Azure Cosmos DB 資料庫中。

設定"external":"true"，並指定 externalData hello Azure Data Factory 服務該 hello 資料表的原則資訊是外部 toohello 資料處理站，而不產生 hello data factory 中的活動時。

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Azure Blob 輸出資料集：**

資料會複製的 tooa 新 blob hello 路徑 hello blob 反映 hello 特定的日期時間的小時資料粒度的每個小時。

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
範例 hello Cosmos DB 資料庫中的人員集合中的 JSON 文件：

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
Cosmos DB 支援在階層式 JSON 文件上使用類似 SQL 的語法來查詢文件。

範例： 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

hello 下列管線將資料從 hello hello Azure Cosmos DB 資料庫 tooan Azure blob 中的使用者集合。 Hello 複製活動 hello 一部分已指定輸入和輸出資料集。  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a>範例： 將資料從 Azure Blob tooAzure Cosmos DB 複製 
顯示 hello 以下的範例：

1. [DocumentDb](#azure-documentdb-linked-service-properties)類型的連結服務。
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
3. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4. [DocumentDbCollection](#azure-documentdb-dataset-type-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
5. 具有使用 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 和 [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

hello 範例會將資料從 Azure blob tooAzure Cosmos DB。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

**Azure Blob 儲存體連結服務：**

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
**Azure Cosmos DB 連結服務︰**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
**Azure Blob 輸入資料集：**

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
**Azure Cosmos DB 輸出資料集︰**

hello 範例會從名為"Person"的資料 tooa 集合複製。

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
hello 下列管線將資料從 Azure Blob toohello hello Cosmos DB 中的使用者集合。 Hello 複製活動 hello 一部分已指定輸入和輸出資料集。

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
如果輸入 hello 範例 blob 做

```
1,John,,Doe
```
然後 hello 的輸出就會在 Cosmos DB 中的 JSON:

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
Azure Cosmos DB 是 JSON 文件的 NoSQL 存放區 (允許巢狀結構)。 Azure Data Factory 可讓使用者透過的 toodenote 階層**nestingSeparator**，也就是"。" 。 Hello 分隔符號 hello 複製活動會產生三個子系的元素與 hello"Name"物件第一個中間和最後一個、 相應 too"Name.First"，"Name.Middle"和"Name.Last"hello 在資料表定義。

## <a name="appendix"></a>附錄
1. **問題：**沒有 hello 複製活動支援更新現有的記錄嗎？

    **答：** 否。
2. **問題：**的運作方式的複製 tooAzure Cosmos DB 處理重試已複製的記錄嗎？

    **回答：**如果記錄具有 「 識別碼 」 欄位，而且 hello 複製作業會嘗試 tooinsert hello 的記錄相同識別碼 hello 複製作業會擲回錯誤。  
3. **問：**Data Factory 支援[範圍或雜湊式資料分割](../documentdb/documentdb-partition-data.md)嗎？

    **答：** 否。
4. **問：**我可以為資料表指定多個 Azure Cosmos DB 集合嗎？

    **答：** 否。 目前只能指定一個集合。

## <a name="performance-and-tuning"></a>效能和微調
請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。
