---
title: "使用 Azure Application Insights 的 Java Web 應用程式分析 | Microsoft Docs"
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
ms.openlocfilehash: a75815885d7ccd7cd56db3da2f3f92cae78fe033
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a><span data-ttu-id="e26e5-103">在 Java Web 專案中開始使用 Application Insights</span><span class="sxs-lookup"><span data-stu-id="e26e5-103">Get started with Application Insights in a Java web project</span></span>


<span data-ttu-id="e26e5-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) 是一項 Web 開發人員可延伸的分析服務，可幫助您了解即時應用程式的效能和使用情形。</span><span class="sxs-lookup"><span data-stu-id="e26e5-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is an extensible analytics service for web developers that helps you understand the performance and usage of your live application.</span></span> <span data-ttu-id="e26e5-105">使用它可[偵測及診斷效能問題和例外狀況](app-insights-detect-triage-diagnose.md)，以及[撰寫程式碼][api]來追蹤使用者對應用程式執行的動作。</span><span class="sxs-lookup"><span data-stu-id="e26e5-105">Use it to [detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [write code][api] to track what users do with your app.</span></span>

![範例資料](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="e26e5-107">Application Insights 支援 Linux、Unix 或 Windows 上執行的 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e26e5-107">Application Insights supports Java apps running on Linux, Unix, or Windows.</span></span>

<span data-ttu-id="e26e5-108">您需要：</span><span class="sxs-lookup"><span data-stu-id="e26e5-108">You need:</span></span>

* <span data-ttu-id="e26e5-109">Oracle JRE 1.6 或更新版本，或 Zulu JRE 1.6 或更新版本</span><span class="sxs-lookup"><span data-stu-id="e26e5-109">Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later</span></span>
* <span data-ttu-id="e26e5-110">[Microsoft Azure](https://azure.microsoft.com/)訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e26e5-110">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span></span>

<span data-ttu-id="e26e5-111">如果您有使用中的 Web 應用程式，您可以依照替代的程序[在執行階段於 Web 伺服器中新增 SDK ](app-insights-java-live.md)。替代方法可避免重建程式碼，但您沒有選項可撰寫程式碼來追蹤使用者活動。</span><span class="sxs-lookup"><span data-stu-id="e26e5-111">*If you have a web app that's already live, you could follow the alternative procedure to [add the SDK at runtime in the web server](app-insights-java-live.md). That alternative avoids rebuilding the code, but you don't get the option to write code to track user activity.*</span></span>

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="e26e5-112">1.取得 Application Insights 檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="e26e5-112">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="e26e5-113">登入 [Microsoft Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="e26e5-113">Sign in to the [Microsoft Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e26e5-114">建立 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="e26e5-114">Create an Application Insights resource.</span></span> <span data-ttu-id="e26e5-115">將應用程式類型設定為 Java Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e26e5-115">Set the application type to Java web application.</span></span>

    ![填寫名稱，選擇 [Java Web 應用程式]，然後按一下 [建立]](./media/app-insights-java-get-started/02-create.png)
3. <span data-ttu-id="e26e5-117">尋找新資源的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="e26e5-117">Find the instrumentation key of the new resource.</span></span> <span data-ttu-id="e26e5-118">您很快需要將此金鑰貼到程式碼專案中。</span><span class="sxs-lookup"><span data-stu-id="e26e5-118">You'll need to paste this key into your code project shortly.</span></span>

    ![在新資源概觀中，按一下 [屬性] 並複製檢測金鑰](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-the-application-insights-sdk-for-java-to-your-project"></a><span data-ttu-id="e26e5-120">2.將 Java 適用的 Application Insights SDK 加入至專案</span><span class="sxs-lookup"><span data-stu-id="e26e5-120">2. Add the Application Insights SDK for Java to your project</span></span>
<span data-ttu-id="e26e5-121">*選擇適合您的專案的方式。*</span><span class="sxs-lookup"><span data-stu-id="e26e5-121">*Choose the appropriate way for your project.*</span></span>

#### <a name="if-youre-using-eclipse-to-create-a-maven-or-dynamic-web-project-"></a><span data-ttu-id="e26e5-122">如果您使用 Eclipse 建立 Maven 或動態 Web 專案...</span><span class="sxs-lookup"><span data-stu-id="e26e5-122">If you're using Eclipse to create a Maven or Dynamic Web project ...</span></span>
<span data-ttu-id="e26e5-123">使用 [Java 適用的 Application Insights SDK 外掛程式][eclipse]。</span><span class="sxs-lookup"><span data-stu-id="e26e5-123">Use the [Application Insights SDK for Java plug-in][eclipse].</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="e26e5-124">如果您使用 Maven...</span><span class="sxs-lookup"><span data-stu-id="e26e5-124">If you're using Maven...</span></span>
<span data-ttu-id="e26e5-125">如果您的專案已設定為使用 Maven 來建置，請將下列程式碼合併至 pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="e26e5-125">If your project is already set up to use Maven for build, merge the following code to your pom.xml file.</span></span>

<span data-ttu-id="e26e5-126">然後重新整理專案相依性，以下載程式庫。</span><span class="sxs-lookup"><span data-stu-id="e26e5-126">Then, refresh the project dependencies to get the binaries downloaded.</span></span>

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

* <span data-ttu-id="e26e5-127">*建置或總和檢查碼驗證錯誤？*</span><span class="sxs-lookup"><span data-stu-id="e26e5-127">*Build or checksum validation errors?*</span></span> <span data-ttu-id="e26e5-128">嘗試使用特定版本，例如：`<version>1.0.n</version>`。</span><span class="sxs-lookup"><span data-stu-id="e26e5-128">Try using a specific version, such as: `<version>1.0.n</version>`.</span></span> <span data-ttu-id="e26e5-129">您可以在 [SDK 版本資訊](https://github.com/Microsoft/ApplicationInsights-Java#release-notes)或 [Maven 成品](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights)中找到最新版本。</span><span class="sxs-lookup"><span data-stu-id="e26e5-129">You'll find the latest version in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) or in our [Maven artifacts](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span></span>
* <span data-ttu-id="e26e5-130">*需要更新為新的 SDK？*</span><span class="sxs-lookup"><span data-stu-id="e26e5-130">*Need to update to a new SDK?*</span></span> <span data-ttu-id="e26e5-131">請重新整理專案的相依項目。</span><span class="sxs-lookup"><span data-stu-id="e26e5-131">Refresh your project's dependencies.</span></span>

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="e26e5-132">如果您使用 Gradle...</span><span class="sxs-lookup"><span data-stu-id="e26e5-132">If you're using Gradle...</span></span>
<span data-ttu-id="e26e5-133">如果您的專案已設定為要使用 Gradle 建置，請將下列程式碼合併至 build.gradle 檔案。</span><span class="sxs-lookup"><span data-stu-id="e26e5-133">If your project is already set up to use Gradle for build, merge the following code to your build.gradle file.</span></span>

<span data-ttu-id="e26e5-134">然後重新整理專案相依性，以下載程式庫。</span><span class="sxs-lookup"><span data-stu-id="e26e5-134">Then refresh the project dependencies to get the binaries downloaded.</span></span>

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* <span data-ttu-id="e26e5-135">*建置或總和檢查碼驗證錯誤？嘗試使用特定版本，例如：* `version:'1.0.n'`。</span><span class="sxs-lookup"><span data-stu-id="e26e5-135">*Build or checksum validation errors? Try using a specific version, such as:* `version:'1.0.n'`.</span></span> <span data-ttu-id="e26e5-136">您可以在 [SDK 版本資訊](https://github.com/Microsoft/ApplicationInsights-Java#release-notes)。</span><span class="sxs-lookup"><span data-stu-id="e26e5-136">*You'll find the latest version in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span></span>
* <span data-ttu-id="e26e5-137">*更新為新版 SDK*</span><span class="sxs-lookup"><span data-stu-id="e26e5-137">*To update to a new SDK*</span></span>
  * <span data-ttu-id="e26e5-138">請重新整理專案的相依項目。</span><span class="sxs-lookup"><span data-stu-id="e26e5-138">Refresh your project's dependencies.</span></span>

#### <a name="otherwise-"></a><span data-ttu-id="e26e5-139">否則...</span><span class="sxs-lookup"><span data-stu-id="e26e5-139">Otherwise ...</span></span>
<span data-ttu-id="e26e5-140">手動加入 SDK：</span><span class="sxs-lookup"><span data-stu-id="e26e5-140">Manually add the SDK:</span></span>

1. <span data-ttu-id="e26e5-141">下載 [Application Insights SDK for Java](https://aka.ms/aijavasdk)。</span><span class="sxs-lookup"><span data-stu-id="e26e5-141">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="e26e5-142">從 ZIP 檔案解壓縮二進位檔案，然後加入您的專案。</span><span class="sxs-lookup"><span data-stu-id="e26e5-142">Extract the binaries from the zip file and add them to your project.</span></span>

### <a name="questions"></a><span data-ttu-id="e26e5-143">問題...</span><span class="sxs-lookup"><span data-stu-id="e26e5-143">Questions...</span></span>
* <span data-ttu-id="e26e5-144">ZIP 中的 `-core` 和 `-web` 元件之間有何關係？</span><span class="sxs-lookup"><span data-stu-id="e26e5-144">*What's the relationship between the `-core` and `-web` components in the zip?*</span></span>

  * <span data-ttu-id="e26e5-145">`applicationinsights-core` 會提供裸機 API。</span><span class="sxs-lookup"><span data-stu-id="e26e5-145">`applicationinsights-core` gives you the bare API.</span></span> <span data-ttu-id="e26e5-146">您一定需要此元件。</span><span class="sxs-lookup"><span data-stu-id="e26e5-146">You always need this component.</span></span>
  * <span data-ttu-id="e26e5-147">`applicationinsights-web` 提供追蹤 HTTP 要求計數和回應時間的度量。</span><span class="sxs-lookup"><span data-stu-id="e26e5-147">`applicationinsights-web` gives you metrics that track HTTP request counts and response times.</span></span> <span data-ttu-id="e26e5-148">如果您不想自動收集此原則，您可以忽略這個。</span><span class="sxs-lookup"><span data-stu-id="e26e5-148">You can omit this component if you don't want this telemetry automatically collected.</span></span> <span data-ttu-id="e26e5-149">例如，如果您想要自己撰寫。</span><span class="sxs-lookup"><span data-stu-id="e26e5-149">For example, if you want to write your own.</span></span>
* <span data-ttu-id="e26e5-150">*在我們發佈變更時更新 SDK*</span><span class="sxs-lookup"><span data-stu-id="e26e5-150">*To update the SDK when we publish changes*</span></span>

  * <span data-ttu-id="e26e5-151">下載最新的 [Application Insights SDK for Java](https://aka.ms/qqkaq6) 並取代舊的。</span><span class="sxs-lookup"><span data-stu-id="e26e5-151">Download the latest [Application Insights SDK for Java](https://aka.ms/qqkaq6) and replace the old ones.</span></span>
  * <span data-ttu-id="e26e5-152">[SDK 版本資訊](https://github.com/Microsoft/ApplicationInsights-Java#release-notes)中會說明變更內容。</span><span class="sxs-lookup"><span data-stu-id="e26e5-152">Changes are described in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="e26e5-153">3.加入 Application Insights .XML 檔案</span><span class="sxs-lookup"><span data-stu-id="e26e5-153">3. Add an Application Insights .xml file</span></span>
<span data-ttu-id="e26e5-154">在專案中的資源資料夾中加入 ApplicationInsights.xml，或確定已將其加入專案部署類別路徑。</span><span class="sxs-lookup"><span data-stu-id="e26e5-154">Add ApplicationInsights.xml to the resources folder in your project, or make sure it is added to your project’s deployment class path.</span></span> <span data-ttu-id="e26e5-155">將下列 XML 複製到其中。</span><span class="sxs-lookup"><span data-stu-id="e26e5-155">Copy the following XML into it.</span></span>

<span data-ttu-id="e26e5-156">替換為您從 Azure 入口網站取得的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="e26e5-156">Substitute the instrumentation key that you got from the Azure portal.</span></span>

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


* <span data-ttu-id="e26e5-157">檢測金鑰會隨著遙測的每個項目傳送，並告知 Application Insights 在您的資源中顯示它。</span><span class="sxs-lookup"><span data-stu-id="e26e5-157">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>
* <span data-ttu-id="e26e5-158">HTTP 要求元件是選用的。</span><span class="sxs-lookup"><span data-stu-id="e26e5-158">The HTTP Request component is optional.</span></span> <span data-ttu-id="e26e5-159">它會自動將要求和回應時間的遙測傳送到入口網站。</span><span class="sxs-lookup"><span data-stu-id="e26e5-159">It automatically sends telemetry about requests and response times to the portal.</span></span>
* <span data-ttu-id="e26e5-160">事件相互關聯是 HTTP 要求元件的補充。</span><span class="sxs-lookup"><span data-stu-id="e26e5-160">Events correlation is an addition to the HTTP request component.</span></span> <span data-ttu-id="e26e5-161">它會將識別碼指派給伺服器收到的每個要求，並將此識別碼加入為遙測的每個項目的屬性，作為 'Operation.Id' 屬性。</span><span class="sxs-lookup"><span data-stu-id="e26e5-161">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span></span> <span data-ttu-id="e26e5-162">它可讓您相互關聯與每個要求關聯的遙測，方法是在[診斷搜尋][diagnostic]中設定篩選器。</span><span class="sxs-lookup"><span data-stu-id="e26e5-162">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search][diagnostic].</span></span>
* <span data-ttu-id="e26e5-163">可以從 Azure 入口網站以動態方式將 Application Insights 金鑰當作系統屬性傳遞 (-DAPPLICATION_INSIGHTS_IKEY=your_ikey)。</span><span class="sxs-lookup"><span data-stu-id="e26e5-163">The Application Insights key can be passed dynamically from the Azure portal as a system property (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span></span> <span data-ttu-id="e26e5-164">如果未定義任何屬性，它會檢查 Azure App 設定中的環境變數 (APPLICATION_INSIGHTS_IKEY)。</span><span class="sxs-lookup"><span data-stu-id="e26e5-164">If there is no property defined, it checks for environment variable (APPLICATION_INSIGHTS_IKEY) in Azure App Settings.</span></span> <span data-ttu-id="e26e5-165">如果未定義這兩個屬性，則會使用 ApplicationInsights.xml 中的預設 InstrumentationKey。</span><span class="sxs-lookup"><span data-stu-id="e26e5-165">If both the properties are undefined, the default InstrumentationKey is used from ApplicationInsights.xml.</span></span> <span data-ttu-id="e26e5-166">此序列有助於動態管理不同環境的不同 InstrumentationKey。</span><span class="sxs-lookup"><span data-stu-id="e26e5-166">This sequence helps you to manage different InstrumentationKeys for different environments dynamically.</span></span>

### <a name="alternative-ways-to-set-the-instrumentation-key"></a><span data-ttu-id="e26e5-167">設定檢測金鑰的替代方法</span><span class="sxs-lookup"><span data-stu-id="e26e5-167">Alternative ways to set the instrumentation key</span></span>
<span data-ttu-id="e26e5-168">Application Insights SDK 會依此順序尋找此金鑰︰</span><span class="sxs-lookup"><span data-stu-id="e26e5-168">Application Insights SDK looks for the key in this order:</span></span>

1. <span data-ttu-id="e26e5-169">系統屬性：-DAPPLICATION_INSIGHTS_IKEY=your_ikey</span><span class="sxs-lookup"><span data-stu-id="e26e5-169">System property: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span></span>
2. <span data-ttu-id="e26e5-170">環境變數：APPLICATION_INSIGHTS_IKEY</span><span class="sxs-lookup"><span data-stu-id="e26e5-170">Environment variable: APPLICATION_INSIGHTS_IKEY</span></span>
3. <span data-ttu-id="e26e5-171">組態檔︰ApplicationInsights.xml</span><span class="sxs-lookup"><span data-stu-id="e26e5-171">Configuration file: ApplicationInsights.xml</span></span>

<span data-ttu-id="e26e5-172">您也可以 [在程式碼中設定](app-insights-api-custom-events-metrics.md#ikey)：</span><span class="sxs-lookup"><span data-stu-id="e26e5-172">You can also [set it in code](app-insights-api-custom-events-metrics.md#ikey):</span></span>

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a><span data-ttu-id="e26e5-173">4.加入 HTTP 篩選器</span><span class="sxs-lookup"><span data-stu-id="e26e5-173">4. Add an HTTP filter</span></span>
<span data-ttu-id="e26e5-174">上一個組態步驟可讓 HTTP 要求元件記錄每個 Web 要求。</span><span class="sxs-lookup"><span data-stu-id="e26e5-174">The last configuration step allows the HTTP request component to log each web request.</span></span> <span data-ttu-id="e26e5-175">(如果您只需要單純的 API，則非必要。)</span><span class="sxs-lookup"><span data-stu-id="e26e5-175">(Not required if you just want the bare API.)</span></span>

<span data-ttu-id="e26e5-176">在您的專案中找到並開啟 web.xml 檔案，然後將下列程式碼合併至 Web 應用程式節點下，也就是應用程式篩選器設定的位置。</span><span class="sxs-lookup"><span data-stu-id="e26e5-176">Locate and open the web.xml file in your project, and merge the following code under the web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="e26e5-177">為獲得最準確的結果，應該在其他所有篩選器之前先對應此篩選器。</span><span class="sxs-lookup"><span data-stu-id="e26e5-177">To get the most accurate results, the filter should be mapped before all other filters.</span></span>

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

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a><span data-ttu-id="e26e5-178">如果您使用 Spring Web MVC 3.1 或更新版本</span><span class="sxs-lookup"><span data-stu-id="e26e5-178">If you're using Spring Web MVC 3.1 or later</span></span>
<span data-ttu-id="e26e5-179">在 *-servlet.xml 中編輯這些元素來併入 Application Insights 封裝：</span><span class="sxs-lookup"><span data-stu-id="e26e5-179">Edit these elements in *-servlet.xml to include the Application Insights package:</span></span>

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a><span data-ttu-id="e26e5-180">如果您使用 Struts 2</span><span class="sxs-lookup"><span data-stu-id="e26e5-180">If you're using Struts 2</span></span>
<span data-ttu-id="e26e5-181">將此項目加入到 Struts 組態檔案 (通常名稱為 struts.xml 或 struts-default.xml)：</span><span class="sxs-lookup"><span data-stu-id="e26e5-181">Add this item to the Struts configuration file (usually named struts.xml or struts-default.xml):</span></span>

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

<span data-ttu-id="e26e5-182">(如果預設堆疊中定義了攔截器，可以將攔截器加入該堆疊。)</span><span class="sxs-lookup"><span data-stu-id="e26e5-182">(If you have interceptors defined in a default stack, the interceptor can simply be added to that stack.)</span></span>

## <a name="5-run-your-application"></a><span data-ttu-id="e26e5-183">5.執行您的應用程式</span><span class="sxs-lookup"><span data-stu-id="e26e5-183">5. Run your application</span></span>
<span data-ttu-id="e26e5-184">在您的開發電腦上以偵錯模式執行應用程式，或發佈至您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="e26e5-184">Either run it in debug mode on your development machine, or publish to your server.</span></span>

## <a name="6-view-your-telemetry-in-application-insights"></a><span data-ttu-id="e26e5-185">6.在 Application Insights 中檢視遙測</span><span class="sxs-lookup"><span data-stu-id="e26e5-185">6. View your telemetry in Application Insights</span></span>
<span data-ttu-id="e26e5-186">返回 [Microsoft Azure 入口網站](https://portal.azure.com)中的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="e26e5-186">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="e26e5-187">[概觀] 刀鋒視窗上會顯示 HTTP 要求資料。</span><span class="sxs-lookup"><span data-stu-id="e26e5-187">HTTP requests data appears on the overview blade.</span></span> <span data-ttu-id="e26e5-188">(如果沒有出現，請稍等片刻，然後按一下 [重新整理]。)</span><span class="sxs-lookup"><span data-stu-id="e26e5-188">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![範例資料](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="e26e5-190">[深入了解度量。][metrics]</span><span class="sxs-lookup"><span data-stu-id="e26e5-190">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="e26e5-191">按一下任何圖表以查看詳細彙總度量。</span><span class="sxs-lookup"><span data-stu-id="e26e5-191">Click through any chart to see more detailed aggregated metrics.</span></span>

![](./media/app-insights-java-get-started/6-barchart.png)

> <span data-ttu-id="e26e5-192">Application Insights 假設 MVC 應用程式的 HTTP 要求的格式為： `VERB controller/action`。</span><span class="sxs-lookup"><span data-stu-id="e26e5-192">Application Insights assumes the format of HTTP requests for MVC applications is: `VERB controller/action`.</span></span> <span data-ttu-id="e26e5-193">例如，`GET Home/Product/f9anuh81`、`GET Home/Product/2dffwrf5` 和 `GET Home/Product/sdf96vws` 會分組至 `GET Home/Product`。</span><span class="sxs-lookup"><span data-stu-id="e26e5-193">For example, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` and `GET Home/Product/sdf96vws` are grouped into `GET Home/Product`.</span></span> <span data-ttu-id="e26e5-194">此分組方式可提供要求有意義的彙總，例如要求數量和要求的平均執行時間。</span><span class="sxs-lookup"><span data-stu-id="e26e5-194">This grouping enables meaningful aggregations of requests, such as number of requests and average execution time for requests.</span></span>
>
>

### <a name="instance-data"></a><span data-ttu-id="e26e5-195">執行個體資料</span><span class="sxs-lookup"><span data-stu-id="e26e5-195">Instance data</span></span>
<span data-ttu-id="e26e5-196">點選特定要求類型以查看個別執行個體。</span><span class="sxs-lookup"><span data-stu-id="e26e5-196">Click through a specific request type to see individual instances.</span></span>

<span data-ttu-id="e26e5-197">Application Insights 中會顯示兩種類型的資料︰彙總資料 (儲存並顯示為平均值、計數和總和)；以及執行個體資料 (HTTP 要求、例外狀況、頁面檢視或自訂事件的個別報表)。</span><span class="sxs-lookup"><span data-stu-id="e26e5-197">Two kinds of data are displayed in Application Insights: aggregated data, stored and displayed as averages, counts, and sums; and instance data - individual reports of HTTP requests, exceptions, page views, or custom events.</span></span>

<span data-ttu-id="e26e5-198">檢視要求的屬性時，您可以查看與它關聯的遙測事件，例如要求和例外狀況。</span><span class="sxs-lookup"><span data-stu-id="e26e5-198">When viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a><span data-ttu-id="e26e5-199">分析︰功能強大的查詢語言</span><span class="sxs-lookup"><span data-stu-id="e26e5-199">Analytics: Powerful query language</span></span>
<span data-ttu-id="e26e5-200">當您累積更多資料時，您就可以執行查詢以彙總資料並找出個別執行個體。</span><span class="sxs-lookup"><span data-stu-id="e26e5-200">As you accumulate more data, you can run queries both to aggregate data and to find individual instances.</span></span>  <span data-ttu-id="e26e5-201">[分析](app-insights-analytics.md) 是一項強大的工具，既可了解效能和使用情況，也可進行診斷。</span><span class="sxs-lookup"><span data-stu-id="e26e5-201">[Analytics](app-insights-analytics.md) is a powerful tool for both for understanding performance and usage, and for diagnostic purposes.</span></span>

![分析的範例](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-the-server"></a><span data-ttu-id="e26e5-203">7.在伺服器上安裝您的 App</span><span class="sxs-lookup"><span data-stu-id="e26e5-203">7. Install your app on the server</span></span>
<span data-ttu-id="e26e5-204">現在將您的應用程式發佈至伺服器供人使用，然後查看入口網站顯示的遙測。</span><span class="sxs-lookup"><span data-stu-id="e26e5-204">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span></span>

* <span data-ttu-id="e26e5-205">請確定您的防火牆允許應用程式將遙測傳送至這些連接埠：</span><span class="sxs-lookup"><span data-stu-id="e26e5-205">Make sure your firewall allows your application to send telemetry to these ports:</span></span>

  * <span data-ttu-id="e26e5-206">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="e26e5-206">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="e26e5-207">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="e26e5-207">f5.services.visualstudio.com:443</span></span>

* <span data-ttu-id="e26e5-208">如果連出流量必須透過防火牆路由傳送，定義系統屬性 `http.proxyHost` 和 `http.proxyPort`。</span><span class="sxs-lookup"><span data-stu-id="e26e5-208">If outgoing traffic must be routed through a firewall, define system properties `http.proxyHost` and `http.proxyPort`.</span></span>

* <span data-ttu-id="e26e5-209">在 Windows 伺服器上，安裝：</span><span class="sxs-lookup"><span data-stu-id="e26e5-209">On Windows servers, install:</span></span>

  * [<span data-ttu-id="e26e5-210">Microsoft Visual C++ 可轉散發套件</span><span class="sxs-lookup"><span data-stu-id="e26e5-210">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="e26e5-211">(此元件會啟用效能計數器。)</span><span class="sxs-lookup"><span data-stu-id="e26e5-211">(This component enables performance counters.)</span></span>


## <a name="exceptions-and-request-failures"></a><span data-ttu-id="e26e5-212">例外狀況與要求失敗</span><span class="sxs-lookup"><span data-stu-id="e26e5-212">Exceptions and request failures</span></span>
<span data-ttu-id="e26e5-213">會自動收集未處理的例外狀況：</span><span class="sxs-lookup"><span data-stu-id="e26e5-213">Unhandled exceptions are automatically collected:</span></span>

![開啟 [設定]、[失敗]](./media/app-insights-java-get-started/21-exceptions.png)

<span data-ttu-id="e26e5-215">若要收集其他例外狀況的資料，您有兩個選項：</span><span class="sxs-lookup"><span data-stu-id="e26e5-215">To collect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="e26e5-216">[在您的程式碼中插入 trackException() 的呼叫][apiexceptions]。</span><span class="sxs-lookup"><span data-stu-id="e26e5-216">[Insert calls to trackException() in your code][apiexceptions].</span></span>
* <span data-ttu-id="e26e5-217">[在伺服器上安裝 Java 代理程式](app-insights-java-agent.md)。</span><span class="sxs-lookup"><span data-stu-id="e26e5-217">[Install the Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="e26e5-218">指定您想要觀看的方法。</span><span class="sxs-lookup"><span data-stu-id="e26e5-218">You specify the methods you want to watch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="e26e5-219">監視方法呼叫和外部相依性</span><span class="sxs-lookup"><span data-stu-id="e26e5-219">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="e26e5-220">[安裝 Java 代理程式](app-insights-java-agent.md) 以記錄指定的內部方法和透過 JDBC 發出的呼叫與計時資料。</span><span class="sxs-lookup"><span data-stu-id="e26e5-220">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="e26e5-221">效能計數器</span><span class="sxs-lookup"><span data-stu-id="e26e5-221">Performance counters</span></span>
<span data-ttu-id="e26e5-222">開啟 [設定]、[伺服器]，可看到一些效能計數器。</span><span class="sxs-lookup"><span data-stu-id="e26e5-222">Open **Settings**, **Servers**, to see a range of performance counters.</span></span>

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="e26e5-223">自訂效能計數器集合</span><span class="sxs-lookup"><span data-stu-id="e26e5-223">Customize performance counter collection</span></span>
<span data-ttu-id="e26e5-224">若要停用效能計數器的一組標準集合，請將下列程式碼加入 ApplicationInsights.xml 檔案的根節點下：</span><span class="sxs-lookup"><span data-stu-id="e26e5-224">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span></span>

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="e26e5-225">收集其他效能計數器</span><span class="sxs-lookup"><span data-stu-id="e26e5-225">Collect additional performance counters</span></span>
<span data-ttu-id="e26e5-226">您可以指定要收集的其他效能計數器。</span><span class="sxs-lookup"><span data-stu-id="e26e5-226">You can specify additional performance counters to be collected.</span></span>

#### <a name="jmx-counters-exposed-by-the-java-virtual-machine"></a><span data-ttu-id="e26e5-227">JMX 計數器 (由虛擬機器公開)</span><span class="sxs-lookup"><span data-stu-id="e26e5-227">JMX counters (exposed by the Java Virtual Machine)</span></span>

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="e26e5-228">`displayName` – Application Insights 入口網站中顯示的名稱。</span><span class="sxs-lookup"><span data-stu-id="e26e5-228">`displayName` – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="e26e5-229">`objectName` – JMX 物件名稱。</span><span class="sxs-lookup"><span data-stu-id="e26e5-229">`objectName` – The JMX object name.</span></span>
* <span data-ttu-id="e26e5-230">`attribute` – 要提取的 JMX 物件名稱的屬性</span><span class="sxs-lookup"><span data-stu-id="e26e5-230">`attribute` – The attribute of the JMX object name to fetch</span></span>
* <span data-ttu-id="e26e5-231">`type` (選用) - JMX 物件屬性的類型：</span><span class="sxs-lookup"><span data-stu-id="e26e5-231">`type` (optional) - The type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="e26e5-232">預設值：簡易類型，例如 int 或 long。</span><span class="sxs-lookup"><span data-stu-id="e26e5-232">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="e26e5-233">`composite`：效能計數器資料的格式為 'Attribute.Data'</span><span class="sxs-lookup"><span data-stu-id="e26e5-233">`composite`: the perf counter data is in the format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="e26e5-234">`tabular`：效能計數器資料的格式為資料表列</span><span class="sxs-lookup"><span data-stu-id="e26e5-234">`tabular`: the perf counter data is in the format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="e26e5-235">Windows 效能計數器</span><span class="sxs-lookup"><span data-stu-id="e26e5-235">Windows performance counters</span></span>
<span data-ttu-id="e26e5-236">每個 [Windows 效能計數器](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) 是類別的成員 (以欄位是類別成員的相同方式)。</span><span class="sxs-lookup"><span data-stu-id="e26e5-236">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span></span> <span data-ttu-id="e26e5-237">類別可以是全域，或可以有一定數量或指定的執行個體。</span><span class="sxs-lookup"><span data-stu-id="e26e5-237">Categories can either be global, or can have numbered or named instances.</span></span>

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="e26e5-238">displayName – Application Insights 入口網站中顯示的名稱。</span><span class="sxs-lookup"><span data-stu-id="e26e5-238">displayName – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="e26e5-239">categoryName – 與此效能計數器有關聯的效能計數器類別 (效能物件)。</span><span class="sxs-lookup"><span data-stu-id="e26e5-239">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="e26e5-240">counterName – 效能計數器的名稱。</span><span class="sxs-lookup"><span data-stu-id="e26e5-240">counterName – The name of the performance counter.</span></span>
* <span data-ttu-id="e26e5-241">instanceName – 效能計數器類別執行個體的名稱，或如果類別包含單一執行個體，則為空白字串 ("")。</span><span class="sxs-lookup"><span data-stu-id="e26e5-241">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span></span> <span data-ttu-id="e26e5-242">如果 categoryName 為 Process，而您要收集的效能計數器來自應用程式執行所在的目前 JVM 處理程序，請指定 `"__SELF__"`。</span><span class="sxs-lookup"><span data-stu-id="e26e5-242">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="e26e5-243">您的效能計數器會在[計量瀏覽器][metrics]中以自訂度量的形式顯示。</span><span class="sxs-lookup"><span data-stu-id="e26e5-243">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="e26e5-244">Unix 效能計數器</span><span class="sxs-lookup"><span data-stu-id="e26e5-244">Unix performance counters</span></span>
* <span data-ttu-id="e26e5-245">[使用 Application Insights 外掛程式安裝 collectd](app-insights-java-collectd.md) ，來取得各種不同的系統和網路資料。</span><span class="sxs-lookup"><span data-stu-id="e26e5-245">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span></span>

## <a name="get-user-and-session-data"></a><span data-ttu-id="e26e5-246">取得使用者與工作階段資料</span><span class="sxs-lookup"><span data-stu-id="e26e5-246">Get user and session data</span></span>
<span data-ttu-id="e26e5-247">好了，您現在正在從 Web 服務傳送遙測資料。</span><span class="sxs-lookup"><span data-stu-id="e26e5-247">OK, you're sending telemetry from your web server.</span></span> <span data-ttu-id="e26e5-248">現在若要取得應用程式的完整 360 度檢視，可以加入多個監視：</span><span class="sxs-lookup"><span data-stu-id="e26e5-248">Now to get the full 360-degree view of your application, you can add more monitoring:</span></span>

* <span data-ttu-id="e26e5-249">[將遙測加入至您的網頁][usage]，即可監視頁面檢視和使用者度量。</span><span class="sxs-lookup"><span data-stu-id="e26e5-249">[Add telemetry to your web pages][usage] to monitor page views and user metrics.</span></span>
* <span data-ttu-id="e26e5-250">[設定 Web 測試][availability]，以確認應用程式處於線上狀態且能夠回應。</span><span class="sxs-lookup"><span data-stu-id="e26e5-250">[Set up web tests][availability] to make sure your application stays live and responsive.</span></span>

## <a name="capture-log-traces"></a><span data-ttu-id="e26e5-251">擷取記錄追蹤</span><span class="sxs-lookup"><span data-stu-id="e26e5-251">Capture log traces</span></span>
<span data-ttu-id="e26e5-252">您可以使用 Application Insights 將來自 Log4J、Logback 或其他記錄架構的記錄分解。</span><span class="sxs-lookup"><span data-stu-id="e26e5-252">You can use Application Insights to slice and dice logs from Log4J, Logback, or other logging frameworks.</span></span> <span data-ttu-id="e26e5-253">您可以將記錄與 HTTP 要求和其他遙測相互關聯。</span><span class="sxs-lookup"><span data-stu-id="e26e5-253">You can correlate the logs with HTTP requests and other telemetry.</span></span> <span data-ttu-id="e26e5-254">[了解作法][javalogs]。</span><span class="sxs-lookup"><span data-stu-id="e26e5-254">[Learn how][javalogs].</span></span>

## <a name="send-your-own-telemetry"></a><span data-ttu-id="e26e5-255">傳送您自己的遙測</span><span class="sxs-lookup"><span data-stu-id="e26e5-255">Send your own telemetry</span></span>
<span data-ttu-id="e26e5-256">既然您已安裝 SDK，您可以使用 API 來傳送自己的遙測。</span><span class="sxs-lookup"><span data-stu-id="e26e5-256">Now that you've installed the SDK, you can use the API to send your own telemetry.</span></span>

* <span data-ttu-id="e26e5-257">[追蹤自訂事件和度量][api]，以了解使用者正對應用程式進行的動作。</span><span class="sxs-lookup"><span data-stu-id="e26e5-257">[Track custom events and metrics][api] to learn what users are doing with your application.</span></span>
* <span data-ttu-id="e26e5-258">[搜尋事件和記錄][diagnostic]以協助診斷問題。</span><span class="sxs-lookup"><span data-stu-id="e26e5-258">[Search events and logs][diagnostic] to help diagnose problems.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="e26e5-259">可用性 Web 測試</span><span class="sxs-lookup"><span data-stu-id="e26e5-259">Availability web tests</span></span>
<span data-ttu-id="e26e5-260">Application Insights 可讓您定期測試網站，以檢查網站運作中且正常回應。</span><span class="sxs-lookup"><span data-stu-id="e26e5-260">Application Insights can test your website at regular intervals to check that it's up and responding well.</span></span> <span data-ttu-id="e26e5-261">[若要設定][availability]，請按一下 Web 測試。</span><span class="sxs-lookup"><span data-stu-id="e26e5-261">[To set up][availability], click Web tests.</span></span>

![按一下 [Web 測試]，然後按一下 [新增 Web 測試]](./media/app-insights-java-get-started/31-config-web-test.png)

<span data-ttu-id="e26e5-263">您將取得回應時間的圖表，以及若網站關閉還會取得電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="e26e5-263">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Web 測試範例](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

<span data-ttu-id="e26e5-265">[深入了解 Web 測試的可用性。][availability]</span><span class="sxs-lookup"><span data-stu-id="e26e5-265">[Learn more about availability web tests.][availability]</span></span>

## <a name="questions-problems"></a><span data-ttu-id="e26e5-266">有疑問嗎？</span><span class="sxs-lookup"><span data-stu-id="e26e5-266">Questions?</span></span> <span data-ttu-id="e26e5-267">有問題嗎？</span><span class="sxs-lookup"><span data-stu-id="e26e5-267">Problems?</span></span>
[<span data-ttu-id="e26e5-268">疑難排解 Java</span><span class="sxs-lookup"><span data-stu-id="e26e5-268">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

## <a name="video"></a><span data-ttu-id="e26e5-269">影片</span><span class="sxs-lookup"><span data-stu-id="e26e5-269">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="e26e5-270">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e26e5-270">Next steps</span></span>
* [<span data-ttu-id="e26e5-271">監視相依性呼叫</span><span class="sxs-lookup"><span data-stu-id="e26e5-271">Monitor dependency calls</span></span>](app-insights-java-agent.md)
* [<span data-ttu-id="e26e5-272">監視 Unix 效能計數器</span><span class="sxs-lookup"><span data-stu-id="e26e5-272">Monitor Unix performance counters</span></span>](app-insights-java-collectd.md)
* <span data-ttu-id="e26e5-273">新增[對網頁的監視](app-insights-javascript.md)，以監視頁面載入時間、AJAX 呼叫、瀏覽器例外狀況。</span><span class="sxs-lookup"><span data-stu-id="e26e5-273">Add [monitoring to your web pages](app-insights-javascript.md) to monitor page load times, AJAX calls, browser exceptions.</span></span>
* <span data-ttu-id="e26e5-274">撰寫[自訂遙測](app-insights-api-custom-events-metrics.md)，以追蹤瀏覽器中或在伺服器上的使用情況。</span><span class="sxs-lookup"><span data-stu-id="e26e5-274">Write [custom telemetry](app-insights-api-custom-events-metrics.md) to track usage in the browser or at the server.</span></span>
* <span data-ttu-id="e26e5-275">建立[儀表板](app-insights-dashboards.md)，以結合重要圖表來監視您的系統。</span><span class="sxs-lookup"><span data-stu-id="e26e5-275">Create [dashboards](app-insights-dashboards.md) to bring together the key charts for monitoring your system.</span></span>
* <span data-ttu-id="e26e5-276">使用[分析](app-insights-analytics.md)功能從您的應用程式透過遙測進行強大查詢</span><span class="sxs-lookup"><span data-stu-id="e26e5-276">Use  [Analytics](app-insights-analytics.md) for powerful queries over telemetry from your app</span></span>
* <span data-ttu-id="e26e5-277">如需詳細資訊，請瀏覽[適用於 Java 開發人員的 Azure](/java/azure)。</span><span class="sxs-lookup"><span data-stu-id="e26e5-277">For more information, visit [Azure for Java developers](/java/azure).</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
