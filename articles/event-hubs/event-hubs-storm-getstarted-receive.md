---
title: "使用 Apache Storm 從 Azure 事件中樞接收事件 | Microsoft Docs"
description: "開始使用 Apache Storm 從事件中樞接收事件"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: java
ms.devlang: multiple
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 3e15370c7602276ef323708632b324fe05497f41
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="receive-events-from-event-hubs-using-apache-storm"></a><span data-ttu-id="ee8d5-103">使用 Apache Storm 從事件中樞接收事件</span><span class="sxs-lookup"><span data-stu-id="ee8d5-103">Receive events from Event Hubs using Apache Storm</span></span>

<span data-ttu-id="ee8d5-104">[Apache Storm](https://storm.incubator.apache.org) 是分散式即時運算系統，可簡化未繫結資料串流的可靠處理。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-104">[Apache Storm](https://storm.incubator.apache.org) is a distributed real-time computation system that simplifies reliable processing of unbounded streams of data.</span></span> <span data-ttu-id="ee8d5-105">本節說明如何使用「Azure 事件中樞」Storm Spout 來接收來自「事件中樞」的事件。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-105">This section shows how to use an Azure Event Hubs Storm spout to receive events from Event Hubs.</span></span> <span data-ttu-id="ee8d5-106">使用 Apache Storm，您可以將事件分割到多個裝載於不同節點的處理序。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-106">Using Apache Storm, you can split events across multiple processes hosted in different nodes.</span></span> <span data-ttu-id="ee8d5-107">事件中心與 Storm 的整合透過使用 Storm 的 Zookeeper 安裝透明地設定檢查點以檢查其進度、管理持續檢查點以及來自事件中心的平行接收，以簡化事件的使用。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-107">The Event Hubs integration with Storm simplifies event consumption by transparently checkpointing its progress using Storm's Zookeeper installation, managing persistent checkpoints and parallel receives from Event Hubs.</span></span>

<span data-ttu-id="ee8d5-108">如需事件中樞接收模式的詳細資訊，請參閱 [事件中樞概觀][Event Hubs overview]。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-108">For more information about Event Hubs receive patterns, see the [Event Hubs overview][Event Hubs overview].</span></span>

## <a name="create-project-and-add-code"></a><span data-ttu-id="ee8d5-109">建立專案並新增程式碼</span><span class="sxs-lookup"><span data-stu-id="ee8d5-109">Create project and add code</span></span>

<span data-ttu-id="ee8d5-110">本教學課程使用 [HDInsight Storm][HDInsight Storm] 安裝，其包含在已可使用的事件中樞 Spout 中。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-110">This tutorial uses an [HDInsight Storm][HDInsight Storm] installation, which comes with the Event Hubs spout already available.</span></span>

1. <span data-ttu-id="ee8d5-111">請遵循 [HDInsight Storm - 入門](../hdinsight/hdinsight-storm-overview.md) 程序來建立新的 HDInsight 叢集，並透過遠端桌面與其連線。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-111">Follow the [HDInsight Storm - Get Started](../hdinsight/hdinsight-storm-overview.md) procedure to create a new HDInsight cluster, and connect to it via Remote Desktop.</span></span>
2. <span data-ttu-id="ee8d5-112">將 `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` 檔案複製到本機開發環境。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-112">Copy the `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` file to your local development environment.</span></span> <span data-ttu-id="ee8d5-113">這包含 events-storm-spout。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-113">This contains the events-storm-spout.</span></span>
3. <span data-ttu-id="ee8d5-114">使用下列命令將封裝安裝到本機 Maven 存放區。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-114">Use the following command to install the package into the local Maven store.</span></span> <span data-ttu-id="ee8d5-115">這樣可讓您在稍後的步驟中將它加入 Storm 專案中做為參考。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-115">This enables you to add it as a reference in the Storm project in a later step.</span></span>

    ```shell
    mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar
    ```
4. <span data-ttu-id="ee8d5-116">在 Eclipse 中，建立新的 Maven 專案 (依序按一下 [檔案]、[新增]、[專案])。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-116">In Eclipse, create a new Maven project (click **File**, then **New**, then **Project**).</span></span>
   
    ![][12]
5. <span data-ttu-id="ee8d5-117">選取 [使用預設工作區位置]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-117">Select **Use default Workspace location**, then click **Next**</span></span>
6. <span data-ttu-id="ee8d5-118">選取 [maven-archetype-quickstart] 原型，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-118">Select the **maven-archetype-quickstart** archetype, then click **Next**</span></span>
7. <span data-ttu-id="ee8d5-119">插入 **GroupId** 和 **ArtifactId**，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-119">Insert a **GroupId** and **ArtifactId**, then click **Finish**</span></span>
8. <span data-ttu-id="ee8d5-120">在 **pom.xml** 中，於 `<dependency>` 節點中新增下列相依性。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-120">In **pom.xml**, add the following dependencies in the `<dependency>` node.</span></span>

    ```xml  
    <dependency>
        <groupId>org.apache.storm</groupId>
        <artifactId>storm-core</artifactId>
        <version>0.9.2-incubating</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.microsoft.eventhubs</groupId>
        <artifactId>eventhubs-storm-spout</artifactId>
        <version>0.9</version>
    </dependency>
    <dependency>
        <groupId>com.netflix.curator</groupId>
        <artifactId>curator-framework</artifactId>
        <version>1.3.3</version>
        <exclusions>
            <exclusion>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
            </exclusion>
            <exclusion>
                <groupId>org.slf4j</groupId>
                <artifactId>slf4j-log4j12</artifactId>
            </exclusion>
        </exclusions>
        <scope>provided</scope>
    </dependency>
    ```

9. <span data-ttu-id="ee8d5-121">在 **src** 資料夾中，建立名為 **Config.properties** 的檔案，複製下列內容，並取代 `receive rule key` 與 `event hub name` 的值：</span><span class="sxs-lookup"><span data-stu-id="ee8d5-121">In the **src** folder, create a file called **Config.properties** and copy the following content, substituting the `receive rule key` and `event hub name` values:</span></span>

    ```java
    eventhubspout.username = ReceiveRule
    eventhubspout.password = {receive rule key}
    eventhubspout.namespace = ioteventhub-ns
    eventhubspout.entitypath = {event hub name}
    eventhubspout.partitions.count = 16
       
    # if not provided, will use storm's zookeeper settings
    # zookeeper.connectionstring=localhost:2181
       
    eventhubspout.checkpoint.interval = 10
    eventhub.receiver.credits = 10
    ```
    <span data-ttu-id="ee8d5-122">**eventhub.receiver.credits** 的值可決定批次處理多少事件之後，才將它們釋放到 Storm 管線。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-122">The value for **eventhub.receiver.credits** determines how many events are batched before releasing them to the Storm pipeline.</span></span> <span data-ttu-id="ee8d5-123">為了簡單起見，此範例會將此值設定為 10。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-123">For the sake of simplicity, this example sets this value to 10.</span></span> <span data-ttu-id="ee8d5-124">在生產環境中，它通常應設定為較高的值。例如，1024年。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-124">In production, it should usually be set to higher values; for example, 1024.</span></span>
10. <span data-ttu-id="ee8d5-125">使用下列程式碼，建立稱為 **LoggerBolt** 的新類別：</span><span class="sxs-lookup"><span data-stu-id="ee8d5-125">Create a new class called **LoggerBolt** with the following code:</span></span>
    
    ```java
    import java.util.Map;
    import org.slf4j.Logger;
    import org.slf4j.LoggerFactory;
    import backtype.storm.task.OutputCollector;
    import backtype.storm.task.TopologyContext;
    import backtype.storm.topology.OutputFieldsDeclarer;
    import backtype.storm.topology.base.BaseRichBolt;
    import backtype.storm.tuple.Tuple;
    
    public class LoggerBolt extends BaseRichBolt {
        private OutputCollector collector;
        private static final Logger logger = LoggerFactory
                  .getLogger(LoggerBolt.class);
    
        @Override
        public void execute(Tuple tuple) {
            String value = tuple.getString(0);
            logger.info("Tuple value: " + value);
   
            collector.ack(tuple);
        }
   
        @Override
        public void prepare(Map map, TopologyContext context, OutputCollector collector) {
            this.collector = collector;
            this.count = 0;
        }
        
        @Override
        public void declareOutputFields(OutputFieldsDeclarer declarer) {
            // no output fields
        }
    
    }
    ```
    
    <span data-ttu-id="ee8d5-126">此 Storm Bolt 會記錄已接收事件的內容。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-126">This Storm bolt logs the content of the received events.</span></span> <span data-ttu-id="ee8d5-127">這可以輕鬆地擴充以將 Tuple 儲存至儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-127">This can easily be extended to store tuples in a storage service.</span></span> <span data-ttu-id="ee8d5-128">[HDInsight 感應器分析教學課程] 使用這種相同的方式，將資料儲存至 HBase。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-128">The [HDInsight sensor analysis tutorial] uses this same approach to store data into HBase.</span></span>
11. <span data-ttu-id="ee8d5-129">使用下列程式碼，建立稱為 **LogTopology** 的類別：</span><span class="sxs-lookup"><span data-stu-id="ee8d5-129">Create a class called **LogTopology** with the following code:</span></span>
    
    ```java
    import java.io.FileReader;
    import java.util.Properties;
    import backtype.storm.Config;
    import backtype.storm.LocalCluster;
    import backtype.storm.StormSubmitter;
    import backtype.storm.generated.StormTopology;
    import backtype.storm.topology.TopologyBuilder;
    import com.microsoft.eventhubs.samples.EventCount;
    import com.microsoft.eventhubs.spout.EventHubSpout;
    import com.microsoft.eventhubs.spout.EventHubSpoutConfig;
        
    public class LogTopology {
        protected EventHubSpoutConfig spoutConfig;
        protected int numWorkers;
        
        protected void readEHConfig(String[] args) throws Exception {
            Properties properties = new Properties();
            if (args.length > 1) {
                properties.load(new FileReader(args[1]));
            } else {
                properties.load(EventCount.class.getClassLoader()
                        .getResourceAsStream("Config.properties"));
            }
        
            String username = properties.getProperty("eventhubspout.username");
            String password = properties.getProperty("eventhubspout.password");
            String namespaceName = properties
                    .getProperty("eventhubspout.namespace");
            String entityPath = properties.getProperty("eventhubspout.entitypath");
            String zkEndpointAddress = properties
                    .getProperty("zookeeper.connectionstring"); // opt
            int partitionCount = Integer.parseInt(properties
                    .getProperty("eventhubspout.partitions.count"));
            int checkpointIntervalInSeconds = Integer.parseInt(properties
                    .getProperty("eventhubspout.checkpoint.interval"));
            int receiverCredits = Integer.parseInt(properties
                    .getProperty("eventhub.receiver.credits")); // prefetch count
                                                                // (opt)
            System.out.println("Eventhub spout config: ");
            System.out.println("  partition count: " + partitionCount);
            System.out.println("  checkpoint interval: "
                    + checkpointIntervalInSeconds);
            System.out.println("  receiver credits: " + receiverCredits);
     
            spoutConfig = new EventHubSpoutConfig(username, password,
                    namespaceName, entityPath, partitionCount, zkEndpointAddress,
                    checkpointIntervalInSeconds, receiverCredits);
        
            // set the number of workers to be the same as partition number.
            // the idea is to have a spout and a logger bolt co-exist in one
            // worker to avoid shuffling messages across workers in storm cluster.
            numWorkers = spoutConfig.getPartitionCount();
        
            if (args.length > 0) {
                // set topology name so that sample Trident topology can use it as
                // stream name.
                spoutConfig.setTopologyName(args[0]);
            }
        }
        
        protected StormTopology buildTopology() {
            TopologyBuilder topologyBuilder = new TopologyBuilder();
       
            EventHubSpout eventHubSpout = new EventHubSpout(spoutConfig);
            topologyBuilder.setSpout("EventHubsSpout", eventHubSpout,
                    spoutConfig.getPartitionCount()).setNumTasks(
                    spoutConfig.getPartitionCount());
            topologyBuilder
                    .setBolt("LoggerBolt", new LoggerBolt(),
                            spoutConfig.getPartitionCount())
                    .localOrShuffleGrouping("EventHubsSpout")
                    .setNumTasks(spoutConfig.getPartitionCount());
            return topologyBuilder.createTopology();
        }
        
        protected void runScenario(String[] args) throws Exception {
            boolean runLocal = true;
            readEHConfig(args);
            StormTopology topology = buildTopology();
            Config config = new Config();
            config.setDebug(false);
        
            if (runLocal) {
                config.setMaxTaskParallelism(2);
                LocalCluster localCluster = new LocalCluster();
                localCluster.submitTopology("test", config, topology);
                Thread.sleep(5000000);
                localCluster.shutdown();
            } else {
                config.setNumWorkers(numWorkers);
                StormSubmitter.submitTopology(args[0], config, topology);
            }
        }
        
        public static void main(String[] args) throws Exception {
            LogTopology topology = new LogTopology();
            topology.runScenario(args);
        }
    }
    ```

    <span data-ttu-id="ee8d5-130">這個類別會建立新的事件中樞 Spout，方法是使用組態檔中的屬性來進行具現化。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-130">This class creates a new Event Hubs spout, using the properties in the configuration file to instantiate it.</span></span> <span data-ttu-id="ee8d5-131">請務必注意此範例所建立的 Spout 工作數目會與事件中樞內的磁碟分割數目相同，這是為了發揮該事件中樞所允許的平行處理原則上限。</span><span class="sxs-lookup"><span data-stu-id="ee8d5-131">It is important to note that this example creates as many spouts tasks as the number of partitions in the event hub, in order to use the maximum parallelism allowed by that event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee8d5-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ee8d5-132">Next steps</span></span>
<span data-ttu-id="ee8d5-133">您可以造訪下列連結以深入了解事件中樞︰</span><span class="sxs-lookup"><span data-stu-id="ee8d5-133">You can learn more about Event Hubs by visiting the following links:</span></span>

* <span data-ttu-id="ee8d5-134">[事件中樞概觀][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="ee8d5-134">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="ee8d5-135">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="ee8d5-135">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="ee8d5-136">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="ee8d5-136">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
<span data-ttu-id="ee8d5-137">[HDInsight 感應器分析教學課程]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md</span><span class="sxs-lookup"><span data-stu-id="ee8d5-137">[HDInsight sensor analysis tutorial]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md</span></span>

<!-- Images -->

[12]: ./media/event-hubs-get-started-receive-storm/create-storm1.png
