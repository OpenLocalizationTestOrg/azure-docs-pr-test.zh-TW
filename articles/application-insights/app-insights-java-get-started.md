---
title: "使用 Azure Application Insights aaaJava web 應用程式分析 |Microsoft 文件"
description: "使用 Application Insights 針對 Java Web 應用程式進行應用程式效能監視。 "
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 051d4285-f38a-45d8-ad8a-45c3be828d91
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6555ee53a44f937350e4fa296080f7dce4f45226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a><span data-ttu-id="f702e-103">在 Java Web 專案中開始使用 Application Insights</span><span class="sxs-lookup"><span data-stu-id="f702e-103">Get started with Application Insights in a Java web project</span></span>


<span data-ttu-id="f702e-104">[Application Insights](https://azure.microsoft.com/services/application-insights/)是 web 開發人員，可協助您了解 hello 效能和使用即時應用程式的可延伸的分析服務。</span><span class="sxs-lookup"><span data-stu-id="f702e-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is an extensible analytics service for web developers that helps you understand hello performance and usage of your live application.</span></span> <span data-ttu-id="f702e-105">它也使用[偵測及診斷效能問題和例外狀況](app-insights-detect-triage-diagnose.md)，和[撰寫程式碼][ api] tootrack 哪些使用者處理您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f702e-105">Use it too[detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [write code][api] tootrack what users do with your app.</span></span>

![範例資料](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="f702e-107">Application Insights 支援 Linux、Unix 或 Windows 上執行的 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f702e-107">Application Insights supports Java apps running on Linux, Unix, or Windows.</span></span>

<span data-ttu-id="f702e-108">您需要：</span><span class="sxs-lookup"><span data-stu-id="f702e-108">You need:</span></span>

* <span data-ttu-id="f702e-109">Oracle JRE 1.6 或更新版本，或 Zulu JRE 1.6 或更新版本</span><span class="sxs-lookup"><span data-stu-id="f702e-109">Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later</span></span>
* <span data-ttu-id="f702e-110">訂用帳戶太[Microsoft Azure](https://azure.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="f702e-110">A subscription too[Microsoft Azure](https://azure.microsoft.com/).</span></span>

<span data-ttu-id="f702e-111">*如果您有已經是即時的 web 應用程式，您可能太遵循 hello 替代程序[hello web 伺服器中執行階段新增 hello SDK](app-insights-java-live.md)。其他的替代方法可避免重建 hello 程式碼，但沒有得到 hello 選項 toowrite 程式碼 tootrack 使用者活動。*</span><span class="sxs-lookup"><span data-stu-id="f702e-111">*If you have a web app that's already live, you could follow hello alternative procedure too[add hello SDK at runtime in hello web server](app-insights-java-live.md). That alternative avoids rebuilding hello code, but you don't get hello option toowrite code tootrack user activity.*</span></span>

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="f702e-112">1.取得 Application Insights 檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="f702e-112">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="f702e-113">登入 toohello [Microsoft Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f702e-113">Sign in toohello [Microsoft Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f702e-114">建立 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="f702e-114">Create an Application Insights resource.</span></span> <span data-ttu-id="f702e-115">設定 hello 應用程式類型 tooJava web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f702e-115">Set hello application type tooJava web application.</span></span>

    ![填寫名稱，選擇 [Java Web 應用程式]，然後按一下 [建立]](./media/app-insights-java-get-started/02-create.png)
3. <span data-ttu-id="f702e-117">尋找 hello hello 新資源的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="f702e-117">Find hello instrumentation key of hello new resource.</span></span> <span data-ttu-id="f702e-118">您將需要 toopaste 這個機碼到您的程式碼專案很快。</span><span class="sxs-lookup"><span data-stu-id="f702e-118">You'll need toopaste this key into your code project shortly.</span></span>

    ![在新資源概觀 hello，按一下 內容並複製 hello 檢測金鑰](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-hello-application-insights-sdk-for-java-tooyour-project"></a><span data-ttu-id="f702e-120">2.新增 hello Application Insights SDK for Java tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="f702e-120">2. Add hello Application Insights SDK for Java tooyour project</span></span>
<span data-ttu-id="f702e-121">*選擇 hello 適當的方式，為您的專案。*</span><span class="sxs-lookup"><span data-stu-id="f702e-121">*Choose hello appropriate way for your project.*</span></span>

#### <a name="if-youre-using-eclipse-toocreate-a-maven-or-dynamic-web-project-"></a><span data-ttu-id="f702e-122">如果您使用的 Eclipse toocreate Maven 或動態 Web 專案...</span><span class="sxs-lookup"><span data-stu-id="f702e-122">If you're using Eclipse toocreate a Maven or Dynamic Web project ...</span></span>
<span data-ttu-id="f702e-123">使用 hello [Application Insights SDK for Java 外掛程式][eclipse]。</span><span class="sxs-lookup"><span data-stu-id="f702e-123">Use hello [Application Insights SDK for Java plug-in][eclipse].</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="f702e-124">如果您使用 Maven...</span><span class="sxs-lookup"><span data-stu-id="f702e-124">If you're using Maven...</span></span>
<span data-ttu-id="f702e-125">如果您的專案已設定 toouse Maven 組建，合併 hello 下列程式碼 tooyour pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="f702e-125">If your project is already set up toouse Maven for build, merge hello following code tooyour pom.xml file.</span></span>

<span data-ttu-id="f702e-126">然後，重新整理 hello 專案相依性 tooget hello 二進位檔下載。</span><span class="sxs-lookup"><span data-stu-id="f702e-126">Then, refresh hello project dependencies tooget hello binaries downloaded.</span></span>

```XML

    <repositories>
       <repository>
          <id>central</id>
          <name>Central</name>
          <url>http://repo1.maven.org/maven2</url>
       </repository>
    </repositories>

    <dependencies>
      <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-web</artifactId>
        <!-- or applicationinsights-core for bare API -->
        <version>[1.0,)</version>
      </dependency>
    </dependencies>
```

* <span data-ttu-id="f702e-127">*建置或總和檢查碼驗證錯誤？*</span><span class="sxs-lookup"><span data-stu-id="f702e-127">*Build or checksum validation errors?*</span></span> <span data-ttu-id="f702e-128">嘗試使用特定版本，例如：`<version>1.0.n</version>`。</span><span class="sxs-lookup"><span data-stu-id="f702e-128">Try using a specific version, such as: `<version>1.0.n</version>`.</span></span> <span data-ttu-id="f702e-129">您可以找到 hello 最新版本中 hello [SDK 版本資訊](https://github.com/Microsoft/ApplicationInsights-Java#release-notes)或是在我們[Maven 成品](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights)。</span><span class="sxs-lookup"><span data-stu-id="f702e-129">You'll find hello latest version in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) or in our [Maven artifacts](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span></span>
* <span data-ttu-id="f702e-130">*需要 tooupdate tooa 新 SDK 嗎？*</span><span class="sxs-lookup"><span data-stu-id="f702e-130">*Need tooupdate tooa new SDK?*</span></span> <span data-ttu-id="f702e-131">請重新整理專案的相依項目。</span><span class="sxs-lookup"><span data-stu-id="f702e-131">Refresh your project's dependencies.</span></span>

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="f702e-132">如果您使用 Gradle...</span><span class="sxs-lookup"><span data-stu-id="f702e-132">If you're using Gradle...</span></span>
<span data-ttu-id="f702e-133">如果您的專案已設定 toouse Gradle 組建，合併 hello 下列程式碼 tooyour build.gradle 檔案。</span><span class="sxs-lookup"><span data-stu-id="f702e-133">If your project is already set up toouse Gradle for build, merge hello following code tooyour build.gradle file.</span></span>

<span data-ttu-id="f702e-134">然後，重新整理 hello 專案相依性 tooget hello 二進位檔下載。</span><span class="sxs-lookup"><span data-stu-id="f702e-134">Then refresh hello project dependencies tooget hello binaries downloaded.</span></span>

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* <span data-ttu-id="f702e-135">*建置或總和檢查碼驗證錯誤？嘗試使用特定版本，例如：* `version:'1.0.n'`。</span><span class="sxs-lookup"><span data-stu-id="f702e-135">*Build or checksum validation errors? Try using a specific version, such as:* `version:'1.0.n'`.</span></span> <span data-ttu-id="f702e-136">*您可以找到 hello 最新版本中 hello [SDK 版本資訊](https://github.com/Microsoft/ApplicationInsights-Java#release-notes)。*</span><span class="sxs-lookup"><span data-stu-id="f702e-136">*You'll find hello latest version in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span></span>
* <span data-ttu-id="f702e-137">*tooupdate tooa 新的 SDK*</span><span class="sxs-lookup"><span data-stu-id="f702e-137">*tooupdate tooa new SDK*</span></span>
  * <span data-ttu-id="f702e-138">請重新整理專案的相依項目。</span><span class="sxs-lookup"><span data-stu-id="f702e-138">Refresh your project's dependencies.</span></span>

#### <a name="otherwise-"></a><span data-ttu-id="f702e-139">否則...</span><span class="sxs-lookup"><span data-stu-id="f702e-139">Otherwise ...</span></span>
<span data-ttu-id="f702e-140">手動新增 hello SDK:</span><span class="sxs-lookup"><span data-stu-id="f702e-140">Manually add hello SDK:</span></span>

1. <span data-ttu-id="f702e-141">下載 hello [Application Insights SDK for Java](https://aka.ms/aijavasdk)。</span><span class="sxs-lookup"><span data-stu-id="f702e-141">Download hello [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="f702e-142">從 hello zip 檔案解壓縮 hello 二進位檔，並將它們加入 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="f702e-142">Extract hello binaries from hello zip file and add them tooyour project.</span></span>

### <a name="questions"></a><span data-ttu-id="f702e-143">問題...</span><span class="sxs-lookup"><span data-stu-id="f702e-143">Questions...</span></span>
* <span data-ttu-id="f702e-144">*Hello hello 之間的關係為何`-core`和`-web`hello zip 中的元件？*</span><span class="sxs-lookup"><span data-stu-id="f702e-144">*What's hello relationship between hello `-core` and `-web` components in hello zip?*</span></span>

  * <span data-ttu-id="f702e-145">`applicationinsights-core`提供 hello 裸機 API。</span><span class="sxs-lookup"><span data-stu-id="f702e-145">`applicationinsights-core` gives you hello bare API.</span></span> <span data-ttu-id="f702e-146">您一定需要此元件。</span><span class="sxs-lookup"><span data-stu-id="f702e-146">You always need this component.</span></span>
  * <span data-ttu-id="f702e-147">`applicationinsights-web` 提供追蹤 HTTP 要求計數和回應時間的度量。</span><span class="sxs-lookup"><span data-stu-id="f702e-147">`applicationinsights-web` gives you metrics that track HTTP request counts and response times.</span></span> <span data-ttu-id="f702e-148">如果您不想自動收集此原則，您可以忽略這個。</span><span class="sxs-lookup"><span data-stu-id="f702e-148">You can omit this component if you don't want this telemetry automatically collected.</span></span> <span data-ttu-id="f702e-149">例如，如果您想 toowrite 自己。</span><span class="sxs-lookup"><span data-stu-id="f702e-149">For example, if you want toowrite your own.</span></span>
* <span data-ttu-id="f702e-150">*tooupdate hello SDK 當我們發行變更時*</span><span class="sxs-lookup"><span data-stu-id="f702e-150">*tooupdate hello SDK when we publish changes*</span></span>

  * <span data-ttu-id="f702e-151">下載最新的 hello [Application Insights SDK for Java](https://aka.ms/qqkaq6)和 hello 舊的取代。</span><span class="sxs-lookup"><span data-stu-id="f702e-151">Download hello latest [Application Insights SDK for Java](https://aka.ms/qqkaq6) and replace hello old ones.</span></span>
  * <span data-ttu-id="f702e-152">變更詳述於 hello [SDK 版本資訊](https://github.com/Microsoft/ApplicationInsights-Java#release-notes)。</span><span class="sxs-lookup"><span data-stu-id="f702e-152">Changes are described in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="f702e-153">3.加入 Application Insights .XML 檔案</span><span class="sxs-lookup"><span data-stu-id="f702e-153">3. Add an Application Insights .xml file</span></span>
<span data-ttu-id="f702e-154">新增 ApplicationInsights.xml toohello 資源 資料夾在專案中，或請確定它加入 tooyour 專案的部署類別路徑。</span><span class="sxs-lookup"><span data-stu-id="f702e-154">Add ApplicationInsights.xml toohello resources folder in your project, or make sure it is added tooyour project’s deployment class path.</span></span> <span data-ttu-id="f702e-155">複製下列 XML 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="f702e-155">Copy hello following XML into it.</span></span>

<span data-ttu-id="f702e-156">替代 hello 所得 hello Azure 入口網站的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="f702e-156">Substitute hello instrumentation key that you got from hello Azure portal.</span></span>

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


* <span data-ttu-id="f702e-157">hello 檢測金鑰會隨每個項目的遙測資料一起傳送，並告知 Application Insights toodisplay 在您的資源。</span><span class="sxs-lookup"><span data-stu-id="f702e-157">hello instrumentation key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>
* <span data-ttu-id="f702e-158">hello HTTP 要求的元件是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="f702e-158">hello HTTP Request component is optional.</span></span> <span data-ttu-id="f702e-159">它會自動傳送有關要求和回應時間 toohello 入口網站的遙測。</span><span class="sxs-lookup"><span data-stu-id="f702e-159">It automatically sends telemetry about requests and response times toohello portal.</span></span>
* <span data-ttu-id="f702e-160">事件相互關聯是加法 toohello HTTP 要求元件。</span><span class="sxs-lookup"><span data-stu-id="f702e-160">Events correlation is an addition toohello HTTP request component.</span></span> <span data-ttu-id="f702e-161">它會指派 hello 伺服器接收到的識別項 tooeach 要求，並將此識別項的遙測資料的屬性 tooevery 項目為新增為 hello 屬性 'Operation.Id'。</span><span class="sxs-lookup"><span data-stu-id="f702e-161">It assigns an identifier tooeach request received by hello server, and adds this identifier as a property tooevery item of telemetry as hello property 'Operation.Id'.</span></span> <span data-ttu-id="f702e-162">它可讓您藉由設定的篩選條件相關聯的每個要求 toocorrelate hello 遙測[診斷搜尋][diagnostic]。</span><span class="sxs-lookup"><span data-stu-id="f702e-162">It allows you toocorrelate hello telemetry associated with each request by setting a filter in [diagnostic search][diagnostic].</span></span>
* <span data-ttu-id="f702e-163">hello Application Insights 金鑰可以動態地從傳送 hello Azure 入口網站做為系統屬性 (-DAPPLICATION_INSIGHTS_IKEY = your_ikey)。</span><span class="sxs-lookup"><span data-stu-id="f702e-163">hello Application Insights key can be passed dynamically from hello Azure portal as a system property (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span></span> <span data-ttu-id="f702e-164">如果未定義任何屬性，它會檢查 Azure App 設定中的環境變數 (APPLICATION_INSIGHTS_IKEY)。</span><span class="sxs-lookup"><span data-stu-id="f702e-164">If there is no property defined, it checks for environment variable (APPLICATION_INSIGHTS_IKEY) in Azure App Settings.</span></span> <span data-ttu-id="f702e-165">如果這兩個 hello 屬性未定義，從 ApplicationInsights.xml 使用 hello 預設 InstrumentationKey。</span><span class="sxs-lookup"><span data-stu-id="f702e-165">If both hello properties are undefined, hello default InstrumentationKey is used from ApplicationInsights.xml.</span></span> <span data-ttu-id="f702e-166">此順序可協助您 toomanage 不同環境的不同 InstrumentationKeys 動態。</span><span class="sxs-lookup"><span data-stu-id="f702e-166">This sequence helps you toomanage different InstrumentationKeys for different environments dynamically.</span></span>

### <a name="alternative-ways-tooset-hello-instrumentation-key"></a><span data-ttu-id="f702e-167">替代方式 tooset hello 檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="f702e-167">Alternative ways tooset hello instrumentation key</span></span>
<span data-ttu-id="f702e-168">Application Insights SDK 會尋找此順序中的 hello 機碼：</span><span class="sxs-lookup"><span data-stu-id="f702e-168">Application Insights SDK looks for hello key in this order:</span></span>

1. <span data-ttu-id="f702e-169">系統屬性：-DAPPLICATION_INSIGHTS_IKEY=your_ikey</span><span class="sxs-lookup"><span data-stu-id="f702e-169">System property: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span></span>
2. <span data-ttu-id="f702e-170">環境變數：APPLICATION_INSIGHTS_IKEY</span><span class="sxs-lookup"><span data-stu-id="f702e-170">Environment variable: APPLICATION_INSIGHTS_IKEY</span></span>
3. <span data-ttu-id="f702e-171">組態檔︰ApplicationInsights.xml</span><span class="sxs-lookup"><span data-stu-id="f702e-171">Configuration file: ApplicationInsights.xml</span></span>

<span data-ttu-id="f702e-172">您也可以 [在程式碼中設定](app-insights-api-custom-events-metrics.md#ikey)：</span><span class="sxs-lookup"><span data-stu-id="f702e-172">You can also [set it in code](app-insights-api-custom-events-metrics.md#ikey):</span></span>

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a><span data-ttu-id="f702e-173">4.加入 HTTP 篩選器</span><span class="sxs-lookup"><span data-stu-id="f702e-173">4. Add an HTTP filter</span></span>
<span data-ttu-id="f702e-174">最後一個組態步驟 hello 可讓 hello HTTP 要求元件 toolog 每個 web 要求。</span><span class="sxs-lookup"><span data-stu-id="f702e-174">hello last configuration step allows hello HTTP request component toolog each web request.</span></span> <span data-ttu-id="f702e-175">（不需如果您只想要 hello 裸機應用程式開發介面）。</span><span class="sxs-lookup"><span data-stu-id="f702e-175">(Not required if you just want hello bare API.)</span></span>

<span data-ttu-id="f702e-176">找出並開啟您的專案，並合併 hello 下列程式碼 hello web 應用程式 節點下，您的應用程式篩選器設定的位置中的 hello web.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="f702e-176">Locate and open hello web.xml file in your project, and merge hello following code under hello web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="f702e-177">所有其他篩選條件之前，應該要對應 tooget hello 最精確的結果，hello 篩選。</span><span class="sxs-lookup"><span data-stu-id="f702e-177">tooget hello most accurate results, hello filter should be mapped before all other filters.</span></span>

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

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a><span data-ttu-id="f702e-178">如果您使用 Spring Web MVC 3.1 或更新版本</span><span class="sxs-lookup"><span data-stu-id="f702e-178">If you're using Spring Web MVC 3.1 or later</span></span>
<span data-ttu-id="f702e-179">編輯這些項目 *-servlet.xml tooinclude hello Application Insights 套件：</span><span class="sxs-lookup"><span data-stu-id="f702e-179">Edit these elements in *-servlet.xml tooinclude hello Application Insights package:</span></span>

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a><span data-ttu-id="f702e-180">如果您使用 Struts 2</span><span class="sxs-lookup"><span data-stu-id="f702e-180">If you're using Struts 2</span></span>
<span data-ttu-id="f702e-181">加入此項目 toohello Struts 組態檔 （通常是具名的 struts.xml 或 struts default.xml）：</span><span class="sxs-lookup"><span data-stu-id="f702e-181">Add this item toohello Struts configuration file (usually named struts.xml or struts-default.xml):</span></span>

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

<span data-ttu-id="f702e-182">（如果有定義預設堆疊中的攔截器，hello 攔截器可以只被加入 toothat 堆疊）。</span><span class="sxs-lookup"><span data-stu-id="f702e-182">(If you have interceptors defined in a default stack, hello interceptor can simply be added toothat stack.)</span></span>

## <a name="5-run-your-application"></a><span data-ttu-id="f702e-183">5.執行您的應用程式</span><span class="sxs-lookup"><span data-stu-id="f702e-183">5. Run your application</span></span>
<span data-ttu-id="f702e-184">請在偵錯模式中執行您的開發電腦上或發行 tooyour 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f702e-184">Either run it in debug mode on your development machine, or publish tooyour server.</span></span>

## <a name="6-view-your-telemetry-in-application-insights"></a><span data-ttu-id="f702e-185">6.在 Application Insights 中檢視遙測</span><span class="sxs-lookup"><span data-stu-id="f702e-185">6. View your telemetry in Application Insights</span></span>
<span data-ttu-id="f702e-186">傳回在 tooyour Application Insights 資源[Microsoft Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f702e-186">Return tooyour Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="f702e-187">HTTP 要求資料會顯示 hello 概觀刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="f702e-187">HTTP requests data appears on hello overview blade.</span></span> <span data-ttu-id="f702e-188">(如果沒有出現，請稍等片刻，然後按一下重新整理。)</span><span class="sxs-lookup"><span data-stu-id="f702e-188">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![範例資料](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="f702e-190">[深入了解度量。][metrics]</span><span class="sxs-lookup"><span data-stu-id="f702e-190">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="f702e-191">按一下任何詳細的圖表 toosee 透過彙總度量資訊。</span><span class="sxs-lookup"><span data-stu-id="f702e-191">Click through any chart toosee more detailed aggregated metrics.</span></span>

![](./media/app-insights-java-get-started/6-barchart.png)

> <span data-ttu-id="f702e-192">Application Insights 假設 hello 的 MVC 應用程式的 HTTP 要求的格式為： `VERB controller/action`。</span><span class="sxs-lookup"><span data-stu-id="f702e-192">Application Insights assumes hello format of HTTP requests for MVC applications is: `VERB controller/action`.</span></span> <span data-ttu-id="f702e-193">例如，`GET Home/Product/f9anuh81`、`GET Home/Product/2dffwrf5` 和 `GET Home/Product/sdf96vws` 會分組至 `GET Home/Product`。</span><span class="sxs-lookup"><span data-stu-id="f702e-193">For example, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` and `GET Home/Product/sdf96vws` are grouped into `GET Home/Product`.</span></span> <span data-ttu-id="f702e-194">此分組方式可提供要求有意義的彙總，例如要求數量和要求的平均執行時間。</span><span class="sxs-lookup"><span data-stu-id="f702e-194">This grouping enables meaningful aggregations of requests, such as number of requests and average execution time for requests.</span></span>
>
>

### <a name="instance-data"></a><span data-ttu-id="f702e-195">執行個體資料</span><span class="sxs-lookup"><span data-stu-id="f702e-195">Instance data</span></span>
<span data-ttu-id="f702e-196">按一下瀏覽特定要求類型 toosee 個別執行個體。</span><span class="sxs-lookup"><span data-stu-id="f702e-196">Click through a specific request type toosee individual instances.</span></span>

<span data-ttu-id="f702e-197">Application Insights 中會顯示兩種類型的資料︰彙總資料 (儲存並顯示為平均值、計數和總和)；以及執行個體資料 (HTTP 要求、例外狀況、頁面檢視或自訂事件的個別報表)。</span><span class="sxs-lookup"><span data-stu-id="f702e-197">Two kinds of data are displayed in Application Insights: aggregated data, stored and displayed as averages, counts, and sums; and instance data - individual reports of HTTP requests, exceptions, page views, or custom events.</span></span>

<span data-ttu-id="f702e-198">當檢視要求的 hello 屬性，您可以看到 hello 遙測事件與它相關聯，例如要求和例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f702e-198">When viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a><span data-ttu-id="f702e-199">分析︰功能強大的查詢語言</span><span class="sxs-lookup"><span data-stu-id="f702e-199">Analytics: Powerful query language</span></span>
<span data-ttu-id="f702e-200">因為您會累積更多資料，您可以在兩個 tooaggregate 資料和 toofind 個別執行個體時執行查詢。</span><span class="sxs-lookup"><span data-stu-id="f702e-200">As you accumulate more data, you can run queries both tooaggregate data and toofind individual instances.</span></span>  <span data-ttu-id="f702e-201">[分析](app-insights-analytics.md) 是一項強大的工具，既可了解效能和使用情況，也可進行診斷。</span><span class="sxs-lookup"><span data-stu-id="f702e-201">[Analytics](app-insights-analytics.md) is a powerful tool for both for understanding performance and usage, and for diagnostic purposes.</span></span>

![分析的範例](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-hello-server"></a><span data-ttu-id="f702e-203">7.Hello 伺服器上安裝應用程式</span><span class="sxs-lookup"><span data-stu-id="f702e-203">7. Install your app on hello server</span></span>
<span data-ttu-id="f702e-204">現在來發行您的應用程式 toohello 伺服器，可讓您使用它，並留意 hello 遙測 hello 入口網站上顯示。</span><span class="sxs-lookup"><span data-stu-id="f702e-204">Now publish your app toohello server, let people use it, and watch hello telemetry show up on hello portal.</span></span>

* <span data-ttu-id="f702e-205">請確定您的防火牆允許應用程式 toosend 遙測 toothese 連接埠：</span><span class="sxs-lookup"><span data-stu-id="f702e-205">Make sure your firewall allows your application toosend telemetry toothese ports:</span></span>

  * <span data-ttu-id="f702e-206">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="f702e-206">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="f702e-207">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="f702e-207">f5.services.visualstudio.com:443</span></span>

* <span data-ttu-id="f702e-208">如果連出流量必須透過防火牆路由傳送，定義系統屬性 `http.proxyHost` 和 `http.proxyPort`。</span><span class="sxs-lookup"><span data-stu-id="f702e-208">If outgoing traffic must be routed through a firewall, define system properties `http.proxyHost` and `http.proxyPort`.</span></span>

* <span data-ttu-id="f702e-209">在 Windows 伺服器上，安裝：</span><span class="sxs-lookup"><span data-stu-id="f702e-209">On Windows servers, install:</span></span>

  * [<span data-ttu-id="f702e-210">Microsoft Visual C++ 可轉散發套件</span><span class="sxs-lookup"><span data-stu-id="f702e-210">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="f702e-211">(此元件會啟用效能計數器。)</span><span class="sxs-lookup"><span data-stu-id="f702e-211">(This component enables performance counters.)</span></span>


## <a name="exceptions-and-request-failures"></a><span data-ttu-id="f702e-212">例外狀況與要求失敗</span><span class="sxs-lookup"><span data-stu-id="f702e-212">Exceptions and request failures</span></span>
<span data-ttu-id="f702e-213">會自動收集未處理的例外狀況：</span><span class="sxs-lookup"><span data-stu-id="f702e-213">Unhandled exceptions are automatically collected:</span></span>

![開啟 [設定]、[失敗]](./media/app-insights-java-get-started/21-exceptions.png)

<span data-ttu-id="f702e-215">toocollect 資料上的其他例外狀況，您有兩個選項：</span><span class="sxs-lookup"><span data-stu-id="f702e-215">toocollect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="f702e-216">[插入程式碼中呼叫 tootrackException()][apiexceptions]。</span><span class="sxs-lookup"><span data-stu-id="f702e-216">[Insert calls tootrackException() in your code][apiexceptions].</span></span>
* <span data-ttu-id="f702e-217">[在伺服器上安裝 hello Java 代理程式](app-insights-java-agent.md)。</span><span class="sxs-lookup"><span data-stu-id="f702e-217">[Install hello Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="f702e-218">您指定您想要 toowatch hello 方法。</span><span class="sxs-lookup"><span data-stu-id="f702e-218">You specify hello methods you want toowatch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="f702e-219">監視方法呼叫和外部相依性</span><span class="sxs-lookup"><span data-stu-id="f702e-219">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="f702e-220">[安裝 hello Java 代理程式](app-insights-java-agent.md)toolog 指定內部方法與呼叫 JDBC，透過與計時資料。</span><span class="sxs-lookup"><span data-stu-id="f702e-220">[Install hello Java Agent](app-insights-java-agent.md) toolog specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="f702e-221">效能計數器</span><span class="sxs-lookup"><span data-stu-id="f702e-221">Performance counters</span></span>
<span data-ttu-id="f702e-222">開啟**設定**，**伺服器**，toosee 效能計數器的範圍。</span><span class="sxs-lookup"><span data-stu-id="f702e-222">Open **Settings**, **Servers**, toosee a range of performance counters.</span></span>

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="f702e-223">自訂效能計數器集合</span><span class="sxs-lookup"><span data-stu-id="f702e-223">Customize performance counter collection</span></span>
<span data-ttu-id="f702e-224">toodisable hello 組標準的效能計數器集合加入下列程式碼的 hello ApplicationInsights.xml 檔案 hello 根節點下的 hello:</span><span class="sxs-lookup"><span data-stu-id="f702e-224">toodisable collection of hello standard set of performance counters, add hello following code under hello root node of hello ApplicationInsights.xml file:</span></span>

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="f702e-225">收集其他效能計數器</span><span class="sxs-lookup"><span data-stu-id="f702e-225">Collect additional performance counters</span></span>
<span data-ttu-id="f702e-226">您可以指定收集其他效能計數器 toobe。</span><span class="sxs-lookup"><span data-stu-id="f702e-226">You can specify additional performance counters toobe collected.</span></span>

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a><span data-ttu-id="f702e-227">JMX 計數器 （由 hello Java 虛擬機器）</span><span class="sxs-lookup"><span data-stu-id="f702e-227">JMX counters (exposed by hello Java Virtual Machine)</span></span>

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="f702e-228">`displayName`– hello hello Application Insights 入口網站中顯示的名稱。</span><span class="sxs-lookup"><span data-stu-id="f702e-228">`displayName` – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="f702e-229">`objectName`– hello JMX 物件名稱。</span><span class="sxs-lookup"><span data-stu-id="f702e-229">`objectName` – hello JMX object name.</span></span>
* <span data-ttu-id="f702e-230">`attribute`– hello JMX 物件名稱 toofetch hello 屬性</span><span class="sxs-lookup"><span data-stu-id="f702e-230">`attribute` – hello attribute of hello JMX object name toofetch</span></span>
* <span data-ttu-id="f702e-231">`type`（選用）-hello JMX 物件屬性的型別：</span><span class="sxs-lookup"><span data-stu-id="f702e-231">`type` (optional) - hello type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="f702e-232">預設值：簡易類型，例如 int 或 long。</span><span class="sxs-lookup"><span data-stu-id="f702e-232">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="f702e-233">`composite`: hello 的效能計數器資料的格式的 'Attribute.Data' hello</span><span class="sxs-lookup"><span data-stu-id="f702e-233">`composite`: hello perf counter data is in hello format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="f702e-234">`tabular`: hello 的效能計數器資料的資料表資料列的 hello 格式</span><span class="sxs-lookup"><span data-stu-id="f702e-234">`tabular`: hello perf counter data is in hello format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="f702e-235">Windows 效能計數器</span><span class="sxs-lookup"><span data-stu-id="f702e-235">Windows performance counters</span></span>
<span data-ttu-id="f702e-236">每個[Windows 效能計數器](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx)類別目錄的成員 (在 hello 欄位是類別成員一樣)。</span><span class="sxs-lookup"><span data-stu-id="f702e-236">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in hello same way that a field is a member of a class).</span></span> <span data-ttu-id="f702e-237">類別可以是全域，或可以有一定數量或指定的執行個體。</span><span class="sxs-lookup"><span data-stu-id="f702e-237">Categories can either be global, or can have numbered or named instances.</span></span>

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="f702e-238">displayName-hello hello Application Insights 入口網站中顯示的名稱。</span><span class="sxs-lookup"><span data-stu-id="f702e-238">displayName – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="f702e-239">categoryName – hello 效能計數器分類 （效能物件） 與此效能計數器相關聯。</span><span class="sxs-lookup"><span data-stu-id="f702e-239">categoryName – hello performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="f702e-240">counterName – hello hello 效能計數器名稱。</span><span class="sxs-lookup"><span data-stu-id="f702e-240">counterName – hello name of hello performance counter.</span></span>
* <span data-ttu-id="f702e-241">instanceName – hello hello 效能計數器類別執行個體名稱或空字串 ("")，如果 hello 類別包含單一執行個體。</span><span class="sxs-lookup"><span data-stu-id="f702e-241">instanceName – hello name of hello performance counter category instance, or an empty string (""), if hello category contains a single instance.</span></span> <span data-ttu-id="f702e-242">如果 hello categoryName 是程序，而您想要 toocollect hello 效能計數器從 hello 目前 JVM 程序上執行您的應用程式中，指定`"__SELF__"`。</span><span class="sxs-lookup"><span data-stu-id="f702e-242">If hello categoryName is Process, and hello performance counter you'd like toocollect is from hello current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="f702e-243">您的效能計數器會在[計量瀏覽器][metrics]中以自訂度量的形式顯示。</span><span class="sxs-lookup"><span data-stu-id="f702e-243">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="f702e-244">Unix 效能計數器</span><span class="sxs-lookup"><span data-stu-id="f702e-244">Unix performance counters</span></span>
* <span data-ttu-id="f702e-245">[安裝與 hello Application Insights 外掛程式 collectd](app-insights-java-collectd.md) tooget 各種系統和網路的資料。</span><span class="sxs-lookup"><span data-stu-id="f702e-245">[Install collectd with hello Application Insights plugin](app-insights-java-collectd.md) tooget a wide variety of system and network data.</span></span>

## <a name="get-user-and-session-data"></a><span data-ttu-id="f702e-246">取得使用者與工作階段資料</span><span class="sxs-lookup"><span data-stu-id="f702e-246">Get user and session data</span></span>
<span data-ttu-id="f702e-247">好了，您現在正在從 Web 服務傳送遙測資料。</span><span class="sxs-lookup"><span data-stu-id="f702e-247">OK, you're sending telemetry from your web server.</span></span> <span data-ttu-id="f702e-248">現在 tooget hello 完整 360 度檢視您的應用程式，您可以加入更多監視：</span><span class="sxs-lookup"><span data-stu-id="f702e-248">Now tooget hello full 360-degree view of your application, you can add more monitoring:</span></span>

* <span data-ttu-id="f702e-249">[將遙測 tooyour web 網頁][ usage] toomonitor 頁面上，檢視和使用者度量。</span><span class="sxs-lookup"><span data-stu-id="f702e-249">[Add telemetry tooyour web pages][usage] toomonitor page views and user metrics.</span></span>
* <span data-ttu-id="f702e-250">[設定 web 測試][ availability] toomake 即時且回應迅速，保持您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f702e-250">[Set up web tests][availability] toomake sure your application stays live and responsive.</span></span>

## <a name="capture-log-traces"></a><span data-ttu-id="f702e-251">擷取記錄追蹤</span><span class="sxs-lookup"><span data-stu-id="f702e-251">Capture log traces</span></span>
<span data-ttu-id="f702e-252">您可以使用 Application Insights tooslice 並分析從 Log4J、 Logback 或其他的記錄架構的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f702e-252">You can use Application Insights tooslice and dice logs from Log4J, Logback, or other logging frameworks.</span></span> <span data-ttu-id="f702e-253">您可以將 hello 記錄相互關聯的 HTTP 要求與其他遙測。</span><span class="sxs-lookup"><span data-stu-id="f702e-253">You can correlate hello logs with HTTP requests and other telemetry.</span></span> <span data-ttu-id="f702e-254">[了解作法][javalogs]。</span><span class="sxs-lookup"><span data-stu-id="f702e-254">[Learn how][javalogs].</span></span>

## <a name="send-your-own-telemetry"></a><span data-ttu-id="f702e-255">傳送您自己的遙測</span><span class="sxs-lookup"><span data-stu-id="f702e-255">Send your own telemetry</span></span>
<span data-ttu-id="f702e-256">既然您已安裝 hello SDK，您可以使用 hello API toosend 您自己的遙測。</span><span class="sxs-lookup"><span data-stu-id="f702e-256">Now that you've installed hello SDK, you can use hello API toosend your own telemetry.</span></span>

* <span data-ttu-id="f702e-257">[追蹤的自訂事件和度量][ api] toolearn 哪些使用者運用您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f702e-257">[Track custom events and metrics][api] toolearn what users are doing with your application.</span></span>
* <span data-ttu-id="f702e-258">[搜尋事件和記錄檔][ diagnostic] toohelp 診斷問題。</span><span class="sxs-lookup"><span data-stu-id="f702e-258">[Search events and logs][diagnostic] toohelp diagnose problems.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="f702e-259">可用性 Web 測試</span><span class="sxs-lookup"><span data-stu-id="f702e-259">Availability web tests</span></span>
<span data-ttu-id="f702e-260">Application Insights 可以測試您的網站在它已啟動的定期間隔 toocheck 和回應格式。</span><span class="sxs-lookup"><span data-stu-id="f702e-260">Application Insights can test your website at regular intervals toocheck that it's up and responding well.</span></span> <span data-ttu-id="f702e-261">[向上 tooset][availability]，按一下 Web 測試。</span><span class="sxs-lookup"><span data-stu-id="f702e-261">[tooset up][availability], click Web tests.</span></span>

![按一下 [Web 測試]，然後按一下 [新增 Web 測試]](./media/app-insights-java-get-started/31-config-web-test.png)

<span data-ttu-id="f702e-263">您將取得回應時間的圖表，以及若網站關閉還會取得電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="f702e-263">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Web 測試範例](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

<span data-ttu-id="f702e-265">[深入了解 Web 測試的可用性。][availability]</span><span class="sxs-lookup"><span data-stu-id="f702e-265">[Learn more about availability web tests.][availability]</span></span>

## <a name="questions-problems"></a><span data-ttu-id="f702e-266">有疑問嗎？</span><span class="sxs-lookup"><span data-stu-id="f702e-266">Questions?</span></span> <span data-ttu-id="f702e-267">有問題嗎？</span><span class="sxs-lookup"><span data-stu-id="f702e-267">Problems?</span></span>
[<span data-ttu-id="f702e-268">疑難排解 Java</span><span class="sxs-lookup"><span data-stu-id="f702e-268">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

## <a name="video"></a><span data-ttu-id="f702e-269">影片</span><span class="sxs-lookup"><span data-stu-id="f702e-269">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="f702e-270">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f702e-270">Next steps</span></span>
* [<span data-ttu-id="f702e-271">監視相依性呼叫</span><span class="sxs-lookup"><span data-stu-id="f702e-271">Monitor dependency calls</span></span>](app-insights-java-agent.md)
* [<span data-ttu-id="f702e-272">監視 Unix 效能計數器</span><span class="sxs-lookup"><span data-stu-id="f702e-272">Monitor Unix performance counters</span></span>](app-insights-java-collectd.md)
* <span data-ttu-id="f702e-273">新增[監視 tooyour 網頁](app-insights-javascript.md)toomonitor 頁面載入時間，AJAX 呼叫瀏覽器例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f702e-273">Add [monitoring tooyour web pages](app-insights-javascript.md) toomonitor page load times, AJAX calls, browser exceptions.</span></span>
* <span data-ttu-id="f702e-274">寫入[自訂遙測](app-insights-api-custom-events-metrics.md)tootrack 使用量 hello 瀏覽器中，或是在 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f702e-274">Write [custom telemetry](app-insights-api-custom-events-metrics.md) tootrack usage in hello browser or at hello server.</span></span>
* <span data-ttu-id="f702e-275">建立[儀表板](app-insights-dashboards.md)toobring 一起 hello 重要圖表來監視您的系統。</span><span class="sxs-lookup"><span data-stu-id="f702e-275">Create [dashboards](app-insights-dashboards.md) toobring together hello key charts for monitoring your system.</span></span>
* <span data-ttu-id="f702e-276">使用[分析](app-insights-analytics.md)功能從您的應用程式透過遙測進行強大查詢</span><span class="sxs-lookup"><span data-stu-id="f702e-276">Use  [Analytics](app-insights-analytics.md) for powerful queries over telemetry from your app</span></span>
* <span data-ttu-id="f702e-277">如需詳細資訊，請瀏覽[適用於 Java 開發人員的 Azure](/java/azure)。</span><span class="sxs-lookup"><span data-stu-id="f702e-277">For more information, visit [Azure for Java developers](/java/azure).</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
