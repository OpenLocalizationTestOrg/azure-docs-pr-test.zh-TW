---
title: "HDInsight 上的 aaaExample Apache Storm 拓撲 |Microsoft 文件"
description: "利用 Apache Storm on HDInsight 建立和測試的範例 Storm 拓撲清單 (包含基本 basic C# 和 Java 拓撲)，以及使用事件中樞。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f9b1bdff-5928-4705-a76d-52fd200917cb
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: b20299112f6489b7c99360f0a539fc732703c64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="example-storm-topologies-and-components-for-apache-storm-on-hdinsight"></a>HDInsight 上 Apache Storm 的範例 Storm 拓撲及元件

hello 如下範例所建立和維護 Microsoft Apache Storm HDInsight 上搭配使用的清單。 這些範例涵蓋各種主題，從建立基本 C# 和 Java 拓撲 tooworking 與 Azure 服務，例如事件中心、 Cosmos DB，Power BI 中，SQL Database、 HBase HDInsight 和 Azure 儲存體上。 一些範例也示範如何使用非 Azure 或甚至非 Microsoft 的技術，例如 SignalR 和 Socket.IO toowork。

| 說明 | 示範 | 語言/架構 |
|:--- |:--- |:--- |
| [從 Apache Storm 寫入 tooAzure 資料湖存放區](hdinsight-storm-write-data-lake-store.md) |撰寫 tooAzure 資料湖存放區 |Java |
| [事件中樞 Spout 和 Bolt 來源](https://github.com/apache/storm/tree/master/external/storm-eventhubs) |事件中樞 Spout hello 和閃電來源 |Java |
| [開發 Apache Storm on HDInsight 的 Java 型拓撲][5797064f] |Maven |Java |
| [使用 Visual Studio 開發 Apache Storm on HDInsight 的 C# 拓撲][16fce2d1] |HDInsight Tools for Visual Studio |C#，Java |
| [在 C# Storm 拓撲中建立多個資料流][ec5a4064] |多個資料流 |C# |
| [利用 Storm on HDInsight 處理 Azure 事件中樞的事件 (C#)][844d1d81] |事件中樞 |C# 和 Java |
| [使用 Storm on HDInsight 處理 Azure 事件中樞的事件 (Java)](hdinsight-storm-develop-java-event-hub-topology.md) |事件中樞 |Java |
| [使用 Storm 拓撲從 Power Bi toovisualize 資料][94d15238] |Power BI |C# |
| [在 HDInsight 中使用 Storm 和 HBase 分析感應器資料][ab894747] |事件中心、HBase、Socket.IO、Web 儀表板 |C#、Java、JavaScript、HTML |
| [使用 Storm on HDInsight 處理事件中樞的車輛感應器資料][246ee964] |事件中樞、Cosmos DB、Azure 儲存體 Blob (WASB) |C#，Java |
| [擷取、 轉換及載入 (ETL) 從 Azure 事件中心 tooHBase HDInsight 上使用 Storm][b4b68194] |事件中心，HBase |C# |
| [使用 Storm on HDInsight 之 Azure 服務的範本 C# Storm 拓撲專案][ce0c02a2] |事件中樞、Cosmos DB、SQL Database、HBase、SignalR |C#，Java |
| [使用 Storm on HDInsight 從 Azure 事件中樞讀取的延展性效能評比][d6c540e3] |訊息輸送量、事件中心、SQL Database |C#，Java |
| [在 HDInsight 上使用 Storm 和 HBase 讓事件相互關聯](hdinsight-storm-correlation-topology.md) |HBase |C# |
| [搭配 Storm on HDInsight 使用 Python](hdinsight-storm-develop-python-topology.md) |使用 Flux 拓撲的 Python 元件 |Python |
| [搭配 Storm on HDInsight 使用 Kafka](hdinsight-apache-storm-with-kafka.md) | Apache Storm 讀取和寫入 tooApache Kafka | Java |

### <a name="next-steps"></a>後續步驟

* [開始使用 Apache Storm on HDInsight][2b8c3488]
* [深入了解如何 toodeploy 和管理與 HDInsight 上的 Storm Storm 拓撲][6eb0d3b8]

[2b8c3488]: hdinsight-apache-storm-tutorial-get-started-linux.md "了解如何 toocreate HDInsight 叢集及用途的 Storm hello Storm 儀表板 toodeploy 範例拓撲。"
[6eb0d3b8]: hdinsight-storm-deploy-monitor-topology.md "深入了解如何 toodeploy 和管理使用 hello 網頁 Storm 儀表板和 Storm UI 或 hello HDInsight Tools for Visual Studio 的拓撲。"
[16fce2d1]: hdinsight-storm-develop-csharp-visual-studio-topology.md "了解 toocreate C# Storm 拓撲使用 hello HDInsight Tools for Visual Studio 的方式。"
[5797064f]: hdinsight-storm-develop-java-topology.md "深入了解如何在 Java 中，使用 Maven，藉由建立基本 wordcount 拓撲 toocreate Storm 拓撲。"
[94d15238]: hdinsight-storm-power-bi-topology.md "示範如何 toowrite 資料 tooPower BI 從 C# 拓撲，然後建立圖表與儀表板從 hello 資料。"
[ec5a4064]: https://github.com/Blackmist/csharp-storm-example "示範執行在 C# 中實作之字數統計的基本 Storm 拓撲。這也會示範如何 toocreate 多個資料流中的 C# 拓撲。"
[844d1d81]: hdinsight-storm-develop-csharp-event-hub-topology.md "深入了解如何從 Azure 事件中樞與 HDInsight 上的 Storm tooread 和寫入資料。"
[ab894747]: hdinsight-storm-sensor-data-analysis.md "了解如何 toouse Apache Storm 的 Azure 事件中樞，HDInsight tooprocess 感應器資料視覺效果使用 D3.js，以及 （選擇性） 儲存 tooHBase。"
[246ee964]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md "了解如何 toouse Storm 拓撲 tooread 訊息從 Azure 事件中樞，從 Azure Cosmos DB 讀取文件的參考資料和儲存資料 tooAzure 儲存體。"
[d6c540e3]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/EventCountExample "數個拓撲 toodemonstrate 輸送量時 HDInsight 上使用 Apache Storm Azure 事件中心讀取和儲存 tooSQL 資料庫。"
[b4b68194]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample "了解如何 tooread 資料從 Azure 事件中樞，彙總 （& s） 轉換 hello 資料，然後在 HDInsight 上 tooHBase 儲存它。"
[ce0c02a2]: https://github.com/hdinsight/hdinsight-storm-examples/tree/master/templates/HDInsightStormExamples "此專案包含 spouts、 攻擊和拓撲 toointeract 和不同的 Azure 服務，例如事件中心、 Cosmos DB 和 SQL Database 的範本。"

