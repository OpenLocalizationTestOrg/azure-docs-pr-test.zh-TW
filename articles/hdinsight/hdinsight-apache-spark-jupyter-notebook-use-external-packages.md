---
title: "使用 Azure HDInsight 上的 Spark 中 Jupyter aaaUse 自訂 Maven 套件 |Microsoft 文件"
description: "上如何 tooconfigure Jupyter 筆記本適用於 HDInsight Spark 叢集 toouse 自訂的 Maven 封裝的逐步指示。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ba8ac13716bc94ab082a18fe02d4a40b2f1e09e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="38cdb-103">在 HDInsight 上的 Apache Spark 叢集中搭配 Jupyter Notebook 使用外部封裝</span><span class="sxs-lookup"><span data-stu-id="38cdb-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="38cdb-104">使用資料格魔術</span><span class="sxs-lookup"><span data-stu-id="38cdb-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="38cdb-105">使用指令碼動作</span><span class="sxs-lookup"><span data-stu-id="38cdb-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="38cdb-106">了解如何 tooconfigure Jupyter 筆記本 HDInsight toouse 外部、 Apache Spark 叢集中社群貢獻**maven**不封裝在 hello 叢集中包含的方塊外。</span><span class="sxs-lookup"><span data-stu-id="38cdb-106">Learn how tooconfigure a Jupyter notebook in Apache Spark cluster on HDInsight toouse external, community-contributed **maven** packages that are not included out-of-the-box in hello cluster.</span></span> 

<span data-ttu-id="38cdb-107">您可以搜尋 hello [Maven 儲存機制](http://search.maven.org/)如 hello 的封裝所提供的完整清單。</span><span class="sxs-lookup"><span data-stu-id="38cdb-107">You can search hello [Maven repository](http://search.maven.org/) for hello complete list of packages that are available.</span></span> <span data-ttu-id="38cdb-108">您也可以從其他來源取得可用套件清單。</span><span class="sxs-lookup"><span data-stu-id="38cdb-108">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="38cdb-109">例如，從 [Spark 套件](http://spark-packages.org/)可以取得社群提供套件的完整清單。</span><span class="sxs-lookup"><span data-stu-id="38cdb-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="38cdb-110">在本文中，您將學習如何 toouse hello [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar)與 hello Jupyter 筆記本的封裝。</span><span class="sxs-lookup"><span data-stu-id="38cdb-110">In this article, you will learn how toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with hello Jupyter notebook.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="38cdb-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="38cdb-111">Prerequisites</span></span>
<span data-ttu-id="38cdb-112">您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="38cdb-112">You must have hello following:</span></span>

* <span data-ttu-id="38cdb-113">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="38cdb-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="38cdb-114">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="38cdb-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="38cdb-115">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="38cdb-115">Use external packages with Jupyter notebooks</span></span>
1. <span data-ttu-id="38cdb-116">從 hello [Azure 入口網站](https://portal.azure.com/)，從 hello 開始面板中，按一下 Spark 叢集中的 hello 磚 （如果您釘選它 toohello 開始面板）。</span><span class="sxs-lookup"><span data-stu-id="38cdb-116">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="38cdb-117">您也可以導覽 tooyour 叢集下的**瀏覽所有** > **HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="38cdb-117">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="38cdb-118">從 hello Spark 叢集刀鋒視窗中，按一下 **快速連結**，然後從 hello**叢集儀表板**刀鋒視窗中，按一下  **Jupyter 筆記本**。</span><span class="sxs-lookup"><span data-stu-id="38cdb-118">From hello Spark cluster blade, click **Quick Links**, and then from hello **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="38cdb-119">如果出現提示，請輸入 hello 叢集 hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="38cdb-119">If prompted, enter hello admin credentials for hello cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="38cdb-120">您也可能由下列 URL 在瀏覽器中開啟 hello 叢集到達 hello Jupyter 筆記本。</span><span class="sxs-lookup"><span data-stu-id="38cdb-120">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="38cdb-121">取代**CLUSTERNAME** hello 名稱，為您的叢集：</span><span class="sxs-lookup"><span data-stu-id="38cdb-121">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. <span data-ttu-id="38cdb-122">建立新的 Notebook。</span><span class="sxs-lookup"><span data-stu-id="38cdb-122">Create a new notebook.</span></span> <span data-ttu-id="38cdb-123">按一下 新增，然後按一下Spark。</span><span class="sxs-lookup"><span data-stu-id="38cdb-123">Click **New**, and then click **Spark**.</span></span>
   
    <span data-ttu-id="38cdb-124">![建立新的 Jupyter Notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "建立新的 Jupyter Notebook")</span><span class="sxs-lookup"><span data-stu-id="38cdb-124">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="38cdb-125">建立新的記事本，並開啟 hello 名稱 Untitled.pynb。</span><span class="sxs-lookup"><span data-stu-id="38cdb-125">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="38cdb-126">按一下頂端 hello hello 筆記本名稱並輸入好記的名稱。</span><span class="sxs-lookup"><span data-stu-id="38cdb-126">Click hello notebook name at hello top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="38cdb-127">![提供的名稱 hello 筆記本](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "提供 hello 筆記本的名稱")</span><span class="sxs-lookup"><span data-stu-id="38cdb-127">![Provide a name for hello notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Provide a name for hello notebook")</span></span>

5. <span data-ttu-id="38cdb-128">您將使用 hello `%%configure` magic tooconfigure hello 筆記本 toouse 外部的封裝。</span><span class="sxs-lookup"><span data-stu-id="38cdb-128">You will use hello `%%configure` magic tooconfigure hello notebook toouse an external package.</span></span> <span data-ttu-id="38cdb-129">在使用外部封裝的筆記型電腦，請確定呼叫 hello `%%configure` magic hello 第一個程式碼的資料格。</span><span class="sxs-lookup"><span data-stu-id="38cdb-129">In notebooks that use external packages, make sure you call hello `%%configure` magic in hello first code cell.</span></span> <span data-ttu-id="38cdb-130">這可確保該 hello 核心設定的 toouse hello 套件 hello 工作階段開始之前。</span><span class="sxs-lookup"><span data-stu-id="38cdb-130">This ensures that hello kernel is configured toouse hello package before hello session starts.</span></span>

    >[!IMPORTANT] 
    ><span data-ttu-id="38cdb-131">如果您忘記 tooconfigure hello 核心 hello 第一個資料格，您可以使用 hello`%%configure`以 hello`-f`參數，但會重新啟動 hello 工作階段，並將遺失所有的進度。</span><span class="sxs-lookup"><span data-stu-id="38cdb-131">If you forget tooconfigure hello kernel in hello first cell, you can use hello `%%configure` with hello `-f` parameter, but that will restart hello session and all progress will be lost.</span></span>

    | <span data-ttu-id="38cdb-132">HDInsight 版本</span><span class="sxs-lookup"><span data-stu-id="38cdb-132">HDInsight version</span></span> | <span data-ttu-id="38cdb-133">命令</span><span class="sxs-lookup"><span data-stu-id="38cdb-133">Command</span></span> |
    |-------------------|---------|
    |<span data-ttu-id="38cdb-134">HDInsight 3.3 和 HDInsight 3.4</span><span class="sxs-lookup"><span data-stu-id="38cdb-134">For HDInsight 3.3 and HDInsight 3.4</span></span> | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | <span data-ttu-id="38cdb-135">HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="38cdb-135">For HDInsight 3.5</span></span> | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. <span data-ttu-id="38cdb-136">上述的 hello 片段預期 hello Maven 中央儲存機制中的外部封裝 hello maven 座標。</span><span class="sxs-lookup"><span data-stu-id="38cdb-136">hello snippet above expects hello maven coordinates for hello external package in Maven Central Repository.</span></span> <span data-ttu-id="38cdb-137">在此程式碼片段，`com.databricks:spark-csv_2.10:1.4.0`是 hello maven 座標**spark csv**封裝。</span><span class="sxs-lookup"><span data-stu-id="38cdb-137">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is hello maven coordinate for **spark-csv** package.</span></span> <span data-ttu-id="38cdb-138">以下是您如何建立封裝的 hello 座標。</span><span class="sxs-lookup"><span data-stu-id="38cdb-138">Here's how you construct hello coordinates for a package.</span></span>
   
    <span data-ttu-id="38cdb-139">a.</span><span class="sxs-lookup"><span data-stu-id="38cdb-139">a.</span></span> <span data-ttu-id="38cdb-140">在 hello Maven 儲存機制中，找出 hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="38cdb-140">Locate hello package in hello Maven Repository.</span></span> <span data-ttu-id="38cdb-141">針對本教學課程，我們使用 [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar)。</span><span class="sxs-lookup"><span data-stu-id="38cdb-141">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="38cdb-142">b.</span><span class="sxs-lookup"><span data-stu-id="38cdb-142">b.</span></span> <span data-ttu-id="38cdb-143">從 hello 儲存機制，蒐集 hello 值**GroupId**， **ArtifactId**，和**版本**。</span><span class="sxs-lookup"><span data-stu-id="38cdb-143">From hello repository, gather hello values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="38cdb-144">請確定您所收集的 hello 值符合您的叢集。</span><span class="sxs-lookup"><span data-stu-id="38cdb-144">Make sure that hello values you gather match your cluster.</span></span> <span data-ttu-id="38cdb-145">在此情況下，我們使用的是 Scala 2.10 和 Spark 1.4.0 封裝，但您可能 hello 適當 Scala 或 Spark 版本需要 tooselect 不同版本，在您的叢集。</span><span class="sxs-lookup"><span data-stu-id="38cdb-145">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need tooselect different versions for hello appropriate Scala or Spark version in your cluster.</span></span> <span data-ttu-id="38cdb-146">您可以找出 hello Scala 版本在叢集上執行`scala.util.Properties.versionString`或 Spark 送出 hello Spark Jupyter 核心上。</span><span class="sxs-lookup"><span data-stu-id="38cdb-146">You can find out hello Scala version on your cluster by running `scala.util.Properties.versionString` on hello Spark Jupyter kernel or on Spark submit.</span></span> <span data-ttu-id="38cdb-147">您可以找出 hello Spark 版本在叢集上執行`sc.version`Jupyter 筆記本上。</span><span class="sxs-lookup"><span data-stu-id="38cdb-147">You can find out hello Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span></span>
   
    <span data-ttu-id="38cdb-148">![搭配 Jupyter Notebook 使用外部封裝](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "搭配 Jupyter Notebook 使用外部封裝")</span><span class="sxs-lookup"><span data-stu-id="38cdb-148">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="38cdb-149">c.</span><span class="sxs-lookup"><span data-stu-id="38cdb-149">c.</span></span> <span data-ttu-id="38cdb-150">串連 hello 三個值，並以分號 (**:**)。</span><span class="sxs-lookup"><span data-stu-id="38cdb-150">Concatenate hello three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

7. <span data-ttu-id="38cdb-151">執行 hello 程式碼的儲存格以 hello`%%configure`識別常數。</span><span class="sxs-lookup"><span data-stu-id="38cdb-151">Run hello code cell with hello `%%configure` magic.</span></span> <span data-ttu-id="38cdb-152">這會設定 hello 基礎晚總工作階段 toouse hello 您提供的封裝。</span><span class="sxs-lookup"><span data-stu-id="38cdb-152">This will configure hello underlying Livy session toouse hello package you provided.</span></span> <span data-ttu-id="38cdb-153">在儲存格中 hello 後續 hello 筆記本，您現在可以使用 hello 封裝，如下所示。</span><span class="sxs-lookup"><span data-stu-id="38cdb-153">In hello subsequent cells in hello notebook, you can now use hello package, as shown below.</span></span>
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. <span data-ttu-id="38cdb-154">然後，您可以執行 hello 程式碼片段，類似如下所示，tooview hello hello 資料框架的資料建立 hello 上一個步驟中。</span><span class="sxs-lookup"><span data-stu-id="38cdb-154">You can then run hello snippets, like shown below, tooview hello data from hello dataframe you created in hello previous step.</span></span>
   
        df.show()
   
        df.select("Time").count()

## <span data-ttu-id="38cdb-155"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="38cdb-155"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="38cdb-156">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="38cdb-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="38cdb-157">案例</span><span class="sxs-lookup"><span data-stu-id="38cdb-157">Scenarios</span></span>
* [<span data-ttu-id="38cdb-158">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="38cdb-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="38cdb-159">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="38cdb-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="38cdb-160">機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark</span><span class="sxs-lookup"><span data-stu-id="38cdb-160">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="38cdb-161">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="38cdb-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="38cdb-162">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="38cdb-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="38cdb-163">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="38cdb-163">Create and run applications</span></span>
* [<span data-ttu-id="38cdb-164">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="38cdb-164">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="38cdb-165">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="38cdb-165">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="38cdb-166">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="38cdb-166">Tools and extensions</span></span>

* [<span data-ttu-id="38cdb-167">在 HDInsight Linux 上的 Apache Spark 叢集中搭配 Jupyter Notebook 使用外部 Python 套件</span><span class="sxs-lookup"><span data-stu-id="38cdb-167">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span></span>](hdinsight-apache-spark-python-package-installation.md)
* [<span data-ttu-id="38cdb-168">HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="38cdb-168">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="38cdb-169">從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="38cdb-169">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="38cdb-170">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="38cdb-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="38cdb-171">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="38cdb-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="38cdb-172">在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="38cdb-172">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="38cdb-173">管理資源</span><span class="sxs-lookup"><span data-stu-id="38cdb-173">Manage resources</span></span>
* [<span data-ttu-id="38cdb-174">管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="38cdb-174">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="38cdb-175">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="38cdb-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

