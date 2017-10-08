---
title: "Azure Data Lake Store aaaViewing 診斷記錄檔 |Microsoft 文件"
description: "了解如何為 Azure Data Lake Store 的 toosetup 及存取診斷記錄檔 "
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 11fbf7f517f97abdcaf809c1ebeeb51424ab2c1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a>存取 Azure Data Lake Store 的診斷記錄
深入了解如何針對您的帳戶收集 tooenable Data Lake Store 帳戶和 tooview hello 的記錄檔的診斷記錄。

組織可以啟用其帳戶 toocollect 資料存取稽核記錄，提供使用者存取 hello data hello 資料存取的頻率、 資料量的資訊，例如清單會儲存在 hello 的 Azure Data Lake Store 的診斷記錄帳戶等等。

## <a name="prerequisites"></a>必要條件
* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure Data Lake Store 帳戶**。 請遵循指示 hello[開始使用 Azure 資料湖存放區使用 hello Azure 入口網站](data-lake-store-get-started-portal.md)。

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a>啟用 Data Lake Store 帳戶的診斷記錄
1. 登入新 toohello [Azure 入口網站](https://portal.azure.com)。
2. 開啟 Data Lake Store 帳戶，接著在 Data Lake Store 帳戶刀鋒視窗中依序按一下 [設定] 和 [診斷記錄檔]。
3. 在 hello**診斷記錄檔**刀鋒視窗中，按一下 **開啟診斷**。

    ![啟用診斷記錄](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "啟用診斷記錄")

3. 在 hello**診斷**刀鋒視窗中，進行下列變更 tooconfigure 診斷記錄的 hello。
   
    ![啟用診斷記錄](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "啟用診斷記錄")
   
   * 設定**狀態**太**上**tooenable 診斷記錄。
   * 您可以選擇 toostore/處理序 hello 資料不同的方式。
     
        * 選取 hello 選項太**封存 tooa 儲存體帳戶**toostore 記錄 tooan Azure 儲存體帳戶。 如果您想要將在日後會處理批次的 tooarchive hello 資料，您可以使用此選項。 如果您選取這個選項必須提供 Azure 儲存體帳戶 toosave hello 記錄檔。
        
        * 選取 hello 選項太**資料流 tooan 事件中心**toostream 記錄資料 tooan Azure 事件中心。 最有可能您會使用這個選項有下游處理管線 tooanalyze 連入即時記錄檔。 如果您選取此選項時，您必須提供 hello Azure 事件中心想 toouse hello 詳細資料。

        * 選取 hello 選項太**傳送 tooLog 分析**toouse hello Azure 記錄分析服務 tooanalyze hello 產生記錄檔資料。 如果您選取此選項時，您必須提供 hello 詳細說明 hello Operations Management Suite 工作區，您就可以使用 hello 執行記錄分析。
     
   * 指定是否要 tooget 稽核記錄檔或要求記錄檔或兩者。
   * 指定必須保留 hello 資料的 hello 天數。 只有適用於您要使用 Azure 儲存體帳戶 tooarchive 記錄資料保留。
   * 按一下 [儲存] 。

一旦您啟用了診斷設定，您可以觀看 hello 登入 hello**診斷記錄檔** 索引標籤。

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a>檢視 Data Lake Store 帳戶的診斷記錄
有兩種方式的 Data Lake Store 帳戶 tooview hello 記錄資料。

* 從 hello Data Lake Store 帳戶檢視設定
* 從儲存 hello 資料 hello Azure 儲存體帳戶

### <a name="using-hello-data-lake-store-settings-view"></a>使用 hello 資料湖存放區設定檢視
1. 在 Data Lake Store 帳戶的 [設定] 刀鋒視窗中，按一下 [診斷記錄]。
   
    ![檢視診斷記錄](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "檢視診斷記錄") 
2. 在 hello**診斷記錄檔**刀鋒視窗中，您應該會看見 hello 記錄依分類**稽核記錄檔**和**要求記錄檔**。
   
   * 要求記錄檔擷取 hello Data Lake Store 帳戶上所做的每個應用程式開發介面要求。
   * 稽核記錄是類似的 toorequest 記錄，但是提供更詳盡的 hello Data Lake Store 帳戶上所執行的 hello 作業細分。 例如，單一的上傳應用程式開發介面呼叫要求記錄檔中可能會導致 hello 稽核記錄中的多個 「 附加 」 作業。
3. 按一下 hello**下載**針對每個連結記錄項目 toodownload hello 記錄。

### <a name="from-hello-azure-storage-account-that-contains-log-data"></a>從 hello Azure 儲存體帳戶，其中包含記錄資料
1. 開啟記錄，與資料湖存放區相關聯的 hello Azure 儲存體帳戶刀鋒視窗，然後按一下Blob。 hello **Blob 服務**刀鋒視窗會列出兩個容器。
   
    ![檢視診斷記錄](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "檢視診斷記錄")
   
   * hello 容器**insights 記錄檔稽核**包含 hello 稽核記錄檔。
   * hello 容器**insights 記錄要求**包含 hello 要求記錄檔。
2. 這些容器中，內 hello 記錄檔會儲存在下列結構的 hello。
   
    ![檢視診斷記錄](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "檢視診斷記錄")
   
    例如，可能是 hello 完整路徑 tooan 稽核記錄檔`https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`
   
    Hello 完整路徑 tooa 要求記錄檔可能是 similary，`https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`

## <a name="understand-hello-structure-of-hello-log-data"></a>了解 hello hello 記錄資料結構
hello 稽核，並要求記錄檔是以 JSON 格式。 在本節中，我們會查看 hello 結構的 JSON 的要求，稽核記錄檔。

### <a name="request-logs"></a>要求記錄
以下是範例項目 hello JSON 格式要求記錄檔中。 每個 Blob 會一個名為 **記錄** 的根物件，其中包含記錄檔物件的陣列。

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a>要求記錄的結構描述
| Name | 類型 | 說明 |
| --- | --- | --- |
| 分析 |String |hello 時間戳記 （UTC) 的 hello 記錄檔 |
| resourceId |String |hello hello 資源作業所需的 ID 將會置於 |
| category |String |hello 記錄類別目錄。 例如， **要求**。 |
| operationName |String |Hello 作業所記錄的名稱。 例如，getfilestatus。 |
| resultType |String |hello 作業的狀態 hello，例如 200。 |
| callerIpAddress |String |hello 發出 hello 要求的用戶端 hello IP 位址 |
| correlationId |String |hello 識別碼 hello 記錄檔可以 toogroup 同時使用一組相關的記錄項目 |
| 身分識別 |Object |產生的 hello 記錄的 hello 身分識別 |
| 屬性 |JSON |如需詳細資料，請參閱下文 |

#### <a name="request-log-properties-schema"></a>要求記錄屬性結構描述
| Name | 類型 | 說明 |
| --- | --- | --- |
| HttpMethod |String |hello HTTP 方法 hello 作業使用。 例如，GET。 |
| Path |String |hello 路徑 hello 作業上執行 |
| RequestContentLength |int |hello hello HTTP 要求內容長度 |
| ClientRequestId |String |hello 可唯一識別這個要求識別碼 |
| StartTime |String |hello hello 接收伺服器 hello 要求時間 |
| EndTime |String |hello 的 hello 伺服器送出回應的時間 |

### <a name="audit-logs"></a>稽核記錄檔
以下是範例項目 hello JSON 格式的稽核記錄檔中。 每個 Blob 會一個名為 **記錄** 的根物件，其中包含記錄檔物件的陣列

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a>稽核記錄的結構描述
| Name | 類型 | 說明 |
| --- | --- | --- |
| 分析 |String |hello 時間戳記 （UTC) 的 hello 記錄檔 |
| resourceId |String |hello hello 資源作業所需的 ID 將會置於 |
| category |String |hello 記錄類別目錄。 例如， **稽核**。 |
| operationName |String |Hello 作業所記錄的名稱。 例如，getfilestatus。 |
| resultType |String |hello 作業的狀態 hello，例如 200。 |
| correlationId |String |hello 識別碼 hello 記錄檔可以 toogroup 同時使用一組相關的記錄項目 |
| 身分識別 |Object |產生的 hello 記錄的 hello 身分識別 |
| 屬性 |JSON |如需詳細資料，請參閱下文 |

#### <a name="audit-log-properties-schema"></a>稽核記錄屬性結構描述
| Name | 類型 | 說明 |
| --- | --- | --- |
| StreamName |String |hello 路徑 hello 作業上執行 |

## <a name="samples-tooprocess-hello-log-data"></a>範例 tooprocess hello 記錄資料
Azure Data Lake Store 提供的範例如何 tooprocess 和分析 hello 記錄資料。 您可以找到在 hello 範例[https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample)。 

## <a name="see-also"></a>另請參閱
* [Azure Data Lake Store 概觀](data-lake-store-overview.md)
* [保護資料湖存放區中的資料](data-lake-store-secure-data.md)

