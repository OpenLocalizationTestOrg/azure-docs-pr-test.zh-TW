---
title: "使用 U-SQL 指令碼-Azure aaaTransform 資料 |Microsoft 文件"
description: "了解如何藉由執行在 Azure Data Lake Analytics U-SQL 指令碼 tooprocess 或轉換資料計算服務。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: 51fdb40334d0c131720f65c3a96b4c5045a98b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a>在 Azure Data Lake Analytics 上執行 U-SQL 指令碼來轉換資料 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive 活動](data-factory-hive-activity.md) 
> * [Pig 活動](data-factory-pig-activity.md)
> * [MapReduce 活動](data-factory-map-reduce.md)
> * [Hadoop 串流活動](data-factory-hadoop-streaming-activity.md)
> * [Spark 活動](data-factory-spark.md)
> * [Machine Learning Batch 執行活動](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning 更新資源活動](data-factory-azure-ml-update-resource-activity.md)
> * [預存程序活動](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL 活動](data-factory-usql-activity.md)
> * [.NET 自訂活動](data-factory-use-custom-activities.md)

Azure Data Factory 中的「管線」會使用連結的計算服務，來處理連結的儲存體服務中的資料。 它包含一系列活動，其中每個活動都會執行特定的處理作業。 本文說明 hello**資料 Lake Analytics U-SQL 活動**執行**U-SQL**上的指令碼**Azure Data Lake Analytics**計算連結的服務。 

> [!NOTE]
> 使用 Data Lake Analytics「U-SQL 活動」來建立管線之前，請先建立 Azure Data Lake Analytics 帳戶。 toolearn 有關 Azure Data Lake Analytics，請參閱[開始使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)。
> 
> 檢閱 hello[建置您的第一個管線教學課程](data-factory-build-your-first-pipeline.md)的詳細的步驟 toocreate data factory，連結的服務、 資料集和管線。 使用 Data Factory 編輯器或 Visual Studio 或 Azure PowerShell toocreate Data Factory 實體的 JSON 片段。

## <a name="supported-authentication-types"></a>支援的驗證類型
U-SQL 活動支援以下針對 Data Lake Analytics 的驗證類型：
* 服務主體驗證
* 使用者認證 (OAuth) 驗證 

我們建議您使用服務主體驗證，特別是針對排程的 U-SQL 執行。 權杖到期行為會連同使用者認證驗證發生。 設定詳細資料，請參閱 hello[連結服務屬性](#azure-data-lake-analytics-linked-service)> 一節。

## <a name="azure-data-lake-analytics-linked-service"></a>Azure Data Lake Analytics 連結服務
您建立**Azure Data Lake Analytics**連結服務 toolink Azure Data Lake Analytics 計算服務 tooan Azure data factory。 hello hello 管線中的資料 Lake Analytics U-SQL 活動指的是 toothis 連結服務。 

hello 下表提供說明 hello hello JSON 定義中使用的一般內容。 您可以在服務主體與使用者認證驗證之間進一步選擇。

| 屬性 | 說明 | 必要 |
| --- | --- | --- |
| **type** |hello 類型屬性應該設定為： **AzureDataLakeAnalytics**。 |是 |
| **accountName** |Azure Data Lake Analytics 帳戶名稱。 |是 |
| **dataLakeAnalyticsUri** |Azure Data Lake Analytics URI。 |否 |
| **subscriptionId** |Azure 訂用帳戶識別碼 |否 （如果未指定，訂用帳戶的資料處理站可用的 hello）。 |
| **resourceGroupName** |Azure 資源群組名稱 |否 （如果未指定，資源群組的資料處理站可用的 hello）。 |

### <a name="service-principal-authentication-recommended"></a>服務主體驗證 (建議)
服務主體驗證 toouse，註冊在 Azure Active Directory (Azure AD) 和授與它 hello 應用程式的實體存取 tooData 湖存放區。 如需詳細的步驟，請參閱[服務對服務驗證](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)。 請記下的下列值，您使用的 hello toodefine hello 連結服務：
* 應用程式識別碼
* 應用程式金鑰 
* 租用戶識別碼

您可以使用服務主體的驗證方法是指定 hello 下列屬性：

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| **servicePrincipalId** | 指定 hello 應用程式的用戶端識別碼。 | 是 |
| **servicePrincipalKey** | 指定 hello 應用程式的金鑰。 | 是 |
| **tenant** | 指定在您的應用程式所在的 hello 租用戶資訊 (網域名稱或租用戶 ID)。 您可以透過暫留在 hello 右上角的 hello Azure 入口網站中的 hello 滑鼠擷取它。 | 是 |

**範例：服務主體驗證**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>使用者認證驗證
或者，您可以使用使用者認證驗證的 Data Lake Analytics 藉由指定下列屬性的 hello:

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| **authorization** | 按一下 hello**授權**按鈕 hello Data Factory 編輯器中，並輸入您 hello 自動產生的授權 URL toothis 屬性指派的認證。 | 是 |
| **sessionId** | 從 hello OAuth 授權工作階段的 OAuth 工作階段識別碼。 每個工作階段識別碼都是唯一的，只能使用一次。 當您使用 hello Data Factory 編輯器時，此設定會自動產生。 | 是 |

**範例：使用者認證授權**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a>權杖到期
hello 您使用 hello 所產生的授權碼**授權**一段時間後到期 按鈕。 請參閱下表針對不同類型的使用者帳戶的 hello 逾期時間的 hello。 您可能會看到下列錯誤訊息的 hello 當 hello 驗證**權杖到期**： 認證作業發生錯誤： invalid_grant-AADSTS70002： 驗證認證時發生錯誤。 AADSTS70008: hello 提供存取權限已過期或撤銷。 追蹤識別碼：d18629e8-af88-43c5-88e3-d8419eb1fca1 相互關連識別碼：fac30a0c-6be6-4e02-8d69-a776d2ffefd7 時間戳記：2015-12-15 21:09:31Z

| 使用者類型 | 到期時間 |
|:--- |:--- |
| 不受 Azure Active Directory 管理的使用者帳戶 (@hotmail.com、@live.com 等) |12 小時 |
| 受 Azure Active Directory (AAD) 管理的使用者帳戶 |14 天之後 hello 最後一個配量執行。 <br/><br/>如果以 OAuth 式連結服務為基礎的配量至少每 14 天執行一次，則為 90 天。 |

tooavoid/解決這個錯誤，重新授權使用 hello**授權**按鈕時 hello**權杖到期**然後重新部署 hello 連結服務。 您也可以如下使用程式碼，以程式設計方式產生 **sessionId** 和 **authorization** 屬性的值：

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

請參閱[AzureDataLakeStoreLinkedService 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx)， [AzureDataLakeAnalyticsLinkedService 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx)，和[AuthorizationSessionGetResponse 類別](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx)主題的詳細資訊關於 hello hello 程式碼中使用的 Data Factory 類別。 加入的參考： Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll hello WindowsFormsWebAuthenticationDialog 類別。 

## <a name="data-lake-analytics-u-sql-activity"></a>Data Lake Analytics U-SQL 活動
hello 下列 JSON 片段會定義具有資料 Lake Analytics U-SQL 活動的管線。 hello 活動定義具有參考 toohello 您稍早建立的連結的 Azure 資料湖分析服務。   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline toocompute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

hello 下表描述之特定 toothis 活動的屬性名稱和描述。 

| 屬性 | 說明 | 必要 |
|:--- |:--- |:--- |
| 類型 |hello type 屬性必須設定得**DataLakeAnalyticsU SQL**。 |是 |
| scriptPath |路徑 toofolder 包含 hello U-SQL 指令碼。 Hello 檔案的名稱會區分大小寫。 |否 (如果您使用指令碼) |
| scriptLinkedService |連結包含 hello 指令碼 toohello 資料 factory 的 hello 儲存體連結的服務 |否 (如果您使用指令碼) |
| script |指定內嵌指令碼而不是指定 scriptPath 和 scriptLinkedService。 例如： `"script": "CREATE DATABASE test"`。 |否 (如果您使用 scriptPath 和 scriptLinkedService) |
| degreeOfParallelism |hello 的節點數目上限，同時使用 toorun hello 作業。 |否 |
| 優先順序 |決定從所有已排入佇列的作業應該選取的 toorun 第一次。 hello 低 hello 數字，hello hello 優先順序越高。 |否 |
| 參數 |Hello U-SQL 指令碼的參數 |否 |
| runtimeVersion | Hello U-SQL 引擎 toouse 執行階段版本 | 否 | 
| compilationMode | <p>U-SQL 的編譯模式。 必須是下列其中一個值：</p> <ul><li>**Semantic：**僅執行語意檢查和必要的例行性檢查。</li><li>**完整：**執行 hello 完整編譯，包括語法檢查、 最佳化，程式碼產生、 等等。</li><li>**SingleBox:**執行 hello 完整的編譯，TargetType 設定 tooSingleBox。</li></ul><p>如果您未指定此屬性的值，hello 伺服器會決定 hello 最佳編譯模式。 </p>| 否 | 

請參閱[SearchLogProcessing.txt 指令碼定義](#sample-u-sql-script)hello 指令碼定義。 

## <a name="sample-input-and-output-datasets"></a>建立輸入和輸出資料集
### <a name="input-dataset"></a>輸入資料集
在此範例中，hello 輸入的資料位於 Azure 資料湖存放區 （SearchLog.tsv 檔案 hello datalake/輸入資料夾中）。 

```json
{
    "name": "DataLakeTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a>輸出資料集
在此範例中，hello hello U-SQL 指令碼所產生的輸出資料會儲存在 Azure Data Lake Store （datalake/輸出資料夾）。 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a>Data Lake Store 連結服務範例
以下是 hello 定義 Azure Data Lake Store 連結 hello 輸入/輸出資料集所使用的服務的 hello 範例。 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

請參閱[從 Azure 資料湖存放區移動資料 tooand](data-factory-azure-datalake-connector.md) JSON 屬性的說明文章。 

## <a name="sample-u-sql-script"></a>U-SQL 指令碼範例

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    too@out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

hello 值 **@in** 和 **@out**  hello U-SQL 指令碼中的參數傳遞以動態方式的 ADF 使用 hello 'parameters' 區段。 請參閱 hello 管線定義中的 hello 'parameters' 區段。

您可以在管線定義中的 hello hello Azure 資料湖分析服務執行的作業以及指定其他屬性，例如 degreeOfParallelism 和優先順序。

## <a name="dynamic-parameters"></a>動態參數
往返在 hello 範例管線定義中，參數會指派以硬式編碼值。 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

相反地，它是可能 toouse 動態參數。 例如： 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

在此情況下，輸入的檔案仍然從挑選 hello /datalake/input 資料夾和 hello /datalake/output 資料夾中產生輸出檔案。 hello 檔案名稱是動態的 hello 配量的開始時間為基礎。  

