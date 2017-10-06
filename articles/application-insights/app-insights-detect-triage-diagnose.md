---
title: "DevOps 的 Azure Application Insights aaaOverview |Microsoft 文件"
description: "深入了解如何在環境中開發人員 Ops toouse Application Insights。"
author: CFreemanwa
services: application-insights
documentationcenter: 
manager: carmonm
ms.assetid: 6ccab5d4-34c4-4303-9d3b-a0f1b11e6651
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: bwren
ms.openlocfilehash: 42139f4645e815f26378726f4716a9bfbdc78551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-application-insights-for-devops"></a>DevOps 適用的 Application Insights 概觀

透過 [Application Insights](app-insights-overview.md)，您可以迅速瞭解您的應用程式在作用中時如何執行和使用。 如果沒有問題，它可讓您了解，可協助您評估 hello 影響，以及可協助您判斷 hello 可能的原因。

以下是某個開發 Web 應用程式的小組的敘述：

* *「幾天前，我們部署了次要的 Hotfix。我們未執行廣泛測試通過，但不幸的是一些未預期的變更何時合併 hello 承載，造成 hello 前端和後端之間的不相容。立即 surged 伺服器例外狀況，我們警示引發，及我們做了知道 hello 情況。按幾下的滑鼠，離開 hello Application Insights 入口網站上，我們會了足夠的資訊從例外狀況呼叫堆疊 toonarrow hello 問題。我們會立即回復，而且有限的 hello 損毀。Application Insights 進行了循環 hello devops 這部分很簡單，且可採取動作。 」*

本文章中我們會遵循小組開發 hello 的 Fabrikam 銀行線上銀行系統 (OBS) toosee 如何使用 Application Insights tooquickly 回應 toocustomers 及進行更新。  

hello 小組處理 DevOps 循環 hello 下列圖例所示：

![DevOps 循環](./media/app-insights-detect-triage-diagnose/00-devcycle.png)

送入其開發待處理項目 (工作清單) 的需求。 簡單地說，其運作通常提供工作的軟體-通常是在 hello 改良功能和擴充功能 toohello 現有應用程式表單的衝刺。 hello 即時應用程式經常會有新功能更新。 雖然是即時的 hello 小組用來監視其效能和使用 Application Insights hello 協助。 這項 APM 資料會餵送回其開發待處理項目。

hello 小組會使用 Application Insights toomonitor hello 即時 web 應用程式密切：

* 效能。 他們想要如何回應時間隨著要求計數; toounderstand多少 CPU、 網路、 磁碟和其他資源正在使用;其中 hello 瓶頸。
* 失敗。 如果有例外狀況或失敗的要求，或如果效能計數器超出舒適的範圍，hello 小組需要 tooknow 快速，讓它們可以採取的動作。
* 使用狀況。 只要已發行的新功能，hello 小組需要 tooknow toowhat 範圍使用，而且使用者是否有任何問題，與它。

讓我們重點討論 hello 意見反應部分 hello 週期：

![偵測-分級-診斷](./media/app-insights-detect-triage-diagnose/01-pipe1.png)

## <a name="detect-poor-availability"></a>偵測可用性不佳
Marcela Markova 會 hello OBS 小組的資深開發人員，並採用 hello 負責人監視線上效能。 她設定了數項[可用性測試](app-insights-monitor-web-app-availability.md)：

* Hello 應用程式中，hello 主要登陸頁面的單一 URL 測試 http://fabrikambank.com/onlinebanking/。 她設定 HTTP 代碼 200 與文字「歡迎使用！」的準則。 如果此測試失敗，則有嚴重錯誤 hello 網路或 hello 伺服器或可能的部署問題。 （或有人變更過 hello 歡迎使用 ！ 訊息不讓她知道 hello 頁面上。）
* 更深入的多步驟測試將會記錄並取得目前帳戶清單，檢查每個頁面上的一些重要詳細資料。 這項測試會驗證該 hello 連結 toohello 帳戶資料庫運作正常。 她使用虛構的客戶識別碼：其中少數幾個保留供測試目的。

這些測試設定，Marcela 是確定該 hello 團隊會快速了解任何中斷。  

失敗會顯示為 hello web 測試圖表上的紅點：

![顯示的 hello 前面期間執行的 web 測試](./media/app-insights-detect-triage-diagnose/04-webtests.png)

但是更重要的是，任何失敗相關警示以電子郵件傳送 toohello 開發團隊。 如此一來，他們得知之前幾乎全部 hello 客戶。

## <a name="monitor-performance"></a>監視效能
在 Application Insights 中的 hello 概觀頁面上，有是折線圖，顯示各種[金鑰度量](app-insights-web-monitor-performance.md)。

![各種度量](./media/app-insights-detect-triage-diagnose/05-perfMetrics.png)

瀏覽器頁面載入時間是從網頁直接傳送的遙測所衍生。 伺服器回應時間、 伺服器要求計數，以及失敗的要求計數是所有衡量 hello web 伺服器中，並從該處傳送 tooApplication 深入資訊。

Marcela 是稍微關心 hello 伺服器回應圖形。 此圖表顯示 hello 當 hello 伺服器從使用者的瀏覽器、 接收 HTTP 要求與它會傳回 hello 回應之間的平均時間。 它不是異常 toosee 變化，以在此圖中，隨著 hello 系統上的負載而改變。 但在此情況下，似乎那里 toobe 小上升 hello 計數的要求，而且其大小之間的相互關聯上升 hello 回應時間。 可能表示 hello 系統作業只在其限制。

下次開啟 hello 伺服器圖表：

![各種度量](./media/app-insights-detect-triage-diagnose/06.png)

似乎那里 toobe 沒有符號的資源限制，因此可能在 hello 伺服器回應圖表中的 hello 碰撞純屬巧合。

## <a name="set-alerts-toomeet-goals"></a>設定警示 toomeet 目標
不過，她希望 tookeep 眼睛 hello 回應時間。 如果它們移得太高，她想 tooknow 資訊，請立即。

因此，她針對回應時間大於一般臨界值的情況設定了一個[警示](app-insights-metrics-explorer.md)。 這可以確保當回應時間變慢時她就會知道。

![加入警示分頁](./media/app-insights-detect-triage-diagnose/07-alerts.png)

您可以在其他各種不同的度量上設定警示。 比方說，您可以在 hello 例外狀況計數變成高，則 hello 可用的記憶體會變低，或在用戶端要求尖峰是否收到電子郵件。

## <a name="stay-informed-with-smart-detection-alerts"></a>獲得有關智慧型偵測警示的資訊
隔天，確實收到了一封來自 Application Insights 的電子郵件。 但是當她開啟它時，她發現它不是她所設定的 hello 回應時間警示。 而是郵件告知她失敗的要求 (也就是傳回 500 或更高數字之失敗代碼的要求) 數目突然提高。

失敗的要求，則使用者已經看過的錯誤-通常遵循 hello 程式碼中擲回例外狀況。 也許他們會看到訊息指出 「抱歉，我們現在無法更新您的詳細資料。 」 或者，在絕對免於最差，堆疊傾印會出現在 hello 使用者畫面上，受 hello web 伺服器。

此警示是意外，因為 hello 她看，hello 的最後一次失敗計數偏 encouragingly 低的要求。 少量失敗是 toobe 忙碌的伺服器中必須要有。

它也是為她奇怪的位元因為她不需要 tooconfigure 此警示。 Application Insights 包含智慧型偵測。 它會自動調整 tooyour 應用程式的一般失敗模式和 「 取得用來 「 失敗的特定頁面，或者在高負載或連結的 tooother 度量。 只有當此時上升，便會產生 hello 警示決定其上方出現 tooexpect。

![主動診斷電子郵件](./media/app-insights-detect-triage-diagnose/21.png)

這封電子郵件非常有幫助。 它不只是發出警示。 它會執行許多 hello 分級和診斷的工作、 太。

它會顯示有多少客戶，以及哪些網頁或作業受到影響。 Marcela 可以決定是否需要這項工作以演習，tooget hello 整個小組，或等到下一週是否可以被忽略。

hello 電子郵件也會顯示特定的例外狀況發生，而-更有趣的該 hello 發生錯誤的失敗的呼叫 tooa 特定資料庫相關聯。 本節將說明為什麼 hello 錯誤突然出現即使 Marcela 的小組最近尚未部署的任何更新。

Marcella 偵測 hello 資料庫小組這封電子郵件為基礎的 hello 前置字元。 她會學習在發行中 hello 問題修正過去半小時。和糟糕或許可能有次要的結構描述變更...

因此 hello 問題是固定的即使之前調查記錄檔和它所產生的 15 分鐘內的 hello 方式 toobeing 上。 不過，Marcela 按一下 hello 連結 tooopen Application Insights。 它會直接進入失敗的要求，而她可以查看失敗的資料庫呼叫 hello 的相依性呼叫相關聯的清單中。

![失敗的要求](./media/app-insights-detect-triage-diagnose/23.png)

## <a name="detect-exceptions"></a>偵測例外狀況
利用最少的安裝程式，[例外狀況](app-insights-asp-net-exceptions.md)會自動回報的 tooApplication 深入資訊。 它們可以也擷取明確插入的呼叫太[之 trackexception （)](app-insights-api-custom-events-metrics.md#trackexception) hello 程式碼：  

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }


hello Fabrikam 銀行小組發展 hello 作法，一律將遙測傳送的例外狀況，除非有明顯的復原。  

事實上，其策略是比更： 將遙測傳送 hello 客戶是挫折在每個案例中他們想 toodo，是否不論對應 tooan hello 程式碼中的例外狀況。 比方說，如果 hello 外部間銀行傳輸系統因故操作 （hello 客戶的任何錯誤） 傳回 「 無法完成此交易 」 的訊息然後這些追蹤事件。

    var successCode = AttemptTransfer(transferAmount, ...);
    if (successCode < 0)
    {
       var properties = new Dictionary <string, string>
            {{ "Code", returnCode, ... }};
       var measurements = new Dictionary <string, double>
         {{"Value", transferAmount}};
       telemetry.TrackEvent("transfer failed", properties, measurements);
    }

TrackException 是使用的 tooreport 例外狀況，因為它會傳送 hello 堆疊的複本。 TrackEvent 是使用的 tooreport 其他事件。 您可以在診斷中附加可能有幫助的任何屬性。

例外狀況和事件顯示在 hello[診斷搜尋](app-insights-diagnostic-search.md)刀鋒視窗。 您可以鑽研到 toosee hello 其他屬性，堆疊追蹤。

![在診斷搜尋中，使用篩選器 tooshow 特定資料類型](./media/app-insights-detect-triage-diagnose/appinsights-333facets.png)


## <a name="monitor-proactively"></a>主動監視
Marcela 不會無所事事等候警示。 隨後每個重新部署，她接受看[回應時間](app-insights-web-monitor-performance.md)-兩者 hello 整體圖與 hello 資料表最慢的要求，以及例外狀況計數。  

![回應時間圖及伺服器回應時間格線。](./media/app-insights-detect-triage-diagnose/09-dependencies.png)

她可以評估 hello 效能影響每個部署，通常比較每週 hello 與上一次。 如果突然 worsening 時，她會引發，與 hello 相關開發人員。

## <a name="triage-issues"></a>分級問題
分級-評估 hello 嚴重性和問題的範圍-之後偵測的 hello 第一個步驟。 應該我們呼叫 hello 小組在午夜嗎？ 或者可以保留直到 hello 下一個方便的間距 hello 待辦項目嗎？ 分級時有一些重要的問題。

頻率它發生問題？hello 圖表 hello 概觀刀鋒視窗上的提供某些檢視方塊 tooa 問題。 例如，hello Fabrikam 應用程式會產生四個 web 測試警示一個晚上。 查看 hello 圖表中 hello 早上，hello 小組無法查看已確實某些紅點，但仍 hello 測試大多綠色。 鑽研 hello 可用性圖表，了解所有這些間歇性問題都已從一項測試的位置。 這顯然是僅影響一個路徑的網路問題，而且很可能可自行解決。  

相反地，例外狀況計數或回應時間的 hello 圖形大幅且穩定升高很顯然 toopanic 有關。

實用的分級策略是「自己動手做」。 如果您遇到 hello 相同的問題，您會知道它真實。

有多少比例的使用者受到影響？tooobtain 粗略的回應，會將 hello 失敗率除以 hello 工作階段計數。

![失敗的要求和工作階段的圖表](./media/app-insights-detect-triage-diagnose/10-failureRate.png)

回應變慢時，比較最慢回應要求的 hello 資料表 hello 使用量頻率為每個頁面。

重要性是封鎖的 hello 案例？ 如果這是功能性問題，封鎖了特定的使用者劇本，有很大影響嗎？ 如果客戶無法支付帳單，便很嚴重；如果客戶無法變更其畫面色彩喜好設定，也可以稍候再解決。 hello hello 事件或例外狀況的詳細資料或 hello 識別的 hello 慢速網頁，告訴您發生客戶問題。

## <a name="diagnose-issues"></a>診斷問題
診斷不相當 hello 相同偵錯。 開始透過 hello 程式碼的追蹤之前，您應該為何，大概知道發生 hello 問題的位置和時間。

**何時它發生？** hello hello 事件和度量的圖表所提供的歷程記錄檢視可讓您輕鬆 toocorrelate 效果與可能的原因。 如果回應時間或例外狀況率間歇尖峰，查看 hello 要求計數： 如果它在 hello 尖峰相同時，則它看起來像是資源問題。 更多的 CPU 或記憶體需要 tooassign 嗎？ 或者都不能管理 hello 載入的相依性？

**問題在於我們嗎？**  如果您在突然-例如當 hello 客戶想要的帳戶陳述式-要求的特定類型的效能可能就可能是外部的子系統，而不是 web 應用程式。 計量瀏覽器中選取 hello 相依性失敗率和相依性持續時間率和比較其記錄 hello 過去幾個小時或天 hello 您偵測到的問題。 如果有會相互關聯的變更，外部的子系統可能是 tooblame。  

![相依性失敗和呼叫 toodependencies 持續時間的圖表](./media/app-insights-detect-triage-diagnose/11-dependencies.png)

有些緩慢相依性的問題是地理位置問題。 Fabrikam 銀行使用 Azure virtual 機器，並發現他們誤將 Web 伺服器和帳戶伺服器放置在不同國家/地區。 透過移轉其中一部伺服器獲得明顯的改善。

**我們做了什麼？** 如果 hello 問題不會出現 toobe 中相依性，而且不一定有，可能是最近的變更所造成。 hello hello 計量和事件的圖表所提供的歷程記錄檢視方塊可讓您輕鬆 toocorrelate 任何突變進行部署。 會縮減 hello 搜尋 hello 問題。

**發生什麼？** 某些問題很少發生，而且可以是向下的困難 tootrack 藉由離線測試。 即時發生時，我們可以只是 tootry toocapture hello bug。 您可以檢查例外狀況報表中的 hello 堆疊傾印。 此外，您可以使用喜好的記錄架構或使用 TrackTrace() 或 TrackEvent() 來編寫追蹤呼叫。  

Fabrikam 的帳戶間轉送發生間歇性問題，但只有某些帳戶類型有此情況。 toounderstand 更好的事，它們在 hello 程式碼中，附加 hello 帳戶類型，做為屬性 tooeach 呼叫關鍵點插入 tracktrace （） 呼叫。 它只追蹤出輕鬆 toofilter 中進行診斷的搜尋。 它們也會附加為屬性和量值 toohello 追蹤呼叫的參數值。

## <a name="respond-toodiscovered-issues"></a>回應 toodiscovered 問題
一旦您已診斷 hello 的問題，您可以進行計劃 toofix 它。 或許您需要的 tooroll 回到最近的變更，或您或許可以繼續，修正此問題。 一旦完成 hello 修正程式，Application Insights 會告訴您是否成功。  

銀行 Fabrikam 的開發小組採用更結構化方法 tooperformance 以往 toobefore 它們使用 Application Insights。

* Hello Application Insights 概觀 頁面中設定這些欄位依據特定量值的效能目標。
* 他們設計到 hello 從 hello 開始，例如 hello 度量會測量 '漏斗圖。' 的使用者進行的應用程式的效能量值  


## <a name="monitor-user-activity"></a>監視使用者活動
當回應時間是一致的良好且有少數的例外狀況時，hello 開發小組就可以將 toousability 上。 它們可以思考如何 tooimprove hello 的使用者經驗，以及如何 tooencourage 更多使用者 tooachieve hello 預期的目標。

Application Insights 也可以使用的 toolearn 哪些使用者操作應用程式。 一旦順利執行，hello 小組希望的 tooknow 的 hello 最受歡迎的功能什麼使用者喜歡還是有困難，和頻率他們回來。 這些資訊有助於將他們近期的工作排定優先順序。 他們可以將每個功能 toomeasure hello 成功計劃 hello 開發週期的一部分。 

比方說，透過 hello 網站的一般使用者旅程已清除 」 漏斗圖。 」 許多客戶看看不同類型的貸款 hello 率。 較小的數字，請移 toofill hello 引號的形式。 人取得引號，一些請繼續並取出 hello 貸款。

![頁面檢視計數](./media/app-insights-detect-triage-diagnose/12-funnel.png)

考慮 hello 的客戶的最大數目的放置，hello 商務能找出如何 tooget 多個使用者都可以透過 toohello 底部 hello 漏斗。 在某些情況下，可能是使用者經驗 (UX) 失敗-例如，hello '下一步 按鈕會永久 toofind，或 hello 指示不明顯。 更有可能的原因有卸除出更重要的商業原因： 可能 hello 貸款的比率會太高。

任何 hello 的理由，hello 資料可協助 hello 小組解決使用者所執行的動作。 多個追蹤呼叫可以插入 toowork 出更多詳細資料。 Trackevent （） 中的 hello 細微的詳細資料的任何使用者動作時可以是使用的 toocount 按一下個別的按鈕，例如支付貸款 toosignificant 成就。

hello 小組即將使用的 toohaving 使用者活動的資訊。 只是現在，每當設計出一個新功能時，就要思考如何取得其使用方式的意見反應。 這些設計追蹤呼叫 hello 功能從 hello 開始。 使用每個開發週期中的 hello 意見反應 tooimprove hello 功能。

[深入了解如何追蹤使用量](app-insights-usage-overview.md)。

## <a name="apply-hello-devops-cycle"></a>套用 hello DevOps 循環
這就是如何團隊使用 Application Insights toofix 不只是每個問題，但 tooimprove 其開發生命週期。 希望這已提供您一些概念，讓您了解 Application Insights 如何協助您在自己的應用程式中進行應用程式效能管理。

## <a name="video"></a>影片

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>後續步驟
您可以開始在數種方式，根據您的應用程式的 hello 特性。 請挑選最適合您的方式：

* [ASP.NET Web 應用程式](app-insights-asp-net.md)
* [Java Web 應用程式](app-insights-java-get-started.md)
* [Node.js Web 應用程式](app-insights-nodejs.md)
* 裝載於 [IIS](app-insights-monitor-web-app-availability.md)、[J2EE](app-insights-java-live.md) 或 [Azure](app-insights-azure.md) 上的已部署應用程式。
* [Web 網頁](app-insights-javascript.md)-單一頁面應用程式或一般的網頁-以此本身或加入 tooany hello 伺服器選項。
* [可用性測試](app-insights-monitor-web-app-availability.md)tootest 應用程式從 hello 公用網際網路。
