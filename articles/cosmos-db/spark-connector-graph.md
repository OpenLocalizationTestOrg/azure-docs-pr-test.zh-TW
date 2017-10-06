---
title: "Azure Cosmos DB︰使用 Spark 和 Apache TinkerPops Gremlin 執行圖表分析 | Microsoft Docs"
description: "本文提供在 Azure Cosmos DB 中使用 Spark 和 TinkerPop SparkGraphComputer 設定及執行圖形分析和平行計算的指引。"
services: cosmosdb
documentationcenter: 
author: khdang
manager: shireest
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: gremlin
ms.topic: article
ms.date: 06/05/2017
ms.author: khdang
ms.openlocfilehash: 0be5c9b12cdba4a428c809d00e1e68785a9ec1ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a>Azure Cosmos DB︰使用 Spark 和 Apache TinkerPop Gremlin 執行圖表分析

[Azure Cosmos DB](introduction.md)是 hello Microsoft 全域散發、 多模型資料庫服務。 您可以建立及查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是利用 Azure Cosmos DB hello 核心 hello 全域發佈和水平縮放功能。 Azure Cosmos DB 支援使用 [Apache TinkerPop Gremlin](graph-introduction.md) 的線上交易處理 (OLTP) 圖形工作負載。

[Spark](http://spark.apache.org/) 是著重於一般用途線上分析處理 (OLAP) 資料處理的 Apache Software Foundation 專案。 Spark 提供了混合中記憶體/磁碟為基礎分散式運算模型是類似 toohello Hadoop MapReduce 模型。 您可以使用來部署 hello 雲端中的 Apache Spark [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/)。

結合 Azure Cosmos DB 與 Spark，您可以使用 Gremlin 執行 OLTP 和 OLAP 工作負載。 快速入門本文示範如何 toorun Gremlin 查詢 Azure Cosmos DB Azure HDInsight Spark 叢集上。

## <a name="prerequisites"></a>必要條件

您可以執行此範例之前，您必須擁有下列必要條件 hello:
* Azure HDInsight Spark 叢集 2.0
* JDK 1.8+ (如果您沒有 JDK，則執行 `apt-get install default-jdk`。)
* Maven (如果您沒有 Maven，則執行 `apt-get install maven`。)
* Azure 訂用帳戶 ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])

如需有關資訊 tooset Azure HDInsight Spark 叢集，請參閱[佈建的 HDInsight 叢集](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md)。

## <a name="create-an-azure-cosmos-db-database-account"></a>建立 Azure Cosmos DB 資料庫帳戶

首先，建立資料庫帳戶以 hello Graph API，藉由下列 hello:

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>新增集合

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a>取得 Apache TinkerPop

取得 Apache TinkerPop 執行 hello 下列：

1. 遠端 toohello 的 hello HDInsight 叢集的主要節點`ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`。

2. 複製 hello TinkerPop3 來源程式碼、 在本機建置它，再安裝 tooMaven 快取。

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. 安裝 hello Spark Gremlin 外掛程式 

    a. Grape 會處理 hello hello 外掛程式安裝。 才能下載外掛程式 hello 和其相依性，請填入 Grape hello 儲存機制資訊。 

      建立 hello 葡萄組態檔，如果不存在於`~/.groovy/grapeConfig.xml`。 使用下列設定的 hello:

    ```xml
    <ivysettings>
    <settings defaultResolver="downloadGrapes"/>
    <resolvers>
        <chain name="downloadGrapes">
        <filesystem name="cachedGrapes">
            <ivy pattern="${user.home}/.groovy/grapes/[organisation]/[module]/ivy-[revision].xml"/>
            <artifact pattern="${user.home}/.groovy/grapes/[organisation]/[module]/[type]s/[artifact]-[revision].[ext]"/>
        </filesystem>
        <ibiblio name="codehaus" root="http://repository.codehaus.org/" m2compatible="true"/>
        <ibiblio name="central" root="http://central.maven.org/maven2/" m2compatible="true"/>
        <ibiblio name="jitpack" root="https://jitpack.io" m2compatible="true"/>
        <ibiblio name="java.net2" root="http://download.java.net/maven/2/" m2compatible="true"/>
        <ibiblio name="apache-snapshots" root="http://repository.apache.org/snapshots/" m2compatible="true"/>
        <ibiblio name="local" root="file:${user.home}/.m2/repository/" m2compatible="true"/>
        </chain>
    </resolvers>
    </ivysettings>
    ``` 

    b. 啟動 Gremlin 主控台 `bin/gremlin.sh`。
        
    c. 安裝版本與 hello Spark Gremlin 外掛程式 3.3.0-SNAPSHOT，建置於 hello 先前步驟中：

    ```bash
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :install org.apache.tinkerpop spark-gremlin 3.3.0-SNAPSHOT
    ==>loaded: [org.apache.tinkerpop, spark-gremlin, 3.3.0-SNAPSHOT] - restart hello console toouse [tinkerpop.spark]
    gremlin> :q
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :plugin use tinkerpop.spark
    ==>tinkerpop.spark activated
    ```

4. 是否檢查 toosee`Hadoop-Gremlin`會啟動`:plugin list`。 停用此外掛程式，因為它可能會干擾 hello Spark Gremlin 外掛程式`:plugin unuse tinkerpop.hadoop`。

## <a name="prepare-tinkerpop3-dependencies"></a>準備 TinkerPop3 相依性

當您建置 TinkerPop3 hello 上一個步驟中時，hello 程序也會提取所有 jar 相依性 Spark 和 Hadoop hello 目標目錄中。 使用 hello （每，這些瓶），與 HDI，已預先安裝和提取中其他相依性只在必要時。

1. 移 toohello Gremlin 主控台目標目錄在`tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`。 

2. 移動下的所有 （每瓶）`ext/`太`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`。

3. 移除所有 jar 程式庫之下`lib/`，不能在 hello 下列清單：

    ```bash
    # TinkerPop3
    gremlin-console-3.3.0-SNAPSHOT.jar
    gremlin-core-3.3.0-SNAPSHOT.jar       
    gremlin-groovy-3.3.0-SNAPSHOT.jar     
    gremlin-shaded-3.3.0-SNAPSHOT.jar     
    hadoop-gremlin-3.3.0-SNAPSHOT.jar     
    spark-gremlin-3.3.0-SNAPSHOT.jar      
    tinkergraph-gremlin-3.3.0-SNAPSHOT.jar

    # Gremlin depedencies
    asm-3.2.jar                                
    avro-1.7.4.jar                             
    caffeine-2.3.1.jar                         
    cglib-2.2.1-v20090111.jar                  
    gbench-0.4.3-groovy-2.4.jar                
    gprof-0.3.1-groovy-2.4.jar                 
    groovy-2.4.9-indy.jar                      
    groovy-2.4.9.jar                           
    groovy-console-2.4.9.jar                   
    groovy-groovysh-2.4.9-indy.jar             
    groovy-json-2.4.9-indy.jar                 
    groovy-jsr223-2.4.9-indy.jar               
    groovy-sql-2.4.9-indy.jar                  
    groovy-swing-2.4.9.jar                     
    groovy-templates-2.4.9.jar                 
    groovy-xml-2.4.9.jar                       
    hadoop-yarn-server-nodemanager-2.7.2.jar   
    hppc-0.7.1.jar                             
    javatuples-1.2.jar                         
    jaxb-impl-2.2.3-1.jar                      
    jbcrypt-0.4.jar                            
    jcabi-log-0.14.jar                         
    jcabi-manifests-1.1.jar                    
    jersey-core-1.9.jar                        
    jersey-guice-1.9.jar                       
    jersey-json-1.9.jar                        
    jettison-1.1.jar                           
    scalatest_2.11-2.2.6.jar                   
    servlet-api-2.5.jar                        
    snakeyaml-1.15.jar                         
    unused-1.0.0.jar                           
    xml-apis-1.3.04.jar                        
    ```

## <a name="get-hello-azure-cosmos-db-spark-connector"></a>取得 hello Azure Cosmos DB Spark 連接器

1. 取得 hello Azure Cosmos DB Spark 連接器`azure-documentdb-spark-0.0.3-SNAPSHOT.jar`和 Cosmos DB Java SDK`azure-documentdb-1.10.0.jar`從[Azure Cosmos DB GitHub 上的 Spark 連接器](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11)。

2. 或者，您可以在本機建置它。 因為 hello 最新版的 Spark Gremlin Spark 1.6.1 在已建立，而且不與 Spark 2.0.2，目前 hello Azure Cosmos DB Spark 連接器中使用，您可以建置 hello 最新 TinkerPop3 程式碼，並手動安裝 hello （每瓶）。 請勿 hello 遵循：

    a. 複製 hello Azure Cosmos DB Spark 連接器。

    b. 建置 TinkerPop3 (已在先前步驟中完成)。 在本機安裝所有 TinkerPop 3.3.0-SNAPSHOT jar。

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    c. 更新`tinkerpop.version``azure-documentdb-spark/pom.xml`太`3.3.0-SNAPSHOT`。
    
    d. 使用 Maven 建置。 hello 需要 （每瓶） 會放在`target`和`target/alternateLocation`。

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. 複製 hello 先前所述在 （每瓶） tooa 本機目錄 ~ / azure-documentdb-spark:

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-hello-dependencies-toohello-spark-worker-nodes"></a>發佈 hello 相依性 toohello Spark 背景工作節點 

1. 因為圖形資料的 hello 轉換取決於 TinkerPop3，您必須將發佈 hello 相關相依性 tooall Spark 背景工作節點。

2. 複製 hello 先前提到 Gremlin 相依性、 hello CosmosDB Spark 連接器 jar 和 CosmosDB Java SDK toohello 背景工作節點執行 hello 下列動作：

    a. 複製所有 hello （每瓶） 到`~/azure-documentdb-spark`。

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    b. 取得所有 Spark 背景工作節點，您可以在 hello Ambari 儀表板 上找到的 hello 清單`Spark2 Clients`列入 hello `Spark2` > 一節。

    c. 將複製 hello 節點的該目錄 tooeach。

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-hello-environment-variables"></a>設定 hello 環境變數

1. 尋找 hello Spark 叢集 hello HDP 版本。 它是 hello 目錄名稱下的`/usr/hdp/`(例如，2.5.4.2-7)。

2. 設定所有節點的 hdp.version。 Ambari 儀表板 移過**YARN 區段** > **Configs** > **進階**，並執行再 hello 遵循： 
 
    a. 在`Custom yarn-site`，加入新屬性`hdp.version`與 hello hello 主要節點上的 hello HDP 版本值。 
     
    b. 儲存 hello 的組態。 出現警告，您可以忽略。 
     
    c. 重新啟動 hello YARN 和 Oozie 服務因為 hello 通知圖示表示。

3. 下列環境變數 （取代為適當的 hello 值） hello 主要節點上設定 hello:

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-hello-graph-configuration"></a>準備 hello 圖形組態

1. 建立組態檔以 hello Azure Cosmos DB 連接參數和二手設定，然後放在`tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`。

    ```
    gremlin.graph=org.apache.tinkerpop.gremlin.hadoop.structure.HadoopGraph
    gremlin.hadoop.jarsInDistributedCache=true
    gremlin.hadoop.defaultGraphComputer=org.apache.tinkerpop.gremlin.spark.process.computer.SparkGraphComputer

    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    gremlin.hadoop.graphWriter=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBOutputRDD

    ####################################
    # SparkGraphComputer Configuration #
    ####################################
    spark.master=yarn
    spark.executor.memory=3g
    spark.executor.instances=6
    spark.serializer=org.apache.spark.serializer.KryoSerializer
    spark.kryo.registrator=org.apache.tinkerpop.gremlin.spark.structure.io.gryo.GryoRegistrator
    gremlin.spark.persistContext=true

    # Classpath for hello driver and executors
    spark.driver.extraClassPath=/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    spark.executor.extraClassPath=/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    
    ######################################
    # DocumentDB Spark connector         #
    ######################################
    spark.documentdb.connectionMode=Gateway
    spark.documentdb.schema_samplingratio=1.0
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    spark.documentdb.preferredRegions=FILLIN
    ```

2. 更新 hello`spark.driver.extraClassPath`和`spark.executor.extraClassPath`hello （每，這些瓶），在此情況下在 hello 先前步驟中，分散式 tooinclude hello 目錄`/home/sshuser/azure-documentdb-spark/*`。

3. 提供 hello Azure Cosmos 資料庫的下列詳細資料：

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-hello-tinkerpop-graph-and-save-it-tooazure-cosmos-db"></a>載入 hello TinkerPop 圖形，並將它儲存 tooAzure Cosmos DB
toodemonstrate toopersist 圖形到 Azure Cosmos DB，此範例中使用 hello TinkerPop 預先 TinkerPop 現代圖形的定義。 hello 圖形是 Kryo 格式儲存，並且提供 hello TinkerPop 儲存機制中。

1. 因為您執行 Gremlin YARN 模式中，您必須提供 hello 圖形資料 hello Hadoop 檔案系統中。 使用 hello 下列命令 toomake 目錄複製 hello 本機圖形檔到其中。 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. 暫時更新 hello`gremlin-spark.properties`檔案 toouse `GryoInputFormat` tooread hello 圖形。 也表示`inputLocation`hello 目錄為您建立，如 hello 下列所示：

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. 啟動 Gremlin 主控台，然後建立下列計算步驟 toopersist 資料 toohello 設定 Azure Cosmos DB 收集 hello:  

    a. 建立 hello 圖形`graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`。

    b. 使用 SparkGraphComputer 寫入 `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`。

    ```bash
    gremlin> graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")
    ==>hadoopgraph[gryoinputformat->documentdboutputrdd]
    gremlin> hg = graph.
                compute(SparkGraphComputer.class).
                result(GraphComputer.ResultGraph.NEW).
                persist(GraphComputer.Persist.EDGES).
                program(TraversalVertexProgram.build().
                    traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)), "gremlin-groovy", "g.V()").
                    create(graph)).
                submit().
                get() 
    ==>result[hadoopgraph[documentdbinputrdd->documentdboutputrdd],memory[size:1]]
    ```

4. 從資料總管 中，您可以確認資料已該 hello 保存 tooAzure Cosmos DB。

## <a name="load-hello-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a>從 Azure Cosmos DB，載入 hello 圖形，並執行 Gremlin 查詢

1. tooload hello 圖形中，編輯`gremlin-spark.properties`tooset`graphReader`太`DocumentDBInputRDD`:

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. 負載 hello 圖形周遊 hello 資料及 Gremlin 查詢與它執行動作來執行 hello 下列：

    a. 啟動 hello Gremlin 主控台`bin/gremlin.sh`。

    b. Hello 組態建立 hello 圖形`graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`。

    c. 使用 SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)` 建立圖形周遊。

    d. 執行下列 Gremlin graph 查詢 hello:

    ```bash
    gremlin> graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")
    ==>hadoopgraph[documentdbinputrdd->documentdboutputrdd]
    gremlin> g = graph.traversal().withComputer(SparkGraphComputer)
    ==>graphtraversalsource[hadoopgraph[documentdbinputrdd->documentdboutputrdd], sparkgraphcomputer]
    gremlin> g.V().count()
    ==>6
    gremlin> g.E().count()
    ==>6
    gremlin> g.V(1).out().values('name')
    ==>josh
    ==>vadas
    ==>lop
    gremlin> g.V().hasLabel('person').coalesce(values('nickname'), values('name'))
    ==>josh
    ==>peter
    ==>vadas
    ==>marko
    gremlin> g.V().hasLabel('person').
            choose(values('name')).
                option('marko', values('age')).
                option('josh', values('name')).
                option('vadas', valueMap()).
                option('peter', label())
    ==>josh
    ==>person
    ==>[name:[vadas],age:[27]]
    ==>29
    ```

> [!NOTE]
> toosee 詳細記錄 設定中的 hello 記錄層級`conf/log4j-console.properties`tooa 更多詳細資料層級。
>

## <a name="next-steps"></a>後續步驟

快速入門本文中，您已經學會如何與 toowork 圖形結合 Azure Cosmos DB 和 Spark。

> [!div class="nextstepaction"]
