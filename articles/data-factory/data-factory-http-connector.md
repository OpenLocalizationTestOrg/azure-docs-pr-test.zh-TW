---
title: "從 HTTP 來源-Azure aaaMove 資料 |Microsoft 文件"
description: "深入了解如何從內部部署或雲端 HTTP toomove 資料來源使用 Azure Data Factory。"
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
ms.openlocfilehash: e39b9cbff870aef4be91938cacff39a2fd12d64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a>使用 Azure Data Factory 來移動 HTTP 來源的資料
本文概述如何在 Azure Data Factory toomove 資料從雲端上的內部部署/HTTP 端點 tooa toouse hello 複製活動支援接收資料存放區。 這篇文章是根據 hello[資料移動活動](data-factory-data-movement-activities.md)呈現資料移動的一般概觀，以及複製活動與 hello 清單做為來源/接收器所支援的資料存放區的發行項。

資料處理站目前支援僅將資料從 HTTP 來源 tooother 資料存放區，但不是將資料從其他資料會儲存 tooan HTTP 目的地。

## <a name="supported-scenarios-and-authentication-types"></a>支援的案例和驗證類型
您可以使用此 HTTP 連接器 tooretrieve 資料從**雲端和內部部署的 HTTP/s 端點**使用 HTTP**取得**或**POST**方法。 支援下列驗證類型的 hello:**匿名**，**基本**，**摘要**， **Windows**，和**ClientCertificate**。 請注意這個連接器與 hello 的 hello 時差[Web 資料表連接器](data-factory-web-table-connector.md)是： hello 第二種是使用的 tooextract 資料表 HTML 網頁的內容。

複製資料時從內部 HTTP 端點，您需要在 hello 在內部部署環境/Azure VM 中安裝資料管理閘道器。 請參閱[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)文章 toolearn 有關資料管理閘道器和 hello 閘道設定的逐步指示。

## <a name="getting-started"></a>開始使用
您可以建立內含複製活動的管線，使用不同的工具/API 將資料移出 HTTP 來源。

- 最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。 請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。

- 您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。 如 JSON 範例 toocopy HTTP 來源 tooAzure Blob 儲存體的資料，請參閱 < [JSON 範例](#json-examples)此文件的區段。

## <a name="linked-service-properties"></a>連結服務屬性
下表中的 hello 提供 JSON 項目特定 tooHTTP 連結服務的描述。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 | hello 類型屬性必須設定為： `Http`。 | 是 |
| url | 基底 URL toohello Web 伺服器 | 是 |
| authenticationType | 指定 hello 驗證類型。 允許的值為︰**匿名**、**基本**、**摘要**、**Windows**、**ClientCertificate**。 <br><br> 請參閱 「 toosections 上多個屬性和 JSON 範例此表格下方的驗證類型分別。 | 是 |
| enableServerCertificateValidation | 指定是否 tooenable 伺服器 SSL 憑證驗證，是否來源是 HTTPS 的網頁伺服器 | 否，預設值是 True |
| gatewayName | 名稱的 hello 資料管理閘道器 tooconnect tooan 內部 HTTP 的來源。 | 如果從內部部署 HTTP 來源複製資料，則為是。 |
| encryptedCredential | 加密的認證 tooaccess hello HTTP 端點。 自動產生複製精靈] 或 [hello ClickOnce 快顯對話方塊以設定 hello 驗證資訊。 | 否。 僅當從內部部署 HTTP 伺服器複製資料時才套用。 |

請參閱[在內部部署來源和資料管理閘道與 hello 雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)詳細資料設定為內部 HTTP 連接器資料來源的認證。

### <a name="using-basic-digest-or-windows-authentication"></a>使用基本、摘要或 Windows 驗證

設定`authenticationType`為`Basic`， `Digest`，或`Windows`，並指定 hello 除了 hello HTTP 連接器泛型的上方導入了下列屬性：

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| username | 使用者名稱 tooaccess hello HTTP 端點。 | 是 |
| password | Hello 使用者 （使用者名稱） 的密碼。 | 是 |

#### <a name="example-using-basic-digest-or-windows-authentication"></a>範例︰使用基本、摘要或 Windows 驗證

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a>使用 ClientCertificate 驗證

toouse 基本驗證時，設定`authenticationType`為`ClientCertificate`，並指定 hello 除了 hello HTTP 連接器泛型的上方導入了下列屬性：

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| embeddedCertData | hello Base64 編碼內容的 hello 個人資訊交換 (PFX) 檔案的二進位資料。 | 指定任一個 hello`embeddedCertData`或`certThumbprint`。 |
| certThumbprint | hello hello 憑證已安裝在閘道機器的憑證存放區上的憑證指紋。 僅當從內部部署 HTTP 來源複製資料時才套用。 | 指定任一個 hello`embeddedCertData`或`certThumbprint`。 |
| password | Hello 憑證相關聯的密碼。 | 否 |

如果您使用`certThumbprint`安裝適用於驗證和 hello 憑證的 hello hello 本機電腦的個人存放區中，您需要 toogrant hello 的讀取權限 toohello 閘道服務：

1. 啟動 Microsoft Management Console (MMC)。 新增 hello**憑證**嵌入式管理單元的目標 hello**本機電腦**。
2. 展開 [憑證]，[個人]，然後按一下 [憑證]。
3. Hello 個人存放區中的 hello 憑證上按一下滑鼠右鍵，然後選取**所有工作**->**管理私用金鑰...**
3. 在 [hello**安全性**索引標籤上，新增 hello 資料管理閘道主機服務執行使用 hello 讀取權限 toohello 憑證的使用者帳戶。  

#### <a name="example-using-client-certificate"></a>範例︰使用用戶端憑證
此連結服務連結資料 factory tooan 內部 HTTP web 伺服器。 它會使用與資料管理閘道器安裝 hello 機器已安裝的用戶端憑證。

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a>範例︰在檔案中使用用戶端憑證
此連結服務連結資料 factory tooan 內部 HTTP web 伺服器。 它會使用資料管理閘道器安裝 hello 機器上的用戶端憑證檔案。

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a>資料集屬性
區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。 資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。

hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。 hello typeProperties 區段類型的資料集**Http**具有下列屬性的 hello

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| 類型 | 指定的 hello 資料集的 hello 類型。 必須設定得`Http`。 | 是 |
| relativeUrl | 包含 hello 資料的相對 URL toohello 資源。 若未指定路徑，則會使用連結的 hello 服務定義中指定的唯一 hello URL。 <br><br> tooconstruct 動態 URL，您可以使用[Data Factory 函數和系統變數](data-factory-functions-variables.md)，例如"relativeUrl":"$$Text.Format ('/ my/報表？ 月 = {0:yyyy}-{0:MM} （& s) fmt = csv'，SliceStart) 」。 | 否 |
| requestMethod | HTTP 方法。 允許的值為 **GET** 或 **POST**。 | 否。 預設值為 `GET`。 |
| additionalHeaders | 其他 HTTP 要求標頭。 | 否 |
| requestBody | HTTP 要求的內文。 | 否 |
| format | 如果您想 toosimply **hello 資料擷取 HTTP 端點以-為**而不剖析它，請略過此格式設定。 <br><br> 如果您希望 tooparse hello HTTP 回應內容進行複製時，支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。 如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。 |否 |
| compression | 指定 hello 類型和層級的 hello 資料壓縮。 支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。 支援的層級為：**Optimal** 和 **Fastest**。 如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。 |否 |

### <a name="example-using-hello-get-default-method"></a>範例： 使用 hello GET （預設值） 方法

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-hello-post-method"></a>範例： 使用 hello POST 方法

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
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

屬性用於 hello **typeProperties** > 一節的 hello hello 活動另一方面會隨每個活動類型。 複製活動它們而異的來源與接收的 hello 類型。

目前，當複製活動中的 hello 來源屬於型別**HttpSource**，支援下列屬性的 hello。

| 屬性 | 說明 | 必要 |
| -------- | ----------- | -------- |
| httpRequestTimeout | hello 回應 hello HTTP 要求 tooget 的逾時 (TimeSpan)。 它是 hello 逾時 tooget 回應時，不 hello 逾時 tooread 回應資料。 | 否。 預設值：00:01:40 |

## <a name="supported-file-and-compression-formats"></a>支援的檔案和壓縮格式
請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)文章以了解詳細資訊。

## <a name="json-examples"></a>JSON 範例
下列範例中的 hello 提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。 它們會顯示如何從 HTTP toocopy 資料來源 tooAzure Blob 儲存體。 不過，資料可以複製**直接**從任何來源 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。

### <a name="example-copy-data-from-http-source-tooazure-blob-storage"></a>範例： 將資料複製 HTTP 來源 tooAzure Blob 儲存體
hello Data Factory 方案，此範例包含下列 Data Factory 實體的 hello:

1. 一個 [HTTP](#linked-service-properties) 類型的連結服務。
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
3. [Http](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
5. 具有使用 [HttpSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

hello 範例將資料從 Azure blob HTTP 來源 tooan 每小時。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

### <a name="http-linked-service"></a>HTTP 連結服務
這個範例會使用 hello HTTP 連結服務與匿名驗證。 請參閱 [HTTP 連結服務](#linked-service-properties)一節，來了解您可以使用的不同驗證類型。

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a>Azure 儲存體連結服務

```JSON
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

### <a name="http-input-dataset"></a>HTTP 輸入資料集
設定**外部**太**true**該 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時，會通知 hello Data Factory 服務。

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a>Azure Blob 輸出資料集

資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。

```JSON
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

### <a name="pipeline-with-copy-activity"></a>具有複製活動的管線

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**HttpSource**和**接收**類型設定得**BlobSink**。

請參閱[HttpSource](#copy-activity-properties) hello hello HttpSource 支援之屬性的清單。

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
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

> [!NOTE]
> toomap 資料行從來源資料集 toocolumns 從接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。

## <a name="performance-and-tuning"></a>效能和微調
請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。
