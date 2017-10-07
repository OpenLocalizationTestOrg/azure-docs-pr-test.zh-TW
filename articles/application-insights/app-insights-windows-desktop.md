---
title: "aaaMonitoring 使用量和 Windows 桌面應用程式的效能"
description: "使用 HockeyApp 和 Application Insights 分析 Windows 傳統型應用程式的使用情况和效能。"
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 19040746-3315-47e7-8c60-4b3000d2ddc4
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/26/2016
ms.author: bwren
ms.openlocfilehash: 73806885a6f0ed3896c0e43308c90ba087007887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a>監視 Windows 傳統型應用程式的使用情況和效能


[Azure Application Insights](app-insights-overview.md) 和 [HockeyApp](https://hockeyapp.net) 可讓您監視所部署之應用程式的使用情況和效能。

> [!IMPORTANT]
> 我們建議[HockeyApp](https://hockeyapp.net) toodistribute 和監視桌上型電腦和裝置的應用程式。 使用 HockeyApp，您可以管理發佈、即時測試和使用者意見，以及監視使用情況和當機報告。 您也可以 [使用分析匯出及查詢遙測](app-insights-hockeyapp-bridge-app.md)。
> 
> 雖然可以 tooApplication Insights 傳送遙測從桌面應用程式，這是達成做為偵錯和實驗的用途。
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a>從 Windows 應用程式的 toosend 遙測 tooApplication Insights
1. 在 hello [Azure 入口網站](https://portal.azure.com)，[建立 Application Insights 資源](app-insights-create-new-resource.md)。 針對應用程式類型，選擇 ASP.NET 應用程式。
2. 製作 hello 檢測金鑰的複本。 Hello 中找到金鑰 hello Essentials 下拉式清單 hello 您剛建立新的資源。 
3. 在 Visual Studio 中，編輯 hello NuGet 封裝的應用程式專案，並加入 Microsoft.ApplicationInsights.WindowsServer。 （或選擇 Microsoft.ApplicationInsights，如果您只想 hello 裸機 API，沒有 hello 標準遙測集合模組）。
4. 在您的程式碼設定 hello 檢測機碼：
   
    `TelemetryConfiguration.Active.InstrumentationKey = "`您的金鑰 `";` 
   
    或 ApplicationInsights.config （如果您已安裝其中一個 hello 標準遙測套件） 中：
   
    `<InstrumentationKey>`*您的金鑰*`</InstrumentationKey>` 
   
    如果您使用 ApplicationInsights.config，請確定其在 [方案總管] 中的屬性設定太**建置動作 = 複製 tooOutput 目錄的內容 = 複製**。
5. [使用 hello API](app-insights-api-custom-events-metrics.md) toosend 遙測。
6. 執行應用程式，請參閱您在 hello Azure 入口網站中建立的 hello 資源中的 hello 遙測。

## <a name="telemetry"></a>程式碼範例
```C#

    public partial class Form1 : Form
    {
        private TelemetryClient tc = new TelemetryClient();
        ...
        private void Form1_Load(object sender, EventArgs e)
        {
            // Alternative toosetting ikey in config file:
            tc.InstrumentationKey = "key copied from portal";

            // Set session data:
            tc.Context.User.Id = Environment.UserName;
            tc.Context.Session.Id = Guid.NewGuid().ToString();
            tc.Context.Device.OperatingSystem = Environment.OSVersion.ToString();

            // Log a page view:
            tc.TrackPageView("Form1");
            ...
        }

        protected override void OnClosing(CancelEventArgs e)
        {
            stop = true;
            if (tc != null)
            {
                tc.Flush(); // only for desktop apps

                // Allow time for flushing:
                System.Threading.Thread.Sleep(1000);
            }
            base.OnClosing(e);
        }

```

## <a name="next-steps"></a>後續步驟
* [建立儀表板](app-insights-dashboards.md)
* [診斷搜尋](app-insights-diagnostic-search.md)
* [探索度量](app-insights-metrics-explorer.md)
* [撰寫分析查詢](app-insights-analytics.md)

