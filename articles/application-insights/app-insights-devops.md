---
title: "aaaWeb 應用程式效能監視-Azure Application Insights |Microsoft 文件"
description: "Application Insights 如何融入 hello devOps 循環"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 479522a9-ff5c-471e-a405-b8fa221aedb3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: bba2d6c59de1794adcbf8e298d0ef4f0dbaa700f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deep-diagnostics-for-web-apps-and-services-with-application-insights"></a>使用 Application Insights 深入診斷 Web 應用程式
## <a name="why-do-i-need-application-insights"></a>我為什麼需要 Application Insights 呢？
Application Insights 會監視您正在執行的 Web 應用程式。 它會告訴您有關失敗和效能的問題，並協助您分析客戶如何使用您的應用程式。 它適用於許多平台 (ASP.NET、 J2EE，Node.js，...) 上執行的應用程式，而裝載在 hello 雲端或內部部署。 

![Hello 複雜度傳遞 web 應用程式的層面](./media/app-insights-devops/010.png)

在執行時，它是不可或缺的 toomonitor 現代應用程式。 最重要的是，您會想 toodetect 失敗之前執行大部分的客戶。 您也想 toodiscover，並修正效能問題，而不嚴重，可能是作業變慢或會導致某些不便 tooyour 使用者。 和 hello 系統執行 tooyour 滿意度，當您想要哪些 hello 使用者所運用的 tooknow： 它們使用 hello 最新功能？ 是否已成功使用它？

現代化 web 應用程式會以循環的持續傳遞開發： 發行的新功能或改進。觀察程度這也適用於 hello 使用者。規劃 hello 開發該知識為基礎的下一個遞增值。 這個循環的主要部分是 hello 觀察階段。 Application Insights 提供 hello 工具 toomonitor 效能和使用方式的 web 應用程式。

此程序的 hello 最重要層面是診斷和診斷。 如果 hello 應用程式失敗，會在遺失商務。 hello 主要角色的監視架構因此 toodetect 失敗會可靠地，通知您立即和 toopresent hello 資訊所需 toodiagnose hello 問題。 這就是 Application Insights 的確實功用。

### <a name="where-do-bugs-come-from"></a>Bug 來自何處？
Web 系統中的失敗通常是由組態問題或其許多元件之間的互動不良所引起。 hello 第一項工作時處理即時網站事件所以 hello 問題的 tooidentify hello locus： 哪些元件或關聯性是 hello 原因？

我們之中有些人 (灰白頭髮的那些人) 可能還記得那個電腦程式只在一部電腦中執行的單純年代。 hello 開發人員會進行完整的測試之前傳送。擁有出貨，很少會看到，或可再考慮這個。 hello 使用者會 tooput 最多有的 hello 剩餘 bug 多年。 

但現在的情況已變得非常不同。 應用程式，有不同的裝置 toorun 的可能很難 tooguarantee hello 完全相同的行為在每一個。 裝載 hello 雲端中的應用程式表示快速、 修正 bug，但這也表示連續競爭和 hello 期望的新功能頻繁的間隔。 

在這些情況下，hello hello bug 計數確實有控制項只方式 tookeep 自動化單元測試。 不可能 toomanually 重新測試上每一次傳遞的所有內容。 單元測試是 hello 的現在經常一部分建置流程。 Hello Xamarin Test Cloud 等工具協助提供自動化的 UI 測試多個瀏覽器版本上。 這些測試區域可讓我們 toohope 該 hello 應用程式內找到的 bug 就能夠維持速率 tooa 最小值。

典型的 Web 應用程式有許多即時元件。 在加法 toohello 用戶端 （瀏覽器或裝置的應用程式），而且 hello web 伺服器，則可能 toobe 大幅的後端處理。 或許 hello 後端是管線元件中或更加鬆散的共同作業的項目集合。 此外，它們其中有許多都不在您的控制內 - 它們是您所需的外部服務。

這類的組態，它可以是，會發生困難而且 uneconomical tootest 或預期，每個可能的失敗模式，除了在 hello 即時系統本身。 

### <a name="questions-"></a>問題 ...
當我們開發 Web 系統時，會自問數個問題：

* 我的應用程式會當機嗎？ 
* 實際發生什麼事？ -如果要求失敗，我要如何進入那里 tooknow。 我們需要追蹤事件 ...
* 我的應用程式速度夠快嗎？ 多久花費 toorespond tootypical 要求？
* 可以載入 hello 伺服器控制代碼 hello 嗎？ 當要求的 hello 速率上升時，未 hello 回應時間會保有穩定嗎？
* 回應速度是我的相依性-hello REST Api，資料庫和我的應用程式呼叫其他元件。 特別是，如果 hello 系統是慢速，是我的元件，還是我會收到回應變慢其他人？
* 我的應用程式是否正在運作？ 可以看到它從 hello 世界各地嗎？ 讓我知道它是否會停止...
* Hello 根本原因為何？ 已在我的元件或相依性的 hello 失敗？ 是通訊問題嗎？
* 有多少使用者受到影響？ 如果我有一個以上的問題 tootackle，這是最重要的 hello？

## <a name="what-is-application-insights"></a>什麼是 Application Insights？
![Application Insights 的基本工作流程](./media/app-insights-devops/020.png)

1. Application Insights 檢測您的應用程式，並傳送遙測資訊，請參閱 hello 應用程式執行時。 您可以建立 hello Application Insights SDK 至 hello 應用程式，或是您可以套用在執行階段檢測。 您可以加入您自己的遙測 toohello 一般模組 hello 前一個方法是更有彈性。
2. hello 遙測傳送 toohello Application Insights 入口網站，它會在其中儲存及處理。 (雖然 Application Insights 裝載於 Microsoft Azure 中，但是它可以監視任何 Web 應用程式，而不只是 Azure 應用程式)。
3. hello 遙測會顯示 tooyou hello 表單的圖表和資料表的事件中。

遙測有兩種主要類型︰彙總與原始執行個體。 

* 例如，執行個體資料包含您的 Web 應用程式所收到的要求報告。 您可以尋找並檢查 hello hello Application Insights 入口網站中使用 hello 搜尋工具之要求詳細資料。 hello 執行個體會包含資料，例如您的應用程式花費了 toorespond toohello 要求，時間長度，以及 hello 要求的 URL、 用戶端 hello 的約略位置和其他資料。
* 彙總的資料包含每單位時間的事件計數，因此您可以比較 hello hello 回應時間的要求率。 它也包含像是要求回應時間的計量資訊。

hello 資料主要類別如下：

* 要求 tooyour 應用程式 （通常是 HTTP 要求） 的 URL、 回應時間及成功或失敗的資料。
* 相依性 - 您的應用程式所進行的 REST 和 SQL 呼叫，也包含 URI、回應時間和成功
* 例外狀況，包括堆疊追蹤。
* 頁面檢視資料，來自 hello 使用者的瀏覽器。
* 計量資訊 (例如效能計數器)，以及您自行撰寫的計量。 
* 您可以使用 tootrack 商務事件的自訂事件
* 用來偵錯的記錄追蹤。

## <a name="case-study-real-madrid-fc"></a>案例研究：西班牙皇家馬德里隊
hello 的 web 服務[真實馬德里 Football 社團](http://www.realmadrid.com/)做大約 450 百萬風扇 hello 世界各地。 風扇透過網頁瀏覽器進行存取，這兩個，而 hello 社團的行動裝置應用程式。 球迷不只可預約門票，也能存取比賽結果、選手及即將舉行的比賽相關資訊和影片剪輯。 他們會使用像是得分進球數等篩選條件進行搜尋。 也有連結 toosocial 媒體。 hello 使用者經驗高度個人化，並設計做為雙向通訊 tooengage 風扇。

hello 方案[是服務和應用程式在 Microsoft Azure 上的系統](https://www.microsoft.com/en-us/enterprise/microsoftcloud/realmadrid.aspx)。 延展性是關鍵需求︰流量變化無常，而且可在比賽期間和接近比賽時達到非常高的量。

用於真實馬德里，很重要的 toomonitor hello 系統的效能。 Azure 的 Application Insights 提供全方位的視野 hello 系統，確保可靠且高的服務層級。 

hello 社團也會取得深入了解其風扇的： 它們的位置 （只有 3%是在西班牙），它們在播放程式、 歷程記錄的結果和即將發行的遊戲，以及他們如何回應 toomatch 結果中有哪些感興趣。

其中大多數遙測資料會自動收集與任何加入的程式碼，簡化 hello 方案，並降低操作的複雜性。  對於皇家馬德里而言，Application Insights 每個月可處理 38 億個遙測點。

實際馬德里使用 hello Power BI 模組 tooview 其遙測。

![Application Insights 遙測的 Power BI 檢視](./media/app-insights-devops/080.png)

## <a name="smart-detection"></a>智慧型偵測
[主動診斷](app-insights-proactive-diagnostics.md)是一項最新功能。 您不需提供任何特殊組態，Application Insights 就會自動偵測並警示您，關於您應用程式中異常提高的失敗率。 它是聰明 tooignore 背景為偶爾的失敗，而且也會上升只需按比例 tooa 升高要求。 例如，如果其中一種您而定，hello 服務失敗，或新的 hello 建置您剛剛所部署無法運作太好，則只要您查看您的電子郵件，您愈了解它。 (而且會提供 Webhook，讓您能夠觸發其他應用程式)。

這項功能的另一個層面會執行您的遙測，尋找的異常模式的效能，會永久 toodiscover 每日深入分析。 例如，它會找到與特定地理區域或特定瀏覽器版本相關聯的慢速效能。

在這兩種情況下，hello 警示不只會告知 hello 徵狀探索，但也可讓您的資料需要 toohelp 診斷 hello 問題，例如相關的例外狀況報告。

![來自主動診斷的電子郵件](./media/app-insights-devops/030.png)

客戶 Samtec 說：「在最近的功能快速轉換期間，我們發現低於調整規模的資料庫已到達它的資源限制並導致逾時。 主動式偵測警示來自所通告，我們已分級非常接近即時的 hello 問題為常值。 與 hello Azure 平台警示結合此警示可協助我們幾乎可立即修正 hello 問題。 總停機時間 < 10 分鐘。」

## <a name="live-metrics-stream"></a>即時計量串流
部署最新組建的 hello 可以想的體驗。 如果有任何問題，您想要 tooknow 資訊，請立即，如此如有必要，您可以將。 即時計量串流可為您提供大約 1 秒延遲的關鍵計量。

![即時計量](./media/app-insights-devops/040.png)

並可讓您立即檢查任何失敗或例外狀況的樣本。

![即時失敗事件](./media/app-insights-devops/live-stream-failures.png)

## <a name="application-map"></a>應用程式對應
應用程式對應會自動探索您的應用程式的拓撲，用來配置 hello toolet 輕鬆地在您的分散式環境中識別效能瓶頸和有問題的流程，其最上層的效能資訊。 它可讓您 toodiscover 應用程式相依性 Azure 服務上。 您可以了解如果是程式碼相關或相關的相依性分級 hello 問題，而且從單一位置下鑽研至相關的診斷經驗。 比方說，您的應用程式中的 SQL 層的 tooperformance 降低因失敗。 與應用程式對應可以立即看到它，並向下切入到 hello SQL 索引建議程式或查詢 Insights 經驗。

![應用程式對應](./media/app-insights-devops/050.png)

## <a name="application-insights-analytics"></a>Application Insights 分析
使用 [分析](app-insights-analytics.md)，您就能利用功能強大的 SQL 式語言撰寫任意查詢。  診斷跨 hello 整個應用程式堆疊會變得簡單連接各種不同觀點以及您可以詢問 hello 適當的問題 toocorrelate 服務效能的商務計量與客戶經驗。 

您可以查詢所有遙測的執行個體和度量的未經處理資料儲存在 hello 入口網站中。 hello 語言包括篩選、 聯結、 彙總和其他作業。 您可以計算欄位並執行統計分析。 目前提供表格式和圖形視覺效果。

![分析查詢和結果圖表](./media/app-insights-devops/025.png)

例如，很容易：

* 分割應用程式的要求效能資料，客戶層 toounderstand 經驗。
* 在即時網站調查期間，搜尋特定錯誤碼或自訂的事件名稱。
* 向下鑽研至特定客戶 toounderstand hello 應用程式使用功能，如何取得並採用。
* 追蹤工作階段與特定使用者 tooenable 支援和作業團隊 tooprovide 立即客戶支援服務的回應時間。
* 判斷常用的應用程式功能 tooanswer 功能優先順序的問題。

客戶 DNN 說: 「 Application Insights 提供以 hello 遺漏 hello 方程式所能 toocombine、 排序、 查詢和篩選資料所需的部分。 讓我們的團隊 toouse 自己精巧和體驗 toofind 使用功能強大的查詢語言的資料已允許我們 toofind insights 及解決的問題，我們還不知道我們必須。 許多有趣的答案來自 hello 問題開頭*' 我奇觀 if...'。*"

## <a name="development-tools-integration"></a>開發工具整合
### <a name="configuring-application-insights"></a>設定 Application Insights
Visual Studio 和 Eclipse 有工具 tooconfigure hello 正確 SDK 套件 hello 專案所開發。 沒有功能表命令 tooadd Application Insights。

若您使用的追蹤記錄架構，例如 Log4N、 NLog 或 System.Diagnostics.Trace toobe，然後您取得 hello 選項 toosend hello 記錄 tooApplication Insights hello 與其他遙測，以便輕鬆地將要求與 hello 追蹤相互關聯相依性呼叫和例外狀況。

### <a name="search-telemetry-in-visual-studio"></a>在 Visual Studio 中搜尋遙測
在開發和偵錯功能，您可以檢視和搜尋 hello 直接在 Visual Studio 中使用相同搜尋機關以 hello web 入口網站中的 hello 的遙測。

當 Application Insights 記錄例外狀況時，您還可以和在 Visual Studio 中檢視 hello 資料點跳直線 toohello 相關的程式碼。

![Visual Studio 搜尋](./media/app-insights-devops/060.png)

偵錯期間，您在 hello 選項 tookeep hello 遙測在開發電腦、 Visual Studio 中，但不將它傳送 toohello 入口網站加以檢視。 此本機選項可避免與生產環境的遙測偵錯混合在一起。

### <a name="build-annotations"></a>建置註解
如果您使用 Visual Studio Team Services toobuild 並部署您的應用程式時，部署註解顯示 hello 入口網站中的圖表上。 如果您的最新版本沒有 hello 標準的任何作用，它就很明顯。

![建置註解](./media/app-insights-devops/070.png)

### <a name="work-items"></a>工作項目
產生警示時，Application Insights 可以在您的工作追蹤系統中自動建立工作項目。

## <a name="but-what-about"></a>但是，您認為...？
* [隱私權和儲存體](app-insights-data-retention-privacy.md) - 您的遙測會保留於 Azure 安全伺服器上。
* 效能-hello 影響是非常低。 遙測會進行批次處理。
* [價格](app-insights-pricing.md) - 您可以開始免費使用，當您處於低用量期間可繼續使用。


## <a name="video"></a>影片

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>後續步驟
開始使用 Application Insights 很簡單。 hello 主要選項包括：

* 檢測已在執行的 Web 應用程式。 這可讓您所有的 hello 內建的效能遙測資料。 其適用於 [Java](app-insights-java-live.md) 和 [IIS 伺服器](app-insights-monitor-performance-live-website-now.md)，以及 [Azure Web 應用程式](app-insights-azure.md)。
* 在開發期間檢測您的專案。 您可以針對 [ASP.NET](app-insights-asp-net.md) 或 [Java](app-insights-java-get-started.md) 應用程式，以及 [Node.js](app-insights-nodejs.md) 和許多[其他類型](app-insights-platforms.md)執行此動作。 
* 藉由新增簡短的程式碼片段來檢測 [任何網頁](app-insights-javascript.md) 。

