---
title: "Azure Application Insights 中的 Java web 應用程式監視 aaaPerformance |Microsoft 文件"
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
ms.openlocfilehash: bf3983e3b4a16e72bc606b6468a757288d05ebaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a><span data-ttu-id="554ea-103">監視 Java Web 應用程式中的相依性、例外狀況和執行時間</span><span class="sxs-lookup"><span data-stu-id="554ea-103">Monitor dependencies, exceptions and execution times in Java web apps</span></span>


<span data-ttu-id="554ea-104">如果您有[檢測您的 Java web 應用程式使用 Application Insights][java]，您可以使用 hello Java 代理程式 tooget 更深入的見解，不需要變更任何程式碼：</span><span class="sxs-lookup"><span data-stu-id="554ea-104">If you have [instrumented your Java web app with Application Insights][java], you can use hello Java Agent tooget deeper insights, without any code changes:</span></span>

* <span data-ttu-id="554ea-105">**相依性：**您應用程式建立 tooother 元件，包括呼叫的相關資料：</span><span class="sxs-lookup"><span data-stu-id="554ea-105">**Dependencies:** Data about calls that your application makes tooother components, including:</span></span>
  * <span data-ttu-id="554ea-106">**REST 呼叫** ：透過 HttpClient、OkHttp 和 RestTemplate (Spring) 進行。</span><span class="sxs-lookup"><span data-stu-id="554ea-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span></span>
  * <span data-ttu-id="554ea-107">**Redis**透過 hello Jedis 用戶端所提出的呼叫。</span><span class="sxs-lookup"><span data-stu-id="554ea-107">**Redis** calls made via hello Jedis client.</span></span> <span data-ttu-id="554ea-108">如果 hello 呼叫費時超過 10s，hello 代理程式也會擷取 hello 呼叫引數。</span><span class="sxs-lookup"><span data-stu-id="554ea-108">If hello call takes longer than 10s, hello agent also fetches hello call arguments.</span></span>
  * <span data-ttu-id="554ea-109">**[JDBC 呼叫](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL、SQL Server、PostgreSQL、SQLite、Oracle DB 或 Apache Derby DB。</span><span class="sxs-lookup"><span data-stu-id="554ea-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span></span> <span data-ttu-id="554ea-110">支援 "executeBatch" 呼叫。</span><span class="sxs-lookup"><span data-stu-id="554ea-110">"executeBatch" calls are supported.</span></span> <span data-ttu-id="554ea-111">如需 MySQL 和 PostgreSQL，hello 呼叫所花費的時間比 10s，如果 hello 代理程式會報告 hello 查詢計劃。</span><span class="sxs-lookup"><span data-stu-id="554ea-111">For MySQL and PostgreSQL, if hello call takes longer than 10s, hello agent reports hello query plan.</span></span>
* <span data-ttu-id="554ea-112">**攔截到例外狀況** ：由程式碼處理的例外狀況相關資料。</span><span class="sxs-lookup"><span data-stu-id="554ea-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="554ea-113">**方法執行時間：** hello 的相關資料的時間它採用 tooexecute 特有的方法。</span><span class="sxs-lookup"><span data-stu-id="554ea-113">**Method execution time:** Data about hello time it takes tooexecute specific methods.</span></span>

<span data-ttu-id="554ea-114">toouse hello Java 代理程式，您安裝在伺服器上。</span><span class="sxs-lookup"><span data-stu-id="554ea-114">toouse hello Java agent, you install it on your server.</span></span> <span data-ttu-id="554ea-115">您的 web 應用程式必須檢測以 hello [Application Insights Java SDK][java]。</span><span class="sxs-lookup"><span data-stu-id="554ea-115">Your web apps must be instrumented with hello [Application Insights Java SDK][java].</span></span> 

## <a name="install-hello-application-insights-agent-for-java"></a><span data-ttu-id="554ea-116">安裝 java hello Application Insights 代理程式</span><span class="sxs-lookup"><span data-stu-id="554ea-116">Install hello Application Insights agent for Java</span></span>
1. <span data-ttu-id="554ea-117">Hello 機器上執行您的 Java 伺服器[下載 hello 代理程式](https://aka.ms/aijavasdk)。</span><span class="sxs-lookup"><span data-stu-id="554ea-117">On hello machine running your Java server, [download hello agent](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="554ea-118">編輯 hello 應用程式伺服器啟動指令碼，並加入下列 JVM hello:</span><span class="sxs-lookup"><span data-stu-id="554ea-118">Edit hello application server startup script, and add hello following JVM:</span></span>
   
    <span data-ttu-id="554ea-119">`javaagent:`*完整路徑 toohello 代理程式 JAR 檔案*</span><span class="sxs-lookup"><span data-stu-id="554ea-119">`javaagent:`*full path toohello agent JAR file*</span></span>
   
    <span data-ttu-id="554ea-120">例如，在 Linux 機器上的 Tomcat 中：</span><span class="sxs-lookup"><span data-stu-id="554ea-120">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path tooagent JAR file>"`
3. <span data-ttu-id="554ea-121">重新啟動您的應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="554ea-121">Restart your application server.</span></span>

## <a name="configure-hello-agent"></a><span data-ttu-id="554ea-122">Hello 代理程式設定</span><span class="sxs-lookup"><span data-stu-id="554ea-122">Configure hello agent</span></span>
<span data-ttu-id="554ea-123">建立名為`AI-Agent.xml`並將它放在 hello 與 hello 代理程式 JAR 檔案相同的資料夾。</span><span class="sxs-lookup"><span data-stu-id="554ea-123">Create a file named `AI-Agent.xml` and place it in hello same folder as hello agent JAR file.</span></span>

<span data-ttu-id="554ea-124">設定 hello hello xml 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="554ea-124">Set hello content of hello xml file.</span></span> <span data-ttu-id="554ea-125">編輯下列範例 tooinclude hello 或省略您想要的 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="554ea-125">Edit hello following example tooinclude or omit hello features you want.</span></span>

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

           <!-- Report on hello particular signature
                void methodTwo(String, int) -->
           <Method name="methodTwo"
              reportExecutionTime="true"
              signature="(Ljava/lang/String;I)V" />
        </Class>

      </Instrumentation>
    </ApplicationInsightsAgent>

```

<span data-ttu-id="554ea-126">您有 tooenable 報告例外狀況以及方法的個別方法的時間。</span><span class="sxs-lookup"><span data-stu-id="554ea-126">You have tooenable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="554ea-127">根據預設，`reportExecutionTime` 為 true，而 `reportCaughtExceptions` 為 false。</span><span class="sxs-lookup"><span data-stu-id="554ea-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-hello-data"></a><span data-ttu-id="554ea-128">檢視 hello 資料</span><span class="sxs-lookup"><span data-stu-id="554ea-128">View hello data</span></span>
<span data-ttu-id="554ea-129">在 hello Application Insights 資源，彙總遠端相依性及方法的執行時間會出現[下 hello 效能磚][metrics]。</span><span class="sxs-lookup"><span data-stu-id="554ea-129">In hello Application Insights resource, aggregated remote dependency and method execution times appears [under hello Performance tile][metrics].</span></span>

<span data-ttu-id="554ea-130">開啟個別的執行個體的相依性、 例外狀況，以及方法報告 toosearch[搜尋][diagnostic]。</span><span class="sxs-lookup"><span data-stu-id="554ea-130">toosearch for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="554ea-131">[診斷相依性問題 - 深入了解](app-insights-asp-net-dependencies.md#diagnosis)。</span><span class="sxs-lookup"><span data-stu-id="554ea-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="554ea-132">有疑問嗎？</span><span class="sxs-lookup"><span data-stu-id="554ea-132">Questions?</span></span> <span data-ttu-id="554ea-133">有問題嗎？</span><span class="sxs-lookup"><span data-stu-id="554ea-133">Problems?</span></span>
* <span data-ttu-id="554ea-134">沒有資料？</span><span class="sxs-lookup"><span data-stu-id="554ea-134">No data?</span></span> [<span data-ttu-id="554ea-135">設定防火牆例外狀況</span><span class="sxs-lookup"><span data-stu-id="554ea-135">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="554ea-136">疑難排解 Java</span><span class="sxs-lookup"><span data-stu-id="554ea-136">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
