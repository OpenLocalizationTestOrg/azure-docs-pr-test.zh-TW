---
title: "使用 Data Factory aaaPush 資料 tooSearch 索引 |Microsoft 文件"
description: "深入了解如何使用 Azure Data Factory 的 toopush 資料 tooAzure 搜尋索引。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a>藉由使用 Azure Data Factory 推播資料 tooan Azure 搜尋索引
本文說明如何 toouse hello 複製活動 toopush 資料從支援的來源資料存放區 tooAzure 搜尋索引。 支援的來源資料存放區會列在 hello 來源資料行的 hello[支援來源與接收](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。 這篇文章是根據 hello[資料移動活動](data-factory-data-movement-activities.md)文件，複製活動與支援的資料存放區組合顯示的資料移動的一般概觀。

## <a name="enabling-connectivity"></a>啟用連線
tooallow Data Factory 服務連接到 tooan 在內部部署資料存放區，您在內部部署環境中安裝資料管理閘道器。 您可以在 hello 裝載 hello 來源資料的同一部電腦儲存，或在不同的機器 tooavoid 競用資源的 hello 資料存放區上安裝閘道。

資料管理閘道器會在內部部署資料來源 toocloud 服務連接安全且受管理的方式。 如需資料管理閘道的詳細資訊，請參閱 [在內部部署和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。

## <a name="getting-started"></a>開始使用
您可以建立管線，與使用不同的工具 Api 會將資料從來源資料存放區 tooAzure 搜尋索引推送複製活動。

最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。 請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。

您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。 

無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello: 

1. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。
2. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。 
3. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。 

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。  具有使用的 toocopy 資料 tooAzure 搜尋索引的 Data Factory 實體的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從內部部署 SQL Server tooAzure 搜尋索引複製](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index)本文一節。 

hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooAzure 搜尋索引的 JSON 屬性的詳細資料：

## <a name="linked-service-properties"></a>連結服務屬性

hello 下表提供說明屬於特定 toohello 連結的 Azure 搜尋服務的 JSON 元素。

| 屬性 | 說明 | 必要 |
| -------- | ----------- | -------- |
| 類型 | hello 類型屬性必須設定為： **AzureSearch**。 | 是 |
| url | Hello Azure 搜尋服務的 URL。 | 是 |
| key | Hello Azure 搜尋服務的管理金鑰。 | 是 |

## <a name="dataset-properties"></a>資料集屬性

區段和屬性都可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。 資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型。 hello **typeProperties**區段是不同的資料集的每個型別。 hello typeProperties 區段 hello 類型的資料集**AzureSearchIndex**具有下列屬性的 hello:

| 屬性 | 說明 | 必要 |
| -------- | ----------- | -------- |
| 類型 | hello type 屬性必須設定得**AzureSearchIndex**。| 是 |
| IndexName | Hello Azure 搜尋索引的名稱。 Data Factory 不會建立 hello 索引。 hello 索引必須存在於 Azure 搜尋中。 | 是 |


## <a name="copy-activity-properties"></a>複製活動屬性
區段和屬性都可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。 屬性 (例如名稱、描述、輸入和輸出資料表，以及各種原則) 適用於所有類型的活動。 而 hello typeProperties 區段中可用的屬性會隨每個活動類型。 複製活動它們而異的來源與接收的 hello 類型。

複製活動 hello 接收器是 hello 類型時的**AzureSearchIndexSink**，typeProperties 節中會使用下列屬性的 hello:

| 屬性 | 說明 | 允許的值 | 必要 |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | 指定是否 toomerge 或取代文件時已存在於 hello 索引。 請參閱 hello [WriteBehavior 屬性](#writebehavior-property)。| 合併 (預設值)<br/>上傳| 否 |
| WriteBatchSize | 將資料上傳至 hello Azure 搜尋索引，當 hello 緩衝區大小到達叫用 writeBatchSize 時。 請參閱 hello[叫用 WriteBatchSize 屬性](#writebatchsize-property)如需詳細資訊。 | 1 too1，000。 預設值為 1000。 | 否 |

### <a name="writebehavior-property"></a>WriteBehavior 屬性
AzureSearchSink 會在寫入資料時更新插入。 換句話說，在撰寫文件中，如果 hello 文件索引鍵已存在於 hello Azure 搜尋索引時，Azure 搜尋更新 hello 現有文件，而不是擲回衝突例外狀況。

hello AzureSearchSink 提供下列兩種 upsert 行為 （藉由使用 AzureSearch SDK） 的 hello:

- **合併**: hello 新文件中的所有 hello 資料行都結合現有的其中一個 hello。 若是 hello 新文件中的 null 值的資料行，則會保留 hello hello 現有的其中一個值。
- **上傳**: hello 新文件取代 hello 現有的我的最愛。 Hello 新文件中未指定資料行，hello 值設定 toonull 是否有非 null 值 hello 現有文件中。

hello 預設行為是**合併**。

### <a name="writebatchsize-property"></a>WriteBatchSize 屬性
Azure 搜尋服務支援批次寫入文件。 批次可包含 1 too1，000 動作。 動作會處理一個文件 tooperform hello 上傳/合併作業。

### <a name="data-type-support"></a>資料類型支援
hello 下表會指定是否支援的 Azure 搜尋資料類型。

| Azure 搜尋服務資料類型 | 在 Azure 搜尋服務接收器中受到支援 |
| ---------------------- | ------------------------------ |
| String | Y |
| Int32 | Y |
| Int64 | Y |
| 兩倍 | Y |
| Boolean | Y |
| DataTimeOffset | Y |
| 字串陣列 | N |
| GeographyPoint | N |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a>JSON 範例： 將資料從內部部署 SQL Server tooAzure 搜尋索引複製

下列範例會示範 hello:

1.  [AzureSearch](#linked-service-properties) 類型的連結服務。
2.  [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties)類型的連結服務。
3.  [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4.  [AzureSearchIndex](#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
4.  具有使用 [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) 和 [AzureSearchIndexSink](#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

hello 範例從內部部署 SQL Server 資料庫 tooan Azure 搜尋索引複製時間序列資料的每小時。 此範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

第一個步驟中，安裝程式在內部部署電腦上的 hello 資料管理閘道器。 hello 中的 hello 指示[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。

**Azure 搜尋服務連結的服務：**

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

**SQL Server 連結服務**

```JSON
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```

**SQL Server 輸入資料集**

hello 範例假設您已建立資料表"MyTable"SQL Server 中，而且包含稱為"timestampcolumn 「 時間序列資料的資料行。 您可以透過 hello hello 資料集的 tableName typeProperty 必須使用相同的資料庫，使用單一資料集，但單一資料表內的多個資料表進行查詢。

設定"external":"true"會通知 Data Factory 服務的 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時。

```JSON
{
  "name": "SqlServerDataset",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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

**Azure 搜尋服務輸出資料集：**

hello 範例複本資料 tooan Azure 搜尋索引名為**產品**。 Data Factory 不會建立 hello 索引。 tootest hello 範例，請使用此名稱建立索引。 建立 hello Azure 搜尋索引以 hello 與 hello 輸入資料集的資料行數目相同。 新的項目會加入 toohello Azure 搜尋索引的每個小時。

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

**具有 SQL 來源和「Azure 搜尋索引」接收器的管線中複製活動：**

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**SqlSource**和**接收**類型設定得**AzureSearchIndexSink**。 指定 hello SQL 查詢**SqlReaderQuery**屬性選取 hello 資料在過去小時 toocopy hello。

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
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

如果您從雲端資料存放區將資料複製到 Azure 搜尋服務，則 `executionLocation` 是必要屬性。 hello 下列 JSON 片段顯示需要在複製活動的 hello 變更`typeProperties`做為範例。 參閱[在雲端資料存放區之間複製資料](data-factory-data-movement-activities.md#global)一節以取得支援的值和更多詳細資料。

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a>從雲端來源複製
如果您從雲端資料存放區將資料複製到 Azure 搜尋服務，則 `executionLocation` 是必要屬性。 hello 下列 JSON 片段顯示需要在複製活動的 hello 變更`typeProperties`做為範例。 參閱[在雲端資料存放區之間複製資料](data-factory-data-movement-activities.md#global)一節以取得支援的值和更多詳細資料。

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

您也可以將對應從來源資料集 toocolumns 接收 hello 複製活動定義中的資料集的資料行。 如需詳細資料，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。

## <a name="performance-and-tuning"></a>效能和微調  
請參閱 hello[複製活動效能及微調指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 和各種方式 toooptimize 它。

## <a name="next-steps"></a>後續步驟
請參閱下列文章 hello:

* [複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) ，以取得使用「複製活動」來建立管線的逐步指示。
