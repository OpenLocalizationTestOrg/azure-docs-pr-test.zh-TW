---
title: "Azure CDN 的 aaaLog 分析 |Microsoft 文件"
description: "客戶可以啟用 Azure CDN 的記錄分析功能。"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a>Azure CDN 的診斷記錄

在您的應用程式啟用 CDN 之後, 將可能 toomonitor hello CDN 使用方式，檢查您傳遞的 hello 健全狀況，然後疑難排解潛在問題。 Azure CDN 利用 [CDN 核心分析](cdn-analyze-usage-patterns.md)和[診斷記錄](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)來提供這些功能

## <a name="cdn-core-analytics"></a>CDN 核心分析
以目前 Azure CDN 使用者與 Verizon 標準或進階設定檔，您已無法 tooview 核心分析採用 hello 補充入口網站可透過 hello 「 管理 」 選項從 hello Azure 入口網站存取。 

## <a name="azure-diagnostic-logs"></a>Azure 診斷記錄

透過這項新功能，您現在可以檢視核心分析，並將它們儲存到一或多個目的地，包括：

 - Azure 儲存體帳戶
 - Azure 事件中心
 - [OMS Log Analytics 存放庫](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 這項功能適用於所有屬於 tooVerizon （Standard 和 Premium） 和 （標準） Akamai CDN 設定檔的 CDN 端點。

診斷記錄檔可讓您從您的 CDN 端點 tooa 不同的來源 tooexport 基本的使用計量，讓您可以使用這些自訂的方式。 例如，您可以執行下列類型的資料匯出 hello:

- 匯出資料 tooblob 儲存、 匯出 tooCSV，並產生圖形在 excel 中。
- 匯出資料 tooevent 中樞，並與其他 azure 服務的資料相互關聯。
- 匯出資料 toolog 分析和檢視資料在您自己的 OMS 工作空間中

hello 下圖顯示典型的 CDN 核心分析檢視資料。

![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/01_OMS-workspace.png)

*圖 1 - CDN 核心分析檢視*

下列逐步解說的 hello 經歷 hello 核心分析資料，在啟用 「 hello 」 功能與傳遞 toovarious 目的地，以及從這些目的地使用所需步驟的 hello 結構描述。

## <a name="enable-logging-with-azure-portal"></a>使用 Azure 入口網站啟用記錄

> [!NOTE]
> hello 診斷記錄檔已**關閉**預設。 

請遵循以下 tooenable CDN 核心分析記錄 hello 步驟：

登入 toohello [Azure 入口網站](http://portal.azure.com)。 如果您尚未為您的工作流程啟用 CDN，請先[啟用 Azure CDN](cdn-create-new-endpoint.md)，再繼續進行。

1. 在 hello 入口網站中，瀏覽過**的 CDN 設定檔**。
2. 選取的 CDN 設定檔，然後選取您想 tooenable hello CDN 端點**診斷記錄檔**。

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. 跳過**診斷記錄檔**刀鋒視窗底下**監視**區段，然後變更 hello 狀態太**上**。

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a>使用 Azure 儲存體來啟用記錄功能
    
toouse Azure 儲存體 toostore hello 記錄檔，選取**封存 tooa 儲存體帳戶**，選取 保留天數，然後按一下**CoreAnalytics**下**記錄**。

![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

*圖 2 - 使用 Azure 儲存體進行記錄*

### <a name="logging-with-oms-log-analytics"></a>使用 OMS Log Analytics 進行記錄

toouse OMS 記錄分析 toostore hello 記錄檔，請遵循下列步驟：

1. 從 hello**診斷記錄檔**刀鋒視窗底下**監視**，選取**傳送 tooLog 分析**從 

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. 在設定，即可設定 hello 記錄分析記錄。 這會帶您 tooa 對話方塊，您可以在其中選取先前的工作區或另外新建一個。

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. 按一下 [建立新工作區]。

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/07_Create-new.png)

4. 接下來，您必須選取新的工作區名稱、現有的訂用帳戶、資源群組 (新的或現有的)、位置和定價層。 您可以釘選此組態 tooyour 儀表板的 hello 選擇。 按一下 [確定] toocomplete hello 組態。

    接下來，您應該會看到工作區上顯示您的 OMS 工作區名稱與資源群組名稱。 這些名稱必須是唯一的，而且只能使用字母、數字和連字號。 不允許使用空格和底線。 

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. 接下來，您會取得簡短訊息，指出已建立您的工作區，並將您返回 tooyour 記錄 組態畫面中。 您可以確認您的記錄分析工作區的 hello 名稱。

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    在您設定 hello 記錄分析設定，請確定您也檢查 CDN 記錄的 hello CoreAnalytics 方塊。

6. 如果一切 tooyour 喜好，請按一下 hello**儲存**在 hello hello 組態對話方塊頂端的按鈕。

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/10_Save-me.png)

    hello**儲存**按鈕不再作用中，且該 hello 上/關閉按鈕現在是 ON，但藍色，而不是紫色。

7. 如果您想 toosee 新的 OMS 工作區，移 tooyour Azure 入口網站儀表板，按一下 記錄分析工作區的 hello 名稱。 接下來，您會看到您的工作區 （請確定 OMS 工作區會反白顯示 hello 左邊）。 按一下 hello OMS 入口網站磚 toosee hello OMS 儲存機制中的工作區。 

    ![入口網站 - 診斷記錄](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    您的 OMS 儲存機制已就緒 toolog 資料。 若要 tooconsume 該資料，您必須使用[項 OMS 解決方案](#consuming-oms-log-analytics-data)、 涵蓋在本文稍後。

如需有關記錄資料延遲的詳細資訊，請瀏覽[這裡](#log-data-delays)。

## <a name="enable-logging-with-powershell"></a>使用 PowerShell 啟用記錄

以下是有關如何透過 tooenable 和 get 診斷記錄 hello Azure PowerShell Cmdlet 的範例。

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a>啟用儲存體帳戶中的診斷記錄

先登入並選取訂用帳戶：

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


tooEnable 診斷記錄檔儲存體帳戶，使用此命令：

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
tooEnable 診斷記錄檔中的 OMS 工作區中，使用此命令：

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a>從 Azure 儲存體取用診斷記錄
本節描述的 hello CDN 核心分析的 hello 結構描述，這些組織內的 Azure 儲存體帳戶，並提供如何範例程式碼 toodownload hello 記錄 tooa CSV 檔案中。

### <a name="using-microsoft-azure-storage-explorer"></a>使用 Microsoft Azure 儲存體總管
您可以從 hello Azure 儲存體帳戶存取 hello 核心分析資料之前，您必須先儲存體帳戶中的工具 tooaccess hello 內容。 Hello 市場中有數種工具可用，我們建議的其中一個 hello 是 hello Microsoft Azure 儲存體總管。 您可以下載從 hello 工具[這裡](http://storageexplorer.com/)。 下載並安裝 hello 軟體設定之後 toouse hello 相同的 Azure 儲存體帳戶設定為目的地 toohello CDN 診斷記錄檔。

1.  開啟 [Microsoft Azure 儲存體總管]
2.  找出 hello 儲存體帳戶
3.  移 toohello **[Blob 容器]**節點下這個儲存體帳戶，然後展開 [hello] 節點
4.  名為選取的 hello 容器**"insights-記錄檔-coreanalytics"**然後按兩下該檔案
5.  上 hello 右窗格從 hello 開始層級，如下所示，向上結果顯示**"resourceId ="**。 繼續按所有 hello 方法，直到您看到 hello 檔案**PT1H.json**。 請參閱下列附註說明 hello 路徑 hello。
6.  每個 blob **PT1H.json**代表特定的 CDN 端點或自訂網域的一小時 hello 分析記錄檔。
7.  hello 結構描述的 JSON 檔案的 hello 內容節將說明 hello 結構描述的 hello 核心分析記錄檔


> [!NOTE]
> **Blob 路徑格式**
> 
> Core Analytics 記錄每小時產生一次。 系統會將一小時的資料全部收集並儲存在單一 Azure Blob 內作為 JSON 承載。 hello 路徑 toothis Azure Blob 隨即出現，如同是階層式結構。 這是因為 hello 儲存體總管工具會解譯 '/' 做為目錄分隔符號，並顯示 hello 階層，為了方便起見。 實際上，hello 整個路徑只代表 hello blob 名稱。 這個 hello blob 的名稱會遵循下列命名慣例的 hello 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

**欄位說明：**

|value|說明|
|-------|---------|
|訂用帳戶識別碼    |Hello Azure 訂用帳戶的識別碼。 這是 hello Guid 格式。|
|資源 |屬於 hello 資源群組 toowhich hello CDN 資源群組名稱。|
|設定檔名稱 |Hello 的 CDN 設定檔的名稱|
|端點名稱 |Hello CDN 端點的名稱|
|Year|  hello 年，例如 2017年 4 位數表示法|
|月| hello 月份數字 2 位數表示。 01 = 一月...12 =十二月|
|天|   2 位數 hello hello 月份的天數表示法|
|PT1H.json| 實際的 JSON 檔案儲存 hello 分析資料|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a>匯出 hello 核心分析資料 tooa CSV 檔案

toomake it 輕鬆 tooaccess hello 核心分析，我們提供的工具，可讓您為一般模式以逗號分隔的檔案格式，可以使用的 tooeasily 下載 hello JSON 檔案的範例程式碼建立的圖表或其他彙總。

以下是如何使用 hello 工具：

1.  請瀏覽 hello github 連結： [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )
2.  下載 hello 程式碼
3.  請依照下列指示 toocompile 和設定
4.  執行 hello 工具
5.  產生的 CSV 檔案會顯示簡單的一般階層中的 hello 分析資料。

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a>從 OMS Log Analytics 存放庫取用診斷記錄
記錄分析是在 Operations Management Suite (OMS)，以監視您的雲端和內部部署環境 toomaintain 其可用性和效能的服務。 它會收集您的雲端和內部部署環境和其他監視工具 tooprovide 分析資源所產生的跨多個來源資料。 

toouse 記錄分析，您必須[啟用記錄](#enable-logging-with-azure-storage)toohello Azure OMS 記錄分析儲存機制，這稍早在本文章中討論。

### <a name="using-hello-oms-repository"></a>使用 hello OMS 儲存機制

 下列圖表顯示 hello 架構的 hello 輸入和輸出 hello 儲存機制的 hello:

![OMS Log Analytics 存放庫](./media/cdn-diagnostics-log/12_Repo-overview.png)

*圖 3 - Log Analytics 存放庫*

您可以使用管理解決方案，在各種不同的方式顯示 hello 資料。 您可以從 hello 取得管理解決方案[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions)。

您可以從 Azure marketplace 所提供安裝管理解決方案，依序按一下 hello**立即下載**在每個解決方案的 hello 底部的連結。

### <a name="adding-an-oms-cdn-management-solution"></a>新增 OMS CDN 管理解決方案

請遵循這些步驟 tooadd 管理解決方案：

1.   如果您尚未這樣做，請登入 toohello 使用您的 Azure 訂用帳戶的 Azure 入口網站，並移 tooyour 儀表板。
    ![Azure 儀表板](./media/cdn-diagnostics-log/13_Azure-dashboard.png)

2. 在 hello**新增**刀鋒視窗底下**Marketplace**，選取**監視 + 管理**。

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. 在 hello**監視 + 管理**刀鋒視窗中，按一下 **查看所有**。

    ![檢視全部](./media/cdn-diagnostics-log/15_See-all.png)

4.  搜尋 hello [搜尋] 方塊中的 CDN。

    ![檢視全部](./media/cdn-diagnostics-log/16_Search-for.png)

5.  選取 [Azure CDN 核心分析]。 

    ![檢視全部](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  按一下後**建立**，將會詢問 toocreate 新的 OMS 工作區，或使用現有的一個。 

    ![檢視全部](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  選取您之前建立的 hello 工作區。 然後，您會需要 tooadd 自動化帳戶。

    ![檢視全部](./media/cdn-diagnostics-log/19_Add-automation.png)

8. hello 下列畫面顯示 hello 自動化帳戶表單，您必須先填寫。 

    ![檢視全部](./media/cdn-diagnostics-log/20_Automation.png)

9. 一旦您已經建立 hello 自動化帳戶，您就準備好 tooadd 您的方案。 按一下 hello**建立** 按鈕。

    ![檢視全部](./media/cdn-diagnostics-log/21_Ready.png)

10. 您的方案現在已加入 tooyour 工作區。 返回 tooyour Azure 入口網站儀表板。

    ![檢視全部](./media/cdn-diagnostics-log/22_Dashboard.png)

    按一下 建立工作區中 tooyour toogo hello 記錄分析工作區。 

11. 按一下 hello **OMS 入口網站**磚 toosee 您 hello OMS 入口網站中的新方案。

    ![檢視全部](./media/cdn-diagnostics-log/23_workspace.png)

12. 您的 OMS 入口網站現在看起來應該像下列螢幕 hello:

    ![檢視全部](./media/cdn-diagnostics-log/24_OMS-solution.png)

    為您的資料，按一下其中一個 hello 磚 toosee 數個檢視。

    ![檢視全部](./media/cdn-diagnostics-log/25_Interior-view.png)

    您可以向左捲動或向右 toosee 進一步磚 hello 資料表示個別的檢視。 

    按一下其中一個 hello 磚可讓您更多詳細資料。

     ![檢視全部](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a>優惠和定價層

您可以在[這裡](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)看到 OMS 管理解決方案的供應項目和定價層。

### <a name="customizing-views"></a>自訂檢視

您可以使用來自訂 hello 檢視資料 hello**檢視表設計工具**。 請移 tooyour OMS 工作區，並依序按一下 hello 開始設計**檢視表設計工具**磚。

![[檢視設計工具]](./media/cdn-diagnostics-log/27_Designer.png)

您可以拖曳和 hello 左從卸除類型的圖表和填入您想要上剩餘的 hello tooanalyze hello 資料詳細資料。

![[檢視設計工具]](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a>記錄資料延遲

Verizon 記錄資料延遲 | Akamai 記錄資料延遲
--- | ---
Verizon 記錄資料延遲是 1 小時，並佔用 too2 小時 toostart 端點傳播完成後出現。 | Akamai 記錄資料是 24 小時的延遲，並會佔用 too2 小時 toostart 顯示它是建立超過 24 小時。 如果它最近建立的就可以在出現的 hello 記錄 toostart too25 小時。

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a>CDN 核心分析的診斷記錄類型

目前，我們會提供僅核心分析記錄檔，其中包含顯示 HTTP 回應的統計資料和輸出統計資料從 hello CDN Pop/邊緣所見度量。

### <a name="core-analytics-metrics-details"></a>Core Analytics 計量詳細資料
下表中的 hello 顯示的 hello 核心分析記錄中可用的度量的清單。 並非所有提供者的所有計量皆可用，雖然這樣的差異極少。 hello 也下表顯示指定的度量是否可從提供者。 請注意 hello 度量，皆可用於在其上有流量的 CDN 端點。


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
| RequestCountCacheHit |產生快取命中的所有要求計數。 這表示 hello 資產處理直接從 hello POP toohello 用戶端。               | 是  |否   |
| RequestCountCacheMiss | 產生快取遺漏的所有要求計數。 這表示 hello 資產 hello POP 最接近 toohello 用戶端上，找不到，因此擷取自 hello 原點。              |是   | 否  |
| RequestCountCacheNoCache | 所有要求計數 tooan 資產，所以無法被快取到期 tooa hello 邊緣上的使用者設定。              |是   | 否  |
| RequestCountCacheUncacheable | 要求 tooassets 防止 hello 資產的快取控制快取和到期標頭，這表示，它應該不會快取彈出或 hello HTTP 用戶端的所有計數                |是   |否   |
| RequestCountCacheOthers | 非上述快取狀態的所有要求計數。              |是   | 否  |
| EgressTotal | 輸出資料傳輸 (單位 GB)              |是   |是   |
| EgressHttpStatus2xx | 狀態代碼為 2xx HTTP 之回應的輸出資料傳輸* (單位為 GB)            |是   |否   |
| EgressHttpStatus3xx | 狀態代碼為 3xx HTTP 之回應的輸出資料傳輸 (單位為 GB)              |是   |否   |
| EgressHttpStatus4xx | 狀態代碼為 4xx HTTP 之回應的輸出資料傳輸 (單位為 GB)               |是   | 否  |
| EgressHttpStatus5xx | 狀態代碼為 5xx HTTP 之回應的輸出資料傳輸 (單位為 GB)               |是   |  否 |
| EgressHttpStatusOthers | 狀態代碼為其他 HTTP 之回應的輸出資料傳輸 (單位為 GB)                |是   |否   |
| EgressCacheHit |  傳出資料傳輸所傳送的回應直接從 hello CDN 快取上 hello CDN Pop/邊緣  |是   |  否 |
| EgressCacheMiss | 傳出資料傳輸不上最接近的 POP 伺服器 hello 找到和擷取自 hello 來源伺服器的回應              |是   |  否 |
| EgressCacheNoCache | 輸出資料傳輸會禁止快取的到期 tooa hello 邊緣上的使用者設定的資產。                |是   |否   |
| EgressCacheUncacheable | 傳出資料傳輸會阻止 hello 資產的快取控制及/或 Expires 標頭，這表示，它應該不會快取彈出或 hello HTTP 用戶端快取的資產                    |是   | 否  |
| EgressCacheOthers |  其他快取案例的輸出資料傳輸。             |是   | 否  |

* 連出資料傳輸是指 tootraffic 傳遞從用戶端-伺服器 toohello CDN POP。


### <a name="schema-of-hello-core-analytics-logs"></a>Hello 核心分析記錄檔的結構描述 

所有記錄檔會儲存在 JSON 格式，而且每個項目具有下列 hello 下列結構描述的字串欄位：

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
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

其中 hello 'time' 代表 hello 的 hello 小時界限 hello 統計資料報告的開始時間。 當 CDN 提供者不支援計量時，而非雙精確度值或整數值，則將會有 null 值。 這個 null 值表示度量資訊，hello 不存在，這點不同於 0 的值。 也請注意，將會是每個網域的 hello 結束點上設定這些度量的一組。

範例屬性如下︰

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
* [Azure OMS Log Analytics](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [Azure Log Analytics REST API](https://docs.microsoft.com/en-us/rest/api/loganalytics)







