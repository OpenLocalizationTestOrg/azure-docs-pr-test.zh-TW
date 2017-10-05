---
title: "監視 Windows 傳統型應用程式的使用情況和效能"
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
ms.openlocfilehash: 9d7e2a390adf10cbf5d88dd0084ce09136987309
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a><span data-ttu-id="f9cdb-103">監視 Windows 傳統型應用程式的使用情況和效能</span><span class="sxs-lookup"><span data-stu-id="f9cdb-103">Monitoring usage and performance in Windows Desktop apps</span></span>


<span data-ttu-id="f9cdb-104">[Azure Application Insights](app-insights-overview.md) 和 [HockeyApp](https://hockeyapp.net) 可讓您監視所部署之應用程式的使用情況和效能。</span><span class="sxs-lookup"><span data-stu-id="f9cdb-104">[Azure Application Insights](app-insights-overview.md) and [HockeyApp](https://hockeyapp.net) let you monitor your deployed application for usage and performance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9cdb-105">我們建議使用 [HockeyApp](https://hockeyapp.net) 來發佈和監視傳統型應用程式和裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="f9cdb-105">We recommend [HockeyApp](https://hockeyapp.net) to distribute and monitor desktop and device apps.</span></span> <span data-ttu-id="f9cdb-106">使用 HockeyApp，您可以管理發佈、即時測試和使用者意見，以及監視使用情況和當機報告。</span><span class="sxs-lookup"><span data-stu-id="f9cdb-106">With HockeyApp, you can manage distribution, live testing, and user feedback, as well as monitor usage and crash reports.</span></span> <span data-ttu-id="f9cdb-107">您也可以 [使用分析匯出及查詢遙測](app-insights-hockeyapp-bridge-app.md)。</span><span class="sxs-lookup"><span data-stu-id="f9cdb-107">You can also [export and query your telemetry with Analytics](app-insights-hockeyapp-bridge-app.md).</span></span>
> 
> <span data-ttu-id="f9cdb-108">雖然遙測可以從傳統型應用程式傳送至 Application Insights，但這主要是用來進行偵錯和實驗性用途。</span><span class="sxs-lookup"><span data-stu-id="f9cdb-108">Although telemetry can be sent to Application Insights from a desktop application, this is chiefly useful for debugging and experimental purposes.</span></span>
> 
> 

## <a name="to-send-telemetry-to-application-insights-from-a-windows-application"></a><span data-ttu-id="f9cdb-109">若要從 Windows 應用程式將遙測傳送至 Application Insights</span><span class="sxs-lookup"><span data-stu-id="f9cdb-109">To send telemetry to Application Insights from a Windows application</span></span>
1. <span data-ttu-id="f9cdb-110">在 [Azure 入口網站](https://portal.azure.com)中，建立 [Application Insights 資源](app-insights-create-new-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="f9cdb-110">In the [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="f9cdb-111">針對應用程式類型，選擇 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f9cdb-111">For application type, choose ASP.NET app.</span></span>
2. <span data-ttu-id="f9cdb-112">取得檢測金鑰的副本。</span><span class="sxs-lookup"><span data-stu-id="f9cdb-112">Take a copy of the Instrumentation Key.</span></span> <span data-ttu-id="f9cdb-113">在您剛才建立的新資源之 [Essentials] 下拉式清單中尋找金鑰。</span><span class="sxs-lookup"><span data-stu-id="f9cdb-113">Find the key in the Essentials drop-down of the new resource you just created.</span></span> 
3. <span data-ttu-id="f9cdb-114">在 Visual Studio 中，編輯應用程式專案的 NuGet 封裝，並新增 Microsoft.ApplicationInsights.WindowsServer。</span><span class="sxs-lookup"><span data-stu-id="f9cdb-114">In Visual Studio, edit the NuGet packages of your app project, and add Microsoft.ApplicationInsights.WindowsServer.</span></span> <span data-ttu-id="f9cdb-115">(或選擇 Microsoft.ApplicationInsights，如果您只想要單純的 API，而不需要標準遙測集合模組。)</span><span class="sxs-lookup"><span data-stu-id="f9cdb-115">(Or choose Microsoft.ApplicationInsights if you just want the bare API, without the standard telemetry collection modules.)</span></span>
4. <span data-ttu-id="f9cdb-116">在程式碼中設定檢測金鑰︰</span><span class="sxs-lookup"><span data-stu-id="f9cdb-116">Set the instrumentation key either in your code:</span></span>
   
    <span data-ttu-id="f9cdb-117">`TelemetryConfiguration.Active.InstrumentationKey = "`您的金鑰 `";`</span><span class="sxs-lookup"><span data-stu-id="f9cdb-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
   
    <span data-ttu-id="f9cdb-118">或在 ApplicationInsights.config 中設定檢測金鑰 (如果您已安裝其中一個標準遙測封裝)︰</span><span class="sxs-lookup"><span data-stu-id="f9cdb-118">or in ApplicationInsights.config (if you installed one of the standard telemetry packages):</span></span>
   
    <span data-ttu-id="f9cdb-119">`<InstrumentationKey>`*您的金鑰*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="f9cdb-119">`<InstrumentationKey>`*your key*`</InstrumentationKey>`</span></span> 
   
    <span data-ttu-id="f9cdb-120">如果使用 ApplicationInsights.config，請確定其在方案總管中的屬性已設定為 [建置動作] = [內容]、[複製到輸出目錄] = [複製] 。</span><span class="sxs-lookup"><span data-stu-id="f9cdb-120">If you use ApplicationInsights.config, make sure its properties in Solution Explorer are set to **Build Action = Content, Copy to Output Directory = Copy**.</span></span>
5. <span data-ttu-id="f9cdb-121">[使用 API](app-insights-api-custom-events-metrics.md) 傳送遙測。</span><span class="sxs-lookup"><span data-stu-id="f9cdb-121">[Use the API](app-insights-api-custom-events-metrics.md) to send telemetry.</span></span>
6. <span data-ttu-id="f9cdb-122">執行應用程式，並查看您在 Azure 入口網站中建立的資源內的遙測。</span><span class="sxs-lookup"><span data-stu-id="f9cdb-122">Run your app, and see the telemetry in the resource you created in the Azure Portal.</span></span>

## <span data-ttu-id="f9cdb-123"><a name="telemetry"></a>程式碼範例</span><span class="sxs-lookup"><span data-stu-id="f9cdb-123"><a name="telemetry"></a>Example code</span></span>
```C#

    public partial class Form1 : Form
    {
        private TelemetryClient tc = new TelemetryClient();
        ...
        private void Form1_Load(object sender, EventArgs e)
        {
            // Alternative to setting ikey in config file:
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

## <a name="next-steps"></a><span data-ttu-id="f9cdb-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f9cdb-124">Next steps</span></span>
* [<span data-ttu-id="f9cdb-125">建立儀表板</span><span class="sxs-lookup"><span data-stu-id="f9cdb-125">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="f9cdb-126">診斷搜尋</span><span class="sxs-lookup"><span data-stu-id="f9cdb-126">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="f9cdb-127">探索度量</span><span class="sxs-lookup"><span data-stu-id="f9cdb-127">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="f9cdb-128">撰寫分析查詢</span><span class="sxs-lookup"><span data-stu-id="f9cdb-128">Write Analytics queries</span></span>](app-insights-analytics.md)

