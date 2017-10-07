---
title: "使用 Azure Data Factory 的 SAP Business Warehouse aaaMove 資料 |Microsoft 文件"
description: "深入了解如何使用 Azure Data Factory 的 SAP Business Warehouse toomove 資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 85df16f4759a846f578cad301e3cf918179143d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a>使用 Azure Data Factory 從 SAP Business Warehouse 移動資料
本文說明如何 toouse hello Azure Data Factory toomove 資料從內部部署 SAP Business 倉儲 (BW) 中的複製活動。 它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。

您可以從內部部署 SAP Business Warehouse 資料存放區支援 tooany 接收資料存放區複製資料。 取得一份資料存放區支援接收由 hello 複製活動時，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。 資料處理站目前只支援將資料從 SAP Business Warehouse tooother 資料存放區，但不是會將資料從其他資料儲存 tooan SAP Business Warehouse 的。 

## <a name="supported-versions-and-installation"></a>支援的版本和安裝
此連接器支援 SAP Business Warehouse 7.x 版。 它支援使用 MDX 查詢從 Infocube 和 QueryCubes (包括 BEx 查詢) 複製資料。

tooenable hello 連線 toohello SAP BW 的執行個體，安裝下列元件的 hello:
- **資料管理閘道器**: tooon 內部部署資料連接的 Data Factory 服務支援 （包括 SAP Business Warehouse） 存放區使用的元件稱為 「 資料管理閘道器。 請參閱有關資料管理閘道器和 hello 閘道設定的逐步指示 toolearn [toocloud 資料存放區的內部部署資料之間移動資料存放區](data-factory-move-data-between-onprem-and-cloud.md)發行項。 即使 hello SAP Business Warehouse 裝載於 Azure IaaS 虛擬機器 (VM) 需要閘道。 您可以在相同的 VM 為 hello 資料儲存，或在不同的 VM 只要 hello 閘道可以連接 toohello 資料庫 hello 安裝 hello 閘道。
- **SAP NetWeaver 程式庫**hello 閘道機器上。 您可以取得 hello SAP Netweaver 程式庫，從 SAP 管理員，或直接從 hello [SAP 軟體下載中心](https://support.sap.com/swdc)。 搜尋 hello **SAP 附註 #1025361** tooget hello 下載位置 hello 最新版本。 請確定 hello 架構 hello SAP NetWeaver 程式庫 （32 位元或 64 位元） 符合您的閘道安裝。 接著，安裝包含在 hello SAP NetWeaver RFC SDK 相應 toohello SAP 附註的所有檔案。 hello SAP NetWeaver 程式庫也會包含在 hello SAP 用戶端工具安裝中。

> [!TIP]
> 將擷取自 hello NetWeaver RFC SDK 至 system32 資料夾中的 hello dll。

## <a name="getting-started"></a>開始使用
您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 Cassandra 資料存放區移動資料。 

- 最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。 請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。 
- 您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。 

無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:

1. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。
2. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。 
3. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。 

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。  具有使用的 toocopy 資料從內部部署 SAP Business Warehouse 的 Data Factory 實體的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從 SAP Business Warehouse tooAzure Blob 複製](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob)本文一節。 

hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooan SAP BW 資料存放區的 JSON 屬性的詳細資料：

## <a name="linked-service-properties"></a>連結服務屬性
下表中的 hello 提供 JSON 項目特定 tooSAP 商務倉儲 (BW) 連結服務的描述。

屬性 | 說明 | 允許的值 | 必要
-------- | ----------- | -------------- | --------
伺服器 | 執行個體所在的 hello SAP BW 的 hello 伺服器的名稱。 | 字串 | 是
systemNumber | Hello SAP BW 系統的系統編號。 | 以字串表示的二位數十進位數字。 | 是
clientId | Hello W SAP 系統中的 hello 用戶端的用戶端識別碼。 | 以字串表示的三位數十進位數字。 | 是
username | Hello 使用者具有存取 toohello SAP 伺服器的名稱 | 字串 | 是
password | Hello 使用者密碼。 | 字串 | 是
gatewayName | Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 SAP BW 的執行個體。 | 字串 | 是
encryptedCredential | hello 加密認證的字串。 | 字串 | 否

## <a name="dataset-properties"></a>資料集屬性
區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。 資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。

hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。 支援的型別 hello SAP BW 資料集沒有特定型別的屬性**RelationalTable**。 


## <a name="copy-activity-properties"></a>複製活動屬性
區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。 屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。

而 hello 中可用屬性**typeProperties** hello 活動的區段會隨每個活動類型。 複製活動它們而異的來源與接收的 hello 類型。

複製活動中的來源時的型別**RelationalSource** （包含 SAP BW），下列屬性的 hello 可用 typeProperties 區段中：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| query | 指定 hello MDX 查詢 tooread 資料從 hello SAP BW 的執行個體。 | MDX 查詢。 | 是 |


## <a name="json-example-copy-data-from-sap-business-warehouse-tooazure-blob"></a>JSON 範例： 從 SAP Business Warehouse tooAzure Blob 複製資料
hello 下列範例將提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。 這個範例示範如何從 Azure Blob 儲存體的內部部署 SAP Business Warehouse tooan toocopy 資料。 不過，資料可以複製**直接**hello 接收所述的 tooany[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。  

> [!IMPORTANT]
> 此範例提供 JSON 程式碼片段。 它不包含建立 hello 資料處理站的逐步指示。 如需逐步指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。

hello 範例具有下列資料 factory 實體的 hello:

1. [SapBw](#linked-service-properties) 類型的連結服務。
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
3. [RelationalTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
5. 具有使用 [RelationalSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

hello 範例從 SAP Business Warehouse 執行個體 tooan Azure blob 複製資料的每小時。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

第一個步驟中，安裝程式 hello 資料管理閘道器。 hello 中的 hello 指示[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。

### <a name="sap-business-warehouse-linked-service"></a>SAP Business Warehouse 連結服務
此連結服務連結您的 SAP BW 執行個體 toohello data factory。 hello type 屬性設定太**SapBw**。 hello typeProperties > 一節提供 hello SAP BW 的執行個體的連接資訊。 

```json
{
    "name": "SapBwLinkedService",
    "properties":
    {
        "type": "SapBw",
        "typeProperties":
        {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a>Azure 儲存體連結服務
此連結服務連結您的 Azure 儲存體帳戶 toohello data factory。 hello type 屬性設定太**AzureStorage**。 hello typeProperties > 一節提供 hello Azure 儲存體帳戶的連接資訊。

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

### <a name="sap-bw-input-dataset"></a>SAP BW 輸入資料集
此資料集定義 hello SAP Business Warehouse 的資料集。 您設定的 hello Data Factory 資料集的 hello 類型太**RelationalTable**。 目前，您未指定 SAP BW 資料集的任何類型特定屬性。 hello 複製活動定義中的 hello 查詢指定了哪些資料 tooread，從 hello SAP BW 的執行個體。 

設定外部屬性 tootrue 通知 hello Data Factory 服務，該 hello 資料表是外部 toohello 資料處理站，就不會產生 hello data factory 中活動。

頻率和間隔 屬性定義 hello 排程。 在此情況下，hello 資料是從讀取 hello SAP BW 的執行個體每小時。 

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```



### <a name="azure-blob-output-dataset"></a>Azure Blob 輸出資料集
此資料集定義 hello 輸出 Azure Blob 資料集。 hello type 屬性設定 tooAzureBlob。 hello typeProperties 區段提供從 hello SAP BW 的執行個體複製 hello 資料的儲存位置。 hello 資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。 hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sapbw/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a>具有複製活動的管線
hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**RelationalSource** （適用於 SAP BW 來源） 和**接收**類型設定得**BlobSink**. 指定的 hello hello 查詢**查詢**屬性選取 hello 資料在過去小時 toocopy hello。

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<MDX query for SAP BW>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapBwDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
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
                "name": "SapBwToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```



### <a name="type-mapping-for-sap-bw"></a>SAP BW 的類型對應
Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)發行項，複製活動會執行自動類型轉換來源類型 toosink 類型以下列兩種方法的 hello:

1. 從原生的來源類型 too.NET 類型轉換
2. 從.NET 型別 toonative 接收器類型轉換

從 SAP BW 資料時，下列對應的 hello 可用從 SAP BW 類型 too.NET 型別。

Hello ABAP 字典中的資料類型 | .Net 資料類型
-------------------------------- | --------------
ACCP |  int
CHAR | String
CLNT | String
CURR | 十進位
CUKY | String
DEC | 十進位
FLTP | 兩倍
INT1 | 位元組
INT2 | Int16
INT4 | int
LANG | String
LCHR | String
LRAW | Byte[]
PREC | Int16
QUAN | 十進位
RAW | Byte[]
RAWSTRING | Byte[]
STRING | String
單位 | String
DATS | String
NUMC | String
TIMS | String

> [!NOTE]
> toomap 資料行從來源資料集 toocolumns 從接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。


## <a name="map-source-toosink-columns"></a>將來源 toosink 資料行對應
toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。

## <a name="repeatable-read-from-relational-sources"></a>從關聯式來源進行可重複的讀取
複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。 在 Azure Data Factory 中，您可以手動重新執行配量。 您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。 當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。 請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)

## <a name="performance-and-tuning"></a>效能和微調
請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。
