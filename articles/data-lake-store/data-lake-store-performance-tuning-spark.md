---
title: "資料湖存放區 Spark 效能調整指導方針 aaaAzure |Microsoft 文件"
description: "Azure Data Lake Store Spark 效能微調方針"
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
ms.openlocfilehash: da1d172e9cb1199ad95605ea1718e78559f79650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-spark-on-hdinsight-and-azure-data-lake-store"></a>HDInsight 和 Azure Data Lake Store 上的 Spark 效能微調方針

當微調效能上的 Spark，您需要將您的叢集執行的應用程式的 tooconsider hello 數。  根據預設，您可以執行 4 應用程式同時 HDI 叢集上的 (附註： hello 預設設定是主體 toochange)。  您可能會決定 toouse 較少的應用程式讓您可以覆寫 hello 預設設定，並針對這些應用程式使用多個 hello 叢集。  

## <a name="prerequisites"></a>必要條件

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure Data Lake Store 帳戶**。 如需有關指示 toocreate 一個，請參閱[開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)
* **Azure HDInsight 叢集**與存取 tooa Data Lake Store 帳戶。 請參閱 [建立具有 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-portal.md)。 請確定您已啟用遠端桌面 hello 叢集。
* **在 Azure Data Lake Store 上執行 Spark 叢集**。  如需詳細資訊，請參閱[資料湖存放區中的使用 HDInsight Spark 叢集 tooanalyze 資料](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-use-with-data-lake-store)
* **ADLS 的效能微調指導方針**。  如需一般的效能概念，請參閱 [Data Lake Store 效能微調指導方針](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance) 

## <a name="parameters"></a>參數

當執行作業的 Spark，如下 hello 最重要的設定可微調的 tooincrease ADLS 效能：

* **Num 執行程式**-hello 的可執行的並行工作數。

* **執行程式記憶體**-hello 配置的記憶體數量 tooeach 執行程式。

* **執行程式核心**-hello 核心數目配置 tooeach 執行程式。                     

**Num 執行程式**Num 執行程式將會設定 hello 可以平行執行的工作數目上限。  hello 實際可以平行執行的工作數目會受限於 hello 記憶體和 CPU 資源在叢集中可用。

**執行程式記憶體**這是 hello tooeach 執行程式所配置的記憶體數量。  每一個執行程式所需的 hello 記憶體會視 hello 作業。  Hello 記憶體複雜的作業，需要 toobe 更高版本。  讀取和寫入等簡單作業的記憶體需求會較低。  Ambari 中，您可以檢視 hello 每一個執行程式的記憶體數量。  在 Ambari 瀏覽 tooSpark 並檢視 hello 組態 索引標籤。  

**執行程式核心**這會設定每個執行程式，會決定 hello 數目每執行者可以執行的平行執行緒使用的核心的 hello 數量。  例如，如果執行者核心 = 2，則每一個執行程式可以在 hello 執行者執行 2 的平行工作。  hello executor 核心需要將會相依於 hello 作業。  需要大量 I/O 的作業所需的每一工作記憶體並不需要太多，因此每個執行程式可以處理更多的平行工作。

依預設，在 HDInsight 上執行 Spark 時，會為每個實體核心定義兩個虛擬 YARN 核心。  這個數量能在並行能力與從多個執行緒切換而來的內容數量取得良好平衡。  

## <a name="guidance"></a>指引

在執行分析工作負載 toowork Spark 資料湖存放區中的資料，我們建議您搭配資料湖存放區使用 hello 最近 HDInsight 版本 tooget hello 達到最佳效能。 當您的工作是多個密集的磁碟 I/O 時，某些參數可以是設定的 tooimprove 效能。  Azure Data Lake Store 是具有高擴充性的儲存體平台，可處理高輸送量。  如果 hello 作業主要是由讀取或寫入所組成，再增加並行存取從 Azure 資料湖存放區的 I/O tooand 無法提高效能。

有幾個 I/O 密集的工作的一般方式 tooincrease 並行存取。

**步驟 1： 決定多少應用程式正在執行您的叢集上**– 您應該知道多少應用程式正在執行包括 hello 目前 hello 叢集上。  設定會假設每個 Spark 的 hello 預設值，有 4 同時執行的應用程式。  因此，您將只有 25%的 hello 叢集中每個應用程式。  tooget 更佳的效能，您可以覆寫 hello 預設值變更 hello 執行程式的數目。  

**步驟 2： 設定執行程式記憶體**– hello tooset 首先是 hello executor 記憶體。  hello 記憶體將會相依於您是將 toorun hello 作業。  您可以為每個執行程式配置較少的記憶體，以增加並行數量。  如果您看見記憶體不足例外狀況時執行您的工作，您應該增加 hello 此參數的值。  一個替代方法是 tooget 更多的記憶體使用具有較高的記憶體數量的叢集或叢集的 hello 大小增加。  更多的記憶體可讓多個執行程式 toobe 使用，這表示多個並行存取。

**步驟 3： 設定執行程式核心**– I/O 密集型工作負載沒有複雜的作業，對於良好 toostart 有大量的執行程式核心 tooincrease hello 每次執行程式的平行工作數。  設定執行程式核心 too4 是不錯的起點。   

    executor-cores = 4
增加執行程式核心的 hello 數目可讓您更多的平行處理原則讓您試驗不同的執行程式核心。  對於有更複雜的作業的工作，您應該降低 hello 執行程式對每個核心的數目。  如果 executor-cores 設定為高於 4，則記憶體回收可能會變得沒有效率而降低效能。

**步驟 4︰決定叢集中的 YARN 記憶體數量** – 這項資訊可在 Ambari 中取得。  瀏覽 tooYARN 並檢視 hello 組態 索引標籤。 hello YARN 記憶體會顯示此視窗中。  
注意： 當您在 [hello] 視窗中，您也可以查看 hello 預設 YARN 容器大小。  hello YARN 容器大小是 hello 與記憶體每秒執行程式的參數相同。

    Total YARN memory = nodes * YARN memory per node
**步驟 5︰計算 num-executors**

**計算記憶體條件約束**-hello num 執行程式參數會限制記憶體或 CPU。  您的應用程式可用的 YARN 記憶體的 hello 數量取決於 hello 記憶體條件約束。  您應該取得 YARN 記憶體總數，然後除以 executor-memory。  hello 的條件約束需要 toobe 取消採的應用程式的 hello 數讓我們除以 hello 應用程式數目。

    Memory constraint = (total YARN memory / executor memory) / # of apps   
**計算 CPU 的條件約束**-hello CPU 的條件約束會計算為 hello 除以 hello 每個執行程式的核心數目的虛擬核心總數。  每個實體核心有 2 個虛擬核心。  類似 toohello 記憶體條件約束，我們有除以 hello 應用程式數目。

    virtual cores = (nodes in cluster * # of physical cores in node * 2)
    CPU constraint = (total virtual cores / # of cores per executor) / # of apps
**設定 num 執行程式**– hello num 執行程式的參數由採用 hello hello 記憶體條件約束和 hello CPU 的條件約束的最小值。 

    num-executors = Min (total virtual Cores / # of cores per executor, available YARN memory / executor-memory)   
設定較高的 num-executors 數值未必能提升效能。  您應該考慮到，新增更多執行程式會對每個額外的執行程式新增額外的負擔，而可能降低效能。  Num 執行程式受限於 hello 叢集資源。    

## <a name="example-calculation"></a>範例計算

例如，假設您目前已為應用程式包括 hello 一個要 toorun 執行 2 叢集 8 D4v2 節點所組成。  

**步驟 1： 決定多少應用程式正在執行您的叢集上**– 知道您有 2 上您的叢集，包括其中一個要 toorun hello 應用程式。  

**步驟 2︰設定 executor-memory** – 在此範例中，我們判斷 6 GB 的 executor-memory 就足夠 I/O 密集作業使用。  

    executor-memory = 6GB
**步驟 3： 設定執行程式核心**– 因為這是 I/O 密集工作，我們可以設定的每一個執行程式 too4 核心的 hello 數目。  大於 4 可能會導致記憶體回收集合問題，請設定每個執行者 toolarger 核心。  

    executor-cores = 4
**步驟 4： 決定 YARN 叢集中的記憶體數量**– 我們巡覽 tooAmbari toofind 出每個 D4v2 有 25 GB 的 YARN 記憶體。  由於有 8 個節點，hello 可用 YARN 記憶體乘以 8。

    Total YARN memory = nodes * YARN memory* per node
    Total YARN memory = 8 nodes * 25GB = 200GB
**步驟 5： 計算 num 執行程式**– hello num 執行程式的參數取決於採取 hello 最少的 hello 記憶體條件約束和除以 hello hello CPU 條件約束數目上的 Spark 執行應用程式。    

**計算記憶體條件約束**– hello 記憶體條件約束的計算方式為 hello YARN 記憶體總數除以 hello 記憶體每秒執行程式。

    Memory constraint = (total YARN memory / executor memory) / # of apps   
    Memory constraint = (200GB / 6GB) / 2   
    Memory constraint = 16 (rounded)
**計算 CPU 的條件約束**-hello CPU 的條件約束會計算為 hello 總 yarn 核心數目除以 hello 執行程式對每個核心的數目。
    
    YARN cores = nodes in cluster * # of cores per node * 2   
    YARN cores = 8 nodes * 8 cores per D14 * 2 = 128
    CPU constraint = (total YARN cores / # of cores per executor) / # of apps
    CPU constraint = (128 / 4) / 2
    CPU constraint = 16
**設定 num-executors**

    num-executors = Min (memory constraint, CPU constraint)
    num-executors = Min (16, 16)
    num-executors = 16    

