---
title: "將資料從 Salesforce aaaMove 使用 Data Factory |Microsoft 文件"
description: "深入了解如何將資料從 Salesforce toomove 使用 Azure Data Factory。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: c1bde2a333f5a3c0a995eb8c13ecf585132888b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a>使用 Azure Data Factory 從 Salesforce 移動資料
本文概述如何使用複製活動，以及在 Azure data factory toocopy 資料從 Salesforce tooany 資料存放區中 hello hello 接收的資料行底下所列[支援來源與接收](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。 這篇文章是根據 hello[資料移動活動](data-factory-data-movement-activities.md)文件，複製活動與支援的資料存放區組合顯示的資料移動的一般概觀。

Azure Data Factory 目前只支援將資料從 Salesforce 移過[支援接收資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)，但不支援從其他資料存放區 tooSalesforce 移動資料。

## <a name="supported-versions"></a>支援的版本
此連接器支援下列 Salesforce 的版本中的 hello: Developer Edition、 專業版、 企業版或無限制的版本。 並且支援從 Salesforce 生產、沙箱和自訂網域複製。

## <a name="prerequisites"></a>必要條件
* 必須啟用 API 權限。 請參閱 [如何在 Salesforce 中透過權限集啟用 API 存取權？](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)
* 從 Salesforce tooon 內部部署資料存放區 toocopy 資料，您必須至少在內部部署環境中安裝資料管理閘道器 2.0。

## <a name="salesforce-request-limits"></a>Salesforce 要求限制
Salesforce 對於 API 要求總數和並行 API 要求均有限制。 請注意下列點 hello:

- 如果 hello 並行要求數目超過 hello 限制，就會發生節流，而且您會看到隨機失敗。
- 如果 hello 的總要求數超出 hello 限制，hello 的 Salesforce 帳戶會被封鎖 24 小時。

您也可能會收到 hello"REQUEST_LIMIT_EXCEEDED 」 錯誤，這兩種案例中。 請參閱 hello hello"應用程式開發介面要求的限制 」 一節[Salesforce 開發人員限制](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf)文件以取得詳細資料。

## <a name="getting-started"></a>開始使用
您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從 Salesforce 移動資料。

最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。 請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。

您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。 請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。 

無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello: 

1. 建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。
2. 建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。 
3. 建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。 

當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。 當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。  具有使用的 toocopy 資料來自 Salesforce 的 Data Factory 實體的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從 Salesforce tooAzure Blob 複製](#json-example-copy-data-from-salesforce-to-azure-blob)本文一節。 

hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooSalesforce 的 JSON 屬性的詳細資料： 

## <a name="linked-service-properties"></a>連結服務屬性
hello 下表提供說明是特定 toohello Salesforce 連結服務的 JSON 元素。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| 類型 |hello 類型屬性必須設定為： **Salesforce**。 |是 |
| environmentUrl | 指定 hello URL 的 Salesforce 執行個體。 <br><br> - 預設值為 " https://login.salesforce.com "。 <br> -從沙箱，toocopy 資料指定"https://test.salesforce.com"。 <br> -toocopy 資料從自訂網域，指定，例如，"https://[domain].my.salesforce.com"。 |否 |
| username |指定 hello 使用者帳戶的使用者名稱。 |是 |
| password |指定 hello 使用者帳戶的密碼。 |是 |
| securityToken |指定 hello 使用者帳戶的安全性權杖。 請參閱[取得安全性權杖](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm)如需有關指示 tooreset 取得安全性權杖。 一般情況下，請參閱關於安全性權杖的 toolearn[安全性和 hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm)。 |是 |

## <a name="dataset-properties"></a>資料集屬性
區段和屬性都可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。 資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。

hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。 hello typeProperties 區段 hello 類型的資料集**RelationalTable**具有下列屬性的 hello:

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| tableName |在 Salesforce 中的 hello 資料表的名稱。 |否 (如果已指定 **RelationalSource** 的 **query**) |

> [!IMPORTANT]
> hello"__c"hello API 名稱部分所需的任何自訂的物件。

![Data Factory - Salesforce 連線 - API 名稱](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a>複製活動屬性
區段和屬性都可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。 名稱、描述、輸入和輸出資料表以及各種原則等屬性都適用於所有活動類型。

中可用的 hello 屬性 hello typeProperties > 一節的 hello 活動 hello 另一方面，每個活動類型而有所不同。 複製活動它們而異的來源與接收的 hello 類型。

複製活動中，當 hello 來源 hello 型別的**RelationalSource** （包括 Salesforce），下列屬性的 hello 可用 typeProperties 區段中：

| 屬性 | 說明 | 允許的值 | 必要 |
| --- | --- | --- | --- |
| query |使用自訂查詢 tooread hello 的資料。 |SQL-92 查詢或 [Salesforce 物件查詢語言 (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) 查詢。 例如：`select * from MyTable__c`。 |否 (如果 hello **tableName**的 hello**資料集**指定) |

> [!IMPORTANT]
> hello"__c"hello API 名稱部分所需的任何自訂的物件。

![Data Factory - Salesforce 連線 - API 名稱](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a>查詢秘訣
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a>在 DateTime 資料行上使用 Where 子句來擷取資料
何時指定 hello SOQL 或 SQL 查詢，請注意 toohello 日期時間格式的差異。 例如：

* **SOQL 範例**：`$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`
* **SQL 範例**：
    * **使用複製精靈 toospecify hello 查詢：**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`
    * **使用 JSON 編輯 toospecify hello 查詢 （逸出字元正確）：**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`

### <a name="retrieving-data-from-salesforce-report"></a>從 Salesforce 報表擷取資料
例如，您可以藉由以 `{call "<report name>"}` 方式指定查詢，從 Salesforce 報表擷取資料。 `"query": "{call \"TestReport\"}"`。

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a>從 Salesforce 資源回收筒擷取已刪除的記錄
來自 Salesforce 的 資源回收筒 tooquery hello 虛刪除記錄，您可以指定**"IsDeleted = 1"**在查詢中。 例如，

* tooquery 只有 hello 刪除記錄，會指定 「 選取 * 從 MyTable__c**其中 IsDeleted = 1**"
* 所有 hello 記錄包括現有的 hello 和刪除，hello tooquery 指定 「 選取 * 從 MyTable__c**其中 IsDeleted = 0 或 IsDeleted = 1**"

## <a name="json-example-copy-data-from-salesforce-tooazure-blob"></a>JSON 範例： 從 Salesforce tooAzure Blob 複製資料
hello 下列範例將提供範例 JSON 定義，您可以使用 toocreate 管線使用 hello [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)， [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)，或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。 它們會顯示如何從 Salesforce tooAzure Blob 儲存體 toocopy 資料。 不過，資料可以複製的 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。   

以下是您將需要 toocreate tooimplement hello 案例 hello Data Factory 成品。 hello 以下各節 hello 清單提供關於這些步驟的詳細資料。

* 連結的類型之服務的 hello [Salesforce](#linked-service-properties)
* 連結的類型之服務的 hello [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* 輸入[資料集](data-factory-create-datasets.md)hello 型別的[RelationalTable](#dataset-properties)
* 輸出[資料集](data-factory-create-datasets.md)hello 型別的[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
* 具有使用 [RelationalSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)

**Salesforce 連結服務**

這個範例會使用 hello **Salesforce**連結服務。 請參閱 hello [Salesforce 連結服務](#linked-service-properties)hello 屬性這項連結服務所支援的區段。  請參閱[取得安全性權杖](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm)如需如何 tooreset/get hello 安全性權杖的指示。

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
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
**Salesforce 輸入資料集**

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
        },
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

設定**外部**太**true**該 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時，會通知 hello Data Factory 服務。

> [!IMPORTANT]
> hello"__c"hello API 名稱部分所需的任何自訂的物件。

![Data Factory - Salesforce 連線 - API 名稱](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

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
            "folderPath": "adfgetstarted/alltypes_c"
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

hello 管線包含設定的複製活動 toouse hello 輸入和輸出資料集，並為排程的 toorun 每個小時。 在 hello 管線 JSON 定義中，hello**來源**類型設定得**RelationalSource**，和 hello**接收**類型設定得**BlobSink**。

請參閱[RelationalSource 類型屬性](#copy-activity-properties)的 hello hello RelationalSource 所支援的屬性清單。

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
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
> [!IMPORTANT]
> hello"__c"hello API 名稱部分所需的任何自訂的物件。

![Data Factory - Salesforce 連線 - API 名稱](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a>Salesforce 的類型對應
| Salesforce 類型 | 以 .NET 為基礎的類型 |
| --- | --- |
| 自動編號 |String |
| 核取方塊 |Boolean |
| 貨幣 |兩倍 |
| 日期 |DateTime |
| 日期/時間 |DateTime |
| 電子郵件 |String |
| 識別碼 |String |
| 查閱關聯性 |String |
| 複選挑選清單 |String |
| Number |兩倍 |
| 百分比 |兩倍 |
| 電話 |String |
| 挑選清單 |String |
| 文字 |String |
| 文字區域 |String |
| 文字區域 (完整) |String |
| 文字區域 (豐富) |String |
| 文字 (加密) |String |
| URL |String |

> [!NOTE]
> toomap 資料行從來源資料集 toocolumns 從接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a>效能和微調
請參閱 hello[複製活動效能及微調指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。
