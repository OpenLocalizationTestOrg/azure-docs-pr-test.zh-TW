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
ms.openlocfilehash: 27c4d945e418b130c68cfde845571eb93658101e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a><span data-ttu-id="64a6a-103">Azure Cosmos DB︰使用 Spark 和 Apache TinkerPop Gremlin 執行圖表分析</span><span class="sxs-lookup"><span data-stu-id="64a6a-103">Azure Cosmos DB: Perform graph analytics by using Spark and Apache TinkerPop Gremlin</span></span>

<span data-ttu-id="64a6a-104">[Azure Cosmos DB](introduction.md) 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="64a6a-104">[Azure Cosmos DB](introduction.md) is the globally distributed, multi-model database service from Microsoft.</span></span> <span data-ttu-id="64a6a-105">您可以建立及查詢文件、索引鍵/值及圖形資料庫，所有這些都受惠於位於 Azure Cosmos DB 核心的全域散發和水平調整功能。</span><span class="sxs-lookup"><span data-stu-id="64a6a-105">You can create and query document, key/value, and graph databases, all of which benefit from the global-distribution and horizontal-scale capabilities at the core of Azure Cosmos DB.</span></span> <span data-ttu-id="64a6a-106">Azure Cosmos DB 支援使用 [Apache TinkerPop Gremlin](graph-introduction.md) 的線上交易處理 (OLTP) 圖形工作負載。</span><span class="sxs-lookup"><span data-stu-id="64a6a-106">Azure Cosmos DB supports online transaction processing (OLTP) graph workloads that use [Apache TinkerPop Gremlin](graph-introduction.md).</span></span>

<span data-ttu-id="64a6a-107">[Spark](http://spark.apache.org/) 是著重於一般用途線上分析處理 (OLAP) 資料處理的 Apache Software Foundation 專案。</span><span class="sxs-lookup"><span data-stu-id="64a6a-107">[Spark](http://spark.apache.org/) is an Apache Software Foundation project that's focused on general-purpose online analytical processing (OLAP) data processing.</span></span> <span data-ttu-id="64a6a-108">Spark 會提供混合式記憶體內/磁碟型分散式運算模型，其類似於 Hadoop MapReduce 模型。</span><span class="sxs-lookup"><span data-stu-id="64a6a-108">Spark provides a hybrid in-memory/disk-based distributed computing model that is similar to the Hadoop MapReduce model.</span></span> <span data-ttu-id="64a6a-109">您可以使用 [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/) 在雲端部署 Apache Spark。</span><span class="sxs-lookup"><span data-stu-id="64a6a-109">You can deploy Apache Spark in the cloud by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="64a6a-110">結合 Azure Cosmos DB 與 Spark，您可以使用 Gremlin 執行 OLTP 和 OLAP 工作負載。</span><span class="sxs-lookup"><span data-stu-id="64a6a-110">By combining Azure Cosmos DB and Spark, you can perform both OLTP and OLAP workloads when you use Gremlin.</span></span> <span data-ttu-id="64a6a-111">本快速入門文章示範如何在 Azure HDInsight Spark 叢集上對 Azure Cosmos DB 執行 Gremlin 查詢。</span><span class="sxs-lookup"><span data-stu-id="64a6a-111">This quick-start article demonstrates how to run Gremlin queries against Azure Cosmos DB on an Azure HDInsight Spark cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64a6a-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="64a6a-112">Prerequisites</span></span>

<span data-ttu-id="64a6a-113">您必須具備下列必要條件，才能執行此範例：</span><span class="sxs-lookup"><span data-stu-id="64a6a-113">Before you can run this sample, you must have the following prerequisites:</span></span>
* <span data-ttu-id="64a6a-114">Azure HDInsight Spark 叢集 2.0</span><span class="sxs-lookup"><span data-stu-id="64a6a-114">Azure HDInsight Spark cluster 2.0</span></span>
* <span data-ttu-id="64a6a-115">JDK 1.8+ (如果您沒有 JDK，則執行 `apt-get install default-jdk`。)</span><span class="sxs-lookup"><span data-stu-id="64a6a-115">JDK 1.8+ (If you don't have JDK, run `apt-get install default-jdk`.)</span></span>
* <span data-ttu-id="64a6a-116">Maven (如果您沒有 Maven，則執行 `apt-get install maven`。)</span><span class="sxs-lookup"><span data-stu-id="64a6a-116">Maven (If you don't have Maven, run `apt-get install maven`.)</span></span>
* <span data-ttu-id="64a6a-117">Azure 訂用帳戶 ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span><span class="sxs-lookup"><span data-stu-id="64a6a-117">An Azure subscription ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span></span>

<span data-ttu-id="64a6a-118">如需有關如何設定 Azure HDInsight Spark 叢集的詳細資訊，請參閱[佈建 HDInsight 叢集](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="64a6a-118">For information about how to set up an Azure HDInsight Spark cluster, see [Provisioning HDInsight clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="64a6a-119">建立 Azure Cosmos DB 資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="64a6a-119">Create an Azure Cosmos DB database account</span></span>

<span data-ttu-id="64a6a-120">首先，執行下列動作以使用圖形 API 建立資料庫帳戶：</span><span class="sxs-lookup"><span data-stu-id="64a6a-120">First, create a database account with the Graph API by doing the following:</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="64a6a-121">新增集合</span><span class="sxs-lookup"><span data-stu-id="64a6a-121">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a><span data-ttu-id="64a6a-122">取得 Apache TinkerPop</span><span class="sxs-lookup"><span data-stu-id="64a6a-122">Get Apache TinkerPop</span></span>

<span data-ttu-id="64a6a-123">執行下列動作來取得 Apache TinkerPop：</span><span class="sxs-lookup"><span data-stu-id="64a6a-123">Get Apache TinkerPop by doing the following:</span></span>

1. <span data-ttu-id="64a6a-124">在 HDInsight 叢集 `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net` 的主要節點遠端。</span><span class="sxs-lookup"><span data-stu-id="64a6a-124">Remote to the master node of the HDInsight cluster `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span></span>

2. <span data-ttu-id="64a6a-125">複製 TinkerPop3 來源程式碼，在本機加以建置，並將它安裝至 Maven 快取。</span><span class="sxs-lookup"><span data-stu-id="64a6a-125">Clone the TinkerPop3 source code, build it locally, and install it to Maven cache.</span></span>

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. <span data-ttu-id="64a6a-126">安裝 Spark-Gremlin 外掛程式</span><span class="sxs-lookup"><span data-stu-id="64a6a-126">Install the Spark-Gremlin plug-in</span></span> 

    <span data-ttu-id="64a6a-127">a.</span><span class="sxs-lookup"><span data-stu-id="64a6a-127">a.</span></span> <span data-ttu-id="64a6a-128">此外掛程式的安裝是由 Grape 處理。</span><span class="sxs-lookup"><span data-stu-id="64a6a-128">The installation of the plug-in is handled by Grape.</span></span> <span data-ttu-id="64a6a-129">填入 Grape 的存放庫資訊，才能下載外掛程式和其相依性。</span><span class="sxs-lookup"><span data-stu-id="64a6a-129">Populate the repositories information for Grape so it can download the plug-in and its dependencies.</span></span> 

      <span data-ttu-id="64a6a-130">建立 Grape 組態檔 (如果它未顯示於 `~/.groovy/grapeConfig.xml`)。</span><span class="sxs-lookup"><span data-stu-id="64a6a-130">Create the grape configuration file if it's not present at `~/.groovy/grapeConfig.xml`.</span></span> <span data-ttu-id="64a6a-131">套用下列設定：</span><span class="sxs-lookup"><span data-stu-id="64a6a-131">Use the following settings:</span></span>

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

    <span data-ttu-id="64a6a-132">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="64a6a-132">b.</span></span> <span data-ttu-id="64a6a-133">啟動 Gremlin 主控台 `bin/gremlin.sh`。</span><span class="sxs-lookup"><span data-stu-id="64a6a-133">Start Gremlin console `bin/gremlin.sh`.</span></span>
        
    <span data-ttu-id="64a6a-134">c.</span><span class="sxs-lookup"><span data-stu-id="64a6a-134">c.</span></span> <span data-ttu-id="64a6a-135">使用您在先前步驟中建立的 3.3.0-SNAPSHOT 版來安裝 Spark-Gremlin 外掛程式：</span><span class="sxs-lookup"><span data-stu-id="64a6a-135">Install the Spark-Gremlin plug-in with version 3.3.0-SNAPSHOT, which you built in the previous steps:</span></span>

    ```bash
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :install org.apache.tinkerpop spark-gremlin 3.3.0-SNAPSHOT
    ==>loaded: [org.apache.tinkerpop, spark-gremlin, 3.3.0-SNAPSHOT] - restart the console to use [tinkerpop.spark]
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

4. <span data-ttu-id="64a6a-136">檢查 `Hadoop-Gremlin` 是否已啟動 `:plugin list`。</span><span class="sxs-lookup"><span data-stu-id="64a6a-136">Check to see whether `Hadoop-Gremlin` is activated with `:plugin list`.</span></span> <span data-ttu-id="64a6a-137">停用此外掛程式，因為它可能會干擾 Spark-Gremlin 外掛程式 `:plugin unuse tinkerpop.hadoop`。</span><span class="sxs-lookup"><span data-stu-id="64a6a-137">Disable this plug-in, because it could interfere with the Spark-Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.</span></span>

## <a name="prepare-tinkerpop3-dependencies"></a><span data-ttu-id="64a6a-138">準備 TinkerPop3 相依性</span><span class="sxs-lookup"><span data-stu-id="64a6a-138">Prepare TinkerPop3 dependencies</span></span>

<span data-ttu-id="64a6a-139">當您在上一個步驟中建置 TinkerPop3 時，處理序也會提取目標目錄中 Spark 與 Hadoop 的所有 jar 相依性。</span><span class="sxs-lookup"><span data-stu-id="64a6a-139">When you built TinkerPop3 in the previous step, the process also pulled all jar dependencies for Spark and Hadoop in the target directory.</span></span> <span data-ttu-id="64a6a-140">使用預先與 HDI 一起安裝的 jar，並視需要只提取其他相依性。</span><span class="sxs-lookup"><span data-stu-id="64a6a-140">Use the jars that are pre-installed with HDI, and pull in additional dependencies only as necessary.</span></span>

1. <span data-ttu-id="64a6a-141">移至位於 `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone` 的 Gremlin 主控台目標目錄。</span><span class="sxs-lookup"><span data-stu-id="64a6a-141">Go to the Gremlin Console target directory at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span></span> 

2. <span data-ttu-id="64a6a-142">將 `ext/` 之下的所有 jar 移至 `lib/`：`find ext/ -name '*.jar' -exec mv {} lib/ \;`。</span><span class="sxs-lookup"><span data-stu-id="64a6a-142">Move all jars under `ext/` to `lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span></span>

3. <span data-ttu-id="64a6a-143">移除 `lib/` 之下不在下列清單中的所有 jar 程式庫：</span><span class="sxs-lookup"><span data-stu-id="64a6a-143">Remove all jar libraries under `lib/` that are not in the following list:</span></span>

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

## <a name="get-the-azure-cosmos-db-spark-connector"></a><span data-ttu-id="64a6a-144">取得 Azure Cosmos DB Spark 連接器</span><span class="sxs-lookup"><span data-stu-id="64a6a-144">Get the Azure Cosmos DB Spark connector</span></span>

1. <span data-ttu-id="64a6a-145">從 [GitHub 上的 Azure Cosmos DB Spark 連接器](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11)，取得 Azure Cosmos DB Spark 連接器`azure-documentdb-spark-0.0.3-SNAPSHOT.jar` 和 Cosmos DB Java SDK `azure-documentdb-1.10.0.jar`。</span><span class="sxs-lookup"><span data-stu-id="64a6a-145">Get the Azure Cosmos DB Spark connector `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` and Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` from [Azure Cosmos DB Spark Connector on GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span></span>

2. <span data-ttu-id="64a6a-146">或者，您可以在本機建置它。</span><span class="sxs-lookup"><span data-stu-id="64a6a-146">Alternatively, you can build it locally.</span></span> <span data-ttu-id="64a6a-147">因為最新版的 Spark-Gremlin 是使用 Spark 1.6.1 建置，且與 Azure Cosmos DB Spark 連接器中目前使用的 Spark 2.0.2 不相容，您可以建置最新的 TinkerPop3 程式碼及手動安裝 jar。</span><span class="sxs-lookup"><span data-stu-id="64a6a-147">Because the latest version of Spark-Gremlin was built with Spark 1.6.1 and is not compatible with Spark 2.0.2, which is currently used in the Azure Cosmos DB Spark connector, you can build the latest TinkerPop3 code and install the jars manually.</span></span> <span data-ttu-id="64a6a-148">執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="64a6a-148">Do the following:</span></span>

    <span data-ttu-id="64a6a-149">a.</span><span class="sxs-lookup"><span data-stu-id="64a6a-149">a.</span></span> <span data-ttu-id="64a6a-150">複製 Azure Cosmos DB Spark 連接器。</span><span class="sxs-lookup"><span data-stu-id="64a6a-150">Clone the Azure Cosmos DB Spark connector.</span></span>

    <span data-ttu-id="64a6a-151">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="64a6a-151">b.</span></span> <span data-ttu-id="64a6a-152">建置 TinkerPop3 (已在先前步驟中完成)。</span><span class="sxs-lookup"><span data-stu-id="64a6a-152">Build TinkerPop3 (already done in previous steps).</span></span> <span data-ttu-id="64a6a-153">在本機安裝所有 TinkerPop 3.3.0-SNAPSHOT jar。</span><span class="sxs-lookup"><span data-stu-id="64a6a-153">Install all TinkerPop 3.3.0-SNAPSHOT jars locally.</span></span>

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    <span data-ttu-id="64a6a-154">c.</span><span class="sxs-lookup"><span data-stu-id="64a6a-154">c.</span></span> <span data-ttu-id="64a6a-155">將 `tinkerpop.version` `azure-documentdb-spark/pom.xml` 更新為 `3.3.0-SNAPSHOT`。</span><span class="sxs-lookup"><span data-stu-id="64a6a-155">Update `tinkerpop.version` `azure-documentdb-spark/pom.xml` to `3.3.0-SNAPSHOT`.</span></span>
    
    <span data-ttu-id="64a6a-156">d.</span><span class="sxs-lookup"><span data-stu-id="64a6a-156">d.</span></span> <span data-ttu-id="64a6a-157">使用 Maven 建置。</span><span class="sxs-lookup"><span data-stu-id="64a6a-157">Build with Maven.</span></span> <span data-ttu-id="64a6a-158">所需的 jar 都會置於 `target` 和 `target/alternateLocation` 中。</span><span class="sxs-lookup"><span data-stu-id="64a6a-158">The needed jars are placed in `target` and `target/alternateLocation`.</span></span>

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. <span data-ttu-id="64a6a-159">將先前所提的 jar 複製到本機目錄 (位於 ~/azure-documentdb-spark)：</span><span class="sxs-lookup"><span data-stu-id="64a6a-159">Copy the previously mentioned jars to a local directory at ~/azure-documentdb-spark:</span></span>

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-the-dependencies-to-the-spark-worker-nodes"></a><span data-ttu-id="64a6a-160">將相依性散發至 Spark 背景工作角色節點</span><span class="sxs-lookup"><span data-stu-id="64a6a-160">Distribute the dependencies to the Spark worker nodes</span></span> 

1. <span data-ttu-id="64a6a-161">因為圖形資料的轉換取決於 TinkerPop3，所以您必須將相關的相依性散發至所有 Spark 背景工作角色節點。</span><span class="sxs-lookup"><span data-stu-id="64a6a-161">Because the transformation of graph data depends on TinkerPop3, you must distribute the related dependencies to all Spark worker nodes.</span></span>

2. <span data-ttu-id="64a6a-162">執行下列動作，將先前所提的 Gremlin 相依性、CosmosDB Spark 連接器 jar 和 CosmosDB Java SDK 複製到背景工作節點：</span><span class="sxs-lookup"><span data-stu-id="64a6a-162">Copy the previously mentioned Gremlin dependencies, the CosmosDB Spark connector jar, and CosmosDB Java SDK to the worker nodes by doing the following:</span></span>

    <span data-ttu-id="64a6a-163">a.</span><span class="sxs-lookup"><span data-stu-id="64a6a-163">a.</span></span> <span data-ttu-id="64a6a-164">將所有 jar 複製到 `~/azure-documentdb-spark` 中。</span><span class="sxs-lookup"><span data-stu-id="64a6a-164">Copy all the jars into `~/azure-documentdb-spark`.</span></span>

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    <span data-ttu-id="64a6a-165">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="64a6a-165">b.</span></span> <span data-ttu-id="64a6a-166">在 `Spark2` 區段的 `Spark2 Clients` 清單中，取得所有 Spark 背景工作節點的清單 (您可以在 Ambari 儀表板上找到)。</span><span class="sxs-lookup"><span data-stu-id="64a6a-166">Get the list of all Spark worker nodes, which you can find on Ambari Dashboard, in the `Spark2 Clients` list in the `Spark2` section.</span></span>

    <span data-ttu-id="64a6a-167">c.</span><span class="sxs-lookup"><span data-stu-id="64a6a-167">c.</span></span> <span data-ttu-id="64a6a-168">將該目錄複製到每個節點。</span><span class="sxs-lookup"><span data-stu-id="64a6a-168">Copy that directory to each of the nodes.</span></span>

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-the-environment-variables"></a><span data-ttu-id="64a6a-169">設定環境變數</span><span class="sxs-lookup"><span data-stu-id="64a6a-169">Set up the environment variables</span></span>

1. <span data-ttu-id="64a6a-170">尋找 Spark 叢集的 HDP 版本。</span><span class="sxs-lookup"><span data-stu-id="64a6a-170">Find the HDP version of the Spark cluster.</span></span> <span data-ttu-id="64a6a-171">這是 `/usr/hdp/` 之下的目錄名稱 (例如 2.5.4.2-7)。</span><span class="sxs-lookup"><span data-stu-id="64a6a-171">It is the directory name under `/usr/hdp/` (for example, 2.5.4.2-7).</span></span>

2. <span data-ttu-id="64a6a-172">設定所有節點的 hdp.version。</span><span class="sxs-lookup"><span data-stu-id="64a6a-172">Set hdp.version for all nodes.</span></span> <span data-ttu-id="64a6a-173">在 Ambari 儀表板中，移至 **YARN 區段** > [設定] > [進階]，然後執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="64a6a-173">In Ambari Dashboard, go to **YARN section** > **Configs** > **Advanced**, and then do the following:</span></span> 
 
    <span data-ttu-id="64a6a-174">a.</span><span class="sxs-lookup"><span data-stu-id="64a6a-174">a.</span></span> <span data-ttu-id="64a6a-175">在 `Custom yarn-site` 中，於主要節點上新增一個屬性 `hdp.version`，其值為 HDP 版本。</span><span class="sxs-lookup"><span data-stu-id="64a6a-175">In `Custom yarn-site`, add a new property `hdp.version` with the value of the HDP version on the master node.</span></span> 
     
    <span data-ttu-id="64a6a-176">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="64a6a-176">b.</span></span> <span data-ttu-id="64a6a-177">儲存組態。</span><span class="sxs-lookup"><span data-stu-id="64a6a-177">Save the configurations.</span></span> <span data-ttu-id="64a6a-178">出現警告，您可以忽略。</span><span class="sxs-lookup"><span data-stu-id="64a6a-178">There are warnings, which you can ignore.</span></span> 
     
    <span data-ttu-id="64a6a-179">c.</span><span class="sxs-lookup"><span data-stu-id="64a6a-179">c.</span></span> <span data-ttu-id="64a6a-180">如通知圖示所指出，重新啟動 YARN 和 Oozie 服務。</span><span class="sxs-lookup"><span data-stu-id="64a6a-180">Restart the YARN and Oozie services as the notification icons indicate.</span></span>

3. <span data-ttu-id="64a6a-181">在主要節點上設定下列環境變數 (取代為適當的值)︰</span><span class="sxs-lookup"><span data-stu-id="64a6a-181">Set the following environment variables on the master node (replace the values as appropriate):</span></span>

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-the-graph-configuration"></a><span data-ttu-id="64a6a-182">準備圖形組態</span><span class="sxs-lookup"><span data-stu-id="64a6a-182">Prepare the graph configuration</span></span>

1. <span data-ttu-id="64a6a-183">使用 Azure Cosmos DB 連線參數和 Spark 設定來建立組態檔，並將它放在 `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`。</span><span class="sxs-lookup"><span data-stu-id="64a6a-183">Create a configuration file with the Azure Cosmos DB connection parameters and Spark settings, and put it at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span></span>

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

    # Classpath for the driver and executors
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

2. <span data-ttu-id="64a6a-184">更新 `spark.driver.extraClassPath` 和 `spark.executor.extraClassPath` 以包含您在上一個步驟中散發之 jar 的目錄，在此例中為 `/home/sshuser/azure-documentdb-spark/*`。</span><span class="sxs-lookup"><span data-stu-id="64a6a-184">Update the `spark.driver.extraClassPath` and `spark.executor.extraClassPath` to include the directory of the jars that you distributed in the previous step, in this case `/home/sshuser/azure-documentdb-spark/*`.</span></span>

3. <span data-ttu-id="64a6a-185">提供 Azure Cosmos DB 的下列詳細資料︰</span><span class="sxs-lookup"><span data-stu-id="64a6a-185">Provide the following details for Azure Cosmos DB:</span></span>

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-the-tinkerpop-graph-and-save-it-to-azure-cosmos-db"></a><span data-ttu-id="64a6a-186">載入 TinkerPop 圖形，然後將它儲存到 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="64a6a-186">Load the TinkerPop graph, and save it to Azure Cosmos DB</span></span>
<span data-ttu-id="64a6a-187">為了示範如何將圖形保存在 Azure Cosmos DB 中，此範例使用 TinkerPop 預先定義的 TinkerPop 新式圖形。</span><span class="sxs-lookup"><span data-stu-id="64a6a-187">To demonstrate how to persist a graph into Azure Cosmos DB, this example uses the TinkerPop predefined TinkerPop modern graph.</span></span> <span data-ttu-id="64a6a-188">此圖形是以 Kryo 格式儲存，並且在 TinkerPop 存放庫中提供。</span><span class="sxs-lookup"><span data-stu-id="64a6a-188">The graph is stored in Kryo format, and it's provided in the TinkerPop repository.</span></span>

1. <span data-ttu-id="64a6a-189">因為您是以 YARN 模式執行 Gremlin，所以您必須在 Hadoop 檔案系統中提供圖形資料。</span><span class="sxs-lookup"><span data-stu-id="64a6a-189">Because you are running Gremlin in YARN mode, you must make the graph data available in the Hadoop file system.</span></span> <span data-ttu-id="64a6a-190">使用下列命令建立一個目錄，並將本機圖形檔案複製到其中。</span><span class="sxs-lookup"><span data-stu-id="64a6a-190">Use the following commands to make a directory and copy the local graph file into it.</span></span> 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. <span data-ttu-id="64a6a-191">暫時更新 `gremlin-spark.properties` 檔案，以使用 `GryoInputFormat` 讀取圖形。</span><span class="sxs-lookup"><span data-stu-id="64a6a-191">Temporarily update the `gremlin-spark.properties` file to use `GryoInputFormat` to read the graph.</span></span> <span data-ttu-id="64a6a-192">此外，指定 `inputLocation` 作為您建立的目錄，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="64a6a-192">Also indicate `inputLocation` as the directory you create, as in the following:</span></span>

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. <span data-ttu-id="64a6a-193">啟動 Gremlin 主控台，然後建立下列計算步驟，將資料保留於已設定的 Azure Cosmos DB 集合︰</span><span class="sxs-lookup"><span data-stu-id="64a6a-193">Start Gremlin Console, and then create the following computation steps to persist data to the configured Azure Cosmos DB collection:</span></span>  

    <span data-ttu-id="64a6a-194">a.</span><span class="sxs-lookup"><span data-stu-id="64a6a-194">a.</span></span> <span data-ttu-id="64a6a-195">建立圖形 `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`。</span><span class="sxs-lookup"><span data-stu-id="64a6a-195">Create the graph `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span></span>

    <span data-ttu-id="64a6a-196">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="64a6a-196">b.</span></span> <span data-ttu-id="64a6a-197">使用 SparkGraphComputer 寫入 `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`。</span><span class="sxs-lookup"><span data-stu-id="64a6a-197">Use SparkGraphComputer for writing `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span></span>

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

4. <span data-ttu-id="64a6a-198">在資料總管中，您可以確認資料已保存至 Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="64a6a-198">From Data Explorer, you can verify that the data has been persisted to Azure Cosmos DB.</span></span>

## <a name="load-the-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a><span data-ttu-id="64a6a-199">從 Azure Cosmos DB 載入圖形，然後執行 Gremlin 查詢</span><span class="sxs-lookup"><span data-stu-id="64a6a-199">Load the graph from Azure Cosmos DB, and run Gremlin queries</span></span>

1. <span data-ttu-id="64a6a-200">若要載入圖形，請編輯 `gremlin-spark.properties` 以將 `graphReader` 設定為 `DocumentDBInputRDD`：</span><span class="sxs-lookup"><span data-stu-id="64a6a-200">To load the graph, edit `gremlin-spark.properties` to set `graphReader` to `DocumentDBInputRDD`:</span></span>

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. <span data-ttu-id="64a6a-201">執行下列動作，載入圖形、周遊資料，以及執行 Gremlin 查詢︰</span><span class="sxs-lookup"><span data-stu-id="64a6a-201">Load the graph, traverse the data, and run Gremlin queries with it by doing the following:</span></span>

    <span data-ttu-id="64a6a-202">a.</span><span class="sxs-lookup"><span data-stu-id="64a6a-202">a.</span></span> <span data-ttu-id="64a6a-203">啟動 Gremlin 主控台 `bin/gremlin.sh`。</span><span class="sxs-lookup"><span data-stu-id="64a6a-203">Start the Gremlin Console `bin/gremlin.sh`.</span></span>

    <span data-ttu-id="64a6a-204">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="64a6a-204">b.</span></span> <span data-ttu-id="64a6a-205">使用組態 `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')` 建立圖形。</span><span class="sxs-lookup"><span data-stu-id="64a6a-205">Create the graph with the configuration `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span></span>

    <span data-ttu-id="64a6a-206">c.</span><span class="sxs-lookup"><span data-stu-id="64a6a-206">c.</span></span> <span data-ttu-id="64a6a-207">使用 SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)` 建立圖形周遊。</span><span class="sxs-lookup"><span data-stu-id="64a6a-207">Create a graph traversal with SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span></span>

    <span data-ttu-id="64a6a-208">d.</span><span class="sxs-lookup"><span data-stu-id="64a6a-208">d.</span></span> <span data-ttu-id="64a6a-209">執行下列 Gremlin 圖形查詢︰</span><span class="sxs-lookup"><span data-stu-id="64a6a-209">Run the following Gremlin graph queries:</span></span>

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
> <span data-ttu-id="64a6a-210">若要查看更詳細的記錄，請將 `conf/log4j-console.properties` 中的記錄層級設定為更詳細的層級。</span><span class="sxs-lookup"><span data-stu-id="64a6a-210">To see more detailed logging, set the log level in `conf/log4j-console.properties` to a more verbose level.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="64a6a-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64a6a-211">Next steps</span></span>

<span data-ttu-id="64a6a-212">在本快速入門文章中，您已經了解如何結合 Azure Cosmos DB 與 Spark 來處理圖形。</span><span class="sxs-lookup"><span data-stu-id="64a6a-212">In this quick-start article, you've learned how to work with graphs by combining Azure Cosmos DB and Spark.</span></span>

> [!div class="nextstepaction"]
