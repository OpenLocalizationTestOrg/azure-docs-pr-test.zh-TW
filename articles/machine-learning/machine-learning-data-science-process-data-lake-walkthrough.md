---
title: "Azure Data Lake 中可調整的資料科學︰完整的逐步解說 | Microsoft Docs"
description: "如何使用 Azure Data Lake 在資料集上進行資料探索和二元分類工作。"
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
ms.openlocfilehash: 34fbe99572b4a6cee73de6ae5412a0ec09dd1ccc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a><span data-ttu-id="e26cb-103">Azure Data Lake 中可調整的資料科學︰完整的逐步解說</span><span class="sxs-lookup"><span data-stu-id="e26cb-103">Scalable Data Science with Azure Data Lake: An end-to-end Walkthrough</span></span>
<span data-ttu-id="e26cb-104">本逐步解說示範如何使用 Azure Data Lake，在 NYC 計程車車程和車費資料集上執行資料探索和二元分類，以預測一趟車程是否收費。</span><span class="sxs-lookup"><span data-stu-id="e26cb-104">This walkthrough shows how to use Azure Data Lake to do data exploration and binary classification tasks on a sample of the NYC taxi trip and fare dataset to predict whether or not a tip will be paid by a fare.</span></span> <span data-ttu-id="e26cb-105">其中，從取得資料開始，經過模型訓練，然後部署 Web 服務來發佈模型，從頭到尾逐步引導您完成 [Team Data Science Process](http://aka.ms/datascienceprocess)。</span><span class="sxs-lookup"><span data-stu-id="e26cb-105">It walks you through the steps of the [Team Data Science Process](http://aka.ms/datascienceprocess), end-to-end, from data acquisition to model training, and then to the deployment of a web service that publishes the model.</span></span>

### <a name="azure-data-lake-analytics"></a><span data-ttu-id="e26cb-106">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="e26cb-106">Azure Data Lake Analytics</span></span>
<span data-ttu-id="e26cb-107">[Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) 具備所有必要的功能，讓資料科學家能夠輕易地儲存任何大小、形狀和速度的資料，並以高延展性且符合成本效益的方式，進行資料處理、進階分析和建構機器學習服務模型。</span><span class="sxs-lookup"><span data-stu-id="e26cb-107">The [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) has all the capabilities required to make it easy for data scientists to store data of any size, shape and speed, and to conduct data processing, advanced analytics, and machine learning modeling with high scalability in a cost-effective way.</span></span>   <span data-ttu-id="e26cb-108">只在實際處理資料時，才需要依個別作業付費。</span><span class="sxs-lookup"><span data-stu-id="e26cb-108">You pay on a per-job basis, only when data is actually being processed.</span></span> <span data-ttu-id="e26cb-109">Azure Data Lake Analytics 包括 U-SQL，此語言融合 SQL 的宣告性質和 C# 表達能力，提供可調整的分散式查詢功能。</span><span class="sxs-lookup"><span data-stu-id="e26cb-109">Azure Data Lake Analytics includes U-SQL, a language that blends the declarative nature of SQL with the expressive power of C# to provide scalable distributed query capability.</span></span> <span data-ttu-id="e26cb-110">它可讓您在讀取、插入自訂邏輯和使用者定義函數 (UDF) 上套用結構描述，以處理非結構化資料，並包含擴充性，可精細控制如何大規模執行。</span><span class="sxs-lookup"><span data-stu-id="e26cb-110">It enables you to process unstructured data by applying schema on read, insert custom logic and user defined functions (UDFs), and includes extensibility to enable fine grained control over how to execute at scale.</span></span> <span data-ttu-id="e26cb-111">若要深入了解 U-SQL 背後的設計原理，請參閱 [Visual Studio 部落格文章](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/)。</span><span class="sxs-lookup"><span data-stu-id="e26cb-111">To learn more about the design philosophy behind U-SQL, see [Visual Studio blog post](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

<span data-ttu-id="e26cb-112">Data Lake Analytics 也是 Cortana Analytics 套件的重要組成部分，可搭配 Azure SQL 資料倉儲、Power BI 與 Data Factory 一起使用。</span><span class="sxs-lookup"><span data-stu-id="e26cb-112">Data Lake Analytics is also a key part of Cortana Analytics Suite and works with Azure SQL Data Warehouse, Power BI, and Data Factory.</span></span> <span data-ttu-id="e26cb-113">這讓您有一個完整的雲端巨量資料和進階分析平台。</span><span class="sxs-lookup"><span data-stu-id="e26cb-113">This gives you a complete cloud big data and advanced analytics platform.</span></span>

<span data-ttu-id="e26cb-114">本逐步解說首先描述使用 Data Lake Analytics 完成工作所需的必要條件和資源，以構成資料科學程序，並說明如何安裝這些資源。</span><span class="sxs-lookup"><span data-stu-id="e26cb-114">This walkthrough begins by describing the prerequisites and resources that are needed to complete the tasks with Data Lake Analytics that form the data science process and how to install them.</span></span> <span data-ttu-id="e26cb-115">接著，將概述使用 U-SQL 的資料處理步驟，最後將示範如何搭配 Azure Machine Learning Studio 使用 Python 和 Hive 來建置和部署預測模型。</span><span class="sxs-lookup"><span data-stu-id="e26cb-115">Then it outlines the data processing steps using U-SQL and concludes by showing how to use Python and Hive with Azure Machine Learning Studio to build and deploy the predictive models.</span></span> 

### <a name="u-sql-and-visual-studio"></a><span data-ttu-id="e26cb-116">U-SQL 和 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e26cb-116">U-SQL and Visual Studio</span></span>
<span data-ttu-id="e26cb-117">本逐步解說建議使用 Visual Studio 編輯 U-SQL 指令碼來處理資料集。</span><span class="sxs-lookup"><span data-stu-id="e26cb-117">This walkthrough recommends using Visual Studio to edit U-SQL scripts to process the dataset.</span></span> <span data-ttu-id="e26cb-118">這些 U-SQL 指令碼說明於此，也在個別檔案中提供 。</span><span class="sxs-lookup"><span data-stu-id="e26cb-118">The U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="e26cb-119">過程包括擷取、探索和取樣資料。</span><span class="sxs-lookup"><span data-stu-id="e26cb-119">The process includes ingesting, exploring, and sampling the data.</span></span> <span data-ttu-id="e26cb-120">同時還會示範如何從 Azure 入口網站執行 U-SQL 指令碼作業。</span><span class="sxs-lookup"><span data-stu-id="e26cb-120">It also shows how to run a U-SQL scripted job from the Azure portal.</span></span> <span data-ttu-id="e26cb-121">相關聯的 HDInsight 叢集中會為資料建立 Hive 資料表，以利於 Azure Machine Learning Studio 中建置和部署二元分類模型。</span><span class="sxs-lookup"><span data-stu-id="e26cb-121">Hive tables are created for the data in an associated HDInsight cluster to facilitate the building and deployment of a binary classification model in Azure Machine Learning Studio.</span></span>  

### <a name="python"></a><span data-ttu-id="e26cb-122">Python</span><span class="sxs-lookup"><span data-stu-id="e26cb-122">Python</span></span>
<span data-ttu-id="e26cb-123">本逐步解說也包含一個小節，示範如何搭配 Azure Machine Learning Studio 使用 Python 來建置和部署預測模型。</span><span class="sxs-lookup"><span data-stu-id="e26cb-123">This walkthrough also contains a section that shows how to build and deploy a predictive model using Python with Azure Machine Learning Studio.</span></span>  <span data-ttu-id="e26cb-124">我們針對此程序中的這些步驟提供 Jupyter Notebook 和 Python 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e26cb-124">We provide a Jupyter notebook with the Python scripts for these steps in this process.</span></span> <span data-ttu-id="e26cb-125">除了此處所述的二元分類模型，此 Notebook 還包含一些額外特徵工程步驟和模型建構的程式碼，例如多類別分類和迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="e26cb-125">The notebook includes code for some additional feature engineering steps and models construction such as multiclass classification and regression modeling in addition to the binary classification model outlined here.</span></span> <span data-ttu-id="e26cb-126">迴歸工作是根據其他小費特徵來預測小費金額。</span><span class="sxs-lookup"><span data-stu-id="e26cb-126">The regression task is to predict the amount of the tip based on other tip features.</span></span> 

### <a name="azure-machine-learning"></a><span data-ttu-id="e26cb-127">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e26cb-127">Azure Machine Learning</span></span>
<span data-ttu-id="e26cb-128">Azure Machine Learning Studio 可用來建置和部署預測模型。</span><span class="sxs-lookup"><span data-stu-id="e26cb-128">Azure Machine Learning Studio is used to build and deploy the predictive models.</span></span> <span data-ttu-id="e26cb-129">這是使用下列兩種方法來完成︰首先會使用 Python 指令碼，接著使用 HDInsight (Hadoop) 叢集上的 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="e26cb-129">This is done using two approaches: first with Python scripts and then with Hive tables on an HDInsight (Hadoop) cluster.</span></span>

### <a name="scripts"></a><span data-ttu-id="e26cb-130">指令碼</span><span class="sxs-lookup"><span data-stu-id="e26cb-130">Scripts</span></span>
<span data-ttu-id="e26cb-131">本逐步解說只概述主要步驟。</span><span class="sxs-lookup"><span data-stu-id="e26cb-131">Only the principal steps are outlined in this walkthrough.</span></span> <span data-ttu-id="e26cb-132">您可以從 [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) 下載完整的 **U-SQL 指令碼**和 **Jupyter Notebook**。</span><span class="sxs-lookup"><span data-stu-id="e26cb-132">You can download the full **U-SQL script** and **Jupyter Notebook** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e26cb-133">必要條件</span><span class="sxs-lookup"><span data-stu-id="e26cb-133">Prerequisites</span></span>
<span data-ttu-id="e26cb-134">開始運用這些主題之前，您必須符合下列條件：</span><span class="sxs-lookup"><span data-stu-id="e26cb-134">Before you begin these topics, you must have the following:</span></span>

* <span data-ttu-id="e26cb-135">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e26cb-135">An Azure subscription.</span></span> <span data-ttu-id="e26cb-136">如果還沒有訂用帳戶，請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="e26cb-136">If you do not already have one, see [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="e26cb-137">[建議] Visual Studio 2013 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="e26cb-137">[Recommended] Visual Studio 2013 or later.</span></span> <span data-ttu-id="e26cb-138">如果您還沒有安裝這些版本的其中一個，您可以從 [Visual Studio 社群](https://www.visualstudio.com/vs/community/)下載免費的社群版本。</span><span class="sxs-lookup"><span data-stu-id="e26cb-138">If you do not already have one of these versions installed, you can download a free Community version from [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span></span>

> [!NOTE]
> <span data-ttu-id="e26cb-139">除了 Visual Studio，您也可以使用 Azure 入口網站提交 Azure Data Lake 查詢。</span><span class="sxs-lookup"><span data-stu-id="e26cb-139">Instead of Visual Studio, you can also use the Azure Portal to submit Azure Data Lake queries.</span></span> <span data-ttu-id="e26cb-140">我們將在 **使用 U-SQL 處理資料**一節中提供指示，說明如何使用 Visual Studio 以及在入口網站上執行此動作。</span><span class="sxs-lookup"><span data-stu-id="e26cb-140">We will provide instructions on how to do so both with Visual Studio and on the portal in the section titled **Process data with U-SQL**.</span></span> 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a><span data-ttu-id="e26cb-141">準備 Azure Data Lake 的資料科學環境</span><span class="sxs-lookup"><span data-stu-id="e26cb-141">Prepare data science environment for Azure Data Lake</span></span>
<span data-ttu-id="e26cb-142">若要準備本逐步解說的資料科學環境，請建立下列資源︰</span><span class="sxs-lookup"><span data-stu-id="e26cb-142">To prepare the data science environment for this walkthrough, create the following resources:</span></span>

* <span data-ttu-id="e26cb-143">Azure Data Lake Store (ADLS)</span><span class="sxs-lookup"><span data-stu-id="e26cb-143">Azure Data Lake Store (ADLS)</span></span> 
* <span data-ttu-id="e26cb-144">Azure Data Lake Analytics (ADLA)</span><span class="sxs-lookup"><span data-stu-id="e26cb-144">Azure Data Lake Analytics (ADLA)</span></span>
* <span data-ttu-id="e26cb-145">Azure Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e26cb-145">Azure Blob storage account</span></span>
* <span data-ttu-id="e26cb-146">Azure Machine Learning Studio 帳戶</span><span class="sxs-lookup"><span data-stu-id="e26cb-146">Azure Machine Learning Studio account</span></span>
* <span data-ttu-id="e26cb-147">Azure Data Lake Tools for Visual Studio (建議)</span><span class="sxs-lookup"><span data-stu-id="e26cb-147">Azure Data Lake Tools for Visual Studio (Recommended)</span></span>

<span data-ttu-id="e26cb-148">本節提供如何建立這些資源的指示。</span><span class="sxs-lookup"><span data-stu-id="e26cb-148">This section provides instructions on how to create each of these resources.</span></span> <span data-ttu-id="e26cb-149">如果您選擇搭配 Azure Machine Learning 使用 Hive 資料表 (而不是 Python) 來建置模型，您也必須佈建 HDInsight (Hadoop) 叢集。</span><span class="sxs-lookup"><span data-stu-id="e26cb-149">If you choose to use Hive tables with Azure Machine Learning, instead of Python, to build a model,you will also need to provision an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="e26cb-150">這個替代程序將於後續的適當小節中加以說明。</span><span class="sxs-lookup"><span data-stu-id="e26cb-150">This alternative procedure in described in the appropriate section below.</span></span>


> [!NOTE]
> <span data-ttu-id="e26cb-151">**Azure Data Lake Store** 可以個別建立，或者當您建立 **Azure Data Lake Analytics** 做為預設儲存體時加以建立。</span><span class="sxs-lookup"><span data-stu-id="e26cb-151">The **Azure Data Lake Store** can be created either separately or when you create the **Azure Data Lake Analytics** as the default storage.</span></span> <span data-ttu-id="e26cb-152">以下的參考指示會個別建立這其中的每一個資源，但不需要個別建立 Data Lake 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e26cb-152">Instructions are referenced for creating each of these resources separately below, but the Data Lake storage account need not be created separately.</span></span>
>
> 

### <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="e26cb-153">建立 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e26cb-153">Create an Azure Data Lake Store</span></span>


<span data-ttu-id="e26cb-154">從 [Azure 入口網站](http://portal.azure.com)建立 ADLS。</span><span class="sxs-lookup"><span data-stu-id="e26cb-154">Create an ADLS from the [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="e26cb-155">如需詳細資訊，請參閱 [使用 Azure 入口網站建立 HDInsight 叢集與 Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="e26cb-155">For details, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="e26cb-156">請務必依該文件所述，在 [選擇性組態] 刀鋒視窗的 [資料來源] 刀鋒視窗中設定 [叢集 AAD 身分識別]。</span><span class="sxs-lookup"><span data-stu-id="e26cb-156">Be sure to set up the Cluster AAD Identity in the **DataSource** blade of the **Optional Configuration** blade described there.</span></span> 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a><span data-ttu-id="e26cb-158">建立 Azure Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="e26cb-158">Create an Azure Data Lake Analytics account</span></span>
<span data-ttu-id="e26cb-159">從 [Azure 入口網站](http://portal.azure.com)建立 ADLA 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e26cb-159">Create an ADLA account from the [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="e26cb-160">如需詳細資訊，請參閱 [教學課程：使用 Azure 入口網站開始使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="e26cb-160">For details, see [Tutorial: get started with Azure Data Lake Analytics using Azure Portal](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span> 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="e26cb-162">建立 Azure Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e26cb-162">Create an Azure Blob storage account</span></span>
<span data-ttu-id="e26cb-163">從 [Azure 入口網站](http://portal.azure.com)建立 Azure Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e26cb-163">Create an Azure Blob storage account from the [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="e26cb-164">如需詳細資訊，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)中的＜建立儲存體帳戶＞一節。</span><span class="sxs-lookup"><span data-stu-id="e26cb-164">For details, see the Create a storage account section in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a><span data-ttu-id="e26cb-166">設定 Azure Machine Learning Studio 帳戶</span><span class="sxs-lookup"><span data-stu-id="e26cb-166">Set up an Azure Machine Learning Studio account</span></span>
<span data-ttu-id="e26cb-167">從 [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) 頁面註冊/登入 Azure Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="e26cb-167">Sign up/into Azure Machine Learning Studio from the [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) page.</span></span> <span data-ttu-id="e26cb-168">按一下 [立即開始使用] 按鈕，然後選擇 [免費工作區] 或 [標準工作區]。</span><span class="sxs-lookup"><span data-stu-id="e26cb-168">Click on the **Get started now** button and then choose a "Free Workspace" or "Standard Workspace".</span></span> <span data-ttu-id="e26cb-169">之後，您就能夠在 Azure ML Studio 中建立實驗。</span><span class="sxs-lookup"><span data-stu-id="e26cb-169">After this you will be able to create experiments in Azure ML Studio.</span></span>  

### <a name="install-azure-data-lake-tools-recommended"></a><span data-ttu-id="e26cb-170">安裝 Azure Data Lake 工具 [建議]</span><span class="sxs-lookup"><span data-stu-id="e26cb-170">Install Azure Data Lake Tools [Recommended]</span></span>
<span data-ttu-id="e26cb-171">依照您的 Visual Studio 版本，從 [Azure Data Lake Tools for Visual Studio (Visual Studio 適用的 Azure Data Lake 工具)](https://www.microsoft.com/download/details.aspx?id=49504)中安裝適合的 Azure Data Lake 工具。</span><span class="sxs-lookup"><span data-stu-id="e26cb-171">Install Azure Data Lake Tools for your version of Visual Studio from [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

<span data-ttu-id="e26cb-173">在成功完成安裝之後，開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="e26cb-173">After the installation finishes successfully, open up Visual Studio.</span></span> <span data-ttu-id="e26cb-174">您在頂端的功能表應該會看到 Data Lake 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e26cb-174">You should see the Data Lake tab the menu at the top.</span></span> <span data-ttu-id="e26cb-175">當您登入 Azure 帳戶時，您的 Azure 資源應該會出現在左面板中。</span><span class="sxs-lookup"><span data-stu-id="e26cb-175">Your Azure resources should appear in the left panel when you sign into your Azure account.</span></span>

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="the-nyc-taxi-trips-dataset"></a><span data-ttu-id="e26cb-177">NYC 計程車車程資料集</span><span class="sxs-lookup"><span data-stu-id="e26cb-177">The NYC Taxi Trips dataset</span></span>
<span data-ttu-id="e26cb-178">我們在此處使用的資源集是公開可用的資料集 -- [NYC Taxi Trips (NYC 計程車車程)](http://www.andresmh.com/nyctaxitrips/)資料集。</span><span class="sxs-lookup"><span data-stu-id="e26cb-178">The data set we used here is a publicly available dataset -- the [NYC Taxi Trips dataset](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="e26cb-179">「NYC 計程車車程」資料是由約 20GB 的 CSV 壓縮檔 (未壓縮時可達 48GB) 所組成，裡面記錄了超過 1 億 7300 萬筆個別車程及針對每趟車程所支付的費用。</span><span class="sxs-lookup"><span data-stu-id="e26cb-179">The NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="e26cb-180">每趟車程記錄包括上車和下車的位置與時間、匿名的計程車司機駕照號碼，以及計程車牌照 (計程車的唯一識別碼) 號碼。</span><span class="sxs-lookup"><span data-stu-id="e26cb-180">Each trip record includes the pickup and drop-off locations and times, anonymized hack (driver's) license number, and the medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="e26cb-181">資料涵蓋 2013 年的所有車程，並且每月會在下列兩個資料集中加以提供：</span><span class="sxs-lookup"><span data-stu-id="e26cb-181">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

* <span data-ttu-id="e26cb-182">「trip_data」CSV 檔案包含車程的詳細資訊，例如，乘客數、上車和下車地點、車程持續時間，以及車程長度。</span><span class="sxs-lookup"><span data-stu-id="e26cb-182">The 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="e26cb-183">以下是一些範例記錄：</span><span class="sxs-lookup"><span data-stu-id="e26cb-183">Here are a few sample records:</span></span>
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* <span data-ttu-id="e26cb-184">「trip_fare」CSV 檔案包含針對每趟車程所支付之費用的詳細資訊，例如付款類型、費用金額、銷售稅和稅金、小費和服務費，以及支付的總金額。</span><span class="sxs-lookup"><span data-stu-id="e26cb-184">The 'trip_fare' CSV contains details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="e26cb-185">以下是一些範例記錄：</span><span class="sxs-lookup"><span data-stu-id="e26cb-185">Here are a few sample records:</span></span>
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="e26cb-186">聯結 trip\_data 和 trip\_fare 的唯一索引鍵是由下列三個欄位所組成：medallion、hack\_license 和 pickup\_datetime。</span><span class="sxs-lookup"><span data-stu-id="e26cb-186">The unique key to join trip\_data and trip\_fare is composed of the following three fields: medallion, hack\_license and pickup\_datetime.</span></span> <span data-ttu-id="e26cb-187">從公用 Azure 儲存體 blob 中可以存取原始 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="e26cb-187">The raw CSV files can be accessed from a public Azure storage blob.</span></span> <span data-ttu-id="e26cb-188">適用於此聯結的 U-SQL 指令碼位於 [聯結車程和費用資料表](#join) 一節中。</span><span class="sxs-lookup"><span data-stu-id="e26cb-188">The U-SQL script for this join is in the [Join trip and fare tables](#join) section.</span></span>

## <a name="process-data-with-u-sql"></a><span data-ttu-id="e26cb-189">使用 U-SQL 處理資料</span><span class="sxs-lookup"><span data-stu-id="e26cb-189">Process data with U-SQL</span></span>
<span data-ttu-id="e26cb-190">本節所述的資料處理工作包括擷取、檢查品質、探索和取樣資料。</span><span class="sxs-lookup"><span data-stu-id="e26cb-190">The data processing tasks illustrated in this section include ingesting, checking quality, exploring, and sampling the data.</span></span> <span data-ttu-id="e26cb-191">我們也說明如何聯結車程和費用資料表。</span><span class="sxs-lookup"><span data-stu-id="e26cb-191">We also show how to join trip and fare tables.</span></span> <span data-ttu-id="e26cb-192">最後一節說明從 Azure 入口網站執行 U-SQL 指令碼作業。</span><span class="sxs-lookup"><span data-stu-id="e26cb-192">The final section shows run a U-SQL scripted job from the Azure portal.</span></span> <span data-ttu-id="e26cb-193">以下是各小節的連結︰</span><span class="sxs-lookup"><span data-stu-id="e26cb-193">Here are links to each subsection:</span></span>

* [<span data-ttu-id="e26cb-194">資料擷取：從公用 blob 讀取資料</span><span class="sxs-lookup"><span data-stu-id="e26cb-194">Data ingestion: read in data from public blob</span></span>](#ingest)
* [<span data-ttu-id="e26cb-195">資料品質檢查</span><span class="sxs-lookup"><span data-stu-id="e26cb-195">Data quality checks</span></span>](#quality)
* [<span data-ttu-id="e26cb-196">資料探索</span><span class="sxs-lookup"><span data-stu-id="e26cb-196">Data exploration</span></span>](#explore)
* [<span data-ttu-id="e26cb-197">如何聯結車程和費用資料表</span><span class="sxs-lookup"><span data-stu-id="e26cb-197">Join trip and fare tables</span></span>](#join)
* [<span data-ttu-id="e26cb-198">資料取樣</span><span class="sxs-lookup"><span data-stu-id="e26cb-198">Data sampling</span></span>](#sample)
* [<span data-ttu-id="e26cb-199">執行 U-SQL 作業</span><span class="sxs-lookup"><span data-stu-id="e26cb-199">Run U-SQL jobs</span></span>](#run)

<span data-ttu-id="e26cb-200">這些 U-SQL 指令碼說明於此，也在個別檔案中提供 。</span><span class="sxs-lookup"><span data-stu-id="e26cb-200">The U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="e26cb-201">您可以從 **GitHub** 下載完整的 [U-SQL 指令碼](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough)。</span><span class="sxs-lookup"><span data-stu-id="e26cb-201">You can download the full **U-SQL scripts** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

<span data-ttu-id="e26cb-202">若要執行 U-SQL，請開啟 Visual Studio、按一下 [檔案] --> [新增] --> [專案]、選擇 [U-SQL 專案]，命名並儲存到資料夾。</span><span class="sxs-lookup"><span data-stu-id="e26cb-202">To execute U-SQL, Open Visual Studio, click **File --> New --> Project**, choose **U-SQL Project**, name and save it to a folder.</span></span>

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> <span data-ttu-id="e26cb-204">您可以使用 Azure 入口網站來執行 U-SQL，而不是 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="e26cb-204">It is possible to use the Azure Portal to execute U-SQL instead of Visual Studio.</span></span> <span data-ttu-id="e26cb-205">您可以瀏覽到入口網站上的 Azure Data Lake Analytics 資源並直接提交查詢 (如下圖所示)。</span><span class="sxs-lookup"><span data-stu-id="e26cb-205">You can navigate to the Azure Data Lake Analytics resource on the portal and submit queries directly as illustrated in the following figure.</span></span>
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <span data-ttu-id="e26cb-207"><a name="ingest"></a>資料擷取：從公用 Blob 讀取資料</span><span class="sxs-lookup"><span data-stu-id="e26cb-207"><a name="ingest"></a>Data Ingestion: Read in data from public blob</span></span>
<span data-ttu-id="e26cb-208">Azure Blob 中的資料位置是以 **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** 來參考，可透過 **Extractors.Csv()** 來擷取。</span><span class="sxs-lookup"><span data-stu-id="e26cb-208">The location of the data in the Azure blob is referenced as **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** and can be extracted using **Extractors.Csv()**.</span></span> <span data-ttu-id="e26cb-209">在下列指令碼中，以您自己的容器名稱和儲存體帳戶名稱來替換 wasb 位址中的 container_name@blob_storage_account_name。</span><span class="sxs-lookup"><span data-stu-id="e26cb-209">Substitute your own container name and storage account name in following scripts for container_name@blob_storage_account_name in the wasb address.</span></span> <span data-ttu-id="e26cb-210">由於檔案名稱的格式相同，因此我們可以使用 **trip\_data_{\*\}.csv** 來讀取全部 12 個車程檔案。</span><span class="sxs-lookup"><span data-stu-id="e26cb-210">Since the file names are in same format, we can use **trip\_data_{\*\}.csv** to read in all 12 trip files.</span></span> 

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

<span data-ttu-id="e26cb-211">由於第一列有標頭，我們必須移除標頭，並將資料行類型變更為適當的類型。</span><span class="sxs-lookup"><span data-stu-id="e26cb-211">Since there are headers in the first row, we need to remove the headers and change column types into appropriate ones.</span></span> <span data-ttu-id="e26cb-212">我們可以使用 **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_，將已處理的資料儲存至 Azure Data Lake 儲存體，或使用 **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**，儲存至 Azure Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e26cb-212">We can either save the processed data to Azure Data Lake Storage using **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ or to Azure Blob storage account using  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**.</span></span> 

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

    ////output data to ADL
    OUTPUT @trip   
    TO "swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data to blob
    OUTPUT @trip   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

<span data-ttu-id="e26cb-213">同樣地，我們可以讀取費用資料集。</span><span class="sxs-lookup"><span data-stu-id="e26cb-213">Similarly we can read in the fare data sets.</span></span> <span data-ttu-id="e26cb-214">以滑鼠右鍵按一下 [Azure Data Lake Store]，您可以選擇在 [Azure 入口網站] --> [資料總管] 或 Visual Studio 內的 [檔案總管] 中查看您的資料。</span><span class="sxs-lookup"><span data-stu-id="e26cb-214">Right click Azure Data Lake Store, you can choose to look at your data in **Azure Portal --> Data Explorer** or **File Explorer** within Visual Studio.</span></span> 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <span data-ttu-id="e26cb-217"><a name="quality"></a>資料品質檢查</span><span class="sxs-lookup"><span data-stu-id="e26cb-217"><a name="quality"></a>Data quality checks</span></span>
<span data-ttu-id="e26cb-218">讀取車程和費用資料表之後，即可依下列方式檢查資料品質。</span><span class="sxs-lookup"><span data-stu-id="e26cb-218">After trip and fare tables have been read in, data quality checks can be done in the following way.</span></span> <span data-ttu-id="e26cb-219">產生的 CSV 檔案可以輸出至 Azure Blob 儲存體或 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="e26cb-219">The resulting CSV files can be output to Azure Blob storage or Azure Data Lake Store.</span></span> 

<span data-ttu-id="e26cb-220">尋找獎章數目和卓越的獎章數目：</span><span class="sxs-lookup"><span data-stu-id="e26cb-220">Find the number of medallions and unique number of medallions:</span></span>

    ///check the number of medallions and unique number of medallions
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
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="e26cb-221">尋找有超過 100 個車程的牌照：</span><span class="sxs-lookup"><span data-stu-id="e26cb-221">Find those medallions that had more than 100 trips:</span></span>

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="e26cb-222">找到 pickup_longitude 方面的無效記錄︰</span><span class="sxs-lookup"><span data-stu-id="e26cb-222">Find those invalid records in terms of pickup_longitude:</span></span>

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="e26cb-223">尋找一些變數的遺漏值︰</span><span class="sxs-lookup"><span data-stu-id="e26cb-223">Find missing values for some variables:</span></span>

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
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <span data-ttu-id="e26cb-224"><a name="explore"></a>資料探索</span><span class="sxs-lookup"><span data-stu-id="e26cb-224"><a name="explore"></a>Data exploration</span></span>
<span data-ttu-id="e26cb-225">我們稍微探索資料以更充分了解資料。</span><span class="sxs-lookup"><span data-stu-id="e26cb-225">We can do some data exploration to get a better understanding of the data.</span></span>

<span data-ttu-id="e26cb-226">尋找有小費和無小費車程的分佈︰</span><span class="sxs-lookup"><span data-stu-id="e26cb-226">Find the distribution of tipped and non-tipped trips:</span></span>

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
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="e26cb-227">尋找有截止值的小費金額分佈︰0、5、10 和 20 美金。</span><span class="sxs-lookup"><span data-stu-id="e26cb-227">Find the distribution of tip amount with cut-off values: 0,5,10,and 20 dollars.</span></span>

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
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="e26cb-228">尋找車程距離的基本統計資料︰</span><span class="sxs-lookup"><span data-stu-id="e26cb-228">Find basic statistics of trip distance:</span></span>

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
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

<span data-ttu-id="e26cb-229">尋找車程距離的百分位數︰</span><span class="sxs-lookup"><span data-stu-id="e26cb-229">Find the percentiles of trip distance:</span></span>

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="e26cb-230"><a name="join"></a>聯結車程和費用資料表</span><span class="sxs-lookup"><span data-stu-id="e26cb-230"><a name="join"></a>Join trip and fare tables</span></span>
<span data-ttu-id="e26cb-231">車程和費用資料表可以由 medallion、hack_license 和 pickup_time 聯結。</span><span class="sxs-lookup"><span data-stu-id="e26cb-231">Trip and fare tables can be joined by medallion, hack_license, and pickup_time.</span></span>

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output to blob
    OUTPUT @model_data_full   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data to ADL
    OUTPUT @model_data_full   
    TO "swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


<span data-ttu-id="e26cb-232">對於每個層級的乘客計數，計算記錄數、平均小費金額、小費金額變異數、小費車程的百分比。</span><span class="sxs-lookup"><span data-stu-id="e26cb-232">For each level of passenger count, calculate the number of records, average tip amount, variance of tip amount, percentage of tipped trips.</span></span>

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
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <span data-ttu-id="e26cb-233"><a name="sample"></a>資料取樣</span><span class="sxs-lookup"><span data-stu-id="e26cb-233"><a name="sample"></a>Data sampling</span></span>
<span data-ttu-id="e26cb-234">首先，我們從聯結的資料表隨機選取 0.1% 的資料︰</span><span class="sxs-lookup"><span data-stu-id="e26cb-234">First we randomly select 0.1% of the data from the joined table:</span></span>

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
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="e26cb-235">接著，我們以二元變數 tip_class 進行分層取樣：</span><span class="sxs-lookup"><span data-stu-id="e26cb-235">Then we do stratified sampling by binary variable tip_class:</span></span>

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output to blob
    OUTPUT @model_data_stratified_sample_1_1000   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data to ADL
    OUTPUT @model_data_stratified_sample_1_1000   
    TO "swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="e26cb-236"><a name="run"></a>執行 U-SQL 作業</span><span class="sxs-lookup"><span data-stu-id="e26cb-236"><a name="run"></a>Run U-SQL jobs</span></span>
<span data-ttu-id="e26cb-237">完成編輯 U-SQL 指令碼時，您可以使用 Azure Data Lake Analytics 帳戶將它們提交到伺服器。</span><span class="sxs-lookup"><span data-stu-id="e26cb-237">When you finish editing U-SQL scripts, you can submit them to the server using your Azure Data Lake Analytics account.</span></span> <span data-ttu-id="e26cb-238">依序按一下 [Data Lake] 和 [提交作業]，並選取您的 [Analytics 帳戶]，然後選擇 [平行處理原則]，再按一下 [提交] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e26cb-238">Click **Data Lake**, **Submit Job**, select your **Analytics Account**, choose **Parallelism**, and click **Submit** button.</span></span>  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

<span data-ttu-id="e26cb-240">成功編譯作業後，您作業的狀態會顯示在 Visual Studio 中供您監視。</span><span class="sxs-lookup"><span data-stu-id="e26cb-240">When the job is complied successfully, the status of your job will be displayed in Visual Studio for monitoring.</span></span> <span data-ttu-id="e26cb-241">作業執行完成後，您甚至可以重播作業執行程序，找出瓶頸步驟來提升作業效率。</span><span class="sxs-lookup"><span data-stu-id="e26cb-241">After the job finishes running, you can even replay the job execution process and find out the bottleneck steps to improve your job efficiency.</span></span> <span data-ttu-id="e26cb-242">您也可以移至 Azure 入口網站來檢查 U-SQL 作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="e26cb-242">You can also go to Azure Portal to check the status of your U-SQL jobs.</span></span>

 ![13](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

<span data-ttu-id="e26cb-245">現在，您可以在 Azure Blob 儲存體或 Azure 入口網站中檢查輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="e26cb-245">Now you can check the output files in either Azure Blob storage or Azure Portal.</span></span> <span data-ttu-id="e26cb-246">在下一個步驟中，我們將在模型中使用分層取樣資料。</span><span class="sxs-lookup"><span data-stu-id="e26cb-246">We will use the stratified sample data for our modeling in the next step.</span></span>

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a><span data-ttu-id="e26cb-249">在 Azure Machine Learning 中建置和部署模型</span><span class="sxs-lookup"><span data-stu-id="e26cb-249">Build and deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="e26cb-250">我們將示範兩個可用的選項，讓您可將資料提取到要建置的 Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e26cb-250">We demonstrate two options available for you to pull data into Azure Machine Learning to build and</span></span> 

* <span data-ttu-id="e26cb-251">在第一個選項中，您可以使用已寫入 Azure Blob 的取樣資料 (來自上述的 **資料取樣** 步驟)，然後使用 Python，從 Azure Machine Learning 建置並部署模型。</span><span class="sxs-lookup"><span data-stu-id="e26cb-251">In the first option, you use the sampled data that has been written to an Azure Blob (in the **Data sampling** step above) and use Python to build and deploy models from Azure Machine Learning.</span></span> 
* <span data-ttu-id="e26cb-252">在第二個選項中，您會直接使用 Hive 查詢來查詢 Azure Data Lake 中的資料。</span><span class="sxs-lookup"><span data-stu-id="e26cb-252">In the second option, you query the data in Azure Data Lake directly using a Hive query.</span></span> <span data-ttu-id="e26cb-253">此選項需要您建立新的 HDInsight 叢集，或使用現有的 HDInsight 叢集，其中 Hive 資料表指向 Azure Data Lake Storage 中的 NY 計程車資料。</span><span class="sxs-lookup"><span data-stu-id="e26cb-253">This option requires that you create a new HDInsight cluster or use an existing HDInsight cluster where the Hive tables point to the NY Taxi data in Azure Data Lake Storage.</span></span>  <span data-ttu-id="e26cb-254">以下我們討論這兩個選項。</span><span class="sxs-lookup"><span data-stu-id="e26cb-254">We discuss both these options below.</span></span> 

## <a name="option-1-use-python-to-build-and-deploy-machine-learning-models"></a><span data-ttu-id="e26cb-255">選項 1︰使用 Python 建置和部署機器學習服務模型</span><span class="sxs-lookup"><span data-stu-id="e26cb-255">Option 1: Use Python to build and deploy machine learning models</span></span>
<span data-ttu-id="e26cb-256">若要使用 Python 建置和部署機器學習服務模型，請在您的本機電腦上或在 Azure Machine Learning Studio 中建立 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="e26cb-256">To build and deploy machine learning models using Python, create a Jupyter Notebook on your local machine or in Azure Machine Learning Studio.</span></span> <span data-ttu-id="e26cb-257">[GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) 上提供的 Jupyter Notebook 包含完整的程式碼，可探索、視覺化資料、特徵工程、模型化和部署。</span><span class="sxs-lookup"><span data-stu-id="e26cb-257">The Jupyter Notebook  provided on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contains the full code to explore, visualize data, feature engineering, modeling and deployment.</span></span> <span data-ttu-id="e26cb-258">在本文中，我們只會示範模型化和部署。</span><span class="sxs-lookup"><span data-stu-id="e26cb-258">In this article, we show just the modeling and deployment.</span></span> 

### <a name="import-python-libraries"></a><span data-ttu-id="e26cb-259">匯入 Python 程式庫</span><span class="sxs-lookup"><span data-stu-id="e26cb-259">Import Python libraries</span></span>
<span data-ttu-id="e26cb-260">若要執行範例 Jupyter Notebook 或 Python 指令碼檔案，您需要下列 Python 封裝。</span><span class="sxs-lookup"><span data-stu-id="e26cb-260">In order to run the sample Jupyter Notebook or the Python script file, the following Python packages are needed.</span></span> <span data-ttu-id="e26cb-261">如果您使用 AzureML Notebook 服務，則已預先安裝這些封裝。</span><span class="sxs-lookup"><span data-stu-id="e26cb-261">If you are using the AzureML Notebook service, these packages have been pre-installed.</span></span>

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


### <a name="read-in-the-data-from-blob"></a><span data-ttu-id="e26cb-262">從 blob 讀取資料</span><span class="sxs-lookup"><span data-stu-id="e26cb-262">Read in the data from blob</span></span>
* <span data-ttu-id="e26cb-263">連接字串</span><span class="sxs-lookup"><span data-stu-id="e26cb-263">Connection String</span></span>   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* <span data-ttu-id="e26cb-264">以文字形式讀取</span><span class="sxs-lookup"><span data-stu-id="e26cb-264">Read in as text</span></span>
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds to read in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* <span data-ttu-id="e26cb-266">加入資料行名稱和分隔資料行</span><span class="sxs-lookup"><span data-stu-id="e26cb-266">Add column names and separate columns</span></span>
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* <span data-ttu-id="e26cb-267">將某些資料行變更為數值</span><span class="sxs-lookup"><span data-stu-id="e26cb-267">Change some columns to numeric</span></span>
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a><span data-ttu-id="e26cb-268">建置機器學習服務模型</span><span class="sxs-lookup"><span data-stu-id="e26cb-268">Build machine learning models</span></span>
<span data-ttu-id="e26cb-269">在此，我們建置二元分類模型，預測一趟車程是否收到小費。</span><span class="sxs-lookup"><span data-stu-id="e26cb-269">Here we build a binary classification model to predict whether a trip is tipped or not.</span></span> <span data-ttu-id="e26cb-270">在 Jupyter Notebook 中，您可以發現其他兩個模型︰多類別分類和迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="e26cb-270">In the Jupyter Notebook you can find other two models: multiclass classification, and regression models.</span></span>

* <span data-ttu-id="e26cb-271">首先，我們需要建立可在 scikit-learn 模型中使用的虛擬變數</span><span class="sxs-lookup"><span data-stu-id="e26cb-271">First we need to create dummy variables that can be used in scikit-learn models</span></span>
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* <span data-ttu-id="e26cb-272">建立模型化的資料框架</span><span class="sxs-lookup"><span data-stu-id="e26cb-272">Create data frame for the modeling</span></span>
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* <span data-ttu-id="e26cb-273">訓練和測試 60-40 分割</span><span class="sxs-lookup"><span data-stu-id="e26cb-273">Training and testing 60-40 split</span></span>
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* <span data-ttu-id="e26cb-274">訓練集中的羅吉斯迴歸</span><span class="sxs-lookup"><span data-stu-id="e26cb-274">Logistic Regression in training set</span></span>
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* <span data-ttu-id="e26cb-275">評分測試資料集</span><span class="sxs-lookup"><span data-stu-id="e26cb-275">Score testing data set</span></span>
  
        Y_test_pred = logit_fit.predict(X_test)
* <span data-ttu-id="e26cb-276">計算評估度量</span><span class="sxs-lookup"><span data-stu-id="e26cb-276">Calculate Evaluation metrics</span></span>
  
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

### <a name="build-web-service-api-and-consume-it-in-python"></a><span data-ttu-id="e26cb-277">建置 Web 服務 API 並在 Python 中使用</span><span class="sxs-lookup"><span data-stu-id="e26cb-277">Build Web Service API and consume it in Python</span></span>
<span data-ttu-id="e26cb-278">我們希望機器學習服務模型在建置後開始運作。</span><span class="sxs-lookup"><span data-stu-id="e26cb-278">We want to operationalize the machine learning model after it has been built.</span></span> <span data-ttu-id="e26cb-279">在此，我們以二元羅吉斯模型為例子。</span><span class="sxs-lookup"><span data-stu-id="e26cb-279">Here we use the binary logistic model as an example.</span></span> <span data-ttu-id="e26cb-280">請確定本機電腦中的 scikit-learn 版本是 0.15.1。</span><span class="sxs-lookup"><span data-stu-id="e26cb-280">Make sure the scikit-learn version in your local machine is 0.15.1.</span></span> <span data-ttu-id="e26cb-281">如果您使用 Azure ML Studio 服務，則不必擔心這一點。</span><span class="sxs-lookup"><span data-stu-id="e26cb-281">You don't have to worry about this if you use Azure ML studio service.</span></span>

* <span data-ttu-id="e26cb-282">從 Azure ML Studio 設定中尋找您的工作區認證。</span><span class="sxs-lookup"><span data-stu-id="e26cb-282">Find your workspace credentials from Azure ML studio settings.</span></span> <span data-ttu-id="e26cb-283">在 Azure Machine Learning Studio 中，按一下 [設定] --> [名稱] --> [授權權杖]。</span><span class="sxs-lookup"><span data-stu-id="e26cb-283">In Azure Machine Learning Studio, click **Settings** --> **Name** --> **Authorization Tokens**.</span></span> 
  
    ![c3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* <span data-ttu-id="e26cb-285">建立 Web 服務</span><span class="sxs-lookup"><span data-stu-id="e26cb-285">Create Web Service</span></span>
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* <span data-ttu-id="e26cb-286">取得 Web 服務認證</span><span class="sxs-lookup"><span data-stu-id="e26cb-286">Get web service credentials</span></span>
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* <span data-ttu-id="e26cb-287">呼叫 Web 服務 API。</span><span class="sxs-lookup"><span data-stu-id="e26cb-287">Call Web service API.</span></span> <span data-ttu-id="e26cb-288">執行上一個步驟後，您必須等候 5-10 秒。</span><span class="sxs-lookup"><span data-stu-id="e26cb-288">You have to wait 5-10 seconds after the previous step.</span></span>
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a><span data-ttu-id="e26cb-289">選項 2：直接在 Azure Machine Learning 中建立和部署模型</span><span class="sxs-lookup"><span data-stu-id="e26cb-289">Option 2: Create and deploy models directly in Azure Machine Learning</span></span>
<span data-ttu-id="e26cb-290">Azure Machine Learning Studio 可以直接從 Azure Data Lake Store 讀取資料，然後用來建立和部署模型。</span><span class="sxs-lookup"><span data-stu-id="e26cb-290">Azure Machine Learning Studio can read data directly from Azure Data Lake Store and then be used to create and deploy models.</span></span> <span data-ttu-id="e26cb-291">這個方法會使用指向 Azure Data Lake Store 的 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="e26cb-291">This approach uses a Hive table that points at the Azure Data Lake Store.</span></span> <span data-ttu-id="e26cb-292">這必須佈建不同的 Azure HDInsight 叢集，而 Hive 資料表將建立於其中。</span><span class="sxs-lookup"><span data-stu-id="e26cb-292">This requires that a separate Azure HDInsight cluster be provisioned, on which the Hive table is created.</span></span> <span data-ttu-id="e26cb-293">下列各節將示範如何執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="e26cb-293">The following sections show how to do this.</span></span> 

### <a name="create-an-hdinsight-linux-cluster"></a><span data-ttu-id="e26cb-294">建立 HDInsight Linux 叢集</span><span class="sxs-lookup"><span data-stu-id="e26cb-294">Create an HDInsight Linux Cluster</span></span>
<span data-ttu-id="e26cb-295">從 [Azure 入口網站](http://portal.azure.com)建立 HDInsight 叢集 (Linux)。如需詳細資訊，請參閱[使用 Azure 入口網站建立 HDInsight 叢集與 Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) 中的**建立可存取 Azure Data Lake Store 的 HDInsight 叢集**一節。</span><span class="sxs-lookup"><span data-stu-id="e26cb-295">Create an HDInsight Cluster (Linux) from the [Azure Portal](http://portal.azure.com).For details, see the **Create an HDInsight cluster with access to Azure Data Lake Store** section in [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a><span data-ttu-id="e26cb-297">在 HDInsight 中建立 Hive 資料表</span><span class="sxs-lookup"><span data-stu-id="e26cb-297">Create Hive table in HDInsight</span></span>
<span data-ttu-id="e26cb-298">現在，我們要使用上一個步驟中儲存於 Azure Data Lake Store 中的資料，在 HDInsight 叢集中建立要於 Azure Machine Learning Studio 中使用的 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="e26cb-298">Now we create Hive tables to be used in Azure Machine Learning Studio in the HDInsight cluster using the data stored in Azure Data Lake Store in the previous step.</span></span> <span data-ttu-id="e26cb-299">移至剛建立的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e26cb-299">Go to the HDInsight cluster just created.</span></span> <span data-ttu-id="e26cb-300">按一下 [設定] --> [屬性] --> [叢集 AAD 身分識別] --> [ADLS 存取]，確定已將您的 Azure Data Lake Store 帳戶新增清單中，且具有讀取、寫入及執行權限。</span><span class="sxs-lookup"><span data-stu-id="e26cb-300">Click **Settings** --> **Properties** --> **Cluster AAD Identity** --> **ADLS Access**, make sure your Azure Data Lake Store account is added in the list with read, write and execute rights.</span></span> 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

<span data-ttu-id="e26cb-302">然後，按一下 [設定] 按鈕旁邊的 [儀表板]，隨即出現一個視窗。</span><span class="sxs-lookup"><span data-stu-id="e26cb-302">Then click **Dashboard** next to the **Settings** button and a window will pop up.</span></span> <span data-ttu-id="e26cb-303">按一下頁面右上角的 [Hive 檢視]，您將會看到 [查詢編輯器]。</span><span class="sxs-lookup"><span data-stu-id="e26cb-303">Click **Hive View** in the upper right corner of the page and you will see the **Query Editor**.</span></span>

 ![20](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

<span data-ttu-id="e26cb-306">貼上下列 Hive 指令碼來建立資料表。</span><span class="sxs-lookup"><span data-stu-id="e26cb-306">Paste in the following Hive scripts to create a table.</span></span> <span data-ttu-id="e26cb-307">在 Azure Data Lake Store 中以這種方式參考資料來源的位置：**adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**。</span><span class="sxs-lookup"><span data-stu-id="e26cb-307">The location of data source is in Azure Data Lake Store reference in this way: **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**.</span></span>

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


<span data-ttu-id="e26cb-308">當查詢完成執行時，您會看到像這樣的結果︰</span><span class="sxs-lookup"><span data-stu-id="e26cb-308">When the query finishes running, you will see the results like this:</span></span>

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a><span data-ttu-id="e26cb-310">在 Azure Machine Learning Studio 中建置和部署模型</span><span class="sxs-lookup"><span data-stu-id="e26cb-310">Build and deploy models in Azure Machine Learning Studio</span></span>
<span data-ttu-id="e26cb-311">現在，我們已準備好要建置和部署使用 Azure Machine Learning 來預測是否會支付小費的模型。</span><span class="sxs-lookup"><span data-stu-id="e26cb-311">We are now ready to build and deploy a model that predicts whether or not a tip is paid with Azure Machine Learning.</span></span> <span data-ttu-id="e26cb-312">分層範例資料已經備妥，可在這個二元分類 (有無小費) 問題中使用。</span><span class="sxs-lookup"><span data-stu-id="e26cb-312">The stratified sample data is ready to be used in this binary classification (tip or not) problem.</span></span> <span data-ttu-id="e26cb-313">使用多類別分類 (tip_class) 和迴歸 (tip_amount) 的預測模型也會使用 Azure Machine Learning Studio 來建置和部署，但是我們只會在此處示範如何使用二元分類模型來處理此案例。</span><span class="sxs-lookup"><span data-stu-id="e26cb-313">The predictive models using multiclass classification (tip_class) and regression (tip_amount) can also be built and deployed with Azure Machine Learning Studio, but here we only show how to handle the case using the binary classification model.</span></span>

1. <span data-ttu-id="e26cb-314">使用**匯入資料**模組 (可從**資料輸入和輸出**一節取得)，將資料匯入 Azure ML。</span><span class="sxs-lookup"><span data-stu-id="e26cb-314">Get the data into Azure ML using the **Import Data** module, available in the **Data Input and Output** section.</span></span> <span data-ttu-id="e26cb-315">如需詳細資訊，請參閱 [匯入資料](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) 模組參考頁面。</span><span class="sxs-lookup"><span data-stu-id="e26cb-315">For more information, see the [Import Data module](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) reference page.</span></span>
2. <span data-ttu-id="e26cb-316">在 [屬性] 面板中，選取 [Hive 查詢] 做為 [資料來源]。</span><span class="sxs-lookup"><span data-stu-id="e26cb-316">Select **Hive Query** as the **Data source** in the **Properties** panel.</span></span>
3. <span data-ttu-id="e26cb-317">將下列 Hive 指令碼貼到 [Hive 資料庫查詢] 編輯器中</span><span class="sxs-lookup"><span data-stu-id="e26cb-317">Paste the following Hive script in the **Hive database query** editor</span></span>
   
        select * from nyc_stratified_sample;
4. <span data-ttu-id="e26cb-318">輸入 HDInsight 叢集的 URI (這可以在 Azure 入口網站中找到)、Hadoop 認證、輸出資料的位置，以及 Azure 儲存體帳戶名稱/金鑰/容器名稱。</span><span class="sxs-lookup"><span data-stu-id="e26cb-318">Enter the URI of HDInsight cluster (this can be found in Azure Portal), Hadoop credentials, location of output data, and Azure storage account name/key/container name.</span></span>
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

<span data-ttu-id="e26cb-320">下圖顯示從 Hive 資料表讀取資料的二元分類實驗範例。</span><span class="sxs-lookup"><span data-stu-id="e26cb-320">An example of a binary classification experiment reading data from Hive table is shown in the figure below.</span></span>

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

<span data-ttu-id="e26cb-322">建立實驗之後，按一下 [設定 Web 服務] --> [預測性 Web 服務]</span><span class="sxs-lookup"><span data-stu-id="e26cb-322">After the experiment is created, click  **Set Up Web Service** --> **Predictive Web Service**</span></span>

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

<span data-ttu-id="e26cb-324">執行自動建立的評分實驗，完成後，按一下 [部署 Web 服務]</span><span class="sxs-lookup"><span data-stu-id="e26cb-324">Run the automatically created scoring experiment, when it finishes, click **Deploy Web Service**</span></span>

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

<span data-ttu-id="e26cb-326">不久後就會 Web 服務儀表板︰</span><span class="sxs-lookup"><span data-stu-id="e26cb-326">The web service dashboard will be displayed shortly:</span></span>

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a><span data-ttu-id="e26cb-328">摘要</span><span class="sxs-lookup"><span data-stu-id="e26cb-328">Summary</span></span>
<span data-ttu-id="e26cb-329">完成這個逐步解說之後，您就已經建立了資料科學環境，可在 Azure Data Lake 中建置可調整的端對端解決方案。</span><span class="sxs-lookup"><span data-stu-id="e26cb-329">By completing this walkthrough you have created a data science environment for building scalable end-to-end solutions in Azure Data Lake.</span></span> <span data-ttu-id="e26cb-330">這個環境可用來分析大型公用資料集，透過資料科學程序的標準步驟來取得此公用資料集，過程中從取得資料開始、經過模型訓練，最後將模型部署成 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e26cb-330">This environment was used to analyze a large public dataset, taking it through the canonical steps of the Data Science Process, from data acquisition through model training, and then to the deployment of the model as a web service.</span></span> <span data-ttu-id="e26cb-331">您可以使用 U-SQL 來處理、探索和取樣資料。</span><span class="sxs-lookup"><span data-stu-id="e26cb-331">U-SQL was used to process, explore and sample the data.</span></span> <span data-ttu-id="e26cb-332">Python 和 Hive 會與 Azure Machine Learning Studio 搭配使用來建置和部署預測模型。</span><span class="sxs-lookup"><span data-stu-id="e26cb-332">Python and Hive were used with Azure Machine Learning Studio to build and deploy predictive models.</span></span>

## <a name="whats-next"></a><span data-ttu-id="e26cb-333">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e26cb-333">What's next?</span></span>
<span data-ttu-id="e26cb-334">[Team Data Science Process (TDSP)](http://aka.ms/datascienceprocess) 的學習路徑提供可說明進階分析程序中每個步驟的主題連結。</span><span class="sxs-lookup"><span data-stu-id="e26cb-334">The learning path for the [Team Data Science Process (TDSP)](http://aka.ms/datascienceprocess) provides links to topics describing each step in the advanced analytics process.</span></span> <span data-ttu-id="e26cb-335">[Team Data Science Process 逐步解說](data-science-process-walkthroughs.md) 頁面上分項列出一系列逐步解說，示範如何在各種不同預測性分析案例中使用資源和服務：</span><span class="sxs-lookup"><span data-stu-id="e26cb-335">There are a series of walkthroughs itemized on the [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) page that showcase how to use resources and services in various predictive analytics scenarios:</span></span>

* [<span data-ttu-id="e26cb-336">Team Data Science Process 實務：使用 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="e26cb-336">The Team Data Science Process in action: using SQL Data Warehouse</span></span>](machine-learning-data-science-process-sqldw-walkthrough.md)
* [<span data-ttu-id="e26cb-337">Team Data Science Process 實務：使用 HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="e26cb-337">The Team Data Science Process in action: using HDInsight Hadoop clusters</span></span>](machine-learning-data-science-process-hive-walkthrough.md)
* [<span data-ttu-id="e26cb-338">Team Data Science Process：使用 SQL Server</span><span class="sxs-lookup"><span data-stu-id="e26cb-338">The Team Data Science Process: using SQL Server</span></span>](machine-learning-data-science-process-sql-walkthrough.md)
* [<span data-ttu-id="e26cb-339">在 Azure HDInsight 上使用 Spark 的資料科學程序概觀</span><span class="sxs-lookup"><span data-stu-id="e26cb-339">Overview of the Data Science Process using Spark on Azure HDInsight</span></span>](machine-learning-data-science-spark-overview.md)

