---
title: "HDInsight 上的 Apache Storm 拓撲 | Microsoft Docs"
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
ms.date: 12/01/2017
ms.author: larryfr
ms.openlocfilehash: c6c1a1483191e654c245eb3f05ee9e8406510b08
ms.sourcegitcommit: 9a8b9a24d67ba7b779fa34e67d7f2b45c941785e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="example-storm-topologies-and-components-for-apache-storm-on-hdinsight"></a>HDInsight 上 Apache Storm 的範例 Storm 拓撲及元件

以下是 Microsoft 所建立和維護的範例清單，可搭配 Apache Storm on HDInsight 使用。 這些範例涵蓋各種主題，從建立基本 C# 和 Java 拓撲，到使用 Azure 服務，例如事件中樞、Cosmos DB、SQL Database、HBase on HDInsight 和 Azure 儲存體。 一些範例也會示範如何使用非 Azure 或甚至非 Microsoft 的技術，例如 SignalR 和 Socket.IO。

| 描述 | 示範 | 語言/架構 |
|:--- |:--- |:--- |
| [從 Apache Storm 寫入 Azure Data Lake Store](apache-storm-write-data-lake-store.md) |寫入 Azure Data Lake Store |Java |
| [事件中樞 Spout 和 Bolt 來源](https://github.com/apache/storm/tree/master/external/storm-eventhubs) |事件中樞 Spout 和 Bolt 的來源 |Java |
| [開發 Apache Storm on HDInsight 的 Java 型拓撲][5797064f] |Maven |Java |
| [使用 Visual Studio 開發 Apache Storm on HDInsight 的 C# 拓撲][16fce2d1] |HDInsight Tools for Visual Studio |C#，Java |
| [利用 Storm on HDInsight 處理 Azure 事件中樞的事件 (C#)][844d1d81] |事件中樞 |C# 和 Java |
| [使用 Storm on HDInsight 處理 Azure 事件中樞的事件 (Java)](https://azure.microsoft.com/resources/samples/hdinsight-java-storm-eventhub/) |事件中樞 |Java |
| [使用 Storm on HDInsight 處理事件中樞的車輛感應器資料][246ee964] |事件中樞、Cosmos DB、Azure 儲存體 Blob (WASB) |C#，Java |
| [使用 Storm on HDInsight，從 Azure 事件中樞擷取、轉換及載入 (ETL) 至 HBase][b4b68194] |事件中心，HBase |C# |
| [使用 Storm on HDInsight 之 Azure 服務的範本 C# Storm 拓撲專案][ce0c02a2] |事件中樞、Cosmos DB、SQL Database、HBase、SignalR |C#，Java |
| [使用 Storm on HDInsight 從 Azure 事件中樞讀取的延展性效能評比][d6c540e3] |訊息輸送量、事件中心、SQL Database |C#，Java |
| [搭配 Storm on HDInsight 使用 Python](apache-storm-develop-python-topology.md) |使用 Flux 拓撲的 Python 元件 |Python |
| [搭配 Storm on HDInsight 使用 Kafka](../hdinsight-apache-storm-with-kafka.md) | 讀取和寫入 Apache Kafka 的 Apache Storm | Java |

### <a name="next-steps"></a>後續步驟

* [開始使用 Apache Storm on HDInsight][2b8c3488]
* [了解如何利用 Storm on HDInsight 部署和管理 Storm 拓撲][6eb0d3b8]

[2b8c3488]:apache-storm-tutorial-get-started-linux.md "了解如何建立 Storm on HDInsight 叢集並使用 Storm 儀表板來部署範例拓撲。"
[6eb0d3b8]:apache-storm-deploy-monitor-topology.md "了解如何使用 Web 型 Storm 儀表板和 Storm UI 或 HDInsight Tools for Visual Studio 部署和管理拓撲。"
[16fce2d1]:apache-storm-develop-csharp-visual-studio-topology.md "了解如何使用 HDInsight Tools for Visual Studio 建立 C# Storm 拓撲。"
[5797064f]:apache-storm-develop-java-topology.md "了解如何建立基本字數統計拓撲，以使用 Maven 在 Java 中建立 Storm 拓撲。"
[844d1d81]:apache-storm-develop-csharp-event-hub-topology.md "了解如何利用 Storm on HDInsight 從 Azure 事件中樞讀取和寫入資料。"
[246ee964]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md "了解如何使用 Storm 拓撲讀取 Azure 事件中樞的訊息，閱讀 Azure Cosmos DB 的文件做為資料參考，並將資料儲存至 Azure 儲存體。"
[d6c540e3]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/EventCountExample "示範使用 Apache Storm on HDInsight 從 Azure 事件中樞讀取並儲存至 SQL Database 時之輸送量的幾個拓樸。"
[b4b68194]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample "了解如何讀取 Azure 事件中樞的資料、彙總與轉換資料，然後將它儲存至 HBase on HDInsight。"
[ce0c02a2]: https://github.com/hdinsight/hdinsight-storm-examples/tree/master/templates/HDInsightStormExamples "此專案包含 spout、bolt 和拓撲的範本，藉此和各種 Azure 服務進行互動，例如事件中樞、Cosmos DB 和 SQL Database。"

