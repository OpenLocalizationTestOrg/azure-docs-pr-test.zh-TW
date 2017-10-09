---
title: "Azure Web 應用程式分析資料 aaaView |Microsoft 文件"
description: "您可以使用 Azure Web 應用程式有關的 hello Azure Web 應用程式分析解決方案 toogain insights 藉由收集不同的度量資訊，透過 Azure Web 應用程式的所有資源。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 20ff337f-b1a3-4696-9b5a-d39727a94220
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: banders
ms.openlocfilehash: 7e9725f95c9faf01da89184975ad5444dd19ff95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-analytic-data-for-metrics-across-all-your-azure-web-app-resources"></a>檢視所有 Azure Web 應用程式資源之間的計量分析資料

![Web Apps 符號](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-symbol.png)  
hello Azure Web 應用程式分析 （預覽） 解決方案提供深入了解您[Azure Web Apps](../app-service-web/app-service-web-overview.md)藉由收集不同的度量資訊，透過 Azure Web 應用程式的所有資源。 Hello 方案，您可以分析，並搜尋的 web 應用程式資源的度量資料。

使用 hello 方案，您可以檢視:

- 具有 hello 最高的回應時間的最上層 Web 應用程式
- 整個 Web Apps 間的要求數，包括成功與失敗的要求
- 傳入和傳出流量最高的 Web Apps 排行榜
- CPU 與記憶體使用率最高的服務方案排行榜
- Azure Web Apps 活動記錄作業

## <a name="connected-sources"></a>連接的來源

不同於大部分其他 Log Analytics 解決方案，代理程式不會收集 Azure Web Apps 的資料。 Hello 方案所使用的所有資料都是直接來自 Azure。

| 連接的來源 | 支援 | 說明 |
| --- | --- | --- |
| [Windows 代理程式](log-analytics-windows-agents.md) | 否 | hello 方案不會從 Windows 代理程式收集的資訊。 |
| [Linux 代理程式](log-analytics-linux-agents.md) | 否 | hello 解決方案不會收集從 Linux 代理程式的資訊。 |
| [SCOM 管理群組](log-analytics-om-agents.md) | 否 | hello 方案不會從已連線的 SCOM 管理群組中的代理程式收集的資訊。 |
| [Azure 儲存體帳戶](log-analytics-azure-storage.md) | 否 | hello 方案會從 Azure 儲存體不收集資訊。 |

## <a name="prerequisites"></a>必要條件

- tooaccess Azure Web 應用程式資源的度量資訊，您必須具有 Azure 訂用帳戶。

## <a name="configuration"></a>組態

執行下列步驟為您的工作區 tooconfigure hello Azure Web 應用程式分析解決方案的 hello。

1. 啟用從 hello Azure Web 應用程式分析解決方案[Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview)或使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。
2. [啟用使用 PowerShell 的 Azure 資源計量記錄 tooOMS](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell)。

hello Azure Web 應用程式分析解決方案會從 Azure 收集兩組度量：

- Azure Web Apps 計量
  - 平均記憶體工作集
  - 平均回應時間
  - 已接收/傳送的位元組
  - CPU 時間
  - 要求
  - 記憶體工作集
  - Httpxxx
- App Service 方案計量
  - 已接收/傳送的位元組
  - CPU 百分比
  - 磁碟佇列長度
  - Http 佇列長度
  - 記憶體百分比

如果您使用的是專用的服務方案，則只會收集 App Service 方案計量。 這不會套用 toofree 或共用 App Service 方案。

如果您新增使用 hello OMS 入口網站的 hello 解決方案，您會看到 hello 下列磚。 您需要[啟用使用 PowerShell 的 Azure 資源計量記錄 tooOMS](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell)。

![執行評估通知](./media/log-analytics-azure-web-apps-analytics/performing-assessment.png)

設定 hello 方案之後，資料應該開始送 tooyour 15 分鐘內的工作區。

## <a name="using-hello-solution"></a>使用 hello 解決方案

當您新增 hello Azure Web 應用程式分析解決方案 tooyour 工作區時，hello **Azure Web 應用程式分析**tooyour 概觀儀表板的磚加入。 此磚會顯示 hello hello 方案具有存取 tooin 您 Azure 訂用帳戶的 Azure Web 應用程式數目的計數。

![Azure Web Apps 分析圖格](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-tile.png)

### <a name="view-azure-web-apps-analytics-information"></a>檢視 Azure Web Apps 分析資訊

按一下 hello **Azure Web 應用程式分析**磚 tooopen hello **Azure Web 應用程式分析**儀表板。 hello 儀表板會納入 hello 下表中的 hello 刀鋒視窗。 每個刀鋒視窗會列出 tooten hello 刀鋒視窗的準則指定領域和時間範圍比對的項目。 您可以執行，即可傳回的所有記錄的記錄搜尋**查看所有**底部 hello 的 hello 刀鋒視窗，或按一下 hello 刀鋒視窗中的標頭。

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| 資料欄 | 說明 |
| --- | --- |
| Azure Web Apps |   |
| Web Apps 要求趨勢 | 顯示的 hello hello 日期範圍內，您已選取的 Web 應用程式要求趨勢的折線圖，顯示 hello 前十個 web 要求的清單。 按一下 hello 行圖表 toorun 記錄搜尋<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* (MetricName=Requests OR MetricName=Http*) &#124; measure avg(Average) by MetricName interval 1HOUR</code> <br>按一下 web 要求的項目 toorun hello web 要求度量趨勢，要求的記錄搜尋。 |
| Web Apps 回應時間 | 顯示 hello Web 應用程式回應時間，您已選取的 hello 日期範圍內的折線圖。 也 hello 一份清單會顯示前十個 Web 應用程式回應時間。 按一下 hello 圖表 toorun 記錄搜尋<code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* MetricName="AverageResponseTime" &#124; measure avg(Average) by Resource interval 1HOUR</code><br> 按一下 Web 應用程式 toorun 傳回 hello Web 應用程式的回應時間的記錄搜尋。 |
| Web Apps 流量 | 以 mb 為單位顯示折線圖的 Web 應用程式的流量，並列出 hello 頂端 Web 應用程式的流量。 按一下 hello 圖表 toorun 記錄搜尋<code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"*  MetricName=BytesSent OR BytesReceived &#124; measure sum(Average) by Resource interval 1HOUR</code><br> 它會顯示 hello 過去一分鐘的所有 Web 應用程式的流量。 按一下 記錄搜尋，顯示位元組接收和傳送 hello Web 應用程式的 Web 應用程式 toorun。 |
| Azure App Service 方案 |   |
| CPU 使用率 &gt; 80% 的 App Service 方案 | 顯示應用程式服務方案具有 CPU 使用率超過 80%和清單 hello 前 10 個應用程式服務方案的 CPU 使用率 hello 的總數。 按一下 hello 總面積 toorun 記錄搜尋<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=CpuPercentage &#124; measure Avg(Average) by Resource</code><br> 它會顯示 App Service 方案清單及其平均 CPU 使用率。 按一下 應用程式服務方案的 toorun 顯示其平均 CPU 使用率記錄搜尋。 |
| 記憶體使用率 &gt; 80% 的 App Service 方案 | 顯示應用程式服務方案具有記憶體使用率超過 80%和清單 hello 前 10 個應用程式服務方案的記憶體使用量 hello 的總數。 按一下 hello 總面積 toorun 記錄搜尋<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=MemoryPercentage &#124; measure Avg(Average) by Resource</code><br> 它會顯示 App Service 方案清單及其平均記憶體使用率。 按一下 [App Service 方案的 toorun 記錄搜尋] 顯示其平均記憶體使用率。 |
| Azure Web Apps 活動記錄 |   |
| Azure Web Apps 活動稽核 | 顯示 hello 與 Web 應用程式的總數[活動記錄](log-analytics-activity.md)和清單 hello 前 10 個活動記錄檔作業。 按一下 hello 總面積 toorun 記錄搜尋<code>Type=AzureActivity ResourceProvider= "Azure Web Sites" &#124; measure count() by OperationName</code><br> 它會顯示一份 hello 活動記錄檔作業。 按一下 [活動記錄檔作業 toorun 列出 hello hello 作業記錄的記錄搜尋]。 |



### <a name="azure-web-apps"></a>Azure Web Apps 

在 hello 儀表板，您可以向下鑽研 tooget 您 Web 應用程式的度量的更多見解。 刀鋒視窗的這個第一組經過一段時間顯示 hello hello Web 應用程式要求，數目錯誤 (例如，HTTP404)、 傳輸，以及平均回應時間趨勢。 它也會顯示不同 Web Apps 的這些計量細目。

![Azure Web Apps 刀鋒視窗](./media/log-analytics-azure-web-apps-analytics/web-apps-dash01.png)

顯示您資料的主要原因是，讓您可以識別 Web 應用程式具有高的回應時間和調查 toofind hello 根本原因。 閾值限制也是套用的 toohelp 您更輕鬆地識別 hello 的問題。

- 紅色的 Web Apps 其回應時間超過 1 秒。
- 橘色的 Web Apps 其回應時間超過 0.7 秒，不到 1 秒。
- 綠色的 Web Apps 其回應時間不到 0.7 秒。

在下列記錄搜尋範例影像中的 hello，您可以看到該 hello *anugup3* web 應用程式有更高的回應時間比 hello 其他 web 應用程式。

![記錄搜尋範例](./media/log-analytics-azure-web-apps-analytics/web-app-search-example.png)

### <a name="app-service-plans"></a>App Service 方案

如果您使用專用的服務方案，則亦可收集您 App Service 方案的計量。 在這個檢視中，您會看到 CPU 或記憶體使用率高 (&gt; 80%) 的 App Service 方案。 此外也會顯示 hello 與記憶體或 CPU 使用率過高的最上層應用程式服務。 同樣地，閾值限制是套用的 toohelp 您更輕鬆地識別 hello 的問題。

- 紅色的 App Service 方案其 CPU/記憶體使用率高於 80%。
- 橘色的 App Service 方案其 CPU/記憶體使用率高於 60%，低於 80%。
- 綠色的 App Service 方案其 CPU/記憶體使用率低於 60%。

![Azure App Service 方案刀鋒視窗](./media/log-analytics-azure-web-apps-analytics/web-apps-dash02.png)

## <a name="azure-web-apps-log-searches"></a>Azure Web Apps 記錄搜尋

hello**清單的熱門 Azure Web 應用程式的搜尋查詢**會顯示所有 hello 對 Web 應用程式，提供您 Web 應用程式的資源執行的 hello 操作的深入資訊與相關的活動記錄檔。 它也會列出所有 hello 相關的作業和它們所發生的 hello 次數。

您可以使用任何 hello 記錄搜尋查詢做為起點，您可以輕鬆地建立警示。 比方說，您可能會想 toocreate 警示的度量的平均回應時間大於每 1 秒時。

## <a name="next-steps"></a>後續步驟

- 建立特定計量的[警示](log-analytics-alerts-creating.md)。
- 使用[記錄搜尋](log-analytics-log-searches.md)tooview 的詳細資訊，從您的活動記錄檔。
