---
title: "深入了解 aaaMicrosoft 認知的工具組使用 Azure HDInsight Spark |Microsoft 文件"
description: "了解如何定型 Microsoft 認知 Toolkit 深入學習模型可以是使用 Azure HDInsight Spark 叢集中的 hello Spark Python 應用程式開發介面的 tooa 套用資料集。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="3d9fb-103">使用 Microsoft 辨識工具組深入了解模型與 Azure HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="3d9fb-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="3d9fb-104">在本文中，您下列步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-104">In this article, you do hello following steps.</span></span>

1. <span data-ttu-id="3d9fb-105">Azure HDInsight Spark 叢集上執行自訂指令碼 tooinstall Microsoft 認知工具組。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-105">Run a custom script tooinstall Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="3d9fb-106">如何上傳 Jupyter 筆記本 toohello Spark 叢集 toosee tooapply 定型 Microsoft 認知 Toolkit 深入了解使用 hello Azure Blob 儲存體帳戶中的模型 toofiles [Spark Python 應用程式開發介面 (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span><span class="sxs-lookup"><span data-stu-id="3d9fb-106">Upload a Jupyter notebook toohello Spark cluster toosee how tooapply a trained Microsoft Cognitive Toolkit deep learning model toofiles in an Azure Blob Storage Account using hello [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d9fb-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="3d9fb-107">Prerequisites</span></span>

* <span data-ttu-id="3d9fb-108">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-108">**An Azure subscription**.</span></span> <span data-ttu-id="3d9fb-109">開始進行本教學課程之前，您必須擁有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="3d9fb-110">請參閱[立即建立免費的 Azure 帳戶](https://azure.microsoft.com/free)。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="3d9fb-111">**Azure HDInsight Spark 叢集**。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="3d9fb-112">針對本文，建立 Spark 2.0 叢集。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="3d9fb-113">如需指示，請參閱[在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="3d9fb-114">此解決方案的流程為何？</span><span class="sxs-lookup"><span data-stu-id="3d9fb-114">How does this solution flow?</span></span>

<span data-ttu-id="3d9fb-115">此解決方案可分為本文章與您上傳作為本教學課程一部分的 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="3d9fb-116">在本文中，您將完成 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3d9fb-116">In this article, you complete hello following steps:</span></span>

* <span data-ttu-id="3d9fb-117">HDInsight Spark 叢集上 tooinstall Microsoft 認知工具組，並將 Python 封裝執行的指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-117">Run a script action on an HDInsight Spark cluster tooinstall Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="3d9fb-118">上傳 hello Jupyter 筆記本執行 hello 方案 toohello HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-118">Upload hello Jupyter notebook that runs hello solution toohello HDInsight Spark cluster.</span></span>

<span data-ttu-id="3d9fb-119">hello 下列其餘涵蓋了步驟 hello Jupyter 筆記本中。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-119">hello following remaining steps are covered in hello Jupyter notebook.</span></span>

- <span data-ttu-id="3d9fb-120">將範例映像載入 Spark 復原分散式資料集或 RDD</span><span class="sxs-lookup"><span data-stu-id="3d9fb-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="3d9fb-121">載入模組並定義預設值</span><span class="sxs-lookup"><span data-stu-id="3d9fb-121">Load modules and define presets</span></span>
   - <span data-ttu-id="3d9fb-122">下載 hello hello Spark 叢集，在本機的資料集</span><span class="sxs-lookup"><span data-stu-id="3d9fb-122">Download hello dataset locally on hello Spark cluster</span></span>
   - <span data-ttu-id="3d9fb-123">轉換 RDD hello 資料集</span><span class="sxs-lookup"><span data-stu-id="3d9fb-123">Convert hello dataset into an RDD</span></span>
- <span data-ttu-id="3d9fb-124">使用定型的認知 Toolkit 模型的分數 hello 映像</span><span class="sxs-lookup"><span data-stu-id="3d9fb-124">Score hello images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="3d9fb-125">下載 hello 定型認知 Toolkit 模型 toohello Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="3d9fb-125">Download hello trained Cognitive Toolkit model toohello Spark cluster</span></span>
   - <span data-ttu-id="3d9fb-126">定義背景工作節點使用的函式 toobe</span><span class="sxs-lookup"><span data-stu-id="3d9fb-126">Define functions toobe used by worker nodes</span></span>
   - <span data-ttu-id="3d9fb-127">在背景工作角色節點的分數 hello 映像</span><span class="sxs-lookup"><span data-stu-id="3d9fb-127">Score hello images on worker nodes</span></span>
   - <span data-ttu-id="3d9fb-128">評估模型的精確度</span><span class="sxs-lookup"><span data-stu-id="3d9fb-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="3d9fb-129">安裝 Microsoft 辨識工具組</span><span class="sxs-lookup"><span data-stu-id="3d9fb-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="3d9fb-130">您可以使用指令碼動作在 Spark 叢集上安裝 Microsoft 辨識工具組。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="3d9fb-131">指令碼動作會在無法使用預設的 hello 叢集上使用自訂指令碼 tooinstall 元件。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-131">Script action uses custom scripts tooinstall components on hello cluster that are not available by default.</span></span> <span data-ttu-id="3d9fb-132">使用 HDInsight.NET SDK，或使用 Azure PowerShell，您可以使用 hello hello Azure 入口網站中，從自訂指令碼。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-132">You can use hello custom script from hello Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="3d9fb-133">您也可以為叢集建立或 hello 叢集已啟動並執行後的一部分使用 hello 指令碼 tooinstall hello 工具組。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-133">You can also use hello script tooinstall hello toolkit either as part of cluster creation, or after hello cluster is up and running.</span></span> 

<span data-ttu-id="3d9fb-134">在本文中，我們會使用 hello 入口 tooinstall hello 工具組，建立 hello 叢集之後。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-134">In this article, we use hello portal tooinstall hello toolkit, after hello cluster has been created.</span></span> <span data-ttu-id="3d9fb-135">針對其他方式 toorun hello 自訂指令碼，請參閱[自訂 HDInsight 叢集使用指令碼動作](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-135">For other ways toorun hello custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="3d9fb-136">使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="3d9fb-136">Using hello Azure Portal</span></span>

<span data-ttu-id="3d9fb-137">如需有關如何 toouse hello Azure 入口網站 toorun 指令碼動作的指示，請參閱[自訂 HDInsight 叢集使用指令碼動作](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation)。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-137">For instructions on how toouse hello Azure Portal toorun script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="3d9fb-138">請確定您提供下列輸入 tooinstall Microsoft 認知 Toolkit hello。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-138">Make sure you provide hello following inputs tooinstall Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="3d9fb-139">提供 hello 指令碼動作名稱的值。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-139">Provide a value for hello script action name.</span></span>

* <span data-ttu-id="3d9fb-140">對於 **Bash 指令碼 URI**，輸入 `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="3d9fb-141">請確定您執行 hello 指令碼只在 hello head 和背景工作節點並清除所有 hello 其他核取方塊。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-141">Make sure you run hello script only on hello head and worker nodes and clear all hello other checkboxes.</span></span>

* <span data-ttu-id="3d9fb-142">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-142">Click **Create**.</span></span>

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a><span data-ttu-id="3d9fb-143">上傳 hello Jupyter 筆記本 tooAzure HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="3d9fb-143">Upload hello Jupyter notebook tooAzure HDInsight Spark cluster</span></span>

<span data-ttu-id="3d9fb-144">toouse hello Microsoft 認知 Toolkit 與 hello Azure HDInsight Spark 叢集，您必須先載入 hello Jupyter 筆記本**CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-144">toouse hello Microsoft Cognitive Toolkit with hello Azure HDInsight Spark cluster, you must load hello Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="3d9fb-145">這個 Notebook 可在 GitHub 上取得，網址是：[https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration)。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="3d9fb-146">複製 hello GitHub 儲存機制[https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration)。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-146">Clone hello GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="3d9fb-147">指示 tooclone，請參閱[複製的儲存機制](https://help.github.com/articles/cloning-a-repository/)。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-147">For instructions tooclone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="3d9fb-148">從 hello Azure 入口網站，開啟 已佈建，按一下的 hello Spark 叢集分頁**叢集儀表板**，然後按一下 **Jupyter 筆記本**。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-148">From hello Azure Portal, open hello Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="3d9fb-149">您也可以藉由選取 toohello URL 啟動 hello Jupyter 筆記本`https://<clustername>.azurehdinsight.net/jupyter/`。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-149">You can also launch hello Jupyter notebook by going toohello URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="3d9fb-150">取代\<clustername > hello 名稱，為您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-150">Replace \<clustername> with hello name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="3d9fb-151">從 hello Jupyter 筆記本中，按一下 **上傳**在 hello 右上角，然後瀏覽您再製 hello GitHub 儲存機制的 toohello 位置。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-151">From hello Jupyter notebook, click **Upload** in hello top-right corner and then navigate toohello location where you cloned hello GitHub repository.</span></span>

    <span data-ttu-id="3d9fb-152">![上傳 Jupyter 筆記本 tooAzure HDInsight Spark 叢集](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "上傳 Jupyter 筆記本 tooAzure HDInsight Spark 叢集")</span><span class="sxs-lookup"><span data-stu-id="3d9fb-152">![Upload Jupyter notebook tooAzure HDInsight Spark cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook tooAzure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="3d9fb-153">再次按一下 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-153">Click **Upload** again.</span></span>

5. <span data-ttu-id="3d9fb-154">Hello 筆記本已上傳之後，按一下 hello 筆記本的 hello 名稱，並遵照 tooload hello 資料集和執行 hello 教學課程的方式上本身 hello 筆記本中的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="3d9fb-154">After hello notebook is uploaded, click hello name of hello notebook and then follow hello instructions in hello notebook itself on how tooload hello data set and perform hello tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="3d9fb-155">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3d9fb-155">See also</span></span>
* [<span data-ttu-id="3d9fb-156">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="3d9fb-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="3d9fb-157">案例</span><span class="sxs-lookup"><span data-stu-id="3d9fb-157">Scenarios</span></span>
* [<span data-ttu-id="3d9fb-158">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="3d9fb-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="3d9fb-159">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="3d9fb-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="3d9fb-160">機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark</span><span class="sxs-lookup"><span data-stu-id="3d9fb-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="3d9fb-161">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="3d9fb-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="3d9fb-162">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="3d9fb-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="3d9fb-163">HDInsight 中使用 Spark 的 Application Insight 遙測資料分析</span><span class="sxs-lookup"><span data-stu-id="3d9fb-163">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="3d9fb-164">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="3d9fb-164">Create and run applications</span></span>
* [<span data-ttu-id="3d9fb-165">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="3d9fb-165">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="3d9fb-166">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="3d9fb-166">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="3d9fb-167">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="3d9fb-167">Tools and extensions</span></span>
* [<span data-ttu-id="3d9fb-168">HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="3d9fb-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="3d9fb-169">從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="3d9fb-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="3d9fb-170">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="3d9fb-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="3d9fb-171">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="3d9fb-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="3d9fb-172">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="3d9fb-172">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="3d9fb-173">在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="3d9fb-173">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="3d9fb-174">管理資源</span><span class="sxs-lookup"><span data-stu-id="3d9fb-174">Manage resources</span></span>
* [<span data-ttu-id="3d9fb-175">管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="3d9fb-175">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="3d9fb-176">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="3d9fb-176">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
