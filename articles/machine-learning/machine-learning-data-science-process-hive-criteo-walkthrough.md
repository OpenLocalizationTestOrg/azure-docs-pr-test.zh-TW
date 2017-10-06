---
title: "hello 小組資料科學程序中為 1 TB 的資料集上使用 Azure HDInsight Hadoop 叢集動作 |Microsoft 文件"
description: "使用 hello 小組資料科學程序的端對端案例，採用 HDInsight Hadoop 叢集 toobuild 及部署模型，使用大型 (1TB) 公開可用資料集"
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
ms.openlocfilehash: 59b2af02e7840cb60a4b5b2f2c8ab0611df198ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a><span data-ttu-id="2063c-103">-1 TB 的資料集上使用 Azure HDInsight Hadoop 叢集動作中的 hello 小組資料科學程序</span><span class="sxs-lookup"><span data-stu-id="2063c-103">hello Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset</span></span>

<span data-ttu-id="2063c-104">本逐步解說將示範使用 hello 在端對端案例中使用資料科學的小組流程[Azure HDInsight Hadoop 叢集](https://azure.microsoft.com/services/hdinsight/)toostore，瀏覽、 功能工程師編寫，並公開向下一個 hello 的取樣資料可用[Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/)資料集。</span><span class="sxs-lookup"><span data-stu-id="2063c-104">In this walkthrough, we demonstrate using hello Team Data Science Process in an end-to-end scenario with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore, feature engineer, and down sample data from one of hello publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) datasets.</span></span> <span data-ttu-id="2063c-105">我們在此資料上使用 Azure Machine Learning toobuild 二元分類模型。</span><span class="sxs-lookup"><span data-stu-id="2063c-105">We use Azure Machine Learning toobuild a binary classification model on this data.</span></span> <span data-ttu-id="2063c-106">我們也將顯示如何 toopublish 下列其中一種模型做為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="2063c-106">We also show how toopublish one of these models as a Web service.</span></span>

<span data-ttu-id="2063c-107">它也是可能 toouse IPython 筆記型電腦 tooaccomplish hello 工作本逐步解說。</span><span class="sxs-lookup"><span data-stu-id="2063c-107">It is also possible toouse an IPython notebook tooaccomplish hello tasks presented in this walkthrough.</span></span> <span data-ttu-id="2063c-108">使用者會像這種方法，應洽詢的 tootry hello [Criteo 逐步解說使用 hive 控制檔的 ODBC 連接](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb)主題。</span><span class="sxs-lookup"><span data-stu-id="2063c-108">Users who would like tootry this approach should consult hello [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="2063c-109"><a name="dataset"></a>Criteo 資料集說明</span><span class="sxs-lookup"><span data-stu-id="2063c-109"><a name="dataset"></a>Criteo Dataset Description</span></span>
<span data-ttu-id="2063c-110">hello Criteo 資料是按預測資料集，大約是 370 GB gzip 壓縮 TSV 檔案 (~1.3TB 未壓縮)，可包含多個 4.3 10 億個資料錄。</span><span class="sxs-lookup"><span data-stu-id="2063c-110">hello Criteo data is a click prediction dataset that is approximately 370GB of gzip compressed TSV files (~1.3TB uncompressed), comprising more than 4.3 billion records.</span></span> <span data-ttu-id="2063c-111">它取自 [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/)提供的 24 天點選資料。</span><span class="sxs-lookup"><span data-stu-id="2063c-111">It is taken from 24 days of click data made available by [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span></span> <span data-ttu-id="2063c-112">為資料科學家的 hello 方便起見，我們已將工具解壓縮資料可用 toous 的 tooexperiment 與。</span><span class="sxs-lookup"><span data-stu-id="2063c-112">For hello convenience of data scientists, we have unzipped data available toous tooexperiment with.</span></span>

<span data-ttu-id="2063c-113">在此資料集中的每一筆記錄包含 40 個資料行：</span><span class="sxs-lookup"><span data-stu-id="2063c-113">Each record in this dataset contains 40 columns:</span></span>

* <span data-ttu-id="2063c-114">hello 第一個資料行是標籤資料行，指出使用者是否按一下**新增**（值 1） 或不按一下其中一個 （值 0）</span><span class="sxs-lookup"><span data-stu-id="2063c-114">hello first column is a label column that indicates whether a user clicks an **add** (value 1) or does not click one (value 0)</span></span>
* <span data-ttu-id="2063c-115">接下來 13 個資料行是數字，以及</span><span class="sxs-lookup"><span data-stu-id="2063c-115">next 13 columns are numeric, and</span></span>
* <span data-ttu-id="2063c-116">最後 26 個資料行是類別資料行</span><span class="sxs-lookup"><span data-stu-id="2063c-116">last 26 are categorical columns</span></span>

<span data-ttu-id="2063c-117">hello 資料行匿名的並使用一連串的列舉名稱:"Col1"（適用於 hello 標籤資料行） 太 ' Col40"（為 hello 最後的類別資料行）。</span><span class="sxs-lookup"><span data-stu-id="2063c-117">hello columns are anonymized and use a series of enumerated names: "Col1" (for hello label column) too'Col40" (for hello last categorical column).</span></span>            

<span data-ttu-id="2063c-118">以下是 hello 的摘錄，第一次 20 的資料行與此資料集中的兩個觀察 （資料列）：</span><span class="sxs-lookup"><span data-stu-id="2063c-118">Here is an excerpt of hello first 20 columns of two observations (rows) from this dataset:</span></span>

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

<span data-ttu-id="2063c-119">遺漏值中有兩個 hello 數值和分類資料行中此資料集。</span><span class="sxs-lookup"><span data-stu-id="2063c-119">There are missing values in both hello numeric and categorical columns in this dataset.</span></span> <span data-ttu-id="2063c-120">我們將描述來處理 hello 遺漏值的簡單方法。</span><span class="sxs-lookup"><span data-stu-id="2063c-120">We describe a simple method for handling hello missing values.</span></span> <span data-ttu-id="2063c-121">當我們將它們儲存成 Hive 資料表時，會探索 hello 資料的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2063c-121">Additional details of hello data are explored when we store them into Hive tables.</span></span>

<span data-ttu-id="2063c-122">**定義：** *點選率 (CTR):*這是 hello 百分比 hello 資料點選。</span><span class="sxs-lookup"><span data-stu-id="2063c-122">**Definition:** *Clickthrough rate (CTR):* This is hello percentage of clicks in hello data.</span></span> <span data-ttu-id="2063c-123">在此 Criteo 集中，hello CTR 的大約 3.3%或 0.033。</span><span class="sxs-lookup"><span data-stu-id="2063c-123">In this Criteo dataset, hello CTR is about 3.3% or 0.033.</span></span>

## <span data-ttu-id="2063c-124"><a name="mltasks"></a>預測工作的範例</span><span class="sxs-lookup"><span data-stu-id="2063c-124"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="2063c-125">本逐步解說將討論兩個範例預測問題：</span><span class="sxs-lookup"><span data-stu-id="2063c-125">Two sample prediction problems are addressed in this walkthrough:</span></span>

1. <span data-ttu-id="2063c-126">**二進位分類**：預測使用者是否按下加入：</span><span class="sxs-lookup"><span data-stu-id="2063c-126">**Binary classification**: Predicts whether a user clicked an add:</span></span>
   
   * <span data-ttu-id="2063c-127">類別 0：未按一下</span><span class="sxs-lookup"><span data-stu-id="2063c-127">Class 0: No Click</span></span>
   * <span data-ttu-id="2063c-128">類別 1：按一下</span><span class="sxs-lookup"><span data-stu-id="2063c-128">Class 1: Click</span></span>
2. <span data-ttu-id="2063c-129">**迴歸**： 從使用者特徵 ad 按一下 hello 機率的預測。</span><span class="sxs-lookup"><span data-stu-id="2063c-129">**Regression**: Predicts hello probability of an ad click from user features.</span></span>

## <span data-ttu-id="2063c-130"><a name="setup"></a>為資料科學設定 HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="2063c-130"><a name="setup"></a>Set Up an HDInsight Hadoop cluster for data science</span></span>
<span data-ttu-id="2063c-131">**附註：**這通常是**管理**工作。</span><span class="sxs-lookup"><span data-stu-id="2063c-131">**Note:** This is typically an **Admin** task.</span></span>

<span data-ttu-id="2063c-132">設定 Azure 資料科學環境，用於使用 HDInsight 叢集以三個步驟建置預測性的分析解決方案：</span><span class="sxs-lookup"><span data-stu-id="2063c-132">Set up your Azure Data Science environment for building predictive analytics solutions with HDInsight clusters in three steps:</span></span>

1. <span data-ttu-id="2063c-133">[建立儲存體帳戶](../storage/common/storage-create-storage-account.md)： 這個儲存體帳戶是 Azure Blob 儲存體使用的 toostore 資料。</span><span class="sxs-lookup"><span data-stu-id="2063c-133">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used toostore data in Azure Blob Storage.</span></span> <span data-ttu-id="2063c-134">用於 HDInsight 叢集的 hello 資料儲存在這裡。</span><span class="sxs-lookup"><span data-stu-id="2063c-134">hello data used in HDInsight clusters is stored here.</span></span>
2. <span data-ttu-id="2063c-135">[自訂適用於資料科學的 Azure HDInsight Hadoop 叢集](machine-learning-data-science-customize-hadoop-cluster.md)：這個步驟將會建立已在所有節點上安裝 64 位元 Anaconda Python 2.7 的 Azure HDInsight Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="2063c-135">[Customize Azure HDInsight Hadoop Clusters for Data Science](machine-learning-data-science-customize-hadoop-cluster.md): This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="2063c-136">自訂 hello HDInsight 叢集時，有兩個重要的步驟 （如本主題所述） toocomplete。</span><span class="sxs-lookup"><span data-stu-id="2063c-136">There are two important steps (described in this topic) toocomplete when customizing hello HDInsight cluster.</span></span>
   
   * <span data-ttu-id="2063c-137">您必須連結 hello 時就會建立在與 HDInsight 叢集的步驟 1 中建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2063c-137">You must link hello storage account created in step 1 with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="2063c-138">這個儲存體帳戶用來存取可處理 hello 叢集內的資料。</span><span class="sxs-lookup"><span data-stu-id="2063c-138">This storage account is used for accessing data that can be processed within hello cluster.</span></span>
   * <span data-ttu-id="2063c-139">在建立後，您必須啟用遠端存取 toohello 叢集前端節點 hello。</span><span class="sxs-lookup"><span data-stu-id="2063c-139">You must enable Remote Access toohello head node of hello cluster after it is created.</span></span> <span data-ttu-id="2063c-140">請記住您在此處指定 （不同於所指定的 hello 在其建立的叢集） hello 遠端存取認證： 需要 toocomplete hello 下列程序。</span><span class="sxs-lookup"><span data-stu-id="2063c-140">Remember hello remote access credentials you specify here (different from those specified for hello cluster at its creation): you need them toocomplete hello following procedures.</span></span>
3. <span data-ttu-id="2063c-141">[建立 Azure ML 工作區](machine-learning-create-workspace.md)： 此 Azure 機器學習工作區用來建立機器學習模型之後的初始資料瀏覽和向下 hello HDInsight 叢集上的取樣。</span><span class="sxs-lookup"><span data-stu-id="2063c-141">[Create an Azure ML workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used for building machine learning models after an initial data exploration and down sampling on hello HDInsight cluster.</span></span>

## <span data-ttu-id="2063c-142"><a name="getdata"></a>取得並從公用來源取用資料</span><span class="sxs-lookup"><span data-stu-id="2063c-142"><a name="getdata"></a>Get and consume data from a public source</span></span>
<span data-ttu-id="2063c-143">hello [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/)資料集可以透過按一下 hello 連結，接受 hello 使用條款，並提供名稱。</span><span class="sxs-lookup"><span data-stu-id="2063c-143">hello [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset can be accessed by clicking on hello link, accepting hello terms of use, and providing a name.</span></span> <span data-ttu-id="2063c-144">其外觀的快照如下所示：</span><span class="sxs-lookup"><span data-stu-id="2063c-144">A snapshot of what this looks like is shown here:</span></span>

![接受 Criteo 條款](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

<span data-ttu-id="2063c-146">按一下**繼續 tooDownload** tooread 更多關於 hello 資料集和其可用性。</span><span class="sxs-lookup"><span data-stu-id="2063c-146">Click **Continue tooDownload** tooread more about hello dataset and its availability.</span></span>

<span data-ttu-id="2063c-147">hello 資料常駐於公用中[Azure blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)位置： wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/。</span><span class="sxs-lookup"><span data-stu-id="2063c-147">hello data resides in a public [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) location: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span></span> <span data-ttu-id="2063c-148">hello"wasb 」 是指 tooAzure Blob 儲存體位置。</span><span class="sxs-lookup"><span data-stu-id="2063c-148">hello "wasb" refers tooAzure Blob Storage location.</span></span> 

1. <span data-ttu-id="2063c-149">這個公用 blob 儲存體中的 hello 資料所組成的解壓縮資料的三個子資料夾。</span><span class="sxs-lookup"><span data-stu-id="2063c-149">hello data in this public blob storage consists of three subfolders of unzipped data.</span></span>
   
   1. <span data-ttu-id="2063c-150">hello 子資料夾*原始/count/*包含 hello 第一次的 21 天的資料-從天\_00 tooday\_20</span><span class="sxs-lookup"><span data-stu-id="2063c-150">hello subfolder *raw/count/* contains hello first 21 days of data - from day\_00 tooday\_20</span></span>
   2. <span data-ttu-id="2063c-151">hello 子資料夾*原始/定型/*組成的資料，某一天一天\_21</span><span class="sxs-lookup"><span data-stu-id="2063c-151">hello subfolder *raw/train/* consists of a single day of data, day\_21</span></span>
   3. <span data-ttu-id="2063c-152">hello 子資料夾*原始/測試/*兩天的資料，包含日\_22 和日\_23</span><span class="sxs-lookup"><span data-stu-id="2063c-152">hello subfolder *raw/test/* consists of two days of data, day\_22 and day\_23</span></span>
2. <span data-ttu-id="2063c-153">人員想 toostart hello 原始 gzip 資料，這些是也可用在 hello 的主要資料夾*原始 /*為 day_NN.gz，從 00 too23 NN 的地方。</span><span class="sxs-lookup"><span data-stu-id="2063c-153">For those who want toostart with hello raw gzip data, these are also available in hello main folder *raw/* as day_NN.gz, where NN goes from 00 too23.</span></span>

<span data-ttu-id="2063c-154">替代方法 tooaccess，瀏覽及此不需要任何本機下載說明在此逐步解說稍後當我們建立 Hive 資料表的資料模型。</span><span class="sxs-lookup"><span data-stu-id="2063c-154">An alternative approach tooaccess, explore, and model this data that does not require any local downloads is explained later in this walkthrough when we create Hive tables.</span></span>

## <span data-ttu-id="2063c-155"><a name="login"></a>登入 toohello 叢集前端節點</span><span class="sxs-lookup"><span data-stu-id="2063c-155"><a name="login"></a>Log in toohello cluster headnode</span></span>
<span data-ttu-id="2063c-156">中的 hello 叢集中，使用 hello toohello 前端節點 toolog [Azure 入口網站](https://ms.portal.azure.com)toolocate hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="2063c-156">toolog in toohello headnode of hello cluster, use hello [Azure portal](https://ms.portal.azure.com) toolocate hello cluster.</span></span> <span data-ttu-id="2063c-157">按一下上剩餘的 hello hello HDInsight elephant 圖示，然後按兩下 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="2063c-157">Click hello HDInsight elephant icon on hello left and then double-click hello name of your cluster.</span></span> <span data-ttu-id="2063c-158">瀏覽 toohello**組態**索引標籤，按兩下 hello hello 頁面底部 hello 連接 圖示，然後輸入您的遠端存取認證出現提示時。</span><span class="sxs-lookup"><span data-stu-id="2063c-158">Navigate toohello **Configuration** tab, double-click hello CONNECT icon on hello bottom of hello page, and enter your remote access credentials when prompted.</span></span> <span data-ttu-id="2063c-159">這會帶您 toohello 的 hello 叢集的前端節點。</span><span class="sxs-lookup"><span data-stu-id="2063c-159">This takes you toohello headnode of hello cluster.</span></span>

<span data-ttu-id="2063c-160">以下是典型的第一個記錄檔中 toohello 叢集前端節點看起來像：</span><span class="sxs-lookup"><span data-stu-id="2063c-160">Here is what a typical first log in toohello cluster headnode looks like:</span></span>

![登入 toocluster](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

<span data-ttu-id="2063c-162">左側 hello，我們會看到 「 Hadoop 命令列 」，這是進行 hello 資料瀏覽我們 workhorse hello。</span><span class="sxs-lookup"><span data-stu-id="2063c-162">On hello left, we see hello "Hadoop Command Line", which is our workhorse for hello data exploration.</span></span> <span data-ttu-id="2063c-163">我們也會看到兩個實用的 URL - "Hadoop Yarn Status" 和 "Hadoop Name Node"。</span><span class="sxs-lookup"><span data-stu-id="2063c-163">We also see two useful URLs - "Hadoop Yarn Status" and "Hadoop Name Node".</span></span> <span data-ttu-id="2063c-164">hello yarn 狀態 URL 會顯示工作進度和 hello 名稱節點 URL 在 hello 叢集設定中提供詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2063c-164">hello yarn status URL shows job progress and hello name node URL gives details on hello cluster configuration.</span></span>

<span data-ttu-id="2063c-165">現在我們已設定，並準備 toobegin 第一部分 hello 逐步解說： 使用 Hive 和 Azure 機器學習準備資料的資料瀏覽。</span><span class="sxs-lookup"><span data-stu-id="2063c-165">Now we are set up and ready toobegin first part of hello walkthrough: data exploration using Hive and getting data ready for Azure Machine Learning.</span></span>

## <span data-ttu-id="2063c-166"><a name="hive-db-tables"></a> 建立 Hive 資料庫和資料表</span><span class="sxs-lookup"><span data-stu-id="2063c-166"><a name="hive-db-tables"></a> Create Hive database and tables</span></span>
<span data-ttu-id="2063c-167">toocreate Hive 資料表我們 Criteo 資料集，開啟 hello ***Hadoop 命令列***hello 桌面的 hello 前端節點，且輸入 hello 命令輸入 hello Hive 目錄</span><span class="sxs-lookup"><span data-stu-id="2063c-167">toocreate Hive tables for our Criteo dataset, open hello ***Hadoop Command Line*** on hello desktop of hello head node, and enter hello Hive directory by entering hello command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="2063c-168">在此逐步解說中執行所有的登錄區命令，從 hello Hive bin / 目錄提示字元。</span><span class="sxs-lookup"><span data-stu-id="2063c-168">Run all Hive commands in this walkthrough from hello Hive bin/ directory prompt.</span></span> <span data-ttu-id="2063c-169">如此可自動處理路徑相關問題。</span><span class="sxs-lookup"><span data-stu-id="2063c-169">This takes care of any path issues automatically.</span></span> <span data-ttu-id="2063c-170">我們使用 hello 詞彙"Hive 目錄 prompt"，"Hive bin / 目錄提示字元 」，和 「 Hadoop 命令列 」 交換使用。</span><span class="sxs-lookup"><span data-stu-id="2063c-170">We use hello terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop Command Line" interchangeably.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="2063c-171">tooexecute 任何 Hive 查詢，其中一個永遠都可以使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="2063c-171">tooexecute any Hive query, one can always use hello following commands:</span></span>
> 
> 

        cd %hive_home%\bin
        hive

<span data-ttu-id="2063c-172">Hello Hive REPL 就會出現與 「 hive > 」 登入，只需剪下和貼上 hello 查詢 tooexecute 它。</span><span class="sxs-lookup"><span data-stu-id="2063c-172">After hello Hive REPL appears with a "hive >"sign, simply cut and paste hello query tooexecute it.</span></span>

<span data-ttu-id="2063c-173">hello 下列程式碼建立資料庫 「 criteo 」，並接著會產生 4 資料表：</span><span class="sxs-lookup"><span data-stu-id="2063c-173">hello following code creates a database "criteo" and then generates 4 tables:</span></span>

* <span data-ttu-id="2063c-174">*資料表來產生計數*天天內建\_00 tooday\_20，</span><span class="sxs-lookup"><span data-stu-id="2063c-174">a *table for generating counts* built on days day\_00 tooday\_20,</span></span>
* <span data-ttu-id="2063c-175">*hello 定型資料集資料表用於*建置當天\_21，和</span><span class="sxs-lookup"><span data-stu-id="2063c-175">a *table for use as hello train dataset* built on day\_21, and</span></span>
* <span data-ttu-id="2063c-176">兩個*資料表 hello 做測試資料集*建置當天\_22 和日\_23 分別。</span><span class="sxs-lookup"><span data-stu-id="2063c-176">two *tables for use as hello test datasets* built on day\_22 and day\_23 respectively.</span></span>

<span data-ttu-id="2063c-177">因為其中一個 hello 天為假日中，而且我們想 toodetermine 如果 hello 模型可以偵測到差異假日和非假日 hello 點選連結速度，我們可以分割成兩個不同資料表的我們的測試資料集。</span><span class="sxs-lookup"><span data-stu-id="2063c-177">We split our test dataset into two different tables because one of hello days is a holiday, and we want toodetermine if hello model can detect differences between a holiday and non-holiday from hello clickthrough rate.</span></span>

<span data-ttu-id="2063c-178">hello 指令碼[範例 &#95; hive &#95; 建立 （& s) #95; criteo &#95; 資料庫 &#95; 和 &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)此處會顯示為方便起見：</span><span class="sxs-lookup"><span data-stu-id="2063c-178">hello script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) is displayed here for convenience:</span></span>

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

<span data-ttu-id="2063c-179">我們請注意，所有這些資料表是我們只要點 tooAzure Blob 儲存體 (wasb) 的位置做為外部。</span><span class="sxs-lookup"><span data-stu-id="2063c-179">We note that all these tables are external as we simply point tooAzure Blob Storage (wasb) locations.</span></span>

<span data-ttu-id="2063c-180">**有兩種方式 tooexecute ANY Hive 查詢現在提到。**</span><span class="sxs-lookup"><span data-stu-id="2063c-180">**There are two ways tooexecute ANY Hive query that we now mention.**</span></span>

1. <span data-ttu-id="2063c-181">**使用 hello Hive REPL 命令列**: hello 第一次是 tooissue"hive"命令並複製和貼上在 hello Hive REPL 命令列的查詢。</span><span class="sxs-lookup"><span data-stu-id="2063c-181">**Using hello Hive REPL command-line**: hello first is tooissue a "hive" command and copy and paste a query at hello Hive REPL command-line.</span></span> <span data-ttu-id="2063c-182">toodo 此，請執行：</span><span class="sxs-lookup"><span data-stu-id="2063c-182">toodo this, do:</span></span>
   
        cd %hive_home%\bin
        hive
   
     <span data-ttu-id="2063c-183">現在 hello REPL 命令列，在剪下和貼上 hello 查詢會執行它。</span><span class="sxs-lookup"><span data-stu-id="2063c-183">Now at hello REPL command-line, cutting and pasting hello query executes it.</span></span>
2. <span data-ttu-id="2063c-184">**儲存查詢 tooa 檔案以及執行 hello 命令**: hello 第二種是 toosave hello 查詢 tooa.hql 檔案 ([範例 &#95; hive &#95; 建立 （& s) #95; criteo &#95; 資料庫 &#95; 和 &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) 和問題 hello 下列然後命令 tooexecute hello 查詢：</span><span class="sxs-lookup"><span data-stu-id="2063c-184">**Saving queries tooa file and executing hello command**: hello second is toosave hello queries tooa .hql file ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) and then issue hello following command tooexecute hello query:</span></span>
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a><span data-ttu-id="2063c-185">確認資料庫和資料表的建立</span><span class="sxs-lookup"><span data-stu-id="2063c-185">Confirm database and table creation</span></span>
<span data-ttu-id="2063c-186">接下來，我們以 hello hello Hive 紙匣中的下列命令確認 hello 建立 hello 資料庫 / 目錄提示：</span><span class="sxs-lookup"><span data-stu-id="2063c-186">Next, we confirm hello creation of hello database with hello following command from hello Hive bin/ directory prompt:</span></span>

        hive -e "show databases;"

<span data-ttu-id="2063c-187">這會提供：</span><span class="sxs-lookup"><span data-stu-id="2063c-187">This gives:</span></span>

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

<span data-ttu-id="2063c-188">這可確認 hello 建立 hello 新資料庫，"criteo"。</span><span class="sxs-lookup"><span data-stu-id="2063c-188">This confirms hello creation of hello new database, "criteo".</span></span>

<span data-ttu-id="2063c-189">toosee 資料表建立，我們只是發出 hello 命令這裡 hello Hive 紙匣 / 目錄提示：</span><span class="sxs-lookup"><span data-stu-id="2063c-189">toosee what tables we created, we simply issue hello command here from hello Hive bin/ directory prompt:</span></span>

        hive -e "show tables in criteo;"

<span data-ttu-id="2063c-190">然後，我們會看到 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="2063c-190">We then see hello following output:</span></span>

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <span data-ttu-id="2063c-191"><a name="exploration"></a> 在 Hive 中的資料瀏覽</span><span class="sxs-lookup"><span data-stu-id="2063c-191"><a name="exploration"></a> Data exploration in Hive</span></span>
<span data-ttu-id="2063c-192">現在我們已備妥 toodo 登錄區中的一些基本的資料瀏覽。</span><span class="sxs-lookup"><span data-stu-id="2063c-192">Now we are ready toodo some basic data exploration in Hive.</span></span> <span data-ttu-id="2063c-193">我們透過計算 hello 數目 hello 定型中的範例開頭，而且測試資料的資料表。</span><span class="sxs-lookup"><span data-stu-id="2063c-193">We begin by counting hello number of examples in hello train and test data tables.</span></span>

### <a name="number-of-train-examples"></a><span data-ttu-id="2063c-194">訓練範例的數目</span><span class="sxs-lookup"><span data-stu-id="2063c-194">Number of train examples</span></span>
<span data-ttu-id="2063c-195">hello 內容[範例 &#95; hive #95 計數 &#95; 定型 &#95; 資料表 &; #95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql)如下所示：</span><span class="sxs-lookup"><span data-stu-id="2063c-195">hello contents of [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) are shown here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_train;

<span data-ttu-id="2063c-196">這會產生：</span><span class="sxs-lookup"><span data-stu-id="2063c-196">This yields:</span></span>

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

<span data-ttu-id="2063c-197">或者，其中也可能會發出 hello hello Hive 紙匣中的下列命令 / 目錄提示：</span><span class="sxs-lookup"><span data-stu-id="2063c-197">Alternatively, one may also issue hello following command from hello Hive bin/ directory prompt:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-hello-two-test-datasets"></a><span data-ttu-id="2063c-198">測試中的範例數目 hello 兩個測試資料集</span><span class="sxs-lookup"><span data-stu-id="2063c-198">Number of test examples in hello two test datasets</span></span>
<span data-ttu-id="2063c-199">我們現在計數 hello 的 hello 兩個測試資料集的範例。</span><span class="sxs-lookup"><span data-stu-id="2063c-199">We now count hello number of examples in hello two test datasets.</span></span> <span data-ttu-id="2063c-200">hello 內容[範例 &#95; hive &#95; 計數 &#95; criteo &#95; 測試 &#95; 天 &#95; 22 &#95; 資料表 &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql)這裡：</span><span class="sxs-lookup"><span data-stu-id="2063c-200">hello contents of [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) are here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

<span data-ttu-id="2063c-201">這會產生：</span><span class="sxs-lookup"><span data-stu-id="2063c-201">This yields:</span></span>

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

<span data-ttu-id="2063c-202">像往常一樣，我們也可呼叫 hello 指令碼從 hello Hive bin / 目錄發出 hello 命令提示字元：</span><span class="sxs-lookup"><span data-stu-id="2063c-202">As usual, we may also call hello script from hello Hive bin/ directory prompt by issuing hello command:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

<span data-ttu-id="2063c-203">最後，我們檢驗 hello 測試中的範例數目依據一天的 hello 測試資料集\_23。</span><span class="sxs-lookup"><span data-stu-id="2063c-203">Finally, we examine hello number of test examples in hello test dataset based on day\_23.</span></span>

<span data-ttu-id="2063c-204">hello 命令 toodo 這是只顯示一個類似 toohello (請參閱太[範例 &#95; hive #95 計數 &#95; criteo &#95; 測試 &#95; 天 &#95; 23 &; #95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span><span class="sxs-lookup"><span data-stu-id="2063c-204">hello command toodo this is similar toohello one just shown (refer too[sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

<span data-ttu-id="2063c-205">這會提供：</span><span class="sxs-lookup"><span data-stu-id="2063c-205">This gives:</span></span>

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-hello-train-dataset"></a><span data-ttu-id="2063c-206">Hello 定型資料集內的標籤發佈</span><span class="sxs-lookup"><span data-stu-id="2063c-206">Label distribution in hello train dataset</span></span>
<span data-ttu-id="2063c-207">hello 定型資料集中的 hello 標籤分佈是感興趣。</span><span class="sxs-lookup"><span data-stu-id="2063c-207">hello label distribution in hello train dataset is of interest.</span></span> <span data-ttu-id="2063c-208">toosee，我們顯示的內容[範例 &#95; hive #95 criteo &#95; 標籤 &#95; 散發 &#95; 定型 &; #95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span><span class="sxs-lookup"><span data-stu-id="2063c-208">toosee this, we show contents of [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span></span>

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

<span data-ttu-id="2063c-209">這會產生 hello 標籤發佈：</span><span class="sxs-lookup"><span data-stu-id="2063c-209">This yields hello label distribution:</span></span>

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

<span data-ttu-id="2063c-210">請注意 hello 正面標籤的百分比，大約是 3.3%（與 hello 原始資料集一致）。</span><span class="sxs-lookup"><span data-stu-id="2063c-210">Note that hello percentage of positive labels is about 3.3% (consistent with hello original dataset).</span></span>

### <a name="histogram-distributions-of-some-numeric-variables-in-hello-train-dataset"></a><span data-ttu-id="2063c-211">長條圖分佈在 hello 部分數值變數的定型資料集</span><span class="sxs-lookup"><span data-stu-id="2063c-211">Histogram distributions of some numeric variables in hello train dataset</span></span>
<span data-ttu-id="2063c-212">我們可以使用 Hive 的原生 「 長條圖\_數值"toofind 出 hello 數值變數哪些 hello 分佈看起來像函式。</span><span class="sxs-lookup"><span data-stu-id="2063c-212">We can use Hive's native "histogram\_numeric" function toofind out what hello distribution of hello numeric variables looks like.</span></span> <span data-ttu-id="2063c-213">以下是 hello 內容[範例 &#95; hive #95 criteo &#95; 長條圖 &; #95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span><span class="sxs-lookup"><span data-stu-id="2063c-213">Here are hello contents of [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span></span>

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

<span data-ttu-id="2063c-214">這會產生下列 hello:</span><span class="sxs-lookup"><span data-stu-id="2063c-214">This yields hello following:</span></span>

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

<span data-ttu-id="2063c-215">hello 側檢視-分裂 Hive 做 tooproduce 是類似 SQL 的輸出，而不是 hello 一般清單中的組合。</span><span class="sxs-lookup"><span data-stu-id="2063c-215">hello LATERAL VIEW - explode combination in Hive serves tooproduce a SQL-like output instead of hello usual list.</span></span> <span data-ttu-id="2063c-216">請注意，在 hello 這個資料表，hello 第一個資料行對應 toohello bin 置中與 hello 第二個 toohello bin 頻率。</span><span class="sxs-lookup"><span data-stu-id="2063c-216">Note that in hello this table, hello first column corresponds toohello bin center and hello second toohello bin frequency.</span></span>

### <a name="approximate-percentiles-of-some-numeric-variables-in-hello-train-dataset"></a><span data-ttu-id="2063c-217">大約百分位數 hello 中部分數值變數的定型資料集</span><span class="sxs-lookup"><span data-stu-id="2063c-217">Approximate percentiles of some numeric variables in hello train dataset</span></span>
<span data-ttu-id="2063c-218">也與數值變數的感興趣的是 hello 計算的近似百分比也一樣。</span><span class="sxs-lookup"><span data-stu-id="2063c-218">Also of interest with numeric variables is hello computation of approximate percentiles.</span></span> <span data-ttu-id="2063c-219">Hive 的原生 "percentile\_approx" 會為我們執行此動作。</span><span class="sxs-lookup"><span data-stu-id="2063c-219">Hive's native "percentile\_approx" does this for us.</span></span> <span data-ttu-id="2063c-220">hello 內容[範例 &#95; hive &#95; criteo &#95; 相近 &#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql)是：</span><span class="sxs-lookup"><span data-stu-id="2063c-220">hello contents of [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) are:</span></span>

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

<span data-ttu-id="2063c-221">這會產生：</span><span class="sxs-lookup"><span data-stu-id="2063c-221">This yields:</span></span>

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

<span data-ttu-id="2063c-222">我們在每 hello 依百分位數分佈通常是密切相關的 toohello 長條圖任何的散發數值變數。</span><span class="sxs-lookup"><span data-stu-id="2063c-222">We remark that hello distribution of percentiles is closely related toohello histogram distribution of any numeric variable usually.</span></span>         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-hello-train-dataset"></a><span data-ttu-id="2063c-223">尋找 hello 定型資料集中的某些類別資料行的唯一值數目</span><span class="sxs-lookup"><span data-stu-id="2063c-223">Find number of unique values for some categorical columns in hello train dataset</span></span>
<span data-ttu-id="2063c-224">延續 hello 資料瀏覽，我們現在發現某些類別的資料行，則會接受的唯一值的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="2063c-224">Continuing hello data exploration, we now find, for some categorical columns, hello number of unique values they take.</span></span> <span data-ttu-id="2063c-225">toodo，我們顯示的內容[範例 &#95; hive &#95; criteo &#95; 唯一 &#95; 值 &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span><span class="sxs-lookup"><span data-stu-id="2063c-225">toodo this, we show contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span></span>

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

<span data-ttu-id="2063c-226">這會產生：</span><span class="sxs-lookup"><span data-stu-id="2063c-226">This yields:</span></span>

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

<span data-ttu-id="2063c-227">我們注意到 Col15 有 1900 萬個唯一值！</span><span class="sxs-lookup"><span data-stu-id="2063c-227">We note that Col15 has 19M unique values!</span></span> <span data-ttu-id="2063c-228">使用貝氏技術，如 「 一個熱編碼 」 tooencode 這類高維度的類別變數並不可行。</span><span class="sxs-lookup"><span data-stu-id="2063c-228">Using naive techniques like "one-hot encoding" tooencode such high-dimensional categorical variables is infeasible.</span></span> <span data-ttu-id="2063c-229">特別是，我們將說明並示範稱為 [以計數學習](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) 功能強大又穩健的技術，以有效率地解決此問題。</span><span class="sxs-lookup"><span data-stu-id="2063c-229">In particular, we explain and demonstrate a powerful, robust technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) for tackling this problem efficiently.</span></span>

<span data-ttu-id="2063c-230">我們來結束此子區段查看 hello 的一些其他的類別資料行以及唯一值數目。</span><span class="sxs-lookup"><span data-stu-id="2063c-230">We end this sub-section by looking at hello number of unique values for some other categorical columns as well.</span></span> <span data-ttu-id="2063c-231">hello 內容[範例 &#95; hive &#95; criteo &#95; 唯一 &#95; 值 &#95; 多個 （& s) #95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql)會：</span><span class="sxs-lookup"><span data-stu-id="2063c-231">hello contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) are:</span></span>

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

<span data-ttu-id="2063c-232">這會產生：</span><span class="sxs-lookup"><span data-stu-id="2063c-232">This yields:</span></span>

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

<span data-ttu-id="2063c-233">同樣地我們看到，除了第 20 欄，所有 hello 其他資料行有多個唯一值。</span><span class="sxs-lookup"><span data-stu-id="2063c-233">Again we see that except for Col20, all hello other columns have many unique values.</span></span>

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-hello-train-dataset"></a><span data-ttu-id="2063c-234">成對的 hello 定型資料集中的類別變數的共同的發生次數</span><span class="sxs-lookup"><span data-stu-id="2063c-234">Co-occurrence counts of pairs of categorical variables in hello train dataset</span></span>

<span data-ttu-id="2063c-235">hello 共同的發生次數的類別變數配對也是感興趣。</span><span class="sxs-lookup"><span data-stu-id="2063c-235">hello co-occurrence counts of pairs of categorical variables is also of interest.</span></span> <span data-ttu-id="2063c-236">這可以使用中的 hello 程式碼來決定[範例 &#95; hive &#95; criteo &#95; 配對 &#95; 類別 （& s) #95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span><span class="sxs-lookup"><span data-stu-id="2063c-236">This can be determined using hello code in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span></span>

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

<span data-ttu-id="2063c-237">我們反向順序 hello 計數所發生的情形，並在此情況下查看 hello 前 15。</span><span class="sxs-lookup"><span data-stu-id="2063c-237">We reverse order hello counts by their occurrence and look at hello top 15 in this case.</span></span> <span data-ttu-id="2063c-238">這會提供：</span><span class="sxs-lookup"><span data-stu-id="2063c-238">This gives us:</span></span>

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

## <span data-ttu-id="2063c-239"><a name="downsample"></a>向 Azure 機器學習範例 hello 資料集</span><span class="sxs-lookup"><span data-stu-id="2063c-239"><a name="downsample"></a> Down sample hello datasets for Azure Machine Learning</span></span>
<span data-ttu-id="2063c-240">擁有已探索的 hello 資料集，並示範如何我們可能會執行這種類型的任何變數 （包括組合），我們現在關閉取樣 hello 資料集探索，讓我們可以建立 Azure Machine Learning 中的模型。</span><span class="sxs-lookup"><span data-stu-id="2063c-240">Having explored hello datasets and demonstrated how we may do this type of exploration for any variables (including combinations), we now down sample hello data sets so that we can build models in Azure Machine Learning.</span></span> <span data-ttu-id="2063c-241">請記住，我們著重在該 hello 問題是： 提供一組範例屬性 （從 Col2-Col40 功能值），我們的預測是否 Col1 是 0 （沒有按一下） 或 1 （按一下）。</span><span class="sxs-lookup"><span data-stu-id="2063c-241">Recall that hello problem we focus on is: given a set of example attributes (feature values from Col2 - Col40), we predict if Col1 is a 0 (no click) or a 1 (click).</span></span>

<span data-ttu-id="2063c-242">toodown 範例我們定型和測試資料集 too1 %hello 原始大小，我們使用 Hive 的原生 rand （） 函式。</span><span class="sxs-lookup"><span data-stu-id="2063c-242">toodown sample our train and test datasets too1% of hello original size, we use Hive's native RAND() function.</span></span> <span data-ttu-id="2063c-243">hello 下一個指令碼，[範例 &#95; hive &#95; criteo & #95，可以 #95 定型 &; #95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql)做法 hello 定型資料集：</span><span class="sxs-lookup"><span data-stu-id="2063c-243">hello next script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) does this for hello train dataset:</span></span>

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

<span data-ttu-id="2063c-244">這會產生：</span><span class="sxs-lookup"><span data-stu-id="2063c-244">This yields:</span></span>

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

<span data-ttu-id="2063c-245">hello 指令碼[範例 &#95; hive &#95; criteo & #95，可以 #95 測試 &#95; 天 &#95; 22 &; #95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql)會測試資料，為一天\_22:</span><span class="sxs-lookup"><span data-stu-id="2063c-245">hello script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) does it for test data, day\_22:</span></span>

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

<span data-ttu-id="2063c-246">這會產生：</span><span class="sxs-lookup"><span data-stu-id="2063c-246">This yields:</span></span>

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


<span data-ttu-id="2063c-247">最後，hello 指令碼[範例 &#95; hive &#95; criteo & #95，可以 #95 測試 &#95; 天 &#95; 23 &; #95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql)會測試資料，為一天\_23:</span><span class="sxs-lookup"><span data-stu-id="2063c-247">Finally, hello script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) does it for test data, day\_23:</span></span>

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

<span data-ttu-id="2063c-248">這會產生：</span><span class="sxs-lookup"><span data-stu-id="2063c-248">This yields:</span></span>

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

<span data-ttu-id="2063c-249">與這個項目，我們會準備 toouse 我們向下取樣定型和測試資料集來建立 Azure Machine Learning 中的模型。</span><span class="sxs-lookup"><span data-stu-id="2063c-249">With this, we are ready toouse our down sampled train and test datasets for building models in Azure Machine Learning.</span></span>

<span data-ttu-id="2063c-250">我們將在 tooAzure Machine Learning 中，也就是考量 hello 計數資料表之前，會最後的重要元件。</span><span class="sxs-lookup"><span data-stu-id="2063c-250">There is a final important component before we move on tooAzure Machine Learning, which is concerns hello count table.</span></span> <span data-ttu-id="2063c-251">在 hello 下一步 子區段中，我們將在討論一些詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2063c-251">In hello next sub-section, we discuss this in some detail.</span></span>

## <span data-ttu-id="2063c-252"><a name="count"></a>Hello 計數資料表上的簡短討論</span><span class="sxs-lookup"><span data-stu-id="2063c-252"><a name="count"></a> A brief discussion on hello count table</span></span>
<span data-ttu-id="2063c-253">如我們所見，數個類別變數有極高的維度性。</span><span class="sxs-lookup"><span data-stu-id="2063c-253">As we saw, several categorical variables have a very high dimensionality.</span></span> <span data-ttu-id="2063c-254">在我們的逐步解說中，我們提供功能強大的技術稱為[學習與計算](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx)tooencode 這些變數，以有效率、 強固的方式。</span><span class="sxs-lookup"><span data-stu-id="2063c-254">In our walkthrough, we present a powerful technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode these variables in an efficient, robust manner.</span></span> <span data-ttu-id="2063c-255">在這項技術的詳細資訊是中提供的 hello 連結。</span><span class="sxs-lookup"><span data-stu-id="2063c-255">More information on this technique is in hello link provided.</span></span>

[!NOTE]
><span data-ttu-id="2063c-256">在此逐步解說中，我們會著重在使用的高維度的類別特徵的計數資料表 tooproduce compact 表示。</span><span class="sxs-lookup"><span data-stu-id="2063c-256">In this walkthrough, we focus on using count tables tooproduce compact representations of high-dimensional categorical features.</span></span> <span data-ttu-id="2063c-257">這不是 hello 方式 tooencode 類別的功能。如需其他技術的詳細資訊，想要的使用者可以簽出[一個熱-編碼](http://en.wikipedia.org/wiki/One-hot)和[特徵雜湊](http://en.wikipedia.org/wiki/Feature_hashing)。</span><span class="sxs-lookup"><span data-stu-id="2063c-257">This is not hello only way tooencode categorical features; for more information on other techniques, interested users can check out [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) and [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span></span>
>

<span data-ttu-id="2063c-258">toobuild hello 計數的資料計數資料表，我們會使用 hello 資料 hello 資料夾原始/計數中。</span><span class="sxs-lookup"><span data-stu-id="2063c-258">toobuild count tables on hello count data, we use hello data in hello folder raw/count.</span></span> <span data-ttu-id="2063c-259">在模型化 區段中，我們對使用者顯示 hello 如何 toobuild 這些函數會計算資料表從從頭開始或者 toouse 類別特徵其瀏覽的預先建置的計數資料表。</span><span class="sxs-lookup"><span data-stu-id="2063c-259">In hello modeling section, we show users how toobuild these count tables for categorical features from scratch, or alternatively toouse a pre-built count table for their explorations.</span></span> <span data-ttu-id="2063c-260">在如下所示，當我們太 「 預先建置計數資料表 」，是指使用 hello 我們提供的計數資料表。</span><span class="sxs-lookup"><span data-stu-id="2063c-260">In what follows, when we refer too"pre-built count tables", we mean using hello count tables that we provide.</span></span> <span data-ttu-id="2063c-261">取得如何 tooaccess 這些資料表提供 hello 下一節中的詳細的指示。</span><span class="sxs-lookup"><span data-stu-id="2063c-261">Detailed instructions on how tooaccess these tables are provided in hello next section.</span></span>

## <span data-ttu-id="2063c-262"><a name="aml"></a> 使用 Azure Machine Learning 建置模型</span><span class="sxs-lookup"><span data-stu-id="2063c-262"><a name="aml"></a> Build a model with Azure Machine Learning</span></span>
<span data-ttu-id="2063c-263">在 Azure Machine Learning 建置模型的程序遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2063c-263">Our model building process in Azure Machine Learning follows these steps:</span></span>

1. [<span data-ttu-id="2063c-264">Hive 資料表中的 hello 資料送入 Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2063c-264">Get hello data from Hive tables into Azure Machine Learning</span></span>](#step1)
2. [<span data-ttu-id="2063c-265">建立 hello 實驗： 清除 hello 資料和特徵化的計數資料表</span><span class="sxs-lookup"><span data-stu-id="2063c-265">Create hello experiment: clean hello data and featurize with count tables</span></span>](#step2)
3. [<span data-ttu-id="2063c-266">建置、 火車和分數 hello 模型</span><span class="sxs-lookup"><span data-stu-id="2063c-266">Build, train, and score hello model</span></span>](#step3)
4. [<span data-ttu-id="2063c-267">評估 hello 模型</span><span class="sxs-lookup"><span data-stu-id="2063c-267">Evaluate hello model</span></span>](#step4)
5. [<span data-ttu-id="2063c-268">Hello 模型發佈為 web 服務</span><span class="sxs-lookup"><span data-stu-id="2063c-268">Publish hello model as a web-service</span></span>](#step5)

<span data-ttu-id="2063c-269">現在我們已經準備好 toobuild Azure Machine Learning studio 中的模型。</span><span class="sxs-lookup"><span data-stu-id="2063c-269">Now we are ready toobuild models in Azure Machine Learning studio.</span></span> <span data-ttu-id="2063c-270">我們向下取樣的資料會儲存為 hello 叢集中的 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="2063c-270">Our down sampled data is saved as Hive tables in hello cluster.</span></span> <span data-ttu-id="2063c-271">我們使用 Azure Machine Learning hello**匯入資料**模組 tooread 這項資料。</span><span class="sxs-lookup"><span data-stu-id="2063c-271">We use hello Azure Machine Learning **Import Data** module tooread this data.</span></span> <span data-ttu-id="2063c-272">hello 認證 tooaccess hello 儲存體帳戶的此叢集提供哪些如下所示。</span><span class="sxs-lookup"><span data-stu-id="2063c-272">hello credentials tooaccess hello storage account of this cluster are provided in what follows.</span></span>

### <span data-ttu-id="2063c-273"><a name="step1"></a>步驟 1： 從 Hive 資料表取得資料，放入 Azure 機器學習使用 hello 資料匯入模組，並選取的機器學習實驗</span><span class="sxs-lookup"><span data-stu-id="2063c-273"><a name="step1"></a> Step 1: Get data from Hive tables into Azure Machine Learning using hello Import Data module and select it for a machine learning experiment</span></span>
<span data-ttu-id="2063c-274">藉由選取 [+ 新增] -> [實驗] -> [空白實驗] 開始。</span><span class="sxs-lookup"><span data-stu-id="2063c-274">Start by selecting a **+NEW** -> **EXPERIMENT** -> **Blank Experiment**.</span></span> <span data-ttu-id="2063c-275">然後，從 hello**搜尋**hello 左上方，「 匯入資料 」 的搜尋 方塊。</span><span class="sxs-lookup"><span data-stu-id="2063c-275">Then, from hello **Search** box on hello top left, search for "Import Data".</span></span> <span data-ttu-id="2063c-276">拖放 hello**匯入資料**toohello 實驗畫布 （hello 中間部分囉 」 畫面） toouse hello 模組上存取資料的模組。</span><span class="sxs-lookup"><span data-stu-id="2063c-276">Drag and drop hello **Import Data** module on toohello experiment canvas (hello middle portion of hello screen) toouse hello module for data access.</span></span>

<span data-ttu-id="2063c-277">這是什麼 hello**匯入資料**從 hello Hive 資料表取得資料時看起來像：</span><span class="sxs-lookup"><span data-stu-id="2063c-277">This is what hello **Import Data** looks like while getting data from hello Hive table:</span></span>

![「匯入資料」取得資料](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

<span data-ttu-id="2063c-279">Hello**匯入資料**模組，提供在 hello 圖形都只是範例的 hello 排序值的 hello 參數 hello 值需要 tooprovide。</span><span class="sxs-lookup"><span data-stu-id="2063c-279">For hello **Import Data** module, hello values of hello parameters that are provided in hello graphic are just examples of hello sort of values you need tooprovide.</span></span> <span data-ttu-id="2063c-280">以下是一些一般指導方針 hello toofill out hello 參數的設定方式**匯入資料**模組。</span><span class="sxs-lookup"><span data-stu-id="2063c-280">Here is some general guidance on how toofill out hello parameter set for hello **Import Data** module.</span></span>

1. <span data-ttu-id="2063c-281">對 **資料來源**</span><span class="sxs-lookup"><span data-stu-id="2063c-281">Choose "Hive query" for **Data Source**</span></span>
2. <span data-ttu-id="2063c-282">在 hello **Hive 資料庫查詢**方塊中，簡單的 SELECT * FROM < 您\_資料庫\_name.your\_資料表\_名稱 >-即已足夠。</span><span class="sxs-lookup"><span data-stu-id="2063c-282">In hello **Hive database query** box, a simple SELECT * FROM <your\_database\_name.your\_table\_name> - is enough.</span></span>
3. <span data-ttu-id="2063c-283">**Hcatalog 伺服器 URI**：如果您的叢集是 "abc"，那麼這就是：https://abc.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="2063c-283">**Hcatalog server URI**: If your cluster is "abc", then this is simply: https://abc.azurehdinsight.net</span></span>
4. <span data-ttu-id="2063c-284">**Hadoop 使用者帳戶名稱**: hello 的 commissioning hello 叢集 hello 次選擇的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="2063c-284">**Hadoop user account name**: hello user name chosen at hello time of commissioning hello cluster.</span></span> <span data-ttu-id="2063c-285">（非 hello 遠端存取使用者名稱 ！）</span><span class="sxs-lookup"><span data-stu-id="2063c-285">(NOT hello Remote Access user name!)</span></span>
5. <span data-ttu-id="2063c-286">**Hadoop 使用者帳戶密碼**: hello 選擇時的 commissioning hello 叢集 hello hello 使用者名稱密碼。</span><span class="sxs-lookup"><span data-stu-id="2063c-286">**Hadoop user account password**: hello password for hello user name chosen at hello time of commissioning hello cluster.</span></span> <span data-ttu-id="2063c-287">（不 hello 遠端存取密碼 ！）</span><span class="sxs-lookup"><span data-stu-id="2063c-287">(NOT hello Remote Access password!)</span></span>
6. <span data-ttu-id="2063c-288">**輸出資料的位置**：選擇 "Azure"</span><span class="sxs-lookup"><span data-stu-id="2063c-288">**Location of output data**: Choose "Azure"</span></span>
7. <span data-ttu-id="2063c-289">**Azure 儲存體帳戶名稱**: hello 與 hello 叢集相關聯的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="2063c-289">**Azure storage account name**: hello storage account associated with hello cluster</span></span>
8. <span data-ttu-id="2063c-290">**Azure 儲存體帳戶金鑰**: hello 與 hello 叢集相關聯的 hello 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="2063c-290">**Azure storage account key**: hello key of hello storage account associated with hello cluster.</span></span>
9. <span data-ttu-id="2063c-291">**Azure 容器名稱**： 如果 hello 叢集名稱為"abc"，則這通常是只是"abc，"。</span><span class="sxs-lookup"><span data-stu-id="2063c-291">**Azure container name**: If hello cluster name is "abc", then this is simply "abc", usually.</span></span>

<span data-ttu-id="2063c-292">一次 hello**匯入資料**完成取得的資料 （您將看到在 hello 模組 hello 綠色勾號），將此資料儲存為資料集 （與您選擇的名稱）。</span><span class="sxs-lookup"><span data-stu-id="2063c-292">Once hello **Import Data** finishes getting data (you see hello green tick on hello Module), save this data as a Dataset (with a name of your choice).</span></span> <span data-ttu-id="2063c-293">看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="2063c-293">What this looks like:</span></span>

![「匯入資料」儲存資料](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

<span data-ttu-id="2063c-295">以滑鼠右鍵按一下 hello 輸出連接埠的 hello**匯入資料**模組。</span><span class="sxs-lookup"><span data-stu-id="2063c-295">Right-click hello output port of hello **Import Data** module.</span></span> <span data-ttu-id="2063c-296">這會顯示 [另存為資料集] 選項和 [視覺化] 選項。</span><span class="sxs-lookup"><span data-stu-id="2063c-296">This reveals a **Save as dataset** option and a **Visualize** option.</span></span> <span data-ttu-id="2063c-297">hello**視覺化**選項，如果按下，會顯示 hello 的資料，以及適用於某些摘要統計資料的右方面板的 100 個資料列。</span><span class="sxs-lookup"><span data-stu-id="2063c-297">hello **Visualize** option, if clicked, displays 100 rows of hello data, along with a right panel that is useful for some summary statistics.</span></span> <span data-ttu-id="2063c-298">toosave 資料，只需選取**將儲存為資料集**並遵循指示。</span><span class="sxs-lookup"><span data-stu-id="2063c-298">toosave data, simply select **Save as dataset** and follow instructions.</span></span>

<span data-ttu-id="2063c-299">tooselect hello 儲存的資料集以用於機器學習實驗中，找出 hello 資料集使用 hello**搜尋**hello 遵循圖所示的方塊。</span><span class="sxs-lookup"><span data-stu-id="2063c-299">tooselect hello saved dataset for use in a machine learning experiment, locate hello datasets using hello **Search** box shown in hello following figure.</span></span> <span data-ttu-id="2063c-300">然後只輸入出 hello 名稱指定給 hello 資料集部分並拖曳 hello 資料集拖曳至 tooaccess hello 主面板。</span><span class="sxs-lookup"><span data-stu-id="2063c-300">Then simply type out hello name you gave hello dataset partially tooaccess it and drag hello dataset onto hello main panel.</span></span> <span data-ttu-id="2063c-301">拖曳 hello 主要面板選取用於機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="2063c-301">Dropping it onto hello main panel selects it for use in machine learning modeling.</span></span>

![拖曳到 hello 主要面板的資料集](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> <span data-ttu-id="2063c-303">Hello 定型和 hello 測試資料集執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="2063c-303">Do this for both hello train and hello test datasets.</span></span> <span data-ttu-id="2063c-304">此外，請記得 toouse hello 資料庫名稱和您針對此目的所提供的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="2063c-304">Also, remember toouse hello database name and table names that you gave for this purpose.</span></span> <span data-ttu-id="2063c-305">hello 圖中所使用的 hello 值是僅供圖 purposes.* *</span><span class="sxs-lookup"><span data-stu-id="2063c-305">hello values used in hello figure are solely for illustration purposes.**</span></span>
> 
> 

### <span data-ttu-id="2063c-306"><a name="step2"></a>步驟 2： 建立簡易實驗 Azure Machine Learning toopredict 按 / 沒有按下</span><span class="sxs-lookup"><span data-stu-id="2063c-306"><a name="step2"></a> Step 2: Create a simple experiment in Azure Machine Learning toopredict clicks / no clicks</span></span>
<span data-ttu-id="2063c-307">我們的 Azure ML 實驗看起來如下所示：</span><span class="sxs-lookup"><span data-stu-id="2063c-307">Our Azure ML experiment looks like this:</span></span>

![Machine Learning 實驗](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

<span data-ttu-id="2063c-309">現在，我們會檢查此實驗 hello 重要元件。</span><span class="sxs-lookup"><span data-stu-id="2063c-309">We now examine hello key components of this experiment.</span></span> <span data-ttu-id="2063c-310">提醒您，我們需要的 toodrag 我們已儲存的定型和測試資料集 tooour 實驗畫布上的第一次。</span><span class="sxs-lookup"><span data-stu-id="2063c-310">As a reminder, we need toodrag our saved train and test datasets on tooour experiment canvas first.</span></span>

#### <a name="clean-missing-data"></a><span data-ttu-id="2063c-311">清除遺漏的資料</span><span class="sxs-lookup"><span data-stu-id="2063c-311">Clean Missing Data</span></span>
<span data-ttu-id="2063c-312">hello**清除遺漏資料**模組沒有其名所示： 它會清除遺漏資料可以是使用者指定的方式。</span><span class="sxs-lookup"><span data-stu-id="2063c-312">hello **Clean Missing Data** module does what its name suggests:  it cleans missing data in ways that can be user-specified.</span></span> <span data-ttu-id="2063c-313">查看此模組，我們看到這個：</span><span class="sxs-lookup"><span data-stu-id="2063c-313">Looking into this module, we see this:</span></span>

![清除遺漏的資料](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

<span data-ttu-id="2063c-315">在這裡，我們選擇 tooreplace 完全為遺漏值，以 0。</span><span class="sxs-lookup"><span data-stu-id="2063c-315">Here, we chose tooreplace all missing values with a 0.</span></span> <span data-ttu-id="2063c-316">還有其他選項，可以藉由查看 hello 模組中的 hello 下拉式清單中看到。</span><span class="sxs-lookup"><span data-stu-id="2063c-316">There are other options as well, which can be seen by looking at hello dropdowns in hello module.</span></span>

#### <a name="feature-engineering-on-hello-data"></a><span data-ttu-id="2063c-317">Hello 資料特徵設計</span><span class="sxs-lookup"><span data-stu-id="2063c-317">Feature engineering on hello data</span></span>
<span data-ttu-id="2063c-318">大型資料集的部分類別功能可以有數百萬的唯一值。</span><span class="sxs-lookup"><span data-stu-id="2063c-318">There can be millions of unique values for some categorical features of large datasets.</span></span> <span data-ttu-id="2063c-319">使用像是一個有效編碼的單純方法來表示高維度類別功能是完全不可行的。</span><span class="sxs-lookup"><span data-stu-id="2063c-319">Using naive methods such as one-hot encoding for representing such high-dimensional categorical features is entirely unfeasible.</span></span> <span data-ttu-id="2063c-320">在本逐步解說中，我們將示範如何使用內建的 Azure 機器學習模組 toogenerate toouse 計數功能壓縮這些高維度的類別變數的表示法。</span><span class="sxs-lookup"><span data-stu-id="2063c-320">In this walkthrough, we demonstrate how toouse count features using built-in Azure Machine Learning modules toogenerate compact representations of these high-dimensional categorical variables.</span></span> <span data-ttu-id="2063c-321">hello 最終結果是較小的模型、 更快的定型時間及和效能度量資訊會相當類似 toousing 其他技術。</span><span class="sxs-lookup"><span data-stu-id="2063c-321">hello end-result is a smaller model size, faster training times, and performance metrics that are quite comparable toousing other techniques.</span></span>

##### <a name="building-counting-transforms"></a><span data-ttu-id="2063c-322">建置計數轉換</span><span class="sxs-lookup"><span data-stu-id="2063c-322">Building counting transforms</span></span>
<span data-ttu-id="2063c-323">toobuild 計數功能，我們使用 hello**建置計數轉換**Azure Machine Learning 中使用的模組。</span><span class="sxs-lookup"><span data-stu-id="2063c-323">toobuild count features, we use hello **Build Counting Transform** module that is available in Azure Machine Learning.</span></span> <span data-ttu-id="2063c-324">hello 模組看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="2063c-324">hello module looks like this:</span></span>

<span data-ttu-id="2063c-325">![建置計數轉換模組](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![建置計數轉換模組](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span><span class="sxs-lookup"><span data-stu-id="2063c-325">![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="2063c-326">在 [hello**計算資料行**] 方塊中，我們輸入資料行，我們希望 tooperform 次數。</span><span class="sxs-lookup"><span data-stu-id="2063c-326">In hello **Count columns** box, we enter those columns that we wish tooperform counts on.</span></span> <span data-ttu-id="2063c-327">一般來說，這些是 (如上所述) 高維度類別資料行。</span><span class="sxs-lookup"><span data-stu-id="2063c-327">Typically, these are (as mentioned) high-dimensional categorical columns.</span></span> <span data-ttu-id="2063c-328">我們曾提及 hello 開頭的 hello Criteo 資料集有 26 類別資料行： 從第 15 欄 tooCol40。</span><span class="sxs-lookup"><span data-stu-id="2063c-328">At hello start, we mentioned that hello Criteo dataset has 26 categorical columns: from Col15 tooCol40.</span></span> <span data-ttu-id="2063c-329">在這裡，倚賴它們全部，並提供其索引也 （從 15 too40 所示，以逗號分隔)。</span><span class="sxs-lookup"><span data-stu-id="2063c-329">Here, we count on all of them and give their indices (from 15 too40 separated by commas as shown).</span></span>
> 

<span data-ttu-id="2063c-330">中的 toouse hello 模組 hello MapReduce 模式 （適用於大型資料集），我們需要存取 tooan HDInsight Hadoop 叢集中 (一個用於進行探索功能，可重複使用針對此用途以及 hello) 和它的認證。</span><span class="sxs-lookup"><span data-stu-id="2063c-330">toouse hello module in hello MapReduce mode (appropriate for large datasets), we need access tooan HDInsight Hadoop cluster (hello one used for feature exploration can be reused for this purpose as well) and its credentials.</span></span> <span data-ttu-id="2063c-331">hello 之前的圖表說明哪些 hello 填滿的值外觀 （取代提供您自己使用案例的相關與 hello 值）。</span><span class="sxs-lookup"><span data-stu-id="2063c-331">hello  previous figures illustrate what hello filled-in values look like (replace hello values provided for illustration with those relevant for your own use-case).</span></span>

![模組參數](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

<span data-ttu-id="2063c-333">在 hello 圖中，我們會示範如何 tooenter hello 輸入 blob 的位置。</span><span class="sxs-lookup"><span data-stu-id="2063c-333">In hello figure above, we show how tooenter hello input blob location.</span></span> <span data-ttu-id="2063c-334">此位置已 hello 保留用來建立計數資料表的資料。</span><span class="sxs-lookup"><span data-stu-id="2063c-334">This location has hello data reserved for building count tables on.</span></span>

<span data-ttu-id="2063c-335">此模組執行之後，我們可以儲存 hello 轉換稍後 hello 模組上按一下滑鼠右鍵，然後選取 hello**存轉換**選項：</span><span class="sxs-lookup"><span data-stu-id="2063c-335">After this module finishes running, we can save hello transform for later by right-clicking hello module and selecting hello **Save as Transform** option:</span></span>

![「另存為轉換」選項](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

<span data-ttu-id="2063c-337">在我們實驗架構中如上所示，hello 資料集 」 ytransform2 」 對應精確 tooa 儲存計數轉換。</span><span class="sxs-lookup"><span data-stu-id="2063c-337">In our experiment architecture shown above, hello dataset "ytransform2" corresponds precisely tooa saved count transform.</span></span> <span data-ttu-id="2063c-338">這項實驗中的 hello 其餘部分，我們假設使用該 hello 讀取器**建置計數轉換**模組上某些資料 toogenerate 計數，然後可以使用這些計數 toogenerate 計數功能上 hello 定型和測試資料集。</span><span class="sxs-lookup"><span data-stu-id="2063c-338">For hello remainder of this experiment, we assume that hello reader used a **Build Counting Transform** module on some data toogenerate counts, and can then use those counts toogenerate count features on hello train and test datasets.</span></span>

##### <a name="choosing-what-count-features-tooinclude-as-part-of-hello-train-and-test-datasets"></a><span data-ttu-id="2063c-339">選擇項目計數功能 tooinclude 一部分 hello 定型和測試資料集</span><span class="sxs-lookup"><span data-stu-id="2063c-339">Choosing what count features tooinclude as part of hello train and test datasets</span></span>
<span data-ttu-id="2063c-340">一旦準備好轉換計數，hello 使用者可以選擇哪些功能 tooinclude 中其定型和測試資料集使用 hello**修改計數資料表參數**模組。</span><span class="sxs-lookup"><span data-stu-id="2063c-340">Once we have a count transform ready, hello user can choose what features tooinclude in their train and test datasets using hello **Modify Count Table Parameters** module.</span></span> <span data-ttu-id="2063c-341">為了完整性，我們會在此顯示這個模組，但為了簡單起見，請不要真的在實驗中使用它。</span><span class="sxs-lookup"><span data-stu-id="2063c-341">We just show this module here for completeness, but in interests of simplicity do not actually use it in our experiment.</span></span>

![修改計數資料表參數](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

<span data-ttu-id="2063c-343">在此情況下，可以看出我們已選擇 toouse 只 hello 對數勝算和 tooignore hello back off 資料行。</span><span class="sxs-lookup"><span data-stu-id="2063c-343">In this case, as can be seen, we have chosen toouse just hello log-odds and tooignore hello back off column.</span></span> <span data-ttu-id="2063c-344">我們也可以設定參數，例如 hello 記憶體回收筒臨界值，多少虛擬先前範例 tooadd 變平滑，及是否 toouse 任何拉普拉斯 noise 與否。</span><span class="sxs-lookup"><span data-stu-id="2063c-344">We can also set parameters such as hello garbage bin threshold, how many pseudo-prior examples tooadd for smoothing, and whether toouse any Laplacian noise or not.</span></span> <span data-ttu-id="2063c-345">所有這些都進階功能，而且很 toobe 註明 hello 預設值是很好的起點是新的功能產生 toothis 類型使用者。</span><span class="sxs-lookup"><span data-stu-id="2063c-345">All these are advanced features and it is toobe noted that hello default values are a good starting point for users who are new toothis type of feature generation.</span></span>

##### <a name="data-transformation-before-generating-hello-count-features"></a><span data-ttu-id="2063c-346">資料轉換之前產生 hello 計數功能</span><span class="sxs-lookup"><span data-stu-id="2063c-346">Data transformation before generating hello count features</span></span>
<span data-ttu-id="2063c-347">現在我們著重於很重要的一點需轉換我們定型和測試資料的先前 tooactually 產生計數功能。</span><span class="sxs-lookup"><span data-stu-id="2063c-347">Now we focus on an important point about transforming our train and test data prior tooactually generating count features.</span></span> <span data-ttu-id="2063c-348">請注意，有兩個**執行 R 指令碼**我們套用 hello 計數轉換 tooour 資料之前使用的模組。</span><span class="sxs-lookup"><span data-stu-id="2063c-348">Note that there are two **Execute R Script** modules used before we apply hello count transform tooour data.</span></span>

![執行 R 指令碼模組](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

<span data-ttu-id="2063c-350">以下是第一個 R 指令碼 hello:</span><span class="sxs-lookup"><span data-stu-id="2063c-350">Here is hello first R script:</span></span>

![第一個 R 指令碼](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

<span data-ttu-id="2063c-352">在此 R 指令碼中，我們重新命名我們的資料行 toonames"Col1"太"Col40"。</span><span class="sxs-lookup"><span data-stu-id="2063c-352">In this R script, we rename our columns toonames "Col1" too"Col40".</span></span> <span data-ttu-id="2063c-353">這是因為 hello 計數轉換必須要有這種格式的名稱。</span><span class="sxs-lookup"><span data-stu-id="2063c-353">This is because hello count transform expects names of this format.</span></span>

<span data-ttu-id="2063c-354">在 hello 第二個 R 指令碼中，我們平衡 hello 正數和負數類別之間的通訊群組 （類別 1 和 0 分別） 由 downsampling hello 負類別。</span><span class="sxs-lookup"><span data-stu-id="2063c-354">In hello second R script, we balance hello distribution between positive and negative classes (classes 1 and 0 respectively) by downsampling hello negative class.</span></span> <span data-ttu-id="2063c-355">hello R 指令碼以下顯示如何 toodo 這樣：</span><span class="sxs-lookup"><span data-stu-id="2063c-355">hello R script here shows how toodo this:</span></span>

![第二個 R 指令碼](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

<span data-ttu-id="2063c-357">在這個簡單的 R 指令碼，我們使用 「 pos\_協商\_比率"tooset hello 數量正數 hello 與 hello 負類別之間取得平衡。</span><span class="sxs-lookup"><span data-stu-id="2063c-357">In this simple R script, we use "pos\_neg\_ratio" tooset hello amount of balance between hello positive and hello negative classes.</span></span> <span data-ttu-id="2063c-358">這是很重要，因為通常改善類別不平衡有分類問題中的效能優勢 hello 類別發佈所在 toodo 有所偏差 （請記得，在本例中，我們有 3.3%正類別和 96.7%負類別）。</span><span class="sxs-lookup"><span data-stu-id="2063c-358">This is important toodo since improving class imbalance usually has performance benefits for classification problems where hello class distribution is skewed (recall that in our case, we have 3.3% positive class and 96.7% negative class).</span></span>

##### <a name="applying-hello-count-transformation-on-our-data"></a><span data-ttu-id="2063c-359">在我們的資料上套用 hello 計數轉換</span><span class="sxs-lookup"><span data-stu-id="2063c-359">Applying hello count transformation on our data</span></span>
<span data-ttu-id="2063c-360">最後，我們可以使用 hello**套用轉換**模組 tooapply hello 計數轉換在我們的定型和測試資料集。</span><span class="sxs-lookup"><span data-stu-id="2063c-360">Finally, we can use hello **Apply Transformation** module tooapply hello count transforms on our train and test datasets.</span></span> <span data-ttu-id="2063c-361">此模組會將儲存的 hello 計數轉換，當做一個輸入和 hello 定型或測試資料集，如 hello 其他輸入，並傳回的資料計數功能。</span><span class="sxs-lookup"><span data-stu-id="2063c-361">This module takes hello saved count transform as one input and hello train or test datasets as hello other input, and returns data with count features.</span></span> <span data-ttu-id="2063c-362">如下所示：</span><span class="sxs-lookup"><span data-stu-id="2063c-362">It is shown here:</span></span>

![套用轉換模組](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-hello-count-features-look-like"></a><span data-ttu-id="2063c-364">摘錄，hello 計數功能的外觀</span><span class="sxs-lookup"><span data-stu-id="2063c-364">An excerpt of what hello count features look like</span></span>
<span data-ttu-id="2063c-365">很多好處 toosee hello 計數功能看起來像在我們的案例。</span><span class="sxs-lookup"><span data-stu-id="2063c-365">It is instructive toosee what hello count features look like in our case.</span></span> <span data-ttu-id="2063c-366">以下示範該摘錄：</span><span class="sxs-lookup"><span data-stu-id="2063c-366">Here we show an excerpt of this:</span></span>

![計數功能](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

<span data-ttu-id="2063c-368">在這段摘錄中，我們顯示 hello 我們上計算的資料行，我們得到 hello 計數，且在加法 tooany 相關 backoffs 記錄勝算的特徵。</span><span class="sxs-lookup"><span data-stu-id="2063c-368">In this excerpt, we show that for hello columns that we counted on, we get hello counts and log odds in addition tooany relevant backoffs.</span></span>

<span data-ttu-id="2063c-369">現在，我們已準備好 toobuild 使用這些已轉換的資料集的 Azure 機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="2063c-369">We are now ready toobuild an Azure Machine Learning model using these transformed datasets.</span></span> <span data-ttu-id="2063c-370">Hello 下一節，我們會示範如何完成。</span><span class="sxs-lookup"><span data-stu-id="2063c-370">In hello next section, we show how this can be done.</span></span>

### <span data-ttu-id="2063c-371"><a name="step3"></a>步驟 3： 建立、 定型和計分 hello 模型</span><span class="sxs-lookup"><span data-stu-id="2063c-371"><a name="step3"></a> Step 3: Build, train, and score hello model</span></span>

#### <a name="choice-of-learner"></a><span data-ttu-id="2063c-372">選擇學習者</span><span class="sxs-lookup"><span data-stu-id="2063c-372">Choice of learner</span></span>
<span data-ttu-id="2063c-373">首先，我們需要 toochoose 學習模組。</span><span class="sxs-lookup"><span data-stu-id="2063c-373">First, we need toochoose a learner.</span></span> <span data-ttu-id="2063c-374">我們會持續 toouse 兩個類別，促進式決策樹為我們的學習因子。</span><span class="sxs-lookup"><span data-stu-id="2063c-374">We are going toouse a two class boosted decision tree as our learner.</span></span> <span data-ttu-id="2063c-375">以下是此學習模組的 hello 預設選項：</span><span class="sxs-lookup"><span data-stu-id="2063c-375">Here are hello default options for this learner:</span></span>

![二元促進式決策樹參數](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

<span data-ttu-id="2063c-377">我們實驗中，我們會持續 toochoose hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="2063c-377">For our experiment, we are going toochoose hello default values.</span></span> <span data-ttu-id="2063c-378">記下該 hello 預設都通常有意義，且對效能的好方法 tooget 快速基準。</span><span class="sxs-lookup"><span data-stu-id="2063c-378">We note that hello defaults are usually meaningful and a good way tooget quick baselines on performance.</span></span> <span data-ttu-id="2063c-379">您可以清除參數如果您選擇您有的 tooonce 基準，就可改善效能。</span><span class="sxs-lookup"><span data-stu-id="2063c-379">You can improve on performance by sweeping parameters if you choose tooonce you have a baseline.</span></span>

#### <a name="train-hello-model"></a><span data-ttu-id="2063c-380">定型 hello 模型</span><span class="sxs-lookup"><span data-stu-id="2063c-380">Train hello model</span></span>
<span data-ttu-id="2063c-381">對於訓練，我們只需叫用 **訓練模型** 模組。</span><span class="sxs-lookup"><span data-stu-id="2063c-381">For training, we simply invoke a **Train Model** module.</span></span> <span data-ttu-id="2063c-382">兩個輸入 tooit hello 為 hello 二級促進式決策樹的學習因子和我們的定型資料集。</span><span class="sxs-lookup"><span data-stu-id="2063c-382">hello two inputs tooit are hello Two-Class Boosted Decision Tree learner and our train dataset.</span></span> <span data-ttu-id="2063c-383">其如下所示：</span><span class="sxs-lookup"><span data-stu-id="2063c-383">This is shown here:</span></span>

![訓練模組](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-hello-model"></a><span data-ttu-id="2063c-385">計分 hello 模型</span><span class="sxs-lookup"><span data-stu-id="2063c-385">Score hello model</span></span>
<span data-ttu-id="2063c-386">一旦已定型的模型，我們已準備資料集 tooevaluate tooscore hello 上的測試其效能。</span><span class="sxs-lookup"><span data-stu-id="2063c-386">Once we have a trained model, we are ready tooscore on hello test dataset and tooevaluate its performance.</span></span> <span data-ttu-id="2063c-387">要執行此作業使用 hello**計分模型**hello 遵循圖中，連同所示的模組**評估模型**模組：</span><span class="sxs-lookup"><span data-stu-id="2063c-387">We do this by using hello **Score Model** module shown in hello following figure, along with an **Evaluate Model** module:</span></span>

![Score Model module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <span data-ttu-id="2063c-389"><a name="step4"></a>步驟 4： 評估 hello 模型</span><span class="sxs-lookup"><span data-stu-id="2063c-389"><a name="step4"></a> Step 4: Evaluate hello model</span></span>
<span data-ttu-id="2063c-390">最後，我們希望 tooanalyze 模型效能。</span><span class="sxs-lookup"><span data-stu-id="2063c-390">Finally, we would like tooanalyze model performance.</span></span> <span data-ttu-id="2063c-391">通常，針對兩個類別 （二進位） 的分類問題，良好的量值為 hello AUC。</span><span class="sxs-lookup"><span data-stu-id="2063c-391">Usually, for two class (binary) classification problems, a good measure is hello AUC.</span></span> <span data-ttu-id="2063c-392">toovisualize，我們連接 hello**計分模型**模組 tooan**評估模型**這個模組。</span><span class="sxs-lookup"><span data-stu-id="2063c-392">toovisualize this, we hook up hello **Score Model** module tooan **Evaluate Model** module for this.</span></span> <span data-ttu-id="2063c-393">按一下**視覺化**上 hello**評估模型**模組會產生類似下列其中一個 hello 圖形：</span><span class="sxs-lookup"><span data-stu-id="2063c-393">Clicking **Visualize** on hello **Evaluate Model** module yields a graphic like hello following one:</span></span>

![評估模組 BDT 模型](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

<span data-ttu-id="2063c-395">二進位檔 （或兩個類別） 中分類問題，良好的預測精確度量值為 hello 下曲線區域 (AUC)。</span><span class="sxs-lookup"><span data-stu-id="2063c-395">In binary (or two class) classification problems, a good measure of prediction accuracy is hello Area Under Curve (AUC).</span></span> <span data-ttu-id="2063c-396">接下來，我們會顯示在我們的測試資料集上使用此模型的結果。</span><span class="sxs-lookup"><span data-stu-id="2063c-396">In what follows, we show our results using this model on our test dataset.</span></span> <span data-ttu-id="2063c-397">tooget hello，以滑鼠右鍵按一下 hello 輸出連接埠**評估模型**模組然後**視覺化**。</span><span class="sxs-lookup"><span data-stu-id="2063c-397">tooget this, right-click hello output port of hello **Evaluate Model** module and then **Visualize**.</span></span>

![視覺化評估模型模組](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <span data-ttu-id="2063c-399"><a name="step5"></a>步驟 5: Hello 模型發行為 Web 服務</span><span class="sxs-lookup"><span data-stu-id="2063c-399"><a name="step5"></a> Step 5: Publish hello model as a Web service</span></span>
<span data-ttu-id="2063c-400">hello 能力 toopublish 為 web 服務，並至少加裝製作出 Azure 機器學習模型會進行廣泛使用的重要功能。</span><span class="sxs-lookup"><span data-stu-id="2063c-400">hello ability toopublish an Azure Machine Learning model as web services with a minimum of fuss is a valuable feature for making it widely available.</span></span> <span data-ttu-id="2063c-401">完成之後，任何人都可以製作呼叫 toohello web 服務所需的預測，，和 hello web 服務使用 hello 模型 tooreturn 這些預測的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="2063c-401">Once that is done, anyone can make calls toohello web service with input data that they need predictions for, and hello web service uses hello model tooreturn those predictions.</span></span>

<span data-ttu-id="2063c-402">toodo，我們先儲存我們已定型的模型中當做已定型的模型物件。</span><span class="sxs-lookup"><span data-stu-id="2063c-402">toodo this, we first save our trained model as a Trained Model object.</span></span> <span data-ttu-id="2063c-403">這是以滑鼠右鍵按一下 hello**定型模型**模組，使用 hello**儲存為定型的模型**選項。</span><span class="sxs-lookup"><span data-stu-id="2063c-403">This is done by right-clicking hello **Train Model** module and using hello **Save as Trained Model** option.</span></span>

<span data-ttu-id="2063c-404">接下來，我們需要 toocreate 輸入和輸出的 web 服務連接埠：</span><span class="sxs-lookup"><span data-stu-id="2063c-404">Next, we need toocreate input and output ports for our web service:</span></span>

* <span data-ttu-id="2063c-405">輸入的連接埠 hello 相同形成所需的預測 hello 資料以取得資料</span><span class="sxs-lookup"><span data-stu-id="2063c-405">an input port takes data in hello same form as hello data that we need predictions for</span></span>
* <span data-ttu-id="2063c-406">輸出連接埠傳回 hello 計分標籤和 hello 相關聯的機率。</span><span class="sxs-lookup"><span data-stu-id="2063c-406">an output port returns hello Scored Labels and hello associated probabilities.</span></span>

#### <a name="select-a-few-rows-of-data-for-hello-input-port"></a><span data-ttu-id="2063c-407">選取幾個資料列之資料的 hello 輸入連接埠</span><span class="sxs-lookup"><span data-stu-id="2063c-407">Select a few rows of data for hello input port</span></span>
<span data-ttu-id="2063c-408">它是方便 toouse**套用 SQL 轉換**模組 tooselect 只是 10 的資料列 tooserve hello 為輸入連接埠資料。</span><span class="sxs-lookup"><span data-stu-id="2063c-408">It is convenient toouse an **Apply SQL Transformation** module tooselect just 10 rows tooserve as hello input port data.</span></span> <span data-ttu-id="2063c-409">選取這些資料列的資料，我們使用如下所示的 hello SQL 查詢的輸入連接埠：</span><span class="sxs-lookup"><span data-stu-id="2063c-409">Select just these rows of data for our input port using hello SQL query shown here:</span></span>

![輸入連接埠資料](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a><span data-ttu-id="2063c-411">Web 服務</span><span class="sxs-lookup"><span data-stu-id="2063c-411">Web service</span></span>
<span data-ttu-id="2063c-412">現在我們已備妥 toorun 小型的實驗可能是使用的 toopublish web 服務。</span><span class="sxs-lookup"><span data-stu-id="2063c-412">Now we are ready toorun a small experiment that can be used toopublish our web service.</span></span>

#### <a name="generate-input-data-for-webservice"></a><span data-ttu-id="2063c-413">產生 Web 服務的輸入資料</span><span class="sxs-lookup"><span data-stu-id="2063c-413">Generate input data for webservice</span></span>
<span data-ttu-id="2063c-414">第零個步驟，hello 計數資料表很大，因為我們便會採取的測試資料的幾行並從其中產生輸出的資料計數功能。</span><span class="sxs-lookup"><span data-stu-id="2063c-414">As a zeroth step, since hello count table is large, we take a few lines of test data and generate output data from it with count features.</span></span> <span data-ttu-id="2063c-415">這可做為我們的 web 服務的 hello 輸入的資料格式。</span><span class="sxs-lookup"><span data-stu-id="2063c-415">This can serve as hello input data format for our webservice.</span></span> <span data-ttu-id="2063c-416">其如下所示：</span><span class="sxs-lookup"><span data-stu-id="2063c-416">This is shown here:</span></span>

![建立 BDT 輸入資料](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> <span data-ttu-id="2063c-418">Hello 輸入的資料格式，我們現在使用 hello 的 hello 輸出**Count Featurizer**模組。</span><span class="sxs-lookup"><span data-stu-id="2063c-418">For hello input data format, we now use hello OUTPUT of hello **Count Featurizer** module.</span></span> <span data-ttu-id="2063c-419">此實驗執行完成時，一旦儲存 hello 輸出從 hello **Count Featurizer**模組做為資料集。</span><span class="sxs-lookup"><span data-stu-id="2063c-419">Once this experiment finishes running, save hello output from hello **Count Featurizer** module as a Dataset.</span></span> <span data-ttu-id="2063c-420">此資料集用於 hello hello web 服務中的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="2063c-420">This Dataset is used for hello input data in hello webservice.</span></span>
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a><span data-ttu-id="2063c-421">發佈 Web 服務的評分實驗</span><span class="sxs-lookup"><span data-stu-id="2063c-421">Scoring experiment for publishing webservice</span></span>
<span data-ttu-id="2063c-422">首先，我們顯示其外觀。</span><span class="sxs-lookup"><span data-stu-id="2063c-422">First, we show what this looks like.</span></span> <span data-ttu-id="2063c-423">hello 基本結構是**計分模型**模組接受我們定型的模型物件和我們在使用 hello hello 先前步驟中產生的輸入資料的幾行**Count Featurizer**模組。</span><span class="sxs-lookup"><span data-stu-id="2063c-423">hello essential structure is a **Score Model** module that accepts our trained model object and a few lines of input data that we generated in hello previous steps using hello **Count Featurizer** module.</span></span> <span data-ttu-id="2063c-424">我們使用 「 選取資料行中資料集 」 tooproject 出 hello 計分標籤與 hello 分數機率。</span><span class="sxs-lookup"><span data-stu-id="2063c-424">We use "Select Columns in Dataset" tooproject out hello Scored labels and hello Score probabilities.</span></span>

![選取資料集中的資料行](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

<span data-ttu-id="2063c-426">請注意如何 hello**資料集中選取的資料行**模組可用於 '過濾' 的資料從資料集。</span><span class="sxs-lookup"><span data-stu-id="2063c-426">Notice how hello **Select Columns in Dataset** module can be used for 'filtering' data out from a dataset.</span></span> <span data-ttu-id="2063c-427">我們會顯示以下 hello 內容：</span><span class="sxs-lookup"><span data-stu-id="2063c-427">We show hello contents here:</span></span>

![使用資料集的模組中的 hello 選取資料行篩選](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

<span data-ttu-id="2063c-429">tooget hello 藍色輸入和輸出連接埠，您只是按一下**準備 webservice**在 hello 右下方。</span><span class="sxs-lookup"><span data-stu-id="2063c-429">tooget hello blue input and output ports, you simply click **prepare webservice** at hello bottom right.</span></span> <span data-ttu-id="2063c-430">執行這項實驗也可讓我們 toopublish hello web 服務： 按一下 hello**發佈 WEB 服務**在 hello 下方所示，這裡的圖示：</span><span class="sxs-lookup"><span data-stu-id="2063c-430">Running this experiment also allows us toopublish hello web service: click hello **PUBLISH WEB SERVICE** icon at hello bottom right, shown here:</span></span>

![發佈 Web 服務](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

<span data-ttu-id="2063c-432">Hello webservice 發行之後，我們會取得重新導向的 tooa 頁面，因此看起來：</span><span class="sxs-lookup"><span data-stu-id="2063c-432">Once hello webservice is published, we get redirected tooa page that looks thus:</span></span>

![Web 服務儀表板](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

<span data-ttu-id="2063c-434">我們可以看到兩個 web 服務連結左邊為 hello:</span><span class="sxs-lookup"><span data-stu-id="2063c-434">We see two links for webservices on hello left side:</span></span>

* <span data-ttu-id="2063c-435">hello**要求/回應**服務 （或 RR） 僅供單一預測，而且我們利用此 workshop 中。</span><span class="sxs-lookup"><span data-stu-id="2063c-435">hello **REQUEST/RESPONSE** Service (or RRS) is meant for single predictions and is what we utilize in this workshop.</span></span>
* <span data-ttu-id="2063c-436">hello**批次執行**服務 (BES) 用於批次預測，而且需要 hello 使用的輸入的資料 toomake 預測位於 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="2063c-436">hello **BATCH EXECUTION** Service (BES) is used for batch predictions and requires that hello input data used toomake predictions reside in Azure Blob Storage.</span></span>

<span data-ttu-id="2063c-437">按一下 hello 連結**要求/回應**會帶我們 tooa 頁面，提供預先定義程式碼在 C#、 python 和。進行呼叫 toohello webservice 可以輕鬆地使用這個代碼。</span><span class="sxs-lookup"><span data-stu-id="2063c-437">Clicking on hello link **REQUEST/RESPONSE** takes us tooa page that gives us pre-canned code in C#, python, and R. This code can be conveniently used for making calls toohello webservice.</span></span> <span data-ttu-id="2063c-438">請注意該 hello 這個頁面上的 API 金鑰需要 toobe 用來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="2063c-438">Note that hello API key on this page needs toobe used for authentication.</span></span>

<span data-ttu-id="2063c-439">它是方便 toocopy 此 python 程式碼 hello IPython 筆記型電腦 tooa 新儲存格上方時。</span><span class="sxs-lookup"><span data-stu-id="2063c-439">It is convenient toocopy this python code over tooa new cell in hello IPython notebook.</span></span>

<span data-ttu-id="2063c-440">這裡我們顯示 hello 正確的 API 金鑰的 python 程式碼區段。</span><span class="sxs-lookup"><span data-stu-id="2063c-440">Here we show a segment of python code with hello correct API key.</span></span>

![Python 程式碼](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

<span data-ttu-id="2063c-442">請注意，我們取代 hello 預設 API 金鑰我們 webservices API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="2063c-442">Note that we replaced hello default API key with our webservices's API key.</span></span> <span data-ttu-id="2063c-443">按一下**執行**IPython 中此資料格筆記本會產生下列回應 hello:</span><span class="sxs-lookup"><span data-stu-id="2063c-443">Clicking **Run** on this cell in an IPython notebook yields hello following response:</span></span>

![IPython 回應](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

<span data-ttu-id="2063c-445">我們會了解 hello 兩個測試我們詢問 （hello JSON framework hello python 指令碼) 中的範例，我們得到解答 hello 表單"計分標籤，計分機率 」。</span><span class="sxs-lookup"><span data-stu-id="2063c-445">We see that for hello two test examples we asked about (in hello JSON framework of hello python script), we get back answers in hello form "Scored Labels, Scored Probabilities".</span></span> <span data-ttu-id="2063c-446">請注意，在此情況下，我們選擇 hello 預設值的 hello 預先定義的程式碼提供 (0 的所有數值資料行和 hello 字串的所有類別資料行的 「 值 」)。</span><span class="sxs-lookup"><span data-stu-id="2063c-446">Note that in this case, we chose hello default values that hello pre-canned code provides (0's for all numeric columns and hello string "value" for all categorical columns).</span></span>

<span data-ttu-id="2063c-447">這會結束我們的端對端逐步解說顯示如何使用 Azure Machine Learning toohandle 大型資料集。</span><span class="sxs-lookup"><span data-stu-id="2063c-447">This concludes our end-to-end walkthrough showing how toohandle large-scale dataset using Azure Machine Learning.</span></span> <span data-ttu-id="2063c-448">我們入門 tb 資料、 建構預測模型並將它部署為 web 服務 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="2063c-448">We started with a terabyte of data, constructed a prediction model and deployed it as a web service in hello cloud.</span></span>

