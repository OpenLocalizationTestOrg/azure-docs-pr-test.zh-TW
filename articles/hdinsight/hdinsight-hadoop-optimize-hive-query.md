---
title: "Azure HDInsight aaaOptimize Hive 查詢 |Microsoft 文件"
description: "了解如何 toooptimize 您 Hive 查詢在 HDInsight Hadoop。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d6174c08-06aa-42ac-8e9b-8b8718d9978e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2016
ms.author: jgao
ms.openlocfilehash: d27f8100e1e9f4823040ff9f693e7b78d6192c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a>將 Azure HDInsight 中的 Hive 查詢最佳化

根據預設，Hadoop 叢集不會為了效能進行最佳化。 本文涵蓋您可以套用 tooyour 查詢一些最常見 Hive 效能最佳化方法。

## <a name="scale-out-worker-nodes"></a>相應放大背景工作節點

增加 hello 叢集中的背景工作角色節點的數目可以利用多個自行和 reducers toobe 以平行方式執行。 在 HDInsight 中您有兩種方法可相應放大：

* 在 hello 佈建時，您可以指定 hello 使用 hello Azure 入口網站、 Azure PowerShell 或跨平台命令列介面的背景工作節點數。  如需詳細資訊，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。 hello 下列螢幕擷取畫面顯示 hello 背景工作節點組態 hello Azure 入口網站上：
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* 在執行階段的 hello，您可以也向外延展叢集就必須重新建立其中一個：

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

多個 hello 支援 HDInsight 不同虛擬機器的詳細資訊，請參閱[HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。

## <a name="enable-tez"></a>啟用 Tez

[Apache Tez](http://hortonworks.com/hadoop/tez/)是替代的執行引擎 toohello MapReduce 引擎：

![tez_1][image-hdi-optimize-hive-tez_1]

Tez 比較迅速，因為：

* **以單一工作 hello MapReduce 引擎中執行導向非循環圖 (DAG)**。 hello DAG 需要自行 toobe 後面接著一組 reducers 每組。 這會導致多個 MapReduce 工作 toobe 開始每個 Hive 查詢。 Tez 沒有此種條件約束，並可將複雜的 DAG 當作一項工作處理，因而將工作啟動的額外負荷降至最低。
* **避免不必要的寫入**。 由於 toomultiple 作業正在開始 hello 撰寫 tooHDFS 中繼資料相同的 Hive 查詢 hello MapReduce 引擎，每個工作的 hello 輸出中。 因為 Tez 降到最低的每個 Hive 查詢能夠 tooavoid 不必要的寫入作業數目。
* **將啟動延遲最小化**。 Tez 是更好的無法 toominimize 啟動延遲時間減少 hello 自行它需要 toostart，並在整個也改善最佳化數目。
* **重複使用容器**。 只要可能 Tez 無法 tooreuse 容器 tooensure 到期，延遲 toostarting 向上容器會降低。
* **連續最佳化技巧**。 習慣上，是在編譯階段進行最佳化。 不過 hello 輸入的相關詳細資訊，讓較佳的最佳化在執行階段。 Tez 使用連續的最佳化技術，好讓它在 hello 執行階段 」 階段的進一步 toooptimize hello 計劃。

如需這些概念的詳細資訊，請參閱 [Apache Tez](http://hortonworks.com/hadoop/tez/)。

您可以進行任何 Hive 查詢 Tez hello 設定下列前置詞 hello 查詢的方式啟用：

    set hive.execution.engine=tez;

Linux 的 HDInsight 叢集預設會啟用 Tez。


## <a name="hive-partitioning"></a>Hive 分割

I/O 作業已執行 Hive 查詢的 hello 重大效能瓶頸。 如果資料需要 toobe hello 量唯讀，則可以是可改善 hello 效能降低。 根據預設，Hive 查詢會掃描整個 Hive 資料表。 這很適合資料表掃描之類的查詢。 不過對於只需要 tooscan 小量的資料 （例如，查詢的篩選） 的查詢，這種行為會建立不必要額外負荷。 登錄區的資料分割允許 Hive 資料表中的 Hive 查詢 tooaccess 只有 hello 必要的資料量。

分割區被藉由重新 hello 未經處理資料分割成新的目錄組織擁有它自己的目錄-hello 資料分割定義 hello 使用者所在的每一個資料分割。 hello 下列圖表說明 hello 資料行的資料分割的 Hive 資料表*年*。 每年都會建立新的目錄。

![分割][image-hdi-optimize-hive-partitioning_1]

一些分割考量：

* **請勿分割不足** - 依據只有少數幾個值的資料行進行分割，可能會造成很少的分割區。 例如，依性別分割只會建立兩個資料分割 toobe 建立 （男性和女性），因此只有減少 hello 延遲上限的一半。
* **不是透過資料分割進行**： 在 hello 其他極端的做法是，在具有唯一值 （例如，使用者識別碼） 的資料行上建立資料分割會造成多個資料分割。 透過資料分割會導致多壓力 hello 叢集 namenode 因為它具有 toohandle hello 大量的目錄。
* **避免資料扭曲** - 明智地選擇分割索引鍵，讓所有分割區的大小平均。 上的範例分割區*狀態*可能會造成 hello 數目記錄在加州 toobe 幾乎 30 x 的 Vermont 到期 toohello 母體擴展中的差異。

toocreate 資料分割資料表，使用 hello*分割所*子句：

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

Hello 分割區的資料表建立之後，您可以建立資料分割的靜態或動態磁碟分割。

* **靜態分割**hello 在已經分區化資料的方式適當的目錄，而且您可以詢問 Hive 手動 hello 目錄位置為基礎的資料分割。 下列程式碼片段的 hello 是範例。
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* **動態磁碟分割**表示的 Hive toocreate 分割區會自動為您。 由於我們已經建立 hello 分割 hello 暫存資料表中的資料表，我們只需要 toodo 為插入資料分割的 toohello 資料表：
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

如需詳細資訊，請參閱 [分割的資料表](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables)。

## <a name="use-hello-orcfile-format"></a>使用 hello ORCFile 格式
Hive 支援不同的檔案格式。 例如：

* **文字**： 這是 hello 預設檔案格式，而且適用於大部分的案例
* **Avro**：適用於互通性案例
* **ORC/Parquet**：最適合處理效能

高效率的方式 toostore Hive 資料 ORC （最佳化的資料列單欄式） 格式。 比較的 tooother 格式，ORC 具有下列優點 hello:

* 支援複雜的類型，包括 DateTime 和複雜和半結構化類型
* 向上 too70%壓縮
* 每 10,000 個資料列的索引可讓您略過一些資料列
* 執行階段的執行大幅減少

tooenable ORC 格式，您先建立資料表以 hello 子句*儲存為 ORC*:

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

接下來，您會從暫存資料表的 hello 插入資料表 toohello ORC。 例如：

    INSERT INTO TABLE lineitem_orc
    SELECT L_ORDERKEY as L_ORDERKEY, 
           L_PARTKEY as L_PARTKEY , 
           L_SUPPKEY as L_SUPPKEY,
           L_LINENUMBER as L_LINENUMBER,
            L_QUANTITY as L_QUANTITY, 
           L_EXTENDEDPRICE as L_EXTENDEDPRICE,
           L_DISCOUNT as L_DISCOUNT,
           L_TAX as L_TAX,
           L_RETURNFLAG as L_RETURNFLAG,
           L_LINESTATUS as L_LINESTATUS,
           L_SHIPDATE as L_SHIPDATE,
           L_COMMITDATE as L_COMMITDATE,
           L_RECEIPTDATE as L_RECEIPTDATE, 
           L_SHIPINSTRUCT as L_SHIPINSTRUCT,
           L_SHIPMODE as L_SHIPMODE,
           L_COMMENT as L_COMMENT
    FROM lineitem;

您可以深入 hello ORC 格式[這裡](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC)。

## <a name="vectorization"></a>向量化

向量化可讓 Hive tooprocess 1024 個批次一起資料列而非一次處理一個資料列。 這表示因為較少內部的程式碼需要 toorun 簡單的作業會更快完成。

tooenable 向量化首碼 Hive 查詢以 hello 下列設定：

    set hive.vectorized.execution.enabled = true;

如需詳細資訊，請參閱 [向量化查詢執行](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution)。

## <a name="other-optimization-methods"></a>其他最佳化方法
您有更多最佳化方法可以考慮，例如：

* **Hive 值區：**允許 toocluster 或區段大量資料 toooptimize 查詢效能的技術。
* **聯結最佳化：**的登錄區的查詢執行計劃 tooimprove 最佳化 hello 聯結的效率和減少 hello 使用者提示的需要。 如需詳細資訊，請參閱 [聯結最佳化](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization)。
* **增加歸納器**。

## <a name="next-steps"></a>後續步驟
在本文中，您學到幾種常見的 Hive 查詢最佳化方法。 toolearn 詳細資訊，請參閱下列文章 hello:

* [在 HDInsight 中使用 Apache Hive](hdinsight-use-hive.md)
* [在 HDInsight 中使用 Hive 分析航班延誤資料](hdinsight-analyze-flight-delay-data.md)
* [在 HDInsight 中使用 Hive 分析 Twitter 資料](hdinsight-analyze-twitter-data.md)
* [分析在 HDInsight 中的 Hadoop 使用 hello Hive 查詢主控台感應器資料](hdinsight-hive-analyze-sensor-data.md)
* [使用從網站的 HDInsight tooanalyze 記錄檔的登錄區](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
