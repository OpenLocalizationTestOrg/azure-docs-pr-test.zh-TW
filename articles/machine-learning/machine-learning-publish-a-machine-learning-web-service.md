---
title: "部署機器學習 Web 服務 | Microsoft Docs"
description: "如何將訓練實驗轉換為預測實驗，將其準備妥當進行部署，然後當做 Azure Machine Learning Web 服務發佈。"
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
ms.openlocfilehash: 39761f94efc530452a41ef9f2130976803cff711
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-an-azure-machine-learning-web-service"></a><span data-ttu-id="e2ac0-103">部署 Azure Machine Learning Web 服務</span><span class="sxs-lookup"><span data-stu-id="e2ac0-103">Deploy an Azure Machine Learning web service</span></span>
<span data-ttu-id="e2ac0-104">Azure Machine Learning 可讓您建置、測試以及部署預測性分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-104">Azure Machine Learning enables you to build, test, and deploy predictive analytic solutions.</span></span>

<span data-ttu-id="e2ac0-105">從高階觀點而言，由下列三個步驟完成這個動作：</span><span class="sxs-lookup"><span data-stu-id="e2ac0-105">From a high-level point-of-view, this is done in three steps:</span></span>

* <span data-ttu-id="e2ac0-106">**[建立訓練實驗]** - Azure Machine Learning Studio 是共同作業的視覺化開發環境，您使用所提供的訓練資料來訓練和測試預測分析模型。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-106">**[Create a training experiment]** - Azure Machine Learning Studio is a collaborative visual development environment that you use to train and test a predictive analytics model using training data that you supply.</span></span>
* <span data-ttu-id="e2ac0-107">**[將其轉換為預測實驗]** - 一旦您的模型已使用現有資料訓練好，並準備好使用該模型為新資料評分之後，您就是在準備並簡化您的實驗進行預測。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-107">**[Convert it to a predictive experiment]** - Once your model has been trained with existing data and you're ready to use it to score new data, you prepare and streamline your experiment for predictions.</span></span>
* <span data-ttu-id="e2ac0-108">**[將其部署為 Web 服務]** - 您可以將預測實驗部署為[新式]或[傳統] Azure Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-108">**[Deploy it as a web service]** - You can deploy your predictive experiment as a [new] or [classic] Azure web service.</span></span> <span data-ttu-id="e2ac0-109">使用者可以將資料傳送到您的模型以及接收您的模型的預測。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-109">Users can send data to your model and receive your model's predictions.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="create-a-training-experiment"></a><span data-ttu-id="e2ac0-110">建立訓練實驗</span><span class="sxs-lookup"><span data-stu-id="e2ac0-110">Create a training experiment</span></span>
<span data-ttu-id="e2ac0-111">若要訓練預測分析模型，您使用 Azure Machine Learning Studio 以建立訓練實驗，在其中包含各種模組以載入訓練資料、視需要準備資料、套用機器學習演算法，以及評估結果。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-111">To train a predictive analytics model, you use Azure Machine Learning Studio to create a training experiment where you include various modules to load training data, prepare the data as necessary, apply machine learning algorithms, and evaluate the results.</span></span> <span data-ttu-id="e2ac0-112">您可以逐一查看實驗，並且嘗試不同的機器學習演算法以比較及評估結果。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-112">You can iterate on an experiment and try different machine learning algorithms to compare and evaluate the results.</span></span>

<span data-ttu-id="e2ac0-113">關於建立和管理訓練實驗的處理，其他地方有更詳盡的說明。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-113">The process of creating and managing training experiments is covered more thoroughly elsewhere.</span></span> <span data-ttu-id="e2ac0-114">如需詳細資訊，請參閱這些文章：</span><span class="sxs-lookup"><span data-stu-id="e2ac0-114">For more information, see these articles:</span></span>

* [<span data-ttu-id="e2ac0-115">在 Azure Machine Learning Studio 中建立簡單實驗</span><span class="sxs-lookup"><span data-stu-id="e2ac0-115">Create a simple experiment in Azure Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="e2ac0-116">使用 Azure Machine Learning 開發預測解決方案</span><span class="sxs-lookup"><span data-stu-id="e2ac0-116">Develop a predictive solution with Azure Machine Learning</span></span>](machine-learning-walkthrough-develop-predictive-solution.md)
* [<span data-ttu-id="e2ac0-117">將訓練資料匯入 Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="e2ac0-117">Import your training data into Azure Machine Learning Studio</span></span>](machine-learning-data-science-import-data.md)
* [<span data-ttu-id="e2ac0-118">在 Azure Machine Learning Studio 中管理實驗逐一查看</span><span class="sxs-lookup"><span data-stu-id="e2ac0-118">Manage experiment iterations in Azure Machine Learning Studio</span></span>](machine-learning-manage-experiment-iterations.md)

## <a name="convert-the-training-experiment-to-a-predictive-experiment"></a><span data-ttu-id="e2ac0-119">將訓練實驗轉換為預測實驗</span><span class="sxs-lookup"><span data-stu-id="e2ac0-119">Convert the training experiment to a predictive experiment</span></span>
<span data-ttu-id="e2ac0-120">完成模型訓練後，您就可以將訓練實驗轉換成預測實驗，給新資料評分。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-120">Once you've trained your model, you're ready to convert your training experiment into a predictive experiment to score new data.</span></span>

<span data-ttu-id="e2ac0-121">轉換為預測實驗之後，您就準備好定型模型，可以當做評分 Web 服務部署。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-121">By converting to a predictive experiment, you're getting your trained model ready to be deployed as a scoring web service.</span></span> <span data-ttu-id="e2ac0-122">Web 服務的使用者可以將輸入資料傳送到您的模型，然後您的模型就會傳回預測結果。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-122">Users of the web service can send input data to your model and your model will send back the prediction results.</span></span> <span data-ttu-id="e2ac0-123">當您轉換為預測實驗時，必須記住您預期其他人會如何使用您的模型。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-123">As you convert to a predictive experiment, keep in mind how you expect your model to be used by others.</span></span>

<span data-ttu-id="e2ac0-124">若要將您的訓練實驗轉換為預測實驗，請按一下實驗畫布底端的 [執行]，按一下 [設定 Web 服務]，然後選取 [預測 Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-124">To convert your training experiment to a predictive experiment, click **Run** at the bottom of the experiment canvas, click **Set Up Web Service**, then select **Predictive Web Service**.</span></span>

![轉換為評分實驗](./media/machine-learning-publish-a-machine-learning-web-service/figure-1.png)

<span data-ttu-id="e2ac0-126">如需有關如何執行此對話的詳細資訊，請參閱[如何準備您的模型以在 Azure Machine Learning Studio 中部署](machine-learning-convert-training-experiment-to-scoring-experiment.md)。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-126">For more information on how to perform this conversion, see [How to prepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="e2ac0-127">下列步驟說明將預測實驗部署為新式 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-127">The following steps describe deploying a predictive experiment as a New web service.</span></span> <span data-ttu-id="e2ac0-128">您也可以將實驗部署為傳統 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-128">You can also deploy the experiment as Classic web service.</span></span>

## <a name="deploy-it-as-a-web-service"></a><span data-ttu-id="e2ac0-129">將其部署為 Web 服務</span><span class="sxs-lookup"><span data-stu-id="e2ac0-129">Deploy it as a web service</span></span>

<span data-ttu-id="e2ac0-130">您可以將預測實驗部署為「新式」或「傳統」Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-130">You can deploy the predictive experiment as a New web service or as a Classic web service.</span></span>

### <a name="deploy-the-predictive-experiment-as-a-new-web-service"></a><span data-ttu-id="e2ac0-131">將預測實驗部署為新式 Web 服務</span><span class="sxs-lookup"><span data-stu-id="e2ac0-131">Deploy the predictive experiment as a New web service</span></span>
<span data-ttu-id="e2ac0-132">既然已經備妥預測實驗，您現在即可將它部署為新式 Azure Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-132">Now that the predictive experiment has been prepared, you can deploy it as a new Azure web service.</span></span> <span data-ttu-id="e2ac0-133">使用者可以使用 Web 服務，將料傳送到您的模型，模型就會傳回其預測。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-133">Using the web service, users can send data to your model and the model will return its predictions.</span></span>

<span data-ttu-id="e2ac0-134">若要部署您的預測性實驗，請按一下實驗畫布底端的 [執行]  。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-134">To deploy your predictive experiment, click **Run** at the bottom of the experiment canvas.</span></span> <span data-ttu-id="e2ac0-135">實驗完成執行之後，請按一下 [部署 Web 服務]，然後選取 [部署 Web 服務[新式]]。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-135">Once the experiment has finished running, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span></span>  <span data-ttu-id="e2ac0-136">Machine Learning Web 服務入口網站的 [部署] 頁面將會開啟。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-136">The deployment page of the Machine Learning Web Service portal opens.</span></span>

> [!NOTE] 
> <span data-ttu-id="e2ac0-137">若要部署新的 Web 服務，您必須在要部署 Web 服務的訂用帳戶中具備足夠的權限。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-137">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="e2ac0-138">如需詳細資訊，請參閱[使用 Azure Machine Learning Web 服務入口網站管理 Web 服務](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-138">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

#### <a name="machine-learning-web-service-portal-deploy-experiment-page"></a><span data-ttu-id="e2ac0-139">Machine Learning Web 服務入口網站 [部署實驗] 頁面</span><span class="sxs-lookup"><span data-stu-id="e2ac0-139">Machine Learning Web Service portal Deploy Experiment Page</span></span>
<span data-ttu-id="e2ac0-140">在 [部署實驗] 頁面上，輸入 Web 服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-140">On the Deploy Experiment page, enter a name for the web service.</span></span>
<span data-ttu-id="e2ac0-141">選取定價方案。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-141">Select a pricing plan.</span></span> <span data-ttu-id="e2ac0-142">如果您有現有的定價方案，可以進行選取，否則您必須為服務建立新的定價方案。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-142">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for the service.</span></span>

1. <span data-ttu-id="e2ac0-143">在 [價格方案] 下拉式清單中，選取現有的方案或選取 [選取新的方案] 選項。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-143">In the **Price Plan** drop down, select an existing plan or select the **Select new plan** option.</span></span>
2. <span data-ttu-id="e2ac0-144">在 [方案名稱] 中，輸入將識別您帳單上方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-144">In **Plan Name**, type a name that will identify the plan on your bill.</span></span>
3. <span data-ttu-id="e2ac0-145">選取其中一個 [每月方案層] 。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-145">Select one of the **Monthly Plan Tiers**.</span></span> <span data-ttu-id="e2ac0-146">方案層預設為您預設區域的方案，而您的 Web 服務會部署到該區域。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-146">The plan tiers default to the plans for your default region and your web service is deployed to that region.</span></span>

<span data-ttu-id="e2ac0-147">按一下 [部署]，Web 服務的 [快速入門] 頁面就會開啟。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-147">Click **Deploy** and the **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="e2ac0-148">Web 服務的 [快速入門] 頁面可讓您存取建立 Web 服務之後最常執行的工作，並提供指引。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-148">The web service Quickstart page gives you access and guidance on the most common tasks you will perform after creating a web service.</span></span> <span data-ttu-id="e2ac0-149">從這裡您可以輕鬆地存取 [測試] 頁面和 [取用] 頁面。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-149">From here, you can easily access both the Test page and Consume page.</span></span>

<!-- ![Deploy the web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)-->

#### <a name="test-your-new-web-service"></a><span data-ttu-id="e2ac0-150">測試新式 Web 服務</span><span class="sxs-lookup"><span data-stu-id="e2ac0-150">Test your New web service</span></span>
<span data-ttu-id="e2ac0-151">若要測試新的 Web 服務，請在常見工作下按一下 [測試 Web 服務]  。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-151">To test your new web service, click **Test web service** under common tasks.</span></span> <span data-ttu-id="e2ac0-152">在 [測試] 頁面上，您可以將 Web 服務當成要求-回應服務 (RRS) 或批次執行服務 (BES) 來測試。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-152">On the Test page, you can test your web service as a Request-Response Service (RRS) or a Batch Execution service (BES).</span></span>

<span data-ttu-id="e2ac0-153">RRS 測試頁面會顯示輸入、輸出以及任何您已為實驗定義的全域參數。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-153">The RRS test page displays the inputs, outputs, and any global parameters that you have defined for the experiment.</span></span> <span data-ttu-id="e2ac0-154">若要測試 Web 服務，您可以手動輸入適當的值作為輸入，或提供包含測試值的逗號分隔值 (CSV) 格式檔案。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-154">To test the web service, you can manually enter appropriate values for the inputs or supply a comma separated value (CSV) formatted file containing the test values.</span></span>

<span data-ttu-id="e2ac0-155">若要使用 RRS 測試，請從清單檢視模式，針對輸入輸入適當的值，並按一下 [測試要求-回應] 。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-155">To test using RRS, from the list view mode, enter appropriate values for the inputs and click **Test Request-Response**.</span></span> <span data-ttu-id="e2ac0-156">您的預測結果會顯示在左邊的輸出資料行。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-156">Your prediction results  display in the output column to the left.</span></span>

![部署 Web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-5-test-request-response.png)

<span data-ttu-id="e2ac0-158">若要測試您的 BES，請按一下 [批次] 。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-158">To test your BES, click **Batch**.</span></span> <span data-ttu-id="e2ac0-159">在 [批次] 測試頁面上，在您的輸入下按一下 [瀏覽] 並選取包含適當範例值的 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-159">On the Batch test page, click Browse under your input and select a CSV file containing appropriate sample values.</span></span> <span data-ttu-id="e2ac0-160">如果您沒有 CSV 檔案，而且是使用 Machine Learning Studio 建立預測實驗，您可以下載預測實驗的資料集來使用。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-160">If you don't have a CSV file, and you created your predictive experiment using Machine Learning Studio, you can download the data set for your predictive experiment and use it.</span></span>

<span data-ttu-id="e2ac0-161">若要下載資料集，請開啟 Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-161">To download the data set, open Machine Learning Studio.</span></span> <span data-ttu-id="e2ac0-162">開啟您的預測實驗，並以滑鼠右鍵按一下實驗的輸入。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-162">Open your predictive experiment and right click the input for your experiment.</span></span> <span data-ttu-id="e2ac0-163">從操作功能表中，選取 [資料集]，然後選取 [下載]。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-163">From the context menu, select **dataset** and then select **Download**.</span></span>

![部署 Web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-7-mls-download.png)

<span data-ttu-id="e2ac0-165">按一下 [ **測試**]。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-165">Click **Test**.</span></span> <span data-ttu-id="e2ac0-166">批次執行作業的狀態會顯示在右邊的 [測試批次作業] 之下。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-166">The status of your Batch Execution job displays to the right under **Test Batch Jobs**.</span></span>

![部署 Web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-6-test-batch-execution.png)

<!--![Test the web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)-->

<span data-ttu-id="e2ac0-168">在 [組態] 頁面上，可以變更 Web 服務的描述、標題、更新儲存體帳戶金鑰，以及啟用範例資料。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-168">On the **CONFIGURATION** page, you can change the description, title, update the storage account key, and enable sample data for your web service.</span></span>

![設定 Web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-8-arm-configure.png)

<span data-ttu-id="e2ac0-170">一旦您部署了 Web 服務，您可以：</span><span class="sxs-lookup"><span data-stu-id="e2ac0-170">Once you've deployed the web service, you can:</span></span>

* <span data-ttu-id="e2ac0-171">**存取** 它。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-171">**Access** it through the web service API.</span></span>
* <span data-ttu-id="e2ac0-172">**管理** 它。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-172">**Manage** it through Azure Machine Learning web services portal or the Azure classic portal.</span></span>
* <span data-ttu-id="e2ac0-173">**更新** 它。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-173">**Update** it if your model changes.</span></span>

#### <a name="access-your-new-web-service"></a><span data-ttu-id="e2ac0-174">存取新式 Web 服務</span><span class="sxs-lookup"><span data-stu-id="e2ac0-174">Access your New web service</span></span>
<span data-ttu-id="e2ac0-175">從 Machine Learning Studio 部署您的 Web 服務之後，您可以傳送資料給服務以及以程式設計方式接收回應。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-175">Once you deploy your web service from Machine Learning Studio, you can send data to the service and receive responses programmatically.</span></span>

<span data-ttu-id="e2ac0-176">[取用]  頁面提供您存取 Web 服務所需的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-176">The **Consume** page provides all the information you need to access your web service.</span></span> <span data-ttu-id="e2ac0-177">例如，API 金鑰可用來允許經過授權的存取服務。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-177">For example, the API key is provided to allow authorized access to the service.</span></span>

<span data-ttu-id="e2ac0-178">有關存取 Machine Learning Web 服務的詳細資訊，請參閱[如何使用 Azure Machine Learning Web 服務](machine-learning-consume-web-services.md)。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-178">For more information about accessing a Machine Learning web service, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

#### <a name="manage-your-new-web-service"></a><span data-ttu-id="e2ac0-179">管理新式 Web 服務</span><span class="sxs-lookup"><span data-stu-id="e2ac0-179">Manage your New web service</span></span>
<span data-ttu-id="e2ac0-180">您可以在 Machine Learning Web 服務入口網站中管理新的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-180">You can manage your New web services Machine Learning Web Services portal.</span></span> <span data-ttu-id="e2ac0-181">從[入口網站主頁面](https://services.azureml-test.net/)按一下 [Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-181">From the [main portal page](https://services.azureml-test.net/), click **Web Services**.</span></span> <span data-ttu-id="e2ac0-182">從 Web 服務頁面可以刪除或複製服務。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-182">From the web services page, you can delete or copy a service.</span></span> <span data-ttu-id="e2ac0-183">若要監視特定的服務，請按一下服務，然後按一下 [儀表板] 。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-183">To monitor a specific service, click the service and then click **Dashboard**.</span></span> <span data-ttu-id="e2ac0-184">若要監視與 Web 服務相關聯的批次作業，請按一下 [批次要求記錄檔] 。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-184">To monitor batch jobs associated with the web service, click **Batch Request Log**.</span></span>

### <a name="deploy-the-predictive-experiment-as-a-classic-web-service"></a><span data-ttu-id="e2ac0-185">將預測實驗部署為傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="e2ac0-185">Deploy the predictive experiment as a Classic web service</span></span>

<span data-ttu-id="e2ac0-186">既然已經充分備妥預測實驗，您現在便可將它部署為「傳統」Azure Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-186">Now that the predictive experiment has been sufficiently prepared, you can deploy it as a Classic Azure web service.</span></span> <span data-ttu-id="e2ac0-187">使用者可以使用 Web 服務，將料傳送到您的模型，模型就會傳回其預測。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-187">Using the web service, users can send data to your model and the model will return its predictions.</span></span>

<span data-ttu-id="e2ac0-188">若要部署您的預測實驗，請按一下實驗畫布底端的 [執行]，然後按一下 [部署 Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-188">To deploy your predictive experiment, click **Run** at the bottom of the experiment canvas and then click **Deploy Web Service**.</span></span> <span data-ttu-id="e2ac0-189">系統會設定 Web 服務，且會將您帶往 Web 服務儀表板。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-189">The web service is set up and you are placed in the web service dashboard.</span></span>

![部署 Web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)

#### <a name="test-your-classic-web-service"></a><span data-ttu-id="e2ac0-191">測試傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="e2ac0-191">Test your Classic web service</span></span>

<span data-ttu-id="e2ac0-192">您可以在 Machine Learning Web 服務入口網站或 Machine Learning Studio 中測試 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-192">You can test the web service in either the Machine Learning Web Services portal or Machine Learning Studio.</span></span>

<span data-ttu-id="e2ac0-193">若要測試「要求-回應」Web 服務，請按一下 Web 服務儀表板中的 [測試] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-193">To test the Request Response web service, click the **Test** button in the web service dashboard.</span></span> <span data-ttu-id="e2ac0-194">對話方塊隨即顯示，要求您提供服務的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-194">A dialog pops up to ask you for the input data for the service.</span></span> <span data-ttu-id="e2ac0-195">這些是評分實驗預期的資料行。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-195">These are the columns expected by the scoring experiment.</span></span> <span data-ttu-id="e2ac0-196">輸入一組資料，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-196">Enter a set of data and then click **OK**.</span></span> <span data-ttu-id="e2ac0-197">Web 服務產生的結果會顯示在儀表板底部。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-197">The results generated by the web service are displayed at the bottom of the dashboard.</span></span>

<span data-ttu-id="e2ac0-198">您可以按一下 [測試] 預覽連結，在 Azure Machine Learning Web 服務入口網站中測試您的服務，如先前的「新式 Web 服務」一節所示。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-198">You can click the **Test** preview link to test your service in the Azure Machine Learning Web Services portal as shown previously in the New web service section.</span></span>

<span data-ttu-id="e2ac0-199">若要測試批次執行服務，請按一下 [測試] 預覽連結。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-199">To test the Batch Execution Service, click **Test** preview link .</span></span> <span data-ttu-id="e2ac0-200">在 [批次] 測試頁面上，在您的輸入下按一下 [瀏覽] 並選取包含適當範例值的 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-200">On the Batch test page, click Browse under your input and select a CSV file containing appropriate sample values.</span></span> <span data-ttu-id="e2ac0-201">如果您沒有 CSV 檔案，而且是使用 Machine Learning Studio 建立預測實驗，您可以下載預測實驗的資料集來使用。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-201">If you don't have a CSV file, and you created your predictive experiment using Machine Learning Studio, you can download the data set for your predictive experiment and use it.</span></span>

![測試 Web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)

<span data-ttu-id="e2ac0-203">在 [組態] 索引標籤上，您可以變更服務的顯示名稱，並且給予描述。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-203">On the **CONFIGURATION** page, you can change the display name of the service and give it a description.</span></span> <span data-ttu-id="e2ac0-204">名稱和描述會顯示在管理 Web 服務的 [Azure 傳統入口網站](http://manage.windowsazure.com/) 中。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-204">The name and description is displayed in the [Azure classic portal](http://manage.windowsazure.com/) where you manage your web services.</span></span>

<span data-ttu-id="e2ac0-205">您可以為輸入資料、輸出資料及 Web 服務參數提供描述，方法是在 [輸入結構描述]、[輸出結構描述] 及 [Web 服務參數] 底下的每個資料行輸入字串。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-205">You can provide a description for your input data, output data, and web service parameters by entering a string for each column under **INPUT SCHEMA**, **OUTPUT SCHEMA**, and **Web SERVICE PARAMETER**.</span></span> <span data-ttu-id="e2ac0-206">這些說明會用於為 Web 服務提供的範例程式碼文件。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-206">These descriptions are used in the sample code documentation provided for the web service.</span></span>

<span data-ttu-id="e2ac0-207">您可以啟用記錄來診斷您在 Web 服務被存取時看到的任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-207">You can enable logging to diagnose any failures that you're seeing when your web service is accessed.</span></span> <span data-ttu-id="e2ac0-208">如需詳細資訊，請參閱 [為 Machine Learning Web 服務啟用記錄](machine-learning-web-services-logging.md)。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-208">For more information, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

![設定 Web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-4.png)

<span data-ttu-id="e2ac0-210">您也可以在 Azure Machine Learning Web 服務入口網站中設定 Web 服務的端點，作法類似先前在「新式 Web 服務」一節所示的程序。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-210">You can also configure the endpoints for the web service in the Azure Machine Learning Web Services portal similar to the procedure shown previously in the New web service section.</span></span> <span data-ttu-id="e2ac0-211">選項有所不同，您可以新增或變更服務描述、啟用記錄，以及啟用範例資料進行測試。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-211">The options are different, you can add or change the service description, enable logging, and enable sample data for testing.</span></span>

#### <a name="access-your-classic-web-service"></a><span data-ttu-id="e2ac0-212">存取傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="e2ac0-212">Access your Classic web service</span></span>
<span data-ttu-id="e2ac0-213">從 Machine Learning Studio 部署您的 Web 服務之後，您可以傳送資料給服務以及以程式設計方式接收回應。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-213">Once you deploy your web service from Machine Learning Studio, you can send data to the service and receive responses programmatically.</span></span>

<span data-ttu-id="e2ac0-214">儀表板提供您存取 Web 服務所需的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-214">The dashboard provides all the information you need to access your web service.</span></span> <span data-ttu-id="e2ac0-215">例如，提供 API 金鑰以允許服務的授權存取權，以及提供 API 說明頁面以協助您開始撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-215">For example, the API key is provided to allow authorized access to the service, and API help pages are provided to help you get started writing your code.</span></span>

<span data-ttu-id="e2ac0-216">有關存取 Machine Learning Web 服務的詳細資訊，請參閱[如何使用 Azure Machine Learning Web 服務](machine-learning-consume-web-services.md)。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-216">For more information about accessing a Machine Learning web service, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

#### <a name="manage-your-classic-web-service"></a><span data-ttu-id="e2ac0-217">管理傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="e2ac0-217">Manage your Classic web service</span></span>
<span data-ttu-id="e2ac0-218">您可以執行各種動作來監視 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-218">There are various of actions you can perform to monitor a web service.</span></span> <span data-ttu-id="e2ac0-219">您可以更新它和刪除它。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-219">You can update it, and delete it.</span></span> <span data-ttu-id="e2ac0-220">除了部署傳統 Web 服務時所建立的預設端點之外，您也可以新增其他端點至傳統 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-220">You can also add additional endpoints to a Classic web service in addition to the default endpoint that is created when you deploy it.</span></span>

<span data-ttu-id="e2ac0-221">如需相關資訊，請參閱[管理 Azure Machine Learning 工作區](machine-learning-manage-workspace.md)和[使用 Azure Machine Learning Web 服務入口網站管理 Web 服務](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-221">For more information, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md) and [Manage a web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>

<!-- When this article gets published, fix the link and uncomment
For more information on how to manage Azure Machine Learning web service endpoints using the REST API, see **Azure machine learning web service endpoints**.
-->

## <a name="update-the-web-service"></a><span data-ttu-id="e2ac0-222">更新 Web 服務</span><span class="sxs-lookup"><span data-stu-id="e2ac0-222">Update the web service</span></span>
<span data-ttu-id="e2ac0-223">您可以對您的 Web 服務進行變更，例如使用其他訓練資料更新模型，以及再次部署、覆寫原始 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-223">You can make changes to your web service, such as updating the model with additional training data, and deploy it again, overwriting the original web service.</span></span>

<span data-ttu-id="e2ac0-224">若要更新 Web 服務，請開啟您用來部署 Web 服務的原始預測實驗，然後按一下 [另存新檔] 以製作可編輯的複本。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-224">To update the web service, open the original predictive experiment you used to deploy the web service and make an editable copy by clicking **SAVE AS**.</span></span> <span data-ttu-id="e2ac0-225">進行變更，然後按一下 [部署 Web 服務] 。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-225">Make your changes and then click **Deploy Web Service**.</span></span>

<span data-ttu-id="e2ac0-226">由於您之前部署了這項實驗，所以會詢問您要覆寫 (傳統 Web 服務) 或更新 (新的 Web 服務) 現有的服務。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-226">Because you've deployed this experiment before, you are asked if you want to overwrite (Classic Web Service) or update (New web service) the existing service.</span></span> <span data-ttu-id="e2ac0-227">按一下 [是] 或 [更新] 會停止現有的 Web 服務，然後在其位置部署新的預測實驗。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-227">Clicking **YES** or **Update** stops the existing web service and deploys the new predictive experiment is deployed in its place.</span></span>

> [!NOTE]
> <span data-ttu-id="e2ac0-228">如果您在原始 Web 服務中進行組態變更，例如輸入新的顯示名稱或說明，則您必須再次輸入這些值。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-228">If you made configuration changes in the original web service, for example, entering a new display name or description, you will need to enter those values again.</span></span>
> 
> 

<span data-ttu-id="e2ac0-229">更新 Web 服務的一個選擇是以程式設計方式重新定型模型。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-229">One option for updating your web service is to retrain the model programmatically.</span></span> <span data-ttu-id="e2ac0-230">如需詳細資訊，請參閱 [以程式設計方式重塑機器學習模型](machine-learning-retrain-models-programmatically.md)。</span><span class="sxs-lookup"><span data-stu-id="e2ac0-230">For more information, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

<!-- internal links -->
<span data-ttu-id="e2ac0-231">[建立訓練實驗]: #create-a-training-experiment</span><span class="sxs-lookup"><span data-stu-id="e2ac0-231">[Create a training experiment]: #create-a-training-experiment</span></span>
<span data-ttu-id="e2ac0-232">[將其轉換為預測實驗]: #convert-the-training-experiment-to-a-predictive-experiment</span><span class="sxs-lookup"><span data-stu-id="e2ac0-232">[Convert it to a predictive experiment]: #convert-the-training-experiment-to-a-predictive-experiment</span></span>
<span data-ttu-id="e2ac0-233">[將其部署為 Web 服務]: #deploy-it-as-a-web-service</span><span class="sxs-lookup"><span data-stu-id="e2ac0-233">[Deploy it as a web service]: #deploy-it-as-a-web-service</span></span>
<span data-ttu-id="e2ac0-234">[新式]: #deploy-the-predictive-experiment-as-a-new-Web-service</span><span class="sxs-lookup"><span data-stu-id="e2ac0-234">[new]: #deploy-the-predictive-experiment-as-a-new-Web-service</span></span>
<span data-ttu-id="e2ac0-235">[傳統]: #deploy-the-predictive-experiment-as-a-new-Web-service</span><span class="sxs-lookup"><span data-stu-id="e2ac0-235">[classic]: #deploy-the-predictive-experiment-as-a-new-Web-service</span></span>
[Access]: #access-the-Web-service
[Manage]: #manage-the-Web-service-in-the-azure-management-portal
[Update]: #update-the-Web-service
