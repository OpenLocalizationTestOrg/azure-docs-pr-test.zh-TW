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
# <a name="explore-java-trace-logs-in-application-insights"></a>在 Application Insights 中探索 Java 追蹤記錄
如果您使用 Logback 或 Log4J （v1.2 或 v2.0） 進行追蹤，您可以將自動傳送 tooApplication Insights，您可以在其中瀏覽並在其上搜尋程式追蹤記錄。

## <a name="install-hello-java-sdk"></a>安裝 hello Java SDK

安裝 [Java 適用的 Application Insights SDK][java]，如果您還未完成的話。

(如果您不想 tootrack HTTP 要求，您可以略過大部分的 hello.xml 設定檔，但您必須至少包含 hello`InstrumentationKey`項目。 您也應該呼叫`new TelemetryClient()`tooinitialize hello SDK。)


## <a name="add-logging-libraries-tooyour-project"></a>新增記錄程式庫 tooyour 專案
*選擇 hello 適當的方式，為您的專案。*

#### <a name="if-youre-using-maven"></a>如果您使用 Maven...
如果您的專案已設定 toouse Maven 組建，合併 hello pom.xml 檔案到下列的程式碼片段的其中一個。

然後重新整理 hello 專案相依性，tooget hello 二進位檔下載。

*Logback*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

*Log4J v2.0*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

*Log4J v1.2*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a>如果您使用 Gradle...
如果您的專案已設定 toouse Gradle 組建，加入下列行 toohello hello 的其中一個`dependencies`build.gradle 檔案群組：

然後重新整理 hello 專案相依性，tooget hello 二進位檔下載。

**Logback**

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

**Log4J v2.0**

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

**Log4J v1.2**

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a>否則...
下載並解壓縮 hello 適當附加器，然後加入 hello 適當的程式庫 tooyour 專案：

| 記錄器 | 下載 | 程式庫 |
| --- | --- | --- |
| Logback |[具有 Logback 附加器的 SDK](https://aka.ms/xt62a4) |applicationinsights-logging-logback |
| Log4J v2.0 |[具有 Log4J v2 附加器的 SDK](https://aka.ms/qypznq) |applicationinsights-logging-log4j2 |
| Log4J v1.2 |[具有 Log4J v1.2 附加器的 SDK](https://aka.ms/ky9cbo) |applicationinsights-logging-log4j1_2 |

## <a name="add-hello-appender-tooyour-logging-framework"></a>加入 hello 附加器 tooyour 記錄架構
toostart 入門追蹤、 合併 hello 相關程式碼片段的程式碼 toohello Log4J 或 Logback 組態檔： 

*Logback*

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

*Log4J v2.0*

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

*Log4J v1.2*

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

hello Application Insights appenders 可以參考任何已設定記錄器，並不一定 hello 根記錄器 （如上述的 hello 程式碼範例所示）。

## <a name="explore-your-traces-in-hello-application-insights-portal"></a>瀏覽您 hello Application Insights 入口網站中的追蹤
既然您已設定專案 toosend 追蹤 tooApplication Insights，您可以檢視並在 hello Application Insights 入口網站中 hello 搜尋這些追蹤[搜尋][ diagnostic]刀鋒視窗。

![在 hello Application Insights 入口網站中，開啟 搜尋](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a>後續步驟
[診斷搜尋][diagnostic]

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


