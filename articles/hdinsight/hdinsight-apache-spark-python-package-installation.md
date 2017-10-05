---
title: "指令碼動作 - 在 Azure HDInsight 上搭配 Jupyter 安裝 Python 套件 | Microsoft Docs"
description: "說明如何使用指令碼動作以設定讓 HDInsight Spark 叢集隨附之 Jupyter Notebook 使用外部 Python 套件的逐步指示。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 20cf384c96d4ff4eaf064c8880ad128d521fb9bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-script-action-to-install-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="3fe41-103">使用指令碼動作在 HDInsight Linux 上的 Apache Spark 叢集中安裝 Jupyter Notebook 的外部 Python 封裝</span><span class="sxs-lookup"><span data-stu-id="3fe41-103">Use Script Action to install external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3fe41-104">使用資料格魔術</span><span class="sxs-lookup"><span data-stu-id="3fe41-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="3fe41-105">使用指令碼動作</span><span class="sxs-lookup"><span data-stu-id="3fe41-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="3fe41-106">了解如何使用指令碼動作，將 HDInsight (Linux) 上的 Apache Spark 叢集設定為使用外部、社群的提供 **Python** 套件，而不是叢集中現成隨附的套件。</span><span class="sxs-lookup"><span data-stu-id="3fe41-106">Learn how to use Script Actions to configure an Apache Spark cluster on HDInsight (Linux) to use external, community-contributed **python** packages that are not included out-of-the-box in the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="3fe41-107">您也可以藉由使用 `%%configure` 魔術，設定 Jupyter Notebook 來使用外部的封裝。</span><span class="sxs-lookup"><span data-stu-id="3fe41-107">You can also configure a Jupyter notebook by using `%%configure` magic to use external packages.</span></span> <span data-ttu-id="3fe41-108">如需指示，請參閱[在 HDInsight 上的 Apache Spark 叢集中搭配 Jupyter Notebook 使用外部封裝](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="3fe41-108">For instructions, see [Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span></span>
> 
> 

<span data-ttu-id="3fe41-109">您可以搜尋[套件索引](https://pypi.python.org/pypi)，以取得可用的套件完整清單。</span><span class="sxs-lookup"><span data-stu-id="3fe41-109">You can search the [package index](https://pypi.python.org/pypi) for the complete list of packages that are available.</span></span> <span data-ttu-id="3fe41-110">您也可以從其他來源取得可用套件清單。</span><span class="sxs-lookup"><span data-stu-id="3fe41-110">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="3fe41-111">例如，您可以安裝經由 [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) 或 [conda-forge](https://conda-forge.github.io/feedstocks.html) 提供的套件。</span><span class="sxs-lookup"><span data-stu-id="3fe41-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.github.io/feedstocks.html).</span></span>

<span data-ttu-id="3fe41-112">在本文中，您將學習如何在叢集上使用指令碼動作安裝 [TensorFlow](https://www.tensorflow.org/) 套件，並使用透過 Jupyter Notebook 來使用它。</span><span class="sxs-lookup"><span data-stu-id="3fe41-112">In this article, you will learn how to install the [TensorFlow](https://www.tensorflow.org/) package using Script Actoin on your cluster and use it via the Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fe41-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="3fe41-113">Prerequisites</span></span>
<span data-ttu-id="3fe41-114">您必須滿足以下條件：</span><span class="sxs-lookup"><span data-stu-id="3fe41-114">You must have the following:</span></span>

* <span data-ttu-id="3fe41-115">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fe41-115">An Azure subscription.</span></span> <span data-ttu-id="3fe41-116">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="3fe41-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="3fe41-117">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="3fe41-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="3fe41-118">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="3fe41-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="3fe41-119">如果您在 HDInsight Linux 上還沒有 Spark 叢集，您可以在叢集建立期間執行指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="3fe41-119">If you do not already have a Spark cluster on HDInsight Linux, you can run script actions during cluster creation.</span></span> <span data-ttu-id="3fe41-120">瀏覽有關於[如何使用自訂指令碼動作](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)的文件。</span><span class="sxs-lookup"><span data-stu-id="3fe41-120">Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="3fe41-121">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="3fe41-121">Use external packages with Jupyter notebooks</span></span>

1. <span data-ttu-id="3fe41-122">在 [Azure 入口網站](https://portal.azure.com/)的開始面板中，按一下您的 Spark 叢集磚 (如果您已將其釘選到開始面板)。</span><span class="sxs-lookup"><span data-stu-id="3fe41-122">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="3fe41-123">您也可以按一下 [瀏覽全部] > [HDInsight 叢集] 來瀏覽至您的叢集。</span><span class="sxs-lookup"><span data-stu-id="3fe41-123">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="3fe41-124">從 Spark 叢集刀鋒視窗中，按一下 [使用量] 下的 [指令碼動作]。</span><span class="sxs-lookup"><span data-stu-id="3fe41-124">From the Spark cluster blade, click **Script Actions** under **Usage**.</span></span> <span data-ttu-id="3fe41-125">執行自訂動作，將 TensorFlow 安裝在前端節點和背景工作角色節點。</span><span class="sxs-lookup"><span data-stu-id="3fe41-125">Run the custom action that installs TensorFlow in the head nodes and the worker nodes.</span></span> <span data-ttu-id="3fe41-126">您可以從這裡參考 bash 指令碼: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh 瀏覽有關於 [如何使用自訂指令碼動作](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux) 的文件。</span><span class="sxs-lookup"><span data-stu-id="3fe41-126">The bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit the documentation on [how to use custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   > [!NOTE]
   > <span data-ttu-id="3fe41-127">叢集中有兩個 Python 安裝。</span><span class="sxs-lookup"><span data-stu-id="3fe41-127">There are two python installations in the cluster.</span></span> <span data-ttu-id="3fe41-128">Spark 會使用位於 `/usr/bin/anaconda/bin` 的 Anaconda Python 安裝。</span><span class="sxs-lookup"><span data-stu-id="3fe41-128">Spark will use the Anaconda python installation located at `/usr/bin/anaconda/bin`.</span></span> <span data-ttu-id="3fe41-129">在您的自訂動作中，透過 `/usr/bin/anaconda/bin/pip` 和 `/usr/bin/anaconda/bin/conda` 來參考該安裝。</span><span class="sxs-lookup"><span data-stu-id="3fe41-129">Reference that installation in your custom actions via `/usr/bin/anaconda/bin/pip` and `/usr/bin/anaconda/bin/conda`.</span></span>
   > 
   > 

3. <span data-ttu-id="3fe41-130">開啟 PySpark Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="3fe41-130">Open a PySpark Jupyter notebook</span></span>

    <span data-ttu-id="3fe41-131">![建立新的 Jupyter Notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "建立新的 Jupyter Notebook")</span><span class="sxs-lookup"><span data-stu-id="3fe41-131">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="3fe41-132">系統隨即會建立新 Notebook，並以 Untitled.pynb 的名稱開啟。</span><span class="sxs-lookup"><span data-stu-id="3fe41-132">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="3fe41-133">在頂端按一下 Notebook 名稱，然後輸入好記的名稱。</span><span class="sxs-lookup"><span data-stu-id="3fe41-133">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="3fe41-134">![提供 Notebook 的名稱](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "提供 Notebook 的名稱")</span><span class="sxs-lookup"><span data-stu-id="3fe41-134">![Provide a name for the notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for the notebook")</span></span>

5. <span data-ttu-id="3fe41-135">現在，您將 `import tensorflow` 並執行 hello world 範例。</span><span class="sxs-lookup"><span data-stu-id="3fe41-135">You will now `import tensorflow` and run a hello world example.</span></span> 

    <span data-ttu-id="3fe41-136">要複製的程式碼︰</span><span class="sxs-lookup"><span data-stu-id="3fe41-136">Code to copy:</span></span>

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    <span data-ttu-id="3fe41-137">結果如下所示：</span><span class="sxs-lookup"><span data-stu-id="3fe41-137">The result will look like this:</span></span>
    
    <span data-ttu-id="3fe41-138">![TensorFlow 程式碼執行](./media/hdinsight-apache-spark-python-package-installation/execution.png "執行 TensorFlow 程式碼")</span><span class="sxs-lookup"><span data-stu-id="3fe41-138">![TensorFlow code execution](./media/hdinsight-apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span></span>



## <span data-ttu-id="3fe41-139"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="3fe41-139"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="3fe41-140">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="3fe41-140">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="3fe41-141">案例</span><span class="sxs-lookup"><span data-stu-id="3fe41-141">Scenarios</span></span>
* [<span data-ttu-id="3fe41-142">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="3fe41-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="3fe41-143">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="3fe41-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="3fe41-144">Spark 和機器學習服務：使用 HDInsight 中的 Spark 來預測食品檢查結果</span><span class="sxs-lookup"><span data-stu-id="3fe41-144">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="3fe41-145">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="3fe41-145">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="3fe41-146">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="3fe41-146">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="3fe41-147">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="3fe41-147">Create and run applications</span></span>
* [<span data-ttu-id="3fe41-148">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="3fe41-148">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="3fe41-149">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="3fe41-149">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="3fe41-150">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="3fe41-150">Tools and extensions</span></span>
* [<span data-ttu-id="3fe41-151">在 HDInsight 上的 Apache Spark 叢集中搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="3fe41-151">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="3fe41-152">使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式來建立和提交 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="3fe41-152">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="3fe41-153">使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式遠端偵錯 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="3fe41-153">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="3fe41-154">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="3fe41-154">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="3fe41-155">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="3fe41-155">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="3fe41-156">在電腦上安裝 Jupyter 並連接到 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="3fe41-156">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="3fe41-157">管理資源</span><span class="sxs-lookup"><span data-stu-id="3fe41-157">Manage resources</span></span>
* [<span data-ttu-id="3fe41-158">在 Azure HDInsight 中管理 Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="3fe41-158">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="3fe41-159">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="3fe41-159">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
