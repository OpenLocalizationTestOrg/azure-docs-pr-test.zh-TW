---
title: "aaaWhat 是 HDInsight、 hello Hadoop 技術堆疊與叢集嗎？ - Azure | Microsoft Docs"
description: "簡介 Hadoop 技術 tooHDInsight 和 hello 堆疊和元件，包括 Spark、 Kafka、 Hive、 HBase 巨量資料分析。"
keywords: "azure 的 hadoop、 hadoop azure、 hadoop 簡介、 hadoop 簡介、 hadoop 技術堆疊、 簡介 toohadoop、 簡介 toohadoop，什麼是什麼是 hadoop 叢集的 hadoop 叢集中，hadoop 用途"
services: hdinsight
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: e56a396a-1b39-43e0-b543-f2dee5b8dd3a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: cgronlun
ms.openlocfilehash: 0aed3d1a6cf3c0cdc3b036cfa4865a2e0b58e2c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-hdinsight-hello-hadoop-technology-stack-and-hadoop-clusters"></a>簡介 tooAzure HDInsight、 hello Hadoop 技術堆疊，以及 Hadoop 叢集
 本文章提供簡介 tooAzure HDInsight hello Hadoop 技術堆疊的雲端分佈。 它也涵蓋了 Hadoop 叢集的定義及其使用時機。 

## <a name="what-is-hdinsight-and-hello-hadoop-technology-stack"></a>HDInsight 及 hello Hadoop 技術堆疊是什麼？ 
Azure HDInsight 是雲端分佈 hello Hadoop 元件從 hello [Hortonworks Data Platform (HDP)](https://hortonworks.com/products/data-center/hdp/)。 [Apache Hadoop](http://hadoop.apache.org/)已 hello 原始開放原始碼架構分散式的處理和分析大型的資料集，在叢集的電腦上。 


hello Hadoop 技術堆疊包含相關的軟體和公用程式，包括 Apache Hive、 HBase、 Spark、 Kafka，及其他等等。 toosee 可用 Hadoop 技術堆疊上的元件 HDInsight，請參閱[元件和版本適用於 HDInsight][component-versioning]。 深入了解 HDInsight 中的 Hadoop tooread 看到 hello [hdinsight 的 Azure 功能頁面上](https://azure.microsoft.com/services/hdinsight/)。

## <a name="what-is-a-hadoop-cluster-and-when-do-you-use-it"></a>什麼是 Hadoop 叢集，以及何時使用它？
*Hadoop* 也是具有下列各項的叢集類型：

* 用於作業排程和資源管理的 YARN
* 用於平行處理的 MapReduce
* hello Hadoop 分散式檔案系統 (HDFS)
  
Hadoop 叢集最常用於已儲存資料的批次處理。 HDInsight 中的其他叢集類型具有其他功能：Spark 因為其更快速的記憶體內部處理而日益普及。 如需詳細資訊，請參閱 [HDInsight 上的叢集類型](#overview)。

## <a name="what-is-big-data"></a>什麼是巨量資料？
巨量資料是指任何極為龐大的數位資訊，例如︰

* 工業設備的感應器資料
* 從網站收集的客戶活動
* Twitter 新聞摘要

巨量資料的收集量快速增加，收集速度加快，收集格式也愈來愈多。 它可以是歷程記錄 （表示儲存） 或即時 （表示 hello 來源資料流處理）。 

## <a name="overview"></a>HDInsight 中的叢集類型
HDInsight 包含特定叢集類型和叢集自訂功能，例如新增元件、公用程式及語言。

### <a name="spark-kafka-interactive-hive-hbase-customized-and-other-cluster-types"></a>Spark、Kafka、Interactive Hive、HBase、自訂和其他叢集類型
HDInsight 提供下列叢集類型的 hello:

* **[Apache Hadoop](https://wiki.apache.org/hadoop)**： 使用[HDFS](#hdfs)， [YARN](#yarn)資源管理及簡單[MapReduce](#mapreduce)程式設計模型 tooprocess 和分析平行批次資料。
* **[Apache Spark](http://spark.apache.org/)**: 平行處理架構，可支援的巨量資料分析應用程式中，記憶體中處理 tooboost hello 效能 （SQL)、 資料流處理資料，二手運作和機器學習。 請參閱[什麼是 HDInsight 中的 Apache Spark？](hdinsight-apache-spark-overview.md)
* **[Apache HBase](http://hbase.apache.org/)**：建置於 Hadoop 上的 NoSQL 資料庫，可針對大量非結構化及半結構化資料 (可能是數十億的資料列乘以數百萬的資料行)，提供隨機存取功能和強大一致性。 請參閱[什麼是 HDInsight 上的 HBase？](hdinsight-hbase-overview.md)
* **[Microsoft R 伺服器](https://msdn.microsoft.com/microsoft-r/rserver)**︰可用來裝載和管理並行、分散式 R 程序的伺服器。 會視需要存取 tooscalable，分析在 HDInsight 上的分散式方法的情況下，提供資料科學家，統計學家和 R 程式設計人員。 請參閱 [HDInsight 中的 R 伺服器概觀](hdinsight-hadoop-r-server-overview.md)。
* **[Apache Storm](https://storm.incubator.apache.org/)**：分散式、即時的運算系統，可快速處理大型的資料串流。 Storm 以受管理叢集的形式在 HDInsight 中提供。 請參閱＜ [使用 Storm 和 Hadoop 來分析即時感應器資料](hdinsight-storm-sensor-data-analysis.md)＞。
* **[Apache 互動式 Hive 預覽 (也稱為︰Live Long and Process)](https://cwiki.apache.org/confluence/display/Hive/LLAP)**︰更快速之互動式 Hive 查詢的記憶體內快取。 請參閱[在 HDInsight 中使用互動式 Hive](hdinsight-hadoop-use-interactive-hive.md)。
* **[Apache Kafka](https://kafka.apache.org/)**︰用來建立串流資料管線和應用程式的開放原始碼平台。 Kafka 也會提供訊息佇列功能，可讓您 toopublish 和訂閱 toodata 資料流。 請參閱[簡介 tooApache HDInsight 上 Kafka](hdinsight-apache-kafka-introduction.md)。

您也可以設定使用下列方法 hello 叢集：
* **[已加入網域的叢集預覽](hdinsight-domain-joined-introduction.md)**： 叢集中加入 tooan Active Directory 網域，以便您可以控制的存取，並提供控管資料。
* **[具指令碼動作的自訂叢集](hdinsight-hadoop-customize-cluster-linux.md)**：具指令碼的叢集，該指令碼於佈建期間執行，並安裝其他元件。

### <a name="example-cluster-customization-scripts"></a>範例叢集自訂指令碼
指令碼動作是在 Linux 上的 Bash 指令碼，在叢集佈建，期間執行，且可以使用的 tooinstall hello 叢集上的其他元件。 

hello 下列指令碼範例是根據 hello HDInsight 團隊提供：

* **[色調](hdinsight-hadoop-hue-linux.md)**： 一組在叢集中的 web 應用程式使用 toointeract。 僅限於 Linux 叢集。
* **[Giraph](hdinsight-hadoop-giraph-install-linux.md)**： 處理 toomodel 事項或人員之間的關聯性的圖形。
* **[Solr](hdinsight-hadoop-solr-install-linux.md)**：一種企業級搜尋平台，可對資料進行全文檢索搜尋。

如需開發您自己的指令碼動作相關資訊，請參閱 [使用 HDInsight 開發指令碼動作](hdinsight-hadoop-script-actions-linux.md)。

## <a name="components-and-utilities-on-hdinsight-clusters"></a>HDInsight 叢集上的元件和公用程式
hello 下列元件和公用程式會包含在 HDInsight 叢集上：

* **[Ambari](#ambari)**：叢集佈建、管理、監視和公用程式。
* **[Avro](#avro)**  （Microsoft.NET 程式庫 Avro）： hello Microsoft.NET 環境的資料序列化。 
* **[Hive & HCatalog](#hive)**：類似 SQL 的查詢，以及資料表和儲存體管理層。
* **[Mahout](#mahout)**：適用於可調整的機器學習應用程式。
* **[MapReduce](#mapreduce)**：Hadoop 分散式處理和資源管理的傳統架構。 請參閱 [YARN](#yarn)。
* **[Oozie](#oozie)**：工作流程管理。
* **[Phoenix](#phoenix)**：對 HBase 的關聯式資料庫層。
* **[Pig](#pig)**：簡單撰寫 MapReduce 轉換的指令碼。
* **[Sqoop](#sqoop)**：資料匯入和匯出。
* **[Tez](#tez)**： 大規模有效率地允許資料密集處理序 toorun。
* **[YARN](#yarn)**： 屬於 hello Hadoop 核心程式庫資源管理。
* **[ZooKeeper](#zookeeper)**：協調分散式系統中的程序。

> [!NOTE]
> Hello 特定元件的詳細資訊及版本資訊，請參閱[Hadoop 元件與 HDInsight 中的版本][component-versioning]
>
>

### <a name="ambari"></a>Ambari
Apache Ambari 可用來佈建、管理及監視 Apache Hadoop 叢集。 它包含的運算子工具的直覺式集合和一組強大的應用程式開發介面中隱藏 hello 複雜度 Hadoop，以簡化 hello 作業的叢集。 在 Linux 上的 HDInsight 叢集提供兩者 hello Ambari web UI 和 hello Ambari REST API。 HDInsight 叢集上的 Ambari 檢視允許外掛程式 UI 功能。
請參閱[使用 Ambari 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md)和 <a target="_blank" href="https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md">Apache Ambari API 參考</a>。

### <a name="avro"></a>Avro (Microsoft .NET Library for Avro)
hello Avro 的 Microsoft.NET 程式庫實作序列化 hello Microsoft.NET 環境的 hello Apache Avro compact 的二進位資料交換格式。 它會定義不限語言的結構描述，以某種語言序列化的資料便可使用另一個語言讀取。 Hello 格式的詳細的資訊位於 hello < 目標 = _ 「 空白 」 href ="http://avro.apache.org/docs/current/spec.html"> Apache Avro 規格</a>。 hello 格式 Avro 檔案支援 hello 的分散式程式設計模型的 MapReduce： 檔案是 「 可分割的圖形 」，表示您可以搜尋檔案中的任何時間點，然後從特定的區塊開始讀取。 toofind 出的方式，請參閱[hello Microsoft.NET 程式庫與資料序列化為 Avro](hdinsight-dotnet-avro-serialization.md)。 Linux 為基礎的叢集支援 toocome。

### <a name="hdfs"></a>HDFS
Hadoop 分散式檔案系統 (HDFS) 是的與 YARN 和 MapReduce hello 核心 Hadoop 技術的檔案系統。 它的 hello 標準檔案系統上 HDInsight Hadoop 叢集。 請參閱[從 HDFS 相容儲存體查詢資料](hdinsight-hadoop-use-blob-storage.md)。

### <a name="hive"></a>Hive 和 HCatalog
<a target="_blank" href="http://hive.apache.org/">Apache Hive</a>是資料倉儲可讓您 tooquery 的 Hadoop 上建置的軟體，並使用一種稱為 HiveQL 類似 SQL 的語言來管理分散式儲存體中的大型資料集。 如同 Pig，Hive 是 MapReduce 的抽象概念，可將查詢轉譯成一系列的 MapReduce 作業。 Hive 是 Pig 比接近 tooa 關聯式資料庫管理系統，是使用其他結構化資料。 針對非結構化資料，Pig 是 hello 更好的選擇。 請參閱 [在 HDInsight 上將 Hive 與 Hadoop 搭配使用](hdinsight-use-hive.md)。

<a target="_blank" href="https://cwiki.apache.org/confluence/display/Hive/HCatalog/">Apache HCatalog</a> 是 Hadoop 的資料表和儲存體管理層，可為您提供資料的關聯式檢視。 在 HCatalog 中，您可以任何適用於 Hive SerDe (序列化程式-還原序列化程式) 的格式來讀寫和撰寫檔案。

### <a name="mahout"></a>Mahout
<a target="_blank" href="https://mahout.apache.org/">Apache Mahout</a> 是在 Hadoop 上執行的機器學習演算法程式庫。 機器學習服務應用程式使用統計資料的原則，告訴系統 toolearn 資料和 toouse 過去結果 toodetermine 未來行為。 請參閱＜ [在 Hadoop 上使用 Mahout 來產生電影推薦](hdinsight-mahout.md)＞。

### <a name="mapreduce"></a>MapReduce
MapReduce 是 Hadoop 的 hello 舊版的軟體架構，以平行方式撰寫的應用程式 toobatch 處理大型資料集。 MapReduce 工作分割大型資料集，並將 hello 資料組織成進行處理的索引鍵-值組。 MapReduce 作業會在 [YARN](#yarn) 上執行。 請參閱<a target="_blank" href="http://wiki.apache.org/hadoop/MapReduce">MapReduce</a> hello Hadoop Wiki 中。

### <a name="oozie"></a>Oozie
<a target="_blank" href="http://oozie.apache.org/">Apache Oozie</a> 是可管理 Hadoop 工作的工作流程協調系統。 它與 hello Hadoop 堆疊整合並支援 MapReduce、 Pig、 Hive 和 Sqoop Hadoop 工作。 它也可以使用的 tooschedule 工作特定 tooa 系統，例如 Java 程式或殼層指令碼。 請參閱 [搭配使用 Oozie 與 Hadoop](hdinsight-use-oozie-linux-mac.md)。

### <a name="phoenix"></a>Phoenix
<a  target="_blank" href="http://phoenix.apache.org/">Apache Phoenix</a> 是對 HBase 的關聯式資料庫層。 In Phoenix 包含 JDBC 驅動程式，可讓您 tooquery 及直接管理的 SQL 資料表。 Phoenix 會將查詢和其他陳述式轉譯為原生 NoSQL API 呼叫，而不是使用 MapReduce。因此能更快速地在 NoSQL 存放區上套用。 請參閱[搭配 HBase 叢集使用 Phoenix 和 SQuirreL](hdinsight-hbase-phoenix-squirrel.md)。

### <a name="pig"></a>Pig
<a  target="_blank" href="http://pig.apache.org/">Apache Pig</a>是高層級的平台，可讓您 tooperform 複雜 MapReduce 轉換大型資料集使用稱為 Pig 拉丁文的簡單指令碼語言。 Pig 轉換 hello 拉丁 Pig 指令碼，使其將在 Hadoop 內執行。 您可以建立使用者定義函數 (Udf) tooextend Pig 拉丁。 請參閱 [搭配使用 Pig 與 Hadoop](hdinsight-use-pig.md)。

### <a name="sqoop"></a>Sqoop
<a  target="_blank" href="http://sqoop.apache.org/">Apache Sqoop</a> 是在 Hadoop 與 SQL 之類的關聯式資料庫或其他結構化資料儲存之間盡可能以最高效率傳輸大量資料的工具。 請參閱＜ [使用 Sqoop 與 Hadoop](hdinsight-use-sqoop.md)＞。

### <a name="tez"></a>Tez
<a  target="_blank" href="http://tez.apache.org/">Apache Tez</a> 是以 Hadoop YARN 為建置基礎的應用程式架構，可執行一般資料處理的複雜非循環圖。 它是更有彈性且功能強大後續 toohello MapReduce 架構，允許需要大量資料的處理程序，例如登錄區，toorun 更有效率地在標尺。 請參閱 [＜使用 Hive 和 HiveQL＞中的＜使用 Apache Tez 以提升效能＞](hdinsight-use-hive.md#usetez)。

### <a name="yarn"></a>YARN
Apache YARN 為 hello 新一代的 MapReduce （MapReduce 2.0 或 MRv2），並支援處理具有較大的延展性和即時處理 MapReduce 批次之外的資料處理案例。 YARN 能提供資源管理和分散式應用程式架構。 MapReduce 作業會在 YARN 上執行。 請參閱 <a target="_blank" href="http://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html">Apache Hadoop NextGen MapReduce (YARN)</a>。

### <a name="zookeeper"></a>ZooKeeper
<a  target="_blank" href="http://zookeeper.apache.org/">Apache ZooKeeper</a> 使用資料暫存器 (znode) 的共用階層式命名空間，協調大型分散式系統中的程序。 Znodes 包含少量的處理程序所需的資訊 toocoordinate 中繼： 狀態、 位置、 組態和等等。 請參閱[搭配使用 HBase 叢集與 Apache Phoenix 的 ZooKeeper](hdinsight-hbase-phoenix-squirrel-linux.md) 範例。 

## <a name="programming-languages-on-hdinsight"></a>HDInsight 上的程式設計語言
HDInsight 叢集 (Spark、HBase、Kafka、Hadoop 和其他叢集) 支援許多種程式設計語言，但某些語言並未預設安裝。 程式庫、 模組，或未根據預設，安裝的封裝[使用指令碼動作 tooinstall hello 元件](hdinsight-hadoop-script-actions-linux.md)。 

### <a name="default-programming-language-support"></a>預設的程式設計語言支援
根據預設，HDInsight 叢集可支援：

* Java
* Python

其他語言則可以使用[指令碼動作](hdinsight-hadoop-script-actions-linux.md)來加以安裝。

### <a name="java-virtual-machine-jvm-languages"></a>Java 虛擬機器 (JVM) 語言
Java 虛擬機器 (JVM); 可以執行的許多 Java 以外的語言不過，執行這些語言的某些可能需要額外 hello 叢集上安裝的元件。

HDInsight 叢集上支援下列以 JVM 為基礎的語言：

* Clojure
* Jython (適用於 Java 的 Python)
* Scala

### <a name="hadoop-specific-languages"></a>Hadoop 專屬語言
HDInsight 叢集支援下列語言的特定 toohello Hadoop 技術堆疊 hello:

* 適用於 Pig 工作的 Pig Latin
* 適用於 Hive 工作和 SparkSQL 的 HiveQL

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight Standard 和 HDInsight Premium
HDInsight 提供兩種類型的巨量資料雲端提供項目：Standard 和 Premium。 HDInsight 標準提供企業規模叢集的組織可以使用 toorun 其巨量資料工作負載。 HDInsight Premium 以標準功能為基礎，並提供 HDInsight 叢集的進階分析與安全性功能。 如需詳細資訊，請參閱 [Azure HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium)

## <a name="microsoft-business-intelligence-and-hdinsight"></a>Microsoft 商業智慧和 HDInsight
熟悉的商務智慧 (BI) 工具擷取、 分析和報表資料使用 Power Query 增益集的任一個 hello 與 HDInsight 整合或 hello Microsoft Hive ODBC 驅動程式：

* [有了 Power Query 連接 Excel tooHadoop](hdinsight-connect-excel-power-query.md)： 了解如何 tooconnect Excel toohello 儲存的 Azure 儲存體帳戶 hello 使用 Microsoft Power Query for Excel 的資料從您的 HDInsight 叢集。 必要的 Windows 工作站。 
* [以 hello Microsoft Hive ODBC 驅動程式連接 Excel tooHadoop](hdinsight-connect-excel-hive-odbc-driver.md)： 了解如何從具有 HDInsight tooimport 資料 hello Microsoft Hive ODBC 驅動程式。 必要的 Windows 工作站。 
* [Microsoft 雲端平台](http://www.microsoft.com/server-cloud/solutions/business-intelligence/default.aspx)： 了解 Power BI for Office 365，請下載 hello SQL Server 試用版，並設定 SharePoint Server 2013 和 SQL Server BI。
* [SQL Server Analysis Services](http://msdn.microsoft.com/library/hh231701.aspx)
* [SQL Server Reporting Services](http://msdn.microsoft.com/library/ms159106.aspx)


## <a name="next-steps"></a>後續步驟

* [開始使用 HDInsight 中的 Hadoop](hdinsight-hadoop-linux-tutorial-get-started.md)：佈建 HDInsight Hadoop 叢集以及執行範例 Hive 查詢的快速入門教學課程。
* [開始使用 HDInsight 中的 Spark](hdinsight-apache-spark-jupyter-spark-sql.md)︰建立 Spark 叢集和執行互動式 Spark SQL 查詢的快速入門教學課程。
* [在 HDInsight 上使用 R 伺服器](hdinsight-hadoop-r-server-get-started.md)︰開始在 HDInsight Premium 中使用 R 伺服器。
* [佈建的 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)： 了解如何 tooprovision HDInsight Hadoop 叢集透過 hello Azure 入口網站、 Azure CLI 或 Azure PowerShell。


[component-versioning]: hdinsight-component-versioning.md
[zookeeper]: http://zookeeper.apache.org/