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
# <a name="collectd-linux-performance-metrics-in-application-insights"></a>collectd：Application Insights 中的 Linux 效能計量


tooexplore Linux 系統中的效能標準[Application Insights](app-insights-overview.md)，安裝[collectd](http://collectd.org/)搭配其 Application Insights 外掛程式。 這個開放原始碼解決方案會收集各種系統和網路統計資料。

如果您已[使用 Application Insights 檢測您的 Java Web 服務][java]，通常您會使用 collectd。 它可讓您更多資料 toohelp 您 tooenhance 應用程式效能或診斷問題。 

![範例圖表](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a>取得檢測金鑰
在 hello [Microsoft Azure 入口網站](https://portal.azure.com)，開啟 hello [Application Insights](app-insights-overview.md)想 hello 資料 tooappear 資源。 (或[建立新的資源](app-insights-create-new-resource.md)。)

製作 hello 檢測金鑰識別 hello 資源的複本。

![全部瀏覽，開啟您的資源，然後在 hello Essentials 下拉式清單中，select 和複製 hello 檢測金鑰](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-hello-plug-in"></a>安裝 collectd 和 hello 外掛程式
在您的 Linux 伺服器機器上：

1. 安裝 [collectd](http://collectd.org/) 5.4.0 版或更新版本。
2. 下載 hello [collectd 寫入器的 Application Insights 外掛程式](https://aka.ms/aijavasdk)。 請注意 hello 版本號碼。
3. 複製 hello 外掛程式 JAR 到`/usr/share/collectd/java`。
4. 編輯 `/etc/collectd/collectd.conf`：
   * 請確認[hello Java 外掛程式](https://collectd.org/wiki/index.php/Plugin:Java)已啟用。
   * 更新下列 JAR hello java.class.path tooinclude hello JVMArg。 更新 hello 版本號碼 toomatch hello 您下載：
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * 加入此程式碼片段使用 hello 檢測金鑰從您的資源：

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

以下是範例組態檔的一部分：

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

設定其他 [collectd 外掛程式](https://collectd.org/wiki/index.php/Table_of_Plugins)，它可以從不同來源收集各種資料。

重新啟動 collectd 根據 tooits[手動](https://collectd.org/wiki/index.php/First_steps)。

## <a name="view-hello-data-in-application-insights"></a>檢視 Application Insights 中的 hello 資料
在 Application Insights 資源中，開啟[計量瀏覽器和新增圖表][metrics]，您想從 hello 自訂分類 toosee 選取 hello 度量。

![](./media/app-insights-java-collectd/result.png)

根據預設，會彙總從中 hello 計量所收集的所有主機電腦上的 hello 度量。 tooview hello 度量，每個主機，在 hello 圖表詳細資料 刀鋒視窗，開啟 群組，然後選擇 toogroup CollectD 主機。

## <a name="tooexclude-upload-of-specific-statistics"></a>tooexclude 上傳的特定統計資料
根據預設，hello Application Insights 外掛程式會傳送 hello 讀取所有資料收集的所有啟用的 hello collectd' ' 的外掛程式。 

從特定的外掛程式或資料來源的 tooexclude 資料：

* 編輯 hello 設定檔。 
* 在 `<Plugin ApplicationInsightsWriter>`中，加入指示詞行，如下所示：

| 指示詞 | 效果 |
| --- | --- |
| `Exclude disk` |排除所有的資料收集的 hello`disk`外掛程式 |
| `Exclude disk:read,write` |排除 hello 來源名為`read`和`write`從 hello`disk`外掛程式。 |

以新行分隔個別指示詞。

## <a name="problems"></a>有問題嗎？
*我沒看到 hello 入口網站中的資料*

* 開啟[搜尋][ diagnostic] toosee 如果已到達 hello 未經處理的事件。 有時候會更長的 tooappear 在計量瀏覽器。
* 您可能需要[設定為外送資料的防火牆例外狀況](app-insights-ip-addresses.md)
* 啟用 hello Application Insights 外掛程式中的追蹤。 在 `<Plugin ApplicationInsightsWriter>`內加入這一行：
  * `SDKLogger true`
* 開啟終端機，然後開始 collectd 詳細模式，toosee 它報告任何問題：
  * `sudo collectd -f`

## <a name="known-issue"></a>已知問題

hello 應用程式 Insights 寫入外掛程式是與特定讀取外掛程式不相容。 某些外掛程式有時會傳送 hello Application Insights 外掛程式，必須要有浮點數"NaN"。

徵兆： hello collectd 記錄檔會顯示錯誤，包括 「 AI::...SyntaxError: 未預期的權杖 N」。

因應措施： 排除 hello 問題寫入外掛程式所收集的資料。 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


