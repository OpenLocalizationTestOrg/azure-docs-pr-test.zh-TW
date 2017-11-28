---
title: "Azure HDInsight 中的事件中樞與串流處理的 aaaUse Apache Spark |Microsoft 文件"
description: "建置 Apache Spark 資料流範例等方式 toosend 資料流 tooAzure 事件中心然後 HDInsight Spark 叢集使用 scala 應用程式中接收這些事件。"
keywords: "apache spark 串流, spark 串流, spark 範例, apache spark 串流範例, 事件中樞 azure 範例, spark 範例"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 68894e75-3ffa-47bd-8982-96cdad38b7d0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 10cc5884047b3b8249fe8a8822a16a19780a4af3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="74ddc-104">Apache Spark 串流：在 HDInsight 上使用 Spark 叢集處理來自 Azure 事件中樞的資料</span><span class="sxs-lookup"><span data-stu-id="74ddc-104">Apache Spark streaming: Process data from Azure Event Hubs with Spark cluster on HDInsight</span></span>

<span data-ttu-id="74ddc-105">在本文中，您可以建立資料流的範例，包括下列步驟的 hello Apache Spark:</span><span class="sxs-lookup"><span data-stu-id="74ddc-105">In this article, you create an Apache Spark streaming sample that involves hello following steps:</span></span>

1. <span data-ttu-id="74ddc-106">您可以使用獨立應用程式 tooingest 訊息到 Azure 事件中心。</span><span class="sxs-lookup"><span data-stu-id="74ddc-106">You use a standalone application tooingest messages into an Azure Event Hub.</span></span>

2. <span data-ttu-id="74ddc-107">使用兩種不同的方法，您擷取 hello 訊息從事件中心中即時使用 Azure HDInsight 上的 Spark 叢集中執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="74ddc-107">With two different approaches, you retrieve hello messages from Event Hub in real-time using an application running in Spark cluster on Azure HDInsight.</span></span>

3. <span data-ttu-id="74ddc-108">建置串流分析管線 toopersist 資料 toodifferent 儲存系統，或從 hello 即時資料中取得見解。</span><span class="sxs-lookup"><span data-stu-id="74ddc-108">You build streaming analytic pipelines toopersist data toodifferent storage systems, or get insights from data on hello fly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74ddc-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="74ddc-109">Prerequisites</span></span>

* <span data-ttu-id="74ddc-110">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="74ddc-110">An Azure subscription.</span></span> <span data-ttu-id="74ddc-111">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="74ddc-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="74ddc-112">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="74ddc-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="74ddc-113">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="74ddc-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="spark-streaming-concepts"></a><span data-ttu-id="74ddc-114">Spark 串流處理概念</span><span class="sxs-lookup"><span data-stu-id="74ddc-114">Spark Streaming concepts</span></span>

<span data-ttu-id="74ddc-115">如需 Spark 串流的詳細說明，請參閱 [Apache Spark 串流概觀](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview)。</span><span class="sxs-lookup"><span data-stu-id="74ddc-115">For a detailed explanation of Spark streaming, see [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span></span> <span data-ttu-id="74ddc-116">HDInsight 帶來的 hello Azure 的相同資料流功能 tooa Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="74ddc-116">HDInsight brings hello same streaming features tooa Spark cluster on Azure.</span></span>  

## <a name="what-does-this-solution-do"></a><span data-ttu-id="74ddc-117">此解決方案有哪些功能？</span><span class="sxs-lookup"><span data-stu-id="74ddc-117">What does this solution do?</span></span>

<span data-ttu-id="74ddc-118">在這篇文章 toocreate Spark 串流範例中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="74ddc-118">In this article, toocreate a Spark streaming example, perform hello following steps:</span></span>

1. <span data-ttu-id="74ddc-119">建立會接收事件串流的 Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="74ddc-119">Create an Azure Event Hub that will receive a stream of events.</span></span>

2. <span data-ttu-id="74ddc-120">執行本機的獨立應用程式會產生事件，並將其發送 toohello Azure 事件中心。</span><span class="sxs-lookup"><span data-stu-id="74ddc-120">Run a local standalone application that generates events and pushes it toohello Azure Event Hub.</span></span> <span data-ttu-id="74ddc-121">此 hello 範例應用程式發行在[https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples)。</span><span class="sxs-lookup"><span data-stu-id="74ddc-121">hello sample application that does this is published at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span>

3. <span data-ttu-id="74ddc-122">在 Spark 叢集上遠端執行串流應用程式，該應用程式可從 Azure 事件中樞讀取串流事件，並執行各種資料處理/分析。</span><span class="sxs-lookup"><span data-stu-id="74ddc-122">Run a streaming application remotely on a Spark cluster that reads streaming events from Azure Event Hub and perform various data processing/analysis.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="74ddc-123">建立 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="74ddc-123">Create an Azure Event Hub</span></span>

1. <span data-ttu-id="74ddc-124">登入 toohello [Azure 入口網站](https://ms.portal.azure.com)，然後按一下**新增**hello 在左上方的囉 」 畫面。</span><span class="sxs-lookup"><span data-stu-id="74ddc-124">Log on toohello [Azure Portal](https://ms.portal.azure.com), and click **New** at hello top left of hello screen.</span></span>

2. <span data-ttu-id="74ddc-125">按一下 [物聯網]，然後按一下 [事件中樞]。</span><span class="sxs-lookup"><span data-stu-id="74ddc-125">Click **Internet of Things**, then click **Event Hubs**.</span></span>

    <span data-ttu-id="74ddc-126">![建立 Spark 串流範例的事件中樞](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "建立 Spark 串流範例的事件中樞")</span><span class="sxs-lookup"><span data-stu-id="74ddc-126">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span></span>

3. <span data-ttu-id="74ddc-127">在 hello**建立命名空間**刀鋒視窗中，輸入命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="74ddc-127">In hello **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="74ddc-128">選擇定價層 （基本或標準） 的 hello。</span><span class="sxs-lookup"><span data-stu-id="74ddc-128">choose hello pricing tier (Basic or Standard).</span></span> <span data-ttu-id="74ddc-129">而且請 toocreate hello 資源選擇 Azure 訂用帳戶、 資源群組和位置。</span><span class="sxs-lookup"><span data-stu-id="74ddc-129">Also, choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> <span data-ttu-id="74ddc-130">按一下**建立**toocreate hello 命名空間。</span><span class="sxs-lookup"><span data-stu-id="74ddc-130">Click **Create** toocreate hello namespace.</span></span>

      <span data-ttu-id="74ddc-131">![提供 Spark 串流範例的事件中樞名稱](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "提供 Spark 串流範例的事件中樞名稱")</span><span class="sxs-lookup"><span data-stu-id="74ddc-131">![Provide an event hub name for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span></span>

    > [!NOTE]
    > <span data-ttu-id="74ddc-132">您選取應該 hello 相同**位置**與您的 Apache Spark 叢集，在 HDInsight tooreduce 延遲和成本。</span><span class="sxs-lookup"><span data-stu-id="74ddc-132">You should select hello same **Location** as your Apache Spark cluster in HDInsight tooreduce latency and costs.</span></span>
    >
    >

4. <span data-ttu-id="74ddc-133">在 hello 事件中樞命名空間清單中，按一下 hello 新建的命名空間。</span><span class="sxs-lookup"><span data-stu-id="74ddc-133">In hello Event Hubs namespace list, click hello newly-created namespace.</span></span>      


5. <span data-ttu-id="74ddc-134">在 hello 命名空間刀鋒視窗中，按一下 **事件中心**，然後按一下 **+ 事件中心**toocreate 新的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="74ddc-134">In hello namespace blade, click **Event Hubs**, and then click **+ Event Hub** toocreate a new Event Hub.</span></span>
   
    <span data-ttu-id="74ddc-135">![建立 Spark 串流範例的事件中樞](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "建立 Spark 串流範例的事件中樞")</span><span class="sxs-lookup"><span data-stu-id="74ddc-135">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Create event hub for Spark streaming example")</span></span>

6. <span data-ttu-id="74ddc-136">輸入您的事件中樞、 組 hello 資料分割計數 too10 和訊息保留 too1 的名稱。</span><span class="sxs-lookup"><span data-stu-id="74ddc-136">Type a name for your Event Hub, set hello partition count too10, and message retention too1.</span></span> <span data-ttu-id="74ddc-137">我們不保存此解決方案中的 hello 訊息，因此可以讓 hello 其餘部分，做為預設值，再按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="74ddc-137">We are not archiving hello messages in this solution so you can leave hello rest as default, and then click **Create**.</span></span>
   
    <span data-ttu-id="74ddc-138">![提供 Spark 串流範例的事件中樞詳細資料](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "提供 Spark 串流範例的事件中樞詳細資料")</span><span class="sxs-lookup"><span data-stu-id="74ddc-138">![Provide event hub details for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span></span>

7. <span data-ttu-id="74ddc-139">新建立的事件中樞的 hello 會列在 hello 事件中心刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="74ddc-139">hello newly created Event Hub is listed in hello Event Hub blade.</span></span>
    
     <span data-ttu-id="74ddc-140">![檢視事件中心的 hello Spark 串流範例](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "hello 的檢視事件中心二手資料流範例")</span><span class="sxs-lookup"><span data-stu-id="74ddc-140">![View Event Hub for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "View Event Hub for hello Spark streaming example")</span></span>

8. <span data-ttu-id="74ddc-141">在 hello 命名空間刀鋒視窗中 （不 hello 特定事件中心刀鋒視窗），按一下 **共用存取原則**，然後按一下 **RootManageSharedAccessKey**。</span><span class="sxs-lookup"><span data-stu-id="74ddc-141">Back in hello namespace blade (not hello specific Event Hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
     <span data-ttu-id="74ddc-142">![設定事件中樞原則 hello Spark 串流範例](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "hello 的設定事件中樞原則二手資料流範例")</span><span class="sxs-lookup"><span data-stu-id="74ddc-142">![Set Event Hub policies for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Set Event Hub policies for hello Spark streaming example")</span></span>

9. <span data-ttu-id="74ddc-143">按一下 hello 複製按鈕 toocopy hello **RootManageSharedAccessKey**主要金鑰和連接字串 toohello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="74ddc-143">Click hello copy button toocopy hello **RootManageSharedAccessKey** primary key and connection string toohello clipboard.</span></span> <span data-ttu-id="74ddc-144">儲存這些 toouse hello 教學課程。</span><span class="sxs-lookup"><span data-stu-id="74ddc-144">Save these toouse later in hello tutorial.</span></span>
    
     <span data-ttu-id="74ddc-145">![檢視事件中樞原則機碼，例如 hello Spark 串流](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "hello 檢視事件中樞原則機碼二手資料流範例")</span><span class="sxs-lookup"><span data-stu-id="74ddc-145">![View Event Hub policy keys for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "View Event Hub policy keys for hello Spark streaming example")</span></span>

## <a name="send-messages-tooazure-event-hub-using-a-sample-scala-application"></a><span data-ttu-id="74ddc-146">傳送訊息 tooAzure 使用範例 Scala 應用程式的事件中樞</span><span class="sxs-lookup"><span data-stu-id="74ddc-146">Send messages tooAzure Event Hub using a sample Scala application</span></span>

<span data-ttu-id="74ddc-147">本節中您要使用的獨立本機 Scala 應用程式會產生事件資料流，並將它傳送 tooAzure 您稍早建立的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="74ddc-147">In this section you use a standalone local Scala application that generates a stream of events and sends it tooAzure Event Hub that you created earlier.</span></span> <span data-ttu-id="74ddc-148">此應用程式可從 GitHub 取得，網址是： [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer)。</span><span class="sxs-lookup"><span data-stu-id="74ddc-148">This application is available on GitHub at [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span></span> <span data-ttu-id="74ddc-149">此處 hello 步驟假設您已經分叉時這個 GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="74ddc-149">hello steps here assume that you have already forked this GitHub repository.</span></span>

1. <span data-ttu-id="74ddc-150">請確定您擁有 hello hello 您用來執行此應用程式的電腦上安裝下列項目。</span><span class="sxs-lookup"><span data-stu-id="74ddc-150">Make sure you have hello following installed on hello computer where you run this application.</span></span>

    * <span data-ttu-id="74ddc-151">Oracle Java Development Kit。</span><span class="sxs-lookup"><span data-stu-id="74ddc-151">Oracle Java Development kit.</span></span> <span data-ttu-id="74ddc-152">您可以從[這裡](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)安裝它。</span><span class="sxs-lookup"><span data-stu-id="74ddc-152">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
    * <span data-ttu-id="74ddc-153">Apache Maven。</span><span class="sxs-lookup"><span data-stu-id="74ddc-153">Apache Maven.</span></span> <span data-ttu-id="74ddc-154">您可以從 [這裡](https://maven.apache.org/download.cgi)下載。</span><span class="sxs-lookup"><span data-stu-id="74ddc-154">You can download it from [here](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="74ddc-155">指示 tooinstall Maven 可用[這裡](https://maven.apache.org/install.html)。</span><span class="sxs-lookup"><span data-stu-id="74ddc-155">Instructions tooinstall Maven are available [here](https://maven.apache.org/install.html).</span></span>

2. <span data-ttu-id="74ddc-156">開啟命令提示字元並瀏覽 toohello 位置複製 hello GitHub 儲存機制，用於 hello 範例 Scala 應用程式，執行下列命令 toobuild hello 應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="74ddc-156">Open a command prompt and navigate toohello location you cloned hello GitHub repo for hello sample Scala application and run hello following command toobuild hello application.</span></span>

        mvn package

3. <span data-ttu-id="74ddc-157">hello 輸出 jar hello 應用程式， **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**，下方會建立**/目標**目錄。</span><span class="sxs-lookup"><span data-stu-id="74ddc-157">hello output jar for hello application, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, is created under **/target** directory.</span></span> <span data-ttu-id="74ddc-158">您使用這個 JAR 稍後在這個發行項 tootest hello 完整解決方案。</span><span class="sxs-lookup"><span data-stu-id="74ddc-158">You use this JAR later in this article tootest hello complete solution.</span></span>

## <a name="create-application-tooreceive-messages-from-event-hub-into-a-spark-cluster"></a><span data-ttu-id="74ddc-159">建立 Spark 叢集，以從事件中心應用程式 tooreceive 訊息</span><span class="sxs-lookup"><span data-stu-id="74ddc-159">Create application tooreceive messages from Event Hub into a Spark cluster</span></span> 

<span data-ttu-id="74ddc-160">我們有兩個方法 tooconnect Spark 資料流和 Azure 事件中樞、 收件者為基礎的連接和直接 DStream 基礎的連接。</span><span class="sxs-lookup"><span data-stu-id="74ddc-160">We have two approaches tooconnect Spark Streaming and Azure Event Hubs, Receiver-based connection and Direct-DStream-based connection.</span></span> <span data-ttu-id="74ddc-161">Direct DStream 基礎 2017 年 1 月，在中引進 hello 2.0.3 版本。</span><span class="sxs-lookup"><span data-stu-id="74ddc-161">Direct-DStream-based is introduced on Jan of 2017, in hello 2.0.3 release.</span></span> <span data-ttu-id="74ddc-162">它應該 tooreplace hello 原始收件者為基礎的連接，所以更好的效能和資源效率。</span><span class="sxs-lookup"><span data-stu-id="74ddc-162">It is supposed tooreplace hello original receiver-based connection as it is more performant and resource-efficient.</span></span> <span data-ttu-id="74ddc-163">如需更多詳細資料，請參閱 [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs)。</span><span class="sxs-lookup"><span data-stu-id="74ddc-163">More details found in [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span></span> <span data-ttu-id="74ddc-164">Direct DStream 只支援 Spark 2.0+。</span><span class="sxs-lookup"><span data-stu-id="74ddc-164">Direct DStream only supports Spark 2.0+.</span></span>

### <a name="build-applications-with-hello-dependency-toospark-eventhubs-connector"></a><span data-ttu-id="74ddc-165">建置應用程式與 hello 相依性 toospark eventhubs 連接器</span><span class="sxs-lookup"><span data-stu-id="74ddc-165">Build applications with hello dependency toospark-eventhubs connector</span></span>

<span data-ttu-id="74ddc-166">我們也會發行臨時版 Spark-EventHubs GitHub 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="74ddc-166">We will also publish hello staging version of Spark-EventHubs in GitHub.</span></span> <span data-ttu-id="74ddc-167">toouse hello 臨時版 Spark EventHubs，hello 第一個步驟是 tooindicate GitHub 時加入下列項目 toopom.xml hello hello 來源儲存機制：</span><span class="sxs-lookup"><span data-stu-id="74ddc-167">toouse hello staging version of Spark-EventHubs, hello first step is tooindicate GitHub as hello source repo by adding hello following entry toopom.xml:</span></span>

```xml
<repository>
      <id>spark-eventhubs</id>
      <url>https://raw.github.com/hdinsight/spark-eventhubs/maven-repo/</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>always</updatePolicy>
      </snapshots>
</repository>
```

<span data-ttu-id="74ddc-168">然後，您可以加入下列相依性 tooyour 專案 tootake hello 發行前版本的 hello。</span><span class="sxs-lookup"><span data-stu-id="74ddc-168">You can then add hello following dependency tooyour project tootake hello pre-released version.</span></span>

<span data-ttu-id="74ddc-169">Maven 相依性</span><span class="sxs-lookup"><span data-stu-id="74ddc-169">Maven Dependency</span></span>

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

<span data-ttu-id="74ddc-170">SBT 相依性</span><span class="sxs-lookup"><span data-stu-id="74ddc-170">SBT Dependency</span></span>

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a><span data-ttu-id="74ddc-171">Direct DStream 連線</span><span class="sxs-lookup"><span data-stu-id="74ddc-171">Direct DStream Connection</span></span>

<span data-ttu-id="74ddc-172">包含使用 Direct DStream 範例的預先建立 jar 檔案可在 [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar) 中下載。</span><span class="sxs-lookup"><span data-stu-id="74ddc-172">A pre-built jar file containing examples using Direct DStream can be downloaded in [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span></span>

<span data-ttu-id="74ddc-173">hello jar 檔案包含三個範例的原始程式碼位於[https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream)。</span><span class="sxs-lookup"><span data-stu-id="74ddc-173">hello jar file contains three examples whose source code are available at [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span></span>

<span data-ttu-id="74ddc-174">將 [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) 作為範例：</span><span class="sxs-lookup"><span data-stu-id="74ddc-174">Taking [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) as an example:</span></span>

```scala
private def createStreamingContext(
  sparkCheckpointDir: String,
  batchDuration: Int,
  namespace: String,
  eventHunName: String,
  eventhubParams: Map[String, String],
  progressDir: String) = {
val ssc = new StreamingContext(new SparkContext(), Seconds(batchDuration))
ssc.checkpoint(sparkCheckpointDir)
val inputDirectStream = EventHubsUtils.createDirectStreams(
  ssc,
  namespace,
  progressDir,
  Map(eventHunName -> eventhubParams))

inputDirectStream.map(receivedRecord => (new String(receivedRecord.getBody), 1)).
  reduceByKeyAndWindow((v1, v2) => v1 + v2, (v1, v2) => v1 - v2, Seconds(batchDuration * 3),
    Seconds(batchDuration)).print()

ssc
}

def main(args: Array[String]): Unit = {

if (args.length != 8) {
  println("Usage: program progressDir PolicyName PolicyKey EventHubNamespace EventHubName" +
    " BatchDuration(seconds) Spark_Checkpoint_Directory maxRate")
  sys.exit(1)
}

val progressDir = args(0)
val policyName = args(1)
val policykey = args(2)
val namespace = args(3)
val name = args(4)
val batchDuration = args(5).toInt
val sparkCheckpointDir = args(6)
val maxRate = args(7)

val eventhubParameters = Map[String, String] (
  "eventhubs.policyname" -> policyName,
  "eventhubs.policykey" -> policykey,
  "eventhubs.namespace" -> namespace,
  "eventhubs.name" -> name,
  "eventhubs.partition.count" -> "32",
  "eventhubs.consumergroup" -> "$Default",
  "eventhubs.maxRate" -> s"$maxRate"
)

val ssc = StreamingContext.getOrCreate(sparkCheckpointDir,
  () => createStreamingContext(sparkCheckpointDir, batchDuration, namespace, name,
    eventhubParameters, progressDir))

ssc.start()
ssc.awaitTermination()
}
```

<span data-ttu-id="74ddc-175">在上述範例中，hello`eventhubParameters`是 hello 參數特定 tooa 單一 EventHubs 執行個體，而且您有 toopass 它 toohello`createDirectStreams`建構直接 DStream 物件對應 tooa 事件中樞命名空間的 API。</span><span class="sxs-lookup"><span data-stu-id="74ddc-175">In hello above example, `eventhubParameters` are hello parameters specific tooa single EventHubs instance and you have toopass it toohello `createDirectStreams` API which constructs a Direct DStream object mapping tooa Event Hubs namespace.</span></span> <span data-ttu-id="74ddc-176">透過 hello 直接 DStream 物件，您可以呼叫任何 Spark Streaming API framework 所提供的 DStream API。</span><span class="sxs-lookup"><span data-stu-id="74ddc-176">Over hello Direct DStream object, you can call any DStream API provided by Spark Streaming API framework.</span></span> <span data-ttu-id="74ddc-177">在此範例中，我們可以計算 hello 頻率，每個字 hello 最後 3 微批次間隔內。</span><span class="sxs-lookup"><span data-stu-id="74ddc-177">In this example, we calculate hello frequency of each word within hello last 3 micro batch intervals.</span></span>

### <a name="receiver-based-connection"></a><span data-ttu-id="74ddc-178">收件者型連線</span><span class="sxs-lookup"><span data-stu-id="74ddc-178">Receiver-based Connection</span></span>

<span data-ttu-id="74ddc-179">Spark，串流 Scala，收到事件和路由 hello toodifferent 目的地時，所撰寫的範例應用程式將會位於[https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples)。</span><span class="sxs-lookup"><span data-stu-id="74ddc-179">A Spark streaming example application written in Scala, which receives events and route hello toodifferent destinations, is available at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span> <span data-ttu-id="74ddc-180">步驟 hello tooupdate hello 應用程式的事件中樞設定下，並建立 hello 輸出 jar。</span><span class="sxs-lookup"><span data-stu-id="74ddc-180">Follow hello steps below tooupdate hello application for your Event Hub configuration and create hello output jar.</span></span>

1. <span data-ttu-id="74ddc-181">啟動 IntelliJ 概念，並從 hello 啟動螢幕選取**版本控制中簽出**，然後按一下 **Git**。</span><span class="sxs-lookup"><span data-stu-id="74ddc-181">Launch IntelliJ IDEA and from hello launch screen select **Check out from Version Control** and then click **Git**.</span></span>
   
    <span data-ttu-id="74ddc-182">![Apache Spark 串流範例 - 從 Git 取得來源](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark 串流範例 - 從 Git 取得來源")</span><span class="sxs-lookup"><span data-stu-id="74ddc-182">![Apache Spark streaming example - get sources from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark streaming example - get sources from Git")</span></span>

2. <span data-ttu-id="74ddc-183">在 hello**複製儲存機制**對話方塊中，提供 hello URL toohello Git 儲存機制 tooclone 從、 指定 hello 目錄 tooclone、，然後按一下**複製**。</span><span class="sxs-lookup"><span data-stu-id="74ddc-183">In hello **Clone Repository** dialog box, provide hello URL toohello Git repository tooclone from, specify hello directory tooclone to, and then click **Clone**.</span></span>
   
    <span data-ttu-id="74ddc-184">![Apache Spark 串流範例 - 從 Git 複製](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark 串流範例 - 從 Git 複製")</span><span class="sxs-lookup"><span data-stu-id="74ddc-184">![Apache Spark streaming example - clone from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark streaming example - clone from Git")</span></span>
3. <span data-ttu-id="74ddc-185">直到 hello 專案完全被複製，請依照 hello 提示。</span><span class="sxs-lookup"><span data-stu-id="74ddc-185">Follow hello prompts till hello project is completely cloned.</span></span> <span data-ttu-id="74ddc-186">按**Alt + 1** tooopen hello**專案檢視**。</span><span class="sxs-lookup"><span data-stu-id="74ddc-186">Press **Alt + 1** tooopen hello **Project View**.</span></span> <span data-ttu-id="74ddc-187">它應該類似下列 hello。</span><span class="sxs-lookup"><span data-stu-id="74ddc-187">It should resemble hello following.</span></span>
   
    <span data-ttu-id="74ddc-188">![Apache Spark 串流範例 - 專案檢視](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark 串流範例 - 專案檢視")</span><span class="sxs-lookup"><span data-stu-id="74ddc-188">![Apache Spark streaming example - Project View](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark streaming example - Project View")</span></span>
4. <span data-ttu-id="74ddc-189">請確定 hello 應用程式程式碼會使用 Java8 編譯。</span><span class="sxs-lookup"><span data-stu-id="74ddc-189">Make sure hello application code is compiled with Java8.</span></span> <span data-ttu-id="74ddc-190">tooensure 此，依序按一下**檔案**，按一下 **專案結構**，在 hello**專案**索引標籤上，請確定專案語言層級設定得**8-Lambda，類型註解等**。</span><span class="sxs-lookup"><span data-stu-id="74ddc-190">tooensure this, click **File**, click **Project Structure**, and on hello **Project** tab, make sure Project language level is set too**8 - Lambdas, type annotations, etc.**.</span></span>
   
    <span data-ttu-id="74ddc-191">![Apache Spark 串流範例 - 設定編譯器](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark 串流範例 - 設定編譯器")</span><span class="sxs-lookup"><span data-stu-id="74ddc-191">![Apache Spark streaming example - Set compiler](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark streaming example - Set compiler")</span></span>
5. <span data-ttu-id="74ddc-192">開啟 hello **pom.xml** ，並確定 hello Spark 版本是否正確。</span><span class="sxs-lookup"><span data-stu-id="74ddc-192">Open hello **pom.xml** and make sure hello Spark version is correct.</span></span> <span data-ttu-id="74ddc-193">在下`<properties>`節點中，尋找下列程式碼片段的 hello 和驗證 hello Spark 版本。</span><span class="sxs-lookup"><span data-stu-id="74ddc-193">Under `<properties>` node, look for hello following snippet and verify hello Spark version.</span></span>

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. <span data-ttu-id="74ddc-194">hello 應用程式需要呼叫的相依性 jar **JDBC 驅動程式 jar**。</span><span class="sxs-lookup"><span data-stu-id="74ddc-194">hello application requires a dependency jar called **JDBC driver jar**.</span></span> <span data-ttu-id="74ddc-195">這是必要的 toowrite hello 訊息，從事件中心會接收到 Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="74ddc-195">This is required toowrite hello messages received from Event Hub into an Azure SQL database.</span></span> <span data-ttu-id="74ddc-196">您可以從[這裡](https://msdn.microsoft.com/sqlserver/aa937724.aspx)下載此 jar (4.1 或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="74ddc-196">You can download this jar (v4.1 or later) from [here](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span></span> <span data-ttu-id="74ddc-197">新增參考 toothis jar hello 專案文件庫中。</span><span class="sxs-lookup"><span data-stu-id="74ddc-197">Add reference toothis jar in hello project library.</span></span> <span data-ttu-id="74ddc-198">執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="74ddc-198">Perform hello following steps:</span></span>
     
     1. <span data-ttu-id="74ddc-199">從 IntelliJ 概念您尚未開啟 hello 應用程式 視窗中，按一下 **檔案**，按一下 **專案結構**，然後按一下**文件庫**。</span><span class="sxs-lookup"><span data-stu-id="74ddc-199">From IntelliJ IDEA window where you have hello application open, click **File**, click **Project Structure**, and then click **Libraries**.</span></span> 
     2. <span data-ttu-id="74ddc-200">按一下 hello 加入圖示 (![加入圖示](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png))，按一下  **Java**，然後瀏覽您下載 hello JDBC 驅動程式 jar 的 toohello 位置。</span><span class="sxs-lookup"><span data-stu-id="74ddc-200">Click hello add icon (![add icon](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), click **Java**, and then navigate toohello location where you downloaded hello JDBC driver jar.</span></span> <span data-ttu-id="74ddc-201">請遵循 hello 提示 tooadd hello jar 檔案 toohello 專案程式庫。</span><span class="sxs-lookup"><span data-stu-id="74ddc-201">Follow hello prompts tooadd hello jar file toohello project library.</span></span>

         <span data-ttu-id="74ddc-202">![新增遺失的相依性](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "新增遺失的相依性 jar")</span><span class="sxs-lookup"><span data-stu-id="74ddc-202">![add missing dependencies](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Add missing dependency jars")</span></span>
     3. <span data-ttu-id="74ddc-203">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="74ddc-203">Click **Apply**.</span></span>

7. <span data-ttu-id="74ddc-204">建立 hello 輸出 jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="74ddc-204">Create hello output jar file.</span></span> <span data-ttu-id="74ddc-205">執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="74ddc-205">Perform hello following steps.</span></span>

   1. <span data-ttu-id="74ddc-206">在 hello**專案結構**對話方塊中，按一下 **成品**hello 加上符號，然後按一下。</span><span class="sxs-lookup"><span data-stu-id="74ddc-206">In hello **Project Structure** dialog box, click **Artifacts** and then click hello plus symbol.</span></span> <span data-ttu-id="74ddc-207">Hello 快顯對話方塊方塊中，按一下  **JAR**，然後按一下**具有相依性的模組從**。</span><span class="sxs-lookup"><span data-stu-id="74ddc-207">From hello pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>      
       
       <span data-ttu-id="74ddc-208">![Apache Spark 串流範例 - 建立 jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark 串流範例 - 建立 jar")</span><span class="sxs-lookup"><span data-stu-id="74ddc-208">![Apache Spark streaming example - create JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark streaming example - create JAR")</span></span>
   2. <span data-ttu-id="74ddc-209">在 hello**從模組建立 JAR**對話方塊方塊中，按一下 hello 省略符號 (![省略](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) 針對 hello**主要類別**。</span><span class="sxs-lookup"><span data-stu-id="74ddc-209">In hello **Create JAR from Modules** dialog box, click hello ellipsis (![ellipsis](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) against hello **Main Class**.</span></span>
   3. <span data-ttu-id="74ddc-210">在 hello**選取主要類別**對話方塊方塊中，選取任何 hello 可用的類別，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="74ddc-210">In hello **Select Main Class** dialog box, select any of hello available classes and then click **OK**.</span></span>
      
       <span data-ttu-id="74ddc-211">![Apache Spark 串流範例 - 選取 jar 的類別](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark 串流範例 - 選取 jar 的類別")</span><span class="sxs-lookup"><span data-stu-id="74ddc-211">![Apache Spark streaming example - select class for jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark streaming example - select class for jar")</span></span>
   4. <span data-ttu-id="74ddc-212">在 hello**從模組建立 JAR**對話方塊方塊中，請確定該 hello 選項太**擷取 toohello 目標 JAR**已選取，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="74ddc-212">In hello **Create JAR from Modules** dialog box, make sure that hello option too**extract toohello target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="74ddc-213">這會建立具有所有相依性的單一 JAR。</span><span class="sxs-lookup"><span data-stu-id="74ddc-213">This creates a single JAR with all dependencies.</span></span>
      
       <span data-ttu-id="74ddc-214">![Apache Spark 串流範例 - 從模組建立 jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark 串流範例 - 從模組建立 jar")</span><span class="sxs-lookup"><span data-stu-id="74ddc-214">![Apache Spark streaming example - create jar from modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark streaming example - create jar from modules")</span></span>
   5. <span data-ttu-id="74ddc-215">hello**輸出配置**索引標籤會列出所有 hello （每瓶） 的 hello Maven 專案的一部分。</span><span class="sxs-lookup"><span data-stu-id="74ddc-215">hello **Output Layout** tab lists all hello jars that are included as part of hello Maven project.</span></span> <span data-ttu-id="74ddc-216">您可以選取和刪除 hello 所在的 hello Scala 應用程式並沒有直接相依。</span><span class="sxs-lookup"><span data-stu-id="74ddc-216">You can select and delete hello ones on which hello Scala application has no direct dependency.</span></span> <span data-ttu-id="74ddc-217">對於此建立 hello 應用程式，您可以移除以外的所有 hello 最後一個 (**spark-串流處理的資料-持續性-範例編譯輸出**)。</span><span class="sxs-lookup"><span data-stu-id="74ddc-217">For hello application we are creating here, you can remove all but hello last one (**spark-streaming-data-persistence-examples compile output**).</span></span> <span data-ttu-id="74ddc-218">選取 hello （每瓶) toodelete，然後按一下hello**刪除**圖示 (![刪除圖示](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png))。</span><span class="sxs-lookup"><span data-stu-id="74ddc-218">Select hello jars toodelete and then click hello **Delete** icon (![delete icon](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span></span>
      
       <span data-ttu-id="74ddc-219">![Apache Spark 串流範例 - 將擷取的 jar 刪除](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark 串流範例 - 將擷取的 jar 刪除")</span><span class="sxs-lookup"><span data-stu-id="74ddc-219">![Apache Spark streaming example - delete extracted jars](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark streaming example - delete extracted jars")</span></span>
      
       <span data-ttu-id="74ddc-220">請確定**上進行建置**選取方塊，以確保每次建立或更新 hello 專案建立該 hello jar。</span><span class="sxs-lookup"><span data-stu-id="74ddc-220">Make sure **Build on make** box is selected, which ensures that hello jar is created every time hello project is built or updated.</span></span> <span data-ttu-id="74ddc-221">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="74ddc-221">Click **Apply**.</span></span>
   6. <span data-ttu-id="74ddc-222">在 [hello**輸出版面配置**索引標籤上，直接在 hello 底部 hello**可用的項目**] 方塊中，您擁有 hello SQL JDBC jar 您加入先前 toohello 專案程式庫。</span><span class="sxs-lookup"><span data-stu-id="74ddc-222">In hello **Output Layout** tab, right at hello bottom of hello **Available Elements** box, you have hello SQL JDBC jar that you added earlier toohello project library.</span></span> <span data-ttu-id="74ddc-223">您必須新增此 toohello**輸出配置** 索引標籤。Hello jar 檔案，以滑鼠右鍵按一下，然後按一下**擷取到輸出根**。</span><span class="sxs-lookup"><span data-stu-id="74ddc-223">You must add this toohello **Output Layout** tab. Right-click hello jar file, and then click **Extract Into Output Root**.</span></span>
      
       <span data-ttu-id="74ddc-224">![Apache Spark 串流範例 - 擷取相依性 jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark 串流範例 - 擷取相依性 jar")</span><span class="sxs-lookup"><span data-stu-id="74ddc-224">![Apache Spark streaming example - extract dependency jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark streaming example - extract dependency jar")</span></span>  
      
       <span data-ttu-id="74ddc-225">hello**輸出配置** 索引標籤現在看起來應該像這樣。</span><span class="sxs-lookup"><span data-stu-id="74ddc-225">hello **Output Layout** tab should now look like this.</span></span>
      
       <span data-ttu-id="74ddc-226">![Apache Spark 串流範例 - 最終輸出索引標籤](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark 串流範例 - 最終輸出索引標籤")</span><span class="sxs-lookup"><span data-stu-id="74ddc-226">![Apache Spark streaming example - final output tab](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark streaming example - final output tab")</span></span>        
      
       <span data-ttu-id="74ddc-227">在 hello**專案結構**對話方塊中，按一下 **套用**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="74ddc-227">In hello **Project Structure** dialog box, click **Apply** and then click **OK**.</span></span>    
   7. <span data-ttu-id="74ddc-228">在 hello 功能表列中，按一下**建置**，然後按一下**進行專案**。</span><span class="sxs-lookup"><span data-stu-id="74ddc-228">From hello menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="74ddc-229">您也可以按一下**組建成品**toocreate hello jar。</span><span class="sxs-lookup"><span data-stu-id="74ddc-229">You can also click **Build Artifacts** toocreate hello jar.</span></span> <span data-ttu-id="74ddc-230">hello 輸出 jar 下方會建立**\classes\artifacts**。</span><span class="sxs-lookup"><span data-stu-id="74ddc-230">hello output jar is created under **\classes\artifacts**.</span></span>
      
       <span data-ttu-id="74ddc-231">![Apache Spark 串流範例 - 輸出 jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark 串流範例 - 輸出 jar")</span><span class="sxs-lookup"><span data-stu-id="74ddc-231">![Apache Spark streaming example - output JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark streaming example - output JAR")</span></span>

## <a name="run-hello-application-remotely-on-a-spark-cluster-using-livy"></a><span data-ttu-id="74ddc-232">使用晚總的 Spark 叢集上的遠端執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="74ddc-232">Run hello application remotely on a Spark cluster using Livy</span></span>

<span data-ttu-id="74ddc-233">在本文中您使用晚總 toorun hello Apache Spark 串流應用程式從遠端的 Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="74ddc-233">In this article you use Livy toorun hello Apache Spark streaming application remotely on a Spark cluster.</span></span> <span data-ttu-id="74ddc-234">如需如何 toouse 晚總與 HDInsight Spark 叢集的詳細討論，請參閱[送出工作遠端 tooan Apache Spark 叢集 Azure HDInsight 上](hdinsight-apache-spark-livy-rest-interface.md)。</span><span class="sxs-lookup"><span data-stu-id="74ddc-234">For detailed discussion on how toouse Livy with HDInsight Spark cluster, see [Submit jobs remotely tooan Apache Spark cluster on Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span> <span data-ttu-id="74ddc-235">您可以開始執行 hello Spark 串流應用程式之前，有幾件事您應該執行：</span><span class="sxs-lookup"><span data-stu-id="74ddc-235">Before you can start running hello Spark streaming application, there are a couple of things you should do:</span></span>

1. <span data-ttu-id="74ddc-236">啟動 hello 本機的獨立應用程式 toogenerate 事件，並傳送 tooEvent 中樞。</span><span class="sxs-lookup"><span data-stu-id="74ddc-236">Start hello local standalone application toogenerate events and sent tooEvent Hub.</span></span> <span data-ttu-id="74ddc-237">使用下列命令 toodo 因此 hello:</span><span class="sxs-lookup"><span data-stu-id="74ddc-237">Use hello following command toodo so:</span></span>

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. <span data-ttu-id="74ddc-238">資料流 jar 複製 hello (**spark-串流處理的資料-持續性-examples.jar**) toohello hello 叢集相關聯的 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="74ddc-238">Copy hello streaming jar (**spark-streaming-data-persistence-examples.jar**) toohello Azure Blob storage associated with hello cluster.</span></span> <span data-ttu-id="74ddc-239">這可讓 hello jar 存取 tooLivy。</span><span class="sxs-lookup"><span data-stu-id="74ddc-239">This makes hello jar accessible tooLivy.</span></span> <span data-ttu-id="74ddc-240">您可以使用[ **AzCopy**](../storage/common/storage-use-azcopy.md)，命令列公用程式，toodo 因此。</span><span class="sxs-lookup"><span data-stu-id="74ddc-240">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, toodo so.</span></span> <span data-ttu-id="74ddc-241">有許多的其他用戶端中，您可以使用 tooupload 資料。</span><span class="sxs-lookup"><span data-stu-id="74ddc-241">There are a lot of other clients you can use tooupload data.</span></span> <span data-ttu-id="74ddc-242">您可以在 [在 HDInsight 上將 Hadoop 作業的資料上傳](hdinsight-upload-data.md)中找到其詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="74ddc-242">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
3. <span data-ttu-id="74ddc-243">安裝 CURL hello 執行這些應用程式所在的電腦上。</span><span class="sxs-lookup"><span data-stu-id="74ddc-243">Install CURL on hello computer where you are running these applications from.</span></span> <span data-ttu-id="74ddc-244">我們使用 CURL tooinvoke hello 晚總端點 toorun hello 遠端作業。</span><span class="sxs-lookup"><span data-stu-id="74ddc-244">We use CURL tooinvoke hello Livy endpoints toorun hello jobs remotely.</span></span>

### <a name="run-hello-spark-streaming-application-tooreceive-hello-events-into-an-azure-storage-blob-as-text"></a><span data-ttu-id="74ddc-245">執行 hello Spark 串流應用程式 tooreceive hello 事件至 Azure 儲存體 Blob 做為文字</span><span class="sxs-lookup"><span data-stu-id="74ddc-245">Run hello Spark streaming application tooreceive hello events into an Azure Storage Blob as text</span></span>

<span data-ttu-id="74ddc-246">開啟命令提示字元，巡覽 toohello 目錄 CURL，安裝並執行下列命令 （取代使用者名稱/密碼與叢集名稱） 的 hello:</span><span class="sxs-lookup"><span data-stu-id="74ddc-246">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="74ddc-247">hello hello 檔案中的參數**inputBlob.txt**的定義方式如下：</span><span class="sxs-lookup"><span data-stu-id="74ddc-247">hello parameters in hello file **inputBlob.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="74ddc-248">讓我們了解 hello 輸入檔中的 hello 參數為何：</span><span class="sxs-lookup"><span data-stu-id="74ddc-248">Let us understand what hello parameters in hello input file are:</span></span>

* <span data-ttu-id="74ddc-249">**檔案**是 hello 路徑 toohello 應用程式 jar 檔 hello 與 hello 叢集相關聯的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="74ddc-249">**file** is hello path toohello application jar file on hello Azure storage account associated with hello cluster.</span></span>
* <span data-ttu-id="74ddc-250">**className**是 hello hello jar 中的 hello 類別名稱。</span><span class="sxs-lookup"><span data-stu-id="74ddc-250">**className** is hello name of hello class in hello jar.</span></span>
* <span data-ttu-id="74ddc-251">**引數**是 hello hello 類別所需的引數清單</span><span class="sxs-lookup"><span data-stu-id="74ddc-251">**args** is hello list of arguments required by hello class</span></span>
* <span data-ttu-id="74ddc-252">**numExecutors**是 hello Spark toorun hello 串流處理應用程式所使用的核心數目。</span><span class="sxs-lookup"><span data-stu-id="74ddc-252">**numExecutors** is hello number of cores used by Spark toorun hello streaming application.</span></span> <span data-ttu-id="74ddc-253">這應該一律至少兩次 hello 事件中樞分割區數目。</span><span class="sxs-lookup"><span data-stu-id="74ddc-253">This should always be at least twice hello number of Event Hub partitions.</span></span>
* <span data-ttu-id="74ddc-254">**executorMemory**， **executorCores**， **driverMemory** toohello 串流應用程式是用參數 tooassign 必要資源。</span><span class="sxs-lookup"><span data-stu-id="74ddc-254">**executorMemory**, **executorCores**, **driverMemory** are parameters used tooassign required resources toohello streaming application.</span></span>

> [!NOTE]
> <span data-ttu-id="74ddc-255">您不需要 toocreate hello 輸出資料夾 （EventCheckpoint、 EventCount/EventCount10） 做為參數。</span><span class="sxs-lookup"><span data-stu-id="74ddc-255">You do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="74ddc-256">hello 串流處理應用程式會為您建立它們。</span><span class="sxs-lookup"><span data-stu-id="74ddc-256">hello streaming application creates them for you.</span></span>
>
>

<span data-ttu-id="74ddc-257">當您執行 hello 命令時，您應該會看到類似 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="74ddc-257">When you run hello command, you should see an output like hello following:</span></span>

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact

<span data-ttu-id="74ddc-258">記下的 hello 批次識別碼 hello 的 hello 輸出 （在此範例中，它是 '1'） 的最後一行。</span><span class="sxs-lookup"><span data-stu-id="74ddc-258">Make a note of hello batch ID in hello last line of hello output (in this example it is '1').</span></span> <span data-ttu-id="74ddc-259">hello 應用程式的 tooverify 順利執行，您可以查看您 hello 叢集相關聯的 Azure 儲存體帳戶和您應該會看見 hello **/EventCount/EventCount10**那里建立資料夾。</span><span class="sxs-lookup"><span data-stu-id="74ddc-259">tooverify that hello application runs successfully, you can look at your Azure storage account associated with hello cluster and you should see hello **/EventCount/EventCount10** folder created there.</span></span> <span data-ttu-id="74ddc-260">這個資料夾應該包含擷取的事件處理 hello 中的指定時間週期 hello 參數的 hello 數目的 blob**批次間隔-中-秒**。</span><span class="sxs-lookup"><span data-stu-id="74ddc-260">This folder should contain blobs that captures hello number of events processed within hello time period specified for hello parameter **batch-interval-in-seconds**.</span></span>

<span data-ttu-id="74ddc-261">hello Spark 串流應用程式會繼續 toorun，直到您將其清除。</span><span class="sxs-lookup"><span data-stu-id="74ddc-261">hello Spark streaming application will continue toorun until you kill it.</span></span> <span data-ttu-id="74ddc-262">因此，toodo，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="74ddc-262">toodo so, use hello following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-storage-blob-as-json"></a><span data-ttu-id="74ddc-263">執行 hello 應用程式 tooreceive hello 事件至 Azure 儲存體 Blob 為 JSON</span><span class="sxs-lookup"><span data-stu-id="74ddc-263">Run hello applications tooreceive hello events into an Azure Storage Blob as JSON</span></span>
<span data-ttu-id="74ddc-264">開啟命令提示字元，巡覽 toohello 目錄 CURL，安裝並執行下列命令 （取代使用者名稱/密碼與叢集名稱） 的 hello:</span><span class="sxs-lookup"><span data-stu-id="74ddc-264">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="74ddc-265">hello hello 檔案中的參數**inputJSON.txt**的定義方式如下：</span><span class="sxs-lookup"><span data-stu-id="74ddc-265">hello parameters in hello file **inputJSON.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="74ddc-266">您指定 hello 上一個步驟中的 hello 文字輸出的類似 toowhat 的 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="74ddc-266">hello parameters are similar toowhat you specified for hello text output, in hello previous step.</span></span> <span data-ttu-id="74ddc-267">同樣地，您不需要 toocreate hello 輸出資料夾 （EventCheckpoint、 EventCount/EventCount10） 做為參數。</span><span class="sxs-lookup"><span data-stu-id="74ddc-267">Again, you do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="74ddc-268">hello 串流處理應用程式會為您建立它們。</span><span class="sxs-lookup"><span data-stu-id="74ddc-268">hello streaming application creates them for you.</span></span>

 <span data-ttu-id="74ddc-269">後執行 hello 命令，您可以查看您 hello 叢集相關聯的 Azure 儲存體帳戶中，您應該會看見 hello **/EventStore10**那里建立資料夾。</span><span class="sxs-lookup"><span data-stu-id="74ddc-269">After you run hello command, you can look at your Azure storage account associated with hello cluster and you should see hello **/EventStore10** folder created there.</span></span> <span data-ttu-id="74ddc-270">開啟任何檔案前面加上**一部分-** ，您應該會看見 hello 事件處理是 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="74ddc-270">Open any file prefixed with **part-** and you should see hello events processed in a JSON format.</span></span>

### <a name="run-hello-applications-tooreceive-hello-events-into-a-hive-table"></a><span data-ttu-id="74ddc-271">遇到 hello 應用程式 tooreceive hello 事件的 Hive 資料表</span><span class="sxs-lookup"><span data-stu-id="74ddc-271">Run hello applications tooreceive hello events into a Hive table</span></span>
<span data-ttu-id="74ddc-272">toorun hello Spark 串流應用程式資料流的事件，加入 Hive 資料表您需要一些額外的元件。</span><span class="sxs-lookup"><span data-stu-id="74ddc-272">toorun hello Spark streaming application that streams events into a Hive table you need some additional components.</span></span> <span data-ttu-id="74ddc-273">它們是：</span><span class="sxs-lookup"><span data-stu-id="74ddc-273">These are:</span></span>

* <span data-ttu-id="74ddc-274">datanucleus-api-jdo-3.2.6.jar</span><span class="sxs-lookup"><span data-stu-id="74ddc-274">datanucleus-api-jdo-3.2.6.jar</span></span>
* <span data-ttu-id="74ddc-275">datanucleus-rdbms-3.2.9.jar</span><span class="sxs-lookup"><span data-stu-id="74ddc-275">datanucleus-rdbms-3.2.9.jar</span></span>
* <span data-ttu-id="74ddc-276">datanucleus-core-3.2.10.jar</span><span class="sxs-lookup"><span data-stu-id="74ddc-276">datanucleus-core-3.2.10.jar</span></span>
* <span data-ttu-id="74ddc-277">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="74ddc-277">hive-site.xml</span></span>

<span data-ttu-id="74ddc-278">hello **d**檔案位於您的 HDInsight Spark 叢集，在`/usr/hdp/current/spark-client/lib`。</span><span class="sxs-lookup"><span data-stu-id="74ddc-278">hello **.jar** files are available on your HDInsight Spark cluster at `/usr/hdp/current/spark-client/lib`.</span></span> <span data-ttu-id="74ddc-279">hello **hive-site.xml**位於`/usr/hdp/current/spark-client/conf`。</span><span class="sxs-lookup"><span data-stu-id="74ddc-279">hello **hive-site.xml** is available at `/usr/hdp/current/spark-client/conf`.</span></span>

<span data-ttu-id="74ddc-280">您可以使用[WinScp](http://winscp.net/eng/download.php) toocopy hello 叢集 tooyour 本機電腦從這些檔案。</span><span class="sxs-lookup"><span data-stu-id="74ddc-280">You can use [WinScp](http://winscp.net/eng/download.php) toocopy over these files from hello cluster tooyour local computer.</span></span> <span data-ttu-id="74ddc-281">然後，您可以使用工具 toocopy tooyour 儲存體帳戶的這些檔案與 hello 叢集相關聯。</span><span class="sxs-lookup"><span data-stu-id="74ddc-281">You can then use tools toocopy these files over tooyour storage account associated with hello cluster.</span></span> <span data-ttu-id="74ddc-282">如需有關如何 tooupload 檔案 toohello 儲存體帳戶的詳細資訊，請參閱[HDInsight 中的 Hadoop 工作的資料上傳](hdinsight-upload-data.md)。</span><span class="sxs-lookup"><span data-stu-id="74ddc-282">For more information on how tooupload files toohello storage account, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

<span data-ttu-id="74ddc-283">一旦您複製了 hello 檔案 tooyour Azure 儲存體帳戶，開啟命令提示字元，巡覽 toohello 目錄 CURL，安裝並執行下列命令 （取代使用者名稱/密碼與叢集名稱） 的 hello:</span><span class="sxs-lookup"><span data-stu-id="74ddc-283">Once you have copied over hello files tooyour Azure storage account, open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="74ddc-284">hello hello 檔案中的參數**inputHive.txt**的定義方式如下：</span><span class="sxs-lookup"><span data-stu-id="74ddc-284">hello parameters in hello file **inputHive.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="74ddc-285">您指定 hello 先前步驟中的 hello 文字輸出的類似 toowhat 的 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="74ddc-285">hello parameters are similar toowhat you specified for hello text output, in hello previous steps.</span></span> <span data-ttu-id="74ddc-286">同樣地，您不需要 toocreate hello 輸出資料夾 （EventCheckpoint、 EventCount/EventCount10） 或 hello 輸出做為參數的 Hive 資料表 (EventHiveTable10)。</span><span class="sxs-lookup"><span data-stu-id="74ddc-286">Again, you do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) or hello output Hive table (EventHiveTable10) that are used as parameters.</span></span> <span data-ttu-id="74ddc-287">hello 串流處理應用程式會為您建立它們。</span><span class="sxs-lookup"><span data-stu-id="74ddc-287">hello streaming application creates them for you.</span></span> <span data-ttu-id="74ddc-288">請注意該 hello **（每瓶)**和**檔案**選項包含路徑 toohello d 檔案和 hello hive-site.xml 複製過來 toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="74ddc-288">Note that hello **jars** and **files** option includes paths toohello .jar files and hello hive-site.xml that you copied over toohello storage account.</span></span>

<span data-ttu-id="74ddc-289">hello hive 資料表的 tooverify 已成功建立，您可以指定 SSH 成 hello 叢集和執行的 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="74ddc-289">tooverify that hello hive table was successfully created, you can SSH into hello cluster and run Hive queries.</span></span> <span data-ttu-id="74ddc-290">如需指示，請參閱 [利用 SSH 搭配使用 Hive 與 HDInsight 中的 Hadoop](hdinsight-hadoop-use-hive-ssh.md)。</span><span class="sxs-lookup"><span data-stu-id="74ddc-290">For instructions, see [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-ssh.md).</span></span> <span data-ttu-id="74ddc-291">當您使用 SSH 連線時，您可以執行下列命令 tooverify hello hello Hive 資料表， **EventHiveTable10**，會建立。</span><span class="sxs-lookup"><span data-stu-id="74ddc-291">Once you are connected using SSH, you can run hello following command tooverify that hello Hive table, **EventHiveTable10**, is created.</span></span>

    show tables;

<span data-ttu-id="74ddc-292">您應該會看到類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="74ddc-292">You should see an output similar toohello following:</span></span>

    OK
    eventhivetable10
    hivesampletable

<span data-ttu-id="74ddc-293">您也可以執行 SELECT 查詢 tooview hello hello 資料表內容。</span><span class="sxs-lookup"><span data-stu-id="74ddc-293">You can also run a SELECT query tooview hello contents of hello table.</span></span>

    SELECT * FROM eventhivetable10 LIMIT 10;

<span data-ttu-id="74ddc-294">您應該會看到類似 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="74ddc-294">You should see an output like hello following:</span></span>

    ZN90apUSQODDTx7n6Toh6jDbuPngqT4c
    sor2M7xsFwmaRW8W8NDwMneFNMrOVkW1
    o2HcsU735ejSi2bGEcbUSB4btCFmI1lW
    TLuibq4rbj0T9st9eEzIWJwNGtMWYoYS
    HKCpPlWFWAJILwR69MAq863nCWYzDEw6
    Mvx0GQOPYvPR7ezBEpIHYKTKiEhYammQ
    85dRppSBSbZgThLr1s0GMgKqynDUqudr
    5LAWkNqorLj3ZN9a2mfWr9rZqeXKN4pF
    ulf9wSFNjD7BZXCyunozecov9QpEIYmJ
    vWzM3nvOja8DhYcwn0n5eTfOItZ966pa
    Time taken: 4.434 seconds, Fetched: 10 row(s)


### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-sql-database-table"></a><span data-ttu-id="74ddc-295">執行 hello 應用程式到 Azure SQL 資料庫資料表 tooreceive hello 事件</span><span class="sxs-lookup"><span data-stu-id="74ddc-295">Run hello applications tooreceive hello events into an Azure SQL database table</span></span>
<span data-ttu-id="74ddc-296">執行此步驟之前，請先確定您已建立 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="74ddc-296">Before running this step, make sure you have an Azure SQL database created.</span></span> <span data-ttu-id="74ddc-297">如需指示，請參閱[快速建立 SQL 資料庫](../sql-database/sql-database-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="74ddc-297">For instructions, see [Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="74ddc-298">本章節 toocomplete，您需要資料庫名稱、 資料庫伺服器名稱，和 hello 資料庫系統管理員認證，做為參數的值。</span><span class="sxs-lookup"><span data-stu-id="74ddc-298">toocomplete this section, you need values for database name, database server name, and hello database administrator credentials as parameters.</span></span> <span data-ttu-id="74ddc-299">您雖然不需要 toocreate hello 資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="74ddc-299">You do not need toocreate hello database table though.</span></span> <span data-ttu-id="74ddc-300">hello Spark 串流應用程式會為您建立的。</span><span class="sxs-lookup"><span data-stu-id="74ddc-300">hello Spark streaming application creates that for you.</span></span>

<span data-ttu-id="74ddc-301">開啟命令提示字元，巡覽 toohello 目錄 CURL，安裝並執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="74ddc-301">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="74ddc-302">hello hello 檔案中的參數**inputSQL.txt**的定義方式如下：</span><span class="sxs-lookup"><span data-stu-id="74ddc-302">hello parameters in hello file **inputSQL.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="74ddc-303">hello 應用程式的 tooverify 順利執行，您可以連接使用 SQL Server Management Studio toohello Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="74ddc-303">tooverify that hello application runs successfully, you can connect toohello Azure SQL database using SQL Server Management Studio.</span></span> <span data-ttu-id="74ddc-304">如需指示，請參閱 toodo [tooSQL 資料庫連接使用 SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md)。</span><span class="sxs-lookup"><span data-stu-id="74ddc-304">For instructions on how toodo that, see [Connect tooSQL Database with SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span></span> <span data-ttu-id="74ddc-305">一旦您已連線的 toohello 資料庫，您可以瀏覽 toohello **EventContent** hello 串流處理應用程式所建立的資料表。</span><span class="sxs-lookup"><span data-stu-id="74ddc-305">Once you are connected toohello database, you can navigate toohello **EventContent** table that was created by hello streaming application.</span></span> <span data-ttu-id="74ddc-306">您可以從 hello 資料表執行快速的查詢 tooget hello 資料。</span><span class="sxs-lookup"><span data-stu-id="74ddc-306">You can run a quick query tooget hello data from hello table.</span></span> <span data-ttu-id="74ddc-307">執行下列查詢的 hello:</span><span class="sxs-lookup"><span data-stu-id="74ddc-307">Run hello following query:</span></span>

    SELECT * FROM EventCount

<span data-ttu-id="74ddc-308">您應該會看到類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="74ddc-308">You should see output similar toohello following:</span></span>

    00046b0f-2552-4980-9c3f-8bba5647c8ee
    000b7530-12f9-4081-8e19-90acd26f9c0c
    000bc521-9c1b-4a42-ab08-dc1893b83f3b
    00123a2a-e00d-496a-9104-108920955718
    0017c68f-7a4e-452d-97ad-5cb1fe5ba81b
    001KsmqL2gfu5ZcuQuTqTxQvVyGCqPp9
    001vIZgOStka4DXtud0e3tX7XbfMnZrN
    00220586-3e1a-4d2d-a89b-05c5892e541a
    0029e309-9e54-4e1b-84be-cd04e6fce5ec
    003333cf-874f-4045-9da3-9f98c2b4ea49
    0043c07e-8d73-420a-9af7-1fcb94575356
    004a11a9-0c2c-4bc0-a7d5-2e0ebd947ab9


## <span data-ttu-id="74ddc-309"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="74ddc-309"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="74ddc-310">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="74ddc-310">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)
* [<span data-ttu-id="74ddc-311">收件者型連線和 Direct DStream 的設計</span><span class="sxs-lookup"><span data-stu-id="74ddc-311">Design of Receiver-based Connection and Direct DStream</span></span>](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a><span data-ttu-id="74ddc-312">案例</span><span class="sxs-lookup"><span data-stu-id="74ddc-312">Scenarios</span></span>
* [<span data-ttu-id="74ddc-313">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="74ddc-313">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="74ddc-314">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="74ddc-314">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="74ddc-315">機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark</span><span class="sxs-lookup"><span data-stu-id="74ddc-315">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="74ddc-316">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="74ddc-316">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="74ddc-317">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="74ddc-317">Create and run applications</span></span>
* [<span data-ttu-id="74ddc-318">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="74ddc-318">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="74ddc-319">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="74ddc-319">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="74ddc-320">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="74ddc-320">Tools and extensions</span></span>
* [<span data-ttu-id="74ddc-321">HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 個應用程式</span><span class="sxs-lookup"><span data-stu-id="74ddc-321">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="74ddc-322">從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="74ddc-322">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="74ddc-323">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="74ddc-323">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="74ddc-324">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="74ddc-324">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="74ddc-325">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="74ddc-325">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="74ddc-326">在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="74ddc-326">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="74ddc-327">管理資源</span><span class="sxs-lookup"><span data-stu-id="74ddc-327">Manage resources</span></span>
* [<span data-ttu-id="74ddc-328">管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="74ddc-328">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="74ddc-329">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="74ddc-329">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
