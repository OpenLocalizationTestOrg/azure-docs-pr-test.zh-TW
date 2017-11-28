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
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a><span data-ttu-id="a8048-103">監視 Windows 傳統型應用程式的使用情況和效能</span><span class="sxs-lookup"><span data-stu-id="a8048-103">Monitoring usage and performance in Windows Desktop apps</span></span>


<span data-ttu-id="a8048-104">[Azure Application Insights](app-insights-overview.md) 和 [HockeyApp](https://hockeyapp.net) 可讓您監視所部署之應用程式的使用情況和效能。</span><span class="sxs-lookup"><span data-stu-id="a8048-104">[Azure Application Insights](app-insights-overview.md) and [HockeyApp](https://hockeyapp.net) let you monitor your deployed application for usage and performance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8048-105">我們建議[HockeyApp](https://hockeyapp.net) toodistribute 和監視桌上型電腦和裝置的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a8048-105">We recommend [HockeyApp](https://hockeyapp.net) toodistribute and monitor desktop and device apps.</span></span> <span data-ttu-id="a8048-106">使用 HockeyApp，您可以管理發佈、即時測試和使用者意見，以及監視使用情況和當機報告。</span><span class="sxs-lookup"><span data-stu-id="a8048-106">With HockeyApp, you can manage distribution, live testing, and user feedback, as well as monitor usage and crash reports.</span></span> <span data-ttu-id="a8048-107">您也可以 [使用分析匯出及查詢遙測](app-insights-hockeyapp-bridge-app.md)。</span><span class="sxs-lookup"><span data-stu-id="a8048-107">You can also [export and query your telemetry with Analytics](app-insights-hockeyapp-bridge-app.md).</span></span>
> 
> <span data-ttu-id="a8048-108">雖然可以 tooApplication Insights 傳送遙測從桌面應用程式，這是達成做為偵錯和實驗的用途。</span><span class="sxs-lookup"><span data-stu-id="a8048-108">Although telemetry can be sent tooApplication Insights from a desktop application, this is chiefly useful for debugging and experimental purposes.</span></span>
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a><span data-ttu-id="a8048-109">從 Windows 應用程式的 toosend 遙測 tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="a8048-109">toosend telemetry tooApplication Insights from a Windows application</span></span>
1. <span data-ttu-id="a8048-110">在 hello [Azure 入口網站](https://portal.azure.com)，[建立 Application Insights 資源](app-insights-create-new-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="a8048-110">In hello [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="a8048-111">針對應用程式類型，選擇 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a8048-111">For application type, choose ASP.NET app.</span></span>
2. <span data-ttu-id="a8048-112">製作 hello 檢測金鑰的複本。</span><span class="sxs-lookup"><span data-stu-id="a8048-112">Take a copy of hello Instrumentation Key.</span></span> <span data-ttu-id="a8048-113">Hello 中找到金鑰 hello Essentials 下拉式清單 hello 您剛建立新的資源。</span><span class="sxs-lookup"><span data-stu-id="a8048-113">Find hello key in hello Essentials drop-down of hello new resource you just created.</span></span> 
3. <span data-ttu-id="a8048-114">在 Visual Studio 中，編輯 hello NuGet 封裝的應用程式專案，並加入 Microsoft.ApplicationInsights.WindowsServer。</span><span class="sxs-lookup"><span data-stu-id="a8048-114">In Visual Studio, edit hello NuGet packages of your app project, and add Microsoft.ApplicationInsights.WindowsServer.</span></span> <span data-ttu-id="a8048-115">（或選擇 Microsoft.ApplicationInsights，如果您只想 hello 裸機 API，沒有 hello 標準遙測集合模組）。</span><span class="sxs-lookup"><span data-stu-id="a8048-115">(Or choose Microsoft.ApplicationInsights if you just want hello bare API, without hello standard telemetry collection modules.)</span></span>
4. <span data-ttu-id="a8048-116">在您的程式碼設定 hello 檢測機碼：</span><span class="sxs-lookup"><span data-stu-id="a8048-116">Set hello instrumentation key either in your code:</span></span>
   
    <span data-ttu-id="a8048-117">`TelemetryConfiguration.Active.InstrumentationKey = "`您的金鑰 `";`</span><span class="sxs-lookup"><span data-stu-id="a8048-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
   
    <span data-ttu-id="a8048-118">或 ApplicationInsights.config （如果您已安裝其中一個 hello 標準遙測套件） 中：</span><span class="sxs-lookup"><span data-stu-id="a8048-118">or in ApplicationInsights.config (if you installed one of hello standard telemetry packages):</span></span>
   
    <span data-ttu-id="a8048-119">`<InstrumentationKey>`*您的金鑰*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="a8048-119">`<InstrumentationKey>`*your key*`</InstrumentationKey>`</span></span> 
   
    <span data-ttu-id="a8048-120">如果您使用 ApplicationInsights.config，請確定其在 [方案總管] 中的屬性設定太**建置動作 = 複製 tooOutput 目錄的內容 = 複製**。</span><span class="sxs-lookup"><span data-stu-id="a8048-120">If you use ApplicationInsights.config, make sure its properties in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>
5. <span data-ttu-id="a8048-121">[使用 hello API](app-insights-api-custom-events-metrics.md) toosend 遙測。</span><span class="sxs-lookup"><span data-stu-id="a8048-121">[Use hello API](app-insights-api-custom-events-metrics.md) toosend telemetry.</span></span>
6. <span data-ttu-id="a8048-122">執行應用程式，請參閱您在 hello Azure 入口網站中建立的 hello 資源中的 hello 遙測。</span><span class="sxs-lookup"><span data-stu-id="a8048-122">Run your app, and see hello telemetry in hello resource you created in hello Azure Portal.</span></span>

## <span data-ttu-id="a8048-123"><a name="telemetry"></a>程式碼範例</span><span class="sxs-lookup"><span data-stu-id="a8048-123"><a name="telemetry"></a>Example code</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="a8048-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a8048-124">Next steps</span></span>
* [<span data-ttu-id="a8048-125">建立儀表板</span><span class="sxs-lookup"><span data-stu-id="a8048-125">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="a8048-126">診斷搜尋</span><span class="sxs-lookup"><span data-stu-id="a8048-126">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="a8048-127">探索度量</span><span class="sxs-lookup"><span data-stu-id="a8048-127">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="a8048-128">撰寫分析查詢</span><span class="sxs-lookup"><span data-stu-id="a8048-128">Write Analytics queries</span></span>](app-insights-analytics.md)

