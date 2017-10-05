---
title: "在 Azure HDInsight 上的 Spark 中搭配 Jupyter 使用自訂 Maven 套件 | Microsoft Docs"
description: "說明如何設定讓 HDInsight Spark 叢集隨附之 Jupyter Notebook 使用自訂 Maven 套件的逐步指示。"
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
ms.openlocfilehash: 0bcfe220e60e34937c667c7b416065d5f3dc8d63
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a><span data-ttu-id="12887-103">在 HDInsight 上的 Apache Spark 叢集中搭配 Jupyter Notebook 使用外部封裝</span><span class="sxs-lookup"><span data-stu-id="12887-103">Use external packages with Jupyter notebooks in Apache Spark clusters on HDInsight</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="12887-104">使用資料格魔術</span><span class="sxs-lookup"><span data-stu-id="12887-104">Using cell magic</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [<span data-ttu-id="12887-105">使用指令碼動作</span><span class="sxs-lookup"><span data-stu-id="12887-105">Using Script Action</span></span>](hdinsight-apache-spark-python-package-installation.md)
>
>

<span data-ttu-id="12887-106">了解如何在 HDInsight 上的 Apache Spark 叢集中，將 Jupyter Notebook 設定為使用外部、社群提供的 **maven** 封裝 (不是叢集中現成的)。</span><span class="sxs-lookup"><span data-stu-id="12887-106">Learn how to configure a Jupyter notebook in Apache Spark cluster on HDInsight to use external, community-contributed **maven** packages that are not included out-of-the-box in the cluster.</span></span> 

<span data-ttu-id="12887-107">您可以搜尋 [Maven 儲存機制](http://search.maven.org/) 來取得可用套件的完整清單。</span><span class="sxs-lookup"><span data-stu-id="12887-107">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="12887-108">您也可以從其他來源取得可用套件清單。</span><span class="sxs-lookup"><span data-stu-id="12887-108">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="12887-109">例如，從 [Spark 套件](http://spark-packages.org/)可以取得社群提供套件的完整清單。</span><span class="sxs-lookup"><span data-stu-id="12887-109">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="12887-110">在這篇文章中，您將了解如何搭配 Jupyter Notebook 使用 [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) 套件。</span><span class="sxs-lookup"><span data-stu-id="12887-110">In this article, you will learn how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="12887-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="12887-111">Prerequisites</span></span>
<span data-ttu-id="12887-112">您必須滿足以下條件：</span><span class="sxs-lookup"><span data-stu-id="12887-112">You must have the following:</span></span>

* <span data-ttu-id="12887-113">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="12887-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="12887-114">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="12887-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="use-external-packages-with-jupyter-notebooks"></a><span data-ttu-id="12887-115">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="12887-115">Use external packages with Jupyter notebooks</span></span>
1. <span data-ttu-id="12887-116">在 [Azure 入口網站](https://portal.azure.com/)的開始面板中，按一下您的 Spark 叢集磚 (如果您已將其釘選到開始面板)。</span><span class="sxs-lookup"><span data-stu-id="12887-116">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="12887-117">您也可以按一下 [瀏覽全部] > [HDInsight 叢集] 來瀏覽至您的叢集。</span><span class="sxs-lookup"><span data-stu-id="12887-117">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="12887-118">在 Spark 叢集刀鋒視窗中按一下 [快速連結]，然後在 [叢集儀表板] 刀鋒視窗中按一下 [Jupyter Notebook]。</span><span class="sxs-lookup"><span data-stu-id="12887-118">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="12887-119">出現提示時，輸入叢集的系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="12887-119">If prompted, enter the admin credentials for the cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="12887-120">您也可以在瀏覽器中開啟下列 URL，來連接到您的叢集的 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="12887-120">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="12887-121">使用您叢集的名稱取代 **CLUSTERNAME** ：</span><span class="sxs-lookup"><span data-stu-id="12887-121">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. <span data-ttu-id="12887-122">建立新的 Notebook。</span><span class="sxs-lookup"><span data-stu-id="12887-122">Create a new notebook.</span></span> <span data-ttu-id="12887-123">按一下 [新增]，然後按一下 [Spark]。</span><span class="sxs-lookup"><span data-stu-id="12887-123">Click **New**, and then click **Spark**.</span></span>
   
    <span data-ttu-id="12887-124">![建立新的 Jupyter Notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "建立新的 Jupyter Notebook")</span><span class="sxs-lookup"><span data-stu-id="12887-124">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="12887-125">系統隨即會建立新 Notebook，並以 Untitled.pynb 的名稱開啟。</span><span class="sxs-lookup"><span data-stu-id="12887-125">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="12887-126">在頂端按一下 Notebook 名稱，然後輸入好記的名稱。</span><span class="sxs-lookup"><span data-stu-id="12887-126">Click the notebook name at the top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="12887-127">![提供 Notebook 的名稱](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "提供 Notebook 的名稱")</span><span class="sxs-lookup"><span data-stu-id="12887-127">![Provide a name for the notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Provide a name for the notebook")</span></span>

5. <span data-ttu-id="12887-128">您將使用 `%%configure` magic 來設定讓 Notebook 使用外部套件。</span><span class="sxs-lookup"><span data-stu-id="12887-128">You will use the `%%configure` magic to configure the notebook to use an external package.</span></span> <span data-ttu-id="12887-129">在使用外部套件的 Notebook 中，確定您在第一個程式碼單元中呼叫 `%%configure` magic。</span><span class="sxs-lookup"><span data-stu-id="12887-129">In notebooks that use external packages, make sure you call the `%%configure` magic in the first code cell.</span></span> <span data-ttu-id="12887-130">這可確保將核心設定為在啟動工作階段之前即使用此套件。</span><span class="sxs-lookup"><span data-stu-id="12887-130">This ensures that the kernel is configured to use the package before the session starts.</span></span>

    >[!IMPORTANT] 
    ><span data-ttu-id="12887-131">如果您忘記在第一個單元中設定核心，您可以搭配 `-f` 參數使用 `%%configure`，但這會重新啟動工作階段，而所有進度都將遺失。</span><span class="sxs-lookup"><span data-stu-id="12887-131">If you forget to configure the kernel in the first cell, you can use the `%%configure` with the `-f` parameter, but that will restart the session and all progress will be lost.</span></span>

    | <span data-ttu-id="12887-132">HDInsight 版本</span><span class="sxs-lookup"><span data-stu-id="12887-132">HDInsight version</span></span> | <span data-ttu-id="12887-133">命令</span><span class="sxs-lookup"><span data-stu-id="12887-133">Command</span></span> |
    |-------------------|---------|
    |<span data-ttu-id="12887-134">HDInsight 3.3 和 HDInsight 3.4</span><span class="sxs-lookup"><span data-stu-id="12887-134">For HDInsight 3.3 and HDInsight 3.4</span></span> | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | <span data-ttu-id="12887-135">HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="12887-135">For HDInsight 3.5</span></span> | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. <span data-ttu-id="12887-136">對於 Maven 中央儲存機制中的外部套件，上述程式碼片段預期會使用 Maven 座標。</span><span class="sxs-lookup"><span data-stu-id="12887-136">The snippet above expects the maven coordinates for the external package in Maven Central Repository.</span></span> <span data-ttu-id="12887-137">在此程式碼片段中， `com.databricks:spark-csv_2.10:1.4.0` 是 **spark-csv** 套件的 maven 座標。</span><span class="sxs-lookup"><span data-stu-id="12887-137">In this snippet, `com.databricks:spark-csv_2.10:1.4.0` is the maven coordinate for **spark-csv** package.</span></span> <span data-ttu-id="12887-138">以下說明如何建立套件的座標。</span><span class="sxs-lookup"><span data-stu-id="12887-138">Here's how you construct the coordinates for a package.</span></span>
   
    <span data-ttu-id="12887-139">a.</span><span class="sxs-lookup"><span data-stu-id="12887-139">a.</span></span> <span data-ttu-id="12887-140">在「Maven 儲存機制」中找出套件。</span><span class="sxs-lookup"><span data-stu-id="12887-140">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="12887-141">針對本教學課程，我們使用 [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar)。</span><span class="sxs-lookup"><span data-stu-id="12887-141">For this tutorial, we use [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="12887-142">b.</span><span class="sxs-lookup"><span data-stu-id="12887-142">b.</span></span> <span data-ttu-id="12887-143">從儲存機制收集 [GroupId]、[ArtifactId] 及 [版本] 的值。</span><span class="sxs-lookup"><span data-stu-id="12887-143">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="12887-144">確定您收集的值符合您的叢集。</span><span class="sxs-lookup"><span data-stu-id="12887-144">Make sure that the values you gather match your cluster.</span></span> <span data-ttu-id="12887-145">在此案例中，我們使用 Scala 2.10 與 Spark 1.4.0 套件，但您可能必須為叢集中的適當 Scala 或 Spark 版本選取不同的版本。</span><span class="sxs-lookup"><span data-stu-id="12887-145">In this case, we are using a Scala 2.10 and Spark 1.4.0 package, but you may need to select different versions for the appropriate Scala or Spark version in your cluster.</span></span> <span data-ttu-id="12887-146">您可以透過在 Spark Jupyter 核心或 Spark 提交上執行 `scala.util.Properties.versionString` 以查看您叢集上的 Scala 版本。</span><span class="sxs-lookup"><span data-stu-id="12887-146">You can find out the Scala version on your cluster by running `scala.util.Properties.versionString` on the Spark Jupyter kernel or on Spark submit.</span></span> <span data-ttu-id="12887-147">您可以透過在 Jupyter 筆記本上執行 `sc.version` 以查看您叢集上的 Spark 版本。</span><span class="sxs-lookup"><span data-stu-id="12887-147">You can find out the Spark version on your cluster by running `sc.version` on Jupyter notebooks.</span></span>
   
    <span data-ttu-id="12887-148">![搭配 Jupyter Notebook 使用外部封裝](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "搭配 Jupyter Notebook 使用外部封裝")</span><span class="sxs-lookup"><span data-stu-id="12887-148">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="12887-149">c.</span><span class="sxs-lookup"><span data-stu-id="12887-149">c.</span></span> <span data-ttu-id="12887-150">串連三個值，其中以冒號分隔 (**:**)。</span><span class="sxs-lookup"><span data-stu-id="12887-150">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

7. <span data-ttu-id="12887-151">以 `%%configure` magic 執行程式碼單元。</span><span class="sxs-lookup"><span data-stu-id="12887-151">Run the code cell with the `%%configure` magic.</span></span> <span data-ttu-id="12887-152">這會將基礎 Livy 工作階段設定為使用您提供的套件。</span><span class="sxs-lookup"><span data-stu-id="12887-152">This will configure the underlying Livy session to use the package you provided.</span></span> <span data-ttu-id="12887-153">在 Notebook 的後續單元中，您現在已可以使用套件，如以下所示。</span><span class="sxs-lookup"><span data-stu-id="12887-153">In the subsequent cells in the notebook, you can now use the package, as shown below.</span></span>
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. <span data-ttu-id="12887-154">接著，您可以執行程式碼片段 (如以下所示) 以檢視來自您在上一個步驟中所建立之資料框架的資料。</span><span class="sxs-lookup"><span data-stu-id="12887-154">You can then run the snippets, like shown below, to view the data from the dataframe you created in the previous step.</span></span>
   
        df.show()
   
        df.select("Time").count()

## <span data-ttu-id="12887-155"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="12887-155"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="12887-156">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="12887-156">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="12887-157">案例</span><span class="sxs-lookup"><span data-stu-id="12887-157">Scenarios</span></span>
* [<span data-ttu-id="12887-158">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="12887-158">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="12887-159">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="12887-159">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="12887-160">Spark 和機器學習服務：使用 HDInsight 中的 Spark 來預測食品檢查結果</span><span class="sxs-lookup"><span data-stu-id="12887-160">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="12887-161">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="12887-161">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="12887-162">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="12887-162">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="12887-163">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="12887-163">Create and run applications</span></span>
* [<span data-ttu-id="12887-164">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="12887-164">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="12887-165">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="12887-165">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="12887-166">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="12887-166">Tools and extensions</span></span>

* [<span data-ttu-id="12887-167">在 HDInsight Linux 上的 Apache Spark 叢集中搭配 Jupyter Notebook 使用外部 Python 套件</span><span class="sxs-lookup"><span data-stu-id="12887-167">Use external python packages with Jupyter notebooks in Apache Spark clusters on HDInsight Linux</span></span>](hdinsight-apache-spark-python-package-installation.md)
* [<span data-ttu-id="12887-168">使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式來建立和提交 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="12887-168">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="12887-169">使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式遠端偵錯 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="12887-169">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="12887-170">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="12887-170">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="12887-171">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="12887-171">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="12887-172">在電腦上安裝 Jupyter 並連接到 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="12887-172">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="12887-173">管理資源</span><span class="sxs-lookup"><span data-stu-id="12887-173">Manage resources</span></span>
* [<span data-ttu-id="12887-174">在 Azure HDInsight 中管理 Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="12887-174">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="12887-175">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="12887-175">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

