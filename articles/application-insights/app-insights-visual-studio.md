---
title: "使用 Visual Studio 中的 Azure Application Insights aaaDebug 應用程式 |Microsoft 文件"
description: "偵錯期間和生產環境中的 Web 應用程式效能分析與診斷。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/7/2017
ms.author: bwren
ms.openlocfilehash: 20491fbe4505bf719039e5d1c220b1afec01db25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a>在 Visual Studio 中使用 Azure Application Insights 進行應用程式偵錯
在 Visual Studio (2015 和更新版本) 中，您可以使用 [Azure Application Insights](app-insights-overview.md) 的遙測，在偵錯時和在生產環境中分析 ASP.NET Web 應用程式的效能並診斷問題。

如果您建立使用 Visual Studio 2017 的 ASP.NET web 應用程式或更新版本中，它已經有 hello Application Insights SDK。 否則，如果您沒有這樣做，[加入 Application Insights tooyour 應用程式](app-insights-asp-net.md)。

toomonitor 您的應用程式時在即時的生產環境中，您通常 hello Application Insights 遙測中檢視 hello [Azure 入口網站](https://portal.azure.com)，其中您可以設定警示和適用於功能強大的監視工具。 但偵錯時，也可以搜尋和分析在 Visual Studio 中的 hello 遙測。 從您的生產網站和從偵錯您的開發電腦上執行，您可以使用 Visual Studio tooanalyze 遙測。 在 hello 後者的情況下，您可以分析偵錯執行，即使您尚未設定 hello SDK toosend 遙測 toohello Azure 入口網站。 

## <a name="run"></a> 偵錯您的專案
使用 F5，在本機偵錯模式下執行 Web 應用程式。 開啟不同頁面 toogenerate 某些遙測。

在 Visual Studio 中，您會看到已將您的專案中的 hello Application Insights 模組所記錄的 hello 事件計數。

![在 Visual Studio 中，hello Application Insights 按鈕會顯示在偵錯期間。](./media/app-insights-visual-studio/appinsights-09eventcount.png)

按一下此按鈕 toosearch 您遙測。 

## <a name="application-insights-search"></a>Application Insights 搜尋
hello Application Insights 搜尋視窗會顯示已記錄事件。 (如果您登入 tooAzure，當您設定 Application Insights，您可以搜尋 hello hello Azure 入口網站中的事件相同。)

![Hello 專案上按一下滑鼠右鍵，然後選擇 Application Insights 搜尋](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> 您選取或取消選取篩選器之後，按一下 在 hello 文字搜尋欄位中的 hello 結尾 hello 搜尋 按鈕。
>

hello 任意文字搜尋適用於所有在 hello 事件中的欄位。 例如，搜尋頁面; hello URL 的一部分或 hello 用戶端縣 （市）; 例如屬性的值或特定追蹤記錄檔中的文字。

按一下 任何事件 toosee 其詳細的內容。

要求 tooyour web 應用程式中，您可以按一下 toohello 程式碼。

![要求的詳細資料] 下按一下 [透過 toohello 程式碼](./media/app-insights-visual-studio/31.png)

您也可以開啟相關的項目 toohelp 診斷失敗的要求或例外狀況。

![在 要求詳細資料，向下捲動 toorelated 項目](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a>檢視例外狀況和失敗的要求
例外狀況報告顯示 hello [搜尋] 視窗中。 (在某些較舊類型的 ASP.NET 應用程式，也有[設定例外狀況監視](app-insights-asp-net-exceptions.md)toosee 由 hello 架構會處理的例外狀況。)

按一下 例外狀況 tooget 堆疊追蹤。 如果 hello 的 hello 應用程式的程式碼是在 Visual Studio 中開啟，您可以透過按一下從 hello 堆疊追蹤 toohello 相關 hello 程式碼行。

![例外狀況堆疊追蹤](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-hello-code"></a>Hello 程式碼中檢視要求和例外狀況的摘要
在 hello Code Lens 列每個處理常式方法的上方，您會看到 hello 要求和 Application Insights 在 hello 過去 24 小時記錄的例外狀況的計數。

![例外狀況堆疊追蹤](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> Code Lens 顯示僅限 Application Insights 資料是否您具有[設定您的應用程式 toosend 遙測 toohello Application Insights 入口網站](app-insights-asp-net.md)。
>

[深入了解 Code Lens 中的 Application Insights](app-insights-visual-studio-codelens.md)

## <a name="trends"></a>趨勢
趨勢是用來將應用程式一段時間內行為方式進行視覺化的工具。 

選擇**瀏覽遙測趨勢**從 hello Application Insights 工具列按鈕或 Application Insights 搜尋視窗。 選擇其中一個五個常見的查詢 tooget 啟動。 您可以根據遙測類型、時間範圍和其他屬性，分析不同的資料集。 

在您的資料，toofind 異常選擇其中一個 hello [檢視類型] 下拉式清單底下的 hello 異常選項。 在 hello hello 視窗底部的 hello 篩選選項使得中的輕鬆 toohone 您遙測的特定子集。

![趨勢](./media/app-insights-visual-studio/51.png)

[深入了解趨勢](app-insights-visual-studio-trends.md)。

## <a name="local-monitoring"></a>本機監視
（從 Visual Studio 2015 Update 2)如果您尚未設定 hello SDK toosend 遙測 toohello Application Insights 入口網站 （以便 ApplicationInsights.config 中沒有任何檢測金鑰） hello diagnostics 視窗會顯示您最新偵錯工作階段遙測資料。 

如果您已發佈過應用程式先前的版本，這是比較好的做法。 您不想從您的偵錯工作階段 toobe hello 遙測混 hello 遙測 hello 與 hello 發行的應用程式從 Application Insights 入口網站。

如果您有一些很也有用[自訂遙測](app-insights-api-custom-events-metrics.md)的 toodebug 傳送遙測 toohello 入口網站之前。

* *首先，我可以完整設定 Application Insights toosend 遙測 toohello 入口網站。但現在我想 toosee 只能在 Visual Studio 中的 hello 遙測。*
  
  * 在 hello 搜尋視窗的設定沒有選項 toosearch 本機診斷即使您的應用程式傳送遙測 toohello 入口網站。
  * 正在傳送 toohello 入口網站中，註解 hello 列 toostop 遙測`<instrumentationkey>...`從 ApplicationInsights.config。當您再次準備好 toosend 遙測 toohello 入口網站時，請取消註解。


## <a name="next-steps"></a>後續步驟
|  |  |
| --- | --- |
| **[新增更多測試](app-insights-asp-net-more.md)**<br/>監視使用狀況、可用性、相依性、例外狀況。 整合來自記錄架構的追蹤。 撰寫自訂遙測。 |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| **[使用 hello Application Insights 入口網站](app-insights-dashboards.md)**<br/>檢視儀表板、功能強大的診斷和分析工具、警示、即時的應用程式相依性對應，以及匯出的遙測資料。 |![Visual Studio](./media/app-insights-visual-studio/62.png) |

