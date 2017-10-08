---
title: "資料湖存放區效能調整指導方針 aaaAzure |Microsoft 文件"
description: "Azure Data Lake Store 效能微調指導方針"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: cgronlun
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: stewu
ms.openlocfilehash: 939faa068c0f81d18d9533956f4d336bc4d0cbe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-azure-data-lake-store-for-performance"></a>針對效能目的調整 Azure Data Lake Store

Data Lake Store 支援 I/O 密集分析和資料移動的高輸送量。  在 Azure 資料湖存放區，使用所有可用的輸送量 – hello 可以讀取或寫入每秒資料量 – 是重要的 tooget hello 達到最佳效能。  這可以藉由盡可能平行執行讀取和寫入來達成。

![Data Lake Store 效能](./media/data-lake-store-performance-tuning-guidance/throughput.png)

Azure Data Lake Store 可以調整所有分析案例的 tooprovide hello 必要輸送量。 根據預設，Azure Data Lake Store 帳戶提供自動足夠處理能力 toomeet hello 需求廣泛的類別目錄的使用案例。 客戶會遇到 hello 預設限制 hello 的情況下，hello ADLS 帳戶可以設定的 tooprovide 增加輸送量，藉由連絡 Microsoft 支援服務。

## <a name="data-ingestion"></a>資料擷取

當擷取資料從來源系統 tooADLS，務必 hello 來源硬體、 來源的網路硬體和網路連線 tooADLS 的 tooconsider 可能 hello 形成瓶頸。  

![Data Lake Store 效能](./media/data-lake-store-performance-tuning-guidance/bottleneck.png)

請務必 tooensure hello 資料移動，不會受到這些因素。

### <a name="source-hardware"></a>來源硬體

不論您在 Azure 中使用內部部署電腦或 Vm，您應該仔細選取 hello 適當的硬體。 來源磁碟硬體，偏好 Ssd tooHDDs 並挑選更快的磁針與磁碟硬體。 使用來源網路硬體，hello 最 Nic。  在 Azure 上，我們建議 Azure D14 Vm 有 hello 適當功能強大的磁碟和網路硬體。

### <a name="network-connectivity-tooazure-data-lake-store"></a>網路連線 tooAzure 資料湖存放區

hello 網路連線，您的來源資料與 Azure 資料湖存放區之間有時可能 hello 瓶頸。 當您的來源資料是內部部署時，請考慮使用與 [Azure ExpressRoute](https://azure.microsoft.com/en-us/services/expressroute/) 的專用連結。 如果您的來源資料是在 Azure 中，hello 效能時將會最佳 hello 資料位於 hello 與 hello Data Lake Store 的相同 Azure 區域。

### <a name="configure-data-ingestion-tools-for-maximum-parallelization"></a>設定最大平行處理的資料擷取工具

一旦您解決 hello 來源硬體和網路連線上述的瓶頸，您就準備好 tooconfigure 擷取工具。 hello 下表摘要說明 hello 金鑰設定數個常用的擷取工具並提供深入的效能微調他們的文件。  toolearn 更多有關哪些工具 toouse 案例中，請瀏覽[文章](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-data-scenarios)。

| 工具               | Settings     | 其他詳細資訊                                                                 |
|--------------------|------------------------------------------------------|------------------------------|
| Powershell       | PerFileThreadCount、ConcurrentFileCount |  [連結](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-powershell#performance-guidance-while-using-powershell)   |
| AdlCopy    | Azure Data Lake Analytics units  |   [連結](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob#performance-considerations-for-using-adlcopy)         |
| DistCp            | -m (mapper)   | [連結](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-copy-data-wasb-distcp#performance-considerations-while-using-distcp)                             |
| Azure Data Factory| parallelCopies    | [連結](../data-factory/data-factory-copy-activity-performance.md)                          |
| Sqoop           | fs.azure.block.size、-m (mapper)    |   [連結](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/)        |

## <a name="structure-your-data-set"></a>結構化您的資料集

當資料儲存在資料湖存放區，hello 檔案大小、 檔案及資料夾結構的數字會對效能造成影響。  hello 下一節說明這些區域中的最佳作法。  

### <a name="file-size"></a>檔案大小

一般而言，例如 HDInsight 和 Azure Data Lake Analytics 的分析引擎都有每個檔案的額外負荷。  如果您將資料儲存為許多小型檔案，會造成效能的負面影響。  

一般情況下，將您的資料組織成較大大小的檔案，以提升效能。  根據經驗法則，將檔案中的資料集組織為 256MB 以上。 在類似影像和二進位資料的某些情況下，就不可能 tooprocess 它們以平行方式。  在這些情況下，建議您 tookeep 個別檔案小於 2 GB。

有時候，在資料管線有限有大量的小型檔案 hello 未經處理資料的控制權。  建議 toohave"烹飪 」 程序會產生較大的檔案 toouse 下游應用程式。  

### <a name="organizing-time-series-data-in-folders"></a>組織資料夾中的時間序列資料

Hive 和 ADLA 工作負載的時間序列資料的資料分割剪除有助於某些查詢讀取 hello 資料，進而改善效能的子集。    

擷取時間序列資料的這些管線，通常會以檔案和資料夾結構命名非常嚴謹的方式來處理檔案。 以下是很常見的範例，依日期結構化資料：

    \DataSet\YYYY\MM\DD\datafile_YYYY_MM_DD.tsv

請注意，做為資料夾，以及在 hello 檔名不會顯示 hello 日期時間資訊。

日期和時間，hello 以下是常見的模式

    \DataSet\YYYY\MM\DD\HH\mm\datafile_YYYY_MM_DD_HH_mm.tsv

同樣地，您與 hello 資料夾和檔案的組織選擇的 hello 應該最佳化 hello 較大的檔案大小和合理的每個資料夾中的檔案數目。

## <a name="optimizing-io-intensive-jobs-on-hadoop-and-spark-workloads-on-hdinsight"></a>最佳化 HDInsight 上 Hadoop 和 Spark 工作負載的 I/O 大量作業

作業分為下列三個類別的 hello:

* **CPU 密集作業**  這些作業有很長的計算時間和最短的 I/O 時間。  範例包括機器學習和自然語言處理作業。  
* **記憶體密集作業**  這些作業會使用大量記憶體。  範例包括 PageRank 和即時分析作業。  
* **I/O 密集作業**  這些作業花費大部分時間執行 I/O。  常見範例是僅執行讀取和寫入作業的複製作業。  其他範例包括讀取大量資料時，會執行某些資料轉換的資料準備工作，然後寫入 hello 資料回復 toohello 存放區。  

下列指導方針的 hello 是只適用 tooI/O 密集的工作。

### <a name="general-considerations-for-an-hdinsight-cluster"></a>HDInsight 叢集的一般考量

* **HDInsight 版本** 為了達到最佳效能，使用 HDInsight hello 最新版本。
* **區域** Hello 資料湖存放區置於 hello 與 hello HDInsight 叢集相同的區域。  

HDInsight 叢集是由兩個前端節點和一些背景工作角色節點所組成。 每個背景工作節點提供特定數目的核心和記憶體，由 hello VM 類型所決定。  執行作業，YARN 時配置 hello 可用的記憶體及核心 toocreate 容器的 hello 資源交涉器。  每個容器執行 hello 工作所需的 toocomplete hello 作業。  容器快速地執行平行 tooprocess 工作中。 因此，盡可能平行執行最多容器可提升效能。

有三個層級可以是微調的 tooincrease 的 HDInsight 叢集內 hello 數目的容器，並使用所有可用的輸送量。  

* **實體層**
* **YARN 層**
* **工作負載層**

### <a name="physical-layer"></a>實體層

**執行具有更多節點和/或較大大小 VM 的叢集。**  較大的叢集可讓您 toorun 更多的 YARN 容器 hello 圖所示。

![Data Lake Store 效能](./media/data-lake-store-performance-tuning-guidance/VM.png)

**使用具有較大網路頻寬的 VM。**  hello 的網路頻寬量可能是瓶頸，如果沒有 Data Lake Store 輸送量比網路頻寬比較少。  不同 VM 會有不同的網路頻寬大小。  選擇具有 hello 最大可能的網路頻寬的 VM 類型。

### <a name="yarn-layer"></a>YARN 層

**使用較小的 YARN 容器。**  多個容器以 hello 減少每個 YARN 容器 toocreate hello 大小相同的資源數量。

![Data Lake Store 效能](./media/data-lake-store-performance-tuning-guidance/small-containers.png)

根據您的工作負載，一定有需要的最小 YARN 容器大小。 如果您挑選的容器太小，您的作業會遇到記憶體不足的問題。 通常 YARN 容器應該不小於 1GB。 它是一般 toosee 3 GB YARN 容器。 針對某些工作負載，您可能需要較大的 YARN 容器。  

**增加每個 YARN 容器的核心。**  增加 hello 配置 tooeach 容器 tooincrease hello 數目在每個容器中執行的平行工作的核心數目。  這適用於類似 Spark 的應用程式，它會在每個容器執行多項工作。  應用程式，像是 hive 控制檔的執行單一執行緒的每個容器，它提供更好的 toohave 多個容器，而不是每個容器的更多核心。   

### <a name="workload-layer"></a>工作負載層

**使用所有可用的容器。**  等於或大於 hello 數目可用的容器，以便利用所有資源，設定工作 toobe hello 號碼。

![Data Lake Store 效能](./media/data-lake-store-performance-tuning-guidance/use-containers.png)

**失敗的工作成本很高。** 如果每個工作有大量的資料 tooprocess，工作失敗導致昂貴的重試。  因此，它是較佳的 toocreate 更多的工作，其中每個處理少量資料。

加法 toohello 的一般指導方針上述，在每個應用程式會有不同的參數使用 tootune 該特定應用程式。 hello 下表列出一些 hello 參數和連結 tooget 入門效能調整每個應用程式。

| 工作負載               | 參數 tooset 工作                                                         |
|--------------------|-------------------------------------------------------------------------------------|
| [HDInsight 上的 Spark](data-lake-store-performance-tuning-spark.md)       | <ul><li>Num-executors</li><li>Executor-memory</li><li>Executor-cores</li></ul> |
| [Hive on HDInsight](data-lake-store-performance-tuning-hive.md)    | <ul><li>hive.tez.container.size</li></ul>         |
| [MapReduce on HDInsight](data-lake-store-performance-tuning-mapreduce.md)            | <ul><li>Mapreduce.map.memory</li><li>Mapreduce.job.maps</li><li>Mapreduce.reduce.memory</li><li>Mapreduce.job.reduces</li></ul> |
| [Storm on HDInsight](data-lake-store-performance-tuning-storm.md)| <ul><li>背景工作處理序數目</li><li>Spout 執行程式執行個體數目</li><li>Bolt 執行程式執行個體數目 </li><li>Spout 工作數目</li><li>Bolt 工作數目</li></ul>|

## <a name="see-also"></a>另請參閱
* [Azure Data Lake Store 概觀](data-lake-store-overview.md)
* [開始使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
