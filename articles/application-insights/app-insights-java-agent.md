---
title: "Azure Application Insights 中 Java Web 應用程式的效能監視 | Microsoft Docs"
description: "使用 Application Insights 延伸 Java 網站的效能和使用量監視。"
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 84017a48-1cb3-40c8-aab1-ff68d65e2128
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: 4e56998382610ad3d7224e6a8de5aee5419ebe43
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a><span data-ttu-id="607b6-103">監視 Java Web 應用程式中的相依性、例外狀況和執行時間</span><span class="sxs-lookup"><span data-stu-id="607b6-103">Monitor dependencies, exceptions and execution times in Java web apps</span></span>


<span data-ttu-id="607b6-104">如果您已[使用 Application Insights 檢測您的 Java Web 應用程式][java]，您可以使用 Java 代理程式獲得更深入的見解，而不需變更任何程式碼：</span><span class="sxs-lookup"><span data-stu-id="607b6-104">If you have [instrumented your Java web app with Application Insights][java], you can use the Java Agent to get deeper insights, without any code changes:</span></span>

* <span data-ttu-id="607b6-105">**相依性** ：您的應用程式對其他元件呼叫的相關資料，包括：</span><span class="sxs-lookup"><span data-stu-id="607b6-105">**Dependencies:** Data about calls that your application makes to other components, including:</span></span>
  * <span data-ttu-id="607b6-106">**REST 呼叫** ：透過 HttpClient、OkHttp 和 RestTemplate (Spring) 進行。</span><span class="sxs-lookup"><span data-stu-id="607b6-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span></span>
  * <span data-ttu-id="607b6-107">**Redis 呼叫** ：透過 Jedis 用戶端進行。</span><span class="sxs-lookup"><span data-stu-id="607b6-107">**Redis** calls made via the Jedis client.</span></span> <span data-ttu-id="607b6-108">如果呼叫時間長於 10 秒，代理程式也會擷取呼叫引數。</span><span class="sxs-lookup"><span data-stu-id="607b6-108">If the call takes longer than 10s, the agent also fetches the call arguments.</span></span>
  * <span data-ttu-id="607b6-109">**[JDBC 呼叫](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL、SQL Server、PostgreSQL、SQLite、Oracle DB 或 Apache Derby DB。</span><span class="sxs-lookup"><span data-stu-id="607b6-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span></span> <span data-ttu-id="607b6-110">支援 "executeBatch" 呼叫。</span><span class="sxs-lookup"><span data-stu-id="607b6-110">"executeBatch" calls are supported.</span></span> <span data-ttu-id="607b6-111">MySQL 與 PostgreSQL 的呼叫時間如果長於 10 秒，代理程式會回報查詢計劃。</span><span class="sxs-lookup"><span data-stu-id="607b6-111">For MySQL and PostgreSQL, if the call takes longer than 10s, the agent reports the query plan.</span></span>
* <span data-ttu-id="607b6-112">**攔截到例外狀況** ：由程式碼處理的例外狀況相關資料。</span><span class="sxs-lookup"><span data-stu-id="607b6-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="607b6-113">**方法執行時間** ：執行特定的方法所花費的時間相關資料。</span><span class="sxs-lookup"><span data-stu-id="607b6-113">**Method execution time:** Data about the time it takes to execute specific methods.</span></span>

<span data-ttu-id="607b6-114">若要使用 Java 代理程式，您要在伺服器上安裝它。</span><span class="sxs-lookup"><span data-stu-id="607b6-114">To use the Java agent, you install it on your server.</span></span> <span data-ttu-id="607b6-115">您必須使用 [Application Insights Java SDK][java] 檢測您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="607b6-115">Your web apps must be instrumented with the [Application Insights Java SDK][java].</span></span> 

## <a name="install-the-application-insights-agent-for-java"></a><span data-ttu-id="607b6-116">安裝 Java 的 Application Insights 代理程式</span><span class="sxs-lookup"><span data-stu-id="607b6-116">Install the Application Insights agent for Java</span></span>
1. <span data-ttu-id="607b6-117">在執行 Java 伺服器的電腦上[下載代理程式](https://aka.ms/aijavasdk)。</span><span class="sxs-lookup"><span data-stu-id="607b6-117">On the machine running your Java server, [download the agent](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="607b6-118">編輯應用程式伺服器啟動指令碼，並加入下列 JVM：</span><span class="sxs-lookup"><span data-stu-id="607b6-118">Edit the application server startup script, and add the following JVM:</span></span>
   
    <span data-ttu-id="607b6-119">`javaagent:`*代理程式 JAR 檔案的完整路徑*</span><span class="sxs-lookup"><span data-stu-id="607b6-119">`javaagent:`*full path to the agent JAR file*</span></span>
   
    <span data-ttu-id="607b6-120">例如，在 Linux 機器上的 Tomcat 中：</span><span class="sxs-lookup"><span data-stu-id="607b6-120">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path to agent JAR file>"`
3. <span data-ttu-id="607b6-121">重新啟動您的應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="607b6-121">Restart your application server.</span></span>

## <a name="configure-the-agent"></a><span data-ttu-id="607b6-122">設定代理程式</span><span class="sxs-lookup"><span data-stu-id="607b6-122">Configure the agent</span></span>
<span data-ttu-id="607b6-123">建立名為 `AI-Agent.xml` 的檔案，並將它放在代理程式 JAR 檔案所在的同一資料夾中。</span><span class="sxs-lookup"><span data-stu-id="607b6-123">Create a file named `AI-Agent.xml` and place it in the same folder as the agent JAR file.</span></span>

<span data-ttu-id="607b6-124">設定 XML 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="607b6-124">Set the content of the xml file.</span></span> <span data-ttu-id="607b6-125">編輯下列範例以包含或省略您要的功能。</span><span class="sxs-lookup"><span data-stu-id="607b6-125">Edit the following example to include or omit the features you want.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsightsAgent>
      <Instrumentation>

        <!-- Collect remote dependency data -->
        <BuiltIn enabled="true">
           <!-- Disable Redis or alter threshold call duration above which arguments are sent.
               Defaults: enabled, 10000 ms -->
           <Jedis enabled="true" thresholdInMS="1000"/>

           <!-- Set SQL query duration above which query plan is reported (MySQL, PostgreSQL). Default is 10000 ms. -->
           <MaxStatementQueryLimitInMS>1000</MaxStatementQueryLimitInMS>
        </BuiltIn>

        <!-- Collect data about caught exceptions
             and method execution times -->

        <Class name="com.myCompany.MyClass">
           <Method name="methodOne"
               reportCaughtExceptions="true"
               reportExecutionTime="true"
               />

           <!-- Report on the particular signature
                void methodTwo(String, int) -->
           <Method name="methodTwo"
              reportExecutionTime="true"
              signature="(Ljava/lang/String;I)V" />
        </Class>

      </Instrumentation>
    </ApplicationInsightsAgent>

```

<span data-ttu-id="607b6-126">您必須啟用報告例外狀況和個別方法的方法執行時間。</span><span class="sxs-lookup"><span data-stu-id="607b6-126">You have to enable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="607b6-127">根據預設，`reportExecutionTime` 為 true，而 `reportCaughtExceptions` 為 false。</span><span class="sxs-lookup"><span data-stu-id="607b6-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-the-data"></a><span data-ttu-id="607b6-128">檢視資料</span><span class="sxs-lookup"><span data-stu-id="607b6-128">View the data</span></span>
<span data-ttu-id="607b6-129">在 Application Insights 資源中，彙總的遠端相依性和方法執行時間會出現[在效能圖格下][metrics]。</span><span class="sxs-lookup"><span data-stu-id="607b6-129">In the Application Insights resource, aggregated remote dependency and method execution times appears [under the Performance tile][metrics].</span></span>

<span data-ttu-id="607b6-130">若要搜尋相依性、例外狀況及方法報告的個別執行個體，請開啟[搜尋][diagnostic]。</span><span class="sxs-lookup"><span data-stu-id="607b6-130">To search for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="607b6-131">[診斷相依性問題 - 深入了解](app-insights-asp-net-dependencies.md#diagnosis)。</span><span class="sxs-lookup"><span data-stu-id="607b6-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="607b6-132">有疑問嗎？</span><span class="sxs-lookup"><span data-stu-id="607b6-132">Questions?</span></span> <span data-ttu-id="607b6-133">有問題嗎？</span><span class="sxs-lookup"><span data-stu-id="607b6-133">Problems?</span></span>
* <span data-ttu-id="607b6-134">沒有資料？</span><span class="sxs-lookup"><span data-stu-id="607b6-134">No data?</span></span> [<span data-ttu-id="607b6-135">設定防火牆例外狀況</span><span class="sxs-lookup"><span data-stu-id="607b6-135">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="607b6-136">疑難排解 Java</span><span class="sxs-lookup"><span data-stu-id="607b6-136">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
