---
title: "在 Azure HDInsight 叢集 aaaCreate Apache Spark |Microsoft 文件"
description: "如何 toocreate Apache Spark 叢集在 HDInsight 上的 HDInsight Spark 快速入門。"
keywords: "spark 快速入門, 互動式 spark, 互動式查詢, hdinsight spark, azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 91f41e6a-d463-4eb4-83ef-7bbb1f4556cc
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 002f71b3cd4fb315d4a556cebc9263026515ec4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a><span data-ttu-id="282a5-104">在 Azure HDInsight 中建立 Apache Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="282a5-104">Create an Apache Spark cluster in Azure HDInsight</span></span>

<span data-ttu-id="282a5-105">在本文中，您學會 toocreate Apache Spark 中 Azure HDInsight 叢集的方式。</span><span class="sxs-lookup"><span data-stu-id="282a5-105">In this article, you learn how toocreate an Apache Spark cluster in Azure HDInsight.</span></span> <span data-ttu-id="282a5-106">如需 Spark on HDInsight 相關資訊，請參閱[概觀：Azure HDInsight 上的 Apache Spark](hdinsight-apache-spark-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="282a5-106">For information on Spark on HDInsight, see [Overview: Apache Spark on Azure HDInsight](hdinsight-apache-spark-overview.md).</span></span>

   <span data-ttu-id="282a5-107">![快速入門步驟 toocreate Apache Spark 叢集描述 Azure HDInsight 上的圖表](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "使用 Apache Spark 中 HDInsight Spark 快速入門。說明的步驟︰建立叢集；執行 Spark 互動式查詢")</span><span class="sxs-lookup"><span data-stu-id="282a5-107">![Quickstart diagram describing steps toocreate an Apache Spark cluster on Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark quickstart using Apache Spark in HDInsight. Steps illustrated: create a cluster; run Spark interactive query")</span></span>

## <a name="prerequisites"></a><span data-ttu-id="282a5-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="282a5-108">Prerequisites</span></span>

* <span data-ttu-id="282a5-109">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="282a5-109">**An Azure subscription**.</span></span> <span data-ttu-id="282a5-110">開始進行本教學課程之前，您必須擁有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="282a5-110">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="282a5-111">請參閱[立即建立免費的 Azure 帳戶](https://azure.microsoft.com/free)。</span><span class="sxs-lookup"><span data-stu-id="282a5-111">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

## <a name="create-hdinsight-spark-cluster"></a><span data-ttu-id="282a5-112">建立 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="282a5-112">Create HDInsight Spark cluster</span></span>

<span data-ttu-id="282a5-113">在本節中，您會使用 [Azure Resource Manager 範本](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/)來建立 HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="282a5-113">In this section, you create an HDInsight Spark cluster using an [Azure Resource Manager template](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span></span> <span data-ttu-id="282a5-114">如需其他叢集建立方法，請參閱 [建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="282a5-114">For other cluster creation methods, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="282a5-115">按一下下列映像 tooopen hello 範本 hello Azure 入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="282a5-115">Click hello following image tooopen hello template in hello Azure portal.</span></span>         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="282a5-116">輸入下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="282a5-116">Enter hello following values:</span></span>

    <span data-ttu-id="282a5-117">![使用 Azure Resource Manager 範本建立 HDInsight Spark 叢集](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "在 HDInsight 中使用 Azure Resource Manager 範本建立 Spark 叢集")</span><span class="sxs-lookup"><span data-stu-id="282a5-117">![Create HDInsight Spark cluster using an Azure Resource Manager template](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Create Spark cluster in HDInsight using an Azure Resource Manager template")</span></span>

    * <span data-ttu-id="282a5-118">**訂用帳戶**：針對此叢集選取您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="282a5-118">**Subscription**: Select your Azure subscription for this cluster.</span></span>
    * <span data-ttu-id="282a5-119">**資源群組**：建立資源群組，或選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="282a5-119">**Resource group**: Create a resource group or select an existing one.</span></span> <span data-ttu-id="282a5-120">資源群組是使用的 toomanage 專案的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="282a5-120">Resource group is used toomanage Azure resources for your projects.</span></span>
    * <span data-ttu-id="282a5-121">**位置**： 選取 hello 資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="282a5-121">**Location**: Select a location for hello resource group.</span></span> <span data-ttu-id="282a5-122">hello 範本會使用這個位置建立 hello 叢集也與 hello 預設叢集存放區。</span><span class="sxs-lookup"><span data-stu-id="282a5-122">hello template uses this location for creating hello cluster as well as for hello default cluster storage.</span></span>
    * <span data-ttu-id="282a5-123">**ClusterName**： 輸入您想 toocreate hello HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="282a5-123">**ClusterName**: Enter a name for hello HDInsight cluster that you want toocreate.</span></span>
    * <span data-ttu-id="282a5-124">**Spark 版本**： 選取**2.0**做為您想 tooinstall hello 叢集上的 hello 版本。</span><span class="sxs-lookup"><span data-stu-id="282a5-124">**Spark version**: Select **2.0** as hello version that you want tooinstall on hello cluster.</span></span>
    * <span data-ttu-id="282a5-125">**叢集登入名稱和密碼**: hello 預設登入名稱是系統管理員。</span><span class="sxs-lookup"><span data-stu-id="282a5-125">**Cluster login name and password**: hello default login name is admin.</span></span>
    * <span data-ttu-id="282a5-126">SSH 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="282a5-126">**SSH user name and password**.</span></span>

   <span data-ttu-id="282a5-127">請記下這些值。</span><span class="sxs-lookup"><span data-stu-id="282a5-127">Write down these values.</span></span>  <span data-ttu-id="282a5-128">您稍後在 hello 教學課程需要它們。</span><span class="sxs-lookup"><span data-stu-id="282a5-128">You need them later in hello tutorial.</span></span>

3. <span data-ttu-id="282a5-129">選取**toohello 條款和條件前面所述，即表示我同意**，選取**Pin toodashboard**，然後按一下**購買**。</span><span class="sxs-lookup"><span data-stu-id="282a5-129">Select **I agree toohello terms and conditions stated above**, select **Pin toodashboard**, and then click **Purchase**.</span></span> <span data-ttu-id="282a5-130">您可以看到新的圖格，標題為「提交範本部署的部署」。</span><span class="sxs-lookup"><span data-stu-id="282a5-130">You can see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="282a5-131">它會採用約 20 分鐘 toocreate hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="282a5-131">It takes about 20 minutes toocreate hello cluster.</span></span>

<span data-ttu-id="282a5-132">如果您遇到的問題建立 HDInsight 叢集時，可能是，您不需要 hello 正確的權限 toodo 因此。</span><span class="sxs-lookup"><span data-stu-id="282a5-132">If you run into an issue with creating HDInsight clusters, it could be that you do not have hello right permissions toodo so.</span></span> <span data-ttu-id="282a5-133">如需詳細資訊，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="282a5-133">See [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters) for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="282a5-134">這篇文章建立 Spark 叢集，以使用[hello 與 Azure 儲存體 Blob 叢集儲存體](hdinsight-hadoop-use-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="282a5-134">This article creates a Spark cluster that uses [Azure Storage Blobs as hello cluster storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="282a5-135">您也可以建立使用的 Spark 叢集[Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md)為 hello 預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="282a5-135">You can also create a Spark cluster that uses [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) as hello default storage.</span></span> <span data-ttu-id="282a5-136">如需指示，請參閱 [建立具有 Data Lake Store 的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="282a5-136">For instructions, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>
>
>

## <a name="run-a-hive-query-using-spark-sql"></a><span data-ttu-id="282a5-137">執行使用 Spark SQL 的 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="282a5-137">Run a Hive query using Spark SQL</span></span>

<span data-ttu-id="282a5-138">當您使用 HDInsight Spark 叢集設定 Jupyter 筆記本時，您會取得預設`sqlContext`可讓您使用 Spark SQL toorun Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="282a5-138">When you use a Jupyter notebook configured for your HDInsight Spark cluster, you get a preset `sqlContext` that you can use toorun Hive queries using Spark SQL.</span></span> <span data-ttu-id="282a5-139">在本節中，您學會如何 toostart Jupyter 筆記本，然後執行基本的 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="282a5-139">In this section, you learn how toostart a Jupyter notebook and then run a basic Hive query.</span></span>

1. <span data-ttu-id="282a5-140">開啟 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="282a5-140">Open hello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="282a5-141">如果您選擇 toopin hello 叢集 toohello 儀表板，按一下 hello 叢集磚的 hello 儀表板 toolaunch hello 叢集刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="282a5-141">If you opted toopin hello cluster toohello dashboard, click hello cluster tile from hello dashboard toolaunch hello cluster blade.</span></span>

    <span data-ttu-id="282a5-142">如果您沒有不固定 hello 叢集 toohello 儀表板，從 hello 左窗格中，按一下**HDInsight 叢集**，然後按一下您所建立的 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="282a5-142">If you did not pin hello cluster toohello dashboard, from hello left pane, click **HDInsight clusters**, and then click hello cluster you created.</span></span>

3. <span data-ttu-id="282a5-143">從 快速連結，按一下 叢集儀表板，然後按一下Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="282a5-143">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="282a5-144">如果出現提示，請輸入 hello 叢集 hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="282a5-144">If prompted, enter hello admin credentials for hello cluster.</span></span>

   <span data-ttu-id="282a5-145">![開啟 Jupyter 筆記本 toorun 互動式 Spark SQL 查詢](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "開啟 Jupyter 筆記本 toorun 互動式 Spark SQL 查詢")</span><span class="sxs-lookup"><span data-stu-id="282a5-145">![Open Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook toorun interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="282a5-146">您也可以透過下列 URL 在瀏覽器中開啟 hello 叢集存取 hello Jupyter 筆記本。</span><span class="sxs-lookup"><span data-stu-id="282a5-146">You may also access hello Jupyter notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="282a5-147">取代**CLUSTERNAME** hello 名稱，為您的叢集：</span><span class="sxs-lookup"><span data-stu-id="282a5-147">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="282a5-148">建立 Notebook。</span><span class="sxs-lookup"><span data-stu-id="282a5-148">Create a notebook.</span></span> <span data-ttu-id="282a5-149">按一下 新增，然後按一下PySpark。</span><span class="sxs-lookup"><span data-stu-id="282a5-149">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="282a5-150">![建立 Jupyter 筆記本 toorun 互動式 Spark SQL 查詢](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "建立 Jupyter 筆記本 toorun 互動式 Spark SQL 查詢")</span><span class="sxs-lookup"><span data-stu-id="282a5-150">![Create a Jupyter notebook toorun interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook toorun interactive Spark SQL query")</span></span>

   <span data-ttu-id="282a5-151">建立新的記事本，並開啟 hello 名稱 Untitled(Untitled.pynb)。</span><span class="sxs-lookup"><span data-stu-id="282a5-151">A new notebook is created and opened with hello name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="282a5-152">按一下頂端 hello hello 筆記本名稱，然後輸入易記的名稱，如果您想。</span><span class="sxs-lookup"><span data-stu-id="282a5-152">Click hello notebook name at hello top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="282a5-153">![提供查詢的名稱 hello Jupter 筆記本 toorun 互動式 Spark 從](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "提供 hello Jupter 筆記本 toorun 互動式 Spark 中查詢的名稱")</span><span class="sxs-lookup"><span data-stu-id="282a5-153">![Provide a name for hello Jupter notebook toorun interactive Spark query from](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Provide a name for hello Jupter notebook toorun interactive Spark query from")</span></span>

5.  <span data-ttu-id="282a5-154">貼上 hello 下列空的資料格中的程式碼，然後按下**SHIFT + ENTER** toorun hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="282a5-154">Paste hello following code in an empty cell, and then press **SHIFT + ENTER** toorun hello code.</span></span> <span data-ttu-id="282a5-155">下列程式碼 hello `%%sql` (稱為的 hello sql magic) 會告知 Jupyter 筆記本 toouse hello 預設`sqlContext`toorun hello Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="282a5-155">In hello code below `%%sql` (called hello sql magic) tells Jupyter notebook toouse hello preset `sqlContext` toorun hello Hive query.</span></span> <span data-ttu-id="282a5-156">hello 查詢擷取 Hive 資料表中的 hello 前 10 個資料列 (**hivesampletable**)，而且可根據預設，所有的 HDInsight 叢集上。</span><span class="sxs-lookup"><span data-stu-id="282a5-156">hello query retrieves hello top 10 rows from a Hive table (**hivesampletable**) that is available by default on all HDInsight clusters.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    <span data-ttu-id="282a5-157">![HDInsight Spark 中的 Hive 查詢](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "HDInsight Spark 中的 Hive 查詢")</span><span class="sxs-lookup"><span data-stu-id="282a5-157">![Hive query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span></span>

    <span data-ttu-id="282a5-158">如需有關 hello`%%sql`魔法與 hello 預先設定的內容，請參閱[Jupyter 核心的 HDInsight 叢集供](hdinsight-apache-spark-jupyter-notebook-kernels.md)。</span><span class="sxs-lookup"><span data-stu-id="282a5-158">For more information on hello `%%sql` magic and hello preset contexts, see [Jupyter kernels available for an HDInsight cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="282a5-159">每次您在 Jupyter 執行查詢，會顯示您的 web 瀏覽器視窗標題**（忙碌）**狀態以及 hello 筆記本標題。</span><span class="sxs-lookup"><span data-stu-id="282a5-159">Every time you run a query in Jupyter, your web browser window title shows a **(Busy)** status along with hello notebook title.</span></span> <span data-ttu-id="282a5-160">另請參閱實心圓的下一個 toohello **PySpark** hello 右上角中的文字。</span><span class="sxs-lookup"><span data-stu-id="282a5-160">You also see a solid circle next toohello **PySpark** text in hello top-right corner.</span></span> <span data-ttu-id="282a5-161">Hello 作業完成之後，它會變更 tooa 空心圓圈。</span><span class="sxs-lookup"><span data-stu-id="282a5-161">After hello job is completed, it changes tooa hollow circle.</span></span>
    >
    >
    
6. <span data-ttu-id="282a5-162">囉 」 畫面應該重新整理 tooshow hello 查詢輸出。</span><span class="sxs-lookup"><span data-stu-id="282a5-162">hello screen should refresh tooshow hello query output.</span></span>

    <span data-ttu-id="282a5-163">![HDInsight Spark 中的 Hive 查詢輸出](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "HDInsight Spark 中的 Hive 查詢輸出")</span><span class="sxs-lookup"><span data-stu-id="282a5-163">![Hive query output in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span></span>

7. <span data-ttu-id="282a5-164">您完成執行後，hello 應用程式，請關閉 hello 筆記本 toorelease hello 叢集資源。</span><span class="sxs-lookup"><span data-stu-id="282a5-164">Shut down hello notebook toorelease hello cluster resources after you have finished running hello application.</span></span> <span data-ttu-id="282a5-165">toodo 的話，從 hello**檔案**hello 筆記本功能表按一下**關閉而停止**。</span><span class="sxs-lookup"><span data-stu-id="282a5-165">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span>

8. <span data-ttu-id="282a5-166">如果您稍後打算 toocomplete hello 接下來的步驟，請確定刪除在這篇文章中所建立的 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="282a5-166">If you plan toocomplete hello next steps at a later time, make sure you delete hello HDInsight cluster you created in this article.</span></span> 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a><span data-ttu-id="282a5-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="282a5-167">Next step</span></span> 

<span data-ttu-id="282a5-168">在本文，您學到如何 toocreate HDInsight Spark 叢集，並執行基本的 Spark SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="282a5-168">In this article you learned how toocreate an HDInsight Spark cluster and run a basic Spark SQL query.</span></span> <span data-ttu-id="282a5-169">前進 toohello toouse HDInsight Spark 叢集的方式下一個發行項 toolearn toorun 互動式查詢針對取樣資料。</span><span class="sxs-lookup"><span data-stu-id="282a5-169">Advance toohello next article toolearn how toouse an HDInsight Spark cluster toorun interactive queries on sample data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="282a5-170">在 HDInsight Spark 叢集上執行互動查詢</span><span class="sxs-lookup"><span data-stu-id="282a5-170">Run interactive queries on an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-load-data-run-query.md)



