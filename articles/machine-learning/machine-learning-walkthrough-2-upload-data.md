---
title: "步驟 2：將資料上傳至 Machine Learning 實驗中 | Microsoft Docs"
description: "步驟 2 中的 hello 開發預測方案逐步解說： 上傳到 Azure Machine Learning Studio 中儲存公用資料。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 0ea21dcca2d0934ed06508560cf85cf31b48ce6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a><span data-ttu-id="cce6c-103">逐步解說步驟 2：將現有資料上傳至 Azure Machine Learning 實驗中</span><span class="sxs-lookup"><span data-stu-id="cce6c-103">Walkthrough Step 2: Upload existing data into an Azure Machine Learning experiment</span></span>
<span data-ttu-id="cce6c-104">這是 hello hello 逐步解說中，第二個步驟[開發 Azure Machine Learning 中的預測分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="cce6c-104">This is hello second step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="cce6c-105">建立機器學習服務工作區</span><span class="sxs-lookup"><span data-stu-id="cce6c-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. <span data-ttu-id="cce6c-106">**上傳現有資料**</span><span class="sxs-lookup"><span data-stu-id="cce6c-106">**Upload existing data**</span></span>
3. [<span data-ttu-id="cce6c-107">建立新實驗</span><span class="sxs-lookup"><span data-stu-id="cce6c-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="cce6c-108">來定型及評估 hello 模型</span><span class="sxs-lookup"><span data-stu-id="cce6c-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="cce6c-109">部署 hello Web 服務</span><span class="sxs-lookup"><span data-stu-id="cce6c-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="cce6c-110">存取 hello Web 服務</span><span class="sxs-lookup"><span data-stu-id="cce6c-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="cce6c-111">toodevelop 信用風險的預測模型，我們需要的資料，我們可以使用 tootrain 並接著測試 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="cce6c-111">toodevelop a predictive model for credit risk, we need data that we can use tootrain and then test hello model.</span></span> <span data-ttu-id="cce6c-112">本逐步解說，我們將從 hello UC Irvine 機器學習儲存機制使用 hello 「 UCI Statlog （德文信用卡資料） 的資料集 」。</span><span class="sxs-lookup"><span data-stu-id="cce6c-112">For this walkthrough, we'll use hello "UCI Statlog (German Credit Data) Data Set" from hello UC Irvine Machine Learning repository.</span></span> <span data-ttu-id="cce6c-113">您可以在下列位置找到此儲存機制：</span><span class="sxs-lookup"><span data-stu-id="cce6c-113">You can find it here:</span></span>  
<span data-ttu-id="cce6c-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span><span class="sxs-lookup"><span data-stu-id="cce6c-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span></span>

<span data-ttu-id="cce6c-115">我們會使用名為 「 hello 檔案**german.data**。</span><span class="sxs-lookup"><span data-stu-id="cce6c-115">We'll use hello file named **german.data**.</span></span> <span data-ttu-id="cce6c-116">下載這個檔案 tooyour 本機硬碟。</span><span class="sxs-lookup"><span data-stu-id="cce6c-116">Download this file tooyour local hard drive.</span></span>  

<span data-ttu-id="cce6c-117">hello **german.data**資料集包含資料列的 20 變數的信用額度 1000年過去的履歷表。</span><span class="sxs-lookup"><span data-stu-id="cce6c-117">hello **german.data** dataset contains rows of 20 variables for 1000 past applicants for credit.</span></span> <span data-ttu-id="cce6c-118">這些 20 變數代表 hello 資料集的功能 (hello*特徵向量*)，可提供每個剩餘的信用應徵者的識別特性。</span><span class="sxs-lookup"><span data-stu-id="cce6c-118">These 20 variables represent hello dataset's set of features (hello *feature vector*), which provides identifying characteristics for each credit applicant.</span></span> <span data-ttu-id="cce6c-119">每個資料列中的其他資料行代表 hello 申請者的導出的信用風險，700 低信用風險和 300 視為高風險的履歷表。</span><span class="sxs-lookup"><span data-stu-id="cce6c-119">An additional column in each row represents hello applicant's calculated credit risk, with 700 applicants identified as a low credit risk and 300 as a high risk.</span></span>

<span data-ttu-id="cce6c-120">hello UCI 網站提供的這項資料的 hello 特徵向量 hello 屬性的描述。</span><span class="sxs-lookup"><span data-stu-id="cce6c-120">hello UCI website provides a description of hello attributes of hello feature vector for this data.</span></span> <span data-ttu-id="cce6c-121">包括財務資訊、信用歷史記錄、工作狀態、個人資訊。</span><span class="sxs-lookup"><span data-stu-id="cce6c-121">This includes financial information, credit history, employment status, and personal information.</span></span> <span data-ttu-id="cce6c-122">每個申請者都會有一個二進位評等，指出他們屬於低信用風險還是高風險。</span><span class="sxs-lookup"><span data-stu-id="cce6c-122">For each applicant, a binary rating has been given indicating whether they are a low or high credit risk.</span></span> 

<span data-ttu-id="cce6c-123">我們將使用此資料 tootrain 預測分析模型。</span><span class="sxs-lookup"><span data-stu-id="cce6c-123">We'll use this data tootrain a predictive analytics model.</span></span> <span data-ttu-id="cce6c-124">當我們完成時，我們的模型中要能 tooaccept 特徵向量的新的人員，而且預測他或她是低或高信用風險。</span><span class="sxs-lookup"><span data-stu-id="cce6c-124">When we're done, our model should be able tooaccept a feature vector for a new individual and predict whether he or she is a low or high credit risk.</span></span>  

<span data-ttu-id="cce6c-125">以下提供一個有趣的論點。</span><span class="sxs-lookup"><span data-stu-id="cce6c-125">Here's an interesting twist.</span></span> <span data-ttu-id="cce6c-126">hello hello hello UCI 網站提及上的資料集的描述項目成本如果我們 misclassify 人員的信用風險。</span><span class="sxs-lookup"><span data-stu-id="cce6c-126">hello description of hello dataset on hello UCI website mentions what it costs if we misclassify a person's credit risk.</span></span>
<span data-ttu-id="cce6c-127">如果 hello 模型預測高信用風險的實際低信用風險的人，hello 模型所做的錯誤分類。</span><span class="sxs-lookup"><span data-stu-id="cce6c-127">If hello model predicts a high credit risk for someone who is actually a low credit risk, hello model has made a misclassification.</span></span>
<span data-ttu-id="cce6c-128">但 hello 反向錯誤分類成本五次更高的 toohello 金融機構： 如果 hello 模型預測的人真的高信用風險低信用風險。</span><span class="sxs-lookup"><span data-stu-id="cce6c-128">But hello reverse misclassification is five times more costly toohello financial institution: if hello model predicts a low credit risk for someone who is actually a high credit risk.</span></span>

<span data-ttu-id="cce6c-129">因此，我們想要 tootrain 我們的模型如此 hello 這個第二個類型的錯誤分類成本高於五次 hello 另一種方式將錯誤分類。</span><span class="sxs-lookup"><span data-stu-id="cce6c-129">So, we want tootrain our model so that hello cost of this latter type of misclassification is five times higher than misclassifying hello other way.</span></span>
<span data-ttu-id="cce6c-130">一個簡單的方式 toodo 這在我們的實驗中的 hello 模型定型時複製 （五次） 的項目代表具有高信用風險。</span><span class="sxs-lookup"><span data-stu-id="cce6c-130">One simple way toodo this when training hello model in our experiment is by duplicating (five times) those entries that represent someone with a high credit risk.</span></span> <span data-ttu-id="cce6c-131">然後，如果 hello 模型利用人為低信用風險它們實際上是較高的風險時，hello 模型會該相同的錯誤分類五次，一次為每個重複項目。</span><span class="sxs-lookup"><span data-stu-id="cce6c-131">Then, if hello model misclassifies someone as a low credit risk when they're actually a high risk, hello model does that same misclassification five times, once for each duplicate.</span></span> <span data-ttu-id="cce6c-132">這將會增加 hello 成本 hello 訓練結果中的這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="cce6c-132">This will increase hello cost of this error in hello training results.</span></span>


## <a name="convert-hello-dataset-format"></a><span data-ttu-id="cce6c-133">轉換 hello 資料集格式</span><span class="sxs-lookup"><span data-stu-id="cce6c-133">Convert hello dataset format</span></span>
<span data-ttu-id="cce6c-134">hello 原始資料集使用空白分隔的格式。</span><span class="sxs-lookup"><span data-stu-id="cce6c-134">hello original dataset uses a blank-separated format.</span></span> <span data-ttu-id="cce6c-135">Machine Learning Studio 較適用於以逗號分隔值 (CSV) 檔案，所以我們會使用逗號來取代空格轉換 hello 資料集。</span><span class="sxs-lookup"><span data-stu-id="cce6c-135">Machine Learning Studio works better with a comma-separated value (CSV) file, so we'll convert hello dataset by replacing spaces with commas.</span></span>  

<span data-ttu-id="cce6c-136">有許多方式 tooconvert 這項資料。</span><span class="sxs-lookup"><span data-stu-id="cce6c-136">There are many ways tooconvert this data.</span></span> <span data-ttu-id="cce6c-137">其中一種方式是使用下列 Windows PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="cce6c-137">One way is by using hello following Windows PowerShell command:</span></span>   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

<span data-ttu-id="cce6c-138">另一種方式是使用 hello Unix sed 命令：</span><span class="sxs-lookup"><span data-stu-id="cce6c-138">Another way is by using hello Unix sed command:</span></span>  

    sed 's/ /,/g' german.data > german.csv  

<span data-ttu-id="cce6c-139">在任一情況下，我們建立了名為的檔案中的 hello 資料的逗號分隔版本**german.csv**我們可以在我們的實驗中使用。</span><span class="sxs-lookup"><span data-stu-id="cce6c-139">In either case, we have created a comma-separated version of hello data in a file named **german.csv** that we can use in our experiment.</span></span>

## <a name="upload-hello-dataset-toomachine-learning-studio"></a><span data-ttu-id="cce6c-140">上傳 hello 資料集 tooMachine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="cce6c-140">Upload hello dataset tooMachine Learning Studio</span></span>
<span data-ttu-id="cce6c-141">一旦 hello 資料已轉換的 tooCSV 格式，我們需要 tooupload 到 Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="cce6c-141">Once hello data has been converted tooCSV format, we need tooupload it into Machine Learning Studio.</span></span> 

1. <span data-ttu-id="cce6c-142">開啟 hello Machine Learning Studio 首頁 ([https://studio.azureml.net](https://studio.azureml.net))。</span><span class="sxs-lookup"><span data-stu-id="cce6c-142">Open hello Machine Learning Studio home page ([https://studio.azureml.net](https://studio.azureml.net)).</span></span> 

2. <span data-ttu-id="cce6c-143">按一下 [hello] 功能表![功能表][1]在 hello hello 視窗的左上角，按一下**Azure Machine Learning**，選取**Studio**，並登入。</span><span class="sxs-lookup"><span data-stu-id="cce6c-143">Click hello menu ![Menu][1] in hello upper-left corner of hello window, click **Azure Machine Learning**, select **Studio**, and sign in.</span></span>

3. <span data-ttu-id="cce6c-144">按一下**+ 新增**在 hello hello 視窗的底部。</span><span class="sxs-lookup"><span data-stu-id="cce6c-144">Click **+NEW** at hello bottom of hello window.</span></span>

4. <span data-ttu-id="cce6c-145">選取 [ **資料集**]。</span><span class="sxs-lookup"><span data-stu-id="cce6c-145">Select **DATASET**.</span></span>

5. <span data-ttu-id="cce6c-146">選取 [ **從本機檔案**]。</span><span class="sxs-lookup"><span data-stu-id="cce6c-146">Select **FROM LOCAL FILE**.</span></span>

    ![從本機檔案新增資料集][2]

6. <span data-ttu-id="cce6c-148">在 hello**上傳新的資料集**] 對話方塊中，按一下 [**瀏覽**並尋找 hello **german.csv**您建立的檔案。</span><span class="sxs-lookup"><span data-stu-id="cce6c-148">In hello **Upload a new dataset** dialog, click **Browse** and find hello **german.csv** file you created.</span></span>

7. <span data-ttu-id="cce6c-149">輸入 hello 資料集的名稱。</span><span class="sxs-lookup"><span data-stu-id="cce6c-149">Enter a name for hello dataset.</span></span> <span data-ttu-id="cce6c-150">在此逐步解說中，將它稱為 "UCI German Credit Card Data"。</span><span class="sxs-lookup"><span data-stu-id="cce6c-150">For this walkthrough, call it "UCI German Credit Card Data".</span></span>

8. <span data-ttu-id="cce6c-151">針對資料類型，請選取 **不具標頭的一般 CSV 檔案 (.nh.csv)**。</span><span class="sxs-lookup"><span data-stu-id="cce6c-151">For data type, select **Generic CSV File With no header (.nh.csv)**.</span></span>

9. <span data-ttu-id="cce6c-152">視需要新增說明。</span><span class="sxs-lookup"><span data-stu-id="cce6c-152">Add a description if you’d like.</span></span>

10. <span data-ttu-id="cce6c-153">按一下 hello**確定**核取記號。</span><span class="sxs-lookup"><span data-stu-id="cce6c-153">Click hello **OK** check mark.</span></span>  

    ![上傳 hello 資料集][3]

<span data-ttu-id="cce6c-155">這將 hello 資料上傳至我們可以在實驗中使用的資料集模組。</span><span class="sxs-lookup"><span data-stu-id="cce6c-155">This uploads hello data into a dataset module that we can use in an experiment.</span></span>

<span data-ttu-id="cce6c-156">您可以管理資料集，您已按一下 hello 上載 tooStudio**資料集** 索引標籤 toohello 方 hello Studio 視窗。</span><span class="sxs-lookup"><span data-stu-id="cce6c-156">You can manage datasets that you've uploaded tooStudio by clicking hello **DATASETS** tab toohello left of hello Studio window.</span></span>

![管理資料集][4]

<span data-ttu-id="cce6c-158">如需將其他種資料類型匯入實驗的詳細資訊，請參閱[將訓練資料匯入 Azure Machine Learning Studio](machine-learning-data-science-import-data.md)。</span><span class="sxs-lookup"><span data-stu-id="cce6c-158">For more information about importing other types of data into an experiment, see [Import your training data into Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span></span>

<span data-ttu-id="cce6c-159">**下一步：[建立新實驗](machine-learning-walkthrough-3-create-new-experiment.md)**</span><span class="sxs-lookup"><span data-stu-id="cce6c-159">**Next: [Create a new experiment](machine-learning-walkthrough-3-create-new-experiment.md)**</span></span>

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
