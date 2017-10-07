---
title: "在 Azure Application Insights aaaMonitor Docker 應用程式 |Microsoft 文件"
description: "Docker 的效能計數器、 事件和例外狀況可以顯示在 Application Insights 以及 hello hello 容器化應用程式的遙測。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9aaf1076bae25485a396db1bb3dcd13bccd87c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a><span data-ttu-id="3bd62-103">在 Application Insights 中監視 Docker 應用程式</span><span class="sxs-lookup"><span data-stu-id="3bd62-103">Monitor Docker applications in Application Insights</span></span>
<span data-ttu-id="3bd62-104">[Docker](https://www.docker.com/) 容器的週期事件和效能計數器可以在 Application Insights 上繪製成圖表。</span><span class="sxs-lookup"><span data-stu-id="3bd62-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span></span> <span data-ttu-id="3bd62-105">安裝 hello [Application Insights](app-insights-overview.md)映像的容器中您的主機，而且會顯示 hello 主機的效能計數器，如為適合 hello 其他映像。</span><span class="sxs-lookup"><span data-stu-id="3bd62-105">Install hello [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for hello host, as well as for hello other images.</span></span>

<span data-ttu-id="3bd62-106">使用 Docker，您可以在完成所有相依性的輕量級容器中散發應用程式。</span><span class="sxs-lookup"><span data-stu-id="3bd62-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span></span> <span data-ttu-id="3bd62-107">它們會在執行 Docker 引擎的任何主機電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="3bd62-107">They'll run on any host machine that runs a Docker Engine.</span></span>

<span data-ttu-id="3bd62-108">當您執行 hello [Application Insights 映像](https://hub.docker.com/r/microsoft/applicationinsights/)上 Docker 主機時，您會獲得下列益處：</span><span class="sxs-lookup"><span data-stu-id="3bd62-108">When you run hello [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span></span>

* <span data-ttu-id="3bd62-109">關於執行所有 hello 容器的生命週期遙測 hello 主機-上啟動、 停止和等等。</span><span class="sxs-lookup"><span data-stu-id="3bd62-109">Lifecycle telemetry about all hello containers running on hello host - start, stop, and so on.</span></span>
* <span data-ttu-id="3bd62-110">所有的 hello 容器的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="3bd62-110">Performance counters for all hello containers.</span></span> <span data-ttu-id="3bd62-111">CPU、記憶體、網路使用量等。</span><span class="sxs-lookup"><span data-stu-id="3bd62-111">CPU, memory, network usage, and more.</span></span>
* <span data-ttu-id="3bd62-112">如果您[安裝 Application Insights SDK for Java](app-insights-java-live.md)在 hello hello 容器中執行應用程式，這些應用程式的所有 hello 遙測會都有識別 hello 容器和主機電腦的其他屬性。</span><span class="sxs-lookup"><span data-stu-id="3bd62-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in hello apps running in hello containers, all hello telemetry of those apps will have additional properties identifying hello container and host machine.</span></span> <span data-ttu-id="3bd62-113">例如，如果您在多部主機上執行某個應用程式的多個執行個體，您可以輕鬆地依主機來篩選應用程式遙測。</span><span class="sxs-lookup"><span data-stu-id="3bd62-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span></span>

![範例](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a><span data-ttu-id="3bd62-115">設定您的 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="3bd62-115">Set up your Application Insights resource</span></span>
1. <span data-ttu-id="3bd62-116">登入[Microsoft Azure 入口網站](https://azure.com)並開啟您的應用程式; hello Application Insights 資源或[建立一個新](app-insights-create-new-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="3bd62-116">Sign into [Microsoft Azure portal](https://azure.com) and open hello Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span></span> 
   
    <span data-ttu-id="3bd62-117">*我應該使用哪種資源？*</span><span class="sxs-lookup"><span data-stu-id="3bd62-117">*Which resource should I use?*</span></span> <span data-ttu-id="3bd62-118">如果由其他使用者所開發的 hello 您主機執行您的應用程式，則您需要[建立新的 Application Insights 資源](app-insights-create-new-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="3bd62-118">If hello apps that you are running on your host were developed by someone else, then you need too[create a new Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="3bd62-119">這是供您檢視及分析 hello 遙測。</span><span class="sxs-lookup"><span data-stu-id="3bd62-119">This is where you view and analyze hello telemetry.</span></span> <span data-ttu-id="3bd62-120">（選取 [一般] hello 應用程式類型）。</span><span class="sxs-lookup"><span data-stu-id="3bd62-120">(Select 'General' for hello app type.)</span></span>
   
    <span data-ttu-id="3bd62-121">但如果您是開發人員 hello hello 應用程式，然後我們希望您[加入 Application Insights SDK](app-insights-java-live.md) tooeach 它們。</span><span class="sxs-lookup"><span data-stu-id="3bd62-121">But if you're hello developer of hello apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) tooeach of them.</span></span> <span data-ttu-id="3bd62-122">如果是真正的所有元件的單一商務應用程式，則您可能會設定所有的這些 toosend 遙測 tooone 資源，以及您將使用相同資源 toodisplay hello Docker 生命週期和效能資料。</span><span class="sxs-lookup"><span data-stu-id="3bd62-122">If they're all really components of a single business application, then you might configure all of them toosend telemetry tooone resource, and you'll use that same resource toodisplay hello Docker lifecycle and performance data.</span></span> 
   
    <span data-ttu-id="3bd62-123">第三個案例是您開發了大部分的 hello 應用程式，但您要使用不同的資源 toodisplay 其遙測。</span><span class="sxs-lookup"><span data-stu-id="3bd62-123">A third scenario is that you developed most of hello apps, but you are using separate resources toodisplay their telemetry.</span></span> <span data-ttu-id="3bd62-124">在此情況下，您可能也想 toocreate hello Docker 資料不同的資源。</span><span class="sxs-lookup"><span data-stu-id="3bd62-124">In that case, you probably also want toocreate a separate resource for hello Docker data.</span></span> 
2. <span data-ttu-id="3bd62-125">新增 hello Docker 磚： 選擇**新增磚**，從 hello 圖庫拖曳 hello Docker 磚，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="3bd62-125">Add hello Docker tile: Choose **Add Tile**, drag hello Docker tile from hello gallery, and then click **Done**.</span></span> 
   
    ![範例](./media/app-insights-docker/03.png)
3. <span data-ttu-id="3bd62-127">按一下 hello **Essentials**下拉式清單，並將複製 hello 檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="3bd62-127">Click hello **Essentials** drop-down and copy hello Instrumentation Key.</span></span> <span data-ttu-id="3bd62-128">使用此 tootell hello SDK 其中 toosend 其遙測。</span><span class="sxs-lookup"><span data-stu-id="3bd62-128">You use this tootell hello SDK where toosend its telemetry.</span></span>

    ![範例](./media/app-insights-docker/02-props.png)

<span data-ttu-id="3bd62-130">該瀏覽器視窗保持方便使用，您再回來 tooit 推出 toolook 在您的遙測。</span><span class="sxs-lookup"><span data-stu-id="3bd62-130">Keep that browser window handy, as you'll come back tooit soon toolook at your telemetry.</span></span>

## <a name="run-hello-application-insights-monitor-on-your-host"></a><span data-ttu-id="3bd62-131">在主機上執行 hello Application Insights 監視</span><span class="sxs-lookup"><span data-stu-id="3bd62-131">Run hello Application Insights monitor on your host</span></span>
<span data-ttu-id="3bd62-132">現在，您有某處 toodisplay hello 遙測，您可以設定，將會收集並傳送的 hello 進行容器化應用程式。</span><span class="sxs-lookup"><span data-stu-id="3bd62-132">Now that you've got somewhere toodisplay hello telemetry, you can set up hello containerized app that will collect and send it.</span></span>

1. <span data-ttu-id="3bd62-133">連接 tooyour Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="3bd62-133">Connect tooyour Docker host.</span></span> 
2. <span data-ttu-id="3bd62-134">在這個命令中編輯您的檢測金鑰，然後執行命令：</span><span class="sxs-lookup"><span data-stu-id="3bd62-134">Edit your instrumentation key into this command, and then run it:</span></span>
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

<span data-ttu-id="3bd62-135">每部 Docker 主機只需要一個 Application Insights 映像。</span><span class="sxs-lookup"><span data-stu-id="3bd62-135">Only one Application Insights image is required per Docker host.</span></span> <span data-ttu-id="3bd62-136">如果您的應用程式部署在多部 Docker 主機，然後重複每一部主機的 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="3bd62-136">If your application is deployed on multiple Docker hosts, then repeat hello command on every host.</span></span>

## <a name="update-your-app"></a><span data-ttu-id="3bd62-137">更新應用程式</span><span class="sxs-lookup"><span data-stu-id="3bd62-137">Update your app</span></span>
<span data-ttu-id="3bd62-138">若您的應用程式設有 hello [Application Insights SDK for Java](app-insights-java-get-started.md)，新增到在專案中，在 hello hello ApplicationInsights.xml 檔案下列行 hello`<TelemetryInitializers>`項目：</span><span class="sxs-lookup"><span data-stu-id="3bd62-138">If your application is instrumented with hello [Application Insights SDK for Java](app-insights-java-get-started.md), add hello following line into hello ApplicationInsights.xml file in your project, under hello `<TelemetryInitializers>` element:</span></span>

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

<span data-ttu-id="3bd62-139">如此會將 Docker 例如容器與主機識別碼 tooevery 遙測項目從您的應用程式傳送的資訊。</span><span class="sxs-lookup"><span data-stu-id="3bd62-139">This adds Docker information such as container and host id tooevery telemetry item sent from your app.</span></span>

## <a name="view-your-telemetry"></a><span data-ttu-id="3bd62-140">檢視遙測</span><span class="sxs-lookup"><span data-stu-id="3bd62-140">View your telemetry</span></span>
<span data-ttu-id="3bd62-141">返回 tooyour hello Azure 入口網站中的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="3bd62-141">Go back tooyour Application Insights resource in hello Azure portal.</span></span>

<span data-ttu-id="3bd62-142">按一下瀏覽 hello Docker 磚。</span><span class="sxs-lookup"><span data-stu-id="3bd62-142">Click through hello Docker tile.</span></span>

<span data-ttu-id="3bd62-143">您很快就會看到資料抵達 hello Docker 應用程式，尤其是如果您在 Docker 引擎上執行的其他容器。</span><span class="sxs-lookup"><span data-stu-id="3bd62-143">You'll shortly see data arriving from hello Docker app, especially if you have other containers running on your Docker engine.</span></span>

<span data-ttu-id="3bd62-144">以下是一些您可以取得 hello 檢視。</span><span class="sxs-lookup"><span data-stu-id="3bd62-144">Here are some of hello views you can get.</span></span>

### <a name="perf-counters-by-host-activity-by-image"></a><span data-ttu-id="3bd62-145">依據主機的效能計數器，依據映像的活動</span><span class="sxs-lookup"><span data-stu-id="3bd62-145">Perf counters by host, activity by image</span></span>
![範例](./media/app-insights-docker/10.png)

![範例](./media/app-insights-docker/11.png)

<span data-ttu-id="3bd62-148">按一下任何主機或映像名稱以取得更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3bd62-148">Click any host or image name for more detail.</span></span>

<span data-ttu-id="3bd62-149">toocustomize hello] 檢視中，按一下任何圖、 標題，hello 方格，或使用 [新增圖表。</span><span class="sxs-lookup"><span data-stu-id="3bd62-149">toocustomize hello view, click any chart, hello grid heading, or use Add Chart.</span></span> 

<span data-ttu-id="3bd62-150">[深入了解計量瀏覽器](app-insights-metrics-explorer.md)。</span><span class="sxs-lookup"><span data-stu-id="3bd62-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span></span>

### <a name="docker-container-events"></a><span data-ttu-id="3bd62-151">Docker 容器事件</span><span class="sxs-lookup"><span data-stu-id="3bd62-151">Docker container events</span></span>
![範例](./media/app-insights-docker/13.png)

<span data-ttu-id="3bd62-153">tooinvestigate 個別事件，按一下[搜尋](app-insights-diagnostic-search.md)。</span><span class="sxs-lookup"><span data-stu-id="3bd62-153">tooinvestigate individual events, click [Search](app-insights-diagnostic-search.md).</span></span> <span data-ttu-id="3bd62-154">搜尋和篩選您想要的 toofind hello 事件。</span><span class="sxs-lookup"><span data-stu-id="3bd62-154">Search and filter toofind hello events you want.</span></span> <span data-ttu-id="3bd62-155">按一下任何事件 tooget 更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3bd62-155">Click any event tooget more detail.</span></span>

### <a name="exceptions-by-container-name"></a><span data-ttu-id="3bd62-156">依據容器名稱的例外狀況</span><span class="sxs-lookup"><span data-stu-id="3bd62-156">Exceptions by container name</span></span>
![範例](./media/app-insights-docker/14.png)

### <a name="docker-context-added-tooapp-telemetry"></a><span data-ttu-id="3bd62-158">Docker 內容加入 tooapp 遙測</span><span class="sxs-lookup"><span data-stu-id="3bd62-158">Docker context added tooapp telemetry</span></span>
<span data-ttu-id="3bd62-159">從 hello AI SDK，增添 Docker 內容使用檢測的應用程式傳送要求遙測：</span><span class="sxs-lookup"><span data-stu-id="3bd62-159">Request telemetry sent from hello application instrumented with AI SDK, enriched with Docker context:</span></span>

![範例](./media/app-insights-docker/16.png)

<span data-ttu-id="3bd62-161">處理器時間和可用記憶體效能計數器，並依 Docker 容器名稱擴充和分組：</span><span class="sxs-lookup"><span data-stu-id="3bd62-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span></span>

![範例](./media/app-insights-docker/15.png)

## <a name="q--a"></a><span data-ttu-id="3bd62-163">問答集</span><span class="sxs-lookup"><span data-stu-id="3bd62-163">Q & A</span></span>
<span data-ttu-id="3bd62-164">*Application Insights 可以給我哪些無法從 Docker 取得的功能？*</span><span class="sxs-lookup"><span data-stu-id="3bd62-164">*What does Application Insights give me that I can't get from Docker?*</span></span>

* <span data-ttu-id="3bd62-165">依據容器和映像的效能計數器的詳細分解圖。</span><span class="sxs-lookup"><span data-stu-id="3bd62-165">Detailed breakdown of performance counters by container and image.</span></span>
* <span data-ttu-id="3bd62-166">將容器和應用程式資料整合在一個儀表板中。</span><span class="sxs-lookup"><span data-stu-id="3bd62-166">Integrate container and app data in one dashboard.</span></span>
* <span data-ttu-id="3bd62-167">[匯出遙測](app-insights-export-telemetry.md)進一步分析 tooa 資料庫、 Power BI 或其他儀表板。</span><span class="sxs-lookup"><span data-stu-id="3bd62-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis tooa database, Power BI or other dashboard.</span></span>

<span data-ttu-id="3bd62-168">*如何取得的 hello 應用程式本身的遙測？*</span><span class="sxs-lookup"><span data-stu-id="3bd62-168">*How do I get telemetry from hello app itself?*</span></span>

* <span data-ttu-id="3bd62-169">安裝 Application Insights SDK hello hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="3bd62-169">Install hello Application Insights SDK in hello app.</span></span> <span data-ttu-id="3bd62-170">針對下列項目深入了解：[Java Web 應用程式](app-insights-java-get-started.md)、[Windows Web 應用程式](app-insights-asp-net.md)。</span><span class="sxs-lookup"><span data-stu-id="3bd62-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span></span>

## <a name="video"></a><span data-ttu-id="3bd62-171">影片</span><span class="sxs-lookup"><span data-stu-id="3bd62-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="3bd62-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3bd62-172">Next steps</span></span>

* [<span data-ttu-id="3bd62-173">適用於 Java 的 Application Insights</span><span class="sxs-lookup"><span data-stu-id="3bd62-173">Application Insights for Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="3bd62-174">適用於 Node.js 的 Application Insights</span><span class="sxs-lookup"><span data-stu-id="3bd62-174">Application Insights for Node.js</span></span>](app-insights-nodejs.md)
* [<span data-ttu-id="3bd62-175">適用於 ASP.NET 的 Application Insights</span><span class="sxs-lookup"><span data-stu-id="3bd62-175">Application Insights for ASP.NET</span></span>](app-insights-asp-net.md)
