---
title: "資料湖存放區 MapReduce 效能調整指導方針 aaaAzure |Microsoft 文件"
description: "Azure Data Lake Store MapReduce 效能微調方針"
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
ms.openlocfilehash: e21414a23530e65613c85156af0209c88ec54d2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-mapreduce-on-hdinsight-and-azure-data-lake-store"></a>HDInsight 和 Azure Data Lake Store 上的 MapReduce 效能微調方針


## <a name="prerequisites"></a>必要條件

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure Data Lake Store 帳戶**。 如需有關指示 toocreate 一個，請參閱[開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)
* **Azure HDInsight 叢集**與存取 tooa Data Lake Store 帳戶。 請參閱 [建立具有 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-portal.md)。 請確定您已啟用遠端桌面 hello 叢集。
* **在 HDInsight 上使用 MapReduce**。  如需詳細資訊，請參閱[在 HDInsight 上的 Hadoop 中使用 MapReduce](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-mapreduce)  
* **ADLS 的效能微調指導方針**。  如需一般的效能概念，請參閱 [Data Lake Store 效能微調指導方針](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)  

## <a name="parameters"></a>參數

當執行 MapReduce 工作，以下是 hello 最重要的參數，您可以在 ADLS 設定 tooincrease 效能：

* **Mapreduce.map.memory.mb** – 記憶體 tooallocate tooeach 對應工具的 hello 數量
* **Mapreduce.job.maps** – hello 對應每個作業的工作數目
* **Mapreduce.reduce.memory.mb** – 記憶體 tooallocate tooeach 減壓器的 hello 數量
* **Mapreduce.job.reduces** – hello 減少每個作業的工作數目

**Mapreduce.map.memory / Mapreduce.reduce.memory**這個數字應該根據 hello 對應需要的記憶體容量調整和/或減少工作。  mapreduce.map.memory 與 mapreduce.reduce.memory hello 預設值可以透過 hello Yarn 組態 Ambari 進行檢視。  在 Ambari 瀏覽 tooYARN 並檢視 hello 組態 索引標籤。 將會顯示 hello YARN 記憶體。  

**Mapreduce.job.maps / Mapreduce.job.reduces**這會決定 hello 自行或 reducers toobe 建立的數目上限。  hello 分割數會決定多少自行建立 hello MapReduce 工作。  因此，您可能會收到較少自行比您要求是否有較少分割比 hello 自行要求數目。       

## <a name="guidance"></a>指引

**步驟 1： 決定執行工作的數目**-根據預設，MapReduce 將適用於您作業使用 hello 整個叢集。  您可以使用更少的 hello 叢集使用較少對應工具中有可用的容器。  這份文件中的 hello 指導方針會假設您的應用程式在您的叢集上執行 hello 只有應用程式。      

**步驟 2： 設定 mapreduce.map.memory/mapreduce.reduce.memory** – hello hello 記憶體對應的大小並降低工作將會相依於您特定的工作。  如果您想 tooincrease 並行存取，您可以減少 hello 記憶體大小。  同時執行工作的 hello 數目取決於 hello 數目的容器。  藉由降低 hello 每個對應或減壓器的記憶體數量，多個容器可以建立，可讓多個對應或 reducers toorun 同時。  太多記憶體的遞減 hello 數量可能會導致某些處理程序 toorun，記憶體不足。  如果執行您的工作時，您可以取得堆積錯誤，您應該增加每個對應或減壓器 hello 記憶體。  您應該考慮到，新增更多容器會對每個額外的容器新增額外的負擔，而可能降低效能。  另一個替代方法是 tooget 更多的記憶體使用擁有較高的記憶體數量的叢集，或增加 hello 叢集中的節點數目。  更多的記憶體可讓多個容器 toobe 使用，這表示多個並行存取。  

**步驟 3： 決定總 YARN 記憶體**-tootune mapreduce.job.maps/mapreduce.job.reduces，您應該考慮 hello 可供使用的總 YARN 記憶體數量。  這項資訊可在 Ambari 中取得。  瀏覽 tooYARN 並檢視 hello 組態 索引標籤。 hello YARN 記憶體會顯示此視窗中。  您應該在叢集 tooget hello 總 YARN 記憶體乘以 hello YARN 記憶體與 hello 節點數目。

    Total YARN memory = nodes * YARN memory per node
如果您使用空白的叢集，記憶體可以是 hello YARN 記憶體總計為您的叢集。  如果其他應用程式可以藉由減少 hello 自行或 reducers toohello 數目的容器數目選擇 tooonly 使用您的叢集記憶體的一部分使用的記憶體，您會想 toouse。  

**步驟 4： 計算 YARN 容器數目**– YARN 容器聽寫 hello 可用 hello 作業並行處理的數量。  取得 YARN 記憶體總數，然後除以 mapreduce.map.memory。  

    # of YARN containers = total YARN memory / mapreduce.map.memory

**步驟 5： 設定 mapreduce.job.maps/mapreduce.job.reduces**設定 mapreduce.job.maps/mapreduce.job.reduces tooat 可用的容器的最小 hello 數目。  您可以試驗進一步增加 hello 自行和 reducers toosee 數目，如果您取得較佳的效能。  請記住，更多的對應器會產生額外的負擔，因此對應器過多可能會降低效能。  

CPU 排程和 CPU 隔離會關閉預設讓 hello YARN 容器的數目由記憶體限制。

## <a name="example-calculation"></a>範例計算

讓我們假設您目前有 8 個 D14 節點所組成的叢集，而且您想 toorun I/O 大量工作。  以下是您應該執行的 hello 計算：

**步驟 1： 決定執行工作的數目**-此範例中，我們假設我們的責任是 hello 只有一個執行。  

**步驟 2︰設定 mapreduce.map.memory/mapreduce.reduce.memory** – 在我們的範例中，您將會執行 I/O 密集作業，並決定 3 GB 的記憶體已足夠對應工作使用。

    mapreduce.map.memory = 3GB
**步驟 3︰確定 YARN 記憶體總數**

    total memory from hello cluster is 8 nodes * 96GB of YARN memory for a D14 = 768GB
**步驟 4︰計算 YARN 容器的數目**

    # of YARN containers = 768GB of available memory / 3 GB of memory =   256

**步驟 5：設定 mapreduce.job.maps/mapreduce.job.reduces**

    mapreduce.map.jobs = 256

## <a name="limitations"></a>限制

**ADLS 節流**

ADLS 是多租用戶服務，因此會設定帳戶層級的頻寬限制。  如果您叫用這些限制，您將啟動 toosee 工作失敗。 透過觀察工作記錄檔中的節流錯誤即可加以識別。  如果您的作業需要更多頻寬，請與我們連絡。   

如果您節流 toocheck，您需要 tooenable hello 偵錯記錄 hello 用戶端。 做法如下：

1. Put hello 下列 hello log4j 屬性中 Ambari 屬性 > YARN > 組態 > 進階 yarn log4j: log4j.logger.com.microsoft.azure.datalake.store=DEBUG

2. 重新啟動所有 hello 節點/服務 hello config tootake 效果。

3. 如果您節流，您會看到 hello YARN 記錄檔中的 hello HTTP 429 錯誤程式碼。 hello YARN 記錄檔位於 /tmp/&lt;使用者&gt;/yarn.log

## <a name="examples-toorun"></a>範例 tooRun

toodemonstrate 如何在 Azure 資料湖存放區上執行 MapReduce 下面是一些已在叢集執行，以下列設定的 hello 的範例程式碼：

* 16 節點 D14v2
* 執行 HDI 3.6 的 Hadoop 叢集

起點，以下是一些範例命令 toorun MapReduce Teragen、 Terasort 和 Teravalidate。  您可以根據您的資源調整這些命令。

**Teragen**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 10000000000 adl://example/data/1TB-sort-input

**Terasort**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 -Dmapreduce.job.reduces=512 -Dmapreduce.reduce.memory.mb=3072 adl://example/data/1TB-sort-input adl://example/data/1TB-sort-output

**Teravalidate**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapreduce.job.maps=512 -Dmapreduce.map.memory.mb=3072 adl://example/data/1TB-sort-output adl://example/data/1TB-sort-validate
