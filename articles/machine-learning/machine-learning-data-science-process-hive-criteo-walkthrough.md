---
title: "Team Data Science Process 實務 - 在 1 TB 資料集上使用 Azure HDInsight Hadoop 叢集 | Microsoft Docs"
description: "對採用 HDInsight Hadoop 叢集來建置和部署使用大型 (1 TB) 公開可用資料集模型的端對端案例使用 Team Data Science Process"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 8e6143bca819c9a0484221f8b4feb319aaaa73f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a><span data-ttu-id="61185-103">Team Data Science Process 實務 - 在 1 TB 資料集上使用 Azure HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="61185-103">The Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset</span></span>

<span data-ttu-id="61185-104">在這個逐步解說中，我們會示範在端對端案例中使用 Team Data Science Process 搭配 [Azure HDInsight Hadoop 叢集](https://azure.microsoft.com/services/hdinsight/)進行儲存、探索、特徵工程設計，並從其中一個公開可用的 [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) 資料集縮減取樣資料。</span><span class="sxs-lookup"><span data-stu-id="61185-104">In this walkthrough, we demonstrate using the Team Data Science Process in an end-to-end scenario with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, feature engineer, and down sample data from one of the publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) datasets.</span></span> <span data-ttu-id="61185-105">我們使用 Azure Machine Learning 在此資料上建置二進位的分類模型。</span><span class="sxs-lookup"><span data-stu-id="61185-105">We use Azure Machine Learning to build a binary classification model on this data.</span></span> <span data-ttu-id="61185-106">我們也會顯示如何將其中一個模型發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="61185-106">We also show how to publish one of these models as a Web service.</span></span>

<span data-ttu-id="61185-107">此外，也可以使用 IPython Notebook 來完成此逐步解說中說明的工作。</span><span class="sxs-lookup"><span data-stu-id="61185-107">It is also possible to use an IPython notebook to accomplish the tasks presented in this walkthrough.</span></span> <span data-ttu-id="61185-108">想要嘗試這種方法的使用者，應該查閱 [使用 Hive ODBC 連線的 Criteo 逐步解說](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) 主題。</span><span class="sxs-lookup"><span data-stu-id="61185-108">Users who would like to try this approach should consult the [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="61185-109"><a name="dataset"></a>Criteo 資料集說明</span><span class="sxs-lookup"><span data-stu-id="61185-109"><a name="dataset"></a>Criteo Dataset Description</span></span>
<span data-ttu-id="61185-110">Criteo 資料是點選預測的資料集，大約是 370 GB 的 gzip 壓縮 TSV 檔案 (~1.3 TB 未壓縮)，包含超過 43 億筆記錄。</span><span class="sxs-lookup"><span data-stu-id="61185-110">The Criteo data is a click prediction dataset that is approximately 370GB of gzip compressed TSV files (~1.3TB uncompressed), comprising more than 4.3 billion records.</span></span> <span data-ttu-id="61185-111">它取自 [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/)提供的 24 天點選資料。</span><span class="sxs-lookup"><span data-stu-id="61185-111">It is taken from 24 days of click data made available by [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span></span> <span data-ttu-id="61185-112">為了方便資料科學家，我們已將可供試驗的資料解壓縮。</span><span class="sxs-lookup"><span data-stu-id="61185-112">For the convenience of data scientists, we have unzipped data available to us to experiment with.</span></span>

<span data-ttu-id="61185-113">在此資料集中的每一筆記錄包含 40 個資料行：</span><span class="sxs-lookup"><span data-stu-id="61185-113">Each record in this dataset contains 40 columns:</span></span>

* <span data-ttu-id="61185-114">第一個資料行是標籤資料行，指出使用者是否按一下 **加入** (值 1) 或未按一下 (值 0)</span><span class="sxs-lookup"><span data-stu-id="61185-114">the first column is a label column that indicates whether a user clicks an **add** (value 1) or does not click one (value 0)</span></span>
* <span data-ttu-id="61185-115">接下來 13 個資料行是數字，以及</span><span class="sxs-lookup"><span data-stu-id="61185-115">next 13 columns are numeric, and</span></span>
* <span data-ttu-id="61185-116">最後 26 個資料行是類別資料行</span><span class="sxs-lookup"><span data-stu-id="61185-116">last 26 are categorical columns</span></span>

<span data-ttu-id="61185-117">資料行為匿名，並使用一系列的列舉名稱："Col1" (針對標籤資料行) 至 "Col40" (針對最後一個分類資料行)。</span><span class="sxs-lookup"><span data-stu-id="61185-117">The columns are anonymized and use a series of enumerated names: "Col1" (for the label column) to 'Col40" (for the last categorical column).</span></span>            

<span data-ttu-id="61185-118">以下是來自這個資料集的兩個觀察 (資料列) 的前 20 個資料行的摘錄：</span><span class="sxs-lookup"><span data-stu-id="61185-118">Here is an excerpt of the first 20 columns of two observations (rows) from this dataset:</span></span>

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

<span data-ttu-id="61185-119">此資料集中的數值及分類資料行中有遺漏值。</span><span class="sxs-lookup"><span data-stu-id="61185-119">There are missing values in both the numeric and categorical columns in this dataset.</span></span> <span data-ttu-id="61185-120">我們會說明用來處理遺漏值的簡單方法。</span><span class="sxs-lookup"><span data-stu-id="61185-120">We describe a simple method for handling the missing values.</span></span> <span data-ttu-id="61185-121">資料的其他詳細資料會在將它們儲存成 Hive 資料表時加以探究。</span><span class="sxs-lookup"><span data-stu-id="61185-121">Additional details of the data are explored when we store them into Hive tables.</span></span>

<span data-ttu-id="61185-122">**定義：** *點選率 (CTR)：* 這是資料中點選的百分比。</span><span class="sxs-lookup"><span data-stu-id="61185-122">**Definition:** *Clickthrough rate (CTR):* This is the percentage of clicks in the data.</span></span> <span data-ttu-id="61185-123">在此 Criteo 資料集中，CTR 是大約 3.3%或 0.033。</span><span class="sxs-lookup"><span data-stu-id="61185-123">In this Criteo dataset, the CTR is about 3.3% or 0.033.</span></span>

## <span data-ttu-id="61185-124"><a name="mltasks"></a>預測工作的範例</span><span class="sxs-lookup"><span data-stu-id="61185-124"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="61185-125">本逐步解說將討論兩個範例預測問題：</span><span class="sxs-lookup"><span data-stu-id="61185-125">Two sample prediction problems are addressed in this walkthrough:</span></span>

1. <span data-ttu-id="61185-126">**二進位分類**：預測使用者是否按下加入：</span><span class="sxs-lookup"><span data-stu-id="61185-126">**Binary classification**: Predicts whether a user clicked an add:</span></span>
   
   * <span data-ttu-id="61185-127">類別 0：未按一下</span><span class="sxs-lookup"><span data-stu-id="61185-127">Class 0: No Click</span></span>
   * <span data-ttu-id="61185-128">類別 1：按一下</span><span class="sxs-lookup"><span data-stu-id="61185-128">Class 1: Click</span></span>
2. <span data-ttu-id="61185-129">**迴歸**：預測使用者按一下廣告機率的功能。</span><span class="sxs-lookup"><span data-stu-id="61185-129">**Regression**: Predicts the probability of an ad click from user features.</span></span>

## <span data-ttu-id="61185-130"><a name="setup"></a>為資料科學設定 HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="61185-130"><a name="setup"></a>Set Up an HDInsight Hadoop cluster for data science</span></span>
<span data-ttu-id="61185-131">**附註：**這通常是**管理**工作。</span><span class="sxs-lookup"><span data-stu-id="61185-131">**Note:** This is typically an **Admin** task.</span></span>

<span data-ttu-id="61185-132">設定 Azure 資料科學環境，用於使用 HDInsight 叢集以三個步驟建置預測性的分析解決方案：</span><span class="sxs-lookup"><span data-stu-id="61185-132">Set up your Azure Data Science environment for building predictive analytics solutions with HDInsight clusters in three steps:</span></span>

1. <span data-ttu-id="61185-133">[建立儲存體帳戶](../storage/common/storage-create-storage-account.md)：此儲存體帳戶用來將資料儲存在 Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="61185-133">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used to store data in Azure Blob Storage.</span></span> <span data-ttu-id="61185-134">HDInsight 叢集中使用的資料會儲存在這裡。</span><span class="sxs-lookup"><span data-stu-id="61185-134">The data used in HDInsight clusters is stored here.</span></span>
2. <span data-ttu-id="61185-135">[自訂適用於資料科學的 Azure HDInsight Hadoop 叢集](machine-learning-data-science-customize-hadoop-cluster.md)：這個步驟將會建立已在所有節點上安裝 64 位元 Anaconda Python 2.7 的 Azure HDInsight Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="61185-135">[Customize Azure HDInsight Hadoop Clusters for Data Science](machine-learning-data-science-customize-hadoop-cluster.md): This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="61185-136">自訂 HDInsight 叢集時有兩個需完成的重要步驟 (如本主題所述)。</span><span class="sxs-lookup"><span data-stu-id="61185-136">There are two important steps (described in this topic) to complete when customizing the HDInsight cluster.</span></span>
   
   * <span data-ttu-id="61185-137">建立時您必須將步驟 1 中建立的儲存體帳戶與 HDInsight 叢集連結。</span><span class="sxs-lookup"><span data-stu-id="61185-137">You must link the storage account created in step 1 with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="61185-138">此儲存體帳戶用於存取可以在叢集內處理的資料。</span><span class="sxs-lookup"><span data-stu-id="61185-138">This storage account is used for accessing data that can be processed within the cluster.</span></span>
   * <span data-ttu-id="61185-139">建立後，您必須對叢集的前端節點啟用遠端存取。</span><span class="sxs-lookup"><span data-stu-id="61185-139">You must enable Remote Access to the head node of the cluster after it is created.</span></span> <span data-ttu-id="61185-140">請記住您在此處指定的遠端存取認證 (與建立時指定叢集的不同)：您需要認證以完成下列程序。</span><span class="sxs-lookup"><span data-stu-id="61185-140">Remember the remote access credentials you specify here (different from those specified for the cluster at its creation): you need them to complete the following procedures.</span></span>
3. <span data-ttu-id="61185-141">[建立 Azure ML 工作區](machine-learning-create-workspace.md)：此 Azure Machine Learning 工作區用來在初始資料瀏覽之後建置機器學習模型，並且在 HDInsight 叢集上下載取樣。</span><span class="sxs-lookup"><span data-stu-id="61185-141">[Create an Azure ML workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used for building machine learning models after an initial data exploration and down sampling on the HDInsight cluster.</span></span>

## <span data-ttu-id="61185-142"><a name="getdata"></a>取得並從公用來源取用資料</span><span class="sxs-lookup"><span data-stu-id="61185-142"><a name="getdata"></a>Get and consume data from a public source</span></span>
<span data-ttu-id="61185-143">[Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) 資料集可以透過按一下連結、接受使用條款並提供名稱來存取。</span><span class="sxs-lookup"><span data-stu-id="61185-143">The [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset can be accessed by clicking on the link, accepting the terms of use, and providing a name.</span></span> <span data-ttu-id="61185-144">其外觀的快照如下所示：</span><span class="sxs-lookup"><span data-stu-id="61185-144">A snapshot of what this looks like is shown here:</span></span>

![接受 Criteo 條款](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

<span data-ttu-id="61185-146">按一下 [繼續下載]  來閱讀資料集的相關資訊和它的可用性。</span><span class="sxs-lookup"><span data-stu-id="61185-146">Click **Continue to Download** to read more about the dataset and its availability.</span></span>

<span data-ttu-id="61185-147">資料位於公用 [Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)位置：wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/。</span><span class="sxs-lookup"><span data-stu-id="61185-147">The data resides in a public [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) location: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span></span> <span data-ttu-id="61185-148">"wasb" 指的是 Azure Blob 儲存體位置。</span><span class="sxs-lookup"><span data-stu-id="61185-148">The "wasb" refers to Azure Blob Storage location.</span></span> 

1. <span data-ttu-id="61185-149">這個公用 Blob 儲存體中的資料是由所解壓縮資料的三個子資料夾所組成。</span><span class="sxs-lookup"><span data-stu-id="61185-149">The data in this public blob storage consists of three subfolders of unzipped data.</span></span>
   
   1. <span data-ttu-id="61185-150">子資料夾 *raw/count/*包含前 21 天的資料 - 從 day\_00 到 day\_20</span><span class="sxs-lookup"><span data-stu-id="61185-150">The subfolder *raw/count/* contains the first 21 days of data - from day\_00 to day\_20</span></span>
   2. <span data-ttu-id="61185-151">子資料夾 *raw/train/*由單一天 day\_21 的資料組成</span><span class="sxs-lookup"><span data-stu-id="61185-151">The subfolder *raw/train/* consists of a single day of data, day\_21</span></span>
   3. <span data-ttu-id="61185-152">子資料夾 *raw/test/*由兩天 day\_22 和 day\_23 的資料組成</span><span class="sxs-lookup"><span data-stu-id="61185-152">The subfolder *raw/test/* consists of two days of data, day\_22 and day\_23</span></span>
2. <span data-ttu-id="61185-153">對於想要從原始 gzip 資料開始的使用者，這些也可以在主要資料夾 *raw/* 取得，形式為 day_NN.gz，其中 NN 從 00 到 23。</span><span class="sxs-lookup"><span data-stu-id="61185-153">For those who want to start with the raw gzip data, these are also available in the main folder *raw/* as day_NN.gz, where NN goes from 00 to 23.</span></span>

<span data-ttu-id="61185-154">本逐步解說中稍後會在我們建立 Hive 資料表時說明存取、瀏覽和模型化此資料而不需要任何本機下載的另一種方法。</span><span class="sxs-lookup"><span data-stu-id="61185-154">An alternative approach to access, explore, and model this data that does not require any local downloads is explained later in this walkthrough when we create Hive tables.</span></span>

## <span data-ttu-id="61185-155"><a name="login"></a>登入到叢集前端節點</span><span class="sxs-lookup"><span data-stu-id="61185-155"><a name="login"></a>Log in to the cluster headnode</span></span>
<span data-ttu-id="61185-156">若要登入叢集的前端節點，請使用 [Azure 入口網站](https://ms.portal.azure.com) 來找出叢集。</span><span class="sxs-lookup"><span data-stu-id="61185-156">To log in to the headnode of the cluster, use the [Azure portal](https://ms.portal.azure.com) to locate the cluster.</span></span> <span data-ttu-id="61185-157">在左側按一下 HDInsight 大象圖示，然後按兩下叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="61185-157">Click the HDInsight elephant icon on the left and then double-click the name of your cluster.</span></span> <span data-ttu-id="61185-158">瀏覽至 [組態]  索引標籤上，在頁面底部的 [連接] 圖示上連按兩下，然後在提示時輸入您的遠端存取認證。</span><span class="sxs-lookup"><span data-stu-id="61185-158">Navigate to the **Configuration** tab, double-click the CONNECT icon on the bottom of the page, and enter your remote access credentials when prompted.</span></span> <span data-ttu-id="61185-159">這會帶您前往叢集的前端節點。</span><span class="sxs-lookup"><span data-stu-id="61185-159">This takes you to the headnode of the cluster.</span></span>

<span data-ttu-id="61185-160">以下是典型的第一次登入叢集前端節點時看起來的外觀：</span><span class="sxs-lookup"><span data-stu-id="61185-160">Here is what a typical first log in to the cluster headnode looks like:</span></span>

![登入叢集](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

<span data-ttu-id="61185-162">在左邊，我們會看到「Hadoop 命令列」，這是我們進行資料瀏覽的主要位置。</span><span class="sxs-lookup"><span data-stu-id="61185-162">On the left, we see the "Hadoop Command Line", which is our workhorse for the data exploration.</span></span> <span data-ttu-id="61185-163">我們也會看到兩個實用的 URL - "Hadoop Yarn Status" 和 "Hadoop Name Node"。</span><span class="sxs-lookup"><span data-stu-id="61185-163">We also see two useful URLs - "Hadoop Yarn Status" and "Hadoop Name Node".</span></span> <span data-ttu-id="61185-164">Yarn 狀態 URL 會顯示工作進度，而名稱節點 URL 則會提供叢集組態的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="61185-164">The yarn status URL shows job progress and the name node URL gives details on the cluster configuration.</span></span>

<span data-ttu-id="61185-165">我們現在已設定，並已準備好開始逐步解說的第一個部分：使用 Hive 的資料瀏覽和為 Azure Machine Learning 備妥資料。</span><span class="sxs-lookup"><span data-stu-id="61185-165">Now we are set up and ready to begin first part of the walkthrough: data exploration using Hive and getting data ready for Azure Machine Learning.</span></span>

## <span data-ttu-id="61185-166"><a name="hive-db-tables"></a> 建立 Hive 資料庫和資料表</span><span class="sxs-lookup"><span data-stu-id="61185-166"><a name="hive-db-tables"></a> Create Hive database and tables</span></span>
<span data-ttu-id="61185-167">若要為我們的 Criteo 資料集建立 Hive 資料表，請在前端節點的桌面上開啟 [Hadoop 命令列]，然後輸入以下命令來進入 Hive 目錄</span><span class="sxs-lookup"><span data-stu-id="61185-167">To create Hive tables for our Criteo dataset, open the ***Hadoop Command Line*** on the desktop of the head node, and enter the Hive directory by entering the command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="61185-168">請從 Hive bin/ 目錄提示字元執行本逐步解說中的所有 Hive 命令。</span><span class="sxs-lookup"><span data-stu-id="61185-168">Run all Hive commands in this walkthrough from the Hive bin/ directory prompt.</span></span> <span data-ttu-id="61185-169">如此可自動處理路徑相關問題。</span><span class="sxs-lookup"><span data-stu-id="61185-169">This takes care of any path issues automatically.</span></span> <span data-ttu-id="61185-170">我們會交替使用詞彙「Hive 目錄提示」、「Hive bin/ 目錄提示」和「Hadoop 命令列」。</span><span class="sxs-lookup"><span data-stu-id="61185-170">We use the terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop Command Line" interchangeably.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="61185-171">若要執行任何 Hive 查詢，您永遠可以使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="61185-171">To execute any Hive query, one can always use the following commands:</span></span>
> 
> 

        cd %hive_home%\bin
        hive

<span data-ttu-id="61185-172">Hive REPL "hive >" 出現記號後，只需剪下並貼上查詢即可執行。</span><span class="sxs-lookup"><span data-stu-id="61185-172">After the Hive REPL appears with a "hive >"sign, simply cut and paste the query to execute it.</span></span>

<span data-ttu-id="61185-173">下列程式碼會建立資料庫 "criteo"，然後產生 4 個資料表：</span><span class="sxs-lookup"><span data-stu-id="61185-173">The following code creates a database "criteo" and then generates 4 tables:</span></span>

* <span data-ttu-id="61185-174">建置於 day\_00 到 day\_20 「用於產生計數的資料表」、</span><span class="sxs-lookup"><span data-stu-id="61185-174">a *table for generating counts* built on days day\_00 to day\_20,</span></span>
* <span data-ttu-id="61185-175">建置於 day\_21「用來做為訓練資料集的資料表」，以及</span><span class="sxs-lookup"><span data-stu-id="61185-175">a *table for use as the train dataset* built on day\_21, and</span></span>
* <span data-ttu-id="61185-176">分別建置於 day\_22 和 day\_23 的兩個「用來做為測試資料集的資料表」。</span><span class="sxs-lookup"><span data-stu-id="61185-176">two *tables for use as the test datasets* built on day\_22 and day\_23 respectively.</span></span>

<span data-ttu-id="61185-177">因為其中一天是假日，而且我們想要判斷模型是否可以偵測到假日與非假日之間點選率的差異，我們將我們的測試資料集分割成兩個不同資料表。</span><span class="sxs-lookup"><span data-stu-id="61185-177">We split our test dataset into two different tables because one of the days is a holiday, and we want to determine if the model can detect differences between a holiday and non-holiday from the clickthrough rate.</span></span>

<span data-ttu-id="61185-178">下面顯示指令碼 [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)，以方便使用：</span><span class="sxs-lookup"><span data-stu-id="61185-178">The script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) is displayed here for convenience:</span></span>

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

<span data-ttu-id="61185-179">請注意，這所有資料表都是外部的，因為我們只是指向 Azure Blob 儲存體 (wasb) 位置。</span><span class="sxs-lookup"><span data-stu-id="61185-179">We note that all these tables are external as we simply point to Azure Blob Storage (wasb) locations.</span></span>

<span data-ttu-id="61185-180">**有兩種方式可以執行我們現在提及的任何 Hive 查詢。**</span><span class="sxs-lookup"><span data-stu-id="61185-180">**There are two ways to execute ANY Hive query that we now mention.**</span></span>

1. <span data-ttu-id="61185-181">**使用 Hive REPL 命令列**：第一個是發出 "hive" 命令，複製查詢並在 Hive REPL 命令列貼上。</span><span class="sxs-lookup"><span data-stu-id="61185-181">**Using the Hive REPL command-line**: The first is to issue a "hive" command and copy and paste a query at the Hive REPL command-line.</span></span> <span data-ttu-id="61185-182">若要這樣做，請執行：</span><span class="sxs-lookup"><span data-stu-id="61185-182">To do this, do:</span></span>
   
        cd %hive_home%\bin
        hive
   
     <span data-ttu-id="61185-183">現在，在 REPL 命令列，剪下和貼上查詢即可執行。</span><span class="sxs-lookup"><span data-stu-id="61185-183">Now at the REPL command-line, cutting and pasting the query executes it.</span></span>
2. <span data-ttu-id="61185-184">**將查詢儲存到檔案，並執行命令**：第二個是要將查詢儲存為 .hql 檔案 ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) 然後發出下列命令以執行查詢：</span><span class="sxs-lookup"><span data-stu-id="61185-184">**Saving queries to a file and executing the command**: The second is to save the queries to a .hql file ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) and then issue the following command to execute the query:</span></span>
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a><span data-ttu-id="61185-185">確認資料庫和資料表的建立</span><span class="sxs-lookup"><span data-stu-id="61185-185">Confirm database and table creation</span></span>
<span data-ttu-id="61185-186">接下來，我們從 Hive bin/ 目錄提示使用下列命令，確認資料庫的建立：</span><span class="sxs-lookup"><span data-stu-id="61185-186">Next, we confirm the creation of the database with the following command from the Hive bin/ directory prompt:</span></span>

        hive -e "show databases;"

<span data-ttu-id="61185-187">這會提供：</span><span class="sxs-lookup"><span data-stu-id="61185-187">This gives:</span></span>

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

<span data-ttu-id="61185-188">這會確認建立新資料庫，也就是 "criteo"。</span><span class="sxs-lookup"><span data-stu-id="61185-188">This confirms the creation of the new database, "criteo".</span></span>

<span data-ttu-id="61185-189">若要查看我們建立的資料表，我們只要從 Hive bin/ 目錄提示發出以下命令：</span><span class="sxs-lookup"><span data-stu-id="61185-189">To see what tables we created, we simply issue the command here from the Hive bin/ directory prompt:</span></span>

        hive -e "show tables in criteo;"

<span data-ttu-id="61185-190">我們會看到下列輸出：</span><span class="sxs-lookup"><span data-stu-id="61185-190">We then see the following output:</span></span>

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <span data-ttu-id="61185-191"><a name="exploration"></a> 在 Hive 中的資料瀏覽</span><span class="sxs-lookup"><span data-stu-id="61185-191"><a name="exploration"></a> Data exploration in Hive</span></span>
<span data-ttu-id="61185-192">現在我們已準備好在 Hive 中執行一些基本的資料瀏覽。</span><span class="sxs-lookup"><span data-stu-id="61185-192">Now we are ready to do some basic data exploration in Hive.</span></span> <span data-ttu-id="61185-193">我們從計算訓練中的範例數目和測試資料的資料表開始。</span><span class="sxs-lookup"><span data-stu-id="61185-193">We begin by counting the number of examples in the train and test data tables.</span></span>

### <a name="number-of-train-examples"></a><span data-ttu-id="61185-194">訓練範例的數目</span><span class="sxs-lookup"><span data-stu-id="61185-194">Number of train examples</span></span>
<span data-ttu-id="61185-195">[sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) 的內容如下所示：</span><span class="sxs-lookup"><span data-stu-id="61185-195">The contents of [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) are shown here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_train;

<span data-ttu-id="61185-196">這會產生：</span><span class="sxs-lookup"><span data-stu-id="61185-196">This yields:</span></span>

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

<span data-ttu-id="61185-197">或者，使用者也可以從 Hive bin/ 目錄提示發出下列命令：</span><span class="sxs-lookup"><span data-stu-id="61185-197">Alternatively, one may also issue the following command from the Hive bin/ directory prompt:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-the-two-test-datasets"></a><span data-ttu-id="61185-198">兩個測試資料集中測試範例的數目</span><span class="sxs-lookup"><span data-stu-id="61185-198">Number of test examples in the two test datasets</span></span>
<span data-ttu-id="61185-199">我們現在會計算兩個測試資料集中的範例數目。</span><span class="sxs-lookup"><span data-stu-id="61185-199">We now count the number of examples in the two test datasets.</span></span> <span data-ttu-id="61185-200">[sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) 的內容如下所示：</span><span class="sxs-lookup"><span data-stu-id="61185-200">The contents of [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) are here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

<span data-ttu-id="61185-201">這會產生：</span><span class="sxs-lookup"><span data-stu-id="61185-201">This yields:</span></span>

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

<span data-ttu-id="61185-202">如往常，我們也可以透過發出命令，從 Hive bin/ 目錄提示呼叫指令碼：</span><span class="sxs-lookup"><span data-stu-id="61185-202">As usual, we may also call the script from the Hive bin/ directory prompt by issuing the command:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

<span data-ttu-id="61185-203">最後，我們將檢查以 day\_23 為基礎的測試資料集內的測試範例的數目。</span><span class="sxs-lookup"><span data-stu-id="61185-203">Finally, we examine the number of test examples in the test dataset based on day\_23.</span></span>

<span data-ttu-id="61185-204">要執行此動作的命令類似剛才顯示的命令 (請參閱 [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql))：</span><span class="sxs-lookup"><span data-stu-id="61185-204">The command to do this is similar to the one just shown (refer to [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

<span data-ttu-id="61185-205">這會提供：</span><span class="sxs-lookup"><span data-stu-id="61185-205">This gives:</span></span>

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-the-train-dataset"></a><span data-ttu-id="61185-206">訓練資料集中的標籤分佈</span><span class="sxs-lookup"><span data-stu-id="61185-206">Label distribution in the train dataset</span></span>
<span data-ttu-id="61185-207">訓練資料集中的標籤分佈值得一提。</span><span class="sxs-lookup"><span data-stu-id="61185-207">The label distribution in the train dataset is of interest.</span></span> <span data-ttu-id="61185-208">為了看到此結果，我們顯示 [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql) 的內容：</span><span class="sxs-lookup"><span data-stu-id="61185-208">To see this, we show contents of [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span></span>

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

<span data-ttu-id="61185-209">這會產生標籤分佈：</span><span class="sxs-lookup"><span data-stu-id="61185-209">This yields the label distribution:</span></span>

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

<span data-ttu-id="61185-210">請注意，正數標籤的百分比為大約 3.3% (與原始資料集一致)。</span><span class="sxs-lookup"><span data-stu-id="61185-210">Note that the percentage of positive labels is about 3.3% (consistent with the original dataset).</span></span>

### <a name="histogram-distributions-of-some-numeric-variables-in-the-train-dataset"></a><span data-ttu-id="61185-211">訓練資料集中一些數值變數的長條圖分佈</span><span class="sxs-lookup"><span data-stu-id="61185-211">Histogram distributions of some numeric variables in the train dataset</span></span>
<span data-ttu-id="61185-212">我們可以使用 Hive 的原生 "histogram\_numeric" 函式，來了解數值變數分佈的外觀。</span><span class="sxs-lookup"><span data-stu-id="61185-212">We can use Hive's native "histogram\_numeric" function to find out what the distribution of the numeric variables looks like.</span></span> <span data-ttu-id="61185-213">以下是 [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql) 的內容：</span><span class="sxs-lookup"><span data-stu-id="61185-213">Here are the contents of [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span></span>

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

<span data-ttu-id="61185-214">這會產生下列：</span><span class="sxs-lookup"><span data-stu-id="61185-214">This yields the following:</span></span>

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

<span data-ttu-id="61185-215">橫向檢視 - Hive 中的切割組合是用來產生類似 SQL 的輸出，而不是一般的清單。</span><span class="sxs-lookup"><span data-stu-id="61185-215">The LATERAL VIEW - explode combination in Hive serves to produce a SQL-like output instead of the usual list.</span></span> <span data-ttu-id="61185-216">請注意，在此資料表中，第一個資料行對應至 bin 中心，而第二個對應至 bin 頻率。</span><span class="sxs-lookup"><span data-stu-id="61185-216">Note that in the this table, the first column corresponds to the bin center and the second to the bin frequency.</span></span>

### <a name="approximate-percentiles-of-some-numeric-variables-in-the-train-dataset"></a><span data-ttu-id="61185-217">訓練資料集中一些數值變數的近似百分比</span><span class="sxs-lookup"><span data-stu-id="61185-217">Approximate percentiles of some numeric variables in the train dataset</span></span>
<span data-ttu-id="61185-218">數值變數是近似百分比的計算也值得一提。</span><span class="sxs-lookup"><span data-stu-id="61185-218">Also of interest with numeric variables is the computation of approximate percentiles.</span></span> <span data-ttu-id="61185-219">Hive 的原生 "percentile\_approx" 會為我們執行此動作。</span><span class="sxs-lookup"><span data-stu-id="61185-219">Hive's native "percentile\_approx" does this for us.</span></span> <span data-ttu-id="61185-220">[sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) 的內容為：</span><span class="sxs-lookup"><span data-stu-id="61185-220">The contents of [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) are:</span></span>

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

<span data-ttu-id="61185-221">這會產生：</span><span class="sxs-lookup"><span data-stu-id="61185-221">This yields:</span></span>

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

<span data-ttu-id="61185-222">我們注意到百分比的分佈與通常任何數值變數的長條圖分佈相關。</span><span class="sxs-lookup"><span data-stu-id="61185-222">We remark that the distribution of percentiles is closely related to the histogram distribution of any numeric variable usually.</span></span>         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-the-train-dataset"></a><span data-ttu-id="61185-223">尋找訓練資料集中的某些類別資料行的唯一值數目</span><span class="sxs-lookup"><span data-stu-id="61185-223">Find number of unique values for some categorical columns in the train dataset</span></span>
<span data-ttu-id="61185-224">繼續進行資料瀏覽，我們現在發現，對於某些類別資料行，他們所採取的唯一值數目。</span><span class="sxs-lookup"><span data-stu-id="61185-224">Continuing the data exploration, we now find, for some categorical columns, the number of unique values they take.</span></span> <span data-ttu-id="61185-225">為了執行此動作，我們顯示 [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql) 的內容：</span><span class="sxs-lookup"><span data-stu-id="61185-225">To do this, we show contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span></span>

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

<span data-ttu-id="61185-226">這會產生：</span><span class="sxs-lookup"><span data-stu-id="61185-226">This yields:</span></span>

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

<span data-ttu-id="61185-227">我們注意到 Col15 有 1900 萬個唯一值！</span><span class="sxs-lookup"><span data-stu-id="61185-227">We note that Col15 has 19M unique values!</span></span> <span data-ttu-id="61185-228">使用貝氏方法，像是「一個有效編碼」來編碼這類高維度類別變數不可行。</span><span class="sxs-lookup"><span data-stu-id="61185-228">Using naive techniques like "one-hot encoding" to encode such high-dimensional categorical variables is infeasible.</span></span> <span data-ttu-id="61185-229">特別是，我們將說明並示範稱為 [以計數學習](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) 功能強大又穩健的技術，以有效率地解決此問題。</span><span class="sxs-lookup"><span data-stu-id="61185-229">In particular, we explain and demonstrate a powerful, robust technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) for tackling this problem efficiently.</span></span>

<span data-ttu-id="61185-230">我們在這個子節的最後來看一下一些其他類別資料行的唯一值數目。</span><span class="sxs-lookup"><span data-stu-id="61185-230">We end this sub-section by looking at the number of unique values for some other categorical columns as well.</span></span> <span data-ttu-id="61185-231">[sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) 的內容為：</span><span class="sxs-lookup"><span data-stu-id="61185-231">The contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) are:</span></span>

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

<span data-ttu-id="61185-232">這會產生：</span><span class="sxs-lookup"><span data-stu-id="61185-232">This yields:</span></span>

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

<span data-ttu-id="61185-233">我們看到，除了 Col20 以外，所有其他資料行都有許多唯一值。</span><span class="sxs-lookup"><span data-stu-id="61185-233">Again we see that except for Col20, all the other columns have many unique values.</span></span>

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-the-train-dataset"></a><span data-ttu-id="61185-234">定型資料集中成對類別變數的共生計數</span><span class="sxs-lookup"><span data-stu-id="61185-234">Co-occurrence counts of pairs of categorical variables in the train dataset</span></span>

<span data-ttu-id="61185-235">定型資料集中成對類別變數的共生計數也很有趣。</span><span class="sxs-lookup"><span data-stu-id="61185-235">The co-occurrence counts of pairs of categorical variables is also of interest.</span></span> <span data-ttu-id="61185-236">這可以使用 [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql) 中的程式碼來判斷：</span><span class="sxs-lookup"><span data-stu-id="61185-236">This can be determined using the code in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span></span>

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

<span data-ttu-id="61185-237">我們將依其發生計數反轉順序，並在此情況下查看前 15 個。</span><span class="sxs-lookup"><span data-stu-id="61185-237">We reverse order the counts by their occurrence and look at the top 15 in this case.</span></span> <span data-ttu-id="61185-238">這會提供：</span><span class="sxs-lookup"><span data-stu-id="61185-238">This gives us:</span></span>

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <span data-ttu-id="61185-239"><a name="downsample"></a> 對 Azure Machine Learning 的資料集縮減取樣</span><span class="sxs-lookup"><span data-stu-id="61185-239"><a name="downsample"></a> Down sample the datasets for Azure Machine Learning</span></span>
<span data-ttu-id="61185-240">探索資料集並示範了我們如何可對任何變數 (包括組合) 的這類探索進行的動作之後，我們現在要對資料集縮減取樣，讓我們可以在 Azure Machine Learning 中建置模型。</span><span class="sxs-lookup"><span data-stu-id="61185-240">Having explored the datasets and demonstrated how we may do this type of exploration for any variables (including combinations), we now down sample the data sets so that we can build models in Azure Machine Learning.</span></span> <span data-ttu-id="61185-241">回顧一下我們著重的問題在於：提供一組範例屬性 (從 Col2 到 Col40 的功能值)，我們預測 Col1 是否為 0 (未按一下) 或 1 (按一下)。</span><span class="sxs-lookup"><span data-stu-id="61185-241">Recall that the problem we focus on is: given a set of example attributes (feature values from Col2 - Col40), we predict if Col1 is a 0 (no click) or a 1 (click).</span></span>

<span data-ttu-id="61185-242">為了對我們的訓練和測試資料集縮減取樣至原始大小的 1%，我們使用 Hive 的原生 RAND() 函式。</span><span class="sxs-lookup"><span data-stu-id="61185-242">To down sample our train and test datasets to 1% of the original size, we use Hive's native RAND() function.</span></span> <span data-ttu-id="61185-243">下一個指令碼 ([sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql)) 會為訓練資料集執行此動作：</span><span class="sxs-lookup"><span data-stu-id="61185-243">The next script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) does this for the train dataset:</span></span>

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

<span data-ttu-id="61185-244">這會產生：</span><span class="sxs-lookup"><span data-stu-id="61185-244">This yields:</span></span>

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

<span data-ttu-id="61185-245">[sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql)指令碼會為測試資料 day\_22 執行此動作：</span><span class="sxs-lookup"><span data-stu-id="61185-245">The script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) does it for test data, day\_22:</span></span>

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

<span data-ttu-id="61185-246">這會產生：</span><span class="sxs-lookup"><span data-stu-id="61185-246">This yields:</span></span>

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


<span data-ttu-id="61185-247">最後，[sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql)指令碼會為測試資料 day\_23 執行此動作：</span><span class="sxs-lookup"><span data-stu-id="61185-247">Finally, the script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) does it for test data, day\_23:</span></span>

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

<span data-ttu-id="61185-248">這會產生：</span><span class="sxs-lookup"><span data-stu-id="61185-248">This yields:</span></span>

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

<span data-ttu-id="61185-249">以此方式，我們已準備好使用縮減取樣的訓練和測試資料集，在 Azure Machine Learning 模型中建置模型。</span><span class="sxs-lookup"><span data-stu-id="61185-249">With this, we are ready to use our down sampled train and test datasets for building models in Azure Machine Learning.</span></span>

<span data-ttu-id="61185-250">在我們繼續 Azure Machine Learning 之前，還有最後一個重要元件是考量計數資料表。</span><span class="sxs-lookup"><span data-stu-id="61185-250">There is a final important component before we move on to Azure Machine Learning, which is concerns the count table.</span></span> <span data-ttu-id="61185-251">在下一個子節中，我們將就此討論一些細節。</span><span class="sxs-lookup"><span data-stu-id="61185-251">In the next sub-section, we discuss this in some detail.</span></span>

## <span data-ttu-id="61185-252"><a name="count"></a> 計數資料表的簡短討論</span><span class="sxs-lookup"><span data-stu-id="61185-252"><a name="count"></a> A brief discussion on the count table</span></span>
<span data-ttu-id="61185-253">如我們所見，數個類別變數有極高的維度性。</span><span class="sxs-lookup"><span data-stu-id="61185-253">As we saw, several categorical variables have a very high dimensionality.</span></span> <span data-ttu-id="61185-254">在我們的逐步解說中，我們會提供稱為 [以計數學習](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) 的強大技術，以便利用有效率且穩健的方式編碼這些變數。</span><span class="sxs-lookup"><span data-stu-id="61185-254">In our walkthrough, we present a powerful technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) to encode these variables in an efficient, robust manner.</span></span> <span data-ttu-id="61185-255">提供的連結中說明此技術的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="61185-255">More information on this technique is in the link provided.</span></span>

[!NOTE]
><span data-ttu-id="61185-256">在本逐步解說中，我們著重在使用計數資料表來產生高維度類別功能的精簡表示法。</span><span class="sxs-lookup"><span data-stu-id="61185-256">In this walkthrough, we focus on using count tables to produce compact representations of high-dimensional categorical features.</span></span> <span data-ttu-id="61185-257">這不是編碼類別功能的唯一方式；如需有關其他技術的詳細資訊，有興趣的使用者可以查看 [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) 和[特徵雜湊](http://en.wikipedia.org/wiki/Feature_hashing)。</span><span class="sxs-lookup"><span data-stu-id="61185-257">This is not the only way to encode categorical features; for more information on other techniques, interested users can check out [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) and [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span></span>
>

<span data-ttu-id="61185-258">為了對計數資料建置計數資料表，我們使用 raw/count 資料夾中的資料。</span><span class="sxs-lookup"><span data-stu-id="61185-258">To build count tables on the count data, we use the data in the folder raw/count.</span></span> <span data-ttu-id="61185-259">在模型建構區段中，我們告訴使用者如何從頭建置類別功能的這些計數資料表，或是可以為其瀏覽使用預先建置的計數資料表。</span><span class="sxs-lookup"><span data-stu-id="61185-259">In the modeling section, we show users how to build these count tables for categorical features from scratch, or alternatively to use a pre-built count table for their explorations.</span></span> <span data-ttu-id="61185-260">在下面，我們提到「預先建置的計數資料表」時，表示使用我們提供的計數資料表。</span><span class="sxs-lookup"><span data-stu-id="61185-260">In what follows, when we refer to "pre-built count tables", we mean using the count tables that we provide.</span></span> <span data-ttu-id="61185-261">有關如何存取這些資料表的詳細指示會在下一節提供。</span><span class="sxs-lookup"><span data-stu-id="61185-261">Detailed instructions on how to access these tables are provided in the next section.</span></span>

## <span data-ttu-id="61185-262"><a name="aml"></a> 使用 Azure Machine Learning 建置模型</span><span class="sxs-lookup"><span data-stu-id="61185-262"><a name="aml"></a> Build a model with Azure Machine Learning</span></span>
<span data-ttu-id="61185-263">在 Azure Machine Learning 建置模型的程序遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="61185-263">Our model building process in Azure Machine Learning follows these steps:</span></span>

1. [<span data-ttu-id="61185-264">從 Hive 資料表取得資料到 Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="61185-264">Get the data from Hive tables into Azure Machine Learning</span></span>](#step1)
2. [<span data-ttu-id="61185-265">建立實驗︰清除資料，並使用計數資料表特性化</span><span class="sxs-lookup"><span data-stu-id="61185-265">Create the experiment: clean the data and featurize with count tables</span></span>](#step2)
3. [<span data-ttu-id="61185-266">建立、訓練和評分模型</span><span class="sxs-lookup"><span data-stu-id="61185-266">Build, train, and score the model</span></span>](#step3)
4. [<span data-ttu-id="61185-267">評估模型</span><span class="sxs-lookup"><span data-stu-id="61185-267">Evaluate the model</span></span>](#step4)
5. [<span data-ttu-id="61185-268">將模型發佈為 Web 服務</span><span class="sxs-lookup"><span data-stu-id="61185-268">Publish the model as a web-service</span></span>](#step5)

<span data-ttu-id="61185-269">現在我們已經準備好在 Azure Machine Learning Studio 中建置模型。</span><span class="sxs-lookup"><span data-stu-id="61185-269">Now we are ready to build models in Azure Machine Learning studio.</span></span> <span data-ttu-id="61185-270">我們縮減取樣的資料會在叢集中儲存為 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="61185-270">Our down sampled data is saved as Hive tables in the cluster.</span></span> <span data-ttu-id="61185-271">我們使用 Azure Machine Learning **匯入資料** 模組來讀取此資料。</span><span class="sxs-lookup"><span data-stu-id="61185-271">We use the Azure Machine Learning **Import Data** module to read this data.</span></span> <span data-ttu-id="61185-272">可存取此叢集之儲存體帳戶的認證會在下面提供。</span><span class="sxs-lookup"><span data-stu-id="61185-272">The credentials to access the storage account of this cluster are provided in what follows.</span></span>

### <span data-ttu-id="61185-273"><a name="step1"></a> 步驟 1：使用「匯入資料」模組從 Hive 資料表取得資料並匯入到 Azure Machine Learning，然後選取它來進行機器學習實驗</span><span class="sxs-lookup"><span data-stu-id="61185-273"><a name="step1"></a> Step 1: Get data from Hive tables into Azure Machine Learning using the Import Data module and select it for a machine learning experiment</span></span>
<span data-ttu-id="61185-274">藉由選取 [+ 新增] -> [實驗] -> [空白實驗] 開始。</span><span class="sxs-lookup"><span data-stu-id="61185-274">Start by selecting a **+NEW** -> **EXPERIMENT** -> **Blank Experiment**.</span></span> <span data-ttu-id="61185-275">接著，從左上方的 [搜尋]  方塊，搜尋「匯入資料」。</span><span class="sxs-lookup"><span data-stu-id="61185-275">Then, from the **Search** box on the top left, search for "Import Data".</span></span> <span data-ttu-id="61185-276">將 [匯入資料]  模組拖放到實驗畫布 (螢幕的中間部分) 上，以將模組用於資料存取。</span><span class="sxs-lookup"><span data-stu-id="61185-276">Drag and drop the **Import Data** module on to the experiment canvas (the middle portion of the screen) to use the module for data access.</span></span>

<span data-ttu-id="61185-277">這是從 Hive 資料表取得資料時 **匯入資料** 看起來的樣子：</span><span class="sxs-lookup"><span data-stu-id="61185-277">This is what the **Import Data** looks like while getting data from the Hive table:</span></span>

![「匯入資料」取得資料](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

<span data-ttu-id="61185-279">針對 **匯入資料** 模組，圖形中提供的參數值都只是您需要提供之該類值的範例。</span><span class="sxs-lookup"><span data-stu-id="61185-279">For the **Import Data** module, the values of the parameters that are provided in the graphic are just examples of the sort of values you need to provide.</span></span> <span data-ttu-id="61185-280">以下是一些有關如何填寫 **匯入資料** 模組之參數集的一般指引。</span><span class="sxs-lookup"><span data-stu-id="61185-280">Here is some general guidance on how to fill out the parameter set for the **Import Data** module.</span></span>

1. <span data-ttu-id="61185-281">對 **資料來源**</span><span class="sxs-lookup"><span data-stu-id="61185-281">Choose "Hive query" for **Data Source**</span></span>
2. <span data-ttu-id="61185-282">在 [Hive 資料庫查詢] 方塊中，簡單的 SELECT * FROM <your\_database\_name.your\_table\_name> - 就已經足夠。</span><span class="sxs-lookup"><span data-stu-id="61185-282">In the **Hive database query** box, a simple SELECT * FROM <your\_database\_name.your\_table\_name> - is enough.</span></span>
3. <span data-ttu-id="61185-283">**Hcatalog 伺服器 URI**：如果您的叢集是 "abc"，那麼這就是：https://abc.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="61185-283">**Hcatalog server URI**: If your cluster is "abc", then this is simply: https://abc.azurehdinsight.net</span></span>
4. <span data-ttu-id="61185-284">**Hadoop 使用者帳戶名稱**：委任叢集時選擇的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="61185-284">**Hadoop user account name**: The user name chosen at the time of commissioning the cluster.</span></span> <span data-ttu-id="61185-285">(非遠端存取使用者名稱！)</span><span class="sxs-lookup"><span data-stu-id="61185-285">(NOT the Remote Access user name!)</span></span>
5. <span data-ttu-id="61185-286">**Hadoop 使用者帳戶密碼**：委任叢集時選擇之使用者名稱的密碼。</span><span class="sxs-lookup"><span data-stu-id="61185-286">**Hadoop user account password**: The password for the user name chosen at the time of commissioning the cluster.</span></span> <span data-ttu-id="61185-287">(非遠端存取密碼！)</span><span class="sxs-lookup"><span data-stu-id="61185-287">(NOT the Remote Access password!)</span></span>
6. <span data-ttu-id="61185-288">**輸出資料的位置**：選擇 "Azure"</span><span class="sxs-lookup"><span data-stu-id="61185-288">**Location of output data**: Choose "Azure"</span></span>
7. <span data-ttu-id="61185-289">**Azure 儲存體帳戶名稱**：和叢集相關聯的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="61185-289">**Azure storage account name**: The storage account associated with the cluster</span></span>
8. <span data-ttu-id="61185-290">**Azure 儲存體帳戶金鑰**：和叢集相關聯的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="61185-290">**Azure storage account key**: The key of the storage account associated with the cluster.</span></span>
9. <span data-ttu-id="61185-291">**Azure 容器名稱**：如果叢集名稱是 "abc"，則通常就是 "abc"。</span><span class="sxs-lookup"><span data-stu-id="61185-291">**Azure container name**: If the cluster name is "abc", then this is simply "abc", usually.</span></span>

<span data-ttu-id="61185-292">在 **匯入資料** 完成資料取得後 (您會在模組上看到綠色勾號)，請將此資料儲存為「資料集」(使用您選擇的名稱)。</span><span class="sxs-lookup"><span data-stu-id="61185-292">Once the **Import Data** finishes getting data (you see the green tick on the Module), save this data as a Dataset (with a name of your choice).</span></span> <span data-ttu-id="61185-293">看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="61185-293">What this looks like:</span></span>

![「匯入資料」儲存資料](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

<span data-ttu-id="61185-295">在 **匯入資料** 模組的輸出連接埠上按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="61185-295">Right-click the output port of the **Import Data** module.</span></span> <span data-ttu-id="61185-296">這會顯示 [另存為資料集] 選項和 [視覺化] 選項。</span><span class="sxs-lookup"><span data-stu-id="61185-296">This reveals a **Save as dataset** option and a **Visualize** option.</span></span> <span data-ttu-id="61185-297">**視覺化** 選項，如果按下，會顯示資料 100 個資料列，以及在右側面板顯示某些實用的摘要統計資料。</span><span class="sxs-lookup"><span data-stu-id="61185-297">The **Visualize** option, if clicked, displays 100 rows of the data, along with a right panel that is useful for some summary statistics.</span></span> <span data-ttu-id="61185-298">若要儲存資料，只要選取 [ **另存為資料集** ] 並遵循指示。</span><span class="sxs-lookup"><span data-stu-id="61185-298">To save data, simply select **Save as dataset** and follow instructions.</span></span>

<span data-ttu-id="61185-299">若要選取已儲存的資料集，以用於機器學習實驗，請使用下圖所示的 [搜尋]  方塊找出資料集。</span><span class="sxs-lookup"><span data-stu-id="61185-299">To select the saved dataset for use in a machine learning experiment, locate the datasets using the **Search** box shown in the following figure.</span></span> <span data-ttu-id="61185-300">然後只要輸入您提供給資料集的部分名稱即可存取它，並拖曳至主面板中。</span><span class="sxs-lookup"><span data-stu-id="61185-300">Then simply type out the name you gave the dataset partially to access it and drag the dataset onto the main panel.</span></span> <span data-ttu-id="61185-301">將它拖放到主面板中，選取它來用於機器學習模型建構。</span><span class="sxs-lookup"><span data-stu-id="61185-301">Dropping it onto the main panel selects it for use in machine learning modeling.</span></span>

![將資料集拖曳到主要面板中](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> <span data-ttu-id="61185-303">為訓練和測試資料集執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="61185-303">Do this for both the train and the test datasets.</span></span> <span data-ttu-id="61185-304">此外，請記住要使用您為此目的提供的資料庫名稱和資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="61185-304">Also, remember to use the database name and table names that you gave for this purpose.</span></span> <span data-ttu-id="61185-305">在圖中所使用的值僅供說明之用。</span><span class="sxs-lookup"><span data-stu-id="61185-305">The values used in the figure are solely for illustration purposes.**</span></span>
> 
> 

### <span data-ttu-id="61185-306"><a name="step2"></a> 步驟 2：在 Azure Machine Learning 中建立簡單的實驗來預測按一下/未按一下</span><span class="sxs-lookup"><span data-stu-id="61185-306"><a name="step2"></a> Step 2: Create a simple experiment in Azure Machine Learning to predict clicks / no clicks</span></span>
<span data-ttu-id="61185-307">我們的 Azure ML 實驗看起來如下所示：</span><span class="sxs-lookup"><span data-stu-id="61185-307">Our Azure ML experiment looks like this:</span></span>

![Machine Learning 實驗](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

<span data-ttu-id="61185-309">現在，我們會檢視這項實驗的關鍵元件。</span><span class="sxs-lookup"><span data-stu-id="61185-309">We now examine the key components of this experiment.</span></span> <span data-ttu-id="61185-310">提醒您，我們需要先將已儲存的訓練和測試資料集拖曳至我們的實驗畫布上。</span><span class="sxs-lookup"><span data-stu-id="61185-310">As a reminder, we need to drag our saved train and test datasets on to our experiment canvas first.</span></span>

#### <a name="clean-missing-data"></a><span data-ttu-id="61185-311">清除遺漏的資料</span><span class="sxs-lookup"><span data-stu-id="61185-311">Clean Missing Data</span></span>
<span data-ttu-id="61185-312">**清除遺漏的資料**模組的功能如其名稱示：以使用者指定的方式清除遺漏的資料。</span><span class="sxs-lookup"><span data-stu-id="61185-312">The **Clean Missing Data** module does what its name suggests:  it cleans missing data in ways that can be user-specified.</span></span> <span data-ttu-id="61185-313">查看此模組，我們看到這個：</span><span class="sxs-lookup"><span data-stu-id="61185-313">Looking into this module, we see this:</span></span>

![清除遺漏的資料](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

<span data-ttu-id="61185-315">在這裡，我們選擇將所有的遺漏值取代為 0。</span><span class="sxs-lookup"><span data-stu-id="61185-315">Here, we chose to replace all missing values with a 0.</span></span> <span data-ttu-id="61185-316">還有其他選項，可以藉由查看模組中的下拉式清單看到。</span><span class="sxs-lookup"><span data-stu-id="61185-316">There are other options as well, which can be seen by looking at the dropdowns in the module.</span></span>

#### <a name="feature-engineering-on-the-data"></a><span data-ttu-id="61185-317">資料上的功能工程</span><span class="sxs-lookup"><span data-stu-id="61185-317">Feature engineering on the data</span></span>
<span data-ttu-id="61185-318">大型資料集的部分類別功能可以有數百萬的唯一值。</span><span class="sxs-lookup"><span data-stu-id="61185-318">There can be millions of unique values for some categorical features of large datasets.</span></span> <span data-ttu-id="61185-319">使用像是一個有效編碼的單純方法來表示高維度類別功能是完全不可行的。</span><span class="sxs-lookup"><span data-stu-id="61185-319">Using naive methods such as one-hot encoding for representing such high-dimensional categorical features is entirely unfeasible.</span></span> <span data-ttu-id="61185-320">在本逐步解說中，我們會示範如何透過内建的 Azure Machine Learning 模組來使用計數功能產生這些高維度類別變數的壓縮表示法。</span><span class="sxs-lookup"><span data-stu-id="61185-320">In this walkthrough, we demonstrate how to use count features using built-in Azure Machine Learning modules to generate compact representations of these high-dimensional categorical variables.</span></span> <span data-ttu-id="61185-321">最後結果是較小的模型、更快速的定型時間與相當於使用其他技術的效能度量。</span><span class="sxs-lookup"><span data-stu-id="61185-321">The end-result is a smaller model size, faster training times, and performance metrics that are quite comparable to using other techniques.</span></span>

##### <a name="building-counting-transforms"></a><span data-ttu-id="61185-322">建置計數轉換</span><span class="sxs-lookup"><span data-stu-id="61185-322">Building counting transforms</span></span>
<span data-ttu-id="61185-323">若要建置計數功能，我們會使用 Azure Machine Learning 中可使用的 **建置計數轉換** 模組。</span><span class="sxs-lookup"><span data-stu-id="61185-323">To build count features, we use the **Build Counting Transform** module that is available in Azure Machine Learning.</span></span> <span data-ttu-id="61185-324">此模組如下所示：</span><span class="sxs-lookup"><span data-stu-id="61185-324">The module looks like this:</span></span>

<span data-ttu-id="61185-325">![建置計數轉換模組](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![建置計數轉換模組](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span><span class="sxs-lookup"><span data-stu-id="61185-325">![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="61185-326">在 [計數資料行] 方塊中，我們會輸入我們想要在其中執行計數的資料行。</span><span class="sxs-lookup"><span data-stu-id="61185-326">In the **Count columns** box, we enter those columns that we wish to perform counts on.</span></span> <span data-ttu-id="61185-327">一般來說，這些是 (如上所述) 高維度類別資料行。</span><span class="sxs-lookup"><span data-stu-id="61185-327">Typically, these are (as mentioned) high-dimensional categorical columns.</span></span> <span data-ttu-id="61185-328">一開始，我們曾經提及 Criteo 資料集有 26 個類別資料行：從 Col15 至 Col40。</span><span class="sxs-lookup"><span data-stu-id="61185-328">At the start, we mentioned that the Criteo dataset has 26 categorical columns: from Col15 to Col40.</span></span> <span data-ttu-id="61185-329">在這裡，我們依據這些資料行，並為其提供索引 (從 15 到 40，並以逗號分隔，如下所示)。</span><span class="sxs-lookup"><span data-stu-id="61185-329">Here, we count on all of them and give their indices (from 15 to 40 separated by commas as shown).</span></span>
> 

<span data-ttu-id="61185-330">若要使用 MapReduce 模式中的模組 (適用於大型資料集)，我們必須存取 HDInsight Hadoop 叢集 (用於功能探索的叢集可以重複用於此目的) 和它的認證。</span><span class="sxs-lookup"><span data-stu-id="61185-330">To use the module in the MapReduce mode (appropriate for large datasets), we need access to an HDInsight Hadoop cluster (the one used for feature exploration can be reused for this purpose as well) and its credentials.</span></span> <span data-ttu-id="61185-331">前面的圖表說明填入的值看起來如何 (將提供做說明用途的值取代為您自己使用案例的相關值)。</span><span class="sxs-lookup"><span data-stu-id="61185-331">The  previous figures illustrate what the filled-in values look like (replace the values provided for illustration with those relevant for your own use-case).</span></span>

![模組參數](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

<span data-ttu-id="61185-333">在上圖中，我們說明輸入 blob 位置的輸入方式。</span><span class="sxs-lookup"><span data-stu-id="61185-333">In the figure above, we show how to enter the input blob location.</span></span> <span data-ttu-id="61185-334">這個位置會保留資料以在其中建置計數資料表。</span><span class="sxs-lookup"><span data-stu-id="61185-334">This location has the data reserved for building count tables on.</span></span>

<span data-ttu-id="61185-335">完成執行此模組後，我們稍後可以在模組上以滑鼠右鍵按一下，並選取 **儲存為轉換** 選項以儲存轉換：</span><span class="sxs-lookup"><span data-stu-id="61185-335">After this module finishes running, we can save the transform for later by right-clicking the module and selecting the **Save as Transform** option:</span></span>

![「另存為轉換」選項](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

<span data-ttu-id="61185-337">在如上所示的實驗架構中，資料集 "ytransform2" 會精確地對應已儲存的計數轉換。</span><span class="sxs-lookup"><span data-stu-id="61185-337">In our experiment architecture shown above, the dataset "ytransform2" corresponds precisely to a saved count transform.</span></span> <span data-ttu-id="61185-338">針對這項實驗的其餘部分，我們假設讀取器在某些資料上使用 **建置計數轉換** 模組以產生計數，然後使用這些計數在訓練和測試資料集上產生計數功能。</span><span class="sxs-lookup"><span data-stu-id="61185-338">For the remainder of this experiment, we assume that the reader used a **Build Counting Transform** module on some data to generate counts, and can then use those counts to generate count features on the train and test datasets.</span></span>

##### <a name="choosing-what-count-features-to-include-as-part-of-the-train-and-test-datasets"></a><span data-ttu-id="61185-339">選擇要將哪些計數功能納為訓練和測試資料集的一部分</span><span class="sxs-lookup"><span data-stu-id="61185-339">Choosing what count features to include as part of the train and test datasets</span></span>
<span data-ttu-id="61185-340">一旦我們備妥計數轉換時，使用者可以使用 **修改計數資料表參數** 模組，選擇要將哪些功能納入其訓練和測試資料集。</span><span class="sxs-lookup"><span data-stu-id="61185-340">Once we have a count transform ready, the user can choose what features to include in their train and test datasets using the **Modify Count Table Parameters** module.</span></span> <span data-ttu-id="61185-341">為了完整性，我們會在此顯示這個模組，但為了簡單起見，請不要真的在實驗中使用它。</span><span class="sxs-lookup"><span data-stu-id="61185-341">We just show this module here for completeness, but in interests of simplicity do not actually use it in our experiment.</span></span>

![修改計數資料表參數](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

<span data-ttu-id="61185-343">在此情況下，如您所見，我們選擇只使用對數機率，並忽略撤退資料行。</span><span class="sxs-lookup"><span data-stu-id="61185-343">In this case, as can be seen, we have chosen to use just the log-odds and to ignore the back off column.</span></span> <span data-ttu-id="61185-344">我們也可以設定參數，例如記憶體回收 bin 臨界值，要加入多少虛擬優先範例才能平滑處理，以及是否使用任何 Laplacian 雜訊。</span><span class="sxs-lookup"><span data-stu-id="61185-344">We can also set parameters such as the garbage bin threshold, how many pseudo-prior examples to add for smoothing, and whether to use any Laplacian noise or not.</span></span> <span data-ttu-id="61185-345">這些都是進階的功能，而且要注意的是對此類功能產生的新手使用者而言，預設值是個好起點。</span><span class="sxs-lookup"><span data-stu-id="61185-345">All these are advanced features and it is to be noted that the default values are a good starting point for users who are new to this type of feature generation.</span></span>

##### <a name="data-transformation-before-generating-the-count-features"></a><span data-ttu-id="61185-346">產生計數功能之前的資料轉換</span><span class="sxs-lookup"><span data-stu-id="61185-346">Data transformation before generating the count features</span></span>
<span data-ttu-id="61185-347">現在我們要專注於一個重點，在實際產生計數功能之前要先轉換我們的訓練和測試資料。</span><span class="sxs-lookup"><span data-stu-id="61185-347">Now we focus on an important point about transforming our train and test data prior to actually generating count features.</span></span> <span data-ttu-id="61185-348">請注意，在我們將計數轉換套用至資料之前，已經使用了兩個 **執行 R 指令碼** 模組。</span><span class="sxs-lookup"><span data-stu-id="61185-348">Note that there are two **Execute R Script** modules used before we apply the count transform to our data.</span></span>

![執行 R 指令碼模組](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

<span data-ttu-id="61185-350">以下是第一個 R 指令碼：</span><span class="sxs-lookup"><span data-stu-id="61185-350">Here is the first R script:</span></span>

![第一個 R 指令碼](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

<span data-ttu-id="61185-352">在這個 R 指令碼中，我們將資料行重新命名為 "Col1" 到 "Col40" 等名稱。</span><span class="sxs-lookup"><span data-stu-id="61185-352">In this R script, we rename our columns to names "Col1" to "Col40".</span></span> <span data-ttu-id="61185-353">這是因為計數轉換必須要有這種格式的名稱。</span><span class="sxs-lookup"><span data-stu-id="61185-353">This is because the count transform expects names of this format.</span></span>

<span data-ttu-id="61185-354">在第二個 R 指令碼中，我們藉由降低取樣負類別來平衡正和負類別之間的散發 (分別為類別 1 和 0)。</span><span class="sxs-lookup"><span data-stu-id="61185-354">In the second R script, we balance the distribution between positive and negative classes (classes 1 and 0 respectively) by downsampling the negative class.</span></span> <span data-ttu-id="61185-355">此處的 R 指令碼會示範如何執行這個動作：</span><span class="sxs-lookup"><span data-stu-id="61185-355">The R script here shows how to do this:</span></span>

![第二個 R 指令碼](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

<span data-ttu-id="61185-357">在這個簡單的 R 指令碼中，我們使用 "pos\_neg\_ratio" 設定正與負類別之間的平衡數目。</span><span class="sxs-lookup"><span data-stu-id="61185-357">In this simple R script, we use "pos\_neg\_ratio" to set the amount of balance between the positive and the negative classes.</span></span> <span data-ttu-id="61185-358">這是很重要的動作，因為改善類別失衡通常會具有效能優勢，可處理類別散發扭曲的分類問題 (請記得在我們的案例中，我們有 3.3% 正類別和 96.7% 負類別)。</span><span class="sxs-lookup"><span data-stu-id="61185-358">This is important to do since improving class imbalance usually has performance benefits for classification problems where the class distribution is skewed (recall that in our case, we have 3.3% positive class and 96.7% negative class).</span></span>

##### <a name="applying-the-count-transformation-on-our-data"></a><span data-ttu-id="61185-359">在我們的資料上套用計數轉換</span><span class="sxs-lookup"><span data-stu-id="61185-359">Applying the count transformation on our data</span></span>
<span data-ttu-id="61185-360">最後，我們可以使用 **套用轉換** 模組，將計數轉換套用至我們的訓練和測試資料集。</span><span class="sxs-lookup"><span data-stu-id="61185-360">Finally, we can use the **Apply Transformation** module to apply the count transforms on our train and test datasets.</span></span> <span data-ttu-id="61185-361">此模組會將儲存的計數轉換當成輸入，將訓練或測試資料集當成其他輸入，然後利用計數功能傳回資料。</span><span class="sxs-lookup"><span data-stu-id="61185-361">This module takes the saved count transform as one input and the train or test datasets as the other input, and returns data with count features.</span></span> <span data-ttu-id="61185-362">如下所示：</span><span class="sxs-lookup"><span data-stu-id="61185-362">It is shown here:</span></span>

![套用轉換模組](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-the-count-features-look-like"></a><span data-ttu-id="61185-364">計數功能的摘錄</span><span class="sxs-lookup"><span data-stu-id="61185-364">An excerpt of what the count features look like</span></span>
<span data-ttu-id="61185-365">它對於查看我們的案例中有什麼樣的計數功能很有啟發性。</span><span class="sxs-lookup"><span data-stu-id="61185-365">It is instructive to see what the count features look like in our case.</span></span> <span data-ttu-id="61185-366">以下示範該摘錄：</span><span class="sxs-lookup"><span data-stu-id="61185-366">Here we show an excerpt of this:</span></span>

![計數功能](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

<span data-ttu-id="61185-368">在這個摘錄中，我們說明對於依賴的資料行，除了任何相關輪詢之外，我們還會取得計數和對數機率。</span><span class="sxs-lookup"><span data-stu-id="61185-368">In this excerpt, we show that for the columns that we counted on, we get the counts and log odds in addition to any relevant backoffs.</span></span>

<span data-ttu-id="61185-369">現在，我們已準備好使用這些已轉換的資料集建置 Azure Machine Learning 模型。</span><span class="sxs-lookup"><span data-stu-id="61185-369">We are now ready to build an Azure Machine Learning model using these transformed datasets.</span></span> <span data-ttu-id="61185-370">在下一節中，我們會說明如何完成此作業。</span><span class="sxs-lookup"><span data-stu-id="61185-370">In the next section, we show how this can be done.</span></span>

### <span data-ttu-id="61185-371"><a name="step3"></a> 步驟 3：建立、訓練和評分模型</span><span class="sxs-lookup"><span data-stu-id="61185-371"><a name="step3"></a> Step 3: Build, train, and score the model</span></span>

#### <a name="choice-of-learner"></a><span data-ttu-id="61185-372">選擇學習者</span><span class="sxs-lookup"><span data-stu-id="61185-372">Choice of learner</span></span>
<span data-ttu-id="61185-373">首先，我們必須選擇學習者。</span><span class="sxs-lookup"><span data-stu-id="61185-373">First, we need to choose a learner.</span></span> <span data-ttu-id="61185-374">我們要使用兩個類別推進式決策樹做為我們的學習者。</span><span class="sxs-lookup"><span data-stu-id="61185-374">We are going to use a two class boosted decision tree as our learner.</span></span> <span data-ttu-id="61185-375">以下是這個學習者的預設選項：</span><span class="sxs-lookup"><span data-stu-id="61185-375">Here are the default options for this learner:</span></span>

![二元促進式決策樹參數](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

<span data-ttu-id="61185-377">針對我們的試驗，我們會選擇預設值。</span><span class="sxs-lookup"><span data-stu-id="61185-377">For our experiment, we are going to choose the default values.</span></span> <span data-ttu-id="61185-378">我們注意到預設值通常是有意義的好方法，可以在效能上取得快速的基準。</span><span class="sxs-lookup"><span data-stu-id="61185-378">We note that the defaults are usually meaningful and a good way to get quick baselines on performance.</span></span> <span data-ttu-id="61185-379">一旦您有了基準之後，如果您選擇整理參數，您就可以藉此改善效能。</span><span class="sxs-lookup"><span data-stu-id="61185-379">You can improve on performance by sweeping parameters if you choose to once you have a baseline.</span></span>

#### <a name="train-the-model"></a><span data-ttu-id="61185-380">訓練模型</span><span class="sxs-lookup"><span data-stu-id="61185-380">Train the model</span></span>
<span data-ttu-id="61185-381">對於訓練，我們只需叫用 **訓練模型** 模組。</span><span class="sxs-lookup"><span data-stu-id="61185-381">For training, we simply invoke a **Train Model** module.</span></span> <span data-ttu-id="61185-382">它的兩個輸入是兩個類別推進式決策樹和我們的訓練資料集。</span><span class="sxs-lookup"><span data-stu-id="61185-382">The two inputs to it are the Two-Class Boosted Decision Tree learner and our train dataset.</span></span> <span data-ttu-id="61185-383">其如下所示：</span><span class="sxs-lookup"><span data-stu-id="61185-383">This is shown here:</span></span>

![訓練模組](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-the-model"></a><span data-ttu-id="61185-385">評分模型</span><span class="sxs-lookup"><span data-stu-id="61185-385">Score the model</span></span>
<span data-ttu-id="61185-386">一旦我們擁有定型模型，我們就可以在測試資料集上評分，並評估其效能。</span><span class="sxs-lookup"><span data-stu-id="61185-386">Once we have a trained model, we are ready to score on the test dataset and to evaluate its performance.</span></span> <span data-ttu-id="61185-387">我們可以使用下圖所示的**評分模型**模組，加上**評估模型**模組來執行這項作業：</span><span class="sxs-lookup"><span data-stu-id="61185-387">We do this by using the **Score Model** module shown in the following figure, along with an **Evaluate Model** module:</span></span>

![Score Model module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <span data-ttu-id="61185-389"><a name="step4"></a> 步驟 4：評估模型</span><span class="sxs-lookup"><span data-stu-id="61185-389"><a name="step4"></a> Step 4: Evaluate the model</span></span>
<span data-ttu-id="61185-390">最後，我們想要分析模型的效能。</span><span class="sxs-lookup"><span data-stu-id="61185-390">Finally, we would like to analyze model performance.</span></span> <span data-ttu-id="61185-391">通常，針對兩個類別 (二進位) 分類的問題，AUC 是良好的測量方式。</span><span class="sxs-lookup"><span data-stu-id="61185-391">Usually, for two class (binary) classification problems, a good measure is the AUC.</span></span> <span data-ttu-id="61185-392">為了將此情況視覺化，我們為此將**評分模型**模組連接至**評估模型**模組。</span><span class="sxs-lookup"><span data-stu-id="61185-392">To visualize this, we hook up the **Score Model** module to an **Evaluate Model** module for this.</span></span> <span data-ttu-id="61185-393">在 [評估模型] 模組上按一下 [視覺化] 會產生類似如下的圖形：</span><span class="sxs-lookup"><span data-stu-id="61185-393">Clicking **Visualize** on the **Evaluate Model** module yields a graphic like the following one:</span></span>

![評估模組 BDT 模型](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

<span data-ttu-id="61185-395">在二進位檔 (或兩個類別) 分類的問題中，曲線下面積 (AUC) 是預測準確度良好的測量方式。</span><span class="sxs-lookup"><span data-stu-id="61185-395">In binary (or two class) classification problems, a good measure of prediction accuracy is the Area Under Curve (AUC).</span></span> <span data-ttu-id="61185-396">接下來，我們會顯示在我們的測試資料集上使用此模型的結果。</span><span class="sxs-lookup"><span data-stu-id="61185-396">In what follows, we show our results using this model on our test dataset.</span></span> <span data-ttu-id="61185-397">若要檢查結果，請以滑鼠右鍵按一下 [評估模型] 模組的輸出連接埠，然後選取 [視覺化]。</span><span class="sxs-lookup"><span data-stu-id="61185-397">To get this, right-click the output port of the **Evaluate Model** module and then **Visualize**.</span></span>

![視覺化評估模型模組](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <span data-ttu-id="61185-399"><a name="step5"></a> 步驟 5：將模型發佈為 Web 服務</span><span class="sxs-lookup"><span data-stu-id="61185-399"><a name="step5"></a> Step 5: Publish the model as a Web service</span></span>
<span data-ttu-id="61185-400">發佈 Azure Machine Learning 做為引起最少抱怨之 web 服務的功能，乃是使其可廣泛使用的寶貴功能。</span><span class="sxs-lookup"><span data-stu-id="61185-400">The ability to publish an Azure Machine Learning model as web services with a minimum of fuss is a valuable feature for making it widely available.</span></span> <span data-ttu-id="61185-401">完成作業後，任何人都可以利用他們需要預測的輸入資料來呼叫 web 服務，而 web 服務可使用模型傳回這些預測。</span><span class="sxs-lookup"><span data-stu-id="61185-401">Once that is done, anyone can make calls to the web service with input data that they need predictions for, and the web service uses the model to return those predictions.</span></span>

<span data-ttu-id="61185-402">若要執行此動作，我們先將我們的訓練模型儲存為訓練的模型物件。</span><span class="sxs-lookup"><span data-stu-id="61185-402">To do this, we first save our trained model as a Trained Model object.</span></span> <span data-ttu-id="61185-403">做法是以滑鼠右鍵按一下 [訓練模型] 模組，並使用 [儲存為訓練模型] 選項。</span><span class="sxs-lookup"><span data-stu-id="61185-403">This is done by right-clicking the **Train Model** module and using the **Save as Trained Model** option.</span></span>

<span data-ttu-id="61185-404">接下來，我們需要建立 web 服務的輸入和輸出連接埠：</span><span class="sxs-lookup"><span data-stu-id="61185-404">Next, we need to create input and output ports for our web service:</span></span>

* <span data-ttu-id="61185-405">輸入連接埠會採用的資料形式和我們需要預測的資料相同</span><span class="sxs-lookup"><span data-stu-id="61185-405">an input port takes data in the same form as the data that we need predictions for</span></span>
* <span data-ttu-id="61185-406">輸出連接埠會傳回評分標籤和相關聯的機率。</span><span class="sxs-lookup"><span data-stu-id="61185-406">an output port returns the Scored Labels and the associated probabilities.</span></span>

#### <a name="select-a-few-rows-of-data-for-the-input-port"></a><span data-ttu-id="61185-407">為輸入連接埠選取幾個資料列的資料</span><span class="sxs-lookup"><span data-stu-id="61185-407">Select a few rows of data for the input port</span></span>
<span data-ttu-id="61185-408">我們可以方便地使用 **套用 SQL 轉換** 模組，僅選取 10 個資料列做為輸入連接埠資料。</span><span class="sxs-lookup"><span data-stu-id="61185-408">It is convenient to use an **Apply SQL Transformation** module to select just 10 rows to serve as the input port data.</span></span> <span data-ttu-id="61185-409">使用這裡顯示的 SQL 查詢，只為我們的輸入連接埠選取資料列：</span><span class="sxs-lookup"><span data-stu-id="61185-409">Select just these rows of data for our input port using the SQL query shown here:</span></span>

![輸入連接埠資料](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a><span data-ttu-id="61185-411">Web 服務</span><span class="sxs-lookup"><span data-stu-id="61185-411">Web service</span></span>
<span data-ttu-id="61185-412">現在，我們已經準備好執行可以用來發佈 Web 服務的小型試驗。</span><span class="sxs-lookup"><span data-stu-id="61185-412">Now we are ready to run a small experiment that can be used to publish our web service.</span></span>

#### <a name="generate-input-data-for-webservice"></a><span data-ttu-id="61185-413">產生 Web 服務的輸入資料</span><span class="sxs-lookup"><span data-stu-id="61185-413">Generate input data for webservice</span></span>
<span data-ttu-id="61185-414">做為預備步驟，由於計數資料表很大，我們會取得幾行測試資料，並使用計數功能從它產生輸出資料。</span><span class="sxs-lookup"><span data-stu-id="61185-414">As a zeroth step, since the count table is large, we take a few lines of test data and generate output data from it with count features.</span></span> <span data-ttu-id="61185-415">這會做為 web 服務的輸入資料格式。</span><span class="sxs-lookup"><span data-stu-id="61185-415">This can serve as the input data format for our webservice.</span></span> <span data-ttu-id="61185-416">其如下所示：</span><span class="sxs-lookup"><span data-stu-id="61185-416">This is shown here:</span></span>

![建立 BDT 輸入資料](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> <span data-ttu-id="61185-418">針對輸入資料格式，我們現在要使用 **計數 Featurizer** 模組的輸出。</span><span class="sxs-lookup"><span data-stu-id="61185-418">For the input data format, we now use the OUTPUT of the **Count Featurizer** module.</span></span> <span data-ttu-id="61185-419">一旦此實驗執行完成，將輸出從 **計數 Featurizer** 模組儲存為資料集。</span><span class="sxs-lookup"><span data-stu-id="61185-419">Once this experiment finishes running, save the output from the **Count Featurizer** module as a Dataset.</span></span> <span data-ttu-id="61185-420">此資料集會用於 Web 服務中的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="61185-420">This Dataset is used for the input data in the webservice.</span></span>
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a><span data-ttu-id="61185-421">發佈 Web 服務的評分實驗</span><span class="sxs-lookup"><span data-stu-id="61185-421">Scoring experiment for publishing webservice</span></span>
<span data-ttu-id="61185-422">首先，我們顯示其外觀。</span><span class="sxs-lookup"><span data-stu-id="61185-422">First, we show what this looks like.</span></span> <span data-ttu-id="61185-423">基本結構是**評分模型**模組，其會接受我們的訓練模型物件和我們在先前步驟中使用**計數 Featurizer** 模組產生的一些輸入資料行。</span><span class="sxs-lookup"><span data-stu-id="61185-423">The essential structure is a **Score Model** module that accepts our trained model object and a few lines of input data that we generated in the previous steps using the **Count Featurizer** module.</span></span> <span data-ttu-id="61185-424">我們使用「選取資料集中的資料行」來投射出評分標籤和評分機率。</span><span class="sxs-lookup"><span data-stu-id="61185-424">We use "Select Columns in Dataset" to project out the Scored labels and the Score probabilities.</span></span>

![選取資料集中的資料行](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

<span data-ttu-id="61185-426">請注意如何使用「選取資料集中的資料行」  模組來「篩選」掉資料集中的資料。</span><span class="sxs-lookup"><span data-stu-id="61185-426">Notice how the **Select Columns in Dataset** module can be used for 'filtering' data out from a dataset.</span></span> <span data-ttu-id="61185-427">我們在此顯示內容：</span><span class="sxs-lookup"><span data-stu-id="61185-427">We show the contents here:</span></span>

![使用「選取資料集中的資料行」模組來進行的篩選](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

<span data-ttu-id="61185-429">若要取得藍色的輸入和輸出連接埠，您只要按一下位於右下方的 [ **準備 Web 服務** ]。</span><span class="sxs-lookup"><span data-stu-id="61185-429">To get the blue input and output ports, you simply click **prepare webservice** at the bottom right.</span></span> <span data-ttu-id="61185-430">執行這項實驗也可讓我們發佈 Web 服務：按一下右下方的 [發佈 Web 服務]  圖示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="61185-430">Running this experiment also allows us to publish the web service: click the **PUBLISH WEB SERVICE** icon at the bottom right, shown here:</span></span>

![發佈 Web 服務](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

<span data-ttu-id="61185-432">發佈 Web 服務之後，我們會被重新導向至看起來如下的頁面：</span><span class="sxs-lookup"><span data-stu-id="61185-432">Once the webservice is published, we get redirected to a page that looks thus:</span></span>

![Web 服務儀表板](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

<span data-ttu-id="61185-434">我們在左邊看到兩個 Web 服務的連結：</span><span class="sxs-lookup"><span data-stu-id="61185-434">We see two links for webservices on the left side:</span></span>

* <span data-ttu-id="61185-435">**要求/回應** 服務 (或 RRS) 適用於單一預測，我們會在這場研討會中使用。</span><span class="sxs-lookup"><span data-stu-id="61185-435">The **REQUEST/RESPONSE** Service (or RRS) is meant for single predictions and is what we utilize in this workshop.</span></span>
* <span data-ttu-id="61185-436">**批次執行** 服務 (BES) 用於批次預測，而且要求要用來進行預測的輸入資料位於 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="61185-436">The **BATCH EXECUTION** Service (BES) is used for batch predictions and requires that the input data used to make predictions reside in Azure Blob Storage.</span></span>

<span data-ttu-id="61185-437">按一下連結**要求/回應**會帶我們前往提供我們以 C#、python 和 R 預先定義程式碼的頁面。此程式碼可以方便地用於對 Web 服務進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="61185-437">Clicking on the link **REQUEST/RESPONSE** takes us to a page that gives us pre-canned code in C#, python, and R. This code can be conveniently used for making calls to the webservice.</span></span> <span data-ttu-id="61185-438">請注意，需要使用此頁面上的 API 金鑰來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="61185-438">Note that the API key on this page needs to be used for authentication.</span></span>

<span data-ttu-id="61185-439">將此 python 程式碼複製到 IPython notebook 中新的儲存格很方便。</span><span class="sxs-lookup"><span data-stu-id="61185-439">It is convenient to copy this python code over to a new cell in the IPython notebook.</span></span>

<span data-ttu-id="61185-440">下面我們顯示一段具有正確的 API 金鑰的 python 程式碼。</span><span class="sxs-lookup"><span data-stu-id="61185-440">Here we show a segment of python code with the correct API key.</span></span>

![Python 程式碼](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

<span data-ttu-id="61185-442">請注意，我們將預設 API 金鑰取代為 Web 服務的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="61185-442">Note that we replaced the default API key with our webservices's API key.</span></span> <span data-ttu-id="61185-443">按一下 IPython notebook 中此儲存格上的 [ **執行** ] 會產生下列回應：</span><span class="sxs-lookup"><span data-stu-id="61185-443">Clicking **Run** on this cell in an IPython notebook yields the following response:</span></span>

![IPython 回應](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

<span data-ttu-id="61185-445">我們會看到對我們要求的兩個測試範例 (在 python 指令碼的 JSON 架構中)，我們會以 "Scored Labels, Scored Probabilities" 形式獲得解答。</span><span class="sxs-lookup"><span data-stu-id="61185-445">We see that for the two test examples we asked about (in the JSON framework of the python script), we get back answers in the form "Scored Labels, Scored Probabilities".</span></span> <span data-ttu-id="61185-446">請注意，在此情況下，我們選擇預先定義的程式碼提供的預設值 (所有數值資料行為 0，所有類別資料行為字串 "value")。</span><span class="sxs-lookup"><span data-stu-id="61185-446">Note that in this case, we chose the default values that the pre-canned code provides (0's for all numeric columns and the string "value" for all categorical columns).</span></span>

<span data-ttu-id="61185-447">這包含我們的端對端逐步解說，示範如何使用 Azure Machine Learning 處理大型資料集。</span><span class="sxs-lookup"><span data-stu-id="61185-447">This concludes our end-to-end walkthrough showing how to handle large-scale dataset using Azure Machine Learning.</span></span> <span data-ttu-id="61185-448">我們開始使用 1 TB 的資料、建構預測模型，並將其部署為雲端中的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="61185-448">We started with a terabyte of data, constructed a prediction model and deployed it as a web service in the cloud.</span></span>

