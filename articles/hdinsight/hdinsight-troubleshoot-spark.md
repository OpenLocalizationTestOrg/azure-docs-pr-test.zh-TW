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
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a><span data-ttu-id="02939-104">使用 Azure HDInsight 為 Spark 進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="02939-104">Troubleshoot Spark by using Azure HDInsight</span></span>

<span data-ttu-id="02939-105">了解 hello 最常發生的問題和其解析度使用 Apache Spark 裝載 Apache Ambari 中時。</span><span class="sxs-lookup"><span data-stu-id="02939-105">Learn about hello top issues and their resolutions when working with Apache Spark payloads in Apache Ambari.</span></span>

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a><span data-ttu-id="02939-106">如何使用 Ambari 在叢集上設定 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="02939-106">How do I configure a Spark application by using Ambari on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="02939-107">解決步驟</span><span class="sxs-lookup"><span data-stu-id="02939-107">Resolution steps</span></span>

<span data-ttu-id="02939-108">HDInsight 中先前設定 hello 組態值，這個程序。</span><span class="sxs-lookup"><span data-stu-id="02939-108">hello configuration values for this procedure were previously set in HDInsight.</span></span> <span data-ttu-id="02939-109">toodetermine 的 Spark 組態需要 toobe 組和 toowhat 值，請參閱[導致 Spark 應用程式 OutofMemoryError 例外狀況](#what-causes-a-spark-application-outofmemoryerror-exception)。</span><span class="sxs-lookup"><span data-stu-id="02939-109">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

1. <span data-ttu-id="02939-110">在叢集的 hello 清單中選取**Spark2**。</span><span class="sxs-lookup"><span data-stu-id="02939-110">In hello list of clusters, select **Spark2**.</span></span>

    ![從清單中選取叢集](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. <span data-ttu-id="02939-112">選取 hello **Configs**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="02939-112">Select hello **Configs** tab.</span></span>

    ![選取 hello 組態 索引標籤](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. <span data-ttu-id="02939-114">在 [hello] 清單中的組態，選取**預設 spark2 自訂值**。</span><span class="sxs-lookup"><span data-stu-id="02939-114">In hello list of configurations, select **Custom-spark2-defaults**.</span></span>

    ![選取 [Custom-spark2-defaults]](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. <span data-ttu-id="02939-116">尋找 hello 值，設定您需要 tooadjust，例如**spark.executor.memory**。</span><span class="sxs-lookup"><span data-stu-id="02939-116">Look for hello value setting that you need tooadjust, such as **spark.executor.memory**.</span></span> <span data-ttu-id="02939-117">在此情況下，hello 值**4608 m**太高。</span><span class="sxs-lookup"><span data-stu-id="02939-117">In this case, hello value of **4608m** is too high.</span></span>

    ![選取 hello spark.executor.memory 欄位](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. <span data-ttu-id="02939-119">設定 hello 值 toohello 建議的設定。</span><span class="sxs-lookup"><span data-stu-id="02939-119">Set hello value toohello recommended setting.</span></span> <span data-ttu-id="02939-120">hello 值**2048 m**建議此設定。</span><span class="sxs-lookup"><span data-stu-id="02939-120">hello value **2048m** is recommended for this setting.</span></span>

    ![變更值 too2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. <span data-ttu-id="02939-122">儲存 hello 值並儲存 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="02939-122">Save hello value, and then save hello configuration.</span></span> <span data-ttu-id="02939-123">在 hello 工具列中，選取 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="02939-123">On hello toolbar, select **Save**.</span></span>

    ![儲存 hello 設定和組態](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    <span data-ttu-id="02939-125">如有任何設定需要注意，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="02939-125">You are notified if any configurations need attention.</span></span> <span data-ttu-id="02939-126">請注意 hello 的項目，然後選取 **仍繼續**。</span><span class="sxs-lookup"><span data-stu-id="02939-126">Note hello items, and then select **Proceed Anyway**.</span></span> 

    ![選取 [仍要繼續]](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    <span data-ttu-id="02939-128">撰寫便箋 hello 組態變更的相關資訊，然後選取 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="02939-128">Write a note about hello configuration changes, and then select **Save**.</span></span>

    ![輸入的附註 hello 您所做的變更](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. <span data-ttu-id="02939-130">每次您儲存設定，系統會提示您 toorestart hello 服務。</span><span class="sxs-lookup"><span data-stu-id="02939-130">Whenever a configuration is saved, you are prompted toorestart hello service.</span></span> <span data-ttu-id="02939-131">選取 [重新啟動]。</span><span class="sxs-lookup"><span data-stu-id="02939-131">Select **Restart**.</span></span>

    ![選取 [重新啟動]](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    <span data-ttu-id="02939-133">確認 hello 重新啟動。</span><span class="sxs-lookup"><span data-stu-id="02939-133">Confirm hello restart.</span></span>

    ![選取 [確認全部重新啟動]](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    <span data-ttu-id="02939-135">您可以檢閱 hello 執行的處理序。</span><span class="sxs-lookup"><span data-stu-id="02939-135">You can review hello processes that are running.</span></span>

    ![檢閱執行中的處理序](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. <span data-ttu-id="02939-137">您可以新增設定。</span><span class="sxs-lookup"><span data-stu-id="02939-137">You can add configurations.</span></span> <span data-ttu-id="02939-138">在設定的 hello 清單中選取**預設 spark2 自訂值**，然後選取**加入屬性**。</span><span class="sxs-lookup"><span data-stu-id="02939-138">In hello list of configurations, select **Custom-spark2-defaults**, and then select **Add Property**.</span></span>

    ![選取 [新增屬性]](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. <span data-ttu-id="02939-140">定義新的屬性。</span><span class="sxs-lookup"><span data-stu-id="02939-140">Define a new property.</span></span> <span data-ttu-id="02939-141">您可以使用特定的設定，例如 hello 資料類型的對話方塊來定義單一屬性。</span><span class="sxs-lookup"><span data-stu-id="02939-141">You can define a single property by using a dialog box for specific settings such as hello data type.</span></span> <span data-ttu-id="02939-142">或者，您也可以使用一行一定義的方式定義多個屬性。</span><span class="sxs-lookup"><span data-stu-id="02939-142">Or, you can define multiple properties by using one definition per line.</span></span> 

    <span data-ttu-id="02939-143">在此範例中，hello **spark.driver.memory**值是定義屬性**4g**。</span><span class="sxs-lookup"><span data-stu-id="02939-143">In this example, hello **spark.driver.memory** property is defined with a value of **4g**.</span></span>

    ![定義新的屬性](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. <span data-ttu-id="02939-145">儲存 hello 組態，然後重新 hello 服務步驟 6 和 7 中所述。</span><span class="sxs-lookup"><span data-stu-id="02939-145">Save hello configuration, and then restart hello service as described in steps 6 and 7.</span></span>

<span data-ttu-id="02939-146">這些變更是整個叢集，但當您送出 hello Spark 作業可以覆寫。</span><span class="sxs-lookup"><span data-stu-id="02939-146">These changes are cluster-wide but can be overridden when you submit hello Spark job.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="02939-147">其他閱讀資料</span><span class="sxs-lookup"><span data-stu-id="02939-147">Additional reading</span></span>

[<span data-ttu-id="02939-148">提交 HDInsight 叢集上的 Spark 作業</span><span class="sxs-lookup"><span data-stu-id="02939-148">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a><span data-ttu-id="02939-149">如何使用 Jupyter 筆記本在叢集上設定 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="02939-149">How do I configure a Spark application by using a Jupyter notebook on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="02939-150">解決步驟</span><span class="sxs-lookup"><span data-stu-id="02939-150">Resolution steps</span></span>

1. <span data-ttu-id="02939-151">toodetermine 的 Spark 組態需要 toobe 組和 toowhat 值，請參閱[導致 Spark 應用程式 OutofMemoryError 例外狀況](#what-causes-a-spark-application-outofmemoryerror-exception)。</span><span class="sxs-lookup"><span data-stu-id="02939-151">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="02939-152">Hello hello Jupyter 筆記本 hello 之後的第一個資料格**%%設定**指示詞，指定有效的 JSON 格式的 hello Spark 組態。</span><span class="sxs-lookup"><span data-stu-id="02939-152">In hello first cell of hello Jupyter notebook, after hello **%%configure** directive, specify hello Spark configurations in valid JSON format.</span></span> <span data-ttu-id="02939-153">視需要變更 hello 實際值：</span><span class="sxs-lookup"><span data-stu-id="02939-153">Change hello actual values as necessary:</span></span>

    ![新增設定](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a><span data-ttu-id="02939-155">其他閱讀資料</span><span class="sxs-lookup"><span data-stu-id="02939-155">Additional reading</span></span>

[<span data-ttu-id="02939-156">提交 HDInsight 叢集上的 Spark 作業</span><span class="sxs-lookup"><span data-stu-id="02939-156">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a><span data-ttu-id="02939-157">如何使用 Livy 在叢集上設定 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="02939-157">How do I configure a Spark application by using Livy on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="02939-158">解決步驟</span><span class="sxs-lookup"><span data-stu-id="02939-158">Resolution steps</span></span>

1. <span data-ttu-id="02939-159">toodetermine 的 Spark 組態需要 toobe 組和 toowhat 值，請參閱[導致 Spark 應用程式 OutofMemoryError 例外狀況](#what-causes-a-spark-application-outofmemoryerror-exception)。</span><span class="sxs-lookup"><span data-stu-id="02939-159">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

2. <span data-ttu-id="02939-160">使用 cURL 像 REST 用戶端提交 hello Spark 應用程式 tooLivy。</span><span class="sxs-lookup"><span data-stu-id="02939-160">Submit hello Spark application tooLivy by using a REST client like cURL.</span></span> <span data-ttu-id="02939-161">使用類似 toohello 後的命令。</span><span class="sxs-lookup"><span data-stu-id="02939-161">Use a command similar toohello following.</span></span> <span data-ttu-id="02939-162">視需要變更 hello 實際值：</span><span class="sxs-lookup"><span data-stu-id="02939-162">Change hello actual values as necessary:</span></span>

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a><span data-ttu-id="02939-163">其他閱讀資料</span><span class="sxs-lookup"><span data-stu-id="02939-163">Additional reading</span></span>

[<span data-ttu-id="02939-164">提交 HDInsight 叢集上的 Spark 作業</span><span class="sxs-lookup"><span data-stu-id="02939-164">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a><span data-ttu-id="02939-165">如何使用 spark-submit 在叢集上設定 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="02939-165">How do I configure a Spark application by using spark-submit on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="02939-166">解決步驟</span><span class="sxs-lookup"><span data-stu-id="02939-166">Resolution steps</span></span>

1. <span data-ttu-id="02939-167">toodetermine 的 Spark 組態需要 toobe 組和 toowhat 值，請參閱[導致 Spark 應用程式 OutofMemoryError 例外狀況](#what-causes-a-spark-application-outofmemoryerror-exception)。</span><span class="sxs-lookup"><span data-stu-id="02939-167">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="02939-168">使用類似 toohello 後的命令，以啟動 spark 殼層。</span><span class="sxs-lookup"><span data-stu-id="02939-168">Launch spark-shell by using a command similar toohello following.</span></span> <span data-ttu-id="02939-169">視需要變更 hello 的 hello 組態的實際值：</span><span class="sxs-lookup"><span data-stu-id="02939-169">Change hello actual value of hello configurations as necessary:</span></span> 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a><span data-ttu-id="02939-170">其他閱讀資料</span><span class="sxs-lookup"><span data-stu-id="02939-170">Additional reading</span></span>

[<span data-ttu-id="02939-171">提交 HDInsight 叢集上的 Spark 作業</span><span class="sxs-lookup"><span data-stu-id="02939-171">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a><span data-ttu-id="02939-172">造成 Spark 應用程式 OutofMemoryError 例外狀況的原因</span><span class="sxs-lookup"><span data-stu-id="02939-172">What causes a Spark application OutofMemoryError exception</span></span>

### <a name="detailed-description"></a><span data-ttu-id="02939-173">詳細描述</span><span class="sxs-lookup"><span data-stu-id="02939-173">Detailed description</span></span>

<span data-ttu-id="02939-174">hello Spark 應用程式失敗，並遵循無法攔截的例外狀況類型的 hello:</span><span class="sxs-lookup"><span data-stu-id="02939-174">hello Spark application fails, with hello following types of uncaught exceptions:</span></span>

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

### <a name="probable-cause"></a><span data-ttu-id="02939-175">可能的原因</span><span class="sxs-lookup"><span data-stu-id="02939-175">Probable cause</span></span>

<span data-ttu-id="02939-176">hello 最有可能造成此例外狀況是堆積記憶體不足，無法配置 toohello Java 虛擬機器 (JVMs)。</span><span class="sxs-lookup"><span data-stu-id="02939-176">hello most likely cause of this exception is that not enough heap memory is allocated toohello Java virtual machines (JVMs).</span></span> <span data-ttu-id="02939-177">為執行程式或驅動程式會啟動這些 JVMs，hello Spark 應用程式的一部分。</span><span class="sxs-lookup"><span data-stu-id="02939-177">These JVMs are launched as executors or drivers as part of hello Spark application.</span></span> 

### <a name="resolution-steps"></a><span data-ttu-id="02939-178">解決步驟</span><span class="sxs-lookup"><span data-stu-id="02939-178">Resolution steps</span></span>

1. <span data-ttu-id="02939-179">判斷 hello hello 資料 hello Spark 應用程式控點的大小上限。</span><span class="sxs-lookup"><span data-stu-id="02939-179">Determine hello maximum size of hello data hello Spark application handles.</span></span> <span data-ttu-id="02939-180">您可以進行猜測，根據 hello hello 輸入資料，hello 轉換 hello 輸入的資料和 hello hello 應用程式會進一步轉換 hello 中繼資料時產生的輸出資料所產生的中繼資料的大小上限。</span><span class="sxs-lookup"><span data-stu-id="02939-180">You can make a guess based on hello maximum size of hello input data, hello intermediate data that's produced by transforming hello input data, and hello output data that's produced when hello application is further transforming hello intermediate data.</span></span> <span data-ttu-id="02939-181">如果您無法進行正式的初始估算，也可以設定為反覆的程序。</span><span class="sxs-lookup"><span data-stu-id="02939-181">This process can be an iterative if you can't make an initial formal guess.</span></span> 

2. <span data-ttu-id="02939-182">請確定該 hello HDInsight 叢集，您將 toouse 有足夠的記憶體及核心 tooaccommodate hello Spark 應用程式方面的資源。</span><span class="sxs-lookup"><span data-stu-id="02939-182">Make sure that hello HDInsight cluster that you're going toouse has enough resources in terms of memory and cores tooaccommodate hello Spark application.</span></span> <span data-ttu-id="02939-183">您可以判斷這檢視 hello 叢集度量 hello 值 hello YARN UI 段的**記憶體使用**vs。**記憶體總計**，以及**已使用的 VCore** 和**VCore 總計**的值。</span><span class="sxs-lookup"><span data-stu-id="02939-183">You can determine this by viewing hello cluster metrics section of hello YARN UI for hello values of **Memory Used** vs. **Memory Total**, and **VCores Used** vs. **VCores Total**.</span></span>

3. <span data-ttu-id="02939-184">設定下列 Spark hello 組態 tooappropriate 值不應該超過 90%的可用記憶體的 hello 和核心。</span><span class="sxs-lookup"><span data-stu-id="02939-184">Set hello following Spark configurations tooappropriate values, which should not exceed 90% of hello available memory and cores.</span></span> <span data-ttu-id="02939-185">hello 值應該是 hello 的內 hello Spark 應用程式的記憶體需求：</span><span class="sxs-lookup"><span data-stu-id="02939-185">hello values should be well within hello memory requirements of hello Spark application:</span></span> 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    <span data-ttu-id="02939-186">tooget hello 總所使用的記憶體執行所有的程式，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="02939-186">tooget hello total memory used by all executors, run hello following command:</span></span> 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    <span data-ttu-id="02939-187">tooget hello 使用的記憶體總數 hello 驅動程式，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="02939-187">tooget hello total memory used by hello driver, run hello following command:</span></span>
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a><span data-ttu-id="02939-188">其他閱讀資料</span><span class="sxs-lookup"><span data-stu-id="02939-188">Additional reading</span></span>

- [<span data-ttu-id="02939-189">Spark 記憶體管理概觀</span><span class="sxs-lookup"><span data-stu-id="02939-189">Spark memory management overview</span></span>](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- <span data-ttu-id="02939-190">[Debug a Spark application on an HDInsight cluster](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/) (在 HDInsight 叢集上偵錯 Spark 應用程式)</span><span class="sxs-lookup"><span data-stu-id="02939-190">[Debug a Spark application on an HDInsight cluster](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/)</span></span>

