---
title: "在 Azure HDInsight 叢集化使用 Apache Spark aaaUse 運貨用飛艇筆記本 |Microsoft 文件"
description: "使用 Apache Spark toouse 運貨用飛艇筆記本 Azure HDInsight 上的叢集的逐步指示。"
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
ms.openlocfilehash: 3ab479cfccc7fd38a9bf6a9fb4f5928beec8ff7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="ce416-103">在 Azure HDInsight 上搭配使用 Zeppelin Notebook 和 Apache Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="ce416-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="ce416-104">HDInsight Spark 叢集包含運貨用飛艇筆記本，您可以使用 toorun Spark 作業。</span><span class="sxs-lookup"><span data-stu-id="ce416-104">HDInsight Spark clusters include Zeppelin notebooks that you can use toorun Spark jobs.</span></span> <span data-ttu-id="ce416-105">在本文中，您學會如何 toouse hello 運貨用飛艇筆記本在 HDInsight 叢集上。</span><span class="sxs-lookup"><span data-stu-id="ce416-105">In this article, you learn how toouse hello Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="ce416-106">Zeppelin Notebook 僅適用於 HDInsight 3.5 上的 Spark 1.6.3 以及 HDInsight 3.6 上的 Spark 2.1.0。</span><span class="sxs-lookup"><span data-stu-id="ce416-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="ce416-107">**先決條件：**</span><span class="sxs-lookup"><span data-stu-id="ce416-107">**Prerequisites:**</span></span>

* <span data-ttu-id="ce416-108">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ce416-108">An Azure subscription.</span></span> <span data-ttu-id="ce416-109">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="ce416-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="ce416-110">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="ce416-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="ce416-111">如需指示，請參閱[在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="ce416-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="ce416-112">啟動 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="ce416-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="ce416-113">從 hello Spark 叢集刀鋒視窗中，按一下 **叢集儀表板**，然後按一下**運貨用飛艇筆記本**。</span><span class="sxs-lookup"><span data-stu-id="ce416-113">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="ce416-114">如果出現提示，請輸入 hello 叢集 hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="ce416-114">If prompted, enter hello admin credentials for hello cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ce416-115">您也可能由下列 URL 在瀏覽器中開啟 hello 叢集到達 hello 運貨用飛艇筆記型電腦。</span><span class="sxs-lookup"><span data-stu-id="ce416-115">You may also reach hello Zeppelin Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="ce416-116">取代**CLUSTERNAME** hello 名稱，為您的叢集：</span><span class="sxs-lookup"><span data-stu-id="ce416-116">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="ce416-117">建立新的 Notebook。</span><span class="sxs-lookup"><span data-stu-id="ce416-117">Create a new notebook.</span></span> <span data-ttu-id="ce416-118">從 hello 標頭窗格中，按一下 **筆記本**，然後按一下**建立新便箋**。</span><span class="sxs-lookup"><span data-stu-id="ce416-118">From hello header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="ce416-119">![建立新的 Zeppelin Notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "建立新的 Zeppelin Notebook")</span><span class="sxs-lookup"><span data-stu-id="ce416-119">![Create a new Zeppelin notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="ce416-120">輸入 hello 筆記本的名稱，然後按一下**建立注意**。</span><span class="sxs-lookup"><span data-stu-id="ce416-120">Enter a name for hello notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="ce416-121">此外，請確定 hello 筆記本標頭會顯示已連線的狀態。</span><span class="sxs-lookup"><span data-stu-id="ce416-121">Also, make sure hello notebook header shows a connected status.</span></span> <span data-ttu-id="ce416-122">它是由綠點 hello 右上角中表示。</span><span class="sxs-lookup"><span data-stu-id="ce416-122">It is denoted by a green dot in hello top-right corner.</span></span>
   
    <span data-ttu-id="ce416-123">![Zeppelin Notebook 狀態](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin Notebook 狀態")</span><span class="sxs-lookup"><span data-stu-id="ce416-123">![Zeppelin notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="ce416-124">將範例資料載入暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="ce416-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="ce416-125">當您建立 HDInsight，hello 範例資料檔中的 Spark 叢集**hvac.csv**，是儲存體帳戶相關聯的複製的 toohello **\HdiSamples\SensorSampleData\hvac**。</span><span class="sxs-lookup"><span data-stu-id="ce416-125">When you create a Spark cluster in HDInsight, hello sample data file, **hvac.csv**, is copied toohello associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="ce416-126">在 hello 空白段落所建立的預設 hello 新筆記本中，貼上下列程式碼片段的 hello。</span><span class="sxs-lookup"><span data-stu-id="ce416-126">In hello empty paragraph that is created by default in hello new notebook, paste hello following snippet.</span></span>
   
        %livy.spark
        //hello above magic instructs Zeppelin toouse hello Livy Scala interpreter
   
        // Create an RDD using hello default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map hello values in hello .csv file toohello schema
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
   
    <span data-ttu-id="ce416-127">按**SHIFT + ENTER**或按一下 hello**播放**hello 段落 toorun hello 程式碼片段的按鈕。</span><span class="sxs-lookup"><span data-stu-id="ce416-127">Press **SHIFT + ENTER** or click hello **Play** button for hello paragraph toorun hello snippet.</span></span> <span data-ttu-id="ce416-128">hello 右上角的 hello 段落的 hello 狀態應該從好時，暫止、 正在執行 tooFINISHED 進度。</span><span class="sxs-lookup"><span data-stu-id="ce416-128">hello status on hello right-corner of hello paragraph should progress from READY, PENDING, RUNNING tooFINISHED.</span></span> <span data-ttu-id="ce416-129">在 hello hello 底部顯示 hello 輸出相同的 paragraph。</span><span class="sxs-lookup"><span data-stu-id="ce416-129">hello output shows up at hello bottom of hello same paragraph.</span></span> <span data-ttu-id="ce416-130">hello 螢幕擷取畫面看起來像下列 hello:</span><span class="sxs-lookup"><span data-stu-id="ce416-130">hello screenshot looks like hello following:</span></span>
   
    <span data-ttu-id="ce416-131">![從未經處理資料建立暫存資料表](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "從未經處理資料建立暫存資料表")</span><span class="sxs-lookup"><span data-stu-id="ce416-131">![Create a temporary table from raw data](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="ce416-132">您也可以提供標題 tooeach 段落。</span><span class="sxs-lookup"><span data-stu-id="ce416-132">You can also provide a title tooeach paragraph.</span></span> <span data-ttu-id="ce416-133">從 hello 右上角，按一下 hello**設定**圖示，然後再按一下**顯示標題**。</span><span class="sxs-lookup"><span data-stu-id="ce416-133">From hello right-hand corner, click hello **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="ce416-134">您現在可以執行 Spark SQL 陳述式上 hello **hvac**資料表。</span><span class="sxs-lookup"><span data-stu-id="ce416-134">You can now run Spark SQL statements on hello **hvac** table.</span></span> <span data-ttu-id="ce416-135">貼上下列查詢在新的段落中的 hello。</span><span class="sxs-lookup"><span data-stu-id="ce416-135">Paste hello following query in a new paragraph.</span></span> <span data-ttu-id="ce416-136">hello 查詢會擷取 hello 建置識別碼和 hello hello 目標與實際溫度的每個建置在特定日期之間的差異。</span><span class="sxs-lookup"><span data-stu-id="ce416-136">hello query retrieves hello building ID and hello difference between hello target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="ce416-137">按下 **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="ce416-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="ce416-138">hello **%sql** hello 開頭的陳述式會告知 hello 筆記本 toouse hello 晚總 Scala 直譯器。</span><span class="sxs-lookup"><span data-stu-id="ce416-138">hello **%sql** statement at hello beginning tells hello notebook toouse hello Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="ce416-139">hello 下列螢幕擷取畫面顯示 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="ce416-139">hello following screenshot shows hello output.</span></span>
   
    <span data-ttu-id="ce416-140">![執行使用 hello 筆記本的 Spark SQL 陳述式](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "執行使用 hello 筆記本的 Spark SQL 陳述式")</span><span class="sxs-lookup"><span data-stu-id="ce416-140">![Run a Spark SQL statement using hello notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using hello notebook")</span></span>
   
     <span data-ttu-id="ce416-141">按一下 hello 顯示選項 （反白顯示在矩形） tooswitch hello 不同表示之間相同的輸出。</span><span class="sxs-lookup"><span data-stu-id="ce416-141">Click hello display options (highlighted in rectangle) tooswitch between different representations for hello same output.</span></span> <span data-ttu-id="ce416-142">按一下**設定**toochoose 哪些 consitutes hello 索引鍵和 hello 輸出中的值。</span><span class="sxs-lookup"><span data-stu-id="ce416-142">Click **Settings** toochoose what consitutes hello key and values in hello output.</span></span> <span data-ttu-id="ce416-143">hello 使用上面的螢幕擷取**buildingID**作為 hello 索引鍵和 hello 平均**temp_diff** hello 值。</span><span class="sxs-lookup"><span data-stu-id="ce416-143">hello screen capture above uses **buildingID** as hello key and hello average of **temp_diff** as hello value.</span></span>
6. <span data-ttu-id="ce416-144">您也可以執行在 hello 查詢中使用變數的 Spark SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="ce416-144">You can also run Spark SQL statements using variables in hello query.</span></span> <span data-ttu-id="ce416-145">hello 下一步的程式碼片段說明如何 toodefine 變數， **Temp**，要與 tooquery hello hello 可能值的查詢中。</span><span class="sxs-lookup"><span data-stu-id="ce416-145">hello next snippet shows how toodefine a variable, **Temp**, in hello query with hello possible values you want tooquery with.</span></span> <span data-ttu-id="ce416-146">當您第一次執行 hello 查詢時，下拉式清單會自動填入 hello hello 變數您指定的值。</span><span class="sxs-lookup"><span data-stu-id="ce416-146">When you first run hello query, a drop-down is automatically populated with hello values you specified for hello variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="ce416-147">將此程式碼片段貼到新的段落中，然後按下 **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="ce416-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="ce416-148">hello 下列螢幕擷取畫面顯示 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="ce416-148">hello following screenshot shows hello output.</span></span>
   
    <span data-ttu-id="ce416-149">![執行使用 hello 筆記本的 Spark SQL 陳述式](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "執行使用 hello 筆記本的 Spark SQL 陳述式")</span><span class="sxs-lookup"><span data-stu-id="ce416-149">![Run a Spark SQL statement using hello notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using hello notebook")</span></span>
   
    <span data-ttu-id="ce416-150">對於後續的查詢，您可以從 hello 下拉式清單中選取新的值，然後再次執行 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="ce416-150">For subsequent queries, you can select a new value from hello drop-down and run hello query again.</span></span> <span data-ttu-id="ce416-151">按一下**設定**toochoose 哪些 consitutes hello 索引鍵和 hello 輸出中的值。</span><span class="sxs-lookup"><span data-stu-id="ce416-151">Click **Settings** toochoose what consitutes hello key and values in hello output.</span></span> <span data-ttu-id="ce416-152">hello 使用上面的螢幕擷取**buildingID** hello 索引鍵，hello 平均**temp_diff** hello 值和**targettemp**為 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="ce416-152">hello screen capture above uses **buildingID** as hello key, hello average of **temp_diff** as hello value, and **targettemp** as hello group.</span></span>
7. <span data-ttu-id="ce416-153">重新啟動 hello 晚總直譯器 tooexit hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce416-153">Restart hello Livy interpreter tooexit hello application.</span></span> <span data-ttu-id="ce416-154">toodo，開啟即可 hello 登入使用者名稱，從 hello 右上角的 解譯器設定，然後按一下**直譯器**。</span><span class="sxs-lookup"><span data-stu-id="ce416-154">toodo so, open interpreter settings by clicking hello logged in user name from hello top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="ce416-155">![啟動解譯器](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive 輸出")</span><span class="sxs-lookup"><span data-stu-id="ce416-155">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="ce416-156">捲動 tooLivy 直譯器設定，然後按一下**重新啟動**。</span><span class="sxs-lookup"><span data-stu-id="ce416-156">Scroll tooLivy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="ce416-157">![重新啟動 hello 晚總 intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "hello 運貨用飛艇 intepreter 重新啟動")</span><span class="sxs-lookup"><span data-stu-id="ce416-157">![Restart hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart hello Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-hello-notebook"></a><span data-ttu-id="ce416-158">如何使用與 hello 筆記本的外部封裝？</span><span class="sxs-lookup"><span data-stu-id="ce416-158">How do I use external packages with hello notebook?</span></span>
<span data-ttu-id="ce416-159">您可以設定 hello 運貨用飛艇筆記本 HDInsight (Linux) toouse 外部、 社群貢獻的套件不包含--現成的 hello 叢集中的 Apache Spark 叢集中。</span><span class="sxs-lookup"><span data-stu-id="ce416-159">You can configure hello Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) toouse external, community-contributed packages that are not included out-of-the-box in hello cluster.</span></span> <span data-ttu-id="ce416-160">您可以搜尋 hello [Maven 儲存機制](http://search.maven.org/)如 hello 的封裝所提供的完整清單。</span><span class="sxs-lookup"><span data-stu-id="ce416-160">You can search hello [Maven repository](http://search.maven.org/) for hello complete list of packages that are available.</span></span> <span data-ttu-id="ce416-161">您也可以從其他來源取得可用套件清單。</span><span class="sxs-lookup"><span data-stu-id="ce416-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="ce416-162">例如，從 [Spark 套件](http://spark-packages.org/)可以取得社群提供套件的完整清單。</span><span class="sxs-lookup"><span data-stu-id="ce416-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="ce416-163">在本文中，您會看到如何 toouse hello [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar)與 hello Jupyter 筆記本的封裝。</span><span class="sxs-lookup"><span data-stu-id="ce416-163">In this article, you will see how toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with hello Jupyter notebook.</span></span>

1. <span data-ttu-id="ce416-164">開啟解譯器設定。</span><span class="sxs-lookup"><span data-stu-id="ce416-164">Open interpreter settings.</span></span> <span data-ttu-id="ce416-165">從 hello 右上角，按一下 hello 登入使用者名稱，然後按一下**直譯器**。</span><span class="sxs-lookup"><span data-stu-id="ce416-165">From hello top-right corner, click hello logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="ce416-166">![啟動解譯器](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive 輸出")</span><span class="sxs-lookup"><span data-stu-id="ce416-166">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="ce416-167">捲動 tooLivy 直譯器設定，然後按一下**編輯**。</span><span class="sxs-lookup"><span data-stu-id="ce416-167">Scroll tooLivy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="ce416-168">![變更解譯器設定](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "變更解譯器設定")</span><span class="sxs-lookup"><span data-stu-id="ce416-168">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="ce416-169">加入新機碼，呼叫**livy.spark.jars.packages**並設定其值格式 hello `group:id:version`。</span><span class="sxs-lookup"><span data-stu-id="ce416-169">Add a new key, called **livy.spark.jars.packages** and set its value in hello format `group:id:version`.</span></span> <span data-ttu-id="ce416-170">因此，如果您想要 toouse hello [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar)封裝時，您必須設定 hello hello 機碼值太`com.databricks:spark-csv_2.10:1.4.0`。</span><span class="sxs-lookup"><span data-stu-id="ce416-170">So, if you want toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set hello value of hello key too`com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="ce416-171">![變更解譯器設定](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "變更解譯器設定")</span><span class="sxs-lookup"><span data-stu-id="ce416-171">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="ce416-172">按一下**儲存**然後重新啟動 hello 晚總直譯器。</span><span class="sxs-lookup"><span data-stu-id="ce416-172">Click **Save** and then restart hello Livy interpreter.</span></span>
4. <span data-ttu-id="ce416-173">**提示**： 如果您想的 toounderstand tooarrive hello hello 機碼值在這裡的上方輸入的方式如何。</span><span class="sxs-lookup"><span data-stu-id="ce416-173">**Tip**: If you want toounderstand how tooarrive at hello value of hello key entered above, here's how.</span></span>
   
    <span data-ttu-id="ce416-174">a.</span><span class="sxs-lookup"><span data-stu-id="ce416-174">a.</span></span> <span data-ttu-id="ce416-175">在 hello Maven 儲存機制中，找出 hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="ce416-175">Locate hello package in hello Maven Repository.</span></span> <span data-ttu-id="ce416-176">針對本教學課程，我們使用 [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar)。</span><span class="sxs-lookup"><span data-stu-id="ce416-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="ce416-177">b.</span><span class="sxs-lookup"><span data-stu-id="ce416-177">b.</span></span> <span data-ttu-id="ce416-178">從 hello 儲存機制，蒐集 hello 值**GroupId**， **ArtifactId**，和**版本**。</span><span class="sxs-lookup"><span data-stu-id="ce416-178">From hello repository, gather hello values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="ce416-179">![搭配 Jupyter Notebook 使用外部封裝](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "搭配 Jupyter Notebook 使用外部封裝")</span><span class="sxs-lookup"><span data-stu-id="ce416-179">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="ce416-180">c.</span><span class="sxs-lookup"><span data-stu-id="ce416-180">c.</span></span> <span data-ttu-id="ce416-181">串連 hello 三個值，並以分號 (**:**)。</span><span class="sxs-lookup"><span data-stu-id="ce416-181">Concatenate hello three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-hello-zeppelin-notebooks-saved"></a><span data-ttu-id="ce416-182">在哪裡？ hello 運貨用飛艇筆記本儲存</span><span class="sxs-lookup"><span data-stu-id="ce416-182">Where are hello Zeppelin notebooks saved?</span></span>
<span data-ttu-id="ce416-183">hello 運貨用飛艇筆記本會儲存 toohello 叢集 headnodes。</span><span class="sxs-lookup"><span data-stu-id="ce416-183">hello Zeppelin notebooks are saved toohello cluster headnodes.</span></span> <span data-ttu-id="ce416-184">因此，如果您刪除 hello 叢集時，會一併刪除 hello 筆記型電腦。</span><span class="sxs-lookup"><span data-stu-id="ce416-184">So, if you delete hello cluster, hello notebooks will be deleted as well.</span></span> <span data-ttu-id="ce416-185">如果您想 toopreserve 您筆記本供稍後使用其他叢集上，您必須將它們匯出您完成執行後，hello 作業。</span><span class="sxs-lookup"><span data-stu-id="ce416-185">If you want toopreserve your notebooks for later use on other clusters, you must export them after you have finished running hello jobs.</span></span> <span data-ttu-id="ce416-186">tooexport 筆記本中，按一下 hello**匯出**圖示 hello 圖所示。</span><span class="sxs-lookup"><span data-stu-id="ce416-186">tooexport a notebook, click hello **Export** icon as shown in hello image below.</span></span>

<span data-ttu-id="ce416-187">![下載筆記本](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "下載 hello 筆記本")</span><span class="sxs-lookup"><span data-stu-id="ce416-187">![Download notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download hello notebook")</span></span>

<span data-ttu-id="ce416-188">這可以節省 hello 筆記本作為下載位置在 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="ce416-188">This saves hello notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="ce416-189">Livy 工作階段管理</span><span class="sxs-lookup"><span data-stu-id="ce416-189">Livy session management</span></span>
<span data-ttu-id="ce416-190">當您執行第一個程式碼段落 hello 運貨用飛艇筆記本中時，HDInsight Spark 叢集中建立新的晚總工作階段。</span><span class="sxs-lookup"><span data-stu-id="ce416-190">When you run hello first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="ce416-191">此工作階段可供您後續建立的所有 Zeppelin Notebook 共用。</span><span class="sxs-lookup"><span data-stu-id="ce416-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="ce416-192">如果某些原因 hello 晚總工作階段已終止 （叢集重新開機等），您將無法從 hello 運貨用飛艇筆記本能夠 toorun 作業。</span><span class="sxs-lookup"><span data-stu-id="ce416-192">If for some reason hello Livy session is killed (cluster reboot, etc.), you will not be able toorun jobs from hello Zeppelin notebook.</span></span>

<span data-ttu-id="ce416-193">在這種情況下，您必須執行下列步驟，才能開始執行作業從運貨用飛艇筆記本 hello。</span><span class="sxs-lookup"><span data-stu-id="ce416-193">In such a case, you must perform hello following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="ce416-194">重新啟動 hello 從 hello 運貨用飛艇筆記本晚總直譯器。</span><span class="sxs-lookup"><span data-stu-id="ce416-194">Restart hello Livy interpreter from hello Zeppelin notebook.</span></span> <span data-ttu-id="ce416-195">toodo，開啟即可 hello 登入使用者名稱，從 hello 右上角的 解譯器設定，然後按一下**直譯器**。</span><span class="sxs-lookup"><span data-stu-id="ce416-195">toodo so, open interpreter settings by clicking hello logged in user name from hello top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="ce416-196">![啟動解譯器](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive 輸出")</span><span class="sxs-lookup"><span data-stu-id="ce416-196">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="ce416-197">捲動 tooLivy 直譯器設定，然後按一下**重新啟動**。</span><span class="sxs-lookup"><span data-stu-id="ce416-197">Scroll tooLivy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="ce416-198">![重新啟動 hello 晚總 intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "hello 運貨用飛艇 intepreter 重新啟動")</span><span class="sxs-lookup"><span data-stu-id="ce416-198">![Restart hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart hello Zeppelin intepreter")</span></span>
3. <span data-ttu-id="ce416-199">從現有的 Zeppelin Notebook 執行程式碼單元。</span><span class="sxs-lookup"><span data-stu-id="ce416-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="ce416-200">這會建立新的工作階段晚總 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ce416-200">This creates a new Livy session in hello HDInsight cluster.</span></span>

## <span data-ttu-id="ce416-201"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="ce416-201"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="ce416-202">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="ce416-202">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="ce416-203">案例</span><span class="sxs-lookup"><span data-stu-id="ce416-203">Scenarios</span></span>
* [<span data-ttu-id="ce416-204">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="ce416-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="ce416-205">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="ce416-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="ce416-206">機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark</span><span class="sxs-lookup"><span data-stu-id="ce416-206">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="ce416-207">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="ce416-207">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="ce416-208">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="ce416-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="ce416-209">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="ce416-209">Create and run applications</span></span>
* [<span data-ttu-id="ce416-210">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="ce416-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="ce416-211">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="ce416-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="ce416-212">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="ce416-212">Tools and extensions</span></span>
* [<span data-ttu-id="ce416-213">HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 個應用程式</span><span class="sxs-lookup"><span data-stu-id="ce416-213">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="ce416-214">從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="ce416-214">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="ce416-215">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="ce416-215">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="ce416-216">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="ce416-216">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="ce416-217">在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="ce416-217">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="ce416-218">管理資源</span><span class="sxs-lookup"><span data-stu-id="ce416-218">Manage resources</span></span>
* [<span data-ttu-id="ce416-219">管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="ce416-219">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="ce416-220">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="ce416-220">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







