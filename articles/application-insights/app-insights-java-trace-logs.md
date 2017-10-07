---
title: "aaaExplore Java 追蹤登入 Azure Application Insights |Microsoft 文件"
description: "在 Application Insights 中搜尋 Log4J 或 Logback 追蹤"
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: fc0a9e2f-3beb-4f47-a9fe-3f86cd29d97a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: e5f8e8c67e57753ba7574b97aa96dbb41db00ce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="explore-java-trace-logs-in-application-insights"></a><span data-ttu-id="92f60-103">在 Application Insights 中探索 Java 追蹤記錄</span><span class="sxs-lookup"><span data-stu-id="92f60-103">Explore Java trace logs in Application Insights</span></span>
<span data-ttu-id="92f60-104">如果您使用 Logback 或 Log4J （v1.2 或 v2.0） 進行追蹤，您可以將自動傳送 tooApplication Insights，您可以在其中瀏覽並在其上搜尋程式追蹤記錄。</span><span class="sxs-lookup"><span data-stu-id="92f60-104">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically tooApplication Insights where you can explore and search on them.</span></span>

## <a name="install-hello-java-sdk"></a><span data-ttu-id="92f60-105">安裝 hello Java SDK</span><span class="sxs-lookup"><span data-stu-id="92f60-105">Install hello Java SDK</span></span>

<span data-ttu-id="92f60-106">安裝 [Java 適用的 Application Insights SDK][java]，如果您還未完成的話。</span><span class="sxs-lookup"><span data-stu-id="92f60-106">Install [Application Insights SDK for Java][java], if you haven't already done that.</span></span>

<span data-ttu-id="92f60-107">(如果您不想 tootrack HTTP 要求，您可以略過大部分的 hello.xml 設定檔，但您必須至少包含 hello`InstrumentationKey`項目。</span><span class="sxs-lookup"><span data-stu-id="92f60-107">(If you don't want tootrack HTTP requests, you can omit most of hello .xml configuration file, but you must at least include hello `InstrumentationKey` element.</span></span> <span data-ttu-id="92f60-108">您也應該呼叫`new TelemetryClient()`tooinitialize hello SDK。)</span><span class="sxs-lookup"><span data-stu-id="92f60-108">You should also call `new TelemetryClient()` tooinitialize hello SDK.)</span></span>


## <a name="add-logging-libraries-tooyour-project"></a><span data-ttu-id="92f60-109">新增記錄程式庫 tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="92f60-109">Add logging libraries tooyour project</span></span>
<span data-ttu-id="92f60-110">*選擇 hello 適當的方式，為您的專案。*</span><span class="sxs-lookup"><span data-stu-id="92f60-110">*Choose hello appropriate way for your project.*</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="92f60-111">如果您使用 Maven...</span><span class="sxs-lookup"><span data-stu-id="92f60-111">If you're using Maven...</span></span>
<span data-ttu-id="92f60-112">如果您的專案已設定 toouse Maven 組建，合併 hello pom.xml 檔案到下列的程式碼片段的其中一個。</span><span class="sxs-lookup"><span data-stu-id="92f60-112">If your project is already set up toouse Maven for build, merge one of hello following snippets of code into your pom.xml file.</span></span>

<span data-ttu-id="92f60-113">然後重新整理 hello 專案相依性，tooget hello 二進位檔下載。</span><span class="sxs-lookup"><span data-stu-id="92f60-113">Then refresh hello project dependencies, tooget hello binaries downloaded.</span></span>

<span data-ttu-id="92f60-114">*Logback*</span><span class="sxs-lookup"><span data-stu-id="92f60-114">*Logback*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="92f60-115">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="92f60-115">*Log4J v2.0*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="92f60-116">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="92f60-116">*Log4J v1.2*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="92f60-117">如果您使用 Gradle...</span><span class="sxs-lookup"><span data-stu-id="92f60-117">If you're using Gradle...</span></span>
<span data-ttu-id="92f60-118">如果您的專案已設定 toouse Gradle 組建，加入下列行 toohello hello 的其中一個`dependencies`build.gradle 檔案群組：</span><span class="sxs-lookup"><span data-stu-id="92f60-118">If your project is already set up toouse Gradle for build, add one of hello following lines toohello `dependencies` group in your build.gradle file:</span></span>

<span data-ttu-id="92f60-119">然後重新整理 hello 專案相依性，tooget hello 二進位檔下載。</span><span class="sxs-lookup"><span data-stu-id="92f60-119">Then refresh hello project dependencies, tooget hello binaries downloaded.</span></span>

<span data-ttu-id="92f60-120">**Logback**</span><span class="sxs-lookup"><span data-stu-id="92f60-120">**Logback**</span></span>

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

<span data-ttu-id="92f60-121">**Log4J v2.0**</span><span class="sxs-lookup"><span data-stu-id="92f60-121">**Log4J v2.0**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

<span data-ttu-id="92f60-122">**Log4J v1.2**</span><span class="sxs-lookup"><span data-stu-id="92f60-122">**Log4J v1.2**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a><span data-ttu-id="92f60-123">否則...</span><span class="sxs-lookup"><span data-stu-id="92f60-123">Otherwise ...</span></span>
<span data-ttu-id="92f60-124">下載並解壓縮 hello 適當附加器，然後加入 hello 適當的程式庫 tooyour 專案：</span><span class="sxs-lookup"><span data-stu-id="92f60-124">Download and extract hello appropriate appender, then add hello appropriate library tooyour project:</span></span>

| <span data-ttu-id="92f60-125">記錄器</span><span class="sxs-lookup"><span data-stu-id="92f60-125">Logger</span></span> | <span data-ttu-id="92f60-126">下載</span><span class="sxs-lookup"><span data-stu-id="92f60-126">Download</span></span> | <span data-ttu-id="92f60-127">程式庫</span><span class="sxs-lookup"><span data-stu-id="92f60-127">Library</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92f60-128">Logback</span><span class="sxs-lookup"><span data-stu-id="92f60-128">Logback</span></span> |[<span data-ttu-id="92f60-129">具有 Logback 附加器的 SDK</span><span class="sxs-lookup"><span data-stu-id="92f60-129">SDK with Logback appender</span></span>](https://aka.ms/xt62a4) |<span data-ttu-id="92f60-130">applicationinsights-logging-logback</span><span class="sxs-lookup"><span data-stu-id="92f60-130">applicationinsights-logging-logback</span></span> |
| <span data-ttu-id="92f60-131">Log4J v2.0</span><span class="sxs-lookup"><span data-stu-id="92f60-131">Log4J v2.0</span></span> |[<span data-ttu-id="92f60-132">具有 Log4J v2 附加器的 SDK</span><span class="sxs-lookup"><span data-stu-id="92f60-132">SDK with Log4J v2 appender</span></span>](https://aka.ms/qypznq) |<span data-ttu-id="92f60-133">applicationinsights-logging-log4j2</span><span class="sxs-lookup"><span data-stu-id="92f60-133">applicationinsights-logging-log4j2</span></span> |
| <span data-ttu-id="92f60-134">Log4J v1.2</span><span class="sxs-lookup"><span data-stu-id="92f60-134">Log4j v1.2</span></span> |[<span data-ttu-id="92f60-135">具有 Log4J v1.2 附加器的 SDK</span><span class="sxs-lookup"><span data-stu-id="92f60-135">SDK with Log4J v1.2 appender</span></span>](https://aka.ms/ky9cbo) |<span data-ttu-id="92f60-136">applicationinsights-logging-log4j1_2</span><span class="sxs-lookup"><span data-stu-id="92f60-136">applicationinsights-logging-log4j1_2</span></span> |

## <a name="add-hello-appender-tooyour-logging-framework"></a><span data-ttu-id="92f60-137">加入 hello 附加器 tooyour 記錄架構</span><span class="sxs-lookup"><span data-stu-id="92f60-137">Add hello appender tooyour logging framework</span></span>
<span data-ttu-id="92f60-138">toostart 入門追蹤、 合併 hello 相關程式碼片段的程式碼 toohello Log4J 或 Logback 組態檔：</span><span class="sxs-lookup"><span data-stu-id="92f60-138">toostart getting traces, merge hello relevant snippet of code toohello Log4J or Logback configuration file:</span></span> 

<span data-ttu-id="92f60-139">*Logback*</span><span class="sxs-lookup"><span data-stu-id="92f60-139">*Logback*</span></span>

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="92f60-140">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="92f60-140">*Log4J v2.0*</span></span>

```XML

    <Configuration packages="com.microsoft.applicationinsights.Log4j">
      <Appenders>
        <ApplicationInsightsAppender name="aiAppender" />
      </Appenders>
      <Loggers>
        <Root level="trace">
          <AppenderRef ref="aiAppender"/>
        </Root>
      </Loggers>
    </Configuration>
```

<span data-ttu-id="92f60-141">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="92f60-141">*Log4J v1.2*</span></span>

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="92f60-142">hello Application Insights appenders 可以參考任何已設定記錄器，並不一定 hello 根記錄器 （如上述的 hello 程式碼範例所示）。</span><span class="sxs-lookup"><span data-stu-id="92f60-142">hello Application Insights appenders can be referenced by any configured logger, and not necessarily by hello root logger (as shown in hello code samples above).</span></span>

## <a name="explore-your-traces-in-hello-application-insights-portal"></a><span data-ttu-id="92f60-143">瀏覽您 hello Application Insights 入口網站中的追蹤</span><span class="sxs-lookup"><span data-stu-id="92f60-143">Explore your traces in hello Application Insights portal</span></span>
<span data-ttu-id="92f60-144">既然您已設定專案 toosend 追蹤 tooApplication Insights，您可以檢視並在 hello Application Insights 入口網站中 hello 搜尋這些追蹤[搜尋][ diagnostic]刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="92f60-144">Now that you've configured your project toosend traces tooApplication Insights, you can view and search these traces in hello Application Insights portal, in hello [Search][diagnostic] blade.</span></span>

![在 hello Application Insights 入口網站中，開啟 搜尋](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="92f60-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="92f60-146">Next steps</span></span>
<span data-ttu-id="92f60-147">[診斷搜尋][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="92f60-147">[Diagnostic search][diagnostic]</span></span>

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


