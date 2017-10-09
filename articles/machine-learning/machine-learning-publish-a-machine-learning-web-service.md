---
title: "aaaDeploy 機器學習 web 服務 |Microsoft 文件"
description: "如何 tooconvert 訓練試驗 tooa 預測實驗，準備進行部署，然後將其部署為 Azure Machine Learning web 服務。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 73a3e9c6-00d0-41d4-8cf1-2ec87713867e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9cb7af637632b2c3688c11483f29cf24df8fd065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-machine-learning-web-service"></a><span data-ttu-id="2bc62-103">部署 Azure Machine Learning Web 服務</span><span class="sxs-lookup"><span data-stu-id="2bc62-103">Deploy an Azure Machine Learning web service</span></span>
<span data-ttu-id="2bc62-104">Azure 機器學習可讓您 toobuild、 測試及部署預測分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="2bc62-104">Azure Machine Learning enables you toobuild, test, and deploy predictive analytic solutions.</span></span>

<span data-ttu-id="2bc62-105">從高階觀點而言，由下列三個步驟完成這個動作：</span><span class="sxs-lookup"><span data-stu-id="2bc62-105">From a high-level point-of-view, this is done in three steps:</span></span>

* <span data-ttu-id="2bc62-106">**[建立定型實驗]** -Azure Machine Learning Studio 是共同作業視覺式開發環境，您使用 tootrain 及測試預測分析模型使用您提供的定型資料。</span><span class="sxs-lookup"><span data-stu-id="2bc62-106">**[Create a training experiment]** - Azure Machine Learning Studio is a collaborative visual development environment that you use tootrain and test a predictive analytics model using training data that you supply.</span></span>
* <span data-ttu-id="2bc62-107">**[將它轉換 tooa 預測實驗]** -一旦您的模型已定型使用現有的資料，您已經準備好 toouse 它 tooscore 新的資料，您準備和簡化您的經驗，用於預測。</span><span class="sxs-lookup"><span data-stu-id="2bc62-107">**[Convert it tooa predictive experiment]** - Once your model has been trained with existing data and you're ready toouse it tooscore new data, you prepare and streamline your experiment for predictions.</span></span>
* <span data-ttu-id="2bc62-108">**[將其部署為 Web 服務]** - 您可以將預測實驗部署為[新式]或[傳統] Azure Web 服務。</span><span class="sxs-lookup"><span data-stu-id="2bc62-108">**[Deploy it as a web service]** - You can deploy your predictive experiment as a [new] or [classic] Azure web service.</span></span> <span data-ttu-id="2bc62-109">使用者可以傳送資料 tooyour 模型及接收模型的預測。</span><span class="sxs-lookup"><span data-stu-id="2bc62-109">Users can send data tooyour model and receive your model's predictions.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="create-a-training-experiment"></a><span data-ttu-id="2bc62-110">建立訓練實驗</span><span class="sxs-lookup"><span data-stu-id="2bc62-110">Create a training experiment</span></span>
<span data-ttu-id="2bc62-111">tootrain 預測分析模型，使用 Azure Machine Learning Studio toocreate 定型實驗，其中您包含各種模組 tooload 定型資料、 準備視 hello 資料、 套用機器學習演算法，以及評估 hello 結果.</span><span class="sxs-lookup"><span data-stu-id="2bc62-111">tootrain a predictive analytics model, you use Azure Machine Learning Studio toocreate a training experiment where you include various modules tooload training data, prepare hello data as necessary, apply machine learning algorithms, and evaluate hello results.</span></span> <span data-ttu-id="2bc62-112">您可以逐一查看實驗和不同的機器學習演算法 toocompare 再試一次並評估 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="2bc62-112">You can iterate on an experiment and try different machine learning algorithms toocompare and evaluate hello results.</span></span>

<span data-ttu-id="2bc62-113">建立和管理定型實驗 hello 程序涵蓋更詳盡地其他位置。</span><span class="sxs-lookup"><span data-stu-id="2bc62-113">hello process of creating and managing training experiments is covered more thoroughly elsewhere.</span></span> <span data-ttu-id="2bc62-114">如需詳細資訊，請參閱這些文章：</span><span class="sxs-lookup"><span data-stu-id="2bc62-114">For more information, see these articles:</span></span>

* [<span data-ttu-id="2bc62-115">在 Azure Machine Learning Studio 中建立簡單實驗</span><span class="sxs-lookup"><span data-stu-id="2bc62-115">Create a simple experiment in Azure Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="2bc62-116">使用 Azure Machine Learning 開發預測解決方案</span><span class="sxs-lookup"><span data-stu-id="2bc62-116">Develop a predictive solution with Azure Machine Learning</span></span>](machine-learning-walkthrough-develop-predictive-solution.md)
* [<span data-ttu-id="2bc62-117">將訓練資料匯入 Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="2bc62-117">Import your training data into Azure Machine Learning Studio</span></span>](machine-learning-data-science-import-data.md)
* [<span data-ttu-id="2bc62-118">在 Azure Machine Learning Studio 中管理實驗逐一查看</span><span class="sxs-lookup"><span data-stu-id="2bc62-118">Manage experiment iterations in Azure Machine Learning Studio</span></span>](machine-learning-manage-experiment-iterations.md)

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a><span data-ttu-id="2bc62-119">轉換 hello 定型實驗 tooa 預測實驗</span><span class="sxs-lookup"><span data-stu-id="2bc62-119">Convert hello training experiment tooa predictive experiment</span></span>
<span data-ttu-id="2bc62-120">一旦您已經定型模型，您準備好 tooconvert 訓練試驗預測實驗 tooscore 新資料。</span><span class="sxs-lookup"><span data-stu-id="2bc62-120">Once you've trained your model, you're ready tooconvert your training experiment into a predictive experiment tooscore new data.</span></span>

<span data-ttu-id="2bc62-121">藉由轉換 tooa 預測進行實驗，您要取得您定型的模型就緒 toobe 部署為計分的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="2bc62-121">By converting tooa predictive experiment, you're getting your trained model ready toobe deployed as a scoring web service.</span></span> <span data-ttu-id="2bc62-122">Hello web 服務的使用者可以傳送輸入的資料 tooyour 模型和您的模型會將傳送後 hello 預測結果。</span><span class="sxs-lookup"><span data-stu-id="2bc62-122">Users of hello web service can send input data tooyour model and your model will send back hello prediction results.</span></span> <span data-ttu-id="2bc62-123">當您轉換 tooa 預測實驗之後，請記住您希望其他人使用您模型 toobe 如何。</span><span class="sxs-lookup"><span data-stu-id="2bc62-123">As you convert tooa predictive experiment, keep in mind how you expect your model toobe used by others.</span></span>

<span data-ttu-id="2bc62-124">tooconvert 預測您定型實驗 tooa 實驗中，按一下**執行**在 hello hello 實驗畫布底部，按一下 **設定 Web 服務**，然後選取**預測 Web 服務**.</span><span class="sxs-lookup"><span data-stu-id="2bc62-124">tooconvert your training experiment tooa predictive experiment, click **Run** at hello bottom of hello experiment canvas, click **Set Up Web Service**, then select **Predictive Web Service**.</span></span>

![轉換 tooscoring 實驗](./media/machine-learning-publish-a-machine-learning-web-service/figure-1.png)

<span data-ttu-id="2bc62-126">如需有關如何 tooperform 這項轉換，請參閱[如何 tooprepare Azure Machine Learning Studio 中的部署模型](machine-learning-convert-training-experiment-to-scoring-experiment.md)。</span><span class="sxs-lookup"><span data-stu-id="2bc62-126">For more information on how tooperform this conversion, see [How tooprepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="2bc62-127">hello 下列步驟描述部署為新的 web 服務的預測實驗。</span><span class="sxs-lookup"><span data-stu-id="2bc62-127">hello following steps describe deploying a predictive experiment as a New web service.</span></span> <span data-ttu-id="2bc62-128">您也可以部署 hello 實驗與傳統 web 服務。</span><span class="sxs-lookup"><span data-stu-id="2bc62-128">You can also deploy hello experiment as Classic web service.</span></span>

## <a name="deploy-it-as-a-web-service"></a><span data-ttu-id="2bc62-129">將其部署為 Web 服務</span><span class="sxs-lookup"><span data-stu-id="2bc62-129">Deploy it as a web service</span></span>

<span data-ttu-id="2bc62-130">為新的 web 服務或傳統 web 服務，您可以部署 hello 預測實驗。</span><span class="sxs-lookup"><span data-stu-id="2bc62-130">You can deploy hello predictive experiment as a New web service or as a Classic web service.</span></span>

### <a name="deploy-hello-predictive-experiment-as-a-new-web-service"></a><span data-ttu-id="2bc62-131">部署為新的 web 服務的 hello 預測實驗</span><span class="sxs-lookup"><span data-stu-id="2bc62-131">Deploy hello predictive experiment as a New web service</span></span>
<span data-ttu-id="2bc62-132">既然 hello 預測實驗已備妥，您可以將其部署為新的 Azure web 服務。</span><span class="sxs-lookup"><span data-stu-id="2bc62-132">Now that hello predictive experiment has been prepared, you can deploy it as a new Azure web service.</span></span> <span data-ttu-id="2bc62-133">使用 hello web 服務，使用者可以傳送資料 tooyour 模型和 hello 模型將會傳回預測。</span><span class="sxs-lookup"><span data-stu-id="2bc62-133">Using hello web service, users can send data tooyour model and hello model will return its predictions.</span></span>

<span data-ttu-id="2bc62-134">toodeploy 您預測進行實驗，請按一下**執行**底部 hello hello 實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="2bc62-134">toodeploy your predictive experiment, click **Run** at hello bottom of hello experiment canvas.</span></span> <span data-ttu-id="2bc62-135">一旦 hello 實驗完成執行後，按一下 **部署 Web 服務**選取**部署 Web 服務[新增]**。</span><span class="sxs-lookup"><span data-stu-id="2bc62-135">Once hello experiment has finished running, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span></span>  <span data-ttu-id="2bc62-136">hello 部署的 hello Machine Learning Web 服務入口網站 頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="2bc62-136">hello deployment page of hello Machine Learning Web Service portal opens.</span></span>

> [!NOTE] 
> <span data-ttu-id="2bc62-137">toodeploy 新的 web 服務，您必須擁有足夠的權限 hello 訂用帳戶 toowhich 您部署 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="2bc62-137">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="2bc62-138">如需詳細資訊，請參閱[管理 Web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="2bc62-138">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

#### <a name="machine-learning-web-service-portal-deploy-experiment-page"></a><span data-ttu-id="2bc62-139">Machine Learning Web 服務入口網站 [部署實驗] 頁面</span><span class="sxs-lookup"><span data-stu-id="2bc62-139">Machine Learning Web Service portal Deploy Experiment Page</span></span>
<span data-ttu-id="2bc62-140">在 hello 部署實驗 頁面上，輸入 hello web 服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="2bc62-140">On hello Deploy Experiment page, enter a name for hello web service.</span></span>
<span data-ttu-id="2bc62-141">選取定價方案。</span><span class="sxs-lookup"><span data-stu-id="2bc62-141">Select a pricing plan.</span></span> <span data-ttu-id="2bc62-142">如果您有現有的定價方案，您可以選取它，否則您必須建立新的價格計劃 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="2bc62-142">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for hello service.</span></span>

1. <span data-ttu-id="2bc62-143">在 hello**價格計劃**下拉式清單中，選取現有的方案或選取 hello**選取新的計畫**選項。</span><span class="sxs-lookup"><span data-stu-id="2bc62-143">In hello **Price Plan** drop down, select an existing plan or select hello **Select new plan** option.</span></span>
2. <span data-ttu-id="2bc62-144">在**計劃名稱**，輸入會識別在帳單上的 hello 計劃的名稱。</span><span class="sxs-lookup"><span data-stu-id="2bc62-144">In **Plan Name**, type a name that will identify hello plan on your bill.</span></span>
3. <span data-ttu-id="2bc62-145">選取其中一個 hello**每月的計劃層**。</span><span class="sxs-lookup"><span data-stu-id="2bc62-145">Select one of hello **Monthly Plan Tiers**.</span></span> <span data-ttu-id="2bc62-146">hello 計劃層預設 toohello 計劃您預設的地區和您的 web 服務是部署的 toothat 區域。</span><span class="sxs-lookup"><span data-stu-id="2bc62-146">hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

<span data-ttu-id="2bc62-147">按一下**部署**和 hello**快速入門**web 服務 頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="2bc62-147">Click **Deploy** and hello **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="2bc62-148">hello web 服務快速入門 頁面可讓您存取和指引 hello 建立 web 服務之後，您將執行的最常見工作。</span><span class="sxs-lookup"><span data-stu-id="2bc62-148">hello web service Quickstart page gives you access and guidance on hello most common tasks you will perform after creating a web service.</span></span> <span data-ttu-id="2bc62-149">從這裡，您可以輕鬆地存取 hello 測試頁和取用的頁面。</span><span class="sxs-lookup"><span data-stu-id="2bc62-149">From here, you can easily access both hello Test page and Consume page.</span></span>

<!-- ![Deploy hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)-->

#### <a name="test-your-new-web-service"></a><span data-ttu-id="2bc62-150">測試新式 Web 服務</span><span class="sxs-lookup"><span data-stu-id="2bc62-150">Test your New web service</span></span>
<span data-ttu-id="2bc62-151">tootest 新的 web 服務，按一下 **測試 web 服務**在一般工作。</span><span class="sxs-lookup"><span data-stu-id="2bc62-151">tootest your new web service, click **Test web service** under common tasks.</span></span> <span data-ttu-id="2bc62-152">您可以在 hello 測試頁面上，測試您的 web 服務做為要求-回應服務 (RR) 或批次執行服務 (BES)。</span><span class="sxs-lookup"><span data-stu-id="2bc62-152">On hello Test page, you can test your web service as a Request-Response Service (RRS) or a Batch Execution service (BES).</span></span>

<span data-ttu-id="2bc62-153">hello RR 測試頁面會顯示 hello 輸入、 輸出和 hello 實驗，您已定義任何全域參數。</span><span class="sxs-lookup"><span data-stu-id="2bc62-153">hello RRS test page displays hello inputs, outputs, and any global parameters that you have defined for hello experiment.</span></span> <span data-ttu-id="2bc62-154">tootest hello web 服務，您可以手動輸入適當的值 hello 輸入，或是提供逗號分隔值 (CSV) 格式的檔案包含 hello 測試值。</span><span class="sxs-lookup"><span data-stu-id="2bc62-154">tootest hello web service, you can manually enter appropriate values for hello inputs or supply a comma separated value (CSV) formatted file containing hello test values.</span></span>

<span data-ttu-id="2bc62-155">使用 RR，tootest 從 hello 清單檢視模式中，輸入適當的值為 hello 輸入，然後按一下**測試要求-回應**。</span><span class="sxs-lookup"><span data-stu-id="2bc62-155">tootest using RRS, from hello list view mode, enter appropriate values for hello inputs and click **Test Request-Response**.</span></span> <span data-ttu-id="2bc62-156">在左 hello 輸出資料行 toohello 中，顯示預測結果。</span><span class="sxs-lookup"><span data-stu-id="2bc62-156">Your prediction results  display in hello output column toohello left.</span></span>

![部署 hello web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-5-test-request-response.png)

<span data-ttu-id="2bc62-158">按一下 tootest 您 BES**批次**。</span><span class="sxs-lookup"><span data-stu-id="2bc62-158">tootest your BES, click **Batch**.</span></span> <span data-ttu-id="2bc62-159">在 hello 批次測試頁面上，按一下 瀏覽在您的輸入，並選取包含適當的樣本值的 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="2bc62-159">On hello Batch test page, click Browse under your input and select a CSV file containing appropriate sample values.</span></span> <span data-ttu-id="2bc62-160">如果您不需要為 CSV 檔，並且使用 Machine Learning Studio 預測實驗，您可以下載預測實驗 hello 資料集，並使用它。</span><span class="sxs-lookup"><span data-stu-id="2bc62-160">If you don't have a CSV file, and you created your predictive experiment using Machine Learning Studio, you can download hello data set for your predictive experiment and use it.</span></span>

<span data-ttu-id="2bc62-161">toodownload hello 資料集，開啟 Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="2bc62-161">toodownload hello data set, open Machine Learning Studio.</span></span> <span data-ttu-id="2bc62-162">開啟您預測的經驗，並以滑鼠右鍵按一下您的經驗的 hello 輸入。</span><span class="sxs-lookup"><span data-stu-id="2bc62-162">Open your predictive experiment and right click hello input for your experiment.</span></span> <span data-ttu-id="2bc62-163">Hello 內容功能表中選取**資料集**，然後選取 **下載**。</span><span class="sxs-lookup"><span data-stu-id="2bc62-163">From hello context menu, select **dataset** and then select **Download**.</span></span>

![部署 hello web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-7-mls-download.png)

<span data-ttu-id="2bc62-165">按一下 [ **測試**]。</span><span class="sxs-lookup"><span data-stu-id="2bc62-165">Click **Test**.</span></span> <span data-ttu-id="2bc62-166">批次執行作業的 hello 狀態就會顯示下的 toohello 右邊**測試批次作業**。</span><span class="sxs-lookup"><span data-stu-id="2bc62-166">hello status of your Batch Execution job displays toohello right under **Test Batch Jobs**.</span></span>

![部署 hello web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-6-test-batch-execution.png)

<!--![Test hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)-->

<span data-ttu-id="2bc62-168">在 [hello**組態**] 頁面上，您可以變更 hello 描述、 標題、 更新 hello 儲存體帳戶金鑰，並啟用您的 web 服務的範例資料。</span><span class="sxs-lookup"><span data-stu-id="2bc62-168">On hello **CONFIGURATION** page, you can change hello description, title, update hello storage account key, and enable sample data for your web service.</span></span>

![設定 hello web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-8-arm-configure.png)

<span data-ttu-id="2bc62-170">一旦您已部署的 hello web 服務，您可以：</span><span class="sxs-lookup"><span data-stu-id="2bc62-170">Once you've deployed hello web service, you can:</span></span>

* <span data-ttu-id="2bc62-171">**存取**透過 hello web 服務 API。</span><span class="sxs-lookup"><span data-stu-id="2bc62-171">**Access** it through hello web service API.</span></span>
* <span data-ttu-id="2bc62-172">**管理**透過 Azure Machine Learning web 服務入口網站或 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="2bc62-172">**Manage** it through Azure Machine Learning web services portal or hello Azure classic portal.</span></span>
* <span data-ttu-id="2bc62-173">**更新** 它。</span><span class="sxs-lookup"><span data-stu-id="2bc62-173">**Update** it if your model changes.</span></span>

#### <a name="access-your-new-web-service"></a><span data-ttu-id="2bc62-174">存取新式 Web 服務</span><span class="sxs-lookup"><span data-stu-id="2bc62-174">Access your New web service</span></span>
<span data-ttu-id="2bc62-175">一旦您部署您的 web 服務從 Machine Learning Studio 時，您可以傳送資料 toohello 服務和以程式設計的方式接收回應。</span><span class="sxs-lookup"><span data-stu-id="2bc62-175">Once you deploy your web service from Machine Learning Studio, you can send data toohello service and receive responses programmatically.</span></span>

<span data-ttu-id="2bc62-176">hello**取用**頁面會提供您的 web 服務需要 tooaccess 所有 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="2bc62-176">hello **Consume** page provides all hello information you need tooaccess your web service.</span></span> <span data-ttu-id="2bc62-177">例如，hello API 金鑰會提供 tooallow 獲授權存取 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="2bc62-177">For example, hello API key is provided tooallow authorized access toohello service.</span></span>

<span data-ttu-id="2bc62-178">如需存取的機器學習 web 服務的詳細資訊，請參閱[如何 tooconsume Azure 機器學習 Web 服務](machine-learning-consume-web-services.md)。</span><span class="sxs-lookup"><span data-stu-id="2bc62-178">For more information about accessing a Machine Learning web service, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

#### <a name="manage-your-new-web-service"></a><span data-ttu-id="2bc62-179">管理新式 Web 服務</span><span class="sxs-lookup"><span data-stu-id="2bc62-179">Manage your New web service</span></span>
<span data-ttu-id="2bc62-180">您可以在 Machine Learning Web 服務入口網站中管理新的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="2bc62-180">You can manage your New web services Machine Learning Web Services portal.</span></span> <span data-ttu-id="2bc62-181">從 hello[主要入口網站頁面](https://services.azureml-test.net/)，按一下  **Web 服務**。</span><span class="sxs-lookup"><span data-stu-id="2bc62-181">From hello [main portal page](https://services.azureml-test.net/), click **Web Services**.</span></span> <span data-ttu-id="2bc62-182">從 hello web 服務 頁面上，您可以刪除或複製的服務。</span><span class="sxs-lookup"><span data-stu-id="2bc62-182">From hello web services page, you can delete or copy a service.</span></span> <span data-ttu-id="2bc62-183">toomonitor 特定服務中，按一下 hello 服務，然後按一下**儀表板**。</span><span class="sxs-lookup"><span data-stu-id="2bc62-183">toomonitor a specific service, click hello service and then click **Dashboard**.</span></span> <span data-ttu-id="2bc62-184">按一下 toomonitor hello web 服務，與相關聯的批次作業**批次要求記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="2bc62-184">toomonitor batch jobs associated with hello web service, click **Batch Request Log**.</span></span>

### <a name="deploy-hello-predictive-experiment-as-a-classic-web-service"></a><span data-ttu-id="2bc62-185">與傳統 web 服務部署 hello 預測實驗</span><span class="sxs-lookup"><span data-stu-id="2bc62-185">Deploy hello predictive experiment as a Classic web service</span></span>

<span data-ttu-id="2bc62-186">既然已充分備妥 hello 預測實驗，您可以將其部署為傳統 Azure web 服務。</span><span class="sxs-lookup"><span data-stu-id="2bc62-186">Now that hello predictive experiment has been sufficiently prepared, you can deploy it as a Classic Azure web service.</span></span> <span data-ttu-id="2bc62-187">使用 hello web 服務，使用者可以傳送資料 tooyour 模型和 hello 模型將會傳回預測。</span><span class="sxs-lookup"><span data-stu-id="2bc62-187">Using hello web service, users can send data tooyour model and hello model will return its predictions.</span></span>

<span data-ttu-id="2bc62-188">toodeploy 您預測進行實驗，請按一下**執行**底部 hello hello 試驗畫布，然後按一下**部署 Web 服務**。</span><span class="sxs-lookup"><span data-stu-id="2bc62-188">toodeploy your predictive experiment, click **Run** at hello bottom of hello experiment canvas and then click **Deploy Web Service**.</span></span> <span data-ttu-id="2bc62-189">hello web 服務的設定，您會放置在 hello web 服務儀表板中。</span><span class="sxs-lookup"><span data-stu-id="2bc62-189">hello web service is set up and you are placed in hello web service dashboard.</span></span>

![部署 hello web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)

#### <a name="test-your-classic-web-service"></a><span data-ttu-id="2bc62-191">測試傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="2bc62-191">Test your Classic web service</span></span>

<span data-ttu-id="2bc62-192">您可以在 hello 機器學習 Web 服務入口網站或 Machine Learning Studio 中測試 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="2bc62-192">You can test hello web service in either hello Machine Learning Web Services portal or Machine Learning Studio.</span></span>

<span data-ttu-id="2bc62-193">tootest hello 的要求回應 web 服務，按一下 hello**測試**hello web 服務儀表板 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2bc62-193">tootest hello Request Response web service, click hello **Test** button in hello web service dashboard.</span></span> <span data-ttu-id="2bc62-194">對話方塊會出現 tooask 您 hello hello 服務的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="2bc62-194">A dialog pops up tooask you for hello input data for hello service.</span></span> <span data-ttu-id="2bc62-195">這些是 hello hello 計分實驗所預期的資料行。</span><span class="sxs-lookup"><span data-stu-id="2bc62-195">These are hello columns expected by hello scoring experiment.</span></span> <span data-ttu-id="2bc62-196">輸入一組資料，然後按一下確定 。</span><span class="sxs-lookup"><span data-stu-id="2bc62-196">Enter a set of data and then click **OK**.</span></span> <span data-ttu-id="2bc62-197">hello hello web 服務所產生的結果會顯示在 hello hello 儀表板底部。</span><span class="sxs-lookup"><span data-stu-id="2bc62-197">hello results generated by hello web service are displayed at hello bottom of hello dashboard.</span></span>

<span data-ttu-id="2bc62-198">您可以按一下 hello**測試**預覽連結 tootest 您 hello Azure 機器學習 Web 服務入口網站中的服務，如先前在 hello 新的 web 服務 > 一節中所示。</span><span class="sxs-lookup"><span data-stu-id="2bc62-198">You can click hello **Test** preview link tootest your service in hello Azure Machine Learning Web Services portal as shown previously in hello New web service section.</span></span>

<span data-ttu-id="2bc62-199">tootest hello 批次執行服務，按一下**測試**預覽連結。</span><span class="sxs-lookup"><span data-stu-id="2bc62-199">tootest hello Batch Execution Service, click **Test** preview link .</span></span> <span data-ttu-id="2bc62-200">在 hello 批次測試頁面上，按一下 瀏覽在您的輸入，並選取包含適當的樣本值的 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="2bc62-200">On hello Batch test page, click Browse under your input and select a CSV file containing appropriate sample values.</span></span> <span data-ttu-id="2bc62-201">如果您不需要為 CSV 檔，並且使用 Machine Learning Studio 預測實驗，您可以下載預測實驗 hello 資料集，並使用它。</span><span class="sxs-lookup"><span data-stu-id="2bc62-201">If you don't have a CSV file, and you created your predictive experiment using Machine Learning Studio, you can download hello data set for your predictive experiment and use it.</span></span>

![測試 hello web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)

<span data-ttu-id="2bc62-203">在 [hello**組態**] 頁面上，您可以變更 hello hello 服務顯示名稱，並提供它的描述。</span><span class="sxs-lookup"><span data-stu-id="2bc62-203">On hello **CONFIGURATION** page, you can change hello display name of hello service and give it a description.</span></span> <span data-ttu-id="2bc62-204">hello 名稱和描述會顯示在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)您用來管理您的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="2bc62-204">hello name and description is displayed in hello [Azure classic portal](http://manage.windowsazure.com/) where you manage your web services.</span></span>

<span data-ttu-id="2bc62-205">您可以為輸入資料、輸出資料及 Web 服務參數提供描述，方法是在 [輸入結構描述]、[輸出結構描述] 及 [Web 服務參數] 底下的每個資料行輸入字串。</span><span class="sxs-lookup"><span data-stu-id="2bc62-205">You can provide a description for your input data, output data, and web service parameters by entering a string for each column under **INPUT SCHEMA**, **OUTPUT SCHEMA**, and **Web SERVICE PARAMETER**.</span></span> <span data-ttu-id="2bc62-206">Hello web 服務所提供的 hello 範例程式碼文件中，會使用這些說明。</span><span class="sxs-lookup"><span data-stu-id="2bc62-206">These descriptions are used in hello sample code documentation provided for hello web service.</span></span>

<span data-ttu-id="2bc62-207">您可以啟用記錄 toodiagnose 存取您的 web 服務時看見任何失敗。</span><span class="sxs-lookup"><span data-stu-id="2bc62-207">You can enable logging toodiagnose any failures that you're seeing when your web service is accessed.</span></span> <span data-ttu-id="2bc62-208">如需詳細資訊，請參閱 [為 Machine Learning Web 服務啟用記錄](machine-learning-web-services-logging.md)。</span><span class="sxs-lookup"><span data-stu-id="2bc62-208">For more information, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

![設定 hello web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-4.png)

<span data-ttu-id="2bc62-210">您也可以在 hello Azure 機器學習 Web 服務入口網站類似 toohello 程序稍早顯示 hello 新的 web 服務區段中設定 hello hello web 服務端點。</span><span class="sxs-lookup"><span data-stu-id="2bc62-210">You can also configure hello endpoints for hello web service in hello Azure Machine Learning Web Services portal similar toohello procedure shown previously in hello New web service section.</span></span> <span data-ttu-id="2bc62-211">hello 選項都不同，您可以新增或變更 hello 服務描述、 啟用記錄，以及啟用範例資料用於測試。</span><span class="sxs-lookup"><span data-stu-id="2bc62-211">hello options are different, you can add or change hello service description, enable logging, and enable sample data for testing.</span></span>

#### <a name="access-your-classic-web-service"></a><span data-ttu-id="2bc62-212">存取傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="2bc62-212">Access your Classic web service</span></span>
<span data-ttu-id="2bc62-213">一旦您部署您的 web 服務從 Machine Learning Studio 時，您可以傳送資料 toohello 服務和以程式設計的方式接收回應。</span><span class="sxs-lookup"><span data-stu-id="2bc62-213">Once you deploy your web service from Machine Learning Studio, you can send data toohello service and receive responses programmatically.</span></span>

<span data-ttu-id="2bc62-214">hello 儀表板提供您的 web 服務需要 tooaccess 所有 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="2bc62-214">hello dashboard provides all hello information you need tooaccess your web service.</span></span> <span data-ttu-id="2bc62-215">例如，hello API 金鑰是提供 tooallow 獲授權存取 toohello 服務，以及 API 說明頁面會提供的 toohelp 開始撰寫您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="2bc62-215">For example, hello API key is provided tooallow authorized access toohello service, and API help pages are provided toohelp you get started writing your code.</span></span>

<span data-ttu-id="2bc62-216">如需存取的機器學習 web 服務的詳細資訊，請參閱[如何 tooconsume Azure 機器學習 Web 服務](machine-learning-consume-web-services.md)。</span><span class="sxs-lookup"><span data-stu-id="2bc62-216">For more information about accessing a Machine Learning web service, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

#### <a name="manage-your-classic-web-service"></a><span data-ttu-id="2bc62-217">管理傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="2bc62-217">Manage your Classic web service</span></span>
<span data-ttu-id="2bc62-218">有各種不同的動作，您可以執行 toomonitor web 服務。</span><span class="sxs-lookup"><span data-stu-id="2bc62-218">There are various of actions you can perform toomonitor a web service.</span></span> <span data-ttu-id="2bc62-219">您可以更新它和刪除它。</span><span class="sxs-lookup"><span data-stu-id="2bc62-219">You can update it, and delete it.</span></span> <span data-ttu-id="2bc62-220">您也可以加入其他端點 tooa 傳統 web 服務加入 toohello 預設端點，當您在部署時建立。</span><span class="sxs-lookup"><span data-stu-id="2bc62-220">You can also add additional endpoints tooa Classic web service in addition toohello default endpoint that is created when you deploy it.</span></span>

<span data-ttu-id="2bc62-221">如需詳細資訊，請參閱[管理 Azure Machine Learning 工作區](machine-learning-manage-workspace.md)和[管理 web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="2bc62-221">For more information, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md) and [Manage a web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>

<!-- When this article gets published, fix hello link and uncomment
For more information on how toomanage Azure Machine Learning web service endpoints using hello REST API, see **Azure machine learning web service endpoints**.
-->

## <a name="update-hello-web-service"></a><span data-ttu-id="2bc62-222">更新 hello web 服務</span><span class="sxs-lookup"><span data-stu-id="2bc62-222">Update hello web service</span></span>
<span data-ttu-id="2bc62-223">您可以變更 tooyour web 服務，例如更新 hello 模型額外的定型資料並部署一次，覆寫 hello 原始 web 服務。</span><span class="sxs-lookup"><span data-stu-id="2bc62-223">You can make changes tooyour web service, such as updating hello model with additional training data, and deploy it again, overwriting hello original web service.</span></span>

<span data-ttu-id="2bc62-224">tooupdate hello web 服務，開啟 hello 原始預測實驗用 toodeploy hello web 服務，並依序按一下中進行編輯的複製**SAVE AS**。</span><span class="sxs-lookup"><span data-stu-id="2bc62-224">tooupdate hello web service, open hello original predictive experiment you used toodeploy hello web service and make an editable copy by clicking **SAVE AS**.</span></span> <span data-ttu-id="2bc62-225">進行變更，然後按一下部署 Web 服務 。</span><span class="sxs-lookup"><span data-stu-id="2bc62-225">Make your changes and then click **Deploy Web Service**.</span></span>

<span data-ttu-id="2bc62-226">因為您已部署此實驗之前，會要求您想 toooverwrite （傳統 Web 服務） 或更新 （新的 web 服務） hello 現有服務。</span><span class="sxs-lookup"><span data-stu-id="2bc62-226">Because you've deployed this experiment before, you are asked if you want toooverwrite (Classic Web Service) or update (New web service) hello existing service.</span></span> <span data-ttu-id="2bc62-227">按一下**是**或**更新**停止 hello 現有 web 服務和部署 hello 新預測實驗部署在其位置。</span><span class="sxs-lookup"><span data-stu-id="2bc62-227">Clicking **YES** or **Update** stops hello existing web service and deploys hello new predictive experiment is deployed in its place.</span></span>

> [!NOTE]
> <span data-ttu-id="2bc62-228">如果 hello 原始 web 服務中進行組態變更，例如，輸入新的顯示名稱或描述，您必須 tooenter 這些值一次。</span><span class="sxs-lookup"><span data-stu-id="2bc62-228">If you made configuration changes in hello original web service, for example, entering a new display name or description, you will need tooenter those values again.</span></span>
> 
> 

<span data-ttu-id="2bc62-229">更新您的 web 服務的其中一個選項以程式設計的方式是 tooretrain hello 模型。</span><span class="sxs-lookup"><span data-stu-id="2bc62-229">One option for updating your web service is tooretrain hello model programmatically.</span></span> <span data-ttu-id="2bc62-230">如需詳細資訊，請參閱 [以程式設計方式重塑機器學習模型](machine-learning-retrain-models-programmatically.md)。</span><span class="sxs-lookup"><span data-stu-id="2bc62-230">For more information, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

<!-- internal links -->
[建立定型實驗]: #create-a-training-experiment
[將它轉換 tooa 預測實驗]: #convert-the-training-experiment-to-a-predictive-experiment
[將其部署為 Web 服務]: #deploy-it-as-a-web-service
[新式]: #deploy-the-predictive-experiment-as-a-new-Web-service
[傳統]: #deploy-the-predictive-experiment-as-a-new-Web-service
[Access]: #access-the-Web-service
[Manage]: #manage-the-Web-service-in-the-azure-management-portal
[Update]: #update-the-Web-service
