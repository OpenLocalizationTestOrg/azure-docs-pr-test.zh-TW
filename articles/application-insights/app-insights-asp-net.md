---
title: "設定適用於使用 Azure Application Insights 的 ASP.NET web 應用程式分析 aaaSet |Microsoft 文件"
description: "針對裝載在內部部署環境或 Azure 的 ASP.NET 網站設定效能、可用性及使用情況分析。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d0eee3c0-b328-448f-8123-f478052751db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 61a3cdce68da48bfb9450b1d296acc1535f50a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a>設定 ASP.NET 網站的 Application Insights

此程序會設定您 ASP.NET web 應用程式 toosend 遙測 toohello [Azure Application Insights](app-insights-overview.md)服務。 這也適用於裝載在 IIS 伺服器或 hello 雲端中的 ASP.NET 應用程式。 取得圖表並功能強大的查詢語言來協助您了解 hello 應用程式效能和人員使用的方式，再加上自動警示失敗或效能問題。 許多開發人員會覺得這些功能很好，但您也可以擴充和自訂 hello 遙測，如果您需要。

在 Visual Studio 中只需按幾下滑鼠即可進行安裝。 您擁有 hello 選項 tooavoid 費用限制 hello 的遙測資料的磁碟區。 這可讓您 tooexperiment 和偵錯或 toomonitor 不許多使用者的站台。 當您決定您想繼續 toogo 和監視您的生產網站時，限制它是簡單 tooraise hello 更新版本。

## <a name="before-you-start"></a>開始之前
您需要：

* Visual Studio 2013 Update 3 或更新版本。 越新版越好。
* 訂用帳戶太[Microsoft Azure](http://azure.com)。 如果您的小組或組織有 Azure 訂用帳戶，hello 擁有者可以將您加入 tooit，使用您[Microsoft 帳戶](http://live.com)。

如果您想要，有替代主題 toolook 在：

* [在執行階段檢測 Web 應用程式](app-insights-monitor-performance-live-website-now.md)
* [Azure 雲端服務](app-insights-cloudservices.md)

## <a name="ide"></a>步驟 1： 加入 hello Application Insights SDK

在 [方案總管] 中以滑鼠右鍵按一下 Web 應用程式，然後選擇 [新增] > [Application Insights 遙測] 或 [設定 Application Insights]。

![[方案總管] 的螢幕擷取畫面，其中已醒目提示 [新增 Application Insights 遙測]](./media/app-insights-asp-net/appinsights-03-addExisting.png)

（在 Visual Studio 2015，另外還有 hello 新增專案 對話方塊中的選項 tooadd Application Insights。）

繼續 toohello Application Insights 組態 頁面上：

![[向 Application Insights 註冊您的應用程式] 頁面的螢幕擷取畫面](./media/app-insights-asp-net/visual-studio-register-dialog.png)

**a.** 選取 hello 帳戶和您使用 tooaccess Azure 訂用帳戶。

**b.** 選取您要 toosee hello 資料從您的應用程式的 Azure 中的 hello 資源。 通常︰

* [將單一資源使用於單一應用程式的不同元件](app-insights-monitor-multi-role-apps.md)。 
* 為不相關的應用程式建立個別的資源。
 
如果您想 tooset hello 資源群組或 hello 位置儲存您的資料，請按一下**設定**。 資源群組是使用的 toocontrol 存取 toodata。 相同，例如 hello 如果您有數個應用程式部分系統，您可能會其 Application Insights 資料放入 hello 相同的資源群組。

**c.** 在 hello 可用的資料磁碟區的限制，tooavoid 費用設定的端點。 Application Insights 是釋放 tooa 特定大量的遙測資料。 建立 hello 資源之後，您可以變更您選取 hello 入口網站中的開啟**功能 + 定價** > **資料磁碟區管理** > **每日磁碟區的 cap**。

**d.** 按一下**註冊**toogo 繼續並設定 Application Insights web 應用程式。 遙測傳送 toohello [Azure 入口網站](https://portal.azure.com)，偵錯期間和之後您已經發行您的應用程式。

**e.** 如果偵錯時，您不想 toosend 遙測 toohello 入口網站，只新增 hello Application Insights SDK tooyour 應用程式，但不在 hello 入口網站中設定資源。 在偵錯時，您就可以在 Visual Studio 中的能夠 toosee 遙測。 更新版本中，您可以傳回 toothis 組態 頁面上，或您無法等到部署您的應用程式之後和[在執行階段遙測切換](app-insights-monitor-performance-live-website-now.md)。


## <a name="run"></a> 步驟 2︰執行您的應用程式
按 F5 執行您的應用程式。 開啟不同頁面 toogenerate 某些遙測。

在 Visual Studio 中，您會看到 hello 事件已記錄的計數。

![Visual Studio 的螢幕擷取畫面。 hello Application Insights 按鈕會顯示在偵錯期間。](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a>步驟 3：查看遙測
您可以看到您在 Visual Studio 或 hello Application Insights 入口網站中的遙測。 搜尋遙測 toohelp Visual Studio 中偵錯應用程式。 監視效能和 hello web 入口網站時您的系統是即時的使用量。 

### <a name="see-your-telemetry-in-visual-studio"></a>在 Visual Studio 中查看遙測

在 Visual Studio 中，開啟 hello Application Insights 視窗。 按一下 hello **Application Insights**按鈕，或以滑鼠右鍵按一下您的專案，在 方案總管 中，選取**Application Insights**，然後按一下**搜尋即時遙測**.

在 hello Visual Studio Application Insights 搜尋視窗中，請參閱 hello**偵錯工作階段從資料**遙測 hello 伺服器端應用程式中產生的檢視。 試驗一下 hello 篩選，按一下任何事件 toosee 更多詳細資料。

![螢幕擷取畫面的 hello hello Application Insights 視窗中檢視偵錯工作階段的資料。](./media/app-insights-asp-net/55.png)

> [!NOTE]
> 如果您沒有看到任何資料，請確定 hello 的時間範圍內正確，然後按一下 hello 搜尋圖示。

[深入了解 Visual Studio 中的 Application Insights 工具](app-insights-visual-studio.md)。

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a>請參閱 web 入口網站中的遙測

（除非您選擇 tooinstall 只有 hello SDK），您也可以查看 hello Application Insights 入口網站中的遙測。 hello 入口網站有多個圖表、 分析工具和跨元件檢視比 Visual Studio。 hello 入口網站也提供警示。

開啟 Application Insights 資源。 請登入 toohello [Azure 入口網站](https://portal.azure.com/)和尋找它，或以滑鼠右鍵按一下 hello 專案在 Visual Studio 中，並讓它帶您前往該處。

![螢幕擷取畫面的 Visual Studio 中，顯示如何 tooopen hello Application Insights 入口網站](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> 如果您收到存取錯誤： 有多個 Microsoft 認證集，而且您登入一組錯誤 hello？ 在 hello 入口網站登出並再次登入。

hello 入口網站開啟檢視的 hello 遙測資料從您的應用程式上。

![Application Insights 概觀頁面的螢幕擷取畫面](./media/app-insights-asp-net/66.png)

在 hello 入口網站中，按一下任何磚或圖表 toosee 更多詳細資料。

[深入了解在 hello Azure 入口網站中使用 Application Insights](app-insights-dashboards.md)。

## <a name="step-4-publish-your-app"></a>步驟 4：發佈您的應用程式
發行您的應用程式 tooyour IIS 伺服器或 tooAzure。 監看式[即時度量資料流](app-insights-metrics-explorer.md#live-metrics-stream)toomake 確定可以順利執行。

您遙測中的積存累積 hello Application Insights 入口網站，您可以用它來監視度量，搜尋您遙測，並設定[儀表板](app-insights-dashboards.md)。 您也可以使用 hello 強大[記錄分析查詢語言](https://docs.loganalytics.io/)tooanalyze 使用量和效能或 toofind 特定事件。

您也可以繼續 tooanalyze 您遙測中的[Visual Studio](app-insights-visual-studio.md)，例如診斷搜尋的工具和[趨勢](app-insights-visual-studio-trends.md)。

> [!NOTE]
> 如果您的應用程式傳送足夠的遙測 tooapproach hello[節流限制](app-insights-pricing.md#limits-summary)自動[取樣](app-insights-sampling.md)上切換。 取樣可減少您應用程式傳送的同時保留供診斷之用的資料產生相互關聯的遙測 hello 數量。
>
>

## <a name="land"></a> 您全都準備好了

恭喜！ 您已安裝應用程式中的 hello Application Insights 套件，並在 Azure 上設定 toosend 遙測 toohello Application Insights 服務。

![遙測移動的圖表](./media/app-insights-asp-net/01-scheme.png)

hello 收到您的應用程式遙測的 Azure 資源由*檢測金鑰*。 您可以在 hello ApplicationInsights.config 檔案中找到此機碼。


## <a name="upgrade-toofuture-sdk-versions"></a>升級 toofuture SDK 版本
tooupgrade tooa[新版 hello SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases)，開啟 hello **NuGet 套件管理員**同樣地，和已安裝的封裝上的篩選。 選取 **Microsoft.ApplicationInsights.Web**，然後選擇 [升級]。

如果您進行任何自訂 tooApplicationInsights.config，儲存的副本，然後再升級。 然後，您的變更合併 hello 新版本。

## <a name="video"></a>影片

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>後續步驟

### <a name="more-telemetry"></a>更多遙測

* **[瀏覽器和頁面載入資料](app-insights-javascript.md)** - 在您的網頁中插入程式碼片段。
* **[取得更詳細的相依性和例外狀況監視](app-insights-monitor-performance-live-website-now.md)** - 在您的伺服器上安裝狀態監視器。
* **[程式碼的自訂事件](app-insights-api-custom-events-metrics.md)** toocount、 時間、 或量值使用者動作。
* **[取得記錄資料](app-insights-asp-net-trace-logs.md)** - 將記錄資料與您的遙測相互關聯。

### <a name="analysis"></a>分析

* **[在 Visual Studio 中使用 Application Insights](app-insights-visual-studio.md)**<br/>包含有關使用遙測，偵錯資訊診斷搜尋] 和 [toocode 鑽研。
* **[使用 hello Application Insights 入口網站](app-insights-dashboards.md)**<br/> 包括儀表板、功能強大的診斷和分析工具、警示、即時的應用程式相依性對應，以及遙測匯出的相關資訊。
* **[分析](app-insights-analytics-tour.md)** -hello 功能強大的查詢語言。

### <a name="alerts"></a>Alerts

* [可用性測試](app-insights-monitor-web-app-availability.md)： 建立測試 toomake 確定您的網站會顯示 hello 網站上。
* [智慧型診斷](app-insights-proactive-diagnostics.md)： 這些測試自動執行，因此您不需要 toodo 任何項目 tooset 註冊它們。 它們會讓您知道應用程式是否有不尋常的失敗要求率。
* [度量的警示](app-insights-alerts.md)： 設定這些 toowarn 您如果度量超出閾值。 您可以在撰寫於程式碼中的自訂度量上設定它們。

### <a name="automation"></a>自動化

* [自動建立 Application Insights 資源](app-insights-powershell.md)
