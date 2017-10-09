---
title: "使用 Data Factory MongoDB aaaMove 資料 |Microsoft 文件"
description: "深入了解如何從 MongoDB toomove 資料資料庫使用 Azure Data Factory。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 154e85712f27b978976c7499c43dde9429f124c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a>使用 Azure Data Factory 從 MongoDB 移動資料
本文說明如何 toouse hello Azure Data Factory toomove 資料從內部部署 MongoDB 資料庫中的複製活動。 它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。

您可以從內部部署 MongoDB 資料存放區支援 tooany 接收資料存放區複製資料。 取得一份資料存放區支援接收由 hello 複製活動時，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。 目前資料處理站都會支援只移動資料的 MongoDB 資料儲存 tooother 資料存放區，但不適用於將資料從其他資料存放區 tooan MongoDB 資料存放區。 

## <a name="prerequisites"></a>必要條件
Hello Azure Data Factory 服務 toobe 無法 tooconnect tooyour 內部 MongoDB 資料庫中，您必須安裝下列元件的 hello:

- 支援的 MongoDB 版本為︰2.4、2.6、3.0 及 3.2。
- 資料管理閘道器上 hello 的同一部電腦主機 hello 資料庫或不同的機器 tooavoid 競用資源與 hello 資料庫上。 資料管理閘道器是軟體保護和管理的方式連接內部部署資料來源 toocloud 服務。 如需資料管理閘道的詳細資料，請參閱 [資料管理閘道](data-factory-data-management-gateway.md) 一文。 請參閱[將資料從內部部署 toocloud 移](data-factory-move-data-between-onprem-and-cloud.md)文件以取得有關設定 hello 閘道資料管線 toomove 資料的逐步指示。

    當您安裝 hello 閘道時，它會自動安裝 Microsoft MongoDB ODBC 驅動程式使用 tooconnect tooMongoDB。

    > [!NOTE]
    > 您需要 toouse hello 閘道 tooconnect tooMongoDB，即使它裝載於 Azure IaaS Vm。 如果您嘗試在雲端中裝載的 MongoDB tooconnect tooan 執行個體，您也可以在 hello IaaS VM 中安裝 hello 閘道執行個體。

## <a name="getting-started"></a>開始使用
您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 MongoDB 資料存放區移動資料。

最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。 請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。

您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。 

無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello: 

1. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。
2. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。 
3. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。 

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。  具有使用的 toocopy 資料從內部部署 MongoDB 資料存放區的 Data Factory 實體的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從 MongoDB tooAzure Blob 複製](#json-example-copy-data-from-mongodb-to-azure-blob)本文一節。 

hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooMongoDB 來源的 JSON 屬性的詳細資料：

## <a name="linked-service-properties"></a>連結服務屬性
hello 下表提供的 JSON 特定的項目太**OnPremisesMongoDB**連結服務。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性必須設定為： **OnPremisesMongoDb** |是 |
| 伺服器 |IP 位址或主機名稱的 hello MongoDB 伺服器。 |是 |
| 連接埠 |Hello MongoDB 伺服器的 TCP 連接埠會使用用戶端連線 toolisten。 |選用，預設值︰27017 |
| authenticationType |基本或匿名。 |是 |
| username |使用者帳戶 tooaccess MongoDB。 |是 (如果使用基本驗證)。 |
| password |Hello 使用者密碼。 |是 (如果使用基本驗證)。 |
| authSource |您想 toouse toocheck 您的認證進行驗證的 hello MongoDB 資料庫的名稱。 |選用 (如果使用基本驗證)。 預設值： 使用 hello 系統管理員帳戶和 hello 使用 databaseName 屬性所指定的資料庫。 |
| databaseName |您想 tooaccess hello MongoDB 資料庫的名稱。 |是 |
| gatewayName |Hello 閘道存取 hello 資料存放區的名稱。 |是 |
| encryptedCredential |由閘道加密的認證。 |選用 |

## <a name="dataset-properties"></a>資料集屬性
區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。 資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。

hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。 hello typeProperties 區段類型的資料集**MongoDbCollection**具有下列屬性的 hello:

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| collectionName |MongoDB 資料庫中的 hello 集合的名稱。 |是 |

## <a name="copy-activity-properties"></a>複製活動屬性
區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。 屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。

屬性用於 hello **typeProperties** > 一節的 hello hello 活動另一方面會隨每個活動類型。 複製活動它們而異的來源與接收的 hello 類型。

當 hello 來源屬於型別**MongoDbSource** typeProperties 節中會使用下列屬性的 hello:

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| query |使用自訂查詢 tooread hello 的資料。 |SQL-92 查詢字串。 例如：select * from MyTable。 |否 (如果已指定 **dataset** 的 **collectionName**) |



## <a name="json-example-copy-data-from-mongodb-tooazure-blob"></a>JSON 範例： 從 MongoDB tooAzure Blob 複製資料
此範例中提供的範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。 它會顯示如何從 Azure Blob 儲存體的內部部署 MongoDB tooan toocopy 資料。 不過，資料可以複製的 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。

hello 範例具有下列資料 factory 實體的 hello:

1. [OnPremisesMongoDb](#linked-service-properties)類型的連結服務。
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
3. [MongoDbCollection](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
5. 具有使用 [MongoDbSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

hello 範例將資料從查詢結果 MongoDB 資料庫 tooa blob 中的每個小時。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

第一個步驟中，安裝程式 hello 資料管理閘道器，根據 hello 中的 hello 指示[資料管理閘道器](data-factory-data-management-gateway.md)發行項。

**MongoDB 已連結的服務：**

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",  
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

**Azure 儲存體連結服務：**

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

**MongoDB 輸入資料集：**設定"external":"true"會通知 hello Data Factory 服務的 hello 資料表是外部 toohello 資料處理站，就不會產生 hello data factory 中活動。

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

**Azure Blob 輸出資料集：**

資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。 hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**具有 MongoDB 來源和 Blob 接收器的管線中複製活動：**

hello 管線包含設定的 toouse hello 上方輸入和輸出資料集並為每個小時的排程的 toorun 複製活動。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**MongoDbSource**和**接收**類型設定得**BlobSink**。 指定 hello SQL 查詢**查詢**屬性選取 hello 資料在過去小時 toocopy hello。

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
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
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a>Data factory 的結構描述
Azure Data Factory 服務會使用 hello 集合中的 hello 最新的 100 文件推斷 MongoDB 集合的結構描述。 如果這些 100 的文件未包含完整的結構描述，可能會 hello 複製作業期間忽略某些資料行。

## <a name="type-mapping-for-mongodb"></a>MongoDB 的類型對應
Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)發行項，複製活動會執行自動類型轉換來源類型 toosink 類型以 hello 遵循 2 步驟方法：

1. 從原生的來源類型 too.NET 類型轉換
2. 從.NET 型別 toonative 接收器類型轉換

當您移動資料 tooMongoDB hello 遵循從 MongoDB 類型 too.NET 型別會使用對應。

| MongoDB 類型 | .NET Framework 類型 |
| --- | --- |
| Binary |Byte[] |
| Boolean |Boolean |
| 日期 |DateTime |
| NumberDouble |兩倍 |
| NumberInt |Int32 |
| NumberLong |Int64 |
| ObjectID |String |
| String |String |
| UUID |Guid |
| Object |以「_」做為巢狀分隔符號來重新標準化為壓平合併的資料行 |

> [!NOTE]
> 關於支援使用虛擬資料表，陣列 toolearn 參照太[支援使用虛擬資料表的複雜型別的](#support-for-complex-types-using-virtual-tables)下一節。

目前不支援下列 MongoDB 資料類型的 hello: DBPointer、 JavaScript、 Max/Min 金鑰，規則運算式、 符號、 Timestamp、 未定義

## <a name="support-for-complex-types-using-virtual-tables"></a>使用虛擬資料表之複雜類型的支援
Azure Data Factory 會使用內建 ODBC 驅動程式 tooconnect tooand 複製的資料從 MongoDB 資料庫。 複雜類型例如陣列或物件與不同類型跨 hello 文件，hello 驅動程式重新將資料正規化成對應的虛擬資料表。 具體來說，如果資料表包含這類資料行，hello 驅動程式會產生下列虛擬資料表中的 hello:

* A**基底資料表**，其中包含 hello 與 hello hello 複雜型別資料行除外真正的資料表相同的資料。 hello 基底資料表使用名稱相同的 hello 為 hello 它所代表的實際資料表。
* A**虛擬資料表**每個複雜型別資料行，這樣會將巢狀的 hello 資料。 使用 hello hello 真正的資料表名稱、"_"分隔字元和 hello hello 陣列或物件名稱來命名 hello 虛擬資料表。

虛擬資料表，請參閱 toohello hello 真正的資料表中的資料，啟用 hello 驅動程式 tooaccess hello 非正規化的資料。 如需詳細資訊，請參閱下方的＜範例＞一節。 您可以存取 MongoDB 陣列 hello 的內容查詢及聯結 hello 虛擬資料表。

您可以使用 hello[複製精靈](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity)toointuitively 檢視 hello MongoDB 資料庫包括 hello 虛擬資料表中的資料表清單，並預覽 hello 內的資料。 您也可以建構 hello 複製精靈中的查詢，並驗證 toosee hello 結果。

### <a name="example"></a>範例
例如，下面的「ExampleTable」就是 MongoDB 資料表，其具有一個在每個儲存格中都有物件陣列的資料行 (「發票」)，以及一個具有純量類型陣列的資料行 (「評等」)。

| _id | 客戶名稱 | 發票 | 服務等級 | 評等 |
| --- | --- | --- | --- | --- |
| 1111 |ABC |[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}] |Silver |[5,6] |
| 2222 |XYZ |[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}] |Gold |[1,2] |

hello 驅動程式會產生多個虛擬資料表 toorepresent 這個單一資料表。 hello 的第一個虛擬資料表是名為"ExampleTable 」，如下所示的 hello 基底資料表。 hello 基底資料表包含所有 hello 資料的 hello 原始資料表中，但已省略和展開 hello 虛擬資料表中的 hello hello 陣列資料。

| _id | 客戶名稱 | 服務等級 |
| --- | --- | --- |
| 1111 |ABC |Silver |
| 2222 |XYZ |Gold |

hello 下列表格顯示 hello 代表 hello 範例中的 hello 原始陣列的虛擬資料表。 這些資料表包含下列 hello:

* 參考後 toohello 原始主要索引鍵資料行對應 toohello 資料列的 hello 原始陣列 （透過 hello _id 資料行）
* Hello hello 原始陣列中的 hello 資料位置的指示
* hello 展開每個項目 hello 陣列中的資料

資料表「ExampleTable_Invoices」：

| _id | ExampleTable_Invoices_dim1_idx | invoice_id | item | price | 折扣 |
| --- | --- | --- | --- | --- | --- |
| 1111 |0 |123 |toaster |456 |0.2 |
| 1111 |1 |124 |oven |1235 |0.2 |
| 2222 |0 |135 |fridge |12543 |0.0 |

資料表「ExampleTable_Ratings」：

| _id | ExampleTable_Ratings_dim1_idx | ExampleTable_Ratings |
| --- | --- | --- |
| 1111 |0 |5 |
| 1111 |1 |6 |
| 2222 |0 |1 |
| 2222 |1 |2 |

## <a name="map-source-toosink-columns"></a>將來源 toosink 資料行對應
toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。

## <a name="repeatable-read-from-relational-sources"></a>從關聯式來源進行可重複的讀取
複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。 在 Azure Data Factory 中，您可以手動重新執行配量。 您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。 當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。 請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。

## <a name="performance-and-tuning"></a>效能和微調
請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。

## <a name="next-steps"></a>後續步驟
請參閱[在內部部署與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)為建立在資料管線將資料從內部部署資料存放區 tooan Azure 的資料存放區，如需逐步指示發行項。
