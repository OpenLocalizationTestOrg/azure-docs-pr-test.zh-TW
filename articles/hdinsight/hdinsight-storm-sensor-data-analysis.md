---
title: "使用 Apache Storm 和 HBase 分析感應器資料 | Microsoft Docs"
description: "了解如何透過虛擬網路連線至 Apache Storm。 搭配使用 Storm 和 HBase 來處理事件中樞的感應器資料，並使用 D3.js 將其視覺化呈現。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: 0d1cc959c87bd64ed728f8b56c9b9156fa492a8b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a><span data-ttu-id="760b1-104">在 HDInsight (Hadoop) 中使用 Apache Storm、事件中樞和 HBase 分析感應器資料</span><span class="sxs-lookup"><span data-stu-id="760b1-104">Analyze sensor data with Apache Storm, Event Hub, and HBase in HDInsight (Hadoop)</span></span>

<span data-ttu-id="760b1-105">了解如何使用 Apache Storm on HDInsight 來處理 Azure 事件中樞的感應器資料。</span><span class="sxs-lookup"><span data-stu-id="760b1-105">Learn how to use Apache Storm on HDInsight to process sensor data from Azure Event Hub.</span></span> <span data-ttu-id="760b1-106">接著將資料儲存至 Apache HBase on HDInsight，並使用 D3.js 以視覺化方式呈現。</span><span class="sxs-lookup"><span data-stu-id="760b1-106">The data is then stored into Apache HBase on HDInsight, and visualized using D3.js.</span></span>

<span data-ttu-id="760b1-107">本文件中使用的 Azure Resource Manager 範本示範如何在一個資源群組中建立多個 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="760b1-107">The Azure Resource Manager template used in this document demonstrates how to create multiple Azure resources in a resource group.</span></span> <span data-ttu-id="760b1-108">此範本會建立一個 Azure 虛擬網路、兩個 HDInsight 叢集 (Storm 和 HBase) 以及一個 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="760b1-108">The template creates an Azure Virtual Network, two HDInsight clusters (Storm and HBase) and an Azure Web App.</span></span> <span data-ttu-id="760b1-109">即時 Web 儀表板的 node.js 實作會自動部署至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="760b1-109">A node.js implementation of a real-time web dashboard is automatically deployed to the web app.</span></span>

> [!NOTE]
> <span data-ttu-id="760b1-110">本文件中的資訊與範例都需要 HDInsight 3.6 版。</span><span class="sxs-lookup"><span data-stu-id="760b1-110">The information in this document and example in this document require HDInsight version 3.6.</span></span>
>
> <span data-ttu-id="760b1-111">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="760b1-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="760b1-112">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="760b1-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="760b1-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="760b1-113">Prerequisites</span></span>

* <span data-ttu-id="760b1-114">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="760b1-114">An Azure subscription.</span></span>
* <span data-ttu-id="760b1-115">[Node.js](http://nodejs.org/)︰用來在您的開發環境中於本機預覽 Web 儀表板。</span><span class="sxs-lookup"><span data-stu-id="760b1-115">[Node.js](http://nodejs.org/): Used to preview the web dashboard locally on your development environment.</span></span>
* <span data-ttu-id="760b1-116">[Java 和 JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html)︰用來開發 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="760b1-116">[Java and the JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): Used to develop the Storm topology.</span></span>
* <span data-ttu-id="760b1-117">[Maven](http://maven.apache.org/what-is-maven.html)︰用來建置和編譯專案。</span><span class="sxs-lookup"><span data-stu-id="760b1-117">[Maven](http://maven.apache.org/what-is-maven.html): Used to build and compile the project.</span></span>
* <span data-ttu-id="760b1-118">[Git](http://git-scm.com/)︰用來從 GitHub 下載專案。</span><span class="sxs-lookup"><span data-stu-id="760b1-118">[Git](http://git-scm.com/): Used to download the project from GitHub.</span></span>
* <span data-ttu-id="760b1-119">**SSH 用戶端** ︰用來連接至以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="760b1-119">An **SSH** client: Used to connect to the Linux-based HDInsight clusters.</span></span> <span data-ttu-id="760b1-120">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="760b1-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="760b1-121">您不需刪除現有的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="760b1-121">You do not need an existing HDInsight cluster.</span></span> <span data-ttu-id="760b1-122">本文件中的步驟會建立下列資源：</span><span class="sxs-lookup"><span data-stu-id="760b1-122">The steps in this document create the following resources:</span></span>
> 
> * <span data-ttu-id="760b1-123">Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="760b1-123">An Azure Virtual Network</span></span>
> * <span data-ttu-id="760b1-124">Storm on HDInsight 叢集 (以 Linux 為基礎，兩個背景工作節點)</span><span class="sxs-lookup"><span data-stu-id="760b1-124">A Storm on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="760b1-125">HBase on HDInsight 叢集 (以 Linux 為基礎，兩個背景工作節點)</span><span class="sxs-lookup"><span data-stu-id="760b1-125">An HBase on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="760b1-126">裝載 Web 儀表板的 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="760b1-126">An Azure Web App that hosts the web dashboard</span></span>

## <a name="architecture"></a><span data-ttu-id="760b1-127">架構</span><span class="sxs-lookup"><span data-stu-id="760b1-127">Architecture</span></span>

![架構圖表](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

<span data-ttu-id="760b1-129">此範例由下列元件組成：</span><span class="sxs-lookup"><span data-stu-id="760b1-129">This example consists of the following components:</span></span>

* <span data-ttu-id="760b1-130">**Azure 事件中樞**：包含從感應器收集的資料。</span><span class="sxs-lookup"><span data-stu-id="760b1-130">**Azure Event Hubs**: Contains data that is collected from sensors.</span></span>
* <span data-ttu-id="760b1-131">**Storm on HDInsight**：即時處理事件中樞的資料。</span><span class="sxs-lookup"><span data-stu-id="760b1-131">**Storm on HDInsight**: Provides real-time processing of data from Event Hub.</span></span>
* <span data-ttu-id="760b1-132">**HBase on HDInsight**：針對 Storm 所處理過的資料，提供持續的 NoSQL 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="760b1-132">**HBase on HDInsight**: Provides a persistent NoSQL data store for data after it has been processed by Storm.</span></span>
* <span data-ttu-id="760b1-133">**Azure 虛擬網路服務**：確保 Storm on HDInsight 及 HBase on HDInsight 叢集之間能夠安全通訊。</span><span class="sxs-lookup"><span data-stu-id="760b1-133">**Azure Virtual Network service**: Enables secure communications between the Storm on HDInsight and HBase on HDInsight clusters.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="760b1-134">使用 Java HBase 用戶端 API 時，需要虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="760b1-134">A virtual network is required when using the Java HBase client API.</span></span> <span data-ttu-id="760b1-135">它不會透過 HBase 叢集的公用閘道來公開。</span><span class="sxs-lookup"><span data-stu-id="760b1-135">It is not exposed over the public gateway for HBase clusters.</span></span> <span data-ttu-id="760b1-136">將 HBase 和 Storm 叢集安裝到相同的虛擬網路，可讓 Storm 叢集 (或虛擬網路上的任何其他系統) 直接使用用戶端 API 存取 HBase。</span><span class="sxs-lookup"><span data-stu-id="760b1-136">Installing HBase and Storm clusters into the same virtual network allows the Storm cluster (or any other system on the virtual network) to directly access HBase using client API.</span></span>

* <span data-ttu-id="760b1-137">**儀表板網站**：即時建立資料圖表的範例儀表板。</span><span class="sxs-lookup"><span data-stu-id="760b1-137">**Dashboard website**: An example dashboard that charts data in real time.</span></span>
  
  * <span data-ttu-id="760b1-138">網站會在 Node.js 中實作。</span><span class="sxs-lookup"><span data-stu-id="760b1-138">The website is implemented in Node.js.</span></span>
  * <span data-ttu-id="760b1-139">[Socket.io](http://socket.io/) 用於 Storm 拓撲及網站間的即時通訊。</span><span class="sxs-lookup"><span data-stu-id="760b1-139">[Socket.io](http://socket.io/) is used for real-time communication between the Storm topology and the website.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="760b1-140">使用 Socket.io 進行通訊是實作細節。</span><span class="sxs-lookup"><span data-stu-id="760b1-140">Using Socket.io for communication is an implementation detail.</span></span> <span data-ttu-id="760b1-141">您可以使用任何通訊架構，例如原始 WebSockets 或 SignalR。</span><span class="sxs-lookup"><span data-stu-id="760b1-141">You can use any communications framework, such as raw WebSockets or SignalR.</span></span>

  * <span data-ttu-id="760b1-142">[D3.js](http://d3js.org/) 用於為傳送至網站的資料繪圖。</span><span class="sxs-lookup"><span data-stu-id="760b1-142">[D3.js](http://d3js.org/) is used to graph the data that is sent to the website.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="760b1-143">因為沒有任何支援方法可建立一個同時適用於 Storm 和 HBase 的 HDInsight 叢集，因此必須建立兩個叢集。</span><span class="sxs-lookup"><span data-stu-id="760b1-143">Two clusters are required, as there is no supported method to create one HDInsight cluster for both Storm and HBase.</span></span>

<span data-ttu-id="760b1-144">拓撲會使用 [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) 類別從事件中樞讀取資料，並使用 [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) 類別將資料寫入至 HBase。</span><span class="sxs-lookup"><span data-stu-id="760b1-144">The topology reads data from Event Hub by using the [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) class, and writes data into HBase using the [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) class.</span></span> <span data-ttu-id="760b1-145">與網站之間的通訊必須透過 [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java)來達成。</span><span class="sxs-lookup"><span data-stu-id="760b1-145">Communication with the website is accomplished by using [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span></span>

<span data-ttu-id="760b1-146">下列圖表說明拓撲的配置：</span><span class="sxs-lookup"><span data-stu-id="760b1-146">The following diagram explains the layout of the topology:</span></span>

![拓撲圖](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> <span data-ttu-id="760b1-148">此圖以簡化的方式呈現拓撲。</span><span class="sxs-lookup"><span data-stu-id="760b1-148">This diagram is a simplified view of the topology.</span></span> <span data-ttu-id="760b1-149">系統會針對事件中樞的每個分割區，為各元件建立執行個體。</span><span class="sxs-lookup"><span data-stu-id="760b1-149">An instance of each component is created for each partition in your Event Hub.</span></span> <span data-ttu-id="760b1-150">這些執行個體會分散至叢集的節點上，而資料在節點間路由傳送的情形如下：</span><span class="sxs-lookup"><span data-stu-id="760b1-150">These instances are distributed across the nodes in the cluster, and data is routed between them as follows:</span></span>
> 
> * <span data-ttu-id="760b1-151">從 Spout 傳送至剖析器的資料會經過負載平衡。</span><span class="sxs-lookup"><span data-stu-id="760b1-151">Data from the spout to the parser is load balanced.</span></span>
> * <span data-ttu-id="760b1-152">從剖析器傳送至儀表板及 HBase的資料會依照裝置識別碼分組，讓相同裝置的訊息一律傳送至相同元件。</span><span class="sxs-lookup"><span data-stu-id="760b1-152">Data from the parser to the Dashboard and HBase is grouped by Device ID, so that messages from the same device always flow to the same component.</span></span>

### <a name="topology-components"></a><span data-ttu-id="760b1-153">拓撲元件</span><span class="sxs-lookup"><span data-stu-id="760b1-153">Topology components</span></span>

* <span data-ttu-id="760b1-154">**事件中樞 Spout**：Spout 會作為 Apache Storm 0.10.0 以上版本的一部分提供。</span><span class="sxs-lookup"><span data-stu-id="760b1-154">**Event Hub Spout**: The spout is provided as part of Apache Storm version 0.10.0 and higher.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="760b1-155">此範例中使用的事件中樞 Spout 需要 Storm on HDInsight 叢集 3.5 或 3.6 版。</span><span class="sxs-lookup"><span data-stu-id="760b1-155">The Event Hub spout used in this example requires a Storm on HDInsight cluster version 3.5 or 3.6.</span></span>

* <span data-ttu-id="760b1-156">**ParserBolt.java**：Spout 發出的資料為原始 JSON，有時會一次發出多個事件。</span><span class="sxs-lookup"><span data-stu-id="760b1-156">**ParserBolt.java**: The data that is emitted by the spout is raw JSON, and occasionally more than one event is emitted at a time.</span></span> <span data-ttu-id="760b1-157">此 Bolt 會讀取 Spout 發出的資料，並剖析 JSON 訊息。</span><span class="sxs-lookup"><span data-stu-id="760b1-157">This bolt reads the data emitted by the spout and parses the JSON message.</span></span> <span data-ttu-id="760b1-158">之後 Bolt 會將資料以包含多欄位之 Tuple 的形式發出。</span><span class="sxs-lookup"><span data-stu-id="760b1-158">The bolt then emits the data as a tuple that contains multiple fields.</span></span>
* <span data-ttu-id="760b1-159">**DashboardBolt.java**：此元件示範如何使用 Socket.io 用戶端程式庫，讓 Java 將資料即時傳送至 Web 儀表板。</span><span class="sxs-lookup"><span data-stu-id="760b1-159">**DashboardBolt.java**: This component demonstrates how to use the Socket.io client library for Java to send data in real time to the web dashboard.</span></span>
* <span data-ttu-id="760b1-160">**no-hbase.yaml**：以本機模式執行時使用的拓撲定義。</span><span class="sxs-lookup"><span data-stu-id="760b1-160">**no-hbase.yaml**: The topology definition used when running in local mode.</span></span> <span data-ttu-id="760b1-161">這不會使用到 HBase 的元件。</span><span class="sxs-lookup"><span data-stu-id="760b1-161">It does not use HBase components.</span></span>
* <span data-ttu-id="760b1-162">**with-hbase.yaml**：在叢集上執行拓撲時使用的拓撲定義。</span><span class="sxs-lookup"><span data-stu-id="760b1-162">**with-hbase.yaml**: The topology definition used when running the topology on the cluster.</span></span> <span data-ttu-id="760b1-163">這會使用到 HBase 的元件。</span><span class="sxs-lookup"><span data-stu-id="760b1-163">It does use HBase components.</span></span>
* <span data-ttu-id="760b1-164">**dev.properties**：事件中樞 Spout、HBase Bolt 及儀表板元件的設定資訊。</span><span class="sxs-lookup"><span data-stu-id="760b1-164">**dev.properties**: The configuration information for the Event Hub spout, HBase bolt, and dashboard components.</span></span>

## <a name="prepare-your-environment"></a><span data-ttu-id="760b1-165">準備您的環境</span><span class="sxs-lookup"><span data-stu-id="760b1-165">Prepare your environment</span></span>

<span data-ttu-id="760b1-166">使用此範例之前，您必須建立 Azure 事件中樞以供 Storm 拓撲讀取。</span><span class="sxs-lookup"><span data-stu-id="760b1-166">Before you use this example, you must create an Azure Event Hub, which the Storm topology reads from.</span></span>

### <a name="configure-event-hub"></a><span data-ttu-id="760b1-167">設定事件中樞</span><span class="sxs-lookup"><span data-stu-id="760b1-167">Configure Event Hub</span></span>

<span data-ttu-id="760b1-168">事件中樞是此範例的資料來源。</span><span class="sxs-lookup"><span data-stu-id="760b1-168">Event Hub is the data source for this example.</span></span> <span data-ttu-id="760b1-169">請使用下列步驟來建立事件中樞。</span><span class="sxs-lookup"><span data-stu-id="760b1-169">Use the following steps to create an Event Hub.</span></span>

1. <span data-ttu-id="760b1-170">從 [Azure 入口網站](https://portal.azure.com)，選取 [+新增] -> [物聯網] -> [事件中樞]。</span><span class="sxs-lookup"><span data-stu-id="760b1-170">From the [Azure portal](https://portal.azure.com), select **+ New** -> **Internet of Things** -> **Event Hubs**.</span></span>
2. <span data-ttu-id="760b1-171">在 [建立命名空間] 區段執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="760b1-171">In the **Create Namespace** section, perform the following tasks:</span></span>
   
   1. <span data-ttu-id="760b1-172">輸入命名空間的 **名稱** 。</span><span class="sxs-lookup"><span data-stu-id="760b1-172">Enter a **Name** for the namespace.</span></span>
   2. <span data-ttu-id="760b1-173">選取定價層。</span><span class="sxs-lookup"><span data-stu-id="760b1-173">Select a pricing tier.</span></span> <span data-ttu-id="760b1-174"> 就已足夠。</span><span class="sxs-lookup"><span data-stu-id="760b1-174">**Basic** is sufficient for this example.</span></span>
   3. <span data-ttu-id="760b1-175">選取要使用的 Azure [訂用帳戶]  。</span><span class="sxs-lookup"><span data-stu-id="760b1-175">Select the Azure **Subscription** to use.</span></span>
   4. <span data-ttu-id="760b1-176">選取現有的資源群組，或建立一個新的群組。</span><span class="sxs-lookup"><span data-stu-id="760b1-176">Either select an existing resource group or create a new one.</span></span>
   5. <span data-ttu-id="760b1-177">選取事件中樞的 [位置]  。</span><span class="sxs-lookup"><span data-stu-id="760b1-177">Select the **Location** for the Event Hub.</span></span>
   6. <span data-ttu-id="760b1-178">選取 [釘選到儀表板]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="760b1-178">Select **Pin to dashboard**, and then click **Create**.</span></span>

3. <span data-ttu-id="760b1-179">建立程序完成時，會顯示您命名空間的事件中樞資訊。</span><span class="sxs-lookup"><span data-stu-id="760b1-179">When the creation process completes, the Event Hubs information for your namespace is displayed.</span></span> <span data-ttu-id="760b1-180">從這裡選取 [+ 新增事件中樞] 。</span><span class="sxs-lookup"><span data-stu-id="760b1-180">From here, select **+ Add Event Hub**.</span></span> <span data-ttu-id="760b1-181">在 [建立事件中樞] 區段輸入 **sensordata** 的名稱，然後選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="760b1-181">In the **Create Event Hub** section, enter a name of **sensordata**, and then select **Create**.</span></span> <span data-ttu-id="760b1-182">讓其他欄位保持使用預設值。</span><span class="sxs-lookup"><span data-stu-id="760b1-182">Leave the other fields at the default values.</span></span>
4. <span data-ttu-id="760b1-183">在您命名空間的事件中樞檢視畫面上，選取 [事件中樞]。</span><span class="sxs-lookup"><span data-stu-id="760b1-183">From the Event Hubs view for your namespace, select **Event Hubs**.</span></span> <span data-ttu-id="760b1-184">選取 [sensordata]  項目。</span><span class="sxs-lookup"><span data-stu-id="760b1-184">Select the **sensordata** entry.</span></span>
5. <span data-ttu-id="760b1-185">在 sensordata 事件中樞選取 [共用存取原則]。</span><span class="sxs-lookup"><span data-stu-id="760b1-185">From the sensordata Event Hub, select **Shared access policies**.</span></span> <span data-ttu-id="760b1-186">使用 [+ 新增]  連結新增下列原則︰</span><span class="sxs-lookup"><span data-stu-id="760b1-186">Use the **+ Add** link to add the following policies:</span></span>

    | <span data-ttu-id="760b1-187">原則名稱</span><span class="sxs-lookup"><span data-stu-id="760b1-187">Policy name</span></span> | <span data-ttu-id="760b1-188">Claims</span><span class="sxs-lookup"><span data-stu-id="760b1-188">Claims</span></span> |
    | ----- | ----- |
    | <span data-ttu-id="760b1-189">devices</span><span class="sxs-lookup"><span data-stu-id="760b1-189">devices</span></span> | <span data-ttu-id="760b1-190">傳送</span><span class="sxs-lookup"><span data-stu-id="760b1-190">Send</span></span> |
    | <span data-ttu-id="760b1-191">storm</span><span class="sxs-lookup"><span data-stu-id="760b1-191">storm</span></span> | <span data-ttu-id="760b1-192">接聽</span><span class="sxs-lookup"><span data-stu-id="760b1-192">Listen</span></span> |

1. <span data-ttu-id="760b1-193">選取這兩個原則，並記下 [主索引鍵]  值。</span><span class="sxs-lookup"><span data-stu-id="760b1-193">Select both policies and make a note of the **PRIMARY KEY** value.</span></span> <span data-ttu-id="760b1-194">在後續步驟中，您會需要這兩個原則的值。</span><span class="sxs-lookup"><span data-stu-id="760b1-194">You need the value for both policies in future steps.</span></span>

## <a name="download-and-configure-the-project"></a><span data-ttu-id="760b1-195">下載並設定專案。</span><span class="sxs-lookup"><span data-stu-id="760b1-195">Download and configure the project</span></span>

<span data-ttu-id="760b1-196">使用下列項目從 GitHub 下載專案。</span><span class="sxs-lookup"><span data-stu-id="760b1-196">Use the following to download the project from GitHub.</span></span>

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

<span data-ttu-id="760b1-197">命令執行完畢後，您會擁有以下目錄架構：</span><span class="sxs-lookup"><span data-stu-id="760b1-197">After the command completes, you have the following directory structure:</span></span>

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains the topology
            resources/
                log4j2.xml - set logging to minimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO to the web dashboard.
        dashboard/nodejs/ - this is the node.js web dashboard.
        SendEvents/ - utilities to send fake sensor data.

> [!NOTE]
> <span data-ttu-id="760b1-198">本文件不會深入探究此範例所包含的程式碼。</span><span class="sxs-lookup"><span data-stu-id="760b1-198">This document does not go in to full details of the code included in this example.</span></span> <span data-ttu-id="760b1-199">不過，會附上程式碼的完整註解。</span><span class="sxs-lookup"><span data-stu-id="760b1-199">However, the code is fully commented.</span></span>

<span data-ttu-id="760b1-200">若要將專案設定為讀取事件中心，請開啟 `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` 檔案並在下列幾行加入您的事件中樞的資訊：</span><span class="sxs-lookup"><span data-stu-id="760b1-200">To configure the project to read from Event Hub, open the `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` file and add your Event Hub information to the following lines:</span></span>

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a><span data-ttu-id="760b1-201">編譯並在本機測試</span><span class="sxs-lookup"><span data-stu-id="760b1-201">Compile and test locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="760b1-202">若要在本機使用拓撲，需要可運作的 Storm 開發環境。</span><span class="sxs-lookup"><span data-stu-id="760b1-202">Using the topology locally requires a working Storm development environment.</span></span> <span data-ttu-id="760b1-203">如需詳細資訊，請至 Apache.org 參閱[設定 Storm 開發環境](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html)。</span><span class="sxs-lookup"><span data-stu-id="760b1-203">For more information, see [Setting up a Storm development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) at Apache.org.</span></span>

> [!WARNING]
> <span data-ttu-id="760b1-204">如果您使用的是 Windows 開發環境，本機執行拓撲時可能會收到 `java.io.IOException`。</span><span class="sxs-lookup"><span data-stu-id="760b1-204">If you are using a Windows development environment, you may receive a `java.io.IOException` when running the topology locally.</span></span> <span data-ttu-id="760b1-205">若有收到，請直接在 HDInsight 執行該拓撲。</span><span class="sxs-lookup"><span data-stu-id="760b1-205">If so, move on to running the topology on HDInsight.</span></span>

<span data-ttu-id="760b1-206">測試前，您必須先開啟儀表板，檢視拓撲輸出的資料並產生要存放在事件中樞的資料。</span><span class="sxs-lookup"><span data-stu-id="760b1-206">Before testing, you must start the dashboard to view the output of the topology and generate data to store in Event Hub.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="760b1-207">進行本機測試時，無法使用此拓撲中的 HBase 元件。</span><span class="sxs-lookup"><span data-stu-id="760b1-207">The HBase component of this topology is not active when testing locally.</span></span> <span data-ttu-id="760b1-208">無法從包含叢集的 Azure 虛擬網路外部存取 HBase 叢集的 Java API。</span><span class="sxs-lookup"><span data-stu-id="760b1-208">The Java API for the HBase cluster cannot be accessed from outside the Azure Virtual Network that contains the clusters.</span></span>

### <a name="start-the-web-application"></a><span data-ttu-id="760b1-209">啟動 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="760b1-209">Start the web application</span></span>

1. <span data-ttu-id="760b1-210">開啟命令提示字元，將目錄切換至 `hdinsight-eventhub-example/dashboard`。</span><span class="sxs-lookup"><span data-stu-id="760b1-210">Open a command prompt and change directories to `hdinsight-eventhub-example/dashboard`.</span></span> <span data-ttu-id="760b1-211">使用下列命令來安裝 Web 應用程式所需的相依性：</span><span class="sxs-lookup"><span data-stu-id="760b1-211">Use the following command to install the dependencies needed by the web application:</span></span>
   
    ```bash
    npm install
    ```

2. <span data-ttu-id="760b1-212">使用下列命令啟動 Web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="760b1-212">Use the following command to start the web application:</span></span>
   
    ```bash
    node server.js
    ```
   
    <span data-ttu-id="760b1-213">您會看見類似以下文字的訊息：</span><span class="sxs-lookup"><span data-stu-id="760b1-213">You see a message similar to the following text:</span></span>
   
        Server listening at port 3000

3. <span data-ttu-id="760b1-214">開啟網路瀏覽器，在網址列輸入 `http://localhost:3000/`。</span><span class="sxs-lookup"><span data-stu-id="760b1-214">Open a web browser and enter `http://localhost:3000/` as the address.</span></span> <span data-ttu-id="760b1-215">將會顯示與下圖類似的頁面：</span><span class="sxs-lookup"><span data-stu-id="760b1-215">A page similar to the following image is displayed:</span></span>
   
    ![Web 儀表板](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    <span data-ttu-id="760b1-217">不要關閉命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="760b1-217">Leave this command prompt open.</span></span> <span data-ttu-id="760b1-218">測試完成後，使用 Ctrl-C 鍵中斷 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="760b1-218">After testing, use Ctrl-C to stop the web server.</span></span>

### <a name="generate-data"></a><span data-ttu-id="760b1-219">產生資料</span><span class="sxs-lookup"><span data-stu-id="760b1-219">Generate data</span></span>

> [!NOTE]
> <span data-ttu-id="760b1-220">本節中的步驟採用 Node.js，因此可使用於任何平台上。</span><span class="sxs-lookup"><span data-stu-id="760b1-220">The steps in this section use Node.js so that they can be used on any platform.</span></span> <span data-ttu-id="760b1-221">如需其他語言的範例，請查看 `SendEvents` 目錄。</span><span class="sxs-lookup"><span data-stu-id="760b1-221">For other language examples, see the `SendEvents` directory.</span></span>

1. <span data-ttu-id="760b1-222">開啟新的提示字元、殼層或終端機，然後將目錄切換至 `hdinsight-eventhub-example/SendEvents/nodejs`。</span><span class="sxs-lookup"><span data-stu-id="760b1-222">Open a new prompt, shell, or terminal, and change directories to `hdinsight-eventhub-example/SendEvents/nodejs`.</span></span> <span data-ttu-id="760b1-223">若要安裝 Web 應用程式所需的相依性，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="760b1-223">To install the dependencies needed by the application, use the following command:</span></span>

    ```bash
    npm install
    ```

2. <span data-ttu-id="760b1-224">以文字編輯器開啟 `app.js` 檔案，並新增您稍早取得的事件中樞資訊：</span><span class="sxs-lookup"><span data-stu-id="760b1-224">Open the `app.js` file in a text editor and add the Event Hub information you obtained earlier:</span></span>
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="760b1-225">此範例預設您使用 `sensordata` 為事件中樞的名稱。</span><span class="sxs-lookup"><span data-stu-id="760b1-225">This example assumes that you have used `sensordata` as the name of your Event Hub.</span></span> <span data-ttu-id="760b1-226">且使用 `devices` 作為含有 `Send` 宣告之原則的名稱。</span><span class="sxs-lookup"><span data-stu-id="760b1-226">And that `devices` as the name of the policy that has a `Send` claim.</span></span>

3. <span data-ttu-id="760b1-227">使用以下命令在事件中樞插入新項目：</span><span class="sxs-lookup"><span data-stu-id="760b1-227">Use the following command to insert new entries in Event Hub:</span></span>
   
    ```bash
    node app.js
    ```
   
    <span data-ttu-id="760b1-228">您會看見數行輸出，其中包含傳送至事件中樞的資料：</span><span class="sxs-lookup"><span data-stu-id="760b1-228">You see several lines of output that contain the data sent to Event Hub:</span></span>
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-the-topology"></a><span data-ttu-id="760b1-229">建置並啟動拓撲</span><span class="sxs-lookup"><span data-stu-id="760b1-229">Build and start the topology</span></span>

1. <span data-ttu-id="760b1-230">開啟新的命令提示字元，並將目錄切換至 `hdinsight-eventhub-example/TemperatureMonitor`。</span><span class="sxs-lookup"><span data-stu-id="760b1-230">Open a new command prompt and change directories to `hdinsight-eventhub-example/TemperatureMonitor`.</span></span> <span data-ttu-id="760b1-231">若要建置和封裝拓撲，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="760b1-231">To build and package the topology, use the following command:</span></span> 

    ```bash
    mvn clean package
    ```

2. <span data-ttu-id="760b1-232">若要以本機模式啟動拓撲，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="760b1-232">To start the topology in local mode, use the following command:</span></span>

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * <span data-ttu-id="760b1-233">`--local` 會在本機啟動拓撲。</span><span class="sxs-lookup"><span data-stu-id="760b1-233">`--local` starts the topology in local mode.</span></span>
    * <span data-ttu-id="760b1-234">`--filter` 會使用 `dev.properties` 檔案來填入拓撲定義中的參數。</span><span class="sxs-lookup"><span data-stu-id="760b1-234">`--filter` uses the `dev.properties` file to populate parameters in the topology definition.</span></span>
    * <span data-ttu-id="760b1-235">`resources/no-hbase.yaml` 會使用 `no-hbase.yaml` 拓撲定義。</span><span class="sxs-lookup"><span data-stu-id="760b1-235">`resources/no-hbase.yaml` uses the `no-hbase.yaml` topology definition.</span></span>
 
   <span data-ttu-id="760b1-236">啟動之後，拓撲會從事件中樞讀取項目，並將它們傳送到在本機電腦上執行的儀表板。</span><span class="sxs-lookup"><span data-stu-id="760b1-236">Once started, the topology reads entries from Event Hub, and sends them to the dashboard running on your local machine.</span></span> <span data-ttu-id="760b1-237">您應該會看見 Web 儀表板中出現數個線條，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="760b1-237">You should see lines appear in the web dashboard, similar to the following image:</span></span>
   
    ![儀表板與資料](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. <span data-ttu-id="760b1-239">儀表板執行時，請使用前幾個步驟的 `node app.js` 命令，將新的資料傳送至事件中樞。</span><span class="sxs-lookup"><span data-stu-id="760b1-239">While the dashboard is running, use the `node app.js` command from the previous steps to send new data to Event Hubs.</span></span> <span data-ttu-id="760b1-240">由於溫度值是隨機產生，因此圖形必須更新才能顯示大量溫度變更。</span><span class="sxs-lookup"><span data-stu-id="760b1-240">Because the temperature values are randomly generated, the graph should update to show large changes in temperature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="760b1-241">在使用 `node app.js` 命令時，您必須位於 **hdinsight-eventhub-example/SendEvents/Nodejs** 目錄。</span><span class="sxs-lookup"><span data-stu-id="760b1-241">You must be in the **hdinsight-eventhub-example/SendEvents/Nodejs** directory when using the `node app.js` command.</span></span>

3. <span data-ttu-id="760b1-242">確認儀表板更新之後，請使用 Ctrl+C 鍵來停止拓撲。</span><span class="sxs-lookup"><span data-stu-id="760b1-242">After verifying that the dashboard updates, stop the topology using Ctrl+C.</span></span> <span data-ttu-id="760b1-243">您也可以使用 Ctrl-C 鍵停止本機 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="760b1-243">You can use Ctrl+C to stop the local web server also.</span></span>

## <a name="create-a-storm-and-hbase-cluster"></a><span data-ttu-id="760b1-244">建立 Storm 和 HBase 叢集</span><span class="sxs-lookup"><span data-stu-id="760b1-244">Create a Storm and HBase cluster</span></span>

<span data-ttu-id="760b1-245">本節中的步驟會使用 [Azure Resource Manager 範本](../azure-resource-manager/resource-group-template-deploy.md)，在虛擬網路上建立 Azure 虛擬網路以及 Storm 和 HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="760b1-245">The steps in this section use an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) to create an Azure Virtual Network and a Storm and HBase cluster on the virtual network.</span></span> <span data-ttu-id="760b1-246">這些範本也會建立 Azure Web 應用程式並在其中部署一份儀表板。</span><span class="sxs-lookup"><span data-stu-id="760b1-246">The template also creates an Azure Web App and deploys a copy of the dashboard into it.</span></span>

> [!NOTE]
> <span data-ttu-id="760b1-247">使用虛擬網路，在 Storm 叢集上執行的拓撲便可以使用 HBase Java API 直接與 HBase 叢集通訊。</span><span class="sxs-lookup"><span data-stu-id="760b1-247">A virtual network is used so that the topology running on the Storm cluster can directly communicate with the HBase cluster using the HBase Java API.</span></span>

<span data-ttu-id="760b1-248">本文件中使用的 Resource Manager 範本位於公用 Blob 容器中，**https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**。</span><span class="sxs-lookup"><span data-stu-id="760b1-248">The Resource Manager template used in this document is located in a public blob container at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span></span>

1. <span data-ttu-id="760b1-249">按一下以下按鈕，在 Azure 入口網站中登入 Azure 並開啟 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="760b1-249">Click the following button to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="760b1-250">在 [自訂部署] 區段輸入以下值：</span><span class="sxs-lookup"><span data-stu-id="760b1-250">From the **Custom deployment** section, enter the following values:</span></span>
   
    ![HDInsight 參數](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * <span data-ttu-id="760b1-252">**基底叢集名稱**︰此值會做為 Storm 和 HBase 叢集的基底名稱。</span><span class="sxs-lookup"><span data-stu-id="760b1-252">**Base Cluster Name**: This value is used as the base name for the Storm and HBase clusters.</span></span> <span data-ttu-id="760b1-253">例如，輸入 **abc** 會建立名為 **storm-abc** 的 Storm 叢集以及名為 **hbase-abc** 的 HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="760b1-253">For example, entering **abc** creates a Storm cluster named **storm-abc** and an HBase cluster named **hbase-abc**.</span></span>
   * <span data-ttu-id="760b1-254">**叢集登入使用者名稱**：Storm 和 HBase 叢集的系統管理員使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="760b1-254">**Cluster Login User Name**: The admin user name for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="760b1-255">**叢集登入密碼**：Storm 和 HBase 叢集的系統管理員使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="760b1-255">**Cluster Login Password**: The admin user password for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="760b1-256">**SSH 使用者名稱**︰要針對 Storm 和 HBase 叢集建立的 SSH 使用者。</span><span class="sxs-lookup"><span data-stu-id="760b1-256">**SSH User Name**: The SSH user to create for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="760b1-257">**SSH 密碼**：Storm 和 HBase 叢集的 SSH 使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="760b1-257">**SSH Password**: The password for the SSH user for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="760b1-258">**位置**︰叢集建立所在的區域。</span><span class="sxs-lookup"><span data-stu-id="760b1-258">**Location**: The region that the clusters are created in.</span></span>
     
     <span data-ttu-id="760b1-259">按一下 [確定]  儲存參數。</span><span class="sxs-lookup"><span data-stu-id="760b1-259">Click **OK** to save the parameters.</span></span>

3. <span data-ttu-id="760b1-260">使用 [基本] 區段建立資源群組，或選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="760b1-260">Use the **Basics** section to create a resource group or select an existing one.</span></span>
4. <span data-ttu-id="760b1-261">在 [資源群組位置] 下拉式功能表中，選取與您在 [設定] 區段中針對 [位置] 參數所選取的相同位置。</span><span class="sxs-lookup"><span data-stu-id="760b1-261">In the **Resource group location** dropdown menu, select the same location as you selected for the **Location** parameter in the **Settings** section.</span></span>
5. <span data-ttu-id="760b1-262">讀取條款及條件，然後選取 [我同意上方所述的條款及條件]。</span><span class="sxs-lookup"><span data-stu-id="760b1-262">Read the terms and conditions, and then select **I agree to the terms and conditions stated above**.</span></span>
6. <span data-ttu-id="760b1-263">最後，核取 [釘選到儀表板]，然後選取 [購買]。</span><span class="sxs-lookup"><span data-stu-id="760b1-263">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="760b1-264">大約需要 20 分鐘的時間來建立叢集。</span><span class="sxs-lookup"><span data-stu-id="760b1-264">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="760b1-265">在資源建立後，會顯示資源群組的資訊。</span><span class="sxs-lookup"><span data-stu-id="760b1-265">Once the resources have been created, information about the resource group is displayed.</span></span>

![Vnet 及叢集的資源群組](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="760b1-267">請注意，HDInsight 叢集的名稱是 **storm-BASENAME** 和 **hbase-BASENAME**，其中 BASENAME 是您提供給範本的名稱。</span><span class="sxs-lookup"><span data-stu-id="760b1-267">Notice that the names of the HDInsight clusters are **storm-BASENAME** and **hbase-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="760b1-268">連接到叢集時，您會在稍後步驟中使用這些名稱。</span><span class="sxs-lookup"><span data-stu-id="760b1-268">You use these names in a later step when connecting to the clusters.</span></span> <span data-ttu-id="760b1-269">另請注意，儀表板網站的名稱是 **basename-dashboard**。</span><span class="sxs-lookup"><span data-stu-id="760b1-269">Also note that the name of the dashboard site is **basename-dashboard**.</span></span> <span data-ttu-id="760b1-270">本文件稍後將使用此值。</span><span class="sxs-lookup"><span data-stu-id="760b1-270">This value is used later in this document.</span></span>

## <a name="configure-the-dashboard-bolt"></a><span data-ttu-id="760b1-271">設定儀表板 Bolt</span><span class="sxs-lookup"><span data-stu-id="760b1-271">Configure the Dashboard bolt</span></span>

<span data-ttu-id="760b1-272">若要將資料傳送至部署為 Web 應用程式的儀表板，您必須在 `dev.properties` 檔案中修改下面這行：</span><span class="sxs-lookup"><span data-stu-id="760b1-272">To send data to the dashboard deployed as a web app, you must modify the following line in the `dev.properties`file:</span></span>

```yaml
dashboard.uri: http://localhost:3000
```

<span data-ttu-id="760b1-273">將 `http://localhost:3000` 變更為 `http://BASENAME-dashboard.azurewebsites.net` 並儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="760b1-273">Change `http://localhost:3000` to `http://BASENAME-dashboard.azurewebsites.net` and save the file.</span></span> <span data-ttu-id="760b1-274">以您在先前步驟中提供的基底名稱取代 **BASENAME** 。</span><span class="sxs-lookup"><span data-stu-id="760b1-274">Replace **BASENAME** with the base name you provided in the previous step.</span></span> <span data-ttu-id="760b1-275">您也可以使用先前建立的資源群組來選取儀表板和檢視 URL。</span><span class="sxs-lookup"><span data-stu-id="760b1-275">You can also use the resource group created previously to select the dashboard and view the URL.</span></span>

## <a name="create-the-hbase-table"></a><span data-ttu-id="760b1-276">建立 HBase 資料表</span><span class="sxs-lookup"><span data-stu-id="760b1-276">Create the HBase table</span></span>

<span data-ttu-id="760b1-277">若要將資料儲存在 HBase 中，我們必須先建立資料表。</span><span class="sxs-lookup"><span data-stu-id="760b1-277">To store data in HBase, we must first create a table.</span></span> <span data-ttu-id="760b1-278">請預先建立 Storm 需要寫入的資源，因為嘗試從 Storm 拓撲內部建立資源，可能會導致多個執行個體嘗試建立相同的資源。</span><span class="sxs-lookup"><span data-stu-id="760b1-278">Pre-create resources that Storm needs to write to, as trying to create resources from inside a Storm topology can result in multiple instances trying to create the same resource.</span></span> <span data-ttu-id="760b1-279">在拓撲外部建立資源，並使用 Storm 進行讀取/寫入和分析。</span><span class="sxs-lookup"><span data-stu-id="760b1-279">Create the resources outside the topology and use Storm for reading/writing and analytics.</span></span>

1. <span data-ttu-id="760b1-280">使用您在叢集建立期間提供給範本的 SSH 使用者和密碼，透過 SSH 連線到 HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="760b1-280">Use SSH to connect to the HBase cluster using the SSH user and password you supplied to the template during cluster creation.</span></span> <span data-ttu-id="760b1-281">例如，如果使用 `ssh` 命令進行連線，您應使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="760b1-281">For example, if connecting using the `ssh` command, you would use the following syntax:</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    <span data-ttu-id="760b1-282">將 `sshuser` 取代為您在建立叢集時提供的 SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="760b1-282">Replace `sshuser` with the SSH user name you provided when creating the cluster.</span></span> <span data-ttu-id="760b1-283">將 `clustername` 取代為 HBase 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="760b1-283">Replace `clustername` with the HBase cluster name.</span></span>

2. <span data-ttu-id="760b1-284">在 SSH 工作階段中，啟動 HBase Shell。</span><span class="sxs-lookup"><span data-stu-id="760b1-284">From the SSH session, start the HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="760b1-285">載入殼層後，您會看到 `hbase(main):001:0>` 提示。</span><span class="sxs-lookup"><span data-stu-id="760b1-285">Once the shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="760b1-286">在 HBase Shell 中輸入下列命令，以建立將儲存感應器資料的資料表：</span><span class="sxs-lookup"><span data-stu-id="760b1-286">From the HBase shell, enter the following command to create a table to store the sensor data:</span></span>
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. <span data-ttu-id="760b1-287">使用下列命令來確認資料表已建立：</span><span class="sxs-lookup"><span data-stu-id="760b1-287">Verify that the table has been created by using the following command:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="760b1-288">這會傳回類似下列範例的資訊，指出資料表中有 0 個資料列。</span><span class="sxs-lookup"><span data-stu-id="760b1-288">This returns information similar to the following example, indicating that there are 0 rows in the table.</span></span>
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. <span data-ttu-id="760b1-289">輸入 `exit` 以結束 HBase 殼層：</span><span class="sxs-lookup"><span data-stu-id="760b1-289">Enter `exit` to exit the HBase shell:</span></span>

## <a name="configure-the-hbase-bolt"></a><span data-ttu-id="760b1-290">設定 HBase Bolt</span><span class="sxs-lookup"><span data-stu-id="760b1-290">Configure the HBase bolt</span></span>

<span data-ttu-id="760b1-291">若要從 Storm 叢集寫入至 HBase，您必須將 HBase 叢集的組態詳細資料提供給 HBase bolt。</span><span class="sxs-lookup"><span data-stu-id="760b1-291">To write to HBase from the Storm cluster, you must provide the HBase bolt with the configuration details of your HBase cluster.</span></span>

1. <span data-ttu-id="760b1-292">選擇下列範例之一，為您的 HBase 叢集取出 Zookeeper 仲裁：</span><span class="sxs-lookup"><span data-stu-id="760b1-292">Use one of the following examples to retrieve the Zookeeper quorum for your HBase cluster:</span></span>

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > <span data-ttu-id="760b1-293">將 `your_HDInsight_cluster_name` 替換為 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="760b1-293">Replace `your_HDInsight_cluster_name` with the name of your HDInsight cluster.</span></span> <span data-ttu-id="760b1-294">如需進一步了解 `jq` 的安裝，請參閱 [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/)。</span><span class="sxs-lookup"><span data-stu-id="760b1-294">For more information on installing the `jq` utility, see [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span></span>
    >
    > <span data-ttu-id="760b1-295">出現提示時，請輸入 HDInsight 管理員的登入密碼。</span><span class="sxs-lookup"><span data-stu-id="760b1-295">When prompted, enter the password for the HDInsight admin login.</span></span>

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > <span data-ttu-id="760b1-296">將 your_HDInsight_cluster_name 取代為您的 HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="760b1-296">Replace \`your_HDInsight_cluster_name with the name of your HDInsight cluster.</span></span> <span data-ttu-id="760b1-297">出現提示時，請輸入 HDInsight 管理員的登入密碼。</span><span class="sxs-lookup"><span data-stu-id="760b1-297">When prompted, enter the password for the HDInsight admin login.</span></span>
    >
    > <span data-ttu-id="760b1-298">此範例需要 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="760b1-298">This example requires Azure PowerShell.</span></span> <span data-ttu-id="760b1-299">如需進一步了解 Azure PowerShell 之使用，請參閱 [Azure PowerShell 使用者入門](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span><span class="sxs-lookup"><span data-stu-id="760b1-299">For more information on using Azure PowerShell, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span></span>

    <span data-ttu-id="760b1-300">這些範例傳回的資訊類似於下列文字：</span><span class="sxs-lookup"><span data-stu-id="760b1-300">The information returned by these examples is similar to the following text:</span></span>

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    <span data-ttu-id="760b1-301">Storm 會使用此資訊來與 HBase 叢集溝通。</span><span class="sxs-lookup"><span data-stu-id="760b1-301">This information is used by Storm to communicate with the HBase cluster.</span></span>

2. <span data-ttu-id="760b1-302">修改 `dev.properties` 檔案，並將 Zookeeper 仲裁資訊新增至下行：</span><span class="sxs-lookup"><span data-stu-id="760b1-302">Modify the `dev.properties` file and add the Zookeeper quorum information to the following line:</span></span>

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-the-solution-to-hdinsight"></a><span data-ttu-id="760b1-303">建置、封裝及部署解決方案到 HDInsight</span><span class="sxs-lookup"><span data-stu-id="760b1-303">Build, package, and deploy the solution to HDInsight</span></span>

<span data-ttu-id="760b1-304">在開發環境中，使用下列步驟將 Storm 拓撲部署至 Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="760b1-304">In your development environment, use the following steps to deploy the Storm topology to the storm cluster.</span></span>

1. <span data-ttu-id="760b1-305">從 `TemperatureMonitor` 目錄使用下列命令來執行新的組建，並從專案建立 JAR 封裝：</span><span class="sxs-lookup"><span data-stu-id="760b1-305">From the `TemperatureMonitor` directory, use the following command to perform a new build and create a JAR package from your project:</span></span>
   
        mvn clean package
   
    <span data-ttu-id="760b1-306">此命令會在專案的目標目錄中建立名為 `TemperatureMonitor-1.0-SNAPSHOT.jar in the ` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="760b1-306">This command creates a file named `TemperatureMonitor-1.0-SNAPSHOT.jar in the `target\` directory of your project.</span></span>

2. <span data-ttu-id="760b1-307">使用 scp 將 `TemperatureMonitor-1.0-SNAPSHOT.jar` 及 `dev.properties` 上傳至您的 Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="760b1-307">Use scp to upload the `TemperatureMonitor-1.0-SNAPSHOT.jar` and `dev.properties` files to your Storm cluster.</span></span> <span data-ttu-id="760b1-308">在下列範例中，將 `sshuser` 取代為您創造叢集時提供的 SSH 使用者，並將 `clustername` 取代為您 Storm 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="760b1-308">In the following example, replace `sshuser` with the SSH user you provided when creating the cluster, and `clustername` with the name of your Storm cluster.</span></span> <span data-ttu-id="760b1-309">出現提示時，請輸入 SSH 使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="760b1-309">When prompted, enter the password for the SSH user.</span></span>
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > <span data-ttu-id="760b1-310">檔案可能需要幾分鐘的時間才能上傳完畢。</span><span class="sxs-lookup"><span data-stu-id="760b1-310">It may take several minutes to upload the files.</span></span>

    <span data-ttu-id="760b1-311">如需搭配 HDInsight 使用 `scp` 及 `ssh` 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](./hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="760b1-311">For more information on using the `scp` and `ssh` commands with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

3. <span data-ttu-id="760b1-312">檔案上傳後，使用 SSH 連線至 Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="760b1-312">Once the file has been uploaded, connect to the Storm cluster using SSH.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="760b1-313">將 `sshuser` 取代為 SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="760b1-313">Replace `sshuser` with the SSH user name.</span></span> <span data-ttu-id="760b1-314">將 `clustername` 取代為 Storm 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="760b1-314">Replace `clustername` with the Storm cluster name.</span></span>

4. <span data-ttu-id="760b1-315">若要啟動拓撲，請從 SSH 工作階段中使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="760b1-315">To start the topology, use the following command from the SSH session:</span></span>
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * <span data-ttu-id="760b1-316">`--remote` 會提交拓撲至 Nimbus 服務，該服務會將拓撲散佈至叢集中的監督節點。</span><span class="sxs-lookup"><span data-stu-id="760b1-316">`--remote` submits the topology to the Nimbus service, which distributes it to the supervisor nodes in the cluster.</span></span>
    * <span data-ttu-id="760b1-317">`--filter` 會使用 `dev.properties` 檔案來填入拓撲定義中的參數。</span><span class="sxs-lookup"><span data-stu-id="760b1-317">`--filter` uses the `dev.properties` file to populate parameters in the topology definition.</span></span>
    * <span data-ttu-id="760b1-318">`-R /with-hbase.yaml` 會使用封裝中包含的 `with-hbase.yaml` 拓撲。</span><span class="sxs-lookup"><span data-stu-id="760b1-318">`-R /with-hbase.yaml` uses the `with-hbase.yaml` topology included in the package.</span></span>

5. <span data-ttu-id="760b1-319">拓撲啟動後，以瀏覽器開啟您發佈至 Azure 的網站，然後使用 `node app.js` 命令將資料傳送至事件中樞。</span><span class="sxs-lookup"><span data-stu-id="760b1-319">After the topology has started, open a browser to the website you published on Azure, then use the `node app.js` command to send data to Event Hub.</span></span> <span data-ttu-id="760b1-320">您應該會看見顯示資訊的 Web 儀表板更新。</span><span class="sxs-lookup"><span data-stu-id="760b1-320">You should see the web dashboard update to display the information.</span></span>
   
    ![儀表板](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a><span data-ttu-id="760b1-322">檢視 HBase 資料</span><span class="sxs-lookup"><span data-stu-id="760b1-322">View HBase data</span></span>

<span data-ttu-id="760b1-323">使用下列步驟連接到 HBase，並確認已將資料寫入資料表：</span><span class="sxs-lookup"><span data-stu-id="760b1-323">Use the following steps to connect to HBase and verify that the data has been written to the table:</span></span>

1. <span data-ttu-id="760b1-324">使用 SSH 連接到 HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="760b1-324">Use SSH to connect to the HBase cluster.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="760b1-325">將 `sshuser` 取代為 SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="760b1-325">Replace `sshuser` with the SSH user name.</span></span> <span data-ttu-id="760b1-326">將 `clustername` 取代為 HBase 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="760b1-326">Replace `clustername` with the HBase cluster name.</span></span>

2. <span data-ttu-id="760b1-327">在 SSH 工作階段中，啟動 HBase Shell。</span><span class="sxs-lookup"><span data-stu-id="760b1-327">From the SSH session, start the HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="760b1-328">載入殼層後，您會看到 `hbase(main):001:0>` 提示。</span><span class="sxs-lookup"><span data-stu-id="760b1-328">Once the shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="760b1-329">檢視資料表中的資料列︰</span><span class="sxs-lookup"><span data-stu-id="760b1-329">View rows from the table:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="760b1-330">此命令會傳回類似下列文字的資訊，指出資料表中含有資料。</span><span class="sxs-lookup"><span data-stu-id="760b1-330">This command returns information similar to the following text, indicating that there is data in the table.</span></span>
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > <span data-ttu-id="760b1-331">此掃描作業最多會從資料表傳回 10 個資料列。</span><span class="sxs-lookup"><span data-stu-id="760b1-331">This scan operation returns a maximum of 10 rows from the table.</span></span>

## <a name="delete-your-clusters"></a><span data-ttu-id="760b1-332">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="760b1-332">Delete your clusters</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="760b1-333">若要一次刪除叢集、儲存體和 Web 應用程式，請刪除包含它們的資源群組。</span><span class="sxs-lookup"><span data-stu-id="760b1-333">To delete the clusters, storage, and web app at one time, delete the resource group that contains them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="760b1-334">後續步驟</span><span class="sxs-lookup"><span data-stu-id="760b1-334">Next steps</span></span>

<span data-ttu-id="760b1-335">若需更多搭配 HDInsight 的 Storm 拓撲範例，請參閱 [Storm on HDInsight 的範例拓撲](hdinsight-storm-example-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="760b1-335">For more examples of Storm topologies with HDInsight, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md)</span></span>

<span data-ttu-id="760b1-336">如需關於 Apache Storm 的詳細資訊，請參閱 [Apache Storm](https://storm.incubator.apache.org/) 網站 (英文)。</span><span class="sxs-lookup"><span data-stu-id="760b1-336">For more information about Apache Storm, see the [Apache Storm](https://storm.incubator.apache.org/) site.</span></span>

<span data-ttu-id="760b1-337">如需關於 HBase on HDInsight 的詳細資訊，請參閱 [HBase 與 HDInsight 概觀](hdinsight-hbase-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="760b1-337">For more information about HBase on HDInsight, see the [HBase with HDInsight Overview](hdinsight-hbase-overview.md).</span></span>

<span data-ttu-id="760b1-338">如需關於 Socket.io 的詳細資訊，請參閱 [socket.io](http://socket.io/) 網站 (英文)。</span><span class="sxs-lookup"><span data-stu-id="760b1-338">For more information about Socket.io, see the [socket.io](http://socket.io/) site.</span></span>

<span data-ttu-id="760b1-339">如需關於 D3.js 的詳細資訊，請參閱 [D3.js：資料驅動型文件](http://d3js.org/)(英文)。</span><span class="sxs-lookup"><span data-stu-id="760b1-339">For more information about D3.js, see [D3.js - Data Driven Documents](http://d3js.org/).</span></span>

<span data-ttu-id="760b1-340">如需關於以 Java 建立拓撲的詳細資訊，請參閱 [為 Apache Storm on HDInsight 開發 Java 拓撲](hdinsight-storm-develop-java-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="760b1-340">For information about creating topologies in Java, see [Develop Java topologies for Apache Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="760b1-341">如需關於以 .NET 建立拓撲的詳細資訊，請參閱 [使用 Visual Studio 為 Apache Storm on HDInsight 開發 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="760b1-341">For information about creating topologies in .NET, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

[azure-portal]: https://portal.azure.com
