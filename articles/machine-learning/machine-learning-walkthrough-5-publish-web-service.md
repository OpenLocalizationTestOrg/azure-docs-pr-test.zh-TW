---
title: "步驟 5：部署 Machine Learning Web 服務 | Microsoft Docs"
description: "開發預測解決方案逐步解說的步驟 5：在 Machine Learning Studio 中將預測實驗部署為 Web 服務。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 3fca74a3-c44b-4583-a218-c14c46ee5338
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: cec1bcceea158a20742c7019a266dcefaac4c9cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-5-deploy-the-azure-machine-learning-web-service"></a><span data-ttu-id="c6552-103">逐步解說步驟 5：部署 Azure Machine Learning Web 服務</span><span class="sxs-lookup"><span data-stu-id="c6552-103">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>
<span data-ttu-id="c6552-104">這是 [在 Azure Machine Learning 中為信用風險評估開發預測性分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="c6552-104">This is the fifth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="c6552-105">建立機器學習服務工作區</span><span class="sxs-lookup"><span data-stu-id="c6552-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="c6552-106">上傳現有資料</span><span class="sxs-lookup"><span data-stu-id="c6552-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="c6552-107">建立新實驗</span><span class="sxs-lookup"><span data-stu-id="c6552-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="c6552-108">訓練及評估模型</span><span class="sxs-lookup"><span data-stu-id="c6552-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. <span data-ttu-id="c6552-109">**部署 Web 服務**</span><span class="sxs-lookup"><span data-stu-id="c6552-109">**Deploy the web service**</span></span>
6. [<span data-ttu-id="c6552-110">存取 Web 服務</span><span class="sxs-lookup"><span data-stu-id="c6552-110">Access the web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="c6552-111">為了讓其他人有機會使用此逐步解說中開發的預測模型，我們可以將它部署為 Azure 上的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="c6552-111">To give others a chance to use the predictive model we've developed in this walkthrough, we can deploy it as a web service on Azure.</span></span>

<span data-ttu-id="c6552-112">截至目前為止，我們一直在試驗如何定型模型。</span><span class="sxs-lookup"><span data-stu-id="c6552-112">Up to this point we've been experimenting with training our model.</span></span> <span data-ttu-id="c6552-113">但是已部署的服務就不會再進行訓練，它會根據我們的模型，對使用者的輸入計分以產生預測。</span><span class="sxs-lookup"><span data-stu-id="c6552-113">But the deployed service is no longer going to do training - it's going to generate new predictions by scoring the user's input based on our model.</span></span> <span data-ttu-id="c6552-114">所以我們要進行一些準備工作，將這項實驗從***訓練***實驗轉換為***預測***實驗。</span><span class="sxs-lookup"><span data-stu-id="c6552-114">So we're going to do some preparation to convert this experiment from a ***training*** experiment to a ***predictive*** experiment.</span></span> 

<span data-ttu-id="c6552-115">這是一個三步驟程序：</span><span class="sxs-lookup"><span data-stu-id="c6552-115">This is a three-step process:</span></span>  

1. <span data-ttu-id="c6552-116">移除其中一個模型</span><span class="sxs-lookup"><span data-stu-id="c6552-116">Remove one of the models</span></span>
2. <span data-ttu-id="c6552-117">將我們所建立的*訓練實驗*轉換成*預測實驗*</span><span class="sxs-lookup"><span data-stu-id="c6552-117">Convert the *training experiment* we've created into a *predictive experiment*</span></span>
3. <span data-ttu-id="c6552-118">將預測實驗部署為 Web 服務</span><span class="sxs-lookup"><span data-stu-id="c6552-118">Deploy the predictive experiment as a web service</span></span>

## <a name="remove-one-of-the-models"></a><span data-ttu-id="c6552-119">移除其中一個模型</span><span class="sxs-lookup"><span data-stu-id="c6552-119">Remove one of the models</span></span>

<span data-ttu-id="c6552-120">首先，我們需要更精簡這項實驗。</span><span class="sxs-lookup"><span data-stu-id="c6552-120">First, we need to trim this experiment down a little.</span></span> <span data-ttu-id="c6552-121">我們目前在實驗中有兩個不同的模型，但將此實驗部署為 Web 服務時，我們只要一個模型。</span><span class="sxs-lookup"><span data-stu-id="c6552-121">We currently have two different models in the experiment, but we only want to use one model when we deploy this as a web service.</span></span>  

<span data-ttu-id="c6552-122">假設我們已判斷出促進式樹狀模型比 SVM 模型更適合。</span><span class="sxs-lookup"><span data-stu-id="c6552-122">Let's say we've decided that the boosted tree model performed better than the SVM model.</span></span> <span data-ttu-id="c6552-123">因此，首要之務是移除[二元支援向量機器][two-class-support-vector-machine]模組，以及用於訓練該模組的其他模組。</span><span class="sxs-lookup"><span data-stu-id="c6552-123">So the first thing to do is remove the [Two-Class Support Vector Machine][two-class-support-vector-machine] module and the modules that were used for training it.</span></span> <span data-ttu-id="c6552-124">您可能需要按一下實驗畫布底部的 [ **另存新檔** ]，先建立一份實驗複本。</span><span class="sxs-lookup"><span data-stu-id="c6552-124">You may want to make a copy of the experiment first by clicking **Save As** at the bottom of the experiment canvas.</span></span>

<span data-ttu-id="c6552-125">我們必須刪除下列模組：</span><span class="sxs-lookup"><span data-stu-id="c6552-125">We need to delete the following modules:</span></span>  

* <span data-ttu-id="c6552-126">[二元支援向量機器][two-class-support-vector-machine]</span><span class="sxs-lookup"><span data-stu-id="c6552-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span></span>
* <span data-ttu-id="c6552-127">[訓練模型][train-model]和與之連接的[評分模型][score-model]模組</span><span class="sxs-lookup"><span data-stu-id="c6552-127">[Train Model][train-model] and [Score Model][score-model] modules that were connected to it</span></span>
* <span data-ttu-id="c6552-128">[標準化資料][normalize-data] (兩者)</span><span class="sxs-lookup"><span data-stu-id="c6552-128">[Normalize Data][normalize-data] (both of them)</span></span>
* <span data-ttu-id="c6552-129">[評估模型][evaluate-model] (因為我們已完成模型的評估)</span><span class="sxs-lookup"><span data-stu-id="c6552-129">[Evaluate Model][evaluate-model] (because we're finished evaluating the models)</span></span>

<span data-ttu-id="c6552-130">選取每個模組然後按 Delete 鍵，或用右鍵按一下模組並選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="c6552-130">Select each module and press the Delete key, or right-click the module and select **Delete**.</span></span> 

![已移除 SVM 模型][3a]

<span data-ttu-id="c6552-132">我們的模型現在看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="c6552-132">Our model should now look something like this:</span></span>

![已移除 SVM 模型][3]

<span data-ttu-id="c6552-134">現在我們已經準備好使用[二元促進式決策樹][two-class-boosted-decision-tree]來部署此模型。</span><span class="sxs-lookup"><span data-stu-id="c6552-134">Now we're ready to deploy this model using the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span></span>

## <a name="convert-the-training-experiment-to-a-predictive-experiment"></a><span data-ttu-id="c6552-135">將訓練實驗轉換為預測實驗</span><span class="sxs-lookup"><span data-stu-id="c6552-135">Convert the training experiment to a predictive experiment</span></span>

<span data-ttu-id="c6552-136">若要備妥此模型以進行部署，我們需要將此訓練實驗轉換為預測實驗。</span><span class="sxs-lookup"><span data-stu-id="c6552-136">To get this model ready for deployment, we need to convert this training experiment to a predictive experiment.</span></span> <span data-ttu-id="c6552-137">這牽涉到三個步驟：</span><span class="sxs-lookup"><span data-stu-id="c6552-137">This involves three steps:</span></span>

1. <span data-ttu-id="c6552-138">儲存已定型的模型，並取代我們的定型模組</span><span class="sxs-lookup"><span data-stu-id="c6552-138">Save the model we've trained and then replace our training modules</span></span>
2. <span data-ttu-id="c6552-139">精簡實驗，移除只有定型才需要的模組</span><span class="sxs-lookup"><span data-stu-id="c6552-139">Trim the experiment to remove modules that were only needed for training</span></span>
3. <span data-ttu-id="c6552-140">定義 Web 服務將接受輸入的位置和產生輸出的位置</span><span class="sxs-lookup"><span data-stu-id="c6552-140">Define where the web service will accept input and where it generates the output</span></span>

<span data-ttu-id="c6552-141">我們可以手動進行此動作，但幸好上述三個步驟只要按一下實驗畫布底端的 [設定 Web 服務] (然後選取 [預測性 Web 服務] 選項) 即可完成。</span><span class="sxs-lookup"><span data-stu-id="c6552-141">We could do this manually, but fortunately all three steps can be accomplished by clicking **Set Up Web Service** at the bottom of the experiment canvas (and selecting the **Predictive Web Service** option).</span></span>

> [!TIP]
> <span data-ttu-id="c6552-142">如需將訓練實驗轉換成預測實驗的詳細資訊，請參閱[如何準備您的模型以在 Azure Machine Learning Studio 中部署](machine-learning-convert-training-experiment-to-scoring-experiment.md)。</span><span class="sxs-lookup"><span data-stu-id="c6552-142">If you want more details on what happens when you convert a training experiment to a predictive experiment, see [How to prepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="c6552-143">當您按一下 [設定 Web 服務] ，會發生幾件事：</span><span class="sxs-lookup"><span data-stu-id="c6552-143">When you click **Set Up Web Service**, several things happen:</span></span>

* <span data-ttu-id="c6552-144">定型的模型會轉換為單一**定型模型**模組，並存放在實驗畫布左側的模組選擇區中 (您可以在 [定型模型] 下找到這個模組)</span><span class="sxs-lookup"><span data-stu-id="c6552-144">The trained model is converted to a single **Trained Model** module and stored in the module palette to the left of the experiment canvas (you can find it under **Trained Models**)</span></span>
* <span data-ttu-id="c6552-145">用於定型的模組已遭到移除，尤其是：</span><span class="sxs-lookup"><span data-stu-id="c6552-145">Modules that were used for training are removed; specifically:</span></span>
  * <span data-ttu-id="c6552-146">[二元促進式決策樹][two-class-boosted-decision-tree]</span><span class="sxs-lookup"><span data-stu-id="c6552-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span></span>
  * <span data-ttu-id="c6552-147">[定型模型][train-model]</span><span class="sxs-lookup"><span data-stu-id="c6552-147">[Train Model][train-model]</span></span>
  * <span data-ttu-id="c6552-148">[資料分割][split]</span><span class="sxs-lookup"><span data-stu-id="c6552-148">[Split Data][split]</span></span>
  * <span data-ttu-id="c6552-149">用於測試資料的第二個[執行 R 指令碼][execute-r-script]模組</span><span class="sxs-lookup"><span data-stu-id="c6552-149">the second [Execute R Script][execute-r-script] module that was used for test data</span></span>
* <span data-ttu-id="c6552-150">儲存的定型模型會加回實驗中</span><span class="sxs-lookup"><span data-stu-id="c6552-150">The saved trained model is added back into the experiment</span></span>
* <span data-ttu-id="c6552-151">會新增 **Web 服務輸入**和 **Web 服務輸出**模組 (這些可用來辨識使用者的資料將在何處輸入模型中、傳回什麼資料、在何時存取 Web 服務)</span><span class="sxs-lookup"><span data-stu-id="c6552-151">**Web service input** and **Web service output** modules are added (these identify where the user's data will enter the model, and what data is returned, when the web service is accessed)</span></span>

> [!NOTE]
> <span data-ttu-id="c6552-152">您可以看到，實驗已儲存在已新增至實驗畫布頂端之索引標籤下的兩個部分。</span><span class="sxs-lookup"><span data-stu-id="c6552-152">You can see that the experiment is saved in two parts under tabs that have been added at the top of the experiment canvas.</span></span> <span data-ttu-id="c6552-153">原始的訓練實驗位於 [訓練實驗] 索引標籤底下，新建立的預測實驗位於 [預測實驗] 底下。</span><span class="sxs-lookup"><span data-stu-id="c6552-153">The original training experiment is under the tab **Training experiment**, and the newly created predictive experiment is under **Predictive experiment**.</span></span> <span data-ttu-id="c6552-154">我們將預測實驗部署為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="c6552-154">The predictive experiment is the one we'll deploy as a web service.</span></span>

<span data-ttu-id="c6552-155">我們需要對這項特別的實驗採取一個額外步驟。</span><span class="sxs-lookup"><span data-stu-id="c6552-155">We need to take one additional step with this particular experiment.</span></span>
<span data-ttu-id="c6552-156">我們新增了兩個[執行 R 指令碼][execute-r-script]模組來替資料提供加權函式。</span><span class="sxs-lookup"><span data-stu-id="c6552-156">We added two [Execute R Script][execute-r-script] modules to provide a weighting function to the data.</span></span> <span data-ttu-id="c6552-157">這只是我們為了訓練和測試所用的技巧，因此我們可以從最終模型中拿掉這些模組。</span><span class="sxs-lookup"><span data-stu-id="c6552-157">That was just a trick we needed for training and testing, so we can take out those modules in the final model.</span></span>
<span data-ttu-id="c6552-158">Machine Learning Studio 已在移除[分割][split]模組時移除一個[執行 R 指令碼][execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="c6552-158">Machine Learning Studio removed one [Execute R Script][execute-r-script] module when it removed the [Split][split] module.</span></span> <span data-ttu-id="c6552-159">現在我們可以移除另一個模組，並直接將[中繼資料編輯器][metadata-editor]連接至[評分模型][score-model]。</span><span class="sxs-lookup"><span data-stu-id="c6552-159">Now we can remove the other and connect [Metadata Editor][metadata-editor] directly to [Score Model][score-model].</span></span>    

<span data-ttu-id="c6552-160">實驗現在看起來如下：</span><span class="sxs-lookup"><span data-stu-id="c6552-160">Our experiment should now look like this:</span></span>  

![Scoring the trained model][4]  

> [!NOTE]
> <span data-ttu-id="c6552-162">您可能驚訝我們為什麼要在預測實驗中留下「UCI 德國信用卡資料」資料集。</span><span class="sxs-lookup"><span data-stu-id="c6552-162">You may be wondering why we left the UCI German Credit Card Data dataset in the predictive experiment.</span></span> <span data-ttu-id="c6552-163">服務即將評分使用者的資料，而不是原始資料集，所以為何要讓原始資料集留在模型中？</span><span class="sxs-lookup"><span data-stu-id="c6552-163">The service is going to score the user's data, not the original dataset, so why leave the original dataset in the model?</span></span>
> 
> <span data-ttu-id="c6552-164">服務的確不需要原始信用卡資料。</span><span class="sxs-lookup"><span data-stu-id="c6552-164">It's true that the service doesn't need the original credit card data.</span></span> <span data-ttu-id="c6552-165">但卻需要該資料的結構描述，例如，有多少個資料行及哪些資料行是數值等資訊。</span><span class="sxs-lookup"><span data-stu-id="c6552-165">But it does need the schema for that data, which includes information such as how many columns there are and which columns are numeric.</span></span> <span data-ttu-id="c6552-166">需要此結構描述資訊才能解譯使用者的資料。</span><span class="sxs-lookup"><span data-stu-id="c6552-166">This schema information is necessary to interpret the user's data.</span></span> <span data-ttu-id="c6552-167">我們保持連接這些元件，以便服務執行時，評分模型才會有資料集結構描述。</span><span class="sxs-lookup"><span data-stu-id="c6552-167">We leave these components connected so that the scoring module has the dataset schema when the service is running.</span></span> <span data-ttu-id="c6552-168">不會使用資料，只是使用結構描述。</span><span class="sxs-lookup"><span data-stu-id="c6552-168">The data isn't used, just the schema.</span></span>  
> 
> 

<span data-ttu-id="c6552-169">最後一次執行實驗 (按一下 [執行])。如果要確認模型仍然有效，請按一下 [評分模型][][score-model]模組的輸出結果，並選取 [檢視結果]。</span><span class="sxs-lookup"><span data-stu-id="c6552-169">Run the experiment one last time (click **Run**.) If you want to verify that the model is still working, click the output of the [Score Model][score-model] module and select **View Results**.</span></span> <span data-ttu-id="c6552-170">您可以看到原始資料出現，也會看到信用風險值 ("Scored Labels") 和評分機率值 ("Scored Probabilities")。</span><span class="sxs-lookup"><span data-stu-id="c6552-170">You can see that the original data is displayed, along with the credit risk value ("Scored Labels") and the scoring probability value ("Scored Probabilities".)</span></span> 

## <a name="deploy-the-web-service"></a><span data-ttu-id="c6552-171">部署 Web 服務</span><span class="sxs-lookup"><span data-stu-id="c6552-171">Deploy the web service</span></span>
<span data-ttu-id="c6552-172">您可以將實驗部署為傳統 Web 服務或架構在 Azure Resource Manager 上的新式 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="c6552-172">You can deploy the experiment as either a Classic web service, or as a New web service that's based on Azure Resource Manager.</span></span>

### <a name="deploy-as-a-classic-web-service"></a><span data-ttu-id="c6552-173">部署為傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="c6552-173">Deploy as a Classic web service</span></span>
<span data-ttu-id="c6552-174">若要部署衍生自實驗的傳統 Web 服務，請按一下畫布下方的 [部署 Web 服務]，然後選取 [部署 Web 服務 [傳統]]。</span><span class="sxs-lookup"><span data-stu-id="c6552-174">To deploy a Classic web service derived from our experiment, click **Deploy Web Service** below the canvas and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="c6552-175">Machine Learning Studio 會將實驗當做 Web 服務部署，並帶您前往 Web 服務的儀表板。</span><span class="sxs-lookup"><span data-stu-id="c6552-175">Machine Learning Studio deploys the experiment as a web service and takes you to the dashboard for that web service.</span></span> <span data-ttu-id="c6552-176">您可以從此頁面返回實驗 ([檢視快照] 或 [檢視最新])，並執行簡單的 Web 服務測試 (請參閱下面的**測試 Web 服務**)。</span><span class="sxs-lookup"><span data-stu-id="c6552-176">From this page you can return to the experiment (**View snapshot** or **View latest**) and run a simple test of the web service (see **Test the web service** below).</span></span> <span data-ttu-id="c6552-177">另外這裡還有建立可存取 Web 服務之應用程式的資訊 (此逐步說明的下一個步驟中有該資訊的詳細資料)。</span><span class="sxs-lookup"><span data-stu-id="c6552-177">There is also information here for creating applications that can access the web service (more on that in the next step of this walkthrough).</span></span>

![Web 服務儀表板][6]

<span data-ttu-id="c6552-179">您可以按一下 [設定]  索引標籤來設定服務。</span><span class="sxs-lookup"><span data-stu-id="c6552-179">You can configure the service by clicking the **CONFIGURATION** tab.</span></span> <span data-ttu-id="c6552-180">您可以在這裡修改服務名稱 (預設會指定實驗名稱) 並輸入描述。</span><span class="sxs-lookup"><span data-stu-id="c6552-180">Here you can modify the service name (it's given the experiment name by default) and give it a description.</span></span> <span data-ttu-id="c6552-181">您也可以為輸入和輸出資料指定更好記的標籤。</span><span class="sxs-lookup"><span data-stu-id="c6552-181">You can also give more friendly labels for the input and output data.</span></span>  

![設定 Web 服務][5]  

### <a name="deploy-as-a-new-web-service"></a><span data-ttu-id="c6552-183">部署為新式 Web 服務</span><span class="sxs-lookup"><span data-stu-id="c6552-183">Deploy as a New web service</span></span>

> [!NOTE] 
> <span data-ttu-id="c6552-184">若要部署新式 Web 服務，您必須在要部署 Web 服務的訂用帳戶中具備足夠的權限。</span><span class="sxs-lookup"><span data-stu-id="c6552-184">To deploy a New web service you must have sufficient permissions in the subscription to which you are deploying the web service.</span></span> <span data-ttu-id="c6552-185">如需詳細資訊，請參閱[使用 Azure Machine Learning Web 服務入口網站管理 Web 服務](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="c6552-185">For more information, see [Manage a web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="c6552-186">部署衍生自實驗的新式 Web 服務：</span><span class="sxs-lookup"><span data-stu-id="c6552-186">To deploy a New web service derived from our experiment:</span></span>

1. <span data-ttu-id="c6552-187">按一下畫布底下的 [部署 Web 服務]，然後選取 [部署 Web 服務 [新式]]。</span><span class="sxs-lookup"><span data-stu-id="c6552-187">Click **Deploy Web Service** below the canvas and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="c6552-188">Machine Learning Studio 會帶您到 Azure Machine Learning Web 服務的 [部署實驗] 頁面。</span><span class="sxs-lookup"><span data-stu-id="c6552-188">Machine Learning Studio transfers you to the Azure Machine Learning web services **Deploy Experiment** page.</span></span>

2. <span data-ttu-id="c6552-189">輸入 Web 服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="c6552-189">Enter a name for the web service.</span></span> 

3. <span data-ttu-id="c6552-190">在 [價格方案]，您可以選取現有的定價方案，或選取 [建立新的] 並指定新的方案的名稱，然後選取每月方案選項。</span><span class="sxs-lookup"><span data-stu-id="c6552-190">For **Price Plan**, you can select an existing pricing plan, or select "Create new" and give the new plan a name and select the monthly plan option.</span></span> <span data-ttu-id="c6552-191">方案層預設為您預設區域的方案，而您的 Web 服務會部署到該區域。</span><span class="sxs-lookup"><span data-stu-id="c6552-191">The plan tiers default to the plans for your default region and your web service is deployed to that region.</span></span>

4. <span data-ttu-id="c6552-192">按一下 [ **部署**]。</span><span class="sxs-lookup"><span data-stu-id="c6552-192">Click **Deploy**.</span></span>

<span data-ttu-id="c6552-193">幾分鐘後，Web 服務的 [快速入門] 頁面就會開啟。</span><span class="sxs-lookup"><span data-stu-id="c6552-193">After a few minutes, the **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="c6552-194">您可以按一下 [設定] 索引標籤來設定服務。</span><span class="sxs-lookup"><span data-stu-id="c6552-194">You can configure the service by clicking the **Configure** tab.</span></span> <span data-ttu-id="c6552-195">您可以在這裡修改服務標題並輸入描述。</span><span class="sxs-lookup"><span data-stu-id="c6552-195">Here you can modify the service title and give it a description.</span></span> 

<span data-ttu-id="c6552-196">若要測試 Web 服務，按一下 [測試] 索引標籤 (請參閱下面的**測試 Web 服務**)。</span><span class="sxs-lookup"><span data-stu-id="c6552-196">To test the web service, click the **Test** tab (see **Test the web service** below).</span></span> <span data-ttu-id="c6552-197">如需建立應用程式以存取 Web 服務的相關資訊，請按一下 [取用] 索引標籤 (本逐步解說的下一個步驟將提供更多詳細資料)。</span><span class="sxs-lookup"><span data-stu-id="c6552-197">For information on creating applications that can access the web service, click the **Consume** tab (the next step in this walkthrough will go into more detail).</span></span>

> [!TIP]
> <span data-ttu-id="c6552-198">您可以在部署 Web 服務之後進行更新。</span><span class="sxs-lookup"><span data-stu-id="c6552-198">You can update the web service after you've deployed it.</span></span> <span data-ttu-id="c6552-199">例如，如果想要變更模型，則可以編輯訓練實驗、調整模型參數，然後按一下 [部署 Web 服務]，選取 [部署 Web 服務 [傳統]] 或 [部署 Web 服務 [新式]]。</span><span class="sxs-lookup"><span data-stu-id="c6552-199">For example, if you want to change your model, then you can edit the training experiment, tweak the model parameters, and click **Deploy Web Service**, selecting **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span> <span data-ttu-id="c6552-200">重新部署實驗時，將會取代 Web 服務 (現在使用的是已更新的模型)。</span><span class="sxs-lookup"><span data-stu-id="c6552-200">When you deploy the experiment again, it replaces the web service, now using your updated model.</span></span>  
> 
> 

## <a name="test-the-web-service"></a><span data-ttu-id="c6552-201">測試 Web 服務</span><span class="sxs-lookup"><span data-stu-id="c6552-201">Test the web service</span></span>

<span data-ttu-id="c6552-202">存取 Web 服務時，使用者的資料會透過 **Web 服務輸入**模組輸入，再透過它傳遞給[評分模型][score-model]模組進行評分。</span><span class="sxs-lookup"><span data-stu-id="c6552-202">When the web service is accessed, the user's data enters through the **Web service input** module where it's passed to the [Score Model][score-model] module and scored.</span></span> <span data-ttu-id="c6552-203">基於我們設定預測實驗的方式，模型預期會得到與原始信用風險資料集相同格式的資料。</span><span class="sxs-lookup"><span data-stu-id="c6552-203">The way we've set up the predictive experiment, the model expects data in the same format as the original credit risk dataset.</span></span>
<span data-ttu-id="c6552-204">接著透過 **Web 服務輸出**模組，將結果從 Web 服務傳回給使用者。</span><span class="sxs-lookup"><span data-stu-id="c6552-204">The results are returned to the user from the web service through the **Web service output** module.</span></span>

> [!TIP]
> <span data-ttu-id="c6552-205">基於我們設定預測實驗的方式，會傳回[評分模型][score-model]模組的整個結果。</span><span class="sxs-lookup"><span data-stu-id="c6552-205">The way we have the predictive experiment configured, the entire results from the [Score Model][score-model] module are returned.</span></span> <span data-ttu-id="c6552-206">這包括所有輸入的資料以及信用風險值和評分機率。</span><span class="sxs-lookup"><span data-stu-id="c6552-206">This includes all the input data plus the credit risk value and the scoring probability.</span></span> <span data-ttu-id="c6552-207">但您可以視需要傳回不同的項目，例如，您可以只傳回信用風險值。</span><span class="sxs-lookup"><span data-stu-id="c6552-207">But you can return something different if you want - for example, you could return just the credit risk value.</span></span> <span data-ttu-id="c6552-208">若要這樣做，請在[評分模型][score-model]和 **Web 服務輸出**之間插入[專案資料行][project-columns]模組，以排除您不想讓 Web 服務傳回的資料行。</span><span class="sxs-lookup"><span data-stu-id="c6552-208">To do this, insert a [Project Columns][project-columns] module between [Score Model][score-model] and the **Web service output** to eliminate columns you don't want the web service to return.</span></span> 
> 
> 

<span data-ttu-id="c6552-209">您可以在 **Machine Learning Studio** 或 **Azure Machine Learning Web 服務**入口網站中測試傳統 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="c6552-209">You can test a Classic web service either in **Machine Learning Studio** or in the **Azure Machine Learning Web Services** portal.</span></span>
<span data-ttu-id="c6552-210">您只能在 **Machine Learning Web 服務**入口網站中測試新式 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="c6552-210">You can test a New web service only in the **Machine Learning Web Services** portal.</span></span>

> [!TIP]
> <span data-ttu-id="c6552-211">在 Azure Machine Learning Web 服務入口網站中測試時，您可以用入口網站建立範例資料以用於測試要求-回應服務。</span><span class="sxs-lookup"><span data-stu-id="c6552-211">When testing in the Azure Machine Learning Web Services portal, you can have the portal create sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="c6552-212">在 [設定] 頁面上，[啟用範例資料嗎?] 選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="c6552-212">On the **Configure** page, select "Yes" for **Sample Data Enabled?**.</span></span> <span data-ttu-id="c6552-213">當您開啟 [測試] 頁面上的 [要求-回應] 索引標籤時，入口網站會填入取自原始信用風險資料集的範例資料。</span><span class="sxs-lookup"><span data-stu-id="c6552-213">When you open the Request-Response tab on the **Test** page, the portal fills in sample data taken from the original credit risk dataset.</span></span>

### <a name="test-a-classic-web-service"></a><span data-ttu-id="c6552-214">測試傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="c6552-214">Test a Classic web service</span></span>

<span data-ttu-id="c6552-215">您可以在 Machine Learning Studio 或 Machine Learning Web 服務入口網站中測試傳統 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="c6552-215">You can test a Classic web service in Machine Learning Studio or in the Machine Learning Web Services portal.</span></span> 

#### <a name="test-in-machine-learning-studio"></a><span data-ttu-id="c6552-216">在 Machine Learning Studio 中測試</span><span class="sxs-lookup"><span data-stu-id="c6552-216">Test in Machine Learning Studio</span></span>

1. <span data-ttu-id="c6552-217">在 Web 服務的 [儀表板] 頁面上，按一下 [預設端點] 下的 [測試] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c6552-217">On the **DASHBOARD** page for the web service, click the **Test** button under **Default Endpoint**.</span></span> <span data-ttu-id="c6552-218">對話方塊隨即顯示，要求您提供服務的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="c6552-218">A dialog pops up and asks you for the input data for the service.</span></span> <span data-ttu-id="c6552-219">這些就是在原始的信用風險資料集中出現的資料行。</span><span class="sxs-lookup"><span data-stu-id="c6552-219">These are the same columns that appeared in the original credit risk dataset.</span></span>  

2. <span data-ttu-id="c6552-220">輸入一組資料，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="c6552-220">Enter a set of data and then click **OK**.</span></span> 

#### <a name="test-in-the-machine-learning-web-services-portal"></a><span data-ttu-id="c6552-221">在 Machine Learning Web 服務入口網站中測試</span><span class="sxs-lookup"><span data-stu-id="c6552-221">Test in the Machine Learning Web Services portal</span></span>

1. <span data-ttu-id="c6552-222">在 Web 服務的 [儀表板] 頁面上，按一下 [預設端點] 下的 [測試預覽] 連結。</span><span class="sxs-lookup"><span data-stu-id="c6552-222">On the **DASHBOARD** page for the web service, click the **Test preview** link under **Default Endpoint**.</span></span> <span data-ttu-id="c6552-223">Azure Machine Learning Web 服務入口網站中的 Web 服務端點測試頁面隨即開啟，並要求您提供服務的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="c6552-223">The test page in the Azure Machine Learning Web Services portal for the web service endpoint opens and asks you for the input data for the service.</span></span> <span data-ttu-id="c6552-224">這些就是在原始的信用風險資料集中出現的資料行。</span><span class="sxs-lookup"><span data-stu-id="c6552-224">These are the same columns that appeared in the original credit risk dataset.</span></span>

2. <span data-ttu-id="c6552-225">按一下 [測試要求-回應]。</span><span class="sxs-lookup"><span data-stu-id="c6552-225">Click **Test Request-Response**.</span></span> 

### <a name="test-a-new-web-service"></a><span data-ttu-id="c6552-226">測試新式 Web 服務</span><span class="sxs-lookup"><span data-stu-id="c6552-226">Test a New web service</span></span>

<span data-ttu-id="c6552-227">您只能在 Machine Learning Web 服務入口網站中測試新式 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="c6552-227">You can test a New web service only in the Machine Learning Web Services portal.</span></span>

1. <span data-ttu-id="c6552-228">在 [Azure Machine Learning Web 服務](https://services.azureml.net/quickstart)入口網站中，按一下頁面頂端的 [測試]。</span><span class="sxs-lookup"><span data-stu-id="c6552-228">In the [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal, click **Test** at the top of the page.</span></span> <span data-ttu-id="c6552-229">[測試] 頁面會開啟，您可以輸入服務的資料。</span><span class="sxs-lookup"><span data-stu-id="c6552-229">The **Test** page opens and you can input data for the service.</span></span> <span data-ttu-id="c6552-230">顯示的輸入欄位會對應到在原始的信用風險資料集中出現的資料行。</span><span class="sxs-lookup"><span data-stu-id="c6552-230">The input fields displayed correspond to the columns that appeared in the original credit risk dataset.</span></span> 

2. <span data-ttu-id="c6552-231">輸入一組資料，然後按一下 [測試要求-回應] 。</span><span class="sxs-lookup"><span data-stu-id="c6552-231">Enter a set of data and then click **Test Request-Response**.</span></span>

<span data-ttu-id="c6552-232">測試的結果會顯示在頁面右邊的輸出資料行上。</span><span class="sxs-lookup"><span data-stu-id="c6552-232">The results of the test are displayed on the right-hand side of the page in the output column.</span></span> 


## <a name="manage-the-web-service"></a><span data-ttu-id="c6552-233">管理 Web 服務</span><span class="sxs-lookup"><span data-stu-id="c6552-233">Manage the web service</span></span>

### <a name="manage-a-classic-web-service-in-the-azure-classic-portal"></a><span data-ttu-id="c6552-234">在 Azure 傳統入口網站中管理傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="c6552-234">Manage a Classic web service in the Azure classic portal</span></span>

<span data-ttu-id="c6552-235">一旦部署傳統 Web 服務之後，您就可以從 [Azure 傳統入口網站](https://manage.windowsazure.com)管理它。</span><span class="sxs-lookup"><span data-stu-id="c6552-235">Once you've deployed your Classic web service, you can manage it from the [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="c6552-236">登入 [Azure 傳統入口網站](https://manage.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="c6552-236">Sign in to the [Azure classic portal](https://manage.windowsazure.com)</span></span>
2. <span data-ttu-id="c6552-237">在 Microsoft Azure 服務面板中，按一下 [Machine Learning]</span><span class="sxs-lookup"><span data-stu-id="c6552-237">In the Microsoft Azure services panel, click **MACHINE LEARNING**</span></span>
3. <span data-ttu-id="c6552-238">按一下您的工作區</span><span class="sxs-lookup"><span data-stu-id="c6552-238">Click your workspace</span></span>
4. <span data-ttu-id="c6552-239">按一下 [Web 服務] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="c6552-239">Click the **Web services** tab</span></span>
5. <span data-ttu-id="c6552-240">按一下我們建立的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="c6552-240">Click the web service we created</span></span>
6. <span data-ttu-id="c6552-241">按一下「預設」端點</span><span class="sxs-lookup"><span data-stu-id="c6552-241">Click the "default" endpoint</span></span>

<span data-ttu-id="c6552-242">從這裡您可以進行一些動作，例如監視 Web 服務的執行狀況，以及變更服務可處理的並行呼叫數來調整效能。</span><span class="sxs-lookup"><span data-stu-id="c6552-242">From here, you can do things like monitor how the web service is doing and make performance tweaks by changing how many concurrent calls the service can handle.</span></span>

<span data-ttu-id="c6552-243">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="c6552-243">For more details, see:</span></span>

* [<span data-ttu-id="c6552-244">建立端點</span><span class="sxs-lookup"><span data-stu-id="c6552-244">Creating Endpoints</span></span>](machine-learning-create-endpoint.md)
* [<span data-ttu-id="c6552-245">調整 Web 服務</span><span class="sxs-lookup"><span data-stu-id="c6552-245">Scaling web service</span></span>](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="c6552-246">在 Azure Machine Learning Web 服務入口網站中管理傳統或新式 Web 服務</span><span class="sxs-lookup"><span data-stu-id="c6552-246">Manage a Classic or New web service in the Azure Machine Learning Web Services portal</span></span>

<span data-ttu-id="c6552-247">一旦部署 Web 服務 (傳統或新式) 之後，您就可以從 [Microsoft Azure Machine Learning Web 服務](https://services.azureml.net/quickstart)入口網站管理它。</span><span class="sxs-lookup"><span data-stu-id="c6552-247">Once you've deployed your web service, whether Classic or New, you can manage it from the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal.</span></span>

<span data-ttu-id="c6552-248">監視 Web 服務的效能：</span><span class="sxs-lookup"><span data-stu-id="c6552-248">To monitor the performance of your web service:</span></span>

1. <span data-ttu-id="c6552-249">登入 [Microsoft Azure Machine Learning Web 服務](https://services.azureml.net/quickstart)入口網站</span><span class="sxs-lookup"><span data-stu-id="c6552-249">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal</span></span>
2. <span data-ttu-id="c6552-250">按一下 [Web 服務]</span><span class="sxs-lookup"><span data-stu-id="c6552-250">Click **Web services**</span></span>
3. <span data-ttu-id="c6552-251">按一下您的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="c6552-251">Click your web service</span></span>
4. <span data-ttu-id="c6552-252">按一下 [儀表板]</span><span class="sxs-lookup"><span data-stu-id="c6552-252">Click the **Dashboard**</span></span>

- - -
<span data-ttu-id="c6552-253">**下一步：[存取 Web 服務](machine-learning-walkthrough-6-access-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="c6552-253">**Next: [Access the web service](machine-learning-walkthrough-6-access-web-service.md)**</span></span>

[3]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3.png
[3a]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3a.png
[4]: ./media/machine-learning-walkthrough-5-publish-web-service/publish4.png
[5]: ./media/machine-learning-walkthrough-5-publish-web-service/publish5.png
[6]: ./media/machine-learning-walkthrough-5-publish-web-service/publish6.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[metadata-editor]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[project-columns]: https://msdn.microsoft.com/en-us/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
