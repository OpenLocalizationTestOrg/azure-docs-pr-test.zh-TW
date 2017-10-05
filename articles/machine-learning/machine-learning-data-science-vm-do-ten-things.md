---
title: "您可以在 Data Science Virtual Machine 上做的十件事 | Microsoft Docs"
description: "在 Data science Virtual Machine 上執行各種資料探索和模型分析工作。"
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
ms.openlocfilehash: 45af1cd3a05b483429d2307659f1882ef28921f6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="ten-things-you-can-do-on-the-data-science-virtual-machine"></a><span data-ttu-id="51628-103">您可以在 Data Science Virtual Machine 上做的十件事</span><span class="sxs-lookup"><span data-stu-id="51628-103">Ten things you can do on the Data science Virtual Machine</span></span>
<span data-ttu-id="51628-104">Microsoft Data Science Virtual Machine (DSVM) 是強大的資料科學開發環境，可讓您執行各種資料探索和模型分析工作。</span><span class="sxs-lookup"><span data-stu-id="51628-104">The Microsoft Data Science Virtual Machine (DSVM) is a powerful data science development environment that enables you to perform various data exploration and modeling tasks.</span></span> <span data-ttu-id="51628-105">此環境已內建數個熱門的資料分析工具，以便您快速開始進行內部部署或混合式部署的分析。</span><span class="sxs-lookup"><span data-stu-id="51628-105">The environment comes already built and bundled with several popular data analytics tools that make it easy to get started quickly with your analysis for On-premises, Cloud or hybrid deployments.</span></span> <span data-ttu-id="51628-106">DSVM 與多項 Azure 服務密切合作，並且能夠讀取及處理已儲存在 Azure SQL 資料倉儲、Azure Data Lake、Azure 儲存體或 Azure Cosmos DB 中的資料。</span><span class="sxs-lookup"><span data-stu-id="51628-106">The DSVM works closely with many Azure services and is able to read and process data that is already stored on Azure, in Azure SQL Data Warehouse, Azure Data Lake, Azure Storage, or in Azure Cosmos DB.</span></span> <span data-ttu-id="51628-107">它也可以利用 Azure Machine Learning 和 Azure Data Factory 等其他分析工具。</span><span class="sxs-lookup"><span data-stu-id="51628-107">It can also leverage other analytics tools such as Azure Machine Learning and Azure Data Factory.</span></span>

<span data-ttu-id="51628-108">在本文中，我們會逐步引導您使用 DSVM 來執行各種資料科學工作，並與其他 Azure 服務互動。</span><span class="sxs-lookup"><span data-stu-id="51628-108">In this article we walk you through how to use your DSVM to perform various data science tasks and interact with other Azure services.</span></span> <span data-ttu-id="51628-109">以下是您可以在 DSVM 上做的一些事：</span><span class="sxs-lookup"><span data-stu-id="51628-109">Here are some of the things you can do on the DSVM:</span></span>

1. <span data-ttu-id="51628-110">使用 Microsoft R Server 或 Python 來探索資料並在 DSVM 本機開發模型</span><span class="sxs-lookup"><span data-stu-id="51628-110">Explore data and develop models locally on the DSVM using Microsoft R Server, Python</span></span>
2. <span data-ttu-id="51628-111">使用 Jupyter 筆記本，在採用 Python 2、Python 3、Microsoft R (針對延展性和效能設計的 R 企業就緒版) 的瀏覽器上試驗您的資料</span><span class="sxs-lookup"><span data-stu-id="51628-111">Use a Jupyter notebook to experiment with your data on a browser using Python 2, Python 3, Microsoft R an enterprise ready version of R designed for scalability and performance</span></span>
3. <span data-ttu-id="51628-112">在 Azure Machine Learning 上實作使用 R 和 Python 建置的模型，以便用戶端應用程式使用簡單的 Web 服務介面存取您的模型</span><span class="sxs-lookup"><span data-stu-id="51628-112">Operationalize models built using R and Python on Azure Machine Learning so client applications can access your models using a simple web services interface</span></span>
4. <span data-ttu-id="51628-113">使用 Azure 入口網站或 Powershell 管理您的 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="51628-113">Administer your Azure resources using  Azure portal or Powershell</span></span>
5. <span data-ttu-id="51628-114">建立 Azure 檔案儲存體作為 DSVM 上可掛接的磁碟機，以擴充您的儲存空間並與整個小組共用大型資料集/程式碼</span><span class="sxs-lookup"><span data-stu-id="51628-114">Extend your storage space and share large-scale datasets / code across your whole team by creating an Azure File storage as a mountable drive on your DSVM</span></span>
6. <span data-ttu-id="51628-115">使用 GitHub 來與您的小組共用程式碼，並使用預先安裝的 Git 用戶端 (Git Bash、Git GUI) 來存取您的存放庫。</span><span class="sxs-lookup"><span data-stu-id="51628-115">Share code with your team using GitHub and access your repository using the pre-installed Git clients - Git Bash, Git GUI.</span></span>
7. <span data-ttu-id="51628-116">存取各種 Azure 資料和分析服務，例如 Azure Blob 儲存體，Azure Data Lake、Azure HDInsight (Hadoop)、Azure Cosmos DB、Azure SQL 資料倉儲和資料庫</span><span class="sxs-lookup"><span data-stu-id="51628-116">Access various Azure data and analytics services like Azure blob storage, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse & databases</span></span>
8. <span data-ttu-id="51628-117">使用在 DSVM 上預先安裝的 Power BI Desktop 來建立報告和儀表板並雲端上加以部署</span><span class="sxs-lookup"><span data-stu-id="51628-117">Build reports and dashboard using the Power BI Desktop pre-installed on the DSVM and deploy them on the cloud</span></span>
9. <span data-ttu-id="51628-118">動態調整 DSVM 以符合您的專案需求</span><span class="sxs-lookup"><span data-stu-id="51628-118">Dynamically scale your DSVM to meet your project needs</span></span>
10. <span data-ttu-id="51628-119">在虛擬機器上安裝其他工具</span><span class="sxs-lookup"><span data-stu-id="51628-119">Install additional tools on your virtual machine</span></span>   

> [!NOTE]
> <span data-ttu-id="51628-120">額外的使用費適用於在本文中列出的許多其他資料儲存體和分析服務。</span><span class="sxs-lookup"><span data-stu-id="51628-120">Additional usage charges apply for many of the additional data storage and analytics services listed in this article.</span></span> <span data-ttu-id="51628-121">如需詳細資訊，請參閱 [Azure 價格](https://azure.microsoft.com/pricing/) 頁面。</span><span class="sxs-lookup"><span data-stu-id="51628-121">Please refer to the [Azure Pricing](https://azure.microsoft.com/pricing/) page for details.</span></span>
> 
> 

<span data-ttu-id="51628-122">**先決條件**</span><span class="sxs-lookup"><span data-stu-id="51628-122">**Prerequisites**</span></span>

* <span data-ttu-id="51628-123">您需要 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="51628-123">You need an Azure subscription.</span></span> <span data-ttu-id="51628-124">您可以在[這裡](https://azure.microsoft.com/free/)註冊免費試用。</span><span class="sxs-lookup"><span data-stu-id="51628-124">You can sign up for a free trial [here](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="51628-125">如需在 Azure 入口網站上佈建資料科學虛擬機器的指示，請參閱[建立虛擬機器](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm)。</span><span class="sxs-lookup"><span data-stu-id="51628-125">Instructions for provisioning a Data Science Virtual Machine on the Azure portal are available at [Creating a virtual machine](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span></span>

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a><span data-ttu-id="51628-126">1.使用 Microsoft R Server 或 Python 探索資料和開發模型</span><span class="sxs-lookup"><span data-stu-id="51628-126">1. Explore data and develop models using Microsoft R Server or Python</span></span>
<span data-ttu-id="51628-127">您可以使用 R 和 Python 等語言在 DSVM 上進行資料分析。</span><span class="sxs-lookup"><span data-stu-id="51628-127">You can use languages like R and Python to do your data analytics right on the DSVM.</span></span>

<span data-ttu-id="51628-128">對於 R，您可以使用稱為 "Revolution R Enterprise 8.0" 並可在 [開始] 功能表或桌面找到的 IDE。</span><span class="sxs-lookup"><span data-stu-id="51628-128">For R, you can use an IDE called "Revolution R Enterprise 8.0" that can be found on the start menu or the desktop.</span></span> <span data-ttu-id="51628-129">除了開放原始碼/CRAN-R 以外，Microsoft 提供了額外的程式庫以便進行可調整的分析，以及分析大於進行平行區塊分析允許之記憶體大小的資料。</span><span class="sxs-lookup"><span data-stu-id="51628-129">Microsoft has provided additional libraries on top of the Open source/CRAN-R to enable scalable analytics and the ability to analyze data larger than the memory size allowed by doing parallel chunked analysis.</span></span> <span data-ttu-id="51628-130">您也可以安裝您選擇的 R IDE，例如 [RStudio](https://www.rstudio.com/products/rstudio-desktop/)。</span><span class="sxs-lookup"><span data-stu-id="51628-130">You can also install an R IDE of your choice like [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span></span>

<span data-ttu-id="51628-131">對於 Python，您可以使用已預先安裝 Python Tools for Visual Studio (PTVS) 延伸模組的 Visual Studio Community Edition 等 IDE。</span><span class="sxs-lookup"><span data-stu-id="51628-131">For Python, you can use an IDE like Visual Studio Community Edition which has the Python Tools for Visual Studio (PTVS) extension pre-installed.</span></span> <span data-ttu-id="51628-132">根據預設，PTVS 上只設定基本的 Python 2.7 (不含任何分析程式庫，如 SciKit、Pandas)。</span><span class="sxs-lookup"><span data-stu-id="51628-132">By default, only a basic Python 2.7 is configured on PTVS (without any analytics library like SciKit, Pandas).</span></span> <span data-ttu-id="51628-133">若要啟用 Anaconda Python 2.7 和 3.5，您必須執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="51628-133">In order to enable Anaconda Python 2.7 and 3.5, you need to do the following:</span></span>

* <span data-ttu-id="51628-134">為每個版本建立自訂環境，方法是瀏覽至 [工具] -> [Python 工具] -> [Python 環境]，然後按一下 Visual Studio 2015 Community Edition 中的 [+ 自訂]。</span><span class="sxs-lookup"><span data-stu-id="51628-134">Create custom environments for each version by navigating to **Tools** -> **Python Tools** -> **Python Environments** and then clicking "**+ Custom**" in the Visual Studio 2015 Community Edition</span></span>
* <span data-ttu-id="51628-135">提供描述並將環境路徑前置詞設定為 *c:\anaconda* (適用於 Anaconda Python 2.7) 或 *c:\anaconda\envs\py35* (適用於 Anaconda Python 3.5)</span><span class="sxs-lookup"><span data-stu-id="51628-135">Give a description and set the environment prefix paths as *c:\anaconda* for Anaconda Python 2.7 OR *c:\anaconda\envs\py35* for Anaconda Python 3.5</span></span>
* <span data-ttu-id="51628-136">按一下 [自動偵測]，然後按一下 [套用] 來儲存環境。</span><span class="sxs-lookup"><span data-stu-id="51628-136">Click **Auto Detect** and then **Apply** to save the environment.</span></span>

<span data-ttu-id="51628-137">以下是自訂環境設定在 Visual Studio 中的外觀。</span><span class="sxs-lookup"><span data-stu-id="51628-137">Here is what the custom environment setup looks like in Visual Studio.</span></span>

![PTVS 設定](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

<span data-ttu-id="51628-139">如需有關如何建立 Python 環境的詳細資訊，請參閱 [PTVS 文件](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) 。</span><span class="sxs-lookup"><span data-stu-id="51628-139">See the [PTVS documentation](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) for additional details on how to create Python Environments.</span></span>

<span data-ttu-id="51628-140">現在您將建立新的 Python 專案。</span><span class="sxs-lookup"><span data-stu-id="51628-140">Now you are set up to create a new Python project.</span></span> <span data-ttu-id="51628-141">瀏覽至 [檔案] -> [新增] -> [專案] -> [Python]，然後選取您要建置的 Python 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="51628-141">Navigate to **File** -> **New** -> **Project** -> **Python** and select the type of Python application you are building.</span></span> <span data-ttu-id="51628-142">您可以將目前專案的 Python 環境設為所需的版本 (Anaconda 2.7 或 3.5)：以滑鼠右鍵按一下 [Python 環境]、選取 [新增/移除 Python 環境]，然後選取要與專案相關聯的環境。</span><span class="sxs-lookup"><span data-stu-id="51628-142">You can set the Python environment for the current project to the desired version (Anaconda 2.7 or 3.5): right-click the **Python environment**, select **Add/Remove Python Environments**, and then select the desired environment to associate with the project.</span></span> <span data-ttu-id="51628-143">您可以在 [文件](https://github.com/Microsoft/PTVS/wiki) 頁面找到在產品上使用 PTVS 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="51628-143">You can find more information about working with PTVS on the product [documentation](https://github.com/Microsoft/PTVS/wiki) page.</span></span>

## <a name="2-using-a-jupyter-notebook-to-explore-and-model-your-data-with-python-or-r"></a><span data-ttu-id="51628-144">2.使用 Jupyter Notebook 來探索您的資料，並以 Python 或 R 進行模型分析</span><span class="sxs-lookup"><span data-stu-id="51628-144">2. Using a Jupyter Notebook to explore and model your data with Python or R</span></span>
<span data-ttu-id="51628-145">Jupyter Notebook 是一個強大的環境，可提供以瀏覽器為基礎的 "IDE" 進行資料探索和模型分析。</span><span class="sxs-lookup"><span data-stu-id="51628-145">The Jupyter Notebook is a powerful environment that provides a browser-based "IDE" for data exploration and modeling.</span></span> <span data-ttu-id="51628-146">您可以在 Jupyter Notebook 使用 Python 2、Python 3 或 R (開放原始碼和 Microsoft R Server)。</span><span class="sxs-lookup"><span data-stu-id="51628-146">You can use Python 2, Python 3 or R (both Open Source and the Microsoft R Server) in a Jupyter Notebook.</span></span>

<span data-ttu-id="51628-147">若要啟動 Jupyter Notebook，請按一下標題為 [Jupyter Notebook] 的 [開始] 功能表圖示 / 桌面圖示。</span><span class="sxs-lookup"><span data-stu-id="51628-147">To launch the Jupyter Notebook click on the start menu icon / desktop icon titled **Jupyter Notebook**.</span></span> <span data-ttu-id="51628-148">在 DSVM 上，您也可以瀏覽至 "https://localhost:9999/" 以存取 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="51628-148">On the DSVM you can also browse to "https://localhost:9999/" to access the Jupiter Notebook.</span></span> <span data-ttu-id="51628-149">如果其提示您輸入密碼，請使用[佈建 Microsoft 資料科學虛擬機器](machine-learning-data-science-provision-vm.md)主題之***如何在 Jupyter 筆記本伺服器上建立強式密碼***小節中所提供的指示，以建立強式密碼來存取 Jupyter 筆記本。</span><span class="sxs-lookup"><span data-stu-id="51628-149">If it prompts you for a password, use instructions provided in the ***How to create a strong password on the Jupyter notebook server*** section of the [Provision the Microsoft Data Science Virtual Machine](machine-learning-data-science-provision-vm.md) topic to create a strong password to access the Jupyter notebook.</span></span> 

<span data-ttu-id="51628-150">您開啟筆記本後，應該會看到一個目錄，其中包含一些已預先封裝到 DSVM 中的範例筆記本。</span><span class="sxs-lookup"><span data-stu-id="51628-150">Once you have opened the notebook, you should see a directory that contains a few example notebooks that are pre-packaged into the DSVM.</span></span> <span data-ttu-id="51628-151">現在您可以：</span><span class="sxs-lookup"><span data-stu-id="51628-151">Now you can:</span></span>

* <span data-ttu-id="51628-152">按一下筆記本以查看程式碼。</span><span class="sxs-lookup"><span data-stu-id="51628-152">click on the notebook to see the code.</span></span>
* <span data-ttu-id="51628-153">按 **SHIFT-ENTER**執行每個儲存格。</span><span class="sxs-lookup"><span data-stu-id="51628-153">execute each cell by pressing **SHIFT-ENTER**.</span></span>
* <span data-ttu-id="51628-154">按一下 [儲存格] -> [執行] 執行整個筆記本。</span><span class="sxs-lookup"><span data-stu-id="51628-154">run the entire notebook by clicking on **Cell** -> **Run**</span></span>
* <span data-ttu-id="51628-155">按一下 Jupyter 圖示 (左上角)，並按一下右邊的 [新增] 按鈕，然後選擇筆記本語言 (也稱為核心)，以建立新的筆記本。</span><span class="sxs-lookup"><span data-stu-id="51628-155">create a new notebook by clicking on the Jupyter Icon (left top corner) and then clicking **New** button on the right and then choosing the notebook language (also known as kernels).</span></span>   

> [!NOTE]
> <span data-ttu-id="51628-156">我們目前支援 Python 2.7、Python 3.5 和 R。R 核心支援以開放原始碼 R 以及企業可調整式 Microsoft R Server 進行程式設計。</span><span class="sxs-lookup"><span data-stu-id="51628-156">Currently we support Python 2.7, Python 3.5 and R. The R kernel supports programming in both Open source R as well as the enterprise scalable Microsoft R Server.</span></span>   
> 
> 

<span data-ttu-id="51628-157">一旦位於筆記本，您即可探索資料、建立模型，以及使用您所選的程式庫測試模型。</span><span class="sxs-lookup"><span data-stu-id="51628-157">Once you are in the notebook you can explore your data, build the model, test the model using your choice of libraries.</span></span>

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a><span data-ttu-id="51628-158">3.使用 R 或 Python 建置模型並且使用 Azure Machine Learning 實作</span><span class="sxs-lookup"><span data-stu-id="51628-158">3. Build models using R or Python and Operationalize them using Azure Machine Learning</span></span>
<span data-ttu-id="51628-159">建置並驗證您的模型之後，下一個步驟通常是將它部署到生產環境中。</span><span class="sxs-lookup"><span data-stu-id="51628-159">Once you have built and validated your model the next step is usually to deploy it into production.</span></span> <span data-ttu-id="51628-160">這可讓您的用戶端應用程式以即時或分批模式方式叫用模型預測。</span><span class="sxs-lookup"><span data-stu-id="51628-160">This allows your client applications to invoke the model predictions on a real time or on a batch mode basis.</span></span> <span data-ttu-id="51628-161">Azure Machine Learning 提供一個機制來實作以 R 或 Python 建置的模型。</span><span class="sxs-lookup"><span data-stu-id="51628-161">Azure Machine Learning provides a mechanism to operationalize a model built in either R or Python.</span></span>

<span data-ttu-id="51628-162">當您在 Azure Machine Learning 中實作模型時，系統會公開一項可讓用戶端進行 REST 呼叫的 Web 服務，以便傳入輸入參數以及接收來自模型的預測做為輸出。</span><span class="sxs-lookup"><span data-stu-id="51628-162">When you operationalize your model in Azure Machine Learning, a web service is exposed that allows clients to make REST calls that pass in input parameters and receive predictions from the model as outputs.</span></span>   

> [!NOTE]
> <span data-ttu-id="51628-163">如果您尚未註冊 Azure Machine Learning，請瀏覽 [Azure Machine Learning Studio](https://studio.azureml.net/) 首頁並按一下 [開始使用]，即可取得免費的工作區或標準工作區。</span><span class="sxs-lookup"><span data-stu-id="51628-163">If you have not yet signed up for Azure Machine Learning, you can obtain a free workspace or a standard workspace by visiting the [Azure Machine Learning Studio](https://studio.azureml.net/) home page and clicking on "Get Started".</span></span>   
> 
> 

### <a name="build-and-operationalize-python-models"></a><span data-ttu-id="51628-164">建置和實作 Python 模型</span><span class="sxs-lookup"><span data-stu-id="51628-164">Build and Operationalize Python models</span></span>
<span data-ttu-id="51628-165">以下是在 Python Jupyter Notebook 來開發的程式碼片段，它會使用 Scikit-learn 程式庫建置簡單的模型。</span><span class="sxs-lookup"><span data-stu-id="51628-165">Here is a snippet of code developed in a Python Jupyter Notebook that builds a simple model using the SciKit-learn library.</span></span>

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

<span data-ttu-id="51628-166">用來部署 python 模型到 Azure Machine Learning 的方法，會將模型預測包裝成函式，然後以預先安裝之 Azure Machine Learning python 程式庫所提供的屬性裝飾它，代表您的 Azure Machine Learning 工作區識別碼、API 金鑰，以及輸入和傳回參數。</span><span class="sxs-lookup"><span data-stu-id="51628-166">The method used to deploy your python models to Azure Machine Learning wraps the prediction of the model into a function and decorates it with attributes provided by the pre-installed Azure Machine Learning python library that denote your Azure Machine Learning workspace ID, API Key, and the input and return parameters.</span></span>  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

<span data-ttu-id="51628-167">用戶端現在可以呼叫 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="51628-167">A client can now make calls to the web service.</span></span> <span data-ttu-id="51628-168">有一個可建構 REST API 要求的便利包裝函式。</span><span class="sxs-lookup"><span data-stu-id="51628-168">There are convenience wrappers that construct the REST API requests.</span></span> <span data-ttu-id="51628-169">以下是用來取用 Web 服務的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="51628-169">Here is a sample code to consume the web service.</span></span>

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> <span data-ttu-id="51628-170">Azure Machine Learning 程式庫目前只在 Python 2.7 上支援。</span><span class="sxs-lookup"><span data-stu-id="51628-170">The Azure Machine Learning library is only supported on Python 2.7 currently.</span></span>   
> 
> 

### <a name="build-and-operationalize-r-models"></a><span data-ttu-id="51628-171">建置和實作 R 模型</span><span class="sxs-lookup"><span data-stu-id="51628-171">Build and Operationalize R models</span></span>
<span data-ttu-id="51628-172">您可以用類似於處理 Python 的方式，將在 Data Science Virtual Machine 或其他位置建置的 R 模型部署到 Azure Machine Learning。</span><span class="sxs-lookup"><span data-stu-id="51628-172">You can deploy R models built on the Data Science Virtual Machine or elsewhere onto Azure Machine Learning in a manner that is similar to how it is done for Python.</span></span> <span data-ttu-id="51628-173">步驟如下：</span><span class="sxs-lookup"><span data-stu-id="51628-173">Her are the steps:</span></span>

* <span data-ttu-id="51628-174">建立 settings.json 檔案，以提供您的工作區識別碼和驗證權杖，如下列程式碼範例所示。</span><span class="sxs-lookup"><span data-stu-id="51628-174">create a settings.json file to provide your workspace ID and auth token as shown in the following code sample.</span></span>
* <span data-ttu-id="51628-175">針對模型的預測函式，撰寫一個包裝函式。</span><span class="sxs-lookup"><span data-stu-id="51628-175">write a wrapper for the model's predict function.</span></span>
* <span data-ttu-id="51628-176">呼叫 Azure Machine Learning 程式庫中的 ```publishWebService``` 以傳入函式包裝函式。</span><span class="sxs-lookup"><span data-stu-id="51628-176">call ```publishWebService``` in the Azure Machine Learning library to pass in the function wrapper.</span></span>  

<span data-ttu-id="51628-177">以下是可用來安裝、建置、發佈和取用模型作為 Azure Machine Learning Web 服務的程序和程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="51628-177">Here is the procedure and code snippets that can be used to set up, build, publish, and consume a model as a web service in Azure Machine Learning.</span></span>

#### <a name="setup"></a><span data-ttu-id="51628-178">設定</span><span class="sxs-lookup"><span data-stu-id="51628-178">Setup</span></span>
1. <span data-ttu-id="51628-179">在 Revolution R Enterprise 8.0 IDE 或您的 R IDE 中，輸入 ```install.packages("AzureML")``` 以安裝 Machine Learning R 套件。</span><span class="sxs-lookup"><span data-stu-id="51628-179">Install the Machine Learning R package by typing ```install.packages("AzureML")``` in Revolution R Enterprise 8.0 IDE or your R IDE.</span></span>
2. <span data-ttu-id="51628-180">從[這裡](https://cran.r-project.org/bin/windows/Rtools/)下載 RTools。</span><span class="sxs-lookup"><span data-stu-id="51628-180">Download RTools from [here](https://cran.r-project.org/bin/windows/Rtools/).</span></span> <span data-ttu-id="51628-181">您在路徑中需要有 zip 公用程式 (和具名的 zip.exe)，才能將 R 套件納入 Azure Machine Learning 中。</span><span class="sxs-lookup"><span data-stu-id="51628-181">You need the zip utility in the path (and named zip.exe) to operationalize your R package into Machine Learning.</span></span>
3. <span data-ttu-id="51628-182">在主目錄下名為 ```.azureml``` 的目錄下建立 settings.json 檔案，並輸入來自 Azure Machine Learning 工作區的參數：</span><span class="sxs-lookup"><span data-stu-id="51628-182">Create a settings.json file under a directory called ```.azureml``` under your home directory and enter the parameters from your Azure Machine Learning workspace:</span></span>

<span data-ttu-id="51628-183">settings.json 檔案結構：</span><span class="sxs-lookup"><span data-stu-id="51628-183">settings.json File structure:</span></span>

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a><span data-ttu-id="51628-184">以 R 建置模型並在 Azure Machine Learning 中發佈</span><span class="sxs-lookup"><span data-stu-id="51628-184">Build a model in R and publish it in Azure Machine Learning</span></span>
    library(AzureML)
    ws <- workspace(config="~/.azureml/settings.json")

    if(!require("lme4")) install.packages("lme4")
    library(lme4)
    set.seed(1)
    train <- sleepstudy[sample(nrow(sleepstudy), 120),]
    m <- lm(Reaction ~ Days + Subject, data = train)

    # Define a prediction function to publish based on the model:
    sleepyPredict <- function(newdata){
          predict(m, newdata=newdata)
    }

    ep <- publishWebService(ws, fun = sleepyPredict, name="sleepy lm", inputSchema = sleepstudy, data.frame=TRUE)

#### <a name="consume-the-model-deployed-in-azure-machine-learning"></a><span data-ttu-id="51628-185">取用 Azure Machine Learning 中部署的模型</span><span class="sxs-lookup"><span data-stu-id="51628-185">Consume the model deployed in Azure Machine Learning</span></span>
<span data-ttu-id="51628-186">為了從用戶端應用程式取用模型，我們使用 Azure Machine Learning 程式庫來透過 `services` API 呼叫依名稱查閱已發佈的 Web 服務，進而決定端點。</span><span class="sxs-lookup"><span data-stu-id="51628-186">To consume the model from a client application, we use the Azure Machine Learning library to look up the published web service by name using the `services` API call to determine the endpoint.</span></span> <span data-ttu-id="51628-187">然後您只要呼叫 `consume` 函式並傳入要預測的資料框架。</span><span class="sxs-lookup"><span data-stu-id="51628-187">Then you just call the `consume` function and pass in the data frame to be predicted.</span></span>
<span data-ttu-id="51628-188">下列程式碼用來取用已發佈為 Azure Machine Learning Web 服務的模型。</span><span class="sxs-lookup"><span data-stu-id="51628-188">The following code is used to consume the model published as an Azure Machine Learning web service.</span></span>

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use the last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

<span data-ttu-id="51628-189">Azure Machine Learning R 程式庫的詳細資訊可以在[這裡](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf)找到。</span><span class="sxs-lookup"><span data-stu-id="51628-189">More information about the Azure Machine Learning R library can be found [here](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span></span>

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a><span data-ttu-id="51628-190">4.使用 Azure 入口網站或 Powershell 管理您的 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="51628-190">4. Administer your Azure resources using Azure portal or Powershell</span></span>
<span data-ttu-id="51628-191">DSVM 不僅可讓您在虛擬機器本機建置分析解決方案，也可讓您存取 Microsoft Azure 雲端上的服務。</span><span class="sxs-lookup"><span data-stu-id="51628-191">The DSVM not only allows you to build your analytics solution locally on the virtual machine, but also allows you to access services on Microsoft's Azure cloud.</span></span> <span data-ttu-id="51628-192">Azure 提供數個可從 DSVM 管理和存取的計算、儲存、資料分析服務和其他服務。</span><span class="sxs-lookup"><span data-stu-id="51628-192">Azure provides several compute, storage, data analytics services and other services that you can administer and access from your DSVM.</span></span>

<span data-ttu-id="51628-193">若要管理 Azure 訂用帳戶和雲端資源，您可以使用瀏覽器並指向 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="51628-193">To administer your Azure subscription and cloud resources you can use your browser and point to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="51628-194">您也可以使用 Azure Powershell 並透過指令碼管理 Azure 訂用帳戶和資源。</span><span class="sxs-lookup"><span data-stu-id="51628-194">You can also use Azure Powershell to administer your Azure subscription and resources via a script.</span></span>
<span data-ttu-id="51628-195">您可以從桌面上的捷徑或從標題為 "Microsoft Azure Powershell" 的 [開始] 功能表執行 Azure Powershell。</span><span class="sxs-lookup"><span data-stu-id="51628-195">You can run Azure Powershell from a shortcut on the desktop or from the start menu titled "Microsoft Azure Powershell".</span></span> <span data-ttu-id="51628-196">如需如何使用 Windows Powershell 指令碼管理 Azure 訂用帳戶和資源的詳細資訊，請參閱 [Microsoft Azure Powershell 文件](../powershell-azure-resource-manager.md) 。</span><span class="sxs-lookup"><span data-stu-id="51628-196">Refer to [Microsoft Azure Powershell documentation](../powershell-azure-resource-manager.md) for more information on how you can administer your Azure subscription and resources using Windows Powershell scripts.</span></span>

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a><span data-ttu-id="51628-197">5.使用共用的檔案系統來擴充您的儲存空間</span><span class="sxs-lookup"><span data-stu-id="51628-197">5. Extend your storage space with a shared file system</span></span>
<span data-ttu-id="51628-198">資料科學家可以在小組內共用大型資料集、程式碼或其他資源。</span><span class="sxs-lookup"><span data-stu-id="51628-198">Data scientists can share large datasets, code or other resources within the team.</span></span> <span data-ttu-id="51628-199">DSVM 本身有大約 70GB 的可用空間。</span><span class="sxs-lookup"><span data-stu-id="51628-199">The DSVM itself has about 70GB of space available.</span></span> <span data-ttu-id="51628-200">若要擴充您的儲存體，您可以使用 Azure 檔案服務，然後將它掛接於 DSVM 或透過 REST API 存取。</span><span class="sxs-lookup"><span data-stu-id="51628-200">To extend your storage, you can use the Azure File Service and either mount it on the DSVM or access it via a REST API.</span></span>   

> [!NOTE]
> <span data-ttu-id="51628-201">Azure 檔案服務共用的空間上限為 5TB，而個別的檔案大小限制為 1TB。</span><span class="sxs-lookup"><span data-stu-id="51628-201">The maximum space of the Azure File Service share is 5TB and individual file size limit is 1TB.</span></span>   
> 
> 

<span data-ttu-id="51628-202">您可以使用 Azure PowerShell 建立 Azure 檔案服務共用。</span><span class="sxs-lookup"><span data-stu-id="51628-202">You can use Azure Powershell to create an Azure File Service share.</span></span> <span data-ttu-id="51628-203">以下是可在 Azure PowerShell 下執行以建立 Azure 檔案服務共用的指令碼。</span><span class="sxs-lookup"><span data-stu-id="51628-203">Here is the script to run under Azure PowerShell to create an Azure File service share.</span></span>

    # Authenticate to Azure.
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
    # Create a directory under the FIle share. You can give it any name
    New-AzureStorageDirectory -Share $s -Path <directory name>
    # List the share to confirm that everything worked
    Get-AzureStorageFile -Share $s


<span data-ttu-id="51628-204">您現在已建立 Azure 檔案共用，即可將它掛接在 Azure 的任何虛擬機器中。</span><span class="sxs-lookup"><span data-stu-id="51628-204">Now that you have created an Azure file share, you can mount it in any virtual machine in Azure.</span></span> <span data-ttu-id="51628-205">強烈建議 VM 位於與儲存體帳戶相同的 Azure 資料中心，以避免延遲和資料傳輸費用。</span><span class="sxs-lookup"><span data-stu-id="51628-205">It is highly recommended that the VM is in same Azure data center as the storage account to avoid latency and data transfer charges.</span></span> <span data-ttu-id="51628-206">以下是您可以在 Azure Powershell 上執行以在 DSVM 上掛接磁碟機的命令。</span><span class="sxs-lookup"><span data-stu-id="51628-206">Here are the commands to mount the drive on the DSVM that you can run on Azure Powershell.</span></span>

    # Get storage key of the storage account that has the Azure file share from Azure portal. Store it securely on the VM to avoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount the Azure file share as Z: drive on the VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


<span data-ttu-id="51628-207">您現在可以將此磁碟機當作 VM 上的任何一般磁碟機存取。</span><span class="sxs-lookup"><span data-stu-id="51628-207">Now you can access this drive as you would any normal drive on the VM.</span></span>

## <a name="6-share-code-with-your-team-using-github"></a><span data-ttu-id="51628-208">6.使用 GitHub 與您的小組共用程式碼</span><span class="sxs-lookup"><span data-stu-id="51628-208">6. Share code with your team using GitHub</span></span>
<span data-ttu-id="51628-209">GitHub 是一個程式碼存放庫，您可以在其中找到開發人員分享使用各種技術，針對不同工具建立的大量範例程式碼和原始碼。</span><span class="sxs-lookup"><span data-stu-id="51628-209">GitHub is a code repository where you can find a lot of sample code and sources for different tools using various technologies shared by the developer community.</span></span> <span data-ttu-id="51628-210">它會使用 Git 技術來追蹤和儲存各版本的程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="51628-210">It uses Git as the technology to track and store versions of the code files.</span></span> <span data-ttu-id="51628-211">GitHub 也是一個平台，您可以在其中建立自己的存放庫，以儲存您小組共用的程式碼和文件、實作版本控制，也可以控制有權檢視和貢獻程式碼的人員。</span><span class="sxs-lookup"><span data-stu-id="51628-211">GitHub is also a platform where you can create your own repository to store your team's shared code and documentation, implement version control and also control who have access to view and contribute code.</span></span> <span data-ttu-id="51628-212">如需使用 Git 的詳細資訊，請瀏覽 [GitHub 說明網頁 (英文)](https://help.github.com/)。</span><span class="sxs-lookup"><span data-stu-id="51628-212">Please visit the [GitHub help pages](https://help.github.com/) for more information on using Git.</span></span> <span data-ttu-id="51628-213">您可以使用 GitHub 來與您的小組共同作業、使用社群所開發的程式碼，以及將程式碼貢獻回社群。</span><span class="sxs-lookup"><span data-stu-id="51628-213">You can use GitHub as one of the ways to collaborate with your team, use code developed by the community and contribute code back to the community.</span></span>

<span data-ttu-id="51628-214">DSVM 已在命令列和 GUI 上載入用戶端工具，以便存取 GitHub 存放庫。</span><span class="sxs-lookup"><span data-stu-id="51628-214">The DSVM already comes loaded with client tools on both command-line as well GUI to access GitHub repository.</span></span> <span data-ttu-id="51628-215">可搭配 Git 與 GitHub 使用的命令列工具稱為 Git Bash。</span><span class="sxs-lookup"><span data-stu-id="51628-215">The command-line tool to work with Git and GitHub is called Git Bash.</span></span> <span data-ttu-id="51628-216">DSVM 上安裝的 Visual Studio 具有 Git 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="51628-216">Visual Studio installed on the DSVM has the Git extensions.</span></span> <span data-ttu-id="51628-217">您可以在 [開始] 功能表和桌面上找到這些工具的啟動圖示。</span><span class="sxs-lookup"><span data-stu-id="51628-217">You can find start-up icons for these tools on the start menu and the desktop.</span></span>

<span data-ttu-id="51628-218">若要從 GitHub 存放庫下載程式碼，您可以使用 ```git clone``` 命令。</span><span class="sxs-lookup"><span data-stu-id="51628-218">To download code from a GitHub repository you use the ```git clone``` command.</span></span> <span data-ttu-id="51628-219">例如，若要將 Microsoft 所發佈的資料科學儲存機制下載到目前的目錄中，您可以在 ```git-bash```中執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="51628-219">For example to download data science repository published by Microsoft into the current directory you can run the following command once you are in ```git-bash```.</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="51628-220">您可以在 Visual Studio 中執行相同的複製作業。</span><span class="sxs-lookup"><span data-stu-id="51628-220">In Visual Studio, you can do the same clone operation.</span></span> <span data-ttu-id="51628-221">下列螢幕擷取畫面示範如何在 Visual Studio 中存取 Git 和 GitHub 工具。</span><span class="sxs-lookup"><span data-stu-id="51628-221">The  following screen-shot shows how to access Git and GitHub tools in Visual Studio.</span></span>

![Visual Studio 中的 Git](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

<span data-ttu-id="51628-223">從 github.com 上提供的幾個資源，即可找到透過 Git 使用 GitHub 存放庫的詳細資訊。[功能提要](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) 是有用的參考資料。</span><span class="sxs-lookup"><span data-stu-id="51628-223">You can find more information on using Git to work with your GitHub repository from several resources available on github.com. The [cheat sheet](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) is a useful reference.</span></span>

## <a name="7-access-various-azure-data-and-analytics-services"></a><span data-ttu-id="51628-224">7.存取各種 Azure 資料和分析服務</span><span class="sxs-lookup"><span data-stu-id="51628-224">7. Access various Azure data and analytics services</span></span>
### <a name="azure-blob"></a><span data-ttu-id="51628-225">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="51628-225">Azure Blob</span></span>
<span data-ttu-id="51628-226">Azure blob 是可靠、划算的雲端儲存體，可存放大型和小型的資料。</span><span class="sxs-lookup"><span data-stu-id="51628-226">Azure blob is a reliable, economical cloud storage for data big and small.</span></span> <span data-ttu-id="51628-227">讓我們看一下如何將資料移至 Azure Blob 和存取 Azure Blob 中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="51628-227">Let us look at how you can move data to Azure Blob and access data stored in an Azure Blob.</span></span>

<span data-ttu-id="51628-228">**先決條件**</span><span class="sxs-lookup"><span data-stu-id="51628-228">**Prerequisite**</span></span>

* <span data-ttu-id="51628-229">**從 [Azure 入口網站](https://portal.azure.com)建立 Azure Blob 儲存體帳戶。**</span><span class="sxs-lookup"><span data-stu-id="51628-229">**Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).**</span></span>

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="51628-231">確認預先安裝的命令列 AzCopy 工具位於 ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```。</span><span class="sxs-lookup"><span data-stu-id="51628-231">Confirm that the pre-installed command-line AzCopy tool is found at ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span></span> <span data-ttu-id="51628-232">您可以將包含 azcopy.exe 的目錄加入至您的 PATH 環境變數，如此便不用在執行這項工具時輸入完整的命令路徑。</span><span class="sxs-lookup"><span data-stu-id="51628-232">You can add the directory containing the azcopy.exe to your PATH environment variable to avoid typing the full command path when running this tool.</span></span> <span data-ttu-id="51628-233">如需 AzCopy 工具的詳細資訊，請參閱 [AzCopy 文件](../storage/common/storage-use-azcopy.md)</span><span class="sxs-lookup"><span data-stu-id="51628-233">For more info on AzCopy tool please refer to [AzCopy documentation](../storage/common/storage-use-azcopy.md)</span></span>
* <span data-ttu-id="51628-234">啟動 Azure 儲存體總管工具。</span><span class="sxs-lookup"><span data-stu-id="51628-234">Start the Azure Storage Explorer tool.</span></span> <span data-ttu-id="51628-235">您可以從 [Microsoft Azure 儲存體總管](http://storageexplorer.com/)下載此工具。</span><span class="sxs-lookup"><span data-stu-id="51628-235">It can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

<span data-ttu-id="51628-237">**將資料從 VM 移至 Azure Blob：AzCopy**</span><span class="sxs-lookup"><span data-stu-id="51628-237">**Move data from VM to Azure Blob: AzCopy**</span></span>

<span data-ttu-id="51628-238">若要在本機檔案與 Blob 儲存體之間移動資料，您可以在命令列或 PowerShell 中使用 AzCopy：</span><span class="sxs-lookup"><span data-stu-id="51628-238">To move data between your local files and blob storage, you can use AzCopy in command-line or PowerShell:</span></span>

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

<span data-ttu-id="51628-239">以您的檔案儲存路徑取代 **C:\myfolder**，以您的 Blob 儲存體帳戶名稱取代 **mystorageaccount**、以容器名稱取代 **mycontainer**，並以您的 Blob 儲存體存取金鑰取代 **storage account key**。</span><span class="sxs-lookup"><span data-stu-id="51628-239">Replace **C:\myfolder** to the path where your file is stored, **mystorageaccount** to your blob storage account name, **mycontainer** to the container name, **storage account key** to your blob storage access key.</span></span> <span data-ttu-id="51628-240">您可以在 [Azure 入口網站](https://portal.azure.com)中尋找您的儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="51628-240">You can find your storage account credentials in [Azure portal](https://portal.azure.com).</span></span>

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

<span data-ttu-id="51628-242">在 PowerShell 或從命令提示字元執行 AzCopy 命令。</span><span class="sxs-lookup"><span data-stu-id="51628-242">Run AzCopy command in PowerShell or from a command prompt.</span></span> <span data-ttu-id="51628-243">以下是使用 AzCopy 命令的一些範例：</span><span class="sxs-lookup"><span data-stu-id="51628-243">Here is some example usage of AzCopy command:</span></span>

    # Copy *.sql from local machine to a Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container to Local machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



<span data-ttu-id="51628-244">執行 AzCopy 命令來複製到 Azure Blob 之後，您會看到檔案隨即出現在 Azure 儲存體總管中。</span><span class="sxs-lookup"><span data-stu-id="51628-244">Once you run your AzCopy command to copy to an Azure blob you see your file shows up in Azure Storage Explorer shortly.</span></span>

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

<span data-ttu-id="51628-246">**將資料從 VM 移至 Azure Blob：Azure 儲存體總管**</span><span class="sxs-lookup"><span data-stu-id="51628-246">**Move data from VM to Azure Blob: Azure Storage Explorer**</span></span>

<span data-ttu-id="51628-247">您也可以使用 Azure 儲存體總管，從 VM 中的本機檔案上載資料：</span><span class="sxs-lookup"><span data-stu-id="51628-247">You can also upload data from the local file in your VM using Azure Storage Explorer:</span></span>

* <span data-ttu-id="51628-248">若要將資料上傳至容器，請選取目標容器，然後按一下 [上傳] 按鈕。![儲存體總管中的 [上傳]](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span><span class="sxs-lookup"><span data-stu-id="51628-248">To upload data to a container, select the target container and click the **Upload** button.![Upload in Storage Explorer](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span></span>
* <span data-ttu-id="51628-249">按一下 [檔案] 方塊右邊的 [...]，從檔案系統中選取一或多個要上傳的檔案，然後按一下 [上傳] 以開始上傳檔案。![上傳檔案到 Blob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span><span class="sxs-lookup"><span data-stu-id="51628-249">Click on the **...** to the right of the **Files** box, select one or multiple files to upload from the file system and click **Upload** to begin uploading the files.![Upload files to blob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span></span>

<span data-ttu-id="51628-250">**從 Azure Blob 讀取資料：Machine Learning 讀取器模組**</span><span class="sxs-lookup"><span data-stu-id="51628-250">**Read data from Azure Blob: Machine Learning reader module**</span></span>

<span data-ttu-id="51628-251">您可以在 Azure Machine Learning Studio 中，使用 **匯入資料模組** 從 Blob 讀取資料。</span><span class="sxs-lookup"><span data-stu-id="51628-251">In Azure Machine Learning Studio you can use an **Import Data module** to read data from your blob.</span></span>

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

<span data-ttu-id="51628-253">**從 Azure Blob 讀取資料：Python ODBC**</span><span class="sxs-lookup"><span data-stu-id="51628-253">**Read data from Azure Blob: Python ODBC**</span></span>

<span data-ttu-id="51628-254">您可以使用 **BlobService** 程式庫，直接從 Jupyter 筆記本或 Python 程式的 Blob 中讀取資料。</span><span class="sxs-lookup"><span data-stu-id="51628-254">You can use **BlobService** library to read data directly from blob in a Jupyter Notebook or Python program.</span></span>

<span data-ttu-id="51628-255">首先，匯入所需的封裝：</span><span class="sxs-lookup"><span data-stu-id="51628-255">First, import required packages:</span></span>

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

<span data-ttu-id="51628-256">然後插入您的 Azure Blob 帳戶認證並從 Blob 讀取資料：</span><span class="sxs-lookup"><span data-stu-id="51628-256">Then plug in your Azure Blob account credentials and read data from Blob:</span></span>

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
    print(("It takes %s seconds to download "+BLOBNAME) % (t2 - t1))

    #unzipping downloaded files if needed
    #with zipfile.ZipFile(ZIPPEDLOCALFILE, "r") as z:
    #    z.extractall(LOCALDIRECTORY)

    df1 = pd.read_csv(LOCALFILE, header=0)
    df1.columns = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime','passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude']
    print 'the size of the data is: %d rows and  %d columns' % df1.shape

<span data-ttu-id="51628-257">資料以資料框架的形式讀入：</span><span class="sxs-lookup"><span data-stu-id="51628-257">The data is read in as a data frame:</span></span>

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a><span data-ttu-id="51628-259">Azure 資料湖</span><span class="sxs-lookup"><span data-stu-id="51628-259">Azure Data Lake</span></span>
<span data-ttu-id="51628-260">Azure Data Lake 儲存體是巨量資料分析工作負載的超大規模儲存機制，與 Hadoop 分散式檔案系統 (HDFS) 相容。</span><span class="sxs-lookup"><span data-stu-id="51628-260">Azure Data Lake Storage is a hyper-scale repository for big data analytics workloads and compatible with Hadoop Distributed File System (HDFS).</span></span> <span data-ttu-id="51628-261">它適用於 Hadoop 生態系統以及 Azure Data Lake Analytics。</span><span class="sxs-lookup"><span data-stu-id="51628-261">It works with both the Hadoop ecosystem and the Azure Data Lake Analytics.</span></span> <span data-ttu-id="51628-262">我們會示範如何將資料移至 Azure 資料湖存放區，並使用 Azure 資料湖分析執行分析。</span><span class="sxs-lookup"><span data-stu-id="51628-262">We show how you can move data into the Azure Data Lake Store and run analytics using Azure Data Lake Analytics.</span></span>

<span data-ttu-id="51628-263">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="51628-263">**Prerequisite**</span></span>

* <span data-ttu-id="51628-264">在 [Azure 入口網站](https://portal.azure.com)中建立 Azure Data Lake Analytics。</span><span class="sxs-lookup"><span data-stu-id="51628-264">Create your Azure Data Lake Analytics in [Azure portal](https://portal.azure.com).</span></span>

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* <span data-ttu-id="51628-266">在這個[連結](https://www.microsoft.com/download/details.aspx?id=49504)找到的 **Visual Studio** 中的 **Azure Data Lake Tools**，已安裝於虛擬機器上的 Visual Studio Community 版本。</span><span class="sxs-lookup"><span data-stu-id="51628-266">The  **Azure Data Lake Tools** in **Visual Studio** found at this  [link](https://www.microsoft.com/download/details.aspx?id=49504) is already installed on the Visual Studio Community Edition which is on the virtual machine.</span></span> <span data-ttu-id="51628-267">啟動 Visual Studio 並登入您的 Azure 訂用帳戶之後，您應該會在 Visual Studio 的左面板中看到 Azure 資料分析帳戶和儲存體。</span><span class="sxs-lookup"><span data-stu-id="51628-267">After starting Visual Studio and logging in your Azure subscription, you should see your Azure Data Analytics account and storage in the left panel of Visual Studio.</span></span>

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

<span data-ttu-id="51628-269">**將資料從 VM 移至資料湖：Azure 資料湖總管**</span><span class="sxs-lookup"><span data-stu-id="51628-269">**Move data from VM to Data Lake: Azure Data Lake Explorer**</span></span>

<span data-ttu-id="51628-270">您可以使用 **Azure Data Lake Explorer** ，將資料從虛擬機器中的本機檔案上傳至 Data Lake 儲存體。</span><span class="sxs-lookup"><span data-stu-id="51628-270">You can use **Azure Data Lake Explorer** to upload data from the local files in your Virtual Machine to Data Lake storage.</span></span>

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

<span data-ttu-id="51628-272">您也可以建立資料管線，使用 [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/)將資料移動至 Azure Data Lake 生產化，或將來自 Azure Data Lake 的資料移動生產化。</span><span class="sxs-lookup"><span data-stu-id="51628-272">You can also build a data pipeline to productionize your data movement to or from Azure Data Lake using the [Azure Data Factory(ADF)](https://azure.microsoft.com/services/data-factory/).</span></span> <span data-ttu-id="51628-273">我們會將您帶到這篇 [文章](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) ，引導您完成建立資料管線的步驟。</span><span class="sxs-lookup"><span data-stu-id="51628-273">We refer you to this [article](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) to guide you through the steps to build the data pipelines.</span></span>

<span data-ttu-id="51628-274">**將資料從 Azure Blob 讀取至資料湖：U-SQL**</span><span class="sxs-lookup"><span data-stu-id="51628-274">**Read data from Azure Blob to Data Lake: U-SQL**</span></span>

<span data-ttu-id="51628-275">如果您的資料位於 Azure Blob 儲存體中，您可以在 U-SQL 查詢中從 Azure 儲存體 Blob 直接讀取資料。</span><span class="sxs-lookup"><span data-stu-id="51628-275">If your data resides in Azure Blob storage, you can directly read data from Azure storage blob in U-SQL query.</span></span> <span data-ttu-id="51628-276">撰寫 U-SQL 查詢之前，請確定您的 Blob 儲存體帳戶已連結到您的 Azure 資料湖。</span><span class="sxs-lookup"><span data-stu-id="51628-276">Before composing your U-SQL query, make sure your blob storage account is linked to your Azure Data Lake.</span></span> <span data-ttu-id="51628-277">移至 **Azure 入口網站**、尋找您的 Azure Data Lake Analytics 儀表板、按一下 [新增資料來源]、選取 [Azure 儲存體] 做為儲存體類型，並插入您的 Azure 儲存體帳戶名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="51628-277">Go to **Azure portal**, find your Azure Data Lake Analytics dashboard, click **Add Data Source**, select storage type to **Azure Storage** and plug in your Azure Storage Account Name and Key.</span></span> <span data-ttu-id="51628-278">然後您可以參考儲存體帳戶中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="51628-278">Then you are able to reference the data stored in the storage account.</span></span>

![輸入儲存體帳戶和金鑰](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

<span data-ttu-id="51628-280">您可以在 Visual Studio 中，從 Blob 儲存體讀取資料、進行一些資料操作、功能工程，以及將結果資料輸出至 Azure 資料湖或 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="51628-280">In Visual Studio, you can read data from blob storage, do some data manipulation, feature engineering, and output the resulting data to either Azure Data Lake or Azure Blob Storage.</span></span> <span data-ttu-id="51628-281">當您參考 Blob 儲存體中的資料時，請使用 **wasb://**；當您參考 Azure Data Lake 中的資料時，請使用 **swbhdfs://**</span><span class="sxs-lookup"><span data-stu-id="51628-281">When you reference the data in blob storage, use **wasb://**; when you reference the data in Azure Data Lake, use **swbhdfs://**</span></span>

![資料框架](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

<span data-ttu-id="51628-283">您可以在 Visual Studio 中，使用下列 U-SQL 查詢：</span><span class="sxs-lookup"><span data-stu-id="51628-283">You may use the following U-SQL queries in Visual Studio:</span></span>

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
    TO "swebhdfs://<Azure Data Lake Storage Account Name>.azuredatalakestore.net/<Folder Name>/<Output Data File Name>"
    USING Outputters.Csv();

    OUTPUT @b   
    TO "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Output Data File Name>"
    USING Outputters.Csv();



<span data-ttu-id="51628-284">將查詢提交至伺服器之後，會顯示一個圖表來顯示您的作業狀態。</span><span class="sxs-lookup"><span data-stu-id="51628-284">After your query is submitted to the server, a diagram showing the status of your job is displayed.</span></span>

![作業狀態圖表](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

<span data-ttu-id="51628-286">**查詢資料湖中的資料：U-SQL**</span><span class="sxs-lookup"><span data-stu-id="51628-286">**Query data in Data Lake: U-SQL**</span></span>

<span data-ttu-id="51628-287">將資料集擷取到 Azure Data Lake 之後，您可以使用 [U-SQL 語言](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md)來查詢和探索資料。</span><span class="sxs-lookup"><span data-stu-id="51628-287">After the dataset is ingested into Azure Data Lake, you can use [U-SQL language](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) to query and explore the data.</span></span> <span data-ttu-id="51628-288">U-SQL 語言類似於 T-SQL，但結合了 C# 的一些功能，以便使用者撰寫自訂的模組、使用者定義的功能等。您可以在上一個步驟中使用指令碼。</span><span class="sxs-lookup"><span data-stu-id="51628-288">U-SQL language is similar to T-SQL, but combines some features from C# so that users can write customized modules, user-defined functions, and etc. You can use the scripts in the previous step.</span></span>

<span data-ttu-id="51628-289">將查詢提交到伺服器之後，很快就可以在 **Azure Data Lake Explorer** 中找到 tripdata_summary.CSV，以滑鼠右鍵按一下該檔案即可預覽資料。</span><span class="sxs-lookup"><span data-stu-id="51628-289">After the query is submitted to server, tripdata_summary.CSV can be found shortly in **Azure Data Lake Explorer**, you may preview the data by right-click the file.</span></span>

![Azure Data Lake Explorer 中的檔案](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

<span data-ttu-id="51628-291">若要查看檔案資訊：</span><span class="sxs-lookup"><span data-stu-id="51628-291">To see the file information:</span></span>

![檔案摘要](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a><span data-ttu-id="51628-293">HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="51628-293">HDInsight Hadoop Clusters</span></span>
<span data-ttu-id="51628-294">Azure HDInsight 是在雲端上的受管理 Apache Hadoop、Spark、HBase 和 Storm 服務。</span><span class="sxs-lookup"><span data-stu-id="51628-294">Azure HDInsight is a managed Apache Hadoop, Spark, HBase, and Storm service on the cloud.</span></span> <span data-ttu-id="51628-295">您可以輕鬆地從資料科學虛擬機器使用 Azure HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="51628-295">You can work easily with Azure HDInsight clusters from the data science virtual machine.</span></span>

<span data-ttu-id="51628-296">**先決條件**</span><span class="sxs-lookup"><span data-stu-id="51628-296">**Prerequisite**</span></span>

* <span data-ttu-id="51628-297">從 [Azure 入口網站](https://portal.azure.com)建立 Azure Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="51628-297">Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="51628-298">此儲存體帳戶用來儲存 HDInsight 叢集的資料。</span><span class="sxs-lookup"><span data-stu-id="51628-298">This storage account is used to store data for HDInsight clusters.</span></span>

![建立 Azure Blob 儲存體帳戶](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="51628-300">從 [Azure 入口網站](machine-learning-data-science-customize-hadoop-cluster.md)</span><span class="sxs-lookup"><span data-stu-id="51628-300">Customize Azure HDInsight Hadoop Clusters from [Azure portal](machine-learning-data-science-customize-hadoop-cluster.md)</span></span>
  
  * <span data-ttu-id="51628-301">您必須在建立時，將所建立的儲存體帳戶與 HDInsight 叢集連結。</span><span class="sxs-lookup"><span data-stu-id="51628-301">You must link the storage account created with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="51628-302">此儲存體帳戶用於存取可以在叢集內處理的資料。</span><span class="sxs-lookup"><span data-stu-id="51628-302">This storage account is used for accessing data that can be processed within the cluster.</span></span>

![連結到以 HDInsight 叢集建立的儲存體帳戶](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* <span data-ttu-id="51628-304">建立後，您必須對叢集的前端節點啟用 **遠端存取** 。</span><span class="sxs-lookup"><span data-stu-id="51628-304">You must enable **Remote Access** to the head node of the cluster after it is created.</span></span> <span data-ttu-id="51628-305">請記住您在這裡指定的遠端存取認證 (與建立叢集時指定的不同)：您在後續程序中需要用到它們。</span><span class="sxs-lookup"><span data-stu-id="51628-305">Remember the remote access credentials you specify here (different from those specified for the cluster at its creation): you need them in the subsequent procedure.</span></span>

![啟用遠端存取](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* <span data-ttu-id="51628-307">建立 Azure Machine Learning 工作區。</span><span class="sxs-lookup"><span data-stu-id="51628-307">Create an Azure Machine Learning workspace.</span></span> <span data-ttu-id="51628-308">您的機器學習實驗將會儲存在此 Machine Learning 工作區中。</span><span class="sxs-lookup"><span data-stu-id="51628-308">Your Machine Learning Experiments are stored in this Machine Learning workspace.</span></span> <span data-ttu-id="51628-309">在入口網站中選取反白顯示的選項，如下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="51628-309">Select the highlighted options in Portal as shown in the following screenshot:</span></span>

![建立 Azure Machine Learning 工作區](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* <span data-ttu-id="51628-311">然後輸入工作區的參數</span><span class="sxs-lookup"><span data-stu-id="51628-311">Then enter the parameters for your workspace</span></span>

![輸入 Machine Learning 工作區參數](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* <span data-ttu-id="51628-313">使用 IPython Notebook 上傳資料。</span><span class="sxs-lookup"><span data-stu-id="51628-313">Upload data using IPython Notebook.</span></span> <span data-ttu-id="51628-314">先匯入所需的封裝、插入認證在儲存體帳戶中建立資料庫，然後將資料載入 HDI 叢集。</span><span class="sxs-lookup"><span data-stu-id="51628-314">First import required packages, plug in credentials, create a db in your storage account, then load data to HDI clusters.</span></span>

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


        #Create the connection to Hive using ODBC
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


        #Upload data from blob storage to HDI cluster
        for i in range(1,13):
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxitripraw2/trip_data_%d.csv' INTO TABLE nyctaxidb2.trip PARTITION (month=%d);"%(i,i)
            cursor.execute(queryString)
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxifareraw2/trip_fare_%d.csv' INTO TABLE nyctaxidb2.fare PARTITION (month=%d);"%(i,i)  
            cursor.execute(queryString)


* <span data-ttu-id="51628-315">或者，您可以遵循此[逐步解說](machine-learning-data-science-process-hive-walkthrough.md)，將 NYC 計程車資料上傳至 HDI 叢集。</span><span class="sxs-lookup"><span data-stu-id="51628-315">Alternately,  you can follow this [walkthrough](machine-learning-data-science-process-hive-walkthrough.md) to upload NYC Taxi data to HDI cluster.</span></span> <span data-ttu-id="51628-316">主要步驟包括：</span><span class="sxs-lookup"><span data-stu-id="51628-316">Major steps include:</span></span>
  
  * <span data-ttu-id="51628-317">AzCopy：從公用 Blob 將已壓縮的 CSV 下載到本機資料夾</span><span class="sxs-lookup"><span data-stu-id="51628-317">AzCopy: download zipped CSV's from public blob to your local folder</span></span>
  * <span data-ttu-id="51628-318">AzCopy：從本機資料夾將已解壓縮的 CSV 上傳至 HDI 叢集</span><span class="sxs-lookup"><span data-stu-id="51628-318">AzCopy: upload unzipped CSV's from local folder to HDI cluster</span></span>
  * <span data-ttu-id="51628-319">登入 Hadoop 叢集的前端節點，並準備進行探索資料分析</span><span class="sxs-lookup"><span data-stu-id="51628-319">Log into the head node of Hadoop cluster and prepare for exploratory data analysis</span></span>

<span data-ttu-id="51628-320">在資料載入至 HDI 叢集之後，您可以在 Azure 儲存體總管中檢查您的資料。</span><span class="sxs-lookup"><span data-stu-id="51628-320">After the data is loaded to HDI cluster, you can check your data in Azure Storage Explorer.</span></span> <span data-ttu-id="51628-321">而您會在 HDI 叢集中建立資料庫 nyctaxidb。</span><span class="sxs-lookup"><span data-stu-id="51628-321">And you have a database nyctaxidb created in HDI cluster.</span></span>

<span data-ttu-id="51628-322">**資料探索：Python 中的 Hive 查詢**</span><span class="sxs-lookup"><span data-stu-id="51628-322">**Data exploration: Hive Queries in Python**</span></span>

<span data-ttu-id="51628-323">因為資料位於 Hadoop 叢集中，您可以使用 pyodbc 封裝連接到 Hadoop 叢集，並使用 Hive 查詢資料庫以便進行探索和設計功能。</span><span class="sxs-lookup"><span data-stu-id="51628-323">Since the data is in Hadoop cluster, you can use the pyodbc package to connect to Hadoop Clusters and query database using Hive to do exploration and feature engineering.</span></span> <span data-ttu-id="51628-324">您可以檢視在先決條件步驟中建立的現有資料表。</span><span class="sxs-lookup"><span data-stu-id="51628-324">You can view the existing tables we created in the prerequisite step.</span></span>

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![檢視現有的表格](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

<span data-ttu-id="51628-326">讓我們看一下每個月的記錄筆數以及車程資料表中已付小費或未付小費的頻率：</span><span class="sxs-lookup"><span data-stu-id="51628-326">Let's look at the number of records in each month and the frequencies of tipped or not in the trip table:</span></span>

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

<span data-ttu-id="51628-329">我們也可以計算上車位置與下車位置之間的距離，然後再與車程距離比較。</span><span class="sxs-lookup"><span data-stu-id="51628-329">We can also compute the distance between pickup location and dropoff location and then compare it to the trip distance.</span></span>

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


![上下車距離及車程距離繪圖](./media/machine-learning-data-science-vm-do-ten-things/Exploration_direct_distance_trip_distance_v2.PNG)

<span data-ttu-id="51628-332">現在讓我們準備縮減取樣 (1%) 資料集，以便進行模型分析。</span><span class="sxs-lookup"><span data-stu-id="51628-332">Now let's prepare a down-sampled (1%) set of data for modeling.</span></span> <span data-ttu-id="51628-333">我們可以在 Machine Learning 讀取器模組中使用此資料。</span><span class="sxs-lookup"><span data-stu-id="51628-333">We can use this data in Machine Learning reader module.</span></span>

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

        --- now insert contents of the join into the preceding internal table

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

<span data-ttu-id="51628-334">不久之後，您可以看見資料已載入 Hadoop 叢集中：</span><span class="sxs-lookup"><span data-stu-id="51628-334">After a while, you can see the data has been loaded in Hadoop clusters:</span></span>

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![資料表](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

<span data-ttu-id="51628-336">**使用 Machine Learning 從 HDI 讀取資料：讀取器模組**</span><span class="sxs-lookup"><span data-stu-id="51628-336">**Read data from HDI using Machine Learning: reader module**</span></span>

<span data-ttu-id="51628-337">您也可以在 Machine Learning Studio 中使用**讀取器**模組來存取 Hadoop 叢集中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="51628-337">You may also use the **reader** module in Machine Learning Studio to access the database in Hadoop cluster.</span></span> <span data-ttu-id="51628-338">插入 HDI 叢集和 Azure 儲存體帳戶的認證，以在 HDI 叢集中使用資料庫建置機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="51628-338">Plug in the credentials of your HDI clusters and Azure Storage Account to enable build ing machine learning models using database in HDI clusters.</span></span>

![讀取器模組屬性](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

<span data-ttu-id="51628-340">接著可以檢視評分資料集：</span><span class="sxs-lookup"><span data-stu-id="51628-340">The scored dataset can then be viewed:</span></span>

![檢視已評分的資料集](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a><span data-ttu-id="51628-342">Azure SQL 資料倉儲和資料庫</span><span class="sxs-lookup"><span data-stu-id="51628-342">Azure SQL Data Warehouse & databases</span></span>
<span data-ttu-id="51628-343">Azure SQL 資料倉儲是彈性的資料倉儲即服務，具有企業層級的 SQL Server 體驗。</span><span class="sxs-lookup"><span data-stu-id="51628-343">Azure SQL Data Warehouse is an elastic data warehouse as a service with enterprise-class SQL Server experience.</span></span>

<span data-ttu-id="51628-344">您可以藉由遵循這篇[文章](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md)中提供的指示，佈建您的 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="51628-344">You can provision your Azure SQL Data Warehouse by following the instructions provided in this [article](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span></span> <span data-ttu-id="51628-345">佈建 Azure SQL 資料倉儲之後，就可以使用這個[逐步解說](machine-learning-data-science-process-sqldw-walkthrough.md) ，進行資料上傳、探索以及使用 SQL 資料倉儲中的資料建立模型。</span><span class="sxs-lookup"><span data-stu-id="51628-345">Once you provision your Azure SQL Data Warehouse, you can use this [walkthrough](machine-learning-data-science-process-sqldw-walkthrough.md) to do data upload, exploration and modeling using data within the SQL Data Warehouse.</span></span>

#### <a name="azure-cosmos-db"></a><span data-ttu-id="51628-346">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="51628-346">Azure Cosmos DB</span></span>
<span data-ttu-id="51628-347">Azure Cosmos DB 是雲端中的一種 NoSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="51628-347">Azure Cosmos DB is a NoSQL database in the cloud.</span></span> <span data-ttu-id="51628-348">它可讓您使用 JSON 等文件，並可讓您儲存和查詢文件。</span><span class="sxs-lookup"><span data-stu-id="51628-348">It allows you to work with documents like JSON and allows you to store and query the documents.</span></span>

<span data-ttu-id="51628-349">您必須執行下列必要步驟，才能從 DSVM 存取 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="51628-349">You need to do the following per-requisites steps to access Azure Cosmos DB from the DSVM.</span></span>

1. <span data-ttu-id="51628-350">安裝 DocumentDB Python SDK (從命令提示字元執行 ```pip install pydocumentdb``` )</span><span class="sxs-lookup"><span data-stu-id="51628-350">Install DocumentDB Python SDK (Run ```pip install pydocumentdb``` from command prompt)</span></span>
2. <span data-ttu-id="51628-351">從 [Azure 入口網站](https://portal.azure.com)建立 Azure Cosmos DB 帳戶和資料庫</span><span class="sxs-lookup"><span data-stu-id="51628-351">Create an Azure Cosmos DB account and a database from [Azure portal](https://portal.azure.com)</span></span>
3. <span data-ttu-id="51628-352">從[這裡](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d)下載「Azure Cosmos DB 移轉工具」並解壓縮至您所選的目錄</span><span class="sxs-lookup"><span data-stu-id="51628-352">Download "Azure Cosmos DB Migration Tool" from [here](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) and extract to a directory of your choice</span></span>
4. <span data-ttu-id="51628-353">對移轉工具使用下列命令參數 (Cosmos DB 移轉工具安裝目錄中的 dtui.exe)，將儲存在[公用 Blob](https://cahandson.blob.core.windows.net/samples/volcano.json) 的 JSON 資料 (Volcano 資料) 匯入 Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="51628-353">Import JSON data (volcano data) stored on a [public blob](https://cahandson.blob.core.windows.net/samples/volcano.json) into Cosmos DB with following command parameters to the migration tool (dtui.exe from the directory where you installed the Cosmos DB Migration Tool).</span></span> <span data-ttu-id="51628-354">輸入下面的來源和目標位置參數：</span><span class="sxs-lookup"><span data-stu-id="51628-354">Enter the source and target location with these parameters:</span></span>
   
    <span data-ttu-id="51628-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span><span class="sxs-lookup"><span data-stu-id="51628-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span></span>

<span data-ttu-id="51628-356">一旦匯入資料之後，您即可移至 Jupyter 並開啟標題為 *DocumentDBSample* 且包含 python 程式碼的筆記本，以存取 DocumentDB 及進行一些基本查詢。</span><span class="sxs-lookup"><span data-stu-id="51628-356">Once you import the data, you can go to Jupyter and open the notebook titled *DocumentDBSample* which contains python code to access DocumentDB and do some basic querying.</span></span> <span data-ttu-id="51628-357">如需深入了解 Cosmos DB，請參閱服務[文件頁面](https://docs.microsoft.com/azure/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="51628-357">You can learn more about Cosmos DB by visiting the service [documentation page](https://docs.microsoft.com/azure/cosmos-db/).</span></span>

## <a name="8-build-reports-and-dashboard-using-the-power-bi-desktop"></a><span data-ttu-id="51628-358">8.使用 Power BI Desktop 建立報表和儀表板</span><span class="sxs-lookup"><span data-stu-id="51628-358">8. Build reports and dashboard using the Power BI Desktop</span></span>
<span data-ttu-id="51628-359">讓我們將在 Power BI 的前述 Cosmos DB 範例中看見的 Volcano JSON 檔案視覺化，以深入了解資料。</span><span class="sxs-lookup"><span data-stu-id="51628-359">Let us visualize the Volcano JSON file that we saw in the preceding Cosmos DB example in Power BI to gain visual insights into the data.</span></span> <span data-ttu-id="51628-360">在 [Power BI 文章](../cosmos-db/powerbi-visualize.md)中可找到詳細的步驟。</span><span class="sxs-lookup"><span data-stu-id="51628-360">Detailed steps are available in the [Power BI article](../cosmos-db/powerbi-visualize.md).</span></span> <span data-ttu-id="51628-361">高階步驟如下：</span><span class="sxs-lookup"><span data-stu-id="51628-361">Here are the high-level steps:</span></span>

1. <span data-ttu-id="51628-362">開啟 Power BI Desktop 並執行「取得資料」。</span><span class="sxs-lookup"><span data-stu-id="51628-362">Open Power BI Desktop and do "Get Data".</span></span> <span data-ttu-id="51628-363">將 URL 指定為︰https://cahandson.blob.core.windows.net/samples/volcano.json</span><span class="sxs-lookup"><span data-stu-id="51628-363">Specify the URL as: https://cahandson.blob.core.windows.net/samples/volcano.json</span></span>
2. <span data-ttu-id="51628-364">您應該會看到匯入為清單的 JSON 記錄</span><span class="sxs-lookup"><span data-stu-id="51628-364">You should see the JSON records imported as a list</span></span>
3. <span data-ttu-id="51628-365">將清單轉換成資料表供 PowerBI 使用</span><span class="sxs-lookup"><span data-stu-id="51628-365">Convert the list to a table so Power BI can work with the same</span></span>
4. <span data-ttu-id="51628-366">按一下展開圖示 (資料行左側具有「向左箭號與向右箭號」的圖示)，即可展開資料行</span><span class="sxs-lookup"><span data-stu-id="51628-366">Expand the columns by clicking on the expand icon (the one with the "left arrow and a right arrow" icon on the right of the column)</span></span>
5. <span data-ttu-id="51628-367">請注意，該位置是「記錄」欄位。</span><span class="sxs-lookup"><span data-stu-id="51628-367">Notice that location is a "Record" field.</span></span> <span data-ttu-id="51628-368">展開記錄，然後只選取座標。</span><span class="sxs-lookup"><span data-stu-id="51628-368">Expand the record and select only the coordinates.</span></span> <span data-ttu-id="51628-369">座標是清單資料行</span><span class="sxs-lookup"><span data-stu-id="51628-369">Coordinate is a list column</span></span>
6. <span data-ttu-id="51628-370">加入新的資料行，以將清單座標資料行轉換成逗號分隔的 LatLong 資料行，其使用公式 ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```來串連座標清單欄位中的兩個元素。</span><span class="sxs-lookup"><span data-stu-id="51628-370">Add a new column to convert the list coordinate column into a comma separate LatLong column concatenating the two elements in the coordinate list field using the formula ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span></span>
7. <span data-ttu-id="51628-371">最後將 ```Elevation``` 資料行轉換成 [十進位]，然後選取 [關閉] 和 [套用]。</span><span class="sxs-lookup"><span data-stu-id="51628-371">Finally convert the ```Elevation``` column to Decimal and select the **Close** and **Apply**.</span></span>

<span data-ttu-id="51628-372">除了前述步驟，您可以貼上下列程式碼，此程式碼會以指令碼撰寫在 PowerBI 的 [進階編輯器] 中使用的步驟，讓您以查詢語言撰寫資料轉換。</span><span class="sxs-lookup"><span data-stu-id="51628-372">Instead of preceding steps, you can paste the following code that scripts out the steps used in the Advanced Editor in Power BI that allows you to write the data transformations in a query language.</span></span>

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted to Table" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted to Table", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



<span data-ttu-id="51628-373">您的 Power BI 資料模型中現在會有資料。</span><span class="sxs-lookup"><span data-stu-id="51628-373">You now have the data in your Power BI data model.</span></span> <span data-ttu-id="51628-374">您的 Power BI Desktop 應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="51628-374">Your Power BI desktop should appear as follows:</span></span>

![Power BI 桌面](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

<span data-ttu-id="51628-376">您可以開始使用資料模型來建立報告和視覺效果。</span><span class="sxs-lookup"><span data-stu-id="51628-376">You can start building reports and visualizations using the data model.</span></span> <span data-ttu-id="51628-377">您可以遵循這篇 [Power BI 文章](../cosmos-db/powerbi-visualize.md#build-the-reports)中的步驟來建立報告。</span><span class="sxs-lookup"><span data-stu-id="51628-377">You can follow the steps in this [Power BI article](../cosmos-db/powerbi-visualize.md#build-the-reports) to build a report.</span></span> <span data-ttu-id="51628-378">最後的結果會是如下所示的報告。</span><span class="sxs-lookup"><span data-stu-id="51628-378">The end result is a report that looks like the following.</span></span>

![Power BI Desktop 報告檢視 - Power BI 連接器](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-to-meet-your-project-needs"></a><span data-ttu-id="51628-380">9.動態調整 DSVM 以符合您的專案需求</span><span class="sxs-lookup"><span data-stu-id="51628-380">9. Dynamically scale your DSVM to meet your project needs</span></span>
<span data-ttu-id="51628-381">您可以相應增加和減少 DSVM 以符合您的專案需求。</span><span class="sxs-lookup"><span data-stu-id="51628-381">You can scale up and down the DSVM to meet your project needs.</span></span> <span data-ttu-id="51628-382">如果您在晚上或週末不需要使用 VM，就可以從 [Azure 入口網站](https://portal.azure.com)關閉 VM。</span><span class="sxs-lookup"><span data-stu-id="51628-382">If you don't need to use the VM in the evening or weekends, you can just shut down the VM from the [Azure portal](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="51628-383">如果您只使用 VM 上的作業系統關機按鈕，則需支付計算費用。</span><span class="sxs-lookup"><span data-stu-id="51628-383">You incur compute charges if you use just the Operating system shutdown button on the VM.</span></span>  
> 
> 

<span data-ttu-id="51628-384">如果您需要處理一些大規模分析，而且需要更多 CPU 和/或記憶體和/或磁碟容量，您可以找到許多符合您的計算和預算需求的 VM 大小選擇 (從 CPU 核心、記憶體容量和磁碟類型 (包括固態硬碟機) 方面來看)。</span><span class="sxs-lookup"><span data-stu-id="51628-384">If you need to handle some large-scale analysis and need more CPU and/or memory and/or disk capacity you can find a large choice of VM sizes in terms of CPU cores, memory capacity and disk types (including Solid state drives) that meet your compute and budgetary needs.</span></span> <span data-ttu-id="51628-385">[Azure 虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/)頁面提供完整 VM 清單和其每小時的計算價格。</span><span class="sxs-lookup"><span data-stu-id="51628-385">The full list of VMs along with their hourly compute pricing is available on the [Azure Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/) page.</span></span>

<span data-ttu-id="51628-386">同樣地，如果您的 VM 處理容量需求降低 (例如：將主要工作負載移至 Hadoop 或 Spark 叢集)，您可以從 [Azure 入口網站](https://portal.azure.com)移至您的 VM 執行個體設定來相應減少叢集。</span><span class="sxs-lookup"><span data-stu-id="51628-386">Similarly, if your need for VM processing capacity reduces (for example: you moved a major workload to a Hadoop or a Spark cluster), you can scale down the cluster from the [Azure portal](https://portal.azure.com) and going to the settings of your VM instance.</span></span> <span data-ttu-id="51628-387">以下為螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="51628-387">Here is a screenshot.</span></span>

![VM 執行個體設定](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a><span data-ttu-id="51628-389">10.在虛擬機器上安裝其他工具</span><span class="sxs-lookup"><span data-stu-id="51628-389">10. Install additional tools on your virtual machine</span></span>
<span data-ttu-id="51628-390">我們已封裝數個工具，我們相信這可以滿足許多常見的資料分析需求，並藉由避免必須逐一安裝和設定您的環境而節省您的時間，且只支付您所用的資源而節省您的成本。</span><span class="sxs-lookup"><span data-stu-id="51628-390">We have packaged several tools that we believe are able to address many of the common data analytics needs and that should save you time by avoiding having to install and configure your environments one by one and save you money by paying only for resources that you use.</span></span>

<span data-ttu-id="51628-391">您可以運用本文略述的其他 Azure 資料和分析資料服務，以增強您的分析環境。</span><span class="sxs-lookup"><span data-stu-id="51628-391">You can leverage other Azure data and analytics services profiled in this article to enhance your analytics environment.</span></span> <span data-ttu-id="51628-392">我們了解，在某些情況下您的需求可能需要額外的工具，包括一些專屬的協力廠商工具。</span><span class="sxs-lookup"><span data-stu-id="51628-392">We understand that in some cases your needs may require additional tools, including some proprietary third-party tools.</span></span> <span data-ttu-id="51628-393">您有完整的系統管理權限可在虛擬機器上安裝您所需的新工具。</span><span class="sxs-lookup"><span data-stu-id="51628-393">You have full administrative access on the virtual machine to install new tools you need.</span></span> <span data-ttu-id="51628-394">您也可以在 Python 和 R 中安裝其他未預先安裝的封裝。</span><span class="sxs-lookup"><span data-stu-id="51628-394">You can also install additional packages in Python and R that are not pre-installed.</span></span> <span data-ttu-id="51628-395">對於 Python，您可以使用 ```conda``` 或 ```pip```。</span><span class="sxs-lookup"><span data-stu-id="51628-395">For Python you can use either ```conda``` or ```pip```.</span></span> <span data-ttu-id="51628-396">對於 R，您可以在 R 主控台中使用 ```install.packages()```，或使用整合式開發環境 (IDE) 並選擇 [套件] -> [安裝套件]。</span><span class="sxs-lookup"><span data-stu-id="51628-396">For R you can use the ```install.packages()``` in the R console or use the IDE and choose "**Packages** -> **Install Packages...**".</span></span>

## <a name="summary"></a><span data-ttu-id="51628-397">摘要</span><span class="sxs-lookup"><span data-stu-id="51628-397">Summary</span></span>
<span data-ttu-id="51628-398">這些只是您可以在 Microsoft Data Science Virtual Machine 上可做的一些事情。</span><span class="sxs-lookup"><span data-stu-id="51628-398">These are just some of the things you can do on the Microsoft Data Science Virtual Machine.</span></span> <span data-ttu-id="51628-399">您還可以做更多事情，讓它成為有效的分析環境。</span><span class="sxs-lookup"><span data-stu-id="51628-399">There are many more things you can do to make it an effective analytics environment.</span></span>

