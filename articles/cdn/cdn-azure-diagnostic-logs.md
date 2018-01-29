---
title: "Azure 診斷記錄 | Microsoft Docs"
description: "客戶可以啟用 Azure CDN 的記錄分析功能。"
services: cdn
documentationcenter: 
author: 
manager: 
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/12/2017
ms.author: v-deasim
ms.openlocfilehash: 7bb4eebc80d1c0fdcb9fb5d0f6bb7aeeeb3cb08d
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="azure-diagnostic-logs"></a>Azure 診斷記錄

透過 Azure 診斷記錄，您可以檢視核心分析，並將它們儲存到一或多個目的地，包括：

 - Azure 儲存體帳戶
 - Azure 事件中心
 - [OMS Log Analytics 存放庫](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
這項功能適用於所有屬於 Verizon (標準與進階) 及 Akamai (標準) CDN 設定檔的 CDN 端點。 

Azure 診斷記錄可讓您將 CDN 端點的基本使用情況計量匯出到各種來源，讓您可以使用自訂的方式取用。 例如，您可以執行下列幾種資料匯出作業：

- 匯出資料至 Blob 儲存體、匯出至 CSV，以及在 Excel 中產生圖表。
- 匯出資料至事件中樞，並將資料與其他 Azure 服務相互關聯。
- 匯出資料至 Log Analytics，並在您自己的 OMS 工作區中檢視資料

下圖說明典型的 CDN 核心分析資料檢視。

![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/01_OMS-workspace.png)

圖 1 - CDN 核心分析檢視

如需診斷記錄的詳細資訊，請參閱[診斷記錄](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)。

## <a name="enable-logging-with-azure-portal"></a>使用 Azure 入口網站啟用記錄

請遵循下列步驟，使用 CDN 核心分析來啟用記錄功能：

登入 [Azure 入口網站](http://portal.azure.com)。 如果您尚未為您的工作流程啟用 CDN，請先[啟用 Azure CDN](cdn-create-new-endpoint.md)，再繼續進行。

1. 在入口網站中，瀏覽至 [CDN 設定檔]。
2. 選取 CDN 設定檔，然後選取您需要啟用 [診斷記錄] 的 CDN 端點。

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. 在 [監視] 區段中，選取 [診斷記錄]。

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a>使用 Azure 儲存體來啟用記錄功能
    
1. 若要使用 Azure 儲存體來儲存記錄，請選取 [封存至儲存體帳戶]選取 **CoreAnalytics**，然後選擇 [保留期 (天)] 下方的保留期天數。 保留天數為 0 會無限期地儲存記錄。 
2. 輸入您設定的名稱，然後按一下 [儲存體帳戶]。 選取儲存體帳戶之後，請按一下 [儲存]。

![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

*圖 2 - 使用 Azure 儲存體進行記錄*

### <a name="logging-with-oms-log-analytics"></a>使用 OMS Log Analytics 進行記錄

若要使用 OMS Log Analytics 來儲存記錄，請遵循下列步驟：

1. 從 [診斷記錄] 刀鋒視窗中，選取 [傳送至 Log Analytics]。 

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. 按一下 [設定] 以設定 Log Analytics 記錄。 在 [OMS 工作區] 對話方塊中，您可以選取先前的工作區或建立新的工作區。

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. 按一下 [建立新工作區]。

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/07_Create-new.png)

4. 輸入新的 OMS 工作區名稱。 OMS 工作區名稱必須是唯一的，且只能包含字母、數字和連字號；不允許空格和底線。 
5. 接下來，選取現有的訂用帳戶、資源群組 (新的或現有的)、位置和定價層。 您也可以選擇將此設定釘選到儀表板上。 按一下 [確定] 完成設定。

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5.  建立您的工作區之後，就會返回您診斷記錄的視窗。 確認您新的 Log Analytics 工作區名稱。

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    在設定 Log Analytics 設定之後，請確定您已選取 **CoreAnalytics**。

6. 按一下 [檔案] 。

7. 若要查看新的 OMS 工作區，請前往 Azure 入口網站的儀表板，然後按一下 Log Analytics 工作區的名稱。 按一下 [OMS 入口網站] 圖格，以檢視您在 OMS 存放庫中的工作區。 

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    您的 OMS 存放庫現已可供記錄資料。 若要取用該資料，您必須使用 [OMS 解決方案](#consuming-oms-log-analytics-data) (本文稍後會有說明)。

如需有關記錄資料延遲的詳細資訊，請參閱[記錄資料延遲](#log-data-delays)。

## <a name="enable-logging-with-powershell"></a>使用 PowerShell 啟用記錄

下列範例說明如何透過 Azure PowerShell Cmdlet 啟用診斷記錄。

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a>啟用儲存體帳戶中的診斷記錄

先登入並選取訂用帳戶：

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


若要啟用儲存體帳戶中的診斷記錄，請使用此命令︰

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
若要啟用 OMS 工作區中的診斷記錄，請使用此命令：

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a>從 Azure 儲存體取用診斷記錄
本節說明 CDN Core Analytics 的結構描述、其在 Azure 儲存體帳戶內的組織方式，並提供範例程式碼將記錄下載至 CSV 檔案。

### <a name="using-microsoft-azure-storage-explorer"></a>使用 Microsoft Azure 儲存體總管
首先您需要一個可存取儲存體帳戶中內容的工具，才能夠存取 Azure 儲存體帳戶的核心分析資料。 雖然市場中有數種工具可使用，但我們建議使用 Microsoft Azure 儲存體總管。 若要下載此工具，請參閱 [Azure 儲存體總管](http://storageexplorer.com/)。 下載並安裝軟體後，請將其設定為使用同一個已設定為 CDN 診斷記錄目的地的 Azure 儲存體帳戶。

1.  開啟 [Microsoft Azure 儲存體總管]
2.  找到儲存體帳戶
3.  移至此儲存體帳戶下方的 [Blob 容器] 節點，然後展開該節點
4.  選取名為 [insights-logs-coreanalytics] 的容器，然後對它按兩下
5.  結果會顯示在右側窗格，開頭的第一層顯示 [resourceId=]。 一直按一下 [繼續]，直到您看到 PT1H.json 檔案為止。 請參閱下列附註以取得路徑的說明。
6.  每個 blob PT1H.json 代表特定 CDN 端點或其自訂網域一小時的分析記錄。
7.  此 JSON 檔案內容的結構描述如＜Core Analytics 記錄結構描述＞一節所述


> [!NOTE]
> **Blob 路徑格式**
> 
> 每個小時會產生 Core Analytics 記錄，且會收集資料並加以儲存在單一 Azure blob 作為 JSON 承載。 因為儲存體總管工具會將 '/' 解譯為目錄分隔符號並示範階層，會如同階層結構及代表 blob 名稱顯示 Azure blob 的路徑。 此 blob 名稱會遵循下列命名慣例： 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

**欄位說明：**

|value|說明|
|-------|---------|
|訂用帳戶識別碼    |使用 GUID 格式的 Azure 訂用帳戶識別碼。|
|資源 |群組名稱   CDN 資源所屬資源群組的名稱。|
|設定檔名稱 |CDN 設定檔名稱|
|端點名稱 |CDN 端點名稱|
|Year|  4 位數的年份表示法，例如 2017|
|月| 2 位數的月份表示法。 01 = 一月...12 =十二月|
|天|   2 位數的當月日期表示法|
|PT1H.json| 儲存分析資料的實際 JSON 檔案|

### <a name="exporting-the-core-analytics-data-to-a-csv-file"></a>將 Core Analytics 資料匯出至 CSV 檔案

為讓您輕鬆存取 Core Analytics，我們提供一種工具的範例程式碼。 此工具可讓您將 JSON 檔案下載至以逗號分隔的一般檔案格式，用來輕鬆地建立圖表或其他彙總。

以下為使用此工具的方式：

1.  造訪 github 連結：[https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )
2.  下載程式碼。
3.  依照指示編譯與設定。
4.  執行工具。
5.  產生的 CSV 檔案會以簡單的平面階層顯示分析資料。

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a>從 OMS Log Analytics 存放庫取用診斷記錄
Log Analytics 是 Operations Management Suite (OMS) 中的一項服務，可監視您的雲端和內部部署環境，以維護其可用性和效能。 它會收集您的雲端和內部部署環境中的資源所產生的資料，以及從其他監視工具提供橫跨多個來源的分析。 

若要使用 Log Analytics，您必須對 Azure OMS Log Analytics 存放庫[啟用記錄功能](#enable-logging-with-azure-storage) (本文前面已討論過)。

### <a name="using-the-oms-repository"></a>使用 OMS 存放庫

 下圖顯示存放庫的輸入和輸出架構：

![OMS Log Analytics 存放庫](./media/cdn-diagnostics-log/12_Repo-overview.png)

*圖 3 - Log Analytics 存放庫*

您可以使用管理解決方案，以各種方式顯示資料。 您可以從 [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions) 取得管理解決方案。

按一下每個解決方案底部的 [立刻取得] 連結，即可從 Azure marketplace 安裝管理解決方案。

### <a name="adding-an-oms-cdn-management-solution"></a>新增 OMS CDN 管理解決方案

請遵循下列步驟來新增管理解決方案：

1.   如果您尚未這麼做，請使用 Azure 訂用帳戶登入 Azure 入口網站，然後前往您的儀表板。
    ![Azure 儀表板](./media/cdn-diagnostics-log/13_Azure-dashboard.png)

2. 在 [新增] 刀鋒視窗的 [Marketplace] 底下，選取 [監視 + 管理]。

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. 在 [監視 + 管理] 刀鋒視窗中，按一下 [檢視全部]。

    ![檢視全部](./media/cdn-diagnostics-log/15_See-all.png)

4.  在搜尋方塊中搜尋 CDN。

    ![檢視全部](./media/cdn-diagnostics-log/16_Search-for.png)

5.  選取 [Azure CDN 核心分析]。 

    ![檢視全部](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  在按一下 [建立] 後，系統會詢問您是要建立新的 OMS 工作區，還是使用現有工作區。 

    ![檢視全部](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  選取您之前建立的工作區。 然後，您必須新增自動化帳戶。

    ![檢視全部](./media/cdn-diagnostics-log/19_Add-automation.png)

8. 下列畫面顯示您必須填寫的自動化帳戶表單。 

    ![檢視全部](./media/cdn-diagnostics-log/20_Automation.png)

9. 在建立好自動化帳戶後，您即可新增您的解決方案。 按一下 [ **建立** ] 按鈕。

    ![檢視全部](./media/cdn-diagnostics-log/21_Ready.png)

10. 您的解決方案現已新增至工作區。 回到 Azure 入口網站的儀表板。

    ![檢視全部](./media/cdn-diagnostics-log/22_Dashboard.png)

    按一下您所建立的 Log Analytics 工作區以前往您的工作區。 

11. 按一下 [OMS 入口網站] 圖格，以查看您在 OMS 入口網站的新解決方案。

    ![檢視全部](./media/cdn-diagnostics-log/23_workspace.png)

12. 您的 OMS 入口網站現在看起來應該類似下列畫面︰

    ![檢視全部](./media/cdn-diagnostics-log/24_OMS-solution.png)

    按一下其中一個圖格以查看您資料的幾個檢視。

    ![檢視全部](./media/cdn-diagnostics-log/25_Interior-view.png)

    您可以向左或向右捲動來看到更多代表個別資料檢視的圖格。 

    按一下其中一個圖格，您就會看到資料的更多細節。

     ![檢視全部](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a>優惠和定價層

您可以在[這裡](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)看到 OMS 管理解決方案的供應項目和定價層。

### <a name="customizing-views"></a>自訂檢視

您可以使用**檢視設計工具**來自訂資料的檢視。 若要開始設計，請前往您的 OMS 工作區，然後按一下 [檢視設計工具] 圖格。

![[檢視設計工具]](./media/cdn-diagnostics-log/27_Designer.png)

您可以拖放各種圖表類型，然後填入您需要分析的資料細節。

![[檢視設計工具]](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a>記錄資料延遲

Verizon 記錄資料延遲 | Akamai 記錄資料延遲
--- | ---
Verizon 記錄資料會延遲 1 小時，端點傳播完成後需花費最多 2 小時才會開始出現。 | Akamai 記錄資料會延遲 24 小時，如果資料是在 24 小時前建立的，則需花費最多 2 小時才會開始出現。 如果記錄是剛建立的，則最多需要 25 小時才會開始出現。

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a>CDN Core Analytics 的診斷記錄類型

我們目前僅提供 Core Analytics 記錄，其中包含的計量會顯示 HTTP 回應統計資料和輸出統計資料，如從 CDN POP/邊緣所見。

### <a name="core-analytics-metrics-details"></a>Core Analytics 計量詳細資料
下表說明 Core Analytics 記錄中可用計量的清單。 並非所有提供者的所有計量皆可用，雖然這樣的差異極少。 下表也會顯示某個提供者是否有提供指定的計量。 請注意，計量僅適用於有流量的 CDN 端點。


|計量                     | 說明   | Verizon  | Akamai 
|---------------------------|---------------|---|---|
| RequestCountTotal         |這段期間要求命中總數| 是  |是   |
| RequestCountHttpStatus2xx |產生 2xx HTTP 代碼 (例如 200、202) 的所有要求計數              | 是  |是   |
| RequestCountHttpStatus3xx | 產生 3xx HTTP 代碼 (例如 300、302) 的所有要求計數              | 是  |是   |
| RequestCountHttpStatus4xx |產生 4xx HTTP 代碼 (例如 400、404) 的所有要求計數               | 是   |是   |
| RequestCountHttpStatus5xx | 產生 5xx HTTP 代碼 (例如 500、504) 的所有要求計數              | 是  |是   |
| RequestCountHttpStatusOthers |  所有其他 HTTP 代碼 (2xx-5xx 以外) 的計數 | 是  |是   |
| RequestCountHttpStatus200 | 產生 200 HTTP 代碼回應的所有要求計數              |否   |是   |
| RequestCountHttpStatus206 | 產生 206 HTTP 代碼回應的所有要求計數              |否   |是   |
| RequestCountHttpStatus302 | 產生 302 HTTP 代碼回應的所有要求計數              |否   |是   |
| RequestCountHttpStatus304 |  產生 304 HTTP 代碼回應的所有要求計數             |否   |是   |
| RequestCountHttpStatus404 | 產生 404 HTTP 代碼回應的所有要求計數              |否   |是   |
| RequestCountCacheHit |產生快取命中的所有要求計數。 資產是從 POP 直接提供給用戶端。               | 是  |否   |
| RequestCountCacheMiss | 產生快取遺漏的所有要求計數。 這表示最靠近用戶端的 POP 上找不到資產，且因此從來源擷取。              |是   | 否  |
| RequestCountCacheNoCache | 因為邊緣上的使用者組態之故，而無法予以快取的所有資產要求計數。              |是   | 否  |
| RequestCountCacheUncacheable | 無法由資產的 Cache-Control 與 Expires 標頭快取的所有資產要求計數，這表示不應在 POP 上或由 HTTP 用戶端快取要求                |是   |否   |
| RequestCountCacheOthers | 非上述快取狀態的所有要求計數。              |是   | 否  |
| EgressTotal | 輸出資料傳輸 (單位 GB)              |是   |是   |
| EgressHttpStatus2xx | 狀態代碼為 2xx HTTP 之回應的輸出資料傳輸* (單位為 GB)            |是   |否   |
| EgressHttpStatus3xx | 狀態代碼為 3xx HTTP 之回應的輸出資料傳輸 (單位為 GB)              |是   |否   |
| EgressHttpStatus4xx | 狀態代碼為 4xx HTTP 之回應的輸出資料傳輸 (單位為 GB)               |是   | 否  |
| EgressHttpStatus5xx | 狀態代碼為 5xx HTTP 之回應的輸出資料傳輸 (單位為 GB)               |是   |  否 |
| EgressHttpStatusOthers | 狀態代碼為其他 HTTP 之回應的輸出資料傳輸 (單位為 GB)                |是   |否   |
| EgressCacheHit |  直接從 CDN POP/邊緣上 CDN 快取所傳遞回應的輸出資料傳輸  |是   |  否 |
| EgressCacheMiss | 在最靠近的 POP 伺服器上找不到和從原始伺服器擷取之回應的輸出資料傳輸              |是   |  否 |
| EgressCacheNoCache | 因為邊緣上使用者組態之故而無法予以快取的資產輸出資料傳輸。                |是   |否   |
| EgressCacheUncacheable | 無法由資產的 Cache-Control 和/或 Expires 標頭快取的資產輸出資料傳輸。 表示應該不會在 POP 上加以快取或由 HTTP 用戶端進行快取。                   |是   | 否  |
| EgressCacheOthers |  其他快取案例的輸出資料傳輸。             |是   | 否  |

*輸出資料傳輸是指從 CDN POP 伺服器傳遞到用戶端的流量。


### <a name="schema-of-the-core-analytics-logs"></a>Core Analytics 記錄結構描述 

所有記錄都以 JSON 格式儲存，且每個項目都有根據下列結構描述的字串欄位：

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of the CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of the domain for which the statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

其中 ‘time’ 代表報告某段時間統計資料時該時間範圍的開始時間。 當 CDN 提供者不支援計量時，而非雙精確度值或整數值，則將會有 null 值。 此 null 值表示沒有計量，且與 0 值不同。 各網域會在端點上有一組這類計量設定。

範例屬性︰

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a>其他資源

* [Azure 診斷記錄](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [分析 Azure CDN 使用模式](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [Azure OMS Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)
* [Azure Log Analytics REST API](https://docs.microsoft.com/rest/api/loganalytics)







