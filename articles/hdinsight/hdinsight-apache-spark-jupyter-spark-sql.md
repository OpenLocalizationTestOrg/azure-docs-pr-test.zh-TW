---
title: "在 Azure HDInsight 中建立 Apache Spark 叢集 | Microsoft Docs"
description: "HDInsight Spark 快速入門會說明如何在 HDInsight 中建立 Apache Spark 叢集。"
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
ms.openlocfilehash: ad4330a1fc7f8de154d9aaa8df3acc2ab59b9dc1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a><span data-ttu-id="7d67d-104">在 Azure HDInsight 中建立 Apache Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="7d67d-104">Create an Apache Spark cluster in Azure HDInsight</span></span>

<span data-ttu-id="7d67d-105">本文說明如何在 Azure HDInsight 中建立 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="7d67d-105">In this article, you learn how to create an Apache Spark cluster in Azure HDInsight.</span></span> <span data-ttu-id="7d67d-106">如需 Spark on HDInsight 相關資訊，請參閱[概觀：Azure HDInsight 上的 Apache Spark](hdinsight-apache-spark-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7d67d-106">For information on Spark on HDInsight, see [Overview: Apache Spark on Azure HDInsight](hdinsight-apache-spark-overview.md).</span></span>

   <span data-ttu-id="7d67d-107">![描述在 Azure HDInsight 上建立 Apache Spark 叢集之步驟的快速入門圖表](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "在 HDInsight 中使用 Apache Spark 的 Spark 快速入門。說明的步驟︰建立叢集；執行 Spark 互動式查詢")</span><span class="sxs-lookup"><span data-stu-id="7d67d-107">![Quickstart diagram describing steps to create an Apache Spark cluster on Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark quickstart using Apache Spark in HDInsight. Steps illustrated: create a cluster; run Spark interactive query")</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d67d-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="7d67d-108">Prerequisites</span></span>

* <span data-ttu-id="7d67d-109">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="7d67d-109">**An Azure subscription**.</span></span> <span data-ttu-id="7d67d-110">開始進行本教學課程之前，您必須擁有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7d67d-110">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="7d67d-111">請參閱[立即建立免費的 Azure 帳戶](https://azure.microsoft.com/free)。</span><span class="sxs-lookup"><span data-stu-id="7d67d-111">See [Create your free Azure account today](https://azure.microsoft.com/free).</span></span>

## <a name="create-hdinsight-spark-cluster"></a><span data-ttu-id="7d67d-112">建立 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="7d67d-112">Create HDInsight Spark cluster</span></span>

<span data-ttu-id="7d67d-113">在本節中，您會使用 [Azure Resource Manager 範本](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/)來建立 HDInsight Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="7d67d-113">In this section, you create an HDInsight Spark cluster using an [Azure Resource Manager template](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/).</span></span> <span data-ttu-id="7d67d-114">如需其他叢集建立方法，請參閱 [建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="7d67d-114">For other cluster creation methods, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="7d67d-115">按一下以下影像，在 Azure 入口網站中開啟範本。</span><span class="sxs-lookup"><span data-stu-id="7d67d-115">Click the following image to open the template in the Azure portal.</span></span>         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="7d67d-116">輸入下列值：</span><span class="sxs-lookup"><span data-stu-id="7d67d-116">Enter the following values:</span></span>

    <span data-ttu-id="7d67d-117">![使用 Azure Resource Manager 範本建立 HDInsight Spark 叢集](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "在 HDInsight 中使用 Azure Resource Manager 範本建立 Spark 叢集")</span><span class="sxs-lookup"><span data-stu-id="7d67d-117">![Create HDInsight Spark cluster using an Azure Resource Manager template](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Create Spark cluster in HDInsight using an Azure Resource Manager template")</span></span>

    * <span data-ttu-id="7d67d-118">**訂用帳戶**：針對此叢集選取您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7d67d-118">**Subscription**: Select your Azure subscription for this cluster.</span></span>
    * <span data-ttu-id="7d67d-119">**資源群組**：建立資源群組，或選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="7d67d-119">**Resource group**: Create a resource group or select an existing one.</span></span> <span data-ttu-id="7d67d-120">資源群組用來管理專案的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="7d67d-120">Resource group is used to manage Azure resources for your projects.</span></span>
    * <span data-ttu-id="7d67d-121">**位置**：選取資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="7d67d-121">**Location**: Select a location for the resource group.</span></span> <span data-ttu-id="7d67d-122">此範本會使用這個位置，用於建立叢集以及預設叢集儲存體。</span><span class="sxs-lookup"><span data-stu-id="7d67d-122">The template uses this location for creating the cluster as well as for the default cluster storage.</span></span>
    * <span data-ttu-id="7d67d-123">**ClusterName**：輸入您想要建立的 HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="7d67d-123">**ClusterName**: Enter a name for the HDInsight cluster that you want to create.</span></span>
    * <span data-ttu-id="7d67d-124">**Spark 版本**︰選取 **2.0** 作為您要在叢集上安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="7d67d-124">**Spark version**: Select **2.0** as the version that you want to install on the cluster.</span></span>
    * <span data-ttu-id="7d67d-125">叢集登入名稱和密碼：預設登入名稱是 admin。</span><span class="sxs-lookup"><span data-stu-id="7d67d-125">**Cluster login name and password**: The default login name is admin.</span></span>
    * <span data-ttu-id="7d67d-126">SSH 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="7d67d-126">**SSH user name and password**.</span></span>

   <span data-ttu-id="7d67d-127">請記下這些值。</span><span class="sxs-lookup"><span data-stu-id="7d67d-127">Write down these values.</span></span>  <span data-ttu-id="7d67d-128">稍後在教學課程中需要這些資訊。</span><span class="sxs-lookup"><span data-stu-id="7d67d-128">You need them later in the tutorial.</span></span>

3. <span data-ttu-id="7d67d-129">選取 [我同意上方所述的條款及條件]，選取 [釘選到儀表板]，然後按一下 [購買]。</span><span class="sxs-lookup"><span data-stu-id="7d67d-129">Select **I agree to the terms and conditions stated above**, select **Pin to dashboard**, and then click **Purchase**.</span></span> <span data-ttu-id="7d67d-130">您可以看到新的圖格，標題為「提交範本部署的部署」。</span><span class="sxs-lookup"><span data-stu-id="7d67d-130">You can see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="7d67d-131">大約需要 20 分鐘的時間來建立叢集。</span><span class="sxs-lookup"><span data-stu-id="7d67d-131">It takes about 20 minutes to create the cluster.</span></span>

<span data-ttu-id="7d67d-132">如果您在建立 HDInsight 叢集時遇到問題，可能是您沒有這麼做的適當權限。</span><span class="sxs-lookup"><span data-stu-id="7d67d-132">If you run into an issue with creating HDInsight clusters, it could be that you do not have the right permissions to do so.</span></span> <span data-ttu-id="7d67d-133">如需詳細資訊，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="7d67d-133">See [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters) for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="7d67d-134">本文建立使用 [Azure 儲存體 Blob 做為叢集儲存體](hdinsight-hadoop-use-blob-storage.md)的 Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="7d67d-134">This article creates a Spark cluster that uses [Azure Storage Blobs as the cluster storage](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="7d67d-135">您也可以建立使用 [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) 作為預設儲存體的 Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="7d67d-135">You can also create a Spark cluster that uses [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) as the default storage.</span></span> <span data-ttu-id="7d67d-136">如需指示，請參閱 [建立具有 Data Lake Store 的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="7d67d-136">For instructions, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>
>
>

## <a name="run-a-hive-query-using-spark-sql"></a><span data-ttu-id="7d67d-137">執行使用 Spark SQL 的 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="7d67d-137">Run a Hive query using Spark SQL</span></span>

<span data-ttu-id="7d67d-138">當您使用針對 HDInsight Spark 叢集設定的 Jupyter Notebook 時，您可取得預設 `sqlContext`，用來執行使用 Spark SQL 的 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="7d67d-138">When you use a Jupyter notebook configured for your HDInsight Spark cluster, you get a preset `sqlContext` that you can use to run Hive queries using Spark SQL.</span></span> <span data-ttu-id="7d67d-139">本節說明如何啟動 Jupyter Notebook，然後執行基本 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="7d67d-139">In this section, you learn how to start a Jupyter notebook and then run a basic Hive query.</span></span>

1. <span data-ttu-id="7d67d-140">開啟 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="7d67d-140">Open the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="7d67d-141">如果您選擇將叢集釘選至儀表板，從儀表板按一下 [叢集] 圖格以啟動叢集刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7d67d-141">If you opted to pin the cluster to the dashboard, click the cluster tile from the dashboard to launch the cluster blade.</span></span>

    <span data-ttu-id="7d67d-142">如果您未將叢集釘選至儀表板，從左窗格中按一下 [HDInsight 叢集]，然後按一下您建立的叢集。</span><span class="sxs-lookup"><span data-stu-id="7d67d-142">If you did not pin the cluster to the dashboard, from the left pane, click **HDInsight clusters**, and then click the cluster you created.</span></span>

3. <span data-ttu-id="7d67d-143">從 [快速連結]，按一下 [叢集儀表板]，然後按一下 [Jupyter Notebook]。</span><span class="sxs-lookup"><span data-stu-id="7d67d-143">From **Quick links**, click **Cluster dashboards**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="7d67d-144">出現提示時，輸入叢集的系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="7d67d-144">If prompted, enter the admin credentials for the cluster.</span></span>

   <span data-ttu-id="7d67d-145">![開啟 Jupyter Notebook 來執行互動式 Spark SQL 查詢](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "開啟 Jupyter Notebook 來執行互動式 Spark SQL 查詢")</span><span class="sxs-lookup"><span data-stu-id="7d67d-145">![Open Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter notebook to run interactive Spark SQL query")</span></span>

   > [!NOTE]
   > <span data-ttu-id="7d67d-146">您也可以在瀏覽器中開啟下列 URL，來存取您叢集的 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="7d67d-146">You may also access the Jupyter notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="7d67d-147">使用您叢集的名稱取代 **CLUSTERNAME** ：</span><span class="sxs-lookup"><span data-stu-id="7d67d-147">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="7d67d-148">建立 Notebook。</span><span class="sxs-lookup"><span data-stu-id="7d67d-148">Create a notebook.</span></span> <span data-ttu-id="7d67d-149">按一下 [新增]，然後按一下 [PySpark]。</span><span class="sxs-lookup"><span data-stu-id="7d67d-149">Click **New**, and then click **PySpark**.</span></span>

   <span data-ttu-id="7d67d-150">![建立 Jupyter Notebook 來執行互動式 Spark SQL 查詢](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "建立 Jupyter Notebook 來執行互動式 Spark SQL 查詢")</span><span class="sxs-lookup"><span data-stu-id="7d67d-150">![Create a Jupyter notebook to run interactive Spark SQL query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Create a Jupyter notebook to run interactive Spark SQL query")</span></span>

   <span data-ttu-id="7d67d-151">新的 Notebook 隨即建立並以 Untitled(Untitled.pynb) 名稱開啟。</span><span class="sxs-lookup"><span data-stu-id="7d67d-151">A new notebook is created and opened with the name Untitled(Untitled.pynb).</span></span>

4. <span data-ttu-id="7d67d-152">按一下頂端的 Notebook 名稱，然後輸入好記的名稱。</span><span class="sxs-lookup"><span data-stu-id="7d67d-152">Click the notebook name at the top, and enter a friendly name if you want.</span></span>

    <span data-ttu-id="7d67d-153">![為要執行互動式 Spark 查詢的 Jupter Notebook 命名](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "為要執行互動式 Spark 查詢的 Jupter Notebook 命名")</span><span class="sxs-lookup"><span data-stu-id="7d67d-153">![Provide a name for the Jupter notebook to run interactive Spark query from](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "Provide a name for the Jupter notebook to run interactive Spark query from")</span></span>

5.  <span data-ttu-id="7d67d-154">將以下程式碼貼入空白儲存格，然後按下 **SHIFT + ENTER** 鍵以執行此程式碼。</span><span class="sxs-lookup"><span data-stu-id="7d67d-154">Paste the following code in an empty cell, and then press **SHIFT + ENTER** to run the code.</span></span> <span data-ttu-id="7d67d-155">在以下程式碼中，`%%sql` (稱為 sql magic) 會告知 Jupyter Notebook 使用預設的 `sqlContext` 來執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="7d67d-155">In the code below `%%sql` (called the sql magic) tells Jupyter notebook to use the preset `sqlContext` to run the Hive query.</span></span> <span data-ttu-id="7d67d-156">此查詢會擷取 Hive 資料表 (**hivesampletable**) 中的前 10 個資料列，該資料表預設可用於所有 HDInsight 叢集上。</span><span class="sxs-lookup"><span data-stu-id="7d67d-156">The query retrieves the top 10 rows from a Hive table (**hivesampletable**) that is available by default on all HDInsight clusters.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    <span data-ttu-id="7d67d-157">![HDInsight Spark 中的 Hive 查詢](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "HDInsight Spark 中的 Hive 查詢")</span><span class="sxs-lookup"><span data-stu-id="7d67d-157">![Hive query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive query in HDInsight Spark")</span></span>

    <span data-ttu-id="7d67d-158">如需有關 `%%sql` magic 和預設內容的詳細資訊，請參閱 [HDInsight 叢集可用的 Jupyter 核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)。</span><span class="sxs-lookup"><span data-stu-id="7d67d-158">For more information on the `%%sql` magic and the preset contexts, see [Jupyter kernels available for an HDInsight cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="7d67d-159">每當您在 Jupyter 中執行查詢時，網頁瀏覽器視窗標題將會顯示 Notebook 標題和 **(忙碌)** 狀態。</span><span class="sxs-lookup"><span data-stu-id="7d67d-159">Every time you run a query in Jupyter, your web browser window title shows a **(Busy)** status along with the notebook title.</span></span> <span data-ttu-id="7d67d-160">您也會在右上角的 **PySpark** 文字旁看到一個實心圓。</span><span class="sxs-lookup"><span data-stu-id="7d67d-160">You also see a solid circle next to the **PySpark** text in the top-right corner.</span></span> <span data-ttu-id="7d67d-161">作業完成後，實心圓將變成空心圓。</span><span class="sxs-lookup"><span data-stu-id="7d67d-161">After the job is completed, it changes to a hollow circle.</span></span>
    >
    >
    
6. <span data-ttu-id="7d67d-162">畫面應會重新整理以顯示查詢輸出。</span><span class="sxs-lookup"><span data-stu-id="7d67d-162">The screen should refresh to show the query output.</span></span>

    <span data-ttu-id="7d67d-163">![HDInsight Spark 中的 Hive 查詢輸出](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "HDInsight Spark 中的 Hive 查詢輸出")</span><span class="sxs-lookup"><span data-stu-id="7d67d-163">![Hive query output in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Hive query output in HDInsight Spark")</span></span>

7. <span data-ttu-id="7d67d-164">應用程式執行完畢之後，請關閉 Notebook 來釋放叢集資源。</span><span class="sxs-lookup"><span data-stu-id="7d67d-164">Shut down the notebook to release the cluster resources after you have finished running the application.</span></span> <span data-ttu-id="7d67d-165">若要這樣做，請從 Notebook 的 [檔案] 功能表中，按一下 [關閉並停止]。</span><span class="sxs-lookup"><span data-stu-id="7d67d-165">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span>

8. <span data-ttu-id="7d67d-166">如果您打算稍後完成後續步驟，請務必刪除在本文中建立的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="7d67d-166">If you plan to complete the next steps at a later time, make sure you delete the HDInsight cluster you created in this article.</span></span> 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a><span data-ttu-id="7d67d-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7d67d-167">Next step</span></span> 

<span data-ttu-id="7d67d-168">在本文中，您已了解如何建立 HDInsight Spark 叢集和執行基本的 Spark SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="7d67d-168">In this article you learned how to create an HDInsight Spark cluster and run a basic Spark SQL query.</span></span> <span data-ttu-id="7d67d-169">前往下篇文章，了解如何使用 HDInsight Spark 叢集執行簡單資料的互動查詢。</span><span class="sxs-lookup"><span data-stu-id="7d67d-169">Advance to the next article to learn how to use an HDInsight Spark cluster to run interactive queries on sample data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="7d67d-170">在 HDInsight Spark 叢集上執行互動查詢</span><span class="sxs-lookup"><span data-stu-id="7d67d-170">Run interactive queries on an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-load-data-run-query.md)



