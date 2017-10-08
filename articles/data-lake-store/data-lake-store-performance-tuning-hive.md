---
title: "資料湖存放區 Hive 效能調整指導方針 aaaAzure |Microsoft 文件"
description: "Azure Data Lake Store Hive 效能微調方針"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: e44daeb6ad3b64e893c709df63b56444a330729f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-hive-on-hdinsight-and-azure-data-lake-store"></a>HDInsight 和 Azure Data Lake Store 上的 Hive 效能微調方針

hello 預設設定已設 tooprovide 良好的效能在許多不同的使用案例。  I/O 密集的查詢，Hive 可以微調的 tooget ADLS 與更好的效能。  

## <a name="prerequisites"></a>必要條件

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure Data Lake Store 帳戶**。 如需有關指示 toocreate 一個，請參閱[開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)
* **Azure HDInsight 叢集**與存取 tooa Data Lake Store 帳戶。 請參閱 [建立具有 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-portal.md)。 請確定您已啟用遠端桌面 hello 叢集。
* **在 HDInsight 上執行 Hive**。  在 HDInsight 上執行 Hive 工作相關的 toolearn 請參閱 [使用 HDInsight 上的登錄區] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)
* **ADLS 的效能微調指導方針**。  如需一般的效能概念，請參閱 [Data Lake Store 效能微調指導方針](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)

## <a name="parameters"></a>參數

以下是 hello 最重要設定 tootune 改善 ADLS 效能：

* **hive.tez.container.size** – hello 每個工作所使用的記憶體數量

* **tez.grouping.min-size** – 每個對應器的大小下限

* **tez.grouping.max-size** – 每個對應器的大小上限

* **hive.exec.reducer.bytes.per.reducer** – 每個歸納器的大小

**hive.tez.container.size** -hello 容器大小會決定多少記憶體可供每項工作。  這是控制 hello 並行登錄區中的 hello 主要輸入。  

**tez.grouping.min 大小**– 此參數可讓您的每個對應工具 tooset hello 最小大小。  如果自行 Tez 所選擇的 hello 數目小於 hello 值，這個參數，Tez 會使用 hello 這裡設定的值。  

**tez.grouping.max 大小**– hello 參數可讓您的每個對應工具 tooset hello 最大大小。  如果自行 Tez 所選擇的 hello 數目大於 hello 值，這個參數，Tez 會使用 hello 這裡設定的值。  

**hive.exec.reducer.bytes.per.reducer** – 這個參數會設定每個減壓器 hello 大小。  根據預設，每個歸納器為 256 MB。  

## <a name="guidance"></a>指引

**設定 hive.exec.reducer.bytes.per.reducer** – hello 預設值就非常適合 hello 資料時未壓縮。  壓縮的資料，您應該縮小 hello hello 減壓器。  

**Set hive.tez.container.size** – 在每個節點中，記憶體會由 yarn.nodemanager.resource.memory-mb 指定，且預設應該會在 HDI 叢集上正確設定。  如需有關設定 YARN hello 適當的記憶體的詳細資訊，請參閱此[張貼](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom)。

I/O 密集型工作負載可以從多個平行處理原則獲益，藉由降低 hello Tez 容器大小。 這可讓使用者 hello 可增加並行處理多個容器。  不過，某些 Hive 查詢需要大量的記憶體 (例如 MapJoin)。  如果 hello 工作沒有足夠的記憶體，您會收到記憶體不足例外狀況在執行階段。  如果您收到記憶體不足例外狀況，您應該增加 hello 記憶體。   

hello 並行工作執行或數目平行處理原則將限於 hello YARN 記憶體總數。  hello YARN 容器的數目會指定多少並行工作可以執行。  每個節點的 toofind hello YARN 記憶體，您可以移 tooAmbari。  瀏覽 tooYARN 並檢視 hello 組態 索引標籤。 hello YARN 記憶體會顯示此視窗中。  

        Total YARN memory = nodes * YARN memory per node
        # of YARN containers = Total YARN memory / Tez container size
使用 ADLS hello 金鑰 tooimproving 效能是盡可能 tooincrease hello 並行。  Tez 自動計算 hello 數項工作，因此您不需要 tooset 應該建立它。   

## <a name="example-calculation"></a>範例計算

假設您有 8 節點的 D14 叢集。  

    Total YARN memory = nodes * YARN memory per node
    Total YARN memory = 8 nodes * 96GB = 768GB
    # of YARN containers = 768GB / 3072MB = 256

## <a name="limitations"></a>限制
**ADLS 節流** 

點擊 hello UIf 限制的頻寬提供根據 ADLS，您會啟動 toosee 工作失敗。 透過觀察工作記錄檔中的節流錯誤即可加以識別。  您可以藉由增加 Tez 容器大小減少 hello 平行處理原則。  如果您的作業需要更多並行能力，請與我們連絡。   

如果您節流 toocheck，您需要 tooenable hello 偵錯記錄 hello 用戶端。 做法如下：

1. 將下列屬性 Hive 組態中的 hello log4j 屬性中的 hello。這可藉由 Ambari 檢視： log4j.logger.com.microsoft.azure.datalake.store=DEBUG 重新啟動所有 hello 節點/服務 hello config tootake 效果。

2. 如果您節流，您會看到 hello hive 記錄檔中的 hello HTTP 429 錯誤程式碼。 hello hive 記錄檔位於 /tmp/&lt;使用者&gt;/hive.log

## <a name="further-information-on-hive-tuning"></a>關於微調 Hive 的進一步資訊

以下是一些有助於微調 Hive 查詢的部落格︰
* [在 Hdinsight 中最佳化 Hadoop 的 Hive 查詢](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-optimize-hive-query/)
* [針對 Hive 查詢的效能進行疑難排解](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/)
* [Ignite 講解如何將 HDInsight 上的 Hive 最佳化](https://channel9.msdn.com/events/Machine-Learning-and-Data-Sciences-Conference/Data-Science-Summit-2016/MSDSS25)
