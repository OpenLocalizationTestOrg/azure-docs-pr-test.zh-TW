---
title: "什麼是 Azure Machine Learning Studio？ | Microsoft Docs"
description: "從已準備就緒可供使用之演算法與模組的程式庫快速建置模型的拖放工具 - Azure ML Studio 概觀。"
keywords: azure machine learning,azure ml, ml studio
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e65c8fe1-7991-4a2a-86ef-fd80a7a06269
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 70a1d0acb8ec9bbb591f696281ea5e975b443a15
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-azure-machine-learning-studio"></a><span data-ttu-id="98cf2-105">什麼是 Azure Machine Learning Studio？</span><span class="sxs-lookup"><span data-stu-id="98cf2-105">What is Azure Machine Learning Studio?</span></span>
<span data-ttu-id="98cf2-106">Microsoft Azure Machine Learning Studio 是共同作業式的拖放工具，您可以用來依據您的資料建置、測試及部署預測分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="98cf2-106">Microsoft Azure Machine Learning Studio is a collaborative, drag-and-drop tool you can use to build, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="98cf2-107">Machine Learning Studio 會以 Web 服務方式發佈模型，讓自訂應用程式或 BI 工具 (例如 Excel) 都能夠很容易地使用。</span><span class="sxs-lookup"><span data-stu-id="98cf2-107">Machine Learning Studio publishes models as web services that can easily be consumed by custom apps or BI tools such as Excel.</span></span>

<span data-ttu-id="98cf2-108">Machine Learning Studio 讓資料科學、預測分析、雲端資源和您的資料齊聚一堂！</span><span class="sxs-lookup"><span data-stu-id="98cf2-108">Machine Learning Studio is where data science, predictive analytics, cloud resources, and your data meet.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="the-machine-learning-studio-interactive-workspace"></a><span data-ttu-id="98cf2-109">Machine Learning Studio 互動式工作區</span><span class="sxs-lookup"><span data-stu-id="98cf2-109">The Machine Learning Studio interactive workspace</span></span>
<span data-ttu-id="98cf2-110">若要開發預測分析模型，您通常會使用一或多個來源的資料，透過各種資料操作和統計函數來轉換和分析該資料，然後產生一組結果。</span><span class="sxs-lookup"><span data-stu-id="98cf2-110">To develop a predictive analysis model, you typically use data from one or more sources, transform and analyze that data through various data manipulation and statistical functions, and generate a set of results.</span></span> <span data-ttu-id="98cf2-111">開發此類模型是一種反覆式過程。</span><span class="sxs-lookup"><span data-stu-id="98cf2-111">Developing a model like this is an iterative process.</span></span> <span data-ttu-id="98cf2-112">隨著您修改各種函數及其參數，結果會不斷收斂，直到您對已訓練的有效模型感到滿意為止。</span><span class="sxs-lookup"><span data-stu-id="98cf2-112">As you modify the various functions and their parameters, your results converge until you are satisfied that you have a trained, effective model.</span></span>

<span data-ttu-id="98cf2-113">**Azure Machine Learning Studio** 提供互動式的視覺化工作區，讓您輕鬆建置、測試和反覆運算預測分析模型。</span><span class="sxs-lookup"><span data-stu-id="98cf2-113">**Azure Machine Learning Studio** gives you an interactive, visual workspace to easily build, test, and iterate on a predictive analysis model.</span></span> <span data-ttu-id="98cf2-114">您可以將「資料集」和分析「模組」拖放到互動式畫布，將它們連接在一起以構成「實驗」，然後在 Machine Learning Studio 中執行。</span><span class="sxs-lookup"><span data-stu-id="98cf2-114">You drag-and-drop ***datasets*** and analysis ***modules*** onto an interactive canvas, connecting them together to form an ***experiment***, which you run in Machine Learning Studio.</span></span> <span data-ttu-id="98cf2-115">若要反覆調整模型設計，請編輯實驗，儲存複本 (若需要)，然後重新提交。</span><span class="sxs-lookup"><span data-stu-id="98cf2-115">To iterate on your model design, you edit the experiment, save a copy if desired, and run it again.</span></span> <span data-ttu-id="98cf2-116">當您準備好時，可以將您的「訓練實驗」轉換成「預測實驗」，然後發佈為「Web 服務」，讓其他人可以存取您的模型。</span><span class="sxs-lookup"><span data-stu-id="98cf2-116">When you're ready, you can convert your ***training experiment*** to a ***predictive experiment***, and then publish it as a ***web service*** so that your model can be accessed by others.</span></span>

<span data-ttu-id="98cf2-117">不需要設計程式，只要在視覺上連接資料集和模組，即可建構預測分析模型。</span><span class="sxs-lookup"><span data-stu-id="98cf2-117">There is no programming required, just visually connecting datasets and modules to construct your predictive analysis model.</span></span>

> [!TIP]
> <span data-ttu-id="98cf2-118">若要下載並列印提供 Machine Learning Studio 功能概觀的圖表，請參閱 [Azure Machine Learning Studio 功能的概觀圖](machine-learning-studio-overview-diagram.md)。</span><span class="sxs-lookup"><span data-stu-id="98cf2-118">To download and print a diagram that gives an overview of the capabilities of Machine Learning Studio, see [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
> 
> 

![Azure ML Studio 圖表：建立實驗、讀取許多來源的資料、寫入評分的資料及寫入模型。][ml-studio-overview]

## <a name="get-started-with-machine-learning-studio"></a><span data-ttu-id="98cf2-120">開始使用 Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="98cf2-120">Get started with Machine Learning Studio</span></span>
<span data-ttu-id="98cf2-121">第一次進入 [Machine Learning Studio](https://studio.azureml.net) 時，您會看到 [首頁]。</span><span class="sxs-lookup"><span data-stu-id="98cf2-121">When you first enter [Machine Learning Studio](https://studio.azureml.net) you see the **Home** page.</span></span> <span data-ttu-id="98cf2-122">您可以從這裡檢視文件、影片、網路研討會，以及尋找其他重要資源。</span><span class="sxs-lookup"><span data-stu-id="98cf2-122">From here you can view documentation, videos, webinars, and find other valuable resources.</span></span>

<span data-ttu-id="98cf2-123">按一下左上方的功能表</span><span class="sxs-lookup"><span data-stu-id="98cf2-123">Click the upper-left menu</span></span> ![功能表](media/machine-learning-what-is-ml-studio/menu.png) <span data-ttu-id="98cf2-125">您會看到幾個選項。</span><span class="sxs-lookup"><span data-stu-id="98cf2-125">and you'll see several options.</span></span>

### <a name="cortana-intelligence"></a><span data-ttu-id="98cf2-126">Cortana Intelligence</span><span class="sxs-lookup"><span data-stu-id="98cf2-126">Cortana Intelligence</span></span>
<span data-ttu-id="98cf2-127">按一下 [Cortana Intelligence]，系統會帶您前往 [Cortana Intelligence Suite](https://www.microsoft.com/cloud-platform/cortana-intelligence-suite)的首頁。</span><span class="sxs-lookup"><span data-stu-id="98cf2-127">Click **Cortana Intelligence** and you'll be taken to the home page of the [Cortana Intelligence Suite](https://www.microsoft.com/cloud-platform/cortana-intelligence-suite).</span></span> <span data-ttu-id="98cf2-128">Cortana Intelligence Suite 是受完整管理的巨量資料與進階分析套件，可將資料轉換成可採取的智慧行動。</span><span class="sxs-lookup"><span data-stu-id="98cf2-128">The Cortana Intelligence Suite is a fully managed big data and advanced analytics suite to transform your data into intelligent action.</span></span> <span data-ttu-id="98cf2-129">請參閱 Suite 首頁查看完整的文件，包括客戶經驗談。</span><span class="sxs-lookup"><span data-stu-id="98cf2-129">See the Suite home page for full documentation, including customer stories.</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="98cf2-130">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="98cf2-130">Azure Machine Learning</span></span>
<span data-ttu-id="98cf2-131">這裡有兩個選項，**首頁** (您啟動的頁面)，和 **Studio**。</span><span class="sxs-lookup"><span data-stu-id="98cf2-131">There are two options here, **Home**, the page where you started, and **Studio**.</span></span>

<span data-ttu-id="98cf2-132">按一下 [Studio]，系統會將您帶到 **Azure Machine Learning Studio**。</span><span class="sxs-lookup"><span data-stu-id="98cf2-132">Click **Studio** and you'll be taken to the **Azure Machine Learning Studio**.</span></span> <span data-ttu-id="98cf2-133">首先，會要求您使用您的 Microsoft 帳戶，或是公司帳戶或學校帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="98cf2-133">First you'll be asked to sign in using your Microsoft account, or your work or school account.</span></span> <span data-ttu-id="98cf2-134">登入之後，您會在左邊看到下列索引標籤：</span><span class="sxs-lookup"><span data-stu-id="98cf2-134">Once signed in, you'll see the following tabs on the left:</span></span>

* <span data-ttu-id="98cf2-135">**專案** - 代表單一專案之實驗、資料集、Notebook 和其他資源的集合</span><span class="sxs-lookup"><span data-stu-id="98cf2-135">**PROJECTS** - Collections of experiments, datasets, notebooks, and other resources representing a single project</span></span>
* <span data-ttu-id="98cf2-136">**實驗** - 已建立及執行或儲存為草稿的實驗</span><span class="sxs-lookup"><span data-stu-id="98cf2-136">**EXPERIMENTS** - Experiments that you have created and run or saved as drafts</span></span>
* <span data-ttu-id="98cf2-137">**Web 服務** - 已從您的實驗部署的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="98cf2-137">**WEB SERVICES** - Web services that you have deployed from your experiments</span></span>
* <span data-ttu-id="98cf2-138">**Notebook** - 您已建立的 Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="98cf2-138">**NOTEBOOKS** - Jupyter notebooks that you have created</span></span>
* <span data-ttu-id="98cf2-139">**資料集** - 您已上傳到 Studio 的資料集</span><span class="sxs-lookup"><span data-stu-id="98cf2-139">**DATASETS** - Datasets that you have uploaded into Studio</span></span>
* <span data-ttu-id="98cf2-140">**定型模型** - 您已在實驗中訓練並儲存在 Studio 中的模型</span><span class="sxs-lookup"><span data-stu-id="98cf2-140">**TRAINED MODELS** - Models that you have trained in experiments and saved in Studio</span></span>
* <span data-ttu-id="98cf2-141">**設定** - 可用來設定帳戶和資源的一組設定。</span><span class="sxs-lookup"><span data-stu-id="98cf2-141">**SETTINGS** - A collection of settings that you can use to configure your account and resources.</span></span>

### <a name="gallery"></a><span data-ttu-id="98cf2-142">資源庫</span><span class="sxs-lookup"><span data-stu-id="98cf2-142">Gallery</span></span>
<span data-ttu-id="98cf2-143">按一下 [資源庫]，會帶您進入 **[Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/)**。</span><span class="sxs-lookup"><span data-stu-id="98cf2-143">Click **Gallery** and you'll be taken to the **[Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/)**.</span></span> <span data-ttu-id="98cf2-144">[資源庫] 可以讓資料科學家和開發人員社群在此分享使用 Cortana Intelligence 套件的元件建立的解決方案。</span><span class="sxs-lookup"><span data-stu-id="98cf2-144">The Gallery is a place where a community of data scientists and developers share solutions created using components of the Cortana Intelligence Suite.</span></span>

<span data-ttu-id="98cf2-145">如需有關資源庫的詳細資訊，請參閱 [共用及探索 Cortana Intelligence Gallery 中的方案](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="98cf2-145">For more information about the Gallery, see [Share and discover solutions in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

## <a name="components-of-an-experiment"></a><span data-ttu-id="98cf2-146">實驗的元件</span><span class="sxs-lookup"><span data-stu-id="98cf2-146">Components of an experiment</span></span>
<span data-ttu-id="98cf2-147">實驗由資料集組成，資料集提供資料給分析模組，將模組連接起就能建構預測分析模型。</span><span class="sxs-lookup"><span data-stu-id="98cf2-147">An experiment consists of datasets that provide data to analytical modules, which you connect together to construct a predictive analysis model.</span></span> <span data-ttu-id="98cf2-148">明確地說，有效的實驗有三個特性：</span><span class="sxs-lookup"><span data-stu-id="98cf2-148">Specifically, a valid experiment has these characteristics:</span></span>

* <span data-ttu-id="98cf2-149">實驗至少有一個資料集和一個模組</span><span class="sxs-lookup"><span data-stu-id="98cf2-149">The experiment has at least one dataset and one module</span></span>
* <span data-ttu-id="98cf2-150">資料集只能連接到模組</span><span class="sxs-lookup"><span data-stu-id="98cf2-150">Datasets may be connected only to modules</span></span>
* <span data-ttu-id="98cf2-151">模組可以連接到資料集或其他模組</span><span class="sxs-lookup"><span data-stu-id="98cf2-151">Modules may be connected to either datasets or other modules</span></span>
* <span data-ttu-id="98cf2-152">模組的所有輸入埠必須有資料流程的某些連線</span><span class="sxs-lookup"><span data-stu-id="98cf2-152">All input ports for modules must have some connection to the data flow</span></span>
* <span data-ttu-id="98cf2-153">必須設定每個模組的所有必要參數</span><span class="sxs-lookup"><span data-stu-id="98cf2-153">All required parameters for each module must be set</span></span>

<span data-ttu-id="98cf2-154">您可以從頭建立實驗，或者使用現有的範例實驗做為範本。</span><span class="sxs-lookup"><span data-stu-id="98cf2-154">You can create an experiment from scratch, or you can use an existing sample experiment as a template.</span></span> <span data-ttu-id="98cf2-155">如需詳細資訊，請參閱[複製範例實驗來建立新的機器學習服務實驗](machine-learning-sample-experiments.md)。</span><span class="sxs-lookup"><span data-stu-id="98cf2-155">For more information, see [Copy example experiments to create new machine learning experiments](machine-learning-sample-experiments.md).</span></span>

<span data-ttu-id="98cf2-156">如需建立簡易實驗的範例，請參閱 [在 Azure Machine Learning Studio 中建立簡易實驗](machine-learning-create-experiment.md)。</span><span class="sxs-lookup"><span data-stu-id="98cf2-156">For an example of creating a simple experiment, see [Create a simple experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span>

<span data-ttu-id="98cf2-157">如需建立預測性分析方案的更完整逐步解說，請參閱 [使用 Azure Machine Learning 開發預測方案](machine-learning-walkthrough-develop-predictive-solution.md)。</span><span class="sxs-lookup"><span data-stu-id="98cf2-157">For a more complete walkthrough of creating a predictive analytics solution, see [Develop a predictive solution with Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

### <a name="datasets"></a><span data-ttu-id="98cf2-158">資料集</span><span class="sxs-lookup"><span data-stu-id="98cf2-158">Datasets</span></span>
<span data-ttu-id="98cf2-159">資料集是指已上傳至 Machine Learning Studio 而可供模型化程序中使用的資料。</span><span class="sxs-lookup"><span data-stu-id="98cf2-159">A dataset is data that has been uploaded to Machine Learning Studio so that it can be used in the modeling process.</span></span> <span data-ttu-id="98cf2-160">Machine Learning Studio 隨附許多範例資料集供您實驗，您可以在需要時上傳更多資料集。</span><span class="sxs-lookup"><span data-stu-id="98cf2-160">A number of sample datasets are included with Machine Learning Studio for you to experiment with, and you can upload more datasets as you need them.</span></span> <span data-ttu-id="98cf2-161">以下是隨附資料集的一些例子：</span><span class="sxs-lookup"><span data-stu-id="98cf2-161">Here are some examples of included datasets:</span></span>

* <span data-ttu-id="98cf2-162">**各種汽車的 MPG 資料** - 汽車的每加侖英里 (MPG) 值，以汽缸數、馬力等來識別。</span><span class="sxs-lookup"><span data-stu-id="98cf2-162">**MPG data for various automobiles** - Miles per gallon (MPG) values for automobiles identified by number of cylinders, horsepower, etc.</span></span>
* <span data-ttu-id="98cf2-163">**乳癌資料** - 乳癌診斷資料。</span><span class="sxs-lookup"><span data-stu-id="98cf2-163">**Breast cancer data** - Breast cancer diagnosis data.</span></span>
* <span data-ttu-id="98cf2-164">**森林火災資料** - 葡萄牙西北部的森林火災範圍</span><span class="sxs-lookup"><span data-stu-id="98cf2-164">**Forest fires data** - Forest fire sizes in northeast Portugal.</span></span>

<span data-ttu-id="98cf2-165">當您建置實驗時，可以從畫布左邊的資料集清單選擇。</span><span class="sxs-lookup"><span data-stu-id="98cf2-165">As you build an experiment you can choose from the list of datasets available to the left of the canvas.</span></span>

<span data-ttu-id="98cf2-166">如需 Machine Learning Studio 隨附的範例資料集清單，請參閱 [在 Azure Machine Learning Studio 中使用範例資料集](machine-learning-use-sample-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="98cf2-166">For a list of sample datasets included in Machine Learning Studio, see [Use the sample data sets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md).</span></span>

### <a name="modules"></a><span data-ttu-id="98cf2-167">模組</span><span class="sxs-lookup"><span data-stu-id="98cf2-167">Modules</span></span>
<span data-ttu-id="98cf2-168">模組是指您在資料上可執行的演算法。</span><span class="sxs-lookup"><span data-stu-id="98cf2-168">A module is an algorithm that you can perform on your data.</span></span> <span data-ttu-id="98cf2-169">Machine Learning Studio 有許多模組，從資料輸入函數到訓練、評分和驗證程序都有。</span><span class="sxs-lookup"><span data-stu-id="98cf2-169">Machine Learning Studio has a number of modules ranging from data ingress functions to training, scoring, and validation processes.</span></span> <span data-ttu-id="98cf2-170">以下是隨附模組的一些例子：</span><span class="sxs-lookup"><span data-stu-id="98cf2-170">Here are some examples of included modules:</span></span>

* <span data-ttu-id="98cf2-171">[轉換成 ARFF][convert-to-arff] - 將 .NET 序列化資料集轉換為屬性關聯性檔案格式 (ARFF)。</span><span class="sxs-lookup"><span data-stu-id="98cf2-171">[Convert to ARFF][convert-to-arff] - Converts a .NET serialized dataset to Attribute-Relation File Format (ARFF).</span></span>
* <span data-ttu-id="98cf2-172">[計算基本統計資料][elementary-statistics] - 計算基本統計資料，例如平均值、標準差等。</span><span class="sxs-lookup"><span data-stu-id="98cf2-172">[Compute Elementary Statistics][elementary-statistics] - Calculates elementary statistics such as mean, standard deviation, etc.</span></span>
* <span data-ttu-id="98cf2-173">[線性迴歸][linear-regression] - 建立線上梯度下降線性迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="98cf2-173">[Linear Regression][linear-regression] - Creates an online gradient descent-based linear regression model.</span></span>
* <span data-ttu-id="98cf2-174">[評分模型][score-model] - 給訓練的分類或迴歸模型評分。</span><span class="sxs-lookup"><span data-stu-id="98cf2-174">[Score Model][score-model] - Scores a trained classification or regression model.</span></span>

<span data-ttu-id="98cf2-175">當您建置實驗時，可以從畫布左邊的模組清單選擇。</span><span class="sxs-lookup"><span data-stu-id="98cf2-175">As you build an experiment you can choose from the list of modules available to the left of the canvas.</span></span>  

<span data-ttu-id="98cf2-176">模組可能有一組參數可用來設定模組的內部演算法。</span><span class="sxs-lookup"><span data-stu-id="98cf2-176">A module may have a set of parameters that you can use to configure the module's internal algorithms.</span></span> <span data-ttu-id="98cf2-177">當您在畫布上選取模組時，模組的參數會顯示在畫布右邊的 [屬性]  窗格中。</span><span class="sxs-lookup"><span data-stu-id="98cf2-177">When you select a module on the canvas, the module's parameters are displayed in the **Properties** pane to the right of the canvas.</span></span> <span data-ttu-id="98cf2-178">您可以在此窗格中修改參數來調整模型。</span><span class="sxs-lookup"><span data-stu-id="98cf2-178">You can modify the parameters in that pane to tune your model.</span></span>

<span data-ttu-id="98cf2-179">如需了解機器學習演算法的一些說明，請參閱 [如何選擇 Microsoft Azure Machine Learning 的演算法](machine-learning-algorithm-choice.md)。</span><span class="sxs-lookup"><span data-stu-id="98cf2-179">For some help navigating through the large library of machine learning algorithms available, see [How to choose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>

## <a name="deploying-a-predictive-analytics-web-service"></a><span data-ttu-id="98cf2-180">部署預測性分析 Web 服務</span><span class="sxs-lookup"><span data-stu-id="98cf2-180">Deploying a predictive analytics web service</span></span>
<span data-ttu-id="98cf2-181">當您的預測性分析模型準備好時，可以從 Machine Learning Studio 將它部署為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="98cf2-181">Once your predictive analytics model is ready, you can deploy it as a web service right from Machine Learning Studio.</span></span> <span data-ttu-id="98cf2-182">如需此程序的詳細資訊，請參閱 [部署 Azure Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="98cf2-182">For more details on this process, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

[ml-studio-overview]:./media/machine-learning-what-is-ml-studio/azure-ml-studio-diagram.jpg

<!-- Module References -->
[convert-to-arff]: https://msdn.microsoft.com/library/azure/62d2cece-d832-4a7a-a0bd-f01f03af0960/
[elementary-statistics]: https://msdn.microsoft.com/library/azure/3086b8d4-c895-45ba-8aa9-34f0c944d4d3/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
