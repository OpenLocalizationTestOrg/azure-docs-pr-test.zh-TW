---
title: "aaaLog Analytics 常見問題集 |Microsoft 文件"
description: "Hello Azure 記錄分析服務相關常見問題的解答 toofrequently。"
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ad536ff7-2c60-4850-a46d-230bc9e1ab45
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 25931f521cbb6ec840184221c6c1a5794b3445f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-faq"></a>Log Analytics 常見問題集
此 Microsoft 常見問題集是 Microsoft Operations Management Suite (OMS) 中 Log Analytics 常見問題的清單。 如果您有任何關於記錄分析的其他問題，請移至 toohello[討論區論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights)並張貼您的問題。 當常見問題集問題時，我們將其新增 toothis 發行項，讓它可以快速且輕鬆地找到。

## <a name="general"></a>一般

### <a name="q-does-log-analytics-use-hello-same-agent-as-azure-security-center"></a>問： 記錄分析會使用 hello 以 Azure 資訊安全中心的相同代理程式嗎？

A. Azure 資訊安全中心早期年 6 月 2017，開始使用 hello Microsoft Monitoring Agent toocollect 和存放區資料。 詳細資訊，請參閱 toolearn [Azure 安全性 Center 平台移轉常見問題集](../security-center/security-center-platform-migration-faq.md)。

### <a name="q-what-checks-are-performed-by-hello-ad-and-sql-assessment-solutions"></a>問： Hello AD 和 SQL 評估解決方案會執行哪些檢查？

A. hello 下列查詢顯示目前執行的所有檢查的描述：

```
(Type=SQLAssessmentRecommendation OR Type=ADAssessmentRecommendation) | dedup RecommendationId | select FocusArea, ActionArea, Recommendation, Description | sort Type, FocusArea,ActionArea, Recommendation
```

hello 結果可以匯出的 tooExcel 供進一步檢閱。

### <a name="q-why-do-i-see-something-different-than-oms-in-system-center-operations-manager-console"></a>問：為什麼我在 System Center Operations Manager 主控台中看到與 *OMS* 不同的項目？

答：根據您所採用的 Operations Manager 更新彙總套件而定，您可能會看到 *System Center Advisor*、*Operational Insights* 或 *Log Analytics* 節點。

太 hello 文字字串更新*OMS*包含需要 toobe 手動方式匯入管理組件中。 toosee hello 目前的文字和功能，依照 hello 指示 hello 最新版 System Center Operations Manager 更新彙總套件知識庫文件並重新整理 hello 主控台。

### <a name="q-is-there-an-on-premises-version-of-log-analytics"></a>問：Log Analytics 是否有「內部部署」版本？

答：否。 Log Analytics 可以處理並儲存大量資料。 為雲端服務時，記錄分析會無法 tooscale 接如有必要，並避免任何效能影響 tooyour 環境。

其他優點包括：
- Microsoft 執行 hello 記錄分析基礎結構，您節省成本
- 定期部署功能更新和修正程式。

### <a name="q-how-do-i-troubleshoot-that-log-analytics-is-no-longer-collecting-data"></a>問： 如何針對 Log Analytics 不再收集資料的問題進行疑難排解？

答： 如果您是 hello 免費定價層上，而且已在一天傳送超過 500 MB 的資料，就會停止 hello rest hello 一天的資料收集。 到達 hello 每日限制為記錄分析會停止收集資料，一個常見原因，或出現 toobe 資料遺失。

當資料收集開始及停止時，Log Analytics 會建立 *Operation* 類型的事件。 

執行下列查詢中搜尋 toocheck，如果您是達到 hello 每日限制，而且找不到資料的 hello:`Type=Operation OperationCategory="Data Collection Status"`

當資料收集會停止，hello *OperationStatus*是**警告**。 當資料收集開始，hello *OperationStatus*是**Succeeded**。 

hello 下表描述停止資料收集的原因和建議的動作 tooresume 資料收集：

| 資料收集停止的原因                       | tooresume 資料收集 |
| -------------------------------------------------- | ----------------  |
| 已達免費資料的每日限制<sup>1</sup>       | 等候 hello 下列天集合 tooautomatically 重新啟動，或<br> 變更 tooa 付費定價層 |
| Azure 訂用帳戶處於暫停狀態，原因如下： <br> 免費試用已結束 <br> Azure Pass 已過期 <br> 已達每月消費限制 (例如 MSDN 或 Visual Studio 訂閱)                          | 轉換 tooa 付費訂用帳戶 <br> 轉換 tooa 付費訂用帳戶 <br> 移除限制，或等到限制重設 |

<sup>1</sup>如果您的工作區在 hello 免費定價層，您只能 toosending 500 MB 的每個日期 toohello 服務的資料。 達到 hello 每日限制，就會停止資料收集直到隔天 hello。 在資料收集停止時所傳送的資料不會編製索引，而且無法供搜尋使用。 當資料收集繼續時，只會處理傳送的新資料。 

Log Analytics 使用 UTC 時間，而且每天從午夜 UTC 開始。 如果 hello 工作區已達到 hello 每日限制，處理會繼續在 hello 第一個小時的 hello 下一步的 UTC 日。

### <a name="q-how-can-i-be-notified-when-data-collection-stops"></a>問： 如何在資料收集停止時收到通知？

答： 請使用 hello 中所述的步驟[建立警示規則](log-analytics-alerts-creating.md#create-an-alert-rule)toobe 通知時停止資料收集。

在建立 hello 警示停止資料收集時，設定:
- **名稱**太*停止資料收集*
- **嚴重性**太*警告*
- **搜尋查詢**太`Type=Operation OperationCategory="Data Collection Status" OperationStatus=Warning`
- **時間間隔**太*2 小時*。
- **警示頻率**toobe 一小時後 hello 使用量資料只會更新每小時一次。
- **產生警示根據**toobe*的結果數目*
- **結果數目**toobe*大於 0*

使用中所述的 hello 步驟[新增動作 tooalert 規則](log-analytics-alerts-actions.md)設定電子郵件、 webhook 或 runbook hello 警示規則的動作。


## <a name="configuration"></a>組態
### <a name="q-can-i-change-hello-name-of-hello-tableblob-container-used-tooread-from-azure-diagnostics-wad"></a>問： 我可以變更 hello 資料表 /blob 容器使用 tooread hello 名稱從 Azure 診斷 (WAD)？

A. 否，它不是目前 tooread 任意的資料表或容器中的 Azure 儲存體中。

### <a name="q-what-ip-addresses-does-hello-log-analytics-service-use-how-do-i-ensure-that-my-firewall-only-allows-traffic-toohello-log-analytics-service"></a>問： IP 的位址沒有 hello 記錄分析服務使用嗎？ 如何確定我的防火牆只允許流量 toohello 記錄分析服務？

A. hello 記錄分析服務建置在 Azure 之上。 記錄分析 IP 位址皆位於 hello [Microsoft Azure Datacenter IP 範圍](http://www.microsoft.com/download/details.aspx?id=41653)。

進行服務部署時，變更的記錄分析服務 hello hello 實際 IP 位址。 hello DNS 名稱 tooallow 通過防火牆會記載於[中記錄分析設定 proxy 和防火牆設定](log-analytics-proxy-firewall.md)。

### <a name="q-i-use-expressroute-for-connecting-tooazure-does-my-log-analytics-traffic-use-my-expressroute-connection"></a>問： 我使用 ExpressRoute 連線 tooAzure。 我的 Log Analytics 流量是否會使用我的 ExpressRoute 連線？

A. hello 不同類型的 ExpressRoute 流量描述 hello [ExpressRoute 文件](../expressroute/expressroute-faqs.md#supported-services)。

流量 tooLog 分析會使用 hello 公用對等 ExpressRoute 循環。

### <a name="q-is-there-a-simple-and-easy-way-toomove-an-existing-log-analytics-workspace-tooanother-log-analytics-workspaceazure-subscription"></a>問： 是否有簡單輕鬆的方式 toomove 現有的記錄分析工作區 tooanother 記錄分析工作區 /azure 訂用帳戶？

A. hello `Move-AzureRmResource` cmdlet 可讓您從一個 Azure 訂用帳戶 tooanother 移動記錄分析工作區以及自動化帳戶。 如需詳細資訊，請參閱 [Move-AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx)。

這項變更也進行 hello Azure 入口網站中。

您無法將資料從一個記錄分析工作區 tooanother，移動或變更記錄分析資料會儲存在 hello 區域。

### <a name="q-how-do-i-add-log-analytics-toosystem-center-operations-manager"></a>問： 如何加入記錄分析 tooSystem Center Operations Manager？

答： 更新 toohello 最新的更新彙總，以及匯入管理組件可讓您 tooconnect Operations Manager tooLog 分析。

>[!NOTE]
>hello Operations Manager 連線 tooLog 分析才可使用 System Center Operations Manager 2012 SP1 和更新版本。

### <a name="q-how-can-i-confirm-that-an-agent-is-able-toocommunicate-with-log-analytics"></a>問： 如何確認代理程式是可以 toocommunicate 記錄分析？

答： tooensure hello 代理程式可以與 OMS 通訊，請移至： 控制台、 安全性和設定， **Microsoft Monitoring Agent**。

在 hello **Azure 記錄分析 (OMS)**索引標籤中，找出綠色的核取記號。 綠色核取記號圖示可確認該 hello 代理程式無法 toocommunicate 以 hello OMS 服務。

黃色警告圖示表示 hello 代理程式的通訊出現問題與 OMS。 一個常見的原因是 hello Microsoft Monitoring Agent 服務已停止。 使用服務控制管理員 toorestart hello 服務。

### <a name="q-how-do-i-stop-an-agent-from-communicating-with-log-analytics"></a>問：如何阻止代理程式與 Log Analytics 通訊？

答： 在 System Center Operations Manager，會移除 hello Advisor 受管理的電腦清單中的 hello 電腦。 Operations Manager 更新 hello hello 代理程式 toono 長報表 tooLog Analytics 的組態。 代理程式已直接連接 tooLog 分析，您可以停止其通訊透過： 控制台、 安全性和設定， **Microsoft Monitoring Agent**。
在 **Azure Log Analytics (OMS)** 下，移除所有列出的工作區。

### <a name="q-why-am-i-getting-an-error-when-i-try-toomove-my-workspace-from-one-azure-subscription-tooanother"></a>問： 為什麼我會收到錯誤當我嘗試 toomove 我的工作區，從一個 Azure 訂用帳戶 tooanother？

答： 如果您使用 hello Azure 入口網站，確定只 hello 工作區中已選取 hello 移動。 未選取 hello 解決方案--它們會自動移動 hello 工作區中移動之後。 

請確定您具有這兩個 Azure 訂用帳戶的權限。

## <a name="agent-data"></a>代理程式資料
### <a name="q-how-much-data-can-i-send-through-hello-agent-toolog-analytics-is-there-a-maximum-amount-of-data-per-customer"></a>問： 透過 hello 代理程式 tooLog 分析可以傳送多少資料？ 是否有每位客戶最大的資料量？
A. hello 免費方案設定每個工作區的每日最高量為 500 MB。 hello 標準和高階計劃對 hello 上傳的資料量沒有限制。 記錄分析作為雲端服務，其設計 toohandle hello 磁碟區的小數位數 tooautomatically 來自客戶 – 即使它是每日 tb。

hello 記錄分析代理程式已設計的 tooensure 其使用量很小。 我們的客戶的其中一個有關 hello 測試他們對我們的代理程式 」 和 「 如何它們深刻撰寫部落格。 hello 資料量會根據您啟用的 hello 解決方案而異。 您可以尋找 hello 資料磁碟區上的詳細的資訊，並依據解決方案 hello 查看 hello 各部分[使用量](log-analytics-usage.md)頁面。

如需詳細資訊，您可以閱讀[客戶部落格](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html)有關 hello hello OMS 代理程式的低使用量。

### <a name="q-how-much-network-bandwidth-is-used-by-hello-microsoft-management-agent-mma-when-sending-data-toolog-analytics"></a>問： 傳送資料 tooLog 分析時 hello Microsoft 管理代理程式 (MMA) 會使用多少網路頻寬？

A. 頻寬是傳送資料的 hello 數量上的函式。 透過 hello 網路傳送時會受到壓縮資料。

### <a name="q-how-much-data-is-sent-per-agent"></a>問： 每個代理程式會傳送多少資料？

A. 每個代理程式傳送資料的 hello 數量而定：

* 您已啟用的 hello 解決方案
* 正在收集計數器的記錄檔和效能的 hello 數目
* hello hello 記錄檔中的資料量

hello 免費定價層是很好的方式 tooonboard 幾部量測計與 hello 一般資料量。 整體使用量會顯示在 hello[使用量](log-analytics-usage.md)頁面。

無法 toorun hello WireData 代理程式電腦，使用下列查詢 toosee 正在傳送多少資料 hello:

```
Type=WireData (ProcessName="C:\\Program Files\\Microsoft Monitoring Agent\\Agent\\MonitoringHost.exe") (Direction=Outbound) | measure Sum(TotalBytes) by Computer
```



## <a name="next-steps"></a>後續步驟
* [開始使用記錄分析](log-analytics-get-started.md)toolearn 深入了解記錄分析，以及如何取得最新且正在執行，以分鐘為單位。
