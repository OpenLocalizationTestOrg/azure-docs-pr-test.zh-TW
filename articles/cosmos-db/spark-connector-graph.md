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
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a><span data-ttu-id="922ff-103">Azure Cosmos DB︰使用 Spark 和 Apache TinkerPop Gremlin 執行圖表分析</span><span class="sxs-lookup"><span data-stu-id="922ff-103">Azure Cosmos DB: Perform graph analytics by using Spark and Apache TinkerPop Gremlin</span></span>

<span data-ttu-id="922ff-104">[Azure Cosmos DB](introduction.md)是 hello Microsoft 全域散發、 多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="922ff-104">[Azure Cosmos DB](introduction.md) is hello globally distributed, multi-model database service from Microsoft.</span></span> <span data-ttu-id="922ff-105">您可以建立及查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是利用 Azure Cosmos DB hello 核心 hello 全域發佈和水平縮放功能。</span><span class="sxs-lookup"><span data-stu-id="922ff-105">You can create and query document, key/value, and graph databases, all of which benefit from hello global-distribution and horizontal-scale capabilities at hello core of Azure Cosmos DB.</span></span> <span data-ttu-id="922ff-106">Azure Cosmos DB 支援使用 [Apache TinkerPop Gremlin](graph-introduction.md) 的線上交易處理 (OLTP) 圖形工作負載。</span><span class="sxs-lookup"><span data-stu-id="922ff-106">Azure Cosmos DB supports online transaction processing (OLTP) graph workloads that use [Apache TinkerPop Gremlin](graph-introduction.md).</span></span>

<span data-ttu-id="922ff-107">[Spark](http://spark.apache.org/) 是著重於一般用途線上分析處理 (OLAP) 資料處理的 Apache Software Foundation 專案。</span><span class="sxs-lookup"><span data-stu-id="922ff-107">[Spark](http://spark.apache.org/) is an Apache Software Foundation project that's focused on general-purpose online analytical processing (OLAP) data processing.</span></span> <span data-ttu-id="922ff-108">Spark 提供了混合中記憶體/磁碟為基礎分散式運算模型是類似 toohello Hadoop MapReduce 模型。</span><span class="sxs-lookup"><span data-stu-id="922ff-108">Spark provides a hybrid in-memory/disk-based distributed computing model that is similar toohello Hadoop MapReduce model.</span></span> <span data-ttu-id="922ff-109">您可以使用來部署 hello 雲端中的 Apache Spark [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/)。</span><span class="sxs-lookup"><span data-stu-id="922ff-109">You can deploy Apache Spark in hello cloud by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="922ff-110">結合 Azure Cosmos DB 與 Spark，您可以使用 Gremlin 執行 OLTP 和 OLAP 工作負載。</span><span class="sxs-lookup"><span data-stu-id="922ff-110">By combining Azure Cosmos DB and Spark, you can perform both OLTP and OLAP workloads when you use Gremlin.</span></span> <span data-ttu-id="922ff-111">快速入門本文示範如何 toorun Gremlin 查詢 Azure Cosmos DB Azure HDInsight Spark 叢集上。</span><span class="sxs-lookup"><span data-stu-id="922ff-111">This quick-start article demonstrates how toorun Gremlin queries against Azure Cosmos DB on an Azure HDInsight Spark cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="922ff-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="922ff-112">Prerequisites</span></span>

<span data-ttu-id="922ff-113">您可以執行此範例之前，您必須擁有下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="922ff-113">Before you can run this sample, you must have hello following prerequisites:</span></span>
* <span data-ttu-id="922ff-114">Azure HDInsight Spark 叢集 2.0</span><span class="sxs-lookup"><span data-stu-id="922ff-114">Azure HDInsight Spark cluster 2.0</span></span>
* <span data-ttu-id="922ff-115">JDK 1.8+ (如果您沒有 JDK，則執行 `apt-get install default-jdk`。)</span><span class="sxs-lookup"><span data-stu-id="922ff-115">JDK 1.8+ (If you don't have JDK, run `apt-get install default-jdk`.)</span></span>
* <span data-ttu-id="922ff-116">Maven (如果您沒有 Maven，則執行 `apt-get install maven`。)</span><span class="sxs-lookup"><span data-stu-id="922ff-116">Maven (If you don't have Maven, run `apt-get install maven`.)</span></span>
* <span data-ttu-id="922ff-117">Azure 訂用帳戶 ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span><span class="sxs-lookup"><span data-stu-id="922ff-117">An Azure subscription ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span></span>

<span data-ttu-id="922ff-118">如需有關資訊 tooset Azure HDInsight Spark 叢集，請參閱[佈建的 HDInsight 叢集](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="922ff-118">For information about how tooset up an Azure HDInsight Spark cluster, see [Provisioning HDInsight clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="922ff-119">建立 Azure Cosmos DB 資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="922ff-119">Create an Azure Cosmos DB database account</span></span>

<span data-ttu-id="922ff-120">首先，建立資料庫帳戶以 hello Graph API，藉由下列 hello:</span><span class="sxs-lookup"><span data-stu-id="922ff-120">First, create a database account with hello Graph API by doing hello following:</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="922ff-121">新增集合</span><span class="sxs-lookup"><span data-stu-id="922ff-121">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a><span data-ttu-id="922ff-122">取得 Apache TinkerPop</span><span class="sxs-lookup"><span data-stu-id="922ff-122">Get Apache TinkerPop</span></span>

<span data-ttu-id="922ff-123">取得 Apache TinkerPop 執行 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="922ff-123">Get Apache TinkerPop by doing hello following:</span></span>

1. <span data-ttu-id="922ff-124">遠端 toohello 的 hello HDInsight 叢集的主要節點`ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`。</span><span class="sxs-lookup"><span data-stu-id="922ff-124">Remote toohello master node of hello HDInsight cluster `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span></span>

2. <span data-ttu-id="922ff-125">複製 hello TinkerPop3 來源程式碼、 在本機建置它，再安裝 tooMaven 快取。</span><span class="sxs-lookup"><span data-stu-id="922ff-125">Clone hello TinkerPop3 source code, build it locally, and install it tooMaven cache.</span></span>

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. <span data-ttu-id="922ff-126">安裝 hello Spark Gremlin 外掛程式</span><span class="sxs-lookup"><span data-stu-id="922ff-126">Install hello Spark-Gremlin plug-in</span></span> 

    <span data-ttu-id="922ff-127">a.</span><span class="sxs-lookup"><span data-stu-id="922ff-127">a.</span></span> <span data-ttu-id="922ff-128">Grape 會處理 hello hello 外掛程式安裝。</span><span class="sxs-lookup"><span data-stu-id="922ff-128">hello installation of hello plug-in is handled by Grape.</span></span> <span data-ttu-id="922ff-129">才能下載外掛程式 hello 和其相依性，請填入 Grape hello 儲存機制資訊。</span><span class="sxs-lookup"><span data-stu-id="922ff-129">Populate hello repositories information for Grape so it can download hello plug-in and its dependencies.</span></span> 

      <span data-ttu-id="922ff-130">建立 hello 葡萄組態檔，如果不存在於`~/.groovy/grapeConfig.xml`。</span><span class="sxs-lookup"><span data-stu-id="922ff-130">Create hello grape configuration file if it's not present at `~/.groovy/grapeConfig.xml`.</span></span> <span data-ttu-id="922ff-131">使用下列設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="922ff-131">Use hello following settings:</span></span>

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

    <span data-ttu-id="922ff-132">b.</span><span class="sxs-lookup"><span data-stu-id="922ff-132">b.</span></span> <span data-ttu-id="922ff-133">啟動 Gremlin 主控台 `bin/gremlin.sh`。</span><span class="sxs-lookup"><span data-stu-id="922ff-133">Start Gremlin console `bin/gremlin.sh`.</span></span>
        
    <span data-ttu-id="922ff-134">c.</span><span class="sxs-lookup"><span data-stu-id="922ff-134">c.</span></span> <span data-ttu-id="922ff-135">安裝版本與 hello Spark Gremlin 外掛程式 3.3.0-SNAPSHOT，建置於 hello 先前步驟中：</span><span class="sxs-lookup"><span data-stu-id="922ff-135">Install hello Spark-Gremlin plug-in with version 3.3.0-SNAPSHOT, which you built in hello previous steps:</span></span>

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

4. <span data-ttu-id="922ff-136">是否檢查 toosee`Hadoop-Gremlin`會啟動`:plugin list`。</span><span class="sxs-lookup"><span data-stu-id="922ff-136">Check toosee whether `Hadoop-Gremlin` is activated with `:plugin list`.</span></span> <span data-ttu-id="922ff-137">停用此外掛程式，因為它可能會干擾 hello Spark Gremlin 外掛程式`:plugin unuse tinkerpop.hadoop`。</span><span class="sxs-lookup"><span data-stu-id="922ff-137">Disable this plug-in, because it could interfere with hello Spark-Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.</span></span>

## <a name="prepare-tinkerpop3-dependencies"></a><span data-ttu-id="922ff-138">準備 TinkerPop3 相依性</span><span class="sxs-lookup"><span data-stu-id="922ff-138">Prepare TinkerPop3 dependencies</span></span>

<span data-ttu-id="922ff-139">當您建置 TinkerPop3 hello 上一個步驟中時，hello 程序也會提取所有 jar 相依性 Spark 和 Hadoop hello 目標目錄中。</span><span class="sxs-lookup"><span data-stu-id="922ff-139">When you built TinkerPop3 in hello previous step, hello process also pulled all jar dependencies for Spark and Hadoop in hello target directory.</span></span> <span data-ttu-id="922ff-140">使用 hello （每，這些瓶），與 HDI，已預先安裝和提取中其他相依性只在必要時。</span><span class="sxs-lookup"><span data-stu-id="922ff-140">Use hello jars that are pre-installed with HDI, and pull in additional dependencies only as necessary.</span></span>

1. <span data-ttu-id="922ff-141">移 toohello Gremlin 主控台目標目錄在`tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`。</span><span class="sxs-lookup"><span data-stu-id="922ff-141">Go toohello Gremlin Console target directory at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span></span> 

2. <span data-ttu-id="922ff-142">移動下的所有 （每瓶）`ext/`太`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`。</span><span class="sxs-lookup"><span data-stu-id="922ff-142">Move all jars under `ext/` too`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span></span>

3. <span data-ttu-id="922ff-143">移除所有 jar 程式庫之下`lib/`，不能在 hello 下列清單：</span><span class="sxs-lookup"><span data-stu-id="922ff-143">Remove all jar libraries under `lib/` that are not in hello following list:</span></span>

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

## <a name="get-hello-azure-cosmos-db-spark-connector"></a><span data-ttu-id="922ff-144">取得 hello Azure Cosmos DB Spark 連接器</span><span class="sxs-lookup"><span data-stu-id="922ff-144">Get hello Azure Cosmos DB Spark connector</span></span>

1. <span data-ttu-id="922ff-145">取得 hello Azure Cosmos DB Spark 連接器`azure-documentdb-spark-0.0.3-SNAPSHOT.jar`和 Cosmos DB Java SDK`azure-documentdb-1.10.0.jar`從[Azure Cosmos DB GitHub 上的 Spark 連接器](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11)。</span><span class="sxs-lookup"><span data-stu-id="922ff-145">Get hello Azure Cosmos DB Spark connector `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` and Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` from [Azure Cosmos DB Spark Connector on GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span></span>

2. <span data-ttu-id="922ff-146">或者，您可以在本機建置它。</span><span class="sxs-lookup"><span data-stu-id="922ff-146">Alternatively, you can build it locally.</span></span> <span data-ttu-id="922ff-147">因為 hello 最新版的 Spark Gremlin Spark 1.6.1 在已建立，而且不與 Spark 2.0.2，目前 hello Azure Cosmos DB Spark 連接器中使用，您可以建置 hello 最新 TinkerPop3 程式碼，並手動安裝 hello （每瓶）。</span><span class="sxs-lookup"><span data-stu-id="922ff-147">Because hello latest version of Spark-Gremlin was built with Spark 1.6.1 and is not compatible with Spark 2.0.2, which is currently used in hello Azure Cosmos DB Spark connector, you can build hello latest TinkerPop3 code and install hello jars manually.</span></span> <span data-ttu-id="922ff-148">請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="922ff-148">Do hello following:</span></span>

    <span data-ttu-id="922ff-149">a.</span><span class="sxs-lookup"><span data-stu-id="922ff-149">a.</span></span> <span data-ttu-id="922ff-150">複製 hello Azure Cosmos DB Spark 連接器。</span><span class="sxs-lookup"><span data-stu-id="922ff-150">Clone hello Azure Cosmos DB Spark connector.</span></span>

    <span data-ttu-id="922ff-151">b.</span><span class="sxs-lookup"><span data-stu-id="922ff-151">b.</span></span> <span data-ttu-id="922ff-152">建置 TinkerPop3 (已在先前步驟中完成)。</span><span class="sxs-lookup"><span data-stu-id="922ff-152">Build TinkerPop3 (already done in previous steps).</span></span> <span data-ttu-id="922ff-153">在本機安裝所有 TinkerPop 3.3.0-SNAPSHOT jar。</span><span class="sxs-lookup"><span data-stu-id="922ff-153">Install all TinkerPop 3.3.0-SNAPSHOT jars locally.</span></span>

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    <span data-ttu-id="922ff-154">c.</span><span class="sxs-lookup"><span data-stu-id="922ff-154">c.</span></span> <span data-ttu-id="922ff-155">更新`tinkerpop.version``azure-documentdb-spark/pom.xml`太`3.3.0-SNAPSHOT`。</span><span class="sxs-lookup"><span data-stu-id="922ff-155">Update `tinkerpop.version` `azure-documentdb-spark/pom.xml` too`3.3.0-SNAPSHOT`.</span></span>
    
    <span data-ttu-id="922ff-156">d.</span><span class="sxs-lookup"><span data-stu-id="922ff-156">d.</span></span> <span data-ttu-id="922ff-157">使用 Maven 建置。</span><span class="sxs-lookup"><span data-stu-id="922ff-157">Build with Maven.</span></span> <span data-ttu-id="922ff-158">hello 需要 （每瓶） 會放在`target`和`target/alternateLocation`。</span><span class="sxs-lookup"><span data-stu-id="922ff-158">hello needed jars are placed in `target` and `target/alternateLocation`.</span></span>

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. <span data-ttu-id="922ff-159">複製 hello 先前所述在 （每瓶） tooa 本機目錄 ~ / azure-documentdb-spark:</span><span class="sxs-lookup"><span data-stu-id="922ff-159">Copy hello previously mentioned jars tooa local directory at ~/azure-documentdb-spark:</span></span>

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-hello-dependencies-toohello-spark-worker-nodes"></a><span data-ttu-id="922ff-160">發佈 hello 相依性 toohello Spark 背景工作節點</span><span class="sxs-lookup"><span data-stu-id="922ff-160">Distribute hello dependencies toohello Spark worker nodes</span></span> 

1. <span data-ttu-id="922ff-161">因為圖形資料的 hello 轉換取決於 TinkerPop3，您必須將發佈 hello 相關相依性 tooall Spark 背景工作節點。</span><span class="sxs-lookup"><span data-stu-id="922ff-161">Because hello transformation of graph data depends on TinkerPop3, you must distribute hello related dependencies tooall Spark worker nodes.</span></span>

2. <span data-ttu-id="922ff-162">複製 hello 先前提到 Gremlin 相依性、 hello CosmosDB Spark 連接器 jar 和 CosmosDB Java SDK toohello 背景工作節點執行 hello 下列動作：</span><span class="sxs-lookup"><span data-stu-id="922ff-162">Copy hello previously mentioned Gremlin dependencies, hello CosmosDB Spark connector jar, and CosmosDB Java SDK toohello worker nodes by doing hello following:</span></span>

    <span data-ttu-id="922ff-163">a.</span><span class="sxs-lookup"><span data-stu-id="922ff-163">a.</span></span> <span data-ttu-id="922ff-164">複製所有 hello （每瓶） 到`~/azure-documentdb-spark`。</span><span class="sxs-lookup"><span data-stu-id="922ff-164">Copy all hello jars into `~/azure-documentdb-spark`.</span></span>

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    <span data-ttu-id="922ff-165">b.</span><span class="sxs-lookup"><span data-stu-id="922ff-165">b.</span></span> <span data-ttu-id="922ff-166">取得所有 Spark 背景工作節點，您可以在 hello Ambari 儀表板 上找到的 hello 清單`Spark2 Clients`列入 hello `Spark2` > 一節。</span><span class="sxs-lookup"><span data-stu-id="922ff-166">Get hello list of all Spark worker nodes, which you can find on Ambari Dashboard, in hello `Spark2 Clients` list in hello `Spark2` section.</span></span>

    <span data-ttu-id="922ff-167">c.</span><span class="sxs-lookup"><span data-stu-id="922ff-167">c.</span></span> <span data-ttu-id="922ff-168">將複製 hello 節點的該目錄 tooeach。</span><span class="sxs-lookup"><span data-stu-id="922ff-168">Copy that directory tooeach of hello nodes.</span></span>

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-hello-environment-variables"></a><span data-ttu-id="922ff-169">設定 hello 環境變數</span><span class="sxs-lookup"><span data-stu-id="922ff-169">Set up hello environment variables</span></span>

1. <span data-ttu-id="922ff-170">尋找 hello Spark 叢集 hello HDP 版本。</span><span class="sxs-lookup"><span data-stu-id="922ff-170">Find hello HDP version of hello Spark cluster.</span></span> <span data-ttu-id="922ff-171">它是 hello 目錄名稱下的`/usr/hdp/`(例如，2.5.4.2-7)。</span><span class="sxs-lookup"><span data-stu-id="922ff-171">It is hello directory name under `/usr/hdp/` (for example, 2.5.4.2-7).</span></span>

2. <span data-ttu-id="922ff-172">設定所有節點的 hdp.version。</span><span class="sxs-lookup"><span data-stu-id="922ff-172">Set hdp.version for all nodes.</span></span> <span data-ttu-id="922ff-173">Ambari 儀表板 移過**YARN 區段** > **Configs** > **進階**，並執行再 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="922ff-173">In Ambari Dashboard, go too**YARN section** > **Configs** > **Advanced**, and then do hello following:</span></span> 
 
    <span data-ttu-id="922ff-174">a.</span><span class="sxs-lookup"><span data-stu-id="922ff-174">a.</span></span> <span data-ttu-id="922ff-175">在`Custom yarn-site`，加入新屬性`hdp.version`與 hello hello 主要節點上的 hello HDP 版本值。</span><span class="sxs-lookup"><span data-stu-id="922ff-175">In `Custom yarn-site`, add a new property `hdp.version` with hello value of hello HDP version on hello master node.</span></span> 
     
    <span data-ttu-id="922ff-176">b.</span><span class="sxs-lookup"><span data-stu-id="922ff-176">b.</span></span> <span data-ttu-id="922ff-177">儲存 hello 的組態。</span><span class="sxs-lookup"><span data-stu-id="922ff-177">Save hello configurations.</span></span> <span data-ttu-id="922ff-178">出現警告，您可以忽略。</span><span class="sxs-lookup"><span data-stu-id="922ff-178">There are warnings, which you can ignore.</span></span> 
     
    <span data-ttu-id="922ff-179">c.</span><span class="sxs-lookup"><span data-stu-id="922ff-179">c.</span></span> <span data-ttu-id="922ff-180">重新啟動 hello YARN 和 Oozie 服務因為 hello 通知圖示表示。</span><span class="sxs-lookup"><span data-stu-id="922ff-180">Restart hello YARN and Oozie services as hello notification icons indicate.</span></span>

3. <span data-ttu-id="922ff-181">下列環境變數 （取代為適當的 hello 值） hello 主要節點上設定 hello:</span><span class="sxs-lookup"><span data-stu-id="922ff-181">Set hello following environment variables on hello master node (replace hello values as appropriate):</span></span>

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-hello-graph-configuration"></a><span data-ttu-id="922ff-182">準備 hello 圖形組態</span><span class="sxs-lookup"><span data-stu-id="922ff-182">Prepare hello graph configuration</span></span>

1. <span data-ttu-id="922ff-183">建立組態檔以 hello Azure Cosmos DB 連接參數和二手設定，然後放在`tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`。</span><span class="sxs-lookup"><span data-stu-id="922ff-183">Create a configuration file with hello Azure Cosmos DB connection parameters and Spark settings, and put it at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span></span>

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

2. <span data-ttu-id="922ff-184">更新 hello`spark.driver.extraClassPath`和`spark.executor.extraClassPath`hello （每，這些瓶），在此情況下在 hello 先前步驟中，分散式 tooinclude hello 目錄`/home/sshuser/azure-documentdb-spark/*`。</span><span class="sxs-lookup"><span data-stu-id="922ff-184">Update hello `spark.driver.extraClassPath` and `spark.executor.extraClassPath` tooinclude hello directory of hello jars that you distributed in hello previous step, in this case `/home/sshuser/azure-documentdb-spark/*`.</span></span>

3. <span data-ttu-id="922ff-185">提供 hello Azure Cosmos 資料庫的下列詳細資料：</span><span class="sxs-lookup"><span data-stu-id="922ff-185">Provide hello following details for Azure Cosmos DB:</span></span>

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-hello-tinkerpop-graph-and-save-it-tooazure-cosmos-db"></a><span data-ttu-id="922ff-186">載入 hello TinkerPop 圖形，並將它儲存 tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="922ff-186">Load hello TinkerPop graph, and save it tooAzure Cosmos DB</span></span>
<span data-ttu-id="922ff-187">toodemonstrate toopersist 圖形到 Azure Cosmos DB，此範例中使用 hello TinkerPop 預先 TinkerPop 現代圖形的定義。</span><span class="sxs-lookup"><span data-stu-id="922ff-187">toodemonstrate how toopersist a graph into Azure Cosmos DB, this example uses hello TinkerPop predefined TinkerPop modern graph.</span></span> <span data-ttu-id="922ff-188">hello 圖形是 Kryo 格式儲存，並且提供 hello TinkerPop 儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="922ff-188">hello graph is stored in Kryo format, and it's provided in hello TinkerPop repository.</span></span>

1. <span data-ttu-id="922ff-189">因為您執行 Gremlin YARN 模式中，您必須提供 hello 圖形資料 hello Hadoop 檔案系統中。</span><span class="sxs-lookup"><span data-stu-id="922ff-189">Because you are running Gremlin in YARN mode, you must make hello graph data available in hello Hadoop file system.</span></span> <span data-ttu-id="922ff-190">使用 hello 下列命令 toomake 目錄複製 hello 本機圖形檔到其中。</span><span class="sxs-lookup"><span data-stu-id="922ff-190">Use hello following commands toomake a directory and copy hello local graph file into it.</span></span> 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. <span data-ttu-id="922ff-191">暫時更新 hello`gremlin-spark.properties`檔案 toouse `GryoInputFormat` tooread hello 圖形。</span><span class="sxs-lookup"><span data-stu-id="922ff-191">Temporarily update hello `gremlin-spark.properties` file toouse `GryoInputFormat` tooread hello graph.</span></span> <span data-ttu-id="922ff-192">也表示`inputLocation`hello 目錄為您建立，如 hello 下列所示：</span><span class="sxs-lookup"><span data-stu-id="922ff-192">Also indicate `inputLocation` as hello directory you create, as in hello following:</span></span>

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. <span data-ttu-id="922ff-193">啟動 Gremlin 主控台，然後建立下列計算步驟 toopersist 資料 toohello 設定 Azure Cosmos DB 收集 hello:</span><span class="sxs-lookup"><span data-stu-id="922ff-193">Start Gremlin Console, and then create hello following computation steps toopersist data toohello configured Azure Cosmos DB collection:</span></span>  

    <span data-ttu-id="922ff-194">a.</span><span class="sxs-lookup"><span data-stu-id="922ff-194">a.</span></span> <span data-ttu-id="922ff-195">建立 hello 圖形`graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`。</span><span class="sxs-lookup"><span data-stu-id="922ff-195">Create hello graph `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span></span>

    <span data-ttu-id="922ff-196">b.</span><span class="sxs-lookup"><span data-stu-id="922ff-196">b.</span></span> <span data-ttu-id="922ff-197">使用 SparkGraphComputer 寫入 `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`。</span><span class="sxs-lookup"><span data-stu-id="922ff-197">Use SparkGraphComputer for writing `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span></span>

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

4. <span data-ttu-id="922ff-198">從資料總管 中，您可以確認資料已該 hello 保存 tooAzure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="922ff-198">From Data Explorer, you can verify that hello data has been persisted tooAzure Cosmos DB.</span></span>

## <a name="load-hello-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a><span data-ttu-id="922ff-199">從 Azure Cosmos DB，載入 hello 圖形，並執行 Gremlin 查詢</span><span class="sxs-lookup"><span data-stu-id="922ff-199">Load hello graph from Azure Cosmos DB, and run Gremlin queries</span></span>

1. <span data-ttu-id="922ff-200">tooload hello 圖形中，編輯`gremlin-spark.properties`tooset`graphReader`太`DocumentDBInputRDD`:</span><span class="sxs-lookup"><span data-stu-id="922ff-200">tooload hello graph, edit `gremlin-spark.properties` tooset `graphReader` too`DocumentDBInputRDD`:</span></span>

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. <span data-ttu-id="922ff-201">負載 hello 圖形周遊 hello 資料及 Gremlin 查詢與它執行動作來執行 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="922ff-201">Load hello graph, traverse hello data, and run Gremlin queries with it by doing hello following:</span></span>

    <span data-ttu-id="922ff-202">a.</span><span class="sxs-lookup"><span data-stu-id="922ff-202">a.</span></span> <span data-ttu-id="922ff-203">啟動 hello Gremlin 主控台`bin/gremlin.sh`。</span><span class="sxs-lookup"><span data-stu-id="922ff-203">Start hello Gremlin Console `bin/gremlin.sh`.</span></span>

    <span data-ttu-id="922ff-204">b.</span><span class="sxs-lookup"><span data-stu-id="922ff-204">b.</span></span> <span data-ttu-id="922ff-205">Hello 組態建立 hello 圖形`graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`。</span><span class="sxs-lookup"><span data-stu-id="922ff-205">Create hello graph with hello configuration `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span></span>

    <span data-ttu-id="922ff-206">c.</span><span class="sxs-lookup"><span data-stu-id="922ff-206">c.</span></span> <span data-ttu-id="922ff-207">使用 SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)` 建立圖形周遊。</span><span class="sxs-lookup"><span data-stu-id="922ff-207">Create a graph traversal with SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span></span>

    <span data-ttu-id="922ff-208">d.</span><span class="sxs-lookup"><span data-stu-id="922ff-208">d.</span></span> <span data-ttu-id="922ff-209">執行下列 Gremlin graph 查詢 hello:</span><span class="sxs-lookup"><span data-stu-id="922ff-209">Run hello following Gremlin graph queries:</span></span>

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
> <span data-ttu-id="922ff-210">toosee 詳細記錄 設定中的 hello 記錄層級`conf/log4j-console.properties`tooa 更多詳細資料層級。</span><span class="sxs-lookup"><span data-stu-id="922ff-210">toosee more detailed logging, set hello log level in `conf/log4j-console.properties` tooa more verbose level.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="922ff-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="922ff-211">Next steps</span></span>

<span data-ttu-id="922ff-212">快速入門本文中，您已經學會如何與 toowork 圖形結合 Azure Cosmos DB 和 Spark。</span><span class="sxs-lookup"><span data-stu-id="922ff-212">In this quick-start article, you've learned how toowork with graphs by combining Azure Cosmos DB and Spark.</span></span>

> [!div class="nextstepaction"]
