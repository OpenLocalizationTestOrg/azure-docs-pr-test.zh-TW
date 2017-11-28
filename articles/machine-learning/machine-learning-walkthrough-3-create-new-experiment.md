---
title: "步驟 3：建立新的 Machine Learning 實驗 | Microsoft Docs"
description: "步驟 3 中的 hello 開發預測方案逐步解說： 在 Azure Machine Learning Studio 中建立新的定型實驗。"
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
ms.openlocfilehash: 4697d461a205c50c8d2aa6a3bd56697840cb30f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a><span data-ttu-id="2318e-103">逐步解說步驟 3：建立新的 Azure Machine Learning 實驗</span><span class="sxs-lookup"><span data-stu-id="2318e-103">Walkthrough Step 3: Create a new Azure Machine Learning experiment</span></span>
<span data-ttu-id="2318e-104">這是 hello hello 逐步解說中，第三個步驟[開發 Azure Machine Learning 中的預測分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="2318e-104">This is hello third step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="2318e-105">建立機器學習服務工作區</span><span class="sxs-lookup"><span data-stu-id="2318e-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="2318e-106">上傳現有資料</span><span class="sxs-lookup"><span data-stu-id="2318e-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. <span data-ttu-id="2318e-107">**建立新實驗**</span><span class="sxs-lookup"><span data-stu-id="2318e-107">**Create a new experiment**</span></span>
4. [<span data-ttu-id="2318e-108">來定型及評估 hello 模型</span><span class="sxs-lookup"><span data-stu-id="2318e-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="2318e-109">部署 hello Web 服務</span><span class="sxs-lookup"><span data-stu-id="2318e-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="2318e-110">存取 hello Web 服務</span><span class="sxs-lookup"><span data-stu-id="2318e-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="2318e-111">在此逐步解說中的 hello 下一個步驟是 toocreate 實驗中使用 hello 我們上傳的資料集的 Machine Learning Studio 中。</span><span class="sxs-lookup"><span data-stu-id="2318e-111">hello next step in this walkthrough is toocreate an experiment in Machine Learning Studio that uses hello dataset we uploaded.</span></span>  

1. <span data-ttu-id="2318e-112">在 Studio 中，按一下  **+ 新增**在 hello hello 視窗的底部。</span><span class="sxs-lookup"><span data-stu-id="2318e-112">In Studio, click **+NEW** at hello bottom of hello window.</span></span>
2. <span data-ttu-id="2318e-113">選取 [實驗] ，然後選取 [空白實驗]。</span><span class="sxs-lookup"><span data-stu-id="2318e-113">Select **EXPERIMENT**, and then select "Blank Experiment".</span></span> 

    ![建立新實驗][0]

2. <span data-ttu-id="2318e-115">選取 hello 預設試驗頂端 hello hello 畫布的名稱，以及將它重新命名 toosomething 有意義。</span><span class="sxs-lookup"><span data-stu-id="2318e-115">Select hello default experiment name at hello top of hello canvas and rename it toosomething meaningful.</span></span>

    ![將實驗重新命名][5]
   
   > [!TIP]
   > <span data-ttu-id="2318e-117">它是很好的作法 toofill**摘要**和**描述**hello 實驗中 hello**屬性**窗格。</span><span class="sxs-lookup"><span data-stu-id="2318e-117">It's a good practice toofill in **Summary** and **Description** for hello experiment in hello **Properties** pane.</span></span> <span data-ttu-id="2318e-118">這些屬性提供，以便稍後會查看它的任何人就可以了解您的目標和方法，hello 機會 toodocument hello 實驗。</span><span class="sxs-lookup"><span data-stu-id="2318e-118">These properties give you hello chance toodocument hello experiment so that anyone who looks at it later will understand your goals and methodology.</span></span>
   > 
   > ![實驗屬性][6]
   > 
3. <span data-ttu-id="2318e-120">在 hello 模組調色盤 toohello 左邊 hello 實驗畫布上，依序展開**儲存的資料集**。</span><span class="sxs-lookup"><span data-stu-id="2318e-120">In hello module palette toohello left of hello experiment canvas, expand **Saved Datasets**.</span></span>
4. <span data-ttu-id="2318e-121">尋找 hello 資料集下您建立**我的資料集**並將它拖曳到畫布 hello。</span><span class="sxs-lookup"><span data-stu-id="2318e-121">Find hello dataset you created under **My Datasets** and drag it onto hello canvas.</span></span> <span data-ttu-id="2318e-122">您也可以尋找 hello dataset 中 hello 輸入 hello 名稱**搜尋**hello 調色盤上的方塊。</span><span class="sxs-lookup"><span data-stu-id="2318e-122">You can also find hello dataset by entering hello name in hello **Search** box above hello palette.</span></span>  

    ![新增 hello 資料集 toohello 實驗][7]

## <a name="prepare-hello-data"></a><span data-ttu-id="2318e-124">準備 hello 資料</span><span class="sxs-lookup"><span data-stu-id="2318e-124">Prepare hello data</span></span>
<span data-ttu-id="2318e-125">您可以檢視前 100 個資料列的 hello 和 hello 整個結果集的一些統計資訊 hello： 按一下 hello hello 資料集 （使用 hello 底部 hello 小圓形） 的輸出連接埠，然後選取**視覺化**。</span><span class="sxs-lookup"><span data-stu-id="2318e-125">You can view hello first 100 rows of hello data and some statistical information for hello whole dataset: Click hello output port of hello dataset (hello small circle at hello bottom) and select **Visualize**.</span></span>  

<span data-ttu-id="2318e-126">Studio hello 資料檔案並未隨附資料行標題，因為提供的泛型標題 (Col1，Col2，*等*)。</span><span class="sxs-lookup"><span data-stu-id="2318e-126">Because hello data file didn't come with column headings, Studio has provided generic headings (Col1, Col2, *etc.*).</span></span> <span data-ttu-id="2318e-127">良好標題不是基本 toocreating 模型，但它們會 hello 資料更容易 toowork hello 實驗中。</span><span class="sxs-lookup"><span data-stu-id="2318e-127">Good headings aren't essential toocreating a model, but they make it easier toowork with hello data in hello experiment.</span></span> <span data-ttu-id="2318e-128">此外，當我們最後發行此模型在 web 服務時，hello 標題將有助於識別 hello 服務的 hello 資料行 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="2318e-128">Also, when we eventually publish this model in a web service, hello headings help identify hello columns toohello user of hello service.</span></span>  

<span data-ttu-id="2318e-129">我們可以加入資料行標題使用 hello[編輯中繼資料][ edit-metadata]模組。</span><span class="sxs-lookup"><span data-stu-id="2318e-129">We can add column headings using hello [Edit Metadata][edit-metadata] module.</span></span>
<span data-ttu-id="2318e-130">使用 hello[編輯中繼資料][ edit-metadata]模組 toochange 中繼資料與資料集相關聯。</span><span class="sxs-lookup"><span data-stu-id="2318e-130">You use hello [Edit Metadata][edit-metadata] module toochange metadata associated with a dataset.</span></span> <span data-ttu-id="2318e-131">在此情況下，將使用此值的更多的易記名稱的 tooprovide 針對資料行標題。</span><span class="sxs-lookup"><span data-stu-id="2318e-131">In this case, we use it tooprovide more friendly names for column headings.</span></span> 

<span data-ttu-id="2318e-132">toouse[編輯中繼資料][edit-metadata]，您首先要指定哪些資料行 toomodify，（在此情況下，它們全部。）接下來，您可以指定 hello 動作 toobe 對這些資料行 （在此情況下，變更資料行標題。）</span><span class="sxs-lookup"><span data-stu-id="2318e-132">toouse [Edit Metadata][edit-metadata], you first specify which columns toomodify (in this case, all of them.) Next, you specify hello action toobe performed on those columns (in this case, changing column headings.)</span></span>

1. <span data-ttu-id="2318e-133">Hello 模組調色盤上，輸入 「 中繼資料 」 中 hello**搜尋**方塊。</span><span class="sxs-lookup"><span data-stu-id="2318e-133">In hello module palette, type "metadata" in hello **Search** box.</span></span> <span data-ttu-id="2318e-134">hello[編輯中繼資料][ edit-metadata] hello 模組清單中會出現。</span><span class="sxs-lookup"><span data-stu-id="2318e-134">hello [Edit Metadata][edit-metadata] appears in hello module list.</span></span>

2. <span data-ttu-id="2318e-135">按一下並拖曳 hello[編輯中繼資料][ edit-metadata]模組 hello 到畫布，並將它放在下方 hello 我們先前加入的資料集。</span><span class="sxs-lookup"><span data-stu-id="2318e-135">Click and drag hello [Edit Metadata][edit-metadata] module onto hello canvas and drop it below hello dataset we added earlier.</span></span>

3. <span data-ttu-id="2318e-136">連接 hello 資料集 toohello[編輯中繼資料][edit-metadata]： 按一下 hello hello 資料集 （使用 hello 資料集的 hello 底部 hello 小圓形） 的輸出連接埠中，拖曳 toohello 的輸入連接埠[編輯中繼資料] [ edit-metadata] （hello 小圓圈 hello hello 模組頂端），然後放開 hello 滑鼠按鈕。</span><span class="sxs-lookup"><span data-stu-id="2318e-136">Connect hello dataset toohello [Edit Metadata][edit-metadata]: click hello output port of hello dataset (hello small circle at hello bottom of hello dataset), drag toohello input port of [Edit Metadata][edit-metadata] (hello small circle at hello top of hello module), then release hello mouse button.</span></span> <span data-ttu-id="2318e-137">hello 資料集和模組保持連接，即使您移動其中 hello 畫布上。</span><span class="sxs-lookup"><span data-stu-id="2318e-137">hello dataset and module remain connected even if you move either around on hello canvas.</span></span>
   
   <span data-ttu-id="2318e-138">hello 實驗現在看起來應該像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="2318e-138">hello experiment should now look something like this:</span></span>  
   
   ![新增編輯中繼資料][1]
   
   <span data-ttu-id="2318e-140">hello 紅色驚嘆號表示我們沒有尚未設定此模組的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="2318e-140">hello red exclamation mark indicates that we haven't set hello properties for this module yet.</span></span> <span data-ttu-id="2318e-141">我們接下來會這樣做。</span><span class="sxs-lookup"><span data-stu-id="2318e-141">We'll do that next.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="2318e-142">您可以新增註解 tooa 模組按兩下 hello 模組和輸入的文字。</span><span class="sxs-lookup"><span data-stu-id="2318e-142">You can add a comment tooa module by double-clicking hello module and entering text.</span></span> <span data-ttu-id="2318e-143">這可協助您快速地查看哪些 hello 模組負責在您實驗中。</span><span class="sxs-lookup"><span data-stu-id="2318e-143">This can help you see at a glance what hello module is doing in your experiment.</span></span> <span data-ttu-id="2318e-144">在此情況下，按兩下 hello[編輯中繼資料][ edit-metadata]模組和類型 hello 註解"Add 資料行標題 」。</span><span class="sxs-lookup"><span data-stu-id="2318e-144">In this case, double-click hello [Edit Metadata][edit-metadata] module and type hello comment "Add column headings".</span></span> <span data-ttu-id="2318e-145">按一下任何其他地方 hello 畫布 tooclose hello 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="2318e-145">Click anywhere else on hello canvas tooclose hello text box.</span></span> <span data-ttu-id="2318e-146">toodisplay hello 註解，請按一下 hello 向下箭頭 hello 模組上。</span><span class="sxs-lookup"><span data-stu-id="2318e-146">toodisplay hello comment, click hello down-arrow on hello module.</span></span>
   > 
   > ![編輯中繼資料模組並新增註解][8]
   > 
4. <span data-ttu-id="2318e-148">選取[編輯中繼資料][edit-metadata]，並在 hello**屬性**窗格 toohello hello 畫布的右邊按一下**啟動資料行選取器**。</span><span class="sxs-lookup"><span data-stu-id="2318e-148">Select [Edit Metadata][edit-metadata], and in hello **Properties** pane toohello right of hello canvas, click **Launch column selector**.</span></span>

5. <span data-ttu-id="2318e-149">在 hello**選取資料行**對話方塊中，選取所有 hello 中的資料列**可用的資料行**按一下 > toomove 它們太**選取的資料行**。</span><span class="sxs-lookup"><span data-stu-id="2318e-149">In hello **Select columns** dialog, select all hello rows in **Available Columns** and click > toomove them too**Selected Columns**.</span></span>
   <span data-ttu-id="2318e-150">hello 對話方塊看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="2318e-150">hello dialog should look like this:</span></span>

   ![已選取所有資料行的資料行選取器][2]

6. <span data-ttu-id="2318e-152">按一下 hello**確定**核取記號。</span><span class="sxs-lookup"><span data-stu-id="2318e-152">Click hello **OK** check mark.</span></span>

7. <span data-ttu-id="2318e-153">在 hello**屬性**窗格中，尋找 hello**新資料行名稱**參數。</span><span class="sxs-lookup"><span data-stu-id="2318e-153">Back in hello **Properties** pane, look for hello **New column names** parameter.</span></span> <span data-ttu-id="2318e-154">在此欄位中，輸入 hello 21 hello 資料集，以逗點和資料行順序，以分隔資料行名稱的清單。</span><span class="sxs-lookup"><span data-stu-id="2318e-154">In this field, enter a list of names for hello 21 columns in hello dataset, separated by commas and in column order.</span></span> <span data-ttu-id="2318e-155">您可以從 hello 資料集的文件 hello UCI 在網站上，取得 hello 資料行名稱，或為了方便起見，您可以複製並貼上下列清單中的 hello:</span><span class="sxs-lookup"><span data-stu-id="2318e-155">You can obtain hello columns names from hello dataset documentation on hello UCI website, or for convenience you can copy and paste hello following list:</span></span>  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   <span data-ttu-id="2318e-156">hello 屬性 窗格看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="2318e-156">hello Properties pane looks like this:</span></span>
   
   ![編輯中繼資料的屬性][3]

> [!TIP]
> <span data-ttu-id="2318e-158">如果您想 tooverify hello 資料行標題，請執行 hello 實驗 (按一下**執行**hello 實驗畫布下方)。</span><span class="sxs-lookup"><span data-stu-id="2318e-158">If you want tooverify hello column headings, run hello experiment (click **RUN** below hello experiment canvas).</span></span> <span data-ttu-id="2318e-159">當它完成時執行 (綠色的核取記號會出現在[編輯中繼資料][edit-metadata])，按一下輸出連接埠 hello hello[編輯中繼資料][ edit-metadata]模組，並選取**視覺化**。</span><span class="sxs-lookup"><span data-stu-id="2318e-159">When it finishes running (a green check mark appears on [Edit Metadata][edit-metadata]), click hello output port of hello [Edit Metadata][edit-metadata] module, and select **Visualize**.</span></span> <span data-ttu-id="2318e-160">您可以檢視的任何模組的 hello 輸出中 hello hello 實驗中 hello 資料相同的方式 tooview hello 進度。</span><span class="sxs-lookup"><span data-stu-id="2318e-160">You can view hello output of any module in hello same way tooview hello progress of hello data through hello experiment.</span></span>
> 
> 

## <a name="create-training-and-test-datasets"></a><span data-ttu-id="2318e-161">建立訓練和測試資料集</span><span class="sxs-lookup"><span data-stu-id="2318e-161">Create training and test datasets</span></span>
<span data-ttu-id="2318e-162">我們需要一些資料 tootrain hello 模型和一些 tootest 它。</span><span class="sxs-lookup"><span data-stu-id="2318e-162">We need some data tootrain hello model and some tootest it.</span></span>
<span data-ttu-id="2318e-163">因此在 hello 實驗 hello 下一步，分割 hello 資料集分成兩個不同的資料集： 一個用於培訓我們的模型，另一個用於測試。</span><span class="sxs-lookup"><span data-stu-id="2318e-163">So in hello next step of hello experiment, we split hello dataset into two separate datasets: one for training our model and one for testing it.</span></span>

<span data-ttu-id="2318e-164">toodo，我們使用 hello[分割資料][ split]模組。</span><span class="sxs-lookup"><span data-stu-id="2318e-164">toodo this, we use hello [Split Data][split] module.</span></span>  

1. <span data-ttu-id="2318e-165">尋找 hello[分割資料][ split]模組，將它拖曳至 hello 畫布，並將它連接 toohello[編輯中繼資料][ edit-metadata]模組。</span><span class="sxs-lookup"><span data-stu-id="2318e-165">Find hello [Split Data][split] module, drag it onto hello canvas, and connect it toohello [Edit Metadata][edit-metadata] module.</span></span>

2. <span data-ttu-id="2318e-166">根據預設，hello 分割比例是 0.5 和 hello**隨機分割**參數設定。</span><span class="sxs-lookup"><span data-stu-id="2318e-166">By default, hello split ratio is 0.5 and hello **Randomized split** parameter is set.</span></span> <span data-ttu-id="2318e-167">這表示 hello 資料隨機半是透過一個連接埠的 hello 輸出[分割資料][ split]模組和半透過 hello 其他。</span><span class="sxs-lookup"><span data-stu-id="2318e-167">This means that a random half of hello data is output through one port of hello [Split Data][split] module, and half through hello other.</span></span> <span data-ttu-id="2318e-168">您可以調整這些參數，以及 hello**隨機種子**參數，toochange hello 分割成定型集和測試資料。</span><span class="sxs-lookup"><span data-stu-id="2318e-168">You can adjust these parameters, as well as hello **Random seed** parameter, toochange hello split between training and testing data.</span></span> <span data-ttu-id="2318e-169">在此範例中，我們保持原狀。</span><span class="sxs-lookup"><span data-stu-id="2318e-169">For this example, we leave them as-is.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="2318e-170">hello 屬性**hello 中的資料列的分數，第一次輸出資料集**決定多少 hello 資料是透過 hello 輸出*左*輸出連接埠。</span><span class="sxs-lookup"><span data-stu-id="2318e-170">hello property **Fraction of rows in hello first output dataset** determines how much of hello data is output through hello *left* output port.</span></span> <span data-ttu-id="2318e-171">比方說，如果您設定 hello 比率 too0.7，70%的 hello 資料則透過 hello 左連接埠和 30%，透過 hello 右連接埠的輸出。</span><span class="sxs-lookup"><span data-stu-id="2318e-171">For instance, if you set hello ratio too0.7, then 70% of hello data is output through hello left port and 30% through hello right port.</span></span>  
   > 
   > 

3. <span data-ttu-id="2318e-172">按兩下 hello[分割資料][ split]模組和輸入 hello 註解、 「 定型/測試資料分割的 50%」。</span><span class="sxs-lookup"><span data-stu-id="2318e-172">Double-click hello [Split Data][split] module and enter hello comment, "Training/testing data split 50%".</span></span> 

<span data-ttu-id="2318e-173">我們可以使用的 hello hello 輸出[分割資料][ split]我們喜歡，不過我們選擇 toouse hello 左的輸出做為定型資料，且右 hello 模組輸出為測試資料。</span><span class="sxs-lookup"><span data-stu-id="2318e-173">We can use hello outputs of hello [Split Data][split] module however we like, but let's choose toouse hello left output as training data and hello right output as testing data.</span></span>  

<span data-ttu-id="2318e-174">Hello 中所述[上一個步驟](machine-learning-walkthrough-2-upload-data.md)，hello 高信用風險低為將錯誤分類成本高於五次 hello 為 high 低的信用風險將錯誤分類成本。</span><span class="sxs-lookup"><span data-stu-id="2318e-174">As mentioned in hello [previous step](machine-learning-walkthrough-2-upload-data.md), hello cost of misclassifying a high credit risk as low is five times higher than hello cost of misclassifying a low credit risk as high.</span></span> <span data-ttu-id="2318e-175">這個 tooaccount，我們會產生新的資料集，以反映此成本函式。</span><span class="sxs-lookup"><span data-stu-id="2318e-175">tooaccount for this, we generate a new dataset that reflects this cost function.</span></span> <span data-ttu-id="2318e-176">在 hello 新資料集中，每個高風險範例複寫五次，而不會複寫每個低風險範例。</span><span class="sxs-lookup"><span data-stu-id="2318e-176">In hello new dataset, each high risk example is replicated five times, while each low risk example is not replicated.</span></span>   

<span data-ttu-id="2318e-177">我們可以使用 R 程式碼來執行此複寫：</span><span class="sxs-lookup"><span data-stu-id="2318e-177">We can do this replication using R code:</span></span>  

1. <span data-ttu-id="2318e-178">尋找並拖曳 hello[執行 R 指令碼][ execute-r-script] hello 實驗畫布的模組。</span><span class="sxs-lookup"><span data-stu-id="2318e-178">Find and drag hello [Execute R Script][execute-r-script] module onto hello experiment canvas.</span></span> 

2. <span data-ttu-id="2318e-179">連接保留 hello 輸出連接埠的 hello[分割資料][ split]模組 toohello 的第一個輸入連接埠 (「 Dataset1") 的 hello[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="2318e-179">Connect hello left output port of hello [Split Data][split] module toohello first input port ("Dataset1") of hello [Execute R Script][execute-r-script] module.</span></span>

3. <span data-ttu-id="2318e-180">按兩下 hello[執行 R 指令碼][ execute-r-script]模組，然後輸入 hello 註解，「 成本調整集 」。</span><span class="sxs-lookup"><span data-stu-id="2318e-180">Double-click hello [Execute R Script][execute-r-script] module and enter hello comment, "Set cost adjustment".</span></span>

4. <span data-ttu-id="2318e-181">在 hello**屬性** 窗格中，刪除 hello 預設文字在 hello **R 指令碼**參數，並輸入此指令碼：</span><span class="sxs-lookup"><span data-stu-id="2318e-181">In hello **Properties** pane, delete hello default text in hello **R Script** parameter and enter this script:</span></span>
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![Hello 執行 R 指令碼模組中的 R 指令碼][9]

<span data-ttu-id="2318e-183">我們需要此相同的複寫作業每個輸出的 hello toodo[分割資料][ split]模組，因此該 hello 定型集和測試資料有 hello 相同成本的調整。</span><span class="sxs-lookup"><span data-stu-id="2318e-183">We need toodo this same replication operation for each output of hello [Split Data][split] module so that hello training and testing data have hello same cost adjustment.</span></span> <span data-ttu-id="2318e-184">hello 最簡單的方式 toodo，這是透過複製 hello[執行 R 指令碼][ execute-r-script]模組我們剛才和其他連接 toohello 輸出連接埠 hello[分割資料][split]模組。</span><span class="sxs-lookup"><span data-stu-id="2318e-184">hello easiest way toodo this is by duplicating hello [Execute R Script][execute-r-script] module we just made and connecting it toohello other output port of hello [Split Data][split] module.</span></span>

1. <span data-ttu-id="2318e-185">以滑鼠右鍵按一下 hello[執行 R 指令碼][ execute-r-script]模組，然後選取**複製**。</span><span class="sxs-lookup"><span data-stu-id="2318e-185">Right-click hello [Execute R Script][execute-r-script] module and select **Copy**.</span></span>

2. <span data-ttu-id="2318e-186">以滑鼠右鍵按一下 hello 實驗畫布，然後選取**貼上**。</span><span class="sxs-lookup"><span data-stu-id="2318e-186">Right-click hello experiment canvas and select **Paste**.</span></span>

3. <span data-ttu-id="2318e-187">將 hello 新模組進入位置，然後再將連接 hello hello 右輸出連接埠[分割資料][ split]模組 toohello 的第一個輸入連接埠，這個新[執行 R 指令碼][execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="2318e-187">Drag hello new module into position, and then connect hello right output port of hello [Split Data][split] module toohello first input port of this new [Execute R Script][execute-r-script] module.</span></span> 

4. <span data-ttu-id="2318e-188">在 hello hello 畫布底部，按一下 **執行**。</span><span class="sxs-lookup"><span data-stu-id="2318e-188">At hello bottom of hello canvas, click **Run**.</span></span> 

> [!TIP]
> <span data-ttu-id="2318e-189">hello 複本 hello 執行 R 指令碼模組包含的 hello 相同以 hello 原始模組的指令碼。</span><span class="sxs-lookup"><span data-stu-id="2318e-189">hello copy of hello Execute R Script module contains hello same script as hello original module.</span></span> <span data-ttu-id="2318e-190">當您複製並貼上 hello 畫布上的模組時，hello 複製會保留原始 hello 所有 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="2318e-190">When you copy and paste a module on hello canvas, hello copy retains all hello properties of hello original.</span></span>  
> 
> 

<span data-ttu-id="2318e-191">實驗此時看起來會如下所示：</span><span class="sxs-lookup"><span data-stu-id="2318e-191">Our experiment now looks something like this:</span></span>

![Adding Split module and R scripts][4]

<span data-ttu-id="2318e-193">如需如何在您的實驗中使用 R 指令碼的詳細資訊，請參閱 [透過 R 擴充您的實驗](machine-learning-extend-your-experiment-with-r.md)。</span><span class="sxs-lookup"><span data-stu-id="2318e-193">For more information on using R scripts in your experiments, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md).</span></span>

<span data-ttu-id="2318e-194">**下一步:[定型和評估 hello 模型](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span><span class="sxs-lookup"><span data-stu-id="2318e-194">**Next: [Train and evaluate hello models](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span></span>

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
