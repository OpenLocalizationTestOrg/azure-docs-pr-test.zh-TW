---
title: "aaaAzure Insights 的應用程式的 Windows server 和背景工作角色 |Microsoft 文件"
description: "手動新增 hello Application Insights SDK tooyour ASP.NET 應用程式 tooanalyze 使用狀況、 可用性和效能。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 64643ef637195d10f87fc6020a77169bca66c1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a>為 .NET 應用程式手動設定 Application Insights

您可以設定[Application Insights](app-insights-overview.md) toomonitor 各種不同的應用程式或應用程式角色、 元件或 microservices。 對於 Web 應用程式和服務，Visual Studio 會提供[單步驟設定](app-insights-asp-net.md)。 對於其他類型的 .NET 應用程式 (例如後端伺服器角色或桌面應用程式)，您可以手動設定 Application Insights。

![範例效能監視圖表](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a>開始之前

您需要：

* 訂用帳戶太[Microsoft Azure](http://azure.com)。 如果您的小組或組織有 Azure 訂用帳戶，hello 擁有者可以將您加入 tooit，使用您[Microsoft 帳戶](http://live.com)。
* Visual Studio 2013 或更新版本。

## <a name="add"></a>1.選擇 Application Insights 資源

hello 'resource' 是收集及顯示 hello Azure 入口網站中資料的位置。 您是否需要 toodecide toocreate 一個新或現有的共用。

### <a name="part-of-a-larger-app-use-existing-resource"></a>屬於大型應用程式︰使用現有資源

如果您的 web 應用程式具有數個元件-例如前端的 web 應用程式和一個或多個後端服務層，則您應該從所有 hello 元件 toohello 傳送遙測相同的資源。 這會讓它們顯示在單一的應用程式對應，toobe，並將其可能 tootrace 來自一個元件 tooanother 的要求。

因此，如果您已經監視此應用程式的其他元件，然後只使用 hello 相同資源。

在 hello 開啟 hello 資源[Azure 入口網站](https://portal.azure.com/)。 

### <a name="self-contained-app-create-a-new-resource"></a>獨立應用程式：建立新的資源

如果 hello 新應用程式是不相關的 tooother 應用程式，它應該有它自己的資源。

登入 toohello [Azure 入口網站](https://portal.azure.com/)，並建立新的 Application Insights 資源。 選擇 ASP.NET 做為 hello 應用程式類型。

![按一下 新增，然後按一下Application Insights](./media/app-insights-windows-services/01-new-asp.png)

應用程式類型的 hello 選擇設定 hello 的 hello 資源刀鋒視窗的預設內容。

## <a name="2-copy-hello-instrumentation-key"></a>2.複製檢測機碼 hello
hello 索引鍵識別 hello 資源。 您會將它安裝很快就在 hello SDK，順序 toodirect 資料 toohello 資源中。

![按一下 內容選取 hello 金鑰，請按 ctrl + C](./media/app-insights-windows-services/02-props-asp.png)

## <a name="sdk"></a>3.安裝應用程式中的 hello Application Insights 套件
安裝和設定 hello Application Insights 封裝會根據您正在使用的 hello 平台而有所不同。 

1. 在 Visual Studio 中，以滑鼠右鍵按一下專案，然後選擇 [管理 Nuget 套件]。
   
    ![Hello 專案上按一下滑鼠右鍵，然後選取 管理 Nuget 封裝](./media/app-insights-windows-services/03-nuget.png)
2. 安裝 Windows server 應用程式，「 Microsoft.ApplicationInsights.WindowsServer。"hello Application Insights 套件
   
    ![搜尋「Application Insights」](./media/app-insights-windows-services/04-ai-nuget.png)
   
    *哪個版本？*

    請檢查**包含發行前版本**如果您想 tootry 我們最新的功能。 hello 相關文件或部落格，請注意是否需要發行前版本。
    
    *可以使用其他封裝嗎？*
   
    是。 如果您只想 toouse hello API toosend 您自己的遙測，請選擇 「 Microsoft.ApplicationInsights"。 hello Windows 伺服器套件包含 hello API 以及許多其他封裝，例如效能計數器集合與相依性監視。 

### <a name="tooupgrade-toofuture-package-versions"></a>tooupgrade toofuture 封裝版本
我們發行從時間 tootime hello SDK 的新版本。

tooupgrade tooa[新版 hello 封裝](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/)，再次開啟 NuGet 封裝管理員，然後篩選已安裝的封裝。 選取 **Microsoft.ApplicationInsights.WindowsServer**，然後選擇 [升級]。

如果您進行任何自訂 tooApplicationInsights.config，儲存一份之前升級，之後您的變更合併至 hello 新版本。

## <a name="4-send-telemetry"></a>4.傳送遙測
**如果您已安裝只 hello API 套件：**

* 在中，例如設定在程式碼中的 hello 檢測金鑰`main()`: 
  
    `TelemetryConfiguration.Active.InstrumentationKey = "`您的金鑰 `";` 
* [撰寫您自己使用 hello API 的遙測](app-insights-api-custom-events-metrics.md#ikey)。

**如果您已安裝其他的 Application Insights 套件，**您可以如果您想要的話，使用 hello.config 檔案 tooset hello 檢測金鑰：

* 編輯 ApplicationInsights.config （這由 hello NuGet 安裝所加入）。 這只前面插入結尾標記的 hello:
  
    `<InstrumentationKey>`*hello 檢測金鑰複製*`</InstrumentationKey>`
* 請確定在 方案總管 ApplicationInsights.config hello 屬性會設太**建置動作 = 複製 tooOutput 目錄的內容 = 複製**。

如果您想太是程式碼中的有用 tooset hello 檢測金鑰[不同組建組態的交換器 hello 金鑰](app-insights-separate-resources.md)。 如果您在程式碼中設定 hello 機碼，您不需要 tooset 在 hello`.config`檔案。

## <a name="run"></a> 執行專案
使用 hello **F5** toorun 您的應用程式，現在就試試看： 開啟不同的網頁 toogenerate 某些遙測。

在 Visual Studio 中，您會看到已傳送的 hello 事件計數。

![Visual Studio 中的事件計數](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <a name="monitor"></a> 檢視遙測
傳回 toohello [Azure 入口網站](https://portal.azure.com/)並瀏覽 tooyour Application Insights 資源。

尋找在 hello 概觀圖表中的資料。 剛開始的時候，您只會看見一或兩個資料點。 例如：

![瀏覽 toomore 資料](./media/app-insights-windows-services/12-first-perf.png)

按一下 透過任何圖表 toosee 度量詳細資訊。 [深入了解度量。](app-insights-web-monitor-performance.md)

### <a name="no-data"></a>沒有資料？
* 使用 hello 應用程式，使其產生某些遙測開啟不同的頁面。
* 開啟 hello[搜尋](app-insights-diagnostic-search.md)磚，toosee 個別事件。 有時會事件稍長時 tooget hello 度量管線。
* 請稍等片刻，然後按一下 [重新整理 ]。 圖表定期重新整理本身，但您可以手動重新整理如果正在等待某些資料 tooshow。
* 請參閱 [疑難排解](app-insights-troubleshoot-faq.md)。

## <a name="publish-your-app"></a>發佈您的應用程式
現在，將您的應用程式 tooyour 伺服器部署或 tooAzure 和監看式 hello 資料會累積。

![使用 Visual Studio toopublish 您的應用程式](./media/app-insights-windows-services/15-publish.png)

當您在偵錯模式執行時，以便您應該會看到資料出現在數秒內加速遙測 hello 管線。 以發行組態部署應用程式時，資料累積會較為緩慢。

### <a name="no-data-after-you-publish-tooyour-server"></a>之後您發佈 tooyour 伺服器的任何資料嗎？
請在您的伺服器防火牆中，開啟連出流量的連接埠。 請參閱[本頁](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses)hello 清單的所需的位址 

### <a name="trouble-on-your-build-server"></a>組建伺服器發生問題？
請參閱 [此疑難排解項目](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild)。

> [!NOTE]
> 如果您的應用程式會產生大量的遙測，hello 調整取樣模組將會自動減少 hello 磁碟區所傳送的 toohello 入口網站傳送代表性數部分的事件。 不過，事件是相關的 toohello 相同的要求會被選取或取消選取此選項為群組，如此您可以瀏覽相關的事件之間。 
> [了解取樣](app-insights-sampling.md)。
> 
> 

## <a name="video"></a>影片

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>後續步驟
* [新增更多的遙測](app-insights-asp-net-more.md)tooget hello 完整 360 度檢視您的應用程式。

