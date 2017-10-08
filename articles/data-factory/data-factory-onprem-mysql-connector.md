---
title: "從使用 Azure Data Factory 的 MySQL aaaMove 資料 |Microsoft 文件"
description: "深入了解如何 toomove 資料從 MySQL 資料庫使用 Azure Data Factory。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 452f4fce-9eb5-40a0-92f8-1e98691bea4c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jingwang
ms.openlocfilehash: 3ffe969e42ce1a54b265c4739df43fdc594ea891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a>使用 Azure Data Factory 從 MySQL 移動資料
本文說明如何 toouse hello Azure Data Factory toomove 資料從內部部署 MySQL 資料庫中的複製活動。 它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。

您可以從內部部署 MySQL 資料存放區支援 tooany 接收資料存放區複製資料。 取得一份資料存放區支援接收由 hello 複製活動時，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。 目前資料處理站都會支援只移動資料的 MySQL 資料儲存 tooother 資料存放區，但不適用於將資料從其他資料存放區 tooan MySQL 資料存放區。 

## <a name="prerequisites"></a>必要條件
資料 Factory 服務支援使用 hello 資料管理閘道的連線 tooon 內部部署 MySQL 來源。 請參閱[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)文章 toolearn 有關資料管理閘道器和 hello 閘道設定的逐步指示。

即使 hello MySQL 資料庫裝載於 Azure IaaS 虛擬機器 (VM) 需要閘道。 您可以在相同的 VM 為 hello 資料儲存，或在不同的 VM 只要 hello 閘道可以連接 toohello 資料庫 hello 安裝 hello 閘道。

> [!NOTE]
> 如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。

## <a name="supported-versions-and-installation"></a>支援的版本和安裝
資料管理閘道器 tooconnect toohello MySQL 資料庫，您需要 tooinstall hello [Microsoft Windows 的 MySQL Connector/Net](https://dev.mysql.com/downloads/connector/net/) (6.6.5 版本或更新版本) 在 hello 相同系統 hello 資料管理閘道器。 支援 MySQL 版本 5.1 和以上版本。

> [!TIP]
> 如果您在上叫用錯誤"驗證失敗，因為 hello 遠端群體已經關閉 hello 傳輸資料流。 」，請考慮 tooupgrade hello MySQL Connector/Net toohigher 版本。

## <a name="getting-started"></a>開始使用
您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 Cassandra 資料存放區移動資料。 

- 最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。 請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。 
- 您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。 

無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:

1. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。
2. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。 
3. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。 

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。  具有使用的 toocopy 資料從內部部署 MySQL 資料存放區的 Data Factory 實體的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從 MySQL tooAzure Blob 複製](#json-example-copy-data-from-mysql-to-azure-blob)本文一節。 

hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooa MySQL 資料存放區的 JSON 屬性的詳細資料：

## <a name="linked-service-properties"></a>連結服務屬性
下表中的 hello 提供 JSON 項目特定 tooMySQL 連結服務的描述。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性必須設定為： **OnPremisesMySql** |是 |
| 伺服器 |Hello MySQL 伺服器的名稱。 |是 |
| 資料庫 |Hello MySQL 資料庫的名稱。 |是 |
| 結構描述 |Hello hello 資料庫中的結構描述名稱。 |否 |
| authenticationType |Tooconnect toohello MySQL 資料庫使用的驗證類型。 可能的值為：`Basic`。 |是 |
| username |指定使用者名稱 tooconnect toohello MySQL 資料庫。 |是 |
| password |指定您所指定的 hello 使用者帳戶的密碼。 |是 |
| gatewayName |Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 MySQL 資料庫。 |是 |

## <a name="dataset-properties"></a>資料集屬性
區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。 資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。

hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。 hello typeProperties 區段類型的資料集**RelationalTable** （包括 MySQL 資料集） 具有下列屬性的 hello

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |在 hello MySQL 資料庫連結的服務參考的執行個體中的 hello 資料表的名稱。 |否 (如果已指定 **RelationalSource** 的 **query**) |

## <a name="copy-activity-properties"></a>複製活動屬性
區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。 屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。

而 hello 中可用屬性**typeProperties** hello 活動的區段會隨每個活動類型。 複製活動它們而異的來源與接收的 hello 類型。

複製活動中的來源時的型別**RelationalSource** （包括 MySQL），下列屬性的 hello 可用 typeProperties 區段中：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| query |使用自訂查詢 tooread hello 的資料。 |SQL 查詢字串。 例如：select * from MyTable。 |否 (如果已指定 **dataset** 的 **tableName**) |


## <a name="json-example-copy-data-from-mysql-tooazure-blob"></a>JSON 範例： 將資料從 MySQL tooAzure Blob 複製
此範例中提供的範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。 它會顯示如何 toocopy 資料從內部部署 MySQL 資料庫 tooan Azure Blob 儲存體。 不過，資料可以複製的 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。

> [!IMPORTANT]
> 此範例提供 JSON 程式碼片段。 它不包含建立 hello 資料處理站的逐步指示。 如需逐步指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。

hello 範例具有下列資料 factory 實體的 hello:

1. [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties)類型的連結服務。
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
3. [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
5. 具有使用 [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

hello 範例從 MySQL 資料庫 tooa blob 中的查詢結果複製資料的每小時。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

第一個步驟中，安裝程式 hello 資料管理閘道器。 hello 中的 hello 指示[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。

**MySQL 已連結的服務：**

```JSON
    {
      "name": "OnPremMySqlLinkedService",
      "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
          "server": "<server name>",
          "database": "<database name>",
          "schema": "<schema name>",
          "authenticationType": "<authentication type>",
          "userName": "<user name>",
          "password": "<password>",
          "gatewayName": "<gateway>"
        }
      }
    }
```

**Azure 儲存體連結服務：**

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

**MySQL 輸入資料集：**

hello 範例假設您已建立資料表"MyTable"MySQL 中，而且包含稱為"timestampcolumn 「 時間序列資料的資料行。

設定"external":"true"會通知 hello Data Factory 服務的 hello 資料表是外部 toohello 資料處理站，就不會產生 hello data factory 中活動。

```JSON
    {
        "name": "MySqlDataSet",
        "properties": {
            "published": false,
            "type": "RelationalTable",
            "linkedServiceName": "OnPremMySqlLinkedService",
            "typeProperties": {},
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true,
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
        "name": "AzureBlobMySqlDataSet",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "mycontainer/mysql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**具有複製活動的管線：**

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**RelationalSource**和**接收**類型設定得**BlobSink**。 指定 hello SQL 查詢**查詢**屬性選取 hello 資料在過去小時 toocopy hello。

```JSON
    {
        "name": "CopyMySqlToBlob",
        "properties": {
            "description": "pipeline for copy activity",
            "activities": [
                {
                    "type": "Copy",
                    "typeProperties": {
                        "source": {
                            "type": "RelationalSource",
                            "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                        },
                        "sink": {
                            "type": "BlobSink",
                            "writeBatchSize": 0,
                            "writeBatchTimeout": "00:00:00"
                        }
                    },
                    "inputs": [
                        {
                            "name": "MySqlDataSet"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobMySqlDataSet"
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
                    "name": "MySqlToBlob"
                }
            ],
            "start": "2014-06-01T18:00:00Z",
            "end": "2014-06-01T19:00:00Z"
        }
    }
```


### <a name="type-mapping-for-mysql"></a>MySQL 的類型對應
Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)發行項，複製活動會執行自動類型轉換來源類型 toosink 類型以下列兩種方法的 hello:

1. 從原生的來源類型 too.NET 類型轉換
2. 從.NET 型別 toonative 接收器類型轉換

當您移動資料 tooMySQL，hello 下列會使用對應從 MySQL 類型 too.NET 型別。

| MySQL 資料庫類型 | .NET Framework 類型 |
| --- | --- |
| 不帶正負號的 bigint |十進位 |
| bigint |Int64 |
| bit |十進位 |
| blob |Byte[] |
| 布林 |Boolean |
| char |String |
| 日期 |Datetime |
| Datetime |Datetime |
| 十進位 |十進位 |
| 雙精度 |兩倍 |
| 兩倍 |兩倍 |
| 列舉 |String |
| float |單一 |
| 不帶正負號的 int |Int64 |
| int |Int32 |
| 不帶正負號的整數 |Int64 |
| integer |Int32 |
| 長 varbinary |Byte[] |
| 長 varchar |String |
| longblob |Byte[] |
| longtext |String |
| mediumblob |Byte[] |
| 不帶正負號的 mediumint |Int64 |
| mediumint |Int32 |
| mediumtext |String |
| numeric |十進位 |
| real |兩倍 |
| set |String |
| 不帶正負號的 smallint |Int32 |
| smallint |Int16 |
| 文字 |String |
| 分析 |時間範圍 |
| timestamp |Datetime |
| tinyblob |Byte[] |
| 不帶正負號的 tinyint |Int16 |
| tinyint |Int16 |
| tinytext |String |
| varchar |String |
| 年 |int |

## <a name="map-source-toosink-columns"></a>將來源 toosink 資料行對應
toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。

## <a name="repeatable-read-from-relational-sources"></a>從關聯式來源進行可重複的讀取
複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。 在 Azure Data Factory 中，您可以手動重新執行配量。 您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。 當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。 請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。

## <a name="performance-and-tuning"></a>效能和微調
請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。
