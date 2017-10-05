---
title: "使用 Apache Spark 來分析 Azure Data Lake Store 中的資料 | Microsoft Docs"
description: "執行 Spark 作業來分析 Azure Data Lake Store 中所儲存的資料"
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
ms.openlocfilehash: 66f115c4f348ccaeb8855568ba1ad50faa442173
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-hdinsight-spark-cluster-to-analyze-data-in-data-lake-store"></a><span data-ttu-id="e28f2-103">使用 HDInsight Spark 叢集來分析 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="e28f2-103">Use HDInsight Spark cluster to analyze data in Data Lake Store</span></span>

<span data-ttu-id="e28f2-104">在本教學課程中，您可使用 HDInsight Spark 叢集提供的 Jupyter Notebook 來執行可從 Data Lake Store 帳戶讀取資料的作業。</span><span class="sxs-lookup"><span data-stu-id="e28f2-104">In this tutorial, you use Jupyter notebook available with HDInsight Spark clusters to run a job that reads data from a Data Lake Store account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e28f2-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="e28f2-105">Prerequisites</span></span>

* <span data-ttu-id="e28f2-106">Azure Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e28f2-106">Azure Data Lake Store account.</span></span> <span data-ttu-id="e28f2-107">遵循 [使用 Azure 入口網站開始使用 Azure 資料湖存放區](../data-lake-store/data-lake-store-get-started-portal.md)的指示。</span><span class="sxs-lookup"><span data-stu-id="e28f2-107">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

* <span data-ttu-id="e28f2-108">以 Data Lake Store 做為儲存體的 Azure HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="e28f2-108">Azure HDInsight Spark cluster with Data Lake Store as storage.</span></span> <span data-ttu-id="e28f2-109">如需相關指示，請參閱[使用 Azure 入口網站建立具有 Data Lake Store 的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="e28f2-109">Follow the instructions at [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    
## <a name="prepare-the-data"></a><span data-ttu-id="e28f2-110">準備資料</span><span class="sxs-lookup"><span data-stu-id="e28f2-110">Prepare the data</span></span>

> [!NOTE]
> <span data-ttu-id="e28f2-111">如果您建立具 Data Lake Store 的 HDInsight 叢集做為預設儲存體，則不需執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="e28f2-111">You do not need to perform this step if you have created the HDInsight cluster with Data Lake Store as default storage.</span></span> <span data-ttu-id="e28f2-112">叢集建立程序會在您建立叢集時所指定的 Data Lake Store 帳戶中新增一些範例資料。</span><span class="sxs-lookup"><span data-stu-id="e28f2-112">The cluster creation processes adds some sample data in the Data Lake Store account that you specify while creating the cluster.</span></span> <span data-ttu-id="e28f2-113">請略過[使用具有 Data Lake Store 的 HDInsight Spark 叢集](#use-an-hdinsight-spark-cluster-with-data-lake-store)一節。</span><span class="sxs-lookup"><span data-stu-id="e28f2-113">Skip to the section [Use HDInsight Spark cluster with Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).</span></span>
>
>

<span data-ttu-id="e28f2-114">如果您建立具有 Data Lake Store 的 HDInsight Spark 叢集做為額外的儲存體並以 Azure 儲存體 Blob 做為預設儲存體，您應該先將某些範例資料複製到 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e28f2-114">If you created an HDInsight cluster with Data Lake Store as additional storage and Azure Storage Blob as default storage, you should first copy over some sample data to the Data Lake Store account.</span></span> <span data-ttu-id="e28f2-115">您可以使用與 HDInsight 叢集相關聯之 Azure 儲存體 Blob 中的資料範例。</span><span class="sxs-lookup"><span data-stu-id="e28f2-115">You can use the sample data from the Azure Storage Blob associated with the HDInsight cluster.</span></span> <span data-ttu-id="e28f2-116">您可以使用 [ADLCopy 工具](http://aka.ms/downloadadlcopy) 來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="e28f2-116">You can use the [ADLCopy tool](http://aka.ms/downloadadlcopy) to do so.</span></span> <span data-ttu-id="e28f2-117">從連結下載並安裝此工具。</span><span class="sxs-lookup"><span data-stu-id="e28f2-117">Download and install the tool from the link.</span></span>

1. <span data-ttu-id="e28f2-118">開啟命令提示字元，並瀏覽至安裝 AdlCopy 的目錄，通常是 `%HOMEPATH%\Documents\adlcopy`。</span><span class="sxs-lookup"><span data-stu-id="e28f2-118">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>

2. <span data-ttu-id="e28f2-119">執行下列命令，將特定的 Blob 從來源容器複製到資料湖存放區：</span><span class="sxs-lookup"><span data-stu-id="e28f2-119">Run the following command to copy a specific blob from the source container to a Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="e28f2-120">將位於 **/HdiSamples/HdiSamples/SensorSampleData/hvac/** 的 **HVAC.csv** 範例資料檔複製到 Azure Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e28f2-120">Copy the **HVAC.csv** sample data file at **/HdiSamples/HdiSamples/SensorSampleData/hvac/** to the Azure Data Lake Store account.</span></span> <span data-ttu-id="e28f2-121">程式碼片段看起來應該如下：</span><span class="sxs-lookup"><span data-stu-id="e28f2-121">The code snippet should look like:</span></span>

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > <span data-ttu-id="e28f2-122">確定檔案和路徑名稱的大小寫正確。</span><span class="sxs-lookup"><span data-stu-id="e28f2-122">Make sure you the file and path names are in the proper case.</span></span>
   >
   >
3. <span data-ttu-id="e28f2-123">系統會提示您輸入您 Data Lake Store 帳戶所在 Azure 訂用帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="e28f2-123">You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="e28f2-124">您將看到類似以下的輸出：</span><span class="sxs-lookup"><span data-stu-id="e28f2-124">You will see an output similar to the following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    <span data-ttu-id="e28f2-125">資料檔 (**HVAC.csv**) 將被複製到 Data Lake Store 帳戶中的 **/hvac** 資料夾底下。</span><span class="sxs-lookup"><span data-stu-id="e28f2-125">The data file (**HVAC.csv**) will be copied under a folder **/hvac** in the Data Lake Store account.</span></span>

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a><span data-ttu-id="e28f2-126">使用具有 Data Lake Store 的 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="e28f2-126">Use an HDInsight Spark cluster with Data Lake Store</span></span>

1. <span data-ttu-id="e28f2-127">在 [Azure 入口網站](https://portal.azure.com/)的開始面板中，按一下您的 Spark 叢集磚 (如果您已將其釘選到開始面板)。</span><span class="sxs-lookup"><span data-stu-id="e28f2-127">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="e28f2-128">您也可以按一下 [瀏覽全部] > [HDInsight 叢集] 來瀏覽至您的叢集。</span><span class="sxs-lookup"><span data-stu-id="e28f2-128">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>

2. <span data-ttu-id="e28f2-129">在 Spark 叢集刀鋒視窗中按一下 [快速連結]，然後在 [叢集儀表板] 刀鋒視窗中按一下 [Jupyter Notebook]。</span><span class="sxs-lookup"><span data-stu-id="e28f2-129">From the Spark cluster blade, click **Quick Links**, and then from the **Cluster Dashboard** blade, click **Jupyter Notebook**.</span></span> <span data-ttu-id="e28f2-130">出現提示時，輸入叢集的系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="e28f2-130">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e28f2-131">您也可以在瀏覽器中開啟下列 URL，來連接到您的叢集的 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="e28f2-131">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="e28f2-132">使用您叢集的名稱取代 **CLUSTERNAME** ：</span><span class="sxs-lookup"><span data-stu-id="e28f2-132">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. <span data-ttu-id="e28f2-133">建立新的 Notebook。</span><span class="sxs-lookup"><span data-stu-id="e28f2-133">Create a new notebook.</span></span> <span data-ttu-id="e28f2-134">按一下 [新增]，然後按一下 [PySpark]。</span><span class="sxs-lookup"><span data-stu-id="e28f2-134">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="e28f2-135">![建立新的 Jupyter Notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "建立新的 Jupyter Notebook")</span><span class="sxs-lookup"><span data-stu-id="e28f2-135">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>

4. <span data-ttu-id="e28f2-136">您使用 PySpark 核心建立 Notebook，因此不需要明確建立任何內容。</span><span class="sxs-lookup"><span data-stu-id="e28f2-136">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="e28f2-137">當您執行第一個程式碼儲存格時，系統會自動為您建立 Spark 和 Hive 內容。</span><span class="sxs-lookup"><span data-stu-id="e28f2-137">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="e28f2-138">首先，您可以匯入此案例所需的類型。</span><span class="sxs-lookup"><span data-stu-id="e28f2-138">You can start by importing the types required for this scenario.</span></span> <span data-ttu-id="e28f2-139">方法是將下列程式碼片段貼到儲存格中，然後按下 **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="e28f2-139">To do so, paste the following code snippet in a cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.sql.types import *

    <span data-ttu-id="e28f2-140">每當您在 Jupyter 中執行作業時，網頁瀏覽器視窗標題將會顯示 Notebook 標題和 **(忙碌)** 狀態。</span><span class="sxs-lookup"><span data-stu-id="e28f2-140">Every time you run a job in Jupyter, your web browser window title will show a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="e28f2-141">您也會在右上角的 **PySpark** 文字旁看到一個實心圓。</span><span class="sxs-lookup"><span data-stu-id="e28f2-141">You will also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="e28f2-142">工作完成後，實心圓將變成空心圓。</span><span class="sxs-lookup"><span data-stu-id="e28f2-142">After the job is completed, this will change to a hollow circle.</span></span>

     <span data-ttu-id="e28f2-143">![Jupyter Notebook 作業的狀態](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Jupyter Notebook 作業的狀態")</span><span class="sxs-lookup"><span data-stu-id="e28f2-143">![Status of a Jupyter notebook job](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status of a Jupyter notebook job")</span></span>

5. <span data-ttu-id="e28f2-144">使用您複製到 Data Lake Store 帳戶的 **HVAC.csv** 檔案，將範例資料載入到暫存資料表中。</span><span class="sxs-lookup"><span data-stu-id="e28f2-144">Load sample data into a temporary table using the **HVAC.csv** file you copied to the Data Lake Store account.</span></span> <span data-ttu-id="e28f2-145">您可以使用下列 URL 模式，存取 Data Lake Store 帳戶中的資料。</span><span class="sxs-lookup"><span data-stu-id="e28f2-145">You can access the data in the Data Lake Store account using the following URL pattern.</span></span>

    * <span data-ttu-id="e28f2-146">如果您以 Data Lake Store 做為預設儲存體，HVAC.csv 會位於類似下列 URL 的路徑︰</span><span class="sxs-lookup"><span data-stu-id="e28f2-146">If you have Data Lake Store as default storage, HVAC.csv will be at the path similar to the following URL:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        <span data-ttu-id="e28f2-147">或者，您也可以使用縮短的格式如下︰</span><span class="sxs-lookup"><span data-stu-id="e28f2-147">Or, you could also use a shortened format such as the following:</span></span>

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * <span data-ttu-id="e28f2-148">如果您以 Data Lake Store 做為額外儲存體，HVAC.csv 會位於您複製它的位置，例如︰</span><span class="sxs-lookup"><span data-stu-id="e28f2-148">If you have Data Lake Store as additional storage, HVAC.csv will be at the location where you copied it, such as:</span></span>

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     <span data-ttu-id="e28f2-149">在空白儲存格中，貼上下列程式碼範例、使用您的 Data Lake Store 帳戶名稱取代 **MYDATALAKESTORE**，然後按 **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="e28f2-149">In an empty cell, paste the following code example, replace **MYDATALAKESTORE** with your Data Lake Store account name, and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="e28f2-150">此程式碼範例會將資料註冊到名為 **hvac**的暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="e28f2-150">This code example registers the data into a temporary table called **hvac**.</span></span>

            # Load the data. The path below assumes Data Lake Store is default storage for the Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create the schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse the data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register the data fram as a table to run queries against
            hvacdf.registerTempTable("hvac")

6. <span data-ttu-id="e28f2-151">由於您使用的是 PySpark 核心，因此現在可直接在您剛才使用 `%%sql` magic 建立的暫存資料表 **hvac** 上執行 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="e28f2-151">Because you are using a PySpark kernel, you can now directly run a SQL query on the temporary table **hvac** that you just created by using the `%%sql` magic.</span></span> <span data-ttu-id="e28f2-152">如需 `%%sql` magic 及 PySpark 核心提供的其他 magic 的詳細資訊，請參閱 [使用 Spark HDInsight 叢集之 Jupyter Notebook 上可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)。</span><span class="sxs-lookup"><span data-stu-id="e28f2-152">For more information about the `%%sql` magic, as well as other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. <span data-ttu-id="e28f2-153">一旦工作順利完成後，預設會顯示下列表格式輸出。</span><span class="sxs-lookup"><span data-stu-id="e28f2-153">Once the job is completed successfully, the following tabular output is displayed by default.</span></span>

      <span data-ttu-id="e28f2-154">![查詢結果的資料表輸出](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "查詢結果的資料表輸出")</span><span class="sxs-lookup"><span data-stu-id="e28f2-154">![Table output of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table output of query result")</span></span>

     <span data-ttu-id="e28f2-155">您也可以查看其他視覺效果中的結果。</span><span class="sxs-lookup"><span data-stu-id="e28f2-155">You can also see the results in other visualizations as well.</span></span> <span data-ttu-id="e28f2-156">例如，相同輸出的區域圖看起來會如下所示。</span><span class="sxs-lookup"><span data-stu-id="e28f2-156">For example, an area graph for the same output would look like the following.</span></span>

     <span data-ttu-id="e28f2-157">![查詢結果的區域圖](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "查詢結果的區域圖")</span><span class="sxs-lookup"><span data-stu-id="e28f2-157">![Area graph of query result](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Area graph of query result")</span></span>

8. <span data-ttu-id="e28f2-158">應用程式執行完畢之後，您應該要關閉 Notebook 來釋放資源。</span><span class="sxs-lookup"><span data-stu-id="e28f2-158">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="e28f2-159">若要這樣做，請從 Notebook 的 [檔案] 功能表中，按一下 [關閉並停止]。</span><span class="sxs-lookup"><span data-stu-id="e28f2-159">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="e28f2-160">這樣就能夠結束並關閉 Notebook。</span><span class="sxs-lookup"><span data-stu-id="e28f2-160">This will shutdown and close the notebook.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e28f2-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e28f2-161">Next steps</span></span>

* [<span data-ttu-id="e28f2-162">建立獨立 Scala 應用程式以在 Apache Spark 叢集上執行</span><span class="sxs-lookup"><span data-stu-id="e28f2-162">Create a standalone Scala application to run on Apache Spark cluster</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="e28f2-163">使用適用於 IntelliJ 的 Azure 工具組中的 HDInsight 工具建立 HDInsight Spark Linux 叢集的 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="e28f2-163">Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="e28f2-164">使用適用於 Eclipse 的 Azure 工具組中的 HDInsight 工具建立 HDInsight Spark Linux 叢集的 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="e28f2-164">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications for HDInsight Spark Linux cluster</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
