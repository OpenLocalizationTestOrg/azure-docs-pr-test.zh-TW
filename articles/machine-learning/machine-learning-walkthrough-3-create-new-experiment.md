---
title: "步驟 3：建立新的 Machine Learning 實驗 | Microsoft Docs"
description: "開發預測解決方案逐步解說的步驟 3：在 Azure Machine Learning Studio 中建立新的定型實驗。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: cd410316910bce76f5c915c06e83b24c034481b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a><span data-ttu-id="f9bfa-103">逐步解說步驟 3：建立新的 Azure Machine Learning 實驗</span><span class="sxs-lookup"><span data-stu-id="f9bfa-103">Walkthrough Step 3: Create a new Azure Machine Learning experiment</span></span>
<span data-ttu-id="f9bfa-104">這是 [在 Azure Machine Learning 中為信用風險評估開發預測性分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="f9bfa-104">This is the third step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="f9bfa-105">建立機器學習服務工作區</span><span class="sxs-lookup"><span data-stu-id="f9bfa-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="f9bfa-106">上傳現有資料</span><span class="sxs-lookup"><span data-stu-id="f9bfa-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. <span data-ttu-id="f9bfa-107">**建立新實驗**</span><span class="sxs-lookup"><span data-stu-id="f9bfa-107">**Create a new experiment**</span></span>
4. [<span data-ttu-id="f9bfa-108">訓練及評估模型</span><span class="sxs-lookup"><span data-stu-id="f9bfa-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="f9bfa-109">部署 Web 服務</span><span class="sxs-lookup"><span data-stu-id="f9bfa-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="f9bfa-110">存取 Web 服務</span><span class="sxs-lookup"><span data-stu-id="f9bfa-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="f9bfa-111">本逐步解說的下一步驟是在 Machine Learning Studio 中建立一個實驗，並在實驗中使用我們上傳的資料集。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-111">The next step in this walkthrough is to create an experiment in Machine Learning Studio that uses the dataset we uploaded.</span></span>  

1. <span data-ttu-id="f9bfa-112">在 Studio 中，按一下視窗底部的 [+新增]  。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-112">In Studio, click **+NEW** at the bottom of the window.</span></span>
2. <span data-ttu-id="f9bfa-113">選取 [實驗] ，然後選取 [空白實驗]。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-113">Select **EXPERIMENT**, and then select "Blank Experiment".</span></span> 

    ![建立新實驗][0]

2. <span data-ttu-id="f9bfa-115">選取畫布頂端的預設實驗名稱，然後將它重新命名為有意義的名稱。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-115">Select the default experiment name at the top of the canvas and rename it to something meaningful.</span></span>

    ![將實驗重新命名][5]
   
   > [!TIP]
   > <span data-ttu-id="f9bfa-117">在 [屬性] 窗格中為實驗填入 [摘要] 和 [描述] 是不錯的作法。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-117">It's a good practice to fill in **Summary** and **Description** for the experiment in the **Properties** pane.</span></span> <span data-ttu-id="f9bfa-118">這些屬性會提供記錄實驗的機會，以便稍後查看它的人員能了解您的目標和方法。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-118">These properties give you the chance to document the experiment so that anyone who looks at it later will understand your goals and methodology.</span></span>
   > 
   > ![實驗屬性][6]
   > 
3. <span data-ttu-id="f9bfa-120">在實驗畫布左側的模組調色盤中，展開 [Saved Datasets] 。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-120">In the module palette to the left of the experiment canvas, expand **Saved Datasets**.</span></span>
4. <span data-ttu-id="f9bfa-121">尋找您在 **我的資料集** 下建立的資料集並將它拖曳到畫布上。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-121">Find the dataset you created under **My Datasets** and drag it onto the canvas.</span></span> <span data-ttu-id="f9bfa-122">您也可以在調色盤上方的 [搜尋]  方塊中輸入名稱，以尋找資料集。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-122">You can also find the dataset by entering the name in the **Search** box above the palette.</span></span>  

    ![將資料集新增至實驗][7]

## <a name="prepare-the-data"></a><span data-ttu-id="f9bfa-124">準備資料</span><span class="sxs-lookup"><span data-stu-id="f9bfa-124">Prepare the data</span></span>
<span data-ttu-id="f9bfa-125">您可以按一下資料集的輸出連接埠 (底部的小圓圈)，然後選取 [視覺化] ，來檢視整個資料集的前 100 列資料和部分統計資訊。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-125">You can view the first 100 rows of the data and some statistical information for the whole dataset: Click the output port of the dataset (the small circle at the bottom) and select **Visualize**.</span></span>  

<span data-ttu-id="f9bfa-126">因為資料檔案並未隨附資料行標題，所以 Studio 已提供一般標題 (Col1、Col2 等等 )。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-126">Because the data file didn't come with column headings, Studio has provided generic headings (Col1, Col2, *etc.*).</span></span> <span data-ttu-id="f9bfa-127">建立模型並不一定要有良好的標題，但良好的標題可讓您更容易使用實驗中的資料。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-127">Good headings aren't essential to creating a model, but they make it easier to work with the data in the experiment.</span></span> <span data-ttu-id="f9bfa-128">此外，當我們最終在 Web 服務中發佈此模型時，標題有助於服務的使用者識別資料行。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-128">Also, when we eventually publish this model in a web service, the headings help identify the columns to the user of the service.</span></span>  

<span data-ttu-id="f9bfa-129">我們可以使用 [編輯中繼資料][edit-metadata] 模組來新增資料行標題。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-129">We can add column headings using the [Edit Metadata][edit-metadata] module.</span></span>
<span data-ttu-id="f9bfa-130">您需使用 [編輯中繼資料][edit-metadata] 模組來變更與資料集關聯的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-130">You use the [Edit Metadata][edit-metadata] module to change metadata associated with a dataset.</span></span> <span data-ttu-id="f9bfa-131">在此案例中，我們利用它來為資料行標題提供更易記的名稱。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-131">In this case, we use it to provide more friendly names for column headings.</span></span> 

<span data-ttu-id="f9bfa-132">若要使用 [編輯中繼資料][edit-metadata]，您要先指定要修改哪些資料行 (在此案例中是全部)。接著，指定要對這些資料行執行的動作 (在此案例中是變更資料行標題)。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-132">To use [Edit Metadata][edit-metadata], you first specify which columns to modify (in this case, all of them.) Next, you specify the action to be performed on those columns (in this case, changing column headings.)</span></span>

1. <span data-ttu-id="f9bfa-133">在模組調色盤的 [搜尋]  方塊中，輸入 "metadata"。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-133">In the module palette, type "metadata" in the **Search** box.</span></span> <span data-ttu-id="f9bfa-134">[編輯中繼資料][edit-metadata] 出現在模組清單中。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-134">The [Edit Metadata][edit-metadata] appears in the module list.</span></span>

2. <span data-ttu-id="f9bfa-135">按一下 [編輯中繼資料][edit-metadata] 模組並拖曳到畫布上，將它放在我們稍早新增的資料集下。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-135">Click and drag the [Edit Metadata][edit-metadata] module onto the canvas and drop it below the dataset we added earlier.</span></span>

3. <span data-ttu-id="f9bfa-136">將資料集連接到 [編輯中繼資料][edit-metadata]：按一下資料集的輸出連接埠 (資料集底部的小圓圈)、拖曳到 [編輯中繼資料][edit-metadata] 的輸入連接埠 (模組頂端的小圓圈)，然後放開滑鼠按鍵。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-136">Connect the dataset to the [Edit Metadata][edit-metadata]: click the output port of the dataset (the small circle at the bottom of the dataset), drag to the input port of [Edit Metadata][edit-metadata] (the small circle at the top of the module), then release the mouse button.</span></span> <span data-ttu-id="f9bfa-137">即使您在畫布上移動資料集或模組，這兩者仍會保持連線。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-137">The dataset and module remain connected even if you move either around on the canvas.</span></span>
   
   <span data-ttu-id="f9bfa-138">實驗目前看起來如下：</span><span class="sxs-lookup"><span data-stu-id="f9bfa-138">The experiment should now look something like this:</span></span>  
   
   ![新增編輯中繼資料][1]
   
   <span data-ttu-id="f9bfa-140">紅色驚嘆號標示表示我們尚未設定此模組的屬性。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-140">The red exclamation mark indicates that we haven't set the properties for this module yet.</span></span> <span data-ttu-id="f9bfa-141">我們接下來會這樣做。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-141">We'll do that next.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="f9bfa-142">您可以按兩下模組並輸入文字，為模組新增註解。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-142">You can add a comment to a module by double-clicking the module and entering text.</span></span> <span data-ttu-id="f9bfa-143">這有助於您快速檢視模組在您實驗中的執行情況。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-143">This can help you see at a glance what the module is doing in your experiment.</span></span> <span data-ttu-id="f9bfa-144">在此案例中，請按兩下 [編輯中繼資料][edit-metadata] 模組，然後輸入註解「新增資料行標題」。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-144">In this case, double-click the [Edit Metadata][edit-metadata] module and type the comment "Add column headings".</span></span> <span data-ttu-id="f9bfa-145">按一下畫布上其他的任何地方來關閉文字方塊。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-145">Click anywhere else on the canvas to close the text box.</span></span> <span data-ttu-id="f9bfa-146">若要顯示註解，請按一下模組的向下箭號。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-146">To display the comment, click the down-arrow on the module.</span></span>
   > 
   > ![編輯中繼資料模組並新增註解][8]
   > 
4. <span data-ttu-id="f9bfa-148">選取 [編輯中繼資料][edit-metadata]，然後在畫布右邊的 [屬性] 窗格中，按一下 [啟動資料行選取器]。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-148">Select [Edit Metadata][edit-metadata], and in the **Properties** pane to the right of the canvas, click **Launch column selector**.</span></span>

5. <span data-ttu-id="f9bfa-149">在 [選取資料行] 對話方塊中，選取 [可用的資料行] 中的所有資料列，然後按一下 > 將它們移到 [選取的資料行]。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-149">In the **Select columns** dialog, select all the rows in **Available Columns** and click > to move them to **Selected Columns**.</span></span>
   <span data-ttu-id="f9bfa-150">對話方塊應該會看起來如下：</span><span class="sxs-lookup"><span data-stu-id="f9bfa-150">The dialog should look like this:</span></span>

   ![已選取所有資料行的資料行選取器][2]

6. <span data-ttu-id="f9bfa-152">按一下 **[確定]** \(打勾記號)。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-152">Click the **OK** check mark.</span></span>

7. <span data-ttu-id="f9bfa-153">回到 [屬性] 窗格，找到 [新的資料行名稱] 參數。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-153">Back in the **Properties** pane, look for the **New column names** parameter.</span></span> <span data-ttu-id="f9bfa-154">在這個欄位中，輸入資料集中 21 個資料行的名稱清單，並以逗號加以分隔，且依資料行順序排序。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-154">In this field, enter a list of names for the 21 columns in the dataset, separated by commas and in column order.</span></span> <span data-ttu-id="f9bfa-155">您可以從 UCI 網站上的資料集文件中取得資料行名稱，或為求簡便，您可以複製並貼上下列清單：</span><span class="sxs-lookup"><span data-stu-id="f9bfa-155">You can obtain the columns names from the dataset documentation on the UCI website, or for convenience you can copy and paste the following list:</span></span>  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   <span data-ttu-id="f9bfa-156">[屬性] 窗格看起來像這樣︰</span><span class="sxs-lookup"><span data-stu-id="f9bfa-156">The Properties pane looks like this:</span></span>
   
   ![編輯中繼資料的屬性][3]

> [!TIP]
> <span data-ttu-id="f9bfa-158">如果您想要確認資料行標題，請執行實驗 (按一下實驗畫布下方的 [執行])。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-158">If you want to verify the column headings, run the experiment (click **RUN** below the experiment canvas).</span></span> <span data-ttu-id="f9bfa-159">當執行結束時 ([編輯中繼資料][edit-metadata] 上會出現綠色的打勾記號)，按一下[編輯中繼資料][edit-metadata] 模組的輸出連接埠，然後選取 [視覺化]。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-159">When it finishes running (a green check mark appears on [Edit Metadata][edit-metadata]), click the output port of the [Edit Metadata][edit-metadata] module, and select **Visualize**.</span></span> <span data-ttu-id="f9bfa-160">您可以用相同方式檢視任何模組的輸出，以檢視資料在實驗中的執行進度。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-160">You can view the output of any module in the same way to view the progress of the data through the experiment.</span></span>
> 
> 

## <a name="create-training-and-test-datasets"></a><span data-ttu-id="f9bfa-161">建立訓練和測試資料集</span><span class="sxs-lookup"><span data-stu-id="f9bfa-161">Create training and test datasets</span></span>
<span data-ttu-id="f9bfa-162">我們需要一些資料來訓練模型，有些則可用來測試模型。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-162">We need some data to train the model and some to test it.</span></span>
<span data-ttu-id="f9bfa-163">因此在實驗的下一個步驟中，我們將資料集分割成兩個不同的資料集：一個用於訓練模型，另一個用於測試模型。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-163">So in the next step of the experiment, we split the dataset into two separate datasets: one for training our model and one for testing it.</span></span>

<span data-ttu-id="f9bfa-164">為此，我們使用 [資料分割][split] 模組。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-164">To do this, we use the [Split Data][split] module.</span></span>  

1. <span data-ttu-id="f9bfa-165">找到 [資料分割][split] 模組，將它拖曳到畫布上，然後連接到 [編輯中繼資料][edit-metadata] 模組。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-165">Find the [Split Data][split] module, drag it onto the canvas, and connect it to the [Edit Metadata][edit-metadata] module.</span></span>

2. <span data-ttu-id="f9bfa-166">根據預設，分割率會是 0.5，並且會設定 [Randomized split]  參數。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-166">By default, the split ratio is 0.5 and the **Randomized split** parameter is set.</span></span> <span data-ttu-id="f9bfa-167">這表示有一半資料會隨機透過 [分割資料][split] 模組的一個連接埠輸出，一半透過另一個連接埠輸出。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-167">This means that a random half of the data is output through one port of the [Split Data][split] module, and half through the other.</span></span> <span data-ttu-id="f9bfa-168">您可以調整這些參數和 [隨機種子] 參數，以變更訓練與測試資料之間的分割。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-168">You can adjust these parameters, as well as the **Random seed** parameter, to change the split between training and testing data.</span></span> <span data-ttu-id="f9bfa-169">在此範例中，我們保持原狀。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-169">For this example, we leave them as-is.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="f9bfa-170">[第一個輸出資料集內的資料列比例] 屬性會決定要透過「左側」輸出連接埠輸出多少資料。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-170">The property **Fraction of rows in the first output dataset** determines how much of the data is output through the *left* output port.</span></span> <span data-ttu-id="f9bfa-171">例如，如果您將分割率設為 0.7，則會有 70% 的資料透過左側連接埠輸出，30% 透過右側連接埠輸出。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-171">For instance, if you set the ratio to 0.7, then 70% of the data is output through the left port and 30% through the right port.</span></span>  
   > 
   > 

3. <span data-ttu-id="f9bfa-172">按兩下 [資料分割][split] 模組，並輸入註解「訓練/測試資料分割 50%」。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-172">Double-click the [Split Data][split] module and enter the comment, "Training/testing data split 50%".</span></span> 

<span data-ttu-id="f9bfa-173">我們可以依自身需求使用 [資料分割][split] 模組的輸出，但在範例中，我們要選擇以左側輸出作為訓練資料，右側輸出作為測試資料。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-173">We can use the outputs of the [Split Data][split] module however we like, but let's choose to use the left output as training data and the right output as testing data.</span></span>  

<span data-ttu-id="f9bfa-174">如[上一個步驟](machine-learning-walkthrough-2-upload-data.md)所述，將高信用風險誤判為低風險的成本，會比將低信用風險誤判為高風險的成本多出五倍。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-174">As mentioned in the [previous step](machine-learning-walkthrough-2-upload-data.md), the cost of misclassifying a high credit risk as low is five times higher than the cost of misclassifying a low credit risk as high.</span></span> <span data-ttu-id="f9bfa-175">為了說明這一點，我們將產生新資料集以反映此成本函式。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-175">To account for this, we generate a new dataset that reflects this cost function.</span></span> <span data-ttu-id="f9bfa-176">在此新資料集中，每個高風險範例都會複寫五次，而每個低風險範例則不複寫。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-176">In the new dataset, each high risk example is replicated five times, while each low risk example is not replicated.</span></span>   

<span data-ttu-id="f9bfa-177">我們可以使用 R 程式碼來執行此複寫：</span><span class="sxs-lookup"><span data-stu-id="f9bfa-177">We can do this replication using R code:</span></span>  

1. <span data-ttu-id="f9bfa-178">找到 [執行 R 程式碼][execute-r-script] 模組，並將它拖曳到實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-178">Find and drag the [Execute R Script][execute-r-script] module onto the experiment canvas.</span></span> 

2. <span data-ttu-id="f9bfa-179">將 [資料分割][split] 模組的左側輸出連接埠連接到 [執行 R 指令碼][execute-r-script] 模組的第一個輸入連接埠 ("Dataset1")。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-179">Connect the left output port of the [Split Data][split] module to the first input port ("Dataset1") of the [Execute R Script][execute-r-script] module.</span></span>

3. <span data-ttu-id="f9bfa-180">按兩下 [執行 R 指令碼][execute-r-script] 模組並輸入註解「設定成本調整」。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-180">Double-click the [Execute R Script][execute-r-script] module and enter the comment, "Set cost adjustment".</span></span>

4. <span data-ttu-id="f9bfa-181">在 [屬性] 窗格中，刪除 [R 指令碼] 參數中的預設文字，然後輸入此指令碼：</span><span class="sxs-lookup"><span data-stu-id="f9bfa-181">In the **Properties** pane, delete the default text in the **R Script** parameter and enter this script:</span></span>
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![執行 R 指令碼模組中的 R 指令碼][9]

<span data-ttu-id="f9bfa-183">我們必須為 [資料分割][split] 模組的每個輸出執行此一相同複寫作業，使訓練和測試資料具有相同的成本調整。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-183">We need to do this same replication operation for each output of the [Split Data][split] module so that the training and testing data have the same cost adjustment.</span></span> <span data-ttu-id="f9bfa-184">執行此動作的最簡單方式是複製剛製作的[執行 R 指令碼][execute-r-script]模組，並將其連接至[分割資料][split]模組的其他輸出連接埠。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-184">The easiest way to do this is by duplicating the [Execute R Script][execute-r-script] module we just made and connecting it to the other output port of the [Split Data][split] module.</span></span>

1. <span data-ttu-id="f9bfa-185">以滑鼠右鍵按一下 [執行 R 指令碼][execute-r-script] 模組，然後選取 [複製]。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-185">Right-click the [Execute R Script][execute-r-script] module and select **Copy**.</span></span>

2. <span data-ttu-id="f9bfa-186">以滑鼠右鍵按一下實驗畫布，然後選取 [貼上] 。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-186">Right-click the experiment canvas and select **Paste**.</span></span>

3. <span data-ttu-id="f9bfa-187">將新模組拖曳至畫布中，然後將 [資料分割][split] 模組的右側輸出連接埠連接到這個新的 [執行 R 指令碼][execute-r-script] 模組的第一個輸入連接埠。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-187">Drag the new module into position, and then connect the right output port of the [Split Data][split] module to the first input port of this new [Execute R Script][execute-r-script] module.</span></span> 

4. <span data-ttu-id="f9bfa-188">在實驗畫布底端，按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-188">At the bottom of the canvas, click **Run**.</span></span> 

> [!TIP]
> <span data-ttu-id="f9bfa-189">「執行 R 指令碼」模組的複本會包含與原始模組相同的指令碼。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-189">The copy of the Execute R Script module contains the same script as the original module.</span></span> <span data-ttu-id="f9bfa-190">當您在畫布上複製並貼上模組時，複本將會保留原本的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-190">When you copy and paste a module on the canvas, the copy retains all the properties of the original.</span></span>  
> 
> 

<span data-ttu-id="f9bfa-191">實驗此時看起來會如下所示：</span><span class="sxs-lookup"><span data-stu-id="f9bfa-191">Our experiment now looks something like this:</span></span>

![Adding Split module and R scripts][4]

<span data-ttu-id="f9bfa-193">如需如何在您的實驗中使用 R 指令碼的詳細資訊，請參閱 [透過 R 擴充您的實驗](machine-learning-extend-your-experiment-with-r.md)。</span><span class="sxs-lookup"><span data-stu-id="f9bfa-193">For more information on using R scripts in your experiments, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md).</span></span>

<span data-ttu-id="f9bfa-194">**下一步：[訓練及評估模型](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span><span class="sxs-lookup"><span data-stu-id="f9bfa-194">**Next: [Train and evaluate the models](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span></span>

[0]: ./media/machine-learning-walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/machine-learning-walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/machine-learning-walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/machine-learning-walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/machine-learning-walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
