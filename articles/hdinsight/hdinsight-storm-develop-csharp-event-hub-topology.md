---
title: "在事件中樞內使用 Storm 來處理事件 - Azure HDInsight | Microsoft Docs"
description: "了解如何利用在 Visual Studio 中使用 HDInsight Tools for Visual Studio 所建立之 C# Storm 拓撲來處理 Azure 事件中樞的資料。"
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
ms.openlocfilehash: 4b6fd87b057d93175d3ef284238d77be3bdde61d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a><span data-ttu-id="b66eb-103">利用 Storm on HDInsight 處理 Azure 事件中樞的事件 (C#)</span><span class="sxs-lookup"><span data-stu-id="b66eb-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>

<span data-ttu-id="b66eb-104">了解如何從 Apache Storm on HDInsight 處理 Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="b66eb-104">Learn how to work with Azure Event Hubs from Apache Storm on HDInsight.</span></span> <span data-ttu-id="b66eb-105">本文件使用 C# Storm 拓撲來從事件中樞讀取和寫入資料</span><span class="sxs-lookup"><span data-stu-id="b66eb-105">This document uses a C# Storm topology to read and write data from Evbent Hubs</span></span>

> [!NOTE]
> <span data-ttu-id="b66eb-106">如需本專案的 Java 版本，請參閱[使用 Storm on HDInsight 處理 Azure 事件中樞的事件 (Java)](hdinsight-storm-develop-java-event-hub-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="b66eb-106">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="scpnet"></a><span data-ttu-id="b66eb-107">SCP.NET</span><span class="sxs-lookup"><span data-stu-id="b66eb-107">SCP.NET</span></span>

<span data-ttu-id="b66eb-108">本文件中的步驟使用 SCP.NET，其為 NuGet 套件，可方便您建立 C# 拓撲和元件來與 Storm on HDInsight 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="b66eb-108">The steps in this document use SCP.NET, a NuGet package that makes it easy to create C# topologies and components for use with Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b66eb-109">雖然本文件中的步驟依賴 Windows 開發環境與 Visual Studio，但已編譯的專案可以提交到使用 Linux 之 HDInsight 叢集上的 Storm。</span><span class="sxs-lookup"><span data-stu-id="b66eb-109">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to a Storm on HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="b66eb-110">只有在 2016 年 10 月 28 日之後所建立之以 Linux 為基礎的叢集可支援 SCP.NET 拓撲。</span><span class="sxs-lookup"><span data-stu-id="b66eb-110">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="b66eb-111">HDInsight 3.4 和更高版本使用單聲道來執行 C# 拓撲。</span><span class="sxs-lookup"><span data-stu-id="b66eb-111">HDInsight 3.4 and greater use Mono to run C# topologies.</span></span> <span data-ttu-id="b66eb-112">本文件中使用的範例會使用 HDInsight 3.6。</span><span class="sxs-lookup"><span data-stu-id="b66eb-112">The example used in this document works with HDInsight 3.6.</span></span> <span data-ttu-id="b66eb-113">如果您打算針對 HDInsight 來建立您自己的 .NET 解決方案，請參閱 [Mono 相容性](http://www.mono-project.com/docs/about-mono/compatibility/)文件，以了解可能不相容之處。</span><span class="sxs-lookup"><span data-stu-id="b66eb-113">If you plan on creating your own .NET solutions for HDInsight, check the [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>

### <a name="cluster-versioning"></a><span data-ttu-id="b66eb-114">叢集版本控制</span><span class="sxs-lookup"><span data-stu-id="b66eb-114">Cluster versioning</span></span>

<span data-ttu-id="b66eb-115">用於專案的 Microsoft.SCP.Net.SDK NuGet 套件必須符合安裝在 HDInsight 上的 Storm 主要版本。</span><span class="sxs-lookup"><span data-stu-id="b66eb-115">The Microsoft.SCP.Net.SDK NuGet package you use for your project must match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="b66eb-116">HDInsight 3.5 版及 3.6 版使用 Storm 1.x 版，因此您必須搭配使用 SCP.NET 1.0.x.x 版與這些叢集。</span><span class="sxs-lookup"><span data-stu-id="b66eb-116">HDInsight versions 3.5 and 3.6 use Storm 1.x, so you must use SCP.NET version 1.0.x.x with these clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b66eb-117">本文件中的範例預期使用 HDInsight 3.5 或 3.6 叢集。</span><span class="sxs-lookup"><span data-stu-id="b66eb-117">The example in this document expects an HDInsight 3.5 or 3.6 cluster.</span></span>
>
> <span data-ttu-id="b66eb-118">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="b66eb-118">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b66eb-119">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="b66eb-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="b66eb-120">C# 拓撲也必須以 .NET 4.5 為目標。</span><span class="sxs-lookup"><span data-stu-id="b66eb-120">C# topologies must also target .NET 4.5.</span></span>

## <a name="how-to-work-with-event-hubs"></a><span data-ttu-id="b66eb-121">如何使用事件中樞</span><span class="sxs-lookup"><span data-stu-id="b66eb-121">How to work with Event Hubs</span></span>

<span data-ttu-id="b66eb-122">Microsoft 提供一組可用來從 Storm 拓撲與事件中樞通訊的 Java 元件。</span><span class="sxs-lookup"><span data-stu-id="b66eb-122">Microsoft provides a set of Java components that can be used to communicate with Event Hubs from a Storm topology.</span></span> <span data-ttu-id="b66eb-123">您可以在 [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar) 找到內含這些元件之 HDInsight 3.6 相容版本的 Java 封存檔 (JAR) 檔案。</span><span class="sxs-lookup"><span data-stu-id="b66eb-123">You can find the Java archive (JAR) file that contains an HDInsight 3.6 compatible version of these components at [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b66eb-124">雖然元件是以 Java 所撰寫，您可以輕鬆地從 C# 拓撲使用它們。</span><span class="sxs-lookup"><span data-stu-id="b66eb-124">While the components are written in Java, you can easily use them from a C# topology.</span></span>

<span data-ttu-id="b66eb-125">在此範例中會使用下列元件：</span><span class="sxs-lookup"><span data-stu-id="b66eb-125">The following components are used in this example:</span></span>

* <span data-ttu-id="b66eb-126">__EventHubSpout__：從事件中樞讀取資料。</span><span class="sxs-lookup"><span data-stu-id="b66eb-126">__EventHubSpout__: Reads data from Event Hubs.</span></span>
* <span data-ttu-id="b66eb-127">__EventHubBolt__：將資料寫入事件中樞。</span><span class="sxs-lookup"><span data-stu-id="b66eb-127">__EventHubBolt__: Writes data to Event Hubs.</span></span>
* <span data-ttu-id="b66eb-128">__EventHubSpoutConfig__：用來設定 EventHubSpout。</span><span class="sxs-lookup"><span data-stu-id="b66eb-128">__EventHubSpoutConfig__: Used to configure EventHubSpout.</span></span>
* <span data-ttu-id="b66eb-129">__EventHubBoltConfig__：用來設定 EventHubBolt。</span><span class="sxs-lookup"><span data-stu-id="b66eb-129">__EventHubBoltConfig__: Used to configure EventHubBolt.</span></span>

### <a name="example-spout-usage"></a><span data-ttu-id="b66eb-130">範例 Spout 使用方式</span><span class="sxs-lookup"><span data-stu-id="b66eb-130">Example spout usage</span></span>

<span data-ttu-id="b66eb-131">SCP.NET 會提供將 EventHubSpout 新增至您拓撲的方法。</span><span class="sxs-lookup"><span data-stu-id="b66eb-131">SCP.NET provides methods for adding an EventHubSpout to your topology.</span></span> <span data-ttu-id="b66eb-132">這些方法比使用泛型方法新增 Java 元件更容易新增 Spout。</span><span class="sxs-lookup"><span data-stu-id="b66eb-132">These methods make it easier to add a spout than using the generic methods for adding a Java component.</span></span> <span data-ttu-id="b66eb-133">下列範例示範如何使用 SCP.NET 所提供的 __SetEventHubSpout__ 和 **EventHubSpoutConfig** 方法建立 Spout：</span><span class="sxs-lookup"><span data-stu-id="b66eb-133">The following example demonstrates how to create a spout by using the __SetEventHubSpout__ and **EventHubSpoutConfig** methods provided by SCP.NET:</span></span>

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

<span data-ttu-id="b66eb-134">前一個範例會建立名為 __EventHubSpout__ 的新 Spout 元件，並設定它與事件中樞通訊。</span><span class="sxs-lookup"><span data-stu-id="b66eb-134">The previous example creates a new spout component named __EventHubSpout__, and configures it to communicate with an event hub.</span></span> <span data-ttu-id="b66eb-135">元件的平行處理原則提示設定為事件中樞的資料分割數目。</span><span class="sxs-lookup"><span data-stu-id="b66eb-135">The parallelism hint for the component is set to the number of partitions in the event hub.</span></span> <span data-ttu-id="b66eb-136">此設定可讓 Storm 針對每個資料分割建立元件執行個體。</span><span class="sxs-lookup"><span data-stu-id="b66eb-136">This setting allows Storm to create an instance of the component for each partition.</span></span>

### <a name="example-bolt-usage"></a><span data-ttu-id="b66eb-137">範例 Bolt 使用方式</span><span class="sxs-lookup"><span data-stu-id="b66eb-137">Example bolt usage</span></span>

<span data-ttu-id="b66eb-138">使用 **JavaComponmentConstructor** 方法來建立 Bolt 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="b66eb-138">Use the **JavaComponmentConstructor** method to create an instance of the bolt.</span></span> <span data-ttu-id="b66eb-139">下列範例示範如何建立及設定 **EventHubBolt** 的新執行個體：</span><span class="sxs-lookup"><span data-stu-id="b66eb-139">The following example demonstrates how to create and configure a new instance of the **EventHubBolt**:</span></span>

```csharp
// Java construcvtor for the Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set the bolt to subscribe to data from the spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> <span data-ttu-id="b66eb-140">這個範例會使用以字串傳遞的 Clojure 運算式，而不是如 Spout 範例一樣使用 **JavaComponentConstructor** 來建立 **EventHubBoltConfig**。</span><span class="sxs-lookup"><span data-stu-id="b66eb-140">This example uses a Clojure expression passed as a string, instead of using **JavaComponentConstructor** to create an **EventHubBoltConfig**, as the spout example did.</span></span> <span data-ttu-id="b66eb-141">兩種方法均可。</span><span class="sxs-lookup"><span data-stu-id="b66eb-141">Either method works.</span></span> <span data-ttu-id="b66eb-142">使用覺得較適合您的方法。</span><span class="sxs-lookup"><span data-stu-id="b66eb-142">Use the method that feels best to you.</span></span>

## <a name="download-the-completed-project"></a><span data-ttu-id="b66eb-143">下載完成的專案</span><span class="sxs-lookup"><span data-stu-id="b66eb-143">Download the completed project</span></span>

<span data-ttu-id="b66eb-144">您可以從 [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub) 下載本教學課程中所建立之專案的完整版本。</span><span class="sxs-lookup"><span data-stu-id="b66eb-144">You can download a complete version of the project created in this tutorial from [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span> <span data-ttu-id="b66eb-145">不過，您仍需要遵循本教學課程中的步驟，提供組態設定。</span><span class="sxs-lookup"><span data-stu-id="b66eb-145">However, you still need to provide configuration settings by following the steps in this tutorial.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="b66eb-146">必要條件</span><span class="sxs-lookup"><span data-stu-id="b66eb-146">Prerequisites</span></span>

* <span data-ttu-id="b66eb-147">[Apache Storm on HDInsight 叢集 3.5 或 3.6 版](hdinsight-apache-storm-tutorial-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="b66eb-147">An [Apache Storm on HDInsight cluster version 3.5 or 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span></span>

    > [!WARNING]
    > <span data-ttu-id="b66eb-148">此文件中所使用的範例需要 Storm on HDInsight version 3.5 或 3.6 版。</span><span class="sxs-lookup"><span data-stu-id="b66eb-148">The example used in this document requires Storm on HDInsight version 3.5 or 3.6.</span></span> <span data-ttu-id="b66eb-149">由於重大類別名稱變更，這不適用舊版的 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="b66eb-149">This does not work with older versions of HDInsight, due to breaking class name changes.</span></span> <span data-ttu-id="b66eb-150">如需這個範例適用於較舊叢集的版本，請參閱 [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases)。</span><span class="sxs-lookup"><span data-stu-id="b66eb-150">For a version of this example that works with older clusters, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span></span>

* <span data-ttu-id="b66eb-151">[Azure 事件中樞](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)。</span><span class="sxs-lookup"><span data-stu-id="b66eb-151">An [Azure event hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="b66eb-152">[Azure .NET SDK](http://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="b66eb-152">The [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>

* <span data-ttu-id="b66eb-153">[HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="b66eb-153">The [HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="b66eb-154">開發環境有 Java JDK 1.8 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b66eb-154">Java JDK 1.8 or later on your development environment.</span></span> <span data-ttu-id="b66eb-155">JDK 下載檔可從 [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 取得。</span><span class="sxs-lookup"><span data-stu-id="b66eb-155">JDK downloads are available from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

  * <span data-ttu-id="b66eb-156">**JAVA_HOME** 環境變數必須指向包含 Java 的目錄。</span><span class="sxs-lookup"><span data-stu-id="b66eb-156">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span></span>
  * <span data-ttu-id="b66eb-157">**%JAVA_HOME%/bin** 目錄必須在此路徑中。</span><span class="sxs-lookup"><span data-stu-id="b66eb-157">The **%JAVA_HOME%/bin** directory must be in the path.</span></span>

## <a name="download-the-event-hubs-components"></a><span data-ttu-id="b66eb-158">下載事件中樞元件</span><span class="sxs-lookup"><span data-stu-id="b66eb-158">Download the Event Hubs components</span></span>

<span data-ttu-id="b66eb-159">從 [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar) 下載事件中樞 Spout 和 Bolt 元件。</span><span class="sxs-lookup"><span data-stu-id="b66eb-159">Download the Event Hubs spout and bolt component from [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

<span data-ttu-id="b66eb-160">請建立名為 `eventhubspout` 的目錄，並將檔案儲存到該目錄。</span><span class="sxs-lookup"><span data-stu-id="b66eb-160">Create a directory named `eventhubspout`, and save the file into the directory.</span></span>

## <a name="configure-event-hubs"></a><span data-ttu-id="b66eb-161">設定事件中樞</span><span class="sxs-lookup"><span data-stu-id="b66eb-161">Configure Event Hubs</span></span>

<span data-ttu-id="b66eb-162">事件中樞是此範例的資料來源。</span><span class="sxs-lookup"><span data-stu-id="b66eb-162">Event Hubs is the data source for this example.</span></span> <span data-ttu-id="b66eb-163">請使用[開始使用事件中樞](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)的＜建立事件中樞＞一節中的資訊。</span><span class="sxs-lookup"><span data-stu-id="b66eb-163">Use the information in the "Create an event hub" section of [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

1. <span data-ttu-id="b66eb-164">在建立事件中樞之後，檢視 Azure 入口網站中的 [事件中樞] 刀鋒視窗，然後選取 [共用存取原則]。</span><span class="sxs-lookup"><span data-stu-id="b66eb-164">After the event hub has been created, view the **EventHub** blade in the Azure portal, and select **Shared access policies**.</span></span> <span data-ttu-id="b66eb-165">選取 [+ 新增] 連結來新增下列原則︰</span><span class="sxs-lookup"><span data-stu-id="b66eb-165">Select **+ Add** to add the following policies:</span></span>

   | <span data-ttu-id="b66eb-166">名稱</span><span class="sxs-lookup"><span data-stu-id="b66eb-166">Name</span></span> | <span data-ttu-id="b66eb-167">權限</span><span class="sxs-lookup"><span data-stu-id="b66eb-167">Permissions</span></span> |
   | --- | --- |
   | <span data-ttu-id="b66eb-168">寫入器</span><span class="sxs-lookup"><span data-stu-id="b66eb-168">writer</span></span> |<span data-ttu-id="b66eb-169">傳送</span><span class="sxs-lookup"><span data-stu-id="b66eb-169">Send</span></span> |
   | <span data-ttu-id="b66eb-170">讀取器</span><span class="sxs-lookup"><span data-stu-id="b66eb-170">reader</span></span> |<span data-ttu-id="b66eb-171">接聽</span><span class="sxs-lookup"><span data-stu-id="b66eb-171">Listen</span></span> |

    ![[共用存取原則] 視窗的螢幕擷取畫面](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. <span data-ttu-id="b66eb-173">選取 [讀取器] 和 [寫入器] 原則。</span><span class="sxs-lookup"><span data-stu-id="b66eb-173">Select the **reader** and **writer** policies.</span></span> <span data-ttu-id="b66eb-174">複製並儲存這兩個原則的主索引鍵值，因為稍後將使用這些值。</span><span class="sxs-lookup"><span data-stu-id="b66eb-174">Copy and save the primary key value for both policies, as these values are used later.</span></span>

## <a name="configure-the-eventhubwriter"></a><span data-ttu-id="b66eb-175">設定 EventHubWriter</span><span class="sxs-lookup"><span data-stu-id="b66eb-175">Configure the EventHubWriter</span></span>

1. <span data-ttu-id="b66eb-176">如果您尚未安裝最新版本的 HDInsight Tools for Visual Studio，請參閱[開始使用 HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="b66eb-176">If you have not already installed the latest version of the HDInsight tools for Visual Studio, see [Get started using HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="b66eb-177">從 [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub) 下載方案。</span><span class="sxs-lookup"><span data-stu-id="b66eb-177">Download the solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

3. <span data-ttu-id="b66eb-178">在 **EventHubWriter** 專案中，開啟 **App.config** 檔案。</span><span class="sxs-lookup"><span data-stu-id="b66eb-178">In the **EventHubWriter** project, open the **App.config** file.</span></span> <span data-ttu-id="b66eb-179">使用事件中樞內您稍早設定的資訊填入下列索引鍵的值：</span><span class="sxs-lookup"><span data-stu-id="b66eb-179">Use the information from the event hub that you configured earlier to fill in the value for the following keys:</span></span>

   | <span data-ttu-id="b66eb-180">Key</span><span class="sxs-lookup"><span data-stu-id="b66eb-180">Key</span></span> | <span data-ttu-id="b66eb-181">值</span><span class="sxs-lookup"><span data-stu-id="b66eb-181">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="b66eb-182">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="b66eb-182">EventHubPolicyName</span></span> |<span data-ttu-id="b66eb-183">寫入器 (如果您為具有*傳送*權限的原則使用了不同名稱，請改用該名稱。)</span><span class="sxs-lookup"><span data-stu-id="b66eb-183">writer (If you used a different name for the policy with *Send* permission, use it instead.)</span></span> |
   | <span data-ttu-id="b66eb-184">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="b66eb-184">EventHubPolicyKey</span></span> |<span data-ttu-id="b66eb-185">寫入器原則的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b66eb-185">The key for the writer policy.</span></span> |
   | <span data-ttu-id="b66eb-186">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="b66eb-186">EventHubNamespace</span></span> |<span data-ttu-id="b66eb-187">包含事件中樞的命名空間。</span><span class="sxs-lookup"><span data-stu-id="b66eb-187">The namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="b66eb-188">EventHubName</span><span class="sxs-lookup"><span data-stu-id="b66eb-188">EventHubName</span></span> |<span data-ttu-id="b66eb-189">事件中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="b66eb-189">Your event hub name.</span></span> |
   | <span data-ttu-id="b66eb-190">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="b66eb-190">EventHubPartitionCount</span></span> |<span data-ttu-id="b66eb-191">事件中樞內的資料分割數目。</span><span class="sxs-lookup"><span data-stu-id="b66eb-191">The number of partitions in your event hub.</span></span> |

4. <span data-ttu-id="b66eb-192">儲存並關閉 **App.config** 檔案。</span><span class="sxs-lookup"><span data-stu-id="b66eb-192">Save and close the **App.config** file.</span></span>

## <a name="configure-the-eventhubreader"></a><span data-ttu-id="b66eb-193">設定 EventHubReader</span><span class="sxs-lookup"><span data-stu-id="b66eb-193">Configure the EventHubReader</span></span>

1. <span data-ttu-id="b66eb-194">開啟 **EventHubReader** 專案。</span><span class="sxs-lookup"><span data-stu-id="b66eb-194">Open the **EventHubReader** project.</span></span>

2. <span data-ttu-id="b66eb-195">開啟 **EventHubReader** 的 **App.config** 檔案。</span><span class="sxs-lookup"><span data-stu-id="b66eb-195">Open the **App.config** file for the **EventHubReader**.</span></span> <span data-ttu-id="b66eb-196">使用事件中樞內您稍早設定的資訊填入下列索引鍵的值：</span><span class="sxs-lookup"><span data-stu-id="b66eb-196">Use the information from the event hub that you configured earlier to fill in the value for the following keys:</span></span>

   | <span data-ttu-id="b66eb-197">Key</span><span class="sxs-lookup"><span data-stu-id="b66eb-197">Key</span></span> | <span data-ttu-id="b66eb-198">值</span><span class="sxs-lookup"><span data-stu-id="b66eb-198">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="b66eb-199">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="b66eb-199">EventHubPolicyName</span></span> |<span data-ttu-id="b66eb-200">讀取器 (如果您為具有*接聽*權限的原則使用了不同名稱，請改用該名稱。)</span><span class="sxs-lookup"><span data-stu-id="b66eb-200">reader (If you used a different name for the policy with *listen* permission, use it instead.)</span></span> |
   | <span data-ttu-id="b66eb-201">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="b66eb-201">EventHubPolicyKey</span></span> |<span data-ttu-id="b66eb-202">讀取器原則的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b66eb-202">The key for the reader policy.</span></span> |
   | <span data-ttu-id="b66eb-203">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="b66eb-203">EventHubNamespace</span></span> |<span data-ttu-id="b66eb-204">包含事件中樞的命名空間。</span><span class="sxs-lookup"><span data-stu-id="b66eb-204">The namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="b66eb-205">EventHubName</span><span class="sxs-lookup"><span data-stu-id="b66eb-205">EventHubName</span></span> |<span data-ttu-id="b66eb-206">事件中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="b66eb-206">Your event hub name.</span></span> |
   | <span data-ttu-id="b66eb-207">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="b66eb-207">EventHubPartitionCount</span></span> |<span data-ttu-id="b66eb-208">事件中樞內的資料分割數目。</span><span class="sxs-lookup"><span data-stu-id="b66eb-208">The number of partitions in your event hub.</span></span> |

3. <span data-ttu-id="b66eb-209">儲存並關閉 **App.config** 檔案。</span><span class="sxs-lookup"><span data-stu-id="b66eb-209">Save and close the **App.config** file.</span></span>

## <a name="deploy-the-topologies"></a><span data-ttu-id="b66eb-210">部署拓撲</span><span class="sxs-lookup"><span data-stu-id="b66eb-210">Deploy the topologies</span></span>

1. <span data-ttu-id="b66eb-211">在 [方案總管] 中，以滑鼠右鍵按一下 [EventHubReader] 專案，然後選取 [提交到 Storm on HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="b66eb-211">From **Solution Explorer**, right-click the **EventHubReader** project, and select **Submit to Storm on HDInsight**.</span></span>

    ![[方案總管] 的螢幕擷取畫面，已反白顯示 [提交到 Storm on HDInsight]](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. <span data-ttu-id="b66eb-213">在 [提交拓撲] 對話方塊中，選取您的 [Storm 叢集]。</span><span class="sxs-lookup"><span data-stu-id="b66eb-213">On the **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="b66eb-214">展開 [其他設定]，依序選取 [Java 檔案路徑]、[...]，然後選取包含您稍早下載之 JAR 檔的目錄。</span><span class="sxs-lookup"><span data-stu-id="b66eb-214">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select the directory that contains the JAR file that you downloaded earlier.</span></span> <span data-ttu-id="b66eb-215">最後，按一下 [提交]。</span><span class="sxs-lookup"><span data-stu-id="b66eb-215">Finally, click **Submit**.</span></span>

    ![[提交拓撲] 對話方塊的螢幕擷取畫面](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. <span data-ttu-id="b66eb-217">提交拓撲之後，[Storm 拓撲檢視器] 便會隨即出現。</span><span class="sxs-lookup"><span data-stu-id="b66eb-217">When the topology has been submitted, the **Storm Topologies Viewer** appears.</span></span> <span data-ttu-id="b66eb-218">若要檢視拓撲的相關資訊，請選取左窗格中的 **EventHubReader** 拓撲。</span><span class="sxs-lookup"><span data-stu-id="b66eb-218">To view information about the topology, select the **EventHubReader** topology in the left pane.</span></span>

    ![Storm 拓撲檢視器的螢幕擷取畫面](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. <span data-ttu-id="b66eb-220">在 [方案總管] 中，以滑鼠右鍵按一下 [EventHubWriter] 專案，然後選取 [提交到 Storm on HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="b66eb-220">From **Solution Explorer**, right-click the **EventHubWriter** project, and select **Submit to Storm on HDInsight**.</span></span>

5. <span data-ttu-id="b66eb-221">在 [提交拓撲] 對話方塊中，選取您的 [Storm 叢集]。</span><span class="sxs-lookup"><span data-stu-id="b66eb-221">On the **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="b66eb-222">展開 [其他設定]，依序選取 [Java 檔案路徑]、[...]，然後選取包含您稍早下載之 JAR 檔的目錄。</span><span class="sxs-lookup"><span data-stu-id="b66eb-222">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select the directory that contains the JAR file you downloaded earlier.</span></span> <span data-ttu-id="b66eb-223">最後，按一下 [提交]。</span><span class="sxs-lookup"><span data-stu-id="b66eb-223">Finally, click **Submit**.</span></span>

6. <span data-ttu-id="b66eb-224">提交拓撲之後，請重新整理 [Storm 拓撲檢視器]  中的拓撲清單，以確認兩個拓撲皆在叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="b66eb-224">When the topology has been submitted, refresh the topology list in the **Storm Topologies Viewer** to verify that both topologies are running on the cluster.</span></span>

7. <span data-ttu-id="b66eb-225">在 [Storm 拓撲檢視器] 中，選取 [EventHubReader] 拓撲。</span><span class="sxs-lookup"><span data-stu-id="b66eb-225">In **Storm Topologies Viewer**, select the **EventHubReader** topology.</span></span>

8. <span data-ttu-id="b66eb-226">若要開啟 Bolt 的元件摘要，請按兩下圖表中的 **LogBolt** 元件。</span><span class="sxs-lookup"><span data-stu-id="b66eb-226">To open the component summary for the bolt, double-click the **LogBolt** component in the diagram.</span></span>

9. <span data-ttu-id="b66eb-227">在 [執行程式] 區段中，選取 [連接埠] 資料行內的其中一個連結。</span><span class="sxs-lookup"><span data-stu-id="b66eb-227">In the **Executors** section, select one of the links in the **Port** column.</span></span> <span data-ttu-id="b66eb-228">這會顯示該元件記錄的資訊。</span><span class="sxs-lookup"><span data-stu-id="b66eb-228">This displays information logged by the component.</span></span> <span data-ttu-id="b66eb-229">所記錄的資訊類似下列文字︰</span><span class="sxs-lookup"><span data-stu-id="b66eb-229">The logged information is similar to the following text:</span></span>

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-the-topologies"></a><span data-ttu-id="b66eb-230">停止拓撲</span><span class="sxs-lookup"><span data-stu-id="b66eb-230">Stop the topologies</span></span>

<span data-ttu-id="b66eb-231">若要停止拓撲，請在 [Storm 拓撲檢視器] 中選取每個拓撲，然後選取 [終止]。</span><span class="sxs-lookup"><span data-stu-id="b66eb-231">To stop the topologies, select each topology in the **Storm Topology Viewer**, then click **Kill**.</span></span>

![Storm 拓撲檢視器的螢幕擷取畫面，已反白顯示 [終止] 按鈕](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="b66eb-233">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="b66eb-233">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="b66eb-234">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b66eb-234">Next steps</span></span>

<span data-ttu-id="b66eb-235">在本文件中，您已經了解如何使用 Java 事件中樞 Spout 和 Bolt，以利用 C# 拓撲來使用 Azure 事件中樞的資料。</span><span class="sxs-lookup"><span data-stu-id="b66eb-235">In this document, you have learned how to use the Java Event Hubs spout and bolt from a C# topology to work with data in Azure Event Hubs.</span></span> <span data-ttu-id="b66eb-236">若要深入了解如何建立 C# 拓撲，請參閱下列內容：</span><span class="sxs-lookup"><span data-stu-id="b66eb-236">To learn more about creating C# topologies, see the following:</span></span>

* [<span data-ttu-id="b66eb-237">使用 Visual Studio 開發 Apache Storm on HDInsight 的 C# 拓撲</span><span class="sxs-lookup"><span data-stu-id="b66eb-237">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="b66eb-238">SCP 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="b66eb-238">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)
* [<span data-ttu-id="b66eb-239">Storm on HDInsight 的範例拓撲</span><span class="sxs-lookup"><span data-stu-id="b66eb-239">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
