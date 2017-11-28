---
title: "Machine Learning python azure Python 用戶端程式庫 aaaAccess 資料集 |Microsoft 文件"
description: "安裝和使用 Python 用戶端程式庫 tooaccess hello 和管理 Azure Machine Learning 資料安全地從本機 Python 環境。"
services: machine-learning
documentationcenter: python
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ab42272-c30c-4b7e-8e66-d64eafef22d0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: huvalo;bradsev
ms.openlocfilehash: f55067118f13c52bf677930a20836ce6989f8187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="access-datasets-with-python-using-hello-azure-machine-learning-python-client-library"></a><span data-ttu-id="6733c-103">使用 Python 使用 hello Azure Machine Learning python azure Python 用戶端程式庫的存取資料集</span><span class="sxs-lookup"><span data-stu-id="6733c-103">Access datasets with Python using hello Azure Machine Learning Python client library</span></span>
<span data-ttu-id="6733c-104">Microsoft Azure Machine Learning python azure Python 用戶端程式庫的 hello 預覽可以啟用安全存取 tooyour 本機的 Python 環境的 Azure Machine Learning 資料集，並啟用 hello 建立和管理的工作區中的資料集。</span><span class="sxs-lookup"><span data-stu-id="6733c-104">hello preview of Microsoft Azure Machine Learning Python client library can enable secure access tooyour Azure Machine Learning datasets from a local Python environment and enables hello creation and management of datasets in a workspace.</span></span>

<span data-ttu-id="6733c-105">本主題提供如何執行以下作業的指示：</span><span class="sxs-lookup"><span data-stu-id="6733c-105">This topic provides instructions on how to:</span></span>

* <span data-ttu-id="6733c-106">安裝 hello Machine Learning python azure Python 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="6733c-106">install hello Machine Learning Python client library</span></span> 
* <span data-ttu-id="6733c-107">存取和上傳資料集，包括如何指示 tooget 授權 tooaccess 來自本機 Python 環境的 Azure Machine Learning 資料集</span><span class="sxs-lookup"><span data-stu-id="6733c-107">access and upload datasets, including instructions on how tooget authorization tooaccess Azure Machine Learning datasets from your local Python environment</span></span>
* <span data-ttu-id="6733c-108">存取實驗中的中繼資料集</span><span class="sxs-lookup"><span data-stu-id="6733c-108">access intermediate datasets from experiments</span></span>
* <span data-ttu-id="6733c-109">使用 hello Python 用戶端程式庫 tooenumerate 資料集、 存取中繼資料、 讀取資料集 hello 內容、 建立新的資料集以及更新現有的資料集</span><span class="sxs-lookup"><span data-stu-id="6733c-109">use hello Python client library tooenumerate datasets, access metadata, read hello contents of a dataset, create new datasets and update existing datasets</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <span data-ttu-id="6733c-110"><a name="prerequisites"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="6733c-110"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="6733c-111">hello Python 用戶端程式庫已經過測試，在下列環境的 hello:</span><span class="sxs-lookup"><span data-stu-id="6733c-111">hello Python client library has been tested under hello following environments:</span></span>

* <span data-ttu-id="6733c-112">Windows、Mac 及 Linux</span><span class="sxs-lookup"><span data-stu-id="6733c-112">Windows, Mac and Linux</span></span>
* <span data-ttu-id="6733c-113">Python 2.7、3.3 及 3.4</span><span class="sxs-lookup"><span data-stu-id="6733c-113">Python 2.7, 3.3 and 3.4</span></span>

<span data-ttu-id="6733c-114">它會相依於下列套件 hello 時：</span><span class="sxs-lookup"><span data-stu-id="6733c-114">It has a dependency on hello following packages:</span></span>

* <span data-ttu-id="6733c-115">requests</span><span class="sxs-lookup"><span data-stu-id="6733c-115">requests</span></span>
* <span data-ttu-id="6733c-116">python-dateutil</span><span class="sxs-lookup"><span data-stu-id="6733c-116">python-dateutil</span></span>
* <span data-ttu-id="6733c-117">pandas</span><span class="sxs-lookup"><span data-stu-id="6733c-117">pandas</span></span>

<span data-ttu-id="6733c-118">我們建議使用，例如 Python 發佈[Anaconda](http://continuum.io/downloads#all)或[Canopy](https://store.enthought.com/downloads/)，它會使用 Python，IPython 與上面所列的 hello 三個封裝安裝。</span><span class="sxs-lookup"><span data-stu-id="6733c-118">We recommend using a Python distribution such as [Anaconda](http://continuum.io/downloads#all) or [Canopy](https://store.enthought.com/downloads/), which come with Python, IPython and hello three packages listed above installed.</span></span> <span data-ttu-id="6733c-119">雖然不一定需要 IPython，但它是以互動方式操作和虛擬化資料的絕佳環境。</span><span class="sxs-lookup"><span data-stu-id="6733c-119">Although IPython is not strictly required, it is a great environment for manipulating and visualizing data interactively.</span></span>

### <span data-ttu-id="6733c-120"><a name="installation"></a>如何 tooinstall hello Azure Machine Learning python azure Python 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="6733c-120"><a name="installation"></a>How tooinstall hello Azure Machine Learning Python client library</span></span>
<span data-ttu-id="6733c-121">hello Azure Machine Learning python azure Python 用戶端程式庫也必須是本主題所述安裝的 toocomplete hello 工作。</span><span class="sxs-lookup"><span data-stu-id="6733c-121">hello Azure Machine Learning Python client library must also be installed toocomplete hello tasks outlined in this topic.</span></span> <span data-ttu-id="6733c-122">它是可從 hello [Python 封裝索引](https://pypi.python.org/pypi/azureml)。</span><span class="sxs-lookup"><span data-stu-id="6733c-122">It is available from hello [Python Package Index](https://pypi.python.org/pypi/azureml).</span></span> <span data-ttu-id="6733c-123">tooinstall 它在 Python 環境中，執行下列命令，從本機 Python 環境的 hello:</span><span class="sxs-lookup"><span data-stu-id="6733c-123">tooinstall it in your Python environment, run hello following command from your local Python environment:</span></span>

    pip install azureml

<span data-ttu-id="6733c-124">或者，您可以下載並安裝來自 hello 來源上[github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python)。</span><span class="sxs-lookup"><span data-stu-id="6733c-124">Alternatively, you can download and install from hello sources on [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span></span>

    python setup.py install

<span data-ttu-id="6733c-125">如果您有安裝在您的電腦上的 git，您可以使用 pip tooinstall 直接從 hello git 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="6733c-125">If you have git installed on your machine, you can use pip tooinstall directly from hello git repository:</span></span>

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <span data-ttu-id="6733c-126"><a name="datasetAccess"></a>使用 Studio 程式碼片段 tooaccess 資料集</span><span class="sxs-lookup"><span data-stu-id="6733c-126"><a name="datasetAccess"></a>Use Studio Code snippets tooaccess datasets</span></span>
<span data-ttu-id="6733c-127">hello Python 用戶端程式庫可讓您以程式設計方式存取 tooyour 現有資料集已執行的實驗中。</span><span class="sxs-lookup"><span data-stu-id="6733c-127">hello Python client library gives you programmatic access tooyour existing datasets from experiments that have been run.</span></span>

<span data-ttu-id="6733c-128">從 hello Studio web 介面，您可以產生程式碼片段，其中包括所有 hello 所需的資訊 toodownload 及還原序列化為熊資料框架物件，您位置的電腦上的資料集。</span><span class="sxs-lookup"><span data-stu-id="6733c-128">From hello Studio web interface, you can generate code snippets that include all hello necessary information toodownload and deserialize datasets as Pandas DataFrame objects on your location machine.</span></span>

### <span data-ttu-id="6733c-129"><a name="security"></a>資料存取安全性</span><span class="sxs-lookup"><span data-stu-id="6733c-129"><a name="security"></a>Security for data access</span></span>
<span data-ttu-id="6733c-130">hello Studio 所提供的工作區識別碼和授權，包括與 hello Python 用戶端程式庫搭配使用的程式碼片段語彙基元。</span><span class="sxs-lookup"><span data-stu-id="6733c-130">hello code snippets provided by Studio for use with hello Python client library includes your workspace id and authorization token.</span></span> <span data-ttu-id="6733c-131">這些提供完整存取 tooyour 工作區，必須受到保護，像是密碼一樣。</span><span class="sxs-lookup"><span data-stu-id="6733c-131">These provide full access tooyour workspace and must be protected, like a password.</span></span>

<span data-ttu-id="6733c-132">基於安全性理由，hello 程式碼片段時，才功能已設定為其角色的可用 toousers**擁有者**hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="6733c-132">For security reasons, hello code snippet functionality is only available toousers that have their role set as **Owner** for hello workspace.</span></span> <span data-ttu-id="6733c-133">您的角色會顯示 Azure Machine Learning Studio 中的 hello**使用者**頁面**設定**。</span><span class="sxs-lookup"><span data-stu-id="6733c-133">Your role is displayed in Azure Machine Learning Studio on hello **USERS** page under **Settings**.</span></span>

![安全性][security]

<span data-ttu-id="6733c-135">如果您的角色未設定為**擁有者**，您可以要求 toobe reinvited 作為擁有者，或要求擁有者 hello hello 工作區 tooprovide 您與 hello 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="6733c-135">If your role is not set as **Owner**, you can either request toobe reinvited as an owner, or ask hello owner of hello workspace tooprovide you with hello code snippet.</span></span>

<span data-ttu-id="6733c-136">tooobtain hello 授權權杖，您可以執行 hello 下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="6733c-136">tooobtain hello authorization token, you can do one of hello following:</span></span>

* <span data-ttu-id="6733c-137">向擁有者要求權杖。</span><span class="sxs-lookup"><span data-stu-id="6733c-137">Ask for a token from an owner.</span></span> <span data-ttu-id="6733c-138">擁有者可以從他們的工作區在 Studio 中的 hello [設定] 頁面存取其授權權杖。</span><span class="sxs-lookup"><span data-stu-id="6733c-138">Owners can access their authorization tokens from hello Settings page of their workspace in Studio.</span></span> <span data-ttu-id="6733c-139">選取**設定**從左窗格中，然後按一下 hello**授權權杖**toosee hello 主要和次要的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="6733c-139">Select **Settings** from hello left pane and click **AUTHORIZATION TOKENS** toosee hello primary and secondary tokens.</span></span>  <span data-ttu-id="6733c-140">雖然主要 hello 次要授權權杖可以用 hello 程式碼片段中，建議的擁有者只能共用 hello 次要授權權杖。</span><span class="sxs-lookup"><span data-stu-id="6733c-140">Although either hello primary or hello secondary authorization tokens can be used in hello code snippet, it is recommended that owners only share hello secondary authorization tokens.</span></span>

![授權權杖](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* <span data-ttu-id="6733c-142">要求升級 toobe toorole 的擁有者。</span><span class="sxs-lookup"><span data-stu-id="6733c-142">Ask toobe promoted toorole of owner.</span></span>  <span data-ttu-id="6733c-143">toodo 這 hello 工作區需要 toofirst 的目前擁有者移除您從 hello] 工作區，然後重新邀請您 tooit 作為擁有者。</span><span class="sxs-lookup"><span data-stu-id="6733c-143">toodo this, a current owner of hello workspace needs toofirst remove you from hello workspace then re-invite you tooit as an owner.</span></span>

<span data-ttu-id="6733c-144">一旦開發人員取得 hello 工作區識別碼和授權權杖，它們會是能 tooaccess hello 工作區中使用 hello 程式碼片段，不論其角色。</span><span class="sxs-lookup"><span data-stu-id="6733c-144">Once developers have obtained hello workspace id and authorization token, they are able tooaccess hello workspace using hello code snippet regardless of their role.</span></span>

<span data-ttu-id="6733c-145">授權權杖上 hello 管理**授權權杖**頁面**設定**。</span><span class="sxs-lookup"><span data-stu-id="6733c-145">Authorization tokens are managed on hello **AUTHORIZATION TOKENS** page under **SETTINGS**.</span></span> <span data-ttu-id="6733c-146">您可以重新產生它們，但此程序撤銷存取 toohello 之前語彙基元。</span><span class="sxs-lookup"><span data-stu-id="6733c-146">You can regenerate them, but this procedure revokes access toohello previous token.</span></span>

### <span data-ttu-id="6733c-147"><a name="accessingDatasets"></a>從本機 Python 應用程式存取資料集</span><span class="sxs-lookup"><span data-stu-id="6733c-147"><a name="accessingDatasets"></a>Access datasets from a local Python application</span></span>
1. <span data-ttu-id="6733c-148">在機器學習 Studio 中，按一下 [**資料集**hello hello 左側的導覽列中。</span><span class="sxs-lookup"><span data-stu-id="6733c-148">In Machine Learning Studio, click **DATASETS** in hello navigation bar on hello left.</span></span>
2. <span data-ttu-id="6733c-149">選取您想要 tooaccess hello 資料集。</span><span class="sxs-lookup"><span data-stu-id="6733c-149">Select hello dataset you would like tooaccess.</span></span> <span data-ttu-id="6733c-150">您可以選取任何的 hello 資料集從 hello**我的資料集**清單或從 hello**範例**清單。</span><span class="sxs-lookup"><span data-stu-id="6733c-150">You can select any of hello datasets from hello **MY DATASETS** list or from hello **SAMPLES** list.</span></span>
3. <span data-ttu-id="6733c-151">從 hello 底部工具列中按一下**產生的資料存取程式碼**。</span><span class="sxs-lookup"><span data-stu-id="6733c-151">From hello bottom toolbar, click **Generate Data Access Code**.</span></span> <span data-ttu-id="6733c-152">如果 hello 資料與 hello Python 用戶端程式庫不相容的格式，此按鈕會停用。</span><span class="sxs-lookup"><span data-stu-id="6733c-152">If hello data is in a format incompatible with hello Python client library, this button is disabled.</span></span>
   
    ![資料集][datasets]
4. <span data-ttu-id="6733c-154">從出現的 hello 視窗選取 hello 程式碼片段，並將它複製 tooyour 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="6733c-154">Select hello code snippet from hello window that appears and copy it tooyour clipboard.</span></span>
   
    ![存取程式碼][dataset-access-code]
5. <span data-ttu-id="6733c-156">Hello 程式碼貼到您本機的 Python 應用程式的 hello 筆記本。</span><span class="sxs-lookup"><span data-stu-id="6733c-156">Paste hello code into hello notebook of your local Python application.</span></span>
   
    ![筆記本][ipython-dataset]

## <span data-ttu-id="6733c-158"><a name="accessingIntermediateDatasets"></a>存取機器學習服務實驗中的中繼資料</span><span class="sxs-lookup"><span data-stu-id="6733c-158"><a name="accessingIntermediateDatasets"></a>Access intermediate datasets from Machine Learning experiments</span></span>
<span data-ttu-id="6733c-159">在 hello Machine Learning Studio 中執行實驗之後，就可能 tooaccess hello 中繼資料集從 hello 輸出節點的模組。</span><span class="sxs-lookup"><span data-stu-id="6733c-159">After an experiment is run in hello Machine Learning Studio, it is possible tooaccess hello intermediate datasets from hello output nodes of modules.</span></span> <span data-ttu-id="6733c-160">中繼資料集是指當模型工具執行時
為中繼步驟建立和使用的資料。</span><span class="sxs-lookup"><span data-stu-id="6733c-160">Intermediate datasets are data that has been created and used for intermediate steps when a model tool has been run.</span></span>

<span data-ttu-id="6733c-161">Hello 資料格式為 hello Python 用戶端程式庫相容時，可以存取中繼資料集。</span><span class="sxs-lookup"><span data-stu-id="6733c-161">Intermediate datasets can be accessed as long as hello data format is compatible with hello Python client library.</span></span>

<span data-ttu-id="6733c-162">hello 支援下列格式 (這些常數會在 hello`azureml.DataTypeIds`類別):</span><span class="sxs-lookup"><span data-stu-id="6733c-162">hello following formats are supported (constants for these are in hello `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="6733c-163">純文字</span><span class="sxs-lookup"><span data-stu-id="6733c-163">PlainText</span></span>
* <span data-ttu-id="6733c-164">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="6733c-164">GenericCSV</span></span>
* <span data-ttu-id="6733c-165">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="6733c-165">GenericTSV</span></span>
* <span data-ttu-id="6733c-166">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="6733c-166">GenericCSVNoHeader</span></span>
* <span data-ttu-id="6733c-167">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="6733c-167">GenericTSVNoHeader</span></span>

<span data-ttu-id="6733c-168">您可以判斷 hello 格式，將滑鼠游標停留在模組輸出節點。</span><span class="sxs-lookup"><span data-stu-id="6733c-168">You can determine hello format by hovering over a module output node.</span></span> <span data-ttu-id="6733c-169">它會顯示並以工具提示中的 hello 節點名稱。</span><span class="sxs-lookup"><span data-stu-id="6733c-169">It is displayed along with hello node name, in a tooltip.</span></span>

<span data-ttu-id="6733c-170">某些 hello 模組，例如 hello[分割][ split]模組，名為輸出 tooa 格式`Dataset`，hello Python 用戶端程式庫不支援的。</span><span class="sxs-lookup"><span data-stu-id="6733c-170">Some of hello modules, such as hello [Split][split] module, output tooa format named `Dataset`, which is not supported by hello Python client library.</span></span>

![資料集格式][dataset-format]

<span data-ttu-id="6733c-172">您需要 toouse 轉換模組，例如[轉換 tooCSV][convert-to-csv]，tooget 輸出成支援的格式。</span><span class="sxs-lookup"><span data-stu-id="6733c-172">You need toouse a conversion module, such as [Convert tooCSV][convert-to-csv], tooget an output into a supported format.</span></span>

![GenericCSV 格式][csv-format]

<span data-ttu-id="6733c-174">hello 下列步驟示範的範例會建立一個試驗、 執行及存取 hello 中繼資料集。</span><span class="sxs-lookup"><span data-stu-id="6733c-174">hello following steps show an example that creates an experiment, runs it and accesses hello intermediate dataset.</span></span>

1. <span data-ttu-id="6733c-175">建立新實驗。</span><span class="sxs-lookup"><span data-stu-id="6733c-175">Create a new experiment.</span></span>
2. <span data-ttu-id="6733c-176">插入 [成人收入普查二進位分類資料集]  模組。</span><span class="sxs-lookup"><span data-stu-id="6733c-176">Insert an **Adult Census Income Binary Classification dataset** module.</span></span>
3. <span data-ttu-id="6733c-177">插入[分割][ split]模組，並連接其輸入的 toohello 資料集模組輸出。</span><span class="sxs-lookup"><span data-stu-id="6733c-177">Insert a [Split][split] module, and connect its input toohello dataset module output.</span></span>
4. <span data-ttu-id="6733c-178">插入[轉換 tooCSV] [ convert-to-csv]模組，並連接的 hello 其輸入的 tooone[分割][ split]模組會輸出。</span><span class="sxs-lookup"><span data-stu-id="6733c-178">Insert a [Convert tooCSV][convert-to-csv] module and connect its input tooone of hello [Split][split] module outputs.</span></span>
5. <span data-ttu-id="6733c-179">儲存 hello 實驗中，執行並等候它 toofinish 執行。</span><span class="sxs-lookup"><span data-stu-id="6733c-179">Save hello experiment, run it, and wait for it toofinish running.</span></span>
6. <span data-ttu-id="6733c-180">按一下 hello 輸出節點上 hello[轉換 tooCSV] [ convert-to-csv]模組。</span><span class="sxs-lookup"><span data-stu-id="6733c-180">Click hello output node on hello [Convert tooCSV][convert-to-csv] module.</span></span>
7. <span data-ttu-id="6733c-181">Hello 操作功能表出現時，選取**產生的資料存取程式碼**。</span><span class="sxs-lookup"><span data-stu-id="6733c-181">When hello context menu appears, select **Generate Data Access Code**.</span></span>
   
    ![內容功能表][experiment]
8. <span data-ttu-id="6733c-183">選取 hello 程式碼片段，並將它從出現的 hello 視窗複製 tooyour 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="6733c-183">Select hello code snippet and copy it tooyour clipboard from hello window that appears.</span></span>
   
    ![存取程式碼][intermediate-dataset-access-code]
9. <span data-ttu-id="6733c-185">在筆記本中，貼上 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="6733c-185">Paste hello code in your notebook.</span></span>
   
    ![筆記本][ipython-intermediate-dataset]
10. <span data-ttu-id="6733c-187">您可以視覺化使用 matplotlib hello 資料。</span><span class="sxs-lookup"><span data-stu-id="6733c-187">You can visualize hello data using matplotlib.</span></span> <span data-ttu-id="6733c-188">這會顯示 hello age 資料行的長條圖中：</span><span class="sxs-lookup"><span data-stu-id="6733c-188">This displays in a histogram for hello age column:</span></span>
    
    ![長條圖][ipython-histogram]

## <span data-ttu-id="6733c-190"><a name="clientApis"></a>使用 hello Machine Learning python azure Python 用戶端程式庫 tooaccess、 讀取、 建立及管理資料集</span><span class="sxs-lookup"><span data-stu-id="6733c-190"><a name="clientApis"></a>Use hello Machine Learning Python client library tooaccess, read, create, and manage datasets</span></span>
### <a name="workspace"></a><span data-ttu-id="6733c-191">工作區</span><span class="sxs-lookup"><span data-stu-id="6733c-191">Workspace</span></span>
<span data-ttu-id="6733c-192">hello 工作區是 hello hello Python 用戶端程式庫的進入點。</span><span class="sxs-lookup"><span data-stu-id="6733c-192">hello workspace is hello entry point for hello Python client library.</span></span> <span data-ttu-id="6733c-193">提供 hello`Workspace`工作區識別碼和授權權杖 toocreate 類別執行個體：</span><span class="sxs-lookup"><span data-stu-id="6733c-193">Provide hello `Workspace` class with your workspace id and authorization token toocreate an instance:</span></span>

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a><span data-ttu-id="6733c-194">列舉資料集</span><span class="sxs-lookup"><span data-stu-id="6733c-194">Enumerate datasets</span></span>
<span data-ttu-id="6733c-195">tooenumerate 指定的工作區中的所有資料集：</span><span class="sxs-lookup"><span data-stu-id="6733c-195">tooenumerate all datasets in a given workspace:</span></span>

    for ds in ws.datasets:
        print(ds.name)

<span data-ttu-id="6733c-196">tooenumerate 只 hello 使用者建立資料集：</span><span class="sxs-lookup"><span data-stu-id="6733c-196">tooenumerate just hello user-created datasets:</span></span>

    for ds in ws.user_datasets:
        print(ds.name)

<span data-ttu-id="6733c-197">tooenumerate 只 hello 範例資料集：</span><span class="sxs-lookup"><span data-stu-id="6733c-197">tooenumerate just hello example datasets:</span></span>

    for ds in ws.example_datasets:
        print(ds.name)

<span data-ttu-id="6733c-198">您可以依名稱 (區分大小寫) 存取資料集：</span><span class="sxs-lookup"><span data-stu-id="6733c-198">You can access a dataset by name (which is case-sensitive):</span></span>

    ds = ws.datasets['my dataset name']

<span data-ttu-id="6733c-199">或您可以依索引來存取：</span><span class="sxs-lookup"><span data-stu-id="6733c-199">Or you can access it by index:</span></span>

    ds = ws.datasets[0]


### <a name="metadata"></a><span data-ttu-id="6733c-200">中繼資料</span><span class="sxs-lookup"><span data-stu-id="6733c-200">Metadata</span></span>
<span data-ttu-id="6733c-201">資料集有中繼資料，加法 toocontent 中。</span><span class="sxs-lookup"><span data-stu-id="6733c-201">Datasets have metadata, in addition toocontent.</span></span> <span data-ttu-id="6733c-202">（中繼資料集是例外狀況 toothis 規則和並沒有任何中繼資料）。</span><span class="sxs-lookup"><span data-stu-id="6733c-202">(Intermediate datasets are an exception toothis rule and do not have any metadata.)</span></span>

<span data-ttu-id="6733c-203">在建立時指派 hello 使用者一些中繼資料值：</span><span class="sxs-lookup"><span data-stu-id="6733c-203">Some metadata values are assigned by hello user at creation time:</span></span>

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

<span data-ttu-id="6733c-204">其他則是由 Azure ML 指派的值：</span><span class="sxs-lookup"><span data-stu-id="6733c-204">Others are values assigned by Azure ML:</span></span>

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

<span data-ttu-id="6733c-205">請參閱 hello`SourceDataset`多個在 hello 可用的中繼資料的類別。</span><span class="sxs-lookup"><span data-stu-id="6733c-205">See hello `SourceDataset` class for more on hello available metadata.</span></span>

### <a name="read-contents"></a><span data-ttu-id="6733c-206">讀取內容</span><span class="sxs-lookup"><span data-stu-id="6733c-206">Read contents</span></span>
<span data-ttu-id="6733c-207">hello 程式碼片段 Machine Learning Studio 所提供的自動下載並 hello 資料集 tooa 熊資料框架物件還原序列化。</span><span class="sxs-lookup"><span data-stu-id="6733c-207">hello code snippets provided by Machine Learning Studio automatically download and deserialize hello dataset tooa Pandas DataFrame object.</span></span> <span data-ttu-id="6733c-208">這是以 hello`to_dataframe`方法：</span><span class="sxs-lookup"><span data-stu-id="6733c-208">This is done with hello `to_dataframe` method:</span></span>

    frame = ds.to_dataframe()

<span data-ttu-id="6733c-209">如果您偏好 toodownload hello 未經處理資料，並自行執行 hello 還原序列化時，這是一個選項。</span><span class="sxs-lookup"><span data-stu-id="6733c-209">If you prefer toodownload hello raw data, and perform hello deserialization yourself, that is an option.</span></span> <span data-ttu-id="6733c-210">在 hello 的時刻，這是 hello 的格式，例如 'ARFF'，無法還原序列化的 hello Python 用戶端程式庫的唯一選項。</span><span class="sxs-lookup"><span data-stu-id="6733c-210">At hello moment, this is hello only option for formats such as 'ARFF', which hello Python client library cannot deserialize.</span></span>

<span data-ttu-id="6733c-211">以文字 tooread hello 內容：</span><span class="sxs-lookup"><span data-stu-id="6733c-211">tooread hello contents as text:</span></span>

    text_data = ds.read_as_text()

<span data-ttu-id="6733c-212">為二進位 tooread hello 內容：</span><span class="sxs-lookup"><span data-stu-id="6733c-212">tooread hello contents as binary:</span></span>

    binary_data = ds.read_as_binary()

<span data-ttu-id="6733c-213">您也可以開啟資料流 toohello 內容：</span><span class="sxs-lookup"><span data-stu-id="6733c-213">You can also just open a stream toohello contents:</span></span>

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a><span data-ttu-id="6733c-214">建立新的資料集</span><span class="sxs-lookup"><span data-stu-id="6733c-214">Create a new dataset</span></span>
<span data-ttu-id="6733c-215">hello Python 用戶端程式庫可讓您從您的 Python 程式 tooupload 資料集。</span><span class="sxs-lookup"><span data-stu-id="6733c-215">hello Python client library allows you tooupload datasets from your Python program.</span></span> <span data-ttu-id="6733c-216">這些資料集接著可在您的工作區中使用。</span><span class="sxs-lookup"><span data-stu-id="6733c-216">These datasets are then available for use in your workspace.</span></span>

<span data-ttu-id="6733c-217">如果您將資料熊資料框架中，使用下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="6733c-217">If you have your data in a Pandas DataFrame, use hello following code:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="6733c-218">如果您的資料已經序列化，則可以使用：</span><span class="sxs-lookup"><span data-stu-id="6733c-218">If your data is already serialized, you can use:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="6733c-219">hello Python 用戶端程式庫是無法 tooserialize 熊資料框架 toohello 下列格式 (這些常數會在 hello`azureml.DataTypeIds`類別):</span><span class="sxs-lookup"><span data-stu-id="6733c-219">hello Python client library is able tooserialize a Pandas DataFrame toohello following formats (constants for these are in hello `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="6733c-220">純文字</span><span class="sxs-lookup"><span data-stu-id="6733c-220">PlainText</span></span>
* <span data-ttu-id="6733c-221">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="6733c-221">GenericCSV</span></span>
* <span data-ttu-id="6733c-222">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="6733c-222">GenericTSV</span></span>
* <span data-ttu-id="6733c-223">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="6733c-223">GenericCSVNoHeader</span></span>
* <span data-ttu-id="6733c-224">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="6733c-224">GenericTSVNoHeader</span></span>

### <a name="update-an-existing-dataset"></a><span data-ttu-id="6733c-225">更新現有資料集</span><span class="sxs-lookup"><span data-stu-id="6733c-225">Update an existing dataset</span></span>
<span data-ttu-id="6733c-226">如果您嘗試 tooupload 新的資料集，以符合現有的資料集的名稱，您應該取得衝突錯誤。</span><span class="sxs-lookup"><span data-stu-id="6733c-226">If you try tooupload a new dataset with a name that matches an existing dataset, you should get a conflict error.</span></span>

<span data-ttu-id="6733c-227">tooupdate 現有的資料集，您必須先 tooget 參考 toohello 現有資料集：</span><span class="sxs-lookup"><span data-stu-id="6733c-227">tooupdate an existing dataset, you first need tooget a reference toohello existing dataset:</span></span>

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="6733c-228">然後使用`update_from_dataframe`hello Azure 上的資料集 tooserialize 和取代 hello 內容：</span><span class="sxs-lookup"><span data-stu-id="6733c-228">Then use `update_from_dataframe` tooserialize and replace hello contents of hello dataset on Azure:</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="6733c-229">如果您想 tooserialize hello 資料 tooa 不同格式時，指定選擇性的 hello 值`data_type_id`參數。</span><span class="sxs-lookup"><span data-stu-id="6733c-229">If you want tooserialize hello data tooa different format, specify a value for hello optional `data_type_id` parameter.</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="6733c-230">指定給 hello 的值，您可以選擇設定新的描述`description`參數。</span><span class="sxs-lookup"><span data-stu-id="6733c-230">You can optionally set a new description by specifying a value for hello `description` parameter.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toofeb 2015'

<span data-ttu-id="6733c-231">您可以選擇設定新的名稱所指定的值為 hello`name`參數。</span><span class="sxs-lookup"><span data-stu-id="6733c-231">You can optionally set a new name by specifying a value for hello `name` parameter.</span></span> <span data-ttu-id="6733c-232">從現在起，您會擷取 hello 資料集使用僅 hello 新名稱。</span><span class="sxs-lookup"><span data-stu-id="6733c-232">From now on, you'll retrieve hello dataset using hello new name only.</span></span> <span data-ttu-id="6733c-233">下列程式碼的 hello 更新 hello 資料、 名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="6733c-233">hello following code updates hello data, name and description.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up toofeb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

<span data-ttu-id="6733c-234">hello `data_type_id`，`name`和`description`參數為選擇性，預設 tootheir 先前的值。</span><span class="sxs-lookup"><span data-stu-id="6733c-234">hello `data_type_id`, `name` and `description` parameters are optional and default tootheir previous value.</span></span> <span data-ttu-id="6733c-235">hello`dataframe`參數永遠是必要項。</span><span class="sxs-lookup"><span data-stu-id="6733c-235">hello `dataframe` parameter is always required.</span></span>

<span data-ttu-id="6733c-236">如果您的資料已經序列化，請使用 `update_from_raw_data`，而不是 `update_from_dataframe`：</span><span class="sxs-lookup"><span data-stu-id="6733c-236">If your data is already serialized, use `update_from_raw_data` instead of `update_from_dataframe`.</span></span> <span data-ttu-id="6733c-237">如果您只傳入 `raw_data`，而不是 `dataframe`，其會以類似方式運作。</span><span class="sxs-lookup"><span data-stu-id="6733c-237">If you just pass in `raw_data` instead of  `dataframe`, it works in a similar way.</span></span>

<!-- Images -->
[security]:./media/machine-learning-python-data-access/security.png
[dataset-format]:./media/machine-learning-python-data-access/dataset-format.png
[csv-format]:./media/machine-learning-python-data-access/csv-format.png
[datasets]:./media/machine-learning-python-data-access/datasets.png
[dataset-access-code]:./media/machine-learning-python-data-access/dataset-access-code.png
[ipython-dataset]:./media/machine-learning-python-data-access/ipython-dataset.png
[experiment]:./media/machine-learning-python-data-access/experiment.png
[intermediate-dataset-access-code]:./media/machine-learning-python-data-access/intermediate-dataset-access-code.png
[ipython-intermediate-dataset]:./media/machine-learning-python-data-access/ipython-intermediate-dataset.png
[ipython-histogram]:./media/machine-learning-python-data-access/ipython-histogram.png


<!-- Module References -->
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

