---
title: "aaaMonitor Web 應用程式 |Microsoft 文件"
description: "深入了解如何註冊 Web 應用程式上的監視 tooset"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: c2f5e9842c732a804f1caee5d67e53dad24e190a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-app-service"></a>監視 App Service
本教學課程會逐步引導您透過監視您的應用程式和使用 hello 內建的平台工具 toosolve 問題發生時。

這份文件的每個章節都會復習特定的功能。 同時使用 hello 功能可讓您：
- 識別應用程式中的問題。
- 判斷當 hello 問題的起因是您的程式碼或 hello 平台。
- 請縮小您的程式碼中的 hello 問題 hello 來源。
- 偵錯和修正 hello 問題。

## <a name="before-you-begin"></a>開始之前
- 您需要 Web 應用程式 toomonitor 並遵循 hello 所述的步驟。
    - 您可以建立應用程式遵循 hello 中所述的 hello 步驟[建立 ASP.NET 應用程式在 Azure SQL Database 中](app-service-web-tutorial-dotnet-sqldatabase.md)教學課程。

- 如果您想 tootry**遠端偵錯**應用程式中，您需要 Visual Studio。
    - 如果您還沒有安裝 Visual Studio 2017，您可以下載並使用可用的 hello [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)。
    - 請確定您啟用**Azure 開發**hello Visual Studio 安裝期間。

## <a name="metrics"></a> 步驟 1 - 檢視計量
**度量**會很有用的 toounderstand:
- 應用程式健全狀況
- 應用程式效能
- 資源耗用量

當調查應用程式問題，檢閱度量是很好的起點 toostart。 Azure 入口網站已檢查您的應用程式使用的 hello 度量快速 toovisually **Azure 監視器**。

計量會提供應用程式之數個金鑰彙總的歷程記錄檢視。 App service 中裝載任何應用程式，您應監視 hello Web 應用程式和 hello 應用程式服務方案。

> [!NOTE]
> App Service 方案代表 hello 集合使用的實體資源 toohost 您的應用程式。 所有應用程式指派 tooan 它允許您 toosave 成本裝載多個應用程式時所定義的應用程式服務計劃共用 hello 資源。
>
> App Service 方案可定義：
> * 區域：北歐、美國東部、東南亞等。
> * 執行個體大小：小型、中型、大型等。
> * 級別計數：一、二或三個執行個體等。
> * SKU：免費、共用、基本、標準、進階等。

Web 應用程式，請移 toohello tooreview 度量**概觀**刀鋒視窗中的 hello 應用程式中，您想 toomonitor。 從這裡開始，您能以**監視圖格**的形式檢視應用程式計量的圖表。 按一下 hello 磚 tooedit 並設定哪些度量 tooview，hello 時間範圍 toodisplay。

根據預設 hello 資源刀鋒視窗會提供 hello 應用程式要求的檢視和 hello 過去一小時內的錯誤。
![監視應用程式](media/app-service-web-tutorial-monitoring/app-service-monitor.png)

您可以看到在 hello 範例中，我們會有應用程式會將產生許多**HTTP 伺服器錯誤**。 hello 大量的錯誤是 hello tooinvestigate 我們需要此應用程式的第一個指示。

> [!TIP]
> 深入了解 Azure 監視器以 hello 下列連結：
> - [開始使用 Azure 監視器](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Azure 計量](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [支援 Azure 監視器的計量](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [Azure 儀表板](..\azure-portal\azure-portal-dashboards.md)

## <a name="alerts"></a> 步驟 2 - 設定警示
**警示**可以設定的 tootrigger 應用程式的特定條件。

在[步驟 1-檢視度量](#metrics)，我們可了解 hello 應用程式有大量的錯誤。

可讓您設定警示 tooautomatically 在錯誤發生時收到通知。 在此情況下，我們想 hello 警示 toosend 電子郵件與每次 hello HTTP 50 X 錯誤的數目超過某個臨界值。

toocreate 的警示，瀏覽過**監視** > **警示**按一下**[+] 新增警示**。

![Alerts](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

提供 hello 警示設定中的值：
- **資源：** hello 網站 toomonitor hello 警示。
- **名稱︰**您警示的名稱，在此案例中為︰高 HTTP 50X。
- **描述︰**這項警示所查看的純文字說明。
- **警示項目︰**警示可以查看計量或事件，此範例中，我們要查看計量。
- **計量：**哪些度量 toomonitor，在此情況下： *HTTP 伺服器錯誤*。
- **條件：**當 tooalert，在此情況下選取 hello*大於*選項。
- **臨界值：**什麼是在此情況下，值 toolook: *400*。
- **週期：**在 hello 平均標準值上操作的警示。 較短的時間會造成警示較敏感。 在此情況下，我們看看 5 分鐘。
- **電子郵件擁有者和參與者︰**在此情況下︰已啟用。

既然 hello 警示建立電子郵件會傳送每次 hello 應用程式超過設定的 hello 臨界值。 作用中警示也應審核 hello Azure 入口網站中。

![觸發的警示](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> 深入了解 Azure 警示以 hello 下列連結：
> - [Microsoft Azure 中的警示是什麼](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [對計量採取動作](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [建立計量警示](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <a name="companion"></a> 步驟 3 - App Service Companion
**應用程式服務隨附**提供便利的方式 toomonitor 應用程式與行動裝置 （iOS 或 Android） 的原生體驗。

使用 Azure App Service Companion 來執行下列動作：
- 檢閱應用程式計量
- 檢閱應用程式警示和建議並採取動作
- 執行基本的疑難排解 （瀏覽、 啟動、 停止或重新啟動 hello 應用程式）
- 取得重大事件的推播通知。

![App Service Companion](media/app-service-web-tutorial-monitoring/app-service-companion.png)

[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

您可以從 hello 安裝應用程式服務隨附[App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)或[Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

## <a name="diagnose"></a> 步驟 4 - 診斷並解決問題
**診斷並解決問題**可協助您區隔出應用程式問題與平台問題。 它也可以建議可能的補救措施 tooget 您 Web 應用程式後 toohealthy。

![診斷並解決問題](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

繼續 hello 範例表單上一個步驟，我們可以看到，hello 應用程式具有已有可用性問題。 相反地，從 100%並未移動 hello 平台可用性。

當 hello 應用程式發生問題而且 hello 組成的平台會保持，很清楚，我們在處理應用程式問題的指示。

## <a name="logging"></a> 步驟 5 - 記錄
既然我們已經縮小 hello 失敗 tooan 應用程式問題，我們來看看 hello 應用程式和伺服器記錄檔 tooget 的詳細資訊。

記錄可讓您同時 toocollect **Application Diagnostics**和**Web Server 診斷**Web 應用程式記錄檔。

### <a name="application-diagnostics"></a>應用程式診斷
應用程式診斷可讓您 toocapture 所產生的追蹤 hello 應用程式在執行階段。

加入追蹤 tooyour 應用程式可大幅提升您的能力 toodebug 和 pin 點的問題。

在 ASP.NET 中，您可以記錄使用的應用程式追蹤[System.Diagnostics.Trace 類別](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx)toogenerate hello 記錄基礎結構所擷取的事件。 您也可以指定 hello 追蹤進行更容易篩選 hello 嚴重性。

```csharp
public ActionResult Delete(Guid? id)
{
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id);
    if (id == null)
    {
        System.Diagnostics.Trace.TraceError("/Todos/Delete/ failed, ID is null");
        return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
    }
    Todo todo = db.Todoes.Find(id);
    if (todo == null)
    {
        System.Diagnostics.Trace.TraceWarning("/Todos/Delete/ failed, ID: " + id + " could not be found");
        return HttpNotFound();
    }
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id + "completed successfully");
    return View(todo);
}
```
tooenable 應用程式記錄移過**監視** > **診斷記錄檔**和啟用的應用程式記錄使用 hello 切換。

![監視應用程式](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

應用程式記錄檔可以是預存的 tooyour Web 應用程式的檔案系統或推入 tooblob 儲存體。 生產案例中，對於建議的 toouse blob 儲存體。

> [!IMPORTANT]
> 啟用記錄會影響您的應用程式效能與資源使用率。 如果是生產案例，建議使用錯誤記錄檔。 只有在調查問題時，才能啟用更詳細資料記錄。

 ### <a name="web-server-diagnostics"></a>Web 伺服器診斷
即使未檢測您的應用程式，仍會產生 Web 伺服器記錄。 App Service 可以收集三種不同類型的伺服器記錄：

- **Web 伺服器記錄**
    - 使用 hello HTTP 交易資訊[W3C 擴充的記錄檔格式](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)。
    - 判斷整體站台的度量資訊，例如 hello 處理要求的數目或多少要求來自特定 IP 位址時很有用。
- **詳細錯誤記錄**
    - 對於表示失敗的 HTTP 狀態碼 (狀態碼 400 或更大) 的詳細錯誤資訊。
    - [深入了解詳細的錯誤記錄](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- **失敗要求的追蹤**
    - 失敗的要求，包括 hello IIS 元件的追蹤的詳細的資訊使用 tooprocess hello 要求和 hello 花費時間的每個元件。
    - 當嘗試 tooisolate 造成特定的 HTTP 錯誤的原因，則失敗的要求記錄檔會很有用。
    - [深入了解失敗的要求追蹤](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

tooenable 伺服器記錄：
- 跳過**監視** > **診斷記錄檔**。
- 啟用 hello 不同類型的 Web 伺服器診斷使用 hello 切換。

![監視應用程式](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> 啟用記錄會影響您的應用程式效能與資源使用率。 如果是生產案例，建議使用錯誤記錄檔，只有在調查問題時，才能啟用更詳細資訊記錄。

### <a name="accessing-logs"></a>存取記錄
使用 Azure 儲存體總管來存取 Blob 儲存體中所儲存的記錄。 透過 FTP 存取儲存在 hello Web 應用程式的檔案系統中的記錄檔 hello 下列路徑底下：

- **應用程式記錄** - `%HOME%/LogFiles/Application/`。
    - 此資料夾內含有一或多個文字檔案，這些檔案涵蓋應用程式記錄所產生的資訊。
- **失敗的要求追蹤** - `%HOME%/LogFiles/W3SVC#########/`。
    - 此資料夾內含有一個 XSL 檔案和一或多個 XML 檔案。
- **詳細的錯誤記錄** - `%HOME%/LogFiles/DetailedErrors/`。
    - 此資料夾包含一或多個 .htm 檔案，以及關於您應用程式所產生之 HTTP 錯誤的詳細資訊。
- **Web 伺服器記錄** - `%HOME%/LogFiles/http/RawLogs`。
    - 此資料夾包含一個或多個使用 hello W3C 擴充的記錄檔格式來格式化的文字檔案。

## <a name="streaming"></a> 步驟 6 - 記錄資料流
偵錯應用程式，因為它會將儲存時間太相比時，資料流記錄會很方便[存取 hello 記錄](#Accessing-Logs)透過 FTP。

App Service 可以在產生**應用程式記錄**和 **Web 伺服器記錄**時對它們進行資料流處理。

> [!TIP]
> 然後再嘗試 toostream 記錄檔，請確定您已啟用收集記錄檔，hello 中所述[記錄](#logging)> 一節。

toostream 記錄移過**監視**> **記錄檔資料流**。 根據您要尋找的是何種資訊來選取 [應用程式記錄] 或 [Web 伺服器記錄]。 從這裡，您也可以暫停、 重新啟動，並清除 hello 緩衝區。

![串流記錄](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> Hello 應用程式上沒有流量時，才會產生記錄檔，您也可以增加記錄檔 tooget hello 詳細資訊，多個事件或資訊。

## <a name="remote"></a> 步驟 7 - 遠端偵錯
Pin 碼指向 hello hello 應用程式的問題來源之後，使用**遠端偵錯**toowalk 透過 hello 程式碼。

遠端偵錯可讓您將連接 Web 應用程式的偵錯工具 tooyour hello 雲端中執行。 您可以設定中斷點、 直接管理記憶體、 逐步執行程式碼，和甚至變更 hello 就像在本機執行的應用程式的程式碼路徑。

tooattach hello 偵錯工具 tooyour 應用程式 hello 雲端中執行：

- 使用 Visual Studio 2017，hello 應用程式的開啟 hello 方案想 toodebug
- 設定一些中斷點，就像您針對本機開發所做的。
- 開啟 [Cloud Explorer] \(ctr + /，ctrl + x)。
- 視需要利用您的 Azure 認證登入。
- 尋找您想要 toodebug 的 hello 應用程式
- 選取**附加偵錯工具**表單 hello**動作**窗格。

![遠端偵錯](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

Visual Studio 設定遠端偵錯您應用程式，並啟動瀏覽器視窗瀏覽 tooyour 應用程式。 瀏覽您的應用程式 tootrigger 中斷點和逐步執行 hello 程式碼。

> [!WARNING]
> 不建議在生產環境中執行偵錯模式。 如果您的生產環境應用程式未向外延展 toomultiple 伺服器執行個體中，偵錯防止 hello 回應 tooother 要求 web 伺服器。 如需疑難排解生產環境的問題，您的最佳資源太[設定記錄](#logging)和[Application Insights](#insights)。



## <a name="explorer"></a> 步驟 8 - 處理序總管
當您的應用程式會向外延展比一個執行個體，toomore**處理序總管**可協助您識別執行個體的特定問題。

使用**處理序總管**來執行下列動作：

- 列舉所有 hello 處理程序跨應用程式服務方案的不同執行個體。
- 向下鑽研，並檢視 hello 控點，每個處理序相關聯的模組。
- 檢視 CPU、 工作集和執行緒計數在 hello 處理層級 toohelp 識別失控處理程序
- 尋找開啟檔案控制代碼，甚至終止特定的處理序執行個體。

可在 [監視] > [處理序總管] 下方找到處理序總管。

![處理序總管](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <a name="insights"></a> 步驟 9 - Application Insights
**Application Insights** 可為您的應用程式提供應用程式分析和進階監視功能。

使用 Application Insights toodetect 和診斷例外狀況和 Web 應用程式中的效能問題。

您可以在 [監視] > [Application Insights] 下方，針對 Web 應用程式啟用 Application Insights

> [!NOTE]
> Application Insights 可能會提示您 tooinstall hello Application Insights 站台擴充 toostart 收集資料。 安裝 hello 的網站擴充功能會導致應用程式重新啟動。

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

Application Insights 有豐富的功能設定，toolearn 詳細資訊，請依照下列包含在 hello hello 連結[接下來的步驟](#next)> 一節。

## <a name="next"></a> 後續步驟

 - [什麼是 Application Insights](..\application-insights\app-insights-overview.md)
 - [使用 Application Insights 監視 Azure Web 應用程式效能](..\application-insights\app-insights-azure-web-apps.md)
 - [使用 Application Insights 監視任何網站的可用性和回應性](..\application-insights\app-insights-monitor-web-app-availability.md)
