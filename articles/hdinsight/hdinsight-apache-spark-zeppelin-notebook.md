---
title: "在 Azure HDInsight 上搭配使用 Zeppelin Notebook 和 Apache Spark 叢集 | Microsoft Docs"
description: "如何在 Azure HDInsight 上搭配使用 Zeppelin Notebook 和 Apache Spark 叢集的逐步指示。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7fe5e3ec68e82945b972d2dd44f2cc3b8cf395d1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="56d87-103">在 Azure HDInsight 上搭配使用 Zeppelin Notebook 和 Apache Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="56d87-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="56d87-104">HDInsight Spark 叢集包含可用來執行 Spark 作業的 Zeppelin Notebook。</span><span class="sxs-lookup"><span data-stu-id="56d87-104">HDInsight Spark clusters include Zeppelin notebooks that you can use to run Spark jobs.</span></span> <span data-ttu-id="56d87-105">在本文中，您將學習如何在 HDInsight 叢集上使用 Zeppelin Notebook。</span><span class="sxs-lookup"><span data-stu-id="56d87-105">In this article, you learn how to use the Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="56d87-106">Zeppelin Notebook 僅適用於 HDInsight 3.5 上的 Spark 1.6.3 以及 HDInsight 3.6 上的 Spark 2.1.0。</span><span class="sxs-lookup"><span data-stu-id="56d87-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="56d87-107">**先決條件：**</span><span class="sxs-lookup"><span data-stu-id="56d87-107">**Prerequisites:**</span></span>

* <span data-ttu-id="56d87-108">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="56d87-108">An Azure subscription.</span></span> <span data-ttu-id="56d87-109">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="56d87-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="56d87-110">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="56d87-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="56d87-111">如需指示，請參閱[在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="56d87-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="56d87-112">啟動 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="56d87-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="56d87-113">從 Spark 叢集刀鋒視窗按一下 [叢集儀表板]，然後按一下 [Zeppelin Notebook]。</span><span class="sxs-lookup"><span data-stu-id="56d87-113">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="56d87-114">出現提示時，輸入叢集的系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="56d87-114">If prompted, enter the admin credentials for the cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="56d87-115">您也可以在瀏覽器中開啟下列 URL，來連接到您叢集的 Zeppelin Notebook。</span><span class="sxs-lookup"><span data-stu-id="56d87-115">You may also reach the Zeppelin Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="56d87-116">使用您叢集的名稱取代 **CLUSTERNAME** ：</span><span class="sxs-lookup"><span data-stu-id="56d87-116">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="56d87-117">建立新的 Notebook。</span><span class="sxs-lookup"><span data-stu-id="56d87-117">Create a new notebook.</span></span> <span data-ttu-id="56d87-118">按一下標頭窗格中的 [Notebook]，然後按一下 [建立新 Note]。</span><span class="sxs-lookup"><span data-stu-id="56d87-118">From the header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="56d87-119">![建立新的 Zeppelin Notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "建立新的 Zeppelin Notebook")</span><span class="sxs-lookup"><span data-stu-id="56d87-119">![Create a new Zeppelin notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="56d87-120">輸入 Notebook 的名稱，然後按一下 [建立記事]。</span><span class="sxs-lookup"><span data-stu-id="56d87-120">Enter a name for the notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="56d87-121">此外，請確定 Notebook 標頭顯示的是已連線狀態。</span><span class="sxs-lookup"><span data-stu-id="56d87-121">Also, make sure the notebook header shows a connected status.</span></span> <span data-ttu-id="56d87-122">右上角的綠點即表示此狀態。</span><span class="sxs-lookup"><span data-stu-id="56d87-122">It is denoted by a green dot in the top-right corner.</span></span>
   
    <span data-ttu-id="56d87-123">![Zeppelin Notebook 狀態](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin Notebook 狀態")</span><span class="sxs-lookup"><span data-stu-id="56d87-123">![Zeppelin notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="56d87-124">將範例資料載入暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="56d87-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="56d87-125">當您在 HDInsight 中建立 Spark 叢集時，系統會將範例資料檔案 **hvac.csv** 複製到相關聯的儲存體帳戶中 (位於 **\HdiSamples\SensorSampleData\hvac**)。</span><span class="sxs-lookup"><span data-stu-id="56d87-125">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="56d87-126">將以下程式碼片段貼入新 Notebook 中預設建立的空白段落。</span><span class="sxs-lookup"><span data-stu-id="56d87-126">In the empty paragraph that is created by default in the new notebook, paste the following snippet.</span></span>
   
        %livy.spark
        //The above magic instructs Zeppelin to use the Livy Scala interpreter
   
        // Create an RDD using the default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map the values in the .csv file to the schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    <span data-ttu-id="56d87-127">按下 **SHIFT + ENTER**，或是按一下 [播放] 按鈕來讓段落執行程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="56d87-127">Press **SHIFT + ENTER** or click the **Play** button for the paragraph to run the snippet.</span></span> <span data-ttu-id="56d87-128">段落右上角的狀態應該會從「準備就緒」逐一轉變成「擱置」、「執行中」及「已完成」。</span><span class="sxs-lookup"><span data-stu-id="56d87-128">The status on the right-corner of the paragraph should progress from READY, PENDING, RUNNING to FINISHED.</span></span> <span data-ttu-id="56d87-129">輸出會顯示在同一個段落的底部。</span><span class="sxs-lookup"><span data-stu-id="56d87-129">The output shows up at the bottom of the same paragraph.</span></span> <span data-ttu-id="56d87-130">螢幕擷取畫面如下所示：</span><span class="sxs-lookup"><span data-stu-id="56d87-130">The screenshot looks like the following:</span></span>
   
    <span data-ttu-id="56d87-131">![從未經處理資料建立暫存資料表](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "從未經處理資料建立暫存資料表")</span><span class="sxs-lookup"><span data-stu-id="56d87-131">![Create a temporary table from raw data](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="56d87-132">您也可以為每個段落提供標題。</span><span class="sxs-lookup"><span data-stu-id="56d87-132">You can also provide a title to each paragraph.</span></span> <span data-ttu-id="56d87-133">按一下右下角的 [設定] 圖示，然後按一下 [顯示標題]。</span><span class="sxs-lookup"><span data-stu-id="56d87-133">From the right-hand corner, click the **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="56d87-134">現在，您可以針對 **hvac** 資料表執行 Spark SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="56d87-134">You can now run Spark SQL statements on the **hvac** table.</span></span> <span data-ttu-id="56d87-135">將以下查詢貼入新段落。</span><span class="sxs-lookup"><span data-stu-id="56d87-135">Paste the following query in a new paragraph.</span></span> <span data-ttu-id="56d87-136">此查詢會擷取建築物識別碼，以及在指定日期當天每棟建築物之目標溫度與實際溫度間的差異。</span><span class="sxs-lookup"><span data-stu-id="56d87-136">The query retrieves the building ID and the difference between the target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="56d87-137">按下 **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="56d87-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="56d87-138">開頭的 **%Sql** 陳述式會告訴 Notebook 使用 Livy Scala 解譯器。</span><span class="sxs-lookup"><span data-stu-id="56d87-138">The **%sql** statement at the beginning tells the notebook to use the Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="56d87-139">以下螢幕擷取畫面顯示輸出。</span><span class="sxs-lookup"><span data-stu-id="56d87-139">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="56d87-140">![使用 Notebook 執行 Spark SQL 陳述式](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "使用 Notebook 執行 Spark SQL 陳述式")</span><span class="sxs-lookup"><span data-stu-id="56d87-140">![Run a Spark SQL statement using the notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using the notebook")</span></span>
   
     <span data-ttu-id="56d87-141">按一下顯示選項 (以矩形反白顯示) 以針對相同輸出切換不同的表示法。</span><span class="sxs-lookup"><span data-stu-id="56d87-141">Click the display options (highlighted in rectangle) to switch between different representations for the same output.</span></span> <span data-ttu-id="56d87-142">按一下 [設定] 以選擇構成輸出中索引鍵和值的項目。</span><span class="sxs-lookup"><span data-stu-id="56d87-142">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="56d87-143">在上方的螢幕擷取畫面中，索引鍵為 **buildingID**，而值為 **temp_diff** 的平均值。</span><span class="sxs-lookup"><span data-stu-id="56d87-143">The screen capture above uses **buildingID** as the key and the average of **temp_diff** as the value.</span></span>
6. <span data-ttu-id="56d87-144">您也可以在查詢中使用變數來執行 Spark SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="56d87-144">You can also run Spark SQL statements using variables in the query.</span></span> <span data-ttu-id="56d87-145">下一個程式碼片段示範如何利用您想要查詢的可能值，來定義查詢中的變數 **Temp**。</span><span class="sxs-lookup"><span data-stu-id="56d87-145">The next snippet shows how to define a variable, **Temp**, in the query with the possible values you want to query with.</span></span> <span data-ttu-id="56d87-146">當您第一次執行查詢時，下拉式清單會自動填入您指定的變數值。</span><span class="sxs-lookup"><span data-stu-id="56d87-146">When you first run the query, a drop-down is automatically populated with the values you specified for the variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="56d87-147">將此程式碼片段貼到新的段落中，然後按下 **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="56d87-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="56d87-148">以下螢幕擷取畫面顯示輸出。</span><span class="sxs-lookup"><span data-stu-id="56d87-148">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="56d87-149">![使用 Notebook 執行 Spark SQL 陳述式](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "使用 Notebook 執行 Spark SQL 陳述式")</span><span class="sxs-lookup"><span data-stu-id="56d87-149">![Run a Spark SQL statement using the notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using the notebook")</span></span>
   
    <span data-ttu-id="56d87-150">對於後續的查詢，您可以從下拉式清單選取新的值，然後再次執行查詢。</span><span class="sxs-lookup"><span data-stu-id="56d87-150">For subsequent queries, you can select a new value from the drop-down and run the query again.</span></span> <span data-ttu-id="56d87-151">按一下 [設定] 以選擇構成輸出中索引鍵和值的項目。</span><span class="sxs-lookup"><span data-stu-id="56d87-151">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="56d87-152">上述螢幕擷取畫面使用 **buildingID** 做為索引鍵、平均 **temp_diff** 做為值，而 **targettemp** 做為群組。</span><span class="sxs-lookup"><span data-stu-id="56d87-152">The screen capture above uses **buildingID** as the key, the average of **temp_diff** as the value, and **targettemp** as the group.</span></span>
7. <span data-ttu-id="56d87-153">重新啟動 Livy 解譯器以結束應用程式。</span><span class="sxs-lookup"><span data-stu-id="56d87-153">Restart the Livy interpreter to exit the application.</span></span> <span data-ttu-id="56d87-154">若要進行此操作，請在右上角按一下登入的使用者名稱，然後按一下 [解譯器]，以開啟解譯器設定。</span><span class="sxs-lookup"><span data-stu-id="56d87-154">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="56d87-155">![啟動解譯器](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive 輸出")</span><span class="sxs-lookup"><span data-stu-id="56d87-155">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="56d87-156">捲動到 Livy 解譯器設定，然後按一下 [重新啟動]。</span><span class="sxs-lookup"><span data-stu-id="56d87-156">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="56d87-157">![重新啟動 Livy 解譯器](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "重新啟動 Zeppelin 解譯器")</span><span class="sxs-lookup"><span data-stu-id="56d87-157">![Restart the Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-the-notebook"></a><span data-ttu-id="56d87-158">如何搭配 Notebook 使用外部套件？</span><span class="sxs-lookup"><span data-stu-id="56d87-158">How do I use external packages with the notebook?</span></span>
<span data-ttu-id="56d87-159">您可以在 HDInsight (Linux) 上的 Apache Spark 叢集中設定 Zeppelin Notebook，以使用不是叢集中現成隨附的由社群所提供的外部套件。</span><span class="sxs-lookup"><span data-stu-id="56d87-159">You can configure the Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) to use external, community-contributed packages that are not included out-of-the-box in the cluster.</span></span> <span data-ttu-id="56d87-160">您可以搜尋 [Maven 儲存機制](http://search.maven.org/) 來取得可用套件的完整清單。</span><span class="sxs-lookup"><span data-stu-id="56d87-160">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="56d87-161">您也可以從其他來源取得可用套件清單。</span><span class="sxs-lookup"><span data-stu-id="56d87-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="56d87-162">例如，從 [Spark 套件](http://spark-packages.org/)可以取得社群提供套件的完整清單。</span><span class="sxs-lookup"><span data-stu-id="56d87-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="56d87-163">在本文中，您將了解如何搭配 Jupyter Notebook 使用 [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) 套件。</span><span class="sxs-lookup"><span data-stu-id="56d87-163">In this article, you will see how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>

1. <span data-ttu-id="56d87-164">開啟解譯器設定。</span><span class="sxs-lookup"><span data-stu-id="56d87-164">Open interpreter settings.</span></span> <span data-ttu-id="56d87-165">在右上角按一下登入的使用者名稱，然後按一下 [解譯器]。</span><span class="sxs-lookup"><span data-stu-id="56d87-165">From the top-right corner, click the logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="56d87-166">![啟動解譯器](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive 輸出")</span><span class="sxs-lookup"><span data-stu-id="56d87-166">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="56d87-167">捲動到 Livy 解譯器設定，然後按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="56d87-167">Scroll to Livy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="56d87-168">![變更解譯器設定](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "變更解譯器設定")</span><span class="sxs-lookup"><span data-stu-id="56d87-168">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="56d87-169">新增稱為 **livy.spark.jars.packages** 的金鑰，並以 `group:id:version` 的格式設定其值。</span><span class="sxs-lookup"><span data-stu-id="56d87-169">Add a new key, called **livy.spark.jars.packages** and set its value in the format `group:id:version`.</span></span> <span data-ttu-id="56d87-170">因此，如果您想要使用 [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) 套件，您必須將金鑰值設為 `com.databricks:spark-csv_2.10:1.4.0`。</span><span class="sxs-lookup"><span data-stu-id="56d87-170">So, if you want to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set the value of the key to `com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="56d87-171">![變更解譯器設定](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "變更解譯器設定")</span><span class="sxs-lookup"><span data-stu-id="56d87-171">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="56d87-172">按一下 [儲存]，然後重新啟動 Livy 解譯器。</span><span class="sxs-lookup"><span data-stu-id="56d87-172">Click **Save** and then restart the Livy interpreter.</span></span>
4. <span data-ttu-id="56d87-173">**秘訣**︰如果您想要了解如何得出上面所輸入的金鑰值，其方法如下。</span><span class="sxs-lookup"><span data-stu-id="56d87-173">**Tip**: If you want to understand how to arrive at the value of the key entered above, here's how.</span></span>
   
    <span data-ttu-id="56d87-174">a.</span><span class="sxs-lookup"><span data-stu-id="56d87-174">a.</span></span> <span data-ttu-id="56d87-175">在「Maven 儲存機制」中找出套件。</span><span class="sxs-lookup"><span data-stu-id="56d87-175">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="56d87-176">針對本教學課程，我們使用 [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar)。</span><span class="sxs-lookup"><span data-stu-id="56d87-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="56d87-177">b.</span><span class="sxs-lookup"><span data-stu-id="56d87-177">b.</span></span> <span data-ttu-id="56d87-178">從儲存機制收集 [GroupId]、[ArtifactId] 及 [版本] 的值。</span><span class="sxs-lookup"><span data-stu-id="56d87-178">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="56d87-179">![搭配 Jupyter Notebook 使用外部封裝](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "搭配 Jupyter Notebook 使用外部封裝")</span><span class="sxs-lookup"><span data-stu-id="56d87-179">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="56d87-180">c.</span><span class="sxs-lookup"><span data-stu-id="56d87-180">c.</span></span> <span data-ttu-id="56d87-181">串連三個值，其中以冒號分隔 (**:**)。</span><span class="sxs-lookup"><span data-stu-id="56d87-181">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-the-zeppelin-notebooks-saved"></a><span data-ttu-id="56d87-182">Zeppelin Notebook 儲存在哪裡？</span><span class="sxs-lookup"><span data-stu-id="56d87-182">Where are the Zeppelin notebooks saved?</span></span>
<span data-ttu-id="56d87-183">Zeppelin Notebook 會儲存到叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="56d87-183">The Zeppelin notebooks are saved to the cluster headnodes.</span></span> <span data-ttu-id="56d87-184">因此，如果您刪除叢集，Notebook 會一併刪除。</span><span class="sxs-lookup"><span data-stu-id="56d87-184">So, if you delete the cluster, the notebooks will be deleted as well.</span></span> <span data-ttu-id="56d87-185">如果您想要保留 Notebook 以供稍後用於其他叢集上，您必須在作業執行完成後將 Notebook 匯出。</span><span class="sxs-lookup"><span data-stu-id="56d87-185">If you want to preserve your notebooks for later use on other clusters, you must export them after you have finished running the jobs.</span></span> <span data-ttu-id="56d87-186">若要匯出 Notebook，請按一下 [匯出] 圖示，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="56d87-186">To export a notebook, click the **Export** icon as shown in the image below.</span></span>

<span data-ttu-id="56d87-187">![下載 Notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "下載 Notebook")</span><span class="sxs-lookup"><span data-stu-id="56d87-187">![Download notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download the notebook")</span></span>

<span data-ttu-id="56d87-188">這會將 Notebook 以 JSON 檔案的形式儲存在下載位置中。</span><span class="sxs-lookup"><span data-stu-id="56d87-188">This saves the notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="56d87-189">Livy 工作階段管理</span><span class="sxs-lookup"><span data-stu-id="56d87-189">Livy session management</span></span>
<span data-ttu-id="56d87-190">當您在 Zeppelin Notebook 中執行第一個程式碼段落時，HDInsight Spark 叢集中便會建立新的 Livy 工作階段。</span><span class="sxs-lookup"><span data-stu-id="56d87-190">When you run the first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="56d87-191">此工作階段可供您後續建立的所有 Zeppelin Notebook 共用。</span><span class="sxs-lookup"><span data-stu-id="56d87-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="56d87-192">如果 Livy 工作階段因為某些原因而遭到刪除 (叢集重新開機等)，您就無法從 Zeppelin Notebook 執行作業。</span><span class="sxs-lookup"><span data-stu-id="56d87-192">If for some reason the Livy session is killed (cluster reboot, etc.), you will not be able to run jobs from the Zeppelin notebook.</span></span>

<span data-ttu-id="56d87-193">在這種情況下，您必須先執行下列步驟，然後才能開始從 Zeppelin Notebook 執行作業。</span><span class="sxs-lookup"><span data-stu-id="56d87-193">In such a case, you must perform the following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="56d87-194">從 Zeppelin Notebook 重新啟動 Livy 解譯器。</span><span class="sxs-lookup"><span data-stu-id="56d87-194">Restart the Livy interpreter from the Zeppelin notebook.</span></span> <span data-ttu-id="56d87-195">若要進行此操作，請在右上角按一下登入的使用者名稱，然後按一下 [解譯器]，以開啟解譯器設定。</span><span class="sxs-lookup"><span data-stu-id="56d87-195">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="56d87-196">![啟動解譯器](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive 輸出")</span><span class="sxs-lookup"><span data-stu-id="56d87-196">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="56d87-197">捲動到 Livy 解譯器設定，然後按一下 [重新啟動]。</span><span class="sxs-lookup"><span data-stu-id="56d87-197">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="56d87-198">![重新啟動 Livy 解譯器](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "重新啟動 Zeppelin 解譯器")</span><span class="sxs-lookup"><span data-stu-id="56d87-198">![Restart the Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>
3. <span data-ttu-id="56d87-199">從現有的 Zeppelin Notebook 執行程式碼單元。</span><span class="sxs-lookup"><span data-stu-id="56d87-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="56d87-200">這會在 HDInsight 叢集中建立新的 Livy 工作階段。</span><span class="sxs-lookup"><span data-stu-id="56d87-200">This creates a new Livy session in the HDInsight cluster.</span></span>

## <span data-ttu-id="56d87-201"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="56d87-201"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="56d87-202">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="56d87-202">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="56d87-203">案例</span><span class="sxs-lookup"><span data-stu-id="56d87-203">Scenarios</span></span>
* [<span data-ttu-id="56d87-204">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="56d87-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="56d87-205">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="56d87-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="56d87-206">Spark 和機器學習服務：使用 HDInsight 中的 Spark 來預測食品檢查結果</span><span class="sxs-lookup"><span data-stu-id="56d87-206">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="56d87-207">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="56d87-207">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="56d87-208">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="56d87-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="56d87-209">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="56d87-209">Create and run applications</span></span>
* [<span data-ttu-id="56d87-210">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="56d87-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="56d87-211">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="56d87-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="56d87-212">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="56d87-212">Tools and extensions</span></span>
* [<span data-ttu-id="56d87-213">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons (使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式來建立和提交 Spark Scala 應用程式)</span><span class="sxs-lookup"><span data-stu-id="56d87-213">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="56d87-214">使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式遠端偵錯 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="56d87-214">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="56d87-215">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="56d87-215">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="56d87-216">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="56d87-216">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="56d87-217">在電腦上安裝 Jupyter 並連接到 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="56d87-217">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="56d87-218">管理資源</span><span class="sxs-lookup"><span data-stu-id="56d87-218">Manage resources</span></span>
* [<span data-ttu-id="56d87-219">在 Azure HDInsight 中管理 Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="56d87-219">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="56d87-220">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="56d87-220">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







