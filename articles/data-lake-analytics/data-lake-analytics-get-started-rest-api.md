---
title: "開始使用 Data Lake Analytics 使用 REST API 的 aaaGet |Microsoft 文件"
description: "使用 Data Lake Analytics tooperform WebHDFS REST Api 作業"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 5e133d92-baaa-44c9-890c-ab2d85c91122
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: jgao
ms.openlocfilehash: a0b13d521821fd2d74716cc52485585feb7c51b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a>使用 REST API 開始使用 Azure Data Lake Analytics
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

了解 toouse WebHDFS REST Api 和資料湖分析 REST Api toomanage Data Lake Analytics 帳戶、 作業、 和目錄的方式。 

## <a name="prerequisites"></a>必要條件
* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **建立 Azure Active Directory 應用程式**。 您可以使用 hello Azure AD 應用程式 tooauthenticate hello Data Lake Analytics 應用程式與 Azure AD。 有不同的方法 tooauthenticate 與 Azure AD，這是**使用者驗證**或**服務對服務驗證**。 如需指示和詳細資訊 tooauthenticate，請參閱[驗證與使用 Azure Active Directory 的 Data Lake Analytics](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)。
* [cURL](http://curl.haxx.se/)。 本文使用 cURL toodemonstrate 如何 toomake REST API 呼叫針對 Data Lake Analytics 帳戶。

## <a name="authenticate-with-azure-active-directory"></a>向 Azure Active Directory 進行驗證
向 Azure Active Directory 進行驗證的方法有兩種。

### <a name="end-user-authentication-interactive"></a>使用者驗證 (互動式)
使用此方法時，應用程式會提示中的 hello 使用者 toolog 和 hello hello 使用者內容中執行所有的 hello 作業。 

遵循下列步驟進行互動式驗證：

1. 您的應用程式，透過重新導向 hello 使用者 toohello 下列 URL:
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<重新導向 URI > 需要 toobe 編碼 URL 中使用。 因此，針對 https://localhost，使用 `https%3A%2F%2Flocalhost`)
   > 
   > 
   
    為了 hello 本教學課程，您可以取代上述 hello URL 中的 hello 預留位置值，並將它貼在網頁瀏覽器的網址列中。 您將會重新導向的 tooauthenticate 使用您的 Azure 登入。 一旦您已成功登入，hello 回應會顯示 hello 瀏覽器的網址列中。 hello 回應 hello 遵循格式會是：
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. 擷取 hello 回應 hello 授權碼。 此教學課程中，您可以複製 hello hello web 瀏覽器網址列中的 hello 授權碼，並將它傳遞 hello POST 要求 toohello 權杖端點，在如下所示：
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > 在此情況下，hello\<重新導向 URI > 不需要進行編碼。
   > 
   > 
3. hello 回應是包含存取權杖的 JSON 物件 (例如`"access_token": "<ACCESS_TOKEN>"`) 和重新整理權杖 (例如`"refresh_token": "<REFRESH_TOKEN>"`)。 您的應用程式使用 hello 存取權杖時存取 Azure 資料湖存放區和 hello 重新整理語彙基元 tooget 另一個存取權杖的存取權杖到期時。
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. Hello 存取權杖過期時，您可以要求新的存取權杖使用 hello 重新整理權杖，如下所示：
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

如需互動使用者驗證的詳細資料，請參閱 [授權碼授與流程](https://msdn.microsoft.com/library/azure/dn645542.aspx)。

### <a name="service-to-service-authentication-non-interactive"></a>服務對服務驗證 (非互動式)
使用此方法時，應用程式會提供自己的認證 tooperform hello 作業。 這麼做，您必須發出 POST 要求像 hello 一個如下所示： 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

這項要求的 hello 輸出將包括授權權杖 (表示`access-token`hello 以下的輸出中)，您接下來將會傳遞 REST API 呼叫。 將此驗證權杖儲存在文字檔中；您將在本文稍後需要此權杖。

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

本文使用 hello**非互動式**方法。 如需有關非互動式 （服務對服務呼叫） 的詳細資訊，請參閱[服務會使用認證 tooservice 呼叫](https://msdn.microsoft.com/library/azure/dn645543.aspx)。

## <a name="create-a-data-lake-analytics-account"></a>建立 Data Lake Analytics 帳戶
您必須先建立 Azure 資源群組和 Data Lake Store 帳戶，才可以建立 Data Lake Analytics 帳戶。  請參閱[建立 Data Lake Store 帳戶](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account)。

hello 遵循 Curl 命令顯示如何 toocreate 帳戶：

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

取代\< `REDACTED` \>與 hello 授權權杖， \< `AzureSubscriptionID` \>以您的訂用帳戶 ID， \< `AzureResourceGroupName` \>與現有的 Azure 資源群組名稱和\< `NewAzureDataLakeAnalyticsAccountName` \>以新的資料湖分析帳戶名稱。 此命令的 hello 要求承載包含在 hello **CreateDatalakeAnalyticsAccountRequest.json**提供 hello 檔案`-d`上述的參數。 hello hello input.json 檔內容看起來像下列 hello:

    {  
        "location": "East US 2",  
        "name": "myadla1004",  
        "tags": {},  
        "properties": {  
            "defaultDataLakeStoreAccount": "my1004store",  
            "dataLakeStoreAccounts": [  
                {  
                    "name": "my1004store"  
                }     
            ]
        }  
    }  


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a>列出訂用帳戶中的 Data Lake Analytics 帳戶
hello 下列 Curl 命令顯示如何 toolist 帳戶的訂用帳戶中：

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

取代\< `REDACTED` \>與 hello 授權權杖， \< `AzureSubscriptionID` \>與您的訂用帳戶 id。 hello 輸出如下：

    {
        "value": [
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla0831.azuredatalakeanalytics.net",
                "accountId": "21e74660-0941-4880-ae72-b143c2615ea9",
                "creationTime": "2016-09-01T12:49:12.7451428Z",
                "lastModifiedTime": "2016-09-01T12:49:12.7451428Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla0831rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla0831",
            "name": "myadla0831",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            },
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla1004.azuredatalakeanalytics.net",
                "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
                "creationTime": "2016-10-04T20:46:42.287147Z",
                "lastModifiedTime": "2016-10-04T20:46:42.287147Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
            "name": "myadla1004",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            }
        ]
    }

## <a name="get-information-about-a-data-lake-analytics-account"></a>取得 Data Lake Analytics 帳戶的相關資訊
hello 遵循 Curl 命令顯示如何 tooget 帳戶資訊：

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

取代\< `REDACTED` \>與 hello 授權權杖， \< `AzureSubscriptionID` \>以您的訂用帳戶 ID， \< `AzureResourceGroupName` \>與現有的 Azure 資源群組名稱和\< `DataLakeAnalyticsAccountName` \> hello 現有的資料湖分析帳戶名稱。 hello 輸出如下：

    {
        "properties": {
            "defaultDataLakeStoreAccount": "my1004store",
            "dataLakeStoreAccounts": [
            {
                "properties": {
                "suffix": "azuredatalakestore.net"
                },
                "name": "my1004store"
            }
            ],
            "provisioningState": "Creating",
            "state": null,
            "endpoint": null,
            "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
            "creationTime": null,
            "lastModifiedTime": null
        },
        "location": "East US 2",
        "tags": {},
        "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
        "name": "myadla1004",
        "type": "Microsoft.DataLakeAnalytics/accounts"
    }

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a>列出 Data Lake Analytics 帳戶的 Data Lake Store
hello 下列 Curl 命令顯示如何 toolist 資料湖存放的帳戶：

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

取代\< `REDACTED` \>與 hello 授權權杖， \< `AzureSubscriptionID` \>以您的訂用帳戶 ID， \< `AzureResourceGroupName` \>與現有的 Azure 資源群組名稱和\< `DataLakeAnalyticsAccountName` \> hello 現有的資料湖分析帳戶名稱。 hello 輸出如下：

    {
        "value": [
            {
            "properties": {
                "suffix": "azuredatalakestore.net"
            },
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004/dataLakeStoreAccounts/my1004store",
            "name": "my1004store",
            "type": "Microsoft.DataLakeAnalytics/accounts/dataLakeStoreAccounts"
            }
        ]
    }

## <a name="submit-u-sql-jobs"></a>提交 U-SQL 作業
hello 遵循 Curl 命令顯示如何 toosubmit U SQL 工作：

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

取代\< `REDACTED` \>與 hello 授權權杖， \< `DataLakeAnalyticsAccountName` \> hello 現有的資料湖分析帳戶名稱。 此命令的 hello 要求承載包含在 hello **SubmitADLAJob.json**提供 hello 檔案`-d`上述的參數。 hello hello input.json 檔內容看起來像下列 hello:

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "properties": {
            "type": "USql",
            "script": "@searchlog =\n    EXTRACT UserId          int,\n            Start           DateTime,\n            Region          string,\n            Query          
        string,\n            Duration        int?,\n            Urls            string,\n            ClickedUrls     string\n    FROM \"/Samples/Data/SearchLog.tsv\"\n    US
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    too\"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

hello 輸出如下：

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "myadl@SPI",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "2016-10-05T13:54:59.9871859+00:00",
        "state": "Compiling",
        "result": "Succeeded",
        "stateAuditRecords": [
            {
            "newState": "New",
            "timeStamp": "2016-10-05T13:54:59.9871859+00:00",
            "details": "userName:myadl@SPI;submitMachine:N/A"
            }
        ],
        "properties": {
            "owner": "myadl@SPI",
            "resources": [],
            "runtimeVersion": "default",
            "rootProcessNodeId": "00000000-0000-0000-0000-000000000000",
            "algebraFilePath": "adl://myadls0831.azuredatalakestore.net/system/jobservice/jobs/Usql/2016/10/05/13/54/8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a/algebra.xml",
            "compileMode": "Semantic",
            "errorSource": "Unknown",
            "totalCompilationTime": "PT0S",
            "totalPausedTime": "PT0S",
            "totalQueuedTime": "PT0S",
            "totalRunningTime": "PT0S",
            "type": "USql"
        }
    }


## <a name="list-u-sql-jobs"></a>列出 U-SQL 作業
hello 遵循 Curl 命令顯示如何 toolist U-SQL 作業：

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

取代\< `REDACTED` \>與 hello 授權權杖，並\< `DataLakeAnalyticsAccountName` \> hello 現有的資料湖分析帳戶名稱。 

hello 輸出如下：

    {
    "value": [
        {
        "jobId": "65cf1691-9dbe-43cd-90ed-1cafbfb406fb",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someone@microsoft.com",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:46:53 GMT",
        "startTime": "Wed, 05 Oct 2016 13:47:33 GMT",
        "endTime": "Wed, 05 Oct 2016 13:48:07 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        },
        {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someoneadl@SPI",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:54:59 GMT",
        "startTime": "Wed, 05 Oct 2016 13:55:43 GMT",
        "endTime": "Wed, 05 Oct 2016 13:56:11 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        }
    ],
    "nextLink": null,
    "count": null
    }


## <a name="get-catalog-items"></a>取得目錄項目
hello 下列 Curl 命令顯示如何從 tooget hello 資料庫 hello 目錄：

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

hello 輸出如下：

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a>另請參閱
* toosee 更複雜的查詢，請參閱[使用 Azure Data Lake Analytics 分析網站記錄檔](data-lake-analytics-analyze-weblogs.md)。
* tooget 開始開發 U-SQL 應用程式，請參閱[使用 Data Lake Tools for Visual Studio 的開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。
* toolearn U-SQL，請參閱[開始使用 Azure 資料湖分析 U-SQL 語言](data-lake-analytics-u-sql-get-started.md)。
* 針對管理工作，請參閱 [使用 Azure 入口網站管理 Azure Data Lake Analytics](data-lake-analytics-manage-use-portal.md)。
* tooget 的概觀的 Data Lake Analytics，請參閱[Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)。
* toosee hello 相同教學課程中使用其他工具中，按一下在 hello hello 頁面最上方的 hello 索引標籤選取器。

