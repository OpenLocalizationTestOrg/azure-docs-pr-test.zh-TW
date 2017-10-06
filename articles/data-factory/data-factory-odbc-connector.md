---
title: "從 ODBC 資料存放區 aaaMove 資料 |Microsoft 文件"
description: "深入了解如何從 ODBC 資料 toomove 資料存放區使用 Azure Data Factory。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a>使用 Azure Data Factory 從 ODBC 資料存放區移動資料
本文說明如何儲存在 Azure Data Factory toomove 資料從內部部署 ODBC 資料 toouse hello 複製活動。 它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。

您可以從 ODBC 資料存放區支援 tooany 接收資料存放區複製資料。 取得一份資料存放區支援接收由 hello 複製活動時，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。 目前資料處理站都會支援只移動從 ODBC 資料的資料存放區 tooother 資料存放區，但不適用於將資料從其他資料存放區 tooan ODBC 資料存放區。 

## <a name="enabling-connectivity"></a>啟用連線
資料 Factory 服務支援使用 hello 資料管理閘道的連線 tooon 內部部署 ODBC 來源。 請參閱[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)文章 toolearn 有關資料管理閘道器和 hello 閘道設定的逐步指示。 使用 hello 閘道 tooconnect tooan ODBC 資料存放區，即使它裝載於 Azure IaaS VM。

您可以在 hello 相同的內部部署電腦或 hello 做 hello ODBC 資料存放區的 Azure VM 上安裝 hello 閘道。 不過，我們建議您在個別機器/Azure IaaS VM 上安裝 hello 閘道 tooavoid 資源爭用和較佳的效能。 當您在不同電腦上安裝 hello 閘道時，hello 部應該能夠 tooaccess hello 機器 hello ODBC 資料存放區。

除了 hello 資料管理閘道器，您也需要 tooinstall hello ODBC 驅動程式 hello hello 閘道機器上的資料存放區。

> [!NOTE]
> 如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。

## <a name="getting-started"></a>開始使用
您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從 ODBC 資料存放區移動資料。

最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。 請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。

您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。 

無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello: 

1. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。
2. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。 
3. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。 

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。  使用 Data Factory 實體的 ODBC 資料存放區中的使用的 toocopy 資料的 JSON 定義中的範例，請參閱[JSON 範例： 從 ODBC 資料的複本資料存放區 tooAzure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob)本文一節。 

hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooODBC 資料存放區的 JSON 屬性的詳細資料：

## <a name="linked-service-properties"></a>連結服務屬性
下表中的 hello 提供 JSON 項目特定 tooODBC 連結服務的描述。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性必須設定為： **OnPremisesOdbc** |是 |
| connectionString |hello 非存取認證部分 hello 連接字串和選擇性的加密認證。 請參閱下列各節的 hello 範例。 |是 |
| 認證 |hello 存取認證的 hello 驅動程式特有的屬性值的格式指定的連接字串部分。 範例：“Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”。 |否 |
| authenticationType |Tooconnect toohello ODBC 資料存放區使用的驗證類型。 可能的值為：Anonymous 和 Basic。 |是 |
| username |如果您要使用 Basic 驗證，請指定使用者名稱。 |否 |
| password |指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。 |否 |
| gatewayName |Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello ODBC 資料存放區。 |是 |

### <a name="using-basic-authentication"></a>使用基本驗證

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a>使用基本驗證與加密認證
您可以加密使用 hello hello 認證[新增 AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) （1.0 版本的 Azure PowerShell） 指令程式或[New-azuredatafactoryencryptvalue](https://msdn.microsoft.com/library/dn834940.aspx) （0.9 或更早版本的 helloAzure PowerShell)。  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a>使用匿名驗證

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a>資料集屬性
區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。 資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。

hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。 hello typeProperties 區段類型的資料集**RelationalTable** （包括 ODBC 的資料集） 具有下列屬性的 hello

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |Hello ODBC 資料存放區中的 hello 資料表的名稱。 |是 |

## <a name="copy-activity-properties"></a>複製活動屬性
區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。 屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。

屬性用於 hello **typeProperties** > 一節的 hello hello 活動另一方面會隨每個活動類型。 複製活動它們而異的來源與接收的 hello 類型。

複製活動中，當來源的類型為**RelationalSource** （包括 ODBC），下列屬性的 hello 可用 typeProperties 區段中：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| query |使用自訂查詢 tooread hello 的資料。 |SQL 查詢字串。 例如：select * from MyTable。 |是 |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a>JSON 範例： 從 ODBC 資料的複本資料存放區 tooAzure Blob
此範例中提供的 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。 它會顯示如何從 ODBC toocopy 資料來源 tooan Azure Blob 儲存體。 不過，資料可以複製的 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。

hello 範例具有下列資料 factory 實體的 hello:

1. [OnPremisesOdbc](#linked-service-properties)類型的連結服務。
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。
3. [RelationalTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。
5. 具有使用 [RelationalSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。

hello 範例將資料從 ODBC 資料存放區 tooa blob 中的查詢結果的每個小時。 這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。

第一個步驟中，設定 hello 資料管理閘道器。 hello 中的 hello 指示[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。

**ODBC 的連結服務**本例使用 hello 基本驗證。 請參閱 [ODBC 連結服務](#linked-service-properties) 章節以了解您可以使用的各種不同類型的驗證。

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
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

**ODBC 輸入資料集**

hello 範例假設您已建立資料表"MyTable"中的 ODBC 資料庫而且包含稱為"timestampcolumn 「 時間序列資料的資料行。

設定"external":"true"會通知 hello Data Factory 服務的 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時。

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
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

資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。 hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。 hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


**具有 ODBC 來源 (RelationalSource) 和 Blob 接收器 (BlobSink) 的管線中複製活動**

hello 管線包含複製活動的設定的 toouse 這些輸入和輸出資料集，而排程的 toorun 每小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**RelationalSource**和**接收**類型設定得**BlobSink**。 指定 hello SQL 查詢**查詢**屬性選取 hello 資料在過去小時 toocopy hello。

```json
{
    "name": "CopyODBCToBlob",
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
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
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
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a>ODBC 的類型對應
Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)發行項，複製活動會執行自動類型轉換來源類型 toosink 類型以下列兩種方法的 hello:

1. 從原生的來源類型 too.NET 類型轉換
2. 從.NET 型別 toonative 接收器類型轉換

當從 ODBC 資料存放區移動資料時，ODBC 資料類型會對應的 too.NET 類型 hello 中所述[ODBC 資料類型對應](https://msdn.microsoft.com/library/cc668763.aspx)主題。

## <a name="map-source-toosink-columns"></a>將來源 toosink 資料行對應
toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。

## <a name="repeatable-read-from-relational-sources"></a>從關聯式來源進行可重複的讀取
複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。 在 Azure Data Factory 中，您可以手動重新執行配量。 您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。 當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。 請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。

## <a name="ge-historian-store"></a>GE Historian 存放區
建立連結的 ODBC 服務 toolink [GE Proficy 歷史學家 （現在 GE 歷史學家）](http://www.geautomation.com/products/proficy-historian)資料存放區 tooan 的 Azure data factory 中 hello 下列範例所示：

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

在內部部署電腦上安裝資料管理閘道器，並向 hello 入口網站中的 hello 閘道。 在內部部署電腦上安裝的 hello 閘道 GE 歷史學家 tooconnect toohello GE 歷史學家資料存放區使用 hello ODBC 驅動程式。 因此，如果它尚未安裝 hello 閘道機器上時，才能安裝 hello 驅動程式。 如需詳細資訊，請參閱 [啟用連線](#enabling-connectivity) 一節。

使用的 hello GE 歷史學家儲存在 Data Factory 方案之前，請確認 hello 閘道是否能連接 toohello 資料存放區使用 hello 下一節中的指示。

讀取 hello 的發行項的詳細概觀 hello 從頭使用 ODBC 資料會儲存為複製作業中的來源資料存放區。  

## <a name="troubleshoot-connectivity-issues"></a>疑難排解連線問題
tootroubleshoot 連接問題，使用 hello**診斷** 索引標籤**資料管理閘道組態管理員**。

1. 啟動 **資料管理閘道器組態管理員**。 您可以執行"C:\Program Files\Microsoft 資料管理 Gateway\1.0\Shared\ConfigManager.exe 」 直接 （或） 搜尋的**閘道**toofind 連結太**Microsoft 資料管理閘道器**應用程式中 hello 下列影像所示。

    ![搜尋閘道器](./media/data-factory-odbc-connector/search-gateway.png)
2. 切換 toohello**診斷** 索引標籤。

    ![閘道診斷](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. 選取 hello**類型**的資料儲存區 （連結的服務）。
4. 指定**驗證**輸入**認證**（或） 輸入**連接字串**，是使用的 tooconnect toohello 資料存放區。
5. 按一下**測試連接**tootest hello 連接 toohello 資料存放區。

## <a name="performance-and-tuning"></a>效能和微調
請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。
