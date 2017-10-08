---
title: "aaaWhat 會位於 Azure HDInsight HBase 嗎？ | Microsoft Docs"
description: "簡介 tooApache 在 HDInsight HBase，Hadoop 上建置的 NoSQL 資料庫。 了解使用案例，然後比較 HBase tooother Hadoop 叢集。"
keywords: "bigtable,nosql,什麼是 hbase,apache hbase,hbase,habase 概觀,"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: d2a76d53-133a-4849-a30c-88d9c794391c
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 0d28378d07b1a168e38748548578be11310d2228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hbase-in-hdinsight-a-nosql-database-that-provides-bigtable-like-capabilities-for-hadoop"></a>什麼是 HDInsight 中的 HBase：為 Hadoop 提供類似 BigTable 功能的 NoSQL 資料庫
Apache HBase 是開放原始碼的 NoSQL 資料庫，其建置於 Hadoop 上並模仿 Google BigTable。 HBase 可針對依資料行系列組織的無結構描述資料庫中的大量非結構化及半結構化資料，提供隨機存取功能和強大一致性。

資料會儲存在 hello 資料表，資料列和資料列中的依資料欄系列。 HBase 是 hello 兩者皆非 hello 資料行，也不 hello 類型的資料儲存在它們的意義上 schemaless 資料庫需要 toobe 之前使用這些定義。 hello 開放原始碼縮放數千個節點上以線性方式 toohandle pb 計的資料。 它會依賴資料備援、 批次處理和其他功能所提供的 hello Hadoop 生態系統中的分散式應用程式。

## <a name="how-is-hbase-implemented-in-azure-hdinsight"></a>Azure HDInsight 中的 HBase 是如何實作的？
為受管理的叢集整合到 Azure 環境的 hello 提供 HDInsight HBase。 hello 叢集是直接在設定的 toostore 資料[Azure 儲存體](./hdinsight-hadoop-use-blob-storage.md)或[Azure Data Lake Store](./hdinsight-hadoop-use-data-lake-store.md)，其中提供低延遲、 效能及成本的選項中增加的彈性。 這可讓客戶 toobuild 之互動網站使用大型資料集，儲存感應器和遙測資料包含數百萬個結束點和 tooanalyze toobuild 服務將此資料與 Hadoop 工作。 HBase 和 Hadoop 是很好的起點巨量資料專案中 Azure;尤其，他們可以啟用即時應用程式 toowork 大型資料集。

hello HDInsight 實作會利用 hello 向外延展架構的 HBase tooprovide 自動分區化的資料表，強式一致性的讀取和寫入，以及自動容錯移轉。 透過在記憶體內部快取讀取和高輸送量的串流寫入，來提高效能。 可以在虛擬網路內建立 HBase 叢集。 如需詳細資訊，請參閱[在 Azure 虛擬網路上建立 HDInsight 叢集][hbase-provision-vnet]。

## <a name="how-is-data-managed-in-hdinsight-hbase"></a>如何在 HDInsight HBase 中管理資料？
資料可以使用來管理對 HBase 中 hello `create`， `get`， `put`，和`scan`hello HBase 殼層命令。 資料透過使用撰寫 toohello 資料庫`put`和使用讀取`get`。 hello`scan`命令是使用的 tooobtain 資料從資料表中的多個資料列。 資料也可以使用 hello HBase C# API，可提供用戶端程式庫之上 hello HBase REST API 來管理。 HBase 資料庫也可使用 Hive 進行查詢。 如簡介 toothese，程式設計模型，請參閱[開始透過 HDInsight 中的 Hadoop 使用 HBase][hbase-get-started]。 副處理器也會提供，可讓該主機 hello 資料庫 hello 節點中的資料處理。

> [!NOTE]
> Thrift 不受 HDInsight 中的 HBase 所支援。
>

## <a name="scenarios-use-cases-for-hbase"></a>情節：HBase 的使用案例
hello 標準的使用案例的 BigTable （以及藉由擴充，HBase） 所建立的 web 搜尋。 搜尋引擎會建立對應詞彙 toohello 網頁包含它們的索引。 除此之外，HBase 還有其他許多適用的使用案例，本節會列舉其中幾個。

* 索引鍵-值存放區
  
    HBase 可做為索引鍵-值存放區，也很適合用來管理訊息系統。 Facebook 在訊息系統中使用 HBase，其用來儲存和管理網際網路通訊相當理想。 WebTable 使用 HBase toosearch 的並管理從網頁擷取的資料表。
* 感應器資料
  
    HBase 適合用來擷取從多個來源收集累加的資料。 這包括社交分析、時間序列、讓互動式儀表板保有最新的趨勢與計數器，以及管理稽核記錄系統。 範例包括 Bloomberg 商人終端機和 hello 開啟時間序列的資料庫 (OpenTSDB)，它會儲存，並提供存取 toometrics 收集關於 hello 伺服器系統的健全狀況。
* 即時查詢
  
    [Phoenix](http://phoenix.apache.org/) 是適用於 Apache HBase 的 SQL 查詢引擎。 其以 JDBC 驅動程式的形式進行存取，並可使用 SQL 查詢和管理 HBase 資料表。
* HBase 即平台
  
    應用程式可以將 HBase 做為資料存放區，並在此基礎上執行。 範例包括 Phoenix、OpenTSDB、Kiji 及 Titan。 應用程式也可與 HBase 整合。 範例包括 Hive、Pig、Solr、Storm、Flume、Impala、Spark、Ganglia 及 Drill。

## <a name="next-steps"></a>接續步驟
* [開始在 HDInsight 中搭配使用 HBase 與 Hadoop][hbase-get-started]
* [在 Azure 虛擬網路上建立 HDInsight 叢集][hbase-provision-vnet]
* [在 HDInsight 中設定 HBase 複寫](hdinsight-hbase-replication.md)
* [使用 HDInsight 中的 HBase 分析 Twitter 情緒][hbase-twitter-sentiment]
* [使用 Maven toobuild Java 應用程式與 HDInsight (Hadoop) 使用 HBase][hbase-build-java-maven]

## <a name="see-also"></a>另請參閱
* [Apache HBase](https://hbase.apache.org/)
* [Bigtable：結構化資料的分散式儲存體系統](http://research.google.com/archive/bigtable.html)

[hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md

[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hbase-build-java-maven]: hdinsight-hbase-build-java-maven.md

[hdinsight-use-hive]: hdinsight-use-hive.md

[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md

[hbase-get-started]: http://azure.microsoft.com/documentation/articles/hdinsight-hbase-get-started/

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
