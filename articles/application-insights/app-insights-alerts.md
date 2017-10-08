---
title: "在 Azure Application Insights aaaSet 警示 |Microsoft 文件"
description: "獲知回應時間緩慢、例外狀況，以及 Web 應用程式中的其他效能或使用量變更。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: f8ebde72-f819-4ba5-afa2-31dbd49509a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: e160cb173e68fda2e6d97f29da342c46b7ac4f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-alerts-in-application-insights"></a>在 Application Insights 中設定警示
[Azure 的 Application Insights] [ start]可以提醒您 toochanges 的 web 應用程式中的效能或使用量度量。 

Application Insights 監視即時應用程式上[各種不同的平台][ platforms] toohelp 您診斷效能問題，並了解使用模式。

共有三種警示︰

* **計量警示**會在計量超出某些期間的臨界值 (例如回應時間、例外狀況計數、CPU 使用量或頁面檢視) 的時候通知您。 
* [**Web 測試**] [ availability]告訴您無法在 hello 上使用您的網站是否網際網路或回應速度較慢。 [深入了解][availability]。
* [**主動式診斷**](app-insights-proactive-diagnostics.md)會自動設定 toonotify 您有關不尋常的效能模式。

在本文中，我們著重於計量警示。

## <a name="set-a-metric-alert"></a>設定計量警示
開啟 hello 警示規則刀鋒視窗中，然後再使用 hello 加入按鈕。 

![在 hello 警示規則刀鋒視窗中，選擇 [新增警示]。 設定您的應用程式為 hello 資源 toomeasure、 提供 hello 警示的名稱並選擇計量。](./media/app-insights-alerts/01-set-metric.png)

* 設定前 hello hello 資源的其他屬性。 **選擇 hello 」 （元件） 」 資源**如果您想 tooset 效能或使用量度量的警示。
* 您提供給 toohello 警示的 hello 名稱必須是唯一 hello （不只是您的應用程式） 的資源群組中。
* 能謹慎 toonote hello 單位中，系統會詢問 tooenter hello 臨界值。
* 如果您核取 hello 方塊 」 電子郵件擁有者..."，警示會傳送電子郵件 tooeveryone 擁有存取 toothis 資源群組。 tooexpand 這設定的人員，將它們加入 toohello[資源群組或訂用帳戶](app-insights-resources-roles-access-control.md)(不 hello 資源)。
* 如果您指定 「 其他電子郵件 」，則會收到通知，toothose 個人或群組 （不論您核取 hello 」 電子郵件擁有者..."方塊）。 
* 設定[webhook 位址](../monitoring-and-diagnostics/insights-webhooks-alerts.md)如果您已設定 web 應用程式回應 tooalerts。 它會呼叫啟動 hello 警示和時獲得解決。 (不過請注意，查詢參數目前不會當作 Webhook 屬性傳遞)。
* 您可以停用或啟用 hello 警示： 請參閱 < hello 在 hello hello 刀鋒視窗頂端的按鈕。

*看不見 hello 新增警示 按鈕。* 

* 您是否使用組織帳戶？ 如果您有擁有者或參與者存取 toothis 應用程式資源，您可以設定警示。 看看 hello 存取控制 刀鋒視窗。 [深入了解存取控制][roles]。

> [!NOTE]
> 在 hello 警示刀鋒視窗中，您看到已有的警示集：[主動式診斷](app-insights-proactive-failure-diagnostics.md)。 hello 自動警示監視一個特定度量，要求失敗率。 除非您決定 toodisable hello 主動式警示，您不需要 tooset 上要求失敗率警示。 
> 
> 

## <a name="see-your-alerts"></a>查看您的警示
當警示在非作用中與作用中之間變更狀態時，您會收到電子郵件。 

hello 警示規則 刀鋒視窗會顯示 hello 的每個警示的目前狀態。

下拉式清單沒有 hello 警示中的最近活動的摘要：

![警示下拉式清單](./media/app-insights-alerts/010-alert-drop.png)

hello 變更歷程記錄的狀態處於 hello 活動記錄檔：

![在 hello 概觀刀鋒視窗中，按一下 設定，稽核記錄檔](./media/app-insights-alerts/09-alerts.png)

## <a name="how-alerts-work"></a>警示的運作方式
* 警示有三種狀態：「永遠不啟動」、「已啟動」和「已解決」。 已啟動的方式 hello，已為 true，當上一次評估時指定的條件。
* 警示狀態變更時，會產生通知。 （如果 hello 警示條件已，則為 true，當您建立 hello 警示時，您可能無法取得通知之前 hello 條件變成 false。）
* 如果您檢查 hello 電子郵件 方塊中，或提供電子郵件地址，每個通知就會產生一封電子郵件。 您也可以查看 hello 通知下拉式清單。
* 每次度量抵達時都會評估警示，除此之外則無。
* hello 評估 hello 前面期間，透過彙總 hello 度量，然後比較 toohello 閾值 toodetermine hello 新狀態。
* 您選擇的 hello 期間指定 hello 彙總度量資訊會經過的時間間隔。 它並不會影響 hello 警示評估的頻率： hello 抵達的度量的頻率而定。
* 如果沒有資料到達特定度量的一些時間，hello 差距就會有警示評估和度量總管 中的 hello 圖表上不同的效果。 在度量總管中，如果沒有資料會超過 hello 圖表的取樣間隔內，看到 hello 圖表可顯示值為 0。 但警示根據 hello 相同的度量不會重新評估和 hello 警示的狀態會保持不變。 
  
    當資料最後會到達時，hello 圖表就會跳後 tooa 非零值。 評估 hello 警示根據 hello 資料可供您指定的 hello 週期。 如果只有一個可用 hello 內 hello hello 新資料點，彙總的 hello 以只在資料點。
* 即使您設定的期間較長，警示也可能會在警示和良好狀態之間經常變動。 這種情況 hello 公制值停留周圍 hello 臨界值。 Hello 臨界值中沒有任何 hysteresis: hello 轉換 tooalert 會發生在相同的值為 hello 轉換 toohealthy hello。

## <a name="what-are-good-alerts-tooset"></a>良好的警示 tooset 有哪些？
這取決於您的應用程式。 toostart，最好不 tooset 太多的度量。 花點時間查看的度量的圖表，您的應用程式執行時，tooget 感覺如何正常運作。 這種作法可協助您找到方式 tooimprove 其效能。 然後時，設定警示 tootell 您 hello 度量傳送 hello 一般區域外部。 

熱門的警示包括：

* [瀏覽器計量][client]，適合用於 Web 應用程式，尤其是瀏覽器**頁面載入時間**。 如果您的分頁有許多指令碼，您應該尋找**瀏覽器例外狀況**。 在訂單 tooget 這些度量和警示，您必須 tooset[網頁監視][client]。
* **伺服器回應時間**hello 伺服器端 web 應用程式。 以及設定警示，請留意這個度量 toosee 如果它會隨著不當比例高要求率： 變化可能表示您的應用程式時用資源不足。 
* **伺服器例外狀況**-toosee 它們，您有一些 toodo[額外安裝](app-insights-asp-net-exceptions.md)。

請記住，[主動式失敗率診斷](app-insights-proactive-failure-diagnostics.md)自動監視器 hello 速率您的應用程式會回應 toorequests 的失敗碼。 

## <a name="automation"></a>自動化
* [使用 PowerShell tooautomate 設定警告](app-insights-powershell-alerts.md)
* [使用 webhook tooautomate 回應 tooalerts](../monitoring-and-diagnostics/insights-webhooks-alerts.md)

## <a name="video"></a>影片

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="see-also"></a>另請參閱
* [可用性 Web 測試](app-insights-monitor-web-app-availability.md)
* [自動化設定警示](app-insights-powershell-alerts.md)
* [主動診斷](app-insights-proactive-diagnostics.md) 

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[platforms]: app-insights-platforms.md
[roles]: app-insights-resources-roles-access-control.md
[start]: app-insights-overview.md

