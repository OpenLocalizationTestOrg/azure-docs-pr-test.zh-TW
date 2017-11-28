---
title: "Azure Data Lake 中可調整的資料科學︰完整的逐步解說 | Microsoft Docs"
description: "影響 toouse Azure 資料湖 toodo 資料瀏覽和二元分類工作的資料集。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 91a8207f-1e57-4570-b7fc-7c5fa858ffeb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: bradsev;weig
ms.openlocfilehash: 8b05457ae7045a7aaed350a7502469f2247161e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a><span data-ttu-id="1b959-103">Azure Data Lake 中可調整的資料科學︰完整的逐步解說</span><span class="sxs-lookup"><span data-stu-id="1b959-103">Scalable Data Science with Azure Data Lake: An end-to-end Walkthrough</span></span>
<span data-ttu-id="1b959-104">本逐步解說示範如何 toouse Azure 資料湖 toodo 資料瀏覽和 hello NYC 範例的二元分類工作計程車行程及價位資料集 toopredict 提示將支付的價位。</span><span class="sxs-lookup"><span data-stu-id="1b959-104">This walkthrough shows how toouse Azure Data Lake toodo data exploration and binary classification tasks on a sample of hello NYC taxi trip and fare dataset toopredict whether or not a tip will be paid by a fare.</span></span> <span data-ttu-id="1b959-105">它將引導您完成 hello 步驟的 hello[資料科學的小組流程](http://aka.ms/datascienceprocess)、 端對端從資料擷取 toomodel 定型，然後再 toohello 部署發行 hello 模型的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="1b959-105">It walks you through hello steps of hello [Team Data Science Process](http://aka.ms/datascienceprocess), end-to-end, from data acquisition toomodel training, and then toohello deployment of a web service that publishes hello model.</span></span>

### <a name="azure-data-lake-analytics"></a><span data-ttu-id="1b959-106">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1b959-106">Azure Data Lake Analytics</span></span>
<span data-ttu-id="1b959-107">hello [Microsoft Azure 資料湖](https://azure.microsoft.com/solutions/data-lake/)具有所有 hello 功能需要的 toomake 輕鬆的任何大小、 圖形及速度，以及 tooconduct 資料處理，進階分析和機器學習模型的資料科學家 toostore 資料高延展性符合成本效益的方式。</span><span class="sxs-lookup"><span data-stu-id="1b959-107">hello [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) has all hello capabilities required toomake it easy for data scientists toostore data of any size, shape and speed, and tooconduct data processing, advanced analytics, and machine learning modeling with high scalability in a cost-effective way.</span></span>   <span data-ttu-id="1b959-108">只在實際處理資料時，才需要依個別作業付費。</span><span class="sxs-lookup"><span data-stu-id="1b959-108">You pay on a per-job basis, only when data is actually being processed.</span></span> <span data-ttu-id="1b959-109">Azure Data Lake Analytics 包含 U-SQL、 和諧 hello 與 hello 表達能力 C# tooprovide 可擴充的宣告式本質上 SQL 的語言分散式查詢功能。</span><span class="sxs-lookup"><span data-stu-id="1b959-109">Azure Data Lake Analytics includes U-SQL, a language that blends hello declarative nature of SQL with hello expressive power of C# tooprovide scalable distributed query capability.</span></span> <span data-ttu-id="1b959-110">它可讓您 tooprocess 藉由在讀取時，套用結構描述的非結構化的資料插入自訂邏輯和使用者定義函數 (Udf)，並包含擴充性 tooenable 正常地的控制如何在標尺 tooexecute。</span><span class="sxs-lookup"><span data-stu-id="1b959-110">It enables you tooprocess unstructured data by applying schema on read, insert custom logic and user defined functions (UDFs), and includes extensibility tooenable fine grained control over how tooexecute at scale.</span></span> <span data-ttu-id="1b959-111">toolearn 深入了解 hello 設計原理背後 U-SQL，請參閱[Visual Studio 部落格文章](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/)。</span><span class="sxs-lookup"><span data-stu-id="1b959-111">toolearn more about hello design philosophy behind U-SQL, see [Visual Studio blog post](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

<span data-ttu-id="1b959-112">Data Lake Analytics 也是 Cortana Analytics 套件的重要組成部分，可搭配 Azure SQL 資料倉儲、Power BI 與 Data Factory 一起使用。</span><span class="sxs-lookup"><span data-stu-id="1b959-112">Data Lake Analytics is also a key part of Cortana Analytics Suite and works with Azure SQL Data Warehouse, Power BI, and Data Factory.</span></span> <span data-ttu-id="1b959-113">這讓您有一個完整的雲端巨量資料和進階分析平台。</span><span class="sxs-lookup"><span data-stu-id="1b959-113">This gives you a complete cloud big data and advanced analytics platform.</span></span>

<span data-ttu-id="1b959-114">本逐步解說一開始會描述 hello 必要條件和資源所需 toocomplete hello 使用 Data Lake Analytics 形成 hello 資料科學程序的工作，以及如何 tooinstall 它們。</span><span class="sxs-lookup"><span data-stu-id="1b959-114">This walkthrough begins by describing hello prerequisites and resources that are needed toocomplete hello tasks with Data Lake Analytics that form hello data science process and how tooinstall them.</span></span> <span data-ttu-id="1b959-115">然後它概述使用 U-SQL hello 資料處理步驟結束時，會顯示如何 toouse Python 和 Hive 與 Azure Machine Learning Studio toobuild 和部署 hello 預測模型。</span><span class="sxs-lookup"><span data-stu-id="1b959-115">Then it outlines hello data processing steps using U-SQL and concludes by showing how toouse Python and Hive with Azure Machine Learning Studio toobuild and deploy hello predictive models.</span></span> 

### <a name="u-sql-and-visual-studio"></a><span data-ttu-id="1b959-116">U-SQL 和 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1b959-116">U-SQL and Visual Studio</span></span>
<span data-ttu-id="1b959-117">本逐步解說會建議使用 Visual Studio tooedit U-SQL 指令碼 tooprocess hello 資料集。</span><span class="sxs-lookup"><span data-stu-id="1b959-117">This walkthrough recommends using Visual Studio tooedit U-SQL scripts tooprocess hello dataset.</span></span> <span data-ttu-id="1b959-118">hello U-SQL 指令碼會此處所述，並提供在個別的檔案。</span><span class="sxs-lookup"><span data-stu-id="1b959-118">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="1b959-119">hello 程序包括擷取、 瀏覽，和取樣 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="1b959-119">hello process includes ingesting, exploring, and sampling hello data.</span></span> <span data-ttu-id="1b959-120">它也會示範如何 toorun U-SQL 指令碼從 hello Azure 入口網站的作業。</span><span class="sxs-lookup"><span data-stu-id="1b959-120">It also shows how toorun a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="1b959-121">建立 hello 中的資料相關聯的 HDInsight 叢集 toofacilitate hello 建置和部署 Azure Machine Learning Studio 中的二元分類模型的 hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="1b959-121">Hive tables are created for hello data in an associated HDInsight cluster toofacilitate hello building and deployment of a binary classification model in Azure Machine Learning Studio.</span></span>  

### <a name="python"></a><span data-ttu-id="1b959-122">Python</span><span class="sxs-lookup"><span data-stu-id="1b959-122">Python</span></span>
<span data-ttu-id="1b959-123">此逐步解說也包含新章節，說明如何 toobuild 和部署與 Azure Machine Learning Studio 中使用 Python 的預測模型。</span><span class="sxs-lookup"><span data-stu-id="1b959-123">This walkthrough also contains a section that shows how toobuild and deploy a predictive model using Python with Azure Machine Learning Studio.</span></span>  <span data-ttu-id="1b959-124">我們提供 Jupyter 筆記本 hello Python 指令碼，此程序中的這些步驟。</span><span class="sxs-lookup"><span data-stu-id="1b959-124">We provide a Jupyter notebook with hello Python scripts for these steps in this process.</span></span> <span data-ttu-id="1b959-125">hello 筆記本包含一些額外的功能工程步驟和模型建構，例如多級分類和迴歸模型除了此處所述的 toohello 二元分類模型的程式碼。</span><span class="sxs-lookup"><span data-stu-id="1b959-125">hello notebook includes code for some additional feature engineering steps and models construction such as multiclass classification and regression modeling in addition toohello binary classification model outlined here.</span></span> <span data-ttu-id="1b959-126">hello 迴歸工作是根據其他提示功能 hello 提示 toopredict hello 量。</span><span class="sxs-lookup"><span data-stu-id="1b959-126">hello regression task is toopredict hello amount of hello tip based on other tip features.</span></span> 

### <a name="azure-machine-learning"></a><span data-ttu-id="1b959-127">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1b959-127">Azure Machine Learning</span></span>
<span data-ttu-id="1b959-128">Azure Machine Learning Studio 使用的 toobuild 並部署 hello 預測模型。</span><span class="sxs-lookup"><span data-stu-id="1b959-128">Azure Machine Learning Studio is used toobuild and deploy hello predictive models.</span></span> <span data-ttu-id="1b959-129">這是使用下列兩種方法來完成︰首先會使用 Python 指令碼，接著使用 HDInsight (Hadoop) 叢集上的 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="1b959-129">This is done using two approaches: first with Python scripts and then with Hive tables on an HDInsight (Hadoop) cluster.</span></span>

### <a name="scripts"></a><span data-ttu-id="1b959-130">指令碼</span><span class="sxs-lookup"><span data-stu-id="1b959-130">Scripts</span></span>
<span data-ttu-id="1b959-131">本逐步解說中，描述 hello 主要步驟。</span><span class="sxs-lookup"><span data-stu-id="1b959-131">Only hello principal steps are outlined in this walkthrough.</span></span> <span data-ttu-id="1b959-132">您可以下載完整的 hello **U-SQL 指令碼**和**Jupyter 筆記本**從[GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough)。</span><span class="sxs-lookup"><span data-stu-id="1b959-132">You can download hello full **U-SQL script** and **Jupyter Notebook** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b959-133">必要條件</span><span class="sxs-lookup"><span data-stu-id="1b959-133">Prerequisites</span></span>
<span data-ttu-id="1b959-134">在開始這些主題之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="1b959-134">Before you begin these topics, you must have hello following:</span></span>

* <span data-ttu-id="1b959-135">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b959-135">An Azure subscription.</span></span> <span data-ttu-id="1b959-136">如果還沒有訂用帳戶，請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="1b959-136">If you do not already have one, see [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="1b959-137">[建議] Visual Studio 2013 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="1b959-137">[Recommended] Visual Studio 2013 or later.</span></span> <span data-ttu-id="1b959-138">如果您還沒有安裝這些版本的其中一個，您可以從 [Visual Studio 社群](https://www.visualstudio.com/vs/community/)下載免費的社群版本。</span><span class="sxs-lookup"><span data-stu-id="1b959-138">If you do not already have one of these versions installed, you can download a free Community version from [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span></span>

> [!NOTE]
> <span data-ttu-id="1b959-139">而不是 Visual Studio 中，您也可以使用 hello Azure 入口網站 toosubmit Azure 資料湖查詢。</span><span class="sxs-lookup"><span data-stu-id="1b959-139">Instead of Visual Studio, you can also use hello Azure Portal toosubmit Azure Data Lake queries.</span></span> <span data-ttu-id="1b959-140">我們將提供有關如何 toodo 因此與 Visual Studio 和 hello > 一節中的 hello 入口網站上的標題會指示**處理資料與 U-SQL**。</span><span class="sxs-lookup"><span data-stu-id="1b959-140">We will provide instructions on how toodo so both with Visual Studio and on hello portal in hello section titled **Process data with U-SQL**.</span></span> 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a><span data-ttu-id="1b959-141">準備 Azure Data Lake 的資料科學環境</span><span class="sxs-lookup"><span data-stu-id="1b959-141">Prepare data science environment for Azure Data Lake</span></span>
<span data-ttu-id="1b959-142">這個逐步解說中，tooprepare hello 資料科學環境建立 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="1b959-142">tooprepare hello data science environment for this walkthrough, create hello following resources:</span></span>

* <span data-ttu-id="1b959-143">Azure Data Lake Store (ADLS)</span><span class="sxs-lookup"><span data-stu-id="1b959-143">Azure Data Lake Store (ADLS)</span></span> 
* <span data-ttu-id="1b959-144">Azure Data Lake Analytics (ADLA)</span><span class="sxs-lookup"><span data-stu-id="1b959-144">Azure Data Lake Analytics (ADLA)</span></span>
* <span data-ttu-id="1b959-145">Azure Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="1b959-145">Azure Blob storage account</span></span>
* <span data-ttu-id="1b959-146">Azure Machine Learning Studio 帳戶</span><span class="sxs-lookup"><span data-stu-id="1b959-146">Azure Machine Learning Studio account</span></span>
* <span data-ttu-id="1b959-147">Azure Data Lake Tools for Visual Studio (建議)</span><span class="sxs-lookup"><span data-stu-id="1b959-147">Azure Data Lake Tools for Visual Studio (Recommended)</span></span>

<span data-ttu-id="1b959-148">本節提供如何指示 toocreate 每個這些資源。</span><span class="sxs-lookup"><span data-stu-id="1b959-148">This section provides instructions on how toocreate each of these resources.</span></span> <span data-ttu-id="1b959-149">如果您選擇 toouse Hive 資料表，與 Azure Machine Learning 中，而不是 Python toobuild 模型時，您也必須 tooprovision (Hadoop) HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="1b959-149">If you choose toouse Hive tables with Azure Machine Learning, instead of Python, toobuild a model,you will also need tooprovision an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="1b959-150">這個替代程序中的所述 hello 以下的適當章節。</span><span class="sxs-lookup"><span data-stu-id="1b959-150">This alternative procedure in described in hello appropriate section below.</span></span>


> [!NOTE]
> <span data-ttu-id="1b959-151">hello **Azure Data Lake Store**可以建立，可能是分開，或當您建立 hello **Azure Data Lake Analytics**為 hello 預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="1b959-151">hello **Azure Data Lake Store** can be created either separately or when you create hello **Azure Data Lake Analytics** as hello default storage.</span></span> <span data-ttu-id="1b959-152">指示參考來建立每個個別下列資源，但是需要個別建立 hello 資料湖存放裝置帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b959-152">Instructions are referenced for creating each of these resources separately below, but hello Data Lake storage account need not be created separately.</span></span>
>
> 

### <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="1b959-153">建立 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1b959-153">Create an Azure Data Lake Store</span></span>


<span data-ttu-id="1b959-154">建立從 hello ADLS [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="1b959-154">Create an ADLS from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="1b959-155">如需詳細資訊，請參閱 [使用 Azure 入口網站建立 HDInsight 叢集與 Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="1b959-155">For details, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="1b959-156">是確定 tooset 向上 hello 叢集 AAD 身分識別中 hello **DataSource**刀鋒視窗中的 hello**選擇性組態**刀鋒視窗中那里描述。</span><span class="sxs-lookup"><span data-stu-id="1b959-156">Be sure tooset up hello Cluster AAD Identity in hello **DataSource** blade of hello **Optional Configuration** blade described there.</span></span> 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a><span data-ttu-id="1b959-158">建立 Azure Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="1b959-158">Create an Azure Data Lake Analytics account</span></span>
<span data-ttu-id="1b959-159">建立從 hello ADLA 帳戶[Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="1b959-159">Create an ADLA account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="1b959-160">如需詳細資訊，請參閱 [教學課程：使用 Azure 入口網站開始使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="1b959-160">For details, see [Tutorial: get started with Azure Data Lake Analytics using Azure Portal](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span> 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="1b959-162">建立 Azure Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="1b959-162">Create an Azure Blob storage account</span></span>
<span data-ttu-id="1b959-163">建立 Azure Blob 儲存體帳戶從 hello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="1b959-163">Create an Azure Blob storage account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="1b959-164">如需詳細資訊，請參閱主題中的儲存體帳戶建立 hello[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="1b959-164">For details, see hello Create a storage account section in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a><span data-ttu-id="1b959-166">設定 Azure Machine Learning Studio 帳戶</span><span class="sxs-lookup"><span data-stu-id="1b959-166">Set up an Azure Machine Learning Studio account</span></span>
<span data-ttu-id="1b959-167">從 hello 登入到 Azure Machine Learning Studio 上下[Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)頁面。</span><span class="sxs-lookup"><span data-stu-id="1b959-167">Sign up/into Azure Machine Learning Studio from hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) page.</span></span> <span data-ttu-id="1b959-168">按一下 hello**現在就開始**按鈕，然後選擇 「 免費工作區 」 或 「 一般工作區 」。</span><span class="sxs-lookup"><span data-stu-id="1b959-168">Click on hello **Get started now** button and then choose a "Free Workspace" or "Standard Workspace".</span></span> <span data-ttu-id="1b959-169">在此之後將無法 toocreate 實驗，Azure ML Studio 中。</span><span class="sxs-lookup"><span data-stu-id="1b959-169">After this you will be able toocreate experiments in Azure ML Studio.</span></span>  

### <a name="install-azure-data-lake-tools-recommended"></a><span data-ttu-id="1b959-170">安裝 Azure Data Lake 工具 [建議]</span><span class="sxs-lookup"><span data-stu-id="1b959-170">Install Azure Data Lake Tools [Recommended]</span></span>
<span data-ttu-id="1b959-171">依照您的 Visual Studio 版本，從 [Azure Data Lake Tools for Visual Studio (Visual Studio 適用的 Azure Data Lake 工具)](https://www.microsoft.com/download/details.aspx?id=49504)中安裝適合的 Azure Data Lake 工具。</span><span class="sxs-lookup"><span data-stu-id="1b959-171">Install Azure Data Lake Tools for your version of Visual Studio from [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

<span data-ttu-id="1b959-173">Hello 安裝作業順利完成之後，請開啟安裝 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="1b959-173">After hello installation finishes successfully, open up Visual Studio.</span></span> <span data-ttu-id="1b959-174">您應該會看到 hello Data Lake] 索引標籤頂端 hello 的 hello 功能表。</span><span class="sxs-lookup"><span data-stu-id="1b959-174">You should see hello Data Lake tab hello menu at hello top.</span></span> <span data-ttu-id="1b959-175">您的 Azure 資源應該會出現在 hello 左面板中，當您登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b959-175">Your Azure resources should appear in hello left panel when you sign into your Azure account.</span></span>

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="hello-nyc-taxi-trips-dataset"></a><span data-ttu-id="1b959-177">hello NYC 計程車往返的資料集</span><span class="sxs-lookup"><span data-stu-id="1b959-177">hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="1b959-178">hello 我們這裡使用的資料集已公開可用的資料集-hello [NYC 計程車往返的資料集](http://www.andresmh.com/nyctaxitrips/)。</span><span class="sxs-lookup"><span data-stu-id="1b959-178">hello data set we used here is a publicly available dataset -- hello [NYC Taxi Trips dataset](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="1b959-179">hello NYC 計程車路線資料包含約 20 GB 的壓縮的 CSV 檔案 (~ 48 GB 未壓縮)，錄製超過 173 百萬個個別的往返和 hello fares 支付每往返作業。</span><span class="sxs-lookup"><span data-stu-id="1b959-179">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="1b959-180">每個往返記錄包括 hello 收取和下車位置以及時間、 匿名 hack (driver) 授權編號，並重新 hello medallion (計程車的唯一 id) 數目。</span><span class="sxs-lookup"><span data-stu-id="1b959-180">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="1b959-181">hello 資料涵蓋所有往返 hello 年份 2013年中，並提供下列兩個資料集的每個月的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b959-181">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

* <span data-ttu-id="1b959-182">hello 'trip_data' CSV 包含路線詳細資料，例如乘客、 收取和 dropoff 點數目、 路線持續時間，以及路線長度。</span><span class="sxs-lookup"><span data-stu-id="1b959-182">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="1b959-183">以下是一些範例記錄：</span><span class="sxs-lookup"><span data-stu-id="1b959-183">Here are a few sample records:</span></span>
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* <span data-ttu-id="1b959-184">hello 'trip_fare' CSV 包含 hello 價位支付每個路線，例如付款類型、 價位量、 產生額外負荷及稅金、 秘訣和 tolls，以及 hello 總容量付費的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1b959-184">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="1b959-185">以下是一些範例記錄：</span><span class="sxs-lookup"><span data-stu-id="1b959-185">Here are a few sample records:</span></span>
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="1b959-186">hello 唯一索引鍵 toojoin 路線\_資料和路線\_價位組成 hello 下列三個欄位： medallion 具 「 可回復\_授權與收取\_日期時間。</span><span class="sxs-lookup"><span data-stu-id="1b959-186">hello unique key toojoin trip\_data and trip\_fare is composed of hello following three fields: medallion, hack\_license and pickup\_datetime.</span></span> <span data-ttu-id="1b959-187">hello 未經處理的 CSV 檔案可以存取從公開的 Azure 儲存體 blob。</span><span class="sxs-lookup"><span data-stu-id="1b959-187">hello raw CSV files can be accessed from a public Azure storage blob.</span></span> <span data-ttu-id="1b959-188">hello U-SQL 指令碼，這項聯結為 hello[聯結行程及價位資料表](#join)> 一節。</span><span class="sxs-lookup"><span data-stu-id="1b959-188">hello U-SQL script for this join is in hello [Join trip and fare tables](#join) section.</span></span>

## <a name="process-data-with-u-sql"></a><span data-ttu-id="1b959-189">使用 U-SQL 處理資料</span><span class="sxs-lookup"><span data-stu-id="1b959-189">Process data with U-SQL</span></span>
<span data-ttu-id="1b959-190">這一節所述的 hello 資料處理工作包括擷取、 檢查品質、 瀏覽，以及取樣 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="1b959-190">hello data processing tasks illustrated in this section include ingesting, checking quality, exploring, and sampling hello data.</span></span> <span data-ttu-id="1b959-191">我們也將顯示如何 toojoin 行程及價位表。</span><span class="sxs-lookup"><span data-stu-id="1b959-191">We also show how toojoin trip and fare tables.</span></span> <span data-ttu-id="1b959-192">hello 最後一節顯示從 hello Azure 入口網站將 U-SQL 指令碼的工作執行。</span><span class="sxs-lookup"><span data-stu-id="1b959-192">hello final section shows run a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="1b959-193">以下是連結 tooeach 小節：</span><span class="sxs-lookup"><span data-stu-id="1b959-193">Here are links tooeach subsection:</span></span>

* [<span data-ttu-id="1b959-194">資料擷取：從公用 blob 讀取資料</span><span class="sxs-lookup"><span data-stu-id="1b959-194">Data ingestion: read in data from public blob</span></span>](#ingest)
* [<span data-ttu-id="1b959-195">資料品質檢查</span><span class="sxs-lookup"><span data-stu-id="1b959-195">Data quality checks</span></span>](#quality)
* [<span data-ttu-id="1b959-196">資料探索</span><span class="sxs-lookup"><span data-stu-id="1b959-196">Data exploration</span></span>](#explore)
* [<span data-ttu-id="1b959-197">如何聯結車程和費用資料表</span><span class="sxs-lookup"><span data-stu-id="1b959-197">Join trip and fare tables</span></span>](#join)
* [<span data-ttu-id="1b959-198">資料取樣</span><span class="sxs-lookup"><span data-stu-id="1b959-198">Data sampling</span></span>](#sample)
* [<span data-ttu-id="1b959-199">執行 U-SQL 作業</span><span class="sxs-lookup"><span data-stu-id="1b959-199">Run U-SQL jobs</span></span>](#run)

<span data-ttu-id="1b959-200">hello U-SQL 指令碼會此處所述，並提供在個別的檔案。</span><span class="sxs-lookup"><span data-stu-id="1b959-200">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="1b959-201">您可以下載完整的 hello **U-SQL 指令碼**從[GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough)。</span><span class="sxs-lookup"><span data-stu-id="1b959-201">You can download hello full **U-SQL scripts** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

<span data-ttu-id="1b959-202">tooexecute U-SQL，開啟 Visual Studio 中，按一下**檔案-新增]->--> [專案**，選擇**U-SQL 專案**、 名稱，並將它儲存 tooa 資料夾。</span><span class="sxs-lookup"><span data-stu-id="1b959-202">tooexecute U-SQL, Open Visual Studio, click **File --> New --> Project**, choose **U-SQL Project**, name and save it tooa folder.</span></span>

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> <span data-ttu-id="1b959-204">很可能 toouse hello Azure 入口網站 tooexecute U-SQL 而非 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="1b959-204">It is possible toouse hello Azure Portal tooexecute U-SQL instead of Visual Studio.</span></span> <span data-ttu-id="1b959-205">您可以瀏覽 toohello hello 入口網站上的 Azure Data Lake Analytics 資源，並送出查詢直接依 hello 遵循圖所示。</span><span class="sxs-lookup"><span data-stu-id="1b959-205">You can navigate toohello Azure Data Lake Analytics resource on hello portal and submit queries directly as illustrated in hello following figure.</span></span>
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <span data-ttu-id="1b959-207"><a name="ingest"></a>資料擷取：從公用 Blob 讀取資料</span><span class="sxs-lookup"><span data-stu-id="1b959-207"><a name="ingest"></a>Data Ingestion: Read in data from public blob</span></span>
<span data-ttu-id="1b959-208">hello hello Azure blob 中的 hello 資料的位置參考為** wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name ** ，可以使用擷取**Extractors.Csv()**。</span><span class="sxs-lookup"><span data-stu-id="1b959-208">hello location of hello data in hello Azure blob is referenced as **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** and can be extracted using **Extractors.Csv()**.</span></span> <span data-ttu-id="1b959-209">取代為您自己的容器名稱和儲存體帳戶名稱，如下列指令碼中的container_name@blob_storage_account_namehello wasb 位址中。</span><span class="sxs-lookup"><span data-stu-id="1b959-209">Substitute your own container name and storage account name in following scripts for container_name@blob_storage_account_name in hello wasb address.</span></span> <span data-ttu-id="1b959-210">因為 hello 檔案名稱都位於相同的格式，所以我們可以使用**路線\_資料 _ {\*\}.csv** tooread 12 路線的所有檔案中。</span><span class="sxs-lookup"><span data-stu-id="1b959-210">Since hello file names are in same format, we can use **trip\_data_{\*\}.csv** tooread in all 12 trip files.</span></span> 

    ///Read in Trip data
    @trip0 =
        EXTRACT 
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string
    // This is reading 12 trip data from blob
    FROM "wasb://container_name@blob_storage_account_name.blob.core.windows.net/nyctaxitrip/trip_data_{*}.csv"
    USING Extractors.Csv();

<span data-ttu-id="1b959-211">由於 hello 第一個資料列有標頭，我們需要 tooremove hello 標頭，並將資料行類型變更為適當的。</span><span class="sxs-lookup"><span data-stu-id="1b959-211">Since there are headers in hello first row, we need tooremove hello headers and change column types into appropriate ones.</span></span> <span data-ttu-id="1b959-212">我們可以儲存處理 hello 資料 tooAzure 資料湖存放區使用**swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ 或 tooAzure Blob 儲存體帳戶使用** wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**.</span><span class="sxs-lookup"><span data-stu-id="1b959-212">We can either save hello processed data tooAzure Data Lake Storage using **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ or tooAzure Blob storage account using  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**.</span></span> 

    // change data types
    @trip =
        SELECT 
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        DateTime.Parse(pickup_datetime) AS pickup_datetime,
        DateTime.Parse(dropoff_datetime) AS dropoff_datetime,
        Int32.Parse(passenger_count) AS passenger_count,
        Double.Parse(trip_time_in_secs) AS trip_time_in_secs,
        Double.Parse(trip_distance) AS trip_distance,
        (pickup_longitude==string.Empty ? 0: float.Parse(pickup_longitude)) AS pickup_longitude,
        (pickup_latitude==string.Empty ? 0: float.Parse(pickup_latitude)) AS pickup_latitude,
        (dropoff_longitude==string.Empty ? 0: float.Parse(dropoff_longitude)) AS dropoff_longitude,
        (dropoff_latitude==string.Empty ? 0: float.Parse(dropoff_latitude)) AS dropoff_latitude
    FROM @trip0
    WHERE medallion != "medallion";

    ////output data tooADL
    OUTPUT @trip   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data tooblob
    OUTPUT @trip   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

<span data-ttu-id="1b959-213">同樣地，我們可以讀取 hello 價位資料集。</span><span class="sxs-lookup"><span data-stu-id="1b959-213">Similarly we can read in hello fare data sets.</span></span> <span data-ttu-id="1b959-214">以滑鼠右鍵按一下 [Azure 資料湖存放區中，您可以在您的資料選擇 toolook **Azure 入口網站--> 資料總管**或**檔案總管**Visual Studio 內。</span><span class="sxs-lookup"><span data-stu-id="1b959-214">Right click Azure Data Lake Store, you can choose toolook at your data in **Azure Portal --> Data Explorer** or **File Explorer** within Visual Studio.</span></span> 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <span data-ttu-id="1b959-217"><a name="quality"></a>資料品質檢查</span><span class="sxs-lookup"><span data-stu-id="1b959-217"><a name="quality"></a>Data quality checks</span></span>
<span data-ttu-id="1b959-218">已經在讀取行程及價位資料表之後，資料品質檢查可依下列方式 hello。</span><span class="sxs-lookup"><span data-stu-id="1b959-218">After trip and fare tables have been read in, data quality checks can be done in hello following way.</span></span> <span data-ttu-id="1b959-219">hello 產生 CSV 檔案可以是輸出 tooAzure Blob 儲存體或 Azure 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="1b959-219">hello resulting CSV files can be output tooAzure Blob storage or Azure Data Lake Store.</span></span> 

<span data-ttu-id="1b959-220">尋找 hello medallions 數目和 medallions 唯一數目：</span><span class="sxs-lookup"><span data-stu-id="1b959-220">Find hello number of medallions and unique number of medallions:</span></span>

    ///check hello number of medallions and unique number of medallions
    @trip2 =
        SELECT
        medallion,
        vendor_id,
        pickup_datetime.Month AS pickup_month
        FROM @trip;

    @ex_1 =
        SELECT
        pickup_month, 
        COUNT(medallion) AS cnt_medallion,
        COUNT(DISTINCT(medallion)) AS unique_medallion
        FROM @trip2
        GROUP BY pickup_month;
        OUTPUT @ex_1   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="1b959-221">尋找有超過 100 個車程的牌照：</span><span class="sxs-lookup"><span data-stu-id="1b959-221">Find those medallions that had more than 100 trips:</span></span>

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="1b959-222">找到 pickup_longitude 方面的無效記錄︰</span><span class="sxs-lookup"><span data-stu-id="1b959-222">Find those invalid records in terms of pickup_longitude:</span></span>

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="1b959-223">尋找一些變數的遺漏值︰</span><span class="sxs-lookup"><span data-stu-id="1b959-223">Find missing values for some variables:</span></span>

    //check missing values
    @res =
        SELECT *,
               (medallion == null? 1 : 0) AS missing_medallion
        FROM @trip;

    @trip_summary6 =
        SELECT 
            vendor_id,
        SUM(missing_medallion) AS medallion_empty, 
        COUNT(medallion) AS medallion_total,
        COUNT(DISTINCT(medallion)) AS medallion_total_unique  
        FROM @res
        GROUP BY vendor_id;
    OUTPUT @trip_summary6
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <span data-ttu-id="1b959-224"><a name="explore"></a>資料探索</span><span class="sxs-lookup"><span data-stu-id="1b959-224"><a name="explore"></a>Data exploration</span></span>
<span data-ttu-id="1b959-225">我們可以執行一些資料瀏覽 tooget hello 資料進一步了解。</span><span class="sxs-lookup"><span data-stu-id="1b959-225">We can do some data exploration tooget a better understanding of hello data.</span></span>

<span data-ttu-id="1b959-226">找到 （雪人） 和非傾斜行程 hello 的發佈：</span><span class="sxs-lookup"><span data-stu-id="1b959-226">Find hello distribution of tipped and non-tipped trips:</span></span>

    ///tipped vs. not tipped distribution
    @tip_or_not =
        SELECT *,
               (tip_amount > 0 ? 1: 0) AS tipped
        FROM @fare;

    @ex_4 =
        SELECT tipped,
               COUNT(*) AS tip_freq
        FROM @tip_or_not
        GROUP BY tipped;
        OUTPUT @ex_4   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="1b959-227">找到的截止值的提示數量的 hello 分佈： 0,5,10 和 20 （美元）。</span><span class="sxs-lookup"><span data-stu-id="1b959-227">Find hello distribution of tip amount with cut-off values: 0,5,10,and 20 dollars.</span></span>

    //tip class/range distribution
    @tip_class =
        SELECT *,
               (tip_amount >20? 4: (tip_amount >10? 3:(tip_amount >5 ? 2:(tip_amount > 0 ? 1: 0)))) AS tip_class
        FROM @fare;
    @ex_5 =
        SELECT tip_class,
               COUNT(*) AS tip_freq
        FROM @tip_class
        GROUP BY tip_class;
        OUTPUT @ex_5   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="1b959-228">尋找車程距離的基本統計資料︰</span><span class="sxs-lookup"><span data-stu-id="1b959-228">Find basic statistics of trip distance:</span></span>

    // find basic statistics for trip_distance
    @trip_summary4 =
        SELECT 
            vendor_id,
            COUNT(*) AS cnt_row,
            MIN(trip_distance) AS min_trip_distance,
            MAX(trip_distance) AS max_trip_distance,
            AVG(trip_distance) AS avg_trip_distance 
        FROM @trip
        GROUP BY vendor_id;
    OUTPUT @trip_summary4
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

<span data-ttu-id="1b959-229">尋找 hello 依百分位數的旅行距離：</span><span class="sxs-lookup"><span data-stu-id="1b959-229">Find hello percentiles of trip distance:</span></span>

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="1b959-230"><a name="join"></a>聯結車程和費用資料表</span><span class="sxs-lookup"><span data-stu-id="1b959-230"><a name="join"></a>Join trip and fare tables</span></span>
<span data-ttu-id="1b959-231">車程和費用資料表可以由 medallion、hack_license 和 pickup_time 聯結。</span><span class="sxs-lookup"><span data-stu-id="1b959-231">Trip and fare tables can be joined by medallion, hack_license, and pickup_time.</span></span>

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output tooblob
    OUTPUT @model_data_full   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data tooADL
    OUTPUT @model_data_full   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


<span data-ttu-id="1b959-232">每個層級的旅客計數，計算 hello 記錄、 平均的提示數量、 變異數的提示數量、 百分比 （雪人） 往返數目。</span><span class="sxs-lookup"><span data-stu-id="1b959-232">For each level of passenger count, calculate hello number of records, average tip amount, variance of tip amount, percentage of tipped trips.</span></span>

    // contigency table
    @trip_summary8 =
        SELECT passenger_count,
               COUNT(*) AS cnt,
               AVG(tip_amount) AS avg_tip_amount,
               VAR(tip_amount) AS var_tip_amount,
               SUM(tipped) AS cnt_tipped,
               (float)SUM(tipped)/COUNT(*) AS pct_tipped
        FROM @model_data_full
        GROUP BY passenger_count;
        OUTPUT @trip_summary8
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <span data-ttu-id="1b959-233"><a name="sample"></a>資料取樣</span><span class="sxs-lookup"><span data-stu-id="1b959-233"><a name="sample"></a>Data sampling</span></span>
<span data-ttu-id="1b959-234">首先會隨機選取 0.1 %hello 資料從 hello 聯結的資料表：</span><span class="sxs-lookup"><span data-stu-id="1b959-234">First we randomly select 0.1% of hello data from hello joined table:</span></span>

    //random select 1/1000 data for modeling purpose
    @addrownumberres_randomsample =
    SELECT *,
            ROW_NUMBER() OVER() AS rownum
    FROM @model_data_full;

    @model_data_random_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_randomsample
    WHERE rownum % 1000 == 0;

    OUTPUT @model_data_random_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="1b959-235">接著，我們以二元變數 tip_class 進行分層取樣：</span><span class="sxs-lookup"><span data-stu-id="1b959-235">Then we do stratified sampling by binary variable tip_class:</span></span>

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output tooblob
    OUTPUT @model_data_stratified_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data tooADL
    OUTPUT @model_data_stratified_sample_1_1000   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="1b959-236"><a name="run"></a>執行 U-SQL 作業</span><span class="sxs-lookup"><span data-stu-id="1b959-236"><a name="run"></a>Run U-SQL jobs</span></span>
<span data-ttu-id="1b959-237">當您完成編輯 U-SQL 指令碼時，您可以將它們送出 toohello 伺服器使用 Azure Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b959-237">When you finish editing U-SQL scripts, you can submit them toohello server using your Azure Data Lake Analytics account.</span></span> <span data-ttu-id="1b959-238">依序按一下 [Data Lake] 和 [提交作業]，並選取您的 [Analytics 帳戶]，然後選擇 [平行處理原則]，再按一下 [提交] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1b959-238">Click **Data Lake**, **Submit Job**, select your **Analytics Account**, choose **Parallelism**, and click **Submit** button.</span></span>  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

<span data-ttu-id="1b959-240">當 hello 作業成功編譯時，將顯示 hello 狀態您工作的 Visual Studio 中進行監視。</span><span class="sxs-lookup"><span data-stu-id="1b959-240">When hello job is complied successfully, hello status of your job will be displayed in Visual Studio for monitoring.</span></span> <span data-ttu-id="1b959-241">Hello 作業完成執行後，您可以甚至重新執行 hello 工作執行程序，並找出 hello 瓶頸步驟 tooimprove 工作效率。</span><span class="sxs-lookup"><span data-stu-id="1b959-241">After hello job finishes running, you can even replay hello job execution process and find out hello bottleneck steps tooimprove your job efficiency.</span></span> <span data-ttu-id="1b959-242">您也可以移 tooAzure U-SQL 工作入口網站 toocheck hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="1b959-242">You can also go tooAzure Portal toocheck hello status of your U-SQL jobs.</span></span>

 ![13](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

<span data-ttu-id="1b959-245">現在您可以檢查 Azure Blob 儲存體或 Azure 入口網站中的 hello 輸出檔。</span><span class="sxs-lookup"><span data-stu-id="1b959-245">Now you can check hello output files in either Azure Blob storage or Azure Portal.</span></span> <span data-ttu-id="1b959-246">我們的模型化 hello 下一個步驟中，我們將使用 hello 分層的取樣資料。</span><span class="sxs-lookup"><span data-stu-id="1b959-246">We will use hello stratified sample data for our modeling in hello next step.</span></span>

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a><span data-ttu-id="1b959-249">在 Azure Machine Learning 中建置和部署模型</span><span class="sxs-lookup"><span data-stu-id="1b959-249">Build and deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="1b959-250">我們將示範兩個選項，可讓您 toopull 資料到 Azure Machine Learning toobuild 和</span><span class="sxs-lookup"><span data-stu-id="1b959-250">We demonstrate two options available for you toopull data into Azure Machine Learning toobuild and</span></span> 

* <span data-ttu-id="1b959-251">Hello 第一個選項，在您使用的是已寫入 tooan Azure Blob 的 hello 取樣資料 (在 hello**資料取樣**上述步驟) 和使用 Python toobuild 部署從 Azure 機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="1b959-251">In hello first option, you use hello sampled data that has been written tooan Azure Blob (in hello **Data sampling** step above) and use Python toobuild and deploy models from Azure Machine Learning.</span></span> 
* <span data-ttu-id="1b959-252">在 hello 第二個選項中，您查詢 hello 資料在 Azure Data Lake 中的直接使用 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="1b959-252">In hello second option, you query hello data in Azure Data Lake directly using a Hive query.</span></span> <span data-ttu-id="1b959-253">此選項需要您建立新的 HDInsight 叢集，或使用現有的 HDInsight 叢集 hello Hive 資料表點 toohello NY 計程車資料在 Azure 資料湖存放區中的位置。</span><span class="sxs-lookup"><span data-stu-id="1b959-253">This option requires that you create a new HDInsight cluster or use an existing HDInsight cluster where hello Hive tables point toohello NY Taxi data in Azure Data Lake Storage.</span></span>  <span data-ttu-id="1b959-254">以下我們討論這兩個選項。</span><span class="sxs-lookup"><span data-stu-id="1b959-254">We discuss both these options below.</span></span> 

## <a name="option-1-use-python-toobuild-and-deploy-machine-learning-models"></a><span data-ttu-id="1b959-255">選項 1： 使用 Python toobuild 和部署的機器學習模型</span><span class="sxs-lookup"><span data-stu-id="1b959-255">Option 1: Use Python toobuild and deploy machine learning models</span></span>
<span data-ttu-id="1b959-256">toobuild 和部署使用 Python 的機器學習模型，建立 Jupyter 筆記本，在本機電腦上或在 Azure Machine Learning Studio 中。</span><span class="sxs-lookup"><span data-stu-id="1b959-256">toobuild and deploy machine learning models using Python, create a Jupyter Notebook on your local machine or in Azure Machine Learning Studio.</span></span> <span data-ttu-id="1b959-257">hello Jupyter 筆記本提供[GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough)包含 hello tooexplore 完整的程式碼，以視覺化方式檢視資料、 特徵設計、 模型和部署。</span><span class="sxs-lookup"><span data-stu-id="1b959-257">hello Jupyter Notebook  provided on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contains hello full code tooexplore, visualize data, feature engineering, modeling and deployment.</span></span> <span data-ttu-id="1b959-258">在本文中，我們會示範只 hello 模型和部署。</span><span class="sxs-lookup"><span data-stu-id="1b959-258">In this article, we show just hello modeling and deployment.</span></span> 

### <a name="import-python-libraries"></a><span data-ttu-id="1b959-259">匯入 Python 程式庫</span><span class="sxs-lookup"><span data-stu-id="1b959-259">Import Python libraries</span></span>
<span data-ttu-id="1b959-260">在訂單 toorun hello 範例 Jupyter 筆記本或 hello Python 指令碼檔案，hello 下列 Python 封裝所需。</span><span class="sxs-lookup"><span data-stu-id="1b959-260">In order toorun hello sample Jupyter Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="1b959-261">如果您使用 hello AzureML 筆記本服務，已預先安裝這些套件。</span><span class="sxs-lookup"><span data-stu-id="1b959-261">If you are using hello AzureML Notebook service, these packages have been pre-installed.</span></span>

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random
    import sklearn
    from sklearn.linear_model import LogisticRegression
    from sklearn.cross_validation import train_test_split
    from sklearn import metrics
    from __future__ import division
    from sklearn import linear_model
    from azureml import services


### <a name="read-in-hello-data-from-blob"></a><span data-ttu-id="1b959-262">讀取 hello 資料從 blob 中</span><span class="sxs-lookup"><span data-stu-id="1b959-262">Read in hello data from blob</span></span>
* <span data-ttu-id="1b959-263">連接字串</span><span class="sxs-lookup"><span data-stu-id="1b959-263">Connection String</span></span>   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* <span data-ttu-id="1b959-264">以文字形式讀取</span><span class="sxs-lookup"><span data-stu-id="1b959-264">Read in as text</span></span>
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds tooread in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* <span data-ttu-id="1b959-266">加入資料行名稱和分隔資料行</span><span class="sxs-lookup"><span data-stu-id="1b959-266">Add column names and separate columns</span></span>
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* <span data-ttu-id="1b959-267">變更一些資料行 toonumeric</span><span class="sxs-lookup"><span data-stu-id="1b959-267">Change some columns toonumeric</span></span>
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a><span data-ttu-id="1b959-268">建置機器學習服務模型</span><span class="sxs-lookup"><span data-stu-id="1b959-268">Build machine learning models</span></span>
<span data-ttu-id="1b959-269">這裡我們建立二元分類模型 toopredict 是否路線傾斜與否。</span><span class="sxs-lookup"><span data-stu-id="1b959-269">Here we build a binary classification model toopredict whether a trip is tipped or not.</span></span> <span data-ttu-id="1b959-270">在 [hello Jupyter 筆記本中，您可以找到其他兩個模型： 多級的分類和迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="1b959-270">In hello Jupyter Notebook you can find other two models: multiclass classification, and regression models.</span></span>

* <span data-ttu-id="1b959-271">首先我們需要 toocreate dummy 變數可以用於 scikit-了解模型</span><span class="sxs-lookup"><span data-stu-id="1b959-271">First we need toocreate dummy variables that can be used in scikit-learn models</span></span>
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* <span data-ttu-id="1b959-272">建立資料框架的 hello 模型化</span><span class="sxs-lookup"><span data-stu-id="1b959-272">Create data frame for hello modeling</span></span>
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* <span data-ttu-id="1b959-273">訓練和測試 60-40 分割</span><span class="sxs-lookup"><span data-stu-id="1b959-273">Training and testing 60-40 split</span></span>
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* <span data-ttu-id="1b959-274">訓練集中的羅吉斯迴歸</span><span class="sxs-lookup"><span data-stu-id="1b959-274">Logistic Regression in training set</span></span>
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* <span data-ttu-id="1b959-275">評分測試資料集</span><span class="sxs-lookup"><span data-stu-id="1b959-275">Score testing data set</span></span>
  
        Y_test_pred = logit_fit.predict(X_test)
* <span data-ttu-id="1b959-276">計算評估度量</span><span class="sxs-lookup"><span data-stu-id="1b959-276">Calculate Evaluation metrics</span></span>
  
        fpr_train, tpr_train, thresholds_train = metrics.roc_curve(Y_train, Y_train_pred)
        print fpr_train, tpr_train, thresholds_train
  
        fpr_test, tpr_test, thresholds_test = metrics.roc_curve(Y_test, Y_test_pred) 
        print fpr_test, tpr_test, thresholds_test
  
        #AUC
        print metrics.auc(fpr_train,tpr_train)
        print metrics.auc(fpr_test,tpr_test)
  
        #Confusion Matrix
        print metrics.confusion_matrix(Y_train,Y_train_pred)
        print metrics.confusion_matrix(Y_test,Y_test_pred)
  
       ![c2](./media/machine-learning-data-science-process-data-lake-walkthrough/c2-py-logit-evaluation.PNG)

### <a name="build-web-service-api-and-consume-it-in-python"></a><span data-ttu-id="1b959-277">建置 Web 服務 API 並在 Python 中使用</span><span class="sxs-lookup"><span data-stu-id="1b959-277">Build Web Service API and consume it in Python</span></span>
<span data-ttu-id="1b959-278">我們想要 toooperationalize hello 機器學習模型之後已建置。</span><span class="sxs-lookup"><span data-stu-id="1b959-278">We want toooperationalize hello machine learning model after it has been built.</span></span> <span data-ttu-id="1b959-279">這裡我們使用 hello 二進位羅吉斯模型做為範例。</span><span class="sxs-lookup"><span data-stu-id="1b959-279">Here we use hello binary logistic model as an example.</span></span> <span data-ttu-id="1b959-280">請確定 hello scikit-了解在您的本機版本 0.15.1。</span><span class="sxs-lookup"><span data-stu-id="1b959-280">Make sure hello scikit-learn version in your local machine is 0.15.1.</span></span> <span data-ttu-id="1b959-281">如果您使用 Azure ML studio 服務，您不需要關於此 tooworry。</span><span class="sxs-lookup"><span data-stu-id="1b959-281">You don't have tooworry about this if you use Azure ML studio service.</span></span>

* <span data-ttu-id="1b959-282">從 Azure ML Studio 設定中尋找您的工作區認證。</span><span class="sxs-lookup"><span data-stu-id="1b959-282">Find your workspace credentials from Azure ML studio settings.</span></span> <span data-ttu-id="1b959-283">在 Azure Machine Learning Studio 中，按一下 [設定] --> [名稱] --> [授權權杖]。</span><span class="sxs-lookup"><span data-stu-id="1b959-283">In Azure Machine Learning Studio, click **Settings** --> **Name** --> **Authorization Tokens**.</span></span> 
  
    ![c3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* <span data-ttu-id="1b959-285">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="1b959-285">Create Web Service</span></span>
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* <span data-ttu-id="1b959-286">取得 Web 服務認證</span><span class="sxs-lookup"><span data-stu-id="1b959-286">Get web service credentials</span></span>
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* <span data-ttu-id="1b959-287">呼叫 Web 服務 API。</span><span class="sxs-lookup"><span data-stu-id="1b959-287">Call Web service API.</span></span> <span data-ttu-id="1b959-288">您有 toowait 之後 hello 上一個步驟 5-10 秒。</span><span class="sxs-lookup"><span data-stu-id="1b959-288">You have toowait 5-10 seconds after hello previous step.</span></span>
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a><span data-ttu-id="1b959-289">選項 2：直接在 Azure Machine Learning 中建立和部署模型</span><span class="sxs-lookup"><span data-stu-id="1b959-289">Option 2: Create and deploy models directly in Azure Machine Learning</span></span>
<span data-ttu-id="1b959-290">Azure Machine Learning Studio 可以直接從 Azure 資料湖存放區讀取資料，然後是使用的 toocreate 並部署模型。</span><span class="sxs-lookup"><span data-stu-id="1b959-290">Azure Machine Learning Studio can read data directly from Azure Data Lake Store and then be used toocreate and deploy models.</span></span> <span data-ttu-id="1b959-291">這個方法會使用點的 Hive 資料表在 hello Azure 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="1b959-291">This approach uses a Hive table that points at hello Azure Data Lake Store.</span></span> <span data-ttu-id="1b959-292">這需要不同的 Azure HDInsight 叢集佈建、 哪些 hello 登錄區上建立資料表。</span><span class="sxs-lookup"><span data-stu-id="1b959-292">This requires that a separate Azure HDInsight cluster be provisioned, on which hello Hive table is created.</span></span> <span data-ttu-id="1b959-293">hello 下列各節顯示如何 toodo 這。</span><span class="sxs-lookup"><span data-stu-id="1b959-293">hello following sections show how toodo this.</span></span> 

### <a name="create-an-hdinsight-linux-cluster"></a><span data-ttu-id="1b959-294">建立 HDInsight Linux 叢集</span><span class="sxs-lookup"><span data-stu-id="1b959-294">Create an HDInsight Linux Cluster</span></span>
<span data-ttu-id="1b959-295">建立的 HDInsight 叢集 (Linux) 從 hello [Azure 入口網站](http://portal.azure.com)。如需詳細資訊，請參閱 hello**建立存取 tooAzure Data Lake Store 的 HDInsight 叢集**一節中[建立與使用 Azure 入口網站的 Data Lake Store 的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="1b959-295">Create an HDInsight Cluster (Linux) from hello [Azure Portal](http://portal.azure.com).For details, see hello **Create an HDInsight cluster with access tooAzure Data Lake Store** section in [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a><span data-ttu-id="1b959-297">在 HDInsight 中建立 Hive 資料表</span><span class="sxs-lookup"><span data-stu-id="1b959-297">Create Hive table in HDInsight</span></span>
<span data-ttu-id="1b959-298">現在我們可以建立使用 Azure Machine Learning Studio 中使用 hello 資料儲存在 Azure Data Lake Store hello 上一個步驟中的 hello HDInsight 叢集中的 Hive 資料表 toobe。</span><span class="sxs-lookup"><span data-stu-id="1b959-298">Now we create Hive tables toobe used in Azure Machine Learning Studio in hello HDInsight cluster using hello data stored in Azure Data Lake Store in hello previous step.</span></span> <span data-ttu-id="1b959-299">移 toohello 剛才建立的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="1b959-299">Go toohello HDInsight cluster just created.</span></span> <span data-ttu-id="1b959-300">按一下**設定** --> **屬性** --> **叢集 AAD 身分識別** --> **ADLS 存取**，請確定您的 Azure Data Lake Store 帳戶已新增在 hello 清單中具有讀取、 寫入及執行權限。</span><span class="sxs-lookup"><span data-stu-id="1b959-300">Click **Settings** --> **Properties** --> **Cluster AAD Identity** --> **ADLS Access**, make sure your Azure Data Lake Store account is added in hello list with read, write and execute rights.</span></span> 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

<span data-ttu-id="1b959-302">然後按一下 [**儀表板**下一步 toohello**設定**按鈕和視窗會隨即快顯。</span><span class="sxs-lookup"><span data-stu-id="1b959-302">Then click **Dashboard** next toohello **Settings** button and a window will pop up.</span></span> <span data-ttu-id="1b959-303">按一下**Hive 檢視**hello 在右上角的 hello 頁面，您將會看見 hello**查詢編輯器**。</span><span class="sxs-lookup"><span data-stu-id="1b959-303">Click **Hive View** in hello upper right corner of hello page and you will see hello **Query Editor**.</span></span>

 ![20](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

<span data-ttu-id="1b959-306">貼上下列 hello 的 Hive 指令碼 toocreate 資料表。</span><span class="sxs-lookup"><span data-stu-id="1b959-306">Paste in hello following Hive scripts toocreate a table.</span></span> <span data-ttu-id="1b959-307">資料來源的 hello 位置是在 Azure 資料湖存放區參考，以這種方式： **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**。</span><span class="sxs-lookup"><span data-stu-id="1b959-307">hello location of data source is in Azure Data Lake Store reference in this way: **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**.</span></span>

    CREATE EXTERNAL TABLE nyc_stratified_sample
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string,
      payment_type string,
      fare_amount string,
      surcharge string,
      mta_tax string,
      tolls_amount string,
      total_amount string,
      tip_amount string,
      tipped string,
      tip_class string,
      rownum string
      )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    LOCATION 'adl://data_lake_storage_name.azuredatalakestore.net:443/nyctaxi_folder/demo_ex_9_stratified_1_1000_copy.csv';


<span data-ttu-id="1b959-308">當 hello 查詢完成執行時，您會看到 hello 結果如下：</span><span class="sxs-lookup"><span data-stu-id="1b959-308">When hello query finishes running, you will see hello results like this:</span></span>

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a><span data-ttu-id="1b959-310">在 Azure Machine Learning Studio 中建置和部署模型</span><span class="sxs-lookup"><span data-stu-id="1b959-310">Build and deploy models in Azure Machine Learning Studio</span></span>
<span data-ttu-id="1b959-311">我們現在已準備好 toobuild 和部署一個模型來預測與 Azure Machine Learning 支付提示。</span><span class="sxs-lookup"><span data-stu-id="1b959-311">We are now ready toobuild and deploy a model that predicts whether or not a tip is paid with Azure Machine Learning.</span></span> <span data-ttu-id="1b959-312">hello 分層的取樣資料已準備好用於此二進位分類的 toobe （秘訣與否） 問題。</span><span class="sxs-lookup"><span data-stu-id="1b959-312">hello stratified sample data is ready toobe used in this binary classification (tip or not) problem.</span></span> <span data-ttu-id="1b959-313">hello 使用多級分類 (tip_class) 的預測模型和迴歸 (tip_amount) 可以也建置和部署與 Azure Machine Learning Studio 中，但這裡我們只會顯示如何 toohandle hello 案例使用 hello 二元分類模型。</span><span class="sxs-lookup"><span data-stu-id="1b959-313">hello predictive models using multiclass classification (tip_class) and regression (tip_amount) can also be built and deployed with Azure Machine Learning Studio, but here we only show how toohandle hello case using hello binary classification model.</span></span>

1. <span data-ttu-id="1b959-314">Hello 資料送入使用 hello Azure ML**匯入資料**模組，用於 hello**資料輸入和輸出**> 一節。</span><span class="sxs-lookup"><span data-stu-id="1b959-314">Get hello data into Azure ML using hello **Import Data** module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="1b959-315">如需詳細資訊，請參閱 hello[資料匯入模組](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/)參考頁面。</span><span class="sxs-lookup"><span data-stu-id="1b959-315">For more information, see hello [Import Data module](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) reference page.</span></span>
2. <span data-ttu-id="1b959-316">選取**Hive 查詢**為 hello**資料來源**在 hello**屬性**面板。</span><span class="sxs-lookup"><span data-stu-id="1b959-316">Select **Hive Query** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="1b959-317">下列在 hello 的 Hive 指令碼貼上 hello **Hive 資料庫查詢**編輯器</span><span class="sxs-lookup"><span data-stu-id="1b959-317">Paste hello following Hive script in hello **Hive database query** editor</span></span>
   
        select * from nyc_stratified_sample;
4. <span data-ttu-id="1b959-318">輸入 hello URI 的 HDInsight 叢集 （這可以找到在 Azure 入口網站），Hadoop 認證，輸出資料與 Azure 儲存體帳戶名稱/金鑰容器名稱的位置。</span><span class="sxs-lookup"><span data-stu-id="1b959-318">Enter hello URI of HDInsight cluster (this can be found in Azure Portal), Hadoop credentials, location of output data, and Azure storage account name/key/container name.</span></span>
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

<span data-ttu-id="1b959-320">二元分類實驗 Hive 資料表中讀取資料的範例所示 hello 圖。</span><span class="sxs-lookup"><span data-stu-id="1b959-320">An example of a binary classification experiment reading data from Hive table is shown in hello figure below.</span></span>

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

<span data-ttu-id="1b959-322">建立 hello 實驗之後，按一下**設定 Web 服務** --> **預測 Web 服務**</span><span class="sxs-lookup"><span data-stu-id="1b959-322">After hello experiment is created, click  **Set Up Web Service** --> **Predictive Web Service**</span></span>

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

<span data-ttu-id="1b959-324">完成時，計分實驗中，按一下 [自動建立的執行的 hello**部署 Web 服務**</span><span class="sxs-lookup"><span data-stu-id="1b959-324">Run hello automatically created scoring experiment, when it finishes, click **Deploy Web Service**</span></span>

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

<span data-ttu-id="1b959-326">將會很快顯示 hello web 服務儀表板：</span><span class="sxs-lookup"><span data-stu-id="1b959-326">hello web service dashboard will be displayed shortly:</span></span>

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a><span data-ttu-id="1b959-328">摘要</span><span class="sxs-lookup"><span data-stu-id="1b959-328">Summary</span></span>
<span data-ttu-id="1b959-329">完成這個逐步解說之後，您就已經建立了資料科學環境，可在 Azure Data Lake 中建置可調整的端對端解決方案。</span><span class="sxs-lookup"><span data-stu-id="1b959-329">By completing this walkthrough you have created a data science environment for building scalable end-to-end solutions in Azure Data Lake.</span></span> <span data-ttu-id="1b959-330">此環境中使用的 tooanalyze 大型公用資料集，使其透過 hello hello 資料科學程序，從資料擷取模型定型，透過標準步驟，然後 hello toohello 部署為 web 服務建立的模型。</span><span class="sxs-lookup"><span data-stu-id="1b959-330">This environment was used tooanalyze a large public dataset, taking it through hello canonical steps of hello Data Science Process, from data acquisition through model training, and then toohello deployment of hello model as a web service.</span></span> <span data-ttu-id="1b959-331">U-SQL 已使用的 tooprocess、 瀏覽和範例 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="1b959-331">U-SQL was used tooprocess, explore and sample hello data.</span></span> <span data-ttu-id="1b959-332">Python 和 Hive 與 Azure Machine Learning Studio toobuild 搭配使用，並將預測的模型部署。</span><span class="sxs-lookup"><span data-stu-id="1b959-332">Python and Hive were used with Azure Machine Learning Studio toobuild and deploy predictive models.</span></span>

## <a name="whats-next"></a><span data-ttu-id="1b959-333">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1b959-333">What's next?</span></span>
<span data-ttu-id="1b959-334">hello 學習路徑[小組資料科學程序 (TDSP)](http://aka.ms/datascienceprocess)提供 hello 進階分析程序中的連結 tootopics 描述每個步驟。</span><span class="sxs-lookup"><span data-stu-id="1b959-334">hello learning path for the [Team Data Science Process (TDSP)](http://aka.ms/datascienceprocess) provides links tootopics describing each step in hello advanced analytics process.</span></span> <span data-ttu-id="1b959-335">有一系列逐步解說分上 hello[小組資料科學程序的逐步解說](data-science-process-walkthroughs.md)頁面上，展示如何 toouse 資源和服務在不同的預測分析案例中：</span><span class="sxs-lookup"><span data-stu-id="1b959-335">There are a series of walkthroughs itemized on hello [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) page that showcase how toouse resources and services in various predictive analytics scenarios:</span></span>

* [<span data-ttu-id="1b959-336">在動作中的 hello 小組資料科學程序： 使用 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="1b959-336">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>](machine-learning-data-science-process-sqldw-walkthrough.md)
* [<span data-ttu-id="1b959-337">在動作中的 hello 小組資料科學程序： 使用 HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="1b959-337">hello Team Data Science Process in action: using HDInsight Hadoop clusters</span></span>](machine-learning-data-science-process-hive-walkthrough.md)
* [<span data-ttu-id="1b959-338">hello 小組資料科學程序： 使用 SQL Server</span><span class="sxs-lookup"><span data-stu-id="1b959-338">hello Team Data Science Process: using SQL Server</span></span>](machine-learning-data-science-process-sql-walkthrough.md)
* [<span data-ttu-id="1b959-339">Azure HDInsight 上二手 hello 資料科學程序使用的概觀</span><span class="sxs-lookup"><span data-stu-id="1b959-339">Overview of hello Data Science Process using Spark on Azure HDInsight</span></span>](machine-learning-data-science-spark-overview.md)

