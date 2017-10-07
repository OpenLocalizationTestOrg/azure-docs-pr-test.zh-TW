---
title: "aaaRun Azure HDInsight Spark 叢集上的互動式查詢 |Microsoft 文件"
description: "如何 toocreate Apache Spark 叢集在 HDInsight 上的 HDInsight Spark 快速入門。"
keywords: "spark 快速入門, 互動式 spark, 互動式查詢, hdinsight spark, azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 3864eba50eb3828a9ecb657ded88080e1974585f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="6e356-104">在 HDInsight Spark 叢集上執行互動式查詢</span><span class="sxs-lookup"><span data-stu-id="6e356-104">Run interactive queries on an HDInsight Spark cluster</span></span>

<span data-ttu-id="6e356-105">在本文中，您可以使用 Jupyter 筆記本 toorun 互動式 Spark SQL 查詢的 Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="6e356-105">In this article, you use a Jupyter notebook toorun interactive Spark SQL queries against a Spark cluster.</span></span> <span data-ttu-id="6e356-106">Jupyter 筆記本是擴充 hello 主控台為基礎的互動體驗 toohello Web 瀏覽器型應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e356-106">Jupyter notebook is a browser-based application that extends hello console-based interactive experience toohello Web.</span></span> <span data-ttu-id="6e356-107">如需詳細資訊，請參閱[hello Jupyter 筆記本](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html)。</span><span class="sxs-lookup"><span data-stu-id="6e356-107">For more information, see [hello Jupyter notebook](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).</span></span>

<span data-ttu-id="6e356-108">此教學課程中，您可以使用 hello **PySpark** hello Jupyter 筆記本 toorun 互動式 Spark SQL 查詢中的核心。</span><span class="sxs-lookup"><span data-stu-id="6e356-108">For this tutorial, you use hello **PySpark** kernel in hello Jupyter notebook toorun an interactive Spark SQL query.</span></span> <span data-ttu-id="6e356-109">HDInsight 叢集上的 Jupyter Notebook 也支援其他兩個核心：**PySpark3** 和 **Spark**。</span><span class="sxs-lookup"><span data-stu-id="6e356-109">Jupyter notebooks on HDInsight clusters also support two other kernels - **PySpark3** and **Spark**.</span></span> <span data-ttu-id="6e356-110">如需有關 hello 核心和使用的 hello 優點**PySpark**，請參閱[在 HDInsight 中的使用 Jupyter 筆記本核心使用 Apache Spark 叢集](hdinsight-apache-spark-jupyter-notebook-kernels.md)。</span><span class="sxs-lookup"><span data-stu-id="6e356-110">For more information about hello kernels, and hello benefits of using **PySpark**, see [Use Jupyter notebook kernels with Apache Spark clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e356-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="6e356-111">Prerequisites</span></span>

* <span data-ttu-id="6e356-112">**Azure HDInsight Spark 叢集**。</span><span class="sxs-lookup"><span data-stu-id="6e356-112">**An Azure HDInsight Spark cluster**.</span></span> <span data-ttu-id="6e356-113">如需指示，請參閱[在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="6e356-113">For instructions, see [Create an Apache Spark cluster in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="create-a-jupyter-notebook-toorun-interactive-queries"></a><span data-ttu-id="6e356-114">建立 Jupyter 筆記本 toorun 互動式查詢</span><span class="sxs-lookup"><span data-stu-id="6e356-114">Create a Jupyter notebook toorun interactive queries</span></span>

<span data-ttu-id="6e356-115">toorun 查詢，我們會使用預設 hello 與 hello 叢集相關聯的儲存體中可用的範例資料。</span><span class="sxs-lookup"><span data-stu-id="6e356-115">toorun queries, we use sample data that is by default available in hello storage associated with hello cluster.</span></span> <span data-ttu-id="6e356-116">不過，您必須先將該資料載入到 Spark 作為資料框架。</span><span class="sxs-lookup"><span data-stu-id="6e356-116">However, you must first load that data into Spark as a dataframe.</span></span> <span data-ttu-id="6e356-117">一旦您擁有 hello 資料框架，您可以使用來 hello Jupyter 筆記本執行查詢。</span><span class="sxs-lookup"><span data-stu-id="6e356-117">Once you have hello dataframe, you can run queries on it using hello Jupyter notebook.</span></span> <span data-ttu-id="6e356-118">在本節中，您要查看如何：</span><span class="sxs-lookup"><span data-stu-id="6e356-118">In this section, you look at how to:</span></span>

* <span data-ttu-id="6e356-119">註冊範例資料集作為 Spark 資料框架。</span><span class="sxs-lookup"><span data-stu-id="6e356-119">Register a sample data set as a Spark dataframe.</span></span>
* <span data-ttu-id="6e356-120">Hello 資料框架上執行查詢。</span><span class="sxs-lookup"><span data-stu-id="6e356-120">Run queries on hello dataframe.</span></span>

1. <span data-ttu-id="6e356-121">開啟 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="6e356-121">Open hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="6e356-122">如果您選擇 toopin hello 叢集 toohello 儀表板，按一下 hello 叢集磚的 hello 儀表板 toolaunch hello 叢集刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6e356-122">If you opted toopin hello cluster toohello dashboard, click hello cluster tile from hello dashboard toolaunch hello cluster blade.</span></span>

    <span data-ttu-id="6e356-123">如果您沒有不固定 hello 叢集 toohello 儀表板，從 hello 左窗格中，按一下**HDInsight 叢集**，然後按一下您所建立的 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="6e356-123">If you did not pin hello cluster toohello dashboard, from hello left pane, click **HDInsight clusters**, and then click hello cluster you created.</span></span>

3. <span data-ttu-id="6e356-124">從 快速連結，按一下 叢集儀表板，然後按一下Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="6e356-124">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="6e356-125">如果出現提示，請輸入 hello 叢集 hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="6e356-125">If prompted, enter hello admin credentials for hello cluster.</span></span>

   <span data-ttu-id="6e356-126">![開啟 Jupyter 筆記本 toorun 互動式 Spark SQL 查詢](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "開啟 Jupyter 筆記本 toorun 互動式 Spark SQL 查詢")</span><span class="sxs-lookup"><span data-stu-id="6e356-126">![Open Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook toorun interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="6e356-127">您也可以透過下列 URL 在瀏覽器中開啟 hello 叢集存取 hello Jupyter 筆記本。</span><span class="sxs-lookup"><span data-stu-id="6e356-127">You may also access hello Jupyter notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="6e356-128">取代**CLUSTERNAME** hello 名稱，為您的叢集：</span><span class="sxs-lookup"><span data-stu-id="6e356-128">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="6e356-129">建立 Notebook。</span><span class="sxs-lookup"><span data-stu-id="6e356-129">Create a notebook.</span></span> <span data-ttu-id="6e356-130">按一下 新增，然後按一下PySpark。</span><span class="sxs-lookup"><span data-stu-id="6e356-130">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="6e356-131">![建立 Jupyter 筆記本 toorun 互動式 Spark SQL 查詢](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "建立 Jupyter 筆記本 toorun 互動式 Spark SQL 查詢")</span><span class="sxs-lookup"><span data-stu-id="6e356-131">![Create a Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook toorun interactive Spark SQL query")</span></span>

   <span data-ttu-id="6e356-132">建立新的記事本，並開啟 hello 名稱 Untitled(Untitled.pynb)。</span><span class="sxs-lookup"><span data-stu-id="6e356-132">A new notebook is created and opened with hello name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="6e356-133">按一下頂端 hello hello 筆記本名稱，然後輸入易記的名稱，如果您想。</span><span class="sxs-lookup"><span data-stu-id="6e356-133">Click hello notebook name at hello top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="6e356-134">![提供查詢的名稱 hello Jupter 筆記本 toorun 互動式 Spark 從](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "提供 hello Jupter 筆記本 toorun 互動式 Spark 中查詢的名稱")</span><span class="sxs-lookup"><span data-stu-id="6e356-134">![Provide a name for hello Jupter notebook toorun interactive Spark query from](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Provide a name for hello Jupter notebook toorun interactive Spark query from")</span></span>

5. <span data-ttu-id="6e356-135">貼上 hello 下列空的資料格中的程式碼，然後按下**SHIFT + ENTER** toorun hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="6e356-135">Paste hello following code in an empty cell, and then press **SHIFT + ENTER** toorun hello code.</span></span> <span data-ttu-id="6e356-136">hello 程式碼會匯入這個案例所需的 hello 類型：</span><span class="sxs-lookup"><span data-stu-id="6e356-136">hello code imports hello types required for this scenario:</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="6e356-137">因為您建立使用 hello PySpark 核心筆記本，您不需要 toocreate 任何內容明確。</span><span class="sxs-lookup"><span data-stu-id="6e356-137">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="6e356-138">hello Spark 和 Hive 內容會自動建立，當您執行 hello 第一個程式碼儲存格。</span><span class="sxs-lookup"><span data-stu-id="6e356-138">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span>

    <span data-ttu-id="6e356-139">![互動式 Spark SQL 查詢的狀態](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "互動式 Spark SQL 查詢的狀態")</span><span class="sxs-lookup"><span data-stu-id="6e356-139">![Status of interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status of interactive Spark SQL query")</span></span>

    <span data-ttu-id="6e356-140">每次您在 Jupyter 執行互動式的查詢，您的 web 瀏覽器視窗標題顯示**（忙碌）**狀態以及 hello 筆記本標題。</span><span class="sxs-lookup"><span data-stu-id="6e356-140">Every time you run an interactive query in Jupyter, your web browser window title shows a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="6e356-141">另請參閱實心圓的下一個 toohello **PySpark** hello 右上角中的文字。</span><span class="sxs-lookup"><span data-stu-id="6e356-141">You also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="6e356-142">Hello 作業完成之後，它會變更 tooa 空心圓圈。</span><span class="sxs-lookup"><span data-stu-id="6e356-142">After hello job is completed, it changes tooa hollow circle.</span></span>

6. <span data-ttu-id="6e356-143">Hello 資料載入的 Spark 叢集之前，可讓我們看它的快照集。</span><span class="sxs-lookup"><span data-stu-id="6e356-143">Before you load hello data into a Spark cluster, let us look a snapshot of it.</span></span> <span data-ttu-id="6e356-144">hello 在本教學課程使用範例資料可做為 CSV 檔案 HDInsight Spark 叢集，在所有**\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**。</span><span class="sxs-lookup"><span data-stu-id="6e356-144">hello sample data used in this tutorial is available as a CSV file on all HDInsight Spark clusters at **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**.</span></span> <span data-ttu-id="6e356-145">hello 資料擷取建築物 hello 溫度的變化。</span><span class="sxs-lookup"><span data-stu-id="6e356-145">hello data captures hello temperature variations of a building.</span></span> <span data-ttu-id="6e356-146">以下是 hello hello 資料前的幾個資料列。</span><span class="sxs-lookup"><span data-stu-id="6e356-146">Here are hello first few rows of hello data.</span></span>

    <span data-ttu-id="6e356-147">![互動式 Spark SQL 查詢的資料快照集](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "互動式 Spark SQL 查詢的資料快照集")</span><span class="sxs-lookup"><span data-stu-id="6e356-147">![Snapshot of data for interactive Spark SQL query](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot of data for interactive Spark SQL query")</span></span>

6. <span data-ttu-id="6e356-148">建立資料框架和暫存資料表 (**hvac**) 藉由執行下列程式碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="6e356-148">Create a dataframe and a temporary table (**hvac**) by running hello following code.</span></span> <span data-ttu-id="6e356-149">此教學課程中，我們不要建立 hello 的所有資料行 hello 暫存資料表中做為比較的 toohello hello 未經處理的 CSV 資料中的資料行。</span><span class="sxs-lookup"><span data-stu-id="6e356-149">For this tutorial, we do not create all hello columns in hello temporary table as compared toohello columns in hello raw CSV data.</span></span> 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

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

7. <span data-ttu-id="6e356-150">Hello 資料表建立之後，執行互動式查詢 hello 資料上使用下列程式碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="6e356-150">Once hello table is created, run interactive query on hello data, use hello following code.</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   <span data-ttu-id="6e356-151">因為您使用 PySpark 核心，您現在可以直接執行互動式的 SQL 查詢 hello 暫存資料表上**hvac**您建立使用 hello`%%sql`識別常數。</span><span class="sxs-lookup"><span data-stu-id="6e356-151">Because you are using a PySpark kernel, you can now directly run an interactive SQL query on hello temporary table **hvac** that you created by using hello `%%sql` magic.</span></span> <span data-ttu-id="6e356-152">如需有關 hello`%%sql`魔法和其他適用於 hello PySpark 核心中，我們看到[Jupyter notebook Spark HDInsight 叢集上可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)。</span><span class="sxs-lookup"><span data-stu-id="6e356-152">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

   <span data-ttu-id="6e356-153">根據預設，會顯示 hello 遵循表格式輸出。</span><span class="sxs-lookup"><span data-stu-id="6e356-153">hello following tabular output is displayed by default.</span></span>

     <span data-ttu-id="6e356-154">![互動式 Spark 查詢結果的資料表輸出](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "互動式 Spark 查詢結果的資料表輸出")</span><span class="sxs-lookup"><span data-stu-id="6e356-154">![Table output of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Table output of interactive Spark query result")</span></span>

    <span data-ttu-id="6e356-155">您也可以查看其他視覺效果中的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="6e356-155">You can also see hello results in other visualizations as well.</span></span> <span data-ttu-id="6e356-156">例如，區域圖相同的輸出會如下 hello 示 hello。</span><span class="sxs-lookup"><span data-stu-id="6e356-156">For example, an area graph for hello same output would look like hello following.</span></span>

    <span data-ttu-id="6e356-157">![互動式 Spark 查詢結果的區域圖表](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "互動式 Spark 查詢結果的區域圖表")</span><span class="sxs-lookup"><span data-stu-id="6e356-157">![Area graph of interactive Spark query result](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Area graph of interactive Spark query result")</span></span>

9. <span data-ttu-id="6e356-158">您完成執行後，hello 應用程式，請關閉 hello 筆記本 toorelease hello 叢集資源。</span><span class="sxs-lookup"><span data-stu-id="6e356-158">Shut down hello notebook toorelease hello cluster resources after you have finished running hello application.</span></span> <span data-ttu-id="6e356-159">toodo 的話，從 hello**檔案**hello 筆記本功能表按一下**關閉而停止**。</span><span class="sxs-lookup"><span data-stu-id="6e356-159">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

## <a name="next-step"></a><span data-ttu-id="6e356-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6e356-160">Next step</span></span>

<span data-ttu-id="6e356-161">在這個發行項您學到如何 toorun 使用 Jupyter 筆記本的 Spark 中的互動式查詢。</span><span class="sxs-lookup"><span data-stu-id="6e356-161">In this article you learned how toorun interactive queries in Spark using Jupyter notebook.</span></span> <span data-ttu-id="6e356-162">前進 toohello 如何您的 Spark 中註冊的 hello 資料可以提取下一個發行項 toosee 到 Power BI 等 Tableau BI 分析工具。</span><span class="sxs-lookup"><span data-stu-id="6e356-162">Advance toohello next article toosee how hello data you registered in Spark can be pulled into a BI analytics tool such as Power BI and Tableau.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="6e356-163">使用資料視覺效果工具搭配 Azure HDInsight 的 Spark BI</span><span class="sxs-lookup"><span data-stu-id="6e356-163">Spark BI using data visualization tools with Azure HDInsight</span></span>](hdinsight-apache-spark-use-bi-tools.md)




