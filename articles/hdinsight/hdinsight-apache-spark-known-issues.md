---
title: "在 Azure HDInsight 叢集使用 Apache Spark aaaTroubleshoot 問題 |Microsoft 文件"
description: "了解問題相關的 tooApache Azure HDInsight Spark 叢集以及如何解決那些 toowork。"
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
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="7d3e7-103">HDInsight 上的 Apache Spark 叢集已知問題</span><span class="sxs-lookup"><span data-stu-id="7d3e7-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="7d3e7-104">這份文件會持續追蹤的所有 hello hello HDInsight Spark 公用預覽的已知問題。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-104">This document keeps track of all hello known issues for hello HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="7d3e7-105">Livy 會流失互動式工作階段</span><span class="sxs-lookup"><span data-stu-id="7d3e7-105">Livy leaks interactive session</span></span>
<span data-ttu-id="7d3e7-106">晚總重新啟動時 （從 Ambari 或因為 tooheadnode 0 虛擬機器重新開機） 與仍在執行的互動式工作階段，互動式工作階段會外洩。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-106">When Livy is restarted (from Ambari or due tooheadnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="7d3e7-107">因為這個緣故，新的工作可以陷入 hello 已接受狀態，因此無法啟動。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-107">Because of this, new jobs can stuck in hello Accepted state, and cannot be started.</span></span>

<span data-ttu-id="7d3e7-108">**緩和：**</span><span class="sxs-lookup"><span data-stu-id="7d3e7-108">**Mitigation:**</span></span>

<span data-ttu-id="7d3e7-109">使用下列程序 tooworkaround hello 問題 hello:</span><span class="sxs-lookup"><span data-stu-id="7d3e7-109">Use hello following procedure tooworkaround hello issue:</span></span>

1. <span data-ttu-id="7d3e7-110">Ssh 到前端節點。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-110">Ssh into headnode.</span></span> <span data-ttu-id="7d3e7-111">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="7d3e7-112">執行下列命令 toofind hello 應用程式的 hello 透過晚總啟動 hello 互動式工作的識別碼。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-112">Run hello following command toofind hello application IDs of hello interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="7d3e7-113">hello 預設作業名稱會晚總 hello 工作已有名為沒有明確指定，如 hello 時入門晚總互動式工作階段啟動 Jupyter 筆記本晚總工作階段，hello 工作名稱的開頭將 remotesparkmagics_ *。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-113">hello default job names will be Livy if hello jobs were started with a Livy interactive session with no explicit names specified, For hello Livy session started by Jupyter notebook, hello job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="7d3e7-114">執行下列命令 tookill hello 這些作業。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-114">Run hello following command tookill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="7d3e7-115">新作業將會開始執行。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="7d3e7-116">Spark 歷程記錄伺服器未啟動</span><span class="sxs-lookup"><span data-stu-id="7d3e7-116">Spark History Server not started</span></span>
<span data-ttu-id="7d3e7-117">叢集建立後，不會自動啟動 Spark 歷程記錄伺服器。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="7d3e7-118">**緩和：**</span><span class="sxs-lookup"><span data-stu-id="7d3e7-118">**Mitigation:**</span></span> 

<span data-ttu-id="7d3e7-119">手動從 Ambari 啟動 hello 歷程記錄的伺服器。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-119">Manually start hello history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="7d3e7-120">Spark 記錄檔目錄中的權限問題</span><span class="sxs-lookup"><span data-stu-id="7d3e7-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="7d3e7-121">當 hdiuser 提交 spark-submit 與作業時，就會發生錯誤 java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log （拒絕的權限） 和 hello 驅動程式記錄檔不會寫入。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and hello driver log is not written.</span></span> 

<span data-ttu-id="7d3e7-122">**緩和：**</span><span class="sxs-lookup"><span data-stu-id="7d3e7-122">**Mitigation:**</span></span>

1. <span data-ttu-id="7d3e7-123">新增 hdiuser toohello Hadoop 群組。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-123">Add hdiuser toohello Hadoop group.</span></span> 
2. <span data-ttu-id="7d3e7-124">在叢集建立之後，提供 /var/log/spark 的 777 權限。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="7d3e7-125">更新使用 Ambari toobe 目錄 777 權限與 hello spark 記錄檔位置。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-125">Update hello spark log location using Ambari toobe a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="7d3e7-126">以 sudo 的身分執行 spark-submit。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="7d3e7-127">不支援 Spark-Phoenix 連接器</span><span class="sxs-lookup"><span data-stu-id="7d3e7-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="7d3e7-128">目前，hello Spark in Phoenix 連接器不支援與 HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-128">Currently, hello Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="7d3e7-129">**緩和：**</span><span class="sxs-lookup"><span data-stu-id="7d3e7-129">**Mitigation:**</span></span>

<span data-ttu-id="7d3e7-130">您必須改用 hello Spark HBase 連接器。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-130">You must use hello Spark-HBase connector instead.</span></span> <span data-ttu-id="7d3e7-131">如需指示，請參閱[如何 toouse Spark HBase 連接器](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/)。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-131">For instructions see [How toouse Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-toojupyter-notebooks"></a><span data-ttu-id="7d3e7-132">與 tooJupyter 筆記本相關的問題</span><span class="sxs-lookup"><span data-stu-id="7d3e7-132">Issues related tooJupyter notebooks</span></span>
<span data-ttu-id="7d3e7-133">以下是一些已知的問題相關的 tooJupyter 筆記型電腦。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-133">Following are some known issues related tooJupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="7d3e7-134">Notebook 在檔名中有非 ASCII 字元</span><span class="sxs-lookup"><span data-stu-id="7d3e7-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="7d3e7-135">可以用在 Spark HDInsight 叢集中的 Jupyter Notebook，檔名中不該有非 ASCII 字元。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="7d3e7-136">如果您嘗試 tooupload 透過 hello Jupyter UI 的非 ASCII 檔案名稱的檔案時，會以無訊息模式失敗 （也就是 Jupyter 不會讓您上傳 hello 檔案，但它可能不會擲回看見的錯誤）。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-136">If you try tooupload a file through hello Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload hello file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="7d3e7-137">載入大型 Notebook 時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="7d3e7-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="7d3e7-138">載入大型 Notebook 時，您可能會看到錯誤訊息 **`Error loading notebook`** 。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="7d3e7-139">**緩和：**</span><span class="sxs-lookup"><span data-stu-id="7d3e7-139">**Mitigation:**</span></span>

<span data-ttu-id="7d3e7-140">如果您收到這個錯誤，並不表示您的資料已損毀或遺失。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="7d3e7-141">您的筆記型電腦有仍在磁碟中`/var/lib/jupyter`，您可以 SSH hello 叢集 tooaccess 到它們。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into hello cluster tooaccess them.</span></span> <span data-ttu-id="7d3e7-142">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="7d3e7-143">一旦您已經連接使用 SSH toohello 叢集，您可以從叢集 tooyour 本機電腦 （使用 SCP 或 WinSCP） 複製您筆記本當做備份 tooprevent hello 遺失的 hello 筆記本中的任何重要資料。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-143">Once you have connected toohello cluster using SSH, you can copy your notebooks from your cluster tooyour local machine (using SCP or WinSCP) as a backup tooprevent hello loss of any important data in hello notebook.</span></span> <span data-ttu-id="7d3e7-144">您接著可以 SSH 通道至您的叢集前端節點，在連接埠 8001 tooaccess Jupyter 而不需要透過 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-144">You can then SSH tunnel into your headnode at port 8001 tooaccess Jupyter without going through hello gateway.</span></span>  <span data-ttu-id="7d3e7-145">從該處，您可以清除筆記本的 hello 輸出，並重新儲存 toominimize hello 筆記本的大小。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-145">From there, you can clear hello output of your notebook and re-save it toominimize hello notebook’s size.</span></span>

<span data-ttu-id="7d3e7-146">tooprevent hello 未來，您必須遵循的一些最佳做法中發生此錯誤：</span><span class="sxs-lookup"><span data-stu-id="7d3e7-146">tooprevent this error from happening in hello future, you must follow some best practices:</span></span>

* <span data-ttu-id="7d3e7-147">它是小型的重要 tookeep hello 筆記型電腦大小。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-147">It is important tookeep hello notebook size small.</span></span> <span data-ttu-id="7d3e7-148">任何輸出會傳送回 tooJupyter 會持續保留在 hello 筆記本從 Spark 作業。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-148">Any output from your Spark jobs that is sent back tooJupyter is persisted in hello notebook.</span></span>  <span data-ttu-id="7d3e7-149">與 Jupyter 最佳作法是在執行的一般 tooavoid`.collect()`在大型 RDD 的或資料框架; 相反地，如果您想在 RDD 內容 toopeek，請考慮執行`.take()`或`.sample()`使您的輸出不會太大。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-149">It is a best practice with Jupyter in general tooavoid running `.collect()` on large RDD’s or dataframes; instead, if you want toopeek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="7d3e7-150">此外，當您儲存筆記本，清除所有輸出資料格 tooreduce hello 大小。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-150">Also, when you save a notebook, clear all output cells tooreduce hello size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="7d3e7-151">Notebook 的初始啟動比預期耗時</span><span class="sxs-lookup"><span data-stu-id="7d3e7-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="7d3e7-152">在使用 Spark magic 的 Jupyter Notebook 中，第一個程式碼陳述式可能需耗時一分鐘以上才能執行完畢。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="7d3e7-153">**說明：**</span><span class="sxs-lookup"><span data-stu-id="7d3e7-153">**Explanation:**</span></span>

<span data-ttu-id="7d3e7-154">這是因為執行 hello 第一個程式碼儲存格時。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-154">This happens because when hello first code cell is run.</span></span> <span data-ttu-id="7d3e7-155">在 hello 背景這會起始工作階段設定和 Spark、 SQL、 和 Hive 內容設定。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-155">In hello background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="7d3e7-156">設定這些內容之後，hello 第一個陳述式執行時，這可讓 hello 陳述式所花費很長的時間 toocomplete hello 印象。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-156">After these contexts are set, hello first statement is run and this gives hello impression that hello statement took a long time toocomplete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a><span data-ttu-id="7d3e7-157">在建立 hello 工作階段的 Jupyter 筆記本逾時</span><span class="sxs-lookup"><span data-stu-id="7d3e7-157">Jupyter notebook timeout in creating hello session</span></span>
<span data-ttu-id="7d3e7-158">用完資源 Spark 叢集時，hello Spark 和 Pyspark 核心 hello Jupyter 筆記本中的，將會嘗試 toocreate hello 工作階段逾時。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-158">When Spark cluster is out of resources, hello Spark and Pyspark kernels in hello Jupyter notebook will timeout trying toocreate hello session.</span></span> 

<span data-ttu-id="7d3e7-159">**緩和措施：**</span><span class="sxs-lookup"><span data-stu-id="7d3e7-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="7d3e7-160">藉由下列方式，釋出 Spark 叢集中的一些資源：</span><span class="sxs-lookup"><span data-stu-id="7d3e7-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="7d3e7-161">停止其他移 toohello 關閉和 Halt 功能表或按一下 [關閉 hello 筆記本總管] 中的 Spark 筆記型電腦。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-161">Stopping other Spark notebooks by going toohello Close and Halt menu or clicking Shutdown in hello notebook explorer.</span></span>
   * <span data-ttu-id="7d3e7-162">從 YARN 停止其他 Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="7d3e7-163">重新啟動您嘗試 toostart 向上 hello 筆記型電腦。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-163">Restart hello notebook you were trying toostart up.</span></span> <span data-ttu-id="7d3e7-164">足夠的資源可供您 toocreate 立即的工作階段。</span><span class="sxs-lookup"><span data-stu-id="7d3e7-164">Enough resources should be available for you toocreate a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="7d3e7-165">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7d3e7-165">See also</span></span>
* [<span data-ttu-id="7d3e7-166">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="7d3e7-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="7d3e7-167">案例</span><span class="sxs-lookup"><span data-stu-id="7d3e7-167">Scenarios</span></span>
* [<span data-ttu-id="7d3e7-168">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="7d3e7-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="7d3e7-169">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="7d3e7-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="7d3e7-170">機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark</span><span class="sxs-lookup"><span data-stu-id="7d3e7-170">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="7d3e7-171">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="7d3e7-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="7d3e7-172">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="7d3e7-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="7d3e7-173">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="7d3e7-173">Create and run applications</span></span>
* [<span data-ttu-id="7d3e7-174">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="7d3e7-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="7d3e7-175">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="7d3e7-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="7d3e7-176">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="7d3e7-176">Tools and extensions</span></span>
* [<span data-ttu-id="7d3e7-177">HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 個應用程式</span><span class="sxs-lookup"><span data-stu-id="7d3e7-177">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="7d3e7-178">從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="7d3e7-178">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="7d3e7-179">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="7d3e7-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="7d3e7-180">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="7d3e7-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="7d3e7-181">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="7d3e7-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="7d3e7-182">在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="7d3e7-182">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="7d3e7-183">管理資源</span><span class="sxs-lookup"><span data-stu-id="7d3e7-183">Manage resources</span></span>
* [<span data-ttu-id="7d3e7-184">管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="7d3e7-184">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="7d3e7-185">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="7d3e7-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

