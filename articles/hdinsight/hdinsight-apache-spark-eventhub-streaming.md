---
title: "透過 Azure HDInsight 中的事件中樞使用 Apache Spark 串流 | Microsoft Docs"
description: "建立 Apache Spark 串流範例，說明如何將資料串流傳送到 Azure 事件中樞，然後使用 Scala 應用程式在 HDInsight Spark 叢集中接收這些事件。"
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
ms.openlocfilehash: 175a2ad70b1f554d05846eb62fb685d4f259af7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="4dc45-104">Apache Spark 串流：在 HDInsight 上使用 Spark 叢集處理來自 Azure 事件中樞的資料</span><span class="sxs-lookup"><span data-stu-id="4dc45-104">Apache Spark streaming: Process data from Azure Event Hubs with Spark cluster on HDInsight</span></span>

<span data-ttu-id="4dc45-105">在本文中，您可以建立 Apache Spark 串流範例，包含下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="4dc45-105">In this article, you create an Apache Spark streaming sample that involves the following steps:</span></span>

1. <span data-ttu-id="4dc45-106">您可以使用獨立的應用程式，將訊息內嵌到 Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="4dc45-106">You use a standalone application to ingest messages into an Azure Event Hub.</span></span>

2. <span data-ttu-id="4dc45-107">透過兩種不同的方法，您可以使用 Azure HDInsight 上 Spark 叢集中執行的應用程式，即時擷取 [事件中樞] 中的訊息。</span><span class="sxs-lookup"><span data-stu-id="4dc45-107">With two different approaches, you retrieve the messages from Event Hub in real-time using an application running in Spark cluster on Azure HDInsight.</span></span>

3. <span data-ttu-id="4dc45-108">您可以建置串流分析管線，將資料保存至不同的儲存系統，或從即時資料中取得見解。</span><span class="sxs-lookup"><span data-stu-id="4dc45-108">You build streaming analytic pipelines to persist data to different storage systems, or get insights from data on the fly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4dc45-109">先決條件</span><span class="sxs-lookup"><span data-stu-id="4dc45-109">Prerequisites</span></span>

* <span data-ttu-id="4dc45-110">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4dc45-110">An Azure subscription.</span></span> <span data-ttu-id="4dc45-111">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="4dc45-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="4dc45-112">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="4dc45-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="4dc45-113">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="4dc45-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="spark-streaming-concepts"></a><span data-ttu-id="4dc45-114">Spark 串流處理概念</span><span class="sxs-lookup"><span data-stu-id="4dc45-114">Spark Streaming concepts</span></span>

<span data-ttu-id="4dc45-115">如需 Spark 串流的詳細說明，請參閱 [Apache Spark 串流概觀](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview)。</span><span class="sxs-lookup"><span data-stu-id="4dc45-115">For a detailed explanation of Spark streaming, see [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span></span> <span data-ttu-id="4dc45-116">HDInsight 會將相同的串流功能帶入 Azure 上的 Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="4dc45-116">HDInsight brings the same streaming features to a Spark cluster on Azure.</span></span>  

## <a name="what-does-this-solution-do"></a><span data-ttu-id="4dc45-117">此解決方案有哪些功能？</span><span class="sxs-lookup"><span data-stu-id="4dc45-117">What does this solution do?</span></span>

<span data-ttu-id="4dc45-118">在本文中，若要建立 Spark 串流範例，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4dc45-118">In this article, to create a Spark streaming example, perform the following steps:</span></span>

1. <span data-ttu-id="4dc45-119">建立會接收事件串流的 Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="4dc45-119">Create an Azure Event Hub that will receive a stream of events.</span></span>

2. <span data-ttu-id="4dc45-120">執行會產生事件，並將其推送至 Azure 事件中樞的本機獨立應用程式。</span><span class="sxs-lookup"><span data-stu-id="4dc45-120">Run a local standalone application that generates events and pushes it to the Azure Event Hub.</span></span> <span data-ttu-id="4dc45-121">會執行此作業的範例應用程式發佈於： [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples)。</span><span class="sxs-lookup"><span data-stu-id="4dc45-121">The sample application that does this is published at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span>

3. <span data-ttu-id="4dc45-122">在 Spark 叢集上遠端執行串流應用程式，該應用程式可從 Azure 事件中樞讀取串流事件，並執行各種資料處理/分析。</span><span class="sxs-lookup"><span data-stu-id="4dc45-122">Run a streaming application remotely on a Spark cluster that reads streaming events from Azure Event Hub and perform various data processing/analysis.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="4dc45-123">建立 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="4dc45-123">Create an Azure Event Hub</span></span>

1. <span data-ttu-id="4dc45-124">登入 [Azure 入口網站](https://ms.portal.azure.com)，然後按一下畫面左上方的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4dc45-124">Log on to the [Azure Portal](https://ms.portal.azure.com), and click **New** at the top left of the screen.</span></span>

2. <span data-ttu-id="4dc45-125">按一下 [物聯網]，然後按一下 [事件中樞]。</span><span class="sxs-lookup"><span data-stu-id="4dc45-125">Click **Internet of Things**, then click **Event Hubs**.</span></span>

    <span data-ttu-id="4dc45-126">![建立 Spark 串流範例的事件中樞](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "建立 Spark 串流範例的事件中樞")</span><span class="sxs-lookup"><span data-stu-id="4dc45-126">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span></span>

3. <span data-ttu-id="4dc45-127">在 [建立命名空間]  刀鋒視窗中，輸入命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="4dc45-127">In the **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="4dc45-128">選擇定價層 (基本或標準)。</span><span class="sxs-lookup"><span data-stu-id="4dc45-128">choose the pricing tier (Basic or Standard).</span></span> <span data-ttu-id="4dc45-129">此外，選擇要在其中建立資源的 Azure 訂用帳戶、資源群組和位置。</span><span class="sxs-lookup"><span data-stu-id="4dc45-129">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span></span> <span data-ttu-id="4dc45-130">按一下 [建立]  來建立命名空間。</span><span class="sxs-lookup"><span data-stu-id="4dc45-130">Click **Create** to create the namespace.</span></span>

      <span data-ttu-id="4dc45-131">![提供 Spark 串流範例的事件中樞名稱](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "提供 Spark 串流範例的事件中樞名稱")</span><span class="sxs-lookup"><span data-stu-id="4dc45-131">![Provide an event hub name for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span></span>

    > [!NOTE]
    > <span data-ttu-id="4dc45-132">您應該選取與 HDInsight 中 Apache Spark 叢集相同的 **位置** ，以便降低延遲的情況和成本。</span><span class="sxs-lookup"><span data-stu-id="4dc45-132">You should select the same **Location** as your Apache Spark cluster in HDInsight to reduce latency and costs.</span></span>
    >
    >

4. <span data-ttu-id="4dc45-133">在事件中樞命名空間清單中，按一下新建立的命名空間。</span><span class="sxs-lookup"><span data-stu-id="4dc45-133">In the Event Hubs namespace list, click the newly-created namespace.</span></span>      


5. <span data-ttu-id="4dc45-134">在 [命名空間] 刀鋒視窗中，按一下 [事件中樞]，然後按一下 [+ 事件中樞] 來建立新的事件中樞。</span><span class="sxs-lookup"><span data-stu-id="4dc45-134">In the namespace blade, click **Event Hubs**, and then click **+ Event Hub** to create a new Event Hub.</span></span>
   
    <span data-ttu-id="4dc45-135">![建立 Spark 串流範例的事件中樞](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "建立 Spark 串流範例的事件中樞")</span><span class="sxs-lookup"><span data-stu-id="4dc45-135">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Create event hub for Spark streaming example")</span></span>

6. <span data-ttu-id="4dc45-136">輸入事件中樞的名稱、將分割區計數設為 10，並將訊息保留期設為 1。</span><span class="sxs-lookup"><span data-stu-id="4dc45-136">Type a name for your Event Hub, set the partition count to 10, and message retention to 1.</span></span> <span data-ttu-id="4dc45-137">我們並未在此解決方案中保存訊息，因此您可以讓其餘項目保留為預設值，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="4dc45-137">We are not archiving the messages in this solution so you can leave the rest as default, and then click **Create**.</span></span>
   
    <span data-ttu-id="4dc45-138">![提供 Spark 串流範例的事件中樞詳細資料](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "提供 Spark 串流範例的事件中樞詳細資料")</span><span class="sxs-lookup"><span data-stu-id="4dc45-138">![Provide event hub details for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span></span>

7. <span data-ttu-id="4dc45-139">新建立的事件中樞會列在 [事件中樞] 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="4dc45-139">The newly created Event Hub is listed in the Event Hub blade.</span></span>
    
     <span data-ttu-id="4dc45-140">![檢視 Spark 串流範例的事件中樞](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "檢視 Spark 串流範例的事件中樞")</span><span class="sxs-lookup"><span data-stu-id="4dc45-140">![View Event Hub for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "View Event Hub for the Spark streaming example")</span></span>

8. <span data-ttu-id="4dc45-141">回到命名空間刀鋒視窗 (而不是特定事件中樞刀鋒視窗)，按一下 [共用存取原則]，然後按一下 [RootManageSharedAccessKey]。</span><span class="sxs-lookup"><span data-stu-id="4dc45-141">Back in the namespace blade (not the specific Event Hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
     <span data-ttu-id="4dc45-142">![設定 Spark 串流範例的事件中樞原則](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "設定 Spark 串流範例的事件中樞原則")</span><span class="sxs-lookup"><span data-stu-id="4dc45-142">![Set Event Hub policies for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Set Event Hub policies for the Spark streaming example")</span></span>

9. <span data-ttu-id="4dc45-143">按一下複製按鈕，將 **RootManageSharedAccessKey** 主要金鑰和連接字串複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="4dc45-143">Click the copy button to copy the **RootManageSharedAccessKey** primary key and connection string to the clipboard.</span></span> <span data-ttu-id="4dc45-144">儲存這些項目，以便稍後在本教學課程中使用。</span><span class="sxs-lookup"><span data-stu-id="4dc45-144">Save these to use later in the tutorial.</span></span>
    
     <span data-ttu-id="4dc45-145">![檢視 Spark 串流範例的事件中樞原則金鑰](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "檢視 Spark 串流範例的事件中樞原則金鑰")</span><span class="sxs-lookup"><span data-stu-id="4dc45-145">![View Event Hub policy keys for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "View Event Hub policy keys for the Spark streaming example")</span></span>

## <a name="send-messages-to-azure-event-hub-using-a-sample-scala-application"></a><span data-ttu-id="4dc45-146">使用範例 Scala 應用程式將訊息傳送至 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="4dc45-146">Send messages to Azure Event Hub using a sample Scala application</span></span>

<span data-ttu-id="4dc45-147">在本節中，您會使用獨立的本機 Scala 應用程式來產生事件的串流，並將它傳送至您稍早所建立的 Azure 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="4dc45-147">In this section you use a standalone local Scala application that generates a stream of events and sends it to Azure Event Hub that you created earlier.</span></span> <span data-ttu-id="4dc45-148">此應用程式可從 GitHub 取得，網址是： [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer)。</span><span class="sxs-lookup"><span data-stu-id="4dc45-148">This application is available on GitHub at [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span></span> <span data-ttu-id="4dc45-149">以下步驟假設您已分接此 GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="4dc45-149">The steps here assume that you have already forked this GitHub repository.</span></span>

1. <span data-ttu-id="4dc45-150">請務必在您執行此應用程式的電腦上安裝下列項目。</span><span class="sxs-lookup"><span data-stu-id="4dc45-150">Make sure you have the following installed on the computer where you run this application.</span></span>

    * <span data-ttu-id="4dc45-151">Oracle Java Development Kit。</span><span class="sxs-lookup"><span data-stu-id="4dc45-151">Oracle Java Development kit.</span></span> <span data-ttu-id="4dc45-152">您可以從[這裡](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)安裝它。</span><span class="sxs-lookup"><span data-stu-id="4dc45-152">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
    * <span data-ttu-id="4dc45-153">Apache Maven。</span><span class="sxs-lookup"><span data-stu-id="4dc45-153">Apache Maven.</span></span> <span data-ttu-id="4dc45-154">您可以從 [這裡](https://maven.apache.org/download.cgi)下載。</span><span class="sxs-lookup"><span data-stu-id="4dc45-154">You can download it from [here](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="4dc45-155">您可以在[這裡](https://maven.apache.org/install.html)取得安裝 Maven 的指示。</span><span class="sxs-lookup"><span data-stu-id="4dc45-155">Instructions to install Maven are available [here](https://maven.apache.org/install.html).</span></span>

2. <span data-ttu-id="4dc45-156">開啟命令提示字元並瀏覽至您針對範例 Scala 應用程式複製 GitHub 存放庫的位置，並執行下列命令來建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="4dc45-156">Open a command prompt and navigate to the location you cloned the GitHub repo for the sample Scala application and run the following command to build the application.</span></span>

        mvn package

3. <span data-ttu-id="4dc45-157">應用程式的輸出 jar **com-microsoft-azure-eventhubs-client-example-0.2.0.jar** 會建立在 **/target** 目錄下。</span><span class="sxs-lookup"><span data-stu-id="4dc45-157">The output jar for the application, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, is created under **/target** directory.</span></span> <span data-ttu-id="4dc45-158">您稍後可以使用本文中的這個 JAR 來測試完整的解決方案。</span><span class="sxs-lookup"><span data-stu-id="4dc45-158">You use this JAR later in this article to test the complete solution.</span></span>

## <a name="create-application-to-receive-messages-from-event-hub-into-a-spark-cluster"></a><span data-ttu-id="4dc45-159">建立應用程式以接收事件中樞傳入 Spark 叢集的訊息</span><span class="sxs-lookup"><span data-stu-id="4dc45-159">Create application to receive messages from Event Hub into a Spark cluster</span></span> 

<span data-ttu-id="4dc45-160">我們有兩種方法來連接 Spark 串流和 Azure 事件中樞，分別是收件者型連線與 Direct-DStream 型連線。</span><span class="sxs-lookup"><span data-stu-id="4dc45-160">We have two approaches to connect Spark Streaming and Azure Event Hubs, Receiver-based connection and Direct-DStream-based connection.</span></span> <span data-ttu-id="4dc45-161">Direct-DStream 型在 2017 年 1 月引進，版本為 2.0.3。</span><span class="sxs-lookup"><span data-stu-id="4dc45-161">Direct-DStream-based is introduced on Jan of 2017, in the 2.0.3 release.</span></span> <span data-ttu-id="4dc45-162">它應該取代原始收件者型連線，因為它的效能更好且更節省資源。</span><span class="sxs-lookup"><span data-stu-id="4dc45-162">It is supposed to replace the original receiver-based connection as it is more performant and resource-efficient.</span></span> <span data-ttu-id="4dc45-163">如需更多詳細資料，請參閱 [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs)。</span><span class="sxs-lookup"><span data-stu-id="4dc45-163">More details found in [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span></span> <span data-ttu-id="4dc45-164">Direct DStream 只支援 Spark 2.0+。</span><span class="sxs-lookup"><span data-stu-id="4dc45-164">Direct DStream only supports Spark 2.0+.</span></span>

### <a name="build-applications-with-the-dependency-to-spark-eventhubs-connector"></a><span data-ttu-id="4dc45-165">建置具有 spark-eventhubs 連接器相依性的應用程式</span><span class="sxs-lookup"><span data-stu-id="4dc45-165">Build applications with the dependency to spark-eventhubs connector</span></span>

<span data-ttu-id="4dc45-166">我們也會在 GitHub 中發行臨時版本的 Spark-EventHubs。</span><span class="sxs-lookup"><span data-stu-id="4dc45-166">We will also publish the staging version of Spark-EventHubs in GitHub.</span></span> <span data-ttu-id="4dc45-167">若要使用臨時版本的 Spark-EventHubs，第一個步驟是透過在 pom.xml 加入下列項目，將 GitHub 指定為來源存放庫：</span><span class="sxs-lookup"><span data-stu-id="4dc45-167">To use the staging version of Spark-EventHubs, the first step is to indicate GitHub as the source repo by adding the following entry to pom.xml:</span></span>

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

<span data-ttu-id="4dc45-168">然後，您可以將下列相依性加入您的專案，以取得發行前版本。</span><span class="sxs-lookup"><span data-stu-id="4dc45-168">You can then add the following dependency to your project to take the pre-released version.</span></span>

<span data-ttu-id="4dc45-169">Maven 相依性</span><span class="sxs-lookup"><span data-stu-id="4dc45-169">Maven Dependency</span></span>

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

<span data-ttu-id="4dc45-170">SBT 相依性</span><span class="sxs-lookup"><span data-stu-id="4dc45-170">SBT Dependency</span></span>

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a><span data-ttu-id="4dc45-171">Direct DStream 連線</span><span class="sxs-lookup"><span data-stu-id="4dc45-171">Direct DStream Connection</span></span>

<span data-ttu-id="4dc45-172">包含使用 Direct DStream 範例的預先建立 jar 檔案可在 [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar) 中下載。</span><span class="sxs-lookup"><span data-stu-id="4dc45-172">A pre-built jar file containing examples using Direct DStream can be downloaded in [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span></span>

<span data-ttu-id="4dc45-173">Jar 檔案包含三個範例，其原始程式碼位於 [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream)。</span><span class="sxs-lookup"><span data-stu-id="4dc45-173">The jar file contains three examples whose source code are available at [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span></span>

<span data-ttu-id="4dc45-174">將 [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) 作為範例：</span><span class="sxs-lookup"><span data-stu-id="4dc45-174">Taking [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) as an example:</span></span>

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

<span data-ttu-id="4dc45-175">在上面的範例中，`eventhubParameters` 是單一 EventHubs 執行個體特有的參數，您必須將它傳遞給 `createDirectStreams` API，該 API 會建構對應至 Event Hubs 命名空間的 Direct DStream 物件。</span><span class="sxs-lookup"><span data-stu-id="4dc45-175">In the above example, `eventhubParameters` are the parameters specific to a single EventHubs instance and you have to pass it to the `createDirectStreams` API which constructs a Direct DStream object mapping to a Event Hubs namespace.</span></span> <span data-ttu-id="4dc45-176">透過 Direct DStream 物件，您可以呼叫由 Spark 串流 API 架構提供的任何 DStream API。</span><span class="sxs-lookup"><span data-stu-id="4dc45-176">Over the Direct DStream object, you can call any DStream API provided by Spark Streaming API framework.</span></span> <span data-ttu-id="4dc45-177">在此範例中，我們會計算最後 3 個微批次間隔內每個字的頻率。</span><span class="sxs-lookup"><span data-stu-id="4dc45-177">In this example, we calculate the frequency of each word within the last 3 micro batch intervals.</span></span>

### <a name="receiver-based-connection"></a><span data-ttu-id="4dc45-178">收件者型連線</span><span class="sxs-lookup"><span data-stu-id="4dc45-178">Receiver-based Connection</span></span>

<span data-ttu-id="4dc45-179">以 Scala 撰寫的 Spark 串流範例應用程式 (它會接收事件並路由傳送至不同的目的地) 可在下列位置取得：[https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples)。</span><span class="sxs-lookup"><span data-stu-id="4dc45-179">A Spark streaming example application written in Scala, which receives events and route the to different destinations, is available at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span> <span data-ttu-id="4dc45-180">請遵循下列步驟來更新事件中樞設定的應用程式，並建立輸出 jar。</span><span class="sxs-lookup"><span data-stu-id="4dc45-180">Follow the steps below to update the application for your Event Hub configuration and create the output jar.</span></span>

1. <span data-ttu-id="4dc45-181">啟動 IntelliJ IDEA，並在啟動畫面中選取 [從版本控制簽出]，然後按一下 [Git]。</span><span class="sxs-lookup"><span data-stu-id="4dc45-181">Launch IntelliJ IDEA and from the launch screen select **Check out from Version Control** and then click **Git**.</span></span>
   
    <span data-ttu-id="4dc45-182">![Apache Spark 串流範例 - 從 Git 取得來源](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark 串流範例 - 從 Git 取得來源")</span><span class="sxs-lookup"><span data-stu-id="4dc45-182">![Apache Spark streaming example - get sources from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark streaming example - get sources from Git")</span></span>

2. <span data-ttu-id="4dc45-183">在 [複製儲存機制] 對話方塊中，提供要從中複製之 Git 儲存機制的 URL、指定要複製到的目錄，然後按一下 [複製]。</span><span class="sxs-lookup"><span data-stu-id="4dc45-183">In the **Clone Repository** dialog box, provide the URL to the Git repository to clone from, specify the directory to clone to, and then click **Clone**.</span></span>
   
    <span data-ttu-id="4dc45-184">![Apache Spark 串流範例 - 從 Git 複製](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark 串流範例 - 從 Git 複製")</span><span class="sxs-lookup"><span data-stu-id="4dc45-184">![Apache Spark streaming example - clone from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark streaming example - clone from Git")</span></span>
3. <span data-ttu-id="4dc45-185">依照提示操作，直到專案複製完成。</span><span class="sxs-lookup"><span data-stu-id="4dc45-185">Follow the prompts till the project is completely cloned.</span></span> <span data-ttu-id="4dc45-186">按 **Alt + 1** 以開啟 [專案檢視]。</span><span class="sxs-lookup"><span data-stu-id="4dc45-186">Press **Alt + 1** to open the **Project View**.</span></span> <span data-ttu-id="4dc45-187">其內容應如下所示。</span><span class="sxs-lookup"><span data-stu-id="4dc45-187">It should resemble the following.</span></span>
   
    <span data-ttu-id="4dc45-188">![Apache Spark 串流範例 - 專案檢視](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark 串流範例 - 專案檢視")</span><span class="sxs-lookup"><span data-stu-id="4dc45-188">![Apache Spark streaming example - Project View](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark streaming example - Project View")</span></span>
4. <span data-ttu-id="4dc45-189">請確定以 Java8 編譯應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="4dc45-189">Make sure the application code is compiled with Java8.</span></span> <span data-ttu-id="4dc45-190">若要這樣做，請按一下 [檔案]，按一下 [專案結構]，然後在 [專案] 索引標籤上，確定 [專案語言層級] 設定為 [8 - Lambda、類型註解等]。</span><span class="sxs-lookup"><span data-stu-id="4dc45-190">To ensure this, click **File**, click **Project Structure**, and on the **Project** tab, make sure Project language level is set to **8 - Lambdas, type annotations, etc.**.</span></span>
   
    <span data-ttu-id="4dc45-191">![Apache Spark 串流範例 - 設定編譯器](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark 串流範例 - 設定編譯器")</span><span class="sxs-lookup"><span data-stu-id="4dc45-191">![Apache Spark streaming example - Set compiler](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark streaming example - Set compiler")</span></span>
5. <span data-ttu-id="4dc45-192">開啟 **pom.xml** ，並確定 Spark 版本是正確的。</span><span class="sxs-lookup"><span data-stu-id="4dc45-192">Open the **pom.xml** and make sure the Spark version is correct.</span></span> <span data-ttu-id="4dc45-193">在 `<properties>` 節點下尋找下列程式碼片段，並確認 Spark 版本。</span><span class="sxs-lookup"><span data-stu-id="4dc45-193">Under `<properties>` node, look for the following snippet and verify the Spark version.</span></span>

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. <span data-ttu-id="4dc45-194">應用程式需要稱為 **JDBC 驅動程式 jar** 的相依性 jar。</span><span class="sxs-lookup"><span data-stu-id="4dc45-194">The application requires a dependency jar called **JDBC driver jar**.</span></span> <span data-ttu-id="4dc45-195">必須要有此項目，才能將接收自事件中樞的訊息寫入至 Azure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4dc45-195">This is required to write the messages received from Event Hub into an Azure SQL database.</span></span> <span data-ttu-id="4dc45-196">您可以從[這裡](https://msdn.microsoft.com/sqlserver/aa937724.aspx)下載此 jar (4.1 或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="4dc45-196">You can download this jar (v4.1 or later) from [here](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span></span> <span data-ttu-id="4dc45-197">在專案程式庫中新增此 jar 的參考。</span><span class="sxs-lookup"><span data-stu-id="4dc45-197">Add reference to this jar in the project library.</span></span> <span data-ttu-id="4dc45-198">執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4dc45-198">Perform the following steps:</span></span>
     
     1. <span data-ttu-id="4dc45-199">在已開啟應用程式的 [IntelliJ IDEA] 視窗中，依序按一下 [檔案]、[專案結構] 和 [程式庫]。</span><span class="sxs-lookup"><span data-stu-id="4dc45-199">From IntelliJ IDEA window where you have the application open, click **File**, click **Project Structure**, and then click **Libraries**.</span></span> 
     2. <span data-ttu-id="4dc45-200">按一下 [新增] 圖示 (![新增圖示](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png))、按一下 [Java]，然後導覽至您下載 JDBC 驅動程式 jar 的位置。</span><span class="sxs-lookup"><span data-stu-id="4dc45-200">Click the add icon (![add icon](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), click **Java**, and then navigate to the location where you downloaded the JDBC driver jar.</span></span> <span data-ttu-id="4dc45-201">依照提示，將 jar 檔案新增至專案程式庫。</span><span class="sxs-lookup"><span data-stu-id="4dc45-201">Follow the prompts to add the jar file to the project library.</span></span>

         <span data-ttu-id="4dc45-202">![新增遺失的相依性](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "新增遺失的相依性 jar")</span><span class="sxs-lookup"><span data-stu-id="4dc45-202">![add missing dependencies](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Add missing dependency jars")</span></span>
     3. <span data-ttu-id="4dc45-203">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="4dc45-203">Click **Apply**.</span></span>

7. <span data-ttu-id="4dc45-204">建立輸出 jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="4dc45-204">Create the output jar file.</span></span> <span data-ttu-id="4dc45-205">請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4dc45-205">Perform the following steps.</span></span>

   1. <span data-ttu-id="4dc45-206">在 [專案結構] 對話方塊中，按一下 [構件]，然後按一下加號。</span><span class="sxs-lookup"><span data-stu-id="4dc45-206">In the **Project Structure** dialog box, click **Artifacts** and then click the plus symbol.</span></span> <span data-ttu-id="4dc45-207">在快顯對話方塊中按一下 [JAR]，然後按一下 [從具有相依性的模組]。</span><span class="sxs-lookup"><span data-stu-id="4dc45-207">From the pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>      
       
       <span data-ttu-id="4dc45-208">![Apache Spark 串流範例 - 建立 jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark 串流範例 - 建立 jar")</span><span class="sxs-lookup"><span data-stu-id="4dc45-208">![Apache Spark streaming example - create JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark streaming example - create JAR")</span></span>
   2. <span data-ttu-id="4dc45-209">在 [從模組建立 JAR] 對話方塊中，對 [主要類別] 按一下省略符號 (![ellipsis](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png))。</span><span class="sxs-lookup"><span data-stu-id="4dc45-209">In the **Create JAR from Modules** dialog box, click the ellipsis (![ellipsis](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) against the **Main Class**.</span></span>
   3. <span data-ttu-id="4dc45-210">在 [選取主要類別] 對話方塊中，選取任何可用的類別，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="4dc45-210">In the **Select Main Class** dialog box, select any of the available classes and then click **OK**.</span></span>
      
       <span data-ttu-id="4dc45-211">![Apache Spark 串流範例 - 選取 jar 的類別](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark 串流範例 - 選取 jar 的類別")</span><span class="sxs-lookup"><span data-stu-id="4dc45-211">![Apache Spark streaming example - select class for jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark streaming example - select class for jar")</span></span>
   4. <span data-ttu-id="4dc45-212">在 [從模組建立 JAR] 對話方塊中，確定已選取 [擷取至目標 JAR]選項，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="4dc45-212">In the **Create JAR from Modules** dialog box, make sure that the option to **extract to the target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="4dc45-213">這會建立具有所有相依性的單一 JAR。</span><span class="sxs-lookup"><span data-stu-id="4dc45-213">This creates a single JAR with all dependencies.</span></span>
      
       <span data-ttu-id="4dc45-214">![Apache Spark 串流範例 - 從模組建立 jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark 串流範例 - 從模組建立 jar")</span><span class="sxs-lookup"><span data-stu-id="4dc45-214">![Apache Spark streaming example - create jar from modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark streaming example - create jar from modules")</span></span>
   5. <span data-ttu-id="4dc45-215">[輸出配置] 索引標籤會列出所有納入 Maven 專案中的 jar。</span><span class="sxs-lookup"><span data-stu-id="4dc45-215">The **Output Layout** tab lists all the jars that are included as part of the Maven project.</span></span> <span data-ttu-id="4dc45-216">您可以選取並刪除 Scala 應用程式未直接依存的 jar。</span><span class="sxs-lookup"><span data-stu-id="4dc45-216">You can select and delete the ones on which the Scala application has no direct dependency.</span></span> <span data-ttu-id="4dc45-217">對於我們在這裡建立的應用程式，您可以移除最後一個 jar (**spark-streaming-data-persistence-examples 編譯輸出**) 以外的所有 jar。</span><span class="sxs-lookup"><span data-stu-id="4dc45-217">For the application we are creating here, you can remove all but the last one (**spark-streaming-data-persistence-examples compile output**).</span></span> <span data-ttu-id="4dc45-218">選取要刪除的 jar，然後按一下 [刪除] 圖示 (![delete icon](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png))。</span><span class="sxs-lookup"><span data-stu-id="4dc45-218">Select the jars to delete and then click the **Delete** icon (![delete icon](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span></span>
      
       <span data-ttu-id="4dc45-219">![Apache Spark 串流範例 - 將擷取的 jar 刪除](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark 串流範例 - 將擷取的 jar 刪除")</span><span class="sxs-lookup"><span data-stu-id="4dc45-219">![Apache Spark streaming example - delete extracted jars](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark streaming example - delete extracted jars")</span></span>
      
       <span data-ttu-id="4dc45-220">請確實選取 [在建置時建立]  方塊，以確保在每次建置或更新專案時都會建立 jar。</span><span class="sxs-lookup"><span data-stu-id="4dc45-220">Make sure **Build on make** box is selected, which ensures that the jar is created every time the project is built or updated.</span></span> <span data-ttu-id="4dc45-221">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="4dc45-221">Click **Apply**.</span></span>
   6. <span data-ttu-id="4dc45-222">在 [輸出配置] 索引標籤中的 [可用的項目] 方塊右下方，會有您先前新增至專案程式庫的 SQL JDBC jar。</span><span class="sxs-lookup"><span data-stu-id="4dc45-222">In the **Output Layout** tab, right at the bottom of the **Available Elements** box, you have the SQL JDBC jar that you added earlier to the project library.</span></span> <span data-ttu-id="4dc45-223">您必須將此新增至 [輸出配置]  索引標籤。以滑鼠右鍵按一下 jar 檔案，然後按一下 [解壓縮到輸出根目錄中] 。</span><span class="sxs-lookup"><span data-stu-id="4dc45-223">You must add this to the **Output Layout** tab. Right-click the jar file, and then click **Extract Into Output Root**.</span></span>
      
       <span data-ttu-id="4dc45-224">![Apache Spark 串流範例 - 擷取相依性 jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark 串流範例 - 擷取相依性 jar")</span><span class="sxs-lookup"><span data-stu-id="4dc45-224">![Apache Spark streaming example - extract dependency jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark streaming example - extract dependency jar")</span></span>  
      
       <span data-ttu-id="4dc45-225">[輸出配置]  索引標籤此時應顯示如下。</span><span class="sxs-lookup"><span data-stu-id="4dc45-225">The **Output Layout** tab should now look like this.</span></span>
      
       <span data-ttu-id="4dc45-226">![Apache Spark 串流範例 - 最終輸出索引標籤](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark 串流範例 - 最終輸出索引標籤")</span><span class="sxs-lookup"><span data-stu-id="4dc45-226">![Apache Spark streaming example - final output tab](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark streaming example - final output tab")</span></span>        
      
       <span data-ttu-id="4dc45-227">在 [專案結構] 對話方塊中，按一下 [套用]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="4dc45-227">In the **Project Structure** dialog box, click **Apply** and then click **OK**.</span></span>    
   7. <span data-ttu-id="4dc45-228">在功能表列中按一下 [建置]，然後按一下 [建立專案]。</span><span class="sxs-lookup"><span data-stu-id="4dc45-228">From the menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="4dc45-229">您也可以按一下 [建置構件]，以建立 jar。</span><span class="sxs-lookup"><span data-stu-id="4dc45-229">You can also click **Build Artifacts** to create the jar.</span></span> <span data-ttu-id="4dc45-230">輸出 jar 會建立在 **\classes\artifacts** 下。</span><span class="sxs-lookup"><span data-stu-id="4dc45-230">The output jar is created under **\classes\artifacts**.</span></span>
      
       <span data-ttu-id="4dc45-231">![Apache Spark 串流範例 - 輸出 jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark 串流範例 - 輸出 jar")</span><span class="sxs-lookup"><span data-stu-id="4dc45-231">![Apache Spark streaming example - output JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark streaming example - output JAR")</span></span>

## <a name="run-the-application-remotely-on-a-spark-cluster-using-livy"></a><span data-ttu-id="4dc45-232">使用 Livy 在 Spark 叢集上遠端執行應用程式</span><span class="sxs-lookup"><span data-stu-id="4dc45-232">Run the application remotely on a Spark cluster using Livy</span></span>

<span data-ttu-id="4dc45-233">在本文中，您會使用 Livy，在 Apache Spark 叢集上從遠端執行串流應用程式。</span><span class="sxs-lookup"><span data-stu-id="4dc45-233">In this article you use Livy to run the Apache Spark streaming application remotely on a Spark cluster.</span></span> <span data-ttu-id="4dc45-234">如需如何搭配使用 Livy 與 HDInsight Spark 叢集的詳細討論，請參閱 [從遠端將作業提交到 Azure HDInsight 上的 Apache Spark 叢集](hdinsight-apache-spark-livy-rest-interface.md)。</span><span class="sxs-lookup"><span data-stu-id="4dc45-234">For detailed discussion on how to use Livy with HDInsight Spark cluster, see [Submit jobs remotely to an Apache Spark cluster on Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span> <span data-ttu-id="4dc45-235">您必須先完成若干作業後，才能開始執行 Spark 串流應用程式：</span><span class="sxs-lookup"><span data-stu-id="4dc45-235">Before you can start running the Spark streaming application, there are a couple of things you should do:</span></span>

1. <span data-ttu-id="4dc45-236">啟動本機獨立應用程式以產生事件，並將其傳送至事件中樞。</span><span class="sxs-lookup"><span data-stu-id="4dc45-236">Start the local standalone application to generate events and sent to Event Hub.</span></span> <span data-ttu-id="4dc45-237">請使用下列命令來執行此動作：</span><span class="sxs-lookup"><span data-stu-id="4dc45-237">Use the following command to do so:</span></span>

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. <span data-ttu-id="4dc45-238">將串流處理 jar (**spark-streaming-data-persistence-examples.jar**) 複製到與叢集相關聯的 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="4dc45-238">Copy the streaming jar (**spark-streaming-data-persistence-examples.jar**) to the Azure Blob storage associated with the cluster.</span></span> <span data-ttu-id="4dc45-239">如此，jar 即可供 Livy 存取。</span><span class="sxs-lookup"><span data-stu-id="4dc45-239">This makes the jar accessible to Livy.</span></span> <span data-ttu-id="4dc45-240">您可以使用命令列公用程式 [**AzCopy**](../storage/common/storage-use-azcopy.md) 來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="4dc45-240">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, to do so.</span></span> <span data-ttu-id="4dc45-241">此外也有很多用戶端可用來上傳資料。</span><span class="sxs-lookup"><span data-stu-id="4dc45-241">There are a lot of other clients you can use to upload data.</span></span> <span data-ttu-id="4dc45-242">您可以在 [在 HDInsight 上將 Hadoop 作業的資料上傳](hdinsight-upload-data.md)中找到其詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4dc45-242">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
3. <span data-ttu-id="4dc45-243">將 CURL 安裝在您用來執行這些應用程式的電腦上。</span><span class="sxs-lookup"><span data-stu-id="4dc45-243">Install CURL on the computer where you are running these applications from.</span></span> <span data-ttu-id="4dc45-244">我們使用 CURL 來叫用 Livy 端點，以從遠端執行作業。</span><span class="sxs-lookup"><span data-stu-id="4dc45-244">We use CURL to invoke the Livy endpoints to run the jobs remotely.</span></span>

### <a name="run-the-spark-streaming-application-to-receive-the-events-into-an-azure-storage-blob-as-text"></a><span data-ttu-id="4dc45-245">執行 Spark 串流應用程式，以文字形式將事件接收到 Azure 儲存體 Blob 中</span><span class="sxs-lookup"><span data-stu-id="4dc45-245">Run the Spark streaming application to receive the events into an Azure Storage Blob as text</span></span>

<span data-ttu-id="4dc45-246">開啟命令提示字元，導覽至您安裝 CURL 的目錄，然後執行下列命令 (取代使用者名稱/密碼與叢集名稱)：</span><span class="sxs-lookup"><span data-stu-id="4dc45-246">Open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="4dc45-247">檔案 **inputBlob.txt** 中的參數定義如下：</span><span class="sxs-lookup"><span data-stu-id="4dc45-247">The parameters in the file **inputBlob.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="4dc45-248">我們要了解，輸入檔案中的參數為何：</span><span class="sxs-lookup"><span data-stu-id="4dc45-248">Let us understand what the parameters in the input file are:</span></span>

* <span data-ttu-id="4dc45-249">**file** 是與叢集相關聯的 Azure 儲存體帳戶上的應用程式 jar 檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="4dc45-249">**file** is the path to the application jar file on the Azure storage account associated with the cluster.</span></span>
* <span data-ttu-id="4dc45-250">**className** 是 jar 中的類別名稱。</span><span class="sxs-lookup"><span data-stu-id="4dc45-250">**className** is the name of the class in the jar.</span></span>
* <span data-ttu-id="4dc45-251">**args** 是類別所需的引數清單</span><span class="sxs-lookup"><span data-stu-id="4dc45-251">**args** is the list of arguments required by the class</span></span>
* <span data-ttu-id="4dc45-252">**numExecutors** 是 Spark 用來執行串流應用程式的核心數目。</span><span class="sxs-lookup"><span data-stu-id="4dc45-252">**numExecutors** is the number of cores used by Spark to run the streaming application.</span></span> <span data-ttu-id="4dc45-253">此數目一律至少應為事件中樞資料分割數目的兩倍。</span><span class="sxs-lookup"><span data-stu-id="4dc45-253">This should always be at least twice the number of Event Hub partitions.</span></span>
* <span data-ttu-id="4dc45-254">**executorMemory**、**executorCores**、**driverMemory** 是用來將必要資源指派給串流應用程式的參數。</span><span class="sxs-lookup"><span data-stu-id="4dc45-254">**executorMemory**, **executorCores**, **driverMemory** are parameters used to assign required resources to the streaming application.</span></span>

> [!NOTE]
> <span data-ttu-id="4dc45-255">您不需要建立做為參數的輸出資料夾 (EventCheckpoint、EventCount/EventCount10)。</span><span class="sxs-lookup"><span data-stu-id="4dc45-255">You do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="4dc45-256">串流應用程式會為您建立。</span><span class="sxs-lookup"><span data-stu-id="4dc45-256">The streaming application creates them for you.</span></span>
>
>

<span data-ttu-id="4dc45-257">執行命令時，您應該會看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="4dc45-257">When you run the command, you should see an output like the following:</span></span>

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact

<span data-ttu-id="4dc45-258">請記下位於輸出中最後一行的批次識別碼 (在此範例中為 '1')。</span><span class="sxs-lookup"><span data-stu-id="4dc45-258">Make a note of the batch ID in the last line of the output (in this example it is '1').</span></span> <span data-ttu-id="4dc45-259">若要確認應用程式已成功執行，您可以查看與叢集相關聯的 Azure 儲存體帳戶，您應該會看到該處已建立 **/EventCount/EventCount10** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="4dc45-259">To verify that the application runs successfully, you can look at your Azure storage account associated with the cluster and you should see the **/EventCount/EventCount10** folder created there.</span></span> <span data-ttu-id="4dc45-260">此資料夾應包含相關 blob，其中擷取在為參數 **batch-interval-in-seconds**指定的時段內所處理的事件數目。</span><span class="sxs-lookup"><span data-stu-id="4dc45-260">This folder should contain blobs that captures the number of events processed within the time period specified for the parameter **batch-interval-in-seconds**.</span></span>

<span data-ttu-id="4dc45-261">Spark 串流應用程式會繼續執行，直到您終止為止。</span><span class="sxs-lookup"><span data-stu-id="4dc45-261">The Spark streaming application will continue to run until you kill it.</span></span> <span data-ttu-id="4dc45-262">若要這麼做，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="4dc45-262">To do so, use the following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-the-applications-to-receive-the-events-into-an-azure-storage-blob-as-json"></a><span data-ttu-id="4dc45-263">執行應用程式，以將事件以 JSON 的形式接收到 Azure 儲存體 Blob 中</span><span class="sxs-lookup"><span data-stu-id="4dc45-263">Run the applications to receive the events into an Azure Storage Blob as JSON</span></span>
<span data-ttu-id="4dc45-264">開啟命令提示字元，導覽至您安裝 CURL 的目錄，然後執行下列命令 (取代使用者名稱/密碼與叢集名稱)：</span><span class="sxs-lookup"><span data-stu-id="4dc45-264">Open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="4dc45-265">檔案 **inputJSON.txt** 中的參數定義如下：</span><span class="sxs-lookup"><span data-stu-id="4dc45-265">The parameters in the file **inputJSON.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="4dc45-266">這些參數類似於您在先前的步驟中為文字輸出指定的參數。</span><span class="sxs-lookup"><span data-stu-id="4dc45-266">The parameters are similar to what you specified for the text output, in the previous step.</span></span> <span data-ttu-id="4dc45-267">同樣地，您不需要建立做為參數的輸出資料夾 (EventCheckpoint、EventCount/EventCount10)。</span><span class="sxs-lookup"><span data-stu-id="4dc45-267">Again, you do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="4dc45-268">串流應用程式會為您建立。</span><span class="sxs-lookup"><span data-stu-id="4dc45-268">The streaming application creates them for you.</span></span>

 <span data-ttu-id="4dc45-269">在執行命令之後，您可以查看與叢集相關聯的 Azure 儲存體帳戶，您應該會看到該處已建立 **/EventStore10** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="4dc45-269">After you run the command, you can look at your Azure storage account associated with the cluster and you should see the **/EventStore10** folder created there.</span></span> <span data-ttu-id="4dc45-270">開啟任何以 **part-** 開頭的檔案，您應該會看到以 JSON 格式處理的事件。</span><span class="sxs-lookup"><span data-stu-id="4dc45-270">Open any file prefixed with **part-** and you should see the events processed in a JSON format.</span></span>

### <a name="run-the-applications-to-receive-the-events-into-a-hive-table"></a><span data-ttu-id="4dc45-271">執行應用程式，以將事件接收到 Hive 資料表中</span><span class="sxs-lookup"><span data-stu-id="4dc45-271">Run the applications to receive the events into a Hive table</span></span>
<span data-ttu-id="4dc45-272">若要執行會將事件串流至 Hive 資料表中的 Spark 串流應用程式，您需要一些其他元件。</span><span class="sxs-lookup"><span data-stu-id="4dc45-272">To run the Spark streaming application that streams events into a Hive table you need some additional components.</span></span> <span data-ttu-id="4dc45-273">它們是：</span><span class="sxs-lookup"><span data-stu-id="4dc45-273">These are:</span></span>

* <span data-ttu-id="4dc45-274">datanucleus-api-jdo-3.2.6.jar</span><span class="sxs-lookup"><span data-stu-id="4dc45-274">datanucleus-api-jdo-3.2.6.jar</span></span>
* <span data-ttu-id="4dc45-275">datanucleus-rdbms-3.2.9.jar</span><span class="sxs-lookup"><span data-stu-id="4dc45-275">datanucleus-rdbms-3.2.9.jar</span></span>
* <span data-ttu-id="4dc45-276">datanucleus-core-3.2.10.jar</span><span class="sxs-lookup"><span data-stu-id="4dc45-276">datanucleus-core-3.2.10.jar</span></span>
* <span data-ttu-id="4dc45-277">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="4dc45-277">hive-site.xml</span></span>

<span data-ttu-id="4dc45-278">這些 **.jar** 檔案位於您的 HDInsight Spark 叢集上：`/usr/hdp/current/spark-client/lib`。</span><span class="sxs-lookup"><span data-stu-id="4dc45-278">The **.jar** files are available on your HDInsight Spark cluster at `/usr/hdp/current/spark-client/lib`.</span></span> <span data-ttu-id="4dc45-279">**hive-site.xml** 位於 `/usr/hdp/current/spark-client/conf`。</span><span class="sxs-lookup"><span data-stu-id="4dc45-279">The **hive-site.xml** is available at `/usr/hdp/current/spark-client/conf`.</span></span>

<span data-ttu-id="4dc45-280">您可以使用 [WinScp](http://winscp.net/eng/download.php) 將這些檔案從叢集複製到您的本機電腦。</span><span class="sxs-lookup"><span data-stu-id="4dc45-280">You can use [WinScp](http://winscp.net/eng/download.php) to copy over these files from the cluster to your local computer.</span></span> <span data-ttu-id="4dc45-281">接著，您可以使用工具，將這些檔案複製到與叢集相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4dc45-281">You can then use tools to copy these files over to your storage account associated with the cluster.</span></span> <span data-ttu-id="4dc45-282">如需關於如何將檔案上傳至儲存體帳戶的詳細資訊，請參閱 [在 HDInsight 上將 Hadoop 作業的資料上傳](hdinsight-upload-data.md)。</span><span class="sxs-lookup"><span data-stu-id="4dc45-282">For more information on how to upload files to the storage account, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

<span data-ttu-id="4dc45-283">將檔案複製到您的 Azure 儲存體帳戶之後，請開啟命令提示字元，導覽至您安裝 CURL 的目錄，然後執行下列命令 (取代使用者名稱/密碼與叢集名稱)：</span><span class="sxs-lookup"><span data-stu-id="4dc45-283">Once you have copied over the files to your Azure storage account, open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="4dc45-284">檔案 **inputHive.txt** 中的參數定義如下：</span><span class="sxs-lookup"><span data-stu-id="4dc45-284">The parameters in the file **inputHive.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="4dc45-285">這些參數類似於您在先前的步驟中為文字輸出指定的參數。</span><span class="sxs-lookup"><span data-stu-id="4dc45-285">The parameters are similar to what you specified for the text output, in the previous steps.</span></span> <span data-ttu-id="4dc45-286">同樣地，您不需要建立做為參數的輸出資料夾 (EventCheckpoint、EventCount/EventCount10) 或輸出 Hive 資料表 (EventHiveTable10)。</span><span class="sxs-lookup"><span data-stu-id="4dc45-286">Again, you do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) or the output Hive table (EventHiveTable10) that are used as parameters.</span></span> <span data-ttu-id="4dc45-287">串流應用程式會為您建立。</span><span class="sxs-lookup"><span data-stu-id="4dc45-287">The streaming application creates them for you.</span></span> <span data-ttu-id="4dc45-288">請注意，**jars** 和 **files** 選項會包含您已複製到儲存體帳戶的 .jar 檔案和 hive-site.xml 的路徑。</span><span class="sxs-lookup"><span data-stu-id="4dc45-288">Note that the **jars** and **files** option includes paths to the .jar files and the hive-site.xml that you copied over to the storage account.</span></span>

<span data-ttu-id="4dc45-289">若要確認 Hive 資料表已成功建立，您可以 SSH 到叢集中，並執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="4dc45-289">To verify that the hive table was successfully created, you can SSH into the cluster and run Hive queries.</span></span> <span data-ttu-id="4dc45-290">如需指示，請參閱 [利用 SSH 搭配使用 Hive 與 HDInsight 中的 Hadoop](hdinsight-hadoop-use-hive-ssh.md)。</span><span class="sxs-lookup"><span data-stu-id="4dc45-290">For instructions, see [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-ssh.md).</span></span> <span data-ttu-id="4dc45-291">當您使用 SSH 連線之後，您可以執行下列命令，以確認 Hive 資料表 **EventHiveTable10**已建立。</span><span class="sxs-lookup"><span data-stu-id="4dc45-291">Once you are connected using SSH, you can run the following command to verify that the Hive table, **EventHiveTable10**, is created.</span></span>

    show tables;

<span data-ttu-id="4dc45-292">您應該會看到如下所示的輸出：</span><span class="sxs-lookup"><span data-stu-id="4dc45-292">You should see an output similar to the following:</span></span>

    OK
    eventhivetable10
    hivesampletable

<span data-ttu-id="4dc45-293">您也可以執行 SELECT 查詢，以檢視資料表的內容。</span><span class="sxs-lookup"><span data-stu-id="4dc45-293">You can also run a SELECT query to view the contents of the table.</span></span>

    SELECT * FROM eventhivetable10 LIMIT 10;

<span data-ttu-id="4dc45-294">您應該會看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="4dc45-294">You should see an output like the following:</span></span>

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


### <a name="run-the-applications-to-receive-the-events-into-an-azure-sql-database-table"></a><span data-ttu-id="4dc45-295">執行應用程式，以將事件接收到 Azure SQL Database 資料表中</span><span class="sxs-lookup"><span data-stu-id="4dc45-295">Run the applications to receive the events into an Azure SQL database table</span></span>
<span data-ttu-id="4dc45-296">執行此步驟之前，請先確定您已建立 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="4dc45-296">Before running this step, make sure you have an Azure SQL database created.</span></span> <span data-ttu-id="4dc45-297">如需指示，請參閱[快速建立 SQL 資料庫](../sql-database/sql-database-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="4dc45-297">For instructions, see [Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="4dc45-298">為了完成本節，您需要資料庫名稱、資料庫伺服器名稱和資料庫系統管理員認證的值做為參數。</span><span class="sxs-lookup"><span data-stu-id="4dc45-298">To complete this section, you need values for database name, database server name, and the database administrator credentials as parameters.</span></span> <span data-ttu-id="4dc45-299">但您不需要建立資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="4dc45-299">You do not need to create the database table though.</span></span> <span data-ttu-id="4dc45-300">Spark 串流應用程式會為您建立。</span><span class="sxs-lookup"><span data-stu-id="4dc45-300">The Spark streaming application creates that for you.</span></span>

<span data-ttu-id="4dc45-301">開啟命令提示字元，導覽至您安裝 CURL 的目錄，然後執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="4dc45-301">Open a command prompt, navigate to the directory where you installed CURL, and run the following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="4dc45-302">檔案 **inputSQL.txt** 中的參數定義如下：</span><span class="sxs-lookup"><span data-stu-id="4dc45-302">The parameters in the file **inputSQL.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="4dc45-303">若要驗證應用程式是否順利執行，您可以使用 SQL Server Management Studio 連接到 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="4dc45-303">To verify that the application runs successfully, you can connect to the Azure SQL database using SQL Server Management Studio.</span></span> <span data-ttu-id="4dc45-304">如需如何執行該動作的指示，請參閱 [使用 SQL Server Management Studio 連接到 SQL Database](../sql-database/sql-database-connect-query-ssms.md)。</span><span class="sxs-lookup"><span data-stu-id="4dc45-304">For instructions on how to do that, see [Connect to SQL Database with SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span></span> <span data-ttu-id="4dc45-305">連接到資料庫之後，您可以導覽至串流應用程式所建立的 **EventContent** 資料表。</span><span class="sxs-lookup"><span data-stu-id="4dc45-305">Once you are connected to the database, you can navigate to the **EventContent** table that was created by the streaming application.</span></span> <span data-ttu-id="4dc45-306">您可以執行快速查詢，以取得該資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="4dc45-306">You can run a quick query to get the data from the table.</span></span> <span data-ttu-id="4dc45-307">請執行下列查詢：</span><span class="sxs-lookup"><span data-stu-id="4dc45-307">Run the following query:</span></span>

    SELECT * FROM EventCount

<span data-ttu-id="4dc45-308">您應該會看到如下所示的輸出：</span><span class="sxs-lookup"><span data-stu-id="4dc45-308">You should see output similar to the following:</span></span>

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


## <span data-ttu-id="4dc45-309"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="4dc45-309"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="4dc45-310">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="4dc45-310">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)
* [<span data-ttu-id="4dc45-311">收件者型連線和 Direct DStream 的設計</span><span class="sxs-lookup"><span data-stu-id="4dc45-311">Design of Receiver-based Connection and Direct DStream</span></span>](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a><span data-ttu-id="4dc45-312">案例</span><span class="sxs-lookup"><span data-stu-id="4dc45-312">Scenarios</span></span>
* [<span data-ttu-id="4dc45-313">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="4dc45-313">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="4dc45-314">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="4dc45-314">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="4dc45-315">Spark 和機器學習服務：使用 HDInsight 中的 Spark 來預測食品檢查結果</span><span class="sxs-lookup"><span data-stu-id="4dc45-315">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="4dc45-316">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="4dc45-316">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="4dc45-317">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="4dc45-317">Create and run applications</span></span>
* [<span data-ttu-id="4dc45-318">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="4dc45-318">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="4dc45-319">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="4dc45-319">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="4dc45-320">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="4dc45-320">Tools and extensions</span></span>
* [<span data-ttu-id="4dc45-321">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons (使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式來建立和提交 Spark Scala 應用程式)</span><span class="sxs-lookup"><span data-stu-id="4dc45-321">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="4dc45-322">使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式遠端偵錯 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="4dc45-322">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="4dc45-323">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="4dc45-323">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="4dc45-324">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="4dc45-324">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="4dc45-325">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="4dc45-325">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="4dc45-326">在電腦上安裝 Jupyter 並連接到 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="4dc45-326">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="4dc45-327">管理資源</span><span class="sxs-lookup"><span data-stu-id="4dc45-327">Manage resources</span></span>
* [<span data-ttu-id="4dc45-328">在 Azure HDInsight 中管理 Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="4dc45-328">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="4dc45-329">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="4dc45-329">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
