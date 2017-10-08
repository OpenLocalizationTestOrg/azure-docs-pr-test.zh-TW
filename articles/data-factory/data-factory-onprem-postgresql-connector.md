---
title: "aaaMove 資料從 PostgreSQL 使用 Azure Data Factory |Microsoft 文件"
description: "深入了解如何使用 Azure Data Factory PostgreSQL 資料庫 toomove 資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 888d9ebc-2500-4071-b6d1-0f6bd1b5997c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: ea384f4e06f7d7bedae2949e4ea727c8f8806614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a>使用 Azure Data Factory 從 PostgreSQL 移動資料
本文說明如何 toouse hello Azure Data Factory toomove 資料從內部部署 PostgreSQL 資料庫中的複製活動。 它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。

您可以從內部部署 PostgreSQL 資料存放區支援 tooany 接收資料存放區複製資料。 如需支援為接收 hello 複製活動的資料存放區的清單，請參閱[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。 資料處理站目前支援將資料從 PostgreSQL 資料庫 tooother 資料存放區，但是不會將資料從其他資料儲存 tooan PostgreSQL 資料庫。 

## <a name="prerequisites"></a>先決條件

資料 Factory 服務支援使用 hello 資料管理閘道的連線 tooon 內部部署 PostgreSQL 來源。 請參閱[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)文章 toolearn 有關資料管理閘道器和 hello 閘道設定的逐步指示。

即使 hello PostgreSQL 資料庫裝載於 Azure IaaS VM 需要閘道。 您可以在 hello 相同 IaaS VM 做為 hello 資料儲存或不同的 VM 只要 hello 閘道上可以連接 toohello 資料庫上安裝閘道。

> [!NOTE]
> 如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。

## <a name="supported-versions-and-installation"></a>支援的版本和安裝
資料管理閘道器 tooconnect toohello PostgreSQL 資料庫，如安裝 hello [PostgreSQL Ngpsql 資料提供者](http://go.microsoft.com/fwlink/?linkid=282716)2.0.12 或上方上 hello 相同系統 hello 資料管理閘道器。 支援 PostgreSQL 版本 7.4 和以上版本。

## <a name="getting-started"></a>開始使用
您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 PostgreSQL 資料存放區移動資料。 

- 最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。 請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。 
- 您也可以使用下列工具 toocreate 管線 hello: 
    - Azure 入口網站
    - Visual Studio
    - Azure PowerShell
    - Azure Resource Manager 範本
    - .NET API
    - REST API

     請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。 

無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:

1. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。
2. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。 
3. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。 

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。  具有使用的 toocopy 資料從內部部署 PostgreSQL 資料存放區的 Data Factory 實體的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從 PostgreSQL tooAzure Blob 複製](#json-example-copy-data-from-postgresql-to-azure-blob)本文一節。 

hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooa PostgreSQL 資料存放區的 JSON 屬性的詳細資料：

## <a name="linked-service-properties"></a>連結服務屬性
下表中的 hello 提供 JSON 項目特定 tooPostgreSQL 連結服務的描述。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性必須設定為： **OnPremisesPostgreSql** |是 |
| 伺服器 |Hello PostgreSQL 伺服器的名稱。 |是 |
| 資料庫 |Hello PostgreSQL 資料庫的名稱。 |是 |
| 結構描述 |Hello hello 資料庫中的結構描述名稱。 hello 結構描述名稱會區分大小寫。 |否 |
| authenticationType |Tooconnect toohello PostgreSQL 資料庫使用的驗證類型。 可能的值為：匿名、基本和 Windows。 |是 |
| username |如果您使用基本或 Windows 驗證，請指定使用者名稱。 |否 |
| password |指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。 |否 |
| gatewayName |Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 PostgreSQL 資料庫。 |是 |

## <a name="dataset-properties"></a>資料集屬性
區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。 資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型。

hello typeProperties 章節是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置的相關資訊。 hello typeProperties 區段類型的資料集**RelationalTable** （包括 PostgreSQL 資料集） 具有下列屬性的 hello:

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |Hello PostgreSQL 資料庫連結的服務參考的執行個體中的 hello 資料表的名稱。 hello tableName 是區分大小寫。 |否 (如果已指定 **RelationalSource** 的 **query**) |

## <a name="copy-activity-properties"></a>複製活動屬性
區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。 屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。

而 hello 活動 hello typeProperties 區段中可用的屬性會隨每個活動類型。 複製活動它們而異的來源與接收的 hello 類型。

當來源屬於型別**RelationalSource** （包括 PostgreSQL），下列屬性的 hello 可用 typeProperties 區段中：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| query |使用自訂查詢 tooread hello 的資料。 |SQL 查詢字串。 例如："query": "select * from \"MySchema\".\"MyTable\""。 |否 (如果已指定 **dataset** 的 **tableName**) |

> [!NOTE]
> 結構描述和資料表名稱會區分大小寫。 括住在`""`（雙引號） hello 查詢中。  

**範例：**

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-tooazure-blob"></a>JSON 範例： 從 PostgreSQL tooAzure Blob 複製資料
此範例中提供的範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。 它們會顯示如何 toocopy 資料從 PostgreSQL 資料庫 tooAzure Blob 儲存體。 不過，資料可以複製的 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。   

> [!IMPORTANT]
> 此範例提供 JSON 程式碼片段。 它不包含建立 hello 資料處理站的逐步指示。 如需逐步指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。

hello 範例具有下列資料 factory 實體的 hello:

1. [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties)類型的連結服務。
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
3. [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
5. hello[管線](data-factory-create-pipelines.md)與使用複製活動[RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties)和[BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)。

hello 範例將資料從 PostgreSQL 資料庫 tooa blob 中的查詢結果的每個小時。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

第一個步驟中，安裝程式 hello 資料管理閘道器。 hello 中的 hello 指示[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。

**PostgreSQL 連結服務：**

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
**Azure Blob 儲存體連結服務：**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
    }
    }
}
```
**PostgreSQL 輸入資料集：**

hello 範例假設您已建立資料表"MyTable"中 PostgreSQL 而且包含稱為"timestamp"時間序列資料的資料行。

設定`"external": true`該 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時，會通知 hello Data Factory 服務。

```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
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

資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。 hello 資料夾路徑和檔案名稱 hello blob 會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。

```json
{
    "name": "AzureBlobPostgreSqlDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/postgresql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為每小時排程的 toorun。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**RelationalSource**和**接收**類型設定得**BlobSink**。 指定 hello SQL 查詢**查詢**屬性選取 hello PostgreSQL 資料庫中的 hello public.usstates 資料表中的 hello 資料。

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"public\".\"usstates\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "PostgreSqlDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobPostgreSqlDataSet"
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
                "name": "PostgreSqlToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
## <a name="type-mapping-for-postgresql"></a>PostgreSQL 的類型對應
Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)複製活動的文件以 hello 遵循 2 步驟方法執行從來源類型 toosink 類型的自動類型轉換：

1. 從原生的來源類型 too.NET 類型轉換
2. 從.NET 型別 toonative 接收器類型轉換

當您移動資料 tooPostgreSQL，hello 下列會使用對應從 PostgreSQL 類型 too.NET 型別。

| PostgreSQL 資料庫類型 | PostgresSQL 別名 | .NET Framework 類型 |
| --- | --- | --- |
| abstime | |Datetime | &nbsp;
| bigint |int8 |Int64 |
| bigserial |serial8 |Int64 |
| 位元 [ (n) ] | |Byte[]、String | &nbsp;
| 位元不同 [ (n) ] |varbit |Byte[]、String |
| 布林值 |布林 |布林值 |
| 方塊 | |Byte[]、String |&nbsp;
| bytea | |Byte[]、String |&nbsp;
| 字元 [ (n) ] |char [ (n) ] |String |
| 字元不同 [ (n) ] |varchar [ (n) ] |String |
| cid | |String |&nbsp;
| cidr | |String |&nbsp;
| 圓形 | |Byte[]、String |&nbsp;
| 日期 | |Datetime |&nbsp;
| daterange | |String |&nbsp;
| 雙精度 |float8 |兩倍 |
| inet | |Byte[]、String |&nbsp;
| intarry | |String |&nbsp;
| int4range | |String |&nbsp;
| int8range | |String |&nbsp;
| integer |int, int4 |Int32 |
| 間隔 [ 欄位 ] [ (p) ] | |Timespan |&nbsp;
| json | |String |&nbsp;
| jsonb | |Byte[] |&nbsp;
| 線條 | |Byte[]、String |&nbsp;
| lseg | |Byte[]、String |&nbsp;
| macaddr | |Byte[]、String |&nbsp;
| money | |十進位 |&nbsp;
| 數值 [ (p, s) ] |十進位 [ (p, s) ] |十進位 |
| numrange | |String |&nbsp;
| oid | |Int32 |&nbsp;
| 路徑 | |Byte[]、String |&nbsp;
| pg_lsn | |Int64 |&nbsp;
| 點 | |Byte[]、String |&nbsp;
| 多邊形 | |Byte[]、String |&nbsp;
| real |float4 |單一 |
| smallint |int2 |Int16 |
| smallserial |serial2 |Int16 |
| serial |serial4 |Int32 |
| 文字 | |String |&nbsp;

## <a name="map-source-toosink-columns"></a>將來源 toosink 資料行對應
toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。

## <a name="repeatable-read-from-relational-sources"></a>從關聯式來源進行可重複的讀取
複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。 在 Azure Data Factory 中，您可以手動重新執行配量。 您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。 當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。 請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。

## <a name="performance-and-tuning"></a>效能和微調
請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。
