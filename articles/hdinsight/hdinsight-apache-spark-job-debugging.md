---
title: "Azure HDInsight 上執行作業的 aaaDebug Apache Spark |Microsoft 文件"
description: "使用 YARN UI、 Spark UI 和 Spark 記錄伺服器 tootrack 和偵錯工作在 Azure HDInsight Spark 叢集上執行"
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
ms.openlocfilehash: 33d352a5773920735aa4e5e8532b78122f381377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a><span data-ttu-id="678cb-103">對 Azure HDInsight 上執行的 Apache Spark 作業進行偵錯</span><span class="sxs-lookup"><span data-stu-id="678cb-103">Debug Apache Spark jobs running on Azure HDInsight</span></span>

<span data-ttu-id="678cb-104">在本文中，您將學習如何 tootrack 和偵錯二手使用 hello YARN UI Spark UI 的 HDInsight 叢集上執行的作業以及 hello Spark 歷程記錄的伺服器。</span><span class="sxs-lookup"><span data-stu-id="678cb-104">In this article you will learn how tootrack and debug Spark jobs running on HDInsight clusters using hello YARN UI, Spark UI, and hello Spark History Server.</span></span> <span data-ttu-id="678cb-105">這個發行項，我們將會啟動 Spark 工作 hello Spark 叢集後，使用可用的筆記本**機器學習： 針對使用 MLLib 食物檢查資料的預測分析**。</span><span class="sxs-lookup"><span data-stu-id="678cb-105">For this article, we will start a Spark job using a notebook available with hello Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span></span> <span data-ttu-id="678cb-106">您可以使用下列 tootrack 您送出使用任何其他方法，例如，應用程式的 hello 步驟**spark-submit 對**。</span><span class="sxs-lookup"><span data-stu-id="678cb-106">You can use hello steps below tootrack an application that you submitted using any other approach as well, for example, **spark-submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="678cb-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="678cb-107">Prerequisites</span></span>
<span data-ttu-id="678cb-108">您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="678cb-108">You must have hello following:</span></span>

* <span data-ttu-id="678cb-109">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="678cb-109">An Azure subscription.</span></span> <span data-ttu-id="678cb-110">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="678cb-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="678cb-111">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="678cb-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="678cb-112">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="678cb-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="678cb-113">您應該開始執行 hello 筆記本**[機器學習： 針對使用 MLLib 食物檢查資料的預測分析](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**。</span><span class="sxs-lookup"><span data-stu-id="678cb-113">You should have started running hello notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span></span> <span data-ttu-id="678cb-114">如需有關指示 toorun 筆記本，後續 hello 連結。</span><span class="sxs-lookup"><span data-stu-id="678cb-114">For instructions on how toorun this notebook, follow hello link.</span></span>  

## <a name="track-an-application-in-hello-yarn-ui"></a><span data-ttu-id="678cb-115">追蹤 hello YARN UI 中的應用程式</span><span class="sxs-lookup"><span data-stu-id="678cb-115">Track an application in hello YARN UI</span></span>
1. <span data-ttu-id="678cb-116">啟動 hello YARN UI。</span><span class="sxs-lookup"><span data-stu-id="678cb-116">Launch hello YARN UI.</span></span> <span data-ttu-id="678cb-117">從 hello 叢集刀鋒視窗中，按一下 **叢集儀表板**，然後按一下 **YARN**。</span><span class="sxs-lookup"><span data-stu-id="678cb-117">From hello cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>
   
    ![啟動 YARN UI](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > <span data-ttu-id="678cb-119">或者，您也可以啟動 hello YARN UI 從 hello Ambari UI。</span><span class="sxs-lookup"><span data-stu-id="678cb-119">Alternatively, you can also launch hello YARN UI from hello Ambari UI.</span></span> <span data-ttu-id="678cb-120">按一下 toolaunch hello Ambari UI hello 叢集刀鋒視窗中，從**叢集儀表板**，然後按一下 **HDInsight 叢集儀表板**。</span><span class="sxs-lookup"><span data-stu-id="678cb-120">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="678cb-121">從 hello Ambari UI 中，按一下  **YARN**，按一下 **快速連結**hello 作用中的資源管理員，然後按**ResourceManager UI**。</span><span class="sxs-lookup"><span data-stu-id="678cb-121">From hello Ambari UI, click **YARN**, click **Quick Links**, click hello active resource manager, and then click **ResourceManager UI**.</span></span>    
   > 
   > 
2. <span data-ttu-id="678cb-122">Hello 應用程式，您一開始使用 Jupyter 筆記本 hello Spark 作業，因為已 hello 名稱**remotesparkmagics** （這是 hello hello 筆記本從啟動的所有應用程式的名稱）。</span><span class="sxs-lookup"><span data-stu-id="678cb-122">Because you started hello Spark job using Jupyter notebooks, hello application has hello name **remotesparkmagics** (this is hello name for all applications that are started from hello notebooks).</span></span> <span data-ttu-id="678cb-123">按一下 針對 hello 應用程式名稱 tooget hello 應用程式識別碼 hello 工作的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="678cb-123">Click hello application ID against hello application name tooget more information about hello job.</span></span> <span data-ttu-id="678cb-124">這會啟動 hello 應用程式檢視。</span><span class="sxs-lookup"><span data-stu-id="678cb-124">This launches hello application view.</span></span>
   
    ![尋找 Spark 應用程式識別碼](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    <span data-ttu-id="678cb-126">從 hello Jupyter 筆記本啟動這類應用程式，對於 hello 狀態一律是**執行**等到您結束 hello 筆記型電腦。</span><span class="sxs-lookup"><span data-stu-id="678cb-126">For such applications that are launched from hello Jupyter notebooks, hello status is always **RUNNING** until you exit hello notebook.</span></span>
3. <span data-ttu-id="678cb-127">從 hello 應用程式檢視中，您可以向下鑽研進一步 toofind 出 hello 與 hello 應用程式和 hello 記錄檔 (stdout/stderr) 相關聯的容器。</span><span class="sxs-lookup"><span data-stu-id="678cb-127">From hello application view, you can drill down further toofind out hello containers associated with hello application and hello logs (stdout/stderr).</span></span> <span data-ttu-id="678cb-128">您也可以按一下連結對應 toohello hello 啟動 hello Spark UI**追蹤 URL**，如下所示。</span><span class="sxs-lookup"><span data-stu-id="678cb-128">You can also launch hello Spark UI by clicking hello linking corresponding toohello **Tracking URL**, as shown below.</span></span> 
   
    ![下載容器記錄檔](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-hello-spark-ui"></a><span data-ttu-id="678cb-130">追蹤 hello Spark UI 中的應用程式</span><span class="sxs-lookup"><span data-stu-id="678cb-130">Track an application in hello Spark UI</span></span>
<span data-ttu-id="678cb-131">在 hello Spark UI，您可以向下鑽研由您先前已啟動的 hello 應用程式產生的 hello Spark 作業。</span><span class="sxs-lookup"><span data-stu-id="678cb-131">In hello Spark UI, you can drill down into hello Spark jobs that are spawned by hello application you started earlier.</span></span>

1. <span data-ttu-id="678cb-132">toolaunch hello Spark UI hello 應用程式檢視中，按一下 針對 hello hello 連結**追蹤 URL**hello 螢幕擷取畫面上方所示。</span><span class="sxs-lookup"><span data-stu-id="678cb-132">toolaunch hello Spark UI, from hello application view, click hello link against hello **Tracking URL**, as shown in hello screen capture above.</span></span> <span data-ttu-id="678cb-133">您可以查看所有 hello hello Jupyter 筆記本中執行的應用程式所啟動的 hello Spark 工作。</span><span class="sxs-lookup"><span data-stu-id="678cb-133">You can see all hello Spark jobs that are launched by hello application running in hello Jupyter notebook.</span></span>
   
    ![檢視 Spark 作業](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. <span data-ttu-id="678cb-135">按一下 hello**執行程式**索引標籤上的每一個執行程式的 toosee 處理和儲存體資訊。</span><span class="sxs-lookup"><span data-stu-id="678cb-135">Click hello **Executors** tab toosee processing and storage information for each executor.</span></span> <span data-ttu-id="678cb-136">您也可以擷取 hello 呼叫堆疊上 hello 即可**執行緒傾印**連結。</span><span class="sxs-lookup"><span data-stu-id="678cb-136">You can also retrieve hello call stack by clicking on hello **Thread Dump** link.</span></span>
   
    ![檢視 Spark 執行程式](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. <span data-ttu-id="678cb-138">按一下 hello**階段**hello 應用程式相關聯的 toosee hello 階段索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="678cb-138">Click hello **Stages** tab toosee hello stages associated with hello application.</span></span>
   
    ![檢視 Spark 階段](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    <span data-ttu-id="678cb-140">每個階段可以有多個工作，您可以檢視其執行統計資料，如下所示。</span><span class="sxs-lookup"><span data-stu-id="678cb-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span></span>
   
    ![檢視 Spark 階段](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. <span data-ttu-id="678cb-142">Hello 階段詳細資料頁面中，您可以啟動 DAG 視覺效果。</span><span class="sxs-lookup"><span data-stu-id="678cb-142">From hello stage details page, you can launch DAG Visualization.</span></span> <span data-ttu-id="678cb-143">展開 hello **DAG 視覺效果**連結 hello 頁面頂端的 hello，如下所示。</span><span class="sxs-lookup"><span data-stu-id="678cb-143">Expand hello **DAG Visualization** link at hello top of hello page, as shown below.</span></span>
   
    ![檢視 Spark 階段 DAG 視覺效果](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    <span data-ttu-id="678cb-145">DAG 或直接 Aclyic 圖形代表 hello hello 應用程式中的不同階段。</span><span class="sxs-lookup"><span data-stu-id="678cb-145">DAG or Direct Aclyic Graph represents hello different stages in hello application.</span></span> <span data-ttu-id="678cb-146">Hello 圖形中每一個藍色方塊表示從 hello 應用程式叫用的 Spark 作業。</span><span class="sxs-lookup"><span data-stu-id="678cb-146">Each blue box in hello graph represents a Spark operation invoked from hello application.</span></span>
5. <span data-ttu-id="678cb-147">Hello 階段詳細資料頁面中，您也可以啟動 hello 應用程式時間軸檢視。</span><span class="sxs-lookup"><span data-stu-id="678cb-147">From hello stage details page, you can also launch hello application timeline view.</span></span> <span data-ttu-id="678cb-148">展開 hello**事件時間軸**連結 hello 頁面頂端的 hello，如下所示。</span><span class="sxs-lookup"><span data-stu-id="678cb-148">Expand hello **Event Timeline** link at hello top of hello page, as shown below.</span></span>
   
    ![檢視 Spark 階段事件時間軸](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    <span data-ttu-id="678cb-150">這在 hello 以時刻表的形式顯示 hello Spark 事件。</span><span class="sxs-lookup"><span data-stu-id="678cb-150">This displays hello Spark events in hello form of a timeline.</span></span> <span data-ttu-id="678cb-151">hello 時間表檢視可在三個層級，在工作階段內和作業範圍內。</span><span class="sxs-lookup"><span data-stu-id="678cb-151">hello timeline view is available at three levels, across jobs, within a job, and within a stage.</span></span> <span data-ttu-id="678cb-152">上述的 hello 映像擷取特定階段 hello 時間表檢視。</span><span class="sxs-lookup"><span data-stu-id="678cb-152">hello image above captures hello timeline view for a given stage.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="678cb-153">如果您選取 hello**啟用縮放**核取方塊，您可以左右橫向捲動 hello 時間表檢視。</span><span class="sxs-lookup"><span data-stu-id="678cb-153">If you select hello **Enable zooming** check box, you can scroll left and right across hello timeline view.</span></span>
   > 
   > 
6. <span data-ttu-id="678cb-154">Hello Spark UI 中的其他索引標籤會提供實用資訊以及 hello Spark 執行個體。</span><span class="sxs-lookup"><span data-stu-id="678cb-154">Other tabs in hello Spark UI provide useful information about hello Spark instance as well.</span></span>
   
   * <span data-ttu-id="678cb-155">儲存體索引標籤-如果您的應用程式建立 RDDs，您可以找到 hello 儲存體索引標籤中的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="678cb-155">Storage tab - If your application creates an RDDs, you can find information about those in hello Storage tab.</span></span>
   * <span data-ttu-id="678cb-156">環境索引標籤-此索引標籤提供了許多有用的資訊關於您的 Spark 執行個體，例如 hello</span><span class="sxs-lookup"><span data-stu-id="678cb-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as hello</span></span> 
     * <span data-ttu-id="678cb-157">Scala 版本</span><span class="sxs-lookup"><span data-stu-id="678cb-157">Scala version</span></span>
     * <span data-ttu-id="678cb-158">與 hello 叢集相關聯的事件記錄檔目錄</span><span class="sxs-lookup"><span data-stu-id="678cb-158">Event log directory associated with hello cluster</span></span>
     * <span data-ttu-id="678cb-159">Hello 應用程式的執行程式核心數目</span><span class="sxs-lookup"><span data-stu-id="678cb-159">Number of executor cores for hello application</span></span>
     * <span data-ttu-id="678cb-160">等等</span><span class="sxs-lookup"><span data-stu-id="678cb-160">Etc.</span></span>

## <a name="find-information-about-completed-jobs-using-hello-spark-history-server"></a><span data-ttu-id="678cb-161">尋找使用 hello Spark 記錄伺服器已完成工作的相關資訊</span><span class="sxs-lookup"><span data-stu-id="678cb-161">Find information about completed jobs using hello Spark History Server</span></span>
<span data-ttu-id="678cb-162">完成工作之後，hello hello 工作的資訊會保存在 hello Spark 歷程記錄的伺服器。</span><span class="sxs-lookup"><span data-stu-id="678cb-162">Once a job is completed, hello information about hello job is persisted in hello Spark History Server.</span></span>

1. <span data-ttu-id="678cb-163">toolaunch hello Spark 記錄伺服器上，從 hello 叢集刀鋒視窗中，按一下**叢集儀表板**，然後按一下 **Spark 記錄伺服器**。</span><span class="sxs-lookup"><span data-stu-id="678cb-163">toolaunch hello Spark History Server, from hello cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span>
   
    ![啟動 Spark 歷程記錄伺服器](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > <span data-ttu-id="678cb-165">或者，您也可以啟動 hello Spark 記錄 Server UI 從 hello Ambari UI。</span><span class="sxs-lookup"><span data-stu-id="678cb-165">Alternatively, you can also launch hello Spark History Server UI from hello Ambari UI.</span></span> <span data-ttu-id="678cb-166">按一下 toolaunch hello Ambari UI hello 叢集刀鋒視窗中，從**叢集儀表板**，然後按一下 **HDInsight 叢集儀表板**。</span><span class="sxs-lookup"><span data-stu-id="678cb-166">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="678cb-167">從 hello Ambari UI 中，按一下  **Spark**，按一下 **快速連結**，然後按一下 **Spark 記錄 Server UI**。</span><span class="sxs-lookup"><span data-stu-id="678cb-167">From hello Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span></span>
   > 
   > 
2. <span data-ttu-id="678cb-168">您會看到所有列出的 hello 完成應用程式。</span><span class="sxs-lookup"><span data-stu-id="678cb-168">You will see all hello completed applications listed.</span></span> <span data-ttu-id="678cb-169">如需詳細資訊的應用程式，向下一直按應用程式識別碼 toodrill。</span><span class="sxs-lookup"><span data-stu-id="678cb-169">Click an application ID toodrill down into an application for more info.</span></span>
   
    ![啟動 Spark 歷程記錄伺服器](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a><span data-ttu-id="678cb-171">另請參閱</span><span class="sxs-lookup"><span data-stu-id="678cb-171">See also</span></span>
*  [<span data-ttu-id="678cb-172">管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="678cb-172">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a><span data-ttu-id="678cb-173">針對資料分析師</span><span class="sxs-lookup"><span data-stu-id="678cb-173">For data analysts</span></span>

* [<span data-ttu-id="678cb-174">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="678cb-174">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="678cb-175">機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark</span><span class="sxs-lookup"><span data-stu-id="678cb-175">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="678cb-176">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="678cb-176">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="678cb-177">HDInsight 中使用 Spark 的 Application Insight 遙測資料分析</span><span class="sxs-lookup"><span data-stu-id="678cb-177">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="678cb-178">在 Azure HDInsight Spark 上使用 Caffe 進行分散式深入學習</span><span class="sxs-lookup"><span data-stu-id="678cb-178">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a><span data-ttu-id="678cb-179">針對 Spark 開發人員</span><span class="sxs-lookup"><span data-stu-id="678cb-179">For Spark developers</span></span>

* [<span data-ttu-id="678cb-180">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="678cb-180">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="678cb-181">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="678cb-181">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="678cb-182">HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="678cb-182">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="678cb-183">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="678cb-183">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="678cb-184">從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="678cb-184">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="678cb-185">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="678cb-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="678cb-186">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="678cb-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="678cb-187">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="678cb-187">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="678cb-188">在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="678cb-188">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


