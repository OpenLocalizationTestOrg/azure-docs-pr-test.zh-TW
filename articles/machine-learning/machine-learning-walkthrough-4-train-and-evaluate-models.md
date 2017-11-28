---
title: "步驟 4：訓練和評估預測分析模型 | Microsoft Docs"
description: "開發預測解決方案逐步解說的步驟 4：在 Azure Machine Learning Studio 中定型、計分和評估多個模型。"
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
ms.openlocfilehash: 58d46dd1464ec0a3fc9639f78d4429e0e778c2bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-the-predictive-analytic-models"></a><span data-ttu-id="7787e-103">逐步解說步驟 4：定型和評估預測分析模型</span><span class="sxs-lookup"><span data-stu-id="7787e-103">Walkthrough Step 4: Train and evaluate the predictive analytic models</span></span>
<span data-ttu-id="7787e-104">此主題包含[在 Azure Machine Learning 中開發預測性分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)逐步解說的第四個步驟</span><span class="sxs-lookup"><span data-stu-id="7787e-104">This topic contains the fourth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="7787e-105">建立機器學習服務工作區</span><span class="sxs-lookup"><span data-stu-id="7787e-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="7787e-106">上傳現有資料</span><span class="sxs-lookup"><span data-stu-id="7787e-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="7787e-107">建立新實驗</span><span class="sxs-lookup"><span data-stu-id="7787e-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="7787e-108">**訓練及評估模型**</span><span class="sxs-lookup"><span data-stu-id="7787e-108">**Train and evaluate the models**</span></span>
5. [<span data-ttu-id="7787e-109">部署 Web 服務</span><span class="sxs-lookup"><span data-stu-id="7787e-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="7787e-110">存取 Web 服務</span><span class="sxs-lookup"><span data-stu-id="7787e-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="7787e-111">使用 Azure Machine Learning Studio 來建立機器學習服務模型的優點之一，是能夠在單一實驗中一次嘗試多個模型類型，並比較結果。</span><span class="sxs-lookup"><span data-stu-id="7787e-111">One of the benefits of using Azure Machine Learning Studio for creating machine learning models is the ability to try more than one type of model at a time in a single experiment and compare the results.</span></span> <span data-ttu-id="7787e-112">這類實驗可協助您針對問題找到最佳解決方案。</span><span class="sxs-lookup"><span data-stu-id="7787e-112">This type of experimentation helps you find the best solution for your problem.</span></span>

<span data-ttu-id="7787e-113">在我們正於這個逐步解說中開發的實驗內，將會建立兩種不同的模型，然後比較其計分結果，以決定要用於最終實驗的演算法。</span><span class="sxs-lookup"><span data-stu-id="7787e-113">In the experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results to decide which algorithm we want to use in our final experiment.</span></span>  

<span data-ttu-id="7787e-114">有各種不同的模型可供我們選擇。</span><span class="sxs-lookup"><span data-stu-id="7787e-114">There are various models we could choose from.</span></span> <span data-ttu-id="7787e-115">若要查看可用的模型，請在模組選擇區展開 [機器學習] 節點，然後展開 [初始化模型]，再選擇其下方的節點。</span><span class="sxs-lookup"><span data-stu-id="7787e-115">To see the models available, expand the **Machine Learning** node in the module palette, and then expand **Initialize Model** and the nodes beneath it.</span></span> <span data-ttu-id="7787e-116">基於本實驗的目的，我們將選取[二元支援向量機器][two-class-support-vector-machine] (SVM) 和[二元促進式決策樹][two-class-boosted-decision-tree]模組。</span><span class="sxs-lookup"><span data-stu-id="7787e-116">For the purposes of this experiment, we'll select the [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="7787e-117">如需取得說明以決定哪一種機器學習服務演算法最適合您正在嘗試解決的特定問題，請參閱 [如何選擇 Microsoft Azure Machine Learning 的演算法](machine-learning-algorithm-choice.md)。</span><span class="sxs-lookup"><span data-stu-id="7787e-117">To get help deciding which Machine Learning algorithm best suits the particular problem you're trying to solve, see [How to choose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-the-models"></a><span data-ttu-id="7787e-118">訓練模型</span><span class="sxs-lookup"><span data-stu-id="7787e-118">Train the models</span></span>

<span data-ttu-id="7787e-119">我們將在此實驗中新增[二元促進式決策樹][two-class-boosted-decision-tree]模組和[二元支援向量機器][two-class-support-vector-machine]模組。</span><span class="sxs-lookup"><span data-stu-id="7787e-119">We'll add both the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="7787e-120">二元促進式決策樹</span><span class="sxs-lookup"><span data-stu-id="7787e-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="7787e-121">首先，讓我們設定促進式決策樹模型。</span><span class="sxs-lookup"><span data-stu-id="7787e-121">First, let's set up the boosted decision tree model.</span></span>

1. <span data-ttu-id="7787e-122">在模組選擇區中找到 [[二元促進式決策樹]][two-class-boosted-decision-tree] 模組，將其拖曳到畫布上。</span><span class="sxs-lookup"><span data-stu-id="7787e-122">Find the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in the module palette and drag it onto the canvas.</span></span>

2. <span data-ttu-id="7787e-123">找到 [[訓練模型]][train-model] 模組，將它拖曳到畫布上，然後將[ [二元促進式決策樹]][two-class-boosted-decision-tree] 模組的輸出連接到 [[訓練模型]][train-model] 模組的左側輸入連接埠。</span><span class="sxs-lookup"><span data-stu-id="7787e-123">Find the [Train Model][train-model] module, drag it onto the canvas, and then connect the output of the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="7787e-124">[[二元促進式決策樹]][two-class-boosted-decision-tree] 模組會將一般模組初始化，而 [[訓練模型]][train-model] 則會使用訓練資料來訓練模型。</span><span class="sxs-lookup"><span data-stu-id="7787e-124">The [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes the generic model, and [Train Model][train-model] uses training data to train the model.</span></span> 

3. <span data-ttu-id="7787e-125">將左側 [[執行 R 指令碼]][execute-r-script] 模組的左輸出連接到 [[訓練模型]][train-model] 模組的右側輸入連接埠 (我們在本逐步解說[步驟 3](machine-learning-walkthrough-3-create-new-experiment.md)決定的做法，使用「分割資料」模組左側所傳來的資料用於訓練)。</span><span class="sxs-lookup"><span data-stu-id="7787e-125">Connect the left output of the left [Execute R Script][execute-r-script] module to the right input port of the [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough to use the data coming from the left side of the Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="7787e-126">在這項實驗中，我們不需要 [[執行 R 指令碼]][execute-r-script] 模組的兩個輸入和一個輸出，因此可以讓它們保持未連接。</span><span class="sxs-lookup"><span data-stu-id="7787e-126">We don't need two of the inputs and one of the outputs of the [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="7787e-127">實驗的這部分目前看起來如下：</span><span class="sxs-lookup"><span data-stu-id="7787e-127">This portion of the experiment now looks something like this:</span></span>  

![Training a model][1]

<span data-ttu-id="7787e-129">現在我們要告訴 [[訓練模型]][train-model] 模組，我們要讓模型預測信用風險值。</span><span class="sxs-lookup"><span data-stu-id="7787e-129">Now we need to tell the [Train Model][train-model] module that we want the model to predict the Credit Risk value.</span></span>

1. <span data-ttu-id="7787e-130">選取 [[訓練模型]][train-model] 模組。</span><span class="sxs-lookup"><span data-stu-id="7787e-130">Select the [Train Model][train-model] module.</span></span> <span data-ttu-id="7787e-131">按一下 [屬性] 窗格中的 [啟動資料行選取器]。</span><span class="sxs-lookup"><span data-stu-id="7787e-131">In the **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="7787e-132">在 [選取單一資料行] 對話方塊中，在 [可用的資料行] 下的 [搜尋] 欄位中輸入「信用風險」，然後選取下方的 [信用風險]，按一下向右箭號按鈕 (**>**) 將 [信用風險] 移至 [選取的資料行]。</span><span class="sxs-lookup"><span data-stu-id="7787e-132">In the **Select a single column** dialog, type "credit risk" in the search field under **Available Columns**, select "Credit risk" below, and click the right arrow button (**>**) to move "Credit risk" to **Selected Columns**.</span></span> 

    ![為訓練模型模組選取信用風險資料行][0]

3. <span data-ttu-id="7787e-134">按一下 [確定] \(打勾記號)。</span><span class="sxs-lookup"><span data-stu-id="7787e-134">Click the **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="7787e-135">二元支援向量機器</span><span class="sxs-lookup"><span data-stu-id="7787e-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="7787e-136">接下來，我們設定 SVM 模型。</span><span class="sxs-lookup"><span data-stu-id="7787e-136">Next, we set up the SVM model.</span></span>  

<span data-ttu-id="7787e-137">首先，簡單說明一下 SVM。</span><span class="sxs-lookup"><span data-stu-id="7787e-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="7787e-138">強化的決策樹適合處理任何類型的特性。</span><span class="sxs-lookup"><span data-stu-id="7787e-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="7787e-139">不過，因為 SVM 模組會產生線性分類器，而它所產生的模型在所有數值特性都有相同的尺度時，將具有最佳檢定誤差。</span><span class="sxs-lookup"><span data-stu-id="7787e-139">However, since the SVM module generates a linear classifier, the model that it generates has the best test error when all numeric features have the same scale.</span></span> <span data-ttu-id="7787e-140">為了將所有數值特徵轉換成相同的尺度，我們使用 Tanh 轉換 (搭配[標準化資料][normalize-data]模組)。</span><span class="sxs-lookup"><span data-stu-id="7787e-140">To convert all numeric features to the same scale, we use a "Tanh" transformation (with the [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="7787e-141">這會將我們的數字轉換到 [0,1] 範圍內。</span><span class="sxs-lookup"><span data-stu-id="7787e-141">This transforms our numbers into the [0,1] range.</span></span> <span data-ttu-id="7787e-142">SVM 模組會將字串特徵轉換為類別特性，再轉換為二進位 0/1 特徵，因此我們無須手動轉換字串特徵。</span><span class="sxs-lookup"><span data-stu-id="7787e-142">The SVM module converts string features to categorical features and then to binary 0/1 features, so we don't need to manually transform string features.</span></span> <span data-ttu-id="7787e-143">此外，我們不想要轉換 [信用風險] 資料行 (資料行 21) - 它是數值，但這是我們定型模型來預測的值，因此必須維持原狀。</span><span class="sxs-lookup"><span data-stu-id="7787e-143">Also, we don't want to transform the Credit Risk column (column 21) - it's numeric, but it's the value we're training the model to predict, so we need to leave it alone.</span></span>  

<span data-ttu-id="7787e-144">若要設定 SVM 模型，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="7787e-144">To set up the SVM model, do the following:</span></span>

1. <span data-ttu-id="7787e-145">在模組選擇區中找到 [[二元支援向量機器]][two-class-support-vector-machine] 模組，將它推曳到畫布上。</span><span class="sxs-lookup"><span data-stu-id="7787e-145">Find the [Two-Class Support Vector Machine][two-class-support-vector-machine] module in the module palette and drag it onto the canvas.</span></span>

2. <span data-ttu-id="7787e-146">以滑鼠右鍵按一下 [[訓練模型]][train-model] 模組，選取 [複製]，然後以滑鼠右鍵按一下畫布並選取 [貼上]。</span><span class="sxs-lookup"><span data-stu-id="7787e-146">Right-click the [Train Model][train-model] module, select **Copy**, and then right-click the canvas and select **Paste**.</span></span> <span data-ttu-id="7787e-147">[[訓練模型]][train-model] 模組複本的資料行選擇與原始模組相同。</span><span class="sxs-lookup"><span data-stu-id="7787e-147">The copy of the [Train Model][train-model] module has the same column selection as the original.</span></span>

3. <span data-ttu-id="7787e-148">將 [[二元支援向量機器]][two-class-support-vector-machine] 模組的輸出連接到第二個 [[訓練模型]][train-model] 模組的左側輸入連接埠。</span><span class="sxs-lookup"><span data-stu-id="7787e-148">Connect the output of the [Two-Class Support Vector Machine][two-class-support-vector-machine] module to the left input port of the second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="7787e-149">找到 [[標準化資料]][normalize-data] 模組，將其拖曳到畫布上。</span><span class="sxs-lookup"><span data-stu-id="7787e-149">Find the [Normalize Data][normalize-data] module and drag it onto the canvas.</span></span>

5. <span data-ttu-id="7787e-150">將左側 [[執行 R 指令碼]][execute-r-script] 模組的左側輸出連接到此模組的輸出 (請注意，模組的輸出連接埠可能連接到多個其他模組)。</span><span class="sxs-lookup"><span data-stu-id="7787e-150">Connect the left output of the left [Execute R Script][execute-r-script] module to the input of this module (notice that the output port of a module may be connected to more than one other module).</span></span>

6. <span data-ttu-id="7787e-151">將 [[標準化資料]][normalize-data] 模組的左側輸出連接埠連接到第二個 [[訓練模型]][train-model] 模組的右側輸入連接埠。</span><span class="sxs-lookup"><span data-stu-id="7787e-151">Connect the left output port of the [Normalize Data][normalize-data] module to the right input port of the second [Train Model][train-model] module.</span></span>

<span data-ttu-id="7787e-152">實驗的這部分目前看起來如下：</span><span class="sxs-lookup"><span data-stu-id="7787e-152">This portion of our experiment should now look something like this:</span></span>  

![Training the second model][2]  

<span data-ttu-id="7787e-154">現在，設定 [[標準化資料]][normalize-data] 模組︰</span><span class="sxs-lookup"><span data-stu-id="7787e-154">Now configure the [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="7787e-155">按一下以選取 [[標準化資料]][normalize-data] 模組。</span><span class="sxs-lookup"><span data-stu-id="7787e-155">Click to select the [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="7787e-156">在 [屬性] 窗格中，選取 [Tanh] 做為 [轉換方法] 參數。</span><span class="sxs-lookup"><span data-stu-id="7787e-156">In the **Properties** pane, select **Tanh** for the **Transformation method** parameter.</span></span>

2. <span data-ttu-id="7787e-157">按一下 [啟動資料行選取器]，選取 [開始於] 的 [無資料行]，在第一個下拉式清單中選取 [包含]，在第二個下拉式清單中選取 [資料行類型]，然後在第三個下拉式清單中選取 [數值]。</span><span class="sxs-lookup"><span data-stu-id="7787e-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in the first dropdown, select **column type** in the second dropdown, and select **Numeric** in the third dropdown.</span></span> <span data-ttu-id="7787e-158">這樣會指定轉換所有數值資料行 (且僅限數值)。</span><span class="sxs-lookup"><span data-stu-id="7787e-158">This specifies that all the numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="7787e-159">按一下此資料列右側的加號 (+) - 這會建立一排下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="7787e-159">Click the plus sign (+) to the right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="7787e-160">在第一個下拉式清單中選取 [排除]，在第二個下拉式清單中選取 [資料行名稱]，然後在文字欄位中輸入「信用風險」。</span><span class="sxs-lookup"><span data-stu-id="7787e-160">Select **Exclude** in the first dropdown, select **column names** in the second dropdown, and enter "Credit risk" in the text field.</span></span> <span data-ttu-id="7787e-161">這會指定應忽略 [信用風險] 資料行 (需要這麼做是因為此資料行為數值，如未排除，它會被轉換)。</span><span class="sxs-lookup"><span data-stu-id="7787e-161">This specifies that the Credit Risk column should be ignored (we need to do this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="7787e-162">按一下 [確定] \(打勾記號)。</span><span class="sxs-lookup"><span data-stu-id="7787e-162">Click the **OK** check mark.</span></span>  

    ![選取標準化資料模組的資料行][5]

<span data-ttu-id="7787e-164">[[標準化資料]][normalize-data] 模組現在已設定為在所有數值資料行上執行 Tanh 轉換 ([信用風險] 資料行除外)。</span><span class="sxs-lookup"><span data-stu-id="7787e-164">The [Normalize Data][normalize-data] module is now set to perform a Tanh transformation on all numeric columns except for the Credit Risk column.</span></span>  

## <a name="score-and-evaluate-the-models"></a><span data-ttu-id="7787e-165">計分及評估模型</span><span class="sxs-lookup"><span data-stu-id="7787e-165">Score and evaluate the models</span></span>

<span data-ttu-id="7787e-166">我們將使用由[[資料分割]][split] 模組所分開的測試資料，給我們訓練的模型評分。</span><span class="sxs-lookup"><span data-stu-id="7787e-166">We use the testing data that was separated out by the [Split Data][split] module to score our trained models.</span></span> <span data-ttu-id="7787e-167">然後，我們就可以比較兩個模型的結果，了解何者產生的結果較佳。</span><span class="sxs-lookup"><span data-stu-id="7787e-167">We can then compare the results of the two models to see which generated better results.</span></span>  

### <a name="add-the-score-model-modules"></a><span data-ttu-id="7787e-168">新增評分模型模組</span><span class="sxs-lookup"><span data-stu-id="7787e-168">Add the Score Model modules</span></span>

1. <span data-ttu-id="7787e-169">找到 [[評分模型]][score-model] 模組並拖曳到畫布上。</span><span class="sxs-lookup"><span data-stu-id="7787e-169">Find the [Score Model][score-model] module and drag it onto the canvas.</span></span>

2. <span data-ttu-id="7787e-170">將已連接至 [[二元促進式決策樹]][two-class-boosted-decision-tree] 模組的 [[訓練模型]][train-model] 模組，連接到 [[評分模型]][score-model] 模組的左側輸入連接埠。</span><span class="sxs-lookup"><span data-stu-id="7787e-170">Connect the [Train Model][train-model] module that's connected to the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="7787e-171">將右側 [[執行 R 指令碼]][execute-r-script] 模組 (或測試資料) 連接到 [[評分模型]][score-model] 模組的右側輸入連接埠。</span><span class="sxs-lookup"><span data-stu-id="7787e-171">Connect the right [Execute R Script][execute-r-script] module (our testing data) to the right input port of the [Score Model][score-model] module.</span></span>

    ![已連接評分模型模組][6]
   
   <span data-ttu-id="7787e-173">[[評分模型]][score-model] 模組可以立即從測試資料中採取信用資訊，並且將模型產生的預測情況與測試資料中的實際信用風險資料行進行比較。</span><span class="sxs-lookup"><span data-stu-id="7787e-173">The [Score Model][score-model] module can now take the credit information from the testing data, run it through the model, and compare the predictions the model generates with the actual credit risk column in the testing data.</span></span>

4. <span data-ttu-id="7787e-174">複製並貼上 [[評分模型]][score-model] 模組來建立第二個複本。</span><span class="sxs-lookup"><span data-stu-id="7787e-174">Copy and paste the [Score Model][score-model] module to create a second copy.</span></span>

5. <span data-ttu-id="7787e-175">將 SVM 模型的輸出 (亦即，已連接到 [[二元支援向量機器]][two-class-support-vector-machine] 的 [[訓練模型]][train-model] 模組的輸出連接埠)，連接到第二個 [[評分模型]][score-model] 模組的輸入連接埠。</span><span class="sxs-lookup"><span data-stu-id="7787e-175">Connect the output of the SVM model (that is, the output port of the [Train Model][train-model] module that's connected to the [Two-Class Support Vector Machine][two-class-support-vector-machine] module) to the input port of the second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="7787e-176">在 SVM 模型中，我們必須像是轉換定型資料一樣，對測試資料進行相同的轉換。</span><span class="sxs-lookup"><span data-stu-id="7787e-176">For the SVM model, we have to do the same transformation to the test data as we did to the training data.</span></span> <span data-ttu-id="7787e-177">因此，請複製並貼上 [[標準化資料]][normalize-data] 模組來建立第二個複本，再將其連接到右邊 [[執行 R 指令碼]][execute-r-script] 模組。</span><span class="sxs-lookup"><span data-stu-id="7787e-177">So copy and paste the [Normalize Data][normalize-data] module to create a second copy and connect it to the right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="7787e-178">將第二個 [[標準化資料]][normalize-data] 模組的左邊輸出連接到第二個 [[評分模型]][score-model] 模組的右邊輸入連接埠。</span><span class="sxs-lookup"><span data-stu-id="7787e-178">Connect the left output of the second [Normalize Data][normalize-data] module to the right input port of the second [Score Model][score-model] module.</span></span>

    ![已連接兩個評分模型模組][7]

### <a name="add-the-evaluate-model-module"></a><span data-ttu-id="7787e-180">新增評估模型模組</span><span class="sxs-lookup"><span data-stu-id="7787e-180">Add the Evaluate Model module</span></span>

<span data-ttu-id="7787e-181">為了評估兩個評計分結果並加以比較，我們使用[評估模型][evaluate-model]模組。</span><span class="sxs-lookup"><span data-stu-id="7787e-181">To evaluate the two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="7787e-182">找到 [[評估模型]][evaluate-model] 模組並拖曳到畫布上。</span><span class="sxs-lookup"><span data-stu-id="7787e-182">Find the [Evaluate Model][evaluate-model] module and drag it onto the canvas.</span></span>

2. <span data-ttu-id="7787e-183">將與促進式決策樹模型相關聯的 [[評分模型]][score-model]模組的輸出連接埠，連接到 [[評估模型]][evaluate-model] 模組的左側輸入連接埠。</span><span class="sxs-lookup"><span data-stu-id="7787e-183">Connect the output port of the [Score Model][score-model] module associated with the boosted decision tree model to the left input port of the [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="7787e-184">將其他 [[評分模型]][score-model] 模組連接到右側輸入連接埠。</span><span class="sxs-lookup"><span data-stu-id="7787e-184">Connect the other [Score Model][score-model] module to the right input port.</span></span>  

    ![已連接評估模型模組][8]

### <a name="run-the-experiment-and-check-the-results"></a><span data-ttu-id="7787e-186">執行實驗並檢查結果</span><span class="sxs-lookup"><span data-stu-id="7787e-186">Run the experiment and check the results</span></span>

<span data-ttu-id="7787e-187">若要執行實驗，請按一下畫布下方的 [執行] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7787e-187">To run the experiment, click the **RUN** button below the canvas.</span></span> <span data-ttu-id="7787e-188">可能需要數分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="7787e-188">It may take a few minutes.</span></span> <span data-ttu-id="7787e-189">每個模組上的旋轉指示器表示正在執行，模組完成時會出現綠色打勾記號。</span><span class="sxs-lookup"><span data-stu-id="7787e-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when the module is finished.</span></span> <span data-ttu-id="7787e-190">當所有模組都出現核取記號時，表示實驗執行完成。</span><span class="sxs-lookup"><span data-stu-id="7787e-190">When all the modules have a check mark, the experiment has finished running.</span></span>

<span data-ttu-id="7787e-191">實驗目前看起來如下：</span><span class="sxs-lookup"><span data-stu-id="7787e-191">The experiment should now look something like this:</span></span>  

![Evaluating both models][3]

<span data-ttu-id="7787e-193">若要檢查結果，按一下 [[評估模型]][evaluate-model] 模組的輸出連接埠，然後選取 [視覺化]。</span><span class="sxs-lookup"><span data-stu-id="7787e-193">To check the results, click the output port of the [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="7787e-194">[[評估模型]][evaluate-model] 模組會產生一對曲線和度量，讓您比較兩個評分模型的結果。</span><span class="sxs-lookup"><span data-stu-id="7787e-194">The [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you to compare the results of the two scored models.</span></span> <span data-ttu-id="7787e-195">您可以將結果顯示成「受測者操作特徵 (ROC)」曲線、「正確性/召回」曲線或「升力」曲線。</span><span class="sxs-lookup"><span data-stu-id="7787e-195">You can view the results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="7787e-196">其他顯示的資料還包括混淆矩陣、曲線下面積 (AUC) 的累計值，以及其他度量。</span><span class="sxs-lookup"><span data-stu-id="7787e-196">Additional data displayed includes a confusion matrix, cumulative values for the area under the curve (AUC), and other metrics.</span></span> <span data-ttu-id="7787e-197">您可以將滑動軸左右移動來變更臨界值，觀察這樣如何影響度量組。</span><span class="sxs-lookup"><span data-stu-id="7787e-197">You can change the threshold value by moving the slider left or right and see how it affects the set of metrics.</span></span>  

<span data-ttu-id="7787e-198">在圖形的右邊，按一下 [已計分的資料集] 或 [要比較的已計分資料集]，以醒目提示相關聯的曲線，並在下方顯示相關聯的度量。</span><span class="sxs-lookup"><span data-stu-id="7787e-198">To the right of the graph, click **Scored dataset** or **Scored dataset to compare** to highlight the associated curve and to display the associated metrics below.</span></span> <span data-ttu-id="7787e-199">在曲線的圖例中，"Scored dataset" 對應至 [[評估模型]][evaluate-model] 模組的左側輸入埠 - 在我們的案例中，這是促進式決策樹模型。</span><span class="sxs-lookup"><span data-stu-id="7787e-199">In the legend for the curves, "Scored dataset" corresponds to the left input port of the [Evaluate Model][evaluate-model] module - in our case, this is the boosted decision tree model.</span></span> <span data-ttu-id="7787e-200">「要比較的已計分資料集」會對應至右側輸入連接埠 (在本例中為 SVM 模型)。</span><span class="sxs-lookup"><span data-stu-id="7787e-200">"Scored dataset to compare" corresponds to the right input port - the SVM model in our case.</span></span> <span data-ttu-id="7787e-201">按一下其中一個標籤時，該模型的曲線會反白顯示，並顯示如下圖所示的相對應度量。</span><span class="sxs-lookup"><span data-stu-id="7787e-201">When you click one of these labels, the curve for that model is highlighted and the corresponding metrics are displayed, as shown in the following graphic.</span></span>  

![ROC curves for models][4]

<span data-ttu-id="7787e-203">您可以檢查這些值，以判斷哪個模型最可能提供您想要的結果。</span><span class="sxs-lookup"><span data-stu-id="7787e-203">By examining these values, you can decide which model is closest to giving you the results you're looking for.</span></span> <span data-ttu-id="7787e-204">您可以返回並變更不同模型中的參數值，以反覆執行實驗。</span><span class="sxs-lookup"><span data-stu-id="7787e-204">You can go back and iterate on your experiment by changing parameter values in the different models.</span></span> 

<span data-ttu-id="7787e-205">解讀這些結果和微調模型效能的藝術與科學超出本逐步解說的範圍。</span><span class="sxs-lookup"><span data-stu-id="7787e-205">The science and art of interpreting these results and tuning the model performance is outside the scope of this walkthrough.</span></span> <span data-ttu-id="7787e-206">如需更多說明，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="7787e-206">For additional help, you might read the following articles:</span></span>
- [<span data-ttu-id="7787e-207">如何在 Azure Machine Learning 中評估模型效能</span><span class="sxs-lookup"><span data-stu-id="7787e-207">How to evaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="7787e-208">選擇參數來最佳化 Azure Machine Learning 中的演算法</span><span class="sxs-lookup"><span data-stu-id="7787e-208">Choose parameters to optimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="7787e-209">在 Azure Machine Learning 中解讀模型結果</span><span class="sxs-lookup"><span data-stu-id="7787e-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="7787e-210">每次執行實驗，[執行歷程記錄] 中就會保留該筆逐一查看的記錄。</span><span class="sxs-lookup"><span data-stu-id="7787e-210">Each time you run the experiment a record of that iteration is kept in the Run History.</span></span> <span data-ttu-id="7787e-211">您可以檢視這些反覆運算，按一下畫布下方的 [檢視執行歷程記錄]  即可回到其中任何一個。</span><span class="sxs-lookup"><span data-stu-id="7787e-211">You can view these iterations, and return to any of them, by clicking **VIEW RUN HISTORY** below the canvas.</span></span> <span data-ttu-id="7787e-212">您也可以按一下 [屬性] 窗格中的 [先前執行]，回到您目前開啟的反覆運算之前的那一個反覆運算。</span><span class="sxs-lookup"><span data-stu-id="7787e-212">You can also click **Prior Run** in the **Properties** pane to return to the iteration immediately preceding the one you have open.</span></span>
> 
> <span data-ttu-id="7787e-213">您可以按一下畫布下方的 [另存新檔]  ，為實驗的任何反覆項目製作一個複本。</span><span class="sxs-lookup"><span data-stu-id="7787e-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below the canvas.</span></span> 
> <span data-ttu-id="7787e-214">使用實驗的 [摘要] 和 [描述] 屬性，以記錄在您實驗反覆運算中已嘗試的動作。</span><span class="sxs-lookup"><span data-stu-id="7787e-214">Use the experiment's **Summary** and **Description** properties to keep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="7787e-215">如需詳細資訊，請參閱 [在 Azure Machine Learning Studio 中管理實驗逐一查看](machine-learning-manage-experiment-iterations.md)。</span><span class="sxs-lookup"><span data-stu-id="7787e-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="7787e-216">**下一步：[部署 Web 服務](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="7787e-216">**Next: [Deploy the web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

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
