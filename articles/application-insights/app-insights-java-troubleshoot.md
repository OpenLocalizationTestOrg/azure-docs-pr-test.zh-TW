---
title: "在 Java web 專案中的 Application Insights aaaTroubleshoot"
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
ms.openlocfilehash: c274c01b1992971fae194c3e510512ca06ab76b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="abcd3-103">Application Insights for Java 的疑難排解和問答集</span><span class="sxs-lookup"><span data-stu-id="abcd3-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="abcd3-104">[Java 中的 Azure Application Insights][java] 疑問或問題？</span><span class="sxs-lookup"><span data-stu-id="abcd3-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="abcd3-105">以下是一些秘訣。</span><span class="sxs-lookup"><span data-stu-id="abcd3-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="abcd3-106">建置錯誤</span><span class="sxs-lookup"><span data-stu-id="abcd3-106">Build errors</span></span>
<span data-ttu-id="abcd3-107">**在 Eclipse 中，加入 hello Application Insights SDK，透過 Maven 或 Gradle，我會收到建置或總和檢查碼驗證錯誤。**</span><span class="sxs-lookup"><span data-stu-id="abcd3-107">**In Eclipse, when adding hello Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="abcd3-108">如果 hello 相依性<version>項目使用具有萬用字元的模式 (例如 (Maven)`<version>[1.0,)</version>`或 (Gradle) `version:'1.0.+'`)，請嘗試指定特定版本來取代像是`1.0.2`。</span><span class="sxs-lookup"><span data-stu-id="abcd3-108">If hello dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span></span> <span data-ttu-id="abcd3-109">請參閱 hello[版本資訊](https://github.com/Microsoft/ApplicationInsights-Java#release-notes)hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="abcd3-109">See hello [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for hello latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="abcd3-110">沒有資料</span><span class="sxs-lookup"><span data-stu-id="abcd3-110">No data</span></span>
<span data-ttu-id="abcd3-111">**我已成功加入 Application Insights 並執行我的應用程式，但從未 hello 入口網站中的資料。**</span><span class="sxs-lookup"><span data-stu-id="abcd3-111">**I added Application Insights successfully and ran my app, but I've never seen data in hello portal.**</span></span>

* <span data-ttu-id="abcd3-112">請稍等片刻，然後按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="abcd3-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="abcd3-113">hello 圖表定期重新整理本身，但您也可以手動更新。</span><span class="sxs-lookup"><span data-stu-id="abcd3-113">hello charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="abcd3-114">hello 重新整理間隔取決於 hello 的 hello 圖表的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="abcd3-114">hello refresh interval depends on hello time range of hello chart.</span></span>
* <span data-ttu-id="abcd3-115">請確認您已在 hello ApplicationInsights.xml 檔 （在專案中的 hello 資源資料夾） 中定義的檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="abcd3-115">Check that you have an instrumentation key defined in hello ApplicationInsights.xml file (in hello resources folder in your project)</span></span>
* <span data-ttu-id="abcd3-116">確認沒有任何`<DisableTelemetry>true</DisableTelemetry>`hello xml 檔案中的節點。</span><span class="sxs-lookup"><span data-stu-id="abcd3-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in hello xml file.</span></span>
* <span data-ttu-id="abcd3-117">在您的防火牆，您可能必須 tooopen TCP 連接埠 80 和 443 供連出流量 toodc.services.visualstudio.com。請參閱 hello[的防火牆例外狀況的完整清單](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="abcd3-117">In your firewall, you might have tooopen TCP ports 80 and 443 for outgoing traffic toodc.services.visualstudio.com. See hello [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="abcd3-118">Hello Microsoft Azure 中啟動 面板，請查看 hello 服務狀態對應。</span><span class="sxs-lookup"><span data-stu-id="abcd3-118">In hello Microsoft Azure start board, look at hello service status map.</span></span> <span data-ttu-id="abcd3-119">如果有某些警示的指示，請等到它們都傳回 tooOK 然後關閉再重新開啟 Application Insights 的應用程式刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="abcd3-119">If there are some alert indications, wait until they have returned tooOK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="abcd3-120">開啟 記錄 toohello IDE 主控台視窗中，藉由新增`<SDKLogger />`hello hello ApplicationInsights.xml 檔案 （在 hello 資源資料夾在專案中），並檢查 [錯誤] 開頭處的項目中的根節點下的項目。</span><span class="sxs-lookup"><span data-stu-id="abcd3-120">Turn on logging toohello IDE console window, by adding an `<SDKLogger />` element under hello root node in hello ApplicationInsights.xml file (in hello resources folder in your project), and check for entries prefaced with [Error].</span></span>
* <span data-ttu-id="abcd3-121">請確定該 hello 正確 ApplicationInsights.xml 檔案已成功載入 hello Java SDK 所查看的 」 組態檔已成功找到"陳述式的 hello 主控台輸出訊息。</span><span class="sxs-lookup"><span data-stu-id="abcd3-121">Make sure that hello correct ApplicationInsights.xml file has been successfully loaded by hello Java SDK, by looking at hello console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="abcd3-122">如果找不到 hello 設定檔，請檢查 hello 輸出訊息 toosee hello 設定檔，要搜尋位置，並確定 ApplicationInsights.xml 位於其中一個這些搜尋位置中的 hello。</span><span class="sxs-lookup"><span data-stu-id="abcd3-122">If hello config file is not found, check hello output messages toosee where hello config file is being searched for, and make sure that hello ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="abcd3-123">根據經驗法則，您可以將附近 hello 應用程式 Insights SDK Jar hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="abcd3-123">As a rule of thumb, you can place hello config file near hello Application Insights SDK JARs.</span></span> <span data-ttu-id="abcd3-124">例如： 在 Tomcat 中，這表示 hello WEB-INF/lib 資料夾。</span><span class="sxs-lookup"><span data-stu-id="abcd3-124">For example: in Tomcat, this would mean hello WEB-INF/lib folder.</span></span>

#### <a name="i-used-toosee-data-but-it-has-stopped"></a><span data-ttu-id="abcd3-125">我使用 toosee 資料，但它已停止</span><span class="sxs-lookup"><span data-stu-id="abcd3-125">I used toosee data, but it has stopped</span></span>
* <span data-ttu-id="abcd3-126">檢查 hello[狀態部落格](http://blogs.msdn.com/b/applicationinsights-status/)。</span><span class="sxs-lookup"><span data-stu-id="abcd3-126">Check hello [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="abcd3-127">您有達到資料點的每月配額嗎？</span><span class="sxs-lookup"><span data-stu-id="abcd3-127">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="abcd3-128">開啟 設定/配額和定價 toofind 出。若有達到配額，您可以升級您的方案，或付費取得額外容量。</span><span class="sxs-lookup"><span data-stu-id="abcd3-128">Open Settings/Quota and Pricing toofind out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="abcd3-129">請參閱 hello[定價配置](https://azure.microsoft.com/pricing/details/application-insights/)。</span><span class="sxs-lookup"><span data-stu-id="abcd3-129">See hello [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>

#### <a name="i-dont-see-all-hello-data-im-expecting"></a><span data-ttu-id="abcd3-130">我看不到我預期的所有 hello 資料</span><span class="sxs-lookup"><span data-stu-id="abcd3-130">I don't see all hello data I'm expecting</span></span>
* <span data-ttu-id="abcd3-131">開啟 hello 配額和定價刀鋒視窗，然後檢查是否[取樣](app-insights-sampling.md)在作業。</span><span class="sxs-lookup"><span data-stu-id="abcd3-131">Open hello Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="abcd3-132">（100%傳輸表示取樣，即不會在作業中）。hello Application Insights 服務可以設定 tooaccept 只有一小部份 hello 遙測來自您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="abcd3-132">(100% transmission means that sampling isn't in operation.) hello Application Insights service can be set tooaccept only a fraction of hello telemetry that arrives from your app.</span></span> <span data-ttu-id="abcd3-133">這有助於您維持在每月的遙測配額內。</span><span class="sxs-lookup"><span data-stu-id="abcd3-133">This helps you keep within your monthly quota of telemetry.</span></span> 

## <a name="no-usage-data"></a><span data-ttu-id="abcd3-134">沒有使用狀況資料</span><span class="sxs-lookup"><span data-stu-id="abcd3-134">No usage data</span></span>
<span data-ttu-id="abcd3-135">**我看到要求和回應時間的相關資料，但沒有看到頁面檢視、瀏覽器或使用者資料的相關資料。**</span><span class="sxs-lookup"><span data-stu-id="abcd3-135">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="abcd3-136">您已成功設定應用程式 toosend 遙測從 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="abcd3-136">You successfully set up your app toosend telemetry from hello server.</span></span> <span data-ttu-id="abcd3-137">現在您的下一個步驟太[設定 hello 網頁瀏覽器從您網頁 toosend 遙測][usage]。</span><span class="sxs-lookup"><span data-stu-id="abcd3-137">Now your next step is too[set up your web pages toosend telemetry from hello web browser][usage].</span></span>

<span data-ttu-id="abcd3-138">或者，如果您的用戶端是[手機或其他裝置][platforms]中的應用程式，則可以從該處傳送遙測。</span><span class="sxs-lookup"><span data-stu-id="abcd3-138">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="abcd3-139">使用 hello 相同檢測金鑰 tooset 註冊用戶端和伺服器遙測。</span><span class="sxs-lookup"><span data-stu-id="abcd3-139">Use hello same instrumentation key tooset up both your client and server telemetry.</span></span> <span data-ttu-id="abcd3-140">hello 相同的 Application Insights 資源，以及您可以從用戶端和伺服器可以 toocorrelate 事件，會出現在 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="abcd3-140">hello data will appear in hello same Application Insights resource, and you'll be able toocorrelate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="abcd3-141">停用遙測</span><span class="sxs-lookup"><span data-stu-id="abcd3-141">Disabling telemetry</span></span>
<span data-ttu-id="abcd3-142">**如何停用遙測收集？**</span><span class="sxs-lookup"><span data-stu-id="abcd3-142">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="abcd3-143">在程式碼中：</span><span class="sxs-lookup"><span data-stu-id="abcd3-143">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="abcd3-144">**或**</span><span class="sxs-lookup"><span data-stu-id="abcd3-144">**Or**</span></span> 

<span data-ttu-id="abcd3-145">更新 ApplicationInsights.xml （在專案中的 hello 資源資料夾）。</span><span class="sxs-lookup"><span data-stu-id="abcd3-145">Update ApplicationInsights.xml (in hello resources folder in your project).</span></span> <span data-ttu-id="abcd3-146">加入 hello hello 根節點下的下列：</span><span class="sxs-lookup"><span data-stu-id="abcd3-146">Add hello following under hello root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="abcd3-147">當您變更 hello 值時，使用 hello XML 方法時，有 toorestart hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="abcd3-147">Using hello XML method, you have toorestart hello application when you change hello value.</span></span>

## <a name="changing-hello-target"></a><span data-ttu-id="abcd3-148">變更 hello 目標</span><span class="sxs-lookup"><span data-stu-id="abcd3-148">Changing hello target</span></span>
<span data-ttu-id="abcd3-149">**如何變更我的專案將資料傳送到哪一個 Azure 資源？**</span><span class="sxs-lookup"><span data-stu-id="abcd3-149">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="abcd3-150">[收到 hello hello 新資源的檢測金鑰。][java]</span><span class="sxs-lookup"><span data-stu-id="abcd3-150">[Get hello instrumentation key of hello new resource.][java]</span></span>
* <span data-ttu-id="abcd3-151">如果您加入 Application Insights tooyour 專案使用 hello Azure Toolkit for Eclipse，以滑鼠右鍵按一下您的 web 專案中，選取**Azure**，**設定 Application Insights**，並變更 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="abcd3-151">If you added Application Insights tooyour project using hello Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change hello key.</span></span>
* <span data-ttu-id="abcd3-152">否則，請更新中 ApplicationInsights.xml hello 資源 資料夾中您的專案中的 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="abcd3-152">Otherwise, update hello key in ApplicationInsights.xml in hello resources folder in your project.</span></span>

## <a name="debug-data-from-hello-sdk"></a><span data-ttu-id="abcd3-153">偵錯 hello SDK 的資料</span><span class="sxs-lookup"><span data-stu-id="abcd3-153">Debug data from hello SDK</span></span>

<span data-ttu-id="abcd3-154">**如何得知哪些 hello SDK 執行的動作？**</span><span class="sxs-lookup"><span data-stu-id="abcd3-154">**How can I find out what hello SDK is doing?**</span></span>

<span data-ttu-id="abcd3-155">tooget hello API 中的情況的詳細資訊加入`<SDKLogger/>`hello hello ApplicationInsights.xml 組態檔的根節點下。</span><span class="sxs-lookup"><span data-stu-id="abcd3-155">tooget more information about what's happening in hello API, add `<SDKLogger/>` under hello root node of hello ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="abcd3-156">您也可以指示 hello 記錄器 toooutput tooa 檔案：</span><span class="sxs-lookup"><span data-stu-id="abcd3-156">You can also instruct hello logger toooutput tooa file:</span></span>

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

<span data-ttu-id="abcd3-157">您可以找到 hello 檔案`%temp%\javasdklogs`或`java.io.tmpdir`發生 Tomcat 伺服器。</span><span class="sxs-lookup"><span data-stu-id="abcd3-157">hello files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span></span>


## <a name="hello-azure-start-screen"></a><span data-ttu-id="abcd3-158">hello Azure 開始 畫面</span><span class="sxs-lookup"><span data-stu-id="abcd3-158">hello Azure start screen</span></span>
<span data-ttu-id="abcd3-159">**我正在尋找在[hello Azure 入口網站](https://portal.azure.com)。沒有 hello 對應告訴我的項目有關我的應用程式嗎？**</span><span class="sxs-lookup"><span data-stu-id="abcd3-159">**I'm looking at [hello Azure portal](https://portal.azure.com). Does hello map tell me something about my app?**</span></span>

<span data-ttu-id="abcd3-160">否，它會顯示 hello 健全狀況的 Azure 伺服器 hello 世界各地。</span><span class="sxs-lookup"><span data-stu-id="abcd3-160">No, it shows hello health of Azure servers around hello world.</span></span>

<span data-ttu-id="abcd3-161">*從 hello Azure 開始面板 （主畫面），如何尋找資料我的應用程式？*</span><span class="sxs-lookup"><span data-stu-id="abcd3-161">*From hello Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="abcd3-162">假設您[設定您的應用程式的 Application Insights][java]、 按一下 瀏覽、 選取 Application Insights 和選取您建立應用程式的 hello 應用程式資源。</span><span class="sxs-lookup"><span data-stu-id="abcd3-162">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select hello app resource you created for your app.</span></span> <span data-ttu-id="abcd3-163">tooget 那里在未來更快，您可以釘選您的應用程式 toohello 開始面板。</span><span class="sxs-lookup"><span data-stu-id="abcd3-163">tooget there faster in future, you can pin your app toohello start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="abcd3-164">內部網路伺服器</span><span class="sxs-lookup"><span data-stu-id="abcd3-164">Intranet servers</span></span>
<span data-ttu-id="abcd3-165">**可以在我的內部網路上監視伺服器嗎？**</span><span class="sxs-lookup"><span data-stu-id="abcd3-165">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="abcd3-166">是，提供您的伺服器可以傳送遙測 toohello Application Insights 入口網站來完成 hello 公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="abcd3-166">Yes, provided your server can send telemetry toohello Application Insights portal through hello public internet.</span></span> 

<span data-ttu-id="abcd3-167">在您的防火牆，您可能必須 tooopen TCP 連接埠 80 和 443 供連出流量 toodc.services.visualstudio.com 和 f5.services.visualstudio.com。</span><span class="sxs-lookup"><span data-stu-id="abcd3-167">In your firewall, you might have tooopen TCP ports 80 and 443 for outgoing traffic toodc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="abcd3-168">資料保留</span><span class="sxs-lookup"><span data-stu-id="abcd3-168">Data retention</span></span>
<span data-ttu-id="abcd3-169">**資料保留多久 hello 入口網站中？是否安全？**</span><span class="sxs-lookup"><span data-stu-id="abcd3-169">**How long is data retained in hello portal? Is it secure?**</span></span>

<span data-ttu-id="abcd3-170">請參閱[資料保留和隱私權][data]。</span><span class="sxs-lookup"><span data-stu-id="abcd3-170">See [Data retention and privacy][data].</span></span>

## <a name="next-steps"></a><span data-ttu-id="abcd3-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="abcd3-171">Next steps</span></span>
<span data-ttu-id="abcd3-172">**設定 Java 伺服器應用程式的 Application Insights。我還可以做什麼？**</span><span class="sxs-lookup"><span data-stu-id="abcd3-172">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="abcd3-173">[監視網頁可用性][availability]</span><span class="sxs-lookup"><span data-stu-id="abcd3-173">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="abcd3-174">[監視網頁使用狀況][usage]</span><span class="sxs-lookup"><span data-stu-id="abcd3-174">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="abcd3-175">[追蹤使用狀況並診斷裝置應用程式中的問題][platforms]</span><span class="sxs-lookup"><span data-stu-id="abcd3-175">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="abcd3-176">[撰寫您的應用程式的程式碼 tootrack 使用量][track]</span><span class="sxs-lookup"><span data-stu-id="abcd3-176">[Write code tootrack usage of your app][track]</span></span>
* <span data-ttu-id="abcd3-177">[擷取診斷記錄][javalogs]</span><span class="sxs-lookup"><span data-stu-id="abcd3-177">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="abcd3-178">取得說明</span><span class="sxs-lookup"><span data-stu-id="abcd3-178">Get help</span></span>
* [<span data-ttu-id="abcd3-179">堆疊溢位</span><span class="sxs-lookup"><span data-stu-id="abcd3-179">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

