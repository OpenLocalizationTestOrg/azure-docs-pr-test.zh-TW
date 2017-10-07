---
title: "Azure web 應用程式效能 aaaMonitor |Microsoft 文件"
description: "Azure Web 應用程式的應用程式效能監視。 圖表載入和回應時間、相依性資訊以及設定效能警示。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d1083254e5c504b18f2ac5ae2368610dc2790436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-web-app-performance"></a>監視 Azure Web 應用程式效能
在 hello [Azure 入口網站](https://portal.azure.com)您可以設定應用程式效能監視您[Azure web 應用程式](../app-service-web/app-service-web-overview.md)。 [Azure 的 Application Insights](app-insights-overview.md)檢測其活動 toohello Application Insights 服務，其中會儲存並分析您應用程式 toosend 遙測。 可以用度量圖表和搜尋工具 toohelp 診斷問題、 改善效能，以及評估使用。

## <a name="run-time-or-build-time"></a>執行階段或建置階段
您可以設定監視，可檢測 hello 應用程式在兩種方法之一：

* **執行階段** - 您可以在 Web 應用程式已經上線時，選取效能監視延伸模組。 它不是必要的 toorebuild 或重新安裝您的應用程式。 您會取得一組標準封裝，用以監視回應時間、成功率、例外狀況、相依性等。 
* **建置階段** - 您可以在開發應用程式中安裝封裝。 此選項比較靈活。 在加法 toohello 相同標準的封裝，您可以撰寫程式碼 toocustomize hello 遙測或 toosend 您自己的遙測。 您可以記錄的特定活動或根據您的應用程式網域 toohello 語意的記錄事件。 

## <a name="run-time-instrumentation-with-application-insights"></a>使用 Application Insights 執行時間檢測
如果您已在 Azure 中執行 Web 應用程式，您便已得到一些監視︰要求率和錯誤率。 加入 Application Insights tooget 更多，例如回應時間、 監視呼叫 toodependencies、 智慧型偵測和 hello 功能強大的記錄分析查詢語言。 

1. **選取 [Application Insights**控制台] 中 hello Azure web 應用程式。
   
    ![在 [監視] 之下，選擇 Application Insights](./media/app-insights-azure-web-apps/05-extend.png)
   
   * 選擇 toocreate 新的資源，除非您已經設定此應用程式的 Application Insights 資源的另一個路由。
2. 安裝 Application Insights 之後，**檢測您的 Web 應用程式**。 
   
    ![檢測 Web 應用程式](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   針對頁面檢視和使用者遙測**啟用用戶端監視**。

   * 選取 [設定] > [應用程式設定]
   * 在 [應用程式設定] 之下，新增索引鍵值組︰ 
   
    索引鍵︰`APPINSIGHTS_JAVASCRIPT_ENABLED` 
    
    值: `true`
   * **儲存**hello 設定和**重新啟動**您的應用程式。
3. **監視 Web 應用程式**。  [Expore hello 資料](#explore-the-data)。

稍後，您可以建立 hello 與 Application Insights 的應用程式，如果您想。

*如何移除 Application Insights 或切換 toosending tooanother 資源？*

* 在 Azure 中，開啟 hello web 應用程式控制項刀鋒視窗，並在開發工具，開啟**延伸**。 刪除 hello Application Insights 擴充功能。 然後在 [監視中]，選擇 Application Insights 和建立或選取您想要的 hello 資源。

## <a name="build-hello-app-with-application-insights"></a>建置 hello 與 Application Insights 的應用程式
Application Insights 可以提供更詳細的遙測，方法是將 SDK 安裝至您的 App。 特別是，您可以收集追蹤記錄檔、[撰寫自訂遙測](app-insights-api-custom-events-metrics.md)，並取得更詳細的例外狀況報告。

1. **在 Visual Studio 中** (2013 Update 2 或更新版本)，為專案設定 Application Insights。

    以滑鼠右鍵按一下 hello web 專案，然後選取**新增 > Application Insights**或**設定 Application Insights**。
   
    ![以滑鼠右鍵按一下 hello web 專案，然後選擇 新增或設定 Application Insights](./media/app-insights-azure-web-apps/03-add.png)
   
    如果您詢問 toosign 中的，使用您的 Azure 帳戶 hello 認證。
   
    hello 作業有兩個效果：
   
   1. 在 Azure 中建立 Application Insights 資源，這是存放、分析和顯示遙測資料的位置。
   2. 新增 hello Application Insights NuGet 封裝 tooyour 程式碼 （如果尚未存在），並將它設定 toosend 遙測 toohello Azure 資源。
2. **測試 hello 遙測**所執行的 hello 應用程式，在開發電腦 (F5)。
3. **Hello 應用程式發行**tooAzure hello 以一般方式。 

*我要如何切換 toosending tooa 不同的 Application Insights 資源？*

* 在 Visual Studio 中，以滑鼠右鍵按一下 hello 專案中，選擇 **設定 Application Insights**並選擇您想要的 hello 資源。 您會收到 hello 選項 toocreate 新的資源。 重建並重新部署。

## <a name="explore-hello-data"></a>瀏覽 hello 資料
1. 在 hello Application Insights 刀鋒視窗中的 web 應用程式控制台，您會看到即時的度量，第二個或兩個內顯示要求和失敗發生。 當您要重新發佈應用程式時，這就非常有用 - 您可以立即看到任何問題。
2. 按一下瀏覽 toohello 完整的 Application Insights 資源。

    ![點選](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    您也可以直接從 Azure 資源導覽前往該處。

1. 按一下任何圖 tooget 透過更多詳細資料：
   
    ![在 hello Application Insights 概觀刀鋒視窗中，按一下 圖表](./media/app-insights-azure-web-apps/07-dependency.png)
   
    您可以 [自訂計量刀鋒視窗](app-insights-metrics-explorer.md)。
2. 按一下所有進一步 toosee 個別事件和其屬性：
   
    ![按一下 搜尋篩選該型別的事件類型 tooopen](./media/app-insights-azure-web-apps/08-requests.png)
   
    請注意，"…"hello 連結 tooopen 所有屬性。
   
    您可以 [自訂搜尋](app-insights-diagnostic-search.md)。

透過您的遙測功能更強大的搜尋，請使用 hello[記錄分析查詢語言](app-insights-analytics-tour.md)。

## <a name="more-telemetry"></a>更多遙測

* [網頁載入資料](app-insights-javascript.md)
* [自訂遙測](app-insights-api-custom-events-metrics.md)

## <a name="video"></a>影片

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>後續步驟
* [即時應用程式上執行 hello 分析工具](app-insights-profiler.md)。
* [Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - 使用 Application Insights 監視 Azure Functions
* [啟用 Azure 診斷](app-insights-azure-diagnostics.md)toobe 傳送 tooApplication 深入資訊。
* [監視服務健康狀況度量](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)toomake 確定您的服務可用，並能繼續回應。
* 每當發生作業事件或計量超過臨界值時，[接收警示通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。
* 使用[Application Insights for JavaScript 應用程式及網頁](app-insights-javascript.md)tooget hello 瀏覽器瀏覽網頁用戶端遙測資料。
* [設定可用性 web 測試](app-insights-monitor-web-app-availability.md)toobe 如果您的網站已關閉警示。

