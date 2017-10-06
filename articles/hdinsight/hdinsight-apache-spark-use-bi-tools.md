---
title: "aaaSpark BI 使用 Azure HDInsight 上的資料視覺效果工具 |Microsoft 文件"
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
ms.openlocfilehash: ba4bfff737ce80ffca5c24f1c2c82a1447f467fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a><span data-ttu-id="e2258-104">使用資料視覺效果工具搭配 Azure HDInsight 的 Apache Spark BI</span><span class="sxs-lookup"><span data-stu-id="e2258-104">Apache Spark BI using data visualization tools with Azure HDInsight</span></span>

<span data-ttu-id="e2258-105">了解如何 toouse 資料視覺效果工具，例如 Power BI 和 Tableau tooanalyze HDInsight 叢集上使用 Apache Spark BI 未經處理的範例資料集。</span><span class="sxs-lookup"><span data-stu-id="e2258-105">Learn how toouse data visualization tools such as Power BI and Tableau tooanalyze a raw sample data set using Apache Spark BI on HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="e2258-106">Azure HDInsight 3.6 預覽版的 Spark 2.1 不支援本文所述的 BI 工具連接性。</span><span class="sxs-lookup"><span data-stu-id="e2258-106">Connectivity with BI tools described in this article is not supported on Spark 2.1 on Azure HDInsight 3.6 Preview.</span></span> <span data-ttu-id="e2258-107">僅支援 Spark 1.6 版和 2.0 版 (分別是 HDInsight 3.4 版和 3.5 版)。</span><span class="sxs-lookup"><span data-stu-id="e2258-107">Only Spark versions 1.6 and 2.0 (HDInsight 3.4, 3.5 respectively) are supported.</span></span>
>

<span data-ttu-id="e2258-108">本教學課程也可在 HDInsight Spark 叢集上用來作為 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="e2258-108">This tutorial is also available as a Jupyter notebook on an HDInsight Spark cluster.</span></span> <span data-ttu-id="e2258-109">hello 筆記本體驗可讓您從本身的 hello 筆記本執行 hello Python 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="e2258-109">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="e2258-110">tooperform hello 教學課程中的筆記本內建立 Spark 叢集，請啟動 Jupyter 筆記本 (`https://CLUSTERNAME.azurehdinsight.net/jupyter`)，然後執行 hello 筆記本**使用 BI 工具和 Apache Spark 上 HDInsight.ipynb**下 hello **Python**資料夾。</span><span class="sxs-lookup"><span data-stu-id="e2258-110">tooperform hello tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run hello notebook **Use BI tools with Apache Spark on HDInsight.ipynb** under hello **Python** folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2258-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="e2258-111">Prerequisites</span></span>

* <span data-ttu-id="e2258-112">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="e2258-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="e2258-113">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="e2258-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>


## <span data-ttu-id="e2258-114"><a name="hivetable"></a>準備 Spark 資料視覺效果的資料</span><span class="sxs-lookup"><span data-stu-id="e2258-114"><a name="hivetable"></a>Prepare data for Spark data visualization</span></span>

<span data-ttu-id="e2258-115">在本節中，我們使用 hello [Jupyter](https://jupyter.org)筆記本從 HDInsight Spark 叢集 toorun 作業時，處理未經處理的範例資料，並將它儲存為資料表。</span><span class="sxs-lookup"><span data-stu-id="e2258-115">In this section, we use hello [Jupyter](https://jupyter.org) notebook from an HDInsight Spark cluster toorun jobs that process your raw sample data and save it as a table.</span></span> <span data-ttu-id="e2258-116">上的.csv 檔案 (hvac.csv) 使用預設的所有叢集 hello 範例資料。</span><span class="sxs-lookup"><span data-stu-id="e2258-116">hello sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span> <span data-ttu-id="e2258-117">一旦您的資料會儲存為資料表，hello 下一節中我們使用 BI 工具 tooconnect toohello 資料表並執行資料視覺效果。</span><span class="sxs-lookup"><span data-stu-id="e2258-117">Once your data is saved as a table, in hello next section we use BI tools tooconnect toohello table and perform data visualizations.</span></span>

> [!NOTE]
> <span data-ttu-id="e2258-118">如果您要執行 hello 這篇文章中的步驟完成中的 hello 指示之後[HDInsight Spark 叢集上執行的互動式查詢](hdinsight-apache-spark-load-data-run-query.md)，您可以略過 tooStep 8 下方。</span><span class="sxs-lookup"><span data-stu-id="e2258-118">If you are performing hello steps in this article after completing hello instructions in [Run interactive queries on an HDInsight Spark cluster](hdinsight-apache-spark-load-data-run-query.md), you can skip tooStep 8 below.</span></span>
>

1. <span data-ttu-id="e2258-119">從 hello [Azure 入口網站](https://portal.azure.com/)，從 hello 開始面板中，按一下 Spark 叢集中的 hello 磚 （如果您釘選它 toohello 開始面板）。</span><span class="sxs-lookup"><span data-stu-id="e2258-119">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="e2258-120">您也可以導覽 tooyour 叢集下的**瀏覽所有** > **HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="e2258-120">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   

2. <span data-ttu-id="e2258-121">從 hello Spark 叢集刀鋒視窗中，按一下 **叢集儀表板**，然後按一下 **Jupyter 筆記本**。</span><span class="sxs-lookup"><span data-stu-id="e2258-121">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="e2258-122">如果出現提示，請輸入 hello 叢集 hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="e2258-122">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e2258-123">您也可能由下列 URL 在瀏覽器中開啟 hello 叢集到達 hello Jupyter 筆記本。</span><span class="sxs-lookup"><span data-stu-id="e2258-123">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="e2258-124">取代**CLUSTERNAME** hello 名稱，為您的叢集：</span><span class="sxs-lookup"><span data-stu-id="e2258-124">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="e2258-125">建立 Notebook。</span><span class="sxs-lookup"><span data-stu-id="e2258-125">Create a notebook.</span></span> <span data-ttu-id="e2258-126">按一下 新增，然後按一下PySpark。</span><span class="sxs-lookup"><span data-stu-id="e2258-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="e2258-127">![建立 Apache Spark BI 的 Jupyter Notebook](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "建立 Apache Spark BI 的 Jupyter Notebook")</span><span class="sxs-lookup"><span data-stu-id="e2258-127">![Create a Jupyter notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Create a Jupyter notebook for Apache Spark BI")</span></span>

4. <span data-ttu-id="e2258-128">建立新的記事本，並開啟 hello 名稱 Untitled.pynb。</span><span class="sxs-lookup"><span data-stu-id="e2258-128">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="e2258-129">按一下頂端 hello hello 筆記本名稱並輸入好記的名稱。</span><span class="sxs-lookup"><span data-stu-id="e2258-129">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="e2258-130">![為提供的名稱 hello 筆記本 Apache Spark bi](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Apache Spark bi 提供 hello 筆記本的名稱")</span><span class="sxs-lookup"><span data-stu-id="e2258-130">![Provide a name for hello notebook for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Provide a name for hello notebook for Apache Spark BI")</span></span>

5. <span data-ttu-id="e2258-131">因為您建立使用 hello PySpark 核心筆記本，您不需要 toocreate 任何內容明確。</span><span class="sxs-lookup"><span data-stu-id="e2258-131">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="e2258-132">hello Spark 和 Hive 內容會自動建立，當您執行 hello 第一個程式碼儲存格。</span><span class="sxs-lookup"><span data-stu-id="e2258-132">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="e2258-133">您可以開始匯入此案例所需的 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="e2258-133">You can start by importing hello types required for this scenario.</span></span> <span data-ttu-id="e2258-134">toodo，hello 將游標放在位於 hello 儲存格，按**SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="e2258-134">toodo so, place hello cursor in hello cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import *

6. <span data-ttu-id="e2258-135">將範例資料載入暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="e2258-135">Load sample data into a temporary table.</span></span> <span data-ttu-id="e2258-136">當您建立 HDInsight，hello 範例資料檔中的 Spark 叢集**hvac.csv**，是儲存體帳戶相關聯的複製的 toohello **\HdiSamples\HdiSamples\SensorSampleData\hvac**。</span><span class="sxs-lookup"><span data-stu-id="e2258-136">When you create a Spark cluster in HDInsight, hello sample data file, **hvac.csv**, is copied toohello associated storage account under **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span>

    <span data-ttu-id="e2258-137">在空的資料格，貼上 hello 下列程式碼片段，然後按**SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="e2258-137">In an empty cell, paste hello following snippet and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="e2258-138">這個程式碼片段會註冊 hello 資料到資料表，稱為**hvac**。</span><span class="sxs-lookup"><span data-stu-id="e2258-138">This snippet registers hello data into a table called **hvac**.</span></span>

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))

        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. <span data-ttu-id="e2258-139">請確認已成功建立該 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="e2258-139">Verify that hello table was successfully created.</span></span> <span data-ttu-id="e2258-140">您可以使用 hello`%%sql`直接 magic toorun Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="e2258-140">You can use hello `%%sql` magic toorun Hive queries directly.</span></span> <span data-ttu-id="e2258-141">如需有關 hello`%%sql`魔法和其他適用於 hello PySpark 核心中，我們看到[Jupyter notebook Spark HDInsight 叢集上可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)。</span><span class="sxs-lookup"><span data-stu-id="e2258-141">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SHOW TABLES

    <span data-ttu-id="e2258-142">您會看到如下所示的輸出：</span><span class="sxs-lookup"><span data-stu-id="e2258-142">You see an output like shown below:</span></span>

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    <span data-ttu-id="e2258-143">只有 hello 資料表具有在 hello false **isTemporary**資料行所儲存在 hello 中繼存放區，而且可以從 hello BI 工具存取的 hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="e2258-143">Only hello tables that have false under hello **isTemporary** column are hive tables that are stored in hello metastore and can be accessed from hello BI tools.</span></span> <span data-ttu-id="e2258-144">在本教學課程中，我們連接 toohello **hvac**我們建立的資料表。</span><span class="sxs-lookup"><span data-stu-id="e2258-144">In this tutorial, we connect toohello **hvac** table we created.</span></span>

8. <span data-ttu-id="e2258-145">請確認該 hello 資料表包含 hello 適合的資料。</span><span class="sxs-lookup"><span data-stu-id="e2258-145">Verify that hello table contains hello intended data.</span></span> <span data-ttu-id="e2258-146">在 hello 筆記本中的空資料格，複製 hello 下列程式碼片段，然後按**SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="e2258-146">In an empty cell in hello notebook, copy hello following snippet and press **SHIFT + ENTER**.</span></span>

        %%sql
        SELECT * FROM hvac LIMIT 10

9. <span data-ttu-id="e2258-147">關閉 hello 筆記本 toorelease hello 資源。</span><span class="sxs-lookup"><span data-stu-id="e2258-147">Shut down hello notebook toorelease hello resources.</span></span> <span data-ttu-id="e2258-148">toodo 的話，從 hello**檔案**hello 筆記本功能表按一下**關閉而停止**。</span><span class="sxs-lookup"><span data-stu-id="e2258-148">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

## <span data-ttu-id="e2258-149"><a name="powerbi"></a>使用 Spark 資料視覺效果的 Power BI</span><span class="sxs-lookup"><span data-stu-id="e2258-149"><a name="powerbi"></a>Use Power BI for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="e2258-150">本節只適用於 HDInsight 3.4 上的 Spark 1.6 以及 HDInsight 3.5 上的 Spark 2.0。</span><span class="sxs-lookup"><span data-stu-id="e2258-150">This section is applicable only for Spark 1.6 on HDInsight 3.4 and Spark 2.0 on HDInsight 3.5.</span></span>
>
>

<span data-ttu-id="e2258-151">在 hello 資料儲存為資料表後，您可以使用 Power BI tooconnect toohello 資料和 toocreate 報表視覺效果的儀表板，依此類推。</span><span class="sxs-lookup"><span data-stu-id="e2258-151">Once you have saved hello data as a table, you can use Power BI tooconnect toohello data and visualize it toocreate reports, dashboards, etc.</span></span>

1. <span data-ttu-id="e2258-152">請確定您具有存取 tooPower BI。</span><span class="sxs-lookup"><span data-stu-id="e2258-152">Make sure you have access tooPower BI.</span></span> <span data-ttu-id="e2258-153">您可以從 [http://www.powerbi.com/](http://www.powerbi.com/)取得 Power BI 的免費預覽版訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e2258-153">You can get a free preview subscription of Power BI from [http://www.powerbi.com/](http://www.powerbi.com/).</span></span>

2. <span data-ttu-id="e2258-154">登入太[Power BI](http://www.powerbi.com/)。</span><span class="sxs-lookup"><span data-stu-id="e2258-154">Sign in too[Power BI](http://www.powerbi.com/).</span></span>

3. <span data-ttu-id="e2258-155">從 hello hello 左窗格底部，按一下 **取得資料**。</span><span class="sxs-lookup"><span data-stu-id="e2258-155">From hello bottom of hello left pane, click **Get Data**.</span></span>

4. <span data-ttu-id="e2258-156">在 hello**取得資料**頁面的 **匯入或連接 tooData**，如**資料庫**，按一下**取得**。</span><span class="sxs-lookup"><span data-stu-id="e2258-156">On hello **Get Data** page, under **Import or Connect tooData**, for **Databases**, click **Get**.</span></span>

    <span data-ttu-id="e2258-157">![將資料送入 Apache Spark BI 的 Power BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "將資料送入 Apache Spark BI 的 Power BI")</span><span class="sxs-lookup"><span data-stu-id="e2258-157">![Get data into Power BI for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Get data into Power BI for Apache Spark BI")</span></span>

5. <span data-ttu-id="e2258-158">Hello 下一個畫面上，按一下**Azure HDInsight 上的 Spark** ，然後按一下**連接**。</span><span class="sxs-lookup"><span data-stu-id="e2258-158">On hello next screen, click **Spark on Azure HDInsight** and then click **Connect**.</span></span> <span data-ttu-id="e2258-159">出現提示時，請輸入 hello 叢集 URL (`mysparkcluster.azurehdinsight.net`) 和 hello 認證 tooconnect toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="e2258-159">When prompted, enter hello cluster URL (`mysparkcluster.azurehdinsight.net`) and hello credentials tooconnect toohello cluster.</span></span>

    <span data-ttu-id="e2258-160">![連接 tooApache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "連接 tooApache Spark BI")</span><span class="sxs-lookup"><span data-stu-id="e2258-160">![Connect tooApache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "Connect tooApache Spark BI")</span></span>

    <span data-ttu-id="e2258-161">建立 hello 連接之後，Power BI 會開始從 hello HDInsight 上的 Spark 叢集匯入資料。</span><span class="sxs-lookup"><span data-stu-id="e2258-161">After hello connection is established, Power BI starts importing data from hello Spark cluster on HDInsight.</span></span>

6. <span data-ttu-id="e2258-162">Power BI 匯入 hello 資料，並新增**Spark** hello 資料集**資料集**標題。</span><span class="sxs-lookup"><span data-stu-id="e2258-162">Power BI imports hello data and adds a **Spark** dataset under hello **Datasets** heading.</span></span> <span data-ttu-id="e2258-163">按一下 hello 資料集 tooopen 新的工作表 toovisualize hello 資料。</span><span class="sxs-lookup"><span data-stu-id="e2258-163">Click hello data set tooopen a new worksheet toovisualize hello data.</span></span> <span data-ttu-id="e2258-164">您也可以當做報表儲存 hello 工作表。</span><span class="sxs-lookup"><span data-stu-id="e2258-164">You can also save hello worksheet as a report.</span></span> <span data-ttu-id="e2258-165">工作表，從 hello toosave**檔案**功能表上，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="e2258-165">toosave a worksheet, from hello **File** menu, click **Save**.</span></span>

    <span data-ttu-id="e2258-166">![Power BI 儀表板上的 Apache Spark BI 圖格](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Power BI 儀表板上的 Apache Spark BI 圖格")</span><span class="sxs-lookup"><span data-stu-id="e2258-166">![Apache Spark BI tile on Power BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Apache Spark BI tile on Power BI dashboard")</span></span>
7. <span data-ttu-id="e2258-167">請注意該 hello**欄位**hello 右邊的清單會列出 hello **hvac**您稍早建立的資料表。</span><span class="sxs-lookup"><span data-stu-id="e2258-167">Notice that hello **Fields** list on hello right lists hello **hvac** table you created earlier.</span></span> <span data-ttu-id="e2258-168">如先前在筆記本中定義，請展開 hello 資料表 toosee hello 資料表中的 hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="e2258-168">Expand hello table toosee hello fields in hello table, as you defined in notebook earlier.</span></span>

      <span data-ttu-id="e2258-169">![列出 Apache Spark BI 儀表板上的資料表](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "列出 Apache Spark BI 儀表板上的資料表")</span><span class="sxs-lookup"><span data-stu-id="e2258-169">![List tables on Apache Spark BI dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "List tables on Apache Spark BI dashboard")</span></span>

8. <span data-ttu-id="e2258-170">建置目標溫度和每個建置實際溫度之間的視覺效果 tooshow hello 變異數。</span><span class="sxs-lookup"><span data-stu-id="e2258-170">Build a visualization tooshow hello variance between target temperature and actual temperature for each building.</span></span> <span data-ttu-id="e2258-171">toovisualize 向資料、 選取**區域圖**（顯示為紅色方塊）。</span><span class="sxs-lookup"><span data-stu-id="e2258-171">toovisualize yoru data, select **Area Chart** (shown in red box).</span></span> <span data-ttu-id="e2258-172">toodefine hello 座標軸，拖放 hello **BuildingID**欄位底下**軸**，和**ActualTemp**/**TargetTemp**欄位底下**值**。</span><span class="sxs-lookup"><span data-stu-id="e2258-172">toodefine hello axis, drag-and-drop hello **BuildingID** field under **Axis**, and **ActualTemp**/**TargetTemp** fields under **Value**.</span></span>

    <span data-ttu-id="e2258-173">![使用 Apache Spark BI 建立 Spark 資料視覺效果](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "使用 Apache Spark BI 建立 Spark 資料視覺效果")</span><span class="sxs-lookup"><span data-stu-id="e2258-173">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Create Spark data visualizations using Apache Spark BI")</span></span>

9. <span data-ttu-id="e2258-174">依預設，hello 視覺效果顯示 hello 總和**ActualTemp**和**TargetTemp**。</span><span class="sxs-lookup"><span data-stu-id="e2258-174">By default hello visualization shows hello sum for **ActualTemp** and **TargetTemp**.</span></span> <span data-ttu-id="e2258-175">同時 hello 欄位，從 [hello] 下拉式清單中選取**平均**tooget 實際的平均和這兩個大樓目標溫度。</span><span class="sxs-lookup"><span data-stu-id="e2258-175">For both hello fields, from hello drop-down, select **Average** tooget an average of actual and target temperatures for both buildings.</span></span>

    <span data-ttu-id="e2258-176">![使用 Apache Spark BI 建立 Spark 資料視覺效果](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "使用 Apache Spark BI 建立 Spark 資料視覺效果")</span><span class="sxs-lookup"><span data-stu-id="e2258-176">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Create Spark data visualizations using Apache Spark BI")</span></span>

10. <span data-ttu-id="e2258-177">您的資料視覺效果應該在 hello 螢幕擷取畫面類似 toohello。</span><span class="sxs-lookup"><span data-stu-id="e2258-177">Your data visualization should be similar toohello one in hello screenshot.</span></span> <span data-ttu-id="e2258-178">將游標 hello 視覺效果 tooget 具有相關資料的工具提示。</span><span class="sxs-lookup"><span data-stu-id="e2258-178">Move your cursor over hello visualization tooget tool tips with relevant data.</span></span>

    <span data-ttu-id="e2258-179">![使用 Apache Spark BI 建立 Spark 資料視覺效果](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "使用 Apache Spark BI 建立 Spark 資料視覺效果")</span><span class="sxs-lookup"><span data-stu-id="e2258-179">![Create Spark data visualizations using Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Create Spark data visualizations using Apache Spark BI")</span></span>

11. <span data-ttu-id="e2258-180">按一下**儲存**hello 從最上層功能表，並提供報表的名稱。</span><span class="sxs-lookup"><span data-stu-id="e2258-180">Click **Save** from hello top menu and provide a report name.</span></span> <span data-ttu-id="e2258-181">您可以也視覺效果釘選 hello。</span><span class="sxs-lookup"><span data-stu-id="e2258-181">You can also pin hello visual.</span></span> <span data-ttu-id="e2258-182">當您釘選視覺效果時，它會儲存儀表板上，您可以一眼 hello 最新值。</span><span class="sxs-lookup"><span data-stu-id="e2258-182">When you pin a visualization, it is stored on your dashboard so you can track hello latest value at a glance.</span></span>

   <span data-ttu-id="e2258-183">您可以將許多視覺效果所需要的 hello 相同的資料集，並將其釘選 toohello 儀表板的資料快照集。</span><span class="sxs-lookup"><span data-stu-id="e2258-183">You can add as many visualizations as you want for hello same dataset and pin them toohello dashboard for a snapshot of your data.</span></span> <span data-ttu-id="e2258-184">此外，在 HDInsight 上的 Spark 叢集會連接的 tooPower BI 直接連接。</span><span class="sxs-lookup"><span data-stu-id="e2258-184">Also, Spark clusters on HDInsight are connected tooPower BI with direct connect.</span></span> <span data-ttu-id="e2258-185">這可確保 Power BI 一律具有 hello 大部分從叢集中的最新資料，您不需要 tooschedule 重新整理 hello 資料集。</span><span class="sxs-lookup"><span data-stu-id="e2258-185">This ensures that Power BI always has hello most up-to-date data from your cluster so you do not need tooschedule refreshes for hello dataset.</span></span>

## <span data-ttu-id="e2258-186"><a name="tableau"></a>使用 Spark 資料視覺效果的 Tableau Desktop</span><span class="sxs-lookup"><span data-stu-id="e2258-186"><a name="tableau"></a>Use Tableau Desktop for Spark data visualization</span></span>

> [!NOTE]
> <span data-ttu-id="e2258-187">本節只適用於在 Azure HDInsight 中建立的 Spark 1.5.2 叢集。</span><span class="sxs-lookup"><span data-stu-id="e2258-187">This section is applicable only for Spark 1.5.2 clusters created in Azure HDInsight.</span></span>
>
>

1. <span data-ttu-id="e2258-188">安裝[Tableau 桌面](http://www.tableau.com/products/desktop)hello 執行本教學課程中 Apache Spark BI 所在的電腦上。</span><span class="sxs-lookup"><span data-stu-id="e2258-188">Install [Tableau Desktop](http://www.tableau.com/products/desktop) on hello computer where you are running this Apache Spark BI tutorial.</span></span>

2. <span data-ttu-id="e2258-189">確保這部電腦也也安裝 Microsoft Spark ODBC 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="e2258-189">Make sure that computer also has Microsoft Spark ODBC driver installed.</span></span> <span data-ttu-id="e2258-190">您可以安裝 hello 驅動程式從[這裡](http://go.microsoft.com/fwlink/?LinkId=616229)。</span><span class="sxs-lookup"><span data-stu-id="e2258-190">You can install hello driver from [here](http://go.microsoft.com/fwlink/?LinkId=616229).</span></span>

1. <span data-ttu-id="e2258-191">啟動 Tableau Desktop。</span><span class="sxs-lookup"><span data-stu-id="e2258-191">Launch Tableau Desktop.</span></span> <span data-ttu-id="e2258-192">Hello 左窗格中，從伺服器 tooconnect，hello 清單按一下**Spark SQL**。</span><span class="sxs-lookup"><span data-stu-id="e2258-192">In hello left pane, from hello list of server tooconnect to, click **Spark SQL**.</span></span> <span data-ttu-id="e2258-193">如果 hello 左窗格中預設不會列出 Spark SQL，您可以找出它按一下**多伺服器**。</span><span class="sxs-lookup"><span data-stu-id="e2258-193">If Spark SQL is not listed by default in hello left pane, you can find it by click **More Servers**.</span></span>
2. <span data-ttu-id="e2258-194">在 [hello Spark SQL 連線] 對話方塊中提供 hello 值 hello 螢幕擷取畫面所示，然後按**確定**。</span><span class="sxs-lookup"><span data-stu-id="e2258-194">In hello Spark SQL connection dialog box, provide hello values as shown in hello screenshot, and then click **OK**.</span></span>

    <span data-ttu-id="e2258-195">![Apache Spark bi 連接 tooa 叢集](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Apache Spark bi 連接 tooa 叢集")</span><span class="sxs-lookup"><span data-stu-id="e2258-195">![Connect tooa cluster for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Connect tooa cluster for Apache Spark BI")</span></span>

    <span data-ttu-id="e2258-196">hello 驗證下拉式清單**Microsoft Azure HDInsight 服務**的選項，只有當您安裝 hello [Microsoft Spark ODBC 驅動程式](http://go.microsoft.com/fwlink/?LinkId=616229)hello 電腦上。</span><span class="sxs-lookup"><span data-stu-id="e2258-196">hello authentication drop-down lists **Microsoft Azure HDInsight Service** as an option, only if you installed hello [Microsoft Spark ODBC Driver](http://go.microsoft.com/fwlink/?LinkId=616229) on hello computer.</span></span>
3. <span data-ttu-id="e2258-197">Hello 下一個畫面中，從 hello**結構描述**下拉式清單中，按一下 hello**尋找**圖示，然後再按一下**預設**。</span><span class="sxs-lookup"><span data-stu-id="e2258-197">On hello next screen, from hello **Schema** drop-down, click hello **Find** icon, and then click **default**.</span></span>

    <span data-ttu-id="e2258-198">![尋找 Apache Spark BI 的結構描述](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "尋找 Apache Spark BI 的結構描述")</span><span class="sxs-lookup"><span data-stu-id="e2258-198">![Find schema for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Find schema for Apache Spark BI")</span></span>
4. <span data-ttu-id="e2258-199">Hello**資料表**欄位中，按一下 hello**尋找**圖示再次 toolist 所有 hello Hive hello 叢集中可用的資料表。</span><span class="sxs-lookup"><span data-stu-id="e2258-199">For hello **Table** field, click hello **Find** icon again toolist all hello Hive tables available in hello cluster.</span></span> <span data-ttu-id="e2258-200">您應該會看見 hello **hvac**先前使用 hello 筆記本所建立的資料表。</span><span class="sxs-lookup"><span data-stu-id="e2258-200">You should see hello **hvac** table you created earlier using hello notebook.</span></span>

    <span data-ttu-id="e2258-201">![尋找 Apache Spark BI 的資料表](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "尋找 Apache Spark BI 的資料表")</span><span class="sxs-lookup"><span data-stu-id="e2258-201">![Find table for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Find table for Apache Spark BI")</span></span>
5. <span data-ttu-id="e2258-202">拖放 hello 資料表 toohello 頂端的方塊上 hello 右。</span><span class="sxs-lookup"><span data-stu-id="e2258-202">Drag and drop hello table toohello top box on hello right.</span></span> <span data-ttu-id="e2258-203">Tableau 匯入 hello 資料，並顯示 hello 紅色方塊以反白顯示 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="e2258-203">Tableau imports hello data and displays hello schema as highlighted by hello red box.</span></span>

    <span data-ttu-id="e2258-204">![加入資料表 tooTableau Apache Spark bi](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "新增資料表 tooTableau Apache Spark bi")</span><span class="sxs-lookup"><span data-stu-id="e2258-204">![Add tables tooTableau for Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "Add tables tooTableau for Apache Spark BI")</span></span>
6. <span data-ttu-id="e2258-205">按一下 hello **Sheet1**在 hello 左下方的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e2258-205">Click hello **Sheet1** tab at hello bottom left.</span></span> <span data-ttu-id="e2258-206">請針對每個日期顯示 hello 平均目標與實際溫度所有建築物的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="e2258-206">Make a visualization that shows hello average target and actual temperatures for all buildings for each date.</span></span> <span data-ttu-id="e2258-207">拖曳**日期**和**建置 ID**太**資料行**和**實際 Temp**/**目標 Temp**太**列**。</span><span class="sxs-lookup"><span data-stu-id="e2258-207">Drag **Date** and **Building ID** too**Columns** and **Actual Temp**/**Target Temp** too**Rows**.</span></span> <span data-ttu-id="e2258-208">在下**標記**，選取**區域**toouse Spark 資料視覺效果的區域對應。</span><span class="sxs-lookup"><span data-stu-id="e2258-208">Under **Marks**, select **Area** toouse an area map for Spark data visualization.</span></span>

     <span data-ttu-id="e2258-209">![新增 Spark 資料視覺效果的欄位](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "新增 Spark 資料視覺效果的欄位")</span><span class="sxs-lookup"><span data-stu-id="e2258-209">![Add fields for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Add fields for Spark data visualization")</span></span>
7. <span data-ttu-id="e2258-210">根據預設，hello 溫度欄位會顯示為彙總。</span><span class="sxs-lookup"><span data-stu-id="e2258-210">By default, hello temperature fields are shown as aggregate.</span></span> <span data-ttu-id="e2258-211">若要改為 tooshow hello 平均溫度，您可以從 hello 下拉式清單，如下所示。</span><span class="sxs-lookup"><span data-stu-id="e2258-211">If you want tooshow hello average temperatures instead, you can do so from hello drop-down, as shown below.</span></span>

    <span data-ttu-id="e2258-212">![採取 Spark 資料視覺效果的平均溫度](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "採取 Spark 資料視覺效果的平均溫度")</span><span class="sxs-lookup"><span data-stu-id="e2258-212">![Take average of temperature for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Take average of temperature for Spark data visualization")</span></span>

8. <span data-ttu-id="e2258-213">您也可以超級-強加一個溫度對應超過 hello 其他 tooget 目標與實際的溫度之間差異的好風格。</span><span class="sxs-lookup"><span data-stu-id="e2258-213">You can also super-impose one temperature map over hello other tooget a better feel of difference between target and actual temperatures.</span></span> <span data-ttu-id="e2258-214">移動 hello 較低的區域地圖的 hello 滑鼠 toohello 角，直到您看到 hello 控點圖形中的紅色圓圈反白顯示。</span><span class="sxs-lookup"><span data-stu-id="e2258-214">Move hello mouse toohello corner of hello lower area map till you see hello handle shape highlighted in a red circle.</span></span> <span data-ttu-id="e2258-215">拖曳 hello 對應 toohello hello top 和發行 hello 滑鼠上的其他對應時，您會看到紅色矩形中反白顯示 hello 圖形。</span><span class="sxs-lookup"><span data-stu-id="e2258-215">Drag hello map toohello other map on hello top and release hello mouse when you see hello shape highlighted in red rectangle.</span></span>

    <span data-ttu-id="e2258-216">![合併 Spark 資料視覺效果的對應圖](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "合併 Spark 資料視覺效果的對應圖")</span><span class="sxs-lookup"><span data-stu-id="e2258-216">![Merge maps for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Merge maps for Spark data visualization")</span></span>

     <span data-ttu-id="e2258-217">您的資料視覺效果應該變更 hello 螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="e2258-217">Your data visualization should change as shown in hello screenshot:</span></span>

    <span data-ttu-id="e2258-218">![Spark 資料視覺效果的 Tableau 輸出](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Spark 資料視覺效果的 Tableau 輸出")</span><span class="sxs-lookup"><span data-stu-id="e2258-218">![Tableau output for Spark data visualization](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau output for Spark data visualization")</span></span>
9. <span data-ttu-id="e2258-219">按一下**儲存**toosave hello 工作表。</span><span class="sxs-lookup"><span data-stu-id="e2258-219">Click **Save** toosave hello worksheet.</span></span> <span data-ttu-id="e2258-220">您可以建立儀表板，並新增一或多個工作表 tooit。</span><span class="sxs-lookup"><span data-stu-id="e2258-220">You can create dashboards and add one or more sheets tooit.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2258-221">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e2258-221">Next steps</span></span>

<span data-ttu-id="e2258-222">到目前為止您學會如何 toocreate 叢集中，建立 Spark 資料框架 tooquery 資料，並從 BI 工具存取該資料。</span><span class="sxs-lookup"><span data-stu-id="e2258-222">So far you learned how toocreate a cluster, create Spark data frames tooquery data, and then access that data from BI tools.</span></span> <span data-ttu-id="e2258-223">您現在可以看看如何 toomanage hello 叢集資源和偵錯 HDInsight Spark 叢集中執行的工作上的指示。</span><span class="sxs-lookup"><span data-stu-id="e2258-223">You can now look at instructions on how toomanage hello cluster resources and debug jobs that are running in an HDInsight Spark cluster.</span></span>

* [<span data-ttu-id="e2258-224">管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="e2258-224">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="e2258-225">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="e2258-225">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

