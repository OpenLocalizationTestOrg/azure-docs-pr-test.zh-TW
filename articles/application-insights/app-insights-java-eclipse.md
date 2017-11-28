---
title: "aaaGet 開始使用 Azure Application Insights 使用 Eclipse 中的 Java |Microsoft 文件"
description: "使用 hello Eclipse 外掛程式 tooadd 效能和使用量監視 tooyour Java 網站使用 Application Insights"
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: e88c9f53-cd90-4abc-b097-1f170937908e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: 3142a26a9e2d14c2c433882e3d337f2a8c8f2247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a><span data-ttu-id="2c160-103">在 Eclipse 中利用 Java 開始使用 Application Insights</span><span class="sxs-lookup"><span data-stu-id="2c160-103">Get started with Application Insights with Java in Eclipse</span></span>
<span data-ttu-id="2c160-104">hello Application Insights SDK 從 Java web 應用程式傳送遙測，如此您可以分析使用量和效能。</span><span class="sxs-lookup"><span data-stu-id="2c160-104">hello Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span></span> <span data-ttu-id="2c160-105">以便讓您取得超出 hello 方塊遙測，加上您可以使用 toowrite 自訂遙測的 API，hello Eclipse 外掛程式的 Application Insights 會自動將 hello SDK 安裝在您的專案中。</span><span class="sxs-lookup"><span data-stu-id="2c160-105">hello Eclipse plug-in for Application Insights automatically installs hello SDK in your project so that you get out of hello box telemetry, plus an API that you can use toowrite custom telemetry.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="2c160-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="2c160-106">Prerequisites</span></span>
<span data-ttu-id="2c160-107">目前 hello 外掛程式適用於 Maven 專案並在 Eclipse 中的動態 Web 專案。</span><span class="sxs-lookup"><span data-stu-id="2c160-107">Currently hello plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span></span>
<span data-ttu-id="2c160-108">([加入 Application Insights tooother 類型的 Java 專案][java]。)</span><span class="sxs-lookup"><span data-stu-id="2c160-108">([Add Application Insights tooother types of Java project][java].)</span></span>

<span data-ttu-id="2c160-109">您需要：</span><span class="sxs-lookup"><span data-stu-id="2c160-109">You'll need:</span></span>

* <span data-ttu-id="2c160-110">Oracle JRE 1.6 或更新版本</span><span class="sxs-lookup"><span data-stu-id="2c160-110">Oracle JRE 1.6 or later</span></span>
* <span data-ttu-id="2c160-111">訂用帳戶太[Microsoft Azure](https://azure.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="2c160-111">A subscription too[Microsoft Azure](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="2c160-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/)、Indigo 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="2c160-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span></span>
* <span data-ttu-id="2c160-113">Windows 7 或更新版本，或 Windows Server 2008 或更新版本</span><span class="sxs-lookup"><span data-stu-id="2c160-113">Windows 7 or later, or Windows Server 2008 or later</span></span>

## <a name="install-hello-sdk-on-eclipse-one-time"></a><span data-ttu-id="2c160-114">在 Eclipse （一次） 上安裝 hello SDK</span><span class="sxs-lookup"><span data-stu-id="2c160-114">Install hello SDK on Eclipse (one time)</span></span>
<span data-ttu-id="2c160-115">您只需要 toodo 每台電腦一次。</span><span class="sxs-lookup"><span data-stu-id="2c160-115">You only have toodo this one time per machine.</span></span> <span data-ttu-id="2c160-116">這個步驟會安裝可接著將新增 hello SDK tooeach 動態 Web 專案的工具組。</span><span class="sxs-lookup"><span data-stu-id="2c160-116">This step installs a toolkit which can then add hello SDK tooeach Dynamic Web Project.</span></span>

1. <span data-ttu-id="2c160-117">在 Eclipse 中，按一下 說明，然後按一下安裝新軟體。</span><span class="sxs-lookup"><span data-stu-id="2c160-117">In Eclipse, click Help, Install New Software.</span></span>

    ![[說明] -> [安裝新軟體]](./media/app-insights-java-eclipse/0-plugin.png)
2. <span data-ttu-id="2c160-119">hello SDK 處於 http://dl.microsoft.com/eclipse，在 Azure Toolkit。</span><span class="sxs-lookup"><span data-stu-id="2c160-119">hello SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span></span>
3. <span data-ttu-id="2c160-120">取消勾選 **[連絡所有更新網站...]**</span><span class="sxs-lookup"><span data-stu-id="2c160-120">Uncheck **Contact all update sites...**</span></span>

    ![針對 Application Insights SDK，請清除 [連絡所有更新網站]](./media/app-insights-java-eclipse/1-plugin.png)

<span data-ttu-id="2c160-122">請遵循 hello 剩餘步驟，針對每個 Java 專案。</span><span class="sxs-lookup"><span data-stu-id="2c160-122">Follow hello remaining steps for each Java project.</span></span>

## <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="2c160-123">在 Azure 中建立 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="2c160-123">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="2c160-124">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="2c160-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2c160-125">建立新 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="2c160-125">Create a new Application Insights resource.</span></span> <span data-ttu-id="2c160-126">設定 hello 應用程式類型 tooJava web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c160-126">Set hello application type tooJava web application.</span></span>  

    ![按一下 + 並選擇 [Application Insights]](./media/app-insights-java-eclipse/01-create.png)  

4. <span data-ttu-id="2c160-128">尋找 hello hello 新資源的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="2c160-128">Find hello instrumentation key of hello new resource.</span></span> <span data-ttu-id="2c160-129">您將需要 toopaste 此程式碼專案到很快。</span><span class="sxs-lookup"><span data-stu-id="2c160-129">You'll need toopaste this into your code project shortly.</span></span>  

    ![在新資源概觀 hello，按一下 內容並複製 hello 檢測金鑰](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-tooyour-project"></a><span data-ttu-id="2c160-131">將 Application Insights tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="2c160-131">Add Application Insights tooyour project</span></span>
1. <span data-ttu-id="2c160-132">將 Application Insights 從您的 Java web 專案的 hello 內容功能表。</span><span class="sxs-lookup"><span data-stu-id="2c160-132">Add Application Insights from hello context menu of your Java web project.</span></span>

    ![在新資源概觀 hello，按一下 內容並複製 hello 檢測金鑰](./media/app-insights-java-eclipse/02-context-menu.png)
2. <span data-ttu-id="2c160-134">貼上您從 hello Azure 入口網站取得的 hello 檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="2c160-134">Paste hello instrumentation key that you got from hello Azure portal.</span></span>

    ![在新資源概觀 hello，按一下 內容並複製 hello 檢測金鑰](./media/app-insights-java-eclipse/03-ikey.png)

<span data-ttu-id="2c160-136">hello 金鑰會隨每個項目的遙測資料一起傳送，並告知 Application Insights toodisplay 在您的資源。</span><span class="sxs-lookup"><span data-stu-id="2c160-136">hello key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>

## <a name="run-hello-application-and-see-metrics"></a><span data-ttu-id="2c160-137">執行 hello 應用程式，並查看度量</span><span class="sxs-lookup"><span data-stu-id="2c160-137">Run hello application and see metrics</span></span>
<span data-ttu-id="2c160-138">執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c160-138">Run your application.</span></span>

<span data-ttu-id="2c160-139">在 Microsoft Azure 中傳回 tooyour Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="2c160-139">Return tooyour Application Insights resource in Microsoft Azure.</span></span>

<span data-ttu-id="2c160-140">HTTP 要求資料會出現在 hello 概觀刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2c160-140">HTTP requests data will appear on hello overview blade.</span></span> <span data-ttu-id="2c160-141">(如果沒有出現，請稍等片刻，然後按一下重新整理。)</span><span class="sxs-lookup"><span data-stu-id="2c160-141">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![<span data-ttu-id="2c160-142">伺服器回應、要求計數和失敗</span><span class="sxs-lookup"><span data-stu-id="2c160-142">Server response, request counts, and failures</span></span> ](./media/app-insights-java-eclipse/5-results.png)

<span data-ttu-id="2c160-143">按一下 透過任何圖表 toosee 度量詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2c160-143">Click through any chart toosee more detailed metrics.</span></span>

![依名稱的要求計數](./media/app-insights-java-eclipse/6-barchart.png)

<span data-ttu-id="2c160-145">[深入了解度量。][metrics]</span><span class="sxs-lookup"><span data-stu-id="2c160-145">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="2c160-146">與檢視之要求的 hello 屬性，您會看見 hello 遙測事件與它相關聯，例如要求和例外狀況。</span><span class="sxs-lookup"><span data-stu-id="2c160-146">And when viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![此要求的所有追蹤](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a><span data-ttu-id="2c160-148">用戶端遙測</span><span class="sxs-lookup"><span data-stu-id="2c160-148">Client-side telemetry</span></span>
<span data-ttu-id="2c160-149">從 hello 快速入門刀鋒視窗中，按一下 取得程式碼 toomonitor 我的網頁：</span><span class="sxs-lookup"><span data-stu-id="2c160-149">From hello QuickStart blade, click Get code toomonitor my web pages:</span></span>

![在您的應用程式概觀刀鋒視窗中，選擇 [快速啟動]，取得程式碼 toomonitor 我的網頁。](./media/app-insights-java-eclipse/02-monitor-web-page.png)

<span data-ttu-id="2c160-152">中的 HTML 檔案的 hello 開頭插入 hello 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="2c160-152">Insert hello code snippet in hello head of your HTML files.</span></span>

#### <a name="view-client-side-data"></a><span data-ttu-id="2c160-153">檢視用戶端資料</span><span class="sxs-lookup"><span data-stu-id="2c160-153">View client-side data</span></span>
<span data-ttu-id="2c160-154">開啟您已更新的網頁，並使用它們。</span><span class="sxs-lookup"><span data-stu-id="2c160-154">Open your updated web pages and use them.</span></span> <span data-ttu-id="2c160-155">等待一兩分鐘，然後再返回 tooApplication Insights 和開啟 hello 使用量刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2c160-155">Wait a minute or two, then return tooApplication Insights and open hello usage blade.</span></span> <span data-ttu-id="2c160-156">（從 hello 概觀刀鋒視窗中，向下捲動並按一下 使用方式）。</span><span class="sxs-lookup"><span data-stu-id="2c160-156">(From hello Overview blade, scroll down and click Usage.)</span></span>

<span data-ttu-id="2c160-157">頁面檢視、 使用者和工作階段計量會顯示 hello 使用量刀鋒視窗上：</span><span class="sxs-lookup"><span data-stu-id="2c160-157">Page view, user, and session metrics will appear on hello usage blade:</span></span>

![工作階段、使用者和頁面檢視](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

<span data-ttu-id="2c160-159">[深入了解設定用戶端遙測。][usage]</span><span class="sxs-lookup"><span data-stu-id="2c160-159">[Learn more about setting up client-side telemetry.][usage]</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="2c160-160">發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="2c160-160">Publish your application</span></span>
<span data-ttu-id="2c160-161">現在來發行您的應用程式 toohello 伺服器，可讓您使用它，並留意 hello 遙測 hello 入口網站上顯示。</span><span class="sxs-lookup"><span data-stu-id="2c160-161">Now publish your app toohello server, let people use it, and watch hello telemetry show up on hello portal.</span></span>

* <span data-ttu-id="2c160-162">請確定您的防火牆允許應用程式 toosend 遙測 toothese 連接埠：</span><span class="sxs-lookup"><span data-stu-id="2c160-162">Make sure your firewall allows your application toosend telemetry toothese ports:</span></span>

  * <span data-ttu-id="2c160-163">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="2c160-163">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="2c160-164">dc.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="2c160-164">dc.services.visualstudio.com:80</span></span>
  * <span data-ttu-id="2c160-165">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="2c160-165">f5.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="2c160-166">f5.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="2c160-166">f5.services.visualstudio.com:80</span></span>
* <span data-ttu-id="2c160-167">在 Windows 伺服器上，安裝：</span><span class="sxs-lookup"><span data-stu-id="2c160-167">On Windows servers, install:</span></span>

  * [<span data-ttu-id="2c160-168">Microsoft Visual C++ 可轉散發套件</span><span class="sxs-lookup"><span data-stu-id="2c160-168">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="2c160-169">(這會啟用效能計數器。)</span><span class="sxs-lookup"><span data-stu-id="2c160-169">(This enables performance counters.)</span></span>

## <a name="exceptions-and-request-failures"></a><span data-ttu-id="2c160-170">例外狀況與要求失敗</span><span class="sxs-lookup"><span data-stu-id="2c160-170">Exceptions and request failures</span></span>
<span data-ttu-id="2c160-171">會自動收集未處理的例外狀況：</span><span class="sxs-lookup"><span data-stu-id="2c160-171">Unhandled exceptions are automatically collected:</span></span>

![](./media/app-insights-java-eclipse/21-exceptions.png)

<span data-ttu-id="2c160-172">toocollect 資料上的其他例外狀況，您有兩個選項：</span><span class="sxs-lookup"><span data-stu-id="2c160-172">toocollect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="2c160-173">[插入程式碼中呼叫 tooTrackException](app-insights-api-custom-events-metrics.md#trackexception)。</span><span class="sxs-lookup"><span data-stu-id="2c160-173">[Insert calls tooTrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span></span>
* <span data-ttu-id="2c160-174">[在伺服器上安裝 hello Java 代理程式](app-insights-java-agent.md)。</span><span class="sxs-lookup"><span data-stu-id="2c160-174">[Install hello Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="2c160-175">您指定您想要 toowatch hello 方法。</span><span class="sxs-lookup"><span data-stu-id="2c160-175">You specify hello methods you want toowatch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="2c160-176">監視方法呼叫和外部相依性</span><span class="sxs-lookup"><span data-stu-id="2c160-176">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="2c160-177">[安裝 hello Java 代理程式](app-insights-java-agent.md)toolog 指定內部方法與呼叫 JDBC，透過與計時資料。</span><span class="sxs-lookup"><span data-stu-id="2c160-177">[Install hello Java Agent](app-insights-java-agent.md) toolog specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="2c160-178">效能計數器</span><span class="sxs-lookup"><span data-stu-id="2c160-178">Performance counters</span></span>
<span data-ttu-id="2c160-179">在您概觀刀鋒視窗中，向下捲動並按一下 hello**伺服器**磚。</span><span class="sxs-lookup"><span data-stu-id="2c160-179">On your Overview blade, scroll down and click hello  **Servers** tile.</span></span> <span data-ttu-id="2c160-180">您會看到一些效能計數器。</span><span class="sxs-lookup"><span data-stu-id="2c160-180">You'll see a range of performance counters.</span></span>

![捲動 tooclick hello 伺服器 磚](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="2c160-182">自訂效能計數器集合</span><span class="sxs-lookup"><span data-stu-id="2c160-182">Customize performance counter collection</span></span>
<span data-ttu-id="2c160-183">toodisable hello 組標準的效能計數器集合加入下列程式碼的 hello ApplicationInsights.xml 檔案 hello 根節點下的 hello:</span><span class="sxs-lookup"><span data-stu-id="2c160-183">toodisable collection of hello standard set of performance counters, add hello following code under hello root node of hello ApplicationInsights.xml file:</span></span>

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="2c160-184">收集其他效能計數器</span><span class="sxs-lookup"><span data-stu-id="2c160-184">Collect additional performance counters</span></span>
<span data-ttu-id="2c160-185">您可以指定收集其他效能計數器 toobe。</span><span class="sxs-lookup"><span data-stu-id="2c160-185">You can specify additional performance counters toobe collected.</span></span>

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a><span data-ttu-id="2c160-186">JMX 計數器 （由 hello Java 虛擬機器）</span><span class="sxs-lookup"><span data-stu-id="2c160-186">JMX counters (exposed by hello Java Virtual Machine)</span></span>

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="2c160-187">`displayName`– hello hello Application Insights 入口網站中顯示的名稱。</span><span class="sxs-lookup"><span data-stu-id="2c160-187">`displayName` – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="2c160-188">`objectName`– hello JMX 物件名稱。</span><span class="sxs-lookup"><span data-stu-id="2c160-188">`objectName` – hello JMX object name.</span></span>
* <span data-ttu-id="2c160-189">`attribute`– hello JMX 物件名稱 toofetch hello 屬性</span><span class="sxs-lookup"><span data-stu-id="2c160-189">`attribute` – hello attribute of hello JMX object name toofetch</span></span>
* <span data-ttu-id="2c160-190">`type`（選用）-hello JMX 物件屬性的型別：</span><span class="sxs-lookup"><span data-stu-id="2c160-190">`type` (optional) - hello type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="2c160-191">預設值：簡易類型，例如 int 或 long。</span><span class="sxs-lookup"><span data-stu-id="2c160-191">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="2c160-192">`composite`: hello 的效能計數器資料的格式的 'Attribute.Data' hello</span><span class="sxs-lookup"><span data-stu-id="2c160-192">`composite`: hello perf counter data is in hello format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="2c160-193">`tabular`: hello 的效能計數器資料的資料表資料列的 hello 格式</span><span class="sxs-lookup"><span data-stu-id="2c160-193">`tabular`: hello perf counter data is in hello format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="2c160-194">Windows 效能計數器</span><span class="sxs-lookup"><span data-stu-id="2c160-194">Windows performance counters</span></span>
<span data-ttu-id="2c160-195">每個[Windows 效能計數器](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx)類別目錄的成員 (在 hello 欄位是類別成員一樣)。</span><span class="sxs-lookup"><span data-stu-id="2c160-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in hello same way that a field is a member of a class).</span></span> <span data-ttu-id="2c160-196">類別可以是全域，或可以有一定數量或指定的執行個體。</span><span class="sxs-lookup"><span data-stu-id="2c160-196">Categories can either be global, or can have numbered or named instances.</span></span>

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="2c160-197">displayName-hello hello Application Insights 入口網站中顯示的名稱。</span><span class="sxs-lookup"><span data-stu-id="2c160-197">displayName – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="2c160-198">categoryName – hello 效能計數器分類 （效能物件） 與此效能計數器相關聯。</span><span class="sxs-lookup"><span data-stu-id="2c160-198">categoryName – hello performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="2c160-199">counterName – hello hello 效能計數器名稱。</span><span class="sxs-lookup"><span data-stu-id="2c160-199">counterName – hello name of hello performance counter.</span></span>
* <span data-ttu-id="2c160-200">instanceName – hello hello 效能計數器類別執行個體名稱或空字串 ("")，如果 hello 類別包含單一執行個體。</span><span class="sxs-lookup"><span data-stu-id="2c160-200">instanceName – hello name of hello performance counter category instance, or an empty string (""), if hello category contains a single instance.</span></span> <span data-ttu-id="2c160-201">如果 hello categoryName 是程序，而您想要 toocollect hello 效能計數器從 hello 目前 JVM 程序上執行您的應用程式中，指定`"__SELF__"`。</span><span class="sxs-lookup"><span data-stu-id="2c160-201">If hello categoryName is Process, and hello performance counter you'd like toocollect is from hello current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="2c160-202">您的效能計數器會在[計量瀏覽器][metrics]中以自訂度量的形式顯示。</span><span class="sxs-lookup"><span data-stu-id="2c160-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="2c160-203">Unix 效能計數器</span><span class="sxs-lookup"><span data-stu-id="2c160-203">Unix performance counters</span></span>
* <span data-ttu-id="2c160-204">[安裝與 hello Application Insights 外掛程式 collectd](app-insights-java-collectd.md) tooget 各種系統和網路的資料。</span><span class="sxs-lookup"><span data-stu-id="2c160-204">[Install collectd with hello Application Insights plugin](app-insights-java-collectd.md) tooget a wide variety of system and network data.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="2c160-205">可用性 Web 測試</span><span class="sxs-lookup"><span data-stu-id="2c160-205">Availability web tests</span></span>
<span data-ttu-id="2c160-206">Application Insights 可以測試您的網站在它已啟動的定期間隔 toocheck 和回應格式。</span><span class="sxs-lookup"><span data-stu-id="2c160-206">Application Insights can test your website at regular intervals toocheck that it's up and responding well.</span></span> <span data-ttu-id="2c160-207">[向上 tooset][availability]，捲動 tooclick 可用性。</span><span class="sxs-lookup"><span data-stu-id="2c160-207">[tooset up][availability], scroll down tooclick Availability.</span></span>

![向下捲動，並依序按一下 [可用性]、[加入 Web 測試]](./media/app-insights-java-eclipse/31-config-web-test.png)

<span data-ttu-id="2c160-209">您將取得回應時間的圖表，以及若網站關閉還會取得電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="2c160-209">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Web 測試範例](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

<span data-ttu-id="2c160-211">[深入了解 Web 測試的可用性。][availability]</span><span class="sxs-lookup"><span data-stu-id="2c160-211">[Learn more about availability web tests.][availability]</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="2c160-212">診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="2c160-212">Diagnostic logs</span></span>
<span data-ttu-id="2c160-213">如果您使用 Logback 或 Log4J （v1.2 或 v2.0） 進行追蹤，您可以將自動傳送 tooApplication Insights，您可以在其中瀏覽並在其上搜尋程式追蹤記錄。</span><span class="sxs-lookup"><span data-stu-id="2c160-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically tooApplication Insights where you can explore and search on them.</span></span>

<span data-ttu-id="2c160-214">[深入了解診斷記錄][javalogs]</span><span class="sxs-lookup"><span data-stu-id="2c160-214">[Learn more about diagnostic logs][javalogs]</span></span>

## <a name="custom-telemetry"></a><span data-ttu-id="2c160-215">自訂遙測</span><span class="sxs-lookup"><span data-stu-id="2c160-215">Custom telemetry</span></span>
<span data-ttu-id="2c160-216">在使用者與它的行為時您 Java web 應用程式 toofind 中插入幾行程式碼或 toohelp 診斷問題。</span><span class="sxs-lookup"><span data-stu-id="2c160-216">Insert a few lines of code in your Java web application toofind out what users are doing with it or toohelp diagnose problems.</span></span>

<span data-ttu-id="2c160-217">在網頁 JavaScript 和 hello 伺服器端 Java 中，您可以插入程式碼。</span><span class="sxs-lookup"><span data-stu-id="2c160-217">You can insert code both in web page JavaScript and in hello server-side Java.</span></span>

<span data-ttu-id="2c160-218">[了解自訂遙測][track]</span><span class="sxs-lookup"><span data-stu-id="2c160-218">[Learn about custom telemetry][track]</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c160-219">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2c160-219">Next steps</span></span>
#### <a name="detect-and-diagnose-issues"></a><span data-ttu-id="2c160-220">偵測並診斷問題</span><span class="sxs-lookup"><span data-stu-id="2c160-220">Detect and diagnose issues</span></span>
* <span data-ttu-id="2c160-221">[新增 web 用戶端遙測][ usage] tooget hello web 用戶端效能遙測資料。</span><span class="sxs-lookup"><span data-stu-id="2c160-221">[Add web client telemetry][usage] tooget performance telemetry from hello web client.</span></span>
* <span data-ttu-id="2c160-222">[設定 web 測試][ availability] toomake 即時且回應迅速，保持您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c160-222">[Set up web tests][availability] toomake sure your application stays live and responsive.</span></span>
* <span data-ttu-id="2c160-223">[搜尋事件和記錄檔][ diagnostic] toohelp 診斷問題。</span><span class="sxs-lookup"><span data-stu-id="2c160-223">[Search events and logs][diagnostic] toohelp diagnose problems.</span></span>
* <span data-ttu-id="2c160-224">[擷取 Log4J 或 Logback 追蹤][javalogs]</span><span class="sxs-lookup"><span data-stu-id="2c160-224">[Capture Log4J or Logback traces][javalogs]</span></span>

#### <a name="track-usage"></a><span data-ttu-id="2c160-225">追蹤流量</span><span class="sxs-lookup"><span data-stu-id="2c160-225">Track usage</span></span>
* <span data-ttu-id="2c160-226">[新增 web 用戶端遙測][ usage] toomonitor 頁面上，檢視和基本使用者度量。</span><span class="sxs-lookup"><span data-stu-id="2c160-226">[Add web client telemetry][usage] toomonitor page views and basic user metrics.</span></span>
* <span data-ttu-id="2c160-227">[追蹤的自訂事件和度量](app-insights-web-track-usage.md)toolearn 有關您的應用程式使用方式，在 hello 用戶端和伺服器 hello。</span><span class="sxs-lookup"><span data-stu-id="2c160-227">[Track custom events and metrics](app-insights-web-track-usage.md) toolearn about how your application is used, both at hello client and hello server.</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
