---
title: "aaaWhat 是 Azure Machine Learning Studio？ | Microsoft Docs"
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
ms.openlocfilehash: a25f2d9e75d088a37930de98240c6e14c9567fa4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-machine-learning-studio"></a><span data-ttu-id="60944-105">什麼是 Azure Machine Learning Studio？</span><span class="sxs-lookup"><span data-stu-id="60944-105">What is Azure Machine Learning Studio?</span></span>
<span data-ttu-id="60944-106">Microsoft Azure Machine Learning Studio 是共同作業、 拖放的工具，您可以使用 toobuild、 測試及部署您的資料的預測分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="60944-106">Microsoft Azure Machine Learning Studio is a collaborative, drag-and-drop tool you can use toobuild, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="60944-107">Machine Learning Studio 會以 Web 服務方式發佈模型，讓自訂應用程式或 BI 工具 (例如 Excel) 都能夠很容易地使用。</span><span class="sxs-lookup"><span data-stu-id="60944-107">Machine Learning Studio publishes models as web services that can easily be consumed by custom apps or BI tools such as Excel.</span></span>

<span data-ttu-id="60944-108">Machine Learning Studio 讓資料科學、預測分析、雲端資源和您的資料齊聚一堂！</span><span class="sxs-lookup"><span data-stu-id="60944-108">Machine Learning Studio is where data science, predictive analytics, cloud resources, and your data meet.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-machine-learning-studio-interactive-workspace"></a><span data-ttu-id="60944-109">hello Machine Learning Studio 的互動式工作區</span><span class="sxs-lookup"><span data-stu-id="60944-109">hello Machine Learning Studio interactive workspace</span></span>
<span data-ttu-id="60944-110">toodevelop 預測分析模型，您通常會使用資料從一個或多個來源、 轉換和分析透過各種不同的資料操作和統計函數，該資料，並產生的結果集。</span><span class="sxs-lookup"><span data-stu-id="60944-110">toodevelop a predictive analysis model, you typically use data from one or more sources, transform and analyze that data through various data manipulation and statistical functions, and generate a set of results.</span></span> <span data-ttu-id="60944-111">開發此類模型是一種反覆式過程。</span><span class="sxs-lookup"><span data-stu-id="60944-111">Developing a model like this is an iterative process.</span></span> <span data-ttu-id="60944-112">當您修改 hello 各種函式和其參數、 結果聚合，直到您滿意您有定型、 有效率的模型。</span><span class="sxs-lookup"><span data-stu-id="60944-112">As you modify hello various functions and their parameters, your results converge until you are satisfied that you have a trained, effective model.</span></span>

<span data-ttu-id="60944-113">**Azure Machine Learning Studio**您互動、 視覺化工作區 tooeasily 建置，可讓測試及逐一查看預測分析模型。</span><span class="sxs-lookup"><span data-stu-id="60944-113">**Azure Machine Learning Studio** gives you an interactive, visual workspace tooeasily build, test, and iterate on a predictive analysis model.</span></span> <span data-ttu-id="60944-114">您拖放***資料集***及分析***模組***畫布互動式，它們連接在一起的 tooform***實驗***，在機器學習中執行Studio。</span><span class="sxs-lookup"><span data-stu-id="60944-114">You drag-and-drop ***datasets*** and analysis ***modules*** onto an interactive canvas, connecting them together tooform an ***experiment***, which you run in Machine Learning Studio.</span></span> <span data-ttu-id="60944-115">在模型設計 tooiterate，編輯 hello 實驗中的，儲存複本，如有需要，再執行一次。</span><span class="sxs-lookup"><span data-stu-id="60944-115">tooiterate on your model design, you edit hello experiment, save a copy if desired, and run it again.</span></span> <span data-ttu-id="60944-116">當您準備好時，您可以將轉換您***定型實驗***tooa***預測實驗***，然後將它做為發行***web 服務***以便可以存取您的模型其他人。</span><span class="sxs-lookup"><span data-stu-id="60944-116">When you're ready, you can convert your ***training experiment*** tooa ***predictive experiment***, and then publish it as a ***web service*** so that your model can be accessed by others.</span></span>

<span data-ttu-id="60944-117">沒有不需要任何程式設計，只要以視覺化方式連接資料集和模組 tooconstruct 預測分析模型。</span><span class="sxs-lookup"><span data-stu-id="60944-117">There is no programming required, just visually connecting datasets and modules tooconstruct your predictive analysis model.</span></span>

> [!TIP]
> <span data-ttu-id="60944-118">toodownload 及列印的圖表，hello Machine Learning Studio 中，功能的概觀，請參閱[Azure Machine Learning Studio 功能的概觀圖表](machine-learning-studio-overview-diagram.md)。</span><span class="sxs-lookup"><span data-stu-id="60944-118">toodownload and print a diagram that gives an overview of hello capabilities of Machine Learning Studio, see [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
> 
> 

![Azure ML Studio 圖表：建立實驗、讀取許多來源的資料、寫入評分的資料及寫入模型。][ml-studio-overview]

## <a name="get-started-with-machine-learning-studio"></a><span data-ttu-id="60944-120">開始使用 Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="60944-120">Get started with Machine Learning Studio</span></span>
<span data-ttu-id="60944-121">當您第一次輸入[Machine Learning Studio](https://studio.azureml.net)看到 hello**首頁**頁面。</span><span class="sxs-lookup"><span data-stu-id="60944-121">When you first enter [Machine Learning Studio](https://studio.azureml.net) you see hello **Home** page.</span></span> <span data-ttu-id="60944-122">您可以從這裡檢視文件、影片、網路研討會，以及尋找其他重要資源。</span><span class="sxs-lookup"><span data-stu-id="60944-122">From here you can view documentation, videos, webinars, and find other valuable resources.</span></span>

<span data-ttu-id="60944-123">按一下左上方 hello 功能表</span><span class="sxs-lookup"><span data-stu-id="60944-123">Click hello upper-left menu</span></span> ![功能表](media/machine-learning-what-is-ml-studio/menu.png) <span data-ttu-id="60944-125">您會看到幾個選項。</span><span class="sxs-lookup"><span data-stu-id="60944-125">and you'll see several options.</span></span>

### <a name="cortana-intelligence"></a><span data-ttu-id="60944-126">Cortana Intelligence</span><span class="sxs-lookup"><span data-stu-id="60944-126">Cortana Intelligence</span></span>
<span data-ttu-id="60944-127">按一下**Cortana 智慧**和您將會進入 hello toohello 首頁[Cortana 智慧套件](https://www.microsoft.com/cloud-platform/cortana-intelligence-suite)。</span><span class="sxs-lookup"><span data-stu-id="60944-127">Click **Cortana Intelligence** and you'll be taken toohello home page of hello [Cortana Intelligence Suite](https://www.microsoft.com/cloud-platform/cortana-intelligence-suite).</span></span> <span data-ttu-id="60944-128">hello Cortana 智慧套件是完全受管理的巨量資料，並為智慧型動作 advanced analytics suite tootransform 您的資料。</span><span class="sxs-lookup"><span data-stu-id="60944-128">hello Cortana Intelligence Suite is a fully managed big data and advanced analytics suite tootransform your data into intelligent action.</span></span> <span data-ttu-id="60944-129">請參閱 hello 套件首頁，如完整的文件，包括客戶劇本。</span><span class="sxs-lookup"><span data-stu-id="60944-129">See hello Suite home page for full documentation, including customer stories.</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="60944-130">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="60944-130">Azure Machine Learning</span></span>
<span data-ttu-id="60944-131">有兩個選項在這裡，**首頁**，在您啟動，hello 頁面和**Studio**。</span><span class="sxs-lookup"><span data-stu-id="60944-131">There are two options here, **Home**, hello page where you started, and **Studio**.</span></span>

<span data-ttu-id="60944-132">按一下**Studio**和您將會進入 toohello **Azure Machine Learning Studio**。</span><span class="sxs-lookup"><span data-stu-id="60944-132">Click **Studio** and you'll be taken toohello **Azure Machine Learning Studio**.</span></span> <span data-ttu-id="60944-133">第一次系統會詢問 toosign 中使用您的 Microsoft 帳戶或工作或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="60944-133">First you'll be asked toosign in using your Microsoft account, or your work or school account.</span></span> <span data-ttu-id="60944-134">一旦登入，您會看到下列索引標籤左側 hello hello:</span><span class="sxs-lookup"><span data-stu-id="60944-134">Once signed in, you'll see hello following tabs on hello left:</span></span>

* <span data-ttu-id="60944-135">**專案** - 代表單一專案之實驗、資料集、Notebook 和其他資源的集合</span><span class="sxs-lookup"><span data-stu-id="60944-135">**PROJECTS** - Collections of experiments, datasets, notebooks, and other resources representing a single project</span></span>
* <span data-ttu-id="60944-136">**實驗** - 已建立及執行或儲存為草稿的實驗</span><span class="sxs-lookup"><span data-stu-id="60944-136">**EXPERIMENTS** - Experiments that you have created and run or saved as drafts</span></span>
* <span data-ttu-id="60944-137">**Web 服務** - 已從您的實驗部署的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="60944-137">**WEB SERVICES** - Web services that you have deployed from your experiments</span></span>
* <span data-ttu-id="60944-138">**Notebook** - 您已建立的 Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="60944-138">**NOTEBOOKS** - Jupyter notebooks that you have created</span></span>
* <span data-ttu-id="60944-139">**資料集** - 您已上傳到 Studio 的資料集</span><span class="sxs-lookup"><span data-stu-id="60944-139">**DATASETS** - Datasets that you have uploaded into Studio</span></span>
* <span data-ttu-id="60944-140">**定型模型** - 您已在實驗中訓練並儲存在 Studio 中的模型</span><span class="sxs-lookup"><span data-stu-id="60944-140">**TRAINED MODELS** - Models that you have trained in experiments and saved in Studio</span></span>
* <span data-ttu-id="60944-141">**設定**-設定您的帳戶和資源，您可以使用 tooconfigure 的集合。</span><span class="sxs-lookup"><span data-stu-id="60944-141">**SETTINGS** - A collection of settings that you can use tooconfigure your account and resources.</span></span>

### <a name="gallery"></a><span data-ttu-id="60944-142">資源庫</span><span class="sxs-lookup"><span data-stu-id="60944-142">Gallery</span></span>
<span data-ttu-id="60944-143">按一下**圖庫**和您將會進入 toohello  **[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com/)**。</span><span class="sxs-lookup"><span data-stu-id="60944-143">Click **Gallery** and you'll be taken toohello **[Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/)**.</span></span> <span data-ttu-id="60944-144">hello 圖庫是其中的資料科學家和開發人員社群分享使用 hello Cortana 智慧套件的元件建立方案的位置。</span><span class="sxs-lookup"><span data-stu-id="60944-144">hello Gallery is a place where a community of data scientists and developers share solutions created using components of hello Cortana Intelligence Suite.</span></span>

<span data-ttu-id="60944-145">如需 hello 組件庫的詳細資訊，請參閱[共用及探索 hello Cortana 智慧組件庫中的方案](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="60944-145">For more information about hello Gallery, see [Share and discover solutions in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

## <a name="components-of-an-experiment"></a><span data-ttu-id="60944-146">實驗的元件</span><span class="sxs-lookup"><span data-stu-id="60944-146">Components of an experiment</span></span>
<span data-ttu-id="60944-147">提供資料 tooanalytical 模組，您連接在一起的資料集包含實驗 tooconstruct 預測分析模型。</span><span class="sxs-lookup"><span data-stu-id="60944-147">An experiment consists of datasets that provide data tooanalytical modules, which you connect together tooconstruct a predictive analysis model.</span></span> <span data-ttu-id="60944-148">明確地說，有效的實驗有三個特性：</span><span class="sxs-lookup"><span data-stu-id="60944-148">Specifically, a valid experiment has these characteristics:</span></span>

* <span data-ttu-id="60944-149">hello 實驗具有至少一個資料集和一個模組</span><span class="sxs-lookup"><span data-stu-id="60944-149">hello experiment has at least one dataset and one module</span></span>
* <span data-ttu-id="60944-150">資料集可能是已連線的唯一 toomodules</span><span class="sxs-lookup"><span data-stu-id="60944-150">Datasets may be connected only toomodules</span></span>
* <span data-ttu-id="60944-151">模組可能連接的 tooeither 資料集或其他模組</span><span class="sxs-lookup"><span data-stu-id="60944-151">Modules may be connected tooeither datasets or other modules</span></span>
* <span data-ttu-id="60944-152">所有模組的輸入連接埠必須有一些連接 toohello 資料流</span><span class="sxs-lookup"><span data-stu-id="60944-152">All input ports for modules must have some connection toohello data flow</span></span>
* <span data-ttu-id="60944-153">必須設定每個模組的所有必要參數</span><span class="sxs-lookup"><span data-stu-id="60944-153">All required parameters for each module must be set</span></span>

<span data-ttu-id="60944-154">您可以從頭建立實驗，或者使用現有的範例實驗做為範本。</span><span class="sxs-lookup"><span data-stu-id="60944-154">You can create an experiment from scratch, or you can use an existing sample experiment as a template.</span></span> <span data-ttu-id="60944-155">如需詳細資訊，請參閱[複製範例實驗 toocreate 新機器學習實驗](machine-learning-sample-experiments.md)。</span><span class="sxs-lookup"><span data-stu-id="60944-155">For more information, see [Copy example experiments toocreate new machine learning experiments](machine-learning-sample-experiments.md).</span></span>

<span data-ttu-id="60944-156">如需建立簡易實驗的範例，請參閱 [在 Azure Machine Learning Studio 中建立簡易實驗](machine-learning-create-experiment.md)。</span><span class="sxs-lookup"><span data-stu-id="60944-156">For an example of creating a simple experiment, see [Create a simple experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span>

<span data-ttu-id="60944-157">如需建立預測性分析方案的更完整逐步解說，請參閱 [使用 Azure Machine Learning 開發預測方案](machine-learning-walkthrough-develop-predictive-solution.md)。</span><span class="sxs-lookup"><span data-stu-id="60944-157">For a more complete walkthrough of creating a predictive analytics solution, see [Develop a predictive solution with Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

### <a name="datasets"></a><span data-ttu-id="60944-158">資料集</span><span class="sxs-lookup"><span data-stu-id="60944-158">Datasets</span></span>
<span data-ttu-id="60944-159">資料集是已經過的資料上傳 tooMachine Learning Studio 使用於 hello 模型程序。</span><span class="sxs-lookup"><span data-stu-id="60944-159">A dataset is data that has been uploaded tooMachine Learning Studio so that it can be used in hello modeling process.</span></span> <span data-ttu-id="60944-160">範例資料集的數目隨附於 Machine Learning Studio tooexperiment，如，您可以上傳多個資料集，您需要的時候。</span><span class="sxs-lookup"><span data-stu-id="60944-160">A number of sample datasets are included with Machine Learning Studio for you tooexperiment with, and you can upload more datasets as you need them.</span></span> <span data-ttu-id="60944-161">以下是隨附資料集的一些例子：</span><span class="sxs-lookup"><span data-stu-id="60944-161">Here are some examples of included datasets:</span></span>

* <span data-ttu-id="60944-162">**各種汽車的 MPG 資料** - 汽車的每加侖英里 (MPG) 值，以汽缸數、馬力等來識別。</span><span class="sxs-lookup"><span data-stu-id="60944-162">**MPG data for various automobiles** - Miles per gallon (MPG) values for automobiles identified by number of cylinders, horsepower, etc.</span></span>
* <span data-ttu-id="60944-163">**乳癌資料** - 乳癌診斷資料。</span><span class="sxs-lookup"><span data-stu-id="60944-163">**Breast cancer data** - Breast cancer diagnosis data.</span></span>
* <span data-ttu-id="60944-164">**森林火災資料** - 葡萄牙西北部的森林火災範圍</span><span class="sxs-lookup"><span data-stu-id="60944-164">**Forest fires data** - Forest fire sizes in northeast Portugal.</span></span>

<span data-ttu-id="60944-165">當您建立實驗可以從清單中選擇 hello 可用的資料集的 toohello 方 hello 畫布。</span><span class="sxs-lookup"><span data-stu-id="60944-165">As you build an experiment you can choose from hello list of datasets available toohello left of hello canvas.</span></span>

<span data-ttu-id="60944-166">如需包含 Machine Learning Studio 中的範例資料集的清單，請參閱[使用 Azure Machine Learning Studio 中的 hello 取樣資料集](machine-learning-use-sample-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="60944-166">For a list of sample datasets included in Machine Learning Studio, see [Use hello sample data sets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md).</span></span>

### <a name="modules"></a><span data-ttu-id="60944-167">模組</span><span class="sxs-lookup"><span data-stu-id="60944-167">Modules</span></span>
<span data-ttu-id="60944-168">模組是指您在資料上可執行的演算法。</span><span class="sxs-lookup"><span data-stu-id="60944-168">A module is an algorithm that you can perform on your data.</span></span> <span data-ttu-id="60944-169">Machine Learning Studio 即會從資料輸入函式 tootraining、 計分，以及驗證程序的模組數目。</span><span class="sxs-lookup"><span data-stu-id="60944-169">Machine Learning Studio has a number of modules ranging from data ingress functions tootraining, scoring, and validation processes.</span></span> <span data-ttu-id="60944-170">以下是隨附模組的一些例子：</span><span class="sxs-lookup"><span data-stu-id="60944-170">Here are some examples of included modules:</span></span>

* <span data-ttu-id="60944-171">[轉換 tooARFF] [ convert-to-arff] -將轉換.NET 序列化資料集 tooAttribute 關聯檔案格式 (ARFF)。</span><span class="sxs-lookup"><span data-stu-id="60944-171">[Convert tooARFF][convert-to-arff] - Converts a .NET serialized dataset tooAttribute-Relation File Format (ARFF).</span></span>
* <span data-ttu-id="60944-172">[計算基本統計資料][elementary-statistics] - 計算基本統計資料，例如平均值、標準差等。</span><span class="sxs-lookup"><span data-stu-id="60944-172">[Compute Elementary Statistics][elementary-statistics] - Calculates elementary statistics such as mean, standard deviation, etc.</span></span>
* <span data-ttu-id="60944-173">[線性迴歸][linear-regression] - 建立線上梯度下降線性迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="60944-173">[Linear Regression][linear-regression] - Creates an online gradient descent-based linear regression model.</span></span>
* <span data-ttu-id="60944-174">[評分模型][score-model] - 給訓練的分類或迴歸模型評分。</span><span class="sxs-lookup"><span data-stu-id="60944-174">[Score Model][score-model] - Scores a trained classification or regression model.</span></span>

<span data-ttu-id="60944-175">當您建立實驗可以從清單中選擇 hello 可使用的模組 toohello 方 hello 畫布。</span><span class="sxs-lookup"><span data-stu-id="60944-175">As you build an experiment you can choose from hello list of modules available toohello left of hello canvas.</span></span>  

<span data-ttu-id="60944-176">模組可能會有一組您可以使用 tooconfigure hello 模組的內部演算法的參數。</span><span class="sxs-lookup"><span data-stu-id="60944-176">A module may have a set of parameters that you can use tooconfigure hello module's internal algorithms.</span></span> <span data-ttu-id="60944-177">當您選取 hello 畫布上的模組時，hello 模組參數會顯示在 hello**屬性**窗格 toohello hello 畫布的權限。</span><span class="sxs-lookup"><span data-stu-id="60944-177">When you select a module on hello canvas, hello module's parameters are displayed in hello **Properties** pane toohello right of hello canvas.</span></span> <span data-ttu-id="60944-178">您可以修改您的模型中該窗格 tootune hello 參數。</span><span class="sxs-lookup"><span data-stu-id="60944-178">You can modify hello parameters in that pane tootune your model.</span></span>

<span data-ttu-id="60944-179">某些說明瀏覽可用的機器學習演算法的 hello 大型的程式庫，請參閱[如何為 Microsoft Azure 機器學習 toochoose 演算法](machine-learning-algorithm-choice.md)。</span><span class="sxs-lookup"><span data-stu-id="60944-179">For some help navigating through hello large library of machine learning algorithms available, see [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>

## <a name="deploying-a-predictive-analytics-web-service"></a><span data-ttu-id="60944-180">部署預測性分析 Web 服務</span><span class="sxs-lookup"><span data-stu-id="60944-180">Deploying a predictive analytics web service</span></span>
<span data-ttu-id="60944-181">當您的預測性分析模型準備好時，可以從 Machine Learning Studio 將它部署為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="60944-181">Once your predictive analytics model is ready, you can deploy it as a web service right from Machine Learning Studio.</span></span> <span data-ttu-id="60944-182">如需此程序的詳細資訊，請參閱 [部署 Azure Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="60944-182">For more details on this process, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

[ml-studio-overview]:./media/machine-learning-what-is-ml-studio/azure-ml-studio-diagram.jpg

<!-- Module References -->
[convert-to-arff]: https://msdn.microsoft.com/library/azure/62d2cece-d832-4a7a-a0bd-f01f03af0960/
[elementary-statistics]: https://msdn.microsoft.com/library/azure/3086b8d4-c895-45ba-8aa9-34f0c944d4d3/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
