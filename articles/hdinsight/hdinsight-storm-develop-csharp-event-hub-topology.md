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
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a><span data-ttu-id="583bf-103">利用 Storm on HDInsight 處理 Azure 事件中樞的事件 (C#)</span><span class="sxs-lookup"><span data-stu-id="583bf-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>

<span data-ttu-id="583bf-104">深入了解如何為 Azure 事件中心從 HDInsight 上的 Apache Storm toowork。</span><span class="sxs-lookup"><span data-stu-id="583bf-104">Learn how toowork with Azure Event Hubs from Apache Storm on HDInsight.</span></span> <span data-ttu-id="583bf-105">本文件會使用 C# Storm 拓撲 tooread 及寫入資料從 Evbent 中樞</span><span class="sxs-lookup"><span data-stu-id="583bf-105">This document uses a C# Storm topology tooread and write data from Evbent Hubs</span></span>

> [!NOTE]
> <span data-ttu-id="583bf-106">如需本專案的 Java 版本，請參閱[使用 Storm on HDInsight 處理 Azure 事件中樞的事件 (Java)](hdinsight-storm-develop-java-event-hub-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="583bf-106">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="scpnet"></a><span data-ttu-id="583bf-107">SCP.NET</span><span class="sxs-lookup"><span data-stu-id="583bf-107">SCP.NET</span></span>

<span data-ttu-id="583bf-108">本文件中的 hello 步驟使用 SCP.NET，可讓您輕鬆 toocreate C# 拓撲且 Storm 搭配使用的元件 HDInsight 的 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="583bf-108">hello steps in this document use SCP.NET, a NuGet package that makes it easy toocreate C# topologies and components for use with Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="583bf-109">雖然這份文件中的 hello 步驟依賴 Windows 與 Visual Studio 開發環境，hello 編譯的專案可以提交的 tooa Storm 使用 Linux 的 HDInsight 叢集上。</span><span class="sxs-lookup"><span data-stu-id="583bf-109">While hello steps in this document rely on a Windows development environment with Visual Studio, hello compiled project can be submitted tooa Storm on HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="583bf-110">只有在 2016 年 10 月 28 日之後所建立之以 Linux 為基礎的叢集可支援 SCP.NET 拓撲。</span><span class="sxs-lookup"><span data-stu-id="583bf-110">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="583bf-111">HDInsight 3.4 和更大的使用單聲道 toorun C# 拓撲。</span><span class="sxs-lookup"><span data-stu-id="583bf-111">HDInsight 3.4 and greater use Mono toorun C# topologies.</span></span> <span data-ttu-id="583bf-112">使用這份文件中的 hello 範例搭配 HDInsight 3.6。</span><span class="sxs-lookup"><span data-stu-id="583bf-112">hello example used in this document works with HDInsight 3.6.</span></span> <span data-ttu-id="583bf-113">如果您計劃建立 HDInsight.NET 方案，請檢查 hello[單聲道的相容性](http://www.mono-project.com/docs/about-mono/compatibility/)潛在的不相容的文件。</span><span class="sxs-lookup"><span data-stu-id="583bf-113">If you plan on creating your own .NET solutions for HDInsight, check hello [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>

### <a name="cluster-versioning"></a><span data-ttu-id="583bf-114">叢集版本控制</span><span class="sxs-lookup"><span data-stu-id="583bf-114">Cluster versioning</span></span>

<span data-ttu-id="583bf-115">hello Microsoft.SCP.Net.SDK NuGet 封裝用於您的專案必須符合安裝在 HDInsight 上的 Storm hello 主要版本。</span><span class="sxs-lookup"><span data-stu-id="583bf-115">hello Microsoft.SCP.Net.SDK NuGet package you use for your project must match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="583bf-116">HDInsight 3.5 版及 3.6 版使用 Storm 1.x 版，因此您必須搭配使用 SCP.NET 1.0.x.x 版與這些叢集。</span><span class="sxs-lookup"><span data-stu-id="583bf-116">HDInsight versions 3.5 and 3.6 use Storm 1.x, so you must use SCP.NET version 1.0.x.x with these clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="583bf-117">HDInsight 3.5 或 3.6 叢集，必須要有這個文件中的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="583bf-117">hello example in this document expects an HDInsight 3.5 or 3.6 cluster.</span></span>
>
> <span data-ttu-id="583bf-118">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="583bf-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="583bf-119">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="583bf-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="583bf-120">C# 拓撲也必須以 .NET 4.5 為目標。</span><span class="sxs-lookup"><span data-stu-id="583bf-120">C# topologies must also target .NET 4.5.</span></span>

## <a name="how-toowork-with-event-hubs"></a><span data-ttu-id="583bf-121">如何使用事件中心 toowork</span><span class="sxs-lookup"><span data-stu-id="583bf-121">How toowork with Event Hubs</span></span>

<span data-ttu-id="583bf-122">Microsoft 提供一組可使用 Storm 拓撲從事件中心使用的 toocommunicate Java 元件。</span><span class="sxs-lookup"><span data-stu-id="583bf-122">Microsoft provides a set of Java components that can be used toocommunicate with Event Hubs from a Storm topology.</span></span> <span data-ttu-id="583bf-123">您可以找到包含這些元件在 HDInsight 3.6 相容版本的 hello Java 封存檔 (JAR) 檔案[https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar)。</span><span class="sxs-lookup"><span data-stu-id="583bf-123">You can find hello Java archive (JAR) file that contains an HDInsight 3.6 compatible version of these components at [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="583bf-124">雖然 hello 元件以 Java 撰寫，您可以從 C# 拓撲輕鬆使用它們。</span><span class="sxs-lookup"><span data-stu-id="583bf-124">While hello components are written in Java, you can easily use them from a C# topology.</span></span>

<span data-ttu-id="583bf-125">此範例中使用下列元件的 hello:</span><span class="sxs-lookup"><span data-stu-id="583bf-125">hello following components are used in this example:</span></span>

* <span data-ttu-id="583bf-126">__EventHubSpout__：從事件中樞讀取資料。</span><span class="sxs-lookup"><span data-stu-id="583bf-126">__EventHubSpout__: Reads data from Event Hubs.</span></span>
* <span data-ttu-id="583bf-127">__EventHubBolt__： 寫入資料 tooEvent 集線器。</span><span class="sxs-lookup"><span data-stu-id="583bf-127">__EventHubBolt__: Writes data tooEvent Hubs.</span></span>
* <span data-ttu-id="583bf-128">__EventHubSpoutConfig__： 使用 tooconfigure EventHubSpout。</span><span class="sxs-lookup"><span data-stu-id="583bf-128">__EventHubSpoutConfig__: Used tooconfigure EventHubSpout.</span></span>
* <span data-ttu-id="583bf-129">__EventHubBoltConfig__： 使用 tooconfigure EventHubBolt。</span><span class="sxs-lookup"><span data-stu-id="583bf-129">__EventHubBoltConfig__: Used tooconfigure EventHubBolt.</span></span>

### <a name="example-spout-usage"></a><span data-ttu-id="583bf-130">範例 Spout 使用方式</span><span class="sxs-lookup"><span data-stu-id="583bf-130">Example spout usage</span></span>

<span data-ttu-id="583bf-131">SCP.NET 提供方法來新增 EventHubSpout tooyour 拓撲。</span><span class="sxs-lookup"><span data-stu-id="583bf-131">SCP.NET provides methods for adding an EventHubSpout tooyour topology.</span></span> <span data-ttu-id="583bf-132">這些方法可讓您更輕鬆 tooadd spout 比使用 hello 泛型方法中新增 Java 元件。</span><span class="sxs-lookup"><span data-stu-id="583bf-132">These methods make it easier tooadd a spout than using hello generic methods for adding a Java component.</span></span> <span data-ttu-id="583bf-133">hello 下列範例會示範如何使用 spout toocreate hello __SetEventHubSpout__和**EventHubSpoutConfig** SCP.NET 所提供的方法：</span><span class="sxs-lookup"><span data-stu-id="583bf-133">hello following example demonstrates how toocreate a spout by using hello __SetEventHubSpout__ and **EventHubSpoutConfig** methods provided by SCP.NET:</span></span>

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

<span data-ttu-id="583bf-134">hello 前一個範例會建立名為新 spout 元件__EventHubSpout__，並將它與事件中樞設定 toocommunicate。</span><span class="sxs-lookup"><span data-stu-id="583bf-134">hello previous example creates a new spout component named __EventHubSpout__, and configures it toocommunicate with an event hub.</span></span> <span data-ttu-id="583bf-135">hello 平行處理原則提示 hello 元件是 hello 事件中樞設定 toohello 資料分割數目。</span><span class="sxs-lookup"><span data-stu-id="583bf-135">hello parallelism hint for hello component is set toohello number of partitions in hello event hub.</span></span> <span data-ttu-id="583bf-136">此設定可讓 Storm toocreate hello 元件，每個資料分割的執行個體。</span><span class="sxs-lookup"><span data-stu-id="583bf-136">This setting allows Storm toocreate an instance of hello component for each partition.</span></span>

### <a name="example-bolt-usage"></a><span data-ttu-id="583bf-137">範例 Bolt 使用方式</span><span class="sxs-lookup"><span data-stu-id="583bf-137">Example bolt usage</span></span>

<span data-ttu-id="583bf-138">使用 hello **JavaComponmentConstructor**方法 toocreate hello 閃電的執行個體。</span><span class="sxs-lookup"><span data-stu-id="583bf-138">Use hello **JavaComponmentConstructor** method toocreate an instance of hello bolt.</span></span> <span data-ttu-id="583bf-139">hello 下列範例會示範如何 toocreate 和設定的新執行個體的 hello **EventHubBolt**:</span><span class="sxs-lookup"><span data-stu-id="583bf-139">hello following example demonstrates how toocreate and configure a new instance of hello **EventHubBolt**:</span></span>

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
> <span data-ttu-id="583bf-140">這個範例會使用傳遞為字串，而不是使用 Clojure 運算式**JavaComponentConstructor** toocreate **EventHubBoltConfig**、 hello spout 範例一樣。</span><span class="sxs-lookup"><span data-stu-id="583bf-140">This example uses a Clojure expression passed as a string, instead of using **JavaComponentConstructor** toocreate an **EventHubBoltConfig**, as hello spout example did.</span></span> <span data-ttu-id="583bf-141">兩種方法均可。</span><span class="sxs-lookup"><span data-stu-id="583bf-141">Either method works.</span></span> <span data-ttu-id="583bf-142">使用認為最佳 tooyou hello 方法。</span><span class="sxs-lookup"><span data-stu-id="583bf-142">Use hello method that feels best tooyou.</span></span>

## <a name="download-hello-completed-project"></a><span data-ttu-id="583bf-143">下載完成的 hello 專案</span><span class="sxs-lookup"><span data-stu-id="583bf-143">Download hello completed project</span></span>

<span data-ttu-id="583bf-144">您可以下載從本教學課程建立的 hello 專案的完整版本[GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub)。</span><span class="sxs-lookup"><span data-stu-id="583bf-144">You can download a complete version of hello project created in this tutorial from [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span> <span data-ttu-id="583bf-145">不過，您仍然需要 tooprovide 組態設定依照本教學課程中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="583bf-145">However, you still need tooprovide configuration settings by following hello steps in this tutorial.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="583bf-146">必要條件</span><span class="sxs-lookup"><span data-stu-id="583bf-146">Prerequisites</span></span>

* <span data-ttu-id="583bf-147">[Apache Storm on HDInsight 叢集 3.5 或 3.6 版](hdinsight-apache-storm-tutorial-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="583bf-147">An [Apache Storm on HDInsight cluster version 3.5 or 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span></span>

    > [!WARNING]
    > <span data-ttu-id="583bf-148">本文件中使用的 hello 範例需要在版本 3.5 或 3.6 HDInsight 上的出現。</span><span class="sxs-lookup"><span data-stu-id="583bf-148">hello example used in this document requires Storm on HDInsight version 3.5 or 3.6.</span></span> <span data-ttu-id="583bf-149">這不適用於舊版 HDInsight，因為 toobreaking 類別名稱變更。</span><span class="sxs-lookup"><span data-stu-id="583bf-149">This does not work with older versions of HDInsight, due toobreaking class name changes.</span></span> <span data-ttu-id="583bf-150">如需這個範例適用於較舊叢集的版本，請參閱 [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases)。</span><span class="sxs-lookup"><span data-stu-id="583bf-150">For a version of this example that works with older clusters, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span></span>

* <span data-ttu-id="583bf-151">[Azure 事件中樞](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)。</span><span class="sxs-lookup"><span data-stu-id="583bf-151">An [Azure event hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="583bf-152">hello [Azure.NET SDK](http://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="583bf-152">hello [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>

* <span data-ttu-id="583bf-153">hello [HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="583bf-153">hello [HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="583bf-154">開發環境有 Java JDK 1.8 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="583bf-154">Java JDK 1.8 or later on your development environment.</span></span> <span data-ttu-id="583bf-155">JDK 下載檔可從 [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 取得。</span><span class="sxs-lookup"><span data-stu-id="583bf-155">JDK downloads are available from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

  * <span data-ttu-id="583bf-156">hello **JAVA_HOME**包含 Java 的環境變數必須點 toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="583bf-156">hello **JAVA_HOME** environment variable must point toohello directory that contains Java.</span></span>
  * <span data-ttu-id="583bf-157">hello **%JAVA_HOME%/bin**目錄必須位於 hello 路徑中。</span><span class="sxs-lookup"><span data-stu-id="583bf-157">hello **%JAVA_HOME%/bin** directory must be in hello path.</span></span>

## <a name="download-hello-event-hubs-components"></a><span data-ttu-id="583bf-158">下載 hello 事件中心元件</span><span class="sxs-lookup"><span data-stu-id="583bf-158">Download hello Event Hubs components</span></span>

<span data-ttu-id="583bf-159">下載 hello 事件中心 spout 和閃電元件從[https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar)。</span><span class="sxs-lookup"><span data-stu-id="583bf-159">Download hello Event Hubs spout and bolt component from [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

<span data-ttu-id="583bf-160">建立名為目錄`eventhubspout`，並儲存到 hello 目錄中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="583bf-160">Create a directory named `eventhubspout`, and save hello file into hello directory.</span></span>

## <a name="configure-event-hubs"></a><span data-ttu-id="583bf-161">設定事件中樞</span><span class="sxs-lookup"><span data-stu-id="583bf-161">Configure Event Hubs</span></span>

<span data-ttu-id="583bf-162">事件中心是此範例中的 hello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="583bf-162">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="583bf-163">使用 hello 「 建立事件中心 」 一節中的 hello 資訊[開始使用事件中心](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)。</span><span class="sxs-lookup"><span data-stu-id="583bf-163">Use hello information in hello "Create an event hub" section of [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

1. <span data-ttu-id="583bf-164">Hello 事件中心建立之後，檢視 hello **EventHub**刀鋒視窗中 hello Azure 入口網站，然後選取**共用存取原則**。</span><span class="sxs-lookup"><span data-stu-id="583bf-164">After hello event hub has been created, view hello **EventHub** blade in hello Azure portal, and select **Shared access policies**.</span></span> <span data-ttu-id="583bf-165">選取**+ 加**tooadd hello 下列原則：</span><span class="sxs-lookup"><span data-stu-id="583bf-165">Select **+ Add** tooadd hello following policies:</span></span>

   | <span data-ttu-id="583bf-166">名稱</span><span class="sxs-lookup"><span data-stu-id="583bf-166">Name</span></span> | <span data-ttu-id="583bf-167">權限</span><span class="sxs-lookup"><span data-stu-id="583bf-167">Permissions</span></span> |
   | --- | --- |
   | <span data-ttu-id="583bf-168">寫入器</span><span class="sxs-lookup"><span data-stu-id="583bf-168">writer</span></span> |<span data-ttu-id="583bf-169">傳送</span><span class="sxs-lookup"><span data-stu-id="583bf-169">Send</span></span> |
   | <span data-ttu-id="583bf-170">讀取器</span><span class="sxs-lookup"><span data-stu-id="583bf-170">reader</span></span> |<span data-ttu-id="583bf-171">接聽</span><span class="sxs-lookup"><span data-stu-id="583bf-171">Listen</span></span> |

    ![[共用存取原則] 視窗的螢幕擷取畫面](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. <span data-ttu-id="583bf-173">選取 hello**讀取器**和**寫入器**原則。</span><span class="sxs-lookup"><span data-stu-id="583bf-173">Select hello **reader** and **writer** policies.</span></span> <span data-ttu-id="583bf-174">複製並儲存 hello 主索引鍵值的這兩項原則，因為稍後使用這些值。</span><span class="sxs-lookup"><span data-stu-id="583bf-174">Copy and save hello primary key value for both policies, as these values are used later.</span></span>

## <a name="configure-hello-eventhubwriter"></a><span data-ttu-id="583bf-175">設定 hello EventHubWriter</span><span class="sxs-lookup"><span data-stu-id="583bf-175">Configure hello EventHubWriter</span></span>

1. <span data-ttu-id="583bf-176">如果您有尚未安裝 hello 最新版 hello HDInsight tools for Visual Studio，請參閱[開始使用 HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="583bf-176">If you have not already installed hello latest version of hello HDInsight tools for Visual Studio, see [Get started using HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="583bf-177">下載從 hello 方案[混合 storm eventhub 式](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub)。</span><span class="sxs-lookup"><span data-stu-id="583bf-177">Download hello solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

3. <span data-ttu-id="583bf-178">在 hello **EventHubWriter**專案、 開啟 hello **App.config**檔案。</span><span class="sxs-lookup"><span data-stu-id="583bf-178">In hello **EventHubWriter** project, open hello **App.config** file.</span></span> <span data-ttu-id="583bf-179">使用您設定早 toofill hello hello 下列機碼值從 hello 事件中樞的 hello 資訊：</span><span class="sxs-lookup"><span data-stu-id="583bf-179">Use hello information from hello event hub that you configured earlier toofill in hello value for hello following keys:</span></span>

   | <span data-ttu-id="583bf-180">Key</span><span class="sxs-lookup"><span data-stu-id="583bf-180">Key</span></span> | <span data-ttu-id="583bf-181">值</span><span class="sxs-lookup"><span data-stu-id="583bf-181">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="583bf-182">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="583bf-182">EventHubPolicyName</span></span> |<span data-ttu-id="583bf-183">寫入器 (如果您使用不同的名稱與 hello 原則*傳送*權限，建議您改用。)</span><span class="sxs-lookup"><span data-stu-id="583bf-183">writer (If you used a different name for hello policy with *Send* permission, use it instead.)</span></span> |
   | <span data-ttu-id="583bf-184">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="583bf-184">EventHubPolicyKey</span></span> |<span data-ttu-id="583bf-185">hello 寫入器原則的 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="583bf-185">hello key for hello writer policy.</span></span> |
   | <span data-ttu-id="583bf-186">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="583bf-186">EventHubNamespace</span></span> |<span data-ttu-id="583bf-187">包含事件中心的 hello 命名空間。</span><span class="sxs-lookup"><span data-stu-id="583bf-187">hello namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="583bf-188">EventHubName</span><span class="sxs-lookup"><span data-stu-id="583bf-188">EventHubName</span></span> |<span data-ttu-id="583bf-189">事件中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="583bf-189">Your event hub name.</span></span> |
   | <span data-ttu-id="583bf-190">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="583bf-190">EventHubPartitionCount</span></span> |<span data-ttu-id="583bf-191">hello 中事件中樞分割區數目。</span><span class="sxs-lookup"><span data-stu-id="583bf-191">hello number of partitions in your event hub.</span></span> |

4. <span data-ttu-id="583bf-192">儲存並關閉 hello **App.config**檔案。</span><span class="sxs-lookup"><span data-stu-id="583bf-192">Save and close hello **App.config** file.</span></span>

## <a name="configure-hello-eventhubreader"></a><span data-ttu-id="583bf-193">設定 hello EventHubReader</span><span class="sxs-lookup"><span data-stu-id="583bf-193">Configure hello EventHubReader</span></span>

1. <span data-ttu-id="583bf-194">開啟 hello **EventHubReader**專案。</span><span class="sxs-lookup"><span data-stu-id="583bf-194">Open hello **EventHubReader** project.</span></span>

2. <span data-ttu-id="583bf-195">開啟 hello **App.config**檔案 hello **EventHubReader**。</span><span class="sxs-lookup"><span data-stu-id="583bf-195">Open hello **App.config** file for hello **EventHubReader**.</span></span> <span data-ttu-id="583bf-196">使用您設定早 toofill hello hello 下列機碼值從 hello 事件中樞的 hello 資訊：</span><span class="sxs-lookup"><span data-stu-id="583bf-196">Use hello information from hello event hub that you configured earlier toofill in hello value for hello following keys:</span></span>

   | <span data-ttu-id="583bf-197">Key</span><span class="sxs-lookup"><span data-stu-id="583bf-197">Key</span></span> | <span data-ttu-id="583bf-198">值</span><span class="sxs-lookup"><span data-stu-id="583bf-198">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="583bf-199">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="583bf-199">EventHubPolicyName</span></span> |<span data-ttu-id="583bf-200">讀取器 (如果您使用不同的名稱與 hello 原則*接聽*權限，建議您改用。)</span><span class="sxs-lookup"><span data-stu-id="583bf-200">reader (If you used a different name for hello policy with *listen* permission, use it instead.)</span></span> |
   | <span data-ttu-id="583bf-201">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="583bf-201">EventHubPolicyKey</span></span> |<span data-ttu-id="583bf-202">hello 讀取器原則的 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="583bf-202">hello key for hello reader policy.</span></span> |
   | <span data-ttu-id="583bf-203">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="583bf-203">EventHubNamespace</span></span> |<span data-ttu-id="583bf-204">包含事件中心的 hello 命名空間。</span><span class="sxs-lookup"><span data-stu-id="583bf-204">hello namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="583bf-205">EventHubName</span><span class="sxs-lookup"><span data-stu-id="583bf-205">EventHubName</span></span> |<span data-ttu-id="583bf-206">事件中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="583bf-206">Your event hub name.</span></span> |
   | <span data-ttu-id="583bf-207">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="583bf-207">EventHubPartitionCount</span></span> |<span data-ttu-id="583bf-208">hello 中事件中樞分割區數目。</span><span class="sxs-lookup"><span data-stu-id="583bf-208">hello number of partitions in your event hub.</span></span> |

3. <span data-ttu-id="583bf-209">儲存並關閉 hello **App.config**檔案。</span><span class="sxs-lookup"><span data-stu-id="583bf-209">Save and close hello **App.config** file.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="583bf-210">部署 hello 拓撲</span><span class="sxs-lookup"><span data-stu-id="583bf-210">Deploy hello topologies</span></span>

1. <span data-ttu-id="583bf-211">從**方案總管 中**，以滑鼠右鍵按一下 hello **EventHubReader**專案，然後選取**提交 HDInsight 上的 tooStorm**。</span><span class="sxs-lookup"><span data-stu-id="583bf-211">From **Solution Explorer**, right-click hello **EventHubReader** project, and select **Submit tooStorm on HDInsight**.</span></span>

    ![螢幕擷取畫面的方案總管 中，以反白顯示的 HDInsight 上送出 tooStorm](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. <span data-ttu-id="583bf-213">在 hello**提交拓撲**對話方塊中，選取您**Storm 叢集**。</span><span class="sxs-lookup"><span data-stu-id="583bf-213">On hello **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="583bf-214">展開**額外的組態**，選取**Java 檔案路徑**，選取**...**，並選取 hello 目錄，包含您先前下載的 hello JAR 檔案。</span><span class="sxs-lookup"><span data-stu-id="583bf-214">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select hello directory that contains hello JAR file that you downloaded earlier.</span></span> <span data-ttu-id="583bf-215">最後，按一下 [提交]。</span><span class="sxs-lookup"><span data-stu-id="583bf-215">Finally, click **Submit**.</span></span>

    ![[提交拓撲] 對話方塊的螢幕擷取畫面](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. <span data-ttu-id="583bf-217">當已送出 hello 拓樸時，hello **Storm 拓撲檢視器**隨即出現。</span><span class="sxs-lookup"><span data-stu-id="583bf-217">When hello topology has been submitted, hello **Storm Topologies Viewer** appears.</span></span> <span data-ttu-id="583bf-218">tooview 資訊 hello 拓撲中，選取 hello **EventHubReader** hello 左窗格中的拓撲。</span><span class="sxs-lookup"><span data-stu-id="583bf-218">tooview information about hello topology, select hello **EventHubReader** topology in hello left pane.</span></span>

    ![Storm 拓撲檢視器的螢幕擷取畫面](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. <span data-ttu-id="583bf-220">從**方案總管 中**，以滑鼠右鍵按一下 hello **EventHubWriter**專案，然後選取**提交 HDInsight 上的 tooStorm**。</span><span class="sxs-lookup"><span data-stu-id="583bf-220">From **Solution Explorer**, right-click hello **EventHubWriter** project, and select **Submit tooStorm on HDInsight**.</span></span>

5. <span data-ttu-id="583bf-221">在 hello**提交拓撲**對話方塊中，選取您**Storm 叢集**。</span><span class="sxs-lookup"><span data-stu-id="583bf-221">On hello **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="583bf-222">展開**額外的組態**，選取**Java 檔案路徑**，選取**...**，並選取 hello 目錄，包含 hello JAR 檔案您之前下載。</span><span class="sxs-lookup"><span data-stu-id="583bf-222">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select hello directory that contains hello JAR file you downloaded earlier.</span></span> <span data-ttu-id="583bf-223">最後，按一下 [提交]。</span><span class="sxs-lookup"><span data-stu-id="583bf-223">Finally, click **Submit**.</span></span>

6. <span data-ttu-id="583bf-224">當已送出 hello 拓樸時，重新整理 hello 拓撲清單，在 hello **Storm 拓撲檢視器**tooverify hello 叢集上執行這兩種拓撲。</span><span class="sxs-lookup"><span data-stu-id="583bf-224">When hello topology has been submitted, refresh hello topology list in hello **Storm Topologies Viewer** tooverify that both topologies are running on hello cluster.</span></span>

7. <span data-ttu-id="583bf-225">在**Storm 拓撲檢視器**，選取 hello **EventHubReader**拓撲。</span><span class="sxs-lookup"><span data-stu-id="583bf-225">In **Storm Topologies Viewer**, select hello **EventHubReader** topology.</span></span>

8. <span data-ttu-id="583bf-226">tooopen hello 元件摘要 hello 閃電按兩下 hello **LogBolt** hello 圖表中的元件。</span><span class="sxs-lookup"><span data-stu-id="583bf-226">tooopen hello component summary for hello bolt, double-click hello **LogBolt** component in hello diagram.</span></span>

9. <span data-ttu-id="583bf-227">在 hello**執行程式**區段中，選取其中一個 hello 連結在 hello**連接埠**資料行。</span><span class="sxs-lookup"><span data-stu-id="583bf-227">In hello **Executors** section, select one of hello links in hello **Port** column.</span></span> <span data-ttu-id="583bf-228">這會顯示 hello 元件所記錄的資訊。</span><span class="sxs-lookup"><span data-stu-id="583bf-228">This displays information logged by hello component.</span></span> <span data-ttu-id="583bf-229">為下列文字類似 toohello hello 登入資訊：</span><span class="sxs-lookup"><span data-stu-id="583bf-229">hello logged information is similar toohello following text:</span></span>

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-hello-topologies"></a><span data-ttu-id="583bf-230">停止 hello 拓撲</span><span class="sxs-lookup"><span data-stu-id="583bf-230">Stop hello topologies</span></span>

<span data-ttu-id="583bf-231">toostop hello 拓撲中，選取每種拓撲中 hello **Storm 拓撲檢視器**，然後按一下  **Kill**。</span><span class="sxs-lookup"><span data-stu-id="583bf-231">toostop hello topologies, select each topology in hello **Storm Topology Viewer**, then click **Kill**.</span></span>

![Storm 拓撲檢視器的螢幕擷取畫面，已反白顯示 [終止] 按鈕](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="583bf-233">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="583bf-233">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="583bf-234">後續步驟</span><span class="sxs-lookup"><span data-stu-id="583bf-234">Next steps</span></span>

<span data-ttu-id="583bf-235">在本文件中，您已經學會如何 toouse hello Java 事件中樞 spout 與從 Azure 事件中心中的資料與 C# 拓撲 toowork 閃電。</span><span class="sxs-lookup"><span data-stu-id="583bf-235">In this document, you have learned how toouse hello Java Event Hubs spout and bolt from a C# topology toowork with data in Azure Event Hubs.</span></span> <span data-ttu-id="583bf-236">toolearn 進一步了解建立 C# 拓撲，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="583bf-236">toolearn more about creating C# topologies, see hello following:</span></span>

* [<span data-ttu-id="583bf-237">使用 Visual Studio 開發 Apache Storm on HDInsight 的 C# 拓撲</span><span class="sxs-lookup"><span data-stu-id="583bf-237">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="583bf-238">SCP 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="583bf-238">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)
* [<span data-ttu-id="583bf-239">Storm on HDInsight 的範例拓撲</span><span class="sxs-lookup"><span data-stu-id="583bf-239">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
