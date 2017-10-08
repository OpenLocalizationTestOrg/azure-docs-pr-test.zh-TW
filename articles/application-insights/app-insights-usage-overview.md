---
title: "使用 Azure Application Insights web 應用程式的 aaaUsage 分析 |Microsoft 文件"
description: "了解您的使用者，以及他們如何運用您的 web 應用程式。"
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: f7f9173cf411fa0d2dfb3b5ba99134a02bbc0e89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a>使用 Application Insights 進行 Web 應用程式的使用量分析

您 Web 應用程式的哪些功能最受歡迎？ 您的使用者是否利用您的應用程式達到其目標呢？ 他們會在特定點退出，並在稍後返回嗎？  [Azure Application Insights](app-insights-overview.md) 可協助您深入了解使用者如何使用 Web 應用程式。 每次您更新應用程式時，都可以評估它適用於使用者的程度。 您可以透過了解這些來制定下一個開發週期的相關資料導向決策。

## <a name="send-telemetry-from-your-app"></a>傳送來自您應用程式的遙測

藉由在應用程式伺服器程式碼，和您的網頁中安裝 Application Insights 取得 hello 最佳體驗。 hello 用戶端和伺服器元件，您的應用程式傳送遙測後 toohello Azure 入口網站進行分析。

1. **伺服端程式碼：**安裝 hello 適當模組您[ASP.NET](app-insights-asp-net.md)， [Azure](app-insights-azure.md)， [Java](app-insights-java-get-started.md)， [Node.js](app-insights-nodejs.md)，或[其他](app-insights-platforms.md)應用程式。

    * *不想 tooinstall 伺服端程式碼嗎？請直接[建立 Azure Application Insights 資源](app-insights-create-new-resource.md)。*

2. **網頁程式碼：**開啟 hello [Azure 入口網站](https://portal.azure.com)，開啟您的應用程式的 hello Application Insights 資源，並開啟**入門 > 監視和診斷用戶端**。 

    ![Hello 指令碼複製到的主版網頁的 hello 開頭。](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. **取得遙測：**幾分鐘，偵錯模式執行您的專案，然後尋找 Application Insights 中的 hello 概觀刀鋒視窗中的結果。

    發行應用程式 toomonitor 應用程式效能，並找出您的使用者與您的應用程式的行為。

## <a name="include-user-and-session-id-in-your-telemetry"></a>將使用者與工作階段識別碼加入您的遙測
tootrack 使用者一段時間，Application Insights 需要方式 tooidentify 它們。 hello 事件工具是 hello 唯一的 [使用量] 工具，不需要使用者識別碼或工作階段識別碼。

在[此處](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context)開始傳送這些識別碼。

## <a name="explore-usage-demographics-and-statistics"></a>探索使用量人口統計和統計資料
了解人們在使用您的應用程式時，他們最感興趣的網頁、使用者的所在位置，以及他們使用何種瀏覽器與作業系統。 

hello 使用者和工作階段報表篩選網頁或自訂的事件資料，而且這些區段的屬性，例如位置、 環境及頁面。 您也可以新增自己的篩選條件。

![使用者](./media/app-insights-usage-overview/users.png)  

Hello 右邊的洞察能力點出 hello 資料集的有趣模式。  

* hello**使用者**報告會算進 hello 存取您的網頁，您所選擇的時間週期內的唯一使用者數目。 (會使用 Cookie 來計算使用者。 如果有人使用不同的瀏覽器或用戶端電腦來存取您的網站，或清除其 Cookie，系統就會將他們計算為多次。)
* hello**工作階段**報告會算進 hello 存取您的網站的使用者工作階段數目。 工作階段是使用者活動的一段時間，在閒置時間超過半小時後就會加以終止。

[進一步了解 hello 使用者、 工作階段和事件工具](app-insights-usage-segmentation.md)  

## <a name="page-views"></a>頁面檢視

在 hello 使用量刀鋒視窗中，按一下 透過 hello 頁面檢視磚 tooget 最受歡迎頁面的分析：

![從 hello 概觀刀鋒視窗中，按一下 hello 頁面檢視圖表](./media/app-insights-usage-overview/05-games.png)

hello 上述範例中取自遊戲的網站。 從 hello 圖表，我們可以立即看到：

* 過去一週時，未在 hello 改進使用方式。 也許我們應該考慮搜尋引擎最佳化？
* 鱣是 hello 最受歡迎的遊戲頁面。 讓我們重點討論進一步改進 toothis 頁面。
* 平均而言，使用者瀏覽 hello 鱣頁面三倍每週。 (與使用者相比，工作階段數大約多出三倍)。
* Hello 美國工作週、 期間以及在工作時間，大部分的使用者瀏覽 hello 站台。 可能是我們應該 hello 網頁上提供的 [快速隱藏] 按鈕。
* hello[註解](app-insights-annotations.md)hello 圖表上顯示 當已部署的 hello 網站的新版本。 無 hello 新的部署有明顯的影響，在使用方式。

如果您想 tooinvestigate hello 流量 tooyour 站台的詳細資料，例如分割您的站台傳送它的網頁檢視遙測中的自訂屬性的嗎？

1. 開啟 hello**事件**hello Application Insights 資源功能表中的工具。 此工具可讓您根據各種的篩選、同群使用者及區隔等選項，將應用程式所傳送出的頁面檢視和自訂事件數目進行分析。
2. 在 hello 「 誰使用 」 的下拉式清單中，選取"Any 頁面檢視 」。
3. 在 hello 「 分割 」 的下拉式清單中選取哪個 toosplit 網頁檢視遙測的屬性。

## <a name="retention---how-many-users-come-back"></a>保留期 - 回來使用的使用者人數？

保留可協助您了解頻率您的使用者會傳回 toouse 應用程式中，根據 cohorts 的執行期間特定時間貯體某些商務動作的使用者。 

- 了解哪些特定的功能會導致使用者 toocome 後比其他更多 
- 根據實際使用者資料的表單假設 
- 判斷保留期是否為您產品的問題 

![保留](./media/app-insights-usage-overview/retention.png) 

在最上層的 hello 保留控制項可讓您 toodefine 特定事件和時間範圍 toocalculate 保留。 hello 圖 hello 中間讓 hello 的視覺表示法所指定的時間範圍 hello 整體保留百分比。 hello 下方 hello 圖形代表個別的保留在指定的時段內。 此詳細層級可讓您 toounderstand 哪些使用者執行的工作和功能可能會影響傳回的使用者，更詳細的資料粒度。  

[Hello 保留工具有關的詳細資訊](app-insights-usage-retention.md)

## <a name="custom-business-events"></a>自訂商務事件

tooget 哪些使用者清楚了解如何處理您的 web 應用程式，就很有用的 tooinsert toolog 自訂事件時，程式碼行。 這些事件可以從詳細的使用者動作，例如按一下特定的按鈕，toomore 重要的商務事件，例如在購買或獲勝追蹤任何項目。 

雖然在某些情況下，頁面檢視可以代表有用的事件，但一般而言它並不正確。 使用者可以開啟 [產品] 頁面上，而不購買 hello 產品。 

您可以使用特定商務事件，透過網站將使用者的進度製作成圖表。 您可以找出他們對不同選項的偏好，以及它們退出或遇到困難之處。 使用這項知識，您可以做出有關明智 hello 優先順序開發待辦項目中。

可以在 hello web 網頁中記錄事件：

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

或 hello 伺服器端的 hello web 應用程式：

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

讓您可以篩選或分割 hello 事件，當您檢查這些 hello 入口網站中，您可以附加屬性值 toothese 事件。 此外，一組標準的屬性是使用者的附加的 tooeach 事件，例如匿名使用者識別碼，可讓您 tootrace hello 一連串個別的活動。

深入了解[自訂事件](app-insights-api-custom-events-metrics.md#trackevent)和[屬性](app-insights-api-custom-events-metrics.md#properties)。

### <a name="slice-and-dice-events"></a>將事件進行交叉分析

Hello 使用者、 工作階段和事件工具 中，您可以配量，並分析依使用者、 事件名稱和屬性的自訂事件。
![使用者](./media/app-insights-usage-overview/users.png)  
  
## <a name="design-hello-telemetry-with-hello-app"></a>設計 hello 與 hello 應用程式的遙測

當您在設計您的應用程式的每項功能時，請考慮要如何 toomeasure 成功與您的使用者。 決定您需要 toorecord，和程式碼到您的應用程式追蹤的事件會呼叫從 hello hello 的商務事件的開始。

## <a name="a--b-testing"></a>A | B 測試
如果您不知道哪些 variant 某項功能將會更成功，請將它釋放這兩種，讓每個可存取 toodifferent 使用者。 測量各自的 hello 成功，然後將 tooa 統一的版本。

這項技巧，您附加相異的屬性值 tooall hello 遙測傳送的每個版本的應用程式。 您可以執行，藉由定義屬性在 hello active TelemetryContext。 這些預設屬性會加入 tooevery hello 應用程式的遙測訊息傳送的不只是您自訂的訊息，但也 hello 標準遙測。

在 hello Application Insights 入口網站篩選，並在 hello 屬性值，將資料分割，以 toocompare hello 不同版本。

toodo，[設定遙測的初始設定式](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

Hello web 應用程式初始設定式中 Global.asax.cs 例如：

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

所有新 TelemetryClients 自動加入您所指定的 hello 屬性值。 個別的遙測事件可以覆寫 hello 預設值。

## <a name="next-steps"></a>後續步驟
   - [使用者、工作階段、事件](app-insights-usage-segmentation.md)
   - [漏斗圖](usage-funnels.md)
   - [保留](app-insights-usage-retention.md)
   - [使用者流程](app-insights-usage-flows.md)
   - [活頁簿](app-insights-usage-workbooks.md)
   - [新增使用者內容](app-insights-usage-send-user-context.md)
