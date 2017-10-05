---
title: "適用於使用中 Java Web 應用程式的 Application Insights"
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
ms.openlocfilehash: a2731e3e44f8f3d104d8abc7dbe71fe3a4c3a690
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a><span data-ttu-id="e1e28-103">適用於使用中 Java Web 應用程式的 Application Insights</span><span class="sxs-lookup"><span data-stu-id="e1e28-103">Application Insights for Java web apps that are already live</span></span>


<span data-ttu-id="e1e28-104">如果您有 Web 應用程式已在 J2EE 伺服器上執行，您可以使用 [Application Insights](app-insights-overview.md) 開始監視它，不需要變更程式碼或重新編譯您的專案。</span><span class="sxs-lookup"><span data-stu-id="e1e28-104">If you have a web application that is already running on your J2EE server, you can start monitoring it with [Application Insights](app-insights-overview.md) without the need to make code changes or recompile your project.</span></span> <span data-ttu-id="e1e28-105">使用此選項可以取得傳送至您伺服器的 HTTP 要求、未處理的例外狀況和效能計數器的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e1e28-105">With this option, you get information about HTTP requests sent to your server, unhandled exceptions, and performance counters.</span></span>

<span data-ttu-id="e1e28-106">您將需要 [Microsoft Azure](https://azure.com)訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e1e28-106">You'll need a subscription to [Microsoft Azure](https://azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="e1e28-107">此頁面上的程序會在執行階段將 SDK 加入您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1e28-107">The procedure on this page adds the SDK to your web app at runtime.</span></span> <span data-ttu-id="e1e28-108">如果您不想要更新或重建您的原始程式碼，此執行階段檢測非常好用。</span><span class="sxs-lookup"><span data-stu-id="e1e28-108">This runtime instrumentation is useful if you don't want to update or rebuild your source code.</span></span> <span data-ttu-id="e1e28-109">不過，如果可以的話，我們建議您改為 [將 SDK 加入原始程式碼](app-insights-java-get-started.md) 。</span><span class="sxs-lookup"><span data-stu-id="e1e28-109">But if you can, we recommend you [add the SDK to the source code](app-insights-java-get-started.md) instead.</span></span> <span data-ttu-id="e1e28-110">這樣可以提供您更多選項，包括撰寫程式碼來追蹤使用者活動。</span><span class="sxs-lookup"><span data-stu-id="e1e28-110">That gives you more options such as writing code to track user activity.</span></span>
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="e1e28-111">1.取得 Application Insights 檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="e1e28-111">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="e1e28-112">登入 [Microsoft Azure 入口網站](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="e1e28-112">Sign in to the [Microsoft Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="e1e28-113">建立新的 Application Insights 資源，並將應用程式類型設定為 Java web 應用程式的。</span><span class="sxs-lookup"><span data-stu-id="e1e28-113">Create a new Application Insights resource and set the application type to Java web application.</span></span>
   
    ![填寫名稱，選擇 [Java Web 應用程式]，然後按一下 [建立]](./media/app-insights-java-live/02-create.png)

    <span data-ttu-id="e1e28-115">會在幾秒鐘內建立資源。</span><span class="sxs-lookup"><span data-stu-id="e1e28-115">The resource is created in a few seconds.</span></span>

4. <span data-ttu-id="e1e28-116">開啟新的資源，並取得其檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="e1e28-116">Open the new resource and get its instrumentation key.</span></span> <span data-ttu-id="e1e28-117">您很快需要將此金鑰貼到程式碼專案中。</span><span class="sxs-lookup"><span data-stu-id="e1e28-117">You'll need to paste this key into your code project shortly.</span></span>
   
    ![在新資源概觀中，按一下 [屬性] 並複製檢測金鑰](./media/app-insights-java-live/03-key.png)

## <a name="2-download-the-sdk"></a><span data-ttu-id="e1e28-119">2.下載 SDK</span><span class="sxs-lookup"><span data-stu-id="e1e28-119">2. Download the SDK</span></span>
1. <span data-ttu-id="e1e28-120">下載 [Application Insights SDK for Java](https://aka.ms/aijavasdk)。</span><span class="sxs-lookup"><span data-stu-id="e1e28-120">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span> 
2. <span data-ttu-id="e1e28-121">在您的伺服器上，將 SDK 內容解壓縮到載入您專案二進位檔的目錄。</span><span class="sxs-lookup"><span data-stu-id="e1e28-121">On your server, extract the SDK contents to the directory from which your project binaries are loaded.</span></span> <span data-ttu-id="e1e28-122">如果您使用 Tomcat，此目錄通常在 `webapps/<your_app_name>/WEB-INF/lib` 之下</span><span class="sxs-lookup"><span data-stu-id="e1e28-122">If you’re using Tomcat, this directory would typically be under `webapps/<your_app_name>/WEB-INF/lib`</span></span>

<span data-ttu-id="e1e28-123">請注意，您必須在每個伺服器執行個體上並針對每個應用程式重複此操作。</span><span class="sxs-lookup"><span data-stu-id="e1e28-123">Note that you need to repeat this on each server instance, and for each app.</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="e1e28-124">3.加入 Application Insights XML 檔案</span><span class="sxs-lookup"><span data-stu-id="e1e28-124">3. Add an Application Insights xml file</span></span>
<span data-ttu-id="e1e28-125">您可以在加入 SDK 的資料夾中建立 ApplicationInsights.xml。</span><span class="sxs-lookup"><span data-stu-id="e1e28-125">Create ApplicationInsights.xml in the folder in which you added the SDK.</span></span> <span data-ttu-id="e1e28-126">將下列 XML 放入上述檔案。</span><span class="sxs-lookup"><span data-stu-id="e1e28-126">Put into it the following XML.</span></span>

<span data-ttu-id="e1e28-127">替換為您從 Azure 入口網站取得的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="e1e28-127">Substitute the instrumentation key that you got from the Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- The key from the portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data to each event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* <span data-ttu-id="e1e28-128">檢測金鑰會隨著遙測的每個項目傳送，並告知 Application Insights 在您的資源中顯示它。</span><span class="sxs-lookup"><span data-stu-id="e1e28-128">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>
* <span data-ttu-id="e1e28-129">HTTP 要求元件是選用的。</span><span class="sxs-lookup"><span data-stu-id="e1e28-129">The HTTP Request component is optional.</span></span> <span data-ttu-id="e1e28-130">它會自動將要求和回應時間的遙測傳送到入口網站。</span><span class="sxs-lookup"><span data-stu-id="e1e28-130">It automatically sends telemetry about requests and response times to the portal.</span></span>
* <span data-ttu-id="e1e28-131">事件相互關聯是 HTTP 要求元件的補充。</span><span class="sxs-lookup"><span data-stu-id="e1e28-131">Events correlation is an addition to the HTTP request component.</span></span> <span data-ttu-id="e1e28-132">它會將識別碼指派給伺服器收到的每個要求，並將此識別碼加入為遙測的每個項目的屬性，作為 'Operation.Id' 屬性。</span><span class="sxs-lookup"><span data-stu-id="e1e28-132">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span></span> <span data-ttu-id="e1e28-133">它可讓您相互關聯與每個要求關聯的遙測，方法是在 [診斷搜尋](app-insights-diagnostic-search.md)中設定篩選器。</span><span class="sxs-lookup"><span data-stu-id="e1e28-133">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search](app-insights-diagnostic-search.md).</span></span>

## <a name="4-add-an-http-filter"></a><span data-ttu-id="e1e28-134">4.加入 HTTP 篩選器</span><span class="sxs-lookup"><span data-stu-id="e1e28-134">4. Add an HTTP filter</span></span>
<span data-ttu-id="e1e28-135">在專案中找到並開啟 web.xml 檔案，並合併 web-app 節點下的下列程式碼片段，在其中您可以設定應用程式篩選器。</span><span class="sxs-lookup"><span data-stu-id="e1e28-135">Locate and open the web.xml file in your project, and merge the following snippet of code under the web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="e1e28-136">為獲得最準確的結果，應該在其他所有篩選器之前先對應此篩選器。</span><span class="sxs-lookup"><span data-stu-id="e1e28-136">To get the most accurate results, the filter should be mapped before all other filters.</span></span>

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

## <a name="5-check-firewall-exceptions"></a><span data-ttu-id="e1e28-137">5.檢查防火牆例外狀況</span><span class="sxs-lookup"><span data-stu-id="e1e28-137">5. Check firewall exceptions</span></span>
<span data-ttu-id="e1e28-138">您可能需要 [設定防火牆例外狀況以傳送輸出資料](app-insights-ip-addresses.md)。</span><span class="sxs-lookup"><span data-stu-id="e1e28-138">You might need to [set exceptions to send outgoing data](app-insights-ip-addresses.md).</span></span>

## <a name="6-restart-your-web-app"></a><span data-ttu-id="e1e28-139">6.重新啟動您的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="e1e28-139">6. Restart your web app</span></span>
## <a name="7-view-your-telemetry-in-application-insights"></a><span data-ttu-id="e1e28-140">7.在 Application Insights 中檢視遙測</span><span class="sxs-lookup"><span data-stu-id="e1e28-140">7. View your telemetry in Application Insights</span></span>
<span data-ttu-id="e1e28-141">返回 [Microsoft Azure 入口網站](https://portal.azure.com)中的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="e1e28-141">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="e1e28-142">[概觀] 刀鋒視窗會顯示 HTTP 要求的相關遙測。</span><span class="sxs-lookup"><span data-stu-id="e1e28-142">Telemetry about HTTP requests appears on the overview blade.</span></span> <span data-ttu-id="e1e28-143">(如果沒有出現，請稍等片刻，然後按一下 [重新整理]。)</span><span class="sxs-lookup"><span data-stu-id="e1e28-143">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![範例資料](./media/app-insights-java-live/5-results.png)

<span data-ttu-id="e1e28-145">逐一點選任何圖表以查看更詳細的度量。</span><span class="sxs-lookup"><span data-stu-id="e1e28-145">Click through any chart to see more detailed metrics.</span></span> 

![](./media/app-insights-java-live/6-barchart.png)

<span data-ttu-id="e1e28-146">而檢視要求的屬性時，您可以查看與它關聯的遙測事件，例如要求和例外狀況。</span><span class="sxs-lookup"><span data-stu-id="e1e28-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-live/7-instance.png)

[<span data-ttu-id="e1e28-147">深入了解度量。</span><span class="sxs-lookup"><span data-stu-id="e1e28-147">Learn more about metrics.</span></span>](app-insights-metrics-explorer.md)

## <a name="next-steps"></a><span data-ttu-id="e1e28-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e1e28-148">Next steps</span></span>
* <span data-ttu-id="e1e28-149">[將遙測加入至您的網頁](app-insights-javascript.md) ，即可監視頁面檢視和使用者度量。</span><span class="sxs-lookup"><span data-stu-id="e1e28-149">[Add telemetry to your web pages](app-insights-javascript.md) to monitor page views and user metrics.</span></span>
* <span data-ttu-id="e1e28-150">[設定 Web 測試](app-insights-monitor-web-app-availability.md) ，以確認應用程式處於線上狀態且能夠回應。</span><span class="sxs-lookup"><span data-stu-id="e1e28-150">[Set up web tests](app-insights-monitor-web-app-availability.md) to make sure your application stays live and responsive.</span></span>
* [<span data-ttu-id="e1e28-151">擷取記錄追蹤</span><span class="sxs-lookup"><span data-stu-id="e1e28-151">Capture log traces</span></span>](app-insights-java-trace-logs.md)
* <span data-ttu-id="e1e28-152">[搜尋事件和記錄](app-insights-diagnostic-search.md) 以協助診斷問題。</span><span class="sxs-lookup"><span data-stu-id="e1e28-152">[Search events and logs](app-insights-diagnostic-search.md) to help diagnose problems.</span></span>

