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
# <a name="accelerate-real-time-big-data-analytics-with-hello-spark-tooazure-cosmos-db-connector"></a>加速即時巨量資料分析與 hello Spark tooAzure Cosmos DB 連接器

hello Spark tooAzure Cosmos DB 連接器可讓 Azure Cosmos DB tooact 做為輸入的來源或 Apache Spark 工作的輸出接收。 連接[Spark](http://spark.apache.org/)太[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)加速能力 toosolve 快速移動資料科學問題，您可以使用 Azure Cosmos DB tooquickly 保存及查詢資料。 hello Spark tooAzure Cosmos DB 連接器有效率地利用 hello 原生的受管理的 Azure Cosmos DB 索引。 hello 索引啟用可更新資料行，當您執行的分析能力向下推送述詞篩選針對快速變更全域發佈的物聯網 (IoT) toodata 科學和分析案例的範圍內的資料。

使用 Spark GraphX 和 hello Gremlin 圖形 Azure Cosmos DB 的應用程式開發介面，請參閱[執行圖形分析使用 Spark 和 Apache TinkerPop Gremlin](spark-connector-graph.md)。

## <a name="download"></a>下載

tooget 開始，從 hello 下載 hello Spark tooAzure Cosmos DB 連接器 （預覽） [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) GitHub 上的儲存機制。

## <a name="connector-components"></a>連接器元件

hello 連接器會利用 hello 下列元件：

* [Azure Cosmos DB](http://documentdb.com)可讓客戶 tooprovision 和彈性地調整任何數目的地理區域之間的輸送量與儲存體。 hello 服務可提供：
   * 讓金鑰可供[全域發佈](distribute-data-globally.md)和水平調整
   * 保證個 hello 99th 百分位數延遲
   * [多個定義完善的一致性模型](consistency-levels.md)
   * 保證具有多路連接功能的高可用性
   * 所有功能都受領先業界的完整[服務等級協定](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLA) 支援。

* [Apache Spark](http://spark.apache.org/) 是功能強大的開放原始碼處理引擎，專為速度、易用性和精密分析所打造。

* [Azure HDInsight 上的 Apache Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md)以便您可以使用部署關鍵任務的部署的 hello 雲端中的 Apache Spark [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/)。

正式支援的版本：

| 元件 | 版本 |
|---------|-------|
|Apache Spark|2.0+|
| Scala| 2.11|
| Azure DocumentDB Java SDK | 1.10.0 |

這篇文章可協助您使用 Python （透過 pyDocumentDB) 來執行一些簡單的範例與 hello Scala 介面。

有兩種方法 tooconnect Apache Spark 和 Azure Cosmos DB:
- 使用透過 hello pyDocumentDB [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python)。
- 藉由使用 hello 建立 Java 為基礎的 Spark tooAzure Cosmos DB 連接器[Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java)。

## <a name="pydocumentdb-implementation"></a>pyDocumentDB 實作
目前的 hello [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python)讓您 tooconnect Spark tooAzure Cosmos DB hello 下列圖表所示：

![Spark tooAzure 透過 pyDocumentDB DB Cosmos DB 資料流程](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-hello-pydocumentdb-implementation"></a>Hello pyDocumentDB 實作的資料流程

hello 資料流程如下所示：

1. hello Spark 主要節點連接透過 pyDocumentDB toohello Azure Cosmos DB 閘道節點。 使用者指定只有 hello Spark 和 Azure Cosmos DB 的連線。 連線 toohello 個別 master 和閘道節點是透明 toohello 使用者。
2. hello 閘道節點可讓您針對 Azure Cosmos DB 位置 hello 查詢接著會執行 hello 資料節點中的 hello 集合的資料分割的 hello 查詢。 這些查詢的 hello 回應會傳送回 toohello 閘道節點，且該結果集，則會傳回 toohello Spark 主要節點。
3. 後續的查詢 （例如，針對 Spark 資料框架中） 會傳送 toohello Spark 背景工作節點進行處理。

Spark 與 Azure Cosmos DB 之間的通訊是有限的 toohello Spark 主要節點和 Azure Cosmos DB 閘道節點。  以最快速度 hello 這兩個節點之間的傳輸層級可讓移 hello 查詢。

### <a name="install-pydocumentdb"></a>安裝 pyDocumentDB
您可以使用 **pip**，在驅動程式節點上安裝 pyDocumentDB，例如：

```
pip install pyDocumentDB
```


### <a name="connect-spark-tooazure-cosmos-db-via-pydocumentdb"></a>連接透過 pyDocumentDB Spark tooAzure Cosmos DB
hello 通訊傳輸的 hello 簡化就可以執行從 Spark tooAzure Cosmos DB 查詢透過 pyDocumentDB 相當簡單。

hello 下列程式碼片段會示範如何 toouse pyDocumentDB Spark 內容中的。

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

Hello 程式碼片段所示：

* hello Azure Cosmos DB Python SDK (`pyDocumentDB`) 包含 hello 所有 hello 必要的連接參數。 例如，hello 慣用位置參數選擇 hello 讀取的複本和優先順序的順序。
*  Hello 必要的程式庫匯入及設定您**masterKey**和**主機**toocreate hello Azure Cosmos DB*用戶端*(**pydocumentdb.document_用戶端**)。


### <a name="execute-spark-queries-via-pydocumentdb"></a>透過 pyDocumentDB 執行 Spark 查詢
下列範例使用 hello Azure Cosmos 資料庫執行個體使用 hello hello 先前程式碼片段中所建立的 hello 指定唯讀金鑰。 hello 下列程式碼片段會連接 toohello **airports.codes**稍早指定 hello DoctorWho 帳戶中的集合，並執行查詢 tooextract hello 機場在華盛頓州的城市。

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

透過執行 hello 查詢之後**查詢**，hello 結果是**query_iterable。QueryIterable**也就是轉換的 tooa Python 清單。 使用下列程式碼的 hello Python 清單可以輕鬆地轉換的 tooa Spark 資料框架：

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-hello-pydocumentdb-tooconnect-spark-tooazure-cosmos-db"></a>為何要使用 hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB 嗎？
連接 Spark tooAzure 案例通常是使用 pyDocumentDB Cosmos DB 位置：

* 您想 toouse Python。
* 您要傳回的相對較小的結果集從 Azure Cosmos DB tooSpark。 請注意，hello Azure Cosmos DB 中的基礎資料集可能很龐大。 您要將篩選條件套用至 Azure Cosmos DB 來源，即執行述詞篩選條件。  

## <a name="spark-tooazure-cosmos-db-connector"></a>Spark tooAzure Cosmos DB 連接器

hello Spark tooAzure Cosmos DB 連接器會利用 hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) hello Spark 背景工作節點與 Azure Cosmos DB 之間移動資料，hello 下列圖表所示：

![Hello Spark tooAzure Cosmos DB 連接器中的資料流程](./media/spark-connector/spark-connector.png)

hello 資料流程如下所示：

1. hello Spark 主要節點連接 toohello Azure Cosmos DB 閘道節點 tooobtain hello 分割區對應。 使用者指定只有 hello Spark 和 Azure Cosmos DB 的連線。 連線 toohello 個別 master 和閘道節點是透明 toohello 使用者。
2. 回復 toohello Spark 主要節點時，會提供此資訊。  此時，您應該能夠 tooparse hello 查詢 toodetermine hello 資料分割和其位置，您需要 tooaccess Azure Cosmos DB 中。
3. 這項資訊是傳輸的 toohello Spark 背景工作節點。
4. hello Spark 背景工作節點連接 toohello Azure Cosmos DB 的資料分割，直接 tooextract hello 資料，並傳回 hello 資料 toohello hello Spark 背景工作角色節點中的 Spark 資料分割。

Spark 與 Azure Cosmos DB 之間的通訊速度大幅因為 hello 資料移動是 hello Spark 背景工作節點與 hello Azure Cosmos DB 的資料節點 （資料分割） 之間。

### <a name="build-hello-spark-tooazure-cosmos-db-connector"></a>建置 hello Spark tooAzure Cosmos DB 連接器
目前，hello 連接器專案會使用 maven。 無相依性 toobuild hello 連接器，您可以執行：
```
mvn clean package
```
您也可以從 hello 下載 hello 最新版 hello JAR*釋放*資料夾。

### <a name="include-hello-azure-cosmos-db-spark-jar"></a>包含 Azure Cosmos DB Spark JAR hello
在執行任何程式碼之前，您需要 Azure Cosmos DB Spark JAR tooinclude hello。  如果您使用 hello **spark 殼層**，則您可以透過使用 hello 包含 hello JAR **-（每瓶)**選項。  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

如果您想 tooexecute hello JAR 無相依性，請使用下列程式碼的 hello:

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

如果您使用筆記型電腦服務，例如 Azure HDInsight Jupyter 筆記本服務，您可以使用 hello**二手 magic**命令：

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

hello **（每瓶)**命令可讓您 tooinclude hello 兩個 Jar 的所需的**azure-cosmosdb-spark** （本身和 hello Azure DocumentDB Java SDK），並排除**scala-反映** ，讓它不會干擾晚總呼叫的 hello (Jupyter 筆記本 > 晚總 > Spark)。

### <a name="connect-spark-tooazure-cosmos-db-using-hello-connector"></a>連接 Spark tooAzure Cosmos DB 使用 hello 連接器
雖然 hello 通訊傳輸得較複雜，但是執行查詢，從 Spark tooAzure Cosmos DB 使用 hello 連接器是速度明顯加快。

hello，下列程式碼片段顯示如何 toouse hello Spark 內容中的連接器。

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

Hello 程式碼片段所示：

- **azure-cosmosdb-spark**包含 hello 所有 hello 必要的連接參數，其中包括 hello 慣用位置。 例如，您可以選擇 hello 讀取的複本和優先順序的順序。
- 只匯入 hello 必要的程式庫和主要金鑰和主機 toocreate hello Azure Cosmos DB 用戶端設定。

### <a name="execute-spark-queries-via-hello-connector"></a>查詢透過 hello 連接器的 Spark

下列範例會使用 hello Azure Cosmos 資料庫執行個體使用 hello hello 先前程式碼片段中所建立的 hello 指定唯讀金鑰。 hello 下列程式碼片段連線 toohello DepartureDelays.flights_pcoll 集合 （在 hello DoctorWho 如先前所指定的帳戶) 並執行查詢 tooextract hello 飛行延遲資訊的結果會不同於西雅圖的班機。

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-hello-spark-tooazure-cosmos-db-connector-implementation"></a>為何要使用 hello Spark tooAzure Cosmos DB 連接器實作？

連接 Spark tooAzure 案例通常是藉由使用 hello 連接器 Cosmos DB 位置：

* 您想 toouse Scala 並且更新它 tooinclude Python 包裝函式中有註明[問題 3： 加入 Python 包裝函式和範例](https://github.com/Azure/azure-cosmosdb-spark/issues/3)。
* 您有大量的資料 tootransfer Apache Spark 與 Azure Cosmos DB 之間。

toogive 您了解的 hello 查詢的效能差異，請參閱 hello[查詢測試回合 wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs)。

## <a name="distributed-aggregation-example"></a>分散式彙總範例
本節提供一些範例，示範如何搭配使用 Apache Spark 與 Azure Cosmos DB 來執行分散式彙總和分析。 Azure Cosmos DB 已經支援彙總，其中會討論 hello[地球小數位數的彙總與 Azure Cosmos DB 部落格](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/)。 以下是如何您就可以帶 toohello 接下來使用 Apache Spark 層級。

請注意，這些彙總位於參考 toohello [Spark tooAzure Cosmos DB 連接器筆記本](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb)。

### <a name="connect-tooflights-sample-data"></a>連接 tooflights 範例資料
這些彙總範例會存取儲存在 **DoctorWho** Azure Cosmos DB 資料庫中的一些航班效能資料。 tooconnect tooit，您需要下列程式碼片段的 tooutilize hello:

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

此片段中，我們也會持續 toorun 傳輸 hello 篩選的資料從 Azure Cosmos DB tooSpark 集的基本查詢 hello 後者可以在其中執行分散式彙總。 在此情況下，我們要求從西雅圖 (SEA) 出發的航班資料。

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

hello 下列結果所產生 hello Jupyter 筆記本服務從執行 hello 查詢。  請注意，所有的 hello 程式碼片段泛型和非 tooany 服務。

### <a name="running-limit-and-count-queries"></a>執行 LIMIT 和 COUNT 查詢
就像您是使用 tooin SQL/Spark SQL，讓我們開始**限制**查詢：

![Spark LIMIT 查詢](./media/spark-connector/spark-sql-query.png)

hello 下一個查詢是簡單又快速**計數**查詢：

![Spark COUNT 查詢](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a>GROUP BY 查詢
在接下來的這一組中，我們可以對 Azure Cosmos DB 資料庫輕鬆執行 **GROUP BY** 查詢：

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Spark GROUP BY 查詢圖形](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a>DISTINCT, ORDER BY 查詢
以下是 **DISTINCT, ORDER BY** 查詢：

![Spark GROUP BY 查詢圖形](./media/spark-connector/order-by-query.png)

### <a name="continue-hello-flight-data-analysis"></a>繼續 hello 飛行資料分析
您可以使用下列範例查詢 toocontinue 分析 hello 飛行資料 hello:

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a>從西雅圖出發的前 5 個延遲目的地 (城市)
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Spark 前幾個延遲圖形](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a>計算從西雅圖出發的目的地城市的中間延遲
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Spark 中間幾個延遲圖形](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a>後續步驟

如果您還沒有這麼做，請從 hello 下載 hello Spark tooAzure Cosmos DB 連接器[azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub 儲存機制和瀏覽 hello hello 儲存機制內的其他資源：

* [分散式彙總範例](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples) (英文)
* [指令碼和 Notebook 範例](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples) (英文)

您也可以 tooreview hello [Apache Spark SQL、 資料框架和資料集的指南](http://spark.apache.org/docs/latest/sql-programming-guide.html)和 hello [Azure HDInsight 上的 Apache Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md)發行項。
