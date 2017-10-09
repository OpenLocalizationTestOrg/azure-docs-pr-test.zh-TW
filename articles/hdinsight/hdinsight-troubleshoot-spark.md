---
title: "使用 Azure HDInsight aaaTroubleshoot Spark |Microsoft 文件"
description: "取得解答 toocommon 疑問 Apache Spark 與 Azure HDInsight 工作。"
keywords: "Azure HDInsight, Spark, 常見問題集, 疑難排解指南, 常見問題, 應用程式設定, Ambari"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: 25D89586-DE5B-4268-B5D5-CC2CE12207ED
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: c9f910daf295462238a3143ae2589db6d383097f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a>使用 Azure HDInsight 為 Spark 進行疑難排解

了解 hello 最常發生的問題和其解析度使用 Apache Spark 裝載 Apache Ambari 中時。

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a>如何使用 Ambari 在叢集上設定 Spark 應用程式

### <a name="resolution-steps"></a>解決步驟

HDInsight 中先前設定 hello 組態值，這個程序。 toodetermine 的 Spark 組態需要 toobe 組和 toowhat 值，請參閱[導致 Spark 應用程式 OutofMemoryError 例外狀況](#what-causes-a-spark-application-outofmemoryerror-exception)。 

1. 在叢集的 hello 清單中選取**Spark2**。

    ![從清單中選取叢集](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. 選取 hello **Configs**  索引標籤。

    ![選取 hello 組態 索引標籤](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. 在 [hello] 清單中的組態，選取**預設 spark2 自訂值**。

    ![選取 [Custom-spark2-defaults]](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. 尋找 hello 值，設定您需要 tooadjust，例如**spark.executor.memory**。 在此情況下，hello 值**4608 m**太高。

    ![選取 hello spark.executor.memory 欄位](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. 設定 hello 值 toohello 建議的設定。 hello 值**2048 m**建議此設定。

    ![變更值 too2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. 儲存 hello 值並儲存 hello 組態。 在 hello 工具列中，選取 **儲存**。

    ![儲存 hello 設定和組態](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    如有任何設定需要注意，您會收到通知。 請注意 hello 的項目，然後選取 **仍繼續**。 

    ![選取 [仍要繼續]](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    撰寫便箋 hello 組態變更的相關資訊，然後選取 **儲存**。

    ![輸入的附註 hello 您所做的變更](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. 每次您儲存設定，系統會提示您 toorestart hello 服務。 選取 [重新啟動]。

    ![選取 [重新啟動]](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    確認 hello 重新啟動。

    ![選取 [確認全部重新啟動]](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    您可以檢閱 hello 執行的處理序。

    ![檢閱執行中的處理序](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. 您可以新增設定。 在設定的 hello 清單中選取**預設 spark2 自訂值**，然後選取**加入屬性**。

    ![選取 [新增屬性]](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. 定義新的屬性。 您可以使用特定的設定，例如 hello 資料類型的對話方塊來定義單一屬性。 或者，您也可以使用一行一定義的方式定義多個屬性。 

    在此範例中，hello **spark.driver.memory**值是定義屬性**4g**。

    ![定義新的屬性](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. 儲存 hello 組態，然後重新 hello 服務步驟 6 和 7 中所述。

這些變更是整個叢集，但當您送出 hello Spark 作業可以覆寫。

### <a name="additional-reading"></a>其他閱讀資料

[提交 HDInsight 叢集上的 Spark 作業](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a>如何使用 Jupyter 筆記本在叢集上設定 Spark 應用程式

### <a name="resolution-steps"></a>解決步驟

1. toodetermine 的 Spark 組態需要 toobe 組和 toowhat 值，請參閱[導致 Spark 應用程式 OutofMemoryError 例外狀況](#what-causes-a-spark-application-outofmemoryerror-exception)。

2. Hello hello Jupyter 筆記本 hello 之後的第一個資料格**%%設定**指示詞，指定有效的 JSON 格式的 hello Spark 組態。 視需要變更 hello 實際值：

    ![新增設定](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a>其他閱讀資料

[提交 HDInsight 叢集上的 Spark 作業](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a>如何使用 Livy 在叢集上設定 Spark 應用程式

### <a name="resolution-steps"></a>解決步驟

1. toodetermine 的 Spark 組態需要 toobe 組和 toowhat 值，請參閱[導致 Spark 應用程式 OutofMemoryError 例外狀況](#what-causes-a-spark-application-outofmemoryerror-exception)。 

2. 使用 cURL 像 REST 用戶端提交 hello Spark 應用程式 tooLivy。 使用類似 toohello 後的命令。 視需要變更 hello 實際值：

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a>其他閱讀資料

[提交 HDInsight 叢集上的 Spark 作業](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a>如何使用 spark-submit 在叢集上設定 Spark 應用程式

### <a name="resolution-steps"></a>解決步驟

1. toodetermine 的 Spark 組態需要 toobe 組和 toowhat 值，請參閱[導致 Spark 應用程式 OutofMemoryError 例外狀況](#what-causes-a-spark-application-outofmemoryerror-exception)。

2. 使用類似 toohello 後的命令，以啟動 spark 殼層。 視需要變更 hello 的 hello 組態的實際值： 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a>其他閱讀資料

[提交 HDInsight 叢集上的 Spark 作業](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a>造成 Spark 應用程式 OutofMemoryError 例外狀況的原因

### <a name="detailed-description"></a>詳細描述

hello Spark 應用程式失敗，並遵循無法攔截的例外狀況類型的 hello:

```apache
ERROR Executor: Exception in task 7.0 in stage 6.0 (TID 439) 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

```apache
ERROR SparkUncaughtExceptionHandler: Uncaught exception in thread Thread[Executor task launch worker-0,5,main] 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

### <a name="probable-cause"></a>可能的原因

hello 最有可能造成此例外狀況是堆積記憶體不足，無法配置 toohello Java 虛擬機器 (JVMs)。 為執行程式或驅動程式會啟動這些 JVMs，hello Spark 應用程式的一部分。 

### <a name="resolution-steps"></a>解決步驟

1. 判斷 hello hello 資料 hello Spark 應用程式控點的大小上限。 您可以進行猜測，根據 hello hello 輸入資料，hello 轉換 hello 輸入的資料和 hello hello 應用程式會進一步轉換 hello 中繼資料時產生的輸出資料所產生的中繼資料的大小上限。 如果您無法進行正式的初始估算，也可以設定為反覆的程序。 

2. 請確定該 hello HDInsight 叢集，您將 toouse 有足夠的記憶體及核心 tooaccommodate hello Spark 應用程式方面的資源。 您可以判斷這檢視 hello 叢集度量 hello 值 hello YARN UI 段的**記憶體使用**vs。**記憶體總計**，以及**已使用的 VCore** 和**VCore 總計**的值。

3. 設定下列 Spark hello 組態 tooappropriate 值不應該超過 90%的可用記憶體的 hello 和核心。 hello 值應該是 hello 的內 hello Spark 應用程式的記憶體需求： 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    tooget hello 總所使用的記憶體執行所有的程式，執行下列命令的 hello: 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    tooget hello 使用的記憶體總數 hello 驅動程式，執行下列命令的 hello:
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a>其他閱讀資料

- [Spark 記憶體管理概觀](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- [Debug a Spark application on an HDInsight cluster](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/) (在 HDInsight 叢集上偵錯 Spark 應用程式)

