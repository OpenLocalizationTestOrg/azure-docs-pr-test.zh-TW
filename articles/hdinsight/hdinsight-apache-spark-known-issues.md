---
title: "針對 Azure HDInsight 中的 Apache Spark 叢集問題進行疑難排解 | Microsoft Docs"
description: "了解 Azure HDInsight 中的 Apache Spark 叢集相關問題，以及如何解決這些問題。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3a493a2c35a6cdd31bb1e4ff66113a8f8d97d4f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="b7b43-103">HDInsight 上的 Apache Spark 叢集已知問題</span><span class="sxs-lookup"><span data-stu-id="b7b43-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="b7b43-104">這份文件記錄 HDInsight Spark 公開預覽版本的所有已知問題。</span><span class="sxs-lookup"><span data-stu-id="b7b43-104">This document keeps track of all the known issues for the HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="b7b43-105">Livy 會流失互動式工作階段</span><span class="sxs-lookup"><span data-stu-id="b7b43-105">Livy leaks interactive session</span></span>
<span data-ttu-id="b7b43-106">Livy 在有互動式工作階段仍作用中的情況下重新啟動時 (從 Ambari 或是因為前端節點 0 虛擬機器重新開機)，互動式作業工作階段將會流失。</span><span class="sxs-lookup"><span data-stu-id="b7b43-106">When Livy is restarted (from Ambari or due to headnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="b7b43-107">因為這個緣故，新的作業可能會卡在「已接受」狀態中，而無法啟動。</span><span class="sxs-lookup"><span data-stu-id="b7b43-107">Because of this, new jobs can stuck in the Accepted state, and cannot be started.</span></span>

<span data-ttu-id="b7b43-108">**緩和：**</span><span class="sxs-lookup"><span data-stu-id="b7b43-108">**Mitigation:**</span></span>

<span data-ttu-id="b7b43-109">請使用下列程序解決此問題：</span><span class="sxs-lookup"><span data-stu-id="b7b43-109">Use the following procedure to workaround the issue:</span></span>

1. <span data-ttu-id="b7b43-110">Ssh 到前端節點。</span><span class="sxs-lookup"><span data-stu-id="b7b43-110">Ssh into headnode.</span></span> <span data-ttu-id="b7b43-111">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="b7b43-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="b7b43-112">執行下列命令，以尋找透過 Livy 啟動之互動式作業的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="b7b43-112">Run the following command to find the application IDs of the interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="b7b43-113">如果作業是透過未指定明確名稱的 Livy 互動式工作階段而啟動的，預設的作業名稱將是 Livy；如果是由 Jupyter Notebook 啟動的 Livy 工作階段，則作業名稱將會以 remotesparkmagics_* 開頭。</span><span class="sxs-lookup"><span data-stu-id="b7b43-113">The default job names will be Livy if the jobs were started with a Livy interactive session with no explicit names specified, For the Livy session started by Jupyter notebook, the job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="b7b43-114">執行下列命令以刪除這些作業。</span><span class="sxs-lookup"><span data-stu-id="b7b43-114">Run the following command to kill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="b7b43-115">新作業將會開始執行。</span><span class="sxs-lookup"><span data-stu-id="b7b43-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="b7b43-116">Spark 歷程記錄伺服器未啟動</span><span class="sxs-lookup"><span data-stu-id="b7b43-116">Spark History Server not started</span></span>
<span data-ttu-id="b7b43-117">叢集建立後，不會自動啟動 Spark 歷程記錄伺服器。</span><span class="sxs-lookup"><span data-stu-id="b7b43-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="b7b43-118">**緩和：**</span><span class="sxs-lookup"><span data-stu-id="b7b43-118">**Mitigation:**</span></span> 

<span data-ttu-id="b7b43-119">請從 Ambari 手動啟動歷程記錄伺服器。</span><span class="sxs-lookup"><span data-stu-id="b7b43-119">Manually start the history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="b7b43-120">Spark 記錄檔目錄中的權限問題</span><span class="sxs-lookup"><span data-stu-id="b7b43-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="b7b43-121">在 hdiuser 透過 spark-submit 提交作業時，將會發生錯誤 java.io.FileNotFoundException：/var/log/spark/sparkdriver_hdiuser.log (沒有使用權限)，且不會寫入驅動程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b7b43-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and the driver log is not written.</span></span> 

<span data-ttu-id="b7b43-122">**緩和：**</span><span class="sxs-lookup"><span data-stu-id="b7b43-122">**Mitigation:**</span></span>

1. <span data-ttu-id="b7b43-123">將 hdiuser 新增至 Hadoop 群組。</span><span class="sxs-lookup"><span data-stu-id="b7b43-123">Add hdiuser to the Hadoop group.</span></span> 
2. <span data-ttu-id="b7b43-124">在叢集建立之後，提供 /var/log/spark 的 777 權限。</span><span class="sxs-lookup"><span data-stu-id="b7b43-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="b7b43-125">使用 Ambari 將 Spark 記錄檔位置更新為具有 777 權限的目錄。</span><span class="sxs-lookup"><span data-stu-id="b7b43-125">Update the spark log location using Ambari to be a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="b7b43-126">以 sudo 的身分執行 spark-submit。</span><span class="sxs-lookup"><span data-stu-id="b7b43-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="b7b43-127">不支援 Spark-Phoenix 連接器</span><span class="sxs-lookup"><span data-stu-id="b7b43-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="b7b43-128">目前不支援將 Spark-Phoenix 連接器與 HDInsight Spark 叢集搭配使用。</span><span class="sxs-lookup"><span data-stu-id="b7b43-128">Currently, the Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="b7b43-129">**緩和：**</span><span class="sxs-lookup"><span data-stu-id="b7b43-129">**Mitigation:**</span></span>

<span data-ttu-id="b7b43-130">您必須改用 Spark-HBase 連接器。</span><span class="sxs-lookup"><span data-stu-id="b7b43-130">You must use the Spark-HBase connector instead.</span></span> <span data-ttu-id="b7b43-131">如需指示，請參閱[如何使用 Spark-HBase 連接器 (英文)](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/)。</span><span class="sxs-lookup"><span data-stu-id="b7b43-131">For instructions see [How to use Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-to-jupyter-notebooks"></a><span data-ttu-id="b7b43-132">Jupyter Notebook 的相關問題</span><span class="sxs-lookup"><span data-stu-id="b7b43-132">Issues related to Jupyter notebooks</span></span>
<span data-ttu-id="b7b43-133">以下是 Jupyter Notebook 的已知問題。</span><span class="sxs-lookup"><span data-stu-id="b7b43-133">Following are some known issues related to Jupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="b7b43-134">Notebook 在檔名中有非 ASCII 字元</span><span class="sxs-lookup"><span data-stu-id="b7b43-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="b7b43-135">可以用在 Spark HDInsight 叢集中的 Jupyter Notebook，檔名中不該有非 ASCII 字元。</span><span class="sxs-lookup"><span data-stu-id="b7b43-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="b7b43-136">如果您嘗試透過有非 ASCII 檔名的 Jupyter UI 上傳檔案，它會以無訊息方式失敗 (亦即 Jupyter 不會讓您上傳檔案，但也不會擲回可見的錯誤)。</span><span class="sxs-lookup"><span data-stu-id="b7b43-136">If you try to upload a file through the Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload the file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="b7b43-137">載入大型 Notebook 時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="b7b43-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="b7b43-138">載入大型 Notebook 時，您可能會看到錯誤訊息 **`Error loading notebook`** 。</span><span class="sxs-lookup"><span data-stu-id="b7b43-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="b7b43-139">**緩和：**</span><span class="sxs-lookup"><span data-stu-id="b7b43-139">**Mitigation:**</span></span>

<span data-ttu-id="b7b43-140">如果您收到這個錯誤，並不表示您的資料已損毀或遺失。</span><span class="sxs-lookup"><span data-stu-id="b7b43-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="b7b43-141">您的 Notebook 仍在磁碟的 `/var/lib/jupyter`中，您可以透過 SSH 連線到叢集來加以存取。</span><span class="sxs-lookup"><span data-stu-id="b7b43-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into the cluster to access them.</span></span> <span data-ttu-id="b7b43-142">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="b7b43-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="b7b43-143">在您使用 SSH 連線到叢集之後，您可以從叢集中將 Notebook 複製到本機電腦 (使用 SCP 或 WinSCP) 來做為備份，以避免遺失 Notebook 中的重要資料。</span><span class="sxs-lookup"><span data-stu-id="b7b43-143">Once you have connected to the cluster using SSH, you can copy your notebooks from your cluster to your local machine (using SCP or WinSCP) as a backup to prevent the loss of any important data in the notebook.</span></span> <span data-ttu-id="b7b43-144">您接著可以在連接埠 8001 以 SSH 通道連到前端節點，以存取 Jupyter 而不透過閘道。</span><span class="sxs-lookup"><span data-stu-id="b7b43-144">You can then SSH tunnel into your headnode at port 8001 to access Jupyter without going through the gateway.</span></span>  <span data-ttu-id="b7b43-145">您可以從該處清除 Notebook 的輸出，並將其重新儲存，以盡量縮減 Notebook 的大小。</span><span class="sxs-lookup"><span data-stu-id="b7b43-145">From there, you can clear the output of your notebook and re-save it to minimize the notebook’s size.</span></span>

<span data-ttu-id="b7b43-146">若要防止日後再發生此錯誤，您必須遵循一些最佳作法：</span><span class="sxs-lookup"><span data-stu-id="b7b43-146">To prevent this error from happening in the future, you must follow some best practices:</span></span>

* <span data-ttu-id="b7b43-147">務必讓 Notebook 保持小型規模。</span><span class="sxs-lookup"><span data-stu-id="b7b43-147">It is important to keep the notebook size small.</span></span> <span data-ttu-id="b7b43-148">會傳回到 Jupyter 的任何 Spark 作業輸出皆會保存在 Notebook 中。</span><span class="sxs-lookup"><span data-stu-id="b7b43-148">Any output from your Spark jobs that is sent back to Jupyter is persisted in the notebook.</span></span>  <span data-ttu-id="b7b43-149">一般來說，Jupyter 的最佳做法是避免在大型 RDD 或資料框架上執行 `.collect()`。相反地，如果您想要查看 RDD 的內容，請考慮執行 `.take()` 或 `.sample()`，這可讓輸出不會變得太大。</span><span class="sxs-lookup"><span data-stu-id="b7b43-149">It is a best practice with Jupyter in general to avoid running `.collect()` on large RDD’s or dataframes; instead, if you want to peek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="b7b43-150">此外，當您儲存 Notebook 時，請清除所有輸出儲存格以減少大小。</span><span class="sxs-lookup"><span data-stu-id="b7b43-150">Also, when you save a notebook, clear all output cells to reduce the size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="b7b43-151">Notebook 的初始啟動比預期耗時</span><span class="sxs-lookup"><span data-stu-id="b7b43-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="b7b43-152">在使用 Spark magic 的 Jupyter Notebook 中，第一個程式碼陳述式可能需耗時一分鐘以上才能執行完畢。</span><span class="sxs-lookup"><span data-stu-id="b7b43-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="b7b43-153">**說明：**</span><span class="sxs-lookup"><span data-stu-id="b7b43-153">**Explanation:**</span></span>

<span data-ttu-id="b7b43-154">這會在執行第一個程式碼儲存格時發生。</span><span class="sxs-lookup"><span data-stu-id="b7b43-154">This happens because when the first code cell is run.</span></span> <span data-ttu-id="b7b43-155">它會在背景中起始設定工作階段組態，以及設定 SQL、Spark 和 Hive 內容。</span><span class="sxs-lookup"><span data-stu-id="b7b43-155">In the background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="b7b43-156">設定這些內容後，第一個陳述式才會執行，因此會有陳述式會花很長時間完成的印象。</span><span class="sxs-lookup"><span data-stu-id="b7b43-156">After these contexts are set, the first statement is run and this gives the impression that the statement took a long time to complete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-the-session"></a><span data-ttu-id="b7b43-157">Jupyter Notebook 建立工作階段逾時</span><span class="sxs-lookup"><span data-stu-id="b7b43-157">Jupyter notebook timeout in creating the session</span></span>
<span data-ttu-id="b7b43-158">當 Spark 叢集的資源不足時，Jupyter Notebook 中的 Spark 和 Pyspark 核心在嘗試建立工作階段時將會逾時。</span><span class="sxs-lookup"><span data-stu-id="b7b43-158">When Spark cluster is out of resources, the Spark and Pyspark kernels in the Jupyter notebook will timeout trying to create the session.</span></span> 

<span data-ttu-id="b7b43-159">**緩和措施：**</span><span class="sxs-lookup"><span data-stu-id="b7b43-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="b7b43-160">藉由下列方式，釋出 Spark 叢集中的一些資源：</span><span class="sxs-lookup"><span data-stu-id="b7b43-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="b7b43-161">移至 [關閉並停止] 功能表或按一下 Notebook 總管中的 [關閉]，以停止其他 Spark Notebook。</span><span class="sxs-lookup"><span data-stu-id="b7b43-161">Stopping other Spark notebooks by going to the Close and Halt menu or clicking Shutdown in the notebook explorer.</span></span>
   * <span data-ttu-id="b7b43-162">從 YARN 停止其他 Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7b43-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="b7b43-163">重新啟動您先前嘗試啟動的 Notebook。</span><span class="sxs-lookup"><span data-stu-id="b7b43-163">Restart the notebook you were trying to start up.</span></span> <span data-ttu-id="b7b43-164">此時您應有足夠的資源可建立工作階段。</span><span class="sxs-lookup"><span data-stu-id="b7b43-164">Enough resources should be available for you to create a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="b7b43-165">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b7b43-165">See also</span></span>
* [<span data-ttu-id="b7b43-166">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="b7b43-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="b7b43-167">案例</span><span class="sxs-lookup"><span data-stu-id="b7b43-167">Scenarios</span></span>
* [<span data-ttu-id="b7b43-168">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="b7b43-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="b7b43-169">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="b7b43-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="b7b43-170">Spark 和機器學習服務：使用 HDInsight 中的 Spark 來預測食品檢查結果</span><span class="sxs-lookup"><span data-stu-id="b7b43-170">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="b7b43-171">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="b7b43-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="b7b43-172">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="b7b43-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="b7b43-173">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="b7b43-173">Create and run applications</span></span>
* [<span data-ttu-id="b7b43-174">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="b7b43-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="b7b43-175">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="b7b43-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="b7b43-176">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="b7b43-176">Tools and extensions</span></span>
* [<span data-ttu-id="b7b43-177">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons (使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式來建立和提交 Spark Scala 應用程式)</span><span class="sxs-lookup"><span data-stu-id="b7b43-177">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="b7b43-178">使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式遠端偵錯 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="b7b43-178">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="b7b43-179">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="b7b43-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="b7b43-180">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="b7b43-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="b7b43-181">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="b7b43-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="b7b43-182">在電腦上安裝 Jupyter 並連接到 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="b7b43-182">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="b7b43-183">管理資源</span><span class="sxs-lookup"><span data-stu-id="b7b43-183">Manage resources</span></span>
* [<span data-ttu-id="b7b43-184">在 Azure HDInsight 中管理 Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="b7b43-184">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="b7b43-185">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="b7b43-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

