---
title: "在 Azure Application Insights 中監視 Docker 應用程式 | Microsoft Docs"
description: "Docker 效能計數器、事件和例外狀況可以與來自容器化應用程式的遙測一起顯示在 Application Insights 上。"
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
ms.openlocfilehash: b082e345ca1bb3b12c548e05e699474d3aa9306c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a><span data-ttu-id="0d51c-103">在 Application Insights 中監視 Docker 應用程式</span><span class="sxs-lookup"><span data-stu-id="0d51c-103">Monitor Docker applications in Application Insights</span></span>
<span data-ttu-id="0d51c-104">[Docker](https://www.docker.com/) 容器的週期事件和效能計數器可以在 Application Insights 上繪製成圖表。</span><span class="sxs-lookup"><span data-stu-id="0d51c-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span></span> <span data-ttu-id="0d51c-105">在您的主機的容器中安裝 [Application Insights](app-insights-overview.md) 映像，它會顯示主機及其他映像的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="0d51c-105">Install the [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for the host, as well as for the other images.</span></span>

<span data-ttu-id="0d51c-106">使用 Docker，您可以在完成所有相依性的輕量級容器中散發應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d51c-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span></span> <span data-ttu-id="0d51c-107">它們會在執行 Docker 引擎的任何主機電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="0d51c-107">They'll run on any host machine that runs a Docker Engine.</span></span>

<span data-ttu-id="0d51c-108">當您在 Docker 主機上執行 [Application Insights 映像 (英文)](https://hub.docker.com/r/microsoft/applicationinsights/) 時，可為您提供下列好處：</span><span class="sxs-lookup"><span data-stu-id="0d51c-108">When you run the [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span></span>

* <span data-ttu-id="0d51c-109">主機上執行之所有容器的相關週期遙測 - 啟動、停止等。</span><span class="sxs-lookup"><span data-stu-id="0d51c-109">Lifecycle telemetry about all the containers running on the host - start, stop, and so on.</span></span>
* <span data-ttu-id="0d51c-110">所有容器的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="0d51c-110">Performance counters for all the containers.</span></span> <span data-ttu-id="0d51c-111">CPU、記憶體、網路使用量等。</span><span class="sxs-lookup"><span data-stu-id="0d51c-111">CPU, memory, network usage, and more.</span></span>
* <span data-ttu-id="0d51c-112">如果您在於容器中執行的應用程式中[安裝了 Application Insights SDK for Java](app-insights-java-live.md)，則這些應用程式的所有遙測將會有可識別容器和主機電腦的額外屬性。</span><span class="sxs-lookup"><span data-stu-id="0d51c-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in the apps running in the containers, all the telemetry of those apps will have additional properties identifying the container and host machine.</span></span> <span data-ttu-id="0d51c-113">例如，如果您在多部主機上執行某個應用程式的多個執行個體，您可以輕鬆地依主機來篩選應用程式遙測。</span><span class="sxs-lookup"><span data-stu-id="0d51c-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span></span>

![範例](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a><span data-ttu-id="0d51c-115">設定您的 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="0d51c-115">Set up your Application Insights resource</span></span>
1. <span data-ttu-id="0d51c-116">登入 [Microsoft Azure 入口網站](https://azure.com)，然後開啟您應用程式的 Application Insights 資源；或[建立新的資源](app-insights-create-new-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="0d51c-116">Sign into [Microsoft Azure portal](https://azure.com) and open the Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span></span> 
   
    <span data-ttu-id="0d51c-117">*我應該使用哪種資源？*</span><span class="sxs-lookup"><span data-stu-id="0d51c-117">*Which resource should I use?*</span></span> <span data-ttu-id="0d51c-118">如果您在主機上執行的應用程式是由其他人所開發，則您需要[建立新的 Application Insights 資源](app-insights-create-new-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="0d51c-118">If the apps that you are running on your host were developed by someone else, then you need to [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="0d51c-119">這是您檢視及分析遙測的位置</span><span class="sxs-lookup"><span data-stu-id="0d51c-119">This is where you view and analyze the telemetry.</span></span> <span data-ttu-id="0d51c-120">(針對應用程式類型選取 [一般])。</span><span class="sxs-lookup"><span data-stu-id="0d51c-120">(Select 'General' for the app type.)</span></span>
   
    <span data-ttu-id="0d51c-121">但如果您是應用程式的開發人員，我們希望您 [將 Application Insights SDK 加入](app-insights-java-live.md) 每個應用程式中。</span><span class="sxs-lookup"><span data-stu-id="0d51c-121">But if you're the developer of the apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) to each of them.</span></span> <span data-ttu-id="0d51c-122">如果這些應用程式其實全部都是單一商務應用程式的元件，則您可能會設定所有應用程式將遙測資料傳送至一個資源，再使用該相同的資源來顯示 Docker 週期和效能資料。</span><span class="sxs-lookup"><span data-stu-id="0d51c-122">If they're all really components of a single business application, then you might configure all of them to send telemetry to one resource, and you'll use that same resource to display the Docker lifecycle and performance data.</span></span> 
   
    <span data-ttu-id="0d51c-123">第三種情況是您已開發大部分應用程式，但想要使用不同的資源來顯示其遙測。</span><span class="sxs-lookup"><span data-stu-id="0d51c-123">A third scenario is that you developed most of the apps, but you are using separate resources to display their telemetry.</span></span> <span data-ttu-id="0d51c-124">在這種情況下，您可能也需要為 Docker 資料建立不同的資源。</span><span class="sxs-lookup"><span data-stu-id="0d51c-124">In that case, you probably also want to create a separate resource for the Docker data.</span></span> 
2. <span data-ttu-id="0d51c-125">新增 [Docker] 磚：選擇 [新增磚]，從資源庫拖曳 [Docker] 磚，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="0d51c-125">Add the Docker tile: Choose **Add Tile**, drag the Docker tile from the gallery, and then click **Done**.</span></span> 
   
    ![範例](./media/app-insights-docker/03.png)
3. <span data-ttu-id="0d51c-127">按一下 [程式集]  下拉式清單，然後複製檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="0d51c-127">Click the **Essentials** drop-down and copy the Instrumentation Key.</span></span> <span data-ttu-id="0d51c-128">您將會使用這個項目以告知 SDK 傳送遙測的位置。</span><span class="sxs-lookup"><span data-stu-id="0d51c-128">You use this to tell the SDK where to send its telemetry.</span></span>

    ![範例](./media/app-insights-docker/02-props.png)

<span data-ttu-id="0d51c-130">保持該瀏覽器視窗就緒，因為您稍後即會返回以查看您的遙測。</span><span class="sxs-lookup"><span data-stu-id="0d51c-130">Keep that browser window handy, as you'll come back to it soon to look at your telemetry.</span></span>

## <a name="run-the-application-insights-monitor-on-your-host"></a><span data-ttu-id="0d51c-131">在您的主機上執行 Application Insights 監視器</span><span class="sxs-lookup"><span data-stu-id="0d51c-131">Run the Application Insights monitor on your host</span></span>
<span data-ttu-id="0d51c-132">當您有其他位置可顯示遙測之後，您可以設定收集和傳送遙測的容器化應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d51c-132">Now that you've got somewhere to display the telemetry, you can set up the containerized app that will collect and send it.</span></span>

1. <span data-ttu-id="0d51c-133">連接到您的 Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="0d51c-133">Connect to your Docker host.</span></span> 
2. <span data-ttu-id="0d51c-134">在這個命令中編輯您的檢測金鑰，然後執行命令：</span><span class="sxs-lookup"><span data-stu-id="0d51c-134">Edit your instrumentation key into this command, and then run it:</span></span>
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

<span data-ttu-id="0d51c-135">每部 Docker 主機只需要一個 Application Insights 映像。</span><span class="sxs-lookup"><span data-stu-id="0d51c-135">Only one Application Insights image is required per Docker host.</span></span> <span data-ttu-id="0d51c-136">如果您的應用程式部署在多部 Docker 主機上，請在每部主機上重複執行命令。</span><span class="sxs-lookup"><span data-stu-id="0d51c-136">If your application is deployed on multiple Docker hosts, then repeat the command on every host.</span></span>

## <a name="update-your-app"></a><span data-ttu-id="0d51c-137">更新應用程式</span><span class="sxs-lookup"><span data-stu-id="0d51c-137">Update your app</span></span>
<span data-ttu-id="0d51c-138">如果使用 [Application Insights SDK for Java](app-insights-java-get-started.md) 檢測您的應用程式，請將下行新增到您專案之 ApplicationInsights.xml 檔案中的 `<TelemetryInitializers>` 元素底下：</span><span class="sxs-lookup"><span data-stu-id="0d51c-138">If your application is instrumented with the [Application Insights SDK for Java](app-insights-java-get-started.md), add the following line into the ApplicationInsights.xml file in your project, under the `<TelemetryInitializers>` element:</span></span>

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

<span data-ttu-id="0d51c-139">這會將容器和主機 ID 等 Docker 資訊，加入從您的應用程式送出的每個遙測項目中。</span><span class="sxs-lookup"><span data-stu-id="0d51c-139">This adds Docker information such as container and host id to every telemetry item sent from your app.</span></span>

## <a name="view-your-telemetry"></a><span data-ttu-id="0d51c-140">檢視遙測</span><span class="sxs-lookup"><span data-stu-id="0d51c-140">View your telemetry</span></span>
<span data-ttu-id="0d51c-141">返回 Azure 入口網站中的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="0d51c-141">Go back to your Application Insights resource in the Azure portal.</span></span>

<span data-ttu-id="0d51c-142">點選 [Docker] 磚。</span><span class="sxs-lookup"><span data-stu-id="0d51c-142">Click through the Docker tile.</span></span>

<span data-ttu-id="0d51c-143">您很快就會看到來自 Docker 應用程式的資料抵達，尤其是如果您在 Docker 引擎上有其他容器執行。</span><span class="sxs-lookup"><span data-stu-id="0d51c-143">You'll shortly see data arriving from the Docker app, especially if you have other containers running on your Docker engine.</span></span>

<span data-ttu-id="0d51c-144">以下是一些您可以取得的檢視。</span><span class="sxs-lookup"><span data-stu-id="0d51c-144">Here are some of the views you can get.</span></span>

### <a name="perf-counters-by-host-activity-by-image"></a><span data-ttu-id="0d51c-145">依據主機的效能計數器，依據映像的活動</span><span class="sxs-lookup"><span data-stu-id="0d51c-145">Perf counters by host, activity by image</span></span>
![範例](./media/app-insights-docker/10.png)

![範例](./media/app-insights-docker/11.png)

<span data-ttu-id="0d51c-148">按一下任何主機或映像名稱以取得更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0d51c-148">Click any host or image name for more detail.</span></span>

<span data-ttu-id="0d51c-149">若要自訂檢視，按一下任何圖表、方格標題，或使用 [新增圖表]。</span><span class="sxs-lookup"><span data-stu-id="0d51c-149">To customize the view, click any chart, the grid heading, or use Add Chart.</span></span> 

<span data-ttu-id="0d51c-150">[深入了解計量瀏覽器](app-insights-metrics-explorer.md)。</span><span class="sxs-lookup"><span data-stu-id="0d51c-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span></span>

### <a name="docker-container-events"></a><span data-ttu-id="0d51c-151">Docker 容器事件</span><span class="sxs-lookup"><span data-stu-id="0d51c-151">Docker container events</span></span>
![範例](./media/app-insights-docker/13.png)

<span data-ttu-id="0d51c-153">若要調查個別事件，請按一下 [搜尋](app-insights-diagnostic-search.md)。</span><span class="sxs-lookup"><span data-stu-id="0d51c-153">To investigate individual events, click [Search](app-insights-diagnostic-search.md).</span></span> <span data-ttu-id="0d51c-154">搜尋和篩選以尋找您想要的事件。</span><span class="sxs-lookup"><span data-stu-id="0d51c-154">Search and filter to find the events you want.</span></span> <span data-ttu-id="0d51c-155">按一下任何事件以查看詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0d51c-155">Click any event to get more detail.</span></span>

### <a name="exceptions-by-container-name"></a><span data-ttu-id="0d51c-156">依據容器名稱的例外狀況</span><span class="sxs-lookup"><span data-stu-id="0d51c-156">Exceptions by container name</span></span>
![範例](./media/app-insights-docker/14.png)

### <a name="docker-context-added-to-app-telemetry"></a><span data-ttu-id="0d51c-158">已加入應用程式遙測中的 Docker 內容</span><span class="sxs-lookup"><span data-stu-id="0d51c-158">Docker context added to app telemetry</span></span>
<span data-ttu-id="0d51c-159">從使用 AI SDK 檢測之應用程式送出的要求遙測，並以 Docker 內容擴充：</span><span class="sxs-lookup"><span data-stu-id="0d51c-159">Request telemetry sent from the application instrumented with AI SDK, enriched with Docker context:</span></span>

![範例](./media/app-insights-docker/16.png)

<span data-ttu-id="0d51c-161">處理器時間和可用記憶體效能計數器，並依 Docker 容器名稱擴充和分組：</span><span class="sxs-lookup"><span data-stu-id="0d51c-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span></span>

![範例](./media/app-insights-docker/15.png)

## <a name="q--a"></a><span data-ttu-id="0d51c-163">問答集</span><span class="sxs-lookup"><span data-stu-id="0d51c-163">Q & A</span></span>
<span data-ttu-id="0d51c-164">*Application Insights 可以給我哪些無法從 Docker 取得的功能？*</span><span class="sxs-lookup"><span data-stu-id="0d51c-164">*What does Application Insights give me that I can't get from Docker?*</span></span>

* <span data-ttu-id="0d51c-165">依據容器和映像的效能計數器的詳細分解圖。</span><span class="sxs-lookup"><span data-stu-id="0d51c-165">Detailed breakdown of performance counters by container and image.</span></span>
* <span data-ttu-id="0d51c-166">將容器和應用程式資料整合在一個儀表板中。</span><span class="sxs-lookup"><span data-stu-id="0d51c-166">Integrate container and app data in one dashboard.</span></span>
* <span data-ttu-id="0d51c-167">[匯出遙測](app-insights-export-telemetry.md) 以進行資料庫、Power BI 或其他儀表板的進一步分析。</span><span class="sxs-lookup"><span data-stu-id="0d51c-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis to a database, Power BI or other dashboard.</span></span>

<span data-ttu-id="0d51c-168">*如何從應用程式本身取得遙測？*</span><span class="sxs-lookup"><span data-stu-id="0d51c-168">*How do I get telemetry from the app itself?*</span></span>

* <span data-ttu-id="0d51c-169">在應用程式中安裝 Application Insights SDK。</span><span class="sxs-lookup"><span data-stu-id="0d51c-169">Install the Application Insights SDK in the app.</span></span> <span data-ttu-id="0d51c-170">針對下列項目深入了解：[Java Web 應用程式](app-insights-java-get-started.md)、[Windows Web 應用程式](app-insights-asp-net.md)。</span><span class="sxs-lookup"><span data-stu-id="0d51c-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span></span>

## <a name="video"></a><span data-ttu-id="0d51c-171">影片</span><span class="sxs-lookup"><span data-stu-id="0d51c-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="0d51c-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0d51c-172">Next steps</span></span>

* [<span data-ttu-id="0d51c-173">適用於 Java 的 Application Insights</span><span class="sxs-lookup"><span data-stu-id="0d51c-173">Application Insights for Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="0d51c-174">適用於 Node.js 的 Application Insights</span><span class="sxs-lookup"><span data-stu-id="0d51c-174">Application Insights for Node.js</span></span>](app-insights-nodejs.md)
* [<span data-ttu-id="0d51c-175">適用於 ASP.NET 的 Application Insights</span><span class="sxs-lookup"><span data-stu-id="0d51c-175">Application Insights for ASP.NET</span></span>](app-insights-asp-net.md)
