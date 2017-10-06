---
title: "aaaTen 項目，您可以在 hello Data Science 虛擬機器 |Microsoft 文件"
description: "Hello 資料科學虛擬機器上執行各種資料瀏覽和模型化工作。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 145dfe3e-2bd2-478f-9b6e-99d97d789c62
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;weig;bradsev
ms.openlocfilehash: 4dfe22f14f00208c63e26ce44b05123c9ac4b850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="ten-things-you-can-do-on-hello-data-science-virtual-machine"></a><span data-ttu-id="e18e7-103">您可以執行 hello 資料科學虛擬機器上的十個項目</span><span class="sxs-lookup"><span data-stu-id="e18e7-103">Ten things you can do on hello Data science Virtual Machine</span></span>
<span data-ttu-id="e18e7-104">hello Microsoft 資料科學虛擬機器 (DSVM) 是功能強大的資料科學開發環境，可讓您 tooperform 各種資料探索和模型工作。</span><span class="sxs-lookup"><span data-stu-id="e18e7-104">hello Microsoft Data Science Virtual Machine (DSVM) is a powerful data science development environment that enables you tooperform various data exploration and modeling tasks.</span></span> <span data-ttu-id="e18e7-105">hello 環境包含已建置及配套幾個常見的資料與分析工具，可讓您輕鬆 tooget 快速地開始使用您的分析，在內部部署、 雲端或混合式部署。</span><span class="sxs-lookup"><span data-stu-id="e18e7-105">hello environment comes already built and bundled with several popular data analytics tools that make it easy tooget started quickly with your analysis for On-premises, Cloud or hybrid deployments.</span></span> <span data-ttu-id="e18e7-106">hello DSVM 與許多 Azure 服務密切合作，且無法 tooread 和處理已儲存在 Azure、 在 Azure SQL 資料倉儲、 Azure 資料湖、 Azure 儲存體，或在 Azure Cosmos DB 的資料。</span><span class="sxs-lookup"><span data-stu-id="e18e7-106">hello DSVM works closely with many Azure services and is able tooread and process data that is already stored on Azure, in Azure SQL Data Warehouse, Azure Data Lake, Azure Storage, or in Azure Cosmos DB.</span></span> <span data-ttu-id="e18e7-107">它也可以利用 Azure Machine Learning 和 Azure Data Factory 等其他分析工具。</span><span class="sxs-lookup"><span data-stu-id="e18e7-107">It can also leverage other analytics tools such as Azure Machine Learning and Azure Data Factory.</span></span>

<span data-ttu-id="e18e7-108">本文章中我們逐步引導您 toouse 您 DSVM tooperform 各種資料科學工作以及與其他 Azure 服務互動。</span><span class="sxs-lookup"><span data-stu-id="e18e7-108">In this article we walk you through how toouse your DSVM tooperform various data science tasks and interact with other Azure services.</span></span> <span data-ttu-id="e18e7-109">以下是一些您可以在 hello DSVM 所執行的 hello 事項：</span><span class="sxs-lookup"><span data-stu-id="e18e7-109">Here are some of hello things you can do on hello DSVM:</span></span>

1. <span data-ttu-id="e18e7-110">瀏覽資料並開發模型，在本機上使用 Microsoft R Server Python DSVM hello</span><span class="sxs-lookup"><span data-stu-id="e18e7-110">Explore data and develop models locally on hello DSVM using Microsoft R Server, Python</span></span>
2. <span data-ttu-id="e18e7-111">使用 Python 2，Python 3 Microsoft R R 的延展性和效能而設計的企業就緒版本的瀏覽器上的資料搭配使用 Jupyter 筆記本 tooexperiment</span><span class="sxs-lookup"><span data-stu-id="e18e7-111">Use a Jupyter notebook tooexperiment with your data on a browser using Python 2, Python 3, Microsoft R an enterprise ready version of R designed for scalability and performance</span></span>
3. <span data-ttu-id="e18e7-112">在 Azure Machine Learning 上實作使用 R 和 Python 建置的模型，以便用戶端應用程式使用簡單的 Web 服務介面存取您的模型</span><span class="sxs-lookup"><span data-stu-id="e18e7-112">Operationalize models built using R and Python on Azure Machine Learning so client applications can access your models using a simple web services interface</span></span>
4. <span data-ttu-id="e18e7-113">使用 Azure 入口網站或 Powershell 管理您的 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="e18e7-113">Administer your Azure resources using  Azure portal or Powershell</span></span>
5. <span data-ttu-id="e18e7-114">建立 Azure 檔案儲存體作為 DSVM 上可掛接的磁碟機，以擴充您的儲存空間並與整個小組共用大型資料集/程式碼</span><span class="sxs-lookup"><span data-stu-id="e18e7-114">Extend your storage space and share large-scale datasets / code across your whole team by creating an Azure File storage as a mountable drive on your DSVM</span></span>
6. <span data-ttu-id="e18e7-115">與您使用 GitHub 的小組共用程式碼，並存取您的儲存機制使用 hello 預先安裝的 Git 用戶端-Git Bash Git GUI。</span><span class="sxs-lookup"><span data-stu-id="e18e7-115">Share code with your team using GitHub and access your repository using hello pre-installed Git clients - Git Bash, Git GUI.</span></span>
7. <span data-ttu-id="e18e7-116">存取各種 Azure 資料和分析服務，例如 Azure Blob 儲存體，Azure Data Lake、Azure HDInsight (Hadoop)、Azure Cosmos DB、Azure SQL 資料倉儲和資料庫</span><span class="sxs-lookup"><span data-stu-id="e18e7-116">Access various Azure data and analytics services like Azure blob storage, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse & databases</span></span>
8. <span data-ttu-id="e18e7-117">建立報表和儀表板使用 hello hello DSVM 上預先安裝的 Power BI Desktop，並將其部署的 hello 雲端</span><span class="sxs-lookup"><span data-stu-id="e18e7-117">Build reports and dashboard using hello Power BI Desktop pre-installed on hello DSVM and deploy them on hello cloud</span></span>
9. <span data-ttu-id="e18e7-118">動態調整您的專案需要您 DSVM toomeet</span><span class="sxs-lookup"><span data-stu-id="e18e7-118">Dynamically scale your DSVM toomeet your project needs</span></span>
10. <span data-ttu-id="e18e7-119">在虛擬機器上安裝其他工具</span><span class="sxs-lookup"><span data-stu-id="e18e7-119">Install additional tools on your virtual machine</span></span>   

> [!NOTE]
> <span data-ttu-id="e18e7-120">其他使用費用 適用於許多 hello 其他資料儲存體和分析服務本文所列。</span><span class="sxs-lookup"><span data-stu-id="e18e7-120">Additional usage charges apply for many of hello additional data storage and analytics services listed in this article.</span></span> <span data-ttu-id="e18e7-121">請參閱 toohello [Azure 定價](https://azure.microsoft.com/pricing/)頁面以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e18e7-121">Please refer toohello [Azure Pricing](https://azure.microsoft.com/pricing/) page for details.</span></span>
> 
> 

<span data-ttu-id="e18e7-122">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="e18e7-122">**Prerequisites**</span></span>

* <span data-ttu-id="e18e7-123">您需要 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e18e7-123">You need an Azure subscription.</span></span> <span data-ttu-id="e18e7-124">您可以在[這裡](https://azure.microsoft.com/free/)註冊免費試用。</span><span class="sxs-lookup"><span data-stu-id="e18e7-124">You can sign up for a free trial [here](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="e18e7-125">指示佈建 hello Azure 入口網站上的 Data Science 虛擬機器位於[建立虛擬機器](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm)。</span><span class="sxs-lookup"><span data-stu-id="e18e7-125">Instructions for provisioning a Data Science Virtual Machine on hello Azure portal are available at [Creating a virtual machine](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span></span>

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a><span data-ttu-id="e18e7-126">1.使用 Microsoft R Server 或 Python 探索資料和開發模型</span><span class="sxs-lookup"><span data-stu-id="e18e7-126">1. Explore data and develop models using Microsoft R Server or Python</span></span>
<span data-ttu-id="e18e7-127">您可以在 hello DSVM 使用語言，例如 R，並將 Python toodo 資料分析。</span><span class="sxs-lookup"><span data-stu-id="e18e7-127">You can use languages like R and Python toodo your data analytics right on hello DSVM.</span></span>

<span data-ttu-id="e18e7-128">，您可以使用稱為 「 Revolution R Enterprise 8.0"hello 桌面 hello [開始] 功能表上找到的 IDE。</span><span class="sxs-lookup"><span data-stu-id="e18e7-128">For R, you can use an IDE called "Revolution R Enterprise 8.0" that can be found on hello start menu or hello desktop.</span></span> <span data-ttu-id="e18e7-129">Microsoft 已提供額外的程式庫最上層 hello 開啟來源/CRAN R tooenable 可擴充分析和 hello 能力 tooanalyze 資料大於允許的執行平行區塊的分析 hello 記憶體大小。</span><span class="sxs-lookup"><span data-stu-id="e18e7-129">Microsoft has provided additional libraries on top of hello Open source/CRAN-R tooenable scalable analytics and hello ability tooanalyze data larger than hello memory size allowed by doing parallel chunked analysis.</span></span> <span data-ttu-id="e18e7-130">您也可以安裝您選擇的 R IDE，例如 [RStudio](https://www.rstudio.com/products/rstudio-desktop/)。</span><span class="sxs-lookup"><span data-stu-id="e18e7-130">You can also install an R IDE of your choice like [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span></span>

<span data-ttu-id="e18e7-131">Python，您可以使用像是 Visual Studio Community 版本具有 hello Python Tools for Visual Studio (PTVS) 預先安裝的擴充功能的 IDE。</span><span class="sxs-lookup"><span data-stu-id="e18e7-131">For Python, you can use an IDE like Visual Studio Community Edition which has hello Python Tools for Visual Studio (PTVS) extension pre-installed.</span></span> <span data-ttu-id="e18e7-132">根據預設，PTVS 上只設定基本的 Python 2.7 (不含任何分析程式庫，如 SciKit、Pandas)。</span><span class="sxs-lookup"><span data-stu-id="e18e7-132">By default, only a basic Python 2.7 is configured on PTVS (without any analytics library like SciKit, Pandas).</span></span> <span data-ttu-id="e18e7-133">在訂單 tooenable Anaconda Python 2.7 和 3.5 中，您需要 toodo hello 下列：</span><span class="sxs-lookup"><span data-stu-id="e18e7-133">In order tooenable Anaconda Python 2.7 and 3.5, you need toodo hello following:</span></span>

* <span data-ttu-id="e18e7-134">建立瀏覽過的每個版本的自訂環境**工具** -> **Python Tools** -> **Python 環境**，然後按一下"**+ 自訂**「 在 Visual Studio 2015 Community 版本 hello</span><span class="sxs-lookup"><span data-stu-id="e18e7-134">Create custom environments for each version by navigating too**Tools** -> **Python Tools** -> **Python Environments** and then clicking "**+ Custom**" in hello Visual Studio 2015 Community Edition</span></span>
* <span data-ttu-id="e18e7-135">提供的描述，並設定 hello 環境做為前置詞路徑*c:\anaconda* Anaconda Python 2.7 或*c:\anaconda\envs\py35* Anaconda Python 3.5</span><span class="sxs-lookup"><span data-stu-id="e18e7-135">Give a description and set hello environment prefix paths as *c:\anaconda* for Anaconda Python 2.7 OR *c:\anaconda\envs\py35* for Anaconda Python 3.5</span></span>
* <span data-ttu-id="e18e7-136">按一下**自動偵測**然後**套用**toosave hello 環境。</span><span class="sxs-lookup"><span data-stu-id="e18e7-136">Click **Auto Detect** and then **Apply** toosave hello environment.</span></span>

<span data-ttu-id="e18e7-137">以下是 Visual Studio 中看起來像哪些 hello 自訂環境設定。</span><span class="sxs-lookup"><span data-stu-id="e18e7-137">Here is what hello custom environment setup looks like in Visual Studio.</span></span>

![PTVS 設定](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

<span data-ttu-id="e18e7-139">請參閱 hello [PTVS 文件](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it)的其他詳細資料 toocreate Python 環境。</span><span class="sxs-lookup"><span data-stu-id="e18e7-139">See hello [PTVS documentation](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) for additional details on how toocreate Python Environments.</span></span>

<span data-ttu-id="e18e7-140">現在您會設定 toocreate 新的 Python 專案。</span><span class="sxs-lookup"><span data-stu-id="e18e7-140">Now you are set up toocreate a new Python project.</span></span> <span data-ttu-id="e18e7-141">瀏覽過**檔案** -> **新增** -> **專案** -> **Python**選取 hello 類型您要建置的 Python 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e18e7-141">Navigate too**File** -> **New** -> **Project** -> **Python** and select hello type of Python application you are building.</span></span> <span data-ttu-id="e18e7-142">您可以設定 hello Python 環境的 hello 目前專案 toohello 所需的版本 (Anaconda 2.7 或 3.5 為目標): 以滑鼠右鍵按一下 hello **Python 環境**，選取**新增/移除 Python 環境**，和然後選取所需的 hello 環境 tooassociate 與 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="e18e7-142">You can set hello Python environment for hello current project toohello desired version (Anaconda 2.7 or 3.5): right-click hello **Python environment**, select **Add/Remove Python Environments**, and then select hello desired environment tooassociate with hello project.</span></span> <span data-ttu-id="e18e7-143">您可以找到更多有關如何使用與 PTVS hello 產品[文件](https://github.com/Microsoft/PTVS/wiki)頁面。</span><span class="sxs-lookup"><span data-stu-id="e18e7-143">You can find more information about working with PTVS on hello product [documentation](https://github.com/Microsoft/PTVS/wiki) page.</span></span>

## <a name="2-using-a-jupyter-notebook-tooexplore-and-model-your-data-with-python-or-r"></a><span data-ttu-id="e18e7-144">2.Jupyter 筆記本 tooexplore 和模型資料搭配使用 Python 或 R</span><span class="sxs-lookup"><span data-stu-id="e18e7-144">2. Using a Jupyter Notebook tooexplore and model your data with Python or R</span></span>
<span data-ttu-id="e18e7-145">hello Jupyter 筆記本是功能強大的環境，提供資料探索和模型的瀏覽器型"IDE"。</span><span class="sxs-lookup"><span data-stu-id="e18e7-145">hello Jupyter Notebook is a powerful environment that provides a browser-based "IDE" for data exploration and modeling.</span></span> <span data-ttu-id="e18e7-146">Jupyter 筆記本中，您可以使用 Python 2、 Python 3 或 R （開放原始碼和 Microsoft R Server hello）。</span><span class="sxs-lookup"><span data-stu-id="e18e7-146">You can use Python 2, Python 3 or R (both Open Source and hello Microsoft R Server) in a Jupyter Notebook.</span></span>

<span data-ttu-id="e18e7-147">hello 開始功能表圖示上按一下 toolaunch hello Jupyter 筆記本 / 標題為 桌面圖示**Jupyter 筆記本**。</span><span class="sxs-lookup"><span data-stu-id="e18e7-147">toolaunch hello Jupyter Notebook click on hello start menu icon / desktop icon titled **Jupyter Notebook**.</span></span> <span data-ttu-id="e18e7-148">在 hello DSVM 您也可以瀏覽過"https://localhost:9999 /"tooaccess hello 木星筆記型電腦。</span><span class="sxs-lookup"><span data-stu-id="e18e7-148">On hello DSVM you can also browse too"https://localhost:9999/" tooaccess hello Jupiter Notebook.</span></span> <span data-ttu-id="e18e7-149">如果它會提示您輸入密碼，請使用 hello 中提供的指示***如何 toocreate hello Jupyter 筆記本伺服器上的強式密碼***區段 hello[佈建 hello Microsoft Data Science 虛擬機器](machine-learning-data-science-provision-vm.md)主題 toocreate 強式密碼 tooaccess hello Jupyter 筆記本。</span><span class="sxs-lookup"><span data-stu-id="e18e7-149">If it prompts you for a password, use instructions provided in hello ***How toocreate a strong password on hello Jupyter notebook server*** section of hello [Provision hello Microsoft Data Science Virtual Machine](machine-learning-data-science-provision-vm.md) topic toocreate a strong password tooaccess hello Jupyter notebook.</span></span> 

<span data-ttu-id="e18e7-150">一旦您已開啟 hello 筆記本，您應該會看到包含幾個範例筆記本 hello DSVM 到預先封裝的目錄。</span><span class="sxs-lookup"><span data-stu-id="e18e7-150">Once you have opened hello notebook, you should see a directory that contains a few example notebooks that are pre-packaged into hello DSVM.</span></span> <span data-ttu-id="e18e7-151">現在您可以：</span><span class="sxs-lookup"><span data-stu-id="e18e7-151">Now you can:</span></span>

* <span data-ttu-id="e18e7-152">按一下 hello 筆記本 toosee hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="e18e7-152">click on hello notebook toosee hello code.</span></span>
* <span data-ttu-id="e18e7-153">按 **SHIFT-ENTER**執行每個儲存格。</span><span class="sxs-lookup"><span data-stu-id="e18e7-153">execute each cell by pressing **SHIFT-ENTER**.</span></span>
* <span data-ttu-id="e18e7-154">按一下以執行 hello 整個筆記本**儲存格** -> **執行**</span><span class="sxs-lookup"><span data-stu-id="e18e7-154">run hello entire notebook by clicking on **Cell** -> **Run**</span></span>
* <span data-ttu-id="e18e7-155">hello Jupyter 圖示 （左上角） 上按一下，然後按一下以建立新的記事本**新增**hello 右，然後選擇 hello 筆記本語言 （也稱為核心） 上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="e18e7-155">create a new notebook by clicking on hello Jupyter Icon (left top corner) and then clicking **New** button on hello right and then choosing hello notebook language (also known as kernels).</span></span>   

> [!NOTE]
> <span data-ttu-id="e18e7-156">目前我們支援 Python 2.7、 Python 3.5 和 r hello R 核心開放原始碼 R 以及 hello 企業中支援的程式設計可擴充的 Microsoft R Server。</span><span class="sxs-lookup"><span data-stu-id="e18e7-156">Currently we support Python 2.7, Python 3.5 and R. hello R kernel supports programming in both Open source R as well as hello enterprise scalable Microsoft R Server.</span></span>   
> 
> 

<span data-ttu-id="e18e7-157">當您在 hello 筆記本可以瀏覽資料、 建立 hello 模型、 測試 hello 模型使用您所選擇的程式庫。</span><span class="sxs-lookup"><span data-stu-id="e18e7-157">Once you are in hello notebook you can explore your data, build hello model, test hello model using your choice of libraries.</span></span>

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a><span data-ttu-id="e18e7-158">3.使用 R 或 Python 建置模型並且使用 Azure Machine Learning 實作</span><span class="sxs-lookup"><span data-stu-id="e18e7-158">3. Build models using R or Python and Operationalize them using Azure Machine Learning</span></span>
<span data-ttu-id="e18e7-159">一旦您已經建置和驗證模型 hello 的下一個步驟通常是 toodeploy 它到實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="e18e7-159">Once you have built and validated your model hello next step is usually toodeploy it into production.</span></span> <span data-ttu-id="e18e7-160">這可讓您的用戶端應用程式 tooinvoke hello 模型預測即時或批次模式為基礎。</span><span class="sxs-lookup"><span data-stu-id="e18e7-160">This allows your client applications tooinvoke hello model predictions on a real time or on a batch mode basis.</span></span> <span data-ttu-id="e18e7-161">Azure Machine Learning 提供機制 toooperationalize Python 或 R 中所建立的模型。</span><span class="sxs-lookup"><span data-stu-id="e18e7-161">Azure Machine Learning provides a mechanism toooperationalize a model built in either R or Python.</span></span>

<span data-ttu-id="e18e7-162">當您作業化您在 Azure Machine Learning 中的模型時，web 服務會公開以允許用戶端的傳入輸入參數，且收到 hello 模型中的預測，為輸出 toomake REST 呼叫。</span><span class="sxs-lookup"><span data-stu-id="e18e7-162">When you operationalize your model in Azure Machine Learning, a web service is exposed that allows clients toomake REST calls that pass in input parameters and receive predictions from hello model as outputs.</span></span>   

> [!NOTE]
> <span data-ttu-id="e18e7-163">如果您不尚未已註冊 Azure Machine Learning，您可以取得免費工作區或標準的工作區瀏覽 hello [Azure Machine Learning Studio](https://studio.azureml.net/)首頁上，按一下 在 「 取得已啟動 」。</span><span class="sxs-lookup"><span data-stu-id="e18e7-163">If you have not yet signed up for Azure Machine Learning, you can obtain a free workspace or a standard workspace by visiting hello [Azure Machine Learning Studio](https://studio.azureml.net/) home page and clicking on "Get Started".</span></span>   
> 
> 

### <a name="build-and-operationalize-python-models"></a><span data-ttu-id="e18e7-164">建置和實作 Python 模型</span><span class="sxs-lookup"><span data-stu-id="e18e7-164">Build and Operationalize Python models</span></span>
<span data-ttu-id="e18e7-165">以下是在 Python Jupyter 筆記本中建立簡單的模型使用 hello SciKit 學習程式庫開發程式碼的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="e18e7-165">Here is a snippet of code developed in a Python Jupyter Notebook that builds a simple model using hello SciKit-learn library.</span></span>

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

<span data-ttu-id="e18e7-166">hello 方法使用 toodeploy 您 python 模型 tooAzure Machine Learning 會包裝 hello 的預測 hello 模型到函式和裝飾與 hello 預先安裝 Azure Machine Learning python 程式庫所提供的屬性，代表您的 Azure 機器Learning 工作區識別碼、 API 金鑰，以及 hello 輸入和傳回參數。</span><span class="sxs-lookup"><span data-stu-id="e18e7-166">hello method used toodeploy your python models tooAzure Machine Learning wraps hello prediction of hello model into a function and decorates it with attributes provided by hello pre-installed Azure Machine Learning python library that denote your Azure Machine Learning workspace ID, API Key, and hello input and return parameters.</span></span>  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

<span data-ttu-id="e18e7-167">用戶端現在可以讓呼叫 toohello web 服務。</span><span class="sxs-lookup"><span data-stu-id="e18e7-167">A client can now make calls toohello web service.</span></span> <span data-ttu-id="e18e7-168">沒有建構 hello REST API 要求的便利包裝函式。</span><span class="sxs-lookup"><span data-stu-id="e18e7-168">There are convenience wrappers that construct hello REST API requests.</span></span> <span data-ttu-id="e18e7-169">以下是範例程式碼 tooconsume hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="e18e7-169">Here is a sample code tooconsume hello web service.</span></span>

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> <span data-ttu-id="e18e7-170">hello Azure Machine Learning 文件庫只支援 Python 2.7 目前。</span><span class="sxs-lookup"><span data-stu-id="e18e7-170">hello Azure Machine Learning library is only supported on Python 2.7 currently.</span></span>   
> 
> 

### <a name="build-and-operationalize-r-models"></a><span data-ttu-id="e18e7-171">建置和實作 R 模型</span><span class="sxs-lookup"><span data-stu-id="e18e7-171">Build and Operationalize R models</span></span>
<span data-ttu-id="e18e7-172">您可以部署以類似 toohow 基於 Python 的方式內建 hello Data Science 虛擬機器或其他 Azure 機器學習到的 R 模型。</span><span class="sxs-lookup"><span data-stu-id="e18e7-172">You can deploy R models built on hello Data Science Virtual Machine or elsewhere onto Azure Machine Learning in a manner that is similar toohow it is done for Python.</span></span> <span data-ttu-id="e18e7-173">她 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="e18e7-173">Her are hello steps:</span></span>

* <span data-ttu-id="e18e7-174">建立工作區識別碼和驗證語彙基元 hello 下列程式碼範例所示 settings.json 檔案 tooprovide。</span><span class="sxs-lookup"><span data-stu-id="e18e7-174">create a settings.json file tooprovide your workspace ID and auth token as shown in hello following code sample.</span></span>
* <span data-ttu-id="e18e7-175">寫入包裝函式以進行 hello 模型的預測函數。</span><span class="sxs-lookup"><span data-stu-id="e18e7-175">write a wrapper for hello model's predict function.</span></span>
* <span data-ttu-id="e18e7-176">呼叫```publishWebService```在 hello Azure Machine Learning 文件庫 toopass hello 函式包裝函式中。</span><span class="sxs-lookup"><span data-stu-id="e18e7-176">call ```publishWebService``` in hello Azure Machine Learning library toopass in hello function wrapper.</span></span>  

<span data-ttu-id="e18e7-177">以下是 hello 程序和程式碼的程式碼片段可以是使用的 tooset up、 建置、 發行和取用 Azure Machine Learning 中的 web 服務的模型。</span><span class="sxs-lookup"><span data-stu-id="e18e7-177">Here is hello procedure and code snippets that can be used tooset up, build, publish, and consume a model as a web service in Azure Machine Learning.</span></span>

#### <a name="setup"></a><span data-ttu-id="e18e7-178">設定</span><span class="sxs-lookup"><span data-stu-id="e18e7-178">Setup</span></span>
1. <span data-ttu-id="e18e7-179">輸入安裝 hello 機器學習 R 封裝```install.packages("AzureML")```Revolution R Enterprise 8.0 IDE 或您的 R IDE 中。</span><span class="sxs-lookup"><span data-stu-id="e18e7-179">Install hello Machine Learning R package by typing ```install.packages("AzureML")``` in Revolution R Enterprise 8.0 IDE or your R IDE.</span></span>
2. <span data-ttu-id="e18e7-180">從[這裡](https://cran.r-project.org/bin/windows/Rtools/)下載 RTools。</span><span class="sxs-lookup"><span data-stu-id="e18e7-180">Download RTools from [here](https://cran.r-project.org/bin/windows/Rtools/).</span></span> <span data-ttu-id="e18e7-181">您需要 hello zip 公用程式在 hello 路徑 （和具名的 zip.exe） toooperationalize R 封裝到機器學習。</span><span class="sxs-lookup"><span data-stu-id="e18e7-181">You need hello zip utility in hello path (and named zip.exe) toooperationalize your R package into Machine Learning.</span></span>
3. <span data-ttu-id="e18e7-182">建立 settings.json 底下的檔名的目錄```.azureml```主目錄底下，輸入 hello 參數與您的 Azure Machine Learning 工作區：</span><span class="sxs-lookup"><span data-stu-id="e18e7-182">Create a settings.json file under a directory called ```.azureml``` under your home directory and enter hello parameters from your Azure Machine Learning workspace:</span></span>

<span data-ttu-id="e18e7-183">settings.json 檔案結構：</span><span class="sxs-lookup"><span data-stu-id="e18e7-183">settings.json File structure:</span></span>

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a><span data-ttu-id="e18e7-184">以 R 建置模型並在 Azure Machine Learning 中發佈</span><span class="sxs-lookup"><span data-stu-id="e18e7-184">Build a model in R and publish it in Azure Machine Learning</span></span>
    library(AzureML)
    ws <- workspace(config="~/.azureml/settings.json")

    if(!require("lme4")) install.packages("lme4")
    library(lme4)
    set.seed(1)
    train <- sleepstudy[sample(nrow(sleepstudy), 120),]
    m <- lm(Reaction ~ Days + Subject, data = train)

    # Define a prediction function toopublish based on hello model:
    sleepyPredict <- function(newdata){
          predict(m, newdata=newdata)
    }

    ep <- publishWebService(ws, fun = sleepyPredict, name="sleepy lm", inputSchema = sleepstudy, data.frame=TRUE)

#### <a name="consume-hello-model-deployed-in-azure-machine-learning"></a><span data-ttu-id="e18e7-185">使用 Azure Machine Learning 中部署的 hello 模型</span><span class="sxs-lookup"><span data-stu-id="e18e7-185">Consume hello model deployed in Azure Machine Learning</span></span>
<span data-ttu-id="e18e7-186">tooconsume hello 模型從用戶端應用程式中的，我們使用向上 hello hello Azure Machine Learning 文件庫 toolook 發佈 web 服務的名稱使用 hello `services` API 呼叫 toodetermine hello 端點。</span><span class="sxs-lookup"><span data-stu-id="e18e7-186">tooconsume hello model from a client application, we use hello Azure Machine Learning library toolook up hello published web service by name using hello `services` API call toodetermine hello endpoint.</span></span> <span data-ttu-id="e18e7-187">然後您只需要呼叫 hello`consume`函式，並傳入 hello 資料框架 toobe 預測。</span><span class="sxs-lookup"><span data-stu-id="e18e7-187">Then you just call hello `consume` function and pass in hello data frame toobe predicted.</span></span>
<span data-ttu-id="e18e7-188">下列程式碼的 hello 是使用的 tooconsume hello 模型發佈為 Azure Machine Learning web 服務。</span><span class="sxs-lookup"><span data-stu-id="e18e7-188">hello following code is used tooconsume hello model published as an Azure Machine Learning web service.</span></span>

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use hello last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

<span data-ttu-id="e18e7-189">可以找到 hello Azure 機器學習 R 程式庫的詳細資訊[這裡](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf)。</span><span class="sxs-lookup"><span data-stu-id="e18e7-189">More information about hello Azure Machine Learning R library can be found [here](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span></span>

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a><span data-ttu-id="e18e7-190">4.使用 Azure 入口網站或 Powershell 管理您的 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="e18e7-190">4. Administer your Azure resources using Azure portal or Powershell</span></span>
<span data-ttu-id="e18e7-191">hello DSVM 不僅可讓您 toobuild 分析解決方案上進行本機 hello 虛擬機器，但也允許 tooaccess Microsoft Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="e18e7-191">hello DSVM not only allows you toobuild your analytics solution locally on hello virtual machine, but also allows you tooaccess services on Microsoft's Azure cloud.</span></span> <span data-ttu-id="e18e7-192">Azure 提供數個可從 DSVM 管理和存取的計算、儲存、資料分析服務和其他服務。</span><span class="sxs-lookup"><span data-stu-id="e18e7-192">Azure provides several compute, storage, data analytics services and other services that you can administer and access from your DSVM.</span></span>

<span data-ttu-id="e18e7-193">tooadminister 您的 Azure 訂用帳戶和雲端資源可以使用瀏覽器和點 toothe [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="e18e7-193">tooadminister your Azure subscription and cloud resources you can use your browser and point toothe [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e18e7-194">您的 Azure 訂用帳戶和資源，透過指令碼，您也可以使用 Azure Powershell tooadminister。</span><span class="sxs-lookup"><span data-stu-id="e18e7-194">You can also use Azure Powershell tooadminister your Azure subscription and resources via a script.</span></span>
<span data-ttu-id="e18e7-195">您可以從捷徑 hello 桌面上執行 Azure Powershell 或 hello 從開始功能表標題為 「 Microsoft Azure Powershell 」。</span><span class="sxs-lookup"><span data-stu-id="e18e7-195">You can run Azure Powershell from a shortcut on hello desktop or from hello start menu titled "Microsoft Azure Powershell".</span></span> <span data-ttu-id="e18e7-196">如需如何使用 Windows Powershell 指令碼管理 Azure 訂用帳戶和資源的詳細資訊，請參閱 [Microsoft Azure Powershell 文件](../powershell-azure-resource-manager.md) 。</span><span class="sxs-lookup"><span data-stu-id="e18e7-196">Refer to [Microsoft Azure Powershell documentation](../powershell-azure-resource-manager.md) for more information on how you can administer your Azure subscription and resources using Windows Powershell scripts.</span></span>

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a><span data-ttu-id="e18e7-197">5.使用共用的檔案系統來擴充您的儲存空間</span><span class="sxs-lookup"><span data-stu-id="e18e7-197">5. Extend your storage space with a shared file system</span></span>
<span data-ttu-id="e18e7-198">資料科學家可以共用大型資料集、 程式碼或 hello 小組內的其他資源。</span><span class="sxs-lookup"><span data-stu-id="e18e7-198">Data scientists can share large datasets, code or other resources within hello team.</span></span> <span data-ttu-id="e18e7-199">hello DSVM 本身有大約 70 GB 的可用空間。</span><span class="sxs-lookup"><span data-stu-id="e18e7-199">hello DSVM itself has about 70GB of space available.</span></span> <span data-ttu-id="e18e7-200">tooextend 您的儲存體，您可以使用 hello Azure 檔案服務，然後將其裝載在 hello DSVM 或存取透過 REST API。</span><span class="sxs-lookup"><span data-stu-id="e18e7-200">tooextend your storage, you can use hello Azure File Service and either mount it on hello DSVM or access it via a REST API.</span></span>   

> [!NOTE]
> <span data-ttu-id="e18e7-201">hello hello Azure 檔案服務共用的空間上限是 5 TB，個別的檔案大小上限為 1 TB。</span><span class="sxs-lookup"><span data-stu-id="e18e7-201">hello maximum space of hello Azure File Service share is 5TB and individual file size limit is 1TB.</span></span>   
> 
> 

<span data-ttu-id="e18e7-202">您可以使用 Azure Powershell toocreate Azure 檔案服務共用。</span><span class="sxs-lookup"><span data-stu-id="e18e7-202">You can use Azure Powershell toocreate an Azure File Service share.</span></span> <span data-ttu-id="e18e7-203">以下是在 Azure PowerShell toocreate Azure 檔案服務共用的 hello 指令碼 toorun。</span><span class="sxs-lookup"><span data-stu-id="e18e7-203">Here is hello script toorun under Azure PowerShell toocreate an Azure File service share.</span></span>

    # Authenticate tooAzure.
    Login-AzureRmAccount
    # Select your subscription
    Get-AzureRmSubscription –SubscriptionName "<your subscription name>" | Select-AzureRmSubscription
    # Create a new resource group.
    New-AzureRmResourceGroup -Name <dsvmdatarg>
    # Create a new storage account. You can reuse existing storage account if you wish.
    New-AzureRmStorageAccount -Name <mydatadisk> -ResourceGroupName <dsvmdatarg> -Location "<Azure Data Center Name For eg. South Central US>" -Type "Standard_LRS"
    # Set your current working storage account
    Set-AzureRmCurrentStorageAccount –ResourceGroupName "<dsvmdatarg>" –StorageAccountName <mydatadisk>

    # Create a Azure File Service Share
    $s = New-AzureStorageShare <<teamsharename>>
    # Create a directory under hello FIle share. You can give it any name
    New-AzureStorageDirectory -Share $s -Path <directory name>
    # List hello share tooconfirm that everything worked
    Get-AzureStorageFile -Share $s


<span data-ttu-id="e18e7-204">您現在已建立 Azure 檔案共用，即可將它掛接在 Azure 的任何虛擬機器中。</span><span class="sxs-lookup"><span data-stu-id="e18e7-204">Now that you have created an Azure file share, you can mount it in any virtual machine in Azure.</span></span> <span data-ttu-id="e18e7-205">強烈建議該 hello VM 處於相同的 Azure 資料中心為 hello 儲存體帳戶 tooavoid 延遲和資料傳輸費用。</span><span class="sxs-lookup"><span data-stu-id="e18e7-205">It is highly recommended that hello VM is in same Azure data center as hello storage account tooavoid latency and data transfer charges.</span></span> <span data-ttu-id="e18e7-206">以下是您可以在 Azure Powershell 執行的 DSVM hello hello 命令 toomount hello 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="e18e7-206">Here are hello commands toomount hello drive on hello DSVM that you can run on Azure Powershell.</span></span>

    # Get storage key of hello storage account that has hello Azure file share from Azure portal. Store it securely on hello VM tooavoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount hello Azure file share as Z: drive on hello VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


<span data-ttu-id="e18e7-207">現在您可以在 hello VM 上的任何標準磁碟機一樣，存取此磁碟機。</span><span class="sxs-lookup"><span data-stu-id="e18e7-207">Now you can access this drive as you would any normal drive on hello VM.</span></span>

## <a name="6-share-code-with-your-team-using-github"></a><span data-ttu-id="e18e7-208">6.使用 GitHub 與您的小組共用程式碼</span><span class="sxs-lookup"><span data-stu-id="e18e7-208">6. Share code with your team using GitHub</span></span>
<span data-ttu-id="e18e7-209">GitHub 是可以在哪裡找到大量的範例程式碼和來源使用共用的 hello 開發人員社群的各種技術的不同工具的程式碼儲存機制。</span><span class="sxs-lookup"><span data-stu-id="e18e7-209">GitHub is a code repository where you can find a lot of sample code and sources for different tools using various technologies shared by hello developer community.</span></span> <span data-ttu-id="e18e7-210">它會使用 Git hello hello 的程式碼檔案的技術 tootrack 和存放區版本。</span><span class="sxs-lookup"><span data-stu-id="e18e7-210">It uses Git as hello technology tootrack and store versions of hello code files.</span></span> <span data-ttu-id="e18e7-211">GitHub 也是平台可讓您建立您自己的儲存機制 toostore 您的小組共用的程式碼和文件，實作版本控制以及控制擁有存取 tooview 和程式碼撰寫。</span><span class="sxs-lookup"><span data-stu-id="e18e7-211">GitHub is also a platform where you can create your own repository toostore your team's shared code and documentation, implement version control and also control who have access tooview and contribute code.</span></span> <span data-ttu-id="e18e7-212">請瀏覽 hello [GitHub 說明網頁](https://help.github.com/)如需有關使用 Git。</span><span class="sxs-lookup"><span data-stu-id="e18e7-212">Please visit hello [GitHub help pages](https://help.github.com/) for more information on using Git.</span></span> <span data-ttu-id="e18e7-213">您可以使用 GitHub 做為其中一個 hello 方式 toocollaborate，與您的小組、 使用 hello 社群所開發的程式碼，並提供程式碼後 toohello 社群。</span><span class="sxs-lookup"><span data-stu-id="e18e7-213">You can use GitHub as one of hello ways toocollaborate with your team, use code developed by hello community and contribute code back toohello community.</span></span>

<span data-ttu-id="e18e7-214">hello DSVM 已上線時載入用戶端工具與命令列中以及 GUI tooaccess GitHub 儲存機制以兩者。</span><span class="sxs-lookup"><span data-stu-id="e18e7-214">hello DSVM already comes loaded with client tools on both command-line as well GUI tooaccess GitHub repository.</span></span> <span data-ttu-id="e18e7-215">使用 Git 及 GitHub hello 命令列工具 toowork 稱為 Git Bash。</span><span class="sxs-lookup"><span data-stu-id="e18e7-215">hello command-line tool toowork with Git and GitHub is called Git Bash.</span></span> <span data-ttu-id="e18e7-216">Hello DSVM 上安裝 visual Studio 有 hello Git 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="e18e7-216">Visual Studio installed on hello DSVM has hello Git extensions.</span></span> <span data-ttu-id="e18e7-217">您可以找到這些工具 hello 開始功能表和 hello 桌面啟動圖示。</span><span class="sxs-lookup"><span data-stu-id="e18e7-217">You can find start-up icons for these tools on hello start menu and hello desktop.</span></span>

<span data-ttu-id="e18e7-218">toodownload 程式碼從 GitHub 儲存機制中，您使用 hello```git clone```命令。</span><span class="sxs-lookup"><span data-stu-id="e18e7-218">toodownload code from a GitHub repository you use hello ```git clone``` command.</span></span> <span data-ttu-id="e18e7-219">例如 toodownload 資料科學儲存機制 Microsoft 所發行到 hello 目前目錄中您可以執行下列命令，當您在 hello ```git-bash```。</span><span class="sxs-lookup"><span data-stu-id="e18e7-219">For example toodownload data science repository published by Microsoft into hello current directory you can run hello following command once you are in ```git-bash```.</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="e18e7-220">在 Visual Studio 中，您可以執行 hello 相同的複製作業。</span><span class="sxs-lookup"><span data-stu-id="e18e7-220">In Visual Studio, you can do hello same clone operation.</span></span> <span data-ttu-id="e18e7-221">下列螢幕擷取畫面的 hello 顯示 tooaccess Git 及 GitHub 工具在 Visual Studio 中的方式。</span><span class="sxs-lookup"><span data-stu-id="e18e7-221">hello  following screen-shot shows how tooaccess Git and GitHub tools in Visual Studio.</span></span>

![Visual Studio 中的 Git](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

<span data-ttu-id="e18e7-223">您可以尋找在 Git toowork 使用您的 GitHub 儲存機制從 github.com 上可用的數個資源的詳細資訊。hello[小祕技](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf)是有用的參考。</span><span class="sxs-lookup"><span data-stu-id="e18e7-223">You can find more information on using Git toowork with your GitHub repository from several resources available on github.com. hello [cheat sheet](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) is a useful reference.</span></span>

## <a name="7-access-various-azure-data-and-analytics-services"></a><span data-ttu-id="e18e7-224">7.存取各種 Azure 資料和分析服務</span><span class="sxs-lookup"><span data-stu-id="e18e7-224">7. Access various Azure data and analytics services</span></span>
### <a name="azure-blob"></a><span data-ttu-id="e18e7-225">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="e18e7-225">Azure Blob</span></span>
<span data-ttu-id="e18e7-226">Azure blob 是可靠、划算的雲端儲存體，可存放大型和小型的資料。</span><span class="sxs-lookup"><span data-stu-id="e18e7-226">Azure blob is a reliable, economical cloud storage for data big and small.</span></span> <span data-ttu-id="e18e7-227">讓我們看看如何移動資料 tooAzure Blob 和 Azure Blob 中所儲存的存取資料。</span><span class="sxs-lookup"><span data-stu-id="e18e7-227">Let us look at how you can move data tooAzure Blob and access data stored in an Azure Blob.</span></span>

<span data-ttu-id="e18e7-228">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="e18e7-228">**Prerequisite**</span></span>

* <span data-ttu-id="e18e7-229">**從 [Azure 入口網站](https://portal.azure.com)建立 Azure Blob 儲存體帳戶。**</span><span class="sxs-lookup"><span data-stu-id="e18e7-229">**Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).**</span></span>

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="e18e7-231">確認該 hello 預先安裝命令列 AzCopy 工具位於```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```。</span><span class="sxs-lookup"><span data-stu-id="e18e7-231">Confirm that hello pre-installed command-line AzCopy tool is found at ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span></span> <span data-ttu-id="e18e7-232">執行此工具時，您可以加入 hello 目錄包含 hello azcopy.exe tooyour 環境變數 tooavoid 輸入 hello 完整命令的路徑。</span><span class="sxs-lookup"><span data-stu-id="e18e7-232">You can add hello directory containing hello azcopy.exe tooyour PATH environment variable tooavoid typing hello full command path when running this tool.</span></span> <span data-ttu-id="e18e7-233">如需 AzCopy 工具的詳細資訊，請參閱太[AzCopy 文件](../storage/common/storage-use-azcopy.md)</span><span class="sxs-lookup"><span data-stu-id="e18e7-233">For more info on AzCopy tool please refer too[AzCopy documentation](../storage/common/storage-use-azcopy.md)</span></span>
* <span data-ttu-id="e18e7-234">啟動 hello Azure 儲存體總管工具。</span><span class="sxs-lookup"><span data-stu-id="e18e7-234">Start hello Azure Storage Explorer tool.</span></span> <span data-ttu-id="e18e7-235">您可以從 [Microsoft Azure 儲存體總管](http://storageexplorer.com/)下載此工具。</span><span class="sxs-lookup"><span data-stu-id="e18e7-235">It can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

<span data-ttu-id="e18e7-237">**將資料從 VM tooAzure Blob 移： AzCopy**</span><span class="sxs-lookup"><span data-stu-id="e18e7-237">**Move data from VM tooAzure Blob: AzCopy**</span></span>

<span data-ttu-id="e18e7-238">將本機檔案和 blob 儲存體之間 toomove 資料，您可以在命令列使用 AzCopy 或 PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e18e7-238">toomove data between your local files and blob storage, you can use AzCopy in command-line or PowerShell:</span></span>

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

<span data-ttu-id="e18e7-239">取代**C:\myfolder** toohello 儲存您的檔案位置的路徑**mystorageaccount** tooyour blob 儲存體帳戶名稱， **mycontainer** toohello 容器名稱， **儲存體帳戶金鑰**tooyour blob 儲存體存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="e18e7-239">Replace **C:\myfolder** toohello path where your file is stored, **mystorageaccount** tooyour blob storage account name, **mycontainer** toohello container name, **storage account key** tooyour blob storage access key.</span></span> <span data-ttu-id="e18e7-240">您可以在 [Azure 入口網站](https://portal.azure.com)中尋找您的儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="e18e7-240">You can find your storage account credentials in [Azure portal](https://portal.azure.com).</span></span>

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

<span data-ttu-id="e18e7-242">在 PowerShell 或從命令提示字元執行 AzCopy 命令。</span><span class="sxs-lookup"><span data-stu-id="e18e7-242">Run AzCopy command in PowerShell or from a command prompt.</span></span> <span data-ttu-id="e18e7-243">以下是使用 AzCopy 命令的一些範例：</span><span class="sxs-lookup"><span data-stu-id="e18e7-243">Here is some example usage of AzCopy command:</span></span>

    # Copy *.sql from local machine tooa Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container tooLocal machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



<span data-ttu-id="e18e7-244">一旦您執行您的 AzCopy 命令 toocopy tooan Azure blob，您會看到您的檔案會出現在 Azure 儲存體總管很快。</span><span class="sxs-lookup"><span data-stu-id="e18e7-244">Once you run your AzCopy command toocopy tooan Azure blob you see your file shows up in Azure Storage Explorer shortly.</span></span>

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

<span data-ttu-id="e18e7-246">**將資料從 VM tooAzure Blob 移： Azure 儲存體總管**</span><span class="sxs-lookup"><span data-stu-id="e18e7-246">**Move data from VM tooAzure Blob: Azure Storage Explorer**</span></span>

<span data-ttu-id="e18e7-247">您也可以使用 Azure 儲存體總管在 VM 中上載 hello 本機檔案的資料：</span><span class="sxs-lookup"><span data-stu-id="e18e7-247">You can also upload data from hello local file in your VM using Azure Storage Explorer:</span></span>

* <span data-ttu-id="e18e7-248">tooupload 資料 tooa 容器、 選取 hello 目標容器，按一下 hello**上傳** 按鈕。![儲存體總管中上傳](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span><span class="sxs-lookup"><span data-stu-id="e18e7-248">tooupload data tooa container, select hello target container and click hello **Upload** button.![Upload in Storage Explorer](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span></span>
* <span data-ttu-id="e18e7-249">按一下 hello **...**方 hello toohello**檔案**方塊選取一個或多個檔案 tooupload hello 檔案系統中，按一下**上傳**toobegin hello 檔案上載。![上傳檔案 tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span><span class="sxs-lookup"><span data-stu-id="e18e7-249">Click on hello **...** toohello right of hello **Files** box, select one or multiple files tooupload from hello file system and click **Upload** toobegin uploading hello files.![Upload files tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span></span>

<span data-ttu-id="e18e7-250">**從 Azure Blob 讀取資料：Machine Learning 讀取器模組**</span><span class="sxs-lookup"><span data-stu-id="e18e7-250">**Read data from Azure Blob: Machine Learning reader module**</span></span>

<span data-ttu-id="e18e7-251">您可以使用 Azure Machine Learning Studio**資料匯入模組**tooread 資料從您的 blob。</span><span class="sxs-lookup"><span data-stu-id="e18e7-251">In Azure Machine Learning Studio you can use an **Import Data module** tooread data from your blob.</span></span>

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

<span data-ttu-id="e18e7-253">**從 Azure Blob 讀取資料：Python ODBC**</span><span class="sxs-lookup"><span data-stu-id="e18e7-253">**Read data from Azure Blob: Python ODBC**</span></span>

<span data-ttu-id="e18e7-254">您可以使用**BlobService**媒體櫃 tooread 資料直接從 Jupyter 筆記本或 Python 程式中的 blob。</span><span class="sxs-lookup"><span data-stu-id="e18e7-254">You can use **BlobService** library tooread data directly from blob in a Jupyter Notebook or Python program.</span></span>

<span data-ttu-id="e18e7-255">首先，匯入所需的封裝：</span><span class="sxs-lookup"><span data-stu-id="e18e7-255">First, import required packages:</span></span>

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

<span data-ttu-id="e18e7-256">然後插入您的 Azure Blob 帳戶認證並從 Blob 讀取資料：</span><span class="sxs-lookup"><span data-stu-id="e18e7-256">Then plug in your Azure Blob account credentials and read data from Blob:</span></span>

    CONTAINERNAME = 'xxx'
    STORAGEACCOUNTNAME = 'xxxx'
    STORAGEACCOUNTKEY = 'xxxxxxxxxxxxxxxx'
    BLOBNAME = 'nyctaxidataset/nyctaxitrip/trip_data_1.csv'
    localfilename = 'trip_data_1.csv'
    LOCALDIRECTORY = os.getcwd()
    LOCALFILE =  os.path.join(LOCALDIRECTORY, localfilename)

    #download from blob
    t1 = time.time()
    blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
    blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILE)
    t2 = time.time()
    print(("It takes %s seconds toodownload "+BLOBNAME) % (t2 - t1))

    #unzipping downloaded files if needed
    #with zipfile.ZipFile(ZIPPEDLOCALFILE, "r") as z:
    #    z.extractall(LOCALDIRECTORY)

    df1 = pd.read_csv(LOCALFILE, header=0)
    df1.columns = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime','passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude']
    print 'hello size of hello data is: %d rows and  %d columns' % df1.shape

<span data-ttu-id="e18e7-257">hello 資料被視為資料框架中：</span><span class="sxs-lookup"><span data-stu-id="e18e7-257">hello data is read in as a data frame:</span></span>

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a><span data-ttu-id="e18e7-259">Azure 資料湖</span><span class="sxs-lookup"><span data-stu-id="e18e7-259">Azure Data Lake</span></span>
<span data-ttu-id="e18e7-260">Azure Data Lake 儲存體是巨量資料分析工作負載的超大規模儲存機制，與 Hadoop 分散式檔案系統 (HDFS) 相容。</span><span class="sxs-lookup"><span data-stu-id="e18e7-260">Azure Data Lake Storage is a hyper-scale repository for big data analytics workloads and compatible with Hadoop Distributed File System (HDFS).</span></span> <span data-ttu-id="e18e7-261">它可搭配 hello Hadoop 生態系統和 hello Azure Data Lake Analytics。</span><span class="sxs-lookup"><span data-stu-id="e18e7-261">It works with both hello Hadoop ecosystem and hello Azure Data Lake Analytics.</span></span> <span data-ttu-id="e18e7-262">我們會示範如何將資料移入 hello Azure 資料湖存放區，並執行使用 Azure Data Lake Analytics 分析。</span><span class="sxs-lookup"><span data-stu-id="e18e7-262">We show how you can move data into hello Azure Data Lake Store and run analytics using Azure Data Lake Analytics.</span></span>

<span data-ttu-id="e18e7-263">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="e18e7-263">**Prerequisite**</span></span>

* <span data-ttu-id="e18e7-264">在 [Azure 入口網站](https://portal.azure.com)中建立 Azure Data Lake Analytics。</span><span class="sxs-lookup"><span data-stu-id="e18e7-264">Create your Azure Data Lake Analytics in [Azure portal](https://portal.azure.com).</span></span>

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* <span data-ttu-id="e18e7-266">hello **Azure Data Lake Tools**中**Visual Studio**位於這[連結](https://www.microsoft.com/download/details.aspx?id=49504)hello hello 虛擬機器上的 Visual Studio Community Edition 上已安裝。</span><span class="sxs-lookup"><span data-stu-id="e18e7-266">hello  **Azure Data Lake Tools** in **Visual Studio** found at this  [link](https://www.microsoft.com/download/details.aspx?id=49504) is already installed on hello Visual Studio Community Edition which is on hello virtual machine.</span></span> <span data-ttu-id="e18e7-267">之後啟動 Visual Studio，並記錄您 Azure 訂用帳戶中，您應該會看到您的 Azure 資料分析帳戶和 hello 的 Visual Studio 的左面板中的儲存體。</span><span class="sxs-lookup"><span data-stu-id="e18e7-267">After starting Visual Studio and logging in your Azure subscription, you should see your Azure Data Analytics account and storage in hello left panel of Visual Studio.</span></span>

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

<span data-ttu-id="e18e7-269">**將資料從 VM tooData Lake 移： Azure Data Lake 總管**</span><span class="sxs-lookup"><span data-stu-id="e18e7-269">**Move data from VM tooData Lake: Azure Data Lake Explorer**</span></span>

<span data-ttu-id="e18e7-270">您可以使用**Azure Data Lake 總管**tooupload 資料從虛擬機器 tooData Lake 的存放裝置中的 hello 本機檔案。</span><span class="sxs-lookup"><span data-stu-id="e18e7-270">You can use **Azure Data Lake Explorer** tooupload data from hello local files in your Virtual Machine tooData Lake storage.</span></span>

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

<span data-ttu-id="e18e7-272">您也可以建立資料管線 tooproductionize 您從 Azure Data Lake 的資料移動 tooor 使用 hello [Azure 資料 Factory(ADF)](https://azure.microsoft.com/services/data-factory/)。</span><span class="sxs-lookup"><span data-stu-id="e18e7-272">You can also build a data pipeline tooproductionize your data movement tooor from Azure Data Lake using hello [Azure Data Factory(ADF)](https://azure.microsoft.com/services/data-factory/).</span></span> <span data-ttu-id="e18e7-273">我們參照 toothis[文章](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/)tooguide 您透過 hello 步驟 toobuild hello 資料管線。</span><span class="sxs-lookup"><span data-stu-id="e18e7-273">We refer you toothis [article](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide you through hello steps toobuild hello data pipelines.</span></span>

<span data-ttu-id="e18e7-274">**從 Azure Blob tooData 湖讀取資料： U-SQL**</span><span class="sxs-lookup"><span data-stu-id="e18e7-274">**Read data from Azure Blob tooData Lake: U-SQL**</span></span>

<span data-ttu-id="e18e7-275">如果您的資料位於 Azure Blob 儲存體中，您可以在 U-SQL 查詢中從 Azure 儲存體 Blob 直接讀取資料。</span><span class="sxs-lookup"><span data-stu-id="e18e7-275">If your data resides in Azure Blob storage, you can directly read data from Azure storage blob in U-SQL query.</span></span> <span data-ttu-id="e18e7-276">之前撰寫 U SQL 查詢，請確定您的 blob 儲存體帳戶是連結的 tooyour Azure 資料湖。</span><span class="sxs-lookup"><span data-stu-id="e18e7-276">Before composing your U-SQL query, make sure your blob storage account is linked tooyour Azure Data Lake.</span></span> <span data-ttu-id="e18e7-277">跳過**Azure 入口網站**，尋找您的 Azure Data Lake Analytics 儀表板，按一下**加入資料來源**，選取儲存體類型太**Azure 儲存體**並插入您的 Azure 儲存體帳戶名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="e18e7-277">Go too**Azure portal**, find your Azure Data Lake Analytics dashboard, click **Add Data Source**, select storage type too**Azure Storage** and plug in your Azure Storage Account Name and Key.</span></span> <span data-ttu-id="e18e7-278">您已無法 tooreference hello 資料儲存在 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e18e7-278">Then you are able tooreference hello data stored in hello storage account.</span></span>

![輸入儲存體帳戶和金鑰](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

<span data-ttu-id="e18e7-280">在 Visual Studio 中，您可以從 blob 儲存體讀取資料、 執行一些資料操作、 特徵設計和輸出 hello 產生資料 tooeither Azure 資料湖或 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="e18e7-280">In Visual Studio, you can read data from blob storage, do some data manipulation, feature engineering, and output hello resulting data tooeither Azure Data Lake or Azure Blob Storage.</span></span> <span data-ttu-id="e18e7-281">當您參考 blob 儲存體中的 hello 資料時，使用**wasb: / /**; 當您參考 Azure Data Lake，使用中的 hello 資料**swbhdfs: / /**</span><span class="sxs-lookup"><span data-stu-id="e18e7-281">When you reference hello data in blob storage, use **wasb://**; when you reference hello data in Azure Data Lake, use **swbhdfs://**</span></span>

![資料框架](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

<span data-ttu-id="e18e7-283">您可以使用下列 U SQL 查詢，在 Visual Studio 中的 hello:</span><span class="sxs-lookup"><span data-stu-id="e18e7-283">You may use hello following U-SQL queries in Visual Studio:</span></span>

    @a =
        EXTRACT medallion string,
                hack_license string,
                vendor_id string,
                rate_code string,
                store_and_fwd_flag string,
                pickup_datetime string,
                dropoff_datetime string,
                passenger_count int,
                trip_time_in_secs double,
                trip_distance double,
                pickup_longitude string,
                pickup_latitude string,
                dropoff_longitude string,
                dropoff_latitude string

        FROM "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Input Data File Name>"
        USING Extractors.Csv();

    @b =
        SELECT vendor_id,
        COUNT(medallion) AS cnt_medallion,
        SUM(passenger_count) AS cnt_passenger,
        AVG(trip_distance) AS avg_trip_dist,
        MIN(trip_distance) AS min_trip_dist,
        MAX(trip_distance) AS max_trip_dist,
        AVG(trip_time_in_secs) AS avg_trip_time
        FROM @a
        GROUP BY vendor_id;

    OUTPUT @b   
    too"swebhdfs://<Azure Data Lake Storage Account Name>.azuredatalakestore.net/<Folder Name>/<Output Data File Name>"
    USING Outputters.Csv();

    OUTPUT @b   
    too"wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Output Data File Name>"
    USING Outputters.Csv();



<span data-ttu-id="e18e7-284">您的查詢會提交的 toohello 伺服器之後，會顯示圖表，顯示您工作的 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="e18e7-284">After your query is submitted toohello server, a diagram showing hello status of your job is displayed.</span></span>

![作業狀態圖表](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

<span data-ttu-id="e18e7-286">**查詢資料湖中的資料：U-SQL**</span><span class="sxs-lookup"><span data-stu-id="e18e7-286">**Query data in Data Lake: U-SQL**</span></span>

<span data-ttu-id="e18e7-287">Hello 資料集是內嵌至 Azure 資料湖之後，您可以使用[U-SQL 語言](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md)tooquery 和瀏覽 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="e18e7-287">After hello dataset is ingested into Azure Data Lake, you can use [U-SQL language](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery and explore hello data.</span></span> <span data-ttu-id="e18e7-288">U SQL 語言是類似的 tooT SQL，但結合從 C# 的某些功能，讓使用者都可以寫入自訂的模組、 使用者定義函式和等等。Hello 上一個步驟中，您可以使用 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="e18e7-288">U-SQL language is similar tooT-SQL, but combines some features from C# so that users can write customized modules, user-defined functions, and etc. You can use hello scripts in hello previous step.</span></span>

<span data-ttu-id="e18e7-289">已提交的 tooserver，tripdata_summary hello 查詢之後。CSV 可以在稍後**Azure Data Lake 總管**，您可以預覽 hello 資料，以滑鼠右鍵按一下 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="e18e7-289">After hello query is submitted tooserver, tripdata_summary.CSV can be found shortly in **Azure Data Lake Explorer**, you may preview hello data by right-click hello file.</span></span>

![Azure Data Lake Explorer 中的檔案](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

<span data-ttu-id="e18e7-291">toosee hello 檔案資訊：</span><span class="sxs-lookup"><span data-stu-id="e18e7-291">toosee hello file information:</span></span>

![檔案摘要](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a><span data-ttu-id="e18e7-293">HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="e18e7-293">HDInsight Hadoop Clusters</span></span>
<span data-ttu-id="e18e7-294">Azure HDInsight 是 hello 雲端上的 Apache Hadoop、 Spark、 HBase 和 Storm 受管理的服務。</span><span class="sxs-lookup"><span data-stu-id="e18e7-294">Azure HDInsight is a managed Apache Hadoop, Spark, HBase, and Storm service on hello cloud.</span></span> <span data-ttu-id="e18e7-295">您可以輕鬆地處理從 hello data science 虛擬機器的 Azure HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e18e7-295">You can work easily with Azure HDInsight clusters from hello data science virtual machine.</span></span>

<span data-ttu-id="e18e7-296">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="e18e7-296">**Prerequisite**</span></span>

* <span data-ttu-id="e18e7-297">從 [Azure 入口網站](https://portal.azure.com)建立 Azure Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e18e7-297">Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e18e7-298">這個儲存體帳戶是使用的 toostore 資料 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e18e7-298">This storage account is used toostore data for HDInsight clusters.</span></span>

![建立 Azure Blob 儲存體帳戶](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="e18e7-300">從 [Azure 入口網站](machine-learning-data-science-customize-hadoop-cluster.md)</span><span class="sxs-lookup"><span data-stu-id="e18e7-300">Customize Azure HDInsight Hadoop Clusters from [Azure portal](machine-learning-data-science-customize-hadoop-cluster.md)</span></span>
  
  * <span data-ttu-id="e18e7-301">您必須連結 hello 時就會建立使用您的 HDInsight 叢集建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e18e7-301">You must link hello storage account created with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="e18e7-302">這個儲存體帳戶用來存取可處理 hello 叢集內的資料。</span><span class="sxs-lookup"><span data-stu-id="e18e7-302">This storage account is used for accessing data that can be processed within hello cluster.</span></span>

![建立與 HDInsight 叢集連結 toostorage 帳戶](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* <span data-ttu-id="e18e7-304">您必須啟用**遠端存取**toohello 建立後的 hello 叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="e18e7-304">You must enable **Remote Access** toohello head node of hello cluster after it is created.</span></span> <span data-ttu-id="e18e7-305">請記住您在此處指定 （不同於所指定的 hello 在其建立的叢集） hello 遠端存取認證： hello 後續程序中需要它們。</span><span class="sxs-lookup"><span data-stu-id="e18e7-305">Remember hello remote access credentials you specify here (different from those specified for hello cluster at its creation): you need them in hello subsequent procedure.</span></span>

![啟用遠端存取](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* <span data-ttu-id="e18e7-307">建立 Azure Machine Learning 工作區。</span><span class="sxs-lookup"><span data-stu-id="e18e7-307">Create an Azure Machine Learning workspace.</span></span> <span data-ttu-id="e18e7-308">您的機器學習實驗將會儲存在此 Machine Learning 工作區中。</span><span class="sxs-lookup"><span data-stu-id="e18e7-308">Your Machine Learning Experiments are stored in this Machine Learning workspace.</span></span> <span data-ttu-id="e18e7-309">選取 hello 反白顯示在入口網站中的選項，hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="e18e7-309">Select hello highlighted options in Portal as shown in hello following screenshot:</span></span>

![建立 Azure Machine Learning 工作區](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* <span data-ttu-id="e18e7-311">然後輸入 hello 參數，您的工作區</span><span class="sxs-lookup"><span data-stu-id="e18e7-311">Then enter hello parameters for your workspace</span></span>

![輸入 Machine Learning 工作區參數](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* <span data-ttu-id="e18e7-313">使用 IPython Notebook 上傳資料。</span><span class="sxs-lookup"><span data-stu-id="e18e7-313">Upload data using IPython Notebook.</span></span> <span data-ttu-id="e18e7-314">第一個所需的匯入封裝，插入的認證，請在儲存體帳戶中建立資料庫，然後載入資料 tooHDI 叢集。</span><span class="sxs-lookup"><span data-stu-id="e18e7-314">First import required packages, plug in credentials, create a db in your storage account, then load data tooHDI clusters.</span></span>

        #Import required Packages
        import pyodbc
        import time as time
        import json
        import os
        import urllib
        import urllib2
        import warnings
        import re
        import pandas as pd
        import matplotlib.pyplot as plt
        from azure.storage.blob import BlobService
        warnings.filterwarnings("ignore", category=UserWarning, module='urllib2')


        #Create hello connection tooHive using ODBC
        SERVER_NAME='xxx.azurehdinsight.net'
        DATABASE_NAME='nyctaxidb'
        USERID='xxx'
        PASSWORD='xxxx'
        DB_DRIVER='Microsoft Hive ODBC Driver'
        driver = 'DRIVER={' + DB_DRIVER + '}'
        server = 'Host=' + SERVER_NAME + ';Port=443'
        database = 'Schema=' + DATABASE_NAME
        hiveserv = 'HiveServerType=2'
        auth = 'AuthMech=6'
        uid = 'UID=' + USERID
        pwd = 'PWD=' + PASSWORD
        CONNECTION_STRING = ';'.join([driver,server,database,hiveserv,auth,uid,pwd])
        connection = pyodbc.connect(CONNECTION_STRING, autocommit=True)
        cursor=connection.cursor()


        #Create Hive database and tables
        queryString = "create database if not exists nyctaxidb;"
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.trip
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            rate_code string,
                            store_and_fwd_flag string,
                            pickup_datetime string,
                            dropoff_datetime string,
                            passenger_count int,
                            trip_time_in_secs double,
                            trip_distance double,
                            pickup_longitude double,
                            pickup_latitude double,
                            dropoff_longitude double,
                            dropoff_latitude double)  
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.fare
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            pickup_datetime string,
                            payment_type string,
                            fare_amount double,
                            surcharge double,
                            mta_tax double,
                            tip_amount double,
                            tolls_amount double,
                            total_amount double)
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)


        #Upload data from blob storage tooHDI cluster
        for i in range(1,13):
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxitripraw2/trip_data_%d.csv' INTO TABLE nyctaxidb2.trip PARTITION (month=%d);"%(i,i)
            cursor.execute(queryString)
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxifareraw2/trip_fare_%d.csv' INTO TABLE nyctaxidb2.fare PARTITION (month=%d);"%(i,i)  
            cursor.execute(queryString)


* <span data-ttu-id="e18e7-315">或者，您可以依照這[逐步解說](machine-learning-data-science-process-hive-walkthrough.md)tooupload NYC 計程車資料 tooHDI 叢集。</span><span class="sxs-lookup"><span data-stu-id="e18e7-315">Alternately,  you can follow this [walkthrough](machine-learning-data-science-process-hive-walkthrough.md) tooupload NYC Taxi data tooHDI cluster.</span></span> <span data-ttu-id="e18e7-316">主要步驟包括：</span><span class="sxs-lookup"><span data-stu-id="e18e7-316">Major steps include:</span></span>
  
  * <span data-ttu-id="e18e7-317">AzCopy： 下載公用 blob tooyour 本機資料夾從壓縮的 CSV</span><span class="sxs-lookup"><span data-stu-id="e18e7-317">AzCopy: download zipped CSV's from public blob tooyour local folder</span></span>
  * <span data-ttu-id="e18e7-318">AzCopy： 上傳解壓縮的 CSV 的從本機資料夾 tooHDI 叢集</span><span class="sxs-lookup"><span data-stu-id="e18e7-318">AzCopy: upload unzipped CSV's from local folder tooHDI cluster</span></span>
  * <span data-ttu-id="e18e7-319">登入 hello Hadoop 叢集前端節點，並準備進行探勘測試的資料分析</span><span class="sxs-lookup"><span data-stu-id="e18e7-319">Log into hello head node of Hadoop cluster and prepare for exploratory data analysis</span></span>

<span data-ttu-id="e18e7-320">Hello 資料是載入的 tooHDI 叢集之後，您可以檢查您在 Azure 儲存體總管 中的資料。</span><span class="sxs-lookup"><span data-stu-id="e18e7-320">After hello data is loaded tooHDI cluster, you can check your data in Azure Storage Explorer.</span></span> <span data-ttu-id="e18e7-321">而您會在 HDI 叢集中建立資料庫 nyctaxidb。</span><span class="sxs-lookup"><span data-stu-id="e18e7-321">And you have a database nyctaxidb created in HDI cluster.</span></span>

<span data-ttu-id="e18e7-322">**資料探索：Python 中的 Hive 查詢**</span><span class="sxs-lookup"><span data-stu-id="e18e7-322">**Data exploration: Hive Queries in Python**</span></span>

<span data-ttu-id="e18e7-323">由於 hello 資料在 Hadoop 叢集，您可以使用 hello pyodbc 封裝 tooconnect tooHadoop 叢集與使用 Hive toodo 瀏覽和特徵設計查詢資料庫。</span><span class="sxs-lookup"><span data-stu-id="e18e7-323">Since hello data is in Hadoop cluster, you can use hello pyodbc package tooconnect tooHadoop Clusters and query database using Hive toodo exploration and feature engineering.</span></span> <span data-ttu-id="e18e7-324">您可以檢視 hello hello 必要的步驟中建立的現有資料表。</span><span class="sxs-lookup"><span data-stu-id="e18e7-324">You can view hello existing tables we created in hello prerequisite step.</span></span>

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![檢視現有的表格](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

<span data-ttu-id="e18e7-326">讓我們看看 hello 中的記錄數的每個月份和 hello 頻率 （雪人） 或不在 hello 路線資料表：</span><span class="sxs-lookup"><span data-stu-id="e18e7-326">Let's look at hello number of records in each month and hello frequencies of tipped or not in hello trip table:</span></span>

    queryString = """
        select month, count(*) from nyctaxidb.trip group by month;
        """
    results = pd.read_sql(queryString,connection)

    %matplotlib inline

    results.columns = ['month', 'trip_count']
    df = results.copy()
    df.index = df['month']
    df['trip_count'].plot(kind='bar')


![每個月的記錄數繪圖](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Number_Records_by_Month_v3.PNG)

    queryString = """
        SELECT tipped, COUNT(*) AS tip_freq
        FROM
        (
            SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
            FROM nyctaxidb.fare
        )tc
        GROUP BY tipped;
        """
    results = pd.read_sql(queryString,connection)

    results.columns = ['tipped', 'trip_count']
    df = results.copy()
    df.index = df['tipped']
    df['trip_count'].plot(kind='bar')


![小費頻率繪圖](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Frequency_tip_or_not_v3.PNG)

<span data-ttu-id="e18e7-329">我們可以也計算 hello 收取位置與 dropoff 位置之間的距離，然後比較 toohello 成為距離。</span><span class="sxs-lookup"><span data-stu-id="e18e7-329">We can also compute hello distance between pickup location and dropoff location and then compare it toohello trip distance.</span></span>

    queryString = """
                    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
                        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
                        *radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
                        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
                        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
                        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*
                        pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance
                        from nyctaxidb.trip
                        where month=1
                            and pickup_longitude between -90 and -30
                            and pickup_latitude between 30 and 90
                            and dropoff_longitude between -90 and -30
                            and dropoff_latitude between 30 and 90;
                """
    results = pd.read_sql(queryString,connection)
    results.head(5)


![上下車資料表](./media/machine-learning-data-science-vm-do-ten-things/Exploration_compute_pickup_dropoff_distance_v2.PNG)

    results.columns = ['pickup_longitude', 'pickup_latitude', 'dropoff_longitude',
                       'dropoff_latitude', 'trip_distance', 'trip_time_in_secs', 'direct_distance']
    df = results.loc[results['trip_distance']<=100] #remove outliers
    df = df.loc[df['direct_distance']<=100] #remove outliers
    plt.scatter(df['direct_distance'], df['trip_distance'])


![收取/dropoff 距離 tootrip 距離的圖](./media/machine-learning-data-science-vm-do-ten-things/Exploration_direct_distance_trip_distance_v2.PNG)

<span data-ttu-id="e18e7-332">現在讓我們準備縮減取樣 (1%) 資料集，以便進行模型分析。</span><span class="sxs-lookup"><span data-stu-id="e18e7-332">Now let's prepare a down-sampled (1%) set of data for modeling.</span></span> <span data-ttu-id="e18e7-333">我們可以在 Machine Learning 讀取器模組中使用此資料。</span><span class="sxs-lookup"><span data-stu-id="e18e7-333">We can use this data in Machine Learning reader module.</span></span>

        queryString = """
        create  table if not exists nyctaxi_downsampled_dataset_testNEW (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\\n'
        stored as textfile;
        """
        cursor.execute(queryString)

        --- now insert contents of hello join into hello preceding internal table

        queryString = """
        insert overwrite table nyctaxi_downsampled_dataset_testNEW
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class
        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance,
        rand() as sample_key

        from trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01
        """
        cursor.execute(queryString)

<span data-ttu-id="e18e7-334">在一段時間之後, 您可以看到已經載入 hello 資料在 Hadoop 叢集：</span><span class="sxs-lookup"><span data-stu-id="e18e7-334">After a while, you can see hello data has been loaded in Hadoop clusters:</span></span>

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![資料表](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

<span data-ttu-id="e18e7-336">**使用 Machine Learning 從 HDI 讀取資料：讀取器模組**</span><span class="sxs-lookup"><span data-stu-id="e18e7-336">**Read data from HDI using Machine Learning: reader module**</span></span>

<span data-ttu-id="e18e7-337">您也可以使用 hello**讀取器**Machine Learning Studio tooaccess hello 資料庫 Hadoop 叢集中的模組中。</span><span class="sxs-lookup"><span data-stu-id="e18e7-337">You may also use hello **reader** module in Machine Learning Studio tooaccess hello database in Hadoop cluster.</span></span> <span data-ttu-id="e18e7-338">插入的 HDI 叢集 hello 認證，Azure 儲存體帳戶 tooenable 建置正執行機器學習模型 HDI 叢集在使用資料庫。</span><span class="sxs-lookup"><span data-stu-id="e18e7-338">Plug in hello credentials of your HDI clusters and Azure Storage Account tooenable build ing machine learning models using database in HDI clusters.</span></span>

![讀取器模組屬性](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

<span data-ttu-id="e18e7-340">hello 評分資料集之後可以檢視：</span><span class="sxs-lookup"><span data-stu-id="e18e7-340">hello scored dataset can then be viewed:</span></span>

![檢視已評分的資料集](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a><span data-ttu-id="e18e7-342">Azure SQL 資料倉儲和資料庫</span><span class="sxs-lookup"><span data-stu-id="e18e7-342">Azure SQL Data Warehouse & databases</span></span>
<span data-ttu-id="e18e7-343">Azure SQL 資料倉儲是彈性的資料倉儲即服務，具有企業層級的 SQL Server 體驗。</span><span class="sxs-lookup"><span data-stu-id="e18e7-343">Azure SQL Data Warehouse is an elastic data warehouse as a service with enterprise-class SQL Server experience.</span></span>

<span data-ttu-id="e18e7-344">您可以依照 hello 指示在此提供佈建 Azure SQL 資料倉儲[文章](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md)。</span><span class="sxs-lookup"><span data-stu-id="e18e7-344">You can provision your Azure SQL Data Warehouse by following hello instructions provided in this [article](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span></span> <span data-ttu-id="e18e7-345">一旦您佈建 Azure SQL 資料倉儲，您可以使用這個[逐步解說](machine-learning-data-science-process-sqldw-walkthrough.md)toodo 上傳的資料，探索和使用 hello SQL 資料倉儲內的資料模型。</span><span class="sxs-lookup"><span data-stu-id="e18e7-345">Once you provision your Azure SQL Data Warehouse, you can use this [walkthrough](machine-learning-data-science-process-sqldw-walkthrough.md) toodo data upload, exploration and modeling using data within hello SQL Data Warehouse.</span></span>

#### <a name="azure-cosmos-db"></a><span data-ttu-id="e18e7-346">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e18e7-346">Azure Cosmos DB</span></span>
<span data-ttu-id="e18e7-347">Azure Cosmos DB 是 hello 雲端的 NoSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e18e7-347">Azure Cosmos DB is a NoSQL database in hello cloud.</span></span> <span data-ttu-id="e18e7-348">它可讓您 toowork 類似 JSON 文件，並可讓您 toostore 和查詢 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="e18e7-348">It allows you toowork with documents like JSON and allows you toostore and query hello documents.</span></span>

<span data-ttu-id="e18e7-349">您需要的 hello DSVM 下列每個必要條件步驟 tooaccess Azure Cosmos DB toodo hello。</span><span class="sxs-lookup"><span data-stu-id="e18e7-349">You need toodo hello following per-requisites steps tooaccess Azure Cosmos DB from hello DSVM.</span></span>

1. <span data-ttu-id="e18e7-350">安裝 DocumentDB Python SDK (從命令提示字元執行 ```pip install pydocumentdb``` )</span><span class="sxs-lookup"><span data-stu-id="e18e7-350">Install DocumentDB Python SDK (Run ```pip install pydocumentdb``` from command prompt)</span></span>
2. <span data-ttu-id="e18e7-351">從 [Azure 入口網站](https://portal.azure.com)建立 Azure Cosmos DB 帳戶和資料庫</span><span class="sxs-lookup"><span data-stu-id="e18e7-351">Create an Azure Cosmos DB account and a database from [Azure portal](https://portal.azure.com)</span></span>
3. <span data-ttu-id="e18e7-352">從下載 < Azure Cosmos DB 移轉工具 >[這裡](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d)並解壓縮您選擇的 tooa 目錄</span><span class="sxs-lookup"><span data-stu-id="e18e7-352">Download "Azure Cosmos DB Migration Tool" from [here](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) and extract tooa directory of your choice</span></span>
4. <span data-ttu-id="e18e7-353">匯入 JSON 資料 （火山資料） 儲存在[公用 blob](https://cahandson.blob.core.windows.net/samples/volcano.json)到 Cosmos DB，利用下列命令參數 toohello 移轉工具 (dtui.exe hello hello Cosmos DB 移轉工具的安裝所在的目錄中)。</span><span class="sxs-lookup"><span data-stu-id="e18e7-353">Import JSON data (volcano data) stored on a [public blob](https://cahandson.blob.core.windows.net/samples/volcano.json) into Cosmos DB with following command parameters toohello migration tool (dtui.exe from hello directory where you installed hello Cosmos DB Migration Tool).</span></span> <span data-ttu-id="e18e7-354">輸入 hello 來源和目標位置，使用這些參數：</span><span class="sxs-lookup"><span data-stu-id="e18e7-354">Enter hello source and target location with these parameters:</span></span>
   
    <span data-ttu-id="e18e7-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span><span class="sxs-lookup"><span data-stu-id="e18e7-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span></span>

<span data-ttu-id="e18e7-356">一旦您匯入 hello 資料，您可以移 tooJupyter 然後開啟 hello 筆記本標題為*DocumentDBSample*包含 python 程式碼 tooaccess DocumentDB 並執行一些基本的查詢。</span><span class="sxs-lookup"><span data-stu-id="e18e7-356">Once you import hello data, you can go tooJupyter and open hello notebook titled *DocumentDBSample* which contains python code tooaccess DocumentDB and do some basic querying.</span></span> <span data-ttu-id="e18e7-357">您可以進一步了解 Cosmos DB 瀏覽 hello 服務[文件頁面](https://docs.microsoft.com/azure/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="e18e7-357">You can learn more about Cosmos DB by visiting hello service [documentation page](https://docs.microsoft.com/azure/cosmos-db/).</span></span>

## <a name="8-build-reports-and-dashboard-using-hello-power-bi-desktop"></a><span data-ttu-id="e18e7-358">8.建立報表和儀表板使用 hello Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="e18e7-358">8. Build reports and dashboard using hello Power BI Desktop</span></span>
<span data-ttu-id="e18e7-359">讓我們將視覺化 hello 在 Power BI toogain 視覺化資料的深入 hello 之前 Cosmos DB 範例中的 hello 火山 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="e18e7-359">Let us visualize hello Volcano JSON file that we saw in hello preceding Cosmos DB example in Power BI toogain visual insights into hello data.</span></span> <span data-ttu-id="e18e7-360">會提供在 hello 詳細的步驟[Power BI 文件](../cosmos-db/powerbi-visualize.md)。</span><span class="sxs-lookup"><span data-stu-id="e18e7-360">Detailed steps are available in hello [Power BI article](../cosmos-db/powerbi-visualize.md).</span></span> <span data-ttu-id="e18e7-361">Hello 高階步驟如下：</span><span class="sxs-lookup"><span data-stu-id="e18e7-361">Here are hello high-level steps:</span></span>

1. <span data-ttu-id="e18e7-362">開啟 Power BI Desktop 並執行「取得資料」。</span><span class="sxs-lookup"><span data-stu-id="e18e7-362">Open Power BI Desktop and do "Get Data".</span></span> <span data-ttu-id="e18e7-363">指定與 hello URL: https://cahandson.blob.core.windows.net/samples/volcano.json</span><span class="sxs-lookup"><span data-stu-id="e18e7-363">Specify hello URL as: https://cahandson.blob.core.windows.net/samples/volcano.json</span></span>
2. <span data-ttu-id="e18e7-364">您應該會看見 hello JSON 記錄清單以匯入</span><span class="sxs-lookup"><span data-stu-id="e18e7-364">You should see hello JSON records imported as a list</span></span>
3. <span data-ttu-id="e18e7-365">轉換 hello 清單 tooa 資料表，以便讓 Power BI 可以搭配 hello 相同</span><span class="sxs-lookup"><span data-stu-id="e18e7-365">Convert hello list tooa table so Power BI can work with hello same</span></span>
4. <span data-ttu-id="e18e7-366">展開即可 hello hello 資料行展開圖示 (hello 一個 hello hello 方 hello 資料行上的 「 向的左鍵和向右箭號 」 圖示)</span><span class="sxs-lookup"><span data-stu-id="e18e7-366">Expand hello columns by clicking on hello expand icon (hello one with hello "left arrow and a right arrow" icon on hello right of hello column)</span></span>
5. <span data-ttu-id="e18e7-367">請注意，該位置是「記錄」欄位。</span><span class="sxs-lookup"><span data-stu-id="e18e7-367">Notice that location is a "Record" field.</span></span> <span data-ttu-id="e18e7-368">展開 hello 記錄，然後選取 只 hello 座標。</span><span class="sxs-lookup"><span data-stu-id="e18e7-368">Expand hello record and select only hello coordinates.</span></span> <span data-ttu-id="e18e7-369">座標是清單資料行</span><span class="sxs-lookup"><span data-stu-id="e18e7-369">Coordinate is a list column</span></span>
6. <span data-ttu-id="e18e7-370">將新資料行 tooconvert hello 清單座標的資料行加入至逗號分隔 LatLong 資料行串連 hello 座標欄位使用 hello 公式中的 hello 兩個項目```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```。</span><span class="sxs-lookup"><span data-stu-id="e18e7-370">Add a new column tooconvert hello list coordinate column into a comma separate LatLong column concatenating hello two elements in hello coordinate list field using hello formula ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span></span>
7. <span data-ttu-id="e18e7-371">轉換 hello```Elevation```資料行 tooDecimal 和選取 hello**關閉**和**套用**。</span><span class="sxs-lookup"><span data-stu-id="e18e7-371">Finally convert hello ```Elevation``` column tooDecimal and select hello **Close** and **Apply**.</span></span>

<span data-ttu-id="e18e7-372">而不是上述步驟，您可以貼上下列指令碼中使用的 hello 步驟的程式碼的 hello hello 可讓您的查詢語言的 toowrite hello 資料轉換的 Power BI 中的 進階編輯器。</span><span class="sxs-lookup"><span data-stu-id="e18e7-372">Instead of preceding steps, you can paste hello following code that scripts out hello steps used in hello Advanced Editor in Power BI that allows you toowrite hello data transformations in a query language.</span></span>

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted tooTable" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted tooTable", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



<span data-ttu-id="e18e7-373">您現在會有您 Power BI 資料模型中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="e18e7-373">You now have hello data in your Power BI data model.</span></span> <span data-ttu-id="e18e7-374">您的 Power BI Desktop 應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="e18e7-374">Your Power BI desktop should appear as follows:</span></span>

![Power BI 桌面](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

<span data-ttu-id="e18e7-376">您可以開始建立報表和視覺效果使用 hello 資料模型。</span><span class="sxs-lookup"><span data-stu-id="e18e7-376">You can start building reports and visualizations using hello data model.</span></span> <span data-ttu-id="e18e7-377">您可以遵循這個 hello 步驟[Power BI 文件](../cosmos-db/powerbi-visualize.md#build-the-reports)toobuild 報表。</span><span class="sxs-lookup"><span data-stu-id="e18e7-377">You can follow hello steps in this [Power BI article](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild a report.</span></span> <span data-ttu-id="e18e7-378">hello 最終結果是，看起來像 hello 下列報表。</span><span class="sxs-lookup"><span data-stu-id="e18e7-378">hello end result is a report that looks like hello following.</span></span>

![Power BI Desktop 報告檢視 - Power BI 連接器](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-toomeet-your-project-needs"></a><span data-ttu-id="e18e7-380">9.動態調整您的專案需要您 DSVM toomeet</span><span class="sxs-lookup"><span data-stu-id="e18e7-380">9. Dynamically scale your DSVM toomeet your project needs</span></span>
<span data-ttu-id="e18e7-381">您可以調整您的專案需要 hello DSVM toomeet 上下。</span><span class="sxs-lookup"><span data-stu-id="e18e7-381">You can scale up and down hello DSVM toomeet your project needs.</span></span> <span data-ttu-id="e18e7-382">如果您不需要 toouse hello VM hello 夜晚或週末中，您可以只關閉 hello VM 從 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="e18e7-382">If you don't need toouse hello VM in hello evening or weekends, you can just shut down hello VM from hello [Azure portal](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="e18e7-383">如果您使用只 hello 作業系統關機按鈕 hello VM 上，您就會產生計算費用。</span><span class="sxs-lookup"><span data-stu-id="e18e7-383">You incur compute charges if you use just hello Operating system shutdown button on hello VM.</span></span>  
> 
> 

<span data-ttu-id="e18e7-384">如果您需要 toohandle 某些大規模的分析，而且需要更多的 CPU 和 （或） 記憶體及/或磁碟容量，您可以找到 CPU 核心、 記憶體容量和磁碟型別 （包括固態硬碟） 符合您的計算和預算需求方面的 VM 大小的大型選項。</span><span class="sxs-lookup"><span data-stu-id="e18e7-384">If you need toohandle some large-scale analysis and need more CPU and/or memory and/or disk capacity you can find a large choice of VM sizes in terms of CPU cores, memory capacity and disk types (including Solid state drives) that meet your compute and budgetary needs.</span></span> <span data-ttu-id="e18e7-385">hello 的 Vm 以及其每小時的計算定價的完整清單位於 hello [Azure 虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/)頁面。</span><span class="sxs-lookup"><span data-stu-id="e18e7-385">hello full list of VMs along with their hourly compute pricing is available on hello [Azure Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/) page.</span></span>

<span data-ttu-id="e18e7-386">同樣地，如果您需要處理的 VM 容量減少 (例如： 您將主要工作負載 tooa Hadoop 或 Spark 叢集，以)，您可以從 hello hello 叢集調降規模[Azure 入口網站](https://portal.azure.com)或傳送您的 VM toohello 設定執行個體。</span><span class="sxs-lookup"><span data-stu-id="e18e7-386">Similarly, if your need for VM processing capacity reduces (for example: you moved a major workload tooa Hadoop or a Spark cluster), you can scale down hello cluster from hello [Azure portal](https://portal.azure.com) and going toohello settings of your VM instance.</span></span> <span data-ttu-id="e18e7-387">以下為螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="e18e7-387">Here is a screenshot.</span></span>

![VM 執行個體設定](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a><span data-ttu-id="e18e7-389">10.在虛擬機器上安裝其他工具</span><span class="sxs-lookup"><span data-stu-id="e18e7-389">10. Install additional tools on your virtual machine</span></span>
<span data-ttu-id="e18e7-390">我們有封裝數個工具，我們相信是許多 hello 常見的資料分析需求，而且應該儲存您時間避免 tooinstall 一個環境並設定您，以節省成本支付只資源，您可以 tooaddress使用。</span><span class="sxs-lookup"><span data-stu-id="e18e7-390">We have packaged several tools that we believe are able tooaddress many of hello common data analytics needs and that should save you time by avoiding having tooinstall and configure your environments one by one and save you money by paying only for resources that you use.</span></span>

<span data-ttu-id="e18e7-391">您可以利用其他 Azure 的資料和分析服務剖析此發行項 tooenhance 分析環境。</span><span class="sxs-lookup"><span data-stu-id="e18e7-391">You can leverage other Azure data and analytics services profiled in this article tooenhance your analytics environment.</span></span> <span data-ttu-id="e18e7-392">我們了解，在某些情況下您的需求可能需要額外的工具，包括一些專屬的協力廠商工具。</span><span class="sxs-lookup"><span data-stu-id="e18e7-392">We understand that in some cases your needs may require additional tools, including some proprietary third-party tools.</span></span> <span data-ttu-id="e18e7-393">您具有完整系統管理權限 hello 虛擬機器 tooinstall 新所需的工具。</span><span class="sxs-lookup"><span data-stu-id="e18e7-393">You have full administrative access on hello virtual machine tooinstall new tools you need.</span></span> <span data-ttu-id="e18e7-394">您也可以在 Python 和 R 中安裝其他未預先安裝的封裝。</span><span class="sxs-lookup"><span data-stu-id="e18e7-394">You can also install additional packages in Python and R that are not pre-installed.</span></span> <span data-ttu-id="e18e7-395">對於 Python，您可以使用 ```conda``` 或 ```pip```。</span><span class="sxs-lookup"><span data-stu-id="e18e7-395">For Python you can use either ```conda``` or ```pip```.</span></span> <span data-ttu-id="e18e7-396">中，您可以使用 hello```install.packages()```在 hello R 主控台或使用 hello IDE，並選擇 "**封裝** -> **安裝套件...**".</span><span class="sxs-lookup"><span data-stu-id="e18e7-396">For R you can use hello ```install.packages()``` in hello R console or use hello IDE and choose "**Packages** -> **Install Packages...**".</span></span>

## <a name="summary"></a><span data-ttu-id="e18e7-397">摘要</span><span class="sxs-lookup"><span data-stu-id="e18e7-397">Summary</span></span>
<span data-ttu-id="e18e7-398">這些是一些您可以在 hello Microsoft Data Science 虛擬機器上執行的 hello 事項。</span><span class="sxs-lookup"><span data-stu-id="e18e7-398">These are just some of hello things you can do on hello Microsoft Data Science Virtual Machine.</span></span> <span data-ttu-id="e18e7-399">有更多項目，您可以執行 toomake 它有效分析環境。</span><span class="sxs-lookup"><span data-stu-id="e18e7-399">There are many more things you can do toomake it an effective analytics environment.</span></span>

