---
title: "使用 Apache Storm 和 HBase aaaAnalyze 感應器資料 |Microsoft 文件"
description: "深入了解如何 tooconnect tooApache Storm 與虛擬網路。 使用 Storm HBase tooprocess 感應器資料，從事件中心並視覺化與 D3.js。"
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
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a><span data-ttu-id="4a3ea-104">在 HDInsight (Hadoop) 中使用 Apache Storm、事件中樞和 HBase 分析感應器資料</span><span class="sxs-lookup"><span data-stu-id="4a3ea-104">Analyze sensor data with Apache Storm, Event Hub, and HBase in HDInsight (Hadoop)</span></span>

<span data-ttu-id="4a3ea-105">深入了解如何 toouse Apache Storm 的 HDInsight tooprocess 感應器資料是來自 Azure 事件中心。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-105">Learn how toouse Apache Storm on HDInsight tooprocess sensor data from Azure Event Hub.</span></span> <span data-ttu-id="4a3ea-106">hello 資料會儲存到在 HDInsight 上的 Apache HBase，並使用 D3.js 以視覺化方式檢視。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-106">hello data is then stored into Apache HBase on HDInsight, and visualized using D3.js.</span></span>

<span data-ttu-id="4a3ea-107">本文件中使用的 hello Azure Resource Manager 範本會示範如何 toocreate 資源群組中的多個 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-107">hello Azure Resource Manager template used in this document demonstrates how toocreate multiple Azure resources in a resource group.</span></span> <span data-ttu-id="4a3ea-108">hello 範本會建立 Azure 虛擬網路、 兩個的 HDInsight 叢集 （Storm 和 HBase） 和 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-108">hello template creates an Azure Virtual Network, two HDInsight clusters (Storm and HBase) and an Azure Web App.</span></span> <span data-ttu-id="4a3ea-109">即時 web 儀表板的 node.js 實作是自動部署的 toohello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-109">A node.js implementation of a real-time web dashboard is automatically deployed toohello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="4a3ea-110">此文件和範例，在這份文件中的 hello 資訊需要 HDInsight 3.6 版。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-110">hello information in this document and example in this document require HDInsight version 3.6.</span></span>
>
> <span data-ttu-id="4a3ea-111">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4a3ea-112">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a3ea-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="4a3ea-113">Prerequisites</span></span>

* <span data-ttu-id="4a3ea-114">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-114">An Azure subscription.</span></span>
* <span data-ttu-id="4a3ea-115">[Node.js](http://nodejs.org/)： 使用的 toopreview hello web 儀表板在您的開發環境的本機上。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-115">[Node.js](http://nodejs.org/): Used toopreview hello web dashboard locally on your development environment.</span></span>
* <span data-ttu-id="4a3ea-116">[Java 和 hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html)： 使用 toodevelop hello Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-116">[Java and hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): Used toodevelop hello Storm topology.</span></span>
* <span data-ttu-id="4a3ea-117">[Maven](http://maven.apache.org/what-is-maven.html)： 使用的 toobuild 和編譯 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-117">[Maven](http://maven.apache.org/what-is-maven.html): Used toobuild and compile hello project.</span></span>
* <span data-ttu-id="4a3ea-118">[Git](http://git-scm.com/)： 從 GitHub 使用的 toodownload hello 專案。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-118">[Git](http://git-scm.com/): Used toodownload hello project from GitHub.</span></span>
* <span data-ttu-id="4a3ea-119">**SSH**用戶端： 使用 tooconnect toohello 以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-119">An **SSH** client: Used tooconnect toohello Linux-based HDInsight clusters.</span></span> <span data-ttu-id="4a3ea-120">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="4a3ea-121">您不需刪除現有的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-121">You do not need an existing HDInsight cluster.</span></span> <span data-ttu-id="4a3ea-122">本文件中的 hello 步驟建立 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="4a3ea-122">hello steps in this document create hello following resources:</span></span>
> 
> * <span data-ttu-id="4a3ea-123">Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="4a3ea-123">An Azure Virtual Network</span></span>
> * <span data-ttu-id="4a3ea-124">Storm on HDInsight 叢集 (以 Linux 為基礎，兩個背景工作節點)</span><span class="sxs-lookup"><span data-stu-id="4a3ea-124">A Storm on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="4a3ea-125">HBase on HDInsight 叢集 (以 Linux 為基礎，兩個背景工作節點)</span><span class="sxs-lookup"><span data-stu-id="4a3ea-125">An HBase on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="4a3ea-126">Azure Web 應用程式裝載 hello web 儀表板</span><span class="sxs-lookup"><span data-stu-id="4a3ea-126">An Azure Web App that hosts hello web dashboard</span></span>

## <a name="architecture"></a><span data-ttu-id="4a3ea-127">架構</span><span class="sxs-lookup"><span data-stu-id="4a3ea-127">Architecture</span></span>

![架構圖表](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

<span data-ttu-id="4a3ea-129">這個範例包含下列元件的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a3ea-129">This example consists of hello following components:</span></span>

* <span data-ttu-id="4a3ea-130">**Azure 事件中樞**：包含從感應器收集的資料。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-130">**Azure Event Hubs**: Contains data that is collected from sensors.</span></span>
* <span data-ttu-id="4a3ea-131">**Storm on HDInsight**：即時處理事件中樞的資料。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-131">**Storm on HDInsight**: Provides real-time processing of data from Event Hub.</span></span>
* <span data-ttu-id="4a3ea-132">**HBase on HDInsight**：針對 Storm 所處理過的資料，提供持續的 NoSQL 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-132">**HBase on HDInsight**: Provides a persistent NoSQL data store for data after it has been processed by Storm.</span></span>
* <span data-ttu-id="4a3ea-133">**Azure 虛擬網路服務**: hello HDInsight 上的 Storm 之間 HBase HDInsight 叢集上的安全通訊。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-133">**Azure Virtual Network service**: Enables secure communications between hello Storm on HDInsight and HBase on HDInsight clusters.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="4a3ea-134">使用 hello Java HBase 用戶端應用程式開發介面時，需要虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-134">A virtual network is required when using hello Java HBase client API.</span></span> <span data-ttu-id="4a3ea-135">它不會顯示 hello 公用閘道 HBase 叢集的移轉。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-135">It is not exposed over hello public gateway for HBase clusters.</span></span> <span data-ttu-id="4a3ea-136">安裝 HBase 和 Storm 叢集至相同虛擬網路可讓的 hello hello Storm 叢集 （或任何其他 hello 虛擬網路上的系統） toodirectly 存取 HBase 使用用戶端應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-136">Installing HBase and Storm clusters into hello same virtual network allows hello Storm cluster (or any other system on hello virtual network) toodirectly access HBase using client API.</span></span>

* <span data-ttu-id="4a3ea-137">**儀表板網站**：即時建立資料圖表的範例儀表板。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-137">**Dashboard website**: An example dashboard that charts data in real time.</span></span>
  
  * <span data-ttu-id="4a3ea-138">Node.js 被實作 hello 網站。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-138">hello website is implemented in Node.js.</span></span>
  * <span data-ttu-id="4a3ea-139">[Socket.io](http://socket.io/)用於 hello Storm 拓撲與 hello 網站之間的即時通訊。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-139">[Socket.io](http://socket.io/) is used for real-time communication between hello Storm topology and hello website.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="4a3ea-140">使用 Socket.io 進行通訊是實作細節。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-140">Using Socket.io for communication is an implementation detail.</span></span> <span data-ttu-id="4a3ea-141">您可以使用任何通訊架構，例如原始 WebSockets 或 SignalR。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-141">You can use any communications framework, such as raw WebSockets or SignalR.</span></span>

  * <span data-ttu-id="4a3ea-142">[D3.js](http://d3js.org/)傳送 toohello 網站使用的 toograph hello 資料。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-142">[D3.js](http://d3js.org/) is used toograph hello data that is sent toohello website.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4a3ea-143">因為沒有任何支援的方法 toocreate 一個 HDInsight 叢集的 Storm 和 HBase 需要，這兩個叢集。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-143">Two clusters are required, as there is no supported method toocreate one HDInsight cluster for both Storm and HBase.</span></span>

<span data-ttu-id="4a3ea-144">hello 拓樸，讀取事件中心使用 hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html)類別，並將資料寫入至 HBase 使用 hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html)類別。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-144">hello topology reads data from Event Hub by using hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) class, and writes data into HBase using hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) class.</span></span> <span data-ttu-id="4a3ea-145">與 hello 網站的通訊透過使用[socket.io client.java](https://github.com/nkzawa/socket.io-client.java)。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-145">Communication with hello website is accomplished by using [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span></span>

<span data-ttu-id="4a3ea-146">hello 下列圖表說明拓撲 hello 的 hello 版面配置：</span><span class="sxs-lookup"><span data-stu-id="4a3ea-146">hello following diagram explains hello layout of hello topology:</span></span>

![拓撲圖](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> <span data-ttu-id="4a3ea-148">此圖表是 hello 拓撲的簡化的檢視。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-148">This diagram is a simplified view of hello topology.</span></span> <span data-ttu-id="4a3ea-149">系統會針對事件中樞的每個分割區，為各元件建立執行個體。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-149">An instance of each component is created for each partition in your Event Hub.</span></span> <span data-ttu-id="4a3ea-150">這些執行個體分散於 hello hello 叢集中的節點和資料之間路由它們，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4a3ea-150">These instances are distributed across hello nodes in hello cluster, and data is routed between them as follows:</span></span>
> 
> * <span data-ttu-id="4a3ea-151">負載平衡來自 hello spout toohello 剖析器的資料。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-151">Data from hello spout toohello parser is load balanced.</span></span>
> * <span data-ttu-id="4a3ea-152">Hello 剖析器 toohello 儀表板和 HBase 中資料的分組依據裝置識別碼，以便從訊息 hello 相同的裝置一律流程 toohello 同一個元件。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-152">Data from hello parser toohello Dashboard and HBase is grouped by Device ID, so that messages from hello same device always flow toohello same component.</span></span>

### <a name="topology-components"></a><span data-ttu-id="4a3ea-153">拓撲元件</span><span class="sxs-lookup"><span data-stu-id="4a3ea-153">Topology components</span></span>

* <span data-ttu-id="4a3ea-154">**事件中樞 Spout**: hello spout 是在提供的 Apache Storm 版本 0.10.0 及更高版本。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-154">**Event Hub Spout**: hello spout is provided as part of Apache Storm version 0.10.0 and higher.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="4a3ea-155">此範例中使用的 hello 事件中心 spout 需要 HDInsight 叢集版本 3.5 或 3.6 上的出現。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-155">hello Event Hub spout used in this example requires a Storm on HDInsight cluster version 3.5 or 3.6.</span></span>

* <span data-ttu-id="4a3ea-156">**ParserBolt.java**: hello spout 發出的 hello 資料未經處理的 JSON，而且有時候多個事件，就會發出一次。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-156">**ParserBolt.java**: hello data that is emitted by hello spout is raw JSON, and occasionally more than one event is emitted at a time.</span></span> <span data-ttu-id="4a3ea-157">此閃電讀取 spout hello hello 所發出的資料，並剖析 hello JSON 訊息。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-157">This bolt reads hello data emitted by hello spout and parses hello JSON message.</span></span> <span data-ttu-id="4a3ea-158">hello 閃電再發出 hello 資料當做元組，其中包含多個欄位。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-158">hello bolt then emits hello data as a tuple that contains multiple fields.</span></span>
* <span data-ttu-id="4a3ea-159">**DashboardBolt.java**： 此元件會示範如何 toouse hello Socket.io Java toosend 資料即時 toohello web 儀表板中的用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-159">**DashboardBolt.java**: This component demonstrates how toouse hello Socket.io client library for Java toosend data in real time toohello web dashboard.</span></span>
* <span data-ttu-id="4a3ea-160">**否 hbase.yaml**: hello 在本機模式中執行時所使用的拓撲定義。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-160">**no-hbase.yaml**: hello topology definition used when running in local mode.</span></span> <span data-ttu-id="4a3ea-161">這不會使用到 HBase 的元件。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-161">It does not use HBase components.</span></span>
* <span data-ttu-id="4a3ea-162">**與 hbase.yaml**: hello hello 叢集上執行 hello 拓撲時所使用的拓撲定義。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-162">**with-hbase.yaml**: hello topology definition used when running hello topology on hello cluster.</span></span> <span data-ttu-id="4a3ea-163">這會使用到 HBase 的元件。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-163">It does use HBase components.</span></span>
* <span data-ttu-id="4a3ea-164">**dev.properties**: hello hello 事件中心 spout、 HBase 閃電和儀表板元件的組態資訊。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-164">**dev.properties**: hello configuration information for hello Event Hub spout, HBase bolt, and dashboard components.</span></span>

## <a name="prepare-your-environment"></a><span data-ttu-id="4a3ea-165">準備您的環境</span><span class="sxs-lookup"><span data-stu-id="4a3ea-165">Prepare your environment</span></span>

<span data-ttu-id="4a3ea-166">使用此範例之前，您必須建立 Azure 事件中心，從讀取的 hello Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-166">Before you use this example, you must create an Azure Event Hub, which hello Storm topology reads from.</span></span>

### <a name="configure-event-hub"></a><span data-ttu-id="4a3ea-167">設定事件中樞</span><span class="sxs-lookup"><span data-stu-id="4a3ea-167">Configure Event Hub</span></span>

<span data-ttu-id="4a3ea-168">事件中心是此範例中的 hello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-168">Event Hub is hello data source for this example.</span></span> <span data-ttu-id="4a3ea-169">使用下列步驟 toocreate 事件中心的 hello。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-169">Use hello following steps toocreate an Event Hub.</span></span>

1. <span data-ttu-id="4a3ea-170">從 hello [Azure 入口網站](https://portal.azure.com)，選取**+ 新增** -> **物聯網** -> **事件中心**。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-170">From hello [Azure portal](https://portal.azure.com), select **+ New** -> **Internet of Things** -> **Event Hubs**.</span></span>
2. <span data-ttu-id="4a3ea-171">在 hello**建立命名空間**區段中，執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a3ea-171">In hello **Create Namespace** section, perform hello following tasks:</span></span>
   
   1. <span data-ttu-id="4a3ea-172">輸入**名稱**hello 命名空間。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-172">Enter a **Name** for hello namespace.</span></span>
   2. <span data-ttu-id="4a3ea-173">選取定價層。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-173">Select a pricing tier.</span></span> <span data-ttu-id="4a3ea-174"> 就已足夠。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-174">**Basic** is sufficient for this example.</span></span>
   3. <span data-ttu-id="4a3ea-175">選取 hello Azure**訂用帳戶**toouse。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-175">Select hello Azure **Subscription** toouse.</span></span>
   4. <span data-ttu-id="4a3ea-176">選取現有的資源群組，或建立一個新的群組。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-176">Either select an existing resource group or create a new one.</span></span>
   5. <span data-ttu-id="4a3ea-177">選取 hello**位置**hello 事件中心。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-177">Select hello **Location** for hello Event Hub.</span></span>
   6. <span data-ttu-id="4a3ea-178">選取**Pin toodashboard**，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-178">Select **Pin toodashboard**, and then click **Create**.</span></span>

3. <span data-ttu-id="4a3ea-179">Hello 建立程序完成時，會顯示 hello 事件中樞命名空間的資訊。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-179">When hello creation process completes, hello Event Hubs information for your namespace is displayed.</span></span> <span data-ttu-id="4a3ea-180">從這裡選取 [+ 新增事件中樞] 。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-180">From here, select **+ Add Event Hub**.</span></span> <span data-ttu-id="4a3ea-181">在 hello**建立事件中樞**區段中，輸入名稱**sensordata**，然後選取**建立**。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-181">In hello **Create Event Hub** section, enter a name of **sensordata**, and then select **Create**.</span></span> <span data-ttu-id="4a3ea-182">保留 hello hello 預設值，其他欄位。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-182">Leave hello other fields at hello default values.</span></span>
4. <span data-ttu-id="4a3ea-183">從 hello 事件中樞命名空間，選取的檢視**事件中心**。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-183">From hello Event Hubs view for your namespace, select **Event Hubs**.</span></span> <span data-ttu-id="4a3ea-184">選取 hello **sensordata**項目。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-184">Select hello **sensordata** entry.</span></span>
5. <span data-ttu-id="4a3ea-185">從 hello sensordata 事件中樞，選取**共用存取原則**。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-185">From hello sensordata Event Hub, select **Shared access policies**.</span></span> <span data-ttu-id="4a3ea-186">使用 hello **+ 加**連結 tooadd hello 下列原則：</span><span class="sxs-lookup"><span data-stu-id="4a3ea-186">Use hello **+ Add** link tooadd hello following policies:</span></span>

    | <span data-ttu-id="4a3ea-187">原則名稱</span><span class="sxs-lookup"><span data-stu-id="4a3ea-187">Policy name</span></span> | <span data-ttu-id="4a3ea-188">Claims</span><span class="sxs-lookup"><span data-stu-id="4a3ea-188">Claims</span></span> |
    | ----- | ----- |
    | <span data-ttu-id="4a3ea-189">devices</span><span class="sxs-lookup"><span data-stu-id="4a3ea-189">devices</span></span> | <span data-ttu-id="4a3ea-190">傳送</span><span class="sxs-lookup"><span data-stu-id="4a3ea-190">Send</span></span> |
    | <span data-ttu-id="4a3ea-191">storm</span><span class="sxs-lookup"><span data-stu-id="4a3ea-191">storm</span></span> | <span data-ttu-id="4a3ea-192">接聽</span><span class="sxs-lookup"><span data-stu-id="4a3ea-192">Listen</span></span> |

1. <span data-ttu-id="4a3ea-193">選取這兩個原則，並記下 hello**主索引鍵**值。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-193">Select both policies and make a note of hello **PRIMARY KEY** value.</span></span> <span data-ttu-id="4a3ea-194">您需要在未來的步驟中這兩個原則 hello 值。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-194">You need hello value for both policies in future steps.</span></span>

## <a name="download-and-configure-hello-project"></a><span data-ttu-id="4a3ea-195">下載並設定 hello 專案</span><span class="sxs-lookup"><span data-stu-id="4a3ea-195">Download and configure hello project</span></span>

<span data-ttu-id="4a3ea-196">使用 hello GitHub 中的下列 toodownload hello 專案。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-196">Use hello following toodownload hello project from GitHub.</span></span>

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

<span data-ttu-id="4a3ea-197">Hello 命令完成之後，您會有下列目錄結構的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a3ea-197">After hello command completes, you have hello following directory structure:</span></span>

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> <span data-ttu-id="4a3ea-198">這份文件不討論 toofull hello 本範例中包含的程式碼的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-198">This document does not go in toofull details of hello code included in this example.</span></span> <span data-ttu-id="4a3ea-199">不過，完整註解 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-199">However, hello code is fully commented.</span></span>

<span data-ttu-id="4a3ea-200">從事件中樞，開啟 hello tooconfigure hello 專案 tooread`hdinsight-eventhub-example/TemperatureMonitor/dev.properties`檔案，然後加入您的事件中樞資訊 toohello 下列行：</span><span class="sxs-lookup"><span data-stu-id="4a3ea-200">tooconfigure hello project tooread from Event Hub, open hello `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` file and add your Event Hub information toohello following lines:</span></span>

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a><span data-ttu-id="4a3ea-201">編譯並在本機測試</span><span class="sxs-lookup"><span data-stu-id="4a3ea-201">Compile and test locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4a3ea-202">在本機使用 hello 拓撲需要使用 Storm 開發環境。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-202">Using hello topology locally requires a working Storm development environment.</span></span> <span data-ttu-id="4a3ea-203">如需詳細資訊，請至 Apache.org 參閱[設定 Storm 開發環境](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html)。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-203">For more information, see [Setting up a Storm development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) at Apache.org.</span></span>

> [!WARNING]
> <span data-ttu-id="4a3ea-204">如果您使用的 Microsoft 開發環境，您可能會收到`java.io.IOException`時在本機執行 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-204">If you are using a Windows development environment, you may receive a `java.io.IOException` when running hello topology locally.</span></span> <span data-ttu-id="4a3ea-205">如果是這樣，移動 toorunning hello 拓樸 HDInsight 上。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-205">If so, move on toorunning hello topology on HDInsight.</span></span>

<span data-ttu-id="4a3ea-206">在測試之前，必須開始 hello hello 拓樸的儀表板 tooview hello 輸出，然後產生資料 toostore 在事件中樞。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-206">Before testing, you must start hello dashboard tooview hello output of hello topology and generate data toostore in Event Hub.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4a3ea-207">在本機測試時，這種拓撲的 hello HBase 元件未啟用。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-207">hello HBase component of this topology is not active when testing locally.</span></span> <span data-ttu-id="4a3ea-208">無法從外部 hello 包含 hello 叢集的 Azure 虛擬網路中存取 hello Java 應用程式開發介面 hello HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-208">hello Java API for hello HBase cluster cannot be accessed from outside hello Azure Virtual Network that contains hello clusters.</span></span>

### <a name="start-hello-web-application"></a><span data-ttu-id="4a3ea-209">啟動 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4a3ea-209">Start hello web application</span></span>

1. <span data-ttu-id="4a3ea-210">開啟命令提示字元，然後將目錄變更太`hdinsight-eventhub-example/dashboard`。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-210">Open a command prompt and change directories too`hdinsight-eventhub-example/dashboard`.</span></span> <span data-ttu-id="4a3ea-211">使用下列命令 tooinstall hello 相依性 hello web 應用程式所需的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a3ea-211">Use hello following command tooinstall hello dependencies needed by hello web application:</span></span>
   
    ```bash
    npm install
    ```

2. <span data-ttu-id="4a3ea-212">使用下列命令 toostart hello web 應用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a3ea-212">Use hello following command toostart hello web application:</span></span>
   
    ```bash
    node server.js
    ```
   
    <span data-ttu-id="4a3ea-213">您會看到下列文字的訊息類似的 toohello:</span><span class="sxs-lookup"><span data-stu-id="4a3ea-213">You see a message similar toohello following text:</span></span>
   
        Server listening at port 3000

3. <span data-ttu-id="4a3ea-214">開啟網頁瀏覽器並輸入`http://localhost:3000/`hello 位址。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-214">Open a web browser and enter `http://localhost:3000/` as hello address.</span></span> <span data-ttu-id="4a3ea-215">會顯示下列影像頁面類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="4a3ea-215">A page similar toohello following image is displayed:</span></span>
   
    ![Web 儀表板](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    <span data-ttu-id="4a3ea-217">不要關閉命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-217">Leave this command prompt open.</span></span> <span data-ttu-id="4a3ea-218">測試之後，使用 Ctrl + C toostop hello web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-218">After testing, use Ctrl-C toostop hello web server.</span></span>

### <a name="generate-data"></a><span data-ttu-id="4a3ea-219">產生資料</span><span class="sxs-lookup"><span data-stu-id="4a3ea-219">Generate data</span></span>

> [!NOTE]
> <span data-ttu-id="4a3ea-220">hello 本節中的步驟使用 Node.js 以便它們可以用於任何平台上。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-220">hello steps in this section use Node.js so that they can be used on any platform.</span></span> <span data-ttu-id="4a3ea-221">如需其他語言的範例，請參閱 hello`SendEvents`目錄。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-221">For other language examples, see hello `SendEvents` directory.</span></span>

1. <span data-ttu-id="4a3ea-222">開啟新的提示字元、 殼層或終端機，並將目錄變更太`hdinsight-eventhub-example/SendEvents/nodejs`。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-222">Open a new prompt, shell, or terminal, and change directories too`hdinsight-eventhub-example/SendEvents/nodejs`.</span></span> <span data-ttu-id="4a3ea-223">tooinstall hello 相依性所需的 hello 應用程式，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a3ea-223">tooinstall hello dependencies needed by hello application, use hello following command:</span></span>

    ```bash
    npm install
    ```

2. <span data-ttu-id="4a3ea-224">開啟 hello`app.js`檔案文字編輯器中，並新增您稍早取得的事件中樞資訊 hello:</span><span class="sxs-lookup"><span data-stu-id="4a3ea-224">Open hello `app.js` file in a text editor and add hello Event Hub information you obtained earlier:</span></span>
   
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
   > <span data-ttu-id="4a3ea-225">這個範例假設您已經使用`sensordata`做為事件中樞 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-225">This example assumes that you have used `sensordata` as hello name of your Event Hub.</span></span> <span data-ttu-id="4a3ea-226">而且`devices`hello hello 原則具有名稱為`Send`宣告。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-226">And that `devices` as hello name of hello policy that has a `Send` claim.</span></span>

3. <span data-ttu-id="4a3ea-227">使用下列命令 tooinsert 新的項目事件中樞中的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a3ea-227">Use hello following command tooinsert new entries in Event Hub:</span></span>
   
    ```bash
    node app.js
    ```
   
    <span data-ttu-id="4a3ea-228">您會看到的輸出包含 hello 資料的數行傳送 tooEvent 中樞：</span><span class="sxs-lookup"><span data-stu-id="4a3ea-228">You see several lines of output that contain hello data sent tooEvent Hub:</span></span>
   
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

### <a name="build-and-start-hello-topology"></a><span data-ttu-id="4a3ea-229">建置和啟動 hello 拓樸</span><span class="sxs-lookup"><span data-stu-id="4a3ea-229">Build and start hello topology</span></span>

1. <span data-ttu-id="4a3ea-230">開啟新的命令提示字元，然後將目錄變更太`hdinsight-eventhub-example/TemperatureMonitor`。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-230">Open a new command prompt and change directories too`hdinsight-eventhub-example/TemperatureMonitor`.</span></span> <span data-ttu-id="4a3ea-231">toobuild 和套件 hello 拓撲，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a3ea-231">toobuild and package hello topology, use hello following command:</span></span> 

    ```bash
    mvn clean package
    ```

2. <span data-ttu-id="4a3ea-232">在本機模式中，下列命令使用 hello toostart hello 拓撲：</span><span class="sxs-lookup"><span data-stu-id="4a3ea-232">toostart hello topology in local mode, use hello following command:</span></span>

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * <span data-ttu-id="4a3ea-233">`--local`在本機模式中啟動 hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-233">`--local` starts hello topology in local mode.</span></span>
    * <span data-ttu-id="4a3ea-234">`--filter`使用 hello`dev.properties`檔案 toopopulate 參數在 hello 拓撲定義。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-234">`--filter` uses hello `dev.properties` file toopopulate parameters in hello topology definition.</span></span>
    * <span data-ttu-id="4a3ea-235">`resources/no-hbase.yaml`使用 hello`no-hbase.yaml`拓撲定義。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-235">`resources/no-hbase.yaml` uses hello `no-hbase.yaml` topology definition.</span></span>
 
   <span data-ttu-id="4a3ea-236">一旦啟動，hello 拓撲從事件中心讀取項目，並將它們傳送 toohello 儀表板在您的本機電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-236">Once started, hello topology reads entries from Event Hub, and sends them toohello dashboard running on your local machine.</span></span> <span data-ttu-id="4a3ea-237">您應該會看到顯示 hello web 儀表板，類似 toohello 下列映像中的行：</span><span class="sxs-lookup"><span data-stu-id="4a3ea-237">You should see lines appear in hello web dashboard, similar toohello following image:</span></span>
   
    ![儀表板與資料](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. <span data-ttu-id="4a3ea-239">當執行 hello 儀表板時，使用 hello`node app.js`命令，從上一個 hello 步驟 toosend 新資料 tooEvent 集線器。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-239">While hello dashboard is running, use hello `node app.js` command from hello previous steps toosend new data tooEvent Hubs.</span></span> <span data-ttu-id="4a3ea-240">Hello 溫度值會隨機產生，因為 hello 圖形應該更新 tooshow 大量變更的溫度。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-240">Because hello temperature values are randomly generated, hello graph should update tooshow large changes in temperature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4a3ea-241">您必須在 hello **hdinsight-eventhub-範例/SendEvents/Nodejs**目錄時使用 hello`node app.js`命令。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-241">You must be in hello **hdinsight-eventhub-example/SendEvents/Nodejs** directory when using hello `node app.js` command.</span></span>

3. <span data-ttu-id="4a3ea-242">確認該 hello 儀表板更新時，使用 Ctrl + C 停止 hello 拓撲之後。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-242">After verifying that hello dashboard updates, stop hello topology using Ctrl+C.</span></span> <span data-ttu-id="4a3ea-243">您也可以使用 Ctrl + C toostop hello 本機 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-243">You can use Ctrl+C toostop hello local web server also.</span></span>

## <a name="create-a-storm-and-hbase-cluster"></a><span data-ttu-id="4a3ea-244">建立 Storm 和 HBase 叢集</span><span class="sxs-lookup"><span data-stu-id="4a3ea-244">Create a Storm and HBase cluster</span></span>

<span data-ttu-id="4a3ea-245">此區段的使用中的 hello 步驟[Azure Resource Manager 範本](../azure-resource-manager/resource-group-template-deploy.md)toocreate hello 虛擬網路上的 Azure 虛擬網路的 Storm 和 HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-245">hello steps in this section use an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) toocreate an Azure Virtual Network and a Storm and HBase cluster on hello virtual network.</span></span> <span data-ttu-id="4a3ea-246">hello 範本也會建立 Azure Web 應用程式，並部署到它的 hello 儀表板的複本。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-246">hello template also creates an Azure Web App and deploys a copy of hello dashboard into it.</span></span>

> [!NOTE]
> <span data-ttu-id="4a3ea-247">虛擬網路使用，以便與 hello HBase 叢集使用 hello HBase Java 應用程式開發介面，即可直接通訊 hello 拓撲 hello Storm 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-247">A virtual network is used so that hello topology running on hello Storm cluster can directly communicate with hello HBase cluster using hello HBase Java API.</span></span>

<span data-ttu-id="4a3ea-248">使用這份文件中的 hello Resource Manager 範本位於公用 blob 容器**https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-248">hello Resource Manager template used in this document is located in a public blob container at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span></span>

1. <span data-ttu-id="4a3ea-249">按一下下列按鈕 toosign 中 tooAzure 和開啟 hello Resource Manager 範本 hello Azure 入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-249">Click hello following button toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="4a3ea-250">從 hello**自訂部署**區段中，輸入下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a3ea-250">From hello **Custom deployment** section, enter hello following values:</span></span>
   
    ![HDInsight 參數](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * <span data-ttu-id="4a3ea-252">**基底叢集名稱**: hello hello Storm 和 HBase 叢集的基底名稱為使用此值。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-252">**Base Cluster Name**: This value is used as hello base name for hello Storm and HBase clusters.</span></span> <span data-ttu-id="4a3ea-253">例如，輸入 **abc** 會建立名為 **storm-abc** 的 Storm 叢集以及名為 **hbase-abc** 的 HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-253">For example, entering **abc** creates a Storm cluster named **storm-abc** and an HBase cluster named **hbase-abc**.</span></span>
   * <span data-ttu-id="4a3ea-254">**叢集登入使用者名稱**: hello Storm 和 HBase 叢集的 hello 系統管理員使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-254">**Cluster Login User Name**: hello admin user name for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="4a3ea-255">**叢集登入密碼**: hello Storm 和 HBase 叢集 hello 管理使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-255">**Cluster Login Password**: hello admin user password for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="4a3ea-256">**SSH 使用者名稱**: hello SSH 使用者 toocreate hello Storm 和 HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-256">**SSH User Name**: hello SSH user toocreate for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="4a3ea-257">**SSH 密碼**: hello hello Storm 和 HBase 叢集的 hello SSH 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-257">**SSH Password**: hello password for hello SSH user for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="4a3ea-258">**位置**: hello 區域 hello 叢集所建立的。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-258">**Location**: hello region that hello clusters are created in.</span></span>
     
     <span data-ttu-id="4a3ea-259">按一下**確定**toosave hello 參數。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-259">Click **OK** toosave hello parameters.</span></span>

3. <span data-ttu-id="4a3ea-260">使用 hello**基本概念**區段 toocreate 資源群組，或選取現有的我的最愛。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-260">Use hello **Basics** section toocreate a resource group or select an existing one.</span></span>
4. <span data-ttu-id="4a3ea-261">在 hello**資源群組位置**下拉式功能表中，選取 hello 相同的位置，您選取 hello**位置**中 hello 參數**設定**> 一節。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-261">In hello **Resource group location** dropdown menu, select hello same location as you selected for hello **Location** parameter in hello **Settings** section.</span></span>
5. <span data-ttu-id="4a3ea-262">讀取 hello 條款和條件，，然後選取  **toohello 條款和條件前面所述，即表示我同意**。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-262">Read hello terms and conditions, and then select **I agree toohello terms and conditions stated above**.</span></span>
6. <span data-ttu-id="4a3ea-263">最後，檢查**Pin toodashboard** ，然後選取 **購買**。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-263">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="4a3ea-264">它會採用約 20 分鐘 toocreate hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-264">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="4a3ea-265">一旦已建立 hello 資源，則會顯示 hello 資源群組的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-265">Once hello resources have been created, information about hello resource group is displayed.</span></span>

![Hello vnet 與叢集資源群組](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="4a3ea-267">請注意，hello hello HDInsight 叢集名稱**storm BASENAME**和**hbase BASENAME**，其中 BASENAME 是 hello 提供 toohello 範本的名稱。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-267">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **hbase-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="4a3ea-268">連接 toohello 叢集時，您可以使用稍後步驟中的這些名稱。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-268">You use these names in a later step when connecting toohello clusters.</span></span> <span data-ttu-id="4a3ea-269">請注意，hello hello 儀表板網站的名稱也是**basename 儀表板**。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-269">Also note that hello name of hello dashboard site is **basename-dashboard**.</span></span> <span data-ttu-id="4a3ea-270">本文件稍後將使用此值。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-270">This value is used later in this document.</span></span>

## <a name="configure-hello-dashboard-bolt"></a><span data-ttu-id="4a3ea-271">設定 hello 儀表板閃電</span><span class="sxs-lookup"><span data-stu-id="4a3ea-271">Configure hello Dashboard bolt</span></span>

<span data-ttu-id="4a3ea-272">toosend 資料 toohello 儀表板部署為 web 應用程式，您必須修改下列一行 hello hello`dev.properties`檔案：</span><span class="sxs-lookup"><span data-stu-id="4a3ea-272">toosend data toohello dashboard deployed as a web app, you must modify hello following line in hello `dev.properties`file:</span></span>

```yaml
dashboard.uri: http://localhost:3000
```

<span data-ttu-id="4a3ea-273">變更`http://localhost:3000`太`http://BASENAME-dashboard.azurewebsites.net`儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-273">Change `http://localhost:3000` too`http://BASENAME-dashboard.azurewebsites.net` and save hello file.</span></span> <span data-ttu-id="4a3ea-274">取代**BASENAME**與 hello hello 上一個步驟中所提供的基底名稱。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-274">Replace **BASENAME** with hello base name you provided in hello previous step.</span></span> <span data-ttu-id="4a3ea-275">您也可以使用先前建立 tooselect hello 儀表板和檢視 hello URL hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-275">You can also use hello resource group created previously tooselect hello dashboard and view hello URL.</span></span>

## <a name="create-hello-hbase-table"></a><span data-ttu-id="4a3ea-276">建立 hello HBase 資料表</span><span class="sxs-lookup"><span data-stu-id="4a3ea-276">Create hello HBase table</span></span>

<span data-ttu-id="4a3ea-277">對 HBase 中的 toostore 資料，我們必須先建立資料表。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-277">toostore data in HBase, we must first create a table.</span></span> <span data-ttu-id="4a3ea-278">預先建立 Storm 需要 toowrite 到的資源，因為嘗試 toocreate 從內部資源 Storm 拓撲可能會導致多個執行個體嘗試 toocreate hello 相同的資源。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-278">Pre-create resources that Storm needs toowrite to, as trying toocreate resources from inside a Storm topology can result in multiple instances trying toocreate hello same resource.</span></span> <span data-ttu-id="4a3ea-279">建立 hello hello 拓撲之外的資源並使用 Storm 讀取/寫入與分析。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-279">Create hello resources outside hello topology and use Storm for reading/writing and analytics.</span></span>

1. <span data-ttu-id="4a3ea-280">使用 SSH tooconnect toohello HBase 叢集使用 hello SSH 使用者名稱和您在叢集建立期間提供 toohello 範本的密碼。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-280">Use SSH tooconnect toohello HBase cluster using hello SSH user and password you supplied toohello template during cluster creation.</span></span> <span data-ttu-id="4a3ea-281">例如，如果連接使用 hello`ssh`命令時，您可以使用下列語法的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a3ea-281">For example, if connecting using hello `ssh` command, you would use hello following syntax:</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    <span data-ttu-id="4a3ea-282">取代`sshuser`hello SSH 使用者名稱與您在建立時提供 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-282">Replace `sshuser` with hello SSH user name you provided when creating hello cluster.</span></span> <span data-ttu-id="4a3ea-283">取代`clustername`與 hello HBase 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-283">Replace `clustername` with hello HBase cluster name.</span></span>

2. <span data-ttu-id="4a3ea-284">從 hello SSH 工作階段，啟動 hello HBase 殼層。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-284">From hello SSH session, start hello HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="4a3ea-285">當載入 hello 殼層時，您會看到`hbase(main):001:0>`提示字元。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-285">Once hello shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="4a3ea-286">從 hello HBase 殼層中，輸入下列命令 toocreate 資料表 toostore hello 感應器資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a3ea-286">From hello HBase shell, enter hello following command toocreate a table toostore hello sensor data:</span></span>
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. <span data-ttu-id="4a3ea-287">請確認已建立該 hello 資料表使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="4a3ea-287">Verify that hello table has been created by using hello following command:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="4a3ea-288">這會傳回的資訊類似 toohello 下列範例中，指出 hello 資料表中有 0 個資料列。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-288">This returns information similar toohello following example, indicating that there are 0 rows in hello table.</span></span>
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. <span data-ttu-id="4a3ea-289">輸入`exit`tooexit hello HBase 殼層：</span><span class="sxs-lookup"><span data-stu-id="4a3ea-289">Enter `exit` tooexit hello HBase shell:</span></span>

## <a name="configure-hello-hbase-bolt"></a><span data-ttu-id="4a3ea-290">設定 hello HBase 閃電</span><span class="sxs-lookup"><span data-stu-id="4a3ea-290">Configure hello HBase bolt</span></span>

<span data-ttu-id="4a3ea-291">toowrite tooHBase 從 hello Storm 叢集，您必須提供 hello HBase 閃電 HBase 叢集的 hello 設定詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-291">toowrite tooHBase from hello Storm cluster, you must provide hello HBase bolt with hello configuration details of your HBase cluster.</span></span>

1. <span data-ttu-id="4a3ea-292">使用下列範例 tooretrieve hello 動物園管理員仲裁 HBase 叢集的 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="4a3ea-292">Use one of hello following examples tooretrieve hello Zookeeper quorum for your HBase cluster:</span></span>

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > <span data-ttu-id="4a3ea-293">取代`your_HDInsight_cluster_name`hello 名稱，為您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-293">Replace `your_HDInsight_cluster_name` with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="4a3ea-294">如需有關安裝 hello`jq`公用程式，請參閱[https://stedolan.github.io/jq/](https://stedolan.github.io/jq/)。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-294">For more information on installing hello `jq` utility, see [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span></span>
    >
    > <span data-ttu-id="4a3ea-295">出現提示時，輸入 hello 密碼 hello HDInsight admin 登入。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-295">When prompted, enter hello password for hello HDInsight admin login.</span></span>

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > <span data-ttu-id="4a3ea-296">取代 ' your_HDInsight_cluster_name hello 名稱，為您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-296">Replace \`your_HDInsight_cluster_name with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="4a3ea-297">出現提示時，輸入 hello 密碼 hello HDInsight admin 登入。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-297">When prompted, enter hello password for hello HDInsight admin login.</span></span>
    >
    > <span data-ttu-id="4a3ea-298">此範例需要 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-298">This example requires Azure PowerShell.</span></span> <span data-ttu-id="4a3ea-299">如需進一步了解 Azure PowerShell 之使用，請參閱 [Azure PowerShell 使用者入門](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span><span class="sxs-lookup"><span data-stu-id="4a3ea-299">For more information on using Azure PowerShell, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span></span>

    <span data-ttu-id="4a3ea-300">這些範例中所傳回的 hello 資訊是類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="4a3ea-300">hello information returned by these examples is similar toohello following text:</span></span>

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    <span data-ttu-id="4a3ea-301">與 hello HBase 叢集的 Storm toocommunicate 會使用這項資訊。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-301">This information is used by Storm toocommunicate with hello HBase cluster.</span></span>

2. <span data-ttu-id="4a3ea-302">修改 hello`dev.properties`檔案，然後加入下列行 hello 動物園管理員仲裁資訊 toohello:</span><span class="sxs-lookup"><span data-stu-id="4a3ea-302">Modify hello `dev.properties` file and add hello Zookeeper quorum information toohello following line:</span></span>

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a><span data-ttu-id="4a3ea-303">建置、 封裝和部署 hello 方案 tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="4a3ea-303">Build, package, and deploy hello solution tooHDInsight</span></span>

<span data-ttu-id="4a3ea-304">在開發環境中，使用下列步驟 toodeploy hello Storm 拓撲 toohello storm 叢集 hello。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-304">In your development environment, use hello following steps toodeploy hello Storm topology toohello storm cluster.</span></span>

1. <span data-ttu-id="4a3ea-305">從 hello`TemperatureMonitor`目錄下，使用 hello 下列命令 tooperform 新的組建，並從您的專案建立 JAR 封裝：</span><span class="sxs-lookup"><span data-stu-id="4a3ea-305">From hello `TemperatureMonitor` directory, use hello following command tooperform a new build and create a JAR package from your project:</span></span>
   
        mvn clean package
   
    <span data-ttu-id="4a3ea-306">此命令會在專案的目標目錄中建立名為 `TemperatureMonitor-1.0-SNAPSHOT.jar in hello ` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-306">This command creates a file named `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `target\` directory of your project.</span></span>

2. <span data-ttu-id="4a3ea-307">使用 scp tooupload hello`TemperatureMonitor-1.0-SNAPSHOT.jar`和`dev.properties`檔案 tooyour Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-307">Use scp tooupload hello `TemperatureMonitor-1.0-SNAPSHOT.jar` and `dev.properties` files tooyour Storm cluster.</span></span> <span data-ttu-id="4a3ea-308">Hello 在下列範例，取代`sshuser`與 hello 建立 hello 叢集時，您所提供的 SSH 使用者和`clustername`hello Storm 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-308">In hello following example, replace `sshuser` with hello SSH user you provided when creating hello cluster, and `clustername` with hello name of your Storm cluster.</span></span> <span data-ttu-id="4a3ea-309">出現提示時，輸入 hello SSH 使用者 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-309">When prompted, enter hello password for hello SSH user.</span></span>
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > <span data-ttu-id="4a3ea-310">它可能需要幾分鐘的時間 tooupload hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-310">It may take several minutes tooupload hello files.</span></span>

    <span data-ttu-id="4a3ea-311">如需有關使用 hello`scp`和`ssh`命令與 HDInsight，請參閱[搭配使用 SSH 和 HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="4a3ea-311">For more information on using hello `scp` and `ssh` commands with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

3. <span data-ttu-id="4a3ea-312">Hello 檔案已上傳，一旦連接使用 SSH toohello Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-312">Once hello file has been uploaded, connect toohello Storm cluster using SSH.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="4a3ea-313">取代`sshuser`hello SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-313">Replace `sshuser` with hello SSH user name.</span></span> <span data-ttu-id="4a3ea-314">取代`clustername`與 hello Storm 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-314">Replace `clustername` with hello Storm cluster name.</span></span>

4. <span data-ttu-id="4a3ea-315">toostart hello 拓撲，請使用下列命令從 hello SSH 工作階段的 hello:</span><span class="sxs-lookup"><span data-stu-id="4a3ea-315">toostart hello topology, use hello following command from hello SSH session:</span></span>
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * <span data-ttu-id="4a3ea-316">`--remote`送出 hello 拓撲 toohello Nimbus 服務，將其發佈 hello 叢集中的 toohello 監督員節點。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-316">`--remote` submits hello topology toohello Nimbus service, which distributes it toohello supervisor nodes in hello cluster.</span></span>
    * <span data-ttu-id="4a3ea-317">`--filter`使用 hello`dev.properties`檔案 toopopulate 參數在 hello 拓撲定義。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-317">`--filter` uses hello `dev.properties` file toopopulate parameters in hello topology definition.</span></span>
    * <span data-ttu-id="4a3ea-318">`-R /with-hbase.yaml`使用 hello `with-hbase.yaml` hello 封裝中包含的拓撲。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-318">`-R /with-hbase.yaml` uses hello `with-hbase.yaml` topology included in hello package.</span></span>

5. <span data-ttu-id="4a3ea-319">啟動 hello 拓撲後，開啟您在 Azure，然後使用 hello 發行瀏覽器 toohello 網站`node app.js`命令 toosend 資料 tooEvent 中樞。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-319">After hello topology has started, open a browser toohello website you published on Azure, then use hello `node app.js` command toosend data tooEvent Hub.</span></span> <span data-ttu-id="4a3ea-320">您應該會看到 hello web 儀表板更新 toodisplay hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-320">You should see hello web dashboard update toodisplay hello information.</span></span>
   
    ![儀表板](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a><span data-ttu-id="4a3ea-322">檢視 HBase 資料</span><span class="sxs-lookup"><span data-stu-id="4a3ea-322">View HBase data</span></span>

<span data-ttu-id="4a3ea-323">使用下列步驟 tooconnect tooHBase hello，並確認 hello 資料，已寫入 toohello 資料表：</span><span class="sxs-lookup"><span data-stu-id="4a3ea-323">Use hello following steps tooconnect tooHBase and verify that hello data has been written toohello table:</span></span>

1. <span data-ttu-id="4a3ea-324">使用 SSH tooconnect toohello HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-324">Use SSH tooconnect toohello HBase cluster.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="4a3ea-325">取代`sshuser`hello SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-325">Replace `sshuser` with hello SSH user name.</span></span> <span data-ttu-id="4a3ea-326">取代`clustername`與 hello HBase 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-326">Replace `clustername` with hello HBase cluster name.</span></span>

2. <span data-ttu-id="4a3ea-327">從 hello SSH 工作階段，啟動 hello HBase 殼層。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-327">From hello SSH session, start hello HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="4a3ea-328">當載入 hello 殼層時，您會看到`hbase(main):001:0>`提示字元。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-328">Once hello shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="4a3ea-329">Hello 資料表中的檢視資料列：</span><span class="sxs-lookup"><span data-stu-id="4a3ea-329">View rows from hello table:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="4a3ea-330">此命令會傳回下列文字，表示 hello 資料表中沒有資料的資訊類似 toohello。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-330">This command returns information similar toohello following text, indicating that there is data in hello table.</span></span>
   
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
   > <span data-ttu-id="4a3ea-331">這項掃描作業會傳回最多 10 個資料列 hello 資料表中。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-331">This scan operation returns a maximum of 10 rows from hello table.</span></span>

## <a name="delete-your-clusters"></a><span data-ttu-id="4a3ea-332">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="4a3ea-332">Delete your clusters</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="4a3ea-333">toodelete hello 叢集、 存放裝置，以及 web 應用程式一次刪除 hello 包含它們的資源群組。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-333">toodelete hello clusters, storage, and web app at one time, delete hello resource group that contains them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a3ea-334">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4a3ea-334">Next steps</span></span>

<span data-ttu-id="4a3ea-335">若需更多搭配 HDInsight 的 Storm 拓撲範例，請參閱 [Storm on HDInsight 的範例拓撲](hdinsight-storm-example-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-335">For more examples of Storm topologies with HDInsight, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md)</span></span>

<span data-ttu-id="4a3ea-336">如需 Apache Storm 的詳細資訊，請參閱 hello [Apache Storm](https://storm.incubator.apache.org/)站台。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-336">For more information about Apache Storm, see hello [Apache Storm](https://storm.incubator.apache.org/) site.</span></span>

<span data-ttu-id="4a3ea-337">如需 HDInsight HBase 的相關詳細資訊，請參閱 hello[概觀 HDInsight HBase](hdinsight-hbase-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-337">For more information about HBase on HDInsight, see hello [HBase with HDInsight Overview](hdinsight-hbase-overview.md).</span></span>

<span data-ttu-id="4a3ea-338">如需 Socket.io 的詳細資訊，請參閱 hello [socket.io](http://socket.io/)站台。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-338">For more information about Socket.io, see hello [socket.io](http://socket.io/) site.</span></span>

<span data-ttu-id="4a3ea-339">如需關於 D3.js 的詳細資訊，請參閱 [D3.js：資料驅動型文件](http://d3js.org/)(英文)。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-339">For more information about D3.js, see [D3.js - Data Driven Documents](http://d3js.org/).</span></span>

<span data-ttu-id="4a3ea-340">如需關於以 Java 建立拓撲的詳細資訊，請參閱 [為 Apache Storm on HDInsight 開發 Java 拓撲](hdinsight-storm-develop-java-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-340">For information about creating topologies in Java, see [Develop Java topologies for Apache Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="4a3ea-341">如需關於以 .NET 建立拓撲的詳細資訊，請參閱 [使用 Visual Studio 為 Apache Storm on HDInsight 開發 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="4a3ea-341">For information about creating topologies in .NET, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

[azure-portal]: https://portal.azure.com
