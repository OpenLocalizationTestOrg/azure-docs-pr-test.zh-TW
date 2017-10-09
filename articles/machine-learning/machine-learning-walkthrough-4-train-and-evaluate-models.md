---
title: "步驟 4： 來定型及評估 hello 預測分析模型 |Microsoft 文件"
description: "步驟 4 中的 hello 開發預測方案逐步解說： 定型，分數，並評估 Azure Machine Learning Studio 中的多個模型。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a><span data-ttu-id="fb794-103">逐步解說步驟 4： 來定型及評估 hello 預測分析的模型</span><span class="sxs-lookup"><span data-stu-id="fb794-103">Walkthrough Step 4: Train and evaluate hello predictive analytic models</span></span>
<span data-ttu-id="fb794-104">本主題包含 hello hello 逐步解說中，第四個步驟[開發 Azure Machine Learning 中的預測分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="fb794-104">This topic contains hello fourth step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="fb794-105">建立機器學習服務工作區</span><span class="sxs-lookup"><span data-stu-id="fb794-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="fb794-106">上傳現有資料</span><span class="sxs-lookup"><span data-stu-id="fb794-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="fb794-107">建立新實驗</span><span class="sxs-lookup"><span data-stu-id="fb794-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="fb794-108">**來定型及評估 hello 模型**</span><span class="sxs-lookup"><span data-stu-id="fb794-108">**Train and evaluate hello models**</span></span>
5. [<span data-ttu-id="fb794-109">部署 hello Web 服務</span><span class="sxs-lookup"><span data-stu-id="fb794-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="fb794-110">存取 hello Web 服務</span><span class="sxs-lookup"><span data-stu-id="fb794-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="fb794-111">建立機器學習模型中使用 Azure Machine Learning Studio hello 優點的其中一個單一的實驗中一次是 hello 能力 tootry 多個模型類型，並比較 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="fb794-111">One of hello benefits of using Azure Machine Learning Studio for creating machine learning models is hello ability tootry more than one type of model at a time in a single experiment and compare hello results.</span></span> <span data-ttu-id="fb794-112">這種類型的實驗，可協助您尋找 hello 最佳解決方案，針對您的問題。</span><span class="sxs-lookup"><span data-stu-id="fb794-112">This type of experimentation helps you find hello best solution for your problem.</span></span>

<span data-ttu-id="fb794-113">在這個逐步解說中，我們正在開發 hello 實驗中，我們將建立兩個不同類型的模型，然後比較其計分結果 toodecide 哪一個演算法我們想 toouse 我們最後的實驗中。</span><span class="sxs-lookup"><span data-stu-id="fb794-113">In hello experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results toodecide which algorithm we want toouse in our final experiment.</span></span>  

<span data-ttu-id="fb794-114">有各種不同的模型可供我們選擇。</span><span class="sxs-lookup"><span data-stu-id="fb794-114">There are various models we could choose from.</span></span> <span data-ttu-id="fb794-115">toosee hello 模型，依序展開 hello **Machine Learning** hello 模組調色盤中的節點，然後展開 **初始化模型**和其下的 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="fb794-115">toosee hello models available, expand hello **Machine Learning** node in hello module palette, and then expand **Initialize Model** and hello nodes beneath it.</span></span> <span data-ttu-id="fb794-116">基於 hello 這項實驗中，我們將選取 hello[二級支援向量機器][ two-class-support-vector-machine] (SVM) 和 hello[二級促進式決策樹][two-class-boosted-decision-tree]模組。</span><span class="sxs-lookup"><span data-stu-id="fb794-116">For hello purposes of this experiment, we'll select hello [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="fb794-117">tooget 協助以決定哪一個機器學習演算法最適合您正嘗試 toosolve hello 特定問題，請參閱[如何 toochoose 演算法為 Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md)。</span><span class="sxs-lookup"><span data-stu-id="fb794-117">tooget help deciding which Machine Learning algorithm best suits hello particular problem you're trying toosolve, see [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-hello-models"></a><span data-ttu-id="fb794-118">定型的模型 hello</span><span class="sxs-lookup"><span data-stu-id="fb794-118">Train hello models</span></span>

<span data-ttu-id="fb794-119">我們會將這兩個 hello[二級促進式決策樹][ two-class-boosted-decision-tree]模組和[二級支援向量機器][ two-class-support-vector-machine]模組在此實驗。</span><span class="sxs-lookup"><span data-stu-id="fb794-119">We'll add both hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="fb794-120">二元促進式決策樹</span><span class="sxs-lookup"><span data-stu-id="fb794-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="fb794-121">首先，接著要設定 hello 促進式決策樹模型。</span><span class="sxs-lookup"><span data-stu-id="fb794-121">First, let's set up hello boosted decision tree model.</span></span>

1. <span data-ttu-id="fb794-122">尋找 hello[二級促進式決策樹][ two-class-boosted-decision-tree] hello 模組調色盤中的模組並將它拖曳到畫布 hello。</span><span class="sxs-lookup"><span data-stu-id="fb794-122">Find hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="fb794-123">尋找 hello[定型模型][ train-model]模組，將它拖曳至 hello 畫布，然後 hello hello 輸出連接[二級促進式決策樹][ two-class-boosted-decision-tree]模組 toohello 左輸入的連接埠的 hello[定型模型][ train-model]模組。</span><span class="sxs-lookup"><span data-stu-id="fb794-123">Find hello [Train Model][train-model] module, drag it onto hello canvas, and then connect hello output of hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="fb794-124">hello[二級促進式決策樹][ two-class-boosted-decision-tree]模組初始化 hello 通用模型 」 和[定型模型][ train-model]使用定型資料tootrain hello 模型。</span><span class="sxs-lookup"><span data-stu-id="fb794-124">hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes hello generic model, and [Train Model][train-model] uses training data tootrain hello model.</span></span> 

3. <span data-ttu-id="fb794-125">Hello hello 左邊的左邊的輸出連接[執行 R 指令碼][ execute-r-script]模組 toohello 直接輸入連接埠 hello[定型模型][ train-model] （我們的模組在決定[步驟 3](machine-learning-walkthrough-3-create-new-experiment.md)來自 hello 左邊 hello 分割資料模組來定型此逐步解說 toouse hello 資料)。</span><span class="sxs-lookup"><span data-stu-id="fb794-125">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello right input port of hello [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough toouse hello data coming from hello left side of hello Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="fb794-126">我們不需要兩個 hello 輸入以及其中一個 hello 輸出的 hello[執行 R 指令碼][ execute-r-script]此實驗，因此我們可以將它們保留未附加的模組。</span><span class="sxs-lookup"><span data-stu-id="fb794-126">We don't need two of hello inputs and one of hello outputs of hello [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="fb794-127">Hello 實驗的這個部分現在看起來像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="fb794-127">This portion of hello experiment now looks something like this:</span></span>  

![Training a model][1]

<span data-ttu-id="fb794-129">現在，我們必須 tootell hello[定型模型][ train-model]我們想要 hello 模型 toopredict hello 信用風險值的模組。</span><span class="sxs-lookup"><span data-stu-id="fb794-129">Now we need tootell hello [Train Model][train-model] module that we want hello model toopredict hello Credit Risk value.</span></span>

1. <span data-ttu-id="fb794-130">選取 hello[定型模型][ train-model]模組。</span><span class="sxs-lookup"><span data-stu-id="fb794-130">Select hello [Train Model][train-model] module.</span></span> <span data-ttu-id="fb794-131">在 hello**屬性** 窗格中，按一下 **啟動資料行選取器**。</span><span class="sxs-lookup"><span data-stu-id="fb794-131">In hello **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="fb794-132">在 hello**選取單一資料行** 對話方塊中，輸入 「 信用風險"hello 下搜尋 欄位中**可用的資料行**下方，選取 「 信用風險 」，按一下 hello 向右箭號按鈕 ( **>** ) toomove 「 信用風險 」 太**選取的資料行**。</span><span class="sxs-lookup"><span data-stu-id="fb794-132">In hello **Select a single column** dialog, type "credit risk" in hello search field under **Available Columns**, select "Credit risk" below, and click hello right arrow button (**>**) toomove "Credit risk" too**Selected Columns**.</span></span> 

    ![選取 hello 定型模型 」 模組的 hello 信用風險資料行][0]

3. <span data-ttu-id="fb794-134">按一下 hello**確定**核取記號。</span><span class="sxs-lookup"><span data-stu-id="fb794-134">Click hello **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="fb794-135">二元支援向量機器</span><span class="sxs-lookup"><span data-stu-id="fb794-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="fb794-136">接下來，我們設定 hello SVM 模型。</span><span class="sxs-lookup"><span data-stu-id="fb794-136">Next, we set up hello SVM model.</span></span>  

<span data-ttu-id="fb794-137">首先，簡單說明一下 SVM。</span><span class="sxs-lookup"><span data-stu-id="fb794-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="fb794-138">強化的決策樹適合處理任何類型的特性。</span><span class="sxs-lookup"><span data-stu-id="fb794-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="fb794-139">不過，由於 hello SVM 模組會產生線性分類器，hello 模型，它會產生有 hello 最佳測試錯誤時數字的所有功能都具有 hello 相同的標尺。</span><span class="sxs-lookup"><span data-stu-id="fb794-139">However, since hello SVM module generates a linear classifier, hello model that it generates has hello best test error when all numeric features have hello same scale.</span></span> <span data-ttu-id="fb794-140">tooconvert 全都是數字相同擴充功能 toohello，我們使用 「 Tanh 」 轉換 (以 hello[標準化資料][ normalize-data]模組)。</span><span class="sxs-lookup"><span data-stu-id="fb794-140">tooconvert all numeric features toohello same scale, we use a "Tanh" transformation (with hello [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="fb794-141">這會將我們的數字轉換成 hello [0，1] 範圍中。</span><span class="sxs-lookup"><span data-stu-id="fb794-141">This transforms our numbers into hello [0,1] range.</span></span> <span data-ttu-id="fb794-142">hello SVM 模組將轉換字串功能 toocategorical 功能，然後 toobinary 0/1 功能，因此我們不需要 toomanually 轉換字串的功能。</span><span class="sxs-lookup"><span data-stu-id="fb794-142">hello SVM module converts string features toocategorical features and then toobinary 0/1 features, so we don't need toomanually transform string features.</span></span> <span data-ttu-id="fb794-143">此外，我們不希望 tootransform hello 信用風險資料行 （21）： 它是數值，但它是我們要定型的 hello 值 hello 模型 toopredict，因此我們需要 tooleave 單獨它。</span><span class="sxs-lookup"><span data-stu-id="fb794-143">Also, we don't want tootransform hello Credit Risk column (column 21) - it's numeric, but it's hello value we're training hello model toopredict, so we need tooleave it alone.</span></span>  

<span data-ttu-id="fb794-144">tooset hello SVM 模型，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="fb794-144">tooset up hello SVM model, do hello following:</span></span>

1. <span data-ttu-id="fb794-145">尋找 hello[二級支援向量機器][ two-class-support-vector-machine] hello 模組調色盤中的模組並將它拖曳到畫布 hello。</span><span class="sxs-lookup"><span data-stu-id="fb794-145">Find hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="fb794-146">以滑鼠右鍵按一下 hello[定型模型][ train-model]模組中，選取**複製**，然後以滑鼠右鍵按一下 hello 畫布，然後選取**貼上**。</span><span class="sxs-lookup"><span data-stu-id="fb794-146">Right-click hello [Train Model][train-model] module, select **Copy**, and then right-click hello canvas and select **Paste**.</span></span> <span data-ttu-id="fb794-147">hello 副本 hello[定型模型][ train-model]模組有 hello 相同的資料行選取項目為原始的 hello。</span><span class="sxs-lookup"><span data-stu-id="fb794-147">hello copy of hello [Train Model][train-model] module has hello same column selection as hello original.</span></span>

3. <span data-ttu-id="fb794-148">Hello hello 輸出連接[二級支援向量機器][ two-class-support-vector-machine]模組 toohello 會保留第二個輸入連接埠的 hello[定型模型][ train-model]模組。</span><span class="sxs-lookup"><span data-stu-id="fb794-148">Connect hello output of hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module toohello left input port of hello second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="fb794-149">尋找 hello[標準化資料][ normalize-data]模組並將它拖曳到畫布 hello。</span><span class="sxs-lookup"><span data-stu-id="fb794-149">Find hello [Normalize Data][normalize-data] module and drag it onto hello canvas.</span></span>

5. <span data-ttu-id="fb794-150">Hello hello 左邊的左邊的輸出連接[執行 R 指令碼][ execute-r-script]模組 toohello 輸入，此模組 （請注意模組 hello 輸出連接埠可能會比另一個模組的連接的 toomore）。</span><span class="sxs-lookup"><span data-stu-id="fb794-150">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello input of this module (notice that hello output port of a module may be connected toomore than one other module).</span></span>

6. <span data-ttu-id="fb794-151">連接保留 hello 輸出連接埠的 hello[標準化資料][ normalize-data]右模組 toohello 第二個輸入連接埠 hello[定型模型][ train-model]模組。</span><span class="sxs-lookup"><span data-stu-id="fb794-151">Connect hello left output port of hello [Normalize Data][normalize-data] module toohello right input port of hello second [Train Model][train-model] module.</span></span>

<span data-ttu-id="fb794-152">實驗的這部分目前看起來如下：</span><span class="sxs-lookup"><span data-stu-id="fb794-152">This portion of our experiment should now look something like this:</span></span>  

![第二個模型的定型 hello][2]  

<span data-ttu-id="fb794-154">現在設定 hello[標準化資料][ normalize-data]模組：</span><span class="sxs-lookup"><span data-stu-id="fb794-154">Now configure hello [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="fb794-155">按一下 tooselect hello[標準化資料][ normalize-data]模組。</span><span class="sxs-lookup"><span data-stu-id="fb794-155">Click tooselect hello [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="fb794-156">在 hello**屬性**窗格中，選取**Tanh** hello**轉換方法**參數。</span><span class="sxs-lookup"><span data-stu-id="fb794-156">In hello **Properties** pane, select **Tanh** for hello **Transformation method** parameter.</span></span>

2. <span data-ttu-id="fb794-157">按一下**啟動資料行選取器**，選取 「 沒有資料行 」**使用 Begin With**，選取**Include** hello 第一個下拉式清單中選取**資料行類型**在 hello 第二個下拉式清單中，然後選取**數值**hello 第三個下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="fb794-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in hello first dropdown, select **column type** in hello second dropdown, and select **Numeric** in hello third dropdown.</span></span> <span data-ttu-id="fb794-158">這會指定所有 hello 數值資料行 （與唯一的數字） 會都轉換。</span><span class="sxs-lookup"><span data-stu-id="fb794-158">This specifies that all hello numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="fb794-159">按一下 hello 加號 （+） toohello 此資料列的權限-這會建立一個資料列的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="fb794-159">Click hello plus sign (+) toohello right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="fb794-160">選取**排除**hello 第一個下拉式清單中選取**資料行名稱**在 hello 第二個下拉式清單中，然後輸入 hello 文字欄位中的 「 信用風險 」。</span><span class="sxs-lookup"><span data-stu-id="fb794-160">Select **Exclude** in hello first dropdown, select **column names** in hello second dropdown, and enter "Credit risk" in hello text field.</span></span> <span data-ttu-id="fb794-161">這會指定應該忽略該 hello 信用風險資料行 （我們需要的 toodo 這因為此資料行是數值，所以會轉換如果我們未排除它）。</span><span class="sxs-lookup"><span data-stu-id="fb794-161">This specifies that hello Credit Risk column should be ignored (we need toodo this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="fb794-162">按一下 hello**確定**核取記號。</span><span class="sxs-lookup"><span data-stu-id="fb794-162">Click hello **OK** check mark.</span></span>  

    ![選取的資料行 hello 標準化資料模組][5]

<span data-ttu-id="fb794-164">hello[標準化資料][ normalize-data]模組現在會設定 tooperform Tanh 轉換 hello 信用風險資料行以外的所有數值資料行上。</span><span class="sxs-lookup"><span data-stu-id="fb794-164">hello [Normalize Data][normalize-data] module is now set tooperform a Tanh transformation on all numeric columns except for hello Credit Risk column.</span></span>  

## <a name="score-and-evaluate-hello-models"></a><span data-ttu-id="fb794-165">計分，並評估 hello 模型</span><span class="sxs-lookup"><span data-stu-id="fb794-165">Score and evaluate hello models</span></span>

<span data-ttu-id="fb794-166">我們使用測試資料的已隔開 hello hello[分割資料][ split]模組 tooscore 我們定型的模型。</span><span class="sxs-lookup"><span data-stu-id="fb794-166">We use hello testing data that was separated out by hello [Split Data][split] module tooscore our trained models.</span></span> <span data-ttu-id="fb794-167">然後，我們可以比較 hello 結果的 hello 兩個模型 toosee 產生更好的結果。</span><span class="sxs-lookup"><span data-stu-id="fb794-167">We can then compare hello results of hello two models toosee which generated better results.</span></span>  

### <a name="add-hello-score-model-modules"></a><span data-ttu-id="fb794-168">加入 hello 分數模型模組</span><span class="sxs-lookup"><span data-stu-id="fb794-168">Add hello Score Model modules</span></span>

1. <span data-ttu-id="fb794-169">尋找 hello[計分模型][ score-model]模組並將它拖曳到畫布 hello。</span><span class="sxs-lookup"><span data-stu-id="fb794-169">Find hello [Score Model][score-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="fb794-170">連接 hello[定型模型][ train-model]模組已連接 toohello[二級促進式決策樹][ two-class-boosted-decision-tree]模組 toohello 左方的輸入連接埠 hello[計分模型][ score-model]模組。</span><span class="sxs-lookup"><span data-stu-id="fb794-170">Connect hello [Train Model][train-model] module that's connected toohello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="fb794-171">連接 hello 右邊[執行 R 指令碼][ execute-r-script]模組 （我們測試的資料） toohello 直接輸入連接埠 hello[計分模型][ score-model]模組。</span><span class="sxs-lookup"><span data-stu-id="fb794-171">Connect hello right [Execute R Script][execute-r-script] module (our testing data) toohello right input port of hello [Score Model][score-model] module.</span></span>

    ![已連接評分模型模組][6]
   
   <span data-ttu-id="fb794-173">hello[計分模型][ score-model]模組現在能夠利用 hello 信用資訊從測試資料，執行透過 hello 模型 hello 和比較 hello 預測 hello 模型會產生以實際的 hello 信用風險hello 測試資料中的資料行。</span><span class="sxs-lookup"><span data-stu-id="fb794-173">hello [Score Model][score-model] module can now take hello credit information from hello testing data, run it through hello model, and compare hello predictions hello model generates with hello actual credit risk column in hello testing data.</span></span>

4. <span data-ttu-id="fb794-174">複製並貼上 hello[計分模型][ score-model]模組 toocreate 第二個副本。</span><span class="sxs-lookup"><span data-stu-id="fb794-174">Copy and paste hello [Score Model][score-model] module toocreate a second copy.</span></span>

5. <span data-ttu-id="fb794-175">Hello 輸出 hello SVM 模型連接 (也就是 hello 輸出連接埠的 hello[定型模型][ train-model]連接 toohello 的模組[二級支援向量機器][two-class-support-vector-machine]模組) toohello 第二個輸入連接埠 hello[計分模型][ score-model]模組。</span><span class="sxs-lookup"><span data-stu-id="fb794-175">Connect hello output of hello SVM model (that is, hello output port of hello [Train Model][train-model] module that's connected toohello [Two-Class Support Vector Machine][two-class-support-vector-machine] module) toohello input port of hello second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="fb794-176">Hello SVM 模型，我們有 toodo hello 相同轉換 toohello 測試資料，如同 toohello 定型資料。</span><span class="sxs-lookup"><span data-stu-id="fb794-176">For hello SVM model, we have toodo hello same transformation toohello test data as we did toohello training data.</span></span> <span data-ttu-id="fb794-177">因此複製並貼上 hello[標準化資料][ normalize-data]模組 toocreate 第二個複本並將它連接 toohello 右邊[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="fb794-177">So copy and paste hello [Normalize Data][normalize-data] module toocreate a second copy and connect it toohello right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="fb794-178">第二個連接的 hello hello 左的輸出[標準化資料][ normalize-data]右模組 toohello 第二個輸入連接埠 hello[計分模型][ score-model]模組。</span><span class="sxs-lookup"><span data-stu-id="fb794-178">Connect hello left output of hello second [Normalize Data][normalize-data] module toohello right input port of hello second [Score Model][score-model] module.</span></span>

    ![已連接兩個評分模型模組][7]

### <a name="add-hello-evaluate-model-module"></a><span data-ttu-id="fb794-180">新增 hello 評估模型模組</span><span class="sxs-lookup"><span data-stu-id="fb794-180">Add hello Evaluate Model module</span></span>

<span data-ttu-id="fb794-181">tooevaluate hello 兩個計分結果並加以比較，我們使用[評估模型][ evaluate-model]模組。</span><span class="sxs-lookup"><span data-stu-id="fb794-181">tooevaluate hello two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="fb794-182">尋找 hello[評估模型][ evaluate-model]模組並將它拖曳到畫布 hello。</span><span class="sxs-lookup"><span data-stu-id="fb794-182">Find hello [Evaluate Model][evaluate-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="fb794-183">連接 hello hello 輸出連接埠[計分模型][ score-model] hello 與相關聯的模組促進式決策樹模型 toohello 左輸入連接埠 hello[評估模型][evaluate-model]模組。</span><span class="sxs-lookup"><span data-stu-id="fb794-183">Connect hello output port of hello [Score Model][score-model] module associated with hello boosted decision tree model toohello left input port of hello [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="fb794-184">連接其他 hello[計分模型][ score-model]模組 toohello 直接輸入連接埠。</span><span class="sxs-lookup"><span data-stu-id="fb794-184">Connect hello other [Score Model][score-model] module toohello right input port.</span></span>  

    ![已連接評估模型模組][8]

### <a name="run-hello-experiment-and-check-hello-results"></a><span data-ttu-id="fb794-186">執行 hello 實驗，並檢查 hello 結果</span><span class="sxs-lookup"><span data-stu-id="fb794-186">Run hello experiment and check hello results</span></span>

<span data-ttu-id="fb794-187">toorun hello 實驗中，按一下 hello**執行**hello 畫布下方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="fb794-187">toorun hello experiment, click hello **RUN** button below hello canvas.</span></span> <span data-ttu-id="fb794-188">可能需要數分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="fb794-188">It may take a few minutes.</span></span> <span data-ttu-id="fb794-189">旋轉指標上每個模組會顯示正在執行，，和綠色的核取記號然後才顯示完成 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="fb794-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when hello module is finished.</span></span> <span data-ttu-id="fb794-190">當所有 hello 模組都有核取記號時，hello 實驗已經完成執行。</span><span class="sxs-lookup"><span data-stu-id="fb794-190">When all hello modules have a check mark, hello experiment has finished running.</span></span>

<span data-ttu-id="fb794-191">hello 實驗現在看起來應該像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="fb794-191">hello experiment should now look something like this:</span></span>  

![Evaluating both models][3]

<span data-ttu-id="fb794-193">toocheck hello 結果中按一下輸出連接埠 hello hello[評估模型][ evaluate-model]模組，然後選取**視覺化**。</span><span class="sxs-lookup"><span data-stu-id="fb794-193">toocheck hello results, click hello output port of hello [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="fb794-194">hello[評估模型][ evaluate-model]模組會產生一對曲線和 toocompare hello 結果的 hello 兩個計分模型可讓您的度量。</span><span class="sxs-lookup"><span data-stu-id="fb794-194">hello [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you toocompare hello results of hello two scored models.</span></span> <span data-ttu-id="fb794-195">您可以檢視為接收者運算子特性 (ROC) 曲線、 重新叫用精確度/曲線或增益曲線 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="fb794-195">You can view hello results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="fb794-196">顯示的其他資料包括混淆矩陣、 hello 曲線 (AUC)，底下的 hello 區域的累計值和其他度量。</span><span class="sxs-lookup"><span data-stu-id="fb794-196">Additional data displayed includes a confusion matrix, cumulative values for hello area under hello curve (AUC), and other metrics.</span></span> <span data-ttu-id="fb794-197">您可以向左或向右移動的 hello 滑桿來變更 hello 臨界值，並查看它如何影響 hello 組度量。</span><span class="sxs-lookup"><span data-stu-id="fb794-197">You can change hello threshold value by moving hello slider left or right and see how it affects hello set of metrics.</span></span>  

<span data-ttu-id="fb794-198">toohello hello 圖形的右邊按一下**評分資料集**或**計分資料集 toocompare** toohighlight hello 關聯的曲線和 toodisplay hello 相關聯的度量下方。</span><span class="sxs-lookup"><span data-stu-id="fb794-198">toohello right of hello graph, click **Scored dataset** or **Scored dataset toocompare** toohighlight hello associated curve and toodisplay hello associated metrics below.</span></span> <span data-ttu-id="fb794-199">在 hello hello 曲線圖例，"評分資料集 」 對應 toohello 左輸入的連接埠的 hello[評估模型][ evaluate-model]模組-在此案例中，這是 hello 促進式決策樹模型。</span><span class="sxs-lookup"><span data-stu-id="fb794-199">In hello legend for hello curves, "Scored dataset" corresponds toohello left input port of hello [Evaluate Model][evaluate-model] module - in our case, this is hello boosted decision tree model.</span></span> <span data-ttu-id="fb794-200">「 計分資料集 toocompare 」 對應 toohello 右側輸入連接埠-hello SVM 模型，在我們的案例。</span><span class="sxs-lookup"><span data-stu-id="fb794-200">"Scored dataset toocompare" corresponds toohello right input port - hello SVM model in our case.</span></span> <span data-ttu-id="fb794-201">當您按一下其中一個這些標籤時，針對該模型的 hello 曲線會反白顯示，並且顯示 hello 對應度量，hello 下列圖片所示。</span><span class="sxs-lookup"><span data-stu-id="fb794-201">When you click one of these labels, hello curve for that model is highlighted and hello corresponding metrics are displayed, as shown in hello following graphic.</span></span>  

![ROC curves for models][4]

<span data-ttu-id="fb794-203">您可以藉由檢查這些值，決定哪一個模型是最接近 toogiving hello 想要的結果。</span><span class="sxs-lookup"><span data-stu-id="fb794-203">By examining these values, you can decide which model is closest toogiving you hello results you're looking for.</span></span> <span data-ttu-id="fb794-204">您可以返回並變更 hello 不同模型中的參數值逐一查看您的經驗。</span><span class="sxs-lookup"><span data-stu-id="fb794-204">You can go back and iterate on your experiment by changing parameter values in hello different models.</span></span> 

<span data-ttu-id="fb794-205">hello 科學和解譯這些結果和微調 hello 模型效能的封面是本逐步解說的 hello 範圍外。</span><span class="sxs-lookup"><span data-stu-id="fb794-205">hello science and art of interpreting these results and tuning hello model performance is outside hello scope of this walkthrough.</span></span> <span data-ttu-id="fb794-206">如需額外說明，您可能會讀取下列發行項的 hello:</span><span class="sxs-lookup"><span data-stu-id="fb794-206">For additional help, you might read hello following articles:</span></span>
- [<span data-ttu-id="fb794-207">Tooevaluate 建立 Azure Machine Learning 中的效能的模型</span><span class="sxs-lookup"><span data-stu-id="fb794-207">How tooevaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="fb794-208">Azure Machine Learning 中選擇您的演算法參數 toooptimize</span><span class="sxs-lookup"><span data-stu-id="fb794-208">Choose parameters toooptimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="fb794-209">在 Azure Machine Learning 中解讀模型結果</span><span class="sxs-lookup"><span data-stu-id="fb794-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="fb794-210">每次執行 hello 實驗的該反覆項目記錄會保留在 hello 執行歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="fb794-210">Each time you run hello experiment a record of that iteration is kept in hello Run History.</span></span> <span data-ttu-id="fb794-211">您可以檢視這些反覆項目，並傳回 tooany 項目，依序按一下**檢視執行記錄**hello 畫布下方。</span><span class="sxs-lookup"><span data-stu-id="fb794-211">You can view these iterations, and return tooany of them, by clicking **VIEW RUN HISTORY** below hello canvas.</span></span> <span data-ttu-id="fb794-212">您也可以按一下**先前執行**在 hello**屬性**窗格 tooreturn toohello 前面的反覆項目 hello 其中一個已開啟。</span><span class="sxs-lookup"><span data-stu-id="fb794-212">You can also click **Prior Run** in hello **Properties** pane tooreturn toohello iteration immediately preceding hello one you have open.</span></span>
> 
> <span data-ttu-id="fb794-213">您可以建立一份實驗任何反覆項目，依序按一下**SAVE AS** hello 畫布下方。</span><span class="sxs-lookup"><span data-stu-id="fb794-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below hello canvas.</span></span> 
> <span data-ttu-id="fb794-214">使用 hello 實驗**摘要**和**描述**屬性 tookeep 記錄您已嘗試在您實驗反覆項目。</span><span class="sxs-lookup"><span data-stu-id="fb794-214">Use hello experiment's **Summary** and **Description** properties tookeep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="fb794-215">如需詳細資訊，請參閱 [在 Azure Machine Learning Studio 中管理實驗逐一查看](machine-learning-manage-experiment-iterations.md)。</span><span class="sxs-lookup"><span data-stu-id="fb794-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="fb794-216">**下一步:[部署 hello web 服務](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="fb794-216">**Next: [Deploy hello web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
