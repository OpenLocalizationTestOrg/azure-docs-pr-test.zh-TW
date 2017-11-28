---
title: "在 Azure 資料湖存放區中的 Apache Spark tooanalyze 資料 aaaUse |Microsoft 文件"
description: "執行 Spark 作業 tooanalyze 資料儲存在 Azure 資料湖存放區"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 1f174323-c17b-428c-903d-04f0e272784c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 3b7f628f7a8114d2ca6f3f9219ce107905f1c818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-spark-cluster-tooanalyze-data-in-data-lake-store"></a><span data-ttu-id="7416b-103">使用中 Data Lake Store 的 HDInsight Spark 叢集 tooanalyze 資料</span><span class="sxs-lookup"><span data-stu-id="7416b-103">Use HDInsight Spark cluster tooanalyze data in Data Lake Store</span></span>

<span data-ttu-id="7416b-104">在本教學課程中，您可以使用 Jupyter 筆記本可用與 HDInsight Spark 叢集 toorun 從 Data Lake Store 帳戶讀取資料的工作。</span><span class="sxs-lookup"><span data-stu-id="7416b-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters toorun a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7416b-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="7416b-105">Prerequisites</span></span>

* <span data-ttu-id="7416b-106">Azure Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7416b-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="7416b-107">請遵循指示 hello[開始使用 Azure 資料湖存放區使用 hello Azure 入口網站](../data-lake-store/data-lake-store-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="7416b-107">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="7416b-108">以 Data Lake Store 做為儲存體的 Azure HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="7416b-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="7416b-109">請遵循指示 hello[建立與使用 Azure 入口網站的 Data Lake Store 的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="7416b-109">Follow hello instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-hello-data"></a><span data-ttu-id="7416b-110">準備 hello 資料</span><span class="sxs-lookup"><span data-stu-id="7416b-110">Prepare hello data</span></span>

> [!NOTE]
> <span data-ttu-id="7416b-111">您不需要 tooperform 此步驟中如果您已經建立 hello HDInsight 叢集具有做為預設儲存體的資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="7416b-111">You do not need tooperform this step if you have created hello HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="7416b-112">hello 叢集建立程序在您建立 hello 叢集時所指定的 hello Data Lake Store 帳戶新增一些範例資料。</span><span class="sxs-lookup"><span data-stu-id="7416b-112">hello cluster creation processes adds some sample data in hello Data Lake Store account that you specify while creating hello cluster.</span></span> <span data-ttu-id="7416b-113">略過 toohello 區段[資料湖存放區的使用 HDInsight Spark 叢集](#use-an-hdinsight-spark-cluster-with-data-lake-store)。</span><span class="sxs-lookup"><span data-stu-id="7416b-113">Skip toohello section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="7416b-114">如果您的 HDInsight 叢集與資料湖存放區做為建立額外的儲存體和 Azure 儲存體 Blob 做為預設儲存體，您應該先複製某些範例資料 toohello Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7416b-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data toohello Data Lake Store account.</span></span> <span data-ttu-id="7416b-115">您可以使用 hello hello 與 hello HDInsight 叢集相關聯的 Azure 儲存體 Blob 的取樣資料。</span><span class="sxs-lookup"><span data-stu-id="7416b-115">You can use hello sample data from hello Azure Storage Blob associated with hello HDInsight cluster.</span></span> <span data-ttu-id="7416b-116">您可以使用 hello [ADLCopy 工具](http://aka.ms/downloadadlcopy)toodo 如此。</span><span class="sxs-lookup"><span data-stu-id="7416b-116">You can use hello [ADLCopy tool](http://aka.ms/downloadadlcopy) toodo so.</span></span> <span data-ttu-id="7416b-117">下載並安裝 hello 工具從 hello 連結。</span><span class="sxs-lookup"><span data-stu-id="7416b-117">Download and install hello tool from hello link.</span></span>

1. <span data-ttu-id="7416b-118">開啟命令提示字元並瀏覽 toohello AdlCopy 安裝的目錄，通常`%HOMEPATH%\Documents\adlcopy`。</span><span class="sxs-lookup"><span data-stu-id="7416b-118">Open a command prompt and navigate toohello directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="7416b-119">從 hello 來源容器 tooa 資料湖存放區執行下列命令 toocopy hello 特定的 blob:</span><span class="sxs-lookup"><span data-stu-id="7416b-119">Run hello following command toocopy a specific blob from hello source container tooa Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="7416b-120">複製 hello **HVAC.csv**範例資料檔案儲存在**/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello Azure Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7416b-120">Copy hello **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello Azure Data Lake Store account.</span></span> <span data-ttu-id="7416b-121">hello 程式碼片段看起來應該像：</span><span class="sxs-lookup"><span data-stu-id="7416b-121">hello code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="7416b-122">請確定 hello 檔案和路徑名稱會出現在 hello 適當的大小寫。</span><span class="sxs-lookup"><span data-stu-id="7416b-122">Make sure you hello file and path names are in hello proper case.</span></span>
   >
   >
3. <span data-ttu-id="7416b-123">您將會提示的 tooenter hello 認證 hello 您擁有的 Data Lake Store 帳戶所在的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7416b-123">You will be prompted tooenter hello credentials for hello Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="7416b-124">您會看到類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="7416b-124">You will see an output similar toohello following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="7416b-125">hello 資料檔 (**HVAC.csv**) 將會複製資料夾下**/hvac** hello Data Lake Store 帳戶中。</span><span class="sxs-lookup"><span data-stu-id="7416b-125">hello data file (**HVAC.csv**) will be copied under a folder **/hvac** in hello Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="7416b-126">使用具有 Data Lake Store 的 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="7416b-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="7416b-127">從 hello [Azure 入口網站](https://portal.azure.com/)，從 hello 開始面板中，按一下 Spark 叢集中的 hello 磚 （如果您釘選它 toohello 開始面板）。</span><span class="sxs-lookup"><span data-stu-id="7416b-127">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="7416b-128">您也可以導覽 tooyour 叢集下的**瀏覽所有** > **HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="7416b-128">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="7416b-129">從 hello Spark 叢集刀鋒視窗中，按一下 **快速連結**，然後從 hello**叢集儀表板**刀鋒視窗中，按一下  **Jupyter 筆記本**。</span><span class="sxs-lookup"><span data-stu-id="7416b-129">From hello Spark cluster blade, click **Quick Links**, and then from hello **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="7416b-130">如果出現提示，請輸入 hello 叢集 hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="7416b-130">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7416b-131">您也可能由下列 URL 在瀏覽器中開啟 hello 叢集到達 hello Jupyter 筆記本。</span><span class="sxs-lookup"><span data-stu-id="7416b-131">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="7416b-132">取代**CLUSTERNAME** hello 名稱，為您的叢集：</span><span class="sxs-lookup"><span data-stu-id="7416b-132">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="7416b-133">建立新的 Notebook。</span><span class="sxs-lookup"><span data-stu-id="7416b-133">Create a new notebook.</span></span> <span data-ttu-id="7416b-134">按一下 新增，然後按一下PySpark。</span><span class="sxs-lookup"><span data-stu-id="7416b-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="7416b-135">![建立新的 Jupyter Notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "建立新的 Jupyter Notebook")</span><span class="sxs-lookup"><span data-stu-id="7416b-135">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="7416b-136">因為您建立使用 hello PySpark 核心筆記本，您不需要 toocreate 任何內容明確。</span><span class="sxs-lookup"><span data-stu-id="7416b-136">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="7416b-137">hello Spark 和 Hive 內容將會自動為您建立執行 hello 第一個程式碼儲存格時。</span><span class="sxs-lookup"><span data-stu-id="7416b-137">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="7416b-138">您可以開始匯入此案例所需的 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="7416b-138">You can start by importing hello types required for this scenario.</span></span> <span data-ttu-id="7416b-139">toodo，貼上下列程式碼片段中的資料格和按 hello **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="7416b-139">toodo so, paste hello following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="7416b-140">每次您在 Jupyter 執行作業，將會顯示您的 web 瀏覽器視窗標題**（忙碌）**狀態以及 hello 筆記本標題。</span><span class="sxs-lookup"><span data-stu-id="7416b-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="7416b-141">您也會看到實心圓的下一個 toohello **PySpark** hello 右上角中的文字。</span><span class="sxs-lookup"><span data-stu-id="7416b-141">You will also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="7416b-142">Hello 作業完成之後，這會變更 tooa 空心圓圈。</span><span class="sxs-lookup"><span data-stu-id="7416b-142">After hello job is completed, this will change tooa hollow circle.</span></span>

     <span data-ttu-id="7416b-143">![Jupyter Notebook 作業的狀態](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Jupyter Notebook 作業的狀態")</span><span class="sxs-lookup"><span data-stu-id="7416b-143">![Status of a Jupyter notebook job](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="7416b-144">範例資料載入暫存資料表使用 hello **HVAC.csv**複製 toohello Data Lake Store 帳戶的檔案。</span><span class="sxs-lookup"><span data-stu-id="7416b-144">Load sample data into a temporary table using hello **HVAC.csv** file you copied toohello Data Lake Store account.</span></span> <span data-ttu-id="7416b-145">您可以存取 hello 資料中使用下列的 URL 模式的 hello hello Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7416b-145">You can access hello data in hello Data Lake Store account using hello following URL pattern.</span></span>

    * <span data-ttu-id="7416b-146">如果您有做為預設儲存體的資料湖存放區，HVAC.csv 會在 hello 路徑類似 toohello 下列 URL:</span><span class="sxs-lookup"><span data-stu-id="7416b-146">If you have Data Lake Store as default storage, HVAC.csv will be at hello path similar toohello following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="7416b-147">或者，您也可以使用縮短的格式，例如 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="7416b-147">Or, you could also use a shortened format such as hello following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="7416b-148">如果您有額外的存放裝置與資料湖存放區，HVAC.csv 會在 hello 複製的位置，例如：</span><span class="sxs-lookup"><span data-stu-id="7416b-148">If you have Data Lake Store as additional storage, HVAC.csv will be at hello location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="7416b-149">空白儲存格，下列程式碼範例中，貼上 hello 取代**MYDATALAKESTORE**與您的 Data Lake Store 帳戶名稱，請按**SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="7416b-149">In an empty cell, paste hello following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="7416b-150">這個程式碼範例會註冊 hello 資料至暫存資料表稱為**hvac**。</span><span class="sxs-lookup"><span data-stu-id="7416b-150">This code example registers hello data into a temporary table called **hvac**.</span></span>

            # Load hello data. hello path below assumes Data Lake Store is default storage for hello Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create hello schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse hello data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register hello data fram as a table toorun queries against
            hvacdf.registerTempTable("hvac")

6. <span data-ttu-id="7416b-151">因為您使用 PySpark 核心，您現在可以直接執行 SQL 查詢 hello 暫存資料表上**hvac**您剛才所建立的使用 hello`%%sql`識別常數。</span><span class="sxs-lookup"><span data-stu-id="7416b-151">Because you are using a PySpark kernel, you can now directly run a SQL query on hello temporary table **hvac** that you just created by using hello `%%sql` magic.</span></span> <span data-ttu-id="7416b-152">如需有關 hello`%%sql`識別常數，以及其他適用於 hello PySpark 核心中，我們看到[Jupyter notebook Spark HDInsight 叢集上可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)。</span><span class="sxs-lookup"><span data-stu-id="7416b-152">For more information about hello `%%sql` magic, as well as other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="7416b-153">一旦 hello 工作順利完成時，預設會顯示 hello 遵循表格式輸出。</span><span class="sxs-lookup"><span data-stu-id="7416b-153">Once hello job is completed successfully, hello following tabular output is displayed by default.</span></span>

      <span data-ttu-id="7416b-154">![查詢結果的資料表輸出](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "查詢結果的資料表輸出")</span><span class="sxs-lookup"><span data-stu-id="7416b-154">![Table output of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="7416b-155">您也可以查看其他視覺效果中的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="7416b-155">You can also see hello results in other visualizations as well.</span></span> <span data-ttu-id="7416b-156">例如，區域圖相同的輸出會如下 hello 示 hello。</span><span class="sxs-lookup"><span data-stu-id="7416b-156">For example, an area graph for hello same output would look like hello following.</span></span>

     <span data-ttu-id="7416b-157">![查詢結果的區域圖](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "查詢結果的區域圖")</span><span class="sxs-lookup"><span data-stu-id="7416b-157">![Area graph of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="7416b-158">當您完成執行 hello 應用程式之後，您應該關閉 hello 筆記本 toorelease hello 資源。</span><span class="sxs-lookup"><span data-stu-id="7416b-158">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="7416b-159">toodo 的話，從 hello**檔案**hello 筆記本功能表按一下**關閉而停止**。</span><span class="sxs-lookup"><span data-stu-id="7416b-159">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="7416b-160">這將會關機並關閉 hello 筆記本。</span><span class="sxs-lookup"><span data-stu-id="7416b-160">This will shutdown and close hello notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7416b-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7416b-161">Next steps</span></span>

* [<span data-ttu-id="7416b-162">Apache Spark 叢集上建立獨立 Scala 應用程式 toorun</span><span class="sxs-lookup"><span data-stu-id="7416b-162">Create a standalone Scala application toorun on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="7416b-163">在 Azure Toolkit for HDInsight Spark Linux 叢集的 IntelliJ toocreate Spark 應用程式中使用 HDInsight Tools</span><span class="sxs-lookup"><span data-stu-id="7416b-163">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="7416b-164">在 Azure Toolkit for Eclipse HDInsight Spark Linux 叢集 toocreate Spark 應用程式中使用 HDInsight Tools</span><span class="sxs-lookup"><span data-stu-id="7416b-164">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
