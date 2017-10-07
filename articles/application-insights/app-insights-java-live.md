---
title: "aaaApplication Insights for Java web 應用程式已即時"
description: "開始監視已在伺服器上執行的 Web 應用程式"
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 12f3dbb9-915f-4087-87c9-807286030b0b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/10/2016
ms.author: bwren
ms.openlocfilehash: 2b01cd61657522ccf1d2d97b2a29cdeb08ec9a18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a><span data-ttu-id="f3846-103">適用於使用中 Java Web 應用程式的 Application Insights</span><span class="sxs-lookup"><span data-stu-id="f3846-103">Application Insights for Java web apps that are already live</span></span>


<span data-ttu-id="f3846-104">如果您有已經 J2EE 伺服器執行的 web 應用程式，您可以開始進行監視它與[Application Insights](app-insights-overview.md) hello 不需要 toomake 程式碼變更，或重新編譯您的專案。</span><span class="sxs-lookup"><span data-stu-id="f3846-104">If you have a web application that is already running on your J2EE server, you can start monitoring it with [Application Insights](app-insights-overview.md) without hello need toomake code changes or recompile your project.</span></span> <span data-ttu-id="f3846-105">使用此選項，您可以取得 HTTP 要求傳送 tooyour 伺服器、 未處理的例外狀況和效能計數器的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f3846-105">With this option, you get information about HTTP requests sent tooyour server, unhandled exceptions, and performance counters.</span></span>

<span data-ttu-id="f3846-106">您必須訂閱太[Microsoft Azure](https://azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f3846-106">You'll need a subscription too[Microsoft Azure](https://azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="f3846-107">在此頁面上的 hello 程序會加入 hello SDK tooyour web 應用程式在執行階段。</span><span class="sxs-lookup"><span data-stu-id="f3846-107">hello procedure on this page adds hello SDK tooyour web app at runtime.</span></span> <span data-ttu-id="f3846-108">如果您不想 tooupdate 或重建您的程式碼，此執行階段檢測將很有用。</span><span class="sxs-lookup"><span data-stu-id="f3846-108">This runtime instrumentation is useful if you don't want tooupdate or rebuild your source code.</span></span> <span data-ttu-id="f3846-109">如果可以的話，我們建議您，但是[新增 hello SDK toohello 原始程式碼](app-insights-java-get-started.md)改為。</span><span class="sxs-lookup"><span data-stu-id="f3846-109">But if you can, we recommend you [add hello SDK toohello source code](app-insights-java-get-started.md) instead.</span></span> <span data-ttu-id="f3846-110">可讓您更多的選項，例如撰寫程式碼 tootrack 使用者活動。</span><span class="sxs-lookup"><span data-stu-id="f3846-110">That gives you more options such as writing code tootrack user activity.</span></span>
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="f3846-111">1.取得 Application Insights 檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="f3846-111">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="f3846-112">登入 toohello [Microsoft Azure 入口網站](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="f3846-112">Sign in toohello [Microsoft Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="f3846-113">建立新的 Application Insights 資源，並設定 hello 應用程式類型 tooJava web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3846-113">Create a new Application Insights resource and set hello application type tooJava web application.</span></span>
   
    ![填寫名稱，選擇 [Java Web 應用程式]，然後按一下 [建立]](./media/app-insights-java-live/02-create.png)

    <span data-ttu-id="f3846-115">hello 資源建立在幾秒鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="f3846-115">hello resource is created in a few seconds.</span></span>

4. <span data-ttu-id="f3846-116">開啟 hello 新的資源，並取得其檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="f3846-116">Open hello new resource and get its instrumentation key.</span></span> <span data-ttu-id="f3846-117">您將需要 toopaste 這個機碼到您的程式碼專案很快。</span><span class="sxs-lookup"><span data-stu-id="f3846-117">You'll need toopaste this key into your code project shortly.</span></span>
   
    ![在新資源概觀 hello，按一下 內容並複製 hello 檢測金鑰](./media/app-insights-java-live/03-key.png)

## <a name="2-download-hello-sdk"></a><span data-ttu-id="f3846-119">2.下載 SDK hello</span><span class="sxs-lookup"><span data-stu-id="f3846-119">2. Download hello SDK</span></span>
1. <span data-ttu-id="f3846-120">下載 hello [Application Insights SDK for Java](https://aka.ms/aijavasdk)。</span><span class="sxs-lookup"><span data-stu-id="f3846-120">Download hello [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span> 
2. <span data-ttu-id="f3846-121">在伺服器上解壓縮 hello SDK 內容 toohello 目錄載入您的專案二進位檔的。</span><span class="sxs-lookup"><span data-stu-id="f3846-121">On your server, extract hello SDK contents toohello directory from which your project binaries are loaded.</span></span> <span data-ttu-id="f3846-122">如果您使用 Tomcat，此目錄通常在 `webapps/<your_app_name>/WEB-INF/lib` 之下</span><span class="sxs-lookup"><span data-stu-id="f3846-122">If you’re using Tomcat, this directory would typically be under `webapps/<your_app_name>/WEB-INF/lib`</span></span>

<span data-ttu-id="f3846-123">請注意，您需要 toorepeat 這每個伺服器執行個體，而且可用於每個應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3846-123">Note that you need toorepeat this on each server instance, and for each app.</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="f3846-124">3.加入 Application Insights XML 檔案</span><span class="sxs-lookup"><span data-stu-id="f3846-124">3. Add an Application Insights xml file</span></span>
<span data-ttu-id="f3846-125">建立 ApplicationInsights.xml 新增 hello SDK 中的 hello 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="f3846-125">Create ApplicationInsights.xml in hello folder in which you added hello SDK.</span></span> <span data-ttu-id="f3846-126">放入它 hello 下列 XML。</span><span class="sxs-lookup"><span data-stu-id="f3846-126">Put into it hello following XML.</span></span>

<span data-ttu-id="f3846-127">替代 hello 所得 hello Azure 入口網站的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="f3846-127">Substitute hello instrumentation key that you got from hello Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- hello key from hello portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data tooeach event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* <span data-ttu-id="f3846-128">hello 檢測金鑰會隨每個項目的遙測資料一起傳送，並告知 Application Insights toodisplay 在您的資源。</span><span class="sxs-lookup"><span data-stu-id="f3846-128">hello instrumentation key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>
* <span data-ttu-id="f3846-129">hello HTTP 要求的元件是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="f3846-129">hello HTTP Request component is optional.</span></span> <span data-ttu-id="f3846-130">它會自動傳送有關要求和回應時間 toohello 入口網站的遙測。</span><span class="sxs-lookup"><span data-stu-id="f3846-130">It automatically sends telemetry about requests and response times toohello portal.</span></span>
* <span data-ttu-id="f3846-131">事件相互關聯是加法 toohello HTTP 要求元件。</span><span class="sxs-lookup"><span data-stu-id="f3846-131">Events correlation is an addition toohello HTTP request component.</span></span> <span data-ttu-id="f3846-132">它會指派 hello 伺服器接收到的識別項 tooeach 要求，並將此識別項的遙測資料的屬性 tooevery 項目為新增為 hello 屬性 'Operation.Id'。</span><span class="sxs-lookup"><span data-stu-id="f3846-132">It assigns an identifier tooeach request received by hello server, and adds this identifier as a property tooevery item of telemetry as hello property 'Operation.Id'.</span></span> <span data-ttu-id="f3846-133">它可讓您藉由設定的篩選條件相關聯的每個要求 toocorrelate hello 遙測[診斷搜尋](app-insights-diagnostic-search.md)。</span><span class="sxs-lookup"><span data-stu-id="f3846-133">It allows you toocorrelate hello telemetry associated with each request by setting a filter in [diagnostic search](app-insights-diagnostic-search.md).</span></span>

## <a name="4-add-an-http-filter"></a><span data-ttu-id="f3846-134">4.加入 HTTP 篩選器</span><span class="sxs-lookup"><span data-stu-id="f3846-134">4. Add an HTTP filter</span></span>
<span data-ttu-id="f3846-135">找出並開啟您的專案，並遵循您的應用程式篩選器設定的位置的 hello web 應用程式 節點下，程式碼片段合併 hello hello web.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="f3846-135">Locate and open hello web.xml file in your project, and merge hello following snippet of code under hello web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="f3846-136">所有其他篩選條件之前，應該要對應 tooget hello 最精確的結果，hello 篩選。</span><span class="sxs-lookup"><span data-stu-id="f3846-136">tooget hello most accurate results, hello filter should be mapped before all other filters.</span></span>

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

## <a name="5-check-firewall-exceptions"></a><span data-ttu-id="f3846-137">5.檢查防火牆例外狀況</span><span class="sxs-lookup"><span data-stu-id="f3846-137">5. Check firewall exceptions</span></span>
<span data-ttu-id="f3846-138">您可能需要[設定例外狀況 toosend 傳出資料](app-insights-ip-addresses.md)。</span><span class="sxs-lookup"><span data-stu-id="f3846-138">You might need too[set exceptions toosend outgoing data](app-insights-ip-addresses.md).</span></span>

## <a name="6-restart-your-web-app"></a><span data-ttu-id="f3846-139">6.重新啟動您的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="f3846-139">6. Restart your web app</span></span>
## <a name="7-view-your-telemetry-in-application-insights"></a><span data-ttu-id="f3846-140">7.在 Application Insights 中檢視遙測</span><span class="sxs-lookup"><span data-stu-id="f3846-140">7. View your telemetry in Application Insights</span></span>
<span data-ttu-id="f3846-141">傳回在 tooyour Application Insights 資源[Microsoft Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f3846-141">Return tooyour Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="f3846-142">HTTP 要求的相關遙測會顯示 hello 概觀刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="f3846-142">Telemetry about HTTP requests appears on hello overview blade.</span></span> <span data-ttu-id="f3846-143">(如果沒有出現，請稍等片刻，然後按一下重新整理。)</span><span class="sxs-lookup"><span data-stu-id="f3846-143">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![範例資料](./media/app-insights-java-live/5-results.png)

<span data-ttu-id="f3846-145">按一下 透過任何圖表 toosee 度量詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f3846-145">Click through any chart toosee more detailed metrics.</span></span> 

![](./media/app-insights-java-live/6-barchart.png)

<span data-ttu-id="f3846-146">與檢視之要求的 hello 屬性，您會看見 hello 遙測事件與它相關聯，例如要求和例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f3846-146">And when viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-live/7-instance.png)

[<span data-ttu-id="f3846-147">深入了解度量。</span><span class="sxs-lookup"><span data-stu-id="f3846-147">Learn more about metrics.</span></span>](app-insights-metrics-explorer.md)

## <a name="next-steps"></a><span data-ttu-id="f3846-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f3846-148">Next steps</span></span>
* <span data-ttu-id="f3846-149">[將遙測 tooyour web 網頁](app-insights-javascript.md)toomonitor 頁面上，檢視和使用者度量。</span><span class="sxs-lookup"><span data-stu-id="f3846-149">[Add telemetry tooyour web pages](app-insights-javascript.md) toomonitor page views and user metrics.</span></span>
* <span data-ttu-id="f3846-150">[設定 web 測試](app-insights-monitor-web-app-availability.md)toomake 即時且回應迅速，保持您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3846-150">[Set up web tests](app-insights-monitor-web-app-availability.md) toomake sure your application stays live and responsive.</span></span>
* [<span data-ttu-id="f3846-151">擷取記錄追蹤</span><span class="sxs-lookup"><span data-stu-id="f3846-151">Capture log traces</span></span>](app-insights-java-trace-logs.md)
* <span data-ttu-id="f3846-152">[搜尋事件和記錄檔](app-insights-diagnostic-search.md)toohelp 診斷問題。</span><span class="sxs-lookup"><span data-stu-id="f3846-152">[Search events and logs](app-insights-diagnostic-search.md) toohelp diagnose problems.</span></span>

