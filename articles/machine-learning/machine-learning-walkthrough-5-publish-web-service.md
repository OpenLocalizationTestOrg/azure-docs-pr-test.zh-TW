---
title: "步驟 5： 部署的 hello 機器學習 web 服務 |Microsoft 文件"
description: "步驟 5 的 hello 開發預測方案逐步解說： 部署為 web 服務 Machine Learning Studio 中的預測實驗。"
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
ms.openlocfilehash: 76391010972ed1450bbda8bfb2352c7b22b51ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-5-deploy-hello-azure-machine-learning-web-service"></a><span data-ttu-id="dd382-103">逐步解說步驟 5： 部署的 hello Azure Machine Learning web 服務</span><span class="sxs-lookup"><span data-stu-id="dd382-103">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>
<span data-ttu-id="dd382-104">這是 hello hello 逐步解說中，第五個步驟[開發 Azure Machine Learning 中的預測分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="dd382-104">This is hello fifth step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="dd382-105">建立機器學習服務工作區</span><span class="sxs-lookup"><span data-stu-id="dd382-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="dd382-106">上傳現有資料</span><span class="sxs-lookup"><span data-stu-id="dd382-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="dd382-107">建立新實驗</span><span class="sxs-lookup"><span data-stu-id="dd382-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="dd382-108">來定型及評估 hello 模型</span><span class="sxs-lookup"><span data-stu-id="dd382-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. <span data-ttu-id="dd382-109">**部署 hello web 服務**</span><span class="sxs-lookup"><span data-stu-id="dd382-109">**Deploy hello web service**</span></span>
6. [<span data-ttu-id="dd382-110">存取 hello web 服務</span><span class="sxs-lookup"><span data-stu-id="dd382-110">Access hello web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="dd382-111">toogive 其他機率 toouse hello 我們已在本逐步解說中開發的預測模型，我們可以將其部署為 Azure 上的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="dd382-111">toogive others a chance toouse hello predictive model we've developed in this walkthrough, we can deploy it as a web service on Azure.</span></span>

<span data-ttu-id="dd382-112">向上 toothis 點我們已經已試驗訓練我們的模型。</span><span class="sxs-lookup"><span data-stu-id="dd382-112">Up toothis point we've been experimenting with training our model.</span></span> <span data-ttu-id="dd382-113">但即將不再部署的 hello 服務 toodo 定型-它會執行 toogenerate 新預測計分根據我們的模型中的 hello 使用者的輸入。</span><span class="sxs-lookup"><span data-stu-id="dd382-113">But hello deployed service is no longer going toodo training - it's going toogenerate new predictions by scoring hello user's input based on our model.</span></span> <span data-ttu-id="dd382-114">讓我們 toodo 某些準備 tooconvert 這實驗從***訓練***實驗 tooa***預測***實驗。</span><span class="sxs-lookup"><span data-stu-id="dd382-114">So we're going toodo some preparation tooconvert this experiment from a ***training*** experiment tooa ***predictive*** experiment.</span></span> 

<span data-ttu-id="dd382-115">這是一個三步驟程序：</span><span class="sxs-lookup"><span data-stu-id="dd382-115">This is a three-step process:</span></span>  

1. <span data-ttu-id="dd382-116">請移除其中一個 hello 模型</span><span class="sxs-lookup"><span data-stu-id="dd382-116">Remove one of hello models</span></span>
2. <span data-ttu-id="dd382-117">轉換 hello*定型實驗*我們建立了成*預測實驗*</span><span class="sxs-lookup"><span data-stu-id="dd382-117">Convert hello *training experiment* we've created into a *predictive experiment*</span></span>
3. <span data-ttu-id="dd382-118">部署為 web 服務的 hello 預測實驗</span><span class="sxs-lookup"><span data-stu-id="dd382-118">Deploy hello predictive experiment as a web service</span></span>

## <a name="remove-one-of-hello-models"></a><span data-ttu-id="dd382-119">請移除其中一個 hello 模型</span><span class="sxs-lookup"><span data-stu-id="dd382-119">Remove one of hello models</span></span>

<span data-ttu-id="dd382-120">首先，我們需要 tootrim 此實驗向一點。</span><span class="sxs-lookup"><span data-stu-id="dd382-120">First, we need tootrim this experiment down a little.</span></span> <span data-ttu-id="dd382-121">我們目前 hello 實驗中有兩個不同的模型，但我們只想 toouse 一個模型，我們將此部署為 web 服務。</span><span class="sxs-lookup"><span data-stu-id="dd382-121">We currently have two different models in hello experiment, but we only want toouse one model when we deploy this as a web service.</span></span>  

<span data-ttu-id="dd382-122">例如，假設我們已經決定該 hello 促進式樹狀模型的執行效能優於 hello SVM 模型。</span><span class="sxs-lookup"><span data-stu-id="dd382-122">Let's say we've decided that hello boosted tree model performed better than hello SVM model.</span></span> <span data-ttu-id="dd382-123">因此第一件事 toodo hello 是移除 hello[二級支援向量機器][ two-class-support-vector-machine]模組和 hello 模組用於培訓。</span><span class="sxs-lookup"><span data-stu-id="dd382-123">So hello first thing toodo is remove hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module and hello modules that were used for training it.</span></span> <span data-ttu-id="dd382-124">您可以 toomake hello 實驗副本第一次按一下**另存新檔**底部 hello hello 實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="dd382-124">You may want toomake a copy of hello experiment first by clicking **Save As** at hello bottom of hello experiment canvas.</span></span>

<span data-ttu-id="dd382-125">我們需要 toodelete hello 下列模組：</span><span class="sxs-lookup"><span data-stu-id="dd382-125">We need toodelete hello following modules:</span></span>  

* <span data-ttu-id="dd382-126">[二元支援向量機器][two-class-support-vector-machine]</span><span class="sxs-lookup"><span data-stu-id="dd382-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span></span>
* <span data-ttu-id="dd382-127">[定型模型][ train-model]和[計分模型][ score-model]所連接的 tooit 模組</span><span class="sxs-lookup"><span data-stu-id="dd382-127">[Train Model][train-model] and [Score Model][score-model] modules that were connected tooit</span></span>
* <span data-ttu-id="dd382-128">[標準化資料][normalize-data] (兩者)</span><span class="sxs-lookup"><span data-stu-id="dd382-128">[Normalize Data][normalize-data] (both of them)</span></span>
* <span data-ttu-id="dd382-129">[評估模型][ evaluate-model] （因為我們在完成評估 hello 模型）</span><span class="sxs-lookup"><span data-stu-id="dd382-129">[Evaluate Model][evaluate-model] (because we're finished evaluating hello models)</span></span>

<span data-ttu-id="dd382-130">選取每個模組並按下 hello Delete 鍵或以滑鼠右鍵按一下 hello 模組，然後選取**刪除**。</span><span class="sxs-lookup"><span data-stu-id="dd382-130">Select each module and press hello Delete key, or right-click hello module and select **Delete**.</span></span> 

![移除 hello SVM 模型][3a]

<span data-ttu-id="dd382-132">我們的模型現在看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="dd382-132">Our model should now look something like this:</span></span>

![移除 hello SVM 模型][3]

<span data-ttu-id="dd382-134">現在我們準備 toodeploy 此模型使用 hello[二級促進式決策樹][two-class-boosted-decision-tree]。</span><span class="sxs-lookup"><span data-stu-id="dd382-134">Now we're ready toodeploy this model using hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span></span>

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a><span data-ttu-id="dd382-135">轉換 hello 定型實驗 tooa 預測實驗</span><span class="sxs-lookup"><span data-stu-id="dd382-135">Convert hello training experiment tooa predictive experiment</span></span>

<span data-ttu-id="dd382-136">tooget 這模型備妥可進行部署，我們需要 tooconvert 這定型實驗 tooa 預測實驗。</span><span class="sxs-lookup"><span data-stu-id="dd382-136">tooget this model ready for deployment, we need tooconvert this training experiment tooa predictive experiment.</span></span> <span data-ttu-id="dd382-137">這牽涉到三個步驟：</span><span class="sxs-lookup"><span data-stu-id="dd382-137">This involves three steps:</span></span>

1. <span data-ttu-id="dd382-138">儲存 hello 模型，我們已經定型，並取代我們定型模組</span><span class="sxs-lookup"><span data-stu-id="dd382-138">Save hello model we've trained and then replace our training modules</span></span>
2. <span data-ttu-id="dd382-139">Trim 只所需的訓練的 hello 實驗 tooremove 模組</span><span class="sxs-lookup"><span data-stu-id="dd382-139">Trim hello experiment tooremove modules that were only needed for training</span></span>
3. <span data-ttu-id="dd382-140">定義 hello web 服務會接受輸入的位置，以及它會產生 hello 輸出</span><span class="sxs-lookup"><span data-stu-id="dd382-140">Define where hello web service will accept input and where it generates hello output</span></span>

<span data-ttu-id="dd382-141">我們無法手動執行這項，但幸運的是所有三個步驟，可透過按一下**設定 Web 服務**在 hello hello 實驗畫布底部 (選取 hello**預測 Web 服務**選項）。</span><span class="sxs-lookup"><span data-stu-id="dd382-141">We could do this manually, but fortunately all three steps can be accomplished by clicking **Set Up Web Service** at hello bottom of hello experiment canvas (and selecting hello **Predictive Web Service** option).</span></span>

> [!TIP]
> <span data-ttu-id="dd382-142">如果您想更多詳細資料上轉換定型實驗 tooa 預測時，會發生什麼情況進行實驗，請參閱[如何 tooprepare Azure Machine Learning Studio 中的部署模型](machine-learning-convert-training-experiment-to-scoring-experiment.md)。</span><span class="sxs-lookup"><span data-stu-id="dd382-142">If you want more details on what happens when you convert a training experiment tooa predictive experiment, see [How tooprepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="dd382-143">當您按一下 [設定 Web 服務] ，會發生幾件事：</span><span class="sxs-lookup"><span data-stu-id="dd382-143">When you click **Set Up Web Service**, several things happen:</span></span>

* <span data-ttu-id="dd382-144">hello 定型的模型為單一轉換的 tooa**定型的模型**模組，而儲存在 hello 模組調色盤 toohello 實驗畫布左邊的 hello (您可以找到在**定型的模型**)</span><span class="sxs-lookup"><span data-stu-id="dd382-144">hello trained model is converted tooa single **Trained Model** module and stored in hello module palette toohello left of hello experiment canvas (you can find it under **Trained Models**)</span></span>
* <span data-ttu-id="dd382-145">用於定型的模組已遭到移除，尤其是：</span><span class="sxs-lookup"><span data-stu-id="dd382-145">Modules that were used for training are removed; specifically:</span></span>
  * <span data-ttu-id="dd382-146">[二元促進式決策樹][two-class-boosted-decision-tree]</span><span class="sxs-lookup"><span data-stu-id="dd382-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span></span>
  * <span data-ttu-id="dd382-147">[定型模型][train-model]</span><span class="sxs-lookup"><span data-stu-id="dd382-147">[Train Model][train-model]</span></span>
  * <span data-ttu-id="dd382-148">[資料分割][split]</span><span class="sxs-lookup"><span data-stu-id="dd382-148">[Split Data][split]</span></span>
  * <span data-ttu-id="dd382-149">第二個 hello[執行 R 指令碼][ execute-r-script]用於測試資料的模組</span><span class="sxs-lookup"><span data-stu-id="dd382-149">hello second [Execute R Script][execute-r-script] module that was used for test data</span></span>
* <span data-ttu-id="dd382-150">hello 儲存已定型的模型是已加回到 hello 實驗</span><span class="sxs-lookup"><span data-stu-id="dd382-150">hello saved trained model is added back into hello experiment</span></span>
* <span data-ttu-id="dd382-151">**Web 服務輸入**和**Web 服務輸出**加入模組 （這些識別 hello 使用者資料將在其中輸入 hello 模型，以及傳回的資料，存取 hello web 服務時）</span><span class="sxs-lookup"><span data-stu-id="dd382-151">**Web service input** and **Web service output** modules are added (these identify where hello user's data will enter hello model, and what data is returned, when hello web service is accessed)</span></span>

> [!NOTE]
> <span data-ttu-id="dd382-152">您可以看到 hello 實驗會儲存在已加入在 hello 實驗畫布 hello 最上方的索引標籤下的兩個部分。</span><span class="sxs-lookup"><span data-stu-id="dd382-152">You can see that hello experiment is saved in two parts under tabs that have been added at hello top of hello experiment canvas.</span></span> <span data-ttu-id="dd382-153">hello 原始定型實驗是 hello 索引標籤下**定型實驗**，以及新建立的預測實驗 hello 低於**預測實驗**。</span><span class="sxs-lookup"><span data-stu-id="dd382-153">hello original training experiment is under hello tab **Training experiment**, and hello newly created predictive experiment is under **Predictive experiment**.</span></span> <span data-ttu-id="dd382-154">hello 預測實驗為 hello 我們將會部署為 web 服務的其中一個。</span><span class="sxs-lookup"><span data-stu-id="dd382-154">hello predictive experiment is hello one we'll deploy as a web service.</span></span>

<span data-ttu-id="dd382-155">我們需要 tootake 一個額外的步驟與此特定實驗。</span><span class="sxs-lookup"><span data-stu-id="dd382-155">We need tootake one additional step with this particular experiment.</span></span>
<span data-ttu-id="dd382-156">我們新增了兩個[執行 R 指令碼][ execute-r-script]模組 tooprovide 加權函式 toohello 資料。</span><span class="sxs-lookup"><span data-stu-id="dd382-156">We added two [Execute R Script][execute-r-script] modules tooprovide a weighting function toohello data.</span></span> <span data-ttu-id="dd382-157">因此，我們可以接受出 hello 最終模型中的那些模組時只會用於定型和測試，我們需要一墩。</span><span class="sxs-lookup"><span data-stu-id="dd382-157">That was just a trick we needed for training and testing, so we can take out those modules in hello final model.</span></span>
<span data-ttu-id="dd382-158">Machine Learning Studio 移除其中一個[執行 R 指令碼][ execute-r-script]模組時移除它 hello[分割][ split]模組。</span><span class="sxs-lookup"><span data-stu-id="dd382-158">Machine Learning Studio removed one [Execute R Script][execute-r-script] module when it removed hello [Split][split] module.</span></span> <span data-ttu-id="dd382-159">現在我們可以移除其他 hello 以及連接[中繼資料編輯器][ metadata-editor]直接太[計分模型][score-model]。</span><span class="sxs-lookup"><span data-stu-id="dd382-159">Now we can remove hello other and connect [Metadata Editor][metadata-editor] directly too[Score Model][score-model].</span></span>    

<span data-ttu-id="dd382-160">實驗現在看起來如下：</span><span class="sxs-lookup"><span data-stu-id="dd382-160">Our experiment should now look like this:</span></span>  

![計分的 hello 定型的模型][4]  

> [!NOTE]
> <span data-ttu-id="dd382-162">您可能會想知道為什麼我們留 hello UCI 德文信用卡資料集在 hello 預測實驗中。</span><span class="sxs-lookup"><span data-stu-id="dd382-162">You may be wondering why we left hello UCI German Credit Card Data dataset in hello predictive experiment.</span></span> <span data-ttu-id="dd382-163">這樣會產生 tooscore hello 使用者的資料，不 hello 原始資料集，因此為什麼不要 hello 原始資料集 hello 模型中的 hello 服務？</span><span class="sxs-lookup"><span data-stu-id="dd382-163">hello service is going tooscore hello user's data, not hello original dataset, so why leave hello original dataset in hello model?</span></span>
> 
> <span data-ttu-id="dd382-164">」 沒錯 hello 服務不需要 hello 原始信用卡資料。</span><span class="sxs-lookup"><span data-stu-id="dd382-164">It's true that hello service doesn't need hello original credit card data.</span></span> <span data-ttu-id="dd382-165">但 hello 結構描述必須針對該資料，其中包括有多少資料行等資訊，以及哪些資料行是數值。</span><span class="sxs-lookup"><span data-stu-id="dd382-165">But it does need hello schema for that data, which includes information such as how many columns there are and which columns are numeric.</span></span> <span data-ttu-id="dd382-166">這個結構描述資訊是必要的 toointerpret hello 使用者的資料。</span><span class="sxs-lookup"><span data-stu-id="dd382-166">This schema information is necessary toointerpret hello user's data.</span></span> <span data-ttu-id="dd382-167">我們會保留這些連線，如此 hello 計分模組擁有 hello 資料集結構描述時 hello 服務正在執行的元件。</span><span class="sxs-lookup"><span data-stu-id="dd382-167">We leave these components connected so that hello scoring module has hello dataset schema when hello service is running.</span></span> <span data-ttu-id="dd382-168">hello 資料不會使用，只要 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="dd382-168">hello data isn't used, just hello schema.</span></span>  
> 
> 

<span data-ttu-id="dd382-169">執行 hello 實驗最後一次 (按一下**執行**。)如果您想 hello 模型的 tooverify 仍然可以運作，請按一下的 hello hello 輸出[計分模型][ score-model]模組，然後選取**檢視結果**。</span><span class="sxs-lookup"><span data-stu-id="dd382-169">Run hello experiment one last time (click **Run**.) If you want tooverify that hello model is still working, click hello output of hello [Score Model][score-model] module and select **View Results**.</span></span> <span data-ttu-id="dd382-170">您可以看到顯示 hello 原始資料，以及 hello 信用風險值 （「 計分標籤 」），並 hello 計分機率值 （「 計分機率 」。）</span><span class="sxs-lookup"><span data-stu-id="dd382-170">You can see that hello original data is displayed, along with hello credit risk value ("Scored Labels") and hello scoring probability value ("Scored Probabilities".)</span></span> 

## <a name="deploy-hello-web-service"></a><span data-ttu-id="dd382-171">部署 hello web 服務</span><span class="sxs-lookup"><span data-stu-id="dd382-171">Deploy hello web service</span></span>
<span data-ttu-id="dd382-172">為其中一個傳統 web 服務，或為新的 web 服務為基礎的 Azure 資源管理員，您可以部署 hello 實驗。</span><span class="sxs-lookup"><span data-stu-id="dd382-172">You can deploy hello experiment as either a Classic web service, or as a New web service that's based on Azure Resource Manager.</span></span>

### <a name="deploy-as-a-classic-web-service"></a><span data-ttu-id="dd382-173">部署為傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="dd382-173">Deploy as a Classic web service</span></span>
<span data-ttu-id="dd382-174">按一下 toodeploy 傳統 web 服務實驗中，從衍生**部署 Web 服務**下方 hello 畫布，然後選取**部署 Web 服務 [傳統]**。</span><span class="sxs-lookup"><span data-stu-id="dd382-174">toodeploy a Classic web service derived from our experiment, click **Deploy Web Service** below hello canvas and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="dd382-175">Machine Learning Studio 會部署為 web 服務的 hello 實驗，並引導您 toohello 儀表板的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="dd382-175">Machine Learning Studio deploys hello experiment as a web service and takes you toohello dashboard for that web service.</span></span> <span data-ttu-id="dd382-176">從這個頁面中，您可以傳回 toohello 實驗 (**檢視快照集**或**檢視最新**) 並執行簡單的測試 hello web 服務 (請參閱**測試 hello web 服務**下方)。</span><span class="sxs-lookup"><span data-stu-id="dd382-176">From this page you can return toohello experiment (**View snapshot** or **View latest**) and run a simple test of hello web service (see **Test hello web service** below).</span></span> <span data-ttu-id="dd382-177">另外還有這裡建立可以存取 hello web 服務 （更多的 hello 本逐步解說的下一個步驟中） 的應用程式的資訊。</span><span class="sxs-lookup"><span data-stu-id="dd382-177">There is also information here for creating applications that can access hello web service (more on that in hello next step of this walkthrough).</span></span>

![Web 服務儀表板][6]

<span data-ttu-id="dd382-179">您可以設定 hello 服務即可 hello**組態** 索引標籤。您可以在這裡修改 hello （它是預設的給定的 hello 實驗名稱） 的服務名稱並提供它的描述。</span><span class="sxs-lookup"><span data-stu-id="dd382-179">You can configure hello service by clicking hello **CONFIGURATION** tab. Here you can modify hello service name (it's given hello experiment name by default) and give it a description.</span></span> <span data-ttu-id="dd382-180">您也可以提供更多的易記標籤 hello 輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="dd382-180">You can also give more friendly labels for hello input and output data.</span></span>  

![設定 hello web 服務][5]  

### <a name="deploy-as-a-new-web-service"></a><span data-ttu-id="dd382-182">部署為新式 Web 服務</span><span class="sxs-lookup"><span data-stu-id="dd382-182">Deploy as a New web service</span></span>

> [!NOTE] 
> <span data-ttu-id="dd382-183">新的 web 服務，您必須擁有足夠的權限，在您要部署的 hello 訂用帳戶 toowhich toodeploy hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="dd382-183">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you are deploying hello web service.</span></span> <span data-ttu-id="dd382-184">如需詳細資訊，請參閱[管理 web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="dd382-184">For more information, see [Manage a web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="dd382-185">新的 web 服務 toodeploy 衍生自我們實驗：</span><span class="sxs-lookup"><span data-stu-id="dd382-185">toodeploy a New web service derived from our experiment:</span></span>

1. <span data-ttu-id="dd382-186">按一下**部署 Web 服務**下方 hello 畫布，然後選取**部署 Web 服務 [New]**。</span><span class="sxs-lookup"><span data-stu-id="dd382-186">Click **Deploy Web Service** below hello canvas and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="dd382-187">Machine Learning Studio 會傳輸 toohello Azure Machine Learning web 服務**部署實驗**頁面。</span><span class="sxs-lookup"><span data-stu-id="dd382-187">Machine Learning Studio transfers you toohello Azure Machine Learning web services **Deploy Experiment** page.</span></span>

2. <span data-ttu-id="dd382-188">輸入 hello web 服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="dd382-188">Enter a name for hello web service.</span></span> 

3. <span data-ttu-id="dd382-189">如**價格計劃**、 您可以選取現有的定價方案，或選取 「 建立新的 」 和授與 hello 新計劃的名稱和選取 hello 每月的計劃選項。</span><span class="sxs-lookup"><span data-stu-id="dd382-189">For **Price Plan**, you can select an existing pricing plan, or select "Create new" and give hello new plan a name and select hello monthly plan option.</span></span> <span data-ttu-id="dd382-190">hello 計劃層預設 toohello 計劃您預設的地區和您的 web 服務是部署的 toothat 區域。</span><span class="sxs-lookup"><span data-stu-id="dd382-190">hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

4. <span data-ttu-id="dd382-191">按一下 [ **部署**]。</span><span class="sxs-lookup"><span data-stu-id="dd382-191">Click **Deploy**.</span></span>

<span data-ttu-id="dd382-192">請稍候幾分鐘 hello**快速入門**web 服務 頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="dd382-192">After a few minutes, hello **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="dd382-193">您可以設定 hello 服務即可 hello**設定** 索引標籤。您可以在這裡修改 hello 服務標題，並提供它的描述。</span><span class="sxs-lookup"><span data-stu-id="dd382-193">You can configure hello service by clicking hello **Configure** tab. Here you can modify hello service title and give it a description.</span></span> 

<span data-ttu-id="dd382-194">tootest hello web 服務，請按一下 hello**測試** 索引標籤 (請參閱**測試 hello web 服務**下方)。</span><span class="sxs-lookup"><span data-stu-id="dd382-194">tootest hello web service, click hello **Test** tab (see **Test hello web service** below).</span></span> <span data-ttu-id="dd382-195">建立可以存取 hello web 服務的應用程式的資訊，請按一下 hello**取用** 索引標籤 （在此逐步解說中的 hello 下一個步驟將移到更多詳細資料）。</span><span class="sxs-lookup"><span data-stu-id="dd382-195">For information on creating applications that can access hello web service, click hello **Consume** tab (hello next step in this walkthrough will go into more detail).</span></span>

> [!TIP]
> <span data-ttu-id="dd382-196">已部署完成之後，您可以更新 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="dd382-196">You can update hello web service after you've deployed it.</span></span> <span data-ttu-id="dd382-197">例如，如果您想 toochange 您的模型，然後您可以編輯 hello 定型實驗、 調整 hello 模型參數，然後按一下**部署 Web 服務**、 選取**部署 Web 服務 [傳統]**或**部署 Web 服務 [New]**。</span><span class="sxs-lookup"><span data-stu-id="dd382-197">For example, if you want toochange your model, then you can edit hello training experiment, tweak hello model parameters, and click **Deploy Web Service**, selecting **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span> <span data-ttu-id="dd382-198">當您重新部署 hello 實驗時，它會取代 hello web 服務，現在使用更新的模型。</span><span class="sxs-lookup"><span data-stu-id="dd382-198">When you deploy hello experiment again, it replaces hello web service, now using your updated model.</span></span>  
> 
> 

## <a name="test-hello-web-service"></a><span data-ttu-id="dd382-199">測試 hello web 服務</span><span class="sxs-lookup"><span data-stu-id="dd382-199">Test hello web service</span></span>

<span data-ttu-id="dd382-200">Hello 使用者資料存取 hello web 服務時，進入透過 hello **Web 服務輸入**模組，其中已通過 toohello[計分模型][ score-model]模組和計分。</span><span class="sxs-lookup"><span data-stu-id="dd382-200">When hello web service is accessed, hello user's data enters through hello **Web service input** module where it's passed toohello [Score Model][score-model] module and scored.</span></span> <span data-ttu-id="dd382-201">我們設定 hello 預測實驗 hello 方式，hello 模型預期的 hello 相同格式化為 hello 原始信用風險資料集的資料。</span><span class="sxs-lookup"><span data-stu-id="dd382-201">hello way we've set up hello predictive experiment, hello model expects data in hello same format as hello original credit risk dataset.</span></span>
<span data-ttu-id="dd382-202">hello 結果 toohello 使用者從 hello web 服務透過 hello **Web 服務輸出**模組。</span><span class="sxs-lookup"><span data-stu-id="dd382-202">hello results are returned toohello user from hello web service through hello **Web service output** module.</span></span>

> [!TIP]
> <span data-ttu-id="dd382-203">我們有 hello 預測實驗設定，整個 hello hello 方法得到的 hello[計分模型][ score-model]模組會傳回。</span><span class="sxs-lookup"><span data-stu-id="dd382-203">hello way we have hello predictive experiment configured, hello entire results from hello [Score Model][score-model] module are returned.</span></span> <span data-ttu-id="dd382-204">這包括所有 hello 輸入的資料加上 hello 信用風險值和 hello 計分可能性。</span><span class="sxs-lookup"><span data-stu-id="dd382-204">This includes all hello input data plus hello credit risk value and hello scoring probability.</span></span> <span data-ttu-id="dd382-205">但如果您想要傳回不同的項目-例如，您可能會傳回只 hello 信用風險的值。</span><span class="sxs-lookup"><span data-stu-id="dd382-205">But you can return something different if you want - for example, you could return just hello credit risk value.</span></span> <span data-ttu-id="dd382-206">toodo 此，插入[投射資料行][ project-columns]模組之間[計分模型][ score-model]和 hello **Web 服務輸出** tooeliminate 資料行，您不想 hello web 服務 tooreturn。</span><span class="sxs-lookup"><span data-stu-id="dd382-206">toodo this, insert a [Project Columns][project-columns] module between [Score Model][score-model] and hello **Web service output** tooeliminate columns you don't want hello web service tooreturn.</span></span> 
> 
> 

<span data-ttu-id="dd382-207">您可以測試傳統 web 服務有兩種**Machine Learning Studio**或 hello **Azure 機器學習 Web 服務**入口網站。</span><span class="sxs-lookup"><span data-stu-id="dd382-207">You can test a Classic web service either in **Machine Learning Studio** or in hello **Azure Machine Learning Web Services** portal.</span></span>
<span data-ttu-id="dd382-208">您可以測試新的 web 服務只能在 hello**機器學習 Web 服務**入口網站。</span><span class="sxs-lookup"><span data-stu-id="dd382-208">You can test a New web service only in hello **Machine Learning Web Services** portal.</span></span>

> [!TIP]
> <span data-ttu-id="dd382-209">測試時在 hello Azure 機器學習 Web 服務入口網站中，您可以建立範例資料，您可以使用 tootest hello 要求-回應服務的 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="dd382-209">When testing in hello Azure Machine Learning Web Services portal, you can have hello portal create sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="dd382-210">在 hello**設定**頁面上，選取 是**啟用範例資料嗎？**。</span><span class="sxs-lookup"><span data-stu-id="dd382-210">On hello **Configure** page, select "Yes" for **Sample Data Enabled?**.</span></span> <span data-ttu-id="dd382-211">當您開啟 hello 要求-回應 索引標籤上 hello**測試** 頁面上，hello 入口網站會填入取自 hello 原始信用風險資料集的範例資料。</span><span class="sxs-lookup"><span data-stu-id="dd382-211">When you open hello Request-Response tab on hello **Test** page, hello portal fills in sample data taken from hello original credit risk dataset.</span></span>

### <a name="test-a-classic-web-service"></a><span data-ttu-id="dd382-212">測試傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="dd382-212">Test a Classic web service</span></span>

<span data-ttu-id="dd382-213">Machine Learning Studio 中或 hello 機器學習 Web 服務入口網站中，您可以測試傳統 web 服務。</span><span class="sxs-lookup"><span data-stu-id="dd382-213">You can test a Classic web service in Machine Learning Studio or in hello Machine Learning Web Services portal.</span></span> 

#### <a name="test-in-machine-learning-studio"></a><span data-ttu-id="dd382-214">在 Machine Learning Studio 中測試</span><span class="sxs-lookup"><span data-stu-id="dd382-214">Test in Machine Learning Studio</span></span>

1. <span data-ttu-id="dd382-215">在 hello**儀表板**hello web 服務頁面上，按一下 hello**測試**按鈕底下**預設端點**。</span><span class="sxs-lookup"><span data-stu-id="dd382-215">On hello **DASHBOARD** page for hello web service, click hello **Test** button under **Default Endpoint**.</span></span> <span data-ttu-id="dd382-216">對話方塊出現，並會要求您輸入 hello hello 服務的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="dd382-216">A dialog pops up and asks you for hello input data for hello service.</span></span> <span data-ttu-id="dd382-217">這些是 hello 相同的資料行出現在 hello 原始信用風險資料集。</span><span class="sxs-lookup"><span data-stu-id="dd382-217">These are hello same columns that appeared in hello original credit risk dataset.</span></span>  

2. <span data-ttu-id="dd382-218">輸入一組資料，然後按一下確定 。</span><span class="sxs-lookup"><span data-stu-id="dd382-218">Enter a set of data and then click **OK**.</span></span> 

#### <a name="test-in-hello-machine-learning-web-services-portal"></a><span data-ttu-id="dd382-219">在 hello 機器學習 Web 服務入口網站中測試</span><span class="sxs-lookup"><span data-stu-id="dd382-219">Test in hello Machine Learning Web Services portal</span></span>

1. <span data-ttu-id="dd382-220">在 hello**儀表板**hello web 服務頁面上，按一下 hello**測試預覽**連結底下**預設端點**。</span><span class="sxs-lookup"><span data-stu-id="dd382-220">On hello **DASHBOARD** page for hello web service, click hello **Test preview** link under **Default Endpoint**.</span></span> <span data-ttu-id="dd382-221">hello web 服務端點的 hello Azure 機器學習 Web 服務入口網站中的 hello 測試頁隨即開啟，並會要求您輸入 hello hello 服務的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="dd382-221">hello test page in hello Azure Machine Learning Web Services portal for hello web service endpoint opens and asks you for hello input data for hello service.</span></span> <span data-ttu-id="dd382-222">這些是 hello 相同的資料行出現在 hello 原始信用風險資料集。</span><span class="sxs-lookup"><span data-stu-id="dd382-222">These are hello same columns that appeared in hello original credit risk dataset.</span></span>

2. <span data-ttu-id="dd382-223">按一下 [測試要求-回應]。</span><span class="sxs-lookup"><span data-stu-id="dd382-223">Click **Test Request-Response**.</span></span> 

### <a name="test-a-new-web-service"></a><span data-ttu-id="dd382-224">測試新式 Web 服務</span><span class="sxs-lookup"><span data-stu-id="dd382-224">Test a New web service</span></span>

<span data-ttu-id="dd382-225">您可以只在 hello 機器學習 Web 服務入口網站中測試新的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="dd382-225">You can test a New web service only in hello Machine Learning Web Services portal.</span></span>

1. <span data-ttu-id="dd382-226">在 hello [Azure 機器學習 Web 服務](https://services.azureml.net/quickstart)入口網站中，按一下**測試**hello 頁面頂端的 hello。</span><span class="sxs-lookup"><span data-stu-id="dd382-226">In hello [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal, click **Test** at hello top of hello page.</span></span> <span data-ttu-id="dd382-227">hello**測試** 頁面隨即開啟，您可以輸入 hello 服務的資料。</span><span class="sxs-lookup"><span data-stu-id="dd382-227">hello **Test** page opens and you can input data for hello service.</span></span> <span data-ttu-id="dd382-228">hello 輸入所顯示的欄位對應 toohello 資料行出現在 hello 原始信用風險資料集。</span><span class="sxs-lookup"><span data-stu-id="dd382-228">hello input fields displayed correspond toohello columns that appeared in hello original credit risk dataset.</span></span> 

2. <span data-ttu-id="dd382-229">輸入一組資料，然後按一下測試要求-回應 。</span><span class="sxs-lookup"><span data-stu-id="dd382-229">Enter a set of data and then click **Test Request-Response**.</span></span>

<span data-ttu-id="dd382-230">hello hello 測試的結果會顯示在 hello 右手邊的 hello 輸出資料行中的 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="dd382-230">hello results of hello test are displayed on hello right-hand side of hello page in hello output column.</span></span> 


## <a name="manage-hello-web-service"></a><span data-ttu-id="dd382-231">管理 hello web 服務</span><span class="sxs-lookup"><span data-stu-id="dd382-231">Manage hello web service</span></span>

### <a name="manage-a-classic-web-service-in-hello-azure-classic-portal"></a><span data-ttu-id="dd382-232">管理 hello Azure 傳統入口網站中的傳統 web 服務</span><span class="sxs-lookup"><span data-stu-id="dd382-232">Manage a Classic web service in hello Azure classic portal</span></span>

<span data-ttu-id="dd382-233">一旦您部署了傳統 web 服務，您可以從管理 hello [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="dd382-233">Once you've deployed your Classic web service, you can manage it from hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="dd382-234">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="dd382-234">Sign in toohello [Azure classic portal](https://manage.windowsazure.com)</span></span>
2. <span data-ttu-id="dd382-235">在 hello Microsoft Azure 服務面板中，按一下 **機器學習服務**</span><span class="sxs-lookup"><span data-stu-id="dd382-235">In hello Microsoft Azure services panel, click **MACHINE LEARNING**</span></span>
3. <span data-ttu-id="dd382-236">按一下您的工作區</span><span class="sxs-lookup"><span data-stu-id="dd382-236">Click your workspace</span></span>
4. <span data-ttu-id="dd382-237">按一下 hello **Web 服務** 索引標籤</span><span class="sxs-lookup"><span data-stu-id="dd382-237">Click hello **Web services** tab</span></span>
5. <span data-ttu-id="dd382-238">按一下 建立 hello web 服務</span><span class="sxs-lookup"><span data-stu-id="dd382-238">Click hello web service we created</span></span>
6. <span data-ttu-id="dd382-239">按一下 hello 「 預設 」 端點</span><span class="sxs-lookup"><span data-stu-id="dd382-239">Click hello "default" endpoint</span></span>

<span data-ttu-id="dd382-240">從這裡，您可以執行一些作業，例如監視 hello web 服務執行的動作，並變更多少同時呼叫 hello 服務可以處理，導致效能做調整。</span><span class="sxs-lookup"><span data-stu-id="dd382-240">From here, you can do things like monitor how hello web service is doing and make performance tweaks by changing how many concurrent calls hello service can handle.</span></span>

<span data-ttu-id="dd382-241">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="dd382-241">For more details, see:</span></span>

* [<span data-ttu-id="dd382-242">建立端點</span><span class="sxs-lookup"><span data-stu-id="dd382-242">Creating Endpoints</span></span>](machine-learning-create-endpoint.md)
* [<span data-ttu-id="dd382-243">調整 Web 服務</span><span class="sxs-lookup"><span data-stu-id="dd382-243">Scaling web service</span></span>](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="dd382-244">管理傳統或 hello Azure 機器學習 Web 服務入口網站中的新 web 服務</span><span class="sxs-lookup"><span data-stu-id="dd382-244">Manage a Classic or New web service in hello Azure Machine Learning Web Services portal</span></span>

<span data-ttu-id="dd382-245">一旦您是否傳統或新部署您的 web 服務，您可以從管理 hello [Microsoft Azure 機器學習 Web 服務](https://services.azureml.net/quickstart)入口網站。</span><span class="sxs-lookup"><span data-stu-id="dd382-245">Once you've deployed your web service, whether Classic or New, you can manage it from hello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal.</span></span>

<span data-ttu-id="dd382-246">您的 web 服務的 toomonitor hello 效能：</span><span class="sxs-lookup"><span data-stu-id="dd382-246">toomonitor hello performance of your web service:</span></span>

1. <span data-ttu-id="dd382-247">登入 toohello [Microsoft Azure 機器學習 Web 服務](https://services.azureml.net/quickstart)入口網站</span><span class="sxs-lookup"><span data-stu-id="dd382-247">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal</span></span>
2. <span data-ttu-id="dd382-248">按一下 [Web 服務]</span><span class="sxs-lookup"><span data-stu-id="dd382-248">Click **Web services**</span></span>
3. <span data-ttu-id="dd382-249">按一下您的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="dd382-249">Click your web service</span></span>
4. <span data-ttu-id="dd382-250">按一下 hello**儀表板**</span><span class="sxs-lookup"><span data-stu-id="dd382-250">Click hello **Dashboard**</span></span>

- - -
<span data-ttu-id="dd382-251">**下一步:[存取 hello web 服務](machine-learning-walkthrough-6-access-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="dd382-251">**Next: [Access hello web service](machine-learning-walkthrough-6-access-web-service.md)**</span></span>

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
