---
title: "對 Azure HDInsight 上執行的 Apache Spark 作業進行偵錯 | Microsoft Docs"
description: "使用 YARN UI、Spark UI 和 Spark 歷程記錄伺服器，追蹤和偵錯在 Azure HDInsight 中的 Spark 叢集上執行的作業"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: bf66757cc9439a969c9f28abc0b95055ff697c3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a><span data-ttu-id="0a61b-103">對 Azure HDInsight 上執行的 Apache Spark 作業進行偵錯</span><span class="sxs-lookup"><span data-stu-id="0a61b-103">Debug Apache Spark jobs running on Azure HDInsight</span></span>

<span data-ttu-id="0a61b-104">在本文中，您將學習如何使用 YARN UI、Spark UI 和 Spark 歷程記錄伺服器，對 HDInsight 叢集上執行的 Spark 作業進行追蹤和偵錯。</span><span class="sxs-lookup"><span data-stu-id="0a61b-104">In this article you will learn how to track and debug Spark jobs running on HDInsight clusters using the YARN UI, Spark UI, and the Spark History Server.</span></span> <span data-ttu-id="0a61b-105">在本文中，我們會使用 Spark 叢集中可用的 Notebook 啟動 Spark 作業， **機器學習服務︰使用 MLLib 對食物檢查資料進行預測分析**。</span><span class="sxs-lookup"><span data-stu-id="0a61b-105">For this article, we will start a Spark job using a notebook available with the Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span></span> <span data-ttu-id="0a61b-106">您可以使用下列步驟來追蹤您使用任何其他方法提交的應用程式，例如， **spark-submit**。</span><span class="sxs-lookup"><span data-stu-id="0a61b-106">You can use the steps below to track an application that you submitted using any other approach as well, for example, **spark-submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a61b-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="0a61b-107">Prerequisites</span></span>
<span data-ttu-id="0a61b-108">您必須滿足以下條件：</span><span class="sxs-lookup"><span data-stu-id="0a61b-108">You must have the following:</span></span>

* <span data-ttu-id="0a61b-109">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0a61b-109">An Azure subscription.</span></span> <span data-ttu-id="0a61b-110">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="0a61b-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="0a61b-111">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="0a61b-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="0a61b-112">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="0a61b-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="0a61b-113">您應該開始執行 Notebook， **[機器學習服務︰使用 MLLib 對食物檢查資料進行預測分析](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**。</span><span class="sxs-lookup"><span data-stu-id="0a61b-113">You should have started running the notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span></span> <span data-ttu-id="0a61b-114">如需有關如何執行此 Notebook 的指示，請依照下列連結。</span><span class="sxs-lookup"><span data-stu-id="0a61b-114">For instructions on how to run this notebook, follow the link.</span></span>  

## <a name="track-an-application-in-the-yarn-ui"></a><span data-ttu-id="0a61b-115">追蹤 YARN UI 中的應用程式</span><span class="sxs-lookup"><span data-stu-id="0a61b-115">Track an application in the YARN UI</span></span>
1. <span data-ttu-id="0a61b-116">啟動 YARN UI。</span><span class="sxs-lookup"><span data-stu-id="0a61b-116">Launch the YARN UI.</span></span> <span data-ttu-id="0a61b-117">從叢集刀鋒視窗按一下 [叢集儀表板]，然後按一下 [YARN]。</span><span class="sxs-lookup"><span data-stu-id="0a61b-117">From the cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>
   
    ![啟動 YARN UI](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > <span data-ttu-id="0a61b-119">或者，您也可以從 Ambari UI 啟動 YARN UI。</span><span class="sxs-lookup"><span data-stu-id="0a61b-119">Alternatively, you can also launch the YARN UI from the Ambari UI.</span></span> <span data-ttu-id="0a61b-120">若要啟動 Ambari UI，請從叢集刀鋒視窗中按一下 [叢集儀表板]，然後按一下 [HDInsight 叢集儀表板]。</span><span class="sxs-lookup"><span data-stu-id="0a61b-120">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="0a61b-121">從 Ambari UI 中，依序按一下 [YARN]、[快速連結]、作用中的資源管理員，以及 [ResourceManager UI]。</span><span class="sxs-lookup"><span data-stu-id="0a61b-121">From the Ambari UI, click **YARN**, click **Quick Links**, click the active resource manager, and then click **ResourceManager UI**.</span></span>    
   > 
   > 
2. <span data-ttu-id="0a61b-122">因為您使用 Jupyter Notebook 啟動 Spark 作業，應用程式具有名稱 **remotesparkmagics** (這是從 Notebook 啟動之所有應用程式的名稱)。</span><span class="sxs-lookup"><span data-stu-id="0a61b-122">Because you started the Spark job using Jupyter notebooks, the application has the name **remotesparkmagics** (this is the name for all applications that are started from the notebooks).</span></span> <span data-ttu-id="0a61b-123">針對應用程式名稱按一下應用程式識別碼，取得作業的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0a61b-123">Click the application ID against the application name to get more information about the job.</span></span> <span data-ttu-id="0a61b-124">這會啟動應用程式檢視。</span><span class="sxs-lookup"><span data-stu-id="0a61b-124">This launches the application view.</span></span>
   
    ![尋找 Spark 應用程式識別碼](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    <span data-ttu-id="0a61b-126">對於從 Jupyter Notebook 啟動的應用程式，狀態一律是 [執行中]  ，直到您結束 Notebook。</span><span class="sxs-lookup"><span data-stu-id="0a61b-126">For such applications that are launched from the Jupyter notebooks, the status is always **RUNNING** until you exit the notebook.</span></span>
3. <span data-ttu-id="0a61b-127">從應用程式檢視中，您可以進一步向下鑽研以找出與應用程式和記錄檔 (stdout/stderr) 相關聯的容器。</span><span class="sxs-lookup"><span data-stu-id="0a61b-127">From the application view, you can drill down further to find out the containers associated with the application and the logs (stdout/stderr).</span></span> <span data-ttu-id="0a61b-128">您也可以藉由按一下對應至 [追蹤 URL] 的連結，即可啟動 Spark UI，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0a61b-128">You can also launch the Spark UI by clicking the linking corresponding to the **Tracking URL**, as shown below.</span></span> 
   
    ![下載容器記錄檔](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-the-spark-ui"></a><span data-ttu-id="0a61b-130">追蹤 Spark UI 中的應用程式</span><span class="sxs-lookup"><span data-stu-id="0a61b-130">Track an application in the Spark UI</span></span>
<span data-ttu-id="0a61b-131">在 Spark UI 中，您可以向下鑽研至您先前啟動的應用程式所繁衍的 Spark 作業。</span><span class="sxs-lookup"><span data-stu-id="0a61b-131">In the Spark UI, you can drill down into the Spark jobs that are spawned by the application you started earlier.</span></span>

1. <span data-ttu-id="0a61b-132">若要啟動 Spark UI，請從應用程式檢視中，針對 [追蹤 URL] 按一下連結，如上面的螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="0a61b-132">To launch the Spark UI, from the application view, click the link against the **Tracking URL**, as shown in the screen capture above.</span></span> <span data-ttu-id="0a61b-133">您可以看到應用程式啟動的所有 Spark 作業在 Jupyter Notebook 中執行。</span><span class="sxs-lookup"><span data-stu-id="0a61b-133">You can see all the Spark jobs that are launched by the application running in the Jupyter notebook.</span></span>
   
    ![檢視 Spark 作業](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. <span data-ttu-id="0a61b-135">按一下 [執行程式]  索引標籤，查看每個執行程式的處理和儲存資訊。</span><span class="sxs-lookup"><span data-stu-id="0a61b-135">Click the **Executors** tab to see processing and storage information for each executor.</span></span> <span data-ttu-id="0a61b-136">您也可以按一下 [執行緒傾印]  連結，擷取呼叫堆疊。</span><span class="sxs-lookup"><span data-stu-id="0a61b-136">You can also retrieve the call stack by clicking on the **Thread Dump** link.</span></span>
   
    ![檢視 Spark 執行程式](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. <span data-ttu-id="0a61b-138">按一下 [階段]  索引標籤，查看與應用程式相關聯的階段。</span><span class="sxs-lookup"><span data-stu-id="0a61b-138">Click the **Stages** tab to see the stages associated with the application.</span></span>
   
    ![檢視 Spark 階段](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    <span data-ttu-id="0a61b-140">每個階段可以有多個工作，您可以檢視其執行統計資料，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0a61b-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span></span>
   
    ![檢視 Spark 階段](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. <span data-ttu-id="0a61b-142">從階段詳細資料頁面上，您可以啟動 DAG 視覺效果。</span><span class="sxs-lookup"><span data-stu-id="0a61b-142">From the stage details page, you can launch DAG Visualization.</span></span> <span data-ttu-id="0a61b-143">展開頁面頂端的 [DAG 視覺效果]  連結，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0a61b-143">Expand the **DAG Visualization** link at the top of the page, as shown below.</span></span>
   
    ![檢視 Spark 階段 DAG 視覺效果](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    <span data-ttu-id="0a61b-145">DAG 或 Direct Aclyic Graph 代表應用程式中的不同階段。</span><span class="sxs-lookup"><span data-stu-id="0a61b-145">DAG or Direct Aclyic Graph represents the different stages in the application.</span></span> <span data-ttu-id="0a61b-146">每個圖形中的藍色方塊表示從應用程式叫用的 Spark 作業。</span><span class="sxs-lookup"><span data-stu-id="0a61b-146">Each blue box in the graph represents a Spark operation invoked from the application.</span></span>
5. <span data-ttu-id="0a61b-147">您也可以從階段詳細資料頁面上，啟動應用程式時間軸檢視。</span><span class="sxs-lookup"><span data-stu-id="0a61b-147">From the stage details page, you can also launch the application timeline view.</span></span> <span data-ttu-id="0a61b-148">展開頁面頂端的 [事件時間軸]  連結，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0a61b-148">Expand the **Event Timeline** link at the top of the page, as shown below.</span></span>
   
    ![檢視 Spark 階段事件時間軸](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    <span data-ttu-id="0a61b-150">這會以時間軸的形式顯示 Spark 事件。</span><span class="sxs-lookup"><span data-stu-id="0a61b-150">This displays the Spark events in the form of a timeline.</span></span> <span data-ttu-id="0a61b-151">時間軸檢視有三個層級，跨作業、作業內以及階段內。</span><span class="sxs-lookup"><span data-stu-id="0a61b-151">The timeline view is available at three levels, across jobs, within a job, and within a stage.</span></span> <span data-ttu-id="0a61b-152">以上的映像擷取指定階段的時間軸檢視。</span><span class="sxs-lookup"><span data-stu-id="0a61b-152">The image above captures the timeline view for a given stage.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="0a61b-153">如果您選取 [啟用縮放功能] 核取方塊，您可以跨時間軸檢視左右捲動。</span><span class="sxs-lookup"><span data-stu-id="0a61b-153">If you select the **Enable zooming** check box, you can scroll left and right across the timeline view.</span></span>
   > 
   > 
6. <span data-ttu-id="0a61b-154">Spark UI 中的其他索引標籤也提供 Spark 執行個體的實用資訊。</span><span class="sxs-lookup"><span data-stu-id="0a61b-154">Other tabs in the Spark UI provide useful information about the Spark instance as well.</span></span>
   
   * <span data-ttu-id="0a61b-155">[儲存體] 索引標籤 - 如果您的應用程式建立 RDD，您可以在 [儲存體] 索引標籤中找到相關資訊。</span><span class="sxs-lookup"><span data-stu-id="0a61b-155">Storage tab - If your application creates an RDDs, you can find information about those in the Storage tab.</span></span>
   * <span data-ttu-id="0a61b-156">[環境]索引標籤 - 這個標籤提供關於您的 Spark 執行個體的實用資訊，例如</span><span class="sxs-lookup"><span data-stu-id="0a61b-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as the</span></span> 
     * <span data-ttu-id="0a61b-157">Scala 版本</span><span class="sxs-lookup"><span data-stu-id="0a61b-157">Scala version</span></span>
     * <span data-ttu-id="0a61b-158">與叢集相關聯的事件記錄檔目錄</span><span class="sxs-lookup"><span data-stu-id="0a61b-158">Event log directory associated with the cluster</span></span>
     * <span data-ttu-id="0a61b-159">應用程式的執行程式核心數目</span><span class="sxs-lookup"><span data-stu-id="0a61b-159">Number of executor cores for the application</span></span>
     * <span data-ttu-id="0a61b-160">等等</span><span class="sxs-lookup"><span data-stu-id="0a61b-160">Etc.</span></span>

## <a name="find-information-about-completed-jobs-using-the-spark-history-server"></a><span data-ttu-id="0a61b-161">使用 Spark 歷程記錄伺服器尋找已完成作業的相關資訊</span><span class="sxs-lookup"><span data-stu-id="0a61b-161">Find information about completed jobs using the Spark History Server</span></span>
<span data-ttu-id="0a61b-162">完成作業後，作業的相關資訊會保存在 Spark 歷程記錄伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a61b-162">Once a job is completed, the information about the job is persisted in the Spark History Server.</span></span>

1. <span data-ttu-id="0a61b-163">若要啟動 Spark 歷程記錄伺服器，請從叢集刀鋒視窗中按一下 [叢集儀表板]，然後按一下 [Spark 歷程記錄伺服器]。</span><span class="sxs-lookup"><span data-stu-id="0a61b-163">To launch the Spark History Server, from the cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span>
   
    ![啟動 Spark 歷程記錄伺服器](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > <span data-ttu-id="0a61b-165">或者，您也可以從 Ambari UI 啟動 Spark 歷程記錄伺服器 UI。</span><span class="sxs-lookup"><span data-stu-id="0a61b-165">Alternatively, you can also launch the Spark History Server UI from the Ambari UI.</span></span> <span data-ttu-id="0a61b-166">若要啟動 Ambari UI，請從叢集刀鋒視窗中按一下 [叢集儀表板]，然後按一下 [HDInsight 叢集儀表板]。</span><span class="sxs-lookup"><span data-stu-id="0a61b-166">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="0a61b-167">從 Ambari UI 中，依序按一下 [Spark]、[快速連結]和 [Spark 歷程記錄伺服器 UI]。</span><span class="sxs-lookup"><span data-stu-id="0a61b-167">From the Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span></span>
   > 
   > 
2. <span data-ttu-id="0a61b-168">您會看到列出所有已完成應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a61b-168">You will see all the completed applications listed.</span></span> <span data-ttu-id="0a61b-169">按一下應用程式識別碼，向下鑽研至應用程式以取得其他資訊。</span><span class="sxs-lookup"><span data-stu-id="0a61b-169">Click an application ID to drill down into an application for more info.</span></span>
   
    ![啟動 Spark 歷程記錄伺服器](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a><span data-ttu-id="0a61b-171">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0a61b-171">See also</span></span>
*  [<span data-ttu-id="0a61b-172">在 Azure HDInsight 中管理 Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="0a61b-172">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a><span data-ttu-id="0a61b-173">針對資料分析師</span><span class="sxs-lookup"><span data-stu-id="0a61b-173">For data analysts</span></span>

* [<span data-ttu-id="0a61b-174">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="0a61b-174">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="0a61b-175">Spark 和機器學習服務：使用 HDInsight 中的 Spark 來預測食品檢查結果</span><span class="sxs-lookup"><span data-stu-id="0a61b-175">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="0a61b-176">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="0a61b-176">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="0a61b-177">HDInsight 中使用 Spark 的 Application Insight 遙測資料分析</span><span class="sxs-lookup"><span data-stu-id="0a61b-177">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="0a61b-178">在 Azure HDInsight Spark 上使用 Caffe 進行分散式深入學習</span><span class="sxs-lookup"><span data-stu-id="0a61b-178">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a><span data-ttu-id="0a61b-179">針對 Spark 開發人員</span><span class="sxs-lookup"><span data-stu-id="0a61b-179">For Spark developers</span></span>

* [<span data-ttu-id="0a61b-180">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="0a61b-180">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="0a61b-181">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="0a61b-181">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="0a61b-182">使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式來建立和提交 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="0a61b-182">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="0a61b-183">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="0a61b-183">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="0a61b-184">使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式遠端偵錯 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="0a61b-184">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="0a61b-185">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="0a61b-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="0a61b-186">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="0a61b-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="0a61b-187">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="0a61b-187">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="0a61b-188">在電腦上安裝 Jupyter 並連接到 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="0a61b-188">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


