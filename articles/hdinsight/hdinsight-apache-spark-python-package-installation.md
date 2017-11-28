---
title: "aaaScript 動作-安裝 Python 封裝，使用 Azure HDInsight 上 Jupyter |Microsoft 文件"
description: "上如何 toouse 指令碼動作 tooconfigure Jupyter 筆記本適用於 HDInsight Spark 叢集 toouse 外部 python 封裝的逐步指示。"
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
ms.openlocfilehash: 54db79e67995dee7ca00abff979f7d74ae5ab9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-script-action-tooinstall-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="b6b45-103">使用 Apache Spark 叢集，在 HDInsight 上 Jupyter 筆記本的指令碼動作 tooinstall 外部 Python 封裝</span><span class="sxs-lookup"><span data-stu-id="b6b45-103">Use Script Action tooinstall external Python packages for Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b6b45-104">使用資料格魔術</span><span class="sxs-lookup"><span data-stu-id="b6b45-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="b6b45-105">使用指令碼動作</span><span class="sxs-lookup"><span data-stu-id="b6b45-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="b6b45-106">了解如何 toouse 指令碼動作 tooconfigure Apache Spark 叢集上 HDInsight (Linux) toouse 外部、 社群貢獻**python**不封裝在 hello 叢集中包含的方塊外。</span><span class="sxs-lookup"><span data-stu-id="b6b45-106">Learn how toouse Script Actions tooconfigure an Apache Spark cluster on HDInsight (Linux) toouse external, community-contributed **python** packages that are not included out-of-the-box in hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="b6b45-107">您也可以藉由設定 Jupyter 筆記本`%%configure`magic toouse 外部的封裝。</span><span class="sxs-lookup"><span data-stu-id="b6b45-107">You can also configure a Jupyter notebook by using `%%configure` magic toouse external packages.</span></span> <span data-ttu-id="b6b45-108">如需指示，請參閱[在 HDInsight 上的 Apache Spark 叢集中搭配 Jupyter Notebook 使用外部封裝](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="b6b45-108">For instructions, see [Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).</span></span>
> 
> 

<span data-ttu-id="b6b45-109">您可以搜尋 hello[封裝索引](https://pypi.python.org/pypi)如 hello 的封裝所提供的完整清單。</span><span class="sxs-lookup"><span data-stu-id="b6b45-109">You can search hello [package index](https://pypi.python.org/pypi) for hello complete list of packages that are available.</span></span> <span data-ttu-id="b6b45-110">您也可以從其他來源取得可用套件清單。</span><span class="sxs-lookup"><span data-stu-id="b6b45-110">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="b6b45-111">例如，您可以安裝經由 [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) 或 [conda-forge](https://conda-forge.github.io/feedstocks.html) 提供的套件。</span><span class="sxs-lookup"><span data-stu-id="b6b45-111">For example, you can install packages made available through [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) or [conda-forge](https://conda-forge.github.io/feedstocks.html).</span></span>

<span data-ttu-id="b6b45-112">在本文中，您將學習如何 tooinstall hello [TensorFlow](https://www.tensorflow.org/)封裝您的叢集上使用指令碼 Actoin 並使用透過 hello Jupyter 筆記本。</span><span class="sxs-lookup"><span data-stu-id="b6b45-112">In this article, you will learn how tooinstall hello [TensorFlow](https://www.tensorflow.org/) package using Script Actoin on your cluster and use it via hello Jupyter notebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6b45-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="b6b45-113">Prerequisites</span></span>
<span data-ttu-id="b6b45-114">您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="b6b45-114">You must have hello following:</span></span>

* <span data-ttu-id="b6b45-115">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b6b45-115">An Azure subscription.</span></span> <span data-ttu-id="b6b45-116">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="b6b45-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="b6b45-117">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="b6b45-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="b6b45-118">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="b6b45-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="b6b45-119">如果您在 HDInsight Linux 上還沒有 Spark 叢集，您可以在叢集建立期間執行指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="b6b45-119">If you do not already have a Spark cluster on HDInsight Linux, you can run script actions during cluster creation.</span></span> <span data-ttu-id="b6b45-120">瀏覽 hello 文件上[toouse 自訂如何編寫指令碼動作](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)。</span><span class="sxs-lookup"><span data-stu-id="b6b45-120">Visit hello documentation on [how toouse custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="b6b45-121">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="b6b45-121">Use external packages with Jupyter notebooks</span></span>

1. <span data-ttu-id="b6b45-122">從 hello [Azure 入口網站](https://portal.azure.com/)，從 hello 開始面板中，按一下 Spark 叢集中的 hello 磚 （如果您釘選它 toohello 開始面板）。</span><span class="sxs-lookup"><span data-stu-id="b6b45-122">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="b6b45-123">您也可以導覽 tooyour 叢集下的**瀏覽所有** > **HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="b6b45-123">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="b6b45-124">從 hello Spark 叢集刀鋒視窗中，按一下 **指令碼動作**下**使用量**。</span><span class="sxs-lookup"><span data-stu-id="b6b45-124">From hello Spark cluster blade, click **Script Actions** under **Usage**.</span></span> <span data-ttu-id="b6b45-125">執行安裝 TensorFlow hello 前端節點和 hello 背景工作角色節點中的 hello 自訂動作。</span><span class="sxs-lookup"><span data-stu-id="b6b45-125">Run hello custom action that installs TensorFlow in hello head nodes and hello worker nodes.</span></span> <span data-ttu-id="b6b45-126">您可以從參考 hello bash 指令碼： https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh 造訪 hello 文件上的[toouse 自訂如何編寫指令碼動作](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)。</span><span class="sxs-lookup"><span data-stu-id="b6b45-126">hello bash script can be referenced from: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh Visit hello documentation on [how toouse custom script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   > [!NOTE]
   > <span data-ttu-id="b6b45-127">有兩個 python 安裝 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="b6b45-127">There are two python installations in hello cluster.</span></span> <span data-ttu-id="b6b45-128">Spark 會使用 hello Anaconda 的 python 安裝位於`/usr/bin/anaconda/bin`。</span><span class="sxs-lookup"><span data-stu-id="b6b45-128">Spark will use hello Anaconda python installation located at `/usr/bin/anaconda/bin`.</span></span> <span data-ttu-id="b6b45-129">在您的自訂動作中，透過 `/usr/bin/anaconda/bin/pip` 和 `/usr/bin/anaconda/bin/conda` 來參考該安裝。</span><span class="sxs-lookup"><span data-stu-id="b6b45-129">Reference that installation in your custom actions via `/usr/bin/anaconda/bin/pip` and `/usr/bin/anaconda/bin/conda`.</span></span>
   > 
   > 

3. <span data-ttu-id="b6b45-130">開啟 PySpark Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="b6b45-130">Open a PySpark Jupyter notebook</span></span>

    <span data-ttu-id="b6b45-131">![建立新的 Jupyter Notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "建立新的 Jupyter Notebook")</span><span class="sxs-lookup"><span data-stu-id="b6b45-131">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="b6b45-132">建立新的記事本，並開啟 hello 名稱 Untitled.pynb。</span><span class="sxs-lookup"><span data-stu-id="b6b45-132">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="b6b45-133">按一下頂端 hello hello 筆記本名稱並輸入好記的名稱。</span><span class="sxs-lookup"><span data-stu-id="b6b45-133">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="b6b45-134">![提供的名稱 hello 筆記本](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "提供 hello 筆記本的名稱")</span><span class="sxs-lookup"><span data-stu-id="b6b45-134">![Provide a name for hello notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Provide a name for hello notebook")</span></span>

5. <span data-ttu-id="b6b45-135">現在，您將 `import tensorflow` 並執行 hello world 範例。</span><span class="sxs-lookup"><span data-stu-id="b6b45-135">You will now `import tensorflow` and run a hello world example.</span></span> 

    <span data-ttu-id="b6b45-136">程式碼 toocopy:</span><span class="sxs-lookup"><span data-stu-id="b6b45-136">Code toocopy:</span></span>

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    <span data-ttu-id="b6b45-137">hello 結果看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="b6b45-137">hello result will look like this:</span></span>
    
    <span data-ttu-id="b6b45-138">![TensorFlow 程式碼執行](./media/hdinsight-apache-spark-python-package-installation/execution.png "執行 TensorFlow 程式碼")</span><span class="sxs-lookup"><span data-stu-id="b6b45-138">![TensorFlow code execution](./media/hdinsight-apache-spark-python-package-installation/execution.png "Execute TensorFlow code")</span></span>



## <span data-ttu-id="b6b45-139"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="b6b45-139"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="b6b45-140">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="b6b45-140">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="b6b45-141">案例</span><span class="sxs-lookup"><span data-stu-id="b6b45-141">Scenarios</span></span>
* [<span data-ttu-id="b6b45-142">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="b6b45-142">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="b6b45-143">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="b6b45-143">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="b6b45-144">機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark</span><span class="sxs-lookup"><span data-stu-id="b6b45-144">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="b6b45-145">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="b6b45-145">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="b6b45-146">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="b6b45-146">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="b6b45-147">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="b6b45-147">Create and run applications</span></span>
* [<span data-ttu-id="b6b45-148">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="b6b45-148">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="b6b45-149">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="b6b45-149">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="b6b45-150">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="b6b45-150">Tools and extensions</span></span>
* [<span data-ttu-id="b6b45-151">在 HDInsight 上的 Apache Spark 叢集中搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="b6b45-151">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="b6b45-152">HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="b6b45-152">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="b6b45-153">從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="b6b45-153">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="b6b45-154">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="b6b45-154">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="b6b45-155">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="b6b45-155">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="b6b45-156">在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="b6b45-156">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="b6b45-157">管理資源</span><span class="sxs-lookup"><span data-stu-id="b6b45-157">Manage resources</span></span>
* [<span data-ttu-id="b6b45-158">管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="b6b45-158">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="b6b45-159">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="b6b45-159">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
