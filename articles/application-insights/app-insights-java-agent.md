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
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a>監視 Java Web 應用程式中的相依性、例外狀況和執行時間


如果您有[檢測您的 Java web 應用程式使用 Application Insights][java]，您可以使用 hello Java 代理程式 tooget 更深入的見解，不需要變更任何程式碼：

* **相依性：**您應用程式建立 tooother 元件，包括呼叫的相關資料：
  * **REST 呼叫** ：透過 HttpClient、OkHttp 和 RestTemplate (Spring) 進行。
  * **Redis**透過 hello Jedis 用戶端所提出的呼叫。 如果 hello 呼叫費時超過 10s，hello 代理程式也會擷取 hello 呼叫引數。
  * **[JDBC 呼叫](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL、SQL Server、PostgreSQL、SQLite、Oracle DB 或 Apache Derby DB。 支援 "executeBatch" 呼叫。 如需 MySQL 和 PostgreSQL，hello 呼叫所花費的時間比 10s，如果 hello 代理程式會報告 hello 查詢計劃。
* **攔截到例外狀況** ：由程式碼處理的例外狀況相關資料。
* **方法執行時間：** hello 的相關資料的時間它採用 tooexecute 特有的方法。

toouse hello Java 代理程式，您安裝在伺服器上。 您的 web 應用程式必須檢測以 hello [Application Insights Java SDK][java]。 

## <a name="install-hello-application-insights-agent-for-java"></a>安裝 java hello Application Insights 代理程式
1. Hello 機器上執行您的 Java 伺服器[下載 hello 代理程式](https://aka.ms/aijavasdk)。
2. 編輯 hello 應用程式伺服器啟動指令碼，並加入下列 JVM hello:
   
    `javaagent:`*完整路徑 toohello 代理程式 JAR 檔案*
   
    例如，在 Linux 機器上的 Tomcat 中：
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path tooagent JAR file>"`
3. 重新啟動您的應用程式伺服器。

## <a name="configure-hello-agent"></a>Hello 代理程式設定
建立名為`AI-Agent.xml`並將它放在 hello 與 hello 代理程式 JAR 檔案相同的資料夾。

設定 hello hello xml 檔案的內容。 編輯下列範例 tooinclude hello 或省略您想要的 hello 功能。

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

您有 tooenable 報告例外狀況以及方法的個別方法的時間。

根據預設，`reportExecutionTime` 為 true，而 `reportCaughtExceptions` 為 false。

## <a name="view-hello-data"></a>檢視 hello 資料
在 hello Application Insights 資源，彙總遠端相依性及方法的執行時間會出現[下 hello 效能磚][metrics]。

開啟個別的執行個體的相依性、 例外狀況，以及方法報告 toosearch[搜尋][diagnostic]。

[診斷相依性問題 - 深入了解](app-insights-asp-net-dependencies.md#diagnosis)。

## <a name="questions-problems"></a>有疑問嗎？ 有問題嗎？
* 沒有資料？ [設定防火牆例外狀況](app-insights-ip-addresses.md)
* [疑難排解 Java](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
