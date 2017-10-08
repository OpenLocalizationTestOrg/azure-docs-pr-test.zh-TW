---
title: "aaaCopy 資料從 Oracle 使用 Data Factory 的 / |Microsoft 文件"
description: "了解如何 toocopy 資料從 Oracle 資料庫，則使用內部 Azure Data Factory。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: adb6d5fbe38e18791616ac77e8179970bbea37fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a>使用 Azure Data Factory 從內部部署 Oracle 來回複製資料
本文說明如何 toouse hello Azure Data Factory toomove 資料從內部部署 Oracle 資料庫中的複製活動。 它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。

## <a name="supported-scenarios"></a>支援的案例
您可以將資料複製**從 Oracle 資料庫**toohello 下列資料存放區：

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

您可以將資料複製下列資料存放區的 hello **tooan Oracle 資料庫**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a>必要條件
Data Factory 支援使用 hello 資料管理閘道的連線 tooon 內部部署 Oracle 來源。 請參閱[資料管理閘道器](data-factory-data-management-gateway.md)資料管理閘道的相關文章 toolearn 和[將資料從內部部署 toocloud 移](data-factory-move-data-between-onprem-and-cloud.md)文件以取得逐步指示，說明設定 hello 閘道在資料管線toomove 資料。

即使 hello Oracle 裝載於 Azure IaaS VM 需要閘道。 您可以在 hello 相同 IaaS VM 做為 hello 資料儲存或不同的 VM 只要 hello 閘道上可以連接 toohello 資料庫上安裝 hello 閘道。

> [!NOTE]
> 如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。

## <a name="supported-versions-and-installation"></a>支援的版本和安裝
此 Oracle 連接器支援兩種驅動程式版本︰

- **Oracle （建議選項） 的 Microsoft 驅動程式**： 從資料管理閘道器版本 2.7，Microsoft 驅動程式安裝適用於 Oracle 的自動與 hello 閘道，所以您不需要順序的 tooadditionally 控制代碼 hello 驅動程式tooestablish 連線 tooOracle，而且您也會發生較佳複製的效能，使用此驅動程式。 支援以下版本的 Oracle 資料庫︰
    - Oracle 12c R1 (12.1)
    - Oracle 11g R1、R2 (11.1、11.2)
    - Oracle 10g R1、R2 (10.1、10.2)
    - Oracle 9i R1、R2 (9.0.1、9.2)
    - Oracle 8i R3 (8.1.7)

> [!IMPORTANT]
> 目前 Oracle 的 Microsoft 驅動程式僅支援從 Oracle，但不是撰寫 tooOracle 複製資料。 並注意 hello 測試連線能力資料管理閘道診斷 索引標籤中的不支援此驅動程式。 或者，您可以使用 hello 複製精靈 toovalidate hello 連線。
>

- **適用於.NET 的 oracle 資料提供者：**您也可以選擇從 toouse Oracle 資料提供者 toocopy 資料 / tooOracle。 此元件包含於 [適用於 Windows 的 Oracle 資料存取元件](http://www.oracle.com/technetwork/topics/dotnet/downloads/)中。 Hello hello 閘道安裝所在的電腦上安裝 hello 適當版本 （32/64 位元）。 [Oracle 資料提供者.NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149)可以存取 tooOracle Database 10g Release 2 或更新版本。

    如果您選擇 「 XCopy 安裝 」，請遵循 hello readme.htm 中的步驟。 我們建議您選擇 hello 安裝程式與 UI (非-XCopy 一個)。

    安裝 hello 提供者之後,**重新啟動**hello 使用 [服務] 小程式 （或） 資料管理閘道組態管理員在電腦上的資料管理閘道主機服務。  

如果您使用複製精靈 tooauthor hello 複製管線，hello 驅動程式類型將會自動決定。 預設將會使用 Microsoft 驅動程式，除非您的閘道版本低於 2.7 或您選擇使用 Oracle 作為接收 (Sink)。

## <a name="getting-started"></a>開始使用
您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出內部部署的 Oracle 資料庫。

最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。 請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。

您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。

無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:

1. 建立 **Data Factory**。 資料處理站可包含一或多個管線。 
2. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。 例如，如果您從 Azure blob 儲存體 Oralce 資料庫 tooan 複製資料，您建立兩個連結的服務 toolink Oracle 資料庫和 Azure 儲存體帳戶 tooyour 資料 factory。 連結的服務是特定 tooOracle 的內容，請參閱[連結服務屬性](#linked-service-properties)> 一節。
3. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。 在 hello hello 最後一個步驟中所述的範例，您可以建立資料集 toospecify hello 資料表包含 hello 輸入的資料的 Oracle 資料庫中。 建立另一個資料集 toospecify hello blob 容器及保存 hello 資料 hello 資料夾 hello 從 Oracle 資料庫複製。 資料集是特定 tooOracle 的屬性，請參閱[資料集屬性](#dataset-properties)> 一節。
4. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。 在先前所述 hello 範例中，您使用 OracleSource 作為來源和 BlobSink 做為接收器 hello 複製活動。 同樣地，如果您要從 Azure Blob 儲存體 tooOracle 資料庫複製，請使用 BlobSource 和 OracleSink hello 複製活動中。 複製活動特定 tooOracle 資料庫的內容，請參閱[複製活動屬性](#copy-activity-properties)> 一節。 如需如何 toouse 的資料存放區做為來源或接收的詳細資訊，按一下 hello hello 資料存放區上一節中的連結。 

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。  如需使用的 toocopy 資料，從內部部署 Oracle 資料庫的 Data Factory 實體的 JSON 定義的範例，請參閱[JSON 範例](#json-examples-for-copying-data-to-and-from-oracle-database)本文一節。

hello 下列各節提供有關使用的 toodefine Data Factory 實體的 JSON 屬性的詳細資料：

## <a name="linked-service-properties"></a>連結服務屬性
下表中的 hello 提供 JSON 項目特定 tooOracle 連結服務的描述。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性必須設定為： **OnPremisesOracle** |是 |
| driverType | 指定從哪一個驅動程式 toouse toocopy 資料 / tooOracle 資料庫。 允許的值為 **Microsoft** 或 **ODP** (預設值)。 如需驅動程式詳細資料，請參閱[支援的版本和安裝](#supported-versions-and-installation)一節。 | 否 |
| connectionString | 指定所需的資訊 tooconnect toohello Oracle 資料庫執行個體 hello connectionString 屬性。 | 是 |
| gatewayName | Hello 閘道名稱，是使用的 tooconnect toohello 在內部部署 Oracle 伺服器 |是 |

**範例︰使用 Microsoft 驅動程式：**
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**範例︰使用 ODP 驅動程式**

請參閱太[此站台](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/)hello 允許的格式。

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a>資料集屬性
區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。 資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (Oracle、Azure Blob、Azure 資料表等)。

hello typeProperties 章節是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置的相關資訊。 hello 資料集 」 的型別 OracleTable 中的 hello typeProperties 區段具有下列屬性的 hello:

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |Hello hello 連結的服務的 Oracle 資料庫中的 hello 資料表名稱參考。 |否 (如果已指定 **OracleSource** 的 **oracleReaderQuery**) |

## <a name="copy-activity-properties"></a>複製活動屬性
區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。 屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。

> [!NOTE]
> hello 複製活動會採用只有 1 個輸入，並產生一個輸出。

而 hello 活動 hello typeProperties 區段中可用的屬性會隨每個活動類型。 複製活動它們而異的來源與接收的 hello 類型。

### <a name="oraclesource"></a>oracleReaderQuery
複製活動中，當 hello 來源的類型為**OracleSource** hello 下列屬性可用於**typeProperties** > 一節：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| oracleReaderQuery |使用自訂查詢 tooread hello 的資料。 |SQL 查詢字串。 例如：select * from MyTable <br/><br/>如果未指定，hello 執行的 SQL 陳述式： 選取 * from MyTable |否 (如果已指定 **dataset** 的 **tableName**) |

### <a name="oraclesink"></a>管線
**OracleSink**支援 hello 下列屬性：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| writeBatchTimeout |在逾時之前，請等待 hello 批次插入作業 toocomplete 時間。 |時間範圍<br/><br/> 範例：00:30:00 (30 分鐘)。 |否 |
| writeBatchSize |當 hello 緩衝區大小到達叫用 writeBatchSize 時，請將資料插入 hello SQL 資料表。 |整數 (資料列數目) |否 (預設值：100) |
| sqlWriterCleanupScript |複製活動 tooexecute 查詢指定的特定配量的資料清除。 |查詢陳述式。 |否 |
| sliceIdentifierColumnName |指定資料行名稱複製活動 toofill 與自動產生配量識別項，也就是使用的 tooclean 何時重新執行的特定配量的資料。 |資料類型為 binary(32) 之資料行的資料行名稱。 |否 |

## <a name="json-examples-for-copying-data-tooand-from-oracle-database"></a>從 Oracle 資料庫複製資料 tooand JSON 範例
hello 下列範例將提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。 它們會顯示如何從 toocopy 資料 / tooan Oracle 資料庫至 azure 或從 Azure Blob 儲存體。 不過，資料可以複製的 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。   

## <a name="example-copy-data-from-oracle-tooazure-blob"></a>範例： 從 Oracle tooAzure Blob 複製資料

hello 範例具有下列資料 factory 實體的 hello:

1. [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties)類型的連結服務。
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
3. [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
5. 具有使用 [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) 做為來源和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 做為接收之複製活動的[管線](data-factory-create-pipelines.md)。

hello 範例從內部部署 Oracle 資料庫 tooa blob 中的資料表複製資料的每小時。 如需有關 hello 範例中所使用的各種屬性的詳細資訊，請參閱文件中後面 hello 範例的章節。

**Oracle 連結服務：**

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Azure Blob 儲存體連結服務：**

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

**Oracle 輸入資料集：**

hello 範例假設已在 Oracle 中建立資料表"MyTable"，而且包含稱為"timestampcolumn 「 時間序列資料的資料行。

設定"external":"true"會通知 hello Data Factory 服務的 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時。

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2014-02-27T12:00:00",
            "frequency": "Hour"
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

資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。 hello 資料夾路徑和檔案名稱 hello blob 會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。

```json
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

**具有複製活動的管線：**

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為每小時排程的 toorun。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**OracleSource**和**接收**類型設定得**BlobSink**。  使用指定的 hello SQL 查詢**oracleReaderQuery**屬性選取 hello 資料在過去小時 toocopy hello。

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "OracleSource",
                        "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

## <a name="example-copy-data-from-azure-blob-toooracle"></a>範例： 將資料從 Azure Blob tooOracle 複製
這個範例示範如何從 Azure Blob 儲存體 tooan toocopy 資料內部部署 Oracle 資料庫。 不過，資料可以複製**直接**從任何所述的 hello 來源[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。  

hello 範例具有下列資料 factory 實體的 hello:

1. [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties)類型的連結服務。
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
3. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4. [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
5. 具有使用 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 做為來源和 [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) 做為接收之複製活動的[管線](data-factory-create-pipelines.md)。

hello 範例將資料從內部部署 Oracle 資料庫中的 blob tooa 資料表的每個小時。 如需有關 hello 範例中所使用的各種屬性的詳細資訊，請參閱文件中後面 hello 範例的章節。

**Oracle 連結服務：**
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Azure Blob 儲存體連結服務：**
```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

**Azure Blob 輸入資料集**

每小時從新的 Blob 挑選資料 (頻率：小時，間隔：1)。 hello 資料夾路徑和檔案名稱 hello blob 會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 年、 月和日的部分 hello 開始時間，會使用 hello 資料夾路徑和檔案名稱會使用 hello hello 開始時間的小時部分。 "external":"true"的設定會在這個資料表是外部 toohello 資料處理站，而不產生 hello data factory 中的活動時通知 hello Data Factory 服務。

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
            "frequency": "Day",
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

**Oracle 輸出資料集：**

hello 範例假設您有在 Oracle 中建立資料表"MyTable"。 建立 hello 資料表與 Oracle 中如預期般 hello Blob CSV 檔案 toocontain hello 相同數目的資料行。 新的資料列會加入 toohello 資料表的每個小時。

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

**具有複製活動的管線：**

hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**BlobSource**和 hello**接收**類型設定得**OracleSink**。  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "OracleSink"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
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


## <a name="troubleshooting-tips"></a>疑難排解秘訣
### <a name="problem-1-net-framework-data-provider"></a>問題 1：.NET Framework Data Provider

您會看到下列 hello**錯誤訊息**:

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable toofind hello requested .Net Framework Data Provider. It may not be installed”.  

**可能的原因：**

1. 未安裝.NET Framework Data Provider for Oracle hello。
2. hello Oracle 的.NET Framework 資料提供者已安裝的 too.NET Framework 2.0 和.NET Framework 4.0 hello 資料夾中找不到。

**解析/因應措施：**

1. 如果您尚未安裝 hello.NET Provider for Oracle，[安裝](http://www.oracle.com/technetwork/topics/dotnet/downloads/)，然後重試 hello 案例。
2. 如果您收到 hello 錯誤即使安裝 hello 提供者之後，請下列步驟 hello:
   1. 從 hello 資料夾開啟的.NET 2.0 的機器組態： <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config。
   2. 搜尋**適用於.NET 的 Oracle 資料提供者**，而且 hello 遵循底下的範例所示，您應該要能夠 toofind 項目**system.data** -> **DbProviderFactories**:"<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="適用於.NET 的 oracle 資料提供者" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" />」的作法指南。
3. 將這個項目 toohello machine.config 檔案複製 hello 遵循 v4.0 資料夾中： <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config，並變更 hello 版本 too4.xxx.x.x。
4. 執行 hello 全域組件快取 (GAC) 中安裝 「 < ODP.NET 安裝路徑 > \11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll" `gacutil /i [provider path]`。 # # 疑難排解秘訣

### <a name="problem-2-datetime-formatting"></a>問題 2︰日期時間格式

您會看到下列 hello**錯誤訊息**:

    Message=Operation failed in Oracle Database with hello following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

**解析/因應措施：**

您可能需要 tooadjust hello 查詢字串，在您根據在 Oracle 資料庫中，日期的設定方式 hello 下列所示的複製活動中 （使用 hello 使用 to_date 函式） 的範例：

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a>Oracle 的類型對應
Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)複製活動的文件以 hello 遵循 2 步驟方法執行從來源類型 toosink 類型的自動類型轉換：

1. 從原生的來源類型 too.NET 類型轉換
2. 從.NET 型別 toonative 接收器類型轉換

當您從 Oracle 移動資料，從 Oracle 資料型別 too.NET 型別，反之亦然，會使用下列對應的 hello。

| Oracle 資料類型 | .NET Framework 資料類型 |
| --- | --- |
| BFILE |Byte[] |
| BLOB |Byte[] |
| CHAR |String |
| CLOB |String |
| 日期 |DateTime |
| FLOAT |Decimal，字串 (如果精確度 > 28) |
| INTEGER |Decimal，字串 (如果精確度 > 28) |
| 間隔年 tooMONTH |Int32 |
| 間隔日期 tooSECOND |時間範圍 |
| 長 |String |
| 長 RAW |Byte[] |
| NCHAR |String |
| NCLOB |String |
| 數字 |Decimal，字串 (如果精確度 > 28) |
| NVARCHAR2 |String |
| RAW |Byte[] |
| ROWID |String |
| 時間戳記 |DateTime |
| 本地時區的時間戳記 |DateTime |
| 時區的時間戳記 |DateTime |
| 不帶正負號的整數 |數字 |
| VARCHAR2 |String |
| XML |String |

> [!NOTE]
> 資料型別**INTERVAL YEAR tooMONTH**和**INTERVAL DAY tooSECOND**時使用 Microsoft 驅動程式不支援。

## <a name="map-source-toosink-columns"></a>將來源 toosink 資料行對應
toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。

## <a name="repeatable-read-from-relational-sources"></a>從關聯式來源進行可重複的讀取
複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。 在 Azure Data Factory 中，您可以手動重新執行配量。 您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。 當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。 請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。

## <a name="performance-and-tuning"></a>效能和微調
請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。
