---
title: "Azure Data Lake Analytics aaaViewing 診斷記錄檔 |Microsoft 文件"
description: "了解如何 toosetup 及存取診斷記錄的 Azure 資料湖分析 "
services: data-lake-analytics
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 4cd1eb6f585c1ef96c358340232ef85721a972b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a>存取 Azure Data Lake Analytics 的診斷記錄

診斷記錄可讓您 toocollect 資料存取稽核記錄。 這些記錄檔可提供如下資訊︰

* 存取 hello 資料的使用者清單。
* Hello 資料存取的頻率。
* 多少資料會儲存在 hello 帳戶。

## <a name="enable-logging"></a>啟用記錄

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。

2. 開啟您的 Data Lake Analytics 帳戶，然後選取**診斷記錄**從 hello__監視器__> 一節。 接下來，選取 [開啟診斷]。

    ![開啟診斷 toocollect 稽核，並要求記錄檔](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. 從__診斷設定__、 設定 hello 狀態 too__On__，然後選取 記錄選項。

    ![開啟診斷 toocollect 稽核，並要求記錄檔](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "啟用診斷記錄檔")

   * 設定**狀態**太**上**tooenable 診斷記錄。

   * 您可以選擇 toostore/處理序 hello 資料以三個不同的方式。

     * 選取__封存 tooa 儲存體帳戶__toostore 登入 Azure 儲存體帳戶。 如果您想要 tooarchive hello 資料，請使用此選項。 如果您選取此選項時，您必須提供 Azure 儲存體帳戶 toosave hello 記錄檔。

     * 選取**串流 tooan 事件中心**toostream 記錄資料 tooan Azure 事件中心。 如果您有即時分析內送記錄的下游處理管線，請使用此選項。 如果您選取此選項時，您必須提供 hello Azure 事件中心想 toouse hello 詳細資料。

     * 選取__傳送 tooLog 分析__toosend hello 資料 toohello 記錄分析服務。 如果您想 toouse 記錄分析 toogather 和分析記錄檔，請使用此選項。
   * 指定是否要 tooget 稽核記錄檔或要求記錄檔或兩者。  要求記錄會擷取每個應用程式開發介面 (API) 的要求。 稽核記錄則會記錄該 API 要求觸發的所有作業。

   * 如__封存 tooa 儲存體帳戶__，指定 hello 天 tooretain hello 資料數目。

   * 按一下 [檔案] 。

        > [!NOTE]
        > 您必須選取__封存 tooa 儲存體帳戶__，__串流 tooan 事件中心__或__傳送 tooLog 分析__後，再按一下 hello__儲存__ 按鈕。

一旦您啟用了診斷設定，您可以傳回 toohello__診斷記錄檔__刀鋒視窗 tooview hello 記錄檔。

## <a name="view-logs"></a>檢視記錄檔

### <a name="use-hello-data-lake-analytics-view"></a>使用 hello Data Lake Analytics 檢視

1. 從您的資料湖分析帳戶刀鋒視窗中，在**監視**，選取**診斷記錄檔**，然後選取項目 toodisplay 記錄檔。

    ![檢視診斷記錄](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "檢視診斷記錄")

2. hello 記錄檔以分類**稽核記錄檔**和**要求記錄檔**。

    ![記錄項目](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * 要求記錄檔擷取 hello Data Lake Analytics 帳戶上所做的每個應用程式開發介面要求。
   * 稽核記錄是類似的 toorequest 記錄，但是提供更詳盡的 hello 作業細分。 例如，要求記錄中的一個上傳 API 呼叫可能會致使其稽核記錄出現多個「附加」作業。

3. 按一下 hello**下載**記錄的記錄檔項目 toodownload 的連結。

### <a name="use-hello-azure-storage-account-that-contains-log-data"></a>使用包含記錄資料的 hello Azure 儲存體帳戶

1. 開啟 Data Lake Analytics 與記錄相關聯的 hello Azure 儲存體帳戶刀鋒視窗，然後按一下__Blob__。 hello **Blob 服務**刀鋒視窗會列出兩個容器。

    ![檢視診斷記錄](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "檢視診斷記錄")

   * hello 容器**insights 記錄檔稽核**包含 hello 稽核記錄檔。
   * hello 容器**insights 記錄要求**包含 hello 要求記錄檔。
2. 這些容器中，內 hello 記錄檔會儲存在下列結構的 hello:

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > hello `##` hello 路徑中的項目包含 hello 年、 月、 日和小時建立記錄檔中的 hello。 Data Lake Analytics 每小時會建立一個檔案，因此 `m=` 一律會包含 `00` 值。

    例如，可能是 hello 完整路徑 tooan 稽核記錄檔：

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    同樣地，可能是 hello 完整路徑 tooa 要求記錄檔：

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a>記錄檔結構

hello 稽核和要求記錄檔會結構化的 JSON 格式。

### <a name="request-logs"></a>要求記錄

以下是範例項目 hello JSON 格式要求記錄檔中。 每個 Blob 會一個名為 **記錄** 的根物件，其中包含記錄檔物件的陣列。

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a>要求記錄的結構描述

| Name | 類型 | 說明 |
| --- | --- | --- |
| 分析 |String |hello 時間戳記 （UTC) 的 hello 記錄檔 |
| resourceId |String |hello hello 資源作業所需的識別項將會置於 |
| category |String |hello 記錄類別目錄。 例如， **要求**。 |
| operationName |String |Hello 作業所記錄的名稱。 例如，GetAggregatedJobHistory。 |
| resultType |String |hello 作業的狀態 hello，例如 200。 |
| callerIpAddress |String |hello 發出 hello 要求的用戶端 hello IP 位址 |
| correlationId |String |hello hello 記錄識別碼。 這個值可以是使用的 toogroup 一組相關的記錄項目。 |
| 身分識別 |Object |產生的 hello 記錄的 hello 身分識別 |
| 屬性 |JSON |請參閱 hello 下一節 （要求記錄檔的屬性結構描述），如需詳細資訊 |

#### <a name="request-log-properties-schema"></a>要求記錄屬性結構描述

| Name | 類型 | 說明 |
| --- | --- | --- |
| HttpMethod |String |hello HTTP 方法 hello 作業使用。 例如，GET。 |
| Path |String |hello 路徑 hello 作業上執行 |
| RequestContentLength |int |hello hello HTTP 要求內容長度 |
| ClientRequestId |String |hello 識別碼可唯一識別此要求 |
| StartTime |String |hello hello 接收伺服器 hello 要求時間 |
| EndTime |String |hello 的 hello 伺服器送出回應的時間 |

### <a name="audit-logs"></a>稽核記錄檔

以下是範例項目 hello JSON 格式的稽核記錄檔中。 每個 Blob 會一個名為 **記錄** 的根物件，其中包含記錄檔物件的陣列。

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a>稽核記錄的結構描述

| Name | 類型 | 說明 |
| --- | --- | --- |
| 分析 |String |hello 時間戳記 （UTC) 的 hello 記錄檔 |
| resourceId |String |hello hello 資源作業所需的識別項將會置於 |
| category |String |hello 記錄類別目錄。 例如， **稽核**。 |
| operationName |String |Hello 作業所記錄的名稱。 例如，JobSubmitted。 |
| resultType |String |Hello 作業狀態 (operationName) 子狀態。 |
| resultSignature |String |在 hello 作業狀態 (operationName) 上的其他詳細資料。 |
| 身分識別 |String |hello 要求 hello 作業的使用者。 例如： susan@contoso.com。 |
| properties |JSON |請參閱 hello 下一節 （稽核記錄檔的屬性結構描述），如需詳細資訊 |

> [!NOTE]
> **resultType**和**resultSignature** hello 作業的結果，提供相關資訊，並只能包含一個值，如果作業已完成。 例如，只有當 **operationName** 包含 **JobStarted** 或 **JobEnded** 的值時，它們才會包含值。
>
>

#### <a name="audit-log-properties-schema"></a>稽核記錄屬性結構描述

| Name | 類型 | 說明 |
| --- | --- | --- |
| JobId |String |hello ID 指派的 toohello 工作 |
| JobName |String |hello 作業所提供的 hello 名稱 |
| JobRunTime |String |使用 tooprocess hello 作業 hello 執行階段。 |
| SubmitTime |String |hello 時間 （以 utc 格式） 提交該 hello 作業 |
| StartTime |String |hello 時間 hello 作業開始執行之後提交 （以 utc 格式） |
| EndTime |String |hello 時間 hello 作業已結束 |
| 平行處理原則 |String |Data Lake Analytics 單位提交期間要求此作業的 hello 數目 |

> [!NOTE]
> **SubmitTime**、**StartTime**、**EndTime** 和 **Parallelism** 提供作業的相關資訊。 這些項目只會在作業啟動或完成時才包含值。 例如， **SubmitTime**只包含值之後**operationName** hello 值**JobSubmitted**。

## <a name="process-hello-log-data"></a>處理序 hello 記錄資料

Azure Data Lake Analytics 提供的範例如何 tooprocess 和分析 hello 記錄資料。 您可以找到在 hello 範例[https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample)。

## <a name="next-steps"></a>後續步驟
* [Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)
