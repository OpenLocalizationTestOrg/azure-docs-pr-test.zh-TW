---
title: "從 Web 表中使用 Azure Data Factory aaaMove 資料 |Microsoft 文件"
description: "深入了解如何使用 web 資料表的 toomove 資料頁面上使用 Azure Data Factory。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a>使用 Azure Data Factory 來移動 Web 資料表的資料
本文概述如何在 Azure Data Factory toomove 資料從資料表中的網頁 tooa toouse hello 複製活動支援接收資料存放區。 這篇文章是根據 hello[資料移動活動](data-factory-data-movement-activities.md)呈現資料移動的一般概觀，以及複製活動與 hello 清單做為來源/接收器所支援的資料存放區的發行項。

目前資料處理站都會支援只從 Web 資料表 tooother 資料移動的資料存放區，但不是將資料從其他資料會儲存 tooa Web 資料表的目的地。

> [!IMPORTANT]
> 此 Web 連接器目前只支援從 HTML 網頁擷取資料表內容。 從 HTTP/s 的端點，tooretrieve 資料使用[HTTP 連接器](data-factory-http-connector.md)改為。

## <a name="getting-started"></a>開始使用
您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 Cassandra 資料存放區移動資料。 

- 最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。 請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。 
- 您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。 

無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:

1. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。
2. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。 
3. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。 

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。  具有使用的 toocopy 資料從 web 資料表的 Data Factory 實體的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從 Web 資料表 tooAzure Blob 複製](#json-example-copy-data-from-web-table-to-azure-blob)本文一節。 

hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooa Web 資料表的 JSON 屬性的詳細資料：

## <a name="linked-service-properties"></a>連結服務屬性
下表中的 hello 提供 JSON 項目特定 tooWeb 連結服務的描述。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性必須設定為： **Web** |是 |
| Url |URL toohello Web 來源 |是 |
| authenticationType |匿名。 |是 |

### <a name="using-anonymous-authentication"></a>使用匿名驗證

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a>資料集屬性
區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。 資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。

hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。 hello typeProperties 區段類型的資料集**WebTable**具有下列屬性的 hello

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| 類型 |hello 資料集的類型。 必須設定得**WebTable** |是 |
| 路徑 |相對 URL toohello 資源包含 hello 資料表。 |否。 若未指定路徑，則會使用連結的 hello 服務定義中指定的唯一 hello URL。 |
| index |hello hello 資源中的 hello 資料表的索引。 請參閱[Get 索引的資料表中的 HTML 網頁的](#get-index-of-a-table-in-an-html-page)> 一節步驟 toogetting 索引的 HTML 網頁中的資料表。 |是 |

**範例：**

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a>複製活動屬性
區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。 屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。

而 hello 活動 hello typeProperties 區段中可用的屬性會隨每個活動類型。 複製活動它們而異的來源與接收的 hello 類型。

目前，當複製活動中的 hello 來源屬於型別**WebSource**，支援任何其他屬性。


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a>JSON 範例： 從 Web 資料表 tooAzure Blob 複製資料
下列範例會示範 hello:

1. [Web](#linked-service-properties)類型的連結服務。
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
3. [WebTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
5. 具有使用 [WebSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

hello 範例將資料從 Azure blob Web 資料表 tooan 每小時。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

hello 下列範例顯示如何從 Web 資料表 tooan Azure toocopy 資料的 blob。 不過，資料可以複製直接的 hello tooany 接收器中所述的 hello[資料移動活動](data-factory-data-movement-activities.md)hello 複製活動使用 Azure Data Factory 中的發行項。

**Web 連結服務**本例使用 hello Web 連結服務與匿名驗證。 請參閱 [Web 連結服務](#linked-service-properties) 一節，來了解您可以使用的不同驗證類型。

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

**Azure 儲存體連結服務**

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

**WebTable 的輸入資料集**設定**外部**太**true**該 hello 集外部 toohello 資料處理站，且不產生 hello 中的活動時，會通知 hello Data Factory 服務資料處理站。

> [!NOTE]
> 請參閱[Get 索引的資料表中的 HTML 網頁的](#get-index-of-a-table-in-an-html-page)> 一節步驟 toogetting 索引的 HTML 網頁中的資料表。  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


**Azure Blob 輸出資料集**

資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```



**具有複製活動的管線**

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**WebSource**和**接收**類型設定得**BlobSink**。

請參閱[WebSource 類型屬性](#copy-activity-type-properties)hello hello WebSource 支援之屬性的清單。

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
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

## <a name="get-index-of-a-table-in-an-html-page"></a>取得 HTML 網頁中資料表的索引
1. 啟動**Excel 2016**切換 toohello**資料** 索引標籤。  
2. 按一下**新查詢**hello 在工具列上，指向 太**從其他來源**按一下**從 Web**。

    ![Power Query 功能表](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. 在 hello**從 Web**對話方塊方塊中，輸入**URL**您在將使用連結的服務 JSON (例如： https://en.wikipedia.org/wiki/) 以及您可以為 hello 資料集指定的路徑 (例如： AFI %27s_100_Years...100_Movies)，然後按一下**確定**。

    ![[從 Web] 對話方塊](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    此範例中使用的 URL：https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies
4. 如果您看到**存取 Web 內容**對話方塊中，選取 hello 右邊**URL**，**驗證**，然後按一下**連接**。

   ![[存取 Web 內容] 對話方塊](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. 按一下**資料表**hello 樹狀結構檢視 toosee 內容從 hello 資料表中的項目，然後按一下**編輯**hello 底部的按鈕。  

   ![[導覽器] 對話方塊](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. 在 hello**查詢編輯器**視窗中，按一下**進階編輯器**hello 工具列上的按鈕。

    ![[進階編輯器] 按鈕](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. 在 hello [進階編輯器] 對話方塊中，hello 數目接下來太 「 來源 」 是 hello 索引。

    ![進階編輯器及索引](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

如果您使用 Excel 2013，使用[Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) tooget hello 索引。 請參閱[連接 tooa 網頁](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8)文件以取得詳細資料。 hello 步驟很相似，但您使用[Microsoft Power BI desktop](https://powerbi.microsoft.com/desktop/)。

> [!NOTE]
> toomap 資料行從來源資料集 toocolumns 從接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。

## <a name="performance-and-tuning"></a>效能和微調
請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。
