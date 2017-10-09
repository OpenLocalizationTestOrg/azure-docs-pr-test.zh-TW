---
title: "Azure HDInsight 上的 Hadoop 元件 aaaRelease 資訊 |Microsoft 文件"
description: "Azure HDInsight 的 Hadoop 元件的最新版本資訊與版本。 取得 Spark、R Server、Hive 等的開發秘訣和詳細資料。"
services: hdinsight
documentationcenter: 
editor: cgronlun
manager: jhubbard
author: nitinme
tags: azure-portal
ms.assetid: a363e5f6-dd75-476a-87fa-46beb480c1fe
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: nitinme
ms.openlocfilehash: ab08a74380fe0bbd7430c1096dca7eb177c11fe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-hadoop-components-on-azure-hdinsight"></a>Azure HDInsight 上 Hadoop 元件的版本資訊

本文章提供資訊 hello**最近**Azure HDInsight 版本的更新。 如需有關較早版本的詳細資訊，請參閱 [HDInsight 版本資訊封存](hdinsight-release-notes-archive.md)。

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [HDInsight 版本控制文件](hdinsight-component-versioning.md)。


## <a name="notes-for-08012017-release-of-hdinsight"></a>HDInsight 08/01/2017 版本的相關資訊

| Title | 說明 | 受影響的區域  | 叢集類型  | 
| --- | --- | --- | --- | --- |
| Microsoft R Server 9.1 on HDInsight 版本 |HDInsight 現在支援在 HDInsight 上佈建 R Server 9.1 叢集。 如需 Microsoft R Server 9.1 版本的詳細資訊，請參閱[這個部落格](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/introducing-microsoft-r-server-9-1-release/)。 |服務 |R 伺服器 |
| HDInsight 3.6 現在包含 hello Hadoop 堆疊的較新版本|<ul><li>如需更新後版本的詳細清單，請參閱 [HDInsight 中可用的 Hadoop 元件版本](hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions)。</li><li>如需在 hello hello Hadoop 堆疊的最新的版本中修正的 bug，請參閱[Apache 補充資訊](https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.1/bk_release-notes/content/patch_parent.html)。</li><li>如需 HDP 2.6.1 (現在可於 HDInsight 3.6 中取得) 的重大變更清單，請參閱 [https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.1/bk_release-notes/content/behavior_changes.html](https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.1/bk_release-notes/content/behavior_changes.html)。</li><li>如需 HDP 2.6.1 中的已知問題清單，請參閱[已知問題](https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.1/bk_release-notes/content/known_issues.html)。</li></ul> |服務 |全部 |N/A |
| 更新 tooInteractive Hive （預覽） 叢集 |<ul><li><b>功能改進。</b> 快取中繼存放區，減少 hello 負載 hello 後端 SQL 快取 hello 中繼資料，並可改善效能，所有的中繼資料作業的實作。  這項改進現在是所有互動式 Hive 叢集的預設值。 如需詳細資訊，請參閱 [https://issues.apache.org/jira/browse/HIVE-16520](https://issues.apache.org/jira/browse/HIVE-16520)。</li><li><b>功能改進。</b> 動態分割區載入已經過最佳化。 如需詳細資訊，請參閱 [https://issues.apache.org/jira/browse/HIVE-14204] (https://issues.apache.org/jira/browse/HIVE-14204)。</li><li><b>功能改進。</b> 將 Linux 上的 HDInsight 設定最佳化。</li><li><b>錯誤修正。</b> `CredentialProviderFactory$getProviders` 不是安全執行緒。 」 現已修正此問題。 如需詳細資訊，請參閱 [https://issues.apache.org/jira/browse/HADOOP-14195](https://issues.apache.org/jira/browse/HADOOP-14195)。</li><li><b>錯誤修正。</b> WASB 驅動程式 `liststatus` API 若大量使用 CPU 會導致 ATS 效能不佳。 」 現已修正此問題。 如需詳細資訊，請參閱 [https://github.com/Azure/azure-storage-java/pull/154](https://github.com/Azure/azure-storage-java/pull/154)。</li></ul> |服務 |互動式 Hive (預覽) |
| 更新 tooHadoop 叢集 |改進 Templeton 工作作業的可靠性。 如需詳細資訊，請參閱 [https://issues.apache.org/jira/browse/HIVE-15947](https://issues.apache.org/jira/browse/HIVE-15947) |服務 |Hadoop |
| YARN 更新 | HDInsight 現已建立 250 GB 的 Ambari 資料庫 (未增加成本)，以讓客戶獲得更好的體驗。 這項變更應可防止 ATS 用完，從而獲得更好的效能。 |服務 |全部 |
| Spark 更新 | Spark 2.1.1 的版本。 如需詳細資訊，請參閱 [Spark 2.1.1 版](https://spark.apache.org/releases/spark-release-2-1-1.html)。 | 服務 | Spark |

  



## <a name="04062017---general-availability-of-hdinsight-36"></a>2017/04/06 - HDInsight 3.6 正式運作

* 此版本中，Azure HDInsight 新增以 HDP 2.6 為基礎的 3.6 版。 HDP 2.6 版本資訊可在[這裡](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.0/bk_release-notes/content/ch_relnotes.html)找到，而 HDInsight 版本的詳細資訊則可以在[這裡](hdinsight-component-versioning.md)找到。 HDInsight 3.6 適用於下列工作負載的 hello:

    * Hadoop v2.7.3
    * HBase v1.1.2
    * Storm v1.1.0
    * Spark v2.1.0
    * Interactive Hive v2.1.0

* **Hive View 2.0 的支援**。 這應該改善 hello 互動式 hive 控制檔的使用者體驗。 如需詳細資訊，請參閱 [Hortonworks 文件](http://docs.hortonworks.com/HDPDocuments/Ambari-2.5.0.3/bk_ambari-views/content/ch_using_hive_view.html)。

* **使用 Hive LLAP 提高效能**。 如需詳細資訊，請參閱 [Hortonworks 文件](https://hortonworks.com/blog/top-5-performance-boosters-with-apache-hive-llap/)。

* **Hive 的新功能**。 請參閱 [Hortonworks 文件](https://hortonworks.com/apache/hive/#section_4)。

* **Hive CLI 取代**: Hive CLI 即將遭取代，客戶會改為鼓勵的 toouse Beeline。 如需詳細資訊，請參閱 [Apache 文件](https://cwiki.apache.org/confluence/display/Hive/Replacing+the+Implementation+of+Hive+CLI+Using+Beeline)。 如需有關指示 toouse Beeline 與 HDInsight，請參閱[使用 Beeline 的 HDInsight Hadoop 叢集](hdinsight-hadoop-use-hive-beeline.md)。

* **Apache Phoenix 和 HBase 的新功能**。
    * 儲存配額支援︰通常用在多租用戶環境中，允許在個別資料表和個別命名空間等級上維持有限的儲存空間。
    * Phoenix 編製索引改進︰累加索引建立和從先前的失敗中重建/繼續編製索引。
    * Phoenix 資料完整性工具︰支援驗證結構描述、索引和其他中繼資料。


* **問題 HBase**： 時執行 CSV 大量上傳 MapReduce 工作、 hello，請使用下列語法可能會導致錯誤。

        HADOOP_CLASSPATH=$(hbase mapredcp):/path/to/hbase/conf hadoop jar phoenix-<version>-client.jar org.apache.phoenix.mapreduce.CsvBulkLoadTool --table EXAMPLE --input /data/example.csv

    使用 hello 改為使用下列語法：

        HADOOP_CLASSPATH=/path/to/hbase-protocol.jar:/path/to/hbase/conf hadoop jar phoenix-<version>-client.jar org.apache.phoenix.mapreduce.CsvBulkLoadTool --table EXAMPLE --input /data/example.csv


## <a name="02282017---release-of-spark-21-on-hdinsight-36-preview"></a>2017/02/28 - 發行 Spark 2.1 on HDInsight 3.6 (預覽版)
* [Spark 2.1](http://spark.apache.org/releases/spark-release-2-1-0.html) 會改善舊版的許多穩定性和可用性問題。 它也會有跨所有 Spark 工作負載的新功能，例如 Spark Core、SQL、ML 和串流處理。
* 結構化串流會利用事件時間的浮水印和 Kafka 0.10 連接器支援改良延展性。
* Spark SQL 分割現在會使用新的可調整資料分割處理機制來處理。 請參閱詳細[這裡](http://spark.apache.org/releases/spark-release-2-1-0.html)如何 tooupgrade。
* Spark 2.1 on Azure HDInsight 3.6 預覽目前不支援使用 ODBC 驅動程式的 BI 工具連線。
* 此預覽版本不支援從 Spark 2.1 叢集的 Azure Data Lake Store 存取。


## <a name="11182016---release-of-spark-201-on-hdinsight-35"></a>2016/11/18 - 發行 Spark 2.0.1 on HDInsight 3.5
Spark 2.0.1 現已可在 Spark 叢集上取得 (HDInsight 3.5 版)。

## <a name="11162016---release-of-r-server-90-on-hdinsight-35-spark-20"></a>2016/11/16 - 發行 R Server 9.0 on HDInsight 3.5 (Spark 2.0)
*   R 伺服器叢集現在包含兩個版本的 hello 選項： HDI 3.5 (Spark 2.0) 和 R Server 8.0 上 HDI 3.4 (Spark 1.6) 上的 R 伺服器 9.0。
*   建立 R 3.3.2 R 伺服器 9.0 HDI 3.5 (Spark 2.0)，並包含新 ScaleR 資料來源的登錄區中的資料載入呼叫 RxHiveData 和 RxParquetData 函式，並直接 Parquet tooSpark 資料框架 ScaleR 以進行分析。 如需詳細資訊，請參閱說明 R 中這些函式，藉由使用 hello hello 內嵌**嗎？RxHiveData**和**嗎？RxParquetData**命令。
*   （使用退出選項） 的預設值現在已安裝 RStudio Server community edition hello hello 佈建流程一部分的叢集設定 刀鋒視窗。

## <a name="11092016---release-of-spark-20-on-hdinsight"></a>2016/11/09 - 發行 Spark 2.0 on HDInsight
* HDInsight 3.5 上的 Spark 2.0 叢集現在支援 Livy 和 Jupyter 服務。

## <a name="10262016---release-of-r-server-on-hdinsight"></a>2016/10/26 - 發行 R Server on HDInsight
* hello URI 邊緣節點存取已變更過**clustername**-ed-ssh.azurehdinsight.net
* HDInsight 上 R 伺服器的叢集佈建已簡化。
* HDInsight 上的 R 伺服器現在可做為一般 HDInsight「R 伺服器」叢集類型，不會再安裝為個別的 HDInsight 應用程式。 hello 邊緣節點和 R Server 二進位檔是現在已佈建 hello R 伺服器叢集部署的一部分。 這可改善佈建速度和可靠性。 R 伺服器的定價模式也會隨之更新。
* R 伺服器叢集類型價格現在會根據標準層價格加上 R 伺服器額外費用價格。 進階層會保留給不同叢集類型皆有提供的進階功能，不會用於 R 伺服器叢集類型。 這項變更不會影響您的 R 伺服器; 有效定價它會變更只如何 hello 費用會出現在 hello 帳單。 所有現有的 R 伺服器叢集繼續 toowork 和資源管理員範本繼續 toofunction 之前請注意已被取代。 **它是透過建議 tooupdate 已編寫指令碼的部署 toouse 新資源管理員範本。**






