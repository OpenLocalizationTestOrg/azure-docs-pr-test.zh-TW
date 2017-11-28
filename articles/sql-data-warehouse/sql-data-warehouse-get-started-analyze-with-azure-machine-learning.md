---
title: "與 Azure Machine Learning aaaAnalyze 資料 |Microsoft 文件"
description: "使用 Azure 機器學習 toobuild 預測機器學習模型根據儲存在 Azure SQL 資料倉儲中的資料。"
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 337a2cd77aaad4467683827c56e5015b262b2554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a><span data-ttu-id="bae85-103">使用 Azure Machine Learning 分析資料</span><span class="sxs-lookup"><span data-stu-id="bae85-103">Analyze data with Azure Machine Learning</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bae85-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="bae85-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="bae85-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="bae85-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="bae85-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bae85-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="bae85-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="bae85-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="bae85-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="bae85-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="bae85-109">本教學課程使用 Azure 機器學習 toobuild 預測機器學習模型根據儲存在 Azure SQL 資料倉儲中的資料。</span><span class="sxs-lookup"><span data-stu-id="bae85-109">This tutorial uses Azure Machine Learning toobuild a predictive machine learning model based on data stored in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="bae85-110">具體而言，這會建置目標的行銷活動的 hello 自行車購買 Adventure Works，由預測如果客戶可能 toobuy 自行車。</span><span class="sxs-lookup"><span data-stu-id="bae85-110">Specifically, this builds a targeted marketing campaign for Adventure Works, hello bike shop, by predicting if a customer is likely toobuy a bike or not.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="bae85-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="bae85-111">Prerequisites</span></span>
<span data-ttu-id="bae85-112">在本教學課程 toostep，您需要：</span><span class="sxs-lookup"><span data-stu-id="bae85-112">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="bae85-113">預先載入 AdventureWorksDW 範例資料的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="bae85-113">A SQL Data Warehouse pre-loaded with AdventureWorksDW sample data.</span></span> <span data-ttu-id="bae85-114">tooprovision，請參閱[建立 SQL 資料倉儲][ Create a SQL Data Warehouse]選擇 tooload hello 範例資料。</span><span class="sxs-lookup"><span data-stu-id="bae85-114">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="bae85-115">如果您已經有資料倉儲但沒有範例資料，您可以[手動載入範例資料][load sample data manually]。</span><span class="sxs-lookup"><span data-stu-id="bae85-115">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-get-hello-data"></a><span data-ttu-id="bae85-116">1.取得 hello 資料</span><span class="sxs-lookup"><span data-stu-id="bae85-116">1. Get hello data</span></span>
<span data-ttu-id="bae85-117">hello 資料是在 hello AdventureWorksDW 資料庫中的 hello dbo.vTargetMail 檢視。</span><span class="sxs-lookup"><span data-stu-id="bae85-117">hello data is in hello dbo.vTargetMail view in hello AdventureWorksDW database.</span></span> <span data-ttu-id="bae85-118">tooread 這項資料：</span><span class="sxs-lookup"><span data-stu-id="bae85-118">tooread this data:</span></span>

1. <span data-ttu-id="bae85-119">登入 [Azure Machine Learning Studio][Azure Machine Learning studio] 並按一下我的實驗。</span><span class="sxs-lookup"><span data-stu-id="bae85-119">Sign into [Azure Machine Learning studio][Azure Machine Learning studio] and click on my experiments.</span></span>
2. <span data-ttu-id="bae85-120">按一下 [+ 新增] 並選取 [空白實驗]。</span><span class="sxs-lookup"><span data-stu-id="bae85-120">Click **+NEW** and select **Blank Experiment**.</span></span>
3. <span data-ttu-id="bae85-121">輸入您的實驗名稱：目標行銷。</span><span class="sxs-lookup"><span data-stu-id="bae85-121">Enter a name for your experiment: Targeted Marketing.</span></span>
4. <span data-ttu-id="bae85-122">拖曳 hello**讀取器**從 hello 模組窗格將 hello 畫布的模組。</span><span class="sxs-lookup"><span data-stu-id="bae85-122">Drag hello **Reader** module from hello modules pane into hello canvas.</span></span>
5. <span data-ttu-id="bae85-123">Hello 屬性 窗格中指定 SQL 資料倉儲資料庫的 hello 詳細的資料。</span><span class="sxs-lookup"><span data-stu-id="bae85-123">Specify hello details of your SQL Data Warehouse database in hello Properties pane.</span></span>
6. <span data-ttu-id="bae85-124">指定 hello 資料庫**查詢**感興趣的 tooread hello 資料。</span><span class="sxs-lookup"><span data-stu-id="bae85-124">Specify hello database **query** tooread hello data of interest.</span></span>

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

<span data-ttu-id="bae85-125">按一下以執行 hello 實驗**執行**下 hello 實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="bae85-125">Run hello experiment by clicking **Run** under hello experiment canvas.</span></span>
<span data-ttu-id="bae85-126">![執行 hello 實驗][1]</span><span class="sxs-lookup"><span data-stu-id="bae85-126">![Run hello experiment][1]</span></span>

<span data-ttu-id="bae85-127">Hello 實驗順利地完成執行之後，按一下 hello 底部 hello hello 讀取器模組的輸出連接埠，然後選取 **視覺化**toosee hello 匯入資料。</span><span class="sxs-lookup"><span data-stu-id="bae85-127">After hello experiment finishes running successfully, click hello output port at hello bottom of hello Reader module and select **Visualize** toosee hello imported data.</span></span>
<span data-ttu-id="bae85-128">![檢視匯入的資料][3]</span><span class="sxs-lookup"><span data-stu-id="bae85-128">![View imported data][3]</span></span>

## <a name="2-clean-hello-data"></a><span data-ttu-id="bae85-129">2.全新的 hello 資料</span><span class="sxs-lookup"><span data-stu-id="bae85-129">2. Clean hello data</span></span>
<span data-ttu-id="bae85-130">tooclean hello 資料、 卸除某些不相關的 hello 模型的資料行。</span><span class="sxs-lookup"><span data-stu-id="bae85-130">tooclean hello data, drop some columns that are not relevant for hello model.</span></span> <span data-ttu-id="bae85-131">toodo 這樣：</span><span class="sxs-lookup"><span data-stu-id="bae85-131">toodo this:</span></span>

1. <span data-ttu-id="bae85-132">拖曳 hello**投射資料行**hello 畫布模組。</span><span class="sxs-lookup"><span data-stu-id="bae85-132">Drag hello **Project Columns** module into hello canvas.</span></span>
2. <span data-ttu-id="bae85-133">按一下**啟動資料行選取器**hello 屬性窗格 toospecify 想 toodrop 哪些資料行中。</span><span class="sxs-lookup"><span data-stu-id="bae85-133">Click **Launch column selector** in hello Properties pane toospecify which columns you wish toodrop.</span></span>
   <span data-ttu-id="bae85-134">![][4]</span><span class="sxs-lookup"><span data-stu-id="bae85-134">![Project Columns][4]</span></span>
3. <span data-ttu-id="bae85-135">排除兩個資料行：CustomerAlternateKey 和 GeographyKey。</span><span class="sxs-lookup"><span data-stu-id="bae85-135">Exclude two columns: CustomerAlternateKey and GeographyKey.</span></span>
   <span data-ttu-id="bae85-136">![移除不必要的資料行][5]</span><span class="sxs-lookup"><span data-stu-id="bae85-136">![Remove unnecessary columns][5]</span></span>

## <a name="3-build-hello-model"></a><span data-ttu-id="bae85-137">3.建立 hello 模型</span><span class="sxs-lookup"><span data-stu-id="bae85-137">3. Build hello model</span></span>
<span data-ttu-id="bae85-138">我們將會分割 hello 資料 80-20: 80 %tootrain 機器學習模型和 20%tootest hello 模型。</span><span class="sxs-lookup"><span data-stu-id="bae85-138">We will split hello data 80-20: 80% tootrain a machine learning model and 20% tootest hello model.</span></span> <span data-ttu-id="bae85-139">我們可以將這個二元分類問題的 hello 「 二級 」 演算法使用。</span><span class="sxs-lookup"><span data-stu-id="bae85-139">We will make use of hello “Two-Class” algorithms for this binary classification problem.</span></span>

1. <span data-ttu-id="bae85-140">拖曳 hello**分割**hello 畫布模組。</span><span class="sxs-lookup"><span data-stu-id="bae85-140">Drag hello **Split** module into hello canvas.</span></span>
2. <span data-ttu-id="bae85-141">輸入 0.8 hello 第一個輸出資料集在 hello 屬性 窗格中的資料列的分數。</span><span class="sxs-lookup"><span data-stu-id="bae85-141">Enter 0.8 for Fraction of rows in hello first output dataset in hello Properties pane.</span></span>
   <span data-ttu-id="bae85-142">![將資料分成訓練集和測試集][6]</span><span class="sxs-lookup"><span data-stu-id="bae85-142">![Split data into training and test set][6]</span></span>
3. <span data-ttu-id="bae85-143">拖曳 hello**二級促進式決策樹**hello 畫布模組。</span><span class="sxs-lookup"><span data-stu-id="bae85-143">Drag hello **Two-Class Boosted Decision Tree** module into hello canvas.</span></span>
4. <span data-ttu-id="bae85-144">拖曳 hello**定型模型**模組 hello 畫布，並指定 hello 輸入。</span><span class="sxs-lookup"><span data-stu-id="bae85-144">Drag hello **Train Model** module into hello canvas and specify hello inputs.</span></span> <span data-ttu-id="bae85-145">然後，按一下 [**啟動資料行選取器**hello 屬性] 窗格中。</span><span class="sxs-lookup"><span data-stu-id="bae85-145">Then, click **Launch column selector** in hello Properties pane.</span></span>
   * <span data-ttu-id="bae85-146">第一個輸入：ML 演算法。</span><span class="sxs-lookup"><span data-stu-id="bae85-146">First input: ML algorithm.</span></span>
   * <span data-ttu-id="bae85-147">第二個輸入： 在資料 tootrain hello 演算法。</span><span class="sxs-lookup"><span data-stu-id="bae85-147">Second input: Data tootrain hello algorithm on.</span></span>
     <span data-ttu-id="bae85-148">![連接 hello 定型模型 」 模組][7]</span><span class="sxs-lookup"><span data-stu-id="bae85-148">![Connect hello Train Model module][7]</span></span>
5. <span data-ttu-id="bae85-149">選取 hello **BikeBuyer** hello toopredict 資料行資料行。</span><span class="sxs-lookup"><span data-stu-id="bae85-149">Select hello **BikeBuyer** column as hello column toopredict.</span></span>
   <span data-ttu-id="bae85-150">![選取資料行 toopredict][8]</span><span class="sxs-lookup"><span data-stu-id="bae85-150">![Select Column toopredict][8]</span></span>

## <a name="4-score-hello-model"></a><span data-ttu-id="bae85-151">4.計分 hello 模型</span><span class="sxs-lookup"><span data-stu-id="bae85-151">4. Score hello model</span></span>
<span data-ttu-id="bae85-152">現在，我們將測試 hello 模型測試資料上執行的方式。</span><span class="sxs-lookup"><span data-stu-id="bae85-152">Now, we will test how hello model performs on test data.</span></span> <span data-ttu-id="bae85-153">我們將會比較 hello 演算法我們使用不同的演算法 toosee 的效能更好的選擇。</span><span class="sxs-lookup"><span data-stu-id="bae85-153">We will compare hello algorithm of our choice with a different algorithm toosee which performs better.</span></span>

1. <span data-ttu-id="bae85-154">拖曳**計分模型**hello 畫布模組。</span><span class="sxs-lookup"><span data-stu-id="bae85-154">Drag **Score Model** module into hello canvas.</span></span>
    <span data-ttu-id="bae85-155">第一個輸入： 定型模型的第二個輸入： 測試資料![分數 hello 模型][9]</span><span class="sxs-lookup"><span data-stu-id="bae85-155">First input: Trained model Second input: Test data ![Score hello model][9]</span></span>
2. <span data-ttu-id="bae85-156">拖曳 hello**二級貝氏點機器**到 hello 實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="bae85-156">Drag hello **Two-Class Bayes Point Machine** into hello experiment canvas.</span></span> <span data-ttu-id="bae85-157">我們將會比較此演算法如何比較 toohello 二級促進式決策樹中執行。</span><span class="sxs-lookup"><span data-stu-id="bae85-157">We will compare how this algorithm performs in comparison toohello Two-Class Boosted Decision Tree.</span></span>
3. <span data-ttu-id="bae85-158">複製和貼上的 hello 定型模型及計分模型中模組 hello 畫布。</span><span class="sxs-lookup"><span data-stu-id="bae85-158">Copy and Paste hello modules Train Model and Score Model in hello canvas.</span></span>
4. <span data-ttu-id="bae85-159">拖曳 hello**評估模型**hello 畫布 toocompare hello 兩個演算法的模組。</span><span class="sxs-lookup"><span data-stu-id="bae85-159">Drag hello **Evaluate Model** module into hello canvas toocompare hello two algorithms.</span></span>
5. <span data-ttu-id="bae85-160">**執行**hello 實驗。</span><span class="sxs-lookup"><span data-stu-id="bae85-160">**Run** hello experiment.</span></span>
   <span data-ttu-id="bae85-161">![執行 hello 實驗][10]</span><span class="sxs-lookup"><span data-stu-id="bae85-161">![Run hello experiment][10]</span></span>
6. <span data-ttu-id="bae85-162">按一下底部 hello hello 評估模型 」 模組的 hello 輸出連接埠，然後按一下 視覺化。</span><span class="sxs-lookup"><span data-stu-id="bae85-162">Click hello output port at hello bottom of hello Evaluate Model module and click Visualize.</span></span>
   <span data-ttu-id="bae85-163">![將評估結果視覺化][11]</span><span class="sxs-lookup"><span data-stu-id="bae85-163">![Visualize evaluation results][11]</span></span>

<span data-ttu-id="bae85-164">提供的 hello 度量 hello ROC 曲線，有效位數回收圖表，提起曲線。</span><span class="sxs-lookup"><span data-stu-id="bae85-164">hello metrics provided are hello ROC curve, precision-recall diagram and lift curve.</span></span> <span data-ttu-id="bae85-165">查看這些度量，我們可以看到 hello 第二個進一步執行該 hello 第一個模型。</span><span class="sxs-lookup"><span data-stu-id="bae85-165">Looking at these metrics, we can see that hello first model performed better than hello second one.</span></span> <span data-ttu-id="bae85-166">在 hello 什麼 hello 第一個模型來預測，按一下輸出連接埠的 hello 計分模型，然後按一下 視覺化 toolook。</span><span class="sxs-lookup"><span data-stu-id="bae85-166">toolook at hello what hello first model predicted, click on output port of hello Score Model and click Visualize.</span></span>
<span data-ttu-id="bae85-167">![將評分結果視覺化][12]</span><span class="sxs-lookup"><span data-stu-id="bae85-167">![Visualize score results][12]</span></span>

<span data-ttu-id="bae85-168">您會看到兩個的多個資料行加入 tooyour 測試資料集。</span><span class="sxs-lookup"><span data-stu-id="bae85-168">You will see two more columns added tooyour test dataset.</span></span>

* <span data-ttu-id="bae85-169">計分機率： hello 可能性客戶是自行車購買者。</span><span class="sxs-lookup"><span data-stu-id="bae85-169">Scored Probabilities: hello likelihood that a customer is a bike buyer.</span></span>
* <span data-ttu-id="bae85-170">計分標籤： hello 分類由 hello 模型-自行車買主 (1) 與否 (0)。</span><span class="sxs-lookup"><span data-stu-id="bae85-170">Scored Labels: hello classification done by hello model – bike buyer (1) or not (0).</span></span> <span data-ttu-id="bae85-171">用於標示此機率臨界值設定 too50%，而且可加以調整。</span><span class="sxs-lookup"><span data-stu-id="bae85-171">This probability threshold for labeling is set too50% and can be adjusted.</span></span>

<span data-ttu-id="bae85-172">比較 hello 資料行 BikeBuyer （實際） 與 hello 計分標籤 （預測），您可以查看呈現 hello 模型的執行。</span><span class="sxs-lookup"><span data-stu-id="bae85-172">Comparing hello column BikeBuyer (actual) with hello Scored Labels (prediction), you can see how well hello model has performed.</span></span> <span data-ttu-id="bae85-173">做為下一個步驟，您可使用此模型 toomake 預測新客戶並發佈為 web 服務，此模型或寫入結果後 tooSQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="bae85-173">As next steps, you can use this model toomake predictions for new customers and publish this model as a web service or write results back tooSQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bae85-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bae85-174">Next steps</span></span>
<span data-ttu-id="bae85-175">toolearn 有關建立預測的機器學習模型的詳細資訊，請參閱太[簡介 tooMachine 在 Azure 上學習][Introduction tooMachine Learning on Azure]。</span><span class="sxs-lookup"><span data-stu-id="bae85-175">toolearn more about building predictive machine learning models, refer too[Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction tooMachine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
