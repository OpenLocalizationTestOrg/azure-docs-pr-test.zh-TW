---
title: "監視 Linux - Azure 上的 Java Web 應用程式效能 | Microsoft Docs"
description: "使用 Application Insights 的 CollectD 外掛程式擴充您的 Java 網站的應用程式效能監視功能。"
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 40c68f45-197a-4624-bf89-541eb7323002
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: 4ea917b068e0242bfb88d7357eca032607a43a3f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a><span data-ttu-id="76781-103">collectd：Application Insights 中的 Linux 效能計量</span><span class="sxs-lookup"><span data-stu-id="76781-103">collectd: Linux performance metrics in Application Insights</span></span>


<span data-ttu-id="76781-104">若要在 [Application Insights](app-insights-overview.md) 中瀏覽 Linux 系統效能度量，請安裝 [collectd](http://collectd.org/) 以及其 Application Insights 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="76781-104">To explore Linux system performance metrics in [Application Insights](app-insights-overview.md), install [collectd](http://collectd.org/), together with its Application Insights plug-in.</span></span> <span data-ttu-id="76781-105">這個開放原始碼解決方案會收集各種系統和網路統計資料。</span><span class="sxs-lookup"><span data-stu-id="76781-105">This open-source solution gathers various system and network statistics.</span></span>

<span data-ttu-id="76781-106">如果您已[使用 Application Insights 檢測您的 Java Web 服務][java]，通常您會使用 collectd。</span><span class="sxs-lookup"><span data-stu-id="76781-106">Typically you'll use collectd if you have already [instrumented your Java web service with Application Insights][java].</span></span> <span data-ttu-id="76781-107">提供給您更多資料來幫助您增強應用程式的效能或診斷問題。</span><span class="sxs-lookup"><span data-stu-id="76781-107">It gives you more data to help you to enhance your app's performance or diagnose problems.</span></span> 

![範例圖表](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a><span data-ttu-id="76781-109">取得檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="76781-109">Get your instrumentation key</span></span>
<span data-ttu-id="76781-110">在 [Microsoft Azure 入口網站](https://portal.azure.com)中，開啟您要顯示資料的 [Application Insights](app-insights-overview.md) 資源。</span><span class="sxs-lookup"><span data-stu-id="76781-110">In the [Microsoft Azure portal](https://portal.azure.com), open the [Application Insights](app-insights-overview.md) resource where you want the data to appear.</span></span> <span data-ttu-id="76781-111">(或[建立新的資源](app-insights-create-new-resource.md)。)</span><span class="sxs-lookup"><span data-stu-id="76781-111">(Or [create a new resource](app-insights-create-new-resource.md).)</span></span>

<span data-ttu-id="76781-112">取得一份可識別資源的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="76781-112">Take a copy of the instrumentation key, which identifies the resource.</span></span>

![瀏覽全部，開啟您的資源，然後在 [Essentials] 下拉式清單中，選取並複製檢測金鑰](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-the-plug-in"></a><span data-ttu-id="76781-114">安裝 collectd 和外掛程式</span><span class="sxs-lookup"><span data-stu-id="76781-114">Install collectd and the plug-in</span></span>
<span data-ttu-id="76781-115">在您的 Linux 伺服器機器上：</span><span class="sxs-lookup"><span data-stu-id="76781-115">On your Linux server machines:</span></span>

1. <span data-ttu-id="76781-116">安裝 [collectd](http://collectd.org/) 5.4.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="76781-116">Install [collectd](http://collectd.org/) version 5.4.0 or later.</span></span>
2. <span data-ttu-id="76781-117">下載 [Application Insights collectd 寫入器外掛程式](https://aka.ms/aijavasdk)。</span><span class="sxs-lookup"><span data-stu-id="76781-117">Download the [Application Insights collectd writer plugin](https://aka.ms/aijavasdk).</span></span> <span data-ttu-id="76781-118">記下版本號碼。</span><span class="sxs-lookup"><span data-stu-id="76781-118">Note the version number.</span></span>
3. <span data-ttu-id="76781-119">將外掛程式 JAR 複製到 `/usr/share/collectd/java`。</span><span class="sxs-lookup"><span data-stu-id="76781-119">Copy the plugin JAR into `/usr/share/collectd/java`.</span></span>
4. <span data-ttu-id="76781-120">編輯 `/etc/collectd/collectd.conf`：</span><span class="sxs-lookup"><span data-stu-id="76781-120">Edit `/etc/collectd/collectd.conf`:</span></span>
   * <span data-ttu-id="76781-121">確定 [Java 外掛程式](https://collectd.org/wiki/index.php/Plugin:Java) 已啟用。</span><span class="sxs-lookup"><span data-stu-id="76781-121">Ensure that [the Java plugin](https://collectd.org/wiki/index.php/Plugin:Java) is enabled.</span></span>
   * <span data-ttu-id="76781-122">更新 java.class.path 的 JVMArg 以包括下列 JAR。</span><span class="sxs-lookup"><span data-stu-id="76781-122">Update the JVMArg for the java.class.path to include the following JAR.</span></span> <span data-ttu-id="76781-123">更新版本號碼以符合您所下載的版本：</span><span class="sxs-lookup"><span data-stu-id="76781-123">Update the version number to match the one you downloaded:</span></span>
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * <span data-ttu-id="76781-124">使用來自您的資源的檢測金鑰，加入此程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="76781-124">Add this snippet, using the Instrumentation Key from your resource:</span></span>

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

<span data-ttu-id="76781-125">以下是範例組態檔的一部分：</span><span class="sxs-lookup"><span data-stu-id="76781-125">Here's part of a sample configuration file:</span></span>

```XML

    ...
    # collectd plugins
    LoadPlugin cpu
    LoadPlugin disk
    LoadPlugin load
    ...

    # Enable Java Plugin
    LoadPlugin "java"

    # Configure Java Plugin
    <Plugin "java">
      JVMArg "-verbose:jni"
      JVMArg "-Djava.class.path=/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar:/usr/share/collectd/java/collectd-api.jar"

      # Enabling Application Insights plugin
      LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"

      # Configuring Application Insights plugin
      <Plugin ApplicationInsightsWriter>
        InstrumentationKey "12345678-1234-1234-1234-123456781234"
      </Plugin>

      # Other plugin configurations ...
      ...
    </Plugin>
    ...
```

<span data-ttu-id="76781-126">設定其他 [collectd 外掛程式](https://collectd.org/wiki/index.php/Table_of_Plugins)，它可以從不同來源收集各種資料。</span><span class="sxs-lookup"><span data-stu-id="76781-126">Configure other [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), which can collect various data from different sources.</span></span>

<span data-ttu-id="76781-127">根據其 [手冊](https://collectd.org/wiki/index.php/First_steps)重新啟動 collectd。</span><span class="sxs-lookup"><span data-stu-id="76781-127">Restart collectd according to its [manual](https://collectd.org/wiki/index.php/First_steps).</span></span>

## <a name="view-the-data-in-application-insights"></a><span data-ttu-id="76781-128">在 Application Insights 中檢視資料</span><span class="sxs-lookup"><span data-stu-id="76781-128">View the data in Application Insights</span></span>
<span data-ttu-id="76781-129">在您的 Application Insights 資源中，開啟[計量瀏覽器並加入圖表][metrics]，從 [自訂] 類別選取您想要查看的度量。</span><span class="sxs-lookup"><span data-stu-id="76781-129">In your Application Insights resource, open [Metrics Explorer and add charts][metrics], selecting the metrics you want to see from the Custom category.</span></span>

![](./media/app-insights-java-collectd/result.png)

<span data-ttu-id="76781-130">根據預設，會對收集度量來源的所有主機電腦彙總度量。</span><span class="sxs-lookup"><span data-stu-id="76781-130">By default, the metrics are aggregated across all host machines from which the metrics were collected.</span></span> <span data-ttu-id="76781-131">若要檢視每一主機的度量，在圖表的 [詳細資料] 刀鋒視窗中，開啟 [群組]，然後選擇依 CollectD-Host 群組。</span><span class="sxs-lookup"><span data-stu-id="76781-131">To view the metrics per host, in the Chart details blade, turn on Grouping and then choose to group by CollectD-Host.</span></span>

## <a name="to-exclude-upload-of-specific-statistics"></a><span data-ttu-id="76781-132">排除特定統計資料的上傳</span><span class="sxs-lookup"><span data-stu-id="76781-132">To exclude upload of specific statistics</span></span>
<span data-ttu-id="76781-133">根據預設，Application Insights 外掛程式會傳送所有啟用的 collectd 'read' 外掛程式所收集的所有資料。</span><span class="sxs-lookup"><span data-stu-id="76781-133">By default, the Application Insights plugin sends all the data collected by all the enabled collectd 'read' plugins.</span></span> 

<span data-ttu-id="76781-134">若要排除特定外掛程式或資料來源的資料：</span><span class="sxs-lookup"><span data-stu-id="76781-134">To exclude data from specific plugins or data sources:</span></span>

* <span data-ttu-id="76781-135">編輯組態檔。</span><span class="sxs-lookup"><span data-stu-id="76781-135">Edit the configuration file.</span></span> 
* <span data-ttu-id="76781-136">在 `<Plugin ApplicationInsightsWriter>`中，加入指示詞行，如下所示：</span><span class="sxs-lookup"><span data-stu-id="76781-136">In `<Plugin ApplicationInsightsWriter>`, add directive lines like this:</span></span>

| <span data-ttu-id="76781-137">指示詞</span><span class="sxs-lookup"><span data-stu-id="76781-137">Directive</span></span> | <span data-ttu-id="76781-138">效果</span><span class="sxs-lookup"><span data-stu-id="76781-138">Effect</span></span> |
| --- | --- |
| `Exclude disk` |<span data-ttu-id="76781-139">排除 `disk` 外掛程式所收集的所有資料</span><span class="sxs-lookup"><span data-stu-id="76781-139">Exclude all data collected by the `disk` plugin</span></span> |
| `Exclude disk:read,write` |<span data-ttu-id="76781-140">排除來自 `disk` 外掛程式名為 `read` 和 `write` 的來源。</span><span class="sxs-lookup"><span data-stu-id="76781-140">Exclude the sources named `read` and `write` from the `disk` plugin.</span></span> |

<span data-ttu-id="76781-141">以新行分隔個別指示詞。</span><span class="sxs-lookup"><span data-stu-id="76781-141">Separate directives with a newline.</span></span>

## <a name="problems"></a><span data-ttu-id="76781-142">有問題嗎？</span><span class="sxs-lookup"><span data-stu-id="76781-142">Problems?</span></span>
<span data-ttu-id="76781-143">*我在入口網站中看不到任何資料*</span><span class="sxs-lookup"><span data-stu-id="76781-143">*I don't see data in the portal*</span></span>

* <span data-ttu-id="76781-144">開啟[搜尋][diagnostic]以查看原始事件是否已抵達。</span><span class="sxs-lookup"><span data-stu-id="76781-144">Open [Search][diagnostic] to see if the raw events have arrived.</span></span> <span data-ttu-id="76781-145">有時需要較長的時間才會在計量瀏覽器中顯示。</span><span class="sxs-lookup"><span data-stu-id="76781-145">Sometimes they take longer to appear in metrics explorer.</span></span>
* <span data-ttu-id="76781-146">您可能需要 [設定輸出資料的防火牆例外狀況](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="76781-146">You might need to [set firewall exceptions for outgoing data](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="76781-147">在 Application Insights 外掛程式中啟用追蹤。</span><span class="sxs-lookup"><span data-stu-id="76781-147">Enable tracing in the Application Insights plugin.</span></span> <span data-ttu-id="76781-148">在 `<Plugin ApplicationInsightsWriter>`內加入這一行：</span><span class="sxs-lookup"><span data-stu-id="76781-148">Add this line within `<Plugin ApplicationInsightsWriter>`:</span></span>
  * `SDKLogger true`
* <span data-ttu-id="76781-149">開啟終端機，並以詳細資訊模式啟動 collectd，以查看所報告的任何問題：</span><span class="sxs-lookup"><span data-stu-id="76781-149">Open a terminal and start collectd in verbose mode, to see any issues it is reporting:</span></span>
  * `sudo collectd -f`

## <a name="known-issue"></a><span data-ttu-id="76781-150">已知問題</span><span class="sxs-lookup"><span data-stu-id="76781-150">Known issue</span></span>

<span data-ttu-id="76781-151">Application Insights 的「寫入」外掛程式與某些「讀取」外掛程式不相容。</span><span class="sxs-lookup"><span data-stu-id="76781-151">The Application Insights Write plugin is incompatible with certain Read plugins.</span></span> <span data-ttu-id="76781-152">有些外掛程式有時會在 Application Insights 外掛程式預期要有浮點數的位置傳送 "NaN"。</span><span class="sxs-lookup"><span data-stu-id="76781-152">Some plugins sometimes send "NaN" where the Application Insights plugin expects a floating-point number.</span></span>

<span data-ttu-id="76781-153">徵狀：collectd 記錄檔會顯示包含下列資訊的錯誤：「AI: ...SyntaxError: 未預期的權杖 N」。</span><span class="sxs-lookup"><span data-stu-id="76781-153">Symptom: The collectd log shows errors that include "AI: ... SyntaxError: Unexpected token N".</span></span>

<span data-ttu-id="76781-154">因應措施：排除有問題的「寫入」外掛程式所收集的資料。</span><span class="sxs-lookup"><span data-stu-id="76781-154">Workaround: Exclude data collected by the problem Write plugins.</span></span> 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


