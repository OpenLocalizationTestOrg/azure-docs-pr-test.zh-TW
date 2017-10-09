---
title: "從 Azure 事件中心使用 Apache Storm aaaReceive 事件 |Microsoft 文件"
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
ms.openlocfilehash: a0ab860ee8d504a28aac380c504c928f0d6dbc1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-event-hubs-using-apache-storm"></a><span data-ttu-id="cf00a-103">使用 Apache Storm 從事件中樞接收事件</span><span class="sxs-lookup"><span data-stu-id="cf00a-103">Receive events from Event Hubs using Apache Storm</span></span>

<span data-ttu-id="cf00a-104">[Apache Storm](https://storm.incubator.apache.org) 是分散式即時運算系統，可簡化未繫結資料串流的可靠處理。</span><span class="sxs-lookup"><span data-stu-id="cf00a-104">[Apache Storm](https://storm.incubator.apache.org) is a distributed real-time computation system that simplifies reliable processing of unbounded streams of data.</span></span> <span data-ttu-id="cf00a-105">本節說明如何 toouse Azure 事件中心 Storm spout tooreceive 事件，從事件中樞。</span><span class="sxs-lookup"><span data-stu-id="cf00a-105">This section shows how toouse an Azure Event Hubs Storm spout tooreceive events from Event Hubs.</span></span> <span data-ttu-id="cf00a-106">使用 Apache Storm，您可以將事件分割到多個裝載於不同節點的處理序。</span><span class="sxs-lookup"><span data-stu-id="cf00a-106">Using Apache Storm, you can split events across multiple processes hosted in different nodes.</span></span> <span data-ttu-id="cf00a-107">hello Storm 整合事件中心事件取用，藉以簡化無障礙地檢查點進度使用 Storm 的動物園管理員安裝、 管理持續的檢查點並平行收到來自事件中心。</span><span class="sxs-lookup"><span data-stu-id="cf00a-107">hello Event Hubs integration with Storm simplifies event consumption by transparently checkpointing its progress using Storm's Zookeeper installation, managing persistent checkpoints and parallel receives from Event Hubs.</span></span>

<span data-ttu-id="cf00a-108">如需有關事件中心接收模式，請參閱 hello[事件中心概觀][Event Hubs overview]。</span><span class="sxs-lookup"><span data-stu-id="cf00a-108">For more information about Event Hubs receive patterns, see hello [Event Hubs overview][Event Hubs overview].</span></span>

## <a name="create-project-and-add-code"></a><span data-ttu-id="cf00a-109">建立專案並新增程式碼</span><span class="sxs-lookup"><span data-stu-id="cf00a-109">Create project and add code</span></span>

<span data-ttu-id="cf00a-110">本教學課程使用[HDInsight Storm] [ HDInsight Storm]安裝隨附於事件中樞 spout 的 hello 已經使用。</span><span class="sxs-lookup"><span data-stu-id="cf00a-110">This tutorial uses an [HDInsight Storm][HDInsight Storm] installation, which comes with hello Event Hubs spout already available.</span></span>

1. <span data-ttu-id="cf00a-111">請遵循 hello [HDInsight Storm-開始](../hdinsight/hdinsight-storm-overview.md)程序 toocreate 新的 HDInsight 叢集，並連接 tooit 透過遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="cf00a-111">Follow hello [HDInsight Storm - Get Started](../hdinsight/hdinsight-storm-overview.md) procedure toocreate a new HDInsight cluster, and connect tooit via Remote Desktop.</span></span>
2. <span data-ttu-id="cf00a-112">複製 hello`%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar`檔案 tooyour 本機開發環境。</span><span class="sxs-lookup"><span data-stu-id="cf00a-112">Copy hello `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` file tooyour local development environment.</span></span> <span data-ttu-id="cf00a-113">這包含 hello 事件 storm spout。</span><span class="sxs-lookup"><span data-stu-id="cf00a-113">This contains hello events-storm-spout.</span></span>
3. <span data-ttu-id="cf00a-114">使用下列命令 tooinstall hello 封裝到 hello 本機 Maven 存放區的 hello。</span><span class="sxs-lookup"><span data-stu-id="cf00a-114">Use hello following command tooinstall hello package into hello local Maven store.</span></span> <span data-ttu-id="cf00a-115">這可讓您 tooadd 它當做 hello Storm 參考專案中稍後的步驟。</span><span class="sxs-lookup"><span data-stu-id="cf00a-115">This enables you tooadd it as a reference in hello Storm project in a later step.</span></span>

    ```shell
    mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar
    ```
4. <span data-ttu-id="cf00a-116">在 Eclipse 中，建立新的 Maven 專案 (依序按一下 [檔案]、[新增]、[專案])。</span><span class="sxs-lookup"><span data-stu-id="cf00a-116">In Eclipse, create a new Maven project (click **File**, then **New**, then **Project**).</span></span>
   
    ![][12]
5. <span data-ttu-id="cf00a-117">選取 [使用預設工作區位置]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="cf00a-117">Select **Use default Workspace location**, then click **Next**</span></span>
6. <span data-ttu-id="cf00a-118">選取 hello **maven 原型-快速入門**原型，然後按一下 [**下一步]**</span><span class="sxs-lookup"><span data-stu-id="cf00a-118">Select hello **maven-archetype-quickstart** archetype, then click **Next**</span></span>
7. <span data-ttu-id="cf00a-119">插入 **GroupId** 和 **ArtifactId**，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="cf00a-119">Insert a **GroupId** and **ArtifactId**, then click **Finish**</span></span>
8. <span data-ttu-id="cf00a-120">在**pom.xml**，新增下列 hello 中的相依性的 hello`<dependency>`節點。</span><span class="sxs-lookup"><span data-stu-id="cf00a-120">In **pom.xml**, add hello following dependencies in hello `<dependency>` node.</span></span>

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

9. <span data-ttu-id="cf00a-121">在 hello **src**資料夾中，建立名為的檔案**Config.properties**和複製 hello 內容之後，以取代 hello`receive rule key`和`event hub name`值：</span><span class="sxs-lookup"><span data-stu-id="cf00a-121">In hello **src** folder, create a file called **Config.properties** and copy hello following content, substituting hello `receive rule key` and `event hub name` values:</span></span>

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
    <span data-ttu-id="cf00a-122">hello 值**eventhub.receiver.credits**決定多少事件會批次處理才釋放 toohello Storm 管線。</span><span class="sxs-lookup"><span data-stu-id="cf00a-122">hello value for **eventhub.receiver.credits** determines how many events are batched before releasing them toohello Storm pipeline.</span></span> <span data-ttu-id="cf00a-123">為了簡化的 hello 起見，本範例會設定此值 too10。</span><span class="sxs-lookup"><span data-stu-id="cf00a-123">For hello sake of simplicity, this example sets this value too10.</span></span> <span data-ttu-id="cf00a-124">實際執行環境，它通常應該設定 toohigher 值;例如，1024年。</span><span class="sxs-lookup"><span data-stu-id="cf00a-124">In production, it should usually be set toohigher values; for example, 1024.</span></span>
10. <span data-ttu-id="cf00a-125">建立新的類別稱為**LoggerBolt**以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="cf00a-125">Create a new class called **LoggerBolt** with hello following code:</span></span>
    
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
    
    <span data-ttu-id="cf00a-126">此出現閃電記錄 hello 內容的 hello 接收到事件。</span><span class="sxs-lookup"><span data-stu-id="cf00a-126">This Storm bolt logs hello content of hello received events.</span></span> <span data-ttu-id="cf00a-127">這可以輕鬆地擴充儲存體服務中的 toostore tuple。</span><span class="sxs-lookup"><span data-stu-id="cf00a-127">This can easily be extended toostore tuples in a storage service.</span></span> <span data-ttu-id="cf00a-128">hello [HDInsight 感應器分析教學課程]HBase 會使用這個相同的方法 toostore 資料。</span><span class="sxs-lookup"><span data-stu-id="cf00a-128">hello [HDInsight sensor analysis tutorial] uses this same approach toostore data into HBase.</span></span>
11. <span data-ttu-id="cf00a-129">建立類別，稱為**LogTopology**以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="cf00a-129">Create a class called **LogTopology** with hello following code:</span></span>
    
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
        
            // set hello number of workers toobe hello same as partition number.
            // hello idea is toohave a spout and a logger bolt co-exist in one
            // worker tooavoid shuffling messages across workers in storm cluster.
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

    <span data-ttu-id="cf00a-130">這個類別會建立新的事件中心 spout，使用中 hello 設定檔 tooinstantiate hello 屬性它。</span><span class="sxs-lookup"><span data-stu-id="cf00a-130">This class creates a new Event Hubs spout, using hello properties in hello configuration file tooinstantiate it.</span></span> <span data-ttu-id="cf00a-131">請務必這個範例會建立最大數量的 toonote spouts hello hello 事件中心中的資料分割的數字順序 toouse hello 最大平行處理該事件中心所允許的工作。</span><span class="sxs-lookup"><span data-stu-id="cf00a-131">It is important toonote that this example creates as many spouts tasks as hello number of partitions in hello event hub, in order toouse hello maximum parallelism allowed by that event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf00a-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cf00a-132">Next steps</span></span>
<span data-ttu-id="cf00a-133">您可以進一步了解事件中心瀏覽下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="cf00a-133">You can learn more about Event Hubs by visiting hello following links:</span></span>

* <span data-ttu-id="cf00a-134">[事件中樞概觀][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="cf00a-134">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="cf00a-135">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="cf00a-135">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="cf00a-136">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="cf00a-136">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
[HDInsight 感應器分析教學課程]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md

<!-- Images -->

[12]: ./media/event-hubs-get-started-receive-storm/create-storm1.png
