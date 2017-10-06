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
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a>Apache Spark 串流：在 HDInsight 上使用 Spark 叢集處理來自 Azure 事件中樞的資料

在本文中，您可以建立資料流的範例，包括下列步驟的 hello Apache Spark:

1. 您可以使用獨立應用程式 tooingest 訊息到 Azure 事件中心。

2. 使用兩種不同的方法，您擷取 hello 訊息從事件中心中即時使用 Azure HDInsight 上的 Spark 叢集中執行的應用程式。

3. 建置串流分析管線 toopersist 資料 toodifferent 儲存系統，或從 hello 即時資料中取得見解。

## <a name="prerequisites"></a>必要條件

* Azure 訂用帳戶。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。

* HDInsight 上的 Apache Spark 叢集。 如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。

## <a name="spark-streaming-concepts"></a>Spark 串流處理概念

如需 Spark 串流的詳細說明，請參閱 [Apache Spark 串流概觀](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview)。 HDInsight 帶來的 hello Azure 的相同資料流功能 tooa Spark 叢集。  

## <a name="what-does-this-solution-do"></a>此解決方案有哪些功能？

在這篇文章 toocreate Spark 串流範例中，執行下列步驟的 hello:

1. 建立會接收事件串流的 Azure 事件中樞。

2. 執行本機的獨立應用程式會產生事件，並將其發送 toohello Azure 事件中心。 此 hello 範例應用程式發行在[https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples)。

3. 在 Spark 叢集上遠端執行串流應用程式，該應用程式可從 Azure 事件中樞讀取串流事件，並執行各種資料處理/分析。

## <a name="create-an-azure-event-hub"></a>建立 Azure 事件中樞

1. 登入 toohello [Azure 入口網站](https://ms.portal.azure.com)，然後按一下**新增**hello 在左上方的囉 」 畫面。

2. 按一下 [物聯網]，然後按一下 [事件中樞]。

    ![建立 Spark 串流範例的事件中樞](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "建立 Spark 串流範例的事件中樞")

3. 在 hello**建立命名空間**刀鋒視窗中，輸入命名空間名稱。 選擇定價層 （基本或標準） 的 hello。 而且請 toocreate hello 資源選擇 Azure 訂用帳戶、 資源群組和位置。 按一下**建立**toocreate hello 命名空間。

      ![提供 Spark 串流範例的事件中樞名稱](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "提供 Spark 串流範例的事件中樞名稱")

    > [!NOTE]
    > 您選取應該 hello 相同**位置**與您的 Apache Spark 叢集，在 HDInsight tooreduce 延遲和成本。
    >
    >

4. 在 hello 事件中樞命名空間清單中，按一下 hello 新建的命名空間。      


5. 在 hello 命名空間刀鋒視窗中，按一下 **事件中心**，然後按一下 **+ 事件中心**toocreate 新的事件中樞。
   
    ![建立 Spark 串流範例的事件中樞](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "建立 Spark 串流範例的事件中樞")

6. 輸入您的事件中樞、 組 hello 資料分割計數 too10 和訊息保留 too1 的名稱。 我們不保存此解決方案中的 hello 訊息，因此可以讓 hello 其餘部分，做為預設值，再按一下**建立**。
   
    ![提供 Spark 串流範例的事件中樞詳細資料](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "提供 Spark 串流範例的事件中樞詳細資料")

7. 新建立的事件中樞的 hello 會列在 hello 事件中心刀鋒視窗。
    
     ![檢視事件中心的 hello Spark 串流範例](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "hello 的檢視事件中心二手資料流範例")

8. 在 hello 命名空間刀鋒視窗中 （不 hello 特定事件中心刀鋒視窗），按一下 **共用存取原則**，然後按一下 **RootManageSharedAccessKey**。
    
     ![設定事件中樞原則 hello Spark 串流範例](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "hello 的設定事件中樞原則二手資料流範例")

9. 按一下 hello 複製按鈕 toocopy hello **RootManageSharedAccessKey**主要金鑰和連接字串 toohello 剪貼簿。 儲存這些 toouse hello 教學課程。
    
     ![檢視事件中樞原則機碼，例如 hello Spark 串流](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "hello 檢視事件中樞原則機碼二手資料流範例")

## <a name="send-messages-tooazure-event-hub-using-a-sample-scala-application"></a>傳送訊息 tooAzure 使用範例 Scala 應用程式的事件中樞

本節中您要使用的獨立本機 Scala 應用程式會產生事件資料流，並將它傳送 tooAzure 您稍早建立的事件中樞。 此應用程式可從 GitHub 取得，網址是： [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer)。 此處 hello 步驟假設您已經分叉時這個 GitHub 儲存機制。

1. 請確定您擁有 hello hello 您用來執行此應用程式的電腦上安裝下列項目。

    * Oracle Java Development Kit。 您可以從[這裡](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)安裝它。
    * Apache Maven。 您可以從 [這裡](https://maven.apache.org/download.cgi)下載。 指示 tooinstall Maven 可用[這裡](https://maven.apache.org/install.html)。

2. 開啟命令提示字元並瀏覽 toohello 位置複製 hello GitHub 儲存機制，用於 hello 範例 Scala 應用程式，執行下列命令 toobuild hello 應用程式的 hello。

        mvn package

3. hello 輸出 jar hello 應用程式， **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**，下方會建立**/目標**目錄。 您使用這個 JAR 稍後在這個發行項 tootest hello 完整解決方案。

## <a name="create-application-tooreceive-messages-from-event-hub-into-a-spark-cluster"></a>建立 Spark 叢集，以從事件中心應用程式 tooreceive 訊息 

我們有兩個方法 tooconnect Spark 資料流和 Azure 事件中樞、 收件者為基礎的連接和直接 DStream 基礎的連接。 Direct DStream 基礎 2017 年 1 月，在中引進 hello 2.0.3 版本。 它應該 tooreplace hello 原始收件者為基礎的連接，所以更好的效能和資源效率。 如需更多詳細資料，請參閱 [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs)。 Direct DStream 只支援 Spark 2.0+。

### <a name="build-applications-with-hello-dependency-toospark-eventhubs-connector"></a>建置應用程式與 hello 相依性 toospark eventhubs 連接器

我們也會發行臨時版 Spark-EventHubs GitHub 中的 hello。 toouse hello 臨時版 Spark EventHubs，hello 第一個步驟是 tooindicate GitHub 時加入下列項目 toopom.xml hello hello 來源儲存機制：

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

然後，您可以加入下列相依性 tooyour 專案 tootake hello 發行前版本的 hello。

Maven 相依性

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

SBT 相依性

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a>Direct DStream 連線

包含使用 Direct DStream 範例的預先建立 jar 檔案可在 [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar) 中下載。

hello jar 檔案包含三個範例的原始程式碼位於[https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream)。

將 [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) 作為範例：

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

在上述範例中，hello`eventhubParameters`是 hello 參數特定 tooa 單一 EventHubs 執行個體，而且您有 toopass 它 toohello`createDirectStreams`建構直接 DStream 物件對應 tooa 事件中樞命名空間的 API。 透過 hello 直接 DStream 物件，您可以呼叫任何 Spark Streaming API framework 所提供的 DStream API。 在此範例中，我們可以計算 hello 頻率，每個字 hello 最後 3 微批次間隔內。

### <a name="receiver-based-connection"></a>收件者型連線

Spark，串流 Scala，收到事件和路由 hello toodifferent 目的地時，所撰寫的範例應用程式將會位於[https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples)。 步驟 hello tooupdate hello 應用程式的事件中樞設定下，並建立 hello 輸出 jar。

1. 啟動 IntelliJ 概念，並從 hello 啟動螢幕選取**版本控制中簽出**，然後按一下 **Git**。
   
    ![Apache Spark 串流範例 - 從 Git 取得來源](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark 串流範例 - 從 Git 取得來源")

2. 在 hello**複製儲存機制**對話方塊中，提供 hello URL toohello Git 儲存機制 tooclone 從、 指定 hello 目錄 tooclone、，然後按一下**複製**。
   
    ![Apache Spark 串流範例 - 從 Git 複製](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark 串流範例 - 從 Git 複製")
3. 直到 hello 專案完全被複製，請依照 hello 提示。 按**Alt + 1** tooopen hello**專案檢視**。 它應該類似下列 hello。
   
    ![Apache Spark 串流範例 - 專案檢視](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark 串流範例 - 專案檢視")
4. 請確定 hello 應用程式程式碼會使用 Java8 編譯。 tooensure 此，依序按一下**檔案**，按一下 **專案結構**，在 hello**專案**索引標籤上，請確定專案語言層級設定得**8-Lambda，類型註解等**。
   
    ![Apache Spark 串流範例 - 設定編譯器](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark 串流範例 - 設定編譯器")
5. 開啟 hello **pom.xml** ，並確定 hello Spark 版本是否正確。 在下`<properties>`節點中，尋找下列程式碼片段的 hello 和驗證 hello Spark 版本。

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. hello 應用程式需要呼叫的相依性 jar **JDBC 驅動程式 jar**。 這是必要的 toowrite hello 訊息，從事件中心會接收到 Azure SQL database。 您可以從[這裡](https://msdn.microsoft.com/sqlserver/aa937724.aspx)下載此 jar (4.1 或更新版本)。 新增參考 toothis jar hello 專案文件庫中。 執行下列步驟的 hello:
     
     1. 從 IntelliJ 概念您尚未開啟 hello 應用程式 視窗中，按一下 **檔案**，按一下 **專案結構**，然後按一下**文件庫**。 
     2. 按一下 hello 加入圖示 (![加入圖示](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png))，按一下  **Java**，然後瀏覽您下載 hello JDBC 驅動程式 jar 的 toohello 位置。 請遵循 hello 提示 tooadd hello jar 檔案 toohello 專案程式庫。

         ![新增遺失的相依性](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "新增遺失的相依性 jar")
     3. 按一下 [Apply (套用)] 。

7. 建立 hello 輸出 jar 檔案。 執行下列步驟的 hello。

   1. 在 hello**專案結構**對話方塊中，按一下 **成品**hello 加上符號，然後按一下。 Hello 快顯對話方塊方塊中，按一下  **JAR**，然後按一下**具有相依性的模組從**。      
       
       ![Apache Spark 串流範例 - 建立 jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark 串流範例 - 建立 jar")
   2. 在 hello**從模組建立 JAR**對話方塊方塊中，按一下 hello 省略符號 (![省略](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) 針對 hello**主要類別**。
   3. 在 hello**選取主要類別**對話方塊方塊中，選取任何 hello 可用的類別，然後按一下**確定**。
      
       ![Apache Spark 串流範例 - 選取 jar 的類別](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark 串流範例 - 選取 jar 的類別")
   4. 在 hello**從模組建立 JAR**對話方塊方塊中，請確定該 hello 選項太**擷取 toohello 目標 JAR**已選取，然後按一下**確定**。 這會建立具有所有相依性的單一 JAR。
      
       ![Apache Spark 串流範例 - 從模組建立 jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark 串流範例 - 從模組建立 jar")
   5. hello**輸出配置**索引標籤會列出所有 hello （每瓶） 的 hello Maven 專案的一部分。 您可以選取和刪除 hello 所在的 hello Scala 應用程式並沒有直接相依。 對於此建立 hello 應用程式，您可以移除以外的所有 hello 最後一個 (**spark-串流處理的資料-持續性-範例編譯輸出**)。 選取 hello （每瓶) toodelete，然後按一下hello**刪除**圖示 (![刪除圖示](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png))。
      
       ![Apache Spark 串流範例 - 將擷取的 jar 刪除](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark 串流範例 - 將擷取的 jar 刪除")
      
       請確定**上進行建置**選取方塊，以確保每次建立或更新 hello 專案建立該 hello jar。 按一下 [Apply (套用)] 。
   6. 在 [hello**輸出版面配置**索引標籤上，直接在 hello 底部 hello**可用的項目**] 方塊中，您擁有 hello SQL JDBC jar 您加入先前 toohello 專案程式庫。 您必須新增此 toohello**輸出配置** 索引標籤。Hello jar 檔案，以滑鼠右鍵按一下，然後按一下**擷取到輸出根**。
      
       ![Apache Spark 串流範例 - 擷取相依性 jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark 串流範例 - 擷取相依性 jar")  
      
       hello**輸出配置** 索引標籤現在看起來應該像這樣。
      
       ![Apache Spark 串流範例 - 最終輸出索引標籤](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark 串流範例 - 最終輸出索引標籤")        
      
       在 hello**專案結構**對話方塊中，按一下 **套用**，然後按一下**確定**。    
   7. 在 hello 功能表列中，按一下**建置**，然後按一下**進行專案**。 您也可以按一下**組建成品**toocreate hello jar。 hello 輸出 jar 下方會建立**\classes\artifacts**。
      
       ![Apache Spark 串流範例 - 輸出 jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark 串流範例 - 輸出 jar")

## <a name="run-hello-application-remotely-on-a-spark-cluster-using-livy"></a>使用晚總的 Spark 叢集上的遠端執行 hello 應用程式

在本文中您使用晚總 toorun hello Apache Spark 串流應用程式從遠端的 Spark 叢集。 如需如何 toouse 晚總與 HDInsight Spark 叢集的詳細討論，請參閱[送出工作遠端 tooan Apache Spark 叢集 Azure HDInsight 上](hdinsight-apache-spark-livy-rest-interface.md)。 您可以開始執行 hello Spark 串流應用程式之前，有幾件事您應該執行：

1. 啟動 hello 本機的獨立應用程式 toogenerate 事件，並傳送 tooEvent 中樞。 使用下列命令 toodo 因此 hello:

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. 資料流 jar 複製 hello (**spark-串流處理的資料-持續性-examples.jar**) toohello hello 叢集相關聯的 Azure Blob 儲存體。 這可讓 hello jar 存取 tooLivy。 您可以使用[ **AzCopy**](../storage/common/storage-use-azcopy.md)，命令列公用程式，toodo 因此。 有許多的其他用戶端中，您可以使用 tooupload 資料。 您可以在 [在 HDInsight 上將 Hadoop 作業的資料上傳](hdinsight-upload-data.md)中找到其詳細資訊。
3. 安裝 CURL hello 執行這些應用程式所在的電腦上。 我們使用 CURL tooinvoke hello 晚總端點 toorun hello 遠端作業。

### <a name="run-hello-spark-streaming-application-tooreceive-hello-events-into-an-azure-storage-blob-as-text"></a>執行 hello Spark 串流應用程式 tooreceive hello 事件至 Azure 儲存體 Blob 做為文字

開啟命令提示字元，巡覽 toohello 目錄 CURL，安裝並執行下列命令 （取代使用者名稱/密碼與叢集名稱） 的 hello:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

hello hello 檔案中的參數**inputBlob.txt**的定義方式如下：

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

讓我們了解 hello 輸入檔中的 hello 參數為何：

* **檔案**是 hello 路徑 toohello 應用程式 jar 檔 hello 與 hello 叢集相關聯的 Azure 儲存體帳戶。
* **className**是 hello hello jar 中的 hello 類別名稱。
* **引數**是 hello hello 類別所需的引數清單
* **numExecutors**是 hello Spark toorun hello 串流處理應用程式所使用的核心數目。 這應該一律至少兩次 hello 事件中樞分割區數目。
* **executorMemory**， **executorCores**， **driverMemory** toohello 串流應用程式是用參數 tooassign 必要資源。

> [!NOTE]
> 您不需要 toocreate hello 輸出資料夾 （EventCheckpoint、 EventCount/EventCount10） 做為參數。 hello 串流處理應用程式會為您建立它們。
>
>

當您執行 hello 命令時，您應該會看到類似 hello 下列輸出：

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

記下的 hello 批次識別碼 hello 的 hello 輸出 （在此範例中，它是 '1'） 的最後一行。 hello 應用程式的 tooverify 順利執行，您可以查看您 hello 叢集相關聯的 Azure 儲存體帳戶和您應該會看見 hello **/EventCount/EventCount10**那里建立資料夾。 這個資料夾應該包含擷取的事件處理 hello 中的指定時間週期 hello 參數的 hello 數目的 blob**批次間隔-中-秒**。

hello Spark 串流應用程式會繼續 toorun，直到您將其清除。 因此，toodo，請使用下列命令的 hello:

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-storage-blob-as-json"></a>執行 hello 應用程式 tooreceive hello 事件至 Azure 儲存體 Blob 為 JSON
開啟命令提示字元，巡覽 toohello 目錄 CURL，安裝並執行下列命令 （取代使用者名稱/密碼與叢集名稱） 的 hello:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

hello hello 檔案中的參數**inputJSON.txt**的定義方式如下：

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

您指定 hello 上一個步驟中的 hello 文字輸出的類似 toowhat 的 hello 參數。 同樣地，您不需要 toocreate hello 輸出資料夾 （EventCheckpoint、 EventCount/EventCount10） 做為參數。 hello 串流處理應用程式會為您建立它們。

 後執行 hello 命令，您可以查看您 hello 叢集相關聯的 Azure 儲存體帳戶中，您應該會看見 hello **/EventStore10**那里建立資料夾。 開啟任何檔案前面加上**一部分-** ，您應該會看見 hello 事件處理是 JSON 格式。

### <a name="run-hello-applications-tooreceive-hello-events-into-a-hive-table"></a>遇到 hello 應用程式 tooreceive hello 事件的 Hive 資料表
toorun hello Spark 串流應用程式資料流的事件，加入 Hive 資料表您需要一些額外的元件。 它們是：

* datanucleus-api-jdo-3.2.6.jar
* datanucleus-rdbms-3.2.9.jar
* datanucleus-core-3.2.10.jar
* hive-site.xml

hello **d**檔案位於您的 HDInsight Spark 叢集，在`/usr/hdp/current/spark-client/lib`。 hello **hive-site.xml**位於`/usr/hdp/current/spark-client/conf`。

您可以使用[WinScp](http://winscp.net/eng/download.php) toocopy hello 叢集 tooyour 本機電腦從這些檔案。 然後，您可以使用工具 toocopy tooyour 儲存體帳戶的這些檔案與 hello 叢集相關聯。 如需有關如何 tooupload 檔案 toohello 儲存體帳戶的詳細資訊，請參閱[HDInsight 中的 Hadoop 工作的資料上傳](hdinsight-upload-data.md)。

一旦您複製了 hello 檔案 tooyour Azure 儲存體帳戶，開啟命令提示字元，巡覽 toohello 目錄 CURL，安裝並執行下列命令 （取代使用者名稱/密碼與叢集名稱） 的 hello:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

hello hello 檔案中的參數**inputHive.txt**的定義方式如下：

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

您指定 hello 先前步驟中的 hello 文字輸出的類似 toowhat 的 hello 參數。 同樣地，您不需要 toocreate hello 輸出資料夾 （EventCheckpoint、 EventCount/EventCount10） 或 hello 輸出做為參數的 Hive 資料表 (EventHiveTable10)。 hello 串流處理應用程式會為您建立它們。 請注意該 hello **（每瓶)**和**檔案**選項包含路徑 toohello d 檔案和 hello hive-site.xml 複製過來 toohello 儲存體帳戶。

hello hive 資料表的 tooverify 已成功建立，您可以指定 SSH 成 hello 叢集和執行的 Hive 查詢。 如需指示，請參閱 [利用 SSH 搭配使用 Hive 與 HDInsight 中的 Hadoop](hdinsight-hadoop-use-hive-ssh.md)。 當您使用 SSH 連線時，您可以執行下列命令 tooverify hello hello Hive 資料表， **EventHiveTable10**，會建立。

    show tables;

您應該會看到類似 toohello 下列輸出：

    OK
    eventhivetable10
    hivesampletable

您也可以執行 SELECT 查詢 tooview hello hello 資料表內容。

    SELECT * FROM eventhivetable10 LIMIT 10;

您應該會看到類似 hello 下列輸出：

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


### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-sql-database-table"></a>執行 hello 應用程式到 Azure SQL 資料庫資料表 tooreceive hello 事件
執行此步驟之前，請先確定您已建立 Azure SQL Database。 如需指示，請參閱[快速建立 SQL 資料庫](../sql-database/sql-database-get-started.md)。 本章節 toocomplete，您需要資料庫名稱、 資料庫伺服器名稱，和 hello 資料庫系統管理員認證，做為參數的值。 您雖然不需要 toocreate hello 資料庫資料表。 hello Spark 串流應用程式會為您建立的。

開啟命令提示字元，巡覽 toohello 目錄 CURL，安裝並執行下列命令的 hello:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

hello hello 檔案中的參數**inputSQL.txt**的定義方式如下：

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

hello 應用程式的 tooverify 順利執行，您可以連接使用 SQL Server Management Studio toohello Azure SQL database。 如需指示，請參閱 toodo [tooSQL 資料庫連接使用 SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md)。 一旦您已連線的 toohello 資料庫，您可以瀏覽 toohello **EventContent** hello 串流處理應用程式所建立的資料表。 您可以從 hello 資料表執行快速的查詢 tooget hello 資料。 執行下列查詢的 hello:

    SELECT * FROM EventCount

您應該會看到類似 toohello 下列輸出：

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


## <a name="seealso"></a>另請參閱
* [概觀：Azure HDInsight 上的 Apache Spark](hdinsight-apache-spark-overview.md)
* [收件者型連線和 Direct DStream 的設計](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a>案例
* [Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析](hdinsight-apache-spark-use-bi-tools.md)
* [Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [使用 HDInsight 中的 Spark 進行網站記錄分析](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>建立及執行應用程式
* [使用 Scala 建立獨立應用程式](hdinsight-apache-spark-create-standalone-application.md)
* [利用 Livy 在 Spark 叢集上遠端執行作業](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>工具和擴充功能
* [HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 個應用程式](hdinsight-apache-spark-intellij-tool-plugin.md)
* [從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [搭配 Jupyter Notebook 使用外部套件](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>管理資源
* [管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源](hdinsight-apache-spark-resource-manager.md)
* [追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
