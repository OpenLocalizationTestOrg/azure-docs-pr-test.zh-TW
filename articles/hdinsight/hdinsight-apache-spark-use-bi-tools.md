---
title: "在 Azure HDInsight 上使用資料視覺效果工具的 Spark BI | Microsoft Docs"
description: "透過 HDInsight 叢集上的 Apache Spark BI 使用分析的資料視覺效果工具"
keywords: "apache spark bi, spark bi, spark 資料視覺效果, spark 商業智慧"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1448b536-9bc8-46bc-bbc6-d7001623642a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 49dd161049ac442081fe6d26cf8bd3a56a2e0687
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a><span data-ttu-id="be87d-104">使用資料視覺效果工具搭配 Azure HDInsight 的 Apache Spark BI</span><span class="sxs-lookup"><span data-stu-id="be87d-104">Apache Spark BI using data visualization tools with Azure HDInsight</span></span>

<span data-ttu-id="be87d-105">了解如何使用諸如 Power BI 和 Tableau 等資料視覺效果工具，運用 HDInsight 叢集上的 Apache Spark BI 來分析原始範例資料集。</span><span class="sxs-lookup"><span data-stu-id="be87d-105">Learn how to use data visualization tools such as Power BI and Tableau to analyze a raw sample data set using Apache Spark BI on HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="be87d-106">Azure HDInsight 3.6 預覽版的 Spark 2.1 不支援本文所述的 BI 工具連接性。</span><span class="sxs-lookup"><span data-stu-id="be87d-106">Connectivity with BI tools described in this article is not supported on Spark 2.1 on Azure HDInsight 3.6 Preview.</span></span> <span data-ttu-id="be87d-107">僅支援 Spark 1.6 版和 2.0 版 (分別是 HDInsight 3.4 版和 3.5 版)。</span><span class="sxs-lookup"><span data-stu-id="be87d-107">Only Spark versions 1.6 and 2.0 (HDInsight 3.4, 3.5 respectively) are supported.</span></span>
>

<span data-ttu-id="be87d-108">本教學課程也可在 HDInsight Spark 叢集上用來作為 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="be87d-108">This tutorial is also available as a Jupyter notebook on an HDInsight Spark cluster.</span></span> <span data-ttu-id="be87d-109">Notebook 的體驗能讓您從 Notebook 本身執行 Python 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="be87d-109">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="be87d-110">如要從 Notebook 中執行本教學課程，請建立 Spark 叢集、啟動 Jupyter Notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`)，然後執行 **Python** 資料夾中的 Notebook [搭配 HDInsight.ipynb 上的 Apache Spark 來使用 BI 工具]。</span><span class="sxs-lookup"><span data-stu-id="be87d-110">To perform the tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run the notebook **Use BI tools with Apache Spark on HDInsight.ipynb** under the **Python** folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be87d-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="be87d-111">Prerequisites</span></span>

* <span data-ttu-id="be87d-112">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="be87d-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="be87d-113">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="be87d-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>


## <span data-ttu-id="be87d-114"><a name="hivetable"></a>準備 Spark 資料視覺效果的資料</span><span class="sxs-lookup"><span data-stu-id="be87d-114"><a name="hivetable"></a>Prepare data for Spark data visualization</span></span>

<span data-ttu-id="be87d-115">在本節中，我們會使用 HDInsight Spark 叢集中的 [Jupyter](https://jupyter.org) Notebook，執行可處理未經處理範例資料並將這些資料儲存成資料表的工作。</span><span class="sxs-lookup"><span data-stu-id="be87d-115">In this section, we use the [Jupyter](https://jupyter.org) notebook from an HDInsight Spark cluster to run jobs that process your raw sample data and save it as a table.</span></span> <span data-ttu-id="be87d-116">範例資料是所有叢集在預設情況下均有的 .csv 檔案 (hvac.csv)。</span><span class="sxs-lookup"><span data-stu-id="be87d-116">The sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span> <span data-ttu-id="be87d-117">將資料儲存為資料表後，下一節我們將使用 BI 工具連線到資料表，並執行資料視覺效果。</span><span class="sxs-lookup"><span data-stu-id="be87d-117">Once your data is saved as a table, in the next section we use BI tools to connect to the table and perform data visualizations.</span></span>

> [!NOTE]
> <span data-ttu-id="be87d-118">如果您是在完成[在 HDInsight Spark 叢集上執行互動式查詢](hdinsight-apache-spark-load-data-run-query.md)中的指示之後執行本文中的步驟，即可跳到下面的步驟 8。</span><span class="sxs-lookup"><span data-stu-id="be87d-118">If you are performing the steps in this article after completing the instructions in [Run interactive queries on an HDInsight Spark cluster](hdinsight-apache-spark-load-data-run-query.md), you can skip to Step 8 below.</span></span>
>

1. <span data-ttu-id="be87d-119">在 [Azure 入口網站](https://portal.azure.com/)的開始面板中，按一下您的 Spark 叢集格圖格 (如果您已將其釘選到開始面板)。</span><span class="sxs-lookup"><span data-stu-id="be87d-119">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="be87d-120">您也可以按一下 [瀏覽全部] > [HDInsight 叢集] 來瀏覽至您的叢集。</span><span class="sxs-lookup"><span data-stu-id="be87d-120">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="be87d-121">從 Spark 叢集刀鋒視窗按一下 [叢集儀表板]，然後按一下 [Jupyter Notebook]。</span><span class="sxs-lookup"><span data-stu-id="be87d-121">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="be87d-122">出現提示時，輸入叢集的系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="be87d-122">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="be87d-123">您也可以在瀏覽器中開啟下列 URL，來連接到您的叢集的 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="be87d-123">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="be87d-124">使用您叢集的名稱取代 **CLUSTERNAME** ：</span><span class="sxs-lookup"><span data-stu-id="be87d-124">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="be87d-125">建立 Notebook。</span><span class="sxs-lookup"><span data-stu-id="be87d-125">Create a notebook.</span></span> <span data-ttu-id="be87d-126">按一下 [新增]，然後按一下 [PySpark]。</span><span class="sxs-lookup"><span data-stu-id="be87d-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="be87d-127">![建立 Apache Spark BI 的 Jupyter Notebook](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "建立 Apache Spark BI 的 Jupyter Notebook")</span><span class="sxs-lookup"><span data-stu-id="be87d-127">![Create a Jupyter notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Create a Jupyter notebook for Apache Spark BI")</span></span>

4. <span data-ttu-id="be87d-128">系統隨即會建立新 Notebook，並以 Untitled.pynb 的名稱開啟。</span><span class="sxs-lookup"><span data-stu-id="be87d-128">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="be87d-129">在頂端按一下 Notebook 名稱，然後輸入好記的名稱。</span><span class="sxs-lookup"><span data-stu-id="be87d-129">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="be87d-130">![提供 Apache Spark BI Notebook 的名稱](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "提供 Apache Spark BI Notebook 的名稱")</span><span class="sxs-lookup"><span data-stu-id="be87d-130">![Provide a name for the notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Provide a name for the notebook for Apache Spark BI")</span></span>

5. <span data-ttu-id="be87d-131">您使用 PySpark 核心建立 Notebook，因此不需要明確建立任何內容。</span><span class="sxs-lookup"><span data-stu-id="be87d-131">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="be87d-132">當您執行第一個程式碼儲存格時，系統會自動為您建立 Spark 和 Hive 內容。</span><span class="sxs-lookup"><span data-stu-id="be87d-132">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="be87d-133">首先，您可以匯入此案例所需的類型。</span><span class="sxs-lookup"><span data-stu-id="be87d-133">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="be87d-134">若要這樣做，請將游標放在儲存格中，然後按 **SHIFT + ENTER**鍵。</span><span class="sxs-lookup"><span data-stu-id="be87d-134">To do so, place the cursor in the cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import *

6. <span data-ttu-id="be87d-135">將範例資料載入暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="be87d-135">Load sample data into a temporary table.</span></span> <span data-ttu-id="be87d-136">當您在 HDInsight 中建立 Spark 叢集時，系統會將範例資料檔案 **hvac.csv** 複製到相關聯的儲存體帳戶中 (位於 **\HdiSamples\HdiSamples\SensorSampleData\hvac**)。</span><span class="sxs-lookup"><span data-stu-id="be87d-136">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span>

    <span data-ttu-id="be87d-137">將下列程式碼片段貼到空白儲存格中，然後按下 **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="be87d-137">In an empty cell, paste the following snippet and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="be87d-138">此程式碼片段會將資料註冊到名為 **hvac** 的資料表中。</span><span class="sxs-lookup"><span data-stu-id="be87d-138">This snippet registers the data into a table called **hvac**.</span></span>

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse the data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))

        # Infer the schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. <span data-ttu-id="be87d-139">確認資料表已成功建立。</span><span class="sxs-lookup"><span data-stu-id="be87d-139">Verify that the table was successfully created.</span></span> <span data-ttu-id="be87d-140">您可以使用 `%%sql` magic 直接執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="be87d-140">You can use the `%%sql` magic to run Hive queries directly.</span></span> <span data-ttu-id="be87d-141">如需 `%%sql` magic 及 PySpark 核心提供的其他 magic 的詳細資訊，請參閱 [使用 Spark HDInsight 叢集之 Jupyter Notebook 上可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)。</span><span class="sxs-lookup"><span data-stu-id="be87d-141">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SHOW TABLES

    <span data-ttu-id="be87d-142">您會看到如下所示的輸出：</span><span class="sxs-lookup"><span data-stu-id="be87d-142">You see an output like shown below:</span></span>

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    <span data-ttu-id="be87d-143">只有 **isTemporary** 資料行為 false 的資料表會儲存在中繼存放區，並可以從 BI 工具存取的 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="be87d-143">Only the tables that have false under the **isTemporary** column are hive tables that are stored in the metastore and can be accessed from the BI tools.</span></span> <span data-ttu-id="be87d-144">在此教學課程中，我們會連線到我們所建立的 **hvac** 資料表。</span><span class="sxs-lookup"><span data-stu-id="be87d-144">In this tutorial, we connect to the **hvac** table we created.</span></span>

8. <span data-ttu-id="be87d-145">請確認資料表包含預期的資料。</span><span class="sxs-lookup"><span data-stu-id="be87d-145">Verify that the table contains the intended data.</span></span> <span data-ttu-id="be87d-146">將下列程式碼片段貼到 Notebook 的空白儲存格中，然後按下 **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="be87d-146">In an empty cell in the notebook, copy the following snippet and press **SHIFT + ENTER**.</span></span>

        %%sql
        SELECT * FROM hvac LIMIT 10

9. <span data-ttu-id="be87d-147">關閉 Notebook 來釋放資源。</span><span class="sxs-lookup"><span data-stu-id="be87d-147">Shut down the notebook to release the resources.</span></span> <span data-ttu-id="be87d-148">若要這樣做，請從 Notebook 的 [檔案] 功能表中，按一下 [關閉並停止]。</span><span class="sxs-lookup"><span data-stu-id="be87d-148">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

## <span data-ttu-id="be87d-149"><a name="powerbi"></a>使用 Spark 資料視覺效果的 Power BI</span><span class="sxs-lookup"><span data-stu-id="be87d-149"><a name="powerbi"></a>Use Power BI for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="be87d-150">本節只適用於 HDInsight 3.4 上的 Spark 1.6 以及 HDInsight 3.5 上的 Spark 2.0。</span><span class="sxs-lookup"><span data-stu-id="be87d-150">This section is applicable only for Spark 1.6 on HDInsight 3.4 and Spark 2.0 on HDInsight 3.5.</span></span>
>
>

<span data-ttu-id="be87d-151">將資料儲存成資料表後，您可以使用 Power BI 來連線資料並以視覺化方式呈現，以便建立報表、儀表板等。</span><span class="sxs-lookup"><span data-stu-id="be87d-151">Once you have saved the data as a table, you can use Power BI to connect to the data and visualize it to create reports, dashboards, etc.</span></span>

1. <span data-ttu-id="be87d-152">確定您可存取 Power BI。</span><span class="sxs-lookup"><span data-stu-id="be87d-152">Make sure you have access to Power BI.</span></span> <span data-ttu-id="be87d-153">您可以從 [http://www.powerbi.com/](http://www.powerbi.com/)取得 Power BI 的免費預覽版訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="be87d-153">You can get a free preview subscription of Power BI from [http://www.powerbi.com/](http://www.powerbi.com/).</span></span>

2. <span data-ttu-id="be87d-154">登入 [Power BI](http://www.powerbi.com/)。</span><span class="sxs-lookup"><span data-stu-id="be87d-154">Sign in to [Power BI](http://www.powerbi.com/).</span></span>

3. <span data-ttu-id="be87d-155">從左窗格底部，按一下 [取得資料]。</span><span class="sxs-lookup"><span data-stu-id="be87d-155">From the bottom of the left pane, click **Get Data**.</span></span>

4. <span data-ttu-id="be87d-156">在 [取得資料] 頁面的 [匯入或連線至資料] 之下，針對 [資料庫] 按一下 [取得]。</span><span class="sxs-lookup"><span data-stu-id="be87d-156">On the **Get Data** page, under **Import or Connect to Data**, for **Databases**, click **Get**.</span></span>

    <span data-ttu-id="be87d-157">![將資料送入 Apache Spark BI 的 Power BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "將資料送入 Apache Spark BI 的 Power BI")</span><span class="sxs-lookup"><span data-stu-id="be87d-157">![Get data into Power BI for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Get data into Power BI for Apache Spark BI")</span></span>

5. <span data-ttu-id="be87d-158">在下一個畫面中，按一下 [Azure HDInsight 上的 Spark]，然後按一下 [連線]。</span><span class="sxs-lookup"><span data-stu-id="be87d-158">On the next screen, click **Spark on Azure HDInsight** and then click **Connect**.</span></span> <span data-ttu-id="be87d-159">在畫面出現提示時，輸入叢集的 URL (`mysparkcluster.azurehdinsight.net`)，以及要連線到叢集所需的認證。</span><span class="sxs-lookup"><span data-stu-id="be87d-159">When prompted, enter the cluster URL (`mysparkcluster.azurehdinsight.net`) and the credentials to connect to the cluster.</span></span>

    <span data-ttu-id="be87d-160">![連線到 Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "連線到 Apache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="be87d-160">![Connect to Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "Connect to Apache Spark BI")</span></span>

    <span data-ttu-id="be87d-161">建立連線之後，Power BI 會開始從 Spark 叢集將資料匯入 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="be87d-161">After the connection is established, Power BI starts importing data from the Spark cluster on HDInsight.</span></span>

6. <span data-ttu-id="be87d-162">Power BI 會匯入資料，並在 [資料集] 標頭下方新增 **Spark** 資料集。</span><span class="sxs-lookup"><span data-stu-id="be87d-162">Power BI imports the data and adds a **Spark** dataset under the **Datasets** heading.</span></span> <span data-ttu-id="be87d-163">按一下資料集來開啟新的工作表，以便將資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="be87d-163">Click the data set to open a new worksheet to visualize the data.</span></span> <span data-ttu-id="be87d-164">您也可以把工作表儲存成報告。</span><span class="sxs-lookup"><span data-stu-id="be87d-164">You can also save the worksheet as a report.</span></span> <span data-ttu-id="be87d-165">如要儲存工作表，請按一下 [檔案] 功能表中的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="be87d-165">To save a worksheet, from the **File** menu, click **Save**.</span></span>

    <span data-ttu-id="be87d-166">![Power BI 儀表板上的 Apache Spark BI 圖格](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Power BI 儀表板上的 Apache Spark BI 圖格")</span><span class="sxs-lookup"><span data-stu-id="be87d-166">![Apache Spark BI tile on Power BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Apache Spark BI tile on Power BI dashboard")</span></span>
7. <span data-ttu-id="be87d-167">請注意，右側的 [欄位] 清單會列出您先前建立的 **hvac** 資料表。</span><span class="sxs-lookup"><span data-stu-id="be87d-167">Notice that the **Fields** list on the right lists the **hvac** table you created earlier.</span></span> <span data-ttu-id="be87d-168">展開資料表，查看資料表中的欄位是否與稍早在 Notebook 中定義的欄位相同。</span><span class="sxs-lookup"><span data-stu-id="be87d-168">Expand the table to see the fields in the table, as you defined in notebook earlier.</span></span>

      <span data-ttu-id="be87d-169">![列出 Apache Spark BI 儀表板上的資料表](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "列出 Apache Spark BI 儀表板上的資料表")</span><span class="sxs-lookup"><span data-stu-id="be87d-169">![List tables on Apache Spark BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "List tables on Apache Spark BI dashboard")</span></span>

8. <span data-ttu-id="be87d-170">建置視覺效果，顯示每棟建築物之目標溫度和實際溫度間的差異。</span><span class="sxs-lookup"><span data-stu-id="be87d-170">Build a visualization to show the variance between target temperature and actual temperature for each building.</span></span> <span data-ttu-id="be87d-171">若要將資料視覺化，請選取 [區域圖] \(在紅色方框中)。</span><span class="sxs-lookup"><span data-stu-id="be87d-171">To visualize yoru data, select **Area Chart** (shown in red box).</span></span> <span data-ttu-id="be87d-172">如要定義軸線，請把 [BuildingID] 欄位拖放到 [軸] 的下方，然後把 [ActualTemp]/[TargetTemp] 欄位拖放到 [值] 的下方。</span><span class="sxs-lookup"><span data-stu-id="be87d-172">To define the axis, drag-and-drop the **BuildingID** field under **Axis**, and **ActualTemp**/**TargetTemp** fields under **Value**.</span></span>

    <span data-ttu-id="be87d-173">![使用 Apache Spark BI 建立 Spark 資料視覺效果](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "使用 Apache Spark BI 建立 Spark 資料視覺效果")</span><span class="sxs-lookup"><span data-stu-id="be87d-173">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Create Spark data visualizations using Apache Spark BI")</span></span>

9. <span data-ttu-id="be87d-174">根據預設，視覺效果會顯示 **ActualTemp** 和 **TargetTemp** 的總和。</span><span class="sxs-lookup"><span data-stu-id="be87d-174">By default the visualization shows the sum for **ActualTemp** and **TargetTemp**.</span></span> <span data-ttu-id="be87d-175">對於這兩個欄位，請選取下拉式清單中的 [平均]  ，來取得這兩棟建築物的實際和目標溫度的平均值。</span><span class="sxs-lookup"><span data-stu-id="be87d-175">For both the fields, from the drop-down, select **Average** to get an average of actual and target temperatures for both buildings.</span></span>

    <span data-ttu-id="be87d-176">![使用 Apache Spark BI 建立 Spark 資料視覺效果](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "使用 Apache Spark BI 建立 Spark 資料視覺效果")</span><span class="sxs-lookup"><span data-stu-id="be87d-176">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Create Spark data visualizations using Apache Spark BI")</span></span>

10. <span data-ttu-id="be87d-177">資料視覺效果應該類似於底下螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="be87d-177">Your data visualization should be similar to the one in the screenshot.</span></span> <span data-ttu-id="be87d-178">在視覺效果上移動游標可取得相關資料的工具提示。</span><span class="sxs-lookup"><span data-stu-id="be87d-178">Move your cursor over the visualization to get tool tips with relevant data.</span></span>

    <span data-ttu-id="be87d-179">![使用 Apache Spark BI 建立 Spark 資料視覺效果](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "使用 Apache Spark BI 建立 Spark 資料視覺效果")</span><span class="sxs-lookup"><span data-stu-id="be87d-179">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Create Spark data visualizations using Apache Spark BI")</span></span>

11. <span data-ttu-id="be87d-180">按一下頂端功能表的 [儲存]  ，並提供報告名稱。</span><span class="sxs-lookup"><span data-stu-id="be87d-180">Click **Save** from the top menu and provide a report name.</span></span> <span data-ttu-id="be87d-181">您也可以釘選視覺效果。</span><span class="sxs-lookup"><span data-stu-id="be87d-181">You can also pin the visual.</span></span> <span data-ttu-id="be87d-182">釘選視覺效果時，系統會將它儲存在儀表板上，以便您追蹤最的新值。</span><span class="sxs-lookup"><span data-stu-id="be87d-182">When you pin a visualization, it is stored on your dashboard so you can track the latest value at a glance.</span></span>

   <span data-ttu-id="be87d-183">您可以針對同一個資料集加入滿足需求數量的視覺效果，並將它們釘選在儀表板上以取得資料快照。</span><span class="sxs-lookup"><span data-stu-id="be87d-183">You can add as many visualizations as you want for the same dataset and pin them to the dashboard for a snapshot of your data.</span></span> <span data-ttu-id="be87d-184">此外，HDInsight 上的 Spark 叢集已透過直接連線連接 Power BI。</span><span class="sxs-lookup"><span data-stu-id="be87d-184">Also, Spark clusters on HDInsight are connected to Power BI with direct connect.</span></span> <span data-ttu-id="be87d-185">這可確保 Power BI 隨時能取得叢集的最新資料，因此您不需要排程資料集重新整理。</span><span class="sxs-lookup"><span data-stu-id="be87d-185">This ensures that Power BI always has the most up-to-date data from your cluster so you do not need to schedule refreshes for the dataset.</span></span>

## <span data-ttu-id="be87d-186"><a name="tableau"></a>使用 Spark 資料視覺效果的 Tableau Desktop</span><span class="sxs-lookup"><span data-stu-id="be87d-186"><a name="tableau"></a>Use Tableau Desktop for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="be87d-187">本節只適用於在 Azure HDInsight 中建立的 Spark 1.5.2 叢集。</span><span class="sxs-lookup"><span data-stu-id="be87d-187">This section is applicable only for Spark 1.5.2 clusters created in Azure HDInsight.</span></span>
>
>

1. <span data-ttu-id="be87d-188">在執行本 Apache Spark BI 教學課程的電腦上安裝 [Tableau Desktop](http://www.tableau.com/products/desktop)。</span><span class="sxs-lookup"><span data-stu-id="be87d-188">Install [Tableau Desktop](http://www.tableau.com/products/desktop) on the computer where you are running this Apache Spark BI tutorial.</span></span>

2. <span data-ttu-id="be87d-189">確保這部電腦也也安裝 Microsoft Spark ODBC 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="be87d-189">Make sure that computer also has Microsoft Spark ODBC driver installed.</span></span> <span data-ttu-id="be87d-190">您可以前往 [這裡](http://go.microsoft.com/fwlink/?LinkId=616229)來安裝驅動程式。</span><span class="sxs-lookup"><span data-stu-id="be87d-190">You can install the driver from [here](http://go.microsoft.com/fwlink/?LinkId=616229).</span></span>

1. <span data-ttu-id="be87d-191">啟動 Tableau Desktop。</span><span class="sxs-lookup"><span data-stu-id="be87d-191">Launch Tableau Desktop.</span></span> <span data-ttu-id="be87d-192">在左窗格上可連線的伺服器清單中，按一下 [Spark SQL] 。</span><span class="sxs-lookup"><span data-stu-id="be87d-192">In the left pane, from the list of server to connect to, click **Spark SQL**.</span></span> <span data-ttu-id="be87d-193">如果左窗格沒有預設列出 Spark SQL，您可以按一下 [更多伺服器] 來尋找它。</span><span class="sxs-lookup"><span data-stu-id="be87d-193">If Spark SQL is not listed by default in the left pane, you can find it by click **More Servers**.</span></span>
2. <span data-ttu-id="be87d-194">在 Spark SQL 連線對話方塊中，提供螢幕擷取畫面中所示的值，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="be87d-194">In the Spark SQL connection dialog box, provide the values as shown in the screenshot, and then click **OK**.</span></span>

    <span data-ttu-id="be87d-195">![連線至 Apache Spark BI 的叢集](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "連線至 Apache Spark BI 的叢集")</span><span class="sxs-lookup"><span data-stu-id="be87d-195">![Connect to a cluster for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Connect to a cluster for Apache Spark BI")</span></span>

    <span data-ttu-id="be87d-196">您必須先在電腦上安裝 [Microsoft Spark ODBC 驅動程式](http://go.microsoft.com/fwlink/?LinkId=616229)，驗證下拉式清單中才會出現 **Microsoft Azure HDInsight 服務**。</span><span class="sxs-lookup"><span data-stu-id="be87d-196">The authentication drop-down lists **Microsoft Azure HDInsight Service** as an option, only if you installed the [Microsoft Spark ODBC Driver](http://go.microsoft.com/fwlink/?LinkId=616229) on the computer.</span></span>
3. <span data-ttu-id="be87d-197">在下一個畫面中，按一下 [結構描述] 下拉式清單的 [尋找] 圖示，然後按一下 [預設]。</span><span class="sxs-lookup"><span data-stu-id="be87d-197">On the next screen, from the **Schema** drop-down, click the **Find** icon, and then click **default**.</span></span>

    <span data-ttu-id="be87d-198">![尋找 Apache Spark BI 的結構描述](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "尋找 Apache Spark BI 的結構描述")</span><span class="sxs-lookup"><span data-stu-id="be87d-198">![Find schema for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Find schema for Apache Spark BI")</span></span>
4. <span data-ttu-id="be87d-199">對於 [資料表] 欄位，再次按一下 [尋找] 圖示以列出叢集中所有可用的 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="be87d-199">For the **Table** field, click the **Find** icon again to list all the Hive tables available in the cluster.</span></span> <span data-ttu-id="be87d-200">您應該會看到自己先前使用 Notebook 建立的 **hvac** 資料表。</span><span class="sxs-lookup"><span data-stu-id="be87d-200">You should see the **hvac** table you created earlier using the notebook.</span></span>

    <span data-ttu-id="be87d-201">![尋找 Apache Spark BI 的資料表](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "尋找 Apache Spark BI 的資料表")</span><span class="sxs-lookup"><span data-stu-id="be87d-201">![Find table for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Find table for Apache Spark BI")</span></span>
5. <span data-ttu-id="be87d-202">將資料表拖放到右側頂端的方塊。</span><span class="sxs-lookup"><span data-stu-id="be87d-202">Drag and drop the table to the top box on the right.</span></span> <span data-ttu-id="be87d-203">Tableau 會匯入資料，並以紅色方塊反白顯示結構描述。</span><span class="sxs-lookup"><span data-stu-id="be87d-203">Tableau imports the data and displays the schema as highlighted by the red box.</span></span>

    <span data-ttu-id="be87d-204">![將資料表新增至 Apache Spark BI 的 Tableau](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "將資料表新增至 Apache Spark BI 的 Tableau")</span><span class="sxs-lookup"><span data-stu-id="be87d-204">![Add tables to Tableau for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "Add tables to Tableau for Apache Spark BI")</span></span>
6. <span data-ttu-id="be87d-205">按一下左下方的 [Sheet1]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="be87d-205">Click the **Sheet1** tab at the bottom left.</span></span> <span data-ttu-id="be87d-206">針對每個日期，製作出顯示所有建築物之平均目標溫度和實際溫度的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="be87d-206">Make a visualization that shows the average target and actual temperatures for all buildings for each date.</span></span> <span data-ttu-id="be87d-207">請把 [日期] 和 [建築物識別碼] 拖放到 [資料行] 中，然後將 [實際溫度]/[目標溫度] 拖放到 [資料列] 中。</span><span class="sxs-lookup"><span data-stu-id="be87d-207">Drag **Date** and **Building ID** to **Columns** and **Actual Temp**/**Target Temp** to **Rows**.</span></span> <span data-ttu-id="be87d-208">請選取 [標記] 下方的 [區域]，以使用 Spark 資料視覺效果的區域對應圖。</span><span class="sxs-lookup"><span data-stu-id="be87d-208">Under **Marks**, select **Area** to use an area map for Spark data visualization.</span></span>

     <span data-ttu-id="be87d-209">![新增 Spark 資料視覺效果的欄位](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "新增 Spark 資料視覺效果的欄位")</span><span class="sxs-lookup"><span data-stu-id="be87d-209">![Add fields for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Add fields for Spark data visualization")</span></span>
7. <span data-ttu-id="be87d-210">根據預設，溫度欄位以彙總形式顯示。</span><span class="sxs-lookup"><span data-stu-id="be87d-210">By default, the temperature fields are shown as aggregate.</span></span> <span data-ttu-id="be87d-211">如果您想要改為顯示平均溫度，可以從下拉式清單執行操作，如下所示。</span><span class="sxs-lookup"><span data-stu-id="be87d-211">If you want to show the average temperatures instead, you can do so from the drop-down, as shown below.</span></span>

    <span data-ttu-id="be87d-212">![採取 Spark 資料視覺效果的平均溫度](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "採取 Spark 資料視覺效果的平均溫度")</span><span class="sxs-lookup"><span data-stu-id="be87d-212">![Take average of temperature for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Take average of temperature for Spark data visualization")</span></span>

8. <span data-ttu-id="be87d-213">您也可以將溫度對應加諸在其他對應之上，凸顯目標溫度和實際溫度之間的差異。</span><span class="sxs-lookup"><span data-stu-id="be87d-213">You can also super-impose one temperature map over the other to get a better feel of difference between target and actual temperatures.</span></span> <span data-ttu-id="be87d-214">將滑鼠游標移動到區域對應圖下半部的角落，直到控點出現為止 (如紅色圓圈中所示)。</span><span class="sxs-lookup"><span data-stu-id="be87d-214">Move the mouse to the corner of the lower area map till you see the handle shape highlighted in a red circle.</span></span> <span data-ttu-id="be87d-215">把對應圖拖曳到另一個對應圖的頂端，然後在您看到紅色圓圈中所示的形狀時，放開滑鼠按鍵。</span><span class="sxs-lookup"><span data-stu-id="be87d-215">Drag the map to the other map on the top and release the mouse when you see the shape highlighted in red rectangle.</span></span>

    <span data-ttu-id="be87d-216">![合併 Spark 資料視覺效果的對應圖](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "合併 Spark 資料視覺效果的對應圖")</span><span class="sxs-lookup"><span data-stu-id="be87d-216">![Merge maps for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Merge maps for Spark data visualization")</span></span>

     <span data-ttu-id="be87d-217">資料視覺效果應會變更，如底下螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="be87d-217">Your data visualization should change as shown in the screenshot:</span></span>

    <span data-ttu-id="be87d-218">![Spark 資料視覺效果的 Tableau 輸出](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Spark 資料視覺效果的 Tableau 輸出")</span><span class="sxs-lookup"><span data-stu-id="be87d-218">![Tableau output for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau output for Spark data visualization")</span></span>
9. <span data-ttu-id="be87d-219">按一下 [儲存]  以儲存工作表。</span><span class="sxs-lookup"><span data-stu-id="be87d-219">Click **Save** to save the worksheet.</span></span> <span data-ttu-id="be87d-220">您可以建立儀表板，並在儀表板中加入一個或多個工作表。</span><span class="sxs-lookup"><span data-stu-id="be87d-220">You can create dashboards and add one or more sheets to it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be87d-221">後續步驟</span><span class="sxs-lookup"><span data-stu-id="be87d-221">Next steps</span></span>

<span data-ttu-id="be87d-222">到目前為止，您學會了如何建立叢集、建立 Spark 資料框架來查詢資料，然後從 BI 工具中存取該資料。</span><span class="sxs-lookup"><span data-stu-id="be87d-222">So far you learned how to create a cluster, create Spark data frames to query data, and then access that data from BI tools.</span></span> <span data-ttu-id="be87d-223">您現在可以看看如何管理叢集資源，以及對在 HDInsight Spark 叢集中執行的工作進行偵錯的指示。</span><span class="sxs-lookup"><span data-stu-id="be87d-223">You can now look at instructions on how to manage the cluster resources and debug jobs that are running in an HDInsight Spark cluster.</span></span>

* [<span data-ttu-id="be87d-224">在 Azure HDInsight 中管理 Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="be87d-224">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="be87d-225">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="be87d-225">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

