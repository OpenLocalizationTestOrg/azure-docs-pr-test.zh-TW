---
title: "Microsoft 辨識工具組搭配 Azure HDInsight Spark 以深入學習 | Microsoft Docs"
description: "了解如何使用 Azure HDInsight Spark 叢集中的 Spark Python API，將定型的 Microsoft 辨識工具組深入學習模型套用至資料集。"
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
ms.openlocfilehash: fafd738f782660b824732bab8cc3bec8405947e7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a><span data-ttu-id="11bab-103">使用 Microsoft 辨識工具組深入了解模型與 Azure HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="11bab-103">Use Microsoft Cognitive Toolkit deep learning model with Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="11bab-104">在本文中，您會執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="11bab-104">In this article, you do the following steps.</span></span>

1. <span data-ttu-id="11bab-105">執行自訂指令碼，在 Azure HDInsight Spark 叢集上安裝 Microsoft 辨識工具組。</span><span class="sxs-lookup"><span data-stu-id="11bab-105">Run a custom script to install Microsoft Cognitive Toolkit on an Azure HDInsight Spark cluster.</span></span>

2. <span data-ttu-id="11bab-106">將 Jupyter Notebook 上傳至 Spark 叢集，以了解如何使用 [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)，將定型的 Microsoft 辨識工具組深入學習模型套用至 Azure Blob 儲存體帳戶中的檔案</span><span class="sxs-lookup"><span data-stu-id="11bab-106">Upload a Jupyter notebook to the Spark cluster to see how to apply a trained Microsoft Cognitive Toolkit deep learning model to files in an Azure Blob Storage Account using the [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11bab-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="11bab-107">Prerequisites</span></span>

* <span data-ttu-id="11bab-108">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="11bab-108">**An Azure subscription**.</span></span> <span data-ttu-id="11bab-109">開始進行本教學課程之前，您必須擁有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="11bab-109">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="11bab-110">請參閱[立即建立免費的 Azure 帳戶](https://azure.microsoft.com/free)。</span><span class="sxs-lookup"><span data-stu-id="11bab-110">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

* <span data-ttu-id="11bab-111">**Azure HDInsight Spark 叢集**。</span><span class="sxs-lookup"><span data-stu-id="11bab-111">**Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="11bab-112">針對本文，建立 Spark 2.0 叢集。</span><span class="sxs-lookup"><span data-stu-id="11bab-112">For this article, create a Spark 2.0 cluster.</span></span> <span data-ttu-id="11bab-113">如需指示，請參閱[在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="11bab-113">For instructions, see [Create Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-does-this-solution-flow"></a><span data-ttu-id="11bab-114">此解決方案的流程為何？</span><span class="sxs-lookup"><span data-stu-id="11bab-114">How does this solution flow?</span></span>

<span data-ttu-id="11bab-115">此解決方案可分為本文章與您上傳作為本教學課程一部分的 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="11bab-115">This solution is divided between this article and a Jupyter notebook that you upload as part of this tutorial.</span></span> <span data-ttu-id="11bab-116">在本文中，您必須完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="11bab-116">In this article, you complete the following steps:</span></span>

* <span data-ttu-id="11bab-117">在 HDInsight Spark 叢集上執行指令碼動作來安裝 Microsoft 辨識工具組和 Python 套件。</span><span class="sxs-lookup"><span data-stu-id="11bab-117">Run a script action on an HDInsight Spark cluster to install Microsoft Cognitive Toolkit and Python packages.</span></span>
* <span data-ttu-id="11bab-118">將 Jupyter Notebook 上傳至執行此解決方案的 HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="11bab-118">Upload the Jupyter notebook that runs the solution to the HDInsight Spark cluster.</span></span>

<span data-ttu-id="11bab-119">Jupyter Notebook 中涵蓋下列剩餘步驟。</span><span class="sxs-lookup"><span data-stu-id="11bab-119">The following remaining steps are covered in the Jupyter notebook.</span></span>

- <span data-ttu-id="11bab-120">將範例映像載入 Spark 復原分散式資料集或 RDD</span><span class="sxs-lookup"><span data-stu-id="11bab-120">Load sample images into a Spark Resiliant Distributed Dataset or RDD</span></span>
   - <span data-ttu-id="11bab-121">載入模組並定義預設值</span><span class="sxs-lookup"><span data-stu-id="11bab-121">Load modules and define presets</span></span>
   - <span data-ttu-id="11bab-122">在 Spark 叢集上的本機下載資料集</span><span class="sxs-lookup"><span data-stu-id="11bab-122">Download the dataset locally on the Spark cluster</span></span>
   - <span data-ttu-id="11bab-123">將資料集轉換成 RDD</span><span class="sxs-lookup"><span data-stu-id="11bab-123">Convert the dataset into an RDD</span></span>
- <span data-ttu-id="11bab-124">使用定型的辨識工具組模型對映像進行評分</span><span class="sxs-lookup"><span data-stu-id="11bab-124">Score the images using a trained Cognitive Toolkit model</span></span>
   - <span data-ttu-id="11bab-125">下載定型的辨識工具組模型至 Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="11bab-125">Download the trained Cognitive Toolkit model to the Spark cluster</span></span>
   - <span data-ttu-id="11bab-126">定義可供背景工作節點使用的函式</span><span class="sxs-lookup"><span data-stu-id="11bab-126">Define functions to be used by worker nodes</span></span>
   - <span data-ttu-id="11bab-127">在背景工作節點上對映像進行評分</span><span class="sxs-lookup"><span data-stu-id="11bab-127">Score the images on worker nodes</span></span>
   - <span data-ttu-id="11bab-128">評估模型的精確度</span><span class="sxs-lookup"><span data-stu-id="11bab-128">Evaluate model accuracy</span></span>


## <a name="install-microsoft-cognitive-toolkit"></a><span data-ttu-id="11bab-129">安裝 Microsoft 辨識工具組</span><span class="sxs-lookup"><span data-stu-id="11bab-129">Install Microsoft Cognitive Toolkit</span></span>

<span data-ttu-id="11bab-130">您可以使用指令碼動作在 Spark 叢集上安裝 Microsoft 辨識工具組。</span><span class="sxs-lookup"><span data-stu-id="11bab-130">You can install Microsoft Cognitive Toolkit on a Spark cluster using script action.</span></span> <span data-ttu-id="11bab-131">指令碼動作會使用自訂指令碼在叢集上安裝不是預設可用的元件。</span><span class="sxs-lookup"><span data-stu-id="11bab-131">Script action uses custom scripts to install components on the cluster that are not available by default.</span></span> <span data-ttu-id="11bab-132">您可以透過 Azure 入口網站使用自訂指令碼，使用 HDInsight .NET SDK 或 Azure PowerShell 都可以。</span><span class="sxs-lookup"><span data-stu-id="11bab-132">You can use the custom script from the Azure Portal, by using HDInsight .NET SDK, or by using Azure PowerShell.</span></span> <span data-ttu-id="11bab-133">您也可以使用指令碼，在叢集建立期間安裝工具組，或在叢集已啟動並執行之後加以安裝。</span><span class="sxs-lookup"><span data-stu-id="11bab-133">You can also use the script to install the toolkit either as part of cluster creation, or after the cluster is up and running.</span></span> 

<span data-ttu-id="11bab-134">在本文中，我們在建立叢集之後，使用入口網站來安裝工具組。</span><span class="sxs-lookup"><span data-stu-id="11bab-134">In this article, we use the portal to install the toolkit, after the cluster has been created.</span></span> <span data-ttu-id="11bab-135">如需執行自訂指令碼的其他方式，請參閱[使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="11bab-135">For other ways to run the custom script, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="11bab-136">使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="11bab-136">Using the Azure Portal</span></span>

<span data-ttu-id="11bab-137">如需有關如何使用 Azure 入口網站來執行指令碼動作的指示，請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation)。</span><span class="sxs-lookup"><span data-stu-id="11bab-137">For instructions on how to use the Azure Portal to run script action, see [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation).</span></span> <span data-ttu-id="11bab-138">確定您提供下列輸入來安裝 Microsoft 辨識工具組。</span><span class="sxs-lookup"><span data-stu-id="11bab-138">Make sure you provide the following inputs to install Microsoft Cognitive Toolkit.</span></span>

* <span data-ttu-id="11bab-139">提供指令碼動作名稱的值。</span><span class="sxs-lookup"><span data-stu-id="11bab-139">Provide a value for the script action name.</span></span>

* <span data-ttu-id="11bab-140">對於 **Bash 指令碼 URI**，輸入 `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`。</span><span class="sxs-lookup"><span data-stu-id="11bab-140">For **Bash script URI**, enter `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.</span></span>

* <span data-ttu-id="11bab-141">確定您只會在前端和背景工作節點上執行指令碼，並清除所有其他核取方塊。</span><span class="sxs-lookup"><span data-stu-id="11bab-141">Make sure you run the script only on the head and worker nodes and clear all the other checkboxes.</span></span>

* <span data-ttu-id="11bab-142">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="11bab-142">Click **Create**.</span></span>

## <a name="upload-the-jupyter-notebook-to-azure-hdinsight-spark-cluster"></a><span data-ttu-id="11bab-143">將 Jupyter Notebook 上傳至 Azure HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="11bab-143">Upload the Jupyter notebook to Azure HDInsight Spark cluster</span></span>

<span data-ttu-id="11bab-144">若要使用 Microsoft 辨識工具組搭配 Azure HDInsight Spark 叢集，您必須將 Jupyter Notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** 載入至 Azure HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="11bab-144">To use the Microsoft Cognitive Toolkit with the Azure HDInsight Spark cluster, you must load the Jupyter notebook **CNTK_model_scoring_on_Spark_walkthrough.ipynb** to the Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="11bab-145">這個 Notebook 可在 GitHub 上取得，網址是：[https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration)。</span><span class="sxs-lookup"><span data-stu-id="11bab-145">This notebook is available on GitHub at [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span>

1. <span data-ttu-id="11bab-146">複製 GitHub 存放庫 [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration)。</span><span class="sxs-lookup"><span data-stu-id="11bab-146">Clone the GitHub repository [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).</span></span> <span data-ttu-id="11bab-147">如需複製的指示，請參閱[複製存放庫](https://help.github.com/articles/cloning-a-repository/)。</span><span class="sxs-lookup"><span data-stu-id="11bab-147">For instructions to clone, see [Cloning a repository](https://help.github.com/articles/cloning-a-repository/).</span></span>

2. <span data-ttu-id="11bab-148">從 Azure 入口網站開啟您已佈建的 Spark 叢集刀鋒視窗，按一下 [叢集儀表板]，然後按一下 [Jupyter Notebook]。</span><span class="sxs-lookup"><span data-stu-id="11bab-148">From the Azure Portal, open the Spark cluster blade that you already provisioned, click **Cluster Dashboard**, and then click **Jupyter notebook**.</span></span>

    <span data-ttu-id="11bab-149">您也可以移至 URL `https://<clustername>.azurehdinsight.net/jupyter/` 啟動 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="11bab-149">You can also launch the Jupyter notebook by going to the URL `https://<clustername>.azurehdinsight.net/jupyter/`.</span></span> <span data-ttu-id="11bab-150">將 \<clustername> 取代為 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="11bab-150">Replace \<clustername> with the name of your HDInsight cluster.</span></span>

3. <span data-ttu-id="11bab-151">從 Jupyter Notebook 中，於右上角按一下 [上傳]，然後瀏覽至您複製 GitHub 存放庫的位置。</span><span class="sxs-lookup"><span data-stu-id="11bab-151">From the Jupyter notebook, click **Upload** in the top-right corner and then navigate to the location where you cloned the GitHub repository.</span></span>

    <span data-ttu-id="11bab-152">![將 Jupyter Notebook 上傳至 Azure HDInsight Spark 叢集](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "將 Jupyter Notebook 上傳至 Azure HDInsight Spark 叢集")</span><span class="sxs-lookup"><span data-stu-id="11bab-152">![Upload Jupyter notebook to Azure HDInsight Spark cluster](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "Upload Jupyter notebook to Azure HDInsight Spark cluster")</span></span>

4. <span data-ttu-id="11bab-153">再次按一下 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="11bab-153">Click **Upload** again.</span></span>

5. <span data-ttu-id="11bab-154">將 Notebook 上傳之後，按一下 Notebook 名稱，然後遵循 Notebook 本身有關如何載入資料集的指示，並執行教學課程中。</span><span class="sxs-lookup"><span data-stu-id="11bab-154">After the notebook is uploaded, click the name of the notebook and then follow the instructions in the notebook itself on how to load the data set and perform the tutorial.</span></span>

## <a name="see-also"></a><span data-ttu-id="11bab-155">另請參閱</span><span class="sxs-lookup"><span data-stu-id="11bab-155">See also</span></span>
* [<span data-ttu-id="11bab-156">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="11bab-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="11bab-157">案例</span><span class="sxs-lookup"><span data-stu-id="11bab-157">Scenarios</span></span>
* [<span data-ttu-id="11bab-158">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="11bab-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="11bab-159">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="11bab-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="11bab-160">Spark 和機器學習服務：使用 HDInsight 中的 Spark 來預測食品檢查結果</span><span class="sxs-lookup"><span data-stu-id="11bab-160">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="11bab-161">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="11bab-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="11bab-162">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="11bab-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="11bab-163">HDInsight 中使用 Spark 的 Application Insight 遙測資料分析</span><span class="sxs-lookup"><span data-stu-id="11bab-163">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="11bab-164">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="11bab-164">Create and run applications</span></span>
* [<span data-ttu-id="11bab-165">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="11bab-165">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="11bab-166">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="11bab-166">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="11bab-167">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="11bab-167">Tools and extensions</span></span>
* [<span data-ttu-id="11bab-168">使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式來建立和提交 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="11bab-168">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="11bab-169">使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式遠端偵錯 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="11bab-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="11bab-170">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="11bab-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="11bab-171">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="11bab-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="11bab-172">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="11bab-172">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="11bab-173">在電腦上安裝 Jupyter 並連接到 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="11bab-173">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="11bab-174">管理資源</span><span class="sxs-lookup"><span data-stu-id="11bab-174">Manage resources</span></span>
* [<span data-ttu-id="11bab-175">在 Azure HDInsight 中管理 Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="11bab-175">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="11bab-176">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="11bab-176">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
