---
title: "在 Azure Application Insights 中探索 Java 追蹤記錄 | Microsoft Docs"
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
ms.openlocfilehash: 5baba3deaf58a1a24995c60381592a9c2ffefd81
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="explore-java-trace-logs-in-application-insights"></a><span data-ttu-id="84905-103">在 Application Insights 中探索 Java 追蹤記錄</span><span class="sxs-lookup"><span data-stu-id="84905-103">Explore Java trace logs in Application Insights</span></span>
<span data-ttu-id="84905-104">如果您使用 Logback 或 Log4J (v1.2 或 v2.0) 進行追蹤，您可以將追蹤記錄自動傳送到 Application Insights，您可以在其中探索及搜尋記錄。</span><span class="sxs-lookup"><span data-stu-id="84905-104">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically to Application Insights where you can explore and search on them.</span></span>

## <a name="install-the-java-sdk"></a><span data-ttu-id="84905-105">安裝 Java SDK</span><span class="sxs-lookup"><span data-stu-id="84905-105">Install the Java SDK</span></span>

<span data-ttu-id="84905-106">安裝 [Java 適用的 Application Insights SDK][java]，如果您還未完成的話。</span><span class="sxs-lookup"><span data-stu-id="84905-106">Install [Application Insights SDK for Java][java], if you haven't already done that.</span></span>

<span data-ttu-id="84905-107">(如果您不想要追蹤 HTTP 要求，您可以省略大多數 .xml 組態檔，但必須至少包含 `InstrumentationKey` 元素。</span><span class="sxs-lookup"><span data-stu-id="84905-107">(If you don't want to track HTTP requests, you can omit most of the .xml configuration file, but you must at least include the `InstrumentationKey` element.</span></span> <span data-ttu-id="84905-108">您還應該呼叫 `new TelemetryClient()` 來將 SDK 初始化)。</span><span class="sxs-lookup"><span data-stu-id="84905-108">You should also call `new TelemetryClient()` to initialize the SDK.)</span></span>


## <a name="add-logging-libraries-to-your-project"></a><span data-ttu-id="84905-109">將記錄程式庫加入至專案</span><span class="sxs-lookup"><span data-stu-id="84905-109">Add logging libraries to your project</span></span>
<span data-ttu-id="84905-110">*選擇適合您的專案的方式。*</span><span class="sxs-lookup"><span data-stu-id="84905-110">*Choose the appropriate way for your project.*</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="84905-111">如果您使用 Maven...</span><span class="sxs-lookup"><span data-stu-id="84905-111">If you're using Maven...</span></span>
<span data-ttu-id="84905-112">如果您的專案已設定為使用 Maven 來建置，請將下列其中一個程式碼片段合併至 pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="84905-112">If your project is already set up to use Maven for build, merge one of the following snippets of code into your pom.xml file.</span></span>

<span data-ttu-id="84905-113">然後重新整理專案相依性，以下載程式庫。</span><span class="sxs-lookup"><span data-stu-id="84905-113">Then refresh the project dependencies, to get the binaries downloaded.</span></span>

<span data-ttu-id="84905-114">*Logback*</span><span class="sxs-lookup"><span data-stu-id="84905-114">*Logback*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="84905-115">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="84905-115">*Log4J v2.0*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="84905-116">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="84905-116">*Log4J v1.2*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="84905-117">如果您使用 Gradle...</span><span class="sxs-lookup"><span data-stu-id="84905-117">If you're using Gradle...</span></span>
<span data-ttu-id="84905-118">如果您的專案已設定為使用 Gradle 來建置，請將下列其中一行加入至 build.gradle 檔案中的 `dependencies` 群組：</span><span class="sxs-lookup"><span data-stu-id="84905-118">If your project is already set up to use Gradle for build, add one of the following lines to the `dependencies` group in your build.gradle file:</span></span>

<span data-ttu-id="84905-119">然後重新整理專案相依性，以下載程式庫。</span><span class="sxs-lookup"><span data-stu-id="84905-119">Then refresh the project dependencies, to get the binaries downloaded.</span></span>

<span data-ttu-id="84905-120">**Logback**</span><span class="sxs-lookup"><span data-stu-id="84905-120">**Logback**</span></span>

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

<span data-ttu-id="84905-121">**Log4J v2.0**</span><span class="sxs-lookup"><span data-stu-id="84905-121">**Log4J v2.0**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

<span data-ttu-id="84905-122">**Log4J v1.2**</span><span class="sxs-lookup"><span data-stu-id="84905-122">**Log4J v1.2**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a><span data-ttu-id="84905-123">否則...</span><span class="sxs-lookup"><span data-stu-id="84905-123">Otherwise ...</span></span>
<span data-ttu-id="84905-124">下載並擷取適當的附加器，然後加入適當的程式庫至您的專案：</span><span class="sxs-lookup"><span data-stu-id="84905-124">Download and extract the appropriate appender, then add the appropriate library to your project:</span></span>

| <span data-ttu-id="84905-125">記錄器</span><span class="sxs-lookup"><span data-stu-id="84905-125">Logger</span></span> | <span data-ttu-id="84905-126">下載</span><span class="sxs-lookup"><span data-stu-id="84905-126">Download</span></span> | <span data-ttu-id="84905-127">程式庫</span><span class="sxs-lookup"><span data-stu-id="84905-127">Library</span></span> |
| --- | --- | --- |
| <span data-ttu-id="84905-128">Logback</span><span class="sxs-lookup"><span data-stu-id="84905-128">Logback</span></span> |[<span data-ttu-id="84905-129">具有 Logback 附加器的 SDK</span><span class="sxs-lookup"><span data-stu-id="84905-129">SDK with Logback appender</span></span>](https://aka.ms/xt62a4) |<span data-ttu-id="84905-130">applicationinsights-logging-logback</span><span class="sxs-lookup"><span data-stu-id="84905-130">applicationinsights-logging-logback</span></span> |
| <span data-ttu-id="84905-131">Log4J v2.0</span><span class="sxs-lookup"><span data-stu-id="84905-131">Log4J v2.0</span></span> |[<span data-ttu-id="84905-132">具有 Log4J v2 附加器的 SDK</span><span class="sxs-lookup"><span data-stu-id="84905-132">SDK with Log4J v2 appender</span></span>](https://aka.ms/qypznq) |<span data-ttu-id="84905-133">applicationinsights-logging-log4j2</span><span class="sxs-lookup"><span data-stu-id="84905-133">applicationinsights-logging-log4j2</span></span> |
| <span data-ttu-id="84905-134">Log4J v1.2</span><span class="sxs-lookup"><span data-stu-id="84905-134">Log4j v1.2</span></span> |[<span data-ttu-id="84905-135">具有 Log4J v1.2 附加器的 SDK</span><span class="sxs-lookup"><span data-stu-id="84905-135">SDK with Log4J v1.2 appender</span></span>](https://aka.ms/ky9cbo) |<span data-ttu-id="84905-136">applicationinsights-logging-log4j1_2</span><span class="sxs-lookup"><span data-stu-id="84905-136">applicationinsights-logging-log4j1_2</span></span> |

## <a name="add-the-appender-to-your-logging-framework"></a><span data-ttu-id="84905-137">將附加器加入至記錄架構</span><span class="sxs-lookup"><span data-stu-id="84905-137">Add the appender to your logging framework</span></span>
<span data-ttu-id="84905-138">若要開始進行追蹤，請將相關的程式碼片段合併到 Log4J 或 Logback 組態檔案：</span><span class="sxs-lookup"><span data-stu-id="84905-138">To start getting traces, merge the relevant snippet of code to the Log4J or Logback configuration file:</span></span> 

<span data-ttu-id="84905-139">*Logback*</span><span class="sxs-lookup"><span data-stu-id="84905-139">*Logback*</span></span>

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="84905-140">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="84905-140">*Log4J v2.0*</span></span>

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

<span data-ttu-id="84905-141">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="84905-141">*Log4J v1.2*</span></span>

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="84905-142">Application Insights 附加器可由任何設定的記錄器參考，而不一定是根記錄器 (如以上程式碼範例所示)。</span><span class="sxs-lookup"><span data-stu-id="84905-142">The Application Insights appenders can be referenced by any configured logger, and not necessarily by the root logger (as shown in the code samples above).</span></span>

## <a name="explore-your-traces-in-the-application-insights-portal"></a><span data-ttu-id="84905-143">在 Application Insights 入口網站中探索您的追蹤</span><span class="sxs-lookup"><span data-stu-id="84905-143">Explore your traces in the Application Insights portal</span></span>
<span data-ttu-id="84905-144">既然已將專案設定為傳送追蹤至 Application Insights，您可以在 Application Insights 入口網站的[搜尋][diagnostic]刀鋒視窗中檢視及搜尋這些追蹤。</span><span class="sxs-lookup"><span data-stu-id="84905-144">Now that you've configured your project to send traces to Application Insights, you can view and search these traces in the Application Insights portal, in the [Search][diagnostic] blade.</span></span>

![在 Application Insights 入口網站中，開啟 [搜尋]](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="84905-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="84905-146">Next steps</span></span>
<span data-ttu-id="84905-147">[診斷搜尋][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="84905-147">[Diagnostic search][diagnostic]</span></span>

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


