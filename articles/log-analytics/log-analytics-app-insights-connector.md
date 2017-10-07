---
title: "aaaView Azure Application Insights 應用程式資料 |Microsoft 文件"
description: "您可以使用 hello 應用程式 Insights 連接器方案 toodiagnose 效能問題，並了解使用者執行應用程式時使用 Application Insights 監視。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 49280cad-3526-43e1-a365-c6a3bf66db52
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: banders
ms.openlocfilehash: 38109337ebbc8970dccb65365ba8284d9cee19a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-connector-solution-preview-in-operations-management-suite-oms"></a>Operations Management Suite (OMS) 中的 Application Insights Connector 解決方案 (預覽)

![Application Insights 符號](./media/log-analytics-app-insights-connector/app-insights-connector-symbol.png)

hello 應用程式 Insights Connector 解決方案可協助您診斷效能問題，並了解使用者使用達成您的應用程式與監視時[Application Insights](../application-insights/app-insights-overview.md)。 檢視 hello 開發人員，請參閱 Application Insights 中的相同應用程式遙測的可用在 OMS 中。 不過，在整合 Application Insights 應用程式與 OMS 時，將作業與應用程式資料放在一個地方可提高您應用程式的可見性。 具有 hello 相同檢視表可協助您與您的應用程式開發人員 toocollaborate。 hello 常見檢視可以協助減少 hello 時間 toodetect 並解決應用程式與平台問題。

當您使用 hello 方案時，您可以：

- 在一個地方檢視所有 Application Insights 應用程式，即使它們位於不同的 Azure 訂用帳戶中
- 讓基礎結構資料與應用程式資料相互關聯
- 在記錄搜尋中以檢視方塊將應用程式資料視覺化
- 樞紐記錄分析資料 tooyour Application Insights 中的應用程式 hello OMS 和 Azure 入口網站

## <a name="connected-sources"></a>連接的來源

不同於其他大部分記錄分析解決方案，不是應用程式 Insights 連接器 hello 代理程式所收集資料。 Hello 方案所使用的所有資料都是直接來自 Azure。

| 連接的來源 | 支援 | 說明 |
| --- | --- | --- |
| [Windows 代理程式](log-analytics-windows-agents.md) | 否 | hello 方案不會從 Windows 代理程式收集的資訊。 |
| [Linux 代理程式](log-analytics-linux-agents.md) | 否 | hello 解決方案不會收集從 Linux 代理程式的資訊。 |
| [SCOM 管理群組](log-analytics-om-agents.md) | 否 | hello 方案不會從已連線的 SCOM 管理群組中的代理程式收集的資訊。 |
| [Azure 儲存體帳戶](log-analytics-azure-storage.md) | 否 | hello 方案會從 Azure 儲存體不收集資訊。 |

## <a name="prerequisites"></a>必要條件

- tooaccess 應用程式 Insights 連接器資訊，您必須具有 Azure 訂用帳戶
- 您必須至少有一個已設定的 Application Insights 資源。
- 您必須是 hello 的 hello 擁有者或參與者 Application Insights 資源。

## <a name="configuration"></a>組態

1. 啟用從 hello hello Azure Web 應用程式分析解決方案[Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ApplicationInsights?tab=Overview)或使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。
2. 在 hello OMS 入口網站中，按一下 **設定** &gt; **資料** &gt; **Application Insights**。
3. 在 [選取訂用帳戶] 之下，選取擁有 Application Insights 資源的訂用帳戶，然後在 [應用程式名稱] 之下，選取一或多個應用程式。
4. 按一下 [儲存] 。

在大約 30 分鐘內，資料就會變成可用，且 hello Application Insights 磚以更新資料，如同下列映像的 hello:

![Application Insights 圖格](./media/log-analytics-app-insights-connector/app-insights-tile.png)

請注意其他點 tookeep:

- 您可以只將 Application Insights 應用程式 tooone OMS 工作區的連結。
- 您只能連結[Standard 或 Premium Application Insights 資源](https://azure.microsoft.com/pricing/details/application-insights)tooOMS 記錄分析。 不過，您可以使用記錄分析的 hello 免費層。

## <a name="management-packs"></a>管理組件

此解決方案不會在已連線的管理群組中安裝任何管理組件。

## <a name="use-hello-solution"></a>使用 hello 方案

hello 下列章節說明如何使用 hello Application Insights 儀表板 tooview 所示的 hello 刀鋒視窗，並從您的應用程式與資料互動。

### <a name="view-application-insights-connector-information"></a>檢視 Application Insights Connector 資訊

按一下 hello **Application Insights**磚 tooopen hello **Application Insights**儀表板 toosee hello 遵循刀鋒視窗。

![Application Insights 儀表板](./media/log-analytics-app-insights-connector/app-insights-dash01.png)

![Application Insights 儀表板](./media/log-analytics-app-insights-connector/app-insights-dash02.png)

hello 儀表板包含顯示 hello 資料表中的 hello 刀鋒視窗。 每個刀鋒視窗會列出 too10 hello 刀鋒視窗的準則指定領域和時間範圍比對的項目。 您可以執行記錄搜尋，傳回所有記錄，當您按一下**查看所有**底部 hello 的 hello 刀鋒視窗，或當您按一下 hello 刀鋒視窗中的標頭。

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| **資料行** | **說明** |
| --- | --- |
| 應用程式 - 應用程式的數目 | 在應用程式資源會顯示 hello 應用程式數目。 也列出應用程式名稱，並針對每個，hello 應用程式記錄的計數。 按一下 hello 數字 toorun 記錄搜尋<code>Type=ApplicationInsights &#124; measure sum(SampledCount) by ApplicationName</code> <br><br>  按一下 [應用程式名稱 toorun hello 應用程式會顯示每個主控件、 記錄遙測類型和類型 （根據 hello 最後一天） 的所有資料的應用程式記錄的記錄搜尋]。 |
| 資料量 - 傳送資料的主機 | 顯示傳送資料的電腦主機的 hello 數目。 也會列出電腦主機和每部主機的記錄計數。 按一下 hello 數字 toorun 記錄搜尋<code>Type=ApplicationInsights &#124; measure sum(SampledCount) by Host</code> <br><br> 按一下電腦名稱 toorun hello 主機會顯示每個主控件、 記錄遙測類型和類型 （根據 hello 最後一天） 的所有資料的應用程式記錄的記錄搜尋。 |
| 可用性 – Webtest 結果 | 顯示 Web 測試結果的環圈圖，指出成功或失敗。 按一下 hello 圖表 toorun 記錄搜尋<code>Type=ApplicationInsights TelemetryType=Availability &#124; measure sum(SampledCount) by AvailabilityResult</code> <br><br> 結果會顯示 hello 階段，以及所有測試的失敗數目。 它會顯示 hello 過去一分鐘的所有 Web 應用程式的流量。 按一下 [應用程式名稱 tooview 記錄搜尋] 顯示失敗的 web 測試的詳細資料。 |
| 伺服器要求 – 每小時的要求 | Hello 折線圖會顯示每小時的各種應用程式伺服器要求。 將滑鼠停留在 hello 圖表 toosee hello 前 3 個應用程式接收的時間點的要求中的資料行。 也會顯示 hello 接收要求和要求的 hello 數目 hello 選取期間的應用程式清單。 <br><br>按一下 記錄搜尋 hello 圖形 toorun <code>Type=ApplicationInsights TelemetryType=Request &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> ，它會顯示更詳細的折線圖的 hello 每小時的各種應用程式伺服器要求。 <br><br> 按一下 hello 清單 toorun 中的應用程式記錄檔搜尋<code>Type=ApplicationInsights  ApplicationName=yourapplicationname  TelemetryType=Request</code>的回應碼顯示的要求，圖表的時間和要求的持續期間內要求和要求一份清單。   |
| 失敗 – 每小時失敗的要求 | 顯示每小時失敗的應用程式要求折線圖。 將滑鼠停留在 hello 圖表 toosee hello 前 3 個應用程式與某個點的失敗要求的時間。 也會顯示每個應用程式與 hello 失敗要求數目的清單。 按一下 記錄搜尋 hello 圖表 toorun <code>Type=ApplicationInsights TelemetryType=Request  RequestSuccess = false &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> ，它會顯示失敗的應用程式要求的更詳細的線條圖。 <br><br>按一下 記錄搜尋 hello 清單 toorun 中的項目<code>Type=ApplicationInsights ApplicationName=yourapplicationname TelemetryType=Request  RequestSuccess=false</code>顯示失敗的要求，圖表一段時間和要求的持續時間和失敗的要求回應碼清單失敗的要求。 |
| 例外狀況 – 每小時的例外狀況 | 顯示每小時的例外狀況折線圖。 將滑鼠停留在 hello 圖表 toosee hello 前 3 個應用程式與點的例外狀況的時間。 也會顯示與每個例外狀況的 hello 數目的應用程式清單。 按一下 記錄搜尋 hello 圖表 toorun <code>Type=ApplicationInsights TelemetryType=Exception &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> ，它會顯示更詳細的連結圖表的例外狀況。 <br><br>按一下 記錄搜尋 hello 清單 toorun 中的項目<code>Type=ApplicationInsights  ApplicationName=yourapplicationname TelemetryType=Exception</code>，它會顯示一份例外狀況，圖表的時間和失敗的要求，透過例外狀況的例外狀況類型的清單。  |

### <a name="view-hello-application-insights-perspective-with-log-search"></a>檢視 hello Application Insights 觀點來看，使用記錄搜尋

當您按一下 hello 儀表板中的任何項目時，您會看到搜尋 顯示的 Application Insights 檢視方塊。 hello 檢視方塊提供延伸的視覺效果，根據所選取的 hello 遙測類型。 因此，視覺效果內容會隨著不同的遙測類型而改變。

當您按一下任何位置 hello 應用程式 刀鋒視窗時，請參閱 hello 預設**應用程式**檢視方塊。

![Application Insights 應用程式檢視方塊](./media/log-analytics-app-insights-connector/applications-blade-drill-search.png)

hello 檢視方塊會顯示您選取的 hello 應用程式的概觀。

hello**可用性**刀鋒視窗中顯示不同的觀點檢視您可以在其中看到 web 測試結果和相關的失敗的要求。

![Application Insights 可用性檢視方塊](./media/log-analytics-app-insights-connector/availability-blade-drill-search.png)

當您按一下任一處 hello**伺服器要求**或**失敗**刀鋒視窗中，元件變更 toogive hello 觀點來看您相關 toorequests 的視覺效果。

![Application Insights 失敗刀鋒視窗](./media/log-analytics-app-insights-connector/server-requests-failures-drill-search.png)

當您按一下任一處 hello**例外狀況**刀鋒視窗中，您會看到的視覺效果量身訂做 tooexceptions。

![Application Insights 例外狀況刀鋒視窗](./media/log-analytics-app-insights-connector/exceptions-blade-drill-search.png)

不論您選取 項目一個 hello**應用程式 Insights 連接器**hello 中的儀表板**搜尋**頁面本身，Application Insights 資料會顯示 hello 沒有傳回任何查詢應用程式 Insights 檢視方塊。 例如，如果您正在檢視 Application Insights 資料**&#42;**查詢也會顯示類似下列映像的 hello hello 檢視方塊索引標籤：

![Application Insights ](./media/log-analytics-app-insights-connector/app-insights-search.png)

檢視方塊元件會根據 hello 搜尋查詢更新。 這表示您可以藉由使用讓 hello 能力 toosee hello 資料從任何搜尋欄位篩選 hello 結果：

- 所有應用程式
- 單一選取的應用程式
- 應用程式群組

### <a name="pivot-tooan-app-in-hello-azure-portal"></a>在 hello Azure 入口網站中的樞紐分析 tooan 應用程式

應用程式 Insights Connector 刀鋒視窗會設計的 tooenable toopivot toohello 選取 Application Insights 應用程式*當您使用 hello OMS 入口網站*。 您可以使用 hello 解決方案做為概要監視平台，可協助您疑難排解應用程式。 當您在任何已連線應用程式中看到有潛在的問題時，您可以在 OMS 搜尋中的任一切入到它，或可以直接切換 toohello Application Insights 應用程式。

toopivot，按一下 hello 省略符號 (**...**)，會出現在 hello 結尾每一行，並選取**開啟 Application Insights 中**。

>[!NOTE]
>**開啟 Application Insights 中**不適用於 hello Azure 入口網站。

![開啟 Application Insights](./media/log-analytics-app-insights-connector/open-in-app-insights.png)

### <a name="sample-corrected-data"></a>取樣更正資料

Application Insights 提供*[取樣更正](../application-insights/app-insights-sampling.md)* toohelp 減少遙測流量。 當您在 Application Insights 應用程式上啟用取樣功能時，您取得之 Application Insights 和 OMS 中儲存的項目數會減少。 雖然資料的一致性會保留在 hello**應用程式 Insights 連接器**頁面和檢視方塊，您應手動更正您的自訂查詢的取樣的資料。

在記錄搜尋查詢中取樣更正的範例如下：

```
Type=ApplicationInsights | measure sum(SampledCount) by TelemetryType
```

hello**取樣計數**欄位中的所有項目存在，而且顯示 hello hello 項目所代表的資料點數目。 如果您開啟 Application Insights 應用程式的取樣功能，[取樣計數] 會大於 1。 toocount hello 實際的項目數會產生您的應用程式，總和 hello**取樣計數**欄位。

取樣會影響只有 hello 總數的應用程式產生的項目。 您不需要 toocorrect 取樣針對度量的欄位類似**RequestDuration**或**AvailabilityDuration**因為這些欄位會顯示 hello 平均值表示項目。

## <a name="input-data"></a>輸入資料

hello 解決方案接收 hello 已連線的 Application Insights 應用程式中的下列遙測類型的資料：

- Availability
- 例外狀況
- Requests
- 工作區 tooreceive 的頁面檢視表-頁面檢視，您必須設定您的應用程式 toocollect 該資訊。 如需詳細資訊，請參閱 [PageViews](../application-insights/app-insights-api-custom-events-metrics.md#page-views)。
- 自訂事件 – 為您工作區 tooreceive 的自訂事件，您必須設定您的應用程式 toocollect 該資訊。 如需詳細資訊，請參閱 [TrackEvent](../application-insights/app-insights-api-custom-events-metrics.md#trackevent)。

資料可用時，是由 OMS 從 Application Insights 接收。

## <a name="output-data"></a>輸出資料

對於每種類型的輸入資料，系統會建立「類型」 為 ApplicationInsights 的記錄。 ApplicationInsights 記錄都有屬性 hello 下列各節所示：

### <a name="generic-fields"></a>一般欄位

| 屬性 | 說明 |
| --- | --- |
| 類型 | ApplicationInsights |
| ClientIP |   |
| TimeGenerated | Hello 記錄的時間 |
| ApplicationId | Hello Application Insights 應用程式的檢測金鑰 |
| ApplicationName | Hello Application Insights 應用程式的名稱 |
| RoleInstance | 伺服器主機的識別碼 |
| DeviceType | 用戶端裝置 |
| ScreenResolution |   |
| Continent | 大陸參予 hello 要求 |
| 國家 (地區) | Hello 要求產生所在的國家/地區 |
| Province | 市、 省/市或位置 hello 要求源自的地區設定 |
| City | Hello 要求參予的城鎮或城市 |
| isSynthetic | 指出是否由使用者或自動的方法建立 hello 要求。 True = 使用者產生，或 false = 自動化方法 |
| SamplingRate | Hello 傳送 tooportal SDK 所產生的遙測的百分比。 範圍 0.0-100.0。 |
| SampledCount | 100/(SamplingRate)。 例如，4 =&gt; 25% |
| IsAuthenticated | True 或 False |
| OperationID | 具有相同的作業識別碼時，會顯示為相關項目上，在 hello 入口網站中的 hello 的項目。 通常 hello 要求識別碼 |
| ParentOperationID | Hello 父作業的識別碼 |
| OperationName |   |
| SessionId | GUID toouniquely 識別 hello hello 要求建立所在的工作階段 |
| SourceSystem | ApplicationInsights |

### <a name="availability-specific-fields"></a>可用性專屬欄位

| 屬性 | 說明 |
| --- | --- |
| TelemetryType | Availability |
| AvailabilityTestName | Hello web 測試的名稱 |
| AvailabilityRunLocation | http 要求的地理區域來源 |
| AvailabilityResult | 指出 hello 成功 hello web 測試結果 |
| AvailabilityMessage | hello 訊息附加 toohello web 測試 |
| AvailabilityCount | 100/(Sampling Rate)。 例如，4 =&gt; 25% |
| DataSizeMetricValue | 1.0 或 0.0 |
| DataSizeMetricCount | 100/(Sampling Rate)。 例如，4 =&gt; 25% |
| AvailabilityDuration | 時間 （毫秒），hello web 測試的持續時間 |
| AvailabilityDurationCount | 100/(Sampling Rate)。 例如，4 =&gt; 25% |
| AvailabilityValue |   |
| AvailabilityMetricCount |   |
| AvailabilityTestId | Hello web 測試的唯一 GUID |
| AvailabilityTimestamp | Hello 可用性測試的精確時間戳記 |
| AvailabilityDurationMin | 取樣的資料錄，此欄位會顯示 hello 最小的 web 測試持續期間 （毫秒） hello 表示資料點 |
| AvailabilityDurationMax | 取樣的資料錄，此欄位會顯示 hello 最大的 web 測試持續期間 （毫秒） hello 表示資料點 |
| AvailabilityDurationStdDev | 此欄位會顯示 hello hello 表示資料點的所有 web 測試期間 （毫秒） 之間的標準差取樣的資料錄 |
| AvailabilityMin |   |
| AvailabilityMax |   |
| AvailabilityStdDev | &nbsp;  |

### <a name="exception-specific-fields"></a>例外狀況專屬欄位

| 類型 | ApplicationInsights |
| --- | --- |
| TelemetryType | 例外狀況 |
| ExceptionType | Hello 例外狀況類型 |
| ExceptionMethod | 建立 hello 例外狀況的 hello 方法 |
| ExceptionAssembly | 組件包括 hello 架構和版本以及 hello 公開金鑰語彙基元 |
| ExceptionGroup | Hello 例外狀況類型 |
| ExceptionHandledAt | 表示處理 hello 例外狀況的 hello 層級 |
| ExceptionCount | 100/(Sampling Rate)。 例如，4 =&gt; 25% |
| ExceptionMessage | Hello 例外狀況的訊息 |
| ExceptionStack | Hello 例外狀況的完整堆疊 |
| ExceptionHasStack | 如果例外狀況有一個堆疊，則為 True |



### <a name="request-specific-fields"></a>要求專屬欄位

| 屬性 | 說明 |
| --- | --- |
| 類型 | ApplicationInsights |
| TelemetryType | 要求 |
| ResponseCode | HTTP 傳送回應 tooclient |
| RequestSuccess | 指出成功或失敗。 True 或 False。 |
| RequestID | 識別碼 toouniquely 識別 hello 要求 |
| RequestName | GET/POST + URL 基底 |
| RequestDuration | 時間，以秒為單位 hello 要求持續時間 |
| URL | Hello 要求不包含主控件的 URL |
| Host | Web 伺服器主機 |
| URLBase | Hello 要求的完整 URL |
| ApplicationProtocol | Hello 應用程式所使用的通訊協定類型 |
| RequestCount | 100/(Sampling Rate)。 例如，4 =&gt; 25% |
| RequestDurationCount | 100/(Sampling Rate)。 例如，4 =&gt; 25% |
| RequestDurationMin | 取樣的資料錄，此欄位會顯示 hello 表示資料點 hello 最小要求持續時間 （毫秒）。 |
| RequestDurationMax | 取樣的資料錄，此欄位會顯示 hello 表示資料點 hello 最大要求持續時間 （毫秒） |
| RequestDurationStdDev | 此欄位會顯示 hello 所有要求持續時間 （毫秒） hello 表示資料點之間的標準差取樣的資料錄 |

## <a name="sample-log-searches"></a>記錄檔搜尋範例

此解決方案並沒有一組範例顯示 hello 儀表板上的記錄搜尋。 不過，範例記錄搜尋查詢，並說明顯示 hello[檢視應用程式 Insights 連接器資訊](#view-application-insights-connector-information)> 一節。

## <a name="next-steps"></a>後續步驟

- 使用[記錄搜尋](log-analytics-log-searches.md)tooview 詳細 Application Insights 應用程式的資訊。
