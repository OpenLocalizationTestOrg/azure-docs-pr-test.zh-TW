---
title: "aaaWhat 是 Apache Storm 的 Azure HDInsight |Microsoft 文件"
description: "Apache Storm 可讓您的即時資料 tooprocess 資料流。 Azure HDInsight 可讓您 tooeasily hello Azure 雲端上建立 Storm 叢集。 與 Visual Studio 中，您可以建立使用 C# 的 Storm 方案，然後再部署的 tooyour HDInsight Storm 叢集。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "apache storm 使用案例,storm 叢集,什麼是 apache storm"
ms.assetid: 72d54080-1e48-4a5e-aa50-cce4ffc85077
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 6c6b2925ef3e5666dfecc3fb3c835bb362902c51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-storm-on-azure-hdinsight"></a>什麼是 Apache Storm on Azure HDInsight？

[Apache Storm](http://storm.apache.org/) 是一個容錯的分散式開放原始碼計算系統。 您可以使用 Storm tooprocess 資料流的即時的 Hadoop。 Storm 解決方案也可以提供保證的資料處理，與 hello 能力 tooreplay 未成功的資料處理 hello 第一次。

出現在 HDInsight 上的提供下列主要優點 hello:

* 可作為受管理服務執行，且具有 99.9% 運作時間的 SLA。

* 在建立期間或之後針對 Storm 叢集執行指令碼，可支援輕鬆自訂。 如需詳細資訊，請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。

* 使用各種不同的語言。 在您的選擇，例如 Java、 C# 和 Python 的 hello 語言中，您可以撰寫 Storm 元件。

    * 與 HDInsight 的 Visual Studio 整合的 hello 開發、 管理及監視的 C# 拓撲中。 如需詳細資訊，請參閱[以 hello HDInsight Tools for Visual Studio C# 開發 Storm 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。

    * 支援 hello 戟 Java 介面。 您可以建立 Storm 拓撲，以支援一次性處理訊息、交易式資料存放區持續性和一組常用的串流分析作業。

*  輕鬆地相應增加和相應減少 Storm 叢集。 您可以新增或移除背景工作節點沒有影響 toorunning Storm 拓撲。

* 會與下列 Azure 服務的 hello 整合：

    * Azure 事件中心

    * Azure 虛擬網路

    * Azure SQL Database

    * Azure 儲存體

    * Azure Cosmos DB

* 安全地將多個 HDInsight 叢集的 hello 功能結合使用虛擬網路。 您可以建立使用 Storm、Kafka、HBase 或 Hadoop 叢集的分析管線。

如需使用 Apache Storm 作為即時分析解決方案的公司清單，請參閱[使用 Apache Storm 的公司](https://storm.apache.org/documentation/Powered-By.html)。

tooget 啟動使用 Storm，請參閱[開始使用 HDInsight 上的 Storm][gettingstarted]。

## <a name="how-does-storm-work"></a>Storm 的運作方式

Storm 執行而不是 hello 拓撲可能已經熟悉的 MapReduce 工作。 Storm 拓撲是由有向非循環圖 (DAG) 中排列的多個元件所組成。 Hello 圖形中的 hello 元件之間流動的資料。 每個元件會取用一或多個資料流，並可選擇性地發出一或多個資料流。 hello 下列圖表說明基本的字數統計拓撲中的元件之間資料流動的方式：

![Storm 拓撲中元件排列方式的範例](./media/hdinsight-storm-overview/example-apache-storm-topology-diagram.png)

* Spout 元件可將資料帶入拓撲中。 它們會發出一或多個資料流到 hello 拓撲。

* Bolt 元件會取用 Spout 或其他 Bolt 所發出的串流。 發射到 hello 拓撲，可能會選擇性地發出資料流。 發射也會負責撰寫資料 tooexternal 服務或儲存體，例如 HDFS、 Kafka 或 HBase。

## <a name="ease-of-creation"></a>容易建立

只要花數分鐘即可在 HDInsight 上佈建新的 Storm 叢集。 如需建立 Storm 叢集的相關資訊，請參閱[開始使用 Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md)。

## <a name="ease-of-use"></a>容易使用

* __安全殼層 (SSH) 連線__： 您也可以使用 SSH hello 網際網路上存取 hello Storm 叢集前端節點。 您可以使用 SSH，直接在叢集上執行命令。

  如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

* __Web 連線__： 所有的 HDInsight 叢集提供 hello Ambari web UI。 您可以輕鬆地監視、 設定及管理服務在叢集上使用 hello Ambari web UI。 Storm 叢集也提供 hello Storm UI。 您可以監視使用和管理執行 Storm 拓撲從瀏覽器 hello Storm UI。

  如需詳細資訊，請參閱 hello[管理 HDInsight 使用 hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)和[監視和管理使用 hello Storm UI](hdinsight-storm-deploy-monitor-topology-linux.md#monitor-and-manage-storm-ui)文件。

* __Azure PowerShell 和 Azure CLI__: PowerShell 和 CLI 這兩者都提供可讓您從您使用 HDInsight 和其他 Azure 服務的用戶端系統 toowork 命令列公用程式。

* __Visual Studio 整合__: Azure 資料湖 Tools for Visual Studio 包括專案範本建立 C# Storm 拓撲使用 hello SCP.Net 架構。 資料湖工具也提供工具 toodeploy 監視和管理 HDInsight 上出現的解決方案。

  如需詳細資訊，請參閱[以 hello HDInsight Tools for Visual Studio C# 開發 Storm 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。

## <a name="integration-with-other-azure-services"></a>與其他 Azure 服務整合

* __Azure Data Lake Store__：如需使用 Data Lake Store 搭配 Storm 叢集的範例，請參閱[使用 Azure Data Lake Store 搭配 Apache Storm on HDInsight](hdinsight-storm-write-data-lake-store.md)。

* __事件中心__: Storm 叢集與使用事件中心的範例，請參閱下列文件的 hello:

    * [開發 Storm on HDInsight 的 Java 型拓撲](hdinsight-storm-develop-java-topology.md)

    * [利用 Storm on HDInsight 處理 Azure 事件中樞的事件 (C#)](hdinsight-storm-develop-csharp-event-hub-topology.md)

* __SQL Database__， __Cosmos DB__，__事件中心__，和__HBase__： 範本範例隨附 hello Data Lake Tools for Visual Studio。 如需詳細資訊，請參閱[開發 Storm on HDInsight 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。

## <a name="reliability"></a>可靠性

Apache Storm 可保證，每個連入訊息一律會完整處理時，即使 hello 資料分析遍佈數百個節點。

hello Nimbus 節點提供的功能類似 toohello Hadoop JobTracker，並指派工作 tooother 動物園管理員透過叢集中的節點。 動物園管理員節點提供協調叢集，並促進 Nimbus 與 hello 監督員 hello 背景工作節點上的處理序之間的通訊。 如果某個處理節點關閉時，通知 hello Nimbus 節點，並 hello 工作與相關聯的資料 tooanother 節點，會將它指派。

hello Apache Storm 叢集的預設設定是 toohave 只有一個 Nimbus 節點。 Storm on HDInsight 會提供兩個 Nimbus 節點。 如果 hello 主要節點失敗，hello Storm 叢集 hello 主要節點恢復時，就會切換 toohello 次要節點。 hello 下列圖表說明 Storm HDInsight 上的 hello 工作流程組態：

![Nimbus、Zookeeper 和監督員的圖表](./media/hdinsight-storm-overview/nimbus.png)

## <a name="scale"></a>調整

新增或移除背景工作節點即可動態調整 HDInsight 叢集。 在處理資料時，可以執行這項作業。

> [!IMPORTANT]
> tootake 利用新的節點會透過調整，加入需要 toorebalance Storm 拓撲啟動之前已增加 hello 叢集大小。

## <a name="support"></a>支援

Storm on HDInsight 隨附完整的企業級連續支援。 Storm on HDInsight 也有 99.9% 的 SLA。 這表示我們保證 Storm 叢集具備外部連線能力的 hello 時間至少 99.9%。

如需詳細資訊，請參閱 [Azure 文章](https://azure.microsoft.com/support/options/)。

## <a name="apache-storm-use-cases"></a>Apache Storm 使用案例

hello 以下是一些常見的案例，您可能會使用出現在 HDInsight:

* 物聯網 (IoT)
* 詐騙偵測
* 社交分析
* 擷取、轉換和載入 (ETL)
* 網路監視
* 搜尋
* Mobile Engagement

真實世界案例的相關資訊，請參閱 hello[公司如何使用 Storm](https://storm.apache.org/documentation/Powered-By.html)文件。

## <a name="development"></a>開發

.NET 開發人員可以使用 Data Lake Tools for Visual Studio，以 C# 語言設計和實作拓撲。 您也可以建立使用 Java 和 C# 元件的混合式拓撲。

如需詳細資訊，請參閱 [使用 Visual Studio 開發 Storm on HDInsight 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。

您也可以使用您選擇的 IDE hello 開發 Java 方案。 如需詳細資訊，請參閱[開發 Storm on HDInsight 的 Java 拓撲](hdinsight-storm-develop-java-topology.md)。

Python 也可以使用的 toodevelop Storm 元件。 如需詳細資訊，請參閱[使用 Python on HDInsight 開發 Storm 拓撲](hdinsight-storm-develop-python-topology.md)。

## <a name="common-development-patterns"></a>常見的開發模式

### <a name="guaranteed-message-processing"></a>保證處理訊息

Apache Storm 可以提供不同程度的訊息處理保證。 例如，基本的 Storm 應用程式可以保證至少處理一次，而 Trident 可以保證只處理一次。

如需詳細資訊，請參閱 apache.org 上的 [保證處理資料](https://storm.apache.org/about/guarantees-data-processing.html) (英文)。

### <a name="ibasicbolt"></a>IBasicBolt

hello 讀取輸入的 tuple，發出零或多個 tuple 的模式，然後立即結尾 hello hello acking hello 輸入的 tuple execute 方法很常見。 Storm 提供 hello [IBasicBolt](https://storm.apache.org/releases/1.0.3/javadocs/org/apache/storm/topology/IBasicBolt.html)介面 tooautomate 此模式。

### <a name="joins"></a>聯結

資料流的聯結方式會隨應用程式而異。 例如，您可以將多個串流中的每個 Tuple 聯結成一個新的串流，也可以只聯結特定時間範圍的幾批 Tuple。 無論何者，都可利用 [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-) 來完成聯結。 群組欄位會是一種方式定義 tuple 的路由的 toobolts 的方式。

在下列範例 Java hello，fieldsGrouping 會是"1"、"2"和"3"的元件 toohello MyJoiner 閃電源自使用的 tooroute tuple:

    builder.setBolt("join", new MyJoiner(), parallelism) .fieldsGrouping("1", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("2", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("3", new Fields("joinfield1", "joinfield2"));

### <a name="batches"></a>批次

Apache Storm 提供稱為「計時 Tuple」的內部計時機制。 您可以設定在您的拓撲中發出計時 Tuple 的頻率。

如需使用 C# 元件中 tick tuple 的範例，請參閱 [PartialBoltCount.cs](https://github.com/hdinsight/hdinsight-storm-examples/blob/3b2c960549cac122e8874931df4801f0934fffa7/EventCountExample/EventCountTopology/src/main/java/com/microsoft/hdinsight/storm/examples/PartialCountBolt.java)。

### <a name="caches"></a>快取

通常會使用記憶體內部快取當做加速處理的機制，因為此方式可以將常用的資產保留在記憶體內。 由於拓撲會分散到多個節點，多個處理序位於每個節點內，您應該考慮使用 [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-)。 使用`fieldsGrouping`tooensure tuple，其中包含用於快取查閱的 hello 欄位一律會路由的 toohello 相同的處理序。 此群組功能可避免快取項目在程序之間重複。

### <a name="stream-top-n"></a>串流「前 N 個」

計算 top N 值取決於您的拓撲，計算以平行方式 hello 前 n 個值。 然後合併 hello 輸出從這些計算成全域值。 這項作業可藉由來使用[fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-) tooroute 透過平行處理的欄位。 然後您可以路由 tooa 閃電全域決定 hello 前 n 個值。

如需計算前 n 個值的範例，請參閱 hello [RollingTopWords](https://github.com/apache/storm/blob/master/examples/storm-starter/src/jvm/org/apache/storm/starter/RollingTopWords.java)範例。

## <a name="logging"></a>記錄

Storm 使用 Apache Log4j toolog 資訊。 根據預設，大量的資料會記錄，並可能很難 toosort 透過 hello 資訊。 您可以包含記錄的組態檔做為您的 Storm 拓樸 toocontrol 記錄行為的一部分。

示範範例拓撲如何 tooconfigure 記錄，請參閱[Java 為基礎的 WordCount](hdinsight-storm-develop-java-topology.md) Storm HDInsight 上的範例。

## <a name="next-steps"></a>後續步驟

深入了解使用 Storm on HDInsight 的即時分析解決方案：

* [開始使用 Apache Storm on HDInsight][gettingstarted]
* [Apache Storm on HDInsight 的範例拓撲](hdinsight-storm-example-topology.md)

[stormtrident]: https://storm.apache.org/documentation/Trident-API-Overview.html
[samoa]: http://yahooeng.tumblr.com/post/65453012905/introducing-samoa-an-open-source-platform-for-mining
[apachetutorial]: https://storm.apache.org/documentation/Tutorial.html
[gettingstarted]: hdinsight-apache-storm-tutorial-get-started-linux.md
