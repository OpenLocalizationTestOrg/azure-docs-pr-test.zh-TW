---
title: "如何準備您的模型以在 Azure Machine Learning Studio 中部署 | Microsoft Docs"
description: "如何將 Machine Learning Studio 訓練實驗轉換為預測實驗，將其準備妥當進行部署，然後當做 Web 服務部署。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: eb943c45-541a-401d-844a-c3337de82da6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: garye
ms.openlocfilehash: 716a9a9b723df7ff6eb111fa40f2b5941d57d67a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-prepare-your-model-for-deployment-in-azure-machine-learning-studio"></a><span data-ttu-id="4b40c-103">如何準備您的模型以在 Azure Machine Learning Studio 中部署</span><span class="sxs-lookup"><span data-stu-id="4b40c-103">How to prepare your model for deployment in Azure Machine Learning Studio</span></span>

<span data-ttu-id="4b40c-104">Azure Machine Learning Studio 提供所需的工具，以讓您開發預測分析模型，然後將它部署為 Azure Web 服務來進行個人化。</span><span class="sxs-lookup"><span data-stu-id="4b40c-104">Azure Machine Learning Studio gives you the tools you need to develop a predictive analytics model and then operationalize it by deploying it as an Azure web service.</span></span>

<span data-ttu-id="4b40c-105">若要這樣做，您必須使用 Studio 建立一個稱為「訓練實驗」的實驗，以訓練、評分和編輯您的模型。</span><span class="sxs-lookup"><span data-stu-id="4b40c-105">To do this, you use Studio to create an experiment - called a *training experiment* - where you train, score, and edit your model.</span></span> <span data-ttu-id="4b40c-106">滿意之後，即備妥模型以進行部署，方法是將訓練實驗轉換成「預測實驗」，並將後者設定成給使用者資料評分。</span><span class="sxs-lookup"><span data-stu-id="4b40c-106">Once you're satisfied, you get your model ready to deploy by converting your training experiment to a *predictive experiment* that's configured to score user data.</span></span>

<span data-ttu-id="4b40c-107">如需此程序的範例，請參閱[逐步解說：在 Azure Machine Learning 中為信用風險評估開發預測分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)。</span><span class="sxs-lookup"><span data-stu-id="4b40c-107">You can see an example of this process in [Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

<span data-ttu-id="4b40c-108">本文所深入探討的詳細資料是有關如何將訓練實驗轉換成預測實驗，以及預測實驗的部署方式。</span><span class="sxs-lookup"><span data-stu-id="4b40c-108">This article takes a deep dive into the details of how a training experiment gets converted into a predictive experiment, and how that predictive experiment is deployed.</span></span> <span data-ttu-id="4b40c-109">了解這些詳細資料，即可了解如何設定您已部署的模型，以讓它更具效率。</span><span class="sxs-lookup"><span data-stu-id="4b40c-109">By understanding these details, you can learn how to configure your deployed model to make it more effective.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a><span data-ttu-id="4b40c-110">概觀</span><span class="sxs-lookup"><span data-stu-id="4b40c-110">Overview</span></span> 

<span data-ttu-id="4b40c-111">將訓練實驗轉換為預測實驗包含三個步驟：</span><span class="sxs-lookup"><span data-stu-id="4b40c-111">The process of converting a training experiment to a predictive experiment involves three steps:</span></span>

1. <span data-ttu-id="4b40c-112">將機器學習演算法模組取代為定型模型。</span><span class="sxs-lookup"><span data-stu-id="4b40c-112">Replace the machine learning algorithm modules with your trained model.</span></span>
2. <span data-ttu-id="4b40c-113">將訓練調整為僅適用於評分所需的模組。</span><span class="sxs-lookup"><span data-stu-id="4b40c-113">Trim the experiment to only those modules that are needed for scoring.</span></span> <span data-ttu-id="4b40c-114">訓練實驗包含訓練所需但模型受過訓練之後，就不再需要的多個模組。</span><span class="sxs-lookup"><span data-stu-id="4b40c-114">A training experiment includes a number of modules that are necessary for training but are not needed once the model is trained.</span></span>
3. <span data-ttu-id="4b40c-115">定義模型如何接受來自 Web 服務使用者的資料，以及將傳回的資料。</span><span class="sxs-lookup"><span data-stu-id="4b40c-115">Define how your model will accept data from the web service user, and what data will be returned.</span></span>

> [!TIP]
> <span data-ttu-id="4b40c-116">在訓練實驗中，您曾考慮使用您自己的資料來訓練和評分模型。</span><span class="sxs-lookup"><span data-stu-id="4b40c-116">In your training experiment, you've been concerned with training and scoring your model using your own data.</span></span> <span data-ttu-id="4b40c-117">但部署之後，使用者就會將新的資料傳送至您的模型，而且會傳回預測結果。</span><span class="sxs-lookup"><span data-stu-id="4b40c-117">But once deployed, users will send new data to your model and it will return prediction results.</span></span> <span data-ttu-id="4b40c-118">因此，將訓練實驗轉換成預測實驗以準備好進行部署時，請記住其他人如何使用模型。</span><span class="sxs-lookup"><span data-stu-id="4b40c-118">So, as you convert your training experiment to a predictive experiment to get it ready for deployment, keep in mind how the model will be used by others.</span></span>
> 
> 

## <a name="set-up-web-service-button"></a><span data-ttu-id="4b40c-119">設定 Web 服務按鈕</span><span class="sxs-lookup"><span data-stu-id="4b40c-119">Set Up Web Service button</span></span>
<span data-ttu-id="4b40c-120">執行實驗之後 (按一下實驗畫布底端的 [執行])，請按一下 [設定 Web 服務] 按鈕 (選取 [預測 Web 服務] 選項)。</span><span class="sxs-lookup"><span data-stu-id="4b40c-120">After you run your experiment (click **RUN** at the bottom of the experiment canvas), click the **Set Up Web Service** button (select the **Predictive Web Service** option).</span></span> <span data-ttu-id="4b40c-121">[設定 Web 服務] 會執行三個步驟，以將訓練實驗轉換為預測實驗：</span><span class="sxs-lookup"><span data-stu-id="4b40c-121">**Set Up Web Service** performs for you the three steps of converting your training experiment to a predictive experiment:</span></span>

1. <span data-ttu-id="4b40c-122">它會將定型模型儲存到實驗畫布左側之模組選擇區的 [定型模型] 區段中。</span><span class="sxs-lookup"><span data-stu-id="4b40c-122">It saves your trained model in the **Trained Models** section of the module palette (to the left of the experiment canvas).</span></span> <span data-ttu-id="4b40c-123">它接著會將機器學習演算法和[定型模型][train-model]模組取代為所儲存的定型模型。</span><span class="sxs-lookup"><span data-stu-id="4b40c-123">It then replaces the machine learning algorithm and [Train Model][train-model] modules with the saved trained model.</span></span>
2. <span data-ttu-id="4b40c-124">它會分析您的實驗，並移除已清楚僅用於定型且不再需要的模組。</span><span class="sxs-lookup"><span data-stu-id="4b40c-124">It analyzes your experiment and removes modules that were clearly used only for training and are no longer needed.</span></span>
3. <span data-ttu-id="4b40c-125">它會將 _Web 服務輸入_和_輸出_模組插入實驗中的預設位置 (這些模組會接受並傳回使用者資料)。</span><span class="sxs-lookup"><span data-stu-id="4b40c-125">It inserts _Web service input_ and _output_ modules into default locations in your experiment (these modules accept and return user data).</span></span>

<span data-ttu-id="4b40c-126">例如，以下實驗會使用範例人口普查資料，訓練二元推進式決策樹模型：</span><span class="sxs-lookup"><span data-stu-id="4b40c-126">For example, the following experiment trains a two-class boosted decision tree model using sample census data:</span></span>

![訓練實驗][figure1]

<span data-ttu-id="4b40c-128">這項實驗中的模組基本上執行是四個不同的功能：</span><span class="sxs-lookup"><span data-stu-id="4b40c-128">The modules in this experiment perform basically four different functions:</span></span>

![模組功能][figure2]

<span data-ttu-id="4b40c-130">當您將這個訓練實驗轉換為預測實驗時，就不再需要其中一些模組，或它們現在有不同的用途：</span><span class="sxs-lookup"><span data-stu-id="4b40c-130">When you convert this training experiment to a predictive experiment, some of these modules are no longer needed, or they now serve a different purpose:</span></span>

* <span data-ttu-id="4b40c-131">**資料** - 在評分期間，不會使用此範例資料集中的資料，因為 Web 服務的使用者會提供要評分的資料。</span><span class="sxs-lookup"><span data-stu-id="4b40c-131">**Data** - The data in this sample dataset is not used during scoring - the user of the web service will supply the data to be scored.</span></span> <span data-ttu-id="4b40c-132">不過，定型模型會使用此資料集中的中繼資料，例如，資料類型。</span><span class="sxs-lookup"><span data-stu-id="4b40c-132">However, the metadata from this dataset, such as data types, is used by the trained model.</span></span> <span data-ttu-id="4b40c-133">因此，您必須將資料集保留在預測實驗中，讓它能夠提供這項中繼資料。</span><span class="sxs-lookup"><span data-stu-id="4b40c-133">So you need to keep the dataset in the predictive experiment so that it can provide this metadata.</span></span>

* <span data-ttu-id="4b40c-134">**準備** - 根據要提交用於評分的使用者資料而定，這些模組不一定需要處理傳入的資料。</span><span class="sxs-lookup"><span data-stu-id="4b40c-134">**Prep** - Depending on the user data that will be submitted for scoring, these modules may or may not be necessary to process the incoming data.</span></span> <span data-ttu-id="4b40c-135">[設定 Web 服務] 按鈕並未接觸這些項目，您需要決定要如何處理它們。</span><span class="sxs-lookup"><span data-stu-id="4b40c-135">The **Set Up Web Service** button doesn't touch these - you need to decide how you want to handle them.</span></span>
  
    <span data-ttu-id="4b40c-136">例如，在此範例中，範例資料集可能會有遺漏的值，因此，會包含[清除遺漏資料][clean-missing-data]模型來處理它們。</span><span class="sxs-lookup"><span data-stu-id="4b40c-136">For instance, in this example the sample dataset may have missing values, so a [Clean Missing Data][clean-missing-data] module was included to deal with them.</span></span> <span data-ttu-id="4b40c-137">而且，範例資料集會包括培訓模型不需要的資料行。</span><span class="sxs-lookup"><span data-stu-id="4b40c-137">Also, the sample dataset includes columns that are not needed to train the model.</span></span> <span data-ttu-id="4b40c-138">因此，包括[選取資料集中的資料行][select-columns]模組，以將那些額外的資料行從資料流程中排除。</span><span class="sxs-lookup"><span data-stu-id="4b40c-138">So a [Select Columns in Dataset][select-columns] module was included to exclude those extra columns from the data flow.</span></span> <span data-ttu-id="4b40c-139">如果您知道透過 Web 服務提交用於評分的資料不會有遺漏的值，則您可以移除[清除遺漏的資料][clean-missing-data]模組。</span><span class="sxs-lookup"><span data-stu-id="4b40c-139">If you know that the data that will be submitted for scoring through the web service will not have missing values, then you can remove the [Clean Missing Data][clean-missing-data] module.</span></span> <span data-ttu-id="4b40c-140">不過，因為[選取資料集中的資料行][select-columns]模組有助於定義定型模型所預期的資料行，所以必須保留該模組。</span><span class="sxs-lookup"><span data-stu-id="4b40c-140">However, since the [Select Columns in Dataset][select-columns] module helps define the columns of data that the trained model expects, that module needs to remain.</span></span>

* <span data-ttu-id="4b40c-141">**訓練** - 這些模組可用來訓練模型。</span><span class="sxs-lookup"><span data-stu-id="4b40c-141">**Train** - These modules are used to train the model.</span></span> <span data-ttu-id="4b40c-142">當您按一下 [設定 Web 服務] 時，這些模組都會取代為包含定型模型的單一模組。</span><span class="sxs-lookup"><span data-stu-id="4b40c-142">When you click **Set Up Web Service**, these modules are replaced with a single module that contains the model you trained.</span></span> <span data-ttu-id="4b40c-143">這個新模組會儲存在模組調色盤的 [定型模型] 區段。</span><span class="sxs-lookup"><span data-stu-id="4b40c-143">This new module is saved in the **Trained Models** section of the module palette.</span></span>

* <span data-ttu-id="4b40c-144">**評分** - 在此範例中，[分割資料][split]模組是用來將資料流分割成測試資料和訓練資料。</span><span class="sxs-lookup"><span data-stu-id="4b40c-144">**Score** - In this example, the [Split Data][split] module is used to divide the data stream into test data and training data.</span></span> <span data-ttu-id="4b40c-145">在預測實驗中，我們不會再進行訓練，因此可以移除[分割資料][split]。</span><span class="sxs-lookup"><span data-stu-id="4b40c-145">In the predictive experiment, we're not training anymore, so [Split Data][split] can be removed.</span></span> <span data-ttu-id="4b40c-146">同樣地，第二個[評分模型][score-model]模組和[評估模型][evaluate-model]模組會用來比較測試資料的結果，因此在預測實驗中不需要這些模組。</span><span class="sxs-lookup"><span data-stu-id="4b40c-146">Similarly, the second [Score Model][score-model] module and the [Evaluate Model][evaluate-model] module are used to compare results from the test data, so these modules are not needed in the predictive experiment.</span></span> <span data-ttu-id="4b40c-147">但其餘的[評分模型][score-model]模組需要透過 Web 服務傳回評分結果。</span><span class="sxs-lookup"><span data-stu-id="4b40c-147">The remaining [Score Model][score-model] module, however, is needed to return a score result through the web service.</span></span>

<span data-ttu-id="4b40c-148">以下是按一下 [設定 Web 服務] 之後，我們的範例外觀：</span><span class="sxs-lookup"><span data-stu-id="4b40c-148">Here is how our example looks after clicking **Set Up Web Service**:</span></span>

![已轉換的預測實驗][figure3]

<span data-ttu-id="4b40c-150">[設定 Web 服務] 所完成的工作可能足以準備您的實驗，以當做 Web 服務部署。</span><span class="sxs-lookup"><span data-stu-id="4b40c-150">The work done by **Set Up Web Service** may be sufficient to prepare your experiment to be deployed as a web service.</span></span> <span data-ttu-id="4b40c-151">不過，您可能會想要執行一些您的實驗專屬的額外工作。</span><span class="sxs-lookup"><span data-stu-id="4b40c-151">However, you may want to do some additional work specific to your experiment.</span></span>

### <a name="adjust-input-and-output-modules"></a><span data-ttu-id="4b40c-152">調整輸入和輸出模組</span><span class="sxs-lookup"><span data-stu-id="4b40c-152">Adjust input and output modules</span></span>
<span data-ttu-id="4b40c-153">在訓練實驗中，您使用一組訓練資料進行一些處理，以取得 Machine Learning 演算法所需格式的資料。</span><span class="sxs-lookup"><span data-stu-id="4b40c-153">In your training experiment, you used a set of training data and then did some processing to get the data in a form that the machine learning algorithm needed.</span></span> <span data-ttu-id="4b40c-154">如果您預期透過 Web 服務收到的資料不需要這項處理，則可以略過它︰將 **Web 服務輸入模組**的輸出連線至實驗中的不同模組。</span><span class="sxs-lookup"><span data-stu-id="4b40c-154">If the data you expect to receive through the web service will not need this processing, you can bypass it: connect the output of the **Web service input module** to a different module in your experiment.</span></span> <span data-ttu-id="4b40c-155">使用者的資料現在會送到模型的這個位置。</span><span class="sxs-lookup"><span data-stu-id="4b40c-155">The user's data will now arrive in the model at this location.</span></span>

<span data-ttu-id="4b40c-156">例如，[設定 Web 服務] 預設會將 [Web 服務輸入] 模組放在資料流程的頂端，如上圖所示。</span><span class="sxs-lookup"><span data-stu-id="4b40c-156">For example, by default **Set Up Web Service** puts the **Web service input** module at the top of your data flow, as shown in the figure above.</span></span> <span data-ttu-id="4b40c-157">但我們可以手動將 **Web 服務輸入**放在資料處理模組之後：</span><span class="sxs-lookup"><span data-stu-id="4b40c-157">But we can manually position the **Web service input** past the data processing modules:</span></span>

![移動 Web 服務輸入][figure4]

<span data-ttu-id="4b40c-159">透過 Web 服務提供的輸入資料現在會直接傳入 [評分模型] 模組，而不需要任何前置處理。</span><span class="sxs-lookup"><span data-stu-id="4b40c-159">The input data provided through the web service will now pass directly into the Score Model module without any preprocessing.</span></span>

<span data-ttu-id="4b40c-160">同樣地， **設定 Web 服務** 會將 Web 服務輸出模組放在資料流程的底部。</span><span class="sxs-lookup"><span data-stu-id="4b40c-160">Similarly, by default **Set Up Web Service** puts the Web service output module at the bottom of your data flow.</span></span> <span data-ttu-id="4b40c-161">在此範例中，Web 服務會將[評分模型][score-model]模組的輸出傳回給使用者，其中包括完整的輸入資料向量以及評分結果。</span><span class="sxs-lookup"><span data-stu-id="4b40c-161">In this example, the web service will return to the user the output of the [Score Model][score-model] module, which includes the complete input data vector plus the scoring results.</span></span>
<span data-ttu-id="4b40c-162">不過，如果您偏好傳回其他內容，則可以在 **Web 服務輸出**模組之前新增其他模組。</span><span class="sxs-lookup"><span data-stu-id="4b40c-162">However, if you would prefer to return something different, then you can add additional modules before the **Web service output** module.</span></span> 

<span data-ttu-id="4b40c-163">例如，若只要傳回評分結果，而不傳回整個輸入資料向量，請新增[選取資料集中的資料行][select-columns]模組，以排除評分結果以外的所有資料行。</span><span class="sxs-lookup"><span data-stu-id="4b40c-163">For example, to return only the scoring results and not the entire vector of input data, add a [Select Columns in Dataset][select-columns] module to exclude all columns except the scoring results.</span></span> <span data-ttu-id="4b40c-164">接著，將 **Web 服務輸出**模組移到[選取資料集中的資料行][select-columns]模組的輸出。</span><span class="sxs-lookup"><span data-stu-id="4b40c-164">Then move the **Web service output** module to the output of the [Select Columns in Dataset][select-columns] module.</span></span> <span data-ttu-id="4b40c-165">實驗看起來如下：</span><span class="sxs-lookup"><span data-stu-id="4b40c-165">The experiment looks like this:</span></span>

![移動 Web 服務輸出][figure5]

### <a name="add-or-remove-additional-data-processing-modules"></a><span data-ttu-id="4b40c-167">新增或移除其他資料處理模組</span><span class="sxs-lookup"><span data-stu-id="4b40c-167">Add or remove additional data processing modules</span></span>
<span data-ttu-id="4b40c-168">如果在您的實驗中還有您知道在評分期間不需要的模組，則可以移除這些模組。</span><span class="sxs-lookup"><span data-stu-id="4b40c-168">If there are more modules in your experiment that you know will not be needed during scoring, these can be removed.</span></span> <span data-ttu-id="4b40c-169">例如，由於我們已經將 **Web 服務輸入**模組移到資料處理模組之後的某個點，因此我們可以從預測實驗中移除[清除遺漏的資料][clean-missing-data]模組。</span><span class="sxs-lookup"><span data-stu-id="4b40c-169">For example, because we moved the **Web service input** module to a point after the data processing modules, we can remove the [Clean Missing Data][clean-missing-data] module from the predictive experiment.</span></span>

<span data-ttu-id="4b40c-170">我們的預測實驗現在看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="4b40c-170">Our predictive experiment now looks like this:</span></span>

![移除額外的模組][figure6]


### <a name="add-optional-web-service-parameters"></a><span data-ttu-id="4b40c-172">新增選用的 Web 服務參數</span><span class="sxs-lookup"><span data-stu-id="4b40c-172">Add optional Web Service Parameters</span></span>
<span data-ttu-id="4b40c-173">在某些情況下，您可能需要讓 Web 服務的使用者變更存取服務時的模組行為。</span><span class="sxs-lookup"><span data-stu-id="4b40c-173">In some cases, you may want to allow the user of your web service to change the behavior of modules when the service is accessed.</span></span> <span data-ttu-id="4b40c-174">*Web 服務參數* 可讓您執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="4b40c-174">*Web Service Parameters* allow you to do this.</span></span>

<span data-ttu-id="4b40c-175">常見的範例是設定[匯入資料][import-data]模組，讓已部署之 Web 服務的使用者可以在存取 Web 服務時，指定不同的資料來源。</span><span class="sxs-lookup"><span data-stu-id="4b40c-175">A common example is setting up an [Import Data][import-data] module so the user of the deployed web service can specify a different data source when the web service is accessed.</span></span> <span data-ttu-id="4b40c-176">或者，設定[匯出資料][export-data]模組，以便能夠指定不同的目的地。</span><span class="sxs-lookup"><span data-stu-id="4b40c-176">Or configuring an [Export Data][export-data] module so that a different destination can be specified.</span></span>

<span data-ttu-id="4b40c-177">您可以定義 Web 服務參數，並使其與一個或多個模組參數產生關聯，而且您可以指定它們是必要還是選用參數。</span><span class="sxs-lookup"><span data-stu-id="4b40c-177">You can define Web Service Parameters and associate them with one or more module parameters, and you can specify whether they are required or optional.</span></span> <span data-ttu-id="4b40c-178">Web 服務的使用者會在服務受到存取時提供這些參數的值，並據此修改模組動作。</span><span class="sxs-lookup"><span data-stu-id="4b40c-178">The user of the web service provides values for these parameters when the service is accessed, and the module actions are modified accordingly.</span></span>

<span data-ttu-id="4b40c-179">如需 Web 服務參數和其用法的詳細資訊，請參閱[使用 Azure Machine Learning Web 服務參數][webserviceparameters]。</span><span class="sxs-lookup"><span data-stu-id="4b40c-179">For more information about what Web Service Parameters are and how to use them, see [Using Azure Machine Learning Web Service Parameters][webserviceparameters].</span></span>

[webserviceparameters]: machine-learning-web-service-parameters.md


## <a name="deploy-the-predictive-experiment-as-a-web-service"></a><span data-ttu-id="4b40c-180">將預測實驗部署為 Web 服務</span><span class="sxs-lookup"><span data-stu-id="4b40c-180">Deploy the predictive experiment as a web service</span></span>
<span data-ttu-id="4b40c-181">既然已經為預測實驗做好充分的準備，您可以將它當做 Azure Web 服務部署。</span><span class="sxs-lookup"><span data-stu-id="4b40c-181">Now that the predictive experiment has been sufficiently prepared, you can deploy it as an Azure web service.</span></span> <span data-ttu-id="4b40c-182">使用者可以使用 Web 服務，將料傳送到您的模型，模型就會傳回其預測。</span><span class="sxs-lookup"><span data-stu-id="4b40c-182">Using the web service, users can send data to your model and the model will return its predictions.</span></span>

<span data-ttu-id="4b40c-183">如需完整部署流程的詳細資訊，請參閱[部署 Azure Machine Learning Web 服務][deploy]</span><span class="sxs-lookup"><span data-stu-id="4b40c-183">For more information on the complete deployment process, see [Deploy an Azure Machine Learning web service][deploy]</span></span>

[deploy]: machine-learning-publish-a-machine-learning-web-service.md


<!-- Images -->
[figure1]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure1.png
[figure2]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure2.png
[figure3]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure3.png
[figure4]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure4.png
[figure5]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure5.png
[figure6]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure6.png


<!-- Module References -->
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[export-data]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/
