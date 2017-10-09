---
title: "從事件中樞與 Storm-Azure HDInsight aaaProcess 事件 |Microsoft 文件"
description: "了解如何 tooprocess 資料從 Azure 事件中樞與 C# Storm 拓撲中建立 Visual Studio 中，使用 hello HDInsight tools for Visual Studio。"
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 67f9d08c-eea0-401b-952b-db765655dad0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 30cd910d80eba066f283197bcbbaf11145bc5524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a>利用 Storm on HDInsight 處理 Azure 事件中樞的事件 (C#)

深入了解如何為 Azure 事件中心從 HDInsight 上的 Apache Storm toowork。 本文件會使用 C# Storm 拓撲 tooread 及寫入資料從 Evbent 中樞

> [!NOTE]
> 如需本專案的 Java 版本，請參閱[使用 Storm on HDInsight 處理 Azure 事件中樞的事件 (Java)](hdinsight-storm-develop-java-event-hub-topology.md)。

## <a name="scpnet"></a>SCP.NET

本文件中的 hello 步驟使用 SCP.NET，可讓您輕鬆 toocreate C# 拓撲且 Storm 搭配使用的元件 HDInsight 的 NuGet 封裝。

> [!IMPORTANT]
> 雖然這份文件中的 hello 步驟依賴 Windows 與 Visual Studio 開發環境，hello 編譯的專案可以提交的 tooa Storm 使用 Linux 的 HDInsight 叢集上。 只有在 2016 年 10 月 28 日之後所建立之以 Linux 為基礎的叢集可支援 SCP.NET 拓撲。

HDInsight 3.4 和更大的使用單聲道 toorun C# 拓撲。 使用這份文件中的 hello 範例搭配 HDInsight 3.6。 如果您計劃建立 HDInsight.NET 方案，請檢查 hello[單聲道的相容性](http://www.mono-project.com/docs/about-mono/compatibility/)潛在的不相容的文件。

### <a name="cluster-versioning"></a>叢集版本控制

hello Microsoft.SCP.Net.SDK NuGet 封裝用於您的專案必須符合安裝在 HDInsight 上的 Storm hello 主要版本。 HDInsight 3.5 版及 3.6 版使用 Storm 1.x 版，因此您必須搭配使用 SCP.NET 1.0.x.x 版與這些叢集。

> [!IMPORTANT]
> HDInsight 3.5 或 3.6 叢集，必須要有這個文件中的 hello 範例。
>
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

C# 拓撲也必須以 .NET 4.5 為目標。

## <a name="how-toowork-with-event-hubs"></a>如何使用事件中心 toowork

Microsoft 提供一組可使用 Storm 拓撲從事件中心使用的 toocommunicate Java 元件。 您可以找到包含這些元件在 HDInsight 3.6 相容版本的 hello Java 封存檔 (JAR) 檔案[https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar)。

> [!IMPORTANT]
> 雖然 hello 元件以 Java 撰寫，您可以從 C# 拓撲輕鬆使用它們。

此範例中使用下列元件的 hello:

* __EventHubSpout__：從事件中樞讀取資料。
* __EventHubBolt__： 寫入資料 tooEvent 集線器。
* __EventHubSpoutConfig__： 使用 tooconfigure EventHubSpout。
* __EventHubBoltConfig__： 使用 tooconfigure EventHubBolt。

### <a name="example-spout-usage"></a>範例 Spout 使用方式

SCP.NET 提供方法來新增 EventHubSpout tooyour 拓撲。 這些方法可讓您更輕鬆 tooadd spout 比使用 hello 泛型方法中新增 Java 元件。 hello 下列範例會示範如何使用 spout toocreate hello __SetEventHubSpout__和**EventHubSpoutConfig** SCP.NET 所提供的方法：

```csharp
 topologyBuilder.SetEventHubSpout(
    "EventHubSpout",
    new EventHubSpoutConfig(
        ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"],
        ConfigurationManager.AppSettings["EventHubSharedAccessKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        ConfigurationManager.AppSettings["EventHubEntityPath"],
        eventHubPartitions),
    eventHubPartitions);
```

hello 前一個範例會建立名為新 spout 元件__EventHubSpout__，並將它與事件中樞設定 toocommunicate。 hello 平行處理原則提示 hello 元件是 hello 事件中樞設定 toohello 資料分割數目。 此設定可讓 Storm toocreate hello 元件，每個資料分割的執行個體。

### <a name="example-bolt-usage"></a>範例 Bolt 使用方式

使用 hello **JavaComponmentConstructor**方法 toocreate hello 閃電的執行個體。 hello 下列範例會示範如何 toocreate 和設定的新執行個體的 hello **EventHubBolt**:

```csharp
// Java construcvtor for hello Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set hello bolt toosubscribe toodata from hello spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> 這個範例會使用傳遞為字串，而不是使用 Clojure 運算式**JavaComponentConstructor** toocreate **EventHubBoltConfig**、 hello spout 範例一樣。 兩種方法均可。 使用認為最佳 tooyou hello 方法。

## <a name="download-hello-completed-project"></a>下載完成的 hello 專案

您可以下載從本教學課程建立的 hello 專案的完整版本[GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub)。 不過，您仍然需要 tooprovide 組態設定依照本教學課程中的 hello 步驟。

### <a name="prerequisites"></a>必要條件

* [Apache Storm on HDInsight 叢集 3.5 或 3.6 版](hdinsight-apache-storm-tutorial-get-started.md)。

    > [!WARNING]
    > 本文件中使用的 hello 範例需要在版本 3.5 或 3.6 HDInsight 上的出現。 這不適用於舊版 HDInsight，因為 toobreaking 類別名稱變更。 如需這個範例適用於較舊叢集的版本，請參閱 [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases)。

* [Azure 事件中樞](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)。

* hello [Azure.NET SDK](http://azure.microsoft.com/downloads/)。

* hello [HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。

* 開發環境有 Java JDK 1.8 或更新版本。 JDK 下載檔可從 [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 取得。

  * hello **JAVA_HOME**包含 Java 的環境變數必須點 toohello 目錄。
  * hello **%JAVA_HOME%/bin**目錄必須位於 hello 路徑中。

## <a name="download-hello-event-hubs-components"></a>下載 hello 事件中心元件

下載 hello 事件中心 spout 和閃電元件從[https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar)。

建立名為目錄`eventhubspout`，並儲存到 hello 目錄中的 hello 檔案。

## <a name="configure-event-hubs"></a>設定事件中樞

事件中心是此範例中的 hello 資料來源。 使用 hello 「 建立事件中心 」 一節中的 hello 資訊[開始使用事件中心](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)。

1. Hello 事件中心建立之後，檢視 hello **EventHub**刀鋒視窗中 hello Azure 入口網站，然後選取**共用存取原則**。 選取**+ 加**tooadd hello 下列原則：

   | 名稱 | 權限 |
   | --- | --- |
   | 寫入器 |傳送 |
   | 讀取器 |接聽 |

    ![[共用存取原則] 視窗的螢幕擷取畫面](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. 選取 hello**讀取器**和**寫入器**原則。 複製並儲存 hello 主索引鍵值的這兩項原則，因為稍後使用這些值。

## <a name="configure-hello-eventhubwriter"></a>設定 hello EventHubWriter

1. 如果您有尚未安裝 hello 最新版 hello HDInsight tools for Visual Studio，請參閱[開始使用 HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。

2. 下載從 hello 方案[混合 storm eventhub 式](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub)。

3. 在 hello **EventHubWriter**專案、 開啟 hello **App.config**檔案。 使用您設定早 toofill hello hello 下列機碼值從 hello 事件中樞的 hello 資訊：

   | Key | 值 |
   | --- | --- |
   | EventHubPolicyName |寫入器 (如果您使用不同的名稱與 hello 原則*傳送*權限，建議您改用。) |
   | EventHubPolicyKey |hello 寫入器原則的 hello 索引鍵。 |
   | EventHubNamespace |包含事件中心的 hello 命名空間。 |
   | EventHubName |事件中樞名稱。 |
   | EventHubPartitionCount |hello 中事件中樞分割區數目。 |

4. 儲存並關閉 hello **App.config**檔案。

## <a name="configure-hello-eventhubreader"></a>設定 hello EventHubReader

1. 開啟 hello **EventHubReader**專案。

2. 開啟 hello **App.config**檔案 hello **EventHubReader**。 使用您設定早 toofill hello hello 下列機碼值從 hello 事件中樞的 hello 資訊：

   | Key | 值 |
   | --- | --- |
   | EventHubPolicyName |讀取器 (如果您使用不同的名稱與 hello 原則*接聽*權限，建議您改用。) |
   | EventHubPolicyKey |hello 讀取器原則的 hello 索引鍵。 |
   | EventHubNamespace |包含事件中心的 hello 命名空間。 |
   | EventHubName |事件中樞名稱。 |
   | EventHubPartitionCount |hello 中事件中樞分割區數目。 |

3. 儲存並關閉 hello **App.config**檔案。

## <a name="deploy-hello-topologies"></a>部署 hello 拓撲

1. 從**方案總管 中**，以滑鼠右鍵按一下 hello **EventHubReader**專案，然後選取**提交 HDInsight 上的 tooStorm**。

    ![螢幕擷取畫面的方案總管 中，以反白顯示的 HDInsight 上送出 tooStorm](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. 在 hello**提交拓撲**對話方塊中，選取您**Storm 叢集**。 展開**額外的組態**，選取**Java 檔案路徑**，選取**...**，並選取 hello 目錄，包含您先前下載的 hello JAR 檔案。 最後，按一下 [提交]。

    ![[提交拓撲] 對話方塊的螢幕擷取畫面](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. 當已送出 hello 拓樸時，hello **Storm 拓撲檢視器**隨即出現。 tooview 資訊 hello 拓撲中，選取 hello **EventHubReader** hello 左窗格中的拓撲。

    ![Storm 拓撲檢視器的螢幕擷取畫面](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. 從**方案總管 中**，以滑鼠右鍵按一下 hello **EventHubWriter**專案，然後選取**提交 HDInsight 上的 tooStorm**。

5. 在 hello**提交拓撲**對話方塊中，選取您**Storm 叢集**。 展開**額外的組態**，選取**Java 檔案路徑**，選取**...**，並選取 hello 目錄，包含 hello JAR 檔案您之前下載。 最後，按一下 [提交]。

6. 當已送出 hello 拓樸時，重新整理 hello 拓撲清單，在 hello **Storm 拓撲檢視器**tooverify hello 叢集上執行這兩種拓撲。

7. 在**Storm 拓撲檢視器**，選取 hello **EventHubReader**拓撲。

8. tooopen hello 元件摘要 hello 閃電按兩下 hello **LogBolt** hello 圖表中的元件。

9. 在 hello**執行程式**區段中，選取其中一個 hello 連結在 hello**連接埠**資料行。 這會顯示 hello 元件所記錄的資訊。 為下列文字類似 toohello hello 登入資訊：

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-hello-topologies"></a>停止 hello 拓撲

toostop hello 拓撲中，選取每種拓撲中 hello **Storm 拓撲檢視器**，然後按一下  **Kill**。

![Storm 拓撲檢視器的螢幕擷取畫面，已反白顯示 [終止] 按鈕](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a>刪除叢集

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>後續步驟

在本文件中，您已經學會如何 toouse hello Java 事件中樞 spout 與從 Azure 事件中心中的資料與 C# 拓撲 toowork 閃電。 toolearn 進一步了解建立 C# 拓撲，請參閱 hello 下列資訊：

* [使用 Visual Studio 開發 Apache Storm on HDInsight 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [SCP 程式設計指南](hdinsight-storm-scp-programming-guide.md)
* [Storm on HDInsight 的範例拓撲](hdinsight-storm-example-topology.md)
