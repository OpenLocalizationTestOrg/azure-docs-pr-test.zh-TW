---
title: "aaaConnecting Apache Spark tooAzure Cosmos DB |Microsoft 文件"
description: "使用此教學課程 toolearn 有關，可讓您 tooconnect Apache Spark tooAzure Cosmos DB tooperform 分散式彙總與 hello 多租用戶的全域分散式的資料庫系統，從 Microsoft 上的資料科學 hello Azure Cosmos DB Spark 連接器hello 雲端所設計。"
keywords: Apache Spark
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: c4f46007-2606-4273-ab16-29d0e15c0736
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: denlee
ms.openlocfilehash: 70b496fc5ca8f65675f0224e749637f5d533c346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="accelerate-real-time-big-data-analytics-with-hello-spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="b5323-104">加速即時巨量資料分析與 hello Spark tooAzure Cosmos DB 連接器</span><span class="sxs-lookup"><span data-stu-id="b5323-104">Accelerate real-time big-data analytics with hello Spark tooAzure Cosmos DB connector</span></span>

<span data-ttu-id="b5323-105">hello Spark tooAzure Cosmos DB 連接器可讓 Azure Cosmos DB tooact 做為輸入的來源或 Apache Spark 工作的輸出接收。</span><span class="sxs-lookup"><span data-stu-id="b5323-105">hello Spark tooAzure Cosmos DB connector enables Azure Cosmos DB tooact as an input source or output sink for Apache Spark jobs.</span></span> <span data-ttu-id="b5323-106">連接[Spark](http://spark.apache.org/)太[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)加速能力 toosolve 快速移動資料科學問題，您可以使用 Azure Cosmos DB tooquickly 保存及查詢資料。</span><span class="sxs-lookup"><span data-stu-id="b5323-106">Connecting [Spark](http://spark.apache.org/) too[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accelerates your ability toosolve fast-moving data science problems where you can use Azure Cosmos DB tooquickly persist and query data.</span></span> <span data-ttu-id="b5323-107">hello Spark tooAzure Cosmos DB 連接器有效率地利用 hello 原生的受管理的 Azure Cosmos DB 索引。</span><span class="sxs-lookup"><span data-stu-id="b5323-107">hello Spark tooAzure Cosmos DB connector efficiently utilizes hello native Azure Cosmos DB managed indexes.</span></span> <span data-ttu-id="b5323-108">hello 索引啟用可更新資料行，當您執行的分析能力向下推送述詞篩選針對快速變更全域發佈的物聯網 (IoT) toodata 科學和分析案例的範圍內的資料。</span><span class="sxs-lookup"><span data-stu-id="b5323-108">hello indexes enable updateable columns when you perform analytics and push-down predicate filtering against fast-changing globally distributed data, which range from Internet of Things (IoT) toodata science and analytics scenarios.</span></span>

<span data-ttu-id="b5323-109">使用 Spark GraphX 和 hello Gremlin 圖形 Azure Cosmos DB 的應用程式開發介面，請參閱[執行圖形分析使用 Spark 和 Apache TinkerPop Gremlin](spark-connector-graph.md)。</span><span class="sxs-lookup"><span data-stu-id="b5323-109">For working with Spark GraphX and hello Gremlin graph APIs of Azure Cosmos DB, see [Perform graph analytics using Spark and Apache TinkerPop Gremlin](spark-connector-graph.md).</span></span>

## <a name="download"></a><span data-ttu-id="b5323-110">下載</span><span class="sxs-lookup"><span data-stu-id="b5323-110">Download</span></span>

<span data-ttu-id="b5323-111">tooget 開始，從 hello 下載 hello Spark tooAzure Cosmos DB 連接器 （預覽） [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) GitHub 上的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="b5323-111">tooget started, download hello Spark tooAzure Cosmos DB connector (preview) from hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) repository on GitHub.</span></span>

## <a name="connector-components"></a><span data-ttu-id="b5323-112">連接器元件</span><span class="sxs-lookup"><span data-stu-id="b5323-112">Connector components</span></span>

<span data-ttu-id="b5323-113">hello 連接器會利用 hello 下列元件：</span><span class="sxs-lookup"><span data-stu-id="b5323-113">hello connector utilizes hello following components:</span></span>

* <span data-ttu-id="b5323-114">[Azure Cosmos DB](http://documentdb.com)可讓客戶 tooprovision 和彈性地調整任何數目的地理區域之間的輸送量與儲存體。</span><span class="sxs-lookup"><span data-stu-id="b5323-114">[Azure Cosmos DB](http://documentdb.com) enables customers tooprovision and elastically scale both throughput and storage across any number of geographical regions.</span></span> <span data-ttu-id="b5323-115">hello 服務可提供：</span><span class="sxs-lookup"><span data-stu-id="b5323-115">hello service offers:</span></span>
   * <span data-ttu-id="b5323-116">讓金鑰可供[全域發佈](distribute-data-globally.md)和水平調整</span><span class="sxs-lookup"><span data-stu-id="b5323-116">Turn key [global distribution](distribute-data-globally.md) and horizontal scale</span></span>
   * <span data-ttu-id="b5323-117">保證個 hello 99th 百分位數延遲</span><span class="sxs-lookup"><span data-stu-id="b5323-117">Guaranteed single digit latencies at hello 99th percentile</span></span>
   * [<span data-ttu-id="b5323-118">多個定義完善的一致性模型</span><span class="sxs-lookup"><span data-stu-id="b5323-118">Multiple well-defined consistency models</span></span>](consistency-levels.md)
   * <span data-ttu-id="b5323-119">保證具有多路連接功能的高可用性</span><span class="sxs-lookup"><span data-stu-id="b5323-119">Guaranteed high availability with multi-homing capabilities</span></span>
   * <span data-ttu-id="b5323-120">所有功能都受領先業界的完整[服務等級協定](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLA) 支援。</span><span class="sxs-lookup"><span data-stu-id="b5323-120">All features are backed by industry-leading, comprehensive [service level agreements](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLAs).</span></span>

* <span data-ttu-id="b5323-121">[Apache Spark](http://spark.apache.org/) 是功能強大的開放原始碼處理引擎，專為速度、易用性和精密分析所打造。</span><span class="sxs-lookup"><span data-stu-id="b5323-121">[Apache Spark](http://spark.apache.org/) is a powerful open source processing engine that's built around speed, ease of use, and sophisticated analytics.</span></span>

* <span data-ttu-id="b5323-122">[Azure HDInsight 上的 Apache Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md)以便您可以使用部署關鍵任務的部署的 hello 雲端中的 Apache Spark [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/)。</span><span class="sxs-lookup"><span data-stu-id="b5323-122">[Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) so that you can deploy Apache Spark in hello cloud for mission-critical deployments by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="b5323-123">正式支援的版本：</span><span class="sxs-lookup"><span data-stu-id="b5323-123">Officially supported versions:</span></span>

| <span data-ttu-id="b5323-124">元件</span><span class="sxs-lookup"><span data-stu-id="b5323-124">Component</span></span> | <span data-ttu-id="b5323-125">版本</span><span class="sxs-lookup"><span data-stu-id="b5323-125">Version</span></span> |
|---------|-------|
|<span data-ttu-id="b5323-126">Apache Spark</span><span class="sxs-lookup"><span data-stu-id="b5323-126">Apache Spark</span></span>|<span data-ttu-id="b5323-127">2.0+</span><span class="sxs-lookup"><span data-stu-id="b5323-127">2.0+</span></span>|
| <span data-ttu-id="b5323-128">Scala</span><span class="sxs-lookup"><span data-stu-id="b5323-128">Scala</span></span>| <span data-ttu-id="b5323-129">2.11</span><span class="sxs-lookup"><span data-stu-id="b5323-129">2.11</span></span>|
| <span data-ttu-id="b5323-130">Azure DocumentDB Java SDK</span><span class="sxs-lookup"><span data-stu-id="b5323-130">Azure DocumentDB Java SDK</span></span> | <span data-ttu-id="b5323-131">1.10.0</span><span class="sxs-lookup"><span data-stu-id="b5323-131">1.10.0</span></span> |

<span data-ttu-id="b5323-132">這篇文章可協助您使用 Python （透過 pyDocumentDB) 來執行一些簡單的範例與 hello Scala 介面。</span><span class="sxs-lookup"><span data-stu-id="b5323-132">This article helps you run some simple samples by using Python (via pyDocumentDB) and hello Scala interfaces.</span></span>

<span data-ttu-id="b5323-133">有兩種方法 tooconnect Apache Spark 和 Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="b5323-133">There are two approaches tooconnect Apache Spark and Azure Cosmos DB:</span></span>
- <span data-ttu-id="b5323-134">使用透過 hello pyDocumentDB [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python)。</span><span class="sxs-lookup"><span data-stu-id="b5323-134">Use pyDocumentDB via hello [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span></span>
- <span data-ttu-id="b5323-135">藉由使用 hello 建立 Java 為基礎的 Spark tooAzure Cosmos DB 連接器[Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java)。</span><span class="sxs-lookup"><span data-stu-id="b5323-135">Create a Java-based Spark tooAzure Cosmos DB connector by utilizing hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

## <a name="pydocumentdb-implementation"></a><span data-ttu-id="b5323-136">pyDocumentDB 實作</span><span class="sxs-lookup"><span data-stu-id="b5323-136">pyDocumentDB implementation</span></span>
<span data-ttu-id="b5323-137">目前的 hello [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python)讓您 tooconnect Spark tooAzure Cosmos DB hello 下列圖表所示：</span><span class="sxs-lookup"><span data-stu-id="b5323-137">hello current [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) enables you tooconnect Spark tooAzure Cosmos DB as shown in hello following diagram:</span></span>

![Spark tooAzure 透過 pyDocumentDB DB Cosmos DB 資料流程](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-hello-pydocumentdb-implementation"></a><span data-ttu-id="b5323-139">Hello pyDocumentDB 實作的資料流程</span><span class="sxs-lookup"><span data-stu-id="b5323-139">Data flow of hello pyDocumentDB implementation</span></span>

<span data-ttu-id="b5323-140">hello 資料流程如下所示：</span><span class="sxs-lookup"><span data-stu-id="b5323-140">hello data flow is as follows:</span></span>

1. <span data-ttu-id="b5323-141">hello Spark 主要節點連接透過 pyDocumentDB toohello Azure Cosmos DB 閘道節點。</span><span class="sxs-lookup"><span data-stu-id="b5323-141">hello Spark master node connects toohello Azure Cosmos DB gateway node via pyDocumentDB.</span></span> <span data-ttu-id="b5323-142">使用者指定只有 hello Spark 和 Azure Cosmos DB 的連線。</span><span class="sxs-lookup"><span data-stu-id="b5323-142">A user specifies only hello Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="b5323-143">連線 toohello 個別 master 和閘道節點是透明 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="b5323-143">Connections toohello respective master and gateway nodes are transparent toohello user.</span></span>
2. <span data-ttu-id="b5323-144">hello 閘道節點可讓您針對 Azure Cosmos DB 位置 hello 查詢接著會執行 hello 資料節點中的 hello 集合的資料分割的 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="b5323-144">hello gateway node makes hello query against Azure Cosmos DB where hello query subsequently runs against hello collection's partitions in hello data nodes.</span></span> <span data-ttu-id="b5323-145">這些查詢的 hello 回應會傳送回 toohello 閘道節點，且該結果集，則會傳回 toohello Spark 主要節點。</span><span class="sxs-lookup"><span data-stu-id="b5323-145">hello response for those queries is sent back toohello gateway node, and that result set is returned toohello Spark master node.</span></span>
3. <span data-ttu-id="b5323-146">後續的查詢 （例如，針對 Spark 資料框架中） 會傳送 toohello Spark 背景工作節點進行處理。</span><span class="sxs-lookup"><span data-stu-id="b5323-146">Subsequent queries (for example, against a Spark DataFrame) are sent toohello Spark worker nodes for processing.</span></span>

<span data-ttu-id="b5323-147">Spark 與 Azure Cosmos DB 之間的通訊是有限的 toohello Spark 主要節點和 Azure Cosmos DB 閘道節點。</span><span class="sxs-lookup"><span data-stu-id="b5323-147">Communication between Spark and Azure Cosmos DB is limited toohello Spark master node and Azure Cosmos DB gateway nodes.</span></span>  <span data-ttu-id="b5323-148">以最快速度 hello 這兩個節點之間的傳輸層級可讓移 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="b5323-148">hello queries go as fast as hello transport layer between these two nodes allows.</span></span>

### <a name="install-pydocumentdb"></a><span data-ttu-id="b5323-149">安裝 pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="b5323-149">Install pyDocumentDB</span></span>
<span data-ttu-id="b5323-150">您可以使用 **pip**，在驅動程式節點上安裝 pyDocumentDB，例如：</span><span class="sxs-lookup"><span data-stu-id="b5323-150">You can install pyDocumentDB on your driver node by using **pip**, for example:</span></span>

```
pip install pyDocumentDB
```


### <a name="connect-spark-tooazure-cosmos-db-via-pydocumentdb"></a><span data-ttu-id="b5323-151">連接透過 pyDocumentDB Spark tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b5323-151">Connect Spark tooAzure Cosmos DB via pyDocumentDB</span></span>
<span data-ttu-id="b5323-152">hello 通訊傳輸的 hello 簡化就可以執行從 Spark tooAzure Cosmos DB 查詢透過 pyDocumentDB 相當簡單。</span><span class="sxs-lookup"><span data-stu-id="b5323-152">hello simplicity of hello communication transport makes execution of a query from Spark tooAzure Cosmos DB by using pyDocumentDB relatively simple.</span></span>

<span data-ttu-id="b5323-153">hello 下列程式碼片段會示範如何 toouse pyDocumentDB Spark 內容中的。</span><span class="sxs-lookup"><span data-stu-id="b5323-153">hello following code snippet shows how toouse pyDocumentDB in a Spark context.</span></span>

```
# Import Necessary Libraries
import pydocumentdb
from pydocumentdb import document_client
from pydocumentdb import documents
import datetime

# Configuring hello connection policy (allowing for endpoint discovery)
connectionPolicy = documents.ConnectionPolicy()
connectionPolicy.EnableEndpointDiscovery
connectionPolicy.PreferredLocations = ["Central US", "East US 2", "Southeast Asia", "Western Europe","Canada Central"]


# Set keys tooconnect tooAzure Cosmos DB
masterKey = 'le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA=='
host = 'https://doctorwho.documents.azure.com:443/'
client = document_client.DocumentClient(host, {'masterKey': masterKey}, connectionPolicy)
```

<span data-ttu-id="b5323-154">Hello 程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="b5323-154">As noted in hello code snippet:</span></span>

* <span data-ttu-id="b5323-155">hello Azure Cosmos DB Python SDK (`pyDocumentDB`) 包含 hello 所有 hello 必要的連接參數。</span><span class="sxs-lookup"><span data-stu-id="b5323-155">hello Azure Cosmos DB Python SDK (`pyDocumentDB`) contains hello all hello necessary connection parameters.</span></span> <span data-ttu-id="b5323-156">例如，hello 慣用位置參數選擇 hello 讀取的複本和優先順序的順序。</span><span class="sxs-lookup"><span data-stu-id="b5323-156">For example, hello preferred locations parameter chooses hello read replica and priority order.</span></span>
*  <span data-ttu-id="b5323-157">Hello 必要的程式庫匯入及設定您**masterKey**和**主機**toocreate hello Azure Cosmos DB*用戶端*(**pydocumentdb.document_用戶端**)。</span><span class="sxs-lookup"><span data-stu-id="b5323-157">Import hello necessary libraries and configure your **masterKey** and **host** toocreate hello Azure Cosmos DB *client* (**pydocumentdb.document_client**).</span></span>


### <a name="execute-spark-queries-via-pydocumentdb"></a><span data-ttu-id="b5323-158">透過 pyDocumentDB 執行 Spark 查詢</span><span class="sxs-lookup"><span data-stu-id="b5323-158">Execute Spark Queries via pyDocumentDB</span></span>
<span data-ttu-id="b5323-159">下列範例使用 hello Azure Cosmos 資料庫執行個體使用 hello hello 先前程式碼片段中所建立的 hello 指定唯讀金鑰。</span><span class="sxs-lookup"><span data-stu-id="b5323-159">hello following examples use hello Azure Cosmos DB instance that was created in hello previous snippet by using hello specified read-only keys.</span></span> <span data-ttu-id="b5323-160">hello 下列程式碼片段會連接 toohello **airports.codes**稍早指定 hello DoctorWho 帳戶中的集合，並執行查詢 tooextract hello 機場在華盛頓州的城市。</span><span class="sxs-lookup"><span data-stu-id="b5323-160">hello following code snippet connects toohello **airports.codes** collection in hello DoctorWho account as specified earlier and runs a query tooextract hello airport cities in Washington state.</span></span>

```
# Configure Database and Collections
databaseId = 'airports'
collectionId = 'codes'

# Configurations hello Azure Cosmos DB client will use tooconnect toohello database and collection
dbLink = 'dbs/' + databaseId
collLink = dbLink + '/colls/' + collectionId

# Set query parameter
querystr = "SELECT c.City FROM c WHERE c.State='WA'"

# Query documents
query = client.QueryDocuments(collLink, querystr, options=None, partition_key=None)

# Query for partitioned collections
# query = client.QueryDocuments(collLink, query, options= { 'enableCrossPartitionQuery': True }, partition_key=None)

# Push into list `elements`
elements = list(query)
```

<span data-ttu-id="b5323-161">透過執行 hello 查詢之後**查詢**，hello 結果是**query_iterable。QueryIterable**也就是轉換的 tooa Python 清單。</span><span class="sxs-lookup"><span data-stu-id="b5323-161">After hello query has been executed via **query**, hello result is a **query_iterable.QueryIterable** that is converted tooa Python list.</span></span> <span data-ttu-id="b5323-162">使用下列程式碼的 hello Python 清單可以輕鬆地轉換的 tooa Spark 資料框架：</span><span class="sxs-lookup"><span data-stu-id="b5323-162">A Python list can be easily converted tooa Spark DataFrame by using hello following code:</span></span>

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-hello-pydocumentdb-tooconnect-spark-tooazure-cosmos-db"></a><span data-ttu-id="b5323-163">為何要使用 hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB 嗎？</span><span class="sxs-lookup"><span data-stu-id="b5323-163">Why use hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB?</span></span>
<span data-ttu-id="b5323-164">連接 Spark tooAzure 案例通常是使用 pyDocumentDB Cosmos DB 位置：</span><span class="sxs-lookup"><span data-stu-id="b5323-164">Connecting Spark tooAzure Cosmos DB by using pyDocumentDB is typically for scenarios where:</span></span>

* <span data-ttu-id="b5323-165">您想 toouse Python。</span><span class="sxs-lookup"><span data-stu-id="b5323-165">You want toouse Python.</span></span>
* <span data-ttu-id="b5323-166">您要傳回的相對較小的結果集從 Azure Cosmos DB tooSpark。</span><span class="sxs-lookup"><span data-stu-id="b5323-166">You are returning a relatively small result set from Azure Cosmos DB tooSpark.</span></span> <span data-ttu-id="b5323-167">請注意，hello Azure Cosmos DB 中的基礎資料集可能很龐大。</span><span class="sxs-lookup"><span data-stu-id="b5323-167">Note that hello underlying dataset in Azure Cosmos DB can be quite large.</span></span> <span data-ttu-id="b5323-168">您要將篩選條件套用至 Azure Cosmos DB 來源，即執行述詞篩選條件。</span><span class="sxs-lookup"><span data-stu-id="b5323-168">You are applying filters, that is, running predicate filters, against your Azure Cosmos DB source.</span></span>  

## <a name="spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="b5323-169">Spark tooAzure Cosmos DB 連接器</span><span class="sxs-lookup"><span data-stu-id="b5323-169">Spark tooAzure Cosmos DB connector</span></span>

<span data-ttu-id="b5323-170">hello Spark tooAzure Cosmos DB 連接器會利用 hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) hello Spark 背景工作節點與 Azure Cosmos DB 之間移動資料，hello 下列圖表所示：</span><span class="sxs-lookup"><span data-stu-id="b5323-170">hello Spark tooAzure Cosmos DB connector utilizes hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) and moves data between hello Spark worker nodes and Azure Cosmos DB as shown in hello following diagram:</span></span>

![Hello Spark tooAzure Cosmos DB 連接器中的資料流程](./media/spark-connector/spark-connector.png)

<span data-ttu-id="b5323-172">hello 資料流程如下所示：</span><span class="sxs-lookup"><span data-stu-id="b5323-172">hello data flow is as follows:</span></span>

1. <span data-ttu-id="b5323-173">hello Spark 主要節點連接 toohello Azure Cosmos DB 閘道節點 tooobtain hello 分割區對應。</span><span class="sxs-lookup"><span data-stu-id="b5323-173">hello Spark master node connects toohello Azure Cosmos DB gateway node tooobtain hello partition map.</span></span> <span data-ttu-id="b5323-174">使用者指定只有 hello Spark 和 Azure Cosmos DB 的連線。</span><span class="sxs-lookup"><span data-stu-id="b5323-174">A user specifies only hello Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="b5323-175">連線 toohello 個別 master 和閘道節點是透明 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="b5323-175">Connections toohello respective master and gateway nodes are transparent toohello user.</span></span>
2. <span data-ttu-id="b5323-176">回復 toohello Spark 主要節點時，會提供此資訊。</span><span class="sxs-lookup"><span data-stu-id="b5323-176">This information is provided back toohello Spark master node.</span></span>  <span data-ttu-id="b5323-177">此時，您應該能夠 tooparse hello 查詢 toodetermine hello 資料分割和其位置，您需要 tooaccess Azure Cosmos DB 中。</span><span class="sxs-lookup"><span data-stu-id="b5323-177">At this point, you should be able tooparse hello query toodetermine hello partitions and their locations in Azure Cosmos DB that you need tooaccess.</span></span>
3. <span data-ttu-id="b5323-178">這項資訊是傳輸的 toohello Spark 背景工作節點。</span><span class="sxs-lookup"><span data-stu-id="b5323-178">This information is transmitted toohello Spark worker nodes.</span></span>
4. <span data-ttu-id="b5323-179">hello Spark 背景工作節點連接 toohello Azure Cosmos DB 的資料分割，直接 tooextract hello 資料，並傳回 hello 資料 toohello hello Spark 背景工作角色節點中的 Spark 資料分割。</span><span class="sxs-lookup"><span data-stu-id="b5323-179">hello Spark worker nodes connect toohello Azure Cosmos DB partitions directly tooextract hello data and return hello data toohello Spark partitions in hello Spark worker nodes.</span></span>

<span data-ttu-id="b5323-180">Spark 與 Azure Cosmos DB 之間的通訊速度大幅因為 hello 資料移動是 hello Spark 背景工作節點與 hello Azure Cosmos DB 的資料節點 （資料分割） 之間。</span><span class="sxs-lookup"><span data-stu-id="b5323-180">Communication between Spark and Azure Cosmos DB is significantly faster because hello data movement is between hello Spark worker nodes and hello Azure Cosmos DB data nodes (partitions).</span></span>

### <a name="build-hello-spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="b5323-181">建置 hello Spark tooAzure Cosmos DB 連接器</span><span class="sxs-lookup"><span data-stu-id="b5323-181">Build hello Spark tooAzure Cosmos DB connector</span></span>
<span data-ttu-id="b5323-182">目前，hello 連接器專案會使用 maven。</span><span class="sxs-lookup"><span data-stu-id="b5323-182">Currently, hello connector project uses maven.</span></span> <span data-ttu-id="b5323-183">無相依性 toobuild hello 連接器，您可以執行：</span><span class="sxs-lookup"><span data-stu-id="b5323-183">toobuild hello connector without dependencies, you can run:</span></span>
```
mvn clean package
```
<span data-ttu-id="b5323-184">您也可以從 hello 下載 hello 最新版 hello JAR*釋放*資料夾。</span><span class="sxs-lookup"><span data-stu-id="b5323-184">You can also download hello latest versions of hello JAR from hello *releases* folder.</span></span>

### <a name="include-hello-azure-cosmos-db-spark-jar"></a><span data-ttu-id="b5323-185">包含 Azure Cosmos DB Spark JAR hello</span><span class="sxs-lookup"><span data-stu-id="b5323-185">Include hello Azure Cosmos DB Spark JAR</span></span>
<span data-ttu-id="b5323-186">在執行任何程式碼之前，您需要 Azure Cosmos DB Spark JAR tooinclude hello。</span><span class="sxs-lookup"><span data-stu-id="b5323-186">Before you execute any code, you need tooinclude hello Azure Cosmos DB Spark JAR.</span></span>  <span data-ttu-id="b5323-187">如果您使用 hello **spark 殼層**，則您可以透過使用 hello 包含 hello JAR **-（每瓶)**選項。</span><span class="sxs-lookup"><span data-stu-id="b5323-187">If you are using hello **spark-shell**, then you can include hello JAR by using hello **--jars** option.</span></span>  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

<span data-ttu-id="b5323-188">如果您想 tooexecute hello JAR 無相依性，請使用下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="b5323-188">If you want tooexecute hello JAR without dependencies, use hello following code:</span></span>

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

<span data-ttu-id="b5323-189">如果您使用筆記型電腦服務，例如 Azure HDInsight Jupyter 筆記本服務，您可以使用 hello**二手 magic**命令：</span><span class="sxs-lookup"><span data-stu-id="b5323-189">If you are using a notebook service such as Azure HDInsight Jupyter notebook service, you can use hello **spark magic** commands:</span></span>

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

<span data-ttu-id="b5323-190">hello **（每瓶)**命令可讓您 tooinclude hello 兩個 Jar 的所需的**azure-cosmosdb-spark** （本身和 hello Azure DocumentDB Java SDK），並排除**scala-反映** ，讓它不會干擾晚總呼叫的 hello (Jupyter 筆記本 > 晚總 > Spark)。</span><span class="sxs-lookup"><span data-stu-id="b5323-190">hello **jars** command enables you tooinclude hello two JARs that are needed for **azure-cosmosdb-spark** (itself and hello Azure DocumentDB Java SDK) and exclude **scala-reflect** so that it does not interfere with hello Livy calls (Jupyter notebook > Livy > Spark).</span></span>

### <a name="connect-spark-tooazure-cosmos-db-using-hello-connector"></a><span data-ttu-id="b5323-191">連接 Spark tooAzure Cosmos DB 使用 hello 連接器</span><span class="sxs-lookup"><span data-stu-id="b5323-191">Connect Spark tooAzure Cosmos DB using hello connector</span></span>
<span data-ttu-id="b5323-192">雖然 hello 通訊傳輸得較複雜，但是執行查詢，從 Spark tooAzure Cosmos DB 使用 hello 連接器是速度明顯加快。</span><span class="sxs-lookup"><span data-stu-id="b5323-192">Although hello communication transport is a little more complicated, executing a query from Spark tooAzure Cosmos DB by using hello connector is significantly faster.</span></span>

<span data-ttu-id="b5323-193">hello，下列程式碼片段顯示如何 toouse hello Spark 內容中的連接器。</span><span class="sxs-lookup"><span data-stu-id="b5323-193">hello following code snippet shows how toouse hello connector in a Spark context.</span></span>

```
// Import Necessary Libraries
import org.joda.time._
import org.joda.time.format._
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Configure connection tooyour collection
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US2;",
"Collection" -> "flights_pcoll",
"SamplingRatio" -> "1.0"))

// Create collection connection
val coll = spark.sqlContext.read.cosmosDB(readConfig2)
coll.createOrReplaceTempView("c")
```

<span data-ttu-id="b5323-194">Hello 程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="b5323-194">As noted in hello code snippet:</span></span>

- <span data-ttu-id="b5323-195">**azure-cosmosdb-spark**包含 hello 所有 hello 必要的連接參數，其中包括 hello 慣用位置。</span><span class="sxs-lookup"><span data-stu-id="b5323-195">**azure-cosmosdb-spark** contains hello all hello necessary connection parameters, which include hello preferred locations.</span></span> <span data-ttu-id="b5323-196">例如，您可以選擇 hello 讀取的複本和優先順序的順序。</span><span class="sxs-lookup"><span data-stu-id="b5323-196">For example, you can choose hello read replica and priority order.</span></span>
- <span data-ttu-id="b5323-197">只匯入 hello 必要的程式庫和主要金鑰和主機 toocreate hello Azure Cosmos DB 用戶端設定。</span><span class="sxs-lookup"><span data-stu-id="b5323-197">Just import hello necessary libraries and configure your masterKey and host toocreate hello Azure Cosmos DB client.</span></span>

### <a name="execute-spark-queries-via-hello-connector"></a><span data-ttu-id="b5323-198">查詢透過 hello 連接器的 Spark</span><span class="sxs-lookup"><span data-stu-id="b5323-198">Execute Spark queries via hello connector</span></span>

<span data-ttu-id="b5323-199">下列範例會使用 hello Azure Cosmos 資料庫執行個體使用 hello hello 先前程式碼片段中所建立的 hello 指定唯讀金鑰。</span><span class="sxs-lookup"><span data-stu-id="b5323-199">hello following example uses hello Azure Cosmos DB instance that was created in hello previous snippet by using hello specified read-only keys.</span></span> <span data-ttu-id="b5323-200">hello 下列程式碼片段連線 toohello DepartureDelays.flights_pcoll 集合 （在 hello DoctorWho 如先前所指定的帳戶) 並執行查詢 tooextract hello 飛行延遲資訊的結果會不同於西雅圖的班機。</span><span class="sxs-lookup"><span data-stu-id="b5323-200">hello following code snippet connects toohello DepartureDelays.flights_pcoll collection (in hello DoctorWho account as specified earlier) and runs a query tooextract hello flight delay information of flights that are departing from Seattle.</span></span>

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-hello-spark-tooazure-cosmos-db-connector-implementation"></a><span data-ttu-id="b5323-201">為何要使用 hello Spark tooAzure Cosmos DB 連接器實作？</span><span class="sxs-lookup"><span data-stu-id="b5323-201">Why use hello Spark tooAzure Cosmos DB connector implementation?</span></span>

<span data-ttu-id="b5323-202">連接 Spark tooAzure 案例通常是藉由使用 hello 連接器 Cosmos DB 位置：</span><span class="sxs-lookup"><span data-stu-id="b5323-202">Connecting Spark tooAzure Cosmos DB by using hello connector is typically for scenarios where:</span></span>

* <span data-ttu-id="b5323-203">您想 toouse Scala 並且更新它 tooinclude Python 包裝函式中有註明[問題 3： 加入 Python 包裝函式和範例](https://github.com/Azure/azure-cosmosdb-spark/issues/3)。</span><span class="sxs-lookup"><span data-stu-id="b5323-203">You want toouse Scala and update it tooinclude a Python wrapper as noted in [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span></span>
* <span data-ttu-id="b5323-204">您有大量的資料 tootransfer Apache Spark 與 Azure Cosmos DB 之間。</span><span class="sxs-lookup"><span data-stu-id="b5323-204">You have a large amount of data tootransfer between Apache Spark and Azure Cosmos DB.</span></span>

<span data-ttu-id="b5323-205">toogive 您了解的 hello 查詢的效能差異，請參閱 hello[查詢測試回合 wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs)。</span><span class="sxs-lookup"><span data-stu-id="b5323-205">toogive you an idea of hello query performance difference, see hello [Query Test Runs wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span></span>

## <a name="distributed-aggregation-example"></a><span data-ttu-id="b5323-206">分散式彙總範例</span><span class="sxs-lookup"><span data-stu-id="b5323-206">Distributed aggregation example</span></span>
<span data-ttu-id="b5323-207">本節提供一些範例，示範如何搭配使用 Apache Spark 與 Azure Cosmos DB 來執行分散式彙總和分析。</span><span class="sxs-lookup"><span data-stu-id="b5323-207">This section provides some examples of how you can do distributed aggregations and analytics by using Apache Spark and Azure Cosmos DB together.</span></span> <span data-ttu-id="b5323-208">Azure Cosmos DB 已經支援彙總，其中會討論 hello[地球小數位數的彙總與 Azure Cosmos DB 部落格](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/)。</span><span class="sxs-lookup"><span data-stu-id="b5323-208">Azure Cosmos DB already supports aggregations, which is discussed in hello [Planet scale aggregates with Azure Cosmos DB blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span></span> <span data-ttu-id="b5323-209">以下是如何您就可以帶 toohello 接下來使用 Apache Spark 層級。</span><span class="sxs-lookup"><span data-stu-id="b5323-209">Here is how you can take it toohello next level with Apache Spark.</span></span>

<span data-ttu-id="b5323-210">請注意，這些彙總位於參考 toohello [Spark tooAzure Cosmos DB 連接器筆記本](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb)。</span><span class="sxs-lookup"><span data-stu-id="b5323-210">Note that these aggregations are in reference toohello [Spark tooAzure Cosmos DB Connector notebook](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span></span>

### <a name="connect-tooflights-sample-data"></a><span data-ttu-id="b5323-211">連接 tooflights 範例資料</span><span class="sxs-lookup"><span data-stu-id="b5323-211">Connect tooflights sample data</span></span>
<span data-ttu-id="b5323-212">這些彙總範例會存取儲存在 **DoctorWho** Azure Cosmos DB 資料庫中的一些航班效能資料。</span><span class="sxs-lookup"><span data-stu-id="b5323-212">These aggregation examples access some flight performance data that's stored in our **DoctorWho** Azure Cosmos DB database.</span></span> <span data-ttu-id="b5323-213">tooconnect tooit，您需要下列程式碼片段的 tooutilize hello:</span><span class="sxs-lookup"><span data-stu-id="b5323-213">tooconnect tooit, you need tooutilize hello following code snippet:</span></span>

```
// Import Spark tooAzure Cosmos DB connector
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Connect tooAzure Cosmos DB Database
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US 2;",
"Collection" -> "flights_pcoll",
"SamplingRatio" -> "1.0"))

// Create collection connection
val coll = spark.sqlContext.read.cosmosDB(readConfig2)
coll.createOrReplaceTempView("c")
```

<span data-ttu-id="b5323-214">此片段中，我們也會持續 toorun 傳輸 hello 篩選的資料從 Azure Cosmos DB tooSpark 集的基本查詢 hello 後者可以在其中執行分散式彙總。</span><span class="sxs-lookup"><span data-stu-id="b5323-214">With this snippet, we are also going toorun a base query that transfers hello filtered set of data from Azure Cosmos DB tooSpark where hello latter can perform distributed aggregates.</span></span> <span data-ttu-id="b5323-215">在此情況下，我們要求從西雅圖 (SEA) 出發的航班資料。</span><span class="sxs-lookup"><span data-stu-id="b5323-215">In this case, we are asking for flights that depart from Seattle (SEA).</span></span>

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

<span data-ttu-id="b5323-216">hello 下列結果所產生 hello Jupyter 筆記本服務從執行 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="b5323-216">hello following results were generated by running hello queries from hello Jupyter notebook service.</span></span>  <span data-ttu-id="b5323-217">請注意，所有的 hello 程式碼片段泛型和非 tooany 服務。</span><span class="sxs-lookup"><span data-stu-id="b5323-217">Note that all hello code snippets are generic and not specific tooany service.</span></span>

### <a name="running-limit-and-count-queries"></a><span data-ttu-id="b5323-218">執行 LIMIT 和 COUNT 查詢</span><span class="sxs-lookup"><span data-stu-id="b5323-218">Running LIMIT and COUNT queries</span></span>
<span data-ttu-id="b5323-219">就像您是使用 tooin SQL/Spark SQL，讓我們開始**限制**查詢：</span><span class="sxs-lookup"><span data-stu-id="b5323-219">Just like you're used tooin SQL/Spark SQL, let's start off with a **LIMIT** query:</span></span>

![Spark LIMIT 查詢](./media/spark-connector/spark-sql-query.png)

<span data-ttu-id="b5323-221">hello 下一個查詢是簡單又快速**計數**查詢：</span><span class="sxs-lookup"><span data-stu-id="b5323-221">hello next query is a simple and fast **COUNT** query:</span></span>

![Spark COUNT 查詢](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a><span data-ttu-id="b5323-223">GROUP BY 查詢</span><span class="sxs-lookup"><span data-stu-id="b5323-223">GROUP BY query</span></span>
<span data-ttu-id="b5323-224">在接下來的這一組中，我們可以對 Azure Cosmos DB 資料庫輕鬆執行 **GROUP BY** 查詢：</span><span class="sxs-lookup"><span data-stu-id="b5323-224">In this next set, we can easily run **GROUP BY** queries against our Azure Cosmos DB database:</span></span>

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Spark GROUP BY 查詢圖形](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a><span data-ttu-id="b5323-226">DISTINCT, ORDER BY 查詢</span><span class="sxs-lookup"><span data-stu-id="b5323-226">DISTINCT, ORDER BY query</span></span>
<span data-ttu-id="b5323-227">以下是 **DISTINCT, ORDER BY** 查詢：</span><span class="sxs-lookup"><span data-stu-id="b5323-227">And here is a **DISTINCT, ORDER BY** query:</span></span>

![Spark GROUP BY 查詢圖形](./media/spark-connector/order-by-query.png)

### <a name="continue-hello-flight-data-analysis"></a><span data-ttu-id="b5323-229">繼續 hello 飛行資料分析</span><span class="sxs-lookup"><span data-stu-id="b5323-229">Continue hello flight data analysis</span></span>
<span data-ttu-id="b5323-230">您可以使用下列範例查詢 toocontinue 分析 hello 飛行資料 hello:</span><span class="sxs-lookup"><span data-stu-id="b5323-230">You can use hello following example queries toocontinue analysis of hello flight data:</span></span>

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a><span data-ttu-id="b5323-231">從西雅圖出發的前 5 個延遲目的地 (城市)</span><span class="sxs-lookup"><span data-stu-id="b5323-231">Top 5 delayed destinations (cities) departing from Seattle</span></span>
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Spark 前幾個延遲圖形](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a><span data-ttu-id="b5323-233">計算從西雅圖出發的目的地城市的中間延遲</span><span class="sxs-lookup"><span data-stu-id="b5323-233">Calculate median delays by destination cities departing from Seattle</span></span>
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Spark 中間幾個延遲圖形](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a><span data-ttu-id="b5323-235">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b5323-235">Next steps</span></span>

<span data-ttu-id="b5323-236">如果您還沒有這麼做，請從 hello 下載 hello Spark tooAzure Cosmos DB 連接器[azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub 儲存機制和瀏覽 hello hello 儲存機制內的其他資源：</span><span class="sxs-lookup"><span data-stu-id="b5323-236">If you haven't already, download hello Spark tooAzure Cosmos DB connector from hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub repository and explore hello additional resources in hello repo:</span></span>

* <span data-ttu-id="b5323-237">[分散式彙總範例](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples) (英文)</span><span class="sxs-lookup"><span data-stu-id="b5323-237">[Distributed Aggregations Examples](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)</span></span>
* <span data-ttu-id="b5323-238">[指令碼和 Notebook 範例](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples) (英文)</span><span class="sxs-lookup"><span data-stu-id="b5323-238">[Sample Scripts and Notebooks](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)</span></span>

<span data-ttu-id="b5323-239">您也可以 tooreview hello [Apache Spark SQL、 資料框架和資料集的指南](http://spark.apache.org/docs/latest/sql-programming-guide.html)和 hello [Azure HDInsight 上的 Apache Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="b5323-239">You might also want tooreview hello [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) and hello [Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) article.</span></span>
