---
title: "在 Eclipse 中利用 Java 開始使用 Application Insights | Microsoft Docs"
description: "使用 Eclipse 外掛程式來加入效能和使用量計數器監視到您使用 Application Insights 的 Java 網站"
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
ms.openlocfilehash: f2f696a3bbe7893c1f521a3e5588f4f93805d6a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a><span data-ttu-id="0d0fa-103">在 Eclipse 中利用 Java 開始使用 Application Insights</span><span class="sxs-lookup"><span data-stu-id="0d0fa-103">Get started with Application Insights with Java in Eclipse</span></span>
<span data-ttu-id="0d0fa-104">Application Insights SDK 會透過 Java Web 應用程式傳送遙測，使得您可以分析使用量和效能。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-104">The Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span></span> <span data-ttu-id="0d0fa-105">Application Insights 適用的 Eclipse 外掛程式會自動在您的專案中安裝 SDK，使得您可以取得內建的遙測，加上可以用來編寫自訂遙測的 API。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-105">The Eclipse plug-in for Application Insights automatically installs the SDK in your project so that you get out of the box telemetry, plus an API that you can use to write custom telemetry.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="0d0fa-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="0d0fa-106">Prerequisites</span></span>
<span data-ttu-id="0d0fa-107">目前外掛程式可用於 Eclipse 中的 Maven 專案和動態網站專案。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-107">Currently the plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span></span>
<span data-ttu-id="0d0fa-108">([將 Application Insights 新增至其他類型的 Java 專案][java]。)</span><span class="sxs-lookup"><span data-stu-id="0d0fa-108">([Add Application Insights to other types of Java project][java].)</span></span>

<span data-ttu-id="0d0fa-109">您需要：</span><span class="sxs-lookup"><span data-stu-id="0d0fa-109">You'll need:</span></span>

* <span data-ttu-id="0d0fa-110">Oracle JRE 1.6 或更新版本</span><span class="sxs-lookup"><span data-stu-id="0d0fa-110">Oracle JRE 1.6 or later</span></span>
* <span data-ttu-id="0d0fa-111">[Microsoft Azure](https://azure.microsoft.com/)訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-111">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="0d0fa-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/)、Indigo 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span></span>
* <span data-ttu-id="0d0fa-113">Windows 7 或更新版本，或 Windows Server 2008 或更新版本</span><span class="sxs-lookup"><span data-stu-id="0d0fa-113">Windows 7 or later, or Windows Server 2008 or later</span></span>

## <a name="install-the-sdk-on-eclipse-one-time"></a><span data-ttu-id="0d0fa-114">在 Eclipse 上安裝 SDK (一次)</span><span class="sxs-lookup"><span data-stu-id="0d0fa-114">Install the SDK on Eclipse (one time)</span></span>
<span data-ttu-id="0d0fa-115">您只需在每一部機器上執行一次此動作。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-115">You only have to do this one time per machine.</span></span> <span data-ttu-id="0d0fa-116">此步驟會安裝工具組，然後工具組會將 SDK 加入到每個動態網站專案。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-116">This step installs a toolkit which can then add the SDK to each Dynamic Web Project.</span></span>

1. <span data-ttu-id="0d0fa-117">在 Eclipse 中，按一下 [說明]，然後按一下 [安裝新軟體]。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-117">In Eclipse, click Help, Install New Software.</span></span>

    ![[說明] -> [安裝新軟體]](./media/app-insights-java-eclipse/0-plugin.png)
2. <span data-ttu-id="0d0fa-119">SDK 位於 http://dl.microsoft.com/eclipse 中 Azure 工具組底下。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-119">The SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span></span>
3. <span data-ttu-id="0d0fa-120">取消勾選 **[連絡所有更新網站...]**</span><span class="sxs-lookup"><span data-stu-id="0d0fa-120">Uncheck **Contact all update sites...**</span></span>

    ![針對 Application Insights SDK，請清除 [連絡所有更新網站]](./media/app-insights-java-eclipse/1-plugin.png)

<span data-ttu-id="0d0fa-122">對每個 Java 專案遵循其餘的步驟。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-122">Follow the remaining steps for each Java project.</span></span>

## <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="0d0fa-123">在 Azure 中建立 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="0d0fa-123">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="0d0fa-124">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0d0fa-125">建立新 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-125">Create a new Application Insights resource.</span></span> <span data-ttu-id="0d0fa-126">將應用程式類型設定為 Java Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-126">Set the application type to Java web application.</span></span>  

    ![按一下 + 並選擇 [Application Insights]](./media/app-insights-java-eclipse/01-create.png)  

4. <span data-ttu-id="0d0fa-128">尋找新資源的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-128">Find the instrumentation key of the new resource.</span></span> <span data-ttu-id="0d0fa-129">您很快需要將此資訊貼上到程式碼專案中。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-129">You'll need to paste this into your code project shortly.</span></span>  

    ![在新資源概觀中，按一下 [屬性] 並複製檢測金鑰](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-to-your-project"></a><span data-ttu-id="0d0fa-131">將 Application Insights 加入至專案</span><span class="sxs-lookup"><span data-stu-id="0d0fa-131">Add Application Insights to your project</span></span>
1. <span data-ttu-id="0d0fa-132">從 Java Web 專案的內容功能表將 Application Insights 加入。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-132">Add Application Insights from the context menu of your Java web project.</span></span>

    ![在新資源概觀中，按一下 [屬性] 並複製檢測金鑰](./media/app-insights-java-eclipse/02-context-menu.png)
2. <span data-ttu-id="0d0fa-134">將您從 Azure 入口網站取得的檢測金鑰貼上。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-134">Paste the instrumentation key that you got from the Azure portal.</span></span>

    ![在新資源概觀中，按一下 [屬性] 並複製檢測金鑰](./media/app-insights-java-eclipse/03-ikey.png)

<span data-ttu-id="0d0fa-136">金鑰會隨著遙測的每個項目傳送，並告知 Application Insights 在您的資源中顯示它。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-136">The key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>

## <a name="run-the-application-and-see-metrics"></a><span data-ttu-id="0d0fa-137">執行應用程式並查看度量</span><span class="sxs-lookup"><span data-stu-id="0d0fa-137">Run the application and see metrics</span></span>
<span data-ttu-id="0d0fa-138">執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-138">Run your application.</span></span>

<span data-ttu-id="0d0fa-139">返回 Microsoft Azure 中的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-139">Return to your Application Insights resource in Microsoft Azure.</span></span>

<span data-ttu-id="0d0fa-140">[概觀] 分頁上會顯示 HTTP 要求資料。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-140">HTTP requests data will appear on the overview blade.</span></span> <span data-ttu-id="0d0fa-141">(如果沒有出現，請稍等片刻，然後按一下 [重新整理]。)</span><span class="sxs-lookup"><span data-stu-id="0d0fa-141">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![<span data-ttu-id="0d0fa-142">伺服器回應、要求計數和失敗</span><span class="sxs-lookup"><span data-stu-id="0d0fa-142">Server response, request counts, and failures</span></span> ](./media/app-insights-java-eclipse/5-results.png)

<span data-ttu-id="0d0fa-143">逐一點選任何圖表以查看更詳細的度量。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-143">Click through any chart to see more detailed metrics.</span></span>

![依名稱的要求計數](./media/app-insights-java-eclipse/6-barchart.png)

<span data-ttu-id="0d0fa-145">[深入了解度量。][metrics]</span><span class="sxs-lookup"><span data-stu-id="0d0fa-145">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="0d0fa-146">而檢視要求的屬性時，您可以查看與它關聯的遙測事件，例如要求和例外狀況。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![此要求的所有追蹤](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a><span data-ttu-id="0d0fa-148">用戶端遙測</span><span class="sxs-lookup"><span data-stu-id="0d0fa-148">Client-side telemetry</span></span>
<span data-ttu-id="0d0fa-149">在 [快速啟動] 刀鋒視窗中，按一下 [取得程式碼] 來監視我的網頁：</span><span class="sxs-lookup"><span data-stu-id="0d0fa-149">From the QuickStart blade, click Get code to monitor my web pages:</span></span>

![在您的應用程式概觀刀鋒視窗中，選擇 [快速入門]，取得程式碼以監視我的網頁。](./media/app-insights-java-eclipse/02-monitor-web-page.png)

<span data-ttu-id="0d0fa-152">在 HTML 檔案的標頭插入程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-152">Insert the code snippet in the head of your HTML files.</span></span>

#### <a name="view-client-side-data"></a><span data-ttu-id="0d0fa-153">檢視用戶端資料</span><span class="sxs-lookup"><span data-stu-id="0d0fa-153">View client-side data</span></span>
<span data-ttu-id="0d0fa-154">開啟您已更新的網頁，並使用它們。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-154">Open your updated web pages and use them.</span></span> <span data-ttu-id="0d0fa-155">等待一、兩分鐘，然後回到 Application Insights，並開啟 [使用量] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-155">Wait a minute or two, then return to Application Insights and open the usage blade.</span></span> <span data-ttu-id="0d0fa-156">(從 [概觀] 刀鋒視窗上，向下捲動並按一下 [自使用量]。)</span><span class="sxs-lookup"><span data-stu-id="0d0fa-156">(From the Overview blade, scroll down and click Usage.)</span></span>

<span data-ttu-id="0d0fa-157">頁面檢視、使用者和工作階段度量將出現在 [使用量] 刀鋒視窗上：</span><span class="sxs-lookup"><span data-stu-id="0d0fa-157">Page view, user, and session metrics will appear on the usage blade:</span></span>

![工作階段、使用者和頁面檢視](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

<span data-ttu-id="0d0fa-159">[深入了解設定用戶端遙測。][usage]</span><span class="sxs-lookup"><span data-stu-id="0d0fa-159">[Learn more about setting up client-side telemetry.][usage]</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="0d0fa-160">發行您的應用程式</span><span class="sxs-lookup"><span data-stu-id="0d0fa-160">Publish your application</span></span>
<span data-ttu-id="0d0fa-161">現在將您的應用程式發佈至伺服器供人使用，然後查看入口網站顯示的遙測。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-161">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span></span>

* <span data-ttu-id="0d0fa-162">請確定您的防火牆允許應用程式將遙測傳送至這些連接埠：</span><span class="sxs-lookup"><span data-stu-id="0d0fa-162">Make sure your firewall allows your application to send telemetry to these ports:</span></span>

  * <span data-ttu-id="0d0fa-163">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="0d0fa-163">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="0d0fa-164">dc.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="0d0fa-164">dc.services.visualstudio.com:80</span></span>
  * <span data-ttu-id="0d0fa-165">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="0d0fa-165">f5.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="0d0fa-166">f5.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="0d0fa-166">f5.services.visualstudio.com:80</span></span>
* <span data-ttu-id="0d0fa-167">在 Windows 伺服器上，安裝：</span><span class="sxs-lookup"><span data-stu-id="0d0fa-167">On Windows servers, install:</span></span>

  * [<span data-ttu-id="0d0fa-168">Microsoft Visual C++ 可轉散發套件</span><span class="sxs-lookup"><span data-stu-id="0d0fa-168">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="0d0fa-169">(這會啟用效能計數器。)</span><span class="sxs-lookup"><span data-stu-id="0d0fa-169">(This enables performance counters.)</span></span>

## <a name="exceptions-and-request-failures"></a><span data-ttu-id="0d0fa-170">例外狀況與要求失敗</span><span class="sxs-lookup"><span data-stu-id="0d0fa-170">Exceptions and request failures</span></span>
<span data-ttu-id="0d0fa-171">會自動收集未處理的例外狀況：</span><span class="sxs-lookup"><span data-stu-id="0d0fa-171">Unhandled exceptions are automatically collected:</span></span>

![](./media/app-insights-java-eclipse/21-exceptions.png)

<span data-ttu-id="0d0fa-172">若要收集其他例外狀況的資料，您有兩個選項：</span><span class="sxs-lookup"><span data-stu-id="0d0fa-172">To collect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="0d0fa-173">[在您的程式碼中插入 TrackException 的呼叫](app-insights-api-custom-events-metrics.md#trackexception)。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-173">[Insert calls to TrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span></span>
* <span data-ttu-id="0d0fa-174">[在伺服器上安裝 Java 代理程式](app-insights-java-agent.md)。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-174">[Install the Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="0d0fa-175">指定您想要觀看的方法。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-175">You specify the methods you want to watch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="0d0fa-176">監視方法呼叫和外部相依性</span><span class="sxs-lookup"><span data-stu-id="0d0fa-176">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="0d0fa-177">[安裝 Java 代理程式](app-insights-java-agent.md) 以記錄指定的內部方法和透過 JDBC 發出的呼叫與計時資料。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-177">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="0d0fa-178">效能計數器</span><span class="sxs-lookup"><span data-stu-id="0d0fa-178">Performance counters</span></span>
<span data-ttu-id="0d0fa-179">在您的 [概觀] 刀鋒視窗上，向下捲動，然後按一下 [伺服器] 磚。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-179">On your Overview blade, scroll down and click the  **Servers** tile.</span></span> <span data-ttu-id="0d0fa-180">您會看到一些效能計數器。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-180">You'll see a range of performance counters.</span></span>

![向下捲動，按一下 [伺服器] 磚](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="0d0fa-182">自訂效能計數器集合</span><span class="sxs-lookup"><span data-stu-id="0d0fa-182">Customize performance counter collection</span></span>
<span data-ttu-id="0d0fa-183">若要停用效能計數器的一組標準集合，請將下列程式碼加入 ApplicationInsights.xml 檔案的根節點下：</span><span class="sxs-lookup"><span data-stu-id="0d0fa-183">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span></span>

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="0d0fa-184">收集其他效能計數器</span><span class="sxs-lookup"><span data-stu-id="0d0fa-184">Collect additional performance counters</span></span>
<span data-ttu-id="0d0fa-185">您可以指定要收集的其他效能計數器。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-185">You can specify additional performance counters to be collected.</span></span>

#### <a name="jmx-counters-exposed-by-the-java-virtual-machine"></a><span data-ttu-id="0d0fa-186">JMX 計數器 (由虛擬機器公開)</span><span class="sxs-lookup"><span data-stu-id="0d0fa-186">JMX counters (exposed by the Java Virtual Machine)</span></span>

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="0d0fa-187">`displayName` – Application Insights 入口網站中顯示的名稱。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-187">`displayName` – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="0d0fa-188">`objectName` – JMX 物件名稱。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-188">`objectName` – The JMX object name.</span></span>
* <span data-ttu-id="0d0fa-189">`attribute` – 要提取的 JMX 物件名稱的屬性</span><span class="sxs-lookup"><span data-stu-id="0d0fa-189">`attribute` – The attribute of the JMX object name to fetch</span></span>
* <span data-ttu-id="0d0fa-190">`type` (選用) - JMX 物件屬性的類型：</span><span class="sxs-lookup"><span data-stu-id="0d0fa-190">`type` (optional) - The type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="0d0fa-191">預設值：簡易類型，例如 int 或 long。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-191">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="0d0fa-192">`composite`：效能計數器資料的格式為 'Attribute.Data'</span><span class="sxs-lookup"><span data-stu-id="0d0fa-192">`composite`: the perf counter data is in the format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="0d0fa-193">`tabular`：效能計數器資料的格式為資料表列</span><span class="sxs-lookup"><span data-stu-id="0d0fa-193">`tabular`: the perf counter data is in the format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="0d0fa-194">Windows 效能計數器</span><span class="sxs-lookup"><span data-stu-id="0d0fa-194">Windows performance counters</span></span>
<span data-ttu-id="0d0fa-195">每個 [Windows 效能計數器](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) 是類別的成員 (以欄位是類別成員的相同方式)。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span></span> <span data-ttu-id="0d0fa-196">類別可以是全域，或可以有一定數量或指定的執行個體。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-196">Categories can either be global, or can have numbered or named instances.</span></span>

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="0d0fa-197">displayName – Application Insights 入口網站中顯示的名稱。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-197">displayName – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="0d0fa-198">categoryName – 與此效能計數器有關聯的效能計數器類別 (效能物件)。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-198">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="0d0fa-199">counterName – 效能計數器的名稱。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-199">counterName – The name of the performance counter.</span></span>
* <span data-ttu-id="0d0fa-200">instanceName – 效能計數器類別執行個體的名稱，或如果類別包含單一執行個體，則為空白字串 ("")。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-200">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span></span> <span data-ttu-id="0d0fa-201">如果 categoryName 為 Process，而您要收集的效能計數器來自應用程式執行所在的目前 JVM 處理程序，請指定 `"__SELF__"`。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-201">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="0d0fa-202">您的效能計數器會在[計量瀏覽器][metrics]中以自訂度量的形式顯示。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="0d0fa-203">Unix 效能計數器</span><span class="sxs-lookup"><span data-stu-id="0d0fa-203">Unix performance counters</span></span>
* <span data-ttu-id="0d0fa-204">[使用 Application Insights 外掛程式安裝 collectd](app-insights-java-collectd.md) ，來取得各種不同的系統和網路資料。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-204">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="0d0fa-205">可用性 Web 測試</span><span class="sxs-lookup"><span data-stu-id="0d0fa-205">Availability web tests</span></span>
<span data-ttu-id="0d0fa-206">Application Insights 可讓您定期測試網站，以檢查網站運作中且正常回應。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-206">Application Insights can test your website at regular intervals to check that it's up and responding well.</span></span> <span data-ttu-id="0d0fa-207">[若要設定][availability]，請向下捲動來按一下 [可用性]。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-207">[To set up][availability], scroll down to click Availability.</span></span>

![向下捲動，並依序按一下 [可用性]、[加入 Web 測試]](./media/app-insights-java-eclipse/31-config-web-test.png)

<span data-ttu-id="0d0fa-209">您將取得回應時間的圖表，以及若網站關閉還會取得電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-209">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Web 測試範例](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

<span data-ttu-id="0d0fa-211">[深入了解 Web 測試的可用性。][availability]</span><span class="sxs-lookup"><span data-stu-id="0d0fa-211">[Learn more about availability web tests.][availability]</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="0d0fa-212">診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="0d0fa-212">Diagnostic logs</span></span>
<span data-ttu-id="0d0fa-213">如果您使用 Logback 或 Log4J (v1.2 或 v2.0) 進行追蹤，您可以將追蹤記錄自動傳送到 Application Insights，您可以在其中探索及搜尋記錄。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically to Application Insights where you can explore and search on them.</span></span>

<span data-ttu-id="0d0fa-214">[深入了解診斷記錄][javalogs]</span><span class="sxs-lookup"><span data-stu-id="0d0fa-214">[Learn more about diagnostic logs][javalogs]</span></span>

## <a name="custom-telemetry"></a><span data-ttu-id="0d0fa-215">自訂遙測</span><span class="sxs-lookup"><span data-stu-id="0d0fa-215">Custom telemetry</span></span>
<span data-ttu-id="0d0fa-216">在 Java Web 應用程式中插入幾行程式碼，以了解使用者對它進行的動作或協助診斷問題。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-216">Insert a few lines of code in your Java web application to find out what users are doing with it or to help diagnose problems.</span></span>

<span data-ttu-id="0d0fa-217">您可以在網頁 JavaScript 和伺服器端 Java 中插入程式碼。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-217">You can insert code both in web page JavaScript and in the server-side Java.</span></span>

<span data-ttu-id="0d0fa-218">[了解自訂遙測][track]</span><span class="sxs-lookup"><span data-stu-id="0d0fa-218">[Learn about custom telemetry][track]</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d0fa-219">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0d0fa-219">Next steps</span></span>
#### <a name="detect-and-diagnose-issues"></a><span data-ttu-id="0d0fa-220">偵測並診斷問題</span><span class="sxs-lookup"><span data-stu-id="0d0fa-220">Detect and diagnose issues</span></span>
* <span data-ttu-id="0d0fa-221">[新增 Web 用戶端遙測][usage]，從 Web 用戶端取得效能遙測。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-221">[Add web client telemetry][usage] to get performance telemetry from the web client.</span></span>
* <span data-ttu-id="0d0fa-222">[設定 Web 測試][availability]，以確認應用程式處於線上狀態且能夠回應。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-222">[Set up web tests][availability] to make sure your application stays live and responsive.</span></span>
* <span data-ttu-id="0d0fa-223">[搜尋事件和記錄][diagnostic]以協助診斷問題。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-223">[Search events and logs][diagnostic] to help diagnose problems.</span></span>
* <span data-ttu-id="0d0fa-224">[擷取 Log4J 或 Logback 追蹤][javalogs]</span><span class="sxs-lookup"><span data-stu-id="0d0fa-224">[Capture Log4J or Logback traces][javalogs]</span></span>

#### <a name="track-usage"></a><span data-ttu-id="0d0fa-225">追蹤流量</span><span class="sxs-lookup"><span data-stu-id="0d0fa-225">Track usage</span></span>
* <span data-ttu-id="0d0fa-226">[新增 Web 用戶端遙測][usage]，以監視頁面檢視和基本使用者度量。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-226">[Add web client telemetry][usage] to monitor page views and basic user metrics.</span></span>
* <span data-ttu-id="0d0fa-227">[追蹤自訂事件和計量](app-insights-web-track-usage.md)，以了解應用程式在用戶端和伺服器的使用情況。</span><span class="sxs-lookup"><span data-stu-id="0d0fa-227">[Track custom events and metrics](app-insights-web-track-usage.md) to learn about how your application is used, both at the client and the server.</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
