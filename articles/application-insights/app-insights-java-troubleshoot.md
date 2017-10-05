---
title: "疑難排解 Java Web 專案中的 Application Insights"
description: "疑難排解指南 - 使用 Application Insights 監視即時的 Java 應用程式。"
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: ce46a4f561a273dc340b090a5bf0c8932a308722
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="cc370-103">Application Insights for Java 的疑難排解和問答集</span><span class="sxs-lookup"><span data-stu-id="cc370-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="cc370-104">[Java 中的 Azure Application Insights][java] 疑問或問題？</span><span class="sxs-lookup"><span data-stu-id="cc370-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="cc370-105">以下是一些秘訣。</span><span class="sxs-lookup"><span data-stu-id="cc370-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="cc370-106">建置錯誤</span><span class="sxs-lookup"><span data-stu-id="cc370-106">Build errors</span></span>
<span data-ttu-id="cc370-107">**在 Eclipse 中，透過 Maven 或 Gradle 加入 Application Insights SDK 時，我收到建置或總和檢查碼驗證錯誤。**</span><span class="sxs-lookup"><span data-stu-id="cc370-107">**In Eclipse, when adding the Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="cc370-108">如果相依性 <version> 元素使用具有萬用字元的模式 (例如 (Maven) `<version>[1.0,)</version>` 或 (Gradle) `version:'1.0.+'`)，請嘗試改為指定特定版本 (例如 `1.0.2`)。</span><span class="sxs-lookup"><span data-stu-id="cc370-108">If the dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span></span> <span data-ttu-id="cc370-109">請參閱最新版本的 [版本資訊](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) 。</span><span class="sxs-lookup"><span data-stu-id="cc370-109">See the [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for the latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="cc370-110">沒有資料</span><span class="sxs-lookup"><span data-stu-id="cc370-110">No data</span></span>
<span data-ttu-id="cc370-111">**我已成功加入 Application Insights 並執行我的應用程式，但在入口網站中從未看到資料。**</span><span class="sxs-lookup"><span data-stu-id="cc370-111">**I added Application Insights successfully and ran my app, but I've never seen data in the portal.**</span></span>

* <span data-ttu-id="cc370-112">請稍等片刻，然後按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="cc370-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="cc370-113">圖表會定期自行重新整理，但您也可以手動重新整理。</span><span class="sxs-lookup"><span data-stu-id="cc370-113">The charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="cc370-114">重新整理間隔取決於圖表的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="cc370-114">The refresh interval depends on the time range of the chart.</span></span>
* <span data-ttu-id="cc370-115">檢查 ApplicationInsights.xml 檔案 (位於專案的 resources 資料夾) 中已定義檢測機碼</span><span class="sxs-lookup"><span data-stu-id="cc370-115">Check that you have an instrumentation key defined in the ApplicationInsights.xml file (in the resources folder in your project)</span></span>
* <span data-ttu-id="cc370-116">確認 xml 檔案中沒有 `<DisableTelemetry>true</DisableTelemetry>` 節點。</span><span class="sxs-lookup"><span data-stu-id="cc370-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in the xml file.</span></span>
* <span data-ttu-id="cc370-117">在防火牆中，您可能必須開啟 TCP 連接埠 80 和 443，以允許連出流量送往 dc.services.visualstudio.com。請參閱 [完整的防火牆例外狀況清單](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="cc370-117">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com. See the [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="cc370-118">在 Microsoft Azure 開始面板中，查看服務狀態對應。</span><span class="sxs-lookup"><span data-stu-id="cc370-118">In the Microsoft Azure start board, look at the service status map.</span></span> <span data-ttu-id="cc370-119">如果看到一些警示指示，請等待它們恢復 [正常]，然後關閉再重新開啟 Application Insights 應用程式刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="cc370-119">If there are some alert indications, wait until they have returned to OK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="cc370-120">在 ApplicationInsights.xml 檔案 (位於專案的 resources 資料夾) 的根節點下加入 `<SDKLogger />` 元素，即可開啟記錄至 IDE 主控台視窗，然後檢查前面加上 [Error] 的項目。</span><span class="sxs-lookup"><span data-stu-id="cc370-120">Turn on logging to the IDE console window, by adding an `<SDKLogger />` element under the root node in the ApplicationInsights.xml file (in the resources folder in your project), and check for entries prefaced with [Error].</span></span>
* <span data-ttu-id="cc370-121">藉由查看主控台的輸出訊息「已成功找到組態檔」陳述式，確定 Java SDK 已成功載入正確的 ApplicationInsights.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="cc370-121">Make sure that the correct ApplicationInsights.xml file has been successfully loaded by the Java SDK, by looking at the console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="cc370-122">如果找不到組態檔，請檢查輸出訊息以查看在何處搜尋組態檔，並確定 ApplicationInsights.xml 位在這些搜尋位置中的其中一個位置。</span><span class="sxs-lookup"><span data-stu-id="cc370-122">If the config file is not found, check the output messages to see where the config file is being searched for, and make sure that the ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="cc370-123">根據經驗法則，您可以將組態檔置於 Application Insights SDK JAR 附近。</span><span class="sxs-lookup"><span data-stu-id="cc370-123">As a rule of thumb, you can place the config file near the Application Insights SDK JARs.</span></span> <span data-ttu-id="cc370-124">例如：在 Tomcat 中，這可能表示 WEB-INF/lib 資料夾。</span><span class="sxs-lookup"><span data-stu-id="cc370-124">For example: in Tomcat, this would mean the WEB-INF/lib folder.</span></span>

#### <a name="i-used-to-see-data-but-it-has-stopped"></a><span data-ttu-id="cc370-125">我曾經看到資料，但是已停止</span><span class="sxs-lookup"><span data-stu-id="cc370-125">I used to see data, but it has stopped</span></span>
* <span data-ttu-id="cc370-126">檢查 [狀態部落格](http://blogs.msdn.com/b/applicationinsights-status/)。</span><span class="sxs-lookup"><span data-stu-id="cc370-126">Check the [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="cc370-127">您有達到資料點的每月配額嗎？</span><span class="sxs-lookup"><span data-stu-id="cc370-127">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="cc370-128">開啟 [設定/配額和定價] 即可查看。若有達到配額，您可以升級您的方案，或付費取得額外容量。</span><span class="sxs-lookup"><span data-stu-id="cc370-128">Open Settings/Quota and Pricing to find out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="cc370-129">請參閱 [定價配置](https://azure.microsoft.com/pricing/details/application-insights/)。</span><span class="sxs-lookup"><span data-stu-id="cc370-129">See the [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>

#### <a name="i-dont-see-all-the-data-im-expecting"></a><span data-ttu-id="cc370-130">我並沒有看到預期的所有資料</span><span class="sxs-lookup"><span data-stu-id="cc370-130">I don't see all the data I'm expecting</span></span>
* <span data-ttu-id="cc370-131">開啟 [配額和價格] 刀鋒視窗，檢查是否正在進行 [取樣](app-insights-sampling.md) 。</span><span class="sxs-lookup"><span data-stu-id="cc370-131">Open the Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="cc370-132">(100% 傳輸表示目前未進行取樣。)Application Insights 服務可以設定為只接受來自您的應用程式的一小部分遙測。</span><span class="sxs-lookup"><span data-stu-id="cc370-132">(100% transmission means that sampling isn't in operation.) The Application Insights service can be set to accept only a fraction of the telemetry that arrives from your app.</span></span> <span data-ttu-id="cc370-133">這有助於您維持在每月的遙測配額內。</span><span class="sxs-lookup"><span data-stu-id="cc370-133">This helps you keep within your monthly quota of telemetry.</span></span> 

## <a name="no-usage-data"></a><span data-ttu-id="cc370-134">沒有使用狀況資料</span><span class="sxs-lookup"><span data-stu-id="cc370-134">No usage data</span></span>
<span data-ttu-id="cc370-135">**我看到要求和回應時間的相關資料，但沒有看到頁面檢視、瀏覽器或使用者資料的相關資料。**</span><span class="sxs-lookup"><span data-stu-id="cc370-135">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="cc370-136">您已成功設定應用程式從伺服器傳送遙測。</span><span class="sxs-lookup"><span data-stu-id="cc370-136">You successfully set up your app to send telemetry from the server.</span></span> <span data-ttu-id="cc370-137">現在，您的下一步是[設定網頁，以從網頁瀏覽器傳送遙測][usage]。</span><span class="sxs-lookup"><span data-stu-id="cc370-137">Now your next step is to [set up your web pages to send telemetry from the web browser][usage].</span></span>

<span data-ttu-id="cc370-138">或者，如果您的用戶端是[手機或其他裝置][platforms]中的應用程式，則可以從該處傳送遙測。</span><span class="sxs-lookup"><span data-stu-id="cc370-138">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="cc370-139">使用相同的檢測機碼來設定用戶端和伺服器遙測。</span><span class="sxs-lookup"><span data-stu-id="cc370-139">Use the same instrumentation key to set up both your client and server telemetry.</span></span> <span data-ttu-id="cc370-140">資料會出現在相同的 Application Insights 資源中，而且您可以相互關聯來自用戶端和伺服器的事件。</span><span class="sxs-lookup"><span data-stu-id="cc370-140">The data will appear in the same Application Insights resource, and you'll be able to correlate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="cc370-141">停用遙測</span><span class="sxs-lookup"><span data-stu-id="cc370-141">Disabling telemetry</span></span>
<span data-ttu-id="cc370-142">**如何停用遙測收集？**</span><span class="sxs-lookup"><span data-stu-id="cc370-142">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="cc370-143">在程式碼中：</span><span class="sxs-lookup"><span data-stu-id="cc370-143">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="cc370-144">**或**</span><span class="sxs-lookup"><span data-stu-id="cc370-144">**Or**</span></span> 

<span data-ttu-id="cc370-145">更新 ApplicationInsights.xml (位於專案的 resources 資料夾)。</span><span class="sxs-lookup"><span data-stu-id="cc370-145">Update ApplicationInsights.xml (in the resources folder in your project).</span></span> <span data-ttu-id="cc370-146">在根節點下加入下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="cc370-146">Add the following under the root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="cc370-147">如果使用 XML 方法，則必須在變更值時重新啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc370-147">Using the XML method, you have to restart the application when you change the value.</span></span>

## <a name="changing-the-target"></a><span data-ttu-id="cc370-148">變更目標</span><span class="sxs-lookup"><span data-stu-id="cc370-148">Changing the target</span></span>
<span data-ttu-id="cc370-149">**如何變更我的專案將資料傳送到哪一個 Azure 資源？**</span><span class="sxs-lookup"><span data-stu-id="cc370-149">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="cc370-150">[取得新資源的檢測金鑰。][java]</span><span class="sxs-lookup"><span data-stu-id="cc370-150">[Get the instrumentation key of the new resource.][java]</span></span>
* <span data-ttu-id="cc370-151">如果您已使用 Azure Toolkit for Eclipse 將 Application Insights 新增到您的專案，請在 Web 專案上按一下滑鼠右鍵，依序選取 [Azure] 和 [設定 Application Insights]，然後變更金鑰。</span><span class="sxs-lookup"><span data-stu-id="cc370-151">If you added Application Insights to your project using the Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change the key.</span></span>
* <span data-ttu-id="cc370-152">否則，請更新專案之 resources 資料夾的 ApplicationInsights.xml 中的機碼。</span><span class="sxs-lookup"><span data-stu-id="cc370-152">Otherwise, update the key in ApplicationInsights.xml in the resources folder in your project.</span></span>

## <a name="debug-data-from-the-sdk"></a><span data-ttu-id="cc370-153">從 SDK 進行資料偵錯</span><span class="sxs-lookup"><span data-stu-id="cc370-153">Debug data from the SDK</span></span>

<span data-ttu-id="cc370-154">**如何找出 SDK 正在做什麼？**</span><span class="sxs-lookup"><span data-stu-id="cc370-154">**How can I find out what the SDK is doing?**</span></span>

<span data-ttu-id="cc370-155">若要取得有關 API 中所進行作業的詳細資訊，請在 ApplicationInsights.xml 組態檔的根節點底下新增 `<SDKLogger/>`。</span><span class="sxs-lookup"><span data-stu-id="cc370-155">To get more information about what's happening in the API, add `<SDKLogger/>` under the root node of the ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="cc370-156">您也可以指示記錄器輸出至檔案：</span><span class="sxs-lookup"><span data-stu-id="cc370-156">You can also instruct the logger to output to a file:</span></span>

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

<span data-ttu-id="cc370-157">如果是 Tomcat 伺服器，檔案可以在 `%temp%\javasdklogs` 或 `java.io.tmpdir` 底下找到。</span><span class="sxs-lookup"><span data-stu-id="cc370-157">The files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span></span>


## <a name="the-azure-start-screen"></a><span data-ttu-id="cc370-158">Azure 開始畫面</span><span class="sxs-lookup"><span data-stu-id="cc370-158">The Azure start screen</span></span>
<span data-ttu-id="cc370-159">**我正在查看 [Azure 入口網站](https://portal.azure.com)。地圖是否告知有關我的應用程式的相關資訊？**</span><span class="sxs-lookup"><span data-stu-id="cc370-159">**I'm looking at [the Azure portal](https://portal.azure.com). Does the map tell me something about my app?**</span></span>

<span data-ttu-id="cc370-160">否，它會顯示世界各地 Azure 伺服器的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="cc370-160">No, it shows the health of Azure servers around the world.</span></span>

<span data-ttu-id="cc370-161">*從 Azure 開始面板 (主畫面) 中，如何找到我應用程式的相關資料？*</span><span class="sxs-lookup"><span data-stu-id="cc370-161">*From the Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="cc370-162">假設您已[設定 Application Insights 的應用程式][java]，請按一下 [瀏覽]，選取 [Application Insights]，然後選取您為應用程式建立的應用程式資源。</span><span class="sxs-lookup"><span data-stu-id="cc370-162">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select the app resource you created for your app.</span></span> <span data-ttu-id="cc370-163">日後若要更快速地從該處開始，您可以將應用程式釘選至開始面板。</span><span class="sxs-lookup"><span data-stu-id="cc370-163">To get there faster in future, you can pin your app to the start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="cc370-164">內部網路伺服器</span><span class="sxs-lookup"><span data-stu-id="cc370-164">Intranet servers</span></span>
<span data-ttu-id="cc370-165">**可以在我的內部網路上監視伺服器嗎？**</span><span class="sxs-lookup"><span data-stu-id="cc370-165">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="cc370-166">是，前提是您的伺服器可以透過公用網際網路將遙測傳送至 Application Insights 入口網站。</span><span class="sxs-lookup"><span data-stu-id="cc370-166">Yes, provided your server can send telemetry to the Application Insights portal through the public internet.</span></span> 

<span data-ttu-id="cc370-167">在防火牆中，您可能必須開啟 TCP 連接埠 80 和 443，以允許連出流量送往 dc.services.visualstudio.com 和 f5.services.visualstudio.com。</span><span class="sxs-lookup"><span data-stu-id="cc370-167">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="cc370-168">資料保留</span><span class="sxs-lookup"><span data-stu-id="cc370-168">Data retention</span></span>
<span data-ttu-id="cc370-169">**資料保留在入口網站多久的時間？是否安全？**</span><span class="sxs-lookup"><span data-stu-id="cc370-169">**How long is data retained in the portal? Is it secure?**</span></span>

<span data-ttu-id="cc370-170">請參閱[資料保留和隱私權][data]。</span><span class="sxs-lookup"><span data-stu-id="cc370-170">See [Data retention and privacy][data].</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc370-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cc370-171">Next steps</span></span>
<span data-ttu-id="cc370-172">**設定 Java 伺服器應用程式的 Application Insights。我還可以做什麼？**</span><span class="sxs-lookup"><span data-stu-id="cc370-172">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="cc370-173">[監視網頁可用性][availability]</span><span class="sxs-lookup"><span data-stu-id="cc370-173">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="cc370-174">[監視網頁使用狀況][usage]</span><span class="sxs-lookup"><span data-stu-id="cc370-174">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="cc370-175">[追蹤使用狀況並診斷裝置應用程式中的問題][platforms]</span><span class="sxs-lookup"><span data-stu-id="cc370-175">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="cc370-176">[撰寫程式碼以追蹤應用程式使用狀況][track]</span><span class="sxs-lookup"><span data-stu-id="cc370-176">[Write code to track usage of your app][track]</span></span>
* <span data-ttu-id="cc370-177">[擷取診斷記錄][javalogs]</span><span class="sxs-lookup"><span data-stu-id="cc370-177">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="cc370-178">取得說明</span><span class="sxs-lookup"><span data-stu-id="cc370-178">Get help</span></span>
* [<span data-ttu-id="cc370-179">堆疊溢位</span><span class="sxs-lookup"><span data-stu-id="cc370-179">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

