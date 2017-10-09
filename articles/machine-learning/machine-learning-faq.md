---
title: "aaaAzure 常見問題集 (Faq) 的機器學習 |Microsoft 文件"
description: "Azure Machine Learning 簡介：常見問題集，涵蓋計費、功能，以及適用於簡化預測性模型化之雲端服務的限制。"
keywords: "機器學習服務簡介,建立預測模型,什麼是機器學習服務"
services: machine-learning
documentationcenter: 
author: garyericson
manager: paulettm
editor: cgronlun
ms.assetid: a4a32a06-dbed-4727-a857-c10da774ce66
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: 3af84451dde064c3c9520ee520b541128b1eef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-frequently-asked-questions-billing-capabilities-limitations-and-support"></a><span data-ttu-id="433fc-104">Azure Machine Learning 常見問題集：計費、功能、限制及支援</span><span class="sxs-lookup"><span data-stu-id="433fc-104">Azure Machine Learning frequently asked questions: Billing, capabilities, limitations, and support</span></span>
<span data-ttu-id="433fc-105">以下是有關 Azure Machine Learning 的一些常見問題和對應解答，而 Azure Machine Learning 是適合透過 Web 服務開發預測性模型和運作方案的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="433fc-105">Here are some frequently asked questions (FAQs) and corresponding answers about Azure Machine Learning, a cloud service for developing predictive models and operationalizing solutions through web services.</span></span> <span data-ttu-id="433fc-106">這些常見問題集提供有關如何 toouse hello 服務，其中包括 hello 計費模型、 功能、 限制和支援問題。</span><span class="sxs-lookup"><span data-stu-id="433fc-106">These FAQs provide questions about how toouse hello service, which includes hello billing model, capabilities, limitations, and support.</span></span>

<span data-ttu-id="433fc-107">**是否有您無法在這裡找到的問題？**</span><span class="sxs-lookup"><span data-stu-id="433fc-107">**Have a question you can't find here?**</span></span>

<span data-ttu-id="433fc-108">Azure Machine Learning 有其中 hello 資料科學社群的成員可以詢問有關 Azure Machine Learning 的 MSDN 上的論壇。</span><span class="sxs-lookup"><span data-stu-id="433fc-108">Azure Machine Learning has a forum on MSDN where members of hello data science community can ask questions about Azure Machine Learning.</span></span> <span data-ttu-id="433fc-109">hello Azure Machine Learning 小組監視 hello 論壇。</span><span class="sxs-lookup"><span data-stu-id="433fc-109">hello Azure Machine Learning team monitors hello forum.</span></span> <span data-ttu-id="433fc-110">移 toohello [Azure 機器學習論壇](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning)toosearch 答案或 toopost 您自己的新的問題。</span><span class="sxs-lookup"><span data-stu-id="433fc-110">Go toohello [Azure Machine Learning Forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toosearch for answers or toopost a new question of your own.</span></span>

## <a name="general-questions"></a><span data-ttu-id="433fc-111">一般問題</span><span class="sxs-lookup"><span data-stu-id="433fc-111">General questions</span></span>
<span data-ttu-id="433fc-112">**什麼是 Azure Machine Learning 服務？**</span><span class="sxs-lookup"><span data-stu-id="433fc-112">**What is Azure Machine Learning?**</span></span>

<span data-ttu-id="433fc-113">Azure Machine Learning 是完全受管理的服務，您可以使用 toocreate、 測試、 操作及管理 hello 雲端中的預測分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="433fc-113">Azure Machine Learning is a fully managed service that you can use toocreate, test, operate, and manage predictive analytic solutions in hello cloud.</span></span> <span data-ttu-id="433fc-114">僅使用瀏覽器，您即可以登入、上傳資料，以及立即開始機器學習實驗。</span><span class="sxs-lookup"><span data-stu-id="433fc-114">With only a browser, you can sign in, upload data, and immediately start machine-learning experiments.</span></span> <span data-ttu-id="433fc-115">拖放式預測性模型化、大型模組和用以啟動範本的程式庫，讓您得以簡便而快速地執行一般機器學習工作。</span><span class="sxs-lookup"><span data-stu-id="433fc-115">Drag-and-drop predictive modeling, a large pallet of modules, and a library of starting templates make common machine-learning tasks simple and quick.</span></span> <span data-ttu-id="433fc-116">如需詳細資訊，請參閱 hello [Azure 機器學習服務概觀](https://azure.microsoft.com/services/machine-learning/)。</span><span class="sxs-lookup"><span data-stu-id="433fc-116">For more information, see hello [Azure Machine Learning service overview](https://azure.microsoft.com/services/machine-learning/).</span></span> <span data-ttu-id="433fc-117">如簡介 toomachine 學習主要詞彙和概念的說明，請參閱[簡介 tooAzure 機器學習](machine-learning-what-is-machine-learning.md)。</span><span class="sxs-lookup"><span data-stu-id="433fc-117">For an introduction toomachine learning that explains key terminology and concepts, see [Introduction tooAzure Machine Learning](machine-learning-what-is-machine-learning.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="433fc-118">**什麼是 Machine Learning Studio？**</span><span class="sxs-lookup"><span data-stu-id="433fc-118">**What is Machine Learning Studio?**</span></span>

<span data-ttu-id="433fc-119">Machine Learning Studio 是您利用網頁瀏覽器存取的工作區環境。</span><span class="sxs-lookup"><span data-stu-id="433fc-119">Machine Learning Studio is a workbench environment that you access by using a web browser.</span></span> <span data-ttu-id="433fc-120">Machine Learning Studio 主控模組可協助您建立端對端視覺構圖介面中的，實驗的 hello 表單中的資料科學工作流程在棧的板。</span><span class="sxs-lookup"><span data-stu-id="433fc-120">Machine Learning Studio hosts a pallet of modules in a visual composition interface that helps you build an end-to-end, data-science workflow in hello form of an experiment.</span></span>

<span data-ttu-id="433fc-121">如需 Machine Learning Studio 的詳細資訊，請參閱 [什麼是 Machine Learning Studio？](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="433fc-121">For more information about Machine Learning Studio, see [What is Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>

<span data-ttu-id="433fc-122">**什麼是 hello 機器學習 API 服務？**</span><span class="sxs-lookup"><span data-stu-id="433fc-122">**What is hello Machine Learning API service?**</span></span>

<span data-ttu-id="433fc-123">hello 機器學習 API 服務可讓您 toodeploy 預測模型，例如模型內建 Machine Learning Studio 中，為既可調整又容錯，web 服務。</span><span class="sxs-lookup"><span data-stu-id="433fc-123">hello Machine Learning API service enables you toodeploy predictive models, like those that are built into Machine Learning Studio, as scalable, fault-tolerant, web services.</span></span> <span data-ttu-id="433fc-124">建立 hello 機器學習 API 服務的 hello web 服務是 REST Api 可提供外部應用程式與您的預測分析的模型之間的通訊介面。</span><span class="sxs-lookup"><span data-stu-id="433fc-124">hello web services that hello Machine Learning API service creates are REST APIs that provide an interface for communication between external applications and your predictive analytics models.</span></span>

<span data-ttu-id="433fc-125">如需詳細資訊，請參閱[如何 tooconsume Azure 機器學習 Web 服務](machine-learning-consume-web-services.md)。</span><span class="sxs-lookup"><span data-stu-id="433fc-125">For more information, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

<span data-ttu-id="433fc-126">**傳統 Web 服務會在哪裡列出？新型 (Azure Resource Manager 架構) Web 服務會在哪裡列出？**</span><span class="sxs-lookup"><span data-stu-id="433fc-126">**Where are my Classic web services listed? Where are my New (Azure Resource Manager-based) web services listed?**</span></span>

<span data-ttu-id="433fc-127">建立使用 hello 傳統部署模型和 web 服務使用 hello 新的 Azure Resource Manager 部署模型所建立的 web 服務會列在 hello [Microsoft Azure 機器學習 Web 服務](https://services.azureml.net/)入口網站。</span><span class="sxs-lookup"><span data-stu-id="433fc-127">Web services created using hello Classic deployment model and web services created using hello New Azure Resource Manager deployment model are listed in hello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="433fc-128">傳統 web 服務也會列在[Machine Learning Studio](http://studio.azureml.net)上 hello **Web 服務** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="433fc-128">Classic web services are also listed in [Machine Learning Studio](http://studio.azureml.net) on hello **Web services** tab.</span></span>

## <a name="azure-machine-learning-questions"></a><span data-ttu-id="433fc-129">Azure Machine Learning 問題</span><span class="sxs-lookup"><span data-stu-id="433fc-129">Azure Machine Learning questions</span></span>
<span data-ttu-id="433fc-130">**Azure Machine Learning Web 服務是什麼？**</span><span class="sxs-lookup"><span data-stu-id="433fc-130">**What are Azure Machine Learning web services?**</span></span>

<span data-ttu-id="433fc-131">Machine Learning Web 服務可在應用程式與機器學習服務工作流程計分模型之間提供介面。</span><span class="sxs-lookup"><span data-stu-id="433fc-131">Machine Learning web services provide an interface between an application and a Machine Learning workflow scoring model.</span></span> <span data-ttu-id="433fc-132">外部應用程式可以使用 Azure Machine Learning toocommunicate 搭配即時的機器學習服務工作流程計分模型。</span><span class="sxs-lookup"><span data-stu-id="433fc-132">An external application can use Azure Machine Learning toocommunicate with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="433fc-133">呼叫 tooa 機器學習 web 服務傳回預測結果 tooan 外部應用程式。</span><span class="sxs-lookup"><span data-stu-id="433fc-133">A call tooa Machine Learning web service returns prediction results tooan external application.</span></span> <span data-ttu-id="433fc-134">toomake 呼叫 tooa web 服務，您傳遞您部署的 hello web 服務時所建立的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="433fc-134">toomake a call tooa web service, you pass an API key that was created when you deployed hello web service.</span></span> <span data-ttu-id="433fc-135">Machine Learning Web 服務以 REST 為基礎，這是一種常見的 Web 程式設計專案架構。</span><span class="sxs-lookup"><span data-stu-id="433fc-135">A Machine Learning web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="433fc-136">Azure Machine Learning 有兩種 Web 服務類型：</span><span class="sxs-lookup"><span data-stu-id="433fc-136">Azure Machine Learning has two types of web services:</span></span>

* <span data-ttu-id="433fc-137">要求-回應服務 (RR): 的低延遲、 高擴充性服務可提供介面 toohello 無狀態的模型建立和部署使用 Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="433fc-137">Request-Response Service (RRS): A low latency, highly scalable service that provides an interface toohello stateless models created and deployed by using Machine Learning Studio.</span></span>
* <span data-ttu-id="433fc-138">批次執行服務 (BES)：這是一種非同步的服務，為一批資料記錄進行計分。</span><span class="sxs-lookup"><span data-stu-id="433fc-138">Batch Execution Service (BES): An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="433fc-139">有幾種方式 tooconsume hello REST API 及存取 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="433fc-139">There are several ways tooconsume hello REST API and access hello web service.</span></span> <span data-ttu-id="433fc-140">例如，您可以使用部署 hello web 服務時，為您產生 hello 範例程式碼，在 C#、 R、 Python 撰寫應用程式。</span><span class="sxs-lookup"><span data-stu-id="433fc-140">For example, you can write an application in C#, R, or Python by using hello sample code that's generated for you when you deployed hello web service.</span></span>

<span data-ttu-id="433fc-141">hello 範例程式碼位於：</span><span class="sxs-lookup"><span data-stu-id="433fc-141">hello sample code is available on:</span></span>
- <span data-ttu-id="433fc-142">hello hello Azure 機器學習 Web 服務入口網站中的 web 服務的 hello 取用頁面</span><span class="sxs-lookup"><span data-stu-id="433fc-142">hello Consume page for hello web service in hello Azure Machine Learning Web Services portal</span></span>
- <span data-ttu-id="433fc-143">hello web 服務儀表板 Machine Learning Studio 中的 hello API 說明頁面</span><span class="sxs-lookup"><span data-stu-id="433fc-143">hello API Help Page in hello web service dashboard in Machine Learning Studio</span></span>

<span data-ttu-id="433fc-144">您也可以使用 hello 範例 Microsoft Excel 活頁簿會為您建立，且可供 hello web 服務儀表板 Machine Learning Studio 中使用。</span><span class="sxs-lookup"><span data-stu-id="433fc-144">You can also use hello sample Microsoft Excel workbook that's created for you and is available in hello web service dashboard in Machine Learning Studio.</span></span>

<span data-ttu-id="433fc-145">**Hello 主要更新 tooAzure 機器學習服務有哪些？**</span><span class="sxs-lookup"><span data-stu-id="433fc-145">**What are hello main updates tooAzure Machine Learning?**</span></span>

<span data-ttu-id="433fc-146">Hello 最新的更新，請參閱[Azure Machine Learning 中最新消息](machine-learning-whats-new.md)。</span><span class="sxs-lookup"><span data-stu-id="433fc-146">For hello latest updates, see [What's new in Azure Machine Learning](machine-learning-whats-new.md).</span></span>

## <a name="machine-learning-studio-questions"></a><span data-ttu-id="433fc-147">Machine Learning Studio 問題</span><span class="sxs-lookup"><span data-stu-id="433fc-147">Machine Learning Studio questions</span></span>
### <a name="import-and-export-data-for-machine-learning"></a><span data-ttu-id="433fc-148">匯入和匯出 Machine Learning 的資料</span><span class="sxs-lookup"><span data-stu-id="433fc-148">Import and export data for Machine Learning</span></span>
<span data-ttu-id="433fc-149">**機器學習服務支援何種資料來源？**</span><span class="sxs-lookup"><span data-stu-id="433fc-149">**What data sources does Machine Learning support?**</span></span>

<span data-ttu-id="433fc-150">您可以下載資料 tooa Machine Learning Studio 實驗三種方式：</span><span class="sxs-lookup"><span data-stu-id="433fc-150">You can download data tooa Machine Learning Studio experiment in three ways:</span></span>

- <span data-ttu-id="433fc-151">以資料集的形式上傳本機檔案</span><span class="sxs-lookup"><span data-stu-id="433fc-151">Upload a local file as a dataset</span></span>
- <span data-ttu-id="433fc-152">使用模組 tooimport 資料從雲端資料服務</span><span class="sxs-lookup"><span data-stu-id="433fc-152">Use a module tooimport data from cloud data services</span></span>
- <span data-ttu-id="433fc-153">匯入從另一個實驗儲存的資料集</span><span class="sxs-lookup"><span data-stu-id="433fc-153">Import a dataset saved from another experiment</span></span>

<span data-ttu-id="433fc-154">toolearn 深入了解支援的檔案格式，請參閱[定型資料匯入至 Machine Learning Studio](machine-learning-data-science-import-data.md)。</span><span class="sxs-lookup"><span data-stu-id="433fc-154">toolearn more about supported file formats, see [Import training data into Machine Learning Studio](machine-learning-data-science-import-data.md).</span></span>

#### <span data-ttu-id="433fc-155"><a id="ModuleLimit"></a>大小可以 hello 資料集是適用於我的模組？</span><span class="sxs-lookup"><span data-stu-id="433fc-155"><a id="ModuleLimit"></a>How large can hello data set be for my modules?</span></span>
<span data-ttu-id="433fc-156">Machine Learning Studio 中的模組支援常見使用案例的總 too10 GB 的密集的數值資料的資料集。</span><span class="sxs-lookup"><span data-stu-id="433fc-156">Modules in Machine Learning Studio support datasets of up too10 GB of dense numerical data for common use cases.</span></span> <span data-ttu-id="433fc-157">如果模組在多個輸入，hello 10 GB 的值為 hello 的所有輸入的大小總計。</span><span class="sxs-lookup"><span data-stu-id="433fc-157">If a module takes more than one input, hello 10 GB value is hello total of all input sizes.</span></span> <span data-ttu-id="433fc-158">您也可以使用 Hive 或 Azure SQL Database 查詢來取樣較大型資料集，或者在擷取前使用「以計數學習」前置處理。</span><span class="sxs-lookup"><span data-stu-id="433fc-158">You can also sample larger datasets by using queries from Hive or Azure SQL Database, or you can use Learning by Counts preprocessing before ingestion.</span></span>  

<span data-ttu-id="433fc-159">hello 下列類型的資料可以展開 toolarger 資料集特徵正規化期間而且會超過 10 GB 的限制的 tooless:</span><span class="sxs-lookup"><span data-stu-id="433fc-159">hello following types of data can expand toolarger datasets during feature normalization and are limited tooless than 10 GB:</span></span>

* <span data-ttu-id="433fc-160">疏鬆</span><span class="sxs-lookup"><span data-stu-id="433fc-160">Sparse</span></span>
* <span data-ttu-id="433fc-161">類別</span><span class="sxs-lookup"><span data-stu-id="433fc-161">Categorical</span></span>
* <span data-ttu-id="433fc-162">字串</span><span class="sxs-lookup"><span data-stu-id="433fc-162">Strings</span></span>
* <span data-ttu-id="433fc-163">二進位資料</span><span class="sxs-lookup"><span data-stu-id="433fc-163">Binary data</span></span>

<span data-ttu-id="433fc-164">小於 10 GB 的限制的 toodatasets hello 下列模組︰</span><span class="sxs-lookup"><span data-stu-id="433fc-164">hello following modules are limited toodatasets less than 10 GB:</span></span>

* <span data-ttu-id="433fc-165">Recommender 模組</span><span class="sxs-lookup"><span data-stu-id="433fc-165">Recommender modules</span></span>
* <span data-ttu-id="433fc-166">合成少數類過採樣技術 (SMOTE) 模組</span><span class="sxs-lookup"><span data-stu-id="433fc-166">Synthetic Minority Oversampling Technique (SMOTE) module</span></span>
* <span data-ttu-id="433fc-167">指令碼模組：R、Python SQL</span><span class="sxs-lookup"><span data-stu-id="433fc-167">Scripting modules: R, Python, SQL</span></span>
* <span data-ttu-id="433fc-168">模組 hello 輸出的資料大小可能大於輸入的資料大小，例如聯結 」 或 「 特徵雜湊</span><span class="sxs-lookup"><span data-stu-id="433fc-168">Modules where hello output data size can be larger than input data size, such as Join or Feature Hashing</span></span>
* <span data-ttu-id="433fc-169">交叉驗證、 微調模型超、 序數迴歸和其中一個 vs 全部多級，hello 反覆項目數目很大時</span><span class="sxs-lookup"><span data-stu-id="433fc-169">Cross-validation, Tune Model Hyperparameters, Ordinal Regression, and One-vs-All Multiclass, when hello number of iterations is very large</span></span>

#### <span data-ttu-id="433fc-170"><a id="UploadLimit"></a>上傳資料的 hello 限制為何？</span><span class="sxs-lookup"><span data-stu-id="433fc-170"><a id="UploadLimit"></a>What are hello limits for data upload?</span></span>
<span data-ttu-id="433fc-171">對於大於幾個 Gb 的資料集上, 傳資料 tooAzure 儲存體或 Azure SQL Database，或使用 Azure HDInsight 而非直接從本機檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="433fc-171">For datasets that are larger than a couple GBs, upload data tooAzure Storage or Azure SQL Database, or use Azure HDInsight rather than directly uploading from a local file.</span></span>

<span data-ttu-id="433fc-172">**可以從 Amazon S3 讀取資料嗎？**</span><span class="sxs-lookup"><span data-stu-id="433fc-172">**Can I read data from Amazon S3?**</span></span>

<span data-ttu-id="433fc-173">如果您有小量的資料，並想 tooexpose 它透過 HTTP URL，則您可以使用 hello[匯入資料][ import-data]模組。</span><span class="sxs-lookup"><span data-stu-id="433fc-173">If you have a small amount of data and want tooexpose it via an HTTP URL, then you can use hello [Import Data][import-data] module.</span></span> <span data-ttu-id="433fc-174">大量資料，將它傳輸 tooAzure 儲存體第一次，然後再使用 hello[匯入資料][ import-data]模組 toobring 到您的經驗。</span><span class="sxs-lookup"><span data-stu-id="433fc-174">For larger amounts of data, transfer it tooAzure Storage first, and then use hello [Import Data][import-data] module toobring it into your experiment.</span></span>
<!--

<SEE CLOUD DS PROCESS>
-->

<span data-ttu-id="433fc-175">**有內建的影像輸入功能嗎？**</span><span class="sxs-lookup"><span data-stu-id="433fc-175">**Is there a built-in image input capability?**</span></span>

<span data-ttu-id="433fc-176">您可以了解映像輸入 hello 功能[匯入映像][ image-reader]參考。</span><span class="sxs-lookup"><span data-stu-id="433fc-176">You can learn about image input capability in hello [Import Images][image-reader] reference.</span></span>

### <a name="modules"></a><span data-ttu-id="433fc-177">模組</span><span class="sxs-lookup"><span data-stu-id="433fc-177">Modules</span></span>
<span data-ttu-id="433fc-178">**hello 演算法、 資料來源、 資料格式或我正在尋找的資料轉換作業不在 Azure Machine Learning Studio。我有哪些選擇？**</span><span class="sxs-lookup"><span data-stu-id="433fc-178">**hello algorithm, data source, data format, or data transformation operation that I am looking for isn't in Azure Machine Learning Studio. What are my options?**</span></span>

<span data-ttu-id="433fc-179">您可以移 toohello[使用者意見反應論壇](http://go.microsoft.com/fwlink/?LinkId=404231)toosee 功能會要求我們追蹤。</span><span class="sxs-lookup"><span data-stu-id="433fc-179">You can go toohello [user feedback forum](http://go.microsoft.com/fwlink/?LinkId=404231) toosee feature requests that we are tracking.</span></span> <span data-ttu-id="433fc-180">如果已經要求您要尋找的功能，請加入您投票 tooa 的要求。</span><span class="sxs-lookup"><span data-stu-id="433fc-180">Add your vote tooa request if a capability that you're looking for has already been requested.</span></span> <span data-ttu-id="433fc-181">如果您要尋找的 hello 功能不存在，請建立新的要求。</span><span class="sxs-lookup"><span data-stu-id="433fc-181">If hello capability that you're looking for doesn't exist, create a new request.</span></span> <span data-ttu-id="433fc-182">您可以在此論壇中太檢視 hello 要求的狀態。</span><span class="sxs-lookup"><span data-stu-id="433fc-182">You can view hello status of your request in this forum, too.</span></span> <span data-ttu-id="433fc-183">我們會追蹤這份清單，並經常更新的功能可用性的 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="433fc-183">We track this list closely and update hello status of feature availability frequently.</span></span> <span data-ttu-id="433fc-184">此外，您可以使用 hello 內建支援 R，並將 Python toocreate 自訂轉換時所需。</span><span class="sxs-lookup"><span data-stu-id="433fc-184">In addition, you can use hello built-in support for R and Python toocreate custom transformations when needed.</span></span>

<span data-ttu-id="433fc-185">**是否可將我現有的程式碼放入 Machine Learning Studio 中？**</span><span class="sxs-lookup"><span data-stu-id="433fc-185">**Can I bring my existing code into Machine Learning Studio?**</span></span>

<span data-ttu-id="433fc-186">，您可以將現有的 R 或 Python 程式碼帶入 Machine Learning Studio 中，在 hello 相同試驗 Azure Machine Learning 學習模組，並將 hello 方案部署為 web 服務透過 Azure Machine Learning 中執行。</span><span class="sxs-lookup"><span data-stu-id="433fc-186">Yes, you can bring your existing R or Python code into Machine Learning Studio, run it in hello same experiment with Azure Machine Learning learners, and deploy hello solution as a web service via Azure Machine Learning.</span></span> <span data-ttu-id="433fc-187">如需詳細資訊，請參閱[透過 R 擴展您的實驗](machine-learning-extend-your-experiment-with-r.md)和[在 Azure Machine Learning Studio 中執行 Python 機器學習服務指令碼](machine-learning-execute-python-scripts.md)。</span><span class="sxs-lookup"><span data-stu-id="433fc-187">For more information, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md) and [Execute Python machine learning scripts in Azure Machine Learning Studio](machine-learning-execute-python-scripts.md).</span></span>

<span data-ttu-id="433fc-188">**它是類似的可能 toouse [PMML](http://en.wikipedia.org/wiki/Predictive_Model_Markup_Language) toodefine 模型嗎？**</span><span class="sxs-lookup"><span data-stu-id="433fc-188">**Is it possible toouse something like [PMML](http://en.wikipedia.org/wiki/Predictive_Model_Markup_Language) toodefine a model?**</span></span>

<span data-ttu-id="433fc-189">否，不支援預測模型標記語言 (PMML)。</span><span class="sxs-lookup"><span data-stu-id="433fc-189">No, Predictive Model Markup Language (PMML) is not supported.</span></span> <span data-ttu-id="433fc-190">您可以使用自訂 R 和 Python 程式碼 toodefine 模組。</span><span class="sxs-lookup"><span data-stu-id="433fc-190">You can use custom R and Python code toodefine a module.</span></span>

<span data-ttu-id="433fc-191">**在我的實驗中可以平行執行多少個模組？**</span><span class="sxs-lookup"><span data-stu-id="433fc-191">**How many modules can I execute in parallel in my experiment?**</span></span>  

<span data-ttu-id="433fc-192">您可以執行 toofour 模組，以平行方式在實驗中。</span><span class="sxs-lookup"><span data-stu-id="433fc-192">You can execute up toofour modules in parallel in an experiment.</span></span>

### <a name="data-processing"></a><span data-ttu-id="433fc-193">資料處理</span><span class="sxs-lookup"><span data-stu-id="433fc-193">Data processing</span></span>
<span data-ttu-id="433fc-194">**是否有能力 toovisualize 資料 （除了 R 視覺效果） 以互動方式在 hello 實驗？**</span><span class="sxs-lookup"><span data-stu-id="433fc-194">**Is there an ability toovisualize data (beyond R visualizations) interactively within hello experiment?**</span></span>

<span data-ttu-id="433fc-195">按一下 hello 輸出的模組 toovisualize hello 資料及取得統計資料。</span><span class="sxs-lookup"><span data-stu-id="433fc-195">Click hello output of a module toovisualize hello data and get statistics.</span></span>

<span data-ttu-id="433fc-196">**當在預覽結果或在瀏覽器中的資料，資料列和資料行的 hello 數目是限定的。原因為何？**</span><span class="sxs-lookup"><span data-stu-id="433fc-196">**When previewing results or data in a browser, hello number of rows and columns is limited. Why?**</span></span>

<span data-ttu-id="433fc-197">因為大量資料可能會傳送 tooa 瀏覽器，資料大小不受限的 tooprevent 減緩 Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="433fc-197">Because large amounts of data might be sent tooa browser, data size is limited tooprevent slowing down Machine Learning Studio.</span></span> <span data-ttu-id="433fc-198">toovisualize 所有 hello 資料/結果中，它的較佳 toodownload hello 資料，並使用 Excel 或其他工具。</span><span class="sxs-lookup"><span data-stu-id="433fc-198">toovisualize all hello data/results, it's better toodownload hello data and use Excel or another tool.</span></span>

### <a name="algorithms"></a><span data-ttu-id="433fc-199">演算法</span><span class="sxs-lookup"><span data-stu-id="433fc-199">Algorithms</span></span>
<span data-ttu-id="433fc-200">**Machine Learning Studio 中支援哪些現有的演算法？**</span><span class="sxs-lookup"><span data-stu-id="433fc-200">**What existing algorithms are supported in Machine Learning Studio?**</span></span>

<span data-ttu-id="433fc-201">Machine Learning Studio 提供頂級演算法，例如 Scalable Boosted Decision 樹、Bayesian Recommendation 系統、Deep Neural Networks 和 Decision Jungles (由 Microsoft Research 開發)。</span><span class="sxs-lookup"><span data-stu-id="433fc-201">Machine Learning Studio provides state-of-the-art algorithms, such as Scalable Boosted Decision trees, Bayesian Recommendation systems, Deep Neural Networks, and Decision Jungles developed at Microsoft Research.</span></span> <span data-ttu-id="433fc-202">此外也包含可調整的開放原始碼機器學習套件，例如 Vowpal Wabbit。</span><span class="sxs-lookup"><span data-stu-id="433fc-202">Scalable open-source machine learning packages, like Vowpal Wabbit, are also included.</span></span> <span data-ttu-id="433fc-203">Machine Learning Studio 支援多類別與二進位分類、迴歸和叢集的機器學習演算法。</span><span class="sxs-lookup"><span data-stu-id="433fc-203">Machine Learning Studio supports machine learning algorithms for multiclass and binary classification, regression, and clustering.</span></span> <span data-ttu-id="433fc-204">請參閱 hello 的完整清單[機器學習模組][machine-learning-modules]。</span><span class="sxs-lookup"><span data-stu-id="433fc-204">See hello complete list of [Machine Learning Modules][machine-learning-modules].</span></span>

<span data-ttu-id="433fc-205">**您會自動建議 hello 右機器學習演算法 toouse 提供我的資料嗎？**</span><span class="sxs-lookup"><span data-stu-id="433fc-205">**Do you automatically suggest hello right Machine Learning algorithm toouse for my data?**</span></span>

<span data-ttu-id="433fc-206">否，但 Machine Learning Studio 有的幾個 toocompare hello 結果的每個演算法 toodetermine hello 適合您的問題。</span><span class="sxs-lookup"><span data-stu-id="433fc-206">No, but Machine Learning Studio has various ways toocompare hello results of each algorithm toodetermine hello right one for your problem.</span></span>

<span data-ttu-id="433fc-207">**您是否有任何一種演算法挑選透過另一個則針對提供的 hello 演算法的指導方針？**</span><span class="sxs-lookup"><span data-stu-id="433fc-207">**Do you have any guidelines on picking one algorithm over another for hello provided algorithms?**</span></span>

<span data-ttu-id="433fc-208">請參閱[如何 toochoose 演算法](machine-learning-algorithm-choice.md)。</span><span class="sxs-lookup"><span data-stu-id="433fc-208">See [How toochoose an algorithm](machine-learning-algorithm-choice.md).</span></span>

<span data-ttu-id="433fc-209">**提供的 hello 演算法或撰寫的 R Python 嗎？**</span><span class="sxs-lookup"><span data-stu-id="433fc-209">**Are hello provided algorithms written in R or Python?**</span></span>

<span data-ttu-id="433fc-210">否，這些演算法通常會寫入編譯語言 tooprovide 較佳的效能。</span><span class="sxs-lookup"><span data-stu-id="433fc-210">No, these algorithms are mostly written in compiled languages tooprovide better performance.</span></span>

<span data-ttu-id="433fc-211">**是任何 hello 所提供的演算法的詳細資料？**</span><span class="sxs-lookup"><span data-stu-id="433fc-211">**Are any details of hello algorithms provided?**</span></span>

<span data-ttu-id="433fc-212">hello 文件提供一些資訊 hello 演算法並進行微調的參數會描述的 toooptimize hello 演算法，您可以使用。</span><span class="sxs-lookup"><span data-stu-id="433fc-212">hello documentation provides some information about hello algorithms and parameters for tuning are described toooptimize hello algorithm for your use.</span></span>  

<span data-ttu-id="433fc-213">**線上學習是否有任何支援？**</span><span class="sxs-lookup"><span data-stu-id="433fc-213">**Is there any support for online learning?**</span></span>

<span data-ttu-id="433fc-214">否，目前只支援以程式設計方式進行重新訓練。</span><span class="sxs-lookup"><span data-stu-id="433fc-214">No, currently only programmatic retraining is supported.</span></span>

<span data-ttu-id="433fc-215">**可以使用內建模組的 hello 視覺化 hello 圖層的類神經網路模型嗎？**</span><span class="sxs-lookup"><span data-stu-id="433fc-215">**Can I visualize hello layers of a Neural Net Model by using hello built-in module?**</span></span>

<span data-ttu-id="433fc-216">否。</span><span class="sxs-lookup"><span data-stu-id="433fc-216">No.</span></span>

<span data-ttu-id="433fc-217">**可以以 C# 或其他語言建立自己的模組嗎？**</span><span class="sxs-lookup"><span data-stu-id="433fc-217">**Can I create my own modules in C# or some other language?**</span></span>

<span data-ttu-id="433fc-218">目前，您可以只使用 R toocreate 新自訂模組。</span><span class="sxs-lookup"><span data-stu-id="433fc-218">Currently, you can only use R toocreate new custom modules.</span></span>

### <a name="r-module"></a><span data-ttu-id="433fc-219">R 模組</span><span class="sxs-lookup"><span data-stu-id="433fc-219">R module</span></span>
<span data-ttu-id="433fc-220">**Machine Learning Studio 中可使用什麼 R 套件？**</span><span class="sxs-lookup"><span data-stu-id="433fc-220">**What R packages are available in Machine Learning Studio?**</span></span>

<span data-ttu-id="433fc-221">Machine Learning Studio 支援超過 400 CRAN R 封裝，並如下 hello[目前清單](http://az754797.vo.msecnd.net/docs/RPackages.xlsx)所有包含的封裝。</span><span class="sxs-lookup"><span data-stu-id="433fc-221">Machine Learning Studio supports more than 400 CRAN R packages today, and here is hello [current list](http://az754797.vo.msecnd.net/docs/RPackages.xlsx) of all included packages.</span></span> <span data-ttu-id="433fc-222">此外，請參閱[擴充以 R 實驗](machine-learning-extend-your-experiment-with-r.md)toolearn 如何 tooretrieve 這樣列出自己。</span><span class="sxs-lookup"><span data-stu-id="433fc-222">Also, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md) toolearn how tooretrieve this list yourself.</span></span> <span data-ttu-id="433fc-223">如果您想要的 hello 封裝不是這份清單中，提供在 hello hello 套件 hello 名稱[使用者意見反應論壇](http://go.microsoft.com/fwlink/?LinkId=404231)。</span><span class="sxs-lookup"><span data-stu-id="433fc-223">If hello package that you want is not in this list, provide hello name of hello package at hello [user feedback forum](http://go.microsoft.com/fwlink/?LinkId=404231).</span></span>

<span data-ttu-id="433fc-224">**它是可能 toobuild 自訂 R 模組嗎？**</span><span class="sxs-lookup"><span data-stu-id="433fc-224">**Is it possible toobuild a custom R module?**</span></span>

<span data-ttu-id="433fc-225">是，如需詳細資訊，請參閱 [在 Azure Machine Learning 中撰寫自訂 R 模組](machine-learning-custom-r-modules.md) 。</span><span class="sxs-lookup"><span data-stu-id="433fc-225">Yes, see [Author custom R modules in Azure Machine Learning](machine-learning-custom-r-modules.md) for more information.</span></span>

<span data-ttu-id="433fc-226">**是否有 R 適用的 REPL 環境？**</span><span class="sxs-lookup"><span data-stu-id="433fc-226">**Is there a REPL environment for R?**</span></span>

<span data-ttu-id="433fc-227">否，沒有 hello studio 中的 R 的任何讀取 Eval-列印-迴圈 (REPL) 環境。</span><span class="sxs-lookup"><span data-stu-id="433fc-227">No, there is no Read-Eval-Print-Loop (REPL) environment for R in hello studio.</span></span>

### <a name="python-module"></a><span data-ttu-id="433fc-228">Python 模組</span><span class="sxs-lookup"><span data-stu-id="433fc-228">Python module</span></span>
<span data-ttu-id="433fc-229">**它是可能 toobuild 自訂 Python 模組嗎？**</span><span class="sxs-lookup"><span data-stu-id="433fc-229">**Is it possible toobuild a custom Python module?**</span></span>

<span data-ttu-id="433fc-230">目前不可以，但是您可以使用一或多個[執行 Python 指令碼][ python]模組 tooget hello 相同的結果。</span><span class="sxs-lookup"><span data-stu-id="433fc-230">Not currently, but you can use one or more [Execute Python Script][python] modules tooget hello same result.</span></span>

<span data-ttu-id="433fc-231">**是否有 Python 適用的 REPL 環境？**</span><span class="sxs-lookup"><span data-stu-id="433fc-231">**Is there a REPL environment for Python?**</span></span>

<span data-ttu-id="433fc-232">您可以使用 hello Jupyter 筆記本 Machine Learning Studio 中。</span><span class="sxs-lookup"><span data-stu-id="433fc-232">You can use hello Jupyter Notebooks in Machine Learning Studio.</span></span> <span data-ttu-id="433fc-233">如需詳細資訊，請參閱 [介紹 Azure Machine Learning Studio 中的 Jupyter Notebook](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx)。</span><span class="sxs-lookup"><span data-stu-id="433fc-233">For more information, see [Introducing Jupyter Notebooks in Azure Machine Learning Studio](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>

## <a name="web-service"></a><span data-ttu-id="433fc-234">Web 服務</span><span class="sxs-lookup"><span data-stu-id="433fc-234">Web service</span></span>
### <a name="retrain"></a><span data-ttu-id="433fc-235">重新訓練</span><span class="sxs-lookup"><span data-stu-id="433fc-235">Retrain</span></span>
<span data-ttu-id="433fc-236">**如何以程式設計方式重新訓練 Azure Machine Learning 模型？**</span><span class="sxs-lookup"><span data-stu-id="433fc-236">**How do I retrain Azure Machine Learning models programmatically?**</span></span>

<span data-ttu-id="433fc-237">使用 hello 重新訓練應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="433fc-237">Use hello retraining APIs.</span></span> <span data-ttu-id="433fc-238">如需詳細資訊，請參閱 [以程式設計方式重塑機器學習模型](machine-learning-retrain-models-programmatically.md)。</span><span class="sxs-lookup"><span data-stu-id="433fc-238">For more information, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> <span data-ttu-id="433fc-239">範例程式碼也會提供 hello [Microsoft Azure 機器學習重新訓練的示範](https://azuremlretrain.codeplex.com/)。</span><span class="sxs-lookup"><span data-stu-id="433fc-239">Sample code is also available in hello [Microsoft Azure Machine Learning Retraining Demo](https://azuremlretrain.codeplex.com/).</span></span>

### <a name="create"></a><span data-ttu-id="433fc-240">建立</span><span class="sxs-lookup"><span data-stu-id="433fc-240">Create</span></span>
<span data-ttu-id="433fc-241">**在本機或在沒有網際網路連線的應用程式可以部署 hello 模型嗎？**</span><span class="sxs-lookup"><span data-stu-id="433fc-241">**Can I deploy hello model locally or in an application that doesn't have an Internet connection?**</span></span>

<span data-ttu-id="433fc-242">否。</span><span class="sxs-lookup"><span data-stu-id="433fc-242">No.</span></span>

<span data-ttu-id="433fc-243">**所有 Web 服務是否有預期的基準延遲？**</span><span class="sxs-lookup"><span data-stu-id="433fc-243">**Is there a baseline latency that is expected for all web services?**</span></span>

<span data-ttu-id="433fc-244">請參閱 hello [Azure 訂用帳戶限制](../azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="433fc-244">See hello [Azure subscription limits](../azure-subscription-service-limits.md).</span></span>

### <a name="use"></a><span data-ttu-id="433fc-245">使用</span><span class="sxs-lookup"><span data-stu-id="433fc-245">Use</span></span>
<span data-ttu-id="433fc-246">**何時需要 toorun 我預測模型以批次執行的要求回應服務與服務？**</span><span class="sxs-lookup"><span data-stu-id="433fc-246">**When would I want toorun my predictive model as a Batch Execution service versus a Request Response service?**</span></span>

<span data-ttu-id="433fc-247">hello 的要求回應服務 (RR) 是低延遲、 高延展的 web 服務，使用的 tooprovide 介面 toostateless 模型所建立和部署從 hello 實驗環境。</span><span class="sxs-lookup"><span data-stu-id="433fc-247">hello Request Response service (RRS) is a low-latency, high-scale web service that is used tooprovide an interface toostateless models that are created and deployed from hello experimentation environment.</span></span> <span data-ttu-id="433fc-248">hello 批次執行服務 (BES) 是一項服務，以非同步方式分數資料記錄的批次。</span><span class="sxs-lookup"><span data-stu-id="433fc-248">hello Batch Execution service (BES) is a service that asynchronously scores a batch of data records.</span></span> <span data-ttu-id="433fc-249">hello BES 為輸入，例如 RR 使用的資料輸入。</span><span class="sxs-lookup"><span data-stu-id="433fc-249">hello input for BES is like data input that RRS uses.</span></span> <span data-ttu-id="433fc-250">hello 主要差異是 BES 會從各種來源，例如 Azure Blob 儲存體、 Azure 資料表儲存體、 Azure SQL Database、 HDInsight （hive 查詢） 和 HTTP 的來源讀取之記錄區塊。</span><span class="sxs-lookup"><span data-stu-id="433fc-250">hello main difference is that BES reads a block of records from a variety of sources, such as Azure Blob storage, Azure Table storage, Azure SQL Database, HDInsight (hive query), and HTTP sources.</span></span> <span data-ttu-id="433fc-251">如需詳細資訊，請參閱[如何 tooconsume Azure 機器學習 Web 服務](machine-learning-consume-web-services.md)。</span><span class="sxs-lookup"><span data-stu-id="433fc-251">For more information, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

<span data-ttu-id="433fc-252">**如何更新部署的 hello web 服務的 hello 模型？**</span><span class="sxs-lookup"><span data-stu-id="433fc-252">**How do I update hello model for hello deployed web service?**</span></span>

<span data-ttu-id="433fc-253">tooupdate 預測模型已部署的服務，修改並重新執行您用 tooauthor hello 實驗，並儲存 hello 定型的模型。</span><span class="sxs-lookup"><span data-stu-id="433fc-253">tooupdate a predictive model for an already deployed service, modify and rerun hello experiment that you used tooauthor and save hello trained model.</span></span> <span data-ttu-id="433fc-254">您擁有 hello 定型的模型可用的新版本之後，Machine Learning Studio 詢問您是否 tooupdate web 服務。</span><span class="sxs-lookup"><span data-stu-id="433fc-254">After you have a new version of hello trained model available, Machine Learning Studio asks you if you want tooupdate your web service.</span></span> <span data-ttu-id="433fc-255">如需詳細資訊，關於如何 tooupdate 已部署的 web 服務，請參閱[部署機器學習 web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="433fc-255">For details about how tooupdate a deployed web service, see [Deploy a Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="433fc-256">您也可以使用 hello Retraining 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="433fc-256">You can also use hello Retraining APIs.</span></span>
<span data-ttu-id="433fc-257">如需詳細資訊，請參閱 [以程式設計方式重塑機器學習模型](machine-learning-retrain-models-programmatically.md)。</span><span class="sxs-lookup"><span data-stu-id="433fc-257">For more information, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> <span data-ttu-id="433fc-258">範例程式碼也會提供 hello [Microsoft Azure 機器學習重新訓練的示範](https://azuremlretrain.codeplex.com/)。</span><span class="sxs-lookup"><span data-stu-id="433fc-258">Sample code is also available in hello [Microsoft Azure Machine Learning Retraining Demo](https://azuremlretrain.codeplex.com/).</span></span>

<span data-ttu-id="433fc-259">**如何監控部署在實際執行環境中的 Web 服務？**</span><span class="sxs-lookup"><span data-stu-id="433fc-259">**How do I monitor my web service deployed in production?**</span></span>

<span data-ttu-id="433fc-260">部署的預測模型之後，您就可以監視從 hello Azure 傳統入口網站 （僅傳統 web 服務） 或 hello Azure 機器學習 Web 服務網站。</span><span class="sxs-lookup"><span data-stu-id="433fc-260">After you deploy a predictive model, you can monitor it from hello Azure classic portal (Classic web services only) or hello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="433fc-261">每個已部署的服務都有其本身的儀表板，您可以在此處檢視該服務的監控資訊。</span><span class="sxs-lookup"><span data-stu-id="433fc-261">Each deployed service has its own dashboard where you can see monitoring information for that service.</span></span> <span data-ttu-id="433fc-262">如需有關如何 toomanage 已部署的 web 服務，請參閱[管理 Web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)和[管理 Azure Machine Learning 工作區](machine-learning-manage-workspace.md)。</span><span class="sxs-lookup"><span data-stu-id="433fc-262">For more information about how toomanage your deployed web services, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) and [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>

<span data-ttu-id="433fc-263">**有我可以在其中看到我的 RR/BES hello 輸出的位置嗎？**</span><span class="sxs-lookup"><span data-stu-id="433fc-263">**Is there a place where I can see hello output of my RRS/BES?**</span></span>

<span data-ttu-id="433fc-264">RR，如 hello web 服務回應通常是在您看到 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="433fc-264">For RRS, hello web service response is typically where you see hello result.</span></span> <span data-ttu-id="433fc-265">您也可以撰寫它 tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="433fc-265">You can also write it tooAzure Blob storage.</span></span> <span data-ttu-id="433fc-266">BES，如 hello 輸出都會寫入 tooa blob，根據預設。</span><span class="sxs-lookup"><span data-stu-id="433fc-266">For BES, hello output is written tooa blob by default.</span></span> <span data-ttu-id="433fc-267">您也可以撰寫 hello 輸出 tooa 資料庫或資料表，使用 hello[匯出資料][ export-data]模組。</span><span class="sxs-lookup"><span data-stu-id="433fc-267">You can also write hello output tooa database or table by using hello [Export Data][export-data] module.</span></span>

<span data-ttu-id="433fc-268">**只能從 Machine Learning Studio 中建立的模型來建立 Web 服務嗎？**</span><span class="sxs-lookup"><span data-stu-id="433fc-268">**Can I create web services only from models that were created in Machine Learning Studio?**</span></span>

<span data-ttu-id="433fc-269">不，您也可以直接使用 Jupyter Notebook 和 RStudio 來建立 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="433fc-269">No, you can also create web services directly by using Jupyter Notebooks and RStudio.</span></span>

<span data-ttu-id="433fc-270">**哪裡可以找到有關錯誤碼的詳細資訊？**</span><span class="sxs-lookup"><span data-stu-id="433fc-270">**Where can I find information about error codes?**</span></span>

<span data-ttu-id="433fc-271">如需錯誤碼與說明的清單，請參閱 [Machine Learning 模組錯誤碼](https://msdn.microsoft.com/library/azure/dn905910.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="433fc-271">See [Machine Learning Module Error Codes](https://msdn.microsoft.com/library/azure/dn905910.aspx) for a list of error codes and descriptions.</span></span>

## <a name="scalability"></a><span data-ttu-id="433fc-272">延展性</span><span class="sxs-lookup"><span data-stu-id="433fc-272">Scalability</span></span>
<span data-ttu-id="433fc-273">**什麼是 hello 延展性 hello web 服務？**</span><span class="sxs-lookup"><span data-stu-id="433fc-273">**What is hello scalability of hello web service?**</span></span>

<span data-ttu-id="433fc-274">目前，hello 預設端點的佈建 20 並行 RR 要求每個端點。</span><span class="sxs-lookup"><span data-stu-id="433fc-274">Currently, hello default endpoint is provisioned with 20 concurrent RRS requests per endpoint.</span></span> <span data-ttu-id="433fc-275">您可以調整每個端點，這個 too200 並行要求，而且您可以延展中所述的每個 web 服務 too10、 000 每個 web 服務端點[擴充 Web 服務](machine-learning-scaling-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="433fc-275">You can scale this too200 concurrent requests per endpoint, and you can scale each web service too10,000 endpoints per web service as described in [Scaling a Web Service](machine-learning-scaling-webservice.md).</span></span> <span data-ttu-id="433fc-276">對於 BES，每個端點一次可以處理 40 個要求，超過 40 個的其他要求則會排入佇列。</span><span class="sxs-lookup"><span data-stu-id="433fc-276">For BES, each endpoint can process 40 requests at a time, and additional requests beyond 40 requests are queued.</span></span> <span data-ttu-id="433fc-277">這些佇列的要求會自動以 hello 佇列電量。</span><span class="sxs-lookup"><span data-stu-id="433fc-277">These queued requests run automatically as hello queue drains.</span></span>

<span data-ttu-id="433fc-278">**R 作業會分散於節點嗎？**</span><span class="sxs-lookup"><span data-stu-id="433fc-278">**Are R jobs spread across nodes?**</span></span>

<span data-ttu-id="433fc-279">編號</span><span class="sxs-lookup"><span data-stu-id="433fc-279">No.</span></span>  

<span data-ttu-id="433fc-280">**我可以將多少資料用於訓練？**</span><span class="sxs-lookup"><span data-stu-id="433fc-280">**How much data can I use for training?**</span></span>

<span data-ttu-id="433fc-281">Machine Learning Studio 中的模組支援常見使用案例的總 too10 GB 的密集的數值資料的資料集。</span><span class="sxs-lookup"><span data-stu-id="433fc-281">Modules in Machine Learning Studio support datasets of up too10 GB of dense numerical data for common use cases.</span></span> <span data-ttu-id="433fc-282">如果模組需要一個以上的輸入，hello 總所有輸入的大小為 10 GB。</span><span class="sxs-lookup"><span data-stu-id="433fc-282">If a module takes more than one input, hello total size for all inputs is 10 GB.</span></span> <span data-ttu-id="433fc-283">您也可以取樣較大型資料集，方法是透過 Hive 查詢或 Azure SQL Database 查詢，或在擷取前利用[以計數學習][counts]模組進行前置處理。</span><span class="sxs-lookup"><span data-stu-id="433fc-283">You can also sample larger datasets via Hive queries, via Azure SQL Database queries, or by preprocessing with [Learning with Counts][counts] modules before ingestion.</span></span>  

<span data-ttu-id="433fc-284">hello 下列類型的資料可以展開 toolarger 資料集特徵正規化期間而且會超過 10 GB 的限制的 tooless:</span><span class="sxs-lookup"><span data-stu-id="433fc-284">hello following types of data can expand toolarger datasets during feature normalization and are limited tooless than 10 GB:</span></span>

* <span data-ttu-id="433fc-285">疏鬆</span><span class="sxs-lookup"><span data-stu-id="433fc-285">Sparse</span></span>
* <span data-ttu-id="433fc-286">類別</span><span class="sxs-lookup"><span data-stu-id="433fc-286">Categorical</span></span>
* <span data-ttu-id="433fc-287">字串</span><span class="sxs-lookup"><span data-stu-id="433fc-287">Strings</span></span>
* <span data-ttu-id="433fc-288">二進位資料</span><span class="sxs-lookup"><span data-stu-id="433fc-288">Binary data</span></span>

<span data-ttu-id="433fc-289">小於 10 GB 的限制的 toodatasets hello 下列模組︰</span><span class="sxs-lookup"><span data-stu-id="433fc-289">hello following modules are limited toodatasets less than 10 GB:</span></span>

* <span data-ttu-id="433fc-290">Recommender 模組</span><span class="sxs-lookup"><span data-stu-id="433fc-290">Recommender modules</span></span>
* <span data-ttu-id="433fc-291">合成少數類過採樣技術 (SMOTE) 模組</span><span class="sxs-lookup"><span data-stu-id="433fc-291">Synthetic Minority Oversampling Technique (SMOTE) module</span></span>
* <span data-ttu-id="433fc-292">指令碼模組：R、Python SQL</span><span class="sxs-lookup"><span data-stu-id="433fc-292">Scripting modules: R, Python, SQL</span></span>
* <span data-ttu-id="433fc-293">模組 hello 輸出的資料大小可能大於輸入的資料大小，例如聯結 」 或 「 特徵雜湊</span><span class="sxs-lookup"><span data-stu-id="433fc-293">Modules where hello output data size can be larger than input data size, such as Join or Feature Hashing</span></span>
* <span data-ttu-id="433fc-294">當反覆運算數目非常大時的交叉驗證、微調模型超參數、序數迴歸和一對多的多類別</span><span class="sxs-lookup"><span data-stu-id="433fc-294">Cross-Validate, Tune Model Hyperparameters, Ordinal Regression, and One-vs-All Multiclass, when number of iterations is very large</span></span>

<span data-ttu-id="433fc-295">對於大於幾個 Gb 的資料集上, 傳資料 tooAzure 儲存體或 Azure SQL Database，或使用 HDInsight 而非直接從本機檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="433fc-295">For datasets that are larger than a few GBs, upload data tooAzure Storage or Azure SQL Database, or use HDInsight rather than directly uploading from a local file.</span></span>

<span data-ttu-id="433fc-296">**是否有任何向量大小限制嗎？**</span><span class="sxs-lookup"><span data-stu-id="433fc-296">**Are there any vector size limitations?**</span></span>

<span data-ttu-id="433fc-297">資料列和資料行是每個限制的 toohello.NET 的限制上限 Int: 2147483647。</span><span class="sxs-lookup"><span data-stu-id="433fc-297">Rows and columns are each limited toohello .NET limitation of Max Int: 2,147,483,647.</span></span>

<span data-ttu-id="433fc-298">**是否可以調整 hello hello 執行 hello web 服務的虛擬機器的大小？**</span><span class="sxs-lookup"><span data-stu-id="433fc-298">**Can I adjust hello size of hello virtual machine that runs hello web service?**</span></span>

<span data-ttu-id="433fc-299">否。</span><span class="sxs-lookup"><span data-stu-id="433fc-299">No.</span></span>  

## <a name="security-and-availability"></a><span data-ttu-id="433fc-300">安全性和可用性</span><span class="sxs-lookup"><span data-stu-id="433fc-300">Security and availability</span></span>
<span data-ttu-id="433fc-301">**根據預設，誰可以存取 hello web 服務的 hello http 端點？我要如何限制存取 toohello 端點？**</span><span class="sxs-lookup"><span data-stu-id="433fc-301">**Who can access hello http endpoint for hello web service by default? How do I restrict access toohello endpoint?**</span></span>

<span data-ttu-id="433fc-302">部署 Web 服務之後，我們會建立該服務的預設端點。</span><span class="sxs-lookup"><span data-stu-id="433fc-302">After a web service is deployed, a default endpoint is created for that service.</span></span> <span data-ttu-id="433fc-303">使用其 API 金鑰，可以呼叫 hello 預設端點。</span><span class="sxs-lookup"><span data-stu-id="433fc-303">hello default endpoint can be called by using its API key.</span></span> <span data-ttu-id="433fc-304">您可以加入多個端點，其中包含自己索引鍵從 hello Azure 傳統入口網站或以程式設計方式使用 hello Web 服務管理 Api。</span><span class="sxs-lookup"><span data-stu-id="433fc-304">You can add more endpoints with their own keys from hello Azure classic portal or programmatically by using hello Web Service Management APIs.</span></span> <span data-ttu-id="433fc-305">存取金鑰都是必要的 toomake 呼叫 toohello web 服務。</span><span class="sxs-lookup"><span data-stu-id="433fc-305">Access keys are needed toomake calls toohello web service.</span></span> <span data-ttu-id="433fc-306">如需詳細資訊，請參閱[如何 tooconsume Azure 機器學習 Web 服務](machine-learning-consume-web-services.md)。</span><span class="sxs-lookup"><span data-stu-id="433fc-306">For more information, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

<span data-ttu-id="433fc-307">**如果找不到我的 Azure 儲存體帳戶，會發生什麼情況？**</span><span class="sxs-lookup"><span data-stu-id="433fc-307">**What happens if my Azure storage account can't be found?**</span></span>

<span data-ttu-id="433fc-308">Machine Learning Studio 依賴使用者提供 Azure 儲存體帳戶 toosave 中繼資料時，它會執行 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="433fc-308">Machine Learning Studio relies on a user-supplied Azure storage account toosave intermediary data when it executes hello workflow.</span></span> <span data-ttu-id="433fc-309">在建立的工作區時，這個儲存體帳戶會提供 tooMachine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="433fc-309">This storage account is provided tooMachine Learning Studio when a workspace is created.</span></span> <span data-ttu-id="433fc-310">Hello 後會建立工作區中，如果 hello 儲存體帳戶刪除不再找到、 hello 工作區將會停止運作，且所有實驗，區將會失敗。</span><span class="sxs-lookup"><span data-stu-id="433fc-310">After hello workspace is created, if hello storage account is deleted and can no longer be found, hello workspace will stop functioning, and all experiments in that workspace will fail.</span></span>

<span data-ttu-id="433fc-311">如果您不小心刪除 hello 儲存體帳戶，來重新建立 hello 儲存體帳戶，以相同的名稱，在 hello hello hello 與相同的區域刪除儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="433fc-311">If you accidentally deleted hello storage account, recreate hello storage account with hello same name in hello same region as hello deleted storage account.</span></span> <span data-ttu-id="433fc-312">在這之後，重新同步處理 hello 存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="433fc-312">After that, resync hello access key.</span></span>

<span data-ttu-id="433fc-313">**如果我的儲存體帳戶存取金鑰未同步，會發生什麼情況？**</span><span class="sxs-lookup"><span data-stu-id="433fc-313">**What happens if my storage account access key is out of sync?**</span></span>

<span data-ttu-id="433fc-314">Machine Learning Studio 依賴使用者提供 Azure 儲存體帳戶 toostore 中繼資料時，它會執行 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="433fc-314">Machine Learning Studio relies on a user-supplied Azure storage account toostore intermediary data when it executes hello workflow.</span></span> <span data-ttu-id="433fc-315">建立工作區，以及與該工作區相關聯 hello 便捷鍵時，這個儲存體帳戶會提供 tooMachine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="433fc-315">This storage account is provided tooMachine Learning Studio when a workspace is created, and hello access keys are associated with that workspace.</span></span> <span data-ttu-id="433fc-316">如果 hello 工作區建立之後變更 hello 便捷鍵，hello 工作區就無法再存取 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="433fc-316">If hello access keys are changed after hello workspace is created, hello workspace can no longer access hello storage account.</span></span> <span data-ttu-id="433fc-317">它會停止運作，而該工作區中的所有實驗將會失敗。</span><span class="sxs-lookup"><span data-stu-id="433fc-317">It will stop functioning and all experiments in that workspace will fail.</span></span>

<span data-ttu-id="433fc-318">如果您變更儲存體帳戶存取金鑰時，所使用的 hello 工作區中的重新同步處理 hello 便捷鍵 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="433fc-318">If you changed storage account access keys, resync hello access keys in hello workspace by using hello Azure classic portal.</span></span>  

## <a name="support-and-training"></a><span data-ttu-id="433fc-319">支援和訓練</span><span class="sxs-lookup"><span data-stu-id="433fc-319">Support and training</span></span>
<span data-ttu-id="433fc-320">**哪裡可以取得 Azure Machine Learning 的訓練？**</span><span class="sxs-lookup"><span data-stu-id="433fc-320">**Where can I get training for Azure Machine Learning?**</span></span>

<span data-ttu-id="433fc-321">hello [Azure 機器學習服務文件中心](https://azure.microsoft.com/services/machine-learning/)影片教學課程和如何 tooguides 主機。</span><span class="sxs-lookup"><span data-stu-id="433fc-321">hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/services/machine-learning/) hosts video tutorials and how-tooguides.</span></span> <span data-ttu-id="433fc-322">這些逐步指南介紹 hello 服務，並說明 hello 資料科學的匯入資料、 清除資料、 建立預測模型，以及將其部署在生產環境中使用 Azure Machine Learning 的生命週期。</span><span class="sxs-lookup"><span data-stu-id="433fc-322">These step-by-step guides introduce hello services and explain hello data science life cycle of importing data, cleaning data, building predictive models, and deploying them in production by using Azure Machine Learning.</span></span>

<span data-ttu-id="433fc-323">我們持續加入新的材料 toohello 機器學習中心。</span><span class="sxs-lookup"><span data-stu-id="433fc-323">We add new material toohello Machine Learning Center on an ongoing basis.</span></span> <span data-ttu-id="433fc-324">您可以送出要求 hello 在機器學習中心上的其他學習材料[使用者意見反應論壇](https://windowsazure.uservoice.com/forums/257792-machine-learning)。</span><span class="sxs-lookup"><span data-stu-id="433fc-324">You can submit requests for additional learning material on Machine Learning Center at hello [user feedback forum](https://windowsazure.uservoice.com/forums/257792-machine-learning).</span></span>

<span data-ttu-id="433fc-325">您也可以在 [Microsoft Virtual Academy](http://www.microsoftvirtualacademy.com/training-courses/getting-started-with-microsoft-azure-machine-learning)尋找訓練。</span><span class="sxs-lookup"><span data-stu-id="433fc-325">You can also find training at [Microsoft Virtual Academy](http://www.microsoftvirtualacademy.com/training-courses/getting-started-with-microsoft-azure-machine-learning).</span></span>

<span data-ttu-id="433fc-326">**如何取得 Azure Machine Learning 的支援？**</span><span class="sxs-lookup"><span data-stu-id="433fc-326">**How do I get support for Azure Machine Learning?**</span></span>

<span data-ttu-id="433fc-327">tooget Azure 機器學習，技術支援人員移過[Azure 支援](/support/options/)，然後選取**Machine Learning**。</span><span class="sxs-lookup"><span data-stu-id="433fc-327">tooget technical support for Azure Machine Learning, go too[Azure Support](/support/options/), and select **Machine Learning**.</span></span>

<span data-ttu-id="433fc-328">Azure Machine Learning 在 MSDN 上也設有社群論壇，可供您詢問 Azure Machine Learning 的相關問題。</span><span class="sxs-lookup"><span data-stu-id="433fc-328">Azure Machine Learning also has a community forum on MSDN where you can ask questions about Azure Machine Learning.</span></span> <span data-ttu-id="433fc-329">hello Azure Machine Learning 小組監視 hello 論壇。</span><span class="sxs-lookup"><span data-stu-id="433fc-329">hello Azure Machine Learning team monitors hello forum.</span></span> <span data-ttu-id="433fc-330">跳過[Azure 論壇](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning)。</span><span class="sxs-lookup"><span data-stu-id="433fc-330">Go too[Azure Forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning).</span></span>

## <a name="billing-questions"></a><span data-ttu-id="433fc-331">計費問題</span><span class="sxs-lookup"><span data-stu-id="433fc-331">Billing questions</span></span>
<span data-ttu-id="433fc-332">**機器學習服務如何計費？**</span><span class="sxs-lookup"><span data-stu-id="433fc-332">**How does Machine Learning billing work?**</span></span>

<span data-ttu-id="433fc-333">Azure Machine Learning 有兩個元件：Machine Learning Studio 與 Machine Learning Web 服務。</span><span class="sxs-lookup"><span data-stu-id="433fc-333">Azure Machine Learning has two components: Machine Learning Studio and Machine Learning web services.</span></span>

<span data-ttu-id="433fc-334">雖然您正在評估 Machine Learning Studio，您可以使用 hello 免費的計費層。</span><span class="sxs-lookup"><span data-stu-id="433fc-334">While you are evaluating Machine Learning Studio, you can use hello Free billing tier.</span></span> <span data-ttu-id="433fc-335">hello 免費層也可讓您部署的有限容量傳統 web 服務。</span><span class="sxs-lookup"><span data-stu-id="433fc-335">hello Free tier also lets you deploy a Classic web service that has limited capacity.</span></span>

<span data-ttu-id="433fc-336">如果您決定 Azure Machine Learning 符合您的需求，您可以申請 hello Standard 價格區間。</span><span class="sxs-lookup"><span data-stu-id="433fc-336">If you decide that Azure Machine Learning meets your needs, you can sign up for hello Standard tier.</span></span> <span data-ttu-id="433fc-337">向上 toosign，您必須有 Microsoft Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="433fc-337">toosign up, you must have a Microsoft Azure subscription.</span></span>

<span data-ttu-id="433fc-338">在 hello 標準層次中，您所要支付每月在 Machine Learning Studio 中定義的每個工作區。</span><span class="sxs-lookup"><span data-stu-id="433fc-338">In hello Standard tier, you are billed monthly for each workspace that you define in Machine Learning Studio.</span></span> <span data-ttu-id="433fc-339">當您執行實驗 hello studio 中時，您所要支付計算資源時您所執行的實驗。</span><span class="sxs-lookup"><span data-stu-id="433fc-339">When you run an experiment in hello studio, you are billed for compute resources when you are running an experiment.</span></span> <span data-ttu-id="433fc-340">當您部署的傳統 web 服務交易，並計算小時的計費 hello 付制為基礎。</span><span class="sxs-lookup"><span data-stu-id="433fc-340">When you deploy a Classic web service, transactions and compute hours are billed on hello Pay As You Go basis.</span></span>

<span data-ttu-id="433fc-341">新型 (Resource Manager 架構) Web 服務引進了可提高成本可預測性的計費方案。</span><span class="sxs-lookup"><span data-stu-id="433fc-341">New (Resource Manager-based) web services introduce billing plans that allow for more predictability in costs.</span></span> <span data-ttu-id="433fc-342">階層式定價提供折扣優惠 toocustomers 需要大量的容量。</span><span class="sxs-lookup"><span data-stu-id="433fc-342">Tiered pricing offers discounted rates toocustomers who need a large amount of capacity.</span></span>

<span data-ttu-id="433fc-343">當您建立計畫時，您就會認可 tooa 固定成本所隨附的應用程式開發介面運算時數和 API 交易內含數量。</span><span class="sxs-lookup"><span data-stu-id="433fc-343">When you create a plan, you commit tooa fixed cost that comes with an included quantity of API compute hours and API transactions.</span></span> <span data-ttu-id="433fc-344">如果您需要更包含的數量時，您可以加入執行個體 tooyour 計劃。</span><span class="sxs-lookup"><span data-stu-id="433fc-344">If you need more included quantities, you can add instances tooyour plan.</span></span> <span data-ttu-id="433fc-345">如果您需要非常多的包含數量，您可以選擇較高層級的方案，其可提供非常多的包含數量和更好的折扣費率。</span><span class="sxs-lookup"><span data-stu-id="433fc-345">If you need a lot more included quantities, you can choose a higher tier plan that provides considerably more included quantities and a better discounted rate.</span></span>

<span data-ttu-id="433fc-346">Hello 中現有的執行個體包含的數量都用完之後，其他使用方式被收費 hello overage hello 計費方案層與相關聯。</span><span class="sxs-lookup"><span data-stu-id="433fc-346">After hello included quantities in existing instances are used up, additional usage is charged at hello overage rate that's associated with hello billing plan tier.</span></span>

> [!NOTE]
<span data-ttu-id="433fc-347">包含的數量重新配置每隔 30 天，並包含未使用的數量不會彙總 toohello 下一個週期。</span><span class="sxs-lookup"><span data-stu-id="433fc-347">Included quantities are reallocated every 30 days, and unused included quantities do not roll over toohello next period.</span></span>

<span data-ttu-id="433fc-348">如需其他計費和價格資訊，請參閱 [機器學習服務價格](https://azure.microsoft.com/pricing/details/machine-learning/)。</span><span class="sxs-lookup"><span data-stu-id="433fc-348">For additional billing and pricing information, see [Machine Learning Pricing](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span>

<span data-ttu-id="433fc-349">**機器學習服務是否有免費試用版？**</span><span class="sxs-lookup"><span data-stu-id="433fc-349">**Does Machine Learning have a free trial?**</span></span>

 <span data-ttu-id="433fc-350">Azure Machine Learning 有 [Machine Learning 價格](https://azure.microsoft.com/pricing/details/machine-learning/)中說明的免費訂用帳戶選項。</span><span class="sxs-lookup"><span data-stu-id="433fc-350">Azure Machine Learning has a free subscription option that's explained in [Machine Learning Pricing](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span> <span data-ttu-id="433fc-351">Machine Learning Studio 有八小時快速評估試用版，可在您登入太[Machine Learning Studio](https://studio.azureml.net/?selectAccess=true&o=2)。</span><span class="sxs-lookup"><span data-stu-id="433fc-351">Machine Learning Studio has an eight-hour quick evaluation trial that's available when you sign in too[Machine Learning Studio](https://studio.azureml.net/?selectAccess=true&o=2).</span></span>

 <span data-ttu-id="433fc-352">此外，註冊 Azure 免費試用版後，您可以試用任何 Azure 服務一個月。</span><span class="sxs-lookup"><span data-stu-id="433fc-352">In addition, when you sign up for an Azure free trial, you can try any Azure services for a month.</span></span> <span data-ttu-id="433fc-353">toolearn 深入了解 hello Azure 免費試用版，請瀏覽[Azure 免費試用常見問題集](https://azure.microsoft.com/pricing/free-trial-faq/)。</span><span class="sxs-lookup"><span data-stu-id="433fc-353">toolearn more about hello Azure free trial, visit [Azure free trial FAQ](https://azure.microsoft.com/pricing/free-trial-faq/).</span></span>

<span data-ttu-id="433fc-354">**什麼是交易？**</span><span class="sxs-lookup"><span data-stu-id="433fc-354">**What is a transaction?**</span></span>

<span data-ttu-id="433fc-355">交易代表 Azure Machine Learning 所回應的 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="433fc-355">A transaction represents an API call that Azure Machine Learning responds to.</span></span> <span data-ttu-id="433fc-356">來自要求回應服務 (RRS) 和批次執行服務 (BES) 呼叫的交易會彙總起來，並根據計費方案來收費。</span><span class="sxs-lookup"><span data-stu-id="433fc-356">Transactions from Request-Response Service (RRS) and Batch Execution Service (BES) calls are aggregated and charged against your billing plan.</span></span>

<span data-ttu-id="433fc-357">**我可以使用包含 hello 交易數量計劃中 RR 和 BES 交易？**</span><span class="sxs-lookup"><span data-stu-id="433fc-357">**Can I use hello included transaction quantities in a plan for both RRS and BES transactions?**</span></span>

<span data-ttu-id="433fc-358">是，來自 RRS 和 BES 的交易會彙總起來，並根據計費方案來收費。</span><span class="sxs-lookup"><span data-stu-id="433fc-358">Yes, your transactions from your RRS and BES are aggregated and charged against your billing plan.</span></span>

<span data-ttu-id="433fc-359">**什麼是 API 計算時數？**</span><span class="sxs-lookup"><span data-stu-id="433fc-359">**What is an API compute hour?**</span></span>

<span data-ttu-id="433fc-360">應用程式開發介面計算是 hello 計費單位 hello 次應用程式開發介面呼叫 take toorun 使用機器學習來計算資源。</span><span class="sxs-lookup"><span data-stu-id="433fc-360">An API compute hour is hello billing unit for hello time that API calls take toorun by using Machine Learning compute resources.</span></span> <span data-ttu-id="433fc-361">系統會彙總所有呼叫以便計費。</span><span class="sxs-lookup"><span data-stu-id="433fc-361">All your calls are aggregated for billing purposes.</span></span>

<span data-ttu-id="433fc-362">**典型的生產 API 呼叫需要花費多久時間？**</span><span class="sxs-lookup"><span data-stu-id="433fc-362">**How long does a typical production API call take?**</span></span>

<span data-ttu-id="433fc-363">實際執行應用程式開發介面呼叫時間變化相當大，通常介於數百個毫秒 tooa 幾秒鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="433fc-363">Production API call times can vary significantly, generally ranging from hundreds of milliseconds tooa few seconds.</span></span> <span data-ttu-id="433fc-364">有些應用程式開發介面呼叫可能需要分鐘視 hello hello 資料處理和機器學習模型的複雜度而定。</span><span class="sxs-lookup"><span data-stu-id="433fc-364">Some API calls might require minutes depending on hello complexity of hello data processing and machine-learning model.</span></span> <span data-ttu-id="433fc-365">hello 最佳方式 tooestimate 生產應用程式開發介面呼叫時間不 toobenchmark hello 機器學習服務上的模型。</span><span class="sxs-lookup"><span data-stu-id="433fc-365">hello best way tooestimate production API call times is toobenchmark a model on hello Machine Learning service.</span></span>

<span data-ttu-id="433fc-366">**什麼是 Studio 計算時數？**</span><span class="sxs-lookup"><span data-stu-id="433fc-366">**What is a Studio compute hour?**</span></span>

<span data-ttu-id="433fc-367">Studio 計算小時是 hello 計費單位的 hello 彙總的時間，將實驗在 studio 中使用計算資源。</span><span class="sxs-lookup"><span data-stu-id="433fc-367">A Studio compute hour is hello billing unit for hello aggregate time that your experiments use compute resources in studio.</span></span>

<span data-ttu-id="433fc-368">**在新的 （Azure 資源管理員為基礎） 的 web 服務中，是 hello 開發/測試層所謂的？**</span><span class="sxs-lookup"><span data-stu-id="433fc-368">**In New (Azure Resource Manager-based) web services, what is hello Dev/Test tier meant for?**</span></span>

<span data-ttu-id="433fc-369">資源管理員為基礎的 web 服務提供多個層，您可以使用 tooprovision 您的計費方案。</span><span class="sxs-lookup"><span data-stu-id="433fc-369">Resource Manager-based web services provide multiple tiers that you can use tooprovision your billing plan.</span></span> <span data-ttu-id="433fc-370">hello 開發/測試定價層提供有限且包含數量可讓您 tootest 實驗為 web 服務而不會產生成本。</span><span class="sxs-lookup"><span data-stu-id="433fc-370">hello Dev/Test pricing tier provides limited, included quantities that allow you tootest your experiment as a web service without incurring costs.</span></span> <span data-ttu-id="433fc-371">您擁有 hello 機會 toosee 它的運作方式。</span><span class="sxs-lookup"><span data-stu-id="433fc-371">You have hello opportunity toosee how it works.</span></span>

<span data-ttu-id="433fc-372">**儲存體需要另外付費嗎？**</span><span class="sxs-lookup"><span data-stu-id="433fc-372">**Are there separate storage charges?**</span></span>

<span data-ttu-id="433fc-373">hello 機器學習免費層次不需要或不允許不同的儲存體。</span><span class="sxs-lookup"><span data-stu-id="433fc-373">hello Machine Learning Free tier does not require or allow separate storage.</span></span> <span data-ttu-id="433fc-374">hello 機器學習標準層需要使用者 toohave Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="433fc-374">hello Machine Learning Standard tier requires users toohave an Azure storage account.</span></span> <span data-ttu-id="433fc-375">Azure 儲存體是[另外收費](https://azure.microsoft.com/pricing/details/storage/)。</span><span class="sxs-lookup"><span data-stu-id="433fc-375">Azure Storage is [billed separately](https://azure.microsoft.com/pricing/details/storage/).</span></span>

<span data-ttu-id="433fc-376">**Machine Learning 是否支援高可用性？**</span><span class="sxs-lookup"><span data-stu-id="433fc-376">**Does Machine Learning support high availability?**</span></span>

<span data-ttu-id="433fc-377">是。</span><span class="sxs-lookup"><span data-stu-id="433fc-377">Yes.</span></span> <span data-ttu-id="433fc-378">如需詳細資訊，請參閱[機器學習定價](https://azure.microsoft.com/en-us/pricing/details/machine-learning/)hello 服務等級協定 (SLA) 的描述。</span><span class="sxs-lookup"><span data-stu-id="433fc-378">For details, see [Machine Learning Pricing](https://azure.microsoft.com/en-us/pricing/details/machine-learning/) for a description of hello service level agreement (SLA).</span></span>

<span data-ttu-id="433fc-379">**我的生產 API 呼叫將使用哪些特定種類的計算資源來執行？**</span><span class="sxs-lookup"><span data-stu-id="433fc-379">**What specific kind of compute resources will my production API calls be run on?**</span></span>

<span data-ttu-id="433fc-380">hello 機器學習服務是一個多租用戶的服務。</span><span class="sxs-lookup"><span data-stu-id="433fc-380">hello Machine Learning service is a multitenant service.</span></span> <span data-ttu-id="433fc-381">Hello 後端所使用的實際計算資源而有所不同，而且會針對效能和可預測性最佳化。</span><span class="sxs-lookup"><span data-stu-id="433fc-381">Actual compute resources that are used on hello back end vary and are optimized for performance and predictability.</span></span>

### <a name="management-of-new-resource-manager-based-web-services"></a><span data-ttu-id="433fc-382">新型 (Resource Manager 架構) Web 服務的管理</span><span class="sxs-lookup"><span data-stu-id="433fc-382">Management of New (Resource Manager-based) web services</span></span>
<span data-ttu-id="433fc-383">**如果我刪除方案會發生什麼事？**</span><span class="sxs-lookup"><span data-stu-id="433fc-383">**What happens if I delete my plan?**</span></span>

<span data-ttu-id="433fc-384">從您的訂用帳戶中，移除 hello 計畫，您所要支付計算按比例分配的使用方式。</span><span class="sxs-lookup"><span data-stu-id="433fc-384">hello plan is removed from your subscription, and you are billed for prorated usage.</span></span>

> [!NOTE]
<span data-ttu-id="433fc-385">您無法刪除 Web 服務正在使用的方案。</span><span class="sxs-lookup"><span data-stu-id="433fc-385">You cannot delete a plan that a web service is using.</span></span> <span data-ttu-id="433fc-386">toodelete hello 計劃，您必須指派新計劃 toohello web 服務，或者刪除 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="433fc-386">toodelete hello plan, you must either assign a new plan toohello web service or delete hello web service.</span></span>

<span data-ttu-id="433fc-387">**什麼是方案執行個體？**</span><span class="sxs-lookup"><span data-stu-id="433fc-387">**What is a plan instance?**</span></span>

<span data-ttu-id="433fc-388">計劃的執行個體是您可以加入 tooyour 計費計劃包含數量的單位。</span><span class="sxs-lookup"><span data-stu-id="433fc-388">A plan instance is a unit of included quantities that you can add tooyour billing plan.</span></span> <span data-ttu-id="433fc-389">為計費方案選取計費層時，方案便會隨附一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="433fc-389">When you select a billing tier for your billing plan, it comes with one instance.</span></span> <span data-ttu-id="433fc-390">如果您需要更包含的數量時，您可以加入 hello 選計費層 tooyour 計劃的執行個體。</span><span class="sxs-lookup"><span data-stu-id="433fc-390">If you need more included quantities, you can add instances of hello selected billing tier tooyour plan.</span></span>

<span data-ttu-id="433fc-391">**可以新增多少個方案執行個體？**</span><span class="sxs-lookup"><span data-stu-id="433fc-391">**How many plan instances can I add?**</span></span>

<span data-ttu-id="433fc-392">您可以訂用帳戶中有一個 hello 開發/測試定價層的執行個體。</span><span class="sxs-lookup"><span data-stu-id="433fc-392">You can have one instance of hello Dev/Test pricing tier in a subscription.</span></span>

<span data-ttu-id="433fc-393">在標準 S1、標準 S2 和標準 S3 層中，您可以視需要新增多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="433fc-393">For Standard S1, Standard S2, and Standard S3 tiers, you can add as many as necessary.</span></span>

> [!NOTE]
<span data-ttu-id="433fc-394">根據您預期的使用方式，它可能是更符合成本效益更包含數量 tooupgrade tooa 層而非新增執行個體 toohello 目前層。</span><span class="sxs-lookup"><span data-stu-id="433fc-394">Depending on your anticipated usage, it might be more cost effective tooupgrade tooa tier that has more included quantities rather than add instances toohello current tier.</span></span>

<span data-ttu-id="433fc-395">**變更方案層級 (升級/降級) 時會發生什麼事？**</span><span class="sxs-lookup"><span data-stu-id="433fc-395">**What happens when I change plan tiers (upgrade / downgrade)?**</span></span>

<span data-ttu-id="433fc-396">hello 舊計劃已刪除，且 hello 目前使用量計費計算按比例分配的基礎。</span><span class="sxs-lookup"><span data-stu-id="433fc-396">hello old plan is deleted and hello current usage is billed on a prorated basis.</span></span> <span data-ttu-id="433fc-397">與 hello 完整包含的數量 hello 升級/降級層的新計畫會建立 hello 期間 hello 其餘部分。</span><span class="sxs-lookup"><span data-stu-id="433fc-397">A new plan with hello full included quantities of hello upgraded/downgraded tier is created for hello rest of hello period.</span></span>

> [!NOTE]
<span data-ttu-id="433fc-398">包含的數量是針對每個期間來配置，未使用的數量不會展期。</span><span class="sxs-lookup"><span data-stu-id="433fc-398">Included quantities are allocated per period, and unused quantities do not roll over.</span></span>

<span data-ttu-id="433fc-399">**當我計劃中增加 hello 執行個體時，發生什麼事？**</span><span class="sxs-lookup"><span data-stu-id="433fc-399">**What happens when I increase hello instances in a plan?**</span></span>

<span data-ttu-id="433fc-400">數量則包含在計算按比例分配的基礎，而且可能需要 24 小時 toobe 有效。</span><span class="sxs-lookup"><span data-stu-id="433fc-400">Quantities are included on a prorated basis and may take 24 hours toobe effective.</span></span>

<span data-ttu-id="433fc-401">**刪除方案執行個體時會發生什麼事？**</span><span class="sxs-lookup"><span data-stu-id="433fc-401">**What happens when I delete an instance of a plan?**</span></span>

<span data-ttu-id="433fc-402">hello 實例會從您的訂用帳戶中，移除與您所要支付計算按比例分配的使用方式。</span><span class="sxs-lookup"><span data-stu-id="433fc-402">hello instance is removed from your subscription, and you are billed for prorated usage.</span></span>

### <a name="sign-up-for-new-resource-manager-based-web-services-plans"></a><span data-ttu-id="433fc-403">註冊新型 (Resource Manager 架構) Web 服務方案</span><span class="sxs-lookup"><span data-stu-id="433fc-403">Sign up for New (Resource Manager-based) web services plans</span></span>
<span data-ttu-id="433fc-404">**如何註冊方案？**</span><span class="sxs-lookup"><span data-stu-id="433fc-404">**How do I sign up for a plan?**</span></span>

<span data-ttu-id="433fc-405">您有兩種方式 toocreate 計費方案。</span><span class="sxs-lookup"><span data-stu-id="433fc-405">You have two ways toocreate billing plans.</span></span>

<span data-ttu-id="433fc-406">當您第一次部署 Resource Manager 架構 Web 服務時，您可以選擇現有方案，或建立新方案。</span><span class="sxs-lookup"><span data-stu-id="433fc-406">When you first deploy a Resource Manager-based web service, you can choose an existing plan or create a new plan.</span></span>

<span data-ttu-id="433fc-407">您在這種方式中建立的計劃不會在您預設的地區，而且您的 web 服務部署的 toothat 區域。</span><span class="sxs-lookup"><span data-stu-id="433fc-407">Plans that you create in this manner are in your default region, and your web service will be deployed toothat region.</span></span>

<span data-ttu-id="433fc-408">如果您想 toodeploy 服務 tooregions 預設區域以外，您可能想 toodefine 計費的計劃之前部署您的服務。</span><span class="sxs-lookup"><span data-stu-id="433fc-408">If you want toodeploy services tooregions other than your default region, you may want toodefine your billing plans before you deploy your service.</span></span>

<span data-ttu-id="433fc-409">在此情況下，您可以登入 toohello Azure 機器學習 Web 服務入口網站，並移 toohello 計劃 頁面。</span><span class="sxs-lookup"><span data-stu-id="433fc-409">In that case, you can sign in toohello Azure Machine Learning Web Services portal, and go toohello Plans page.</span></span> <span data-ttu-id="433fc-410">您可以在該處新增方案、刪除方案，以及修改現有方案。</span><span class="sxs-lookup"><span data-stu-id="433fc-410">From there, you can add plans, delete plans, and modify existing plans.</span></span>

<span data-ttu-id="433fc-411">**哪一個計劃我應該選擇 toostart 關閉與？**</span><span class="sxs-lookup"><span data-stu-id="433fc-411">**Which plan should I choose toostart off with?**</span></span>

<span data-ttu-id="433fc-412">我們建議您您開始使用 hello 標準 S1 層和監視您的服務使用方式。</span><span class="sxs-lookup"><span data-stu-id="433fc-412">We recommend you that you start with hello Standard S1 tier and monitor your service for usage.</span></span> <span data-ttu-id="433fc-413">如果您發現您正在使用您包含的數量快速，您可以加入執行個體或移動 tooa 更高的層，並取得更好的折扣的率。</span><span class="sxs-lookup"><span data-stu-id="433fc-413">If you find that you are using your included quantities rapidly, you can add instances or move tooa higher tier and get better discounted rates.</span></span> <span data-ttu-id="433fc-414">在整個計費週期內，您都可以視需要調整計費方案。</span><span class="sxs-lookup"><span data-stu-id="433fc-414">You can adjust your billing plan as needed throughout your billing cycle.</span></span>

<span data-ttu-id="433fc-415">**哪些區域可用 hello 新計劃中？**</span><span class="sxs-lookup"><span data-stu-id="433fc-415">**Which regions are hello new plans available in?**</span></span>

<span data-ttu-id="433fc-416">新的計費計畫 hello 可用 hello 三個生產區域中，我們支援 hello 新的 web 服務：</span><span class="sxs-lookup"><span data-stu-id="433fc-416">hello new billing plans are available in hello three production regions in which we support hello new web services:</span></span>

* <span data-ttu-id="433fc-417">美國中南部</span><span class="sxs-lookup"><span data-stu-id="433fc-417">South Central US</span></span>
* <span data-ttu-id="433fc-418">西歐</span><span class="sxs-lookup"><span data-stu-id="433fc-418">West Europe</span></span>
* <span data-ttu-id="433fc-419">東南亞</span><span class="sxs-lookup"><span data-stu-id="433fc-419">South East Asia</span></span>

<span data-ttu-id="433fc-420">**我在多個區域擁有 Web 服務。是否每個區域都需要一個方案？**</span><span class="sxs-lookup"><span data-stu-id="433fc-420">**I have web services in multiple regions. Do I need a plan for every region?**</span></span>

<span data-ttu-id="433fc-421">是。</span><span class="sxs-lookup"><span data-stu-id="433fc-421">Yes.</span></span> <span data-ttu-id="433fc-422">不同區域有不同的方案價格。</span><span class="sxs-lookup"><span data-stu-id="433fc-422">Plan pricing varies by region.</span></span> <span data-ttu-id="433fc-423">當您部署的 web 服務 tooanother 區域時，您需要 tooassign 為特定 toothat 區域計劃。</span><span class="sxs-lookup"><span data-stu-id="433fc-423">When you deploy a web service tooanother region, you need tooassign it a plan that is specific toothat region.</span></span> <span data-ttu-id="433fc-424">如需詳細資訊，請參閱[不同區域提供的產品]( https://azure.microsoft.com/regions/services/)。</span><span class="sxs-lookup"><span data-stu-id="433fc-424">For more information, see [Products available by region]( https://azure.microsoft.com/regions/services/).</span></span>

### <a name="new-web-services-overages"></a><span data-ttu-id="433fc-425">新型 Web 服務：超額</span><span class="sxs-lookup"><span data-stu-id="433fc-425">New web services: Overages</span></span>
<span data-ttu-id="433fc-426">**如何檢查 Web 服務使用量是否超額？**</span><span class="sxs-lookup"><span data-stu-id="433fc-426">**How do I check if I exceeded my web service usage?**</span></span>

<span data-ttu-id="433fc-427">您可以檢視 hello 使用量 hello Azure 機器學習 Web 服務入口網站中的 hello 計畫頁面上所有您計劃。</span><span class="sxs-lookup"><span data-stu-id="433fc-427">You can view hello usage on all your plans on hello Plans page in hello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="433fc-428">登入 toohello 入口網站，然後按一下hello**計劃**功能表選項。</span><span class="sxs-lookup"><span data-stu-id="433fc-428">Sign in toohello portal, and then click hello **Plans** menu option.</span></span>

<span data-ttu-id="433fc-429">在 hello**交易**和**計算**hello 資料表的資料行，您可以看到 hello 包含數量的 hello 計劃並使用 hello 百分比。</span><span class="sxs-lookup"><span data-stu-id="433fc-429">In hello **Transactions** and **Compute** columns of hello table, you can see hello included quantities of hello plan and hello percentage used.</span></span>

<span data-ttu-id="433fc-430">**使用向上 hello 時，會發生什麼事數量納入 hello 開發/測試定價層？**</span><span class="sxs-lookup"><span data-stu-id="433fc-430">**What happens when I use up hello include quantities in hello Dev/Test pricing tier?**</span></span>

<span data-ttu-id="433fc-431">下一個週期或移動 tooa 付費層之前，會停止直到 hello 具有定價層指派 toothem 開發/測試服務。</span><span class="sxs-lookup"><span data-stu-id="433fc-431">Services that have a Dev/Test pricing tier assigned toothem are stopped until hello next period or until you move them tooa paid tier.</span></span>

<span data-ttu-id="433fc-432">**針對傳統 Web 服務和超額的新 (Resource Manager 架構) Web 服務，如何計算要求回應 (RRS) 和批次 (BES) 工作負載的價格？**</span><span class="sxs-lookup"><span data-stu-id="433fc-432">**For Classic web services and overages of New (Resource Manager-based) web services, how are prices calculated for Request Response (RRS) and Batch (BES) workloads?**</span></span>

<span data-ttu-id="433fc-433">針對 RR 工作負載，您負責確定每個 API 交易呼叫以及與這些要求相關聯的 hello 運算時間。</span><span class="sxs-lookup"><span data-stu-id="433fc-433">For an RRS workload, you are charged for every API transaction call that you make and for hello compute time that's associated with those requests.</span></span> <span data-ttu-id="433fc-434">您的應用程式開發介面呼叫的 hello 總數乘以 hello 價格每 1000 （依比例由個別的交易） 的交易都會計算 RR 生產應用程式開發介面交易成本。</span><span class="sxs-lookup"><span data-stu-id="433fc-434">Your RRS production API transaction costs are calculated as hello total number of API calls that you make multiplied by hello price per 1,000 transactions (prorated by individual transaction).</span></span> <span data-ttu-id="433fc-435">RR 應用程式開發介面實際執行應用程式開發介面計算小時成本會計算為 hello 數量乘以 hello API 交易總數，乘以 hello 單價生產應用程式開發介面計算小時每個應用程式開發介面呼叫 toorun 所需的時間。</span><span class="sxs-lookup"><span data-stu-id="433fc-435">Your RRS API production API compute hour costs are calculated as hello amount of time required for each API call toorun, multiplied by hello total number of API transactions, multiplied by hello price per production API compute hour.</span></span>

<span data-ttu-id="433fc-436">比方說，標準 S1 超額部分，如 1000000 API 交易 0.72 秒的每個 toorun 會導致 (1000000 * $0.50/1k API 交易) 在 $500，實際執行應用程式開發介面交易成本和 (1000000 * 0.72 秒 * $2/hr) $400 生產應用程式開發介面計算中總計 $900 個小時。</span><span class="sxs-lookup"><span data-stu-id="433fc-436">For example, for Standard S1 overage, 1,000,000 API transactions that take 0.72 seconds each toorun would result in (1,000,000 * $0.50/1K API transactions) in $500 in production API transaction costs and (1,000,000 * 0.72 sec * $2/hr) $400 in production API compute hours, for a total of $900.</span></span>

<span data-ttu-id="433fc-437">BES 工作負載，您需要付費 hello 中相同的方式。</span><span class="sxs-lookup"><span data-stu-id="433fc-437">For a BES workload, you are charged in hello same manner.</span></span> <span data-ttu-id="433fc-438">不過，hello API 交易成本表示您送出，批次作業的 hello 數目，而 hello 計算成本表示 hello 運算時間的批次作業相關聯。</span><span class="sxs-lookup"><span data-stu-id="433fc-438">However, hello API transaction costs represent hello number of batch jobs that you submit, and hello compute costs represent hello compute time that's associated with those batch jobs.</span></span> <span data-ttu-id="433fc-439">提交的 hello 總數乘以 hello 價格每 1000 （依比例由個別的交易） 的交易都會計算 BES 生產應用程式開發介面交易成本。</span><span class="sxs-lookup"><span data-stu-id="433fc-439">Your BES production API transaction costs are calculated as hello total number of jobs submitted multiplied by hello price per 1,000 transactions (prorated by individual transaction).</span></span> <span data-ttu-id="433fc-440">BES 應用程式開發介面實際執行應用程式開發介面計算小時成本會以 hello 數量乘以 hello 資料列總數乘以 hello 總數乘以 hello 單價生產應用程式開發介面作業的工作中您工作 toorun 中每個資料列所需的時間計算計算小時。</span><span class="sxs-lookup"><span data-stu-id="433fc-440">Your BES API production API compute hour costs are calculated as hello amount of time required for each row in your job toorun multiplied by hello total number of rows in your job multiplied by hello total number of jobs multiplied by hello price per production API compute hour.</span></span> <span data-ttu-id="433fc-441">當您使用 hello 機器學習 [小算盤] 時，hello 交易計量表代表 hello 的作業數目，您計劃 toosubmit，與 hello 每筆交易的時間欄位代表 hello 結合的所有資料列中每個作業 toorun 所需的時間。</span><span class="sxs-lookup"><span data-stu-id="433fc-441">When you use hello Machine Learning calculator, hello transaction meter represents hello number of jobs that you plan toosubmit, and hello time-per-transaction field represents hello combined time that's needed for all rows in each job toorun.</span></span>

<span data-ttu-id="433fc-442">例如，假設採用標準 S1 超額，而且您每天提交 100 個作業，每個作業包含 500 個資料列，且執行時間各為 0.72 秒。</span><span class="sxs-lookup"><span data-stu-id="433fc-442">For example, assume Standard S1 overage, and you submit 100 jobs per day that each consist of 500 rows that take 0.72 seconds each.</span></span> <span data-ttu-id="433fc-443">您的每月超額費用會是 (每天 100 個作業 = 每月 3,100 個作業 * 0.50 美元/1,000 個 API 交易) 1.55 美元的生產 API 交易費用和 (500 個資料列 * 0.72 秒 * 3,100 個作業 * 2 美元/小時) 620 美元的生產 API 計算時數，總計 621.55 美元。</span><span class="sxs-lookup"><span data-stu-id="433fc-443">Your monthly overage costs would be (100 jobs per day = 3,100 jobs/mo * $0.50/1K API transactions) $1.55 in production API transaction costs and (500 rows * 0.72 sec * 3,100 Jobs * $2/hr) $620 in production API compute hours, for a total of $621.55.</span></span>

### <a name="azure-machine-learning-classic-web-services"></a><span data-ttu-id="433fc-444">Azure Machine Learning 傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="433fc-444">Azure Machine Learning Classic web services</span></span>
<span data-ttu-id="433fc-445">**是否還有提供隨用隨付？**</span><span class="sxs-lookup"><span data-stu-id="433fc-445">**Is Pay As You Go still available?**</span></span>

<span data-ttu-id="433fc-446">是，Azure Machine Learning 中仍然提供傳統的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="433fc-446">Yes, Classic web services are still available in Azure Machine Learning.</span></span>  

### <a name="azure-machine-learning-free-and-standard-tier"></a><span data-ttu-id="433fc-447">Azure Machine Learning 的免費層和標準層</span><span class="sxs-lookup"><span data-stu-id="433fc-447">Azure Machine Learning Free and Standard tier</span></span>
<span data-ttu-id="433fc-448">**什麼包含在 hello Azure 機器學習免費層？**</span><span class="sxs-lookup"><span data-stu-id="433fc-448">**What is included in hello Azure Machine Learning Free tier?**</span></span>

<span data-ttu-id="433fc-449">hello Azure 機器學習免費層是預定的 tooprovide 深入了解簡介 toohello Azure Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="433fc-449">hello Azure Machine Learning Free tier is intended tooprovide an in-depth introduction toohello Azure Machine Learning Studio.</span></span> <span data-ttu-id="433fc-450">您只需要為 Microsoft 帳戶 toosign 註冊。</span><span class="sxs-lookup"><span data-stu-id="433fc-450">All you need is a Microsoft account toosign up.</span></span> <span data-ttu-id="433fc-451">hello 免費層包含免費存取 tooone Azure Machine Learning Studio 工作區中的每個[Microsoft 帳戶](https://www.microsoft.com/account/default.aspx)。</span><span class="sxs-lookup"><span data-stu-id="433fc-451">hello Free tier includes free access tooone Azure Machine Learning Studio workspace per [Microsoft account](https://www.microsoft.com/account/default.aspx).</span></span> <span data-ttu-id="433fc-452">在此層級，您可以使用向上 too10 GB 的儲存體，並實施模型做為暫存應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="433fc-452">In this tier, you can use up too10 GB of storage and operationalize models as staging APIs.</span></span> <span data-ttu-id="433fc-453">免費層工作負載不包含在 SLA 內，且僅供開發與個人使用。</span><span class="sxs-lookup"><span data-stu-id="433fc-453">Free tier workloads are not covered by an SLA and are intended for development and personal use only.</span></span> 

<span data-ttu-id="433fc-454">免費層次的工作區具有下列限制的 hello:</span><span class="sxs-lookup"><span data-stu-id="433fc-454">Free tier workspaces have hello following limitations:</span></span>

* <span data-ttu-id="433fc-455">工作負載無法藉由連接 tooan 執行 SQL Server 的內部部署伺服器來存取資料。</span><span class="sxs-lookup"><span data-stu-id="433fc-455">Workloads can't access data by connecting tooan on-premises server that runs SQL Server.</span></span>
* <span data-ttu-id="433fc-456">您無法部署新的 Resource Manager 基底 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="433fc-456">You cannot deploy New Resource Manager base web services.</span></span>


<span data-ttu-id="433fc-457">**什麼包含在 hello Azure 機器學習標準層和計劃？**</span><span class="sxs-lookup"><span data-stu-id="433fc-457">**What is included in hello Azure Machine Learning Standard tier and plans?**</span></span>

<span data-ttu-id="433fc-458">hello Azure 機器學習標準層是付費的實際執行版本的 Azure Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="433fc-458">hello Azure Machine Learning Standard tier is a paid production version of Azure Machine Learning Studio.</span></span> <span data-ttu-id="433fc-459">hello Azure Machine Learning Studio 每月費用計費每個工作區中每個月為基礎和計算按比例分配的局部月數。</span><span class="sxs-lookup"><span data-stu-id="433fc-459">hello Azure Machine Learning Studio monthly fee is billed on a per workspace per month basis and prorated for partial months.</span></span> <span data-ttu-id="433fc-460">Azure Machine Learning Studio 實驗時數會依據進行中實驗的每個計算時數收費。</span><span class="sxs-lookup"><span data-stu-id="433fc-460">Azure Machine Learning Studio experiment hours are billed per compute hour for active experimentation.</span></span> <span data-ttu-id="433fc-461">不足的時數會按比例收費。</span><span class="sxs-lookup"><span data-stu-id="433fc-461">Billing is prorated for partial hours.</span></span>  

<span data-ttu-id="433fc-462">hello Azure 機器學習 API 服務為計費根據它是否傳統 web 服務或新的 （資源管理員為基礎） 的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="433fc-462">hello Azure Machine Learning API service is billed depending on whether it's a Classic web service or a New (Resource Manager-based) web service.</span></span>

<span data-ttu-id="433fc-463">hello 遵循費用會彙總每個訂用帳戶的工作區。</span><span class="sxs-lookup"><span data-stu-id="433fc-463">hello following charges are aggregated per workspace for your subscription.</span></span>

* <span data-ttu-id="433fc-464">機器學習服務工作區訂用帳戶： hello Machine Learning 工作區的訂用帳戶會提供存取 tooa Machine Learning Studio 工作區是按月計價。</span><span class="sxs-lookup"><span data-stu-id="433fc-464">Machine Learning Workspace Subscription: hello Machine Learning workspace subscription is a monthly fee that provides access tooa Machine Learning Studio workspace.</span></span> <span data-ttu-id="433fc-465">hello studio 和 tooutilize hello 在生產環境中應用程式開發介面需要的 toorun 實驗 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="433fc-465">hello subscription is required toorun experiments in hello studio and tooutilize hello production APIs.</span></span>
* <span data-ttu-id="433fc-466">Studio 實驗小時： 這個計費表彙總累加的實驗執行 Machine Learning Studio 中的所有計算費用，並在預備環境的 hello 呼叫執行實際執行應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="433fc-466">Studio Experiment hours: This meter aggregates all compute charges that are accrued by running experiments in Machine Learning Studio and running production API calls in hello staging environment.</span></span>
* <span data-ttu-id="433fc-467">存取由 tooan 執行在程式訓練的模型中的 SQL Server 的內部部署伺服器連接和計分的資料。</span><span class="sxs-lookup"><span data-stu-id="433fc-467">Access data by connecting tooan on-premises server that runs SQL Server in your models for your training and scoring.</span></span>
* <span data-ttu-id="433fc-468">傳統 Web 服務：</span><span class="sxs-lookup"><span data-stu-id="433fc-468">For Classic web services:</span></span>
  * <span data-ttu-id="433fc-469">生產 API 計算時數：此計量包含在生產環境中執行的 Web 服務所產生的計算費用。</span><span class="sxs-lookup"><span data-stu-id="433fc-469">Production API Compute Hours: This meter includes compute charges that are accrued by web services running in production.</span></span>
  * <span data-ttu-id="433fc-470">實際執行應用程式開發介面的交易 （1000): 這個計費表包括會累加的每個呼叫 tooyour 生產環境 web 服務的費用。</span><span class="sxs-lookup"><span data-stu-id="433fc-470">Production API Transactions (in 1000s): This meter includes charges that are accrued per call tooyour production web service.</span></span>

<span data-ttu-id="433fc-471">除了上述費用，在資源管理員為基礎的 web 服務的 hello 案例中的 hello 費用會彙總的 toohello 選取計劃：</span><span class="sxs-lookup"><span data-stu-id="433fc-471">Apart from hello preceding charges, in hello case of Resource Manager-based web service, charges are aggregated toohello selected plan:</span></span>

* <span data-ttu-id="433fc-472">這個計費表標準 S1/S2/S3 API 計劃 （單位）： 表示已選取的資源管理員為基礎的 web 服務的執行個體 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="433fc-472">Standard S1/S2/S3 API Plan (Units): This meter represents hello type of instance that's selected for Resource Manager-based web services.</span></span>
* <span data-ttu-id="433fc-473">標準 S1/S2/S3 Overage API 運算時數： 這個計費表包括會累加的現有執行個體中的 hello 包含數量會用完後才在生產中執行的資源管理員為基礎的 web 服務的計算費用。</span><span class="sxs-lookup"><span data-stu-id="433fc-473">Standard S1/S2/S3 Overage API Compute Hours: This meter includes compute charges that are accrued by Resource Manager-based web services that run in production after hello included quantities in existing instances are used up.</span></span> <span data-ttu-id="433fc-474">hello 額外使用量收費 hello overate S1/S2/S3 計劃層與相關聯的速率。</span><span class="sxs-lookup"><span data-stu-id="433fc-474">hello additional usage is charged at hello overate rate that's associated with S1/S2/S3 plan tier.</span></span>
* <span data-ttu-id="433fc-475">標準 S1/S2/S3 超額部分應用程式開發介面的交易 （1,000s): 這個計費表包含每個呼叫 tooyour 實際執行資源管理員為基礎的 web 服務 hello 納入現有的執行個體的數量之後用完會累算費用。</span><span class="sxs-lookup"><span data-stu-id="433fc-475">Standard S1/S2/S3 Overage API Transactions (in 1,000s): This meter includes charges that are accrued per call tooyour production Resource Manager-based web service after hello included quantities in existing instances are used up.</span></span> <span data-ttu-id="433fc-476">hello 額外使用量收費 hello overate S1/S2/S3 計劃層相關聯的速率。</span><span class="sxs-lookup"><span data-stu-id="433fc-476">hello additional usage is charged at hello overate rate associated with S1/S2/S3 plan tier.</span></span>
* <span data-ttu-id="433fc-477">包含數量的應用程式開發介面運算時數： 與資源管理員為基礎的 web 服務，這個計費表代表 hello 包含數量的應用程式開發介面運算時數。</span><span class="sxs-lookup"><span data-stu-id="433fc-477">Included Quantity API Compute Hours: With Resource Manager-based web services, this meter represents hello included quantity of API compute hours.</span></span>
* <span data-ttu-id="433fc-478">納入數量 API 交易 （1,000s): 使用資源管理員為基礎的 web 服務，這個計費表代表 hello 包含 API 交易數量。</span><span class="sxs-lookup"><span data-stu-id="433fc-478">Included Quantity API Transactions (in 1,000s): With Resource Manager-based web services, this meter represents hello included quantity of API transactions.</span></span>

<span data-ttu-id="433fc-479">**如何註冊 Azure Machine Learning 免費層？**</span><span class="sxs-lookup"><span data-stu-id="433fc-479">**How do I sign up for Azure Machine Learning Free tier?**</span></span>

<span data-ttu-id="433fc-480">您只需要 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="433fc-480">All you need is a Microsoft account.</span></span> <span data-ttu-id="433fc-481">跳過[Azure Machine Learning 首頁](https://azure.microsoft.com/services/machine-learning/)，然後按一下**立即開始**。</span><span class="sxs-lookup"><span data-stu-id="433fc-481">Go too[Azure Machine Learning home](https://azure.microsoft.com/services/machine-learning/), and then click **Start Now**.</span></span> <span data-ttu-id="433fc-482">使用 Microsoft 帳戶登入，系統便會為您建立免費層工作區。</span><span class="sxs-lookup"><span data-stu-id="433fc-482">Sign in with your Microsoft account and a workspace in Free tier is created for you.</span></span> <span data-ttu-id="433fc-483">您可以啟動 tooexplore，並立即建立機器學習實驗。</span><span class="sxs-lookup"><span data-stu-id="433fc-483">You can start tooexplore and create Machine Learning experiments right away.</span></span>

<span data-ttu-id="433fc-484">**如何註冊 Azure Machine Learning 標準層？**</span><span class="sxs-lookup"><span data-stu-id="433fc-484">**How do I sign up for Azure Machine Learning Standard tier?**</span></span>

<span data-ttu-id="433fc-485">您必須先存取 tooan Azure 訂用帳戶 toocreate 標準 Machine Learning 工作區。</span><span class="sxs-lookup"><span data-stu-id="433fc-485">You must first have access tooan Azure subscription toocreate a Standard Machine Learning workspace.</span></span> <span data-ttu-id="433fc-486">您可以註冊 30 天免費試用 Azure 訂用帳戶和更新版本的升級 tooa 付費型 Azure 訂用帳戶，或者，您可以購買付費 Azure 訂用帳戶徹底。</span><span class="sxs-lookup"><span data-stu-id="433fc-486">You can sign up for a 30-day free trial Azure subscription and later upgrade tooa paid Azure subscription, or you can purchase a paid Azure subscription outright.</span></span> <span data-ttu-id="433fc-487">然後您可以從 hello Microsoft Azure 傳統入口網站建立 Machine Learning 工作區之後您就可以存取 toohello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="433fc-487">You can then create a Machine Learning workspace from hello Microsoft Azure classic portal after you gain access toohello subscription.</span></span> <span data-ttu-id="433fc-488">檢視 hello[逐步指示](https://azure.microsoft.com/trial/get-started-machine-learning-b/)。</span><span class="sxs-lookup"><span data-stu-id="433fc-488">View hello [step-by-step instructions](https://azure.microsoft.com/trial/get-started-machine-learning-b/).</span></span>

<span data-ttu-id="433fc-489">或者，您可以邀請由標準的機器學習服務工作區擁有者 tooaccess hello 擁有者的工作區。</span><span class="sxs-lookup"><span data-stu-id="433fc-489">Alternatively, you can be invited by a Standard Machine Learning workspace owner tooaccess hello owner's workspace.</span></span>

<span data-ttu-id="433fc-490">**可以指定自己的 Azure Blob 儲存體帳戶 toouse 與 hello 免費層嗎？**</span><span class="sxs-lookup"><span data-stu-id="433fc-490">**Can I specify my own Azure Blob storage account toouse with hello Free tier?**</span></span>

<span data-ttu-id="433fc-491">否，hello 標準層是 hello 機器學習服務層所導入的 hello 之前，對等 toohello 版本。</span><span class="sxs-lookup"><span data-stu-id="433fc-491">No, hello Standard tier is equivalent toohello version of hello Machine Learning service that was available before hello tiers were introduced.</span></span>

<span data-ttu-id="433fc-492">**可以部署我的機器學習模型做為應用程式開發介面，hello 免費層中嗎？**</span><span class="sxs-lookup"><span data-stu-id="433fc-492">**Can I deploy my machine learning models as APIs in hello Free tier?**</span></span>

<span data-ttu-id="433fc-493">是，您可以實施機器學習模型 toostaging API services hello 免費層的一部分。</span><span class="sxs-lookup"><span data-stu-id="433fc-493">Yes, you can operationalize machine learning models toostaging API services as part of hello Free tier.</span></span> <span data-ttu-id="433fc-494">tooput hello 接 API 服務移到實際執行環境和生產環境端點取得 hello 實際運作的服務，您必須使用 hello Standard 價格區間。</span><span class="sxs-lookup"><span data-stu-id="433fc-494">tooput hello staging API service into production and get a production endpoint for hello operationalized service, you must use hello Standard tier.</span></span>

<span data-ttu-id="433fc-495">**Hello Azure 免費試用版與 Azure 機器學習免費層之間的差異為何？**</span><span class="sxs-lookup"><span data-stu-id="433fc-495">**What is hello difference between Azure free trial and Azure Machine Learning Free tier?**</span></span>

<span data-ttu-id="433fc-496">hello [Microsoft Azure 免費試用](https://azure.microsoft.com/free/)提供信用額度，您可以套用 tooany Azure 服務的一個月。</span><span class="sxs-lookup"><span data-stu-id="433fc-496">hello [Microsoft Azure free trial](https://azure.microsoft.com/free/) offers credits that you can apply tooany Azure service for one month.</span></span> <span data-ttu-id="433fc-497">hello Azure 機器學習 Free 層提供連續存取特別 tooAzure Machine Learning 針對非生產工作負載。</span><span class="sxs-lookup"><span data-stu-id="433fc-497">hello Azure Machine Learning Free tier offers continuous access specifically tooAzure Machine Learning for non-production workloads.</span></span>

<span data-ttu-id="433fc-498">**如何從 hello 免費層 toohello 標準層中移動實驗？**</span><span class="sxs-lookup"><span data-stu-id="433fc-498">**How do I move an experiment from hello Free tier toohello Standard tier?**</span></span>

<span data-ttu-id="433fc-499">toocopy hello 免費層 toohello 標準層將實驗：</span><span class="sxs-lookup"><span data-stu-id="433fc-499">toocopy your experiments from hello Free tier toohello Standard tier:</span></span>

1. <span data-ttu-id="433fc-500">登入 tooAzure Machine Learning Studio 中，並請確定您可以看到 hello 免費工作區和 hello hello hello 上方導覽列中的工作區選取器中的 [標準] 工作區。</span><span class="sxs-lookup"><span data-stu-id="433fc-500">Sign in tooAzure Machine Learning Studio, and make sure that you can see both hello Free workspace and hello Standard workspace in hello workspace selector in hello top navigation bar.</span></span>
2. <span data-ttu-id="433fc-501">如果您是在 hello 標準工作區，請切換 tooFree 工作區。</span><span class="sxs-lookup"><span data-stu-id="433fc-501">Switch tooFree workspace if you are in hello Standard workspace.</span></span>
3. <span data-ttu-id="433fc-502">在 hello 實驗清單檢視中，選取 實驗，您會想 toocopy，，然後按一下hello**複製**命令按鈕。</span><span class="sxs-lookup"><span data-stu-id="433fc-502">In hello experiment list view, select an experiment that you'd like toocopy, and then click hello **Copy** command button.</span></span>
4. <span data-ttu-id="433fc-503">從 hello 對話方塊中，開啟時，請選取 hello 標準工作區，然後按一下hello**複製** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="433fc-503">Select hello Standard workspace from hello dialog box that opens, and then click hello **Copy** button.</span></span>
   <span data-ttu-id="433fc-504">所有 hello 相關聯的資料集，定型的模型，會複製與 hello 實驗 hello 標準工作區。</span><span class="sxs-lookup"><span data-stu-id="433fc-504">All hello associated datasets, trained model, etc. are copied together with hello experiment into hello Standard workspace.</span></span>
5. <span data-ttu-id="433fc-505">您需要 toorerun hello 實驗，並重新發佈 web 服務 hello 標準工作區中的。</span><span class="sxs-lookup"><span data-stu-id="433fc-505">You need toorerun hello experiment and republish your web service in hello Standard workspace.</span></span>

### <a name="studio-workspace"></a><span data-ttu-id="433fc-506">Studio 工作區</span><span class="sxs-lookup"><span data-stu-id="433fc-506">Studio workspace</span></span>
<span data-ttu-id="433fc-507">**不同的工作區會有不同的帳單嗎？**</span><span class="sxs-lookup"><span data-stu-id="433fc-507">**Will I see different bills for different workspaces?**</span></span>

<span data-ttu-id="433fc-508">一份帳單上，工作區費用會依每個適用的度量而個別細分。</span><span class="sxs-lookup"><span data-stu-id="433fc-508">Workspace charges are broken out separately for each applicable meter on a single bill.</span></span>

<span data-ttu-id="433fc-509">**我的實驗作業會在何種特定類型的計算資源上進行？**</span><span class="sxs-lookup"><span data-stu-id="433fc-509">**What specific kind of compute resources will my experiments be run on?**</span></span>

<span data-ttu-id="433fc-510">hello 機器學習服務是一個多租用戶的服務。</span><span class="sxs-lookup"><span data-stu-id="433fc-510">hello Machine Learning service is a multitenant service.</span></span> <span data-ttu-id="433fc-511">Hello 後端所使用的實際計算資源而有所不同，而且會針對效能和可預測性最佳化。</span><span class="sxs-lookup"><span data-stu-id="433fc-511">Actual compute resources that are used on hello back end vary and are optimized for performance and predictability.</span></span>

### <a name="guest-access"></a><span data-ttu-id="433fc-512">來賓存取</span><span class="sxs-lookup"><span data-stu-id="433fc-512">Guest Access</span></span>
<span data-ttu-id="433fc-513">**什麼是來賓存取 tooAzure Machine Learning Studio？**</span><span class="sxs-lookup"><span data-stu-id="433fc-513">**What is Guest Access tooAzure Machine Learning Studio?**</span></span>

<span data-ttu-id="433fc-514">「來賓存取」是有限制的試用經驗。</span><span class="sxs-lookup"><span data-stu-id="433fc-514">Guest Access is a restricted trial experience.</span></span> <span data-ttu-id="433fc-515">您可以在不經驗證的情況下，於 Azure Machine Learning Studio 中免費建立及執行實驗。</span><span class="sxs-lookup"><span data-stu-id="433fc-515">You can create and run experiments in Azure Machine Learning Studio at no cost and without authentication.</span></span> <span data-ttu-id="433fc-516">客體工作階段是在非持續性 （無法儲存），限制 tooeight 小時。</span><span class="sxs-lookup"><span data-stu-id="433fc-516">Guest sessions are non-persistent (cannot be saved) and limited tooeight hours.</span></span> <span data-ttu-id="433fc-517">其他限制包括缺少 R 和 Python 支援、缺少預備 API，以及有限的資料集大小和儲存體容量。</span><span class="sxs-lookup"><span data-stu-id="433fc-517">Other limitations include lack of support for R and Python, lack of staging APIs, and restricted dataset size and storage capacity.</span></span> <span data-ttu-id="433fc-518">相較之下，選擇 toosign 使用 Microsoft 帳戶的使用者擁有完整存取 toohello 免費層的機器學習 Studio 之前，描述其中包括持續性工作區和更完整的功能。</span><span class="sxs-lookup"><span data-stu-id="433fc-518">By comparison, users who choose toosign in with a Microsoft account have full access toohello Free tier of Machine Learning Studio that's described previously, which includes a persistent workspace and more comprehensive capabilities.</span></span> <span data-ttu-id="433fc-519">toochoose 免費的機器學習遇到按一下**開始**上[https://studio.azureml.net](https://studio.azureml.net)，然後選取**猜測存取**或使用 Microsoft 登入。帳戶。</span><span class="sxs-lookup"><span data-stu-id="433fc-519">toochoose your free Machine Learning experience, click **Get started** on [https://studio.azureml.net](https://studio.azureml.net), and then select **Guess Access** or sign in with a Microsoft account.</span></span>

<!-- Module References -->
[image-reader]: https://msdn.microsoft.com/library/azure/893f8c57-1d36-456d-a47b-d29ae67f5d84/
[join]: https://msdn.microsoft.com/library/azure/124865f7-e901-4656-adac-f4cb08248099/
[machine-learning-modules]: https://msdn.microsoft.com/library/azure/6d9e2516-1343-4859-a3dc-9673ccec9edc/
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[python]: https://msdn.microsoft.com/library/azure/CDB56F95-7F4C-404D-BDE7-5BB972E6F232
[counts]: https://msdn.microsoft.com/library/azure/dn913056.aspx
