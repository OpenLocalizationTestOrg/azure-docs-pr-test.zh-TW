---
title: "將資料從 DB2 aaaMove 使用 Azure Data Factory |Microsoft 文件"
description: "了解如何使用 Azure 資料 Factory 複製活動 toomove 資料從內部部署 DB2 資料庫"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 696ac059be644cb3901c37d2fc746e0682c65a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a>使用 Azure Data Factory 複製活動從 DB2 移動資料
本文說明如何使用複製活動，以及在 Azure Data Factory toocopy 資料從內部部署 DB2 資料庫 tooa 資料存放區中。 您可以複製資料 tooany 存放區中 hello 支援接收已列為[Data Factory 資料移動活動](data-factory-data-movement-activities.md#supported-data-stores-and-formats)發行項。 本主題是根據 hello Data Factory 發行項，這會使用複製活動中呈現資料移動的概觀，並列出支援的 hello 資料存放區的組合。 

Data Factory 目前支援從 DB2 資料庫 tooa 只移動資料[支援的接收資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。 將資料從其他資料會儲存 tooa DB2 資料庫不支援。

## <a name="prerequisites"></a>必要條件
Data Factory 支援連接 tooan 在內部部署 DB2 資料庫使用 hello[資料管理閘道器](data-factory-data-management-gateway.md)。 Hello 閘道資料的逐步指示 tooset 管線 toomove 您的資料，請參閱 hello[將資料從內部部署 toocloud 移](data-factory-move-data-between-onprem-and-cloud.md)發行項。

即使 hello DB2 裝載於 Azure IaaS VM，就需要閘道。 您可以在 hello 安裝 hello 閘道相同的 IaaS VM 做為 hello 資料存放區。 如果 hello 閘道可以連接 toohello 資料庫，您可以在不同的 VM 上安裝 hello 閘道。

hello 資料管理閘道器提供內建的 DB2 驅動程式，因此您不需要 toomanually 安裝驅動程式 toocopy 資料從 DB2。

> [!NOTE]
> 如需連接與閘道問題的疑難排解秘訣，請參閱 hello[閘道問題的疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues)發行項。


## <a name="supported-versions"></a>支援的版本
hello 資料 Factory DB2 連接器支援下列 IBM DB2 平台和版本與分散式關聯式資料庫架構 (DRDA) SQL Access Manager 版本 9、 10 和 11 hello:

* IBM DB2 for z/OS 版本 11.1
* IBM DB2 for z/OS 版本 10.1
* IBM DB2 for i (AS400) 版本 7.2
* IBM DB2 for i (AS400) 版本 7.1
* IBM DB2 for Linux, UNIX, and Windows (LUW) 版本 11
* IBM DB2 for LUW 版本 10.5
* IBM DB2 for LUW 版本 10.1

> [!TIP]
> 如果您收到 hello 錯誤訊息 「 hello 套件對應 tooan SQL 陳述式執行的要求已找不到。 SQLSTATE = 51002 SQLCODE =-805，"hello 原因是 hello hello OS 上的一般使用者不會建立所需的套件。 tooresolve 這個問題，請遵循這些指示適用於您的 DB2 伺服器類型：
> - DB2 for i (AS400): 可讓建立 hello 一般使用者的 hello 集合，才能執行複製活動的進階使用者。 使用 hello 命令 toocreate hello 集合：`create collection <username>`
> - DB2 for z/OS 或 LUW： 使用高的權限的帳戶-進階使用者或系統管理員具有封裝授權單位和繫結，BINDADD，授與 EXECUTE tooPUBLIC 權限-toorun hello 複製一次。 hello 複製期間，會自動建立 hello 所需的套件。 之後，您可以在後續複製回合切換後 toohello 一般使用者。

## <a name="getting-started"></a>開始使用
您可以使用不同的工具和 Api，與從內部部署 DB2 資料存放區的複製活動 toomove 資料建立管線： 

- 最簡單方式 toocreate hello 管線為 toouse hello Azure 資料 Factory 複製精靈。 如需使用 hello 複製精靈建立管線的快速逐步解說，請參閱 hello[教學課程： 使用 hello 複製精靈建立的管線](data-factory-copy-data-wizard-tutorial.md)。 
- 您也可以使用工具 toocreate 管線，包括 hello Azure 入口網站、 Visual Studio、 Azure PowerShell、 Azure Resource Manager 範本、 hello.NET API 和 hello REST API。 如需逐步指示 toocreate 具有複製活動的管線，請參閱 hello[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。 

無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:

1. 建立連結的服務 toolink 輸入和輸出資料存放區 tooyour 資料處理站。
2. 建立資料集 toorepresent 輸入和輸出 hello 複製作業的資料。 
3. 建立管線，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。 

當您使用 hello 複製精靈，hello 連結的 Data Factory 服務的 JSON 定義資料集和管線實體會自動為您建立。 當您使用工具或 Api （除了 hello.NET 應用程式開發介面) 時，您會定義使用 hello JSON 格式的 hello Data Factory 實體。 hello [JSON 範例： 將資料從 DB2 tooAzure Blob 儲存體複製](#json-example-copy-data-from-db2-to-azure-blob)顯示 hello hello JSON 定義是使用的 toocopy 資料從內部部署 DB2 資料存放區的 Data Factory 實體。

hello 下列各節提供 hello 詳細資料會使用的 toodefine hello Data Factory 實體的特定 tooa DB2 資料存放區的 JSON 屬性。

## <a name="db2-linked-service-properties"></a>DB2 連結服務屬性
hello 下表列出特定 tooa DB2 連結服務的 hello JSON 屬性。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| **type** |這個屬性必須設定太**OnPremisesDB2**。 |是 |
| **server** |hello hello DB2 伺服器名稱。 |是 |
| **database** |hello hello DB2 資料庫名稱。 |是 |
| **schema** |hello hello DB2 資料庫中的 hello 結構描述名稱。 此屬性必須區分大小寫。 |否 |
| **authenticationType** |hello 使用的 tooconnect toohello DB2 資料庫的驗證類型。 hello 可能的值為： 匿名、 基本和 Windows。 |是 |
| **username** |如果您使用基本或 Windows 驗證的 hello 的使用者帳戶的 hello 名稱。 |否 |
| **password** |hello hello 使用者帳戶密碼。 |否 |
| **gatewayName** |hello hello Data Factory 服務的 hello 閘道名稱應該使用 tooconnect toohello 在內部部署 DB2 資料庫。 |是 |

## <a name="dataset-properties"></a>資料集屬性
如需 hello 區段和屬性都可用來定義資料集的清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。 區段，例如**結構**，**可用性**，和 hello**原則**資料集 JSON，就是類似的所有資料集類型 (Azure SQL，Azure Blob 儲存體，Azure 資料表儲存體，等等）。

hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。 hello **typeProperties**類型的資料集區段**RelationalTable**，其中包含 hello DB2 資料集，具有下列屬性的 hello:

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| **tableName** |hello 名稱 hello 連結的服務的 hello DB2 資料庫執行個體中的 hello 資料表的參考。 此屬性必須區分大小寫。 |否 (如果 hello**查詢**複製活動的型別屬性**RelationalSource**指定) |

## <a name="copy-activity-properties"></a>複製活動屬性
如需 hello 區段和屬性都可用來定義複製活動的清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。 複製活動屬性 (例如**名稱**、**描述**、**輸入**資料表、**輸出**資料表，以及**原則**) 適用於所有類型的活動。 hello，就可以在 hello 屬性**typeProperties** hello 活動的每個活動類型的區段。 複製活動，根據 hello 類型的資料來源與接收 hello 屬性而有所不同。

複製活動，當 hello 來源類型的**RelationalSource** （包括 DB2），下列屬性的 hello 位於 hello **typeProperties** > 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| **查詢** |使用 hello 自訂查詢 tooread hello 資料。 |SQL 查詢字串。 例如：`"query": "select * from "MySchema"."MyTable""` |否 (如果 hello **tableName**指定屬性的資料集) |

> [!NOTE]
> 結構描述和資料表名稱會區分大小寫。 Hello 查詢陳述式中，括住屬性名稱使用""（雙引號）。 例如：
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-tooazure-blob-storage"></a>JSON 範例： 將資料從 DB2 tooAzure Blob 儲存體複製
此範例中提供的範例 JSON 定義，您可以使用 toocreate 管線使用 hello [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)， [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)，或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。 hello 範例將示範如何 toocopy 資料從 DB2 資料庫 tooBlob 儲存體。 但是，太複製資料[任何支援的資料儲存接收器類型](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 Azure 資料 Factory 複製活動。

hello 範例有下列 Data Factory 實體的 hello:

- [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)類型的 DB2 連結服務
- [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 類型的 Azure Blob 儲存體連結服務
- [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)
- [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)
- A[管線](data-factory-create-pipelines.md)與使用 hello 複製活動[RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties)和[BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)屬性

hello 範例從查詢結果中的 DB2 資料庫 tooan Azure blob 複製資料的每小時。 hello 以下各節 hello 實體定義說明 hello hello 範例中使用的 JSON 屬性。

第一個步驟是安裝和設定資料閘道。 Hello 中會有指示[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。

**DB2 連結服務**

```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
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

**Azure Blob 儲存體連結服務**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

**DB2 輸入資料集**

hello 範例假設您已在名為"MyTable"已標示為"timestamp"hello 時間序列資料的資料行的 DB2 中建立資料表。

hello**外部**屬性設定太"，則為 true。 」 此資料集是外部 toohello 資料處理站，並不產生 hello data factory 中的活動時，此設定就會通知 hello Data Factory 服務。 請注意該 hello**類型**屬性設定太**RelationalTable**。


```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
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

**Azure Blob 輸出資料集**

資料寫入 tooa 新 blob 的每個小時設定 hello**頻率**屬性太 「 小時 」 和 hello**間隔**too1 屬性。 hello **folderPath**屬性會動態評估 hello blob 依據 hello 正在處理的 hello 配量的開始時間。 hello 資料夾路徑會使用 hello 的 hello 開始時間的年、 月、 日和小時部分。

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Hello 複製活動的管線**

hello 管線包含設定的複製活動 toouse 指定輸入和輸出資料集，而且是每小時排程的 toorun。 Hello hello 管線 JSON 定義中，在 hello**來源**類型設定得**RelationalSource**和 hello**接收**類型設定得**BlobSink**. 指定 hello SQL 查詢**查詢**屬性選取 hello 「 訂單 」 資料表中的 hello 資料。

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for hello copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"Orders\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
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
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a>DB2 的類型對應
Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)文件，複製活動使用 hello 下列兩個步驟的方法，執行從來源類型 toosink 類型的自動類型轉換：

1. 從原生的來源類型 tooa.NET 型別轉換
2. 從.NET 型別 tooa 原生接收類型轉換

hello 下列的對應會使用複製活動資料轉換時 hello 從 DB2 類型 tooa.NET 類型：

| DB2 資料庫類型 | .NET Framework 類型 |
| --- | --- |
| SmallInt |Int16 |
| Integer |Int32 |
| BigInt |Int64 |
| Real |單一 |
| 兩倍 |兩倍 |
| Float |兩倍 |
| 十進位 |十進位 |
| DecimalFloat |十進位 |
| 數值 |十進位 |
| Date |DateTime |
| 時間 |TimeSpan |
| Timestamp |Datetime |
| xml |Byte[] |
| Char |String |
| VarChar |String |
| LongVarChar |String |
| DB2DynArray |String |
| Binary |Byte[] |
| VarBinary |Byte[] |
| LongVarBinary |Byte[] |
| 圖形 |String |
| VarGraphic |String |
| LongVarGraphic |String |
| Clob |String |
| Blob |Byte[] |
| DbClob |String |
| SmallInt |Int16 |
| Integer |Int32 |
| BigInt |Int64 |
| Real |單一 |
| 兩倍 |兩倍 |
| Float |兩倍 |
| 十進位 |十進位 |
| DecimalFloat |十進位 |
| 數值 |十進位 |
| Date |DateTime |
| 時間 |TimeSpan |
| Timestamp |Datetime |
| xml |Byte[] |
| Char |String |

## <a name="map-source-toosink-columns"></a>將來源 toosink 資料行對應
如何 toomap 資料行中 hello 來源資料集 toocolumns hello 接收的資料集，請參閱的 toolearn [Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。

## <a name="repeatable-reads-from-relational-sources"></a>從關聯式來源進行可重複的讀取
時，您從關聯式資料存放區複製資料，請注意注意 tooavoid 重複性非預期的結果。 在 Azure Data Factory 中，您可以手動重新執行配量。 您也可以設定 hello 重試**原則**屬性的資料集 toorerun 配量時發生錯誤。 請確定的 hello 相同資料如何讀取無論多次 hello 配量是重新執行，以及如何重新執行 hello 配量而定。 如需詳細資訊，請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。

## <a name="performance-and-tuning"></a>效能和微調
深入了解會影響在 hello 複製活動以及方式 toooptimize 效能 hello 效能的關鍵因素[複製活動效能和調整指南](data-factory-copy-activity-performance.md)。
