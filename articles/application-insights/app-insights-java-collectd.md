---
title: "aaaMonitor on Linux 的 Azure 的 Java web 應用程式效能 |Microsoft 文件"
description: "擴充應用程式效能監視您的 Java 網站以 hello CollectD 外掛程式的 Application Insights。"
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
ms.openlocfilehash: f783e8607a83b2b43f67d3a2fc20f100aa2f75ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a><span data-ttu-id="adb97-103">collectd：Application Insights 中的 Linux 效能計量</span><span class="sxs-lookup"><span data-stu-id="adb97-103">collectd: Linux performance metrics in Application Insights</span></span>


<span data-ttu-id="adb97-104">tooexplore Linux 系統中的效能標準[Application Insights](app-insights-overview.md)，安裝[collectd](http://collectd.org/)搭配其 Application Insights 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="adb97-104">tooexplore Linux system performance metrics in [Application Insights](app-insights-overview.md), install [collectd](http://collectd.org/), together with its Application Insights plug-in.</span></span> <span data-ttu-id="adb97-105">這個開放原始碼解決方案會收集各種系統和網路統計資料。</span><span class="sxs-lookup"><span data-stu-id="adb97-105">This open-source solution gathers various system and network statistics.</span></span>

<span data-ttu-id="adb97-106">如果您已[使用 Application Insights 檢測您的 Java Web 服務][java]，通常您會使用 collectd。</span><span class="sxs-lookup"><span data-stu-id="adb97-106">Typically you'll use collectd if you have already [instrumented your Java web service with Application Insights][java].</span></span> <span data-ttu-id="adb97-107">它可讓您更多資料 toohelp 您 tooenhance 應用程式效能或診斷問題。</span><span class="sxs-lookup"><span data-stu-id="adb97-107">It gives you more data toohelp you tooenhance your app's performance or diagnose problems.</span></span> 

![範例圖表](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a><span data-ttu-id="adb97-109">取得檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="adb97-109">Get your instrumentation key</span></span>
<span data-ttu-id="adb97-110">在 hello [Microsoft Azure 入口網站](https://portal.azure.com)，開啟 hello [Application Insights](app-insights-overview.md)想 hello 資料 tooappear 資源。</span><span class="sxs-lookup"><span data-stu-id="adb97-110">In hello [Microsoft Azure portal](https://portal.azure.com), open hello [Application Insights](app-insights-overview.md) resource where you want hello data tooappear.</span></span> <span data-ttu-id="adb97-111">(或[建立新的資源](app-insights-create-new-resource.md)。)</span><span class="sxs-lookup"><span data-stu-id="adb97-111">(Or [create a new resource](app-insights-create-new-resource.md).)</span></span>

<span data-ttu-id="adb97-112">製作 hello 檢測金鑰識別 hello 資源的複本。</span><span class="sxs-lookup"><span data-stu-id="adb97-112">Take a copy of hello instrumentation key, which identifies hello resource.</span></span>

![全部瀏覽，開啟您的資源，然後在 hello Essentials 下拉式清單中，select 和複製 hello 檢測金鑰](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-hello-plug-in"></a><span data-ttu-id="adb97-114">安裝 collectd 和 hello 外掛程式</span><span class="sxs-lookup"><span data-stu-id="adb97-114">Install collectd and hello plug-in</span></span>
<span data-ttu-id="adb97-115">在您的 Linux 伺服器機器上：</span><span class="sxs-lookup"><span data-stu-id="adb97-115">On your Linux server machines:</span></span>

1. <span data-ttu-id="adb97-116">安裝 [collectd](http://collectd.org/) 5.4.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="adb97-116">Install [collectd](http://collectd.org/) version 5.4.0 or later.</span></span>
2. <span data-ttu-id="adb97-117">下載 hello [collectd 寫入器的 Application Insights 外掛程式](https://aka.ms/aijavasdk)。</span><span class="sxs-lookup"><span data-stu-id="adb97-117">Download hello [Application Insights collectd writer plugin](https://aka.ms/aijavasdk).</span></span> <span data-ttu-id="adb97-118">請注意 hello 版本號碼。</span><span class="sxs-lookup"><span data-stu-id="adb97-118">Note hello version number.</span></span>
3. <span data-ttu-id="adb97-119">複製 hello 外掛程式 JAR 到`/usr/share/collectd/java`。</span><span class="sxs-lookup"><span data-stu-id="adb97-119">Copy hello plugin JAR into `/usr/share/collectd/java`.</span></span>
4. <span data-ttu-id="adb97-120">編輯 `/etc/collectd/collectd.conf`：</span><span class="sxs-lookup"><span data-stu-id="adb97-120">Edit `/etc/collectd/collectd.conf`:</span></span>
   * <span data-ttu-id="adb97-121">請確認[hello Java 外掛程式](https://collectd.org/wiki/index.php/Plugin:Java)已啟用。</span><span class="sxs-lookup"><span data-stu-id="adb97-121">Ensure that [hello Java plugin](https://collectd.org/wiki/index.php/Plugin:Java) is enabled.</span></span>
   * <span data-ttu-id="adb97-122">更新下列 JAR hello java.class.path tooinclude hello JVMArg。</span><span class="sxs-lookup"><span data-stu-id="adb97-122">Update hello JVMArg for hello java.class.path tooinclude hello following JAR.</span></span> <span data-ttu-id="adb97-123">更新 hello 版本號碼 toomatch hello 您下載：</span><span class="sxs-lookup"><span data-stu-id="adb97-123">Update hello version number toomatch hello one you downloaded:</span></span>
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * <span data-ttu-id="adb97-124">加入此程式碼片段使用 hello 檢測金鑰從您的資源：</span><span class="sxs-lookup"><span data-stu-id="adb97-124">Add this snippet, using hello Instrumentation Key from your resource:</span></span>

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

<span data-ttu-id="adb97-125">以下是範例組態檔的一部分：</span><span class="sxs-lookup"><span data-stu-id="adb97-125">Here's part of a sample configuration file:</span></span>

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

<span data-ttu-id="adb97-126">設定其他 [collectd 外掛程式](https://collectd.org/wiki/index.php/Table_of_Plugins)，它可以從不同來源收集各種資料。</span><span class="sxs-lookup"><span data-stu-id="adb97-126">Configure other [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), which can collect various data from different sources.</span></span>

<span data-ttu-id="adb97-127">重新啟動 collectd 根據 tooits[手動](https://collectd.org/wiki/index.php/First_steps)。</span><span class="sxs-lookup"><span data-stu-id="adb97-127">Restart collectd according tooits [manual](https://collectd.org/wiki/index.php/First_steps).</span></span>

## <a name="view-hello-data-in-application-insights"></a><span data-ttu-id="adb97-128">檢視 Application Insights 中的 hello 資料</span><span class="sxs-lookup"><span data-stu-id="adb97-128">View hello data in Application Insights</span></span>
<span data-ttu-id="adb97-129">在 Application Insights 資源中，開啟[計量瀏覽器和新增圖表][metrics]，您想從 hello 自訂分類 toosee 選取 hello 度量。</span><span class="sxs-lookup"><span data-stu-id="adb97-129">In your Application Insights resource, open [Metrics Explorer and add charts][metrics], selecting hello metrics you want toosee from hello Custom category.</span></span>

![](./media/app-insights-java-collectd/result.png)

<span data-ttu-id="adb97-130">根據預設，會彙總從中 hello 計量所收集的所有主機電腦上的 hello 度量。</span><span class="sxs-lookup"><span data-stu-id="adb97-130">By default, hello metrics are aggregated across all host machines from which hello metrics were collected.</span></span> <span data-ttu-id="adb97-131">tooview hello 度量，每個主機，在 hello 圖表詳細資料 刀鋒視窗，開啟 群組，然後選擇 toogroup CollectD 主機。</span><span class="sxs-lookup"><span data-stu-id="adb97-131">tooview hello metrics per host, in hello Chart details blade, turn on Grouping and then choose toogroup by CollectD-Host.</span></span>

## <a name="tooexclude-upload-of-specific-statistics"></a><span data-ttu-id="adb97-132">tooexclude 上傳的特定統計資料</span><span class="sxs-lookup"><span data-stu-id="adb97-132">tooexclude upload of specific statistics</span></span>
<span data-ttu-id="adb97-133">根據預設，hello Application Insights 外掛程式會傳送 hello 讀取所有資料收集的所有啟用的 hello collectd' ' 的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="adb97-133">By default, hello Application Insights plugin sends all hello data collected by all hello enabled collectd 'read' plugins.</span></span> 

<span data-ttu-id="adb97-134">從特定的外掛程式或資料來源的 tooexclude 資料：</span><span class="sxs-lookup"><span data-stu-id="adb97-134">tooexclude data from specific plugins or data sources:</span></span>

* <span data-ttu-id="adb97-135">編輯 hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="adb97-135">Edit hello configuration file.</span></span> 
* <span data-ttu-id="adb97-136">在 `<Plugin ApplicationInsightsWriter>`中，加入指示詞行，如下所示：</span><span class="sxs-lookup"><span data-stu-id="adb97-136">In `<Plugin ApplicationInsightsWriter>`, add directive lines like this:</span></span>

| <span data-ttu-id="adb97-137">指示詞</span><span class="sxs-lookup"><span data-stu-id="adb97-137">Directive</span></span> | <span data-ttu-id="adb97-138">效果</span><span class="sxs-lookup"><span data-stu-id="adb97-138">Effect</span></span> |
| --- | --- |
| `Exclude disk` |<span data-ttu-id="adb97-139">排除所有的資料收集的 hello`disk`外掛程式</span><span class="sxs-lookup"><span data-stu-id="adb97-139">Exclude all data collected by hello `disk` plugin</span></span> |
| `Exclude disk:read,write` |<span data-ttu-id="adb97-140">排除 hello 來源名為`read`和`write`從 hello`disk`外掛程式。</span><span class="sxs-lookup"><span data-stu-id="adb97-140">Exclude hello sources named `read` and `write` from hello `disk` plugin.</span></span> |

<span data-ttu-id="adb97-141">以新行分隔個別指示詞。</span><span class="sxs-lookup"><span data-stu-id="adb97-141">Separate directives with a newline.</span></span>

## <a name="problems"></a><span data-ttu-id="adb97-142">有問題嗎？</span><span class="sxs-lookup"><span data-stu-id="adb97-142">Problems?</span></span>
<span data-ttu-id="adb97-143">*我沒看到 hello 入口網站中的資料*</span><span class="sxs-lookup"><span data-stu-id="adb97-143">*I don't see data in hello portal*</span></span>

* <span data-ttu-id="adb97-144">開啟[搜尋][ diagnostic] toosee 如果已到達 hello 未經處理的事件。</span><span class="sxs-lookup"><span data-stu-id="adb97-144">Open [Search][diagnostic] toosee if hello raw events have arrived.</span></span> <span data-ttu-id="adb97-145">有時候會更長的 tooappear 在計量瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="adb97-145">Sometimes they take longer tooappear in metrics explorer.</span></span>
* <span data-ttu-id="adb97-146">您可能需要[設定為外送資料的防火牆例外狀況](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="adb97-146">You might need too[set firewall exceptions for outgoing data](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="adb97-147">啟用 hello Application Insights 外掛程式中的追蹤。</span><span class="sxs-lookup"><span data-stu-id="adb97-147">Enable tracing in hello Application Insights plugin.</span></span> <span data-ttu-id="adb97-148">在 `<Plugin ApplicationInsightsWriter>`內加入這一行：</span><span class="sxs-lookup"><span data-stu-id="adb97-148">Add this line within `<Plugin ApplicationInsightsWriter>`:</span></span>
  * `SDKLogger true`
* <span data-ttu-id="adb97-149">開啟終端機，然後開始 collectd 詳細模式，toosee 它報告任何問題：</span><span class="sxs-lookup"><span data-stu-id="adb97-149">Open a terminal and start collectd in verbose mode, toosee any issues it is reporting:</span></span>
  * `sudo collectd -f`

## <a name="known-issue"></a><span data-ttu-id="adb97-150">已知問題</span><span class="sxs-lookup"><span data-stu-id="adb97-150">Known issue</span></span>

<span data-ttu-id="adb97-151">hello 應用程式 Insights 寫入外掛程式是與特定讀取外掛程式不相容。</span><span class="sxs-lookup"><span data-stu-id="adb97-151">hello Application Insights Write plugin is incompatible with certain Read plugins.</span></span> <span data-ttu-id="adb97-152">某些外掛程式有時會傳送 hello Application Insights 外掛程式，必須要有浮點數"NaN"。</span><span class="sxs-lookup"><span data-stu-id="adb97-152">Some plugins sometimes send "NaN" where hello Application Insights plugin expects a floating-point number.</span></span>

<span data-ttu-id="adb97-153">徵兆： hello collectd 記錄檔會顯示錯誤，包括 「 AI::...SyntaxError: 未預期的權杖 N」。</span><span class="sxs-lookup"><span data-stu-id="adb97-153">Symptom: hello collectd log shows errors that include "AI: ... SyntaxError: Unexpected token N".</span></span>

<span data-ttu-id="adb97-154">因應措施： 排除 hello 問題寫入外掛程式所收集的資料。</span><span class="sxs-lookup"><span data-stu-id="adb97-154">Workaround: Exclude data collected by hello problem Write plugins.</span></span> 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


