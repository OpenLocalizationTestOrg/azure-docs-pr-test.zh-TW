---
title: "步驟 2：將資料上傳至 Machine Learning 實驗中 | Microsoft Docs"
description: "開發預測解決方案逐步解說步驟 2：將儲存的公用資料上傳至 Azure Machine Learning Studio 中。"
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
ms.openlocfilehash: c2ab5f5252e1ea1ec51f6c3bd489826c70ff011c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a><span data-ttu-id="bee7b-103">逐步解說步驟 2：將現有資料上傳至 Azure Machine Learning 實驗中</span><span class="sxs-lookup"><span data-stu-id="bee7b-103">Walkthrough Step 2: Upload existing data into an Azure Machine Learning experiment</span></span>
<span data-ttu-id="bee7b-104">這是 [在 Azure Machine Learning 中為信用風險評估開發預測性分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="bee7b-104">This is the second step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="bee7b-105">建立機器學習服務工作區</span><span class="sxs-lookup"><span data-stu-id="bee7b-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. <span data-ttu-id="bee7b-106">**上傳現有資料**</span><span class="sxs-lookup"><span data-stu-id="bee7b-106">**Upload existing data**</span></span>
3. [<span data-ttu-id="bee7b-107">建立新實驗</span><span class="sxs-lookup"><span data-stu-id="bee7b-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="bee7b-108">訓練及評估模型</span><span class="sxs-lookup"><span data-stu-id="bee7b-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="bee7b-109">部署 Web 服務</span><span class="sxs-lookup"><span data-stu-id="bee7b-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="bee7b-110">存取 Web 服務</span><span class="sxs-lookup"><span data-stu-id="bee7b-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="bee7b-111">為了開發信用風險的預測模型，我們需要可以用於訓練和測試模型的資料。</span><span class="sxs-lookup"><span data-stu-id="bee7b-111">To develop a predictive model for credit risk, we need data that we can use to train and then test the model.</span></span> <span data-ttu-id="bee7b-112">針對此逐步教學，我們將使用 UCI Irvine Machine Learning Repository 中的「UCI Statlog (德國信用資料) 資料集」。</span><span class="sxs-lookup"><span data-stu-id="bee7b-112">For this walkthrough, we'll use the "UCI Statlog (German Credit Data) Data Set" from the UC Irvine Machine Learning repository.</span></span> <span data-ttu-id="bee7b-113">您可以在下列位置找到此儲存機制：</span><span class="sxs-lookup"><span data-stu-id="bee7b-113">You can find it here:</span></span>  
<span data-ttu-id="bee7b-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span><span class="sxs-lookup"><span data-stu-id="bee7b-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span></span>

<span data-ttu-id="bee7b-115">您可以使用名為 **german.data**的檔案。</span><span class="sxs-lookup"><span data-stu-id="bee7b-115">We'll use the file named **german.data**.</span></span> <span data-ttu-id="bee7b-116">將此檔案下載至您的本機硬碟。</span><span class="sxs-lookup"><span data-stu-id="bee7b-116">Download this file to your local hard drive.</span></span>  

<span data-ttu-id="bee7b-117">**german.data** 資料集包含過去 1000 名信用額度申請者的 20 個變數資料列。</span><span class="sxs-lookup"><span data-stu-id="bee7b-117">The **german.data** dataset contains rows of 20 variables for 1000 past applicants for credit.</span></span> <span data-ttu-id="bee7b-118">這 20 個變數代表資料集的特徵集 (「特徵向量」)，可分別提供每個信用額度申請者的識別特性。</span><span class="sxs-lookup"><span data-stu-id="bee7b-118">These 20 variables represent the dataset's set of features (the *feature vector*), which provides identifying characteristics for each credit applicant.</span></span> <span data-ttu-id="bee7b-119">每個資料列另外會有一個資料行代表申請者計算後的信用風險，其中有 700 名申請者被認定為低信用風險，300 名為高風險。</span><span class="sxs-lookup"><span data-stu-id="bee7b-119">An additional column in each row represents the applicant's calculated credit risk, with 700 applicants identified as a low credit risk and 300 as a high risk.</span></span>

<span data-ttu-id="bee7b-120">UCI 網站提供了這項資料的特徵向量的屬性描述。</span><span class="sxs-lookup"><span data-stu-id="bee7b-120">The UCI website provides a description of the attributes of the feature vector for this data.</span></span> <span data-ttu-id="bee7b-121">包括財務資訊、信用歷史記錄、工作狀態、個人資訊。</span><span class="sxs-lookup"><span data-stu-id="bee7b-121">This includes financial information, credit history, employment status, and personal information.</span></span> <span data-ttu-id="bee7b-122">每個申請者都會有一個二進位評等，指出他們屬於低信用風險還是高風險。</span><span class="sxs-lookup"><span data-stu-id="bee7b-122">For each applicant, a binary rating has been given indicating whether they are a low or high credit risk.</span></span> 

<span data-ttu-id="bee7b-123">我們將使用這項資料來訓練預測分析模型。</span><span class="sxs-lookup"><span data-stu-id="bee7b-123">We'll use this data to train a predictive analytics model.</span></span> <span data-ttu-id="bee7b-124">完成之後，我們的模型應能夠接受新申請者的特徵向量，並預測他或她是屬於低信用風險還是高風險。</span><span class="sxs-lookup"><span data-stu-id="bee7b-124">When we're done, our model should be able to accept a feature vector for a new individual and predict whether he or she is a low or high credit risk.</span></span>  

<span data-ttu-id="bee7b-125">以下提供一個有趣的論點。</span><span class="sxs-lookup"><span data-stu-id="bee7b-125">Here's an interesting twist.</span></span> <span data-ttu-id="bee7b-126">UCI 網站上的資料集描述提及，如果我們錯誤分類一個人的信用風險需付出何種代價。</span><span class="sxs-lookup"><span data-stu-id="bee7b-126">The description of the dataset on the UCI website mentions what it costs if we misclassify a person's credit risk.</span></span>
<span data-ttu-id="bee7b-127">如果模型將某個實際為低信用風險的人預測為高信用風險，則此模型做了錯誤分類。</span><span class="sxs-lookup"><span data-stu-id="bee7b-127">If the model predicts a high credit risk for someone who is actually a low credit risk, the model has made a misclassification.</span></span>
<span data-ttu-id="bee7b-128">但反向的錯誤分類對金融機構而言需要付出五倍的代價：如果模型將某個實際為高信用風險的人預測為低信用風險。</span><span class="sxs-lookup"><span data-stu-id="bee7b-128">But the reverse misclassification is five times more costly to the financial institution: if the model predicts a low credit risk for someone who is actually a high credit risk.</span></span>

<span data-ttu-id="bee7b-129">因此，我們想要訓練模型，讓後者的這一個錯誤分類類型的成本比另一種錯誤分類方式高出五倍。</span><span class="sxs-lookup"><span data-stu-id="bee7b-129">So, we want to train our model so that the cost of this latter type of misclassification is five times higher than misclassifying the other way.</span></span>
<span data-ttu-id="bee7b-130">在我們的實驗中，在訓練模型時執行此動作的一個簡單方式是，複製 (五次) 那些代表某個具有高信用風險之人員的項目。</span><span class="sxs-lookup"><span data-stu-id="bee7b-130">One simple way to do this when training the model in our experiment is by duplicating (five times) those entries that represent someone with a high credit risk.</span></span> <span data-ttu-id="bee7b-131">然後，如果模型將某人錯誤分類為低信用風險，但他們實際為高風險時，模型即會會進行該相同錯誤分類五次，針對每個重複項目進行一次。</span><span class="sxs-lookup"><span data-stu-id="bee7b-131">Then, if the model misclassifies someone as a low credit risk when they're actually a high risk, the model does that same misclassification five times, once for each duplicate.</span></span> <span data-ttu-id="bee7b-132">這會在訓練結果中增加此誤差的成本。</span><span class="sxs-lookup"><span data-stu-id="bee7b-132">This will increase the cost of this error in the training results.</span></span>


## <a name="convert-the-dataset-format"></a><span data-ttu-id="bee7b-133">轉換資料集格式</span><span class="sxs-lookup"><span data-stu-id="bee7b-133">Convert the dataset format</span></span>
<span data-ttu-id="bee7b-134">原始資料集使用以空格分隔的格式。</span><span class="sxs-lookup"><span data-stu-id="bee7b-134">The original dataset uses a blank-separated format.</span></span> <span data-ttu-id="bee7b-135">Machine Learning Studio 在使用逗號分隔值 (CSV) 檔案時更能適當運作，因此我們將以逗號取代空格，進行資料集轉換。</span><span class="sxs-lookup"><span data-stu-id="bee7b-135">Machine Learning Studio works better with a comma-separated value (CSV) file, so we'll convert the dataset by replacing spaces with commas.</span></span>  

<span data-ttu-id="bee7b-136">有許多方法可以轉換此資料。</span><span class="sxs-lookup"><span data-stu-id="bee7b-136">There are many ways to convert this data.</span></span> <span data-ttu-id="bee7b-137">其中一種是使用下列的 Windows PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="bee7b-137">One way is by using the following Windows PowerShell command:</span></span>   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

<span data-ttu-id="bee7b-138">另一種方法是使用 Unix Sed 命令：</span><span class="sxs-lookup"><span data-stu-id="bee7b-138">Another way is by using the Unix sed command:</span></span>  

    sed 's/ /,/g' german.data > german.csv  

<span data-ttu-id="bee7b-139">在任一案例中，我們已經以名為 **german.csv** 的檔案建立逗號分隔版本的資料，可在我們的實驗中加以使用。</span><span class="sxs-lookup"><span data-stu-id="bee7b-139">In either case, we have created a comma-separated version of the data in a file named **german.csv** that we can use in our experiment.</span></span>

## <a name="upload-the-dataset-to-machine-learning-studio"></a><span data-ttu-id="bee7b-140">將資料集上傳至 Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="bee7b-140">Upload the dataset to Machine Learning Studio</span></span>
<span data-ttu-id="bee7b-141">在資料轉換為 CSV 格式後，我們必須將其上傳至 Machine Learning Studio 中。</span><span class="sxs-lookup"><span data-stu-id="bee7b-141">Once the data has been converted to CSV format, we need to upload it into Machine Learning Studio.</span></span> 

1. <span data-ttu-id="bee7b-142">開啟 Machine Learning Studio 首頁 ([https://studio.azureml.net/Home](https://studio.azureml.net))。</span><span class="sxs-lookup"><span data-stu-id="bee7b-142">Open the Machine Learning Studio home page ([https://studio.azureml.net](https://studio.azureml.net)).</span></span> 

2. <span data-ttu-id="bee7b-143">按一下視窗左上角的功能表![功能表][1]，按一下 [Azure Machine Learning]，選取 [Studio] 然後登入。</span><span class="sxs-lookup"><span data-stu-id="bee7b-143">Click the menu ![Menu][1] in the upper-left corner of the window, click **Azure Machine Learning**, select **Studio**, and sign in.</span></span>

3. <span data-ttu-id="bee7b-144">按一下視窗底部的 [ **+新增** ]。</span><span class="sxs-lookup"><span data-stu-id="bee7b-144">Click **+NEW** at the bottom of the window.</span></span>

4. <span data-ttu-id="bee7b-145">選取 [ **資料集**]。</span><span class="sxs-lookup"><span data-stu-id="bee7b-145">Select **DATASET**.</span></span>

5. <span data-ttu-id="bee7b-146">選取 [ **從本機檔案**]。</span><span class="sxs-lookup"><span data-stu-id="bee7b-146">Select **FROM LOCAL FILE**.</span></span>

    ![從本機檔案新增資料集][2]

6. <span data-ttu-id="bee7b-148">在 [上傳新的資料集] 對話方塊中，按一下 [瀏覽]，然後尋找您建立的 **german.csv** 檔案。</span><span class="sxs-lookup"><span data-stu-id="bee7b-148">In the **Upload a new dataset** dialog, click **Browse** and find the **german.csv** file you created.</span></span>

7. <span data-ttu-id="bee7b-149">輸入資料集的名稱。</span><span class="sxs-lookup"><span data-stu-id="bee7b-149">Enter a name for the dataset.</span></span> <span data-ttu-id="bee7b-150">在此逐步解說中，將它稱為 "UCI German Credit Card Data"。</span><span class="sxs-lookup"><span data-stu-id="bee7b-150">For this walkthrough, call it "UCI German Credit Card Data".</span></span>

8. <span data-ttu-id="bee7b-151">針對資料類型，請選取 **不具標頭的一般 CSV 檔案 (.nh.csv)**。</span><span class="sxs-lookup"><span data-stu-id="bee7b-151">For data type, select **Generic CSV File With no header (.nh.csv)**.</span></span>

9. <span data-ttu-id="bee7b-152">視需要新增說明。</span><span class="sxs-lookup"><span data-stu-id="bee7b-152">Add a description if you’d like.</span></span>

10. <span data-ttu-id="bee7b-153">按一下 **[確定]** \(打勾記號)。</span><span class="sxs-lookup"><span data-stu-id="bee7b-153">Click the **OK** check mark.</span></span>  

    ![上傳資料集][3]

<span data-ttu-id="bee7b-155">這會將資料上傳至我們可在實驗中使用的資料集模組。</span><span class="sxs-lookup"><span data-stu-id="bee7b-155">This uploads the data into a dataset module that we can use in an experiment.</span></span>

<span data-ttu-id="bee7b-156">您可以管理您已上傳至 Studio 的資料集，請按一下 Studio 視窗左側的 [資料集] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="bee7b-156">You can manage datasets that you've uploaded to Studio by clicking the **DATASETS** tab to the left of the Studio window.</span></span>

![管理資料集][4]

<span data-ttu-id="bee7b-158">如需將其他種資料類型匯入實驗的詳細資訊，請參閱[將訓練資料匯入 Azure Machine Learning Studio](machine-learning-data-science-import-data.md)。</span><span class="sxs-lookup"><span data-stu-id="bee7b-158">For more information about importing other types of data into an experiment, see [Import your training data into Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span></span>

<span data-ttu-id="bee7b-159">**下一步：[建立新實驗](machine-learning-walkthrough-3-create-new-experiment.md)**</span><span class="sxs-lookup"><span data-stu-id="bee7b-159">**Next: [Create a new experiment](machine-learning-walkthrough-3-create-new-experiment.md)**</span></span>

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
