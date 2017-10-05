---
title: "使用 Machine Learning Python 用戶端程式庫存取資料集 | Microsoft Docs"
description: "安裝並使用 Python 用戶端程式庫，從本機 Python 環境存取和管理 Azure Machine Learning 資料。"
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
ms.openlocfilehash: e3ae712e0f8d386f637520fbbff4b348bc86f32d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="access-datasets-with-python-using-the-azure-machine-learning-python-client-library"></a><span data-ttu-id="a12f3-103">使用 Azure Machine Learning Python 用戶端程式庫利用 Python 存取資料集</span><span class="sxs-lookup"><span data-stu-id="a12f3-103">Access datasets with Python using the Azure Machine Learning Python client library</span></span>
<span data-ttu-id="a12f3-104">Microsoft Azure Machine Learning Python 用戶端程式庫的預覽能夠從本機 Python 環境安全存取您的 Azure Machine Learning 資料集，並且可在工作區中建立和管理資料集。</span><span class="sxs-lookup"><span data-stu-id="a12f3-104">The preview of Microsoft Azure Machine Learning Python client library can enable secure access to your Azure Machine Learning datasets from a local Python environment and enables the creation and management of datasets in a workspace.</span></span>

<span data-ttu-id="a12f3-105">本主題提供如何執行以下作業的指示：</span><span class="sxs-lookup"><span data-stu-id="a12f3-105">This topic provides instructions on how to:</span></span>

* <span data-ttu-id="a12f3-106">安裝 Machine Learning Python 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="a12f3-106">install the Machine Learning Python client library</span></span> 
* <span data-ttu-id="a12f3-107">存取和上傳資料集，包括如何從本機 Python 環境取得授權以存取 Azure Machine Learning 資料集</span><span class="sxs-lookup"><span data-stu-id="a12f3-107">access and upload datasets, including instructions on how to get authorization to access Azure Machine Learning datasets from your local Python environment</span></span>
* <span data-ttu-id="a12f3-108">存取實驗中的中繼資料集</span><span class="sxs-lookup"><span data-stu-id="a12f3-108">access intermediate datasets from experiments</span></span>
* <span data-ttu-id="a12f3-109">使用 Python 用端程式庫列舉資料集、存取中繼資料、讀取資料集內容、建立新資料集以及更新現有資料集</span><span class="sxs-lookup"><span data-stu-id="a12f3-109">use the Python client library to enumerate datasets, access metadata, read the contents of a dataset, create new datasets and update existing datasets</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <span data-ttu-id="a12f3-110"><a name="prerequisites"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="a12f3-110"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="a12f3-111">Python 用戶端程式庫已在下列環境下經過測試：</span><span class="sxs-lookup"><span data-stu-id="a12f3-111">The Python client library has been tested under the following environments:</span></span>

* <span data-ttu-id="a12f3-112">Windows、Mac 及 Linux</span><span class="sxs-lookup"><span data-stu-id="a12f3-112">Windows, Mac and Linux</span></span>
* <span data-ttu-id="a12f3-113">Python 2.7、3.3 及 3.4</span><span class="sxs-lookup"><span data-stu-id="a12f3-113">Python 2.7, 3.3 and 3.4</span></span>

<span data-ttu-id="a12f3-114">對下列套件具相依性：</span><span class="sxs-lookup"><span data-stu-id="a12f3-114">It has a dependency on the following packages:</span></span>

* <span data-ttu-id="a12f3-115">requests</span><span class="sxs-lookup"><span data-stu-id="a12f3-115">requests</span></span>
* <span data-ttu-id="a12f3-116">python-dateutil</span><span class="sxs-lookup"><span data-stu-id="a12f3-116">python-dateutil</span></span>
* <span data-ttu-id="a12f3-117">pandas</span><span class="sxs-lookup"><span data-stu-id="a12f3-117">pandas</span></span>

<span data-ttu-id="a12f3-118">建議您使用 Python、IPython 隨附的 [Anaconda](http://continuum.io/downloads#all) 或 [Canopy](https://store.enthought.com/downloads/) 等 Python 發佈，並安裝上面列出的三個套件。</span><span class="sxs-lookup"><span data-stu-id="a12f3-118">We recommend using a Python distribution such as [Anaconda](http://continuum.io/downloads#all) or [Canopy](https://store.enthought.com/downloads/), which come with Python, IPython and the three packages listed above installed.</span></span> <span data-ttu-id="a12f3-119">雖然不一定需要 IPython，但它是以互動方式操作和虛擬化資料的絕佳環境。</span><span class="sxs-lookup"><span data-stu-id="a12f3-119">Although IPython is not strictly required, it is a great environment for manipulating and visualizing data interactively.</span></span>

### <span data-ttu-id="a12f3-120"><a name="installation"></a>如何安裝 Azure Machine Learning Python 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="a12f3-120"><a name="installation"></a>How to install the Azure Machine Learning Python client library</span></span>
<span data-ttu-id="a12f3-121">務必要安裝 Azure Machine Learning Python 用戶端程式庫，才能完成本主題概述的工作。</span><span class="sxs-lookup"><span data-stu-id="a12f3-121">The Azure Machine Learning Python client library must also be installed to complete the tasks outlined in this topic.</span></span> <span data-ttu-id="a12f3-122">您可以從 [Python 套件索引](https://pypi.python.org/pypi/azureml)取得。</span><span class="sxs-lookup"><span data-stu-id="a12f3-122">It is available from the [Python Package Index](https://pypi.python.org/pypi/azureml).</span></span> <span data-ttu-id="a12f3-123">若要在 Python 環境中安裝它，請從本機 Python 環境執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="a12f3-123">To install it in your Python environment, run the following command from your local Python environment:</span></span>

    pip install azureml

<span data-ttu-id="a12f3-124">或者，您可以從 [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python)上的來源下載和安裝。</span><span class="sxs-lookup"><span data-stu-id="a12f3-124">Alternatively, you can download and install from the sources on [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span></span>

    python setup.py install

<span data-ttu-id="a12f3-125">如果必須在您的電腦上安裝 git，您可以使用 PIP 從 git 儲存機制直接安裝：</span><span class="sxs-lookup"><span data-stu-id="a12f3-125">If you have git installed on your machine, you can use pip to install directly from the git repository:</span></span>

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <span data-ttu-id="a12f3-126"><a name="datasetAccess"></a>使用Studio 程式碼片段存取資料集</span><span class="sxs-lookup"><span data-stu-id="a12f3-126"><a name="datasetAccess"></a>Use Studio Code snippets to access datasets</span></span>
<span data-ttu-id="a12f3-127">Python 用戶端程式庫讓您以程式設計方式存取執行實驗所得的現有資料集。</span><span class="sxs-lookup"><span data-stu-id="a12f3-127">The Python client library gives you programmatic access to your existing datasets from experiments that have been run.</span></span>

<span data-ttu-id="a12f3-128">您可以從 Studio Web 介面，產生包含所有必要資訊的程式碼片段，以下載資料集並和還原序列化為您位置電腦的 Pandas DataFrame 物件。</span><span class="sxs-lookup"><span data-stu-id="a12f3-128">From the Studio web interface, you can generate code snippets that include all the necessary information to download and deserialize datasets as Pandas DataFrame objects on your location machine.</span></span>

### <span data-ttu-id="a12f3-129"><a name="security"></a>資料存取安全性</span><span class="sxs-lookup"><span data-stu-id="a12f3-129"><a name="security"></a>Security for data access</span></span>
<span data-ttu-id="a12f3-130">Studio 所提供可與 Python 用戶端程式碼搭配使用的程式碼片段包括工作區識別碼與授權權杖。</span><span class="sxs-lookup"><span data-stu-id="a12f3-130">The code snippets provided by Studio for use with the Python client library includes your workspace id and authorization token.</span></span> <span data-ttu-id="a12f3-131">這些項目可提供工作區的完整存取權，且務必加以保護，像是密碼。</span><span class="sxs-lookup"><span data-stu-id="a12f3-131">These provide full access to your workspace and must be protected, like a password.</span></span>

<span data-ttu-id="a12f3-132">基於安全性理由，程式碼片段功能只提供給其角色設定為工作區「擁有者」  的使用者。</span><span class="sxs-lookup"><span data-stu-id="a12f3-132">For security reasons, the code snippet functionality is only available to users that have their role set as **Owner** for the workspace.</span></span> <span data-ttu-id="a12f3-133">您的角色會在 Azure Machine Learning Studio 中，顯示於 [設定] 的 [使用者] 頁面上。</span><span class="sxs-lookup"><span data-stu-id="a12f3-133">Your role is displayed in Azure Machine Learning Studio on the **USERS** page under **Settings**.</span></span>

![安全性][security]

<span data-ttu-id="a12f3-135">如果您的角色未設定為 [擁有者] ，您可以要求重新受邀為擁有者，或要求該工作區的擁有者將程式碼片段提供給您。</span><span class="sxs-lookup"><span data-stu-id="a12f3-135">If your role is not set as **Owner**, you can either request to be reinvited as an owner, or ask the owner of the workspace to provide you with the code snippet.</span></span>

<span data-ttu-id="a12f3-136">若要取得授權權杖，您可以執行下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="a12f3-136">To obtain the authorization token, you can do one of the following:</span></span>

* <span data-ttu-id="a12f3-137">向擁有者要求權杖。</span><span class="sxs-lookup"><span data-stu-id="a12f3-137">Ask for a token from an owner.</span></span> <span data-ttu-id="a12f3-138">擁有者能夠在 Studio 中，從他們工作區的 [設定] 頁面存取其授權權杖。</span><span class="sxs-lookup"><span data-stu-id="a12f3-138">Owners can access their authorization tokens from the Settings page of their workspace in Studio.</span></span> <span data-ttu-id="a12f3-139">選取左窗格中的 [設定]，然後按一下 [授權權杖]，即可看到主要與次要權杖。</span><span class="sxs-lookup"><span data-stu-id="a12f3-139">Select **Settings** from the left pane and click **AUTHORIZATION TOKENS** to see the primary and secondary tokens.</span></span>  <span data-ttu-id="a12f3-140">雖然主要或次要授權權杖都能用於程式碼片段，但建議擁有者只共用次要授權權杖。</span><span class="sxs-lookup"><span data-stu-id="a12f3-140">Although either the primary or the secondary authorization tokens can be used in the code snippet, it is recommended that owners only share the secondary authorization tokens.</span></span>

![授權權杖](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* <span data-ttu-id="a12f3-142">要求升級成擁有者角色。</span><span class="sxs-lookup"><span data-stu-id="a12f3-142">Ask to be promoted to role of owner.</span></span>  <span data-ttu-id="a12f3-143">若要這樣做，工作區目前的擁有者必須先將您從工作區中移除，再重新邀請您成為其擁有者。</span><span class="sxs-lookup"><span data-stu-id="a12f3-143">To do this, a current owner of the workspace needs to first remove you from the workspace then re-invite you to it as an owner.</span></span>

<span data-ttu-id="a12f3-144">開發人員一旦取得工作區識別碼與授權權杖，無論其角色為何，都能夠使用程式碼片段存取該工作區。</span><span class="sxs-lookup"><span data-stu-id="a12f3-144">Once developers have obtained the workspace id and authorization token, they are able to access the workspace using the code snippet regardless of their role.</span></span>

<span data-ttu-id="a12f3-145">授權權杖可以在 [設定] 下的 [授權權杖] 頁面上管理。</span><span class="sxs-lookup"><span data-stu-id="a12f3-145">Authorization tokens are managed on the **AUTHORIZATION TOKENS** page under **SETTINGS**.</span></span> <span data-ttu-id="a12f3-146">您可以重新產生權杖，但這個程序會撤銷上一個權杖的存取權。</span><span class="sxs-lookup"><span data-stu-id="a12f3-146">You can regenerate them, but this procedure revokes access to the previous token.</span></span>

### <span data-ttu-id="a12f3-147"><a name="accessingDatasets"></a>從本機 Python 應用程式存取資料集</span><span class="sxs-lookup"><span data-stu-id="a12f3-147"><a name="accessingDatasets"></a>Access datasets from a local Python application</span></span>
1. <span data-ttu-id="a12f3-148">在 Machine Learning Studio 的左邊導覽列中，按一下 [資料集]  。</span><span class="sxs-lookup"><span data-stu-id="a12f3-148">In Machine Learning Studio, click **DATASETS** in the navigation bar on the left.</span></span>
2. <span data-ttu-id="a12f3-149">選取您想要存取的資料集。</span><span class="sxs-lookup"><span data-stu-id="a12f3-149">Select the dataset you would like to access.</span></span> <span data-ttu-id="a12f3-150">您可以從 [範例] 清單的 [我的資料集] 清單中，選擇任何資料集。</span><span class="sxs-lookup"><span data-stu-id="a12f3-150">You can select any of the datasets from the **MY DATASETS** list or from the **SAMPLES** list.</span></span>
3. <span data-ttu-id="a12f3-151">按一下底部工具列上的 [產生資料存取程式碼] 。</span><span class="sxs-lookup"><span data-stu-id="a12f3-151">From the bottom toolbar, click **Generate Data Access Code**.</span></span> <span data-ttu-id="a12f3-152">如果資料格式與 Python 用戶端程式的不相容，就會停用這個按鈕。</span><span class="sxs-lookup"><span data-stu-id="a12f3-152">If the data is in a format incompatible with the Python client library, this button is disabled.</span></span>
   
    ![資料集][datasets]
4. <span data-ttu-id="a12f3-154">從出現的視窗中選取程式碼片段，然後複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="a12f3-154">Select the code snippet from the window that appears and copy it to your clipboard.</span></span>
   
    ![存取程式碼][dataset-access-code]
5. <span data-ttu-id="a12f3-156">將程式碼貼入本機 Python 應用程式的筆記本。</span><span class="sxs-lookup"><span data-stu-id="a12f3-156">Paste the code into the notebook of your local Python application.</span></span>
   
    ![筆記本][ipython-dataset]

## <span data-ttu-id="a12f3-158"><a name="accessingIntermediateDatasets"></a>存取機器學習服務實驗中的中繼資料</span><span class="sxs-lookup"><span data-stu-id="a12f3-158"><a name="accessingIntermediateDatasets"></a>Access intermediate datasets from Machine Learning experiments</span></span>
<span data-ttu-id="a12f3-159">在 Machine Learning Studio 中進行實驗後，您能夠從模組的輸出節點存取中繼資料集。</span><span class="sxs-lookup"><span data-stu-id="a12f3-159">After an experiment is run in the Machine Learning Studio, it is possible to access the intermediate datasets from the output nodes of modules.</span></span> <span data-ttu-id="a12f3-160">中繼資料集是指當模型工具執行時
為中繼步驟建立和使用的資料。</span><span class="sxs-lookup"><span data-stu-id="a12f3-160">Intermediate datasets are data that has been created and used for intermediate steps when a model tool has been run.</span></span>

<span data-ttu-id="a12f3-161">只要其資料格式能與 Python 用戶端程式庫相容，就能夠存取中繼資料集。</span><span class="sxs-lookup"><span data-stu-id="a12f3-161">Intermediate datasets can be accessed as long as the data format is compatible with the Python client library.</span></span>

<span data-ttu-id="a12f3-162">以下是支援的格式 (這些都是 `azureml.DataTypeIds` 類別的常數)：</span><span class="sxs-lookup"><span data-stu-id="a12f3-162">The following formats are supported (constants for these are in the `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="a12f3-163">純文字</span><span class="sxs-lookup"><span data-stu-id="a12f3-163">PlainText</span></span>
* <span data-ttu-id="a12f3-164">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="a12f3-164">GenericCSV</span></span>
* <span data-ttu-id="a12f3-165">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="a12f3-165">GenericTSV</span></span>
* <span data-ttu-id="a12f3-166">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="a12f3-166">GenericCSVNoHeader</span></span>
* <span data-ttu-id="a12f3-167">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="a12f3-167">GenericTSVNoHeader</span></span>

<span data-ttu-id="a12f3-168">您可以將滑鼠停留在模組輸出節點上方來判斷其格式。</span><span class="sxs-lookup"><span data-stu-id="a12f3-168">You can determine the format by hovering over a module output node.</span></span> <span data-ttu-id="a12f3-169">其會與節點名稱一同顯示在工具提示中。</span><span class="sxs-lookup"><span data-stu-id="a12f3-169">It is displayed along with the node name, in a tooltip.</span></span>

<span data-ttu-id="a12f3-170">有些模組 (例如[分割][split]模組) 輸出的格式稱為 `Dataset`，但 Python 用戶端程式碼不支援這種格式。</span><span class="sxs-lookup"><span data-stu-id="a12f3-170">Some of the modules, such as the [Split][split] module, output to a format named `Dataset`, which is not supported by the Python client library.</span></span>

![資料集格式][dataset-format]

<span data-ttu-id="a12f3-172">您必須使用轉換模組 (例如，[轉換成 CSV][convert-to-csv])，才能將輸出變成支援的格式。</span><span class="sxs-lookup"><span data-stu-id="a12f3-172">You need to use a conversion module, such as [Convert to CSV][convert-to-csv], to get an output into a supported format.</span></span>

![GenericCSV 格式][csv-format]

<span data-ttu-id="a12f3-174">下列步驟示範說明建立實驗、加以執行，然後群組中繼資料集。</span><span class="sxs-lookup"><span data-stu-id="a12f3-174">The following steps show an example that creates an experiment, runs it and accesses the intermediate dataset.</span></span>

1. <span data-ttu-id="a12f3-175">建立新實驗。</span><span class="sxs-lookup"><span data-stu-id="a12f3-175">Create a new experiment.</span></span>
2. <span data-ttu-id="a12f3-176">插入 [成人收入普查二進位分類資料集]  模組。</span><span class="sxs-lookup"><span data-stu-id="a12f3-176">Insert an **Adult Census Income Binary Classification dataset** module.</span></span>
3. <span data-ttu-id="a12f3-177">插入[分割][split]模組，然後將其輸入連接至資料集模組輸出。</span><span class="sxs-lookup"><span data-stu-id="a12f3-177">Insert a [Split][split] module, and connect its input to the dataset module output.</span></span>
4. <span data-ttu-id="a12f3-178">插入[轉換成 CSV][convert-to-csv] 模組，然後將其輸入連接至其中一個[分割][split]模組輸出。</span><span class="sxs-lookup"><span data-stu-id="a12f3-178">Insert a [Convert to CSV][convert-to-csv] module and connect its input to one of the [Split][split] module outputs.</span></span>
5. <span data-ttu-id="a12f3-179">儲存此實驗、加以執行，然後等待執行完成。</span><span class="sxs-lookup"><span data-stu-id="a12f3-179">Save the experiment, run it, and wait for it to finish running.</span></span>
6. <span data-ttu-id="a12f3-180">按一下 [轉換成 CSV 模組][convert-to-csv] 上的輸出節點。</span><span class="sxs-lookup"><span data-stu-id="a12f3-180">Click the output node on the [Convert to CSV][convert-to-csv] module.</span></span>
7. <span data-ttu-id="a12f3-181">在隨即出現內容功能表，選取 [產生資料存取程式碼]。</span><span class="sxs-lookup"><span data-stu-id="a12f3-181">When the context menu appears, select **Generate Data Access Code**.</span></span>
   
    ![內容功能表][experiment]
8. <span data-ttu-id="a12f3-183">選取程式碼片段，然後從出現的視窗中將它複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="a12f3-183">Select the code snippet and copy it to your clipboard from the window that appears.</span></span>
   
    ![存取程式碼][intermediate-dataset-access-code]
9. <span data-ttu-id="a12f3-185">將程式碼貼入筆記本。</span><span class="sxs-lookup"><span data-stu-id="a12f3-185">Paste the code in your notebook.</span></span>
   
    ![筆記本][ipython-intermediate-dataset]
10. <span data-ttu-id="a12f3-187">您可以使用 matplotlib 將資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="a12f3-187">You can visualize the data using matplotlib.</span></span> <span data-ttu-id="a12f3-188">這樣會以長條圖顯示年齡欄：</span><span class="sxs-lookup"><span data-stu-id="a12f3-188">This displays in a histogram for the age column:</span></span>
    
    ![長條圖][ipython-histogram]

## <span data-ttu-id="a12f3-190"><a name="clientApis"></a>使用 Machine Learning Python 用戶端程式碼來存取、讀取、建立及管理資料集</span><span class="sxs-lookup"><span data-stu-id="a12f3-190"><a name="clientApis"></a>Use the Machine Learning Python client library to access, read, create, and manage datasets</span></span>
### <a name="workspace"></a><span data-ttu-id="a12f3-191">工作區</span><span class="sxs-lookup"><span data-stu-id="a12f3-191">Workspace</span></span>
<span data-ttu-id="a12f3-192">工作區是 Python 用戶端程式碼的進入點。</span><span class="sxs-lookup"><span data-stu-id="a12f3-192">The workspace is the entry point for the Python client library.</span></span> <span data-ttu-id="a12f3-193">將您的工作區識別碼與授權權杖提供給 `Workspace` 類別，就會建立一個執行個體：</span><span class="sxs-lookup"><span data-stu-id="a12f3-193">Provide the `Workspace` class with your workspace id and authorization token to create an instance:</span></span>

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a><span data-ttu-id="a12f3-194">列舉資料集</span><span class="sxs-lookup"><span data-stu-id="a12f3-194">Enumerate datasets</span></span>
<span data-ttu-id="a12f3-195">若要列舉指定工作區中的所有資料集：</span><span class="sxs-lookup"><span data-stu-id="a12f3-195">To enumerate all datasets in a given workspace:</span></span>

    for ds in ws.datasets:
        print(ds.name)

<span data-ttu-id="a12f3-196">若只要列舉使用者建立的資料集：</span><span class="sxs-lookup"><span data-stu-id="a12f3-196">To enumerate just the user-created datasets:</span></span>

    for ds in ws.user_datasets:
        print(ds.name)

<span data-ttu-id="a12f3-197">若只要列舉範例資料集：</span><span class="sxs-lookup"><span data-stu-id="a12f3-197">To enumerate just the example datasets:</span></span>

    for ds in ws.example_datasets:
        print(ds.name)

<span data-ttu-id="a12f3-198">您可以依名稱 (區分大小寫) 存取資料集：</span><span class="sxs-lookup"><span data-stu-id="a12f3-198">You can access a dataset by name (which is case-sensitive):</span></span>

    ds = ws.datasets['my dataset name']

<span data-ttu-id="a12f3-199">或您可以依索引來存取：</span><span class="sxs-lookup"><span data-stu-id="a12f3-199">Or you can access it by index:</span></span>

    ds = ws.datasets[0]


### <a name="metadata"></a><span data-ttu-id="a12f3-200">中繼資料</span><span class="sxs-lookup"><span data-stu-id="a12f3-200">Metadata</span></span>
<span data-ttu-id="a12f3-201">除了內容，資料集還有中繼資料。</span><span class="sxs-lookup"><span data-stu-id="a12f3-201">Datasets have metadata, in addition to content.</span></span> <span data-ttu-id="a12f3-202">(中繼資料集是這個規則的例外，而且沒有任何中繼資料)。</span><span class="sxs-lookup"><span data-stu-id="a12f3-202">(Intermediate datasets are an exception to this rule and do not have any metadata.)</span></span>

<span data-ttu-id="a12f3-203">有些中繼資料值是由使用者在建立時指派：</span><span class="sxs-lookup"><span data-stu-id="a12f3-203">Some metadata values are assigned by the user at creation time:</span></span>

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

<span data-ttu-id="a12f3-204">其他則是由 Azure ML 指派的值：</span><span class="sxs-lookup"><span data-stu-id="a12f3-204">Others are values assigned by Azure ML:</span></span>

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

<span data-ttu-id="a12f3-205">如需可用中繼資料的詳細資訊，請參閱 `SourceDataset` 類別。</span><span class="sxs-lookup"><span data-stu-id="a12f3-205">See the `SourceDataset` class for more on the available metadata.</span></span>

### <a name="read-contents"></a><span data-ttu-id="a12f3-206">讀取內容</span><span class="sxs-lookup"><span data-stu-id="a12f3-206">Read contents</span></span>
<span data-ttu-id="a12f3-207">Machine Learning Studio 提供的程式碼片段會自動下載並將資料集還原序列化為 Pandas DataFrame 物件。</span><span class="sxs-lookup"><span data-stu-id="a12f3-207">The code snippets provided by Machine Learning Studio automatically download and deserialize the dataset to a Pandas DataFrame object.</span></span> <span data-ttu-id="a12f3-208">此動作可用 `to_dataframe` 方法來完成：</span><span class="sxs-lookup"><span data-stu-id="a12f3-208">This is done with the `to_dataframe` method:</span></span>

    frame = ds.to_dataframe()

<span data-ttu-id="a12f3-209">您也可以選擇下載原始資料，並自己執行還原序列化。</span><span class="sxs-lookup"><span data-stu-id="a12f3-209">If you prefer to download the raw data, and perform the deserialization yourself, that is an option.</span></span> <span data-ttu-id="a12f3-210">對於 Python 用戶端程式庫無法還原序列化的格式 (例如 'ARFF')，目前這是唯一選擇。</span><span class="sxs-lookup"><span data-stu-id="a12f3-210">At the moment, this is the only option for formats such as 'ARFF', which the Python client library cannot deserialize.</span></span>

<span data-ttu-id="a12f3-211">若要以文字格式讀取內容：</span><span class="sxs-lookup"><span data-stu-id="a12f3-211">To read the contents as text:</span></span>

    text_data = ds.read_as_text()

<span data-ttu-id="a12f3-212">若要以二進位格式讀取內容：</span><span class="sxs-lookup"><span data-stu-id="a12f3-212">To read the contents as binary:</span></span>

    binary_data = ds.read_as_binary()

<span data-ttu-id="a12f3-213">您也可以開啟內容的資料流：</span><span class="sxs-lookup"><span data-stu-id="a12f3-213">You can also just open a stream to the contents:</span></span>

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a><span data-ttu-id="a12f3-214">建立新的資料集</span><span class="sxs-lookup"><span data-stu-id="a12f3-214">Create a new dataset</span></span>
<span data-ttu-id="a12f3-215">Python 用戶端程式碼可讓您上傳 Python 程式中的資料集。</span><span class="sxs-lookup"><span data-stu-id="a12f3-215">The Python client library allows you to upload datasets from your Python program.</span></span> <span data-ttu-id="a12f3-216">這些資料集接著可在您的工作區中使用。</span><span class="sxs-lookup"><span data-stu-id="a12f3-216">These datasets are then available for use in your workspace.</span></span>

<span data-ttu-id="a12f3-217">如果您有資料在 Pandas DataFrame 中，可以使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="a12f3-217">If you have your data in a Pandas DataFrame, use the following code:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="a12f3-218">如果您的資料已經序列化，則可以使用：</span><span class="sxs-lookup"><span data-stu-id="a12f3-218">If your data is already serialized, you can use:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="a12f3-219">Python 用戶端程式碼能夠將 Pandas DataFrame 序列化為下列格式 (這些都是 `azureml.DataTypeIds` 類別的常數)：</span><span class="sxs-lookup"><span data-stu-id="a12f3-219">The Python client library is able to serialize a Pandas DataFrame to the following formats (constants for these are in the `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="a12f3-220">純文字</span><span class="sxs-lookup"><span data-stu-id="a12f3-220">PlainText</span></span>
* <span data-ttu-id="a12f3-221">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="a12f3-221">GenericCSV</span></span>
* <span data-ttu-id="a12f3-222">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="a12f3-222">GenericTSV</span></span>
* <span data-ttu-id="a12f3-223">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="a12f3-223">GenericCSVNoHeader</span></span>
* <span data-ttu-id="a12f3-224">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="a12f3-224">GenericTSVNoHeader</span></span>

### <a name="update-an-existing-dataset"></a><span data-ttu-id="a12f3-225">更新現有資料集</span><span class="sxs-lookup"><span data-stu-id="a12f3-225">Update an existing dataset</span></span>
<span data-ttu-id="a12f3-226">如果您嘗試以與現有資料集相符的名稱上傳新的資料集，應會發生衝突錯誤。</span><span class="sxs-lookup"><span data-stu-id="a12f3-226">If you try to upload a new dataset with a name that matches an existing dataset, you should get a conflict error.</span></span>

<span data-ttu-id="a12f3-227">若要更新現有資料集，您必須先取得現有資料集的參照：</span><span class="sxs-lookup"><span data-stu-id="a12f3-227">To update an existing dataset, you first need to get a reference to the existing dataset:</span></span>

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="a12f3-228">然後使用 `update_from_dataframe` 以序列化並取代 Azure 上資料集的內容：</span><span class="sxs-lookup"><span data-stu-id="a12f3-228">Then use `update_from_dataframe` to serialize and replace the contents of the dataset on Azure:</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="a12f3-229">如果您想要將資料序列化為不同的格式，可為選擇性 `data_type_id` 參數指定一個值。</span><span class="sxs-lookup"><span data-stu-id="a12f3-229">If you want to serialize the data to a different format, specify a value for the optional `data_type_id` parameter.</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="a12f3-230">您可以選擇性地為 `description` 參數指定一個值，以設定新的描述。</span><span class="sxs-lookup"><span data-stu-id="a12f3-230">You can optionally set a new description by specifying a value for the `description` parameter.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up to feb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to feb 2015'

<span data-ttu-id="a12f3-231">您可以選擇性地為 `name` 參數指定一個值，以設定新的名稱。</span><span class="sxs-lookup"><span data-stu-id="a12f3-231">You can optionally set a new name by specifying a value for the `name` parameter.</span></span> <span data-ttu-id="a12f3-232">從現在起，您只會擷取使用新名稱的資料集。</span><span class="sxs-lookup"><span data-stu-id="a12f3-232">From now on, you'll retrieve the dataset using the new name only.</span></span> <span data-ttu-id="a12f3-233">下列程式碼可更新資料、名稱及描述。</span><span class="sxs-lookup"><span data-stu-id="a12f3-233">The following code updates the data, name and description.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up to feb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up to feb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

<span data-ttu-id="a12f3-234">`data_type_id`、`name` 及 `description` 都是選擇性參數，並以先前的值為預設值。</span><span class="sxs-lookup"><span data-stu-id="a12f3-234">The `data_type_id`, `name` and `description` parameters are optional and default to their previous value.</span></span> <span data-ttu-id="a12f3-235">`dataframe` 一向是必要參數。</span><span class="sxs-lookup"><span data-stu-id="a12f3-235">The `dataframe` parameter is always required.</span></span>

<span data-ttu-id="a12f3-236">如果您的資料已經序列化，請使用 `update_from_raw_data`，而不是 `update_from_dataframe`：</span><span class="sxs-lookup"><span data-stu-id="a12f3-236">If your data is already serialized, use `update_from_raw_data` instead of `update_from_dataframe`.</span></span> <span data-ttu-id="a12f3-237">如果您只傳入 `raw_data`，而不是 `dataframe`，其會以類似方式運作。</span><span class="sxs-lookup"><span data-stu-id="a12f3-237">If you just pass in `raw_data` instead of  `dataframe`, it works in a similar way.</span></span>

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

