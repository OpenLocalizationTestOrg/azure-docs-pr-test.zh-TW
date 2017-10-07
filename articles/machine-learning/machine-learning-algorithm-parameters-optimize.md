---
title: "aaaOptimize 您在 Azure Machine Learning 中的演算法 |Microsoft 文件"
description: "說明如何 toochoose hello 最佳參數設定的 Azure Machine Learning 中的演算法。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6717e30e-b8d8-4cc1-ad0b-1d4727928d32
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: fbf2f71abdbce19483fb048d67a39cbb368a928e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="choose-parameters-toooptimize-your-algorithms-in-azure-machine-learning"></a><span data-ttu-id="b4ce9-103">Azure Machine Learning 中選擇您的演算法參數 toooptimize</span><span class="sxs-lookup"><span data-stu-id="b4ce9-103">Choose parameters toooptimize your algorithms in Azure Machine Learning</span></span>
<span data-ttu-id="b4ce9-104">本主題描述如何 toochoose hello 右 hyperparameter 設定 Azure 機器學習演算法。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-104">This topic describes how toochoose hello right hyperparameter set for an algorithm in Azure Machine Learning.</span></span> <span data-ttu-id="b4ce9-105">大部分的機器學習演算法有參數 tooset。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-105">Most machine learning algorithms have parameters tooset.</span></span> <span data-ttu-id="b4ce9-106">當定型模型時，您會需要這些參數的 tooprovide 值。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-106">When you train a model, you need tooprovide values for those parameters.</span></span> <span data-ttu-id="b4ce9-107">hello 效用 hello 定型的模型取決於您選擇的 hello 模型參數。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-107">hello efficacy of hello trained model depends on hello model parameters that you choose.</span></span> <span data-ttu-id="b4ce9-108">hello 尋找 hello 最佳參數集的程序稱為*模型選取*。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-108">hello process of finding hello optimal set of parameters is known as *model selection*.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="b4ce9-109">有各種方式 toodo 模型選取項目。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-109">There are various ways toodo model selection.</span></span> <span data-ttu-id="b4ce9-110">在 machine learning 中，交叉驗證是最常使用的 hello 方法的模型選取項目，而且 hello 預設模型在 Azure 機器學習的選取範圍機制。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-110">In machine learning, cross-validation is one of hello most widely used methods for model selection, and it is hello default model selection mechanism in Azure Machine Learning.</span></span> <span data-ttu-id="b4ce9-111">由於 Azure Machine Learning 支援 R 和 Python 兩者，因此您一律可以使用 R 或 Python 來實作其自己的模型選擇機制。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-111">Because Azure Machine Learning supports both R and Python, you can always implement their own model selection mechanisms by using either R or Python.</span></span>

<span data-ttu-id="b4ce9-112">尋找 hello 最佳參數集的 hello 程序有四個步驟：</span><span class="sxs-lookup"><span data-stu-id="b4ce9-112">There are four steps in hello process of finding hello best parameter set:</span></span>

1. <span data-ttu-id="b4ce9-113">**定義 hello 參數空間**: hello 的演算法，請先決定您希望 tooconsider hello 確切的參數值。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-113">**Define hello parameter space**: For hello algorithm, first decide hello exact parameter values you want tooconsider.</span></span>
2. <span data-ttu-id="b4ce9-114">**定義 hello 交叉驗證設定**： 決定如何 toochoose 交叉驗證摺疊 hello 資料集。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-114">**Define hello cross-validation settings**: Decide how toochoose cross-validation folds for hello dataset.</span></span>
3. <span data-ttu-id="b4ce9-115">**定義 hello 度量**： 決定哪些度量 toouse 判斷 hello 一組最佳的參數，例如精確度，均方根平方錯誤、 有效位數、 選出或 f 分數。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-115">**Define hello metric**: Decide what metric toouse for determining hello best set of parameters, such as accuracy, root mean squared error, precision, recall, or f-score.</span></span>
4. <span data-ttu-id="b4ce9-116">**定型、 評估並比較**: hello 參數值的每一個唯一組合，交叉驗證是由執行，並根據您定義的 hello 錯誤度量。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-116">**Train, evaluate, and compare**: For each unique combination of hello parameter values, cross-validation is carried out by and based on hello error metric you define.</span></span> <span data-ttu-id="b4ce9-117">評估和比較之後, 您可以選擇 hello 效能最佳模型。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-117">After evaluation and comparison, you can choose hello best-performing model.</span></span>

<span data-ttu-id="b4ce9-118">下列映像的 hello 說明如何達成這在 Azure Machine Learning 中的顯示。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-118">hello following image illustrates shows how this can be achieved in Azure Machine Learning.</span></span>

![尋找 hello 最佳參數集](./media/machine-learning-algorithm-parameters-optimize/fig1.png)

## <a name="define-hello-parameter-space"></a><span data-ttu-id="b4ce9-120">定義 hello 參數空間</span><span class="sxs-lookup"><span data-stu-id="b4ce9-120">Define hello parameter space</span></span>
<span data-ttu-id="b4ce9-121">您可以定義在 hello 模型初始化步驟設定 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-121">You can define hello parameter set at hello model initialization step.</span></span> <span data-ttu-id="b4ce9-122">hello 的所有機器學習演算法參數] 窗格有兩種定型模式：*單一參數*和*參數範圍*。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-122">hello parameter pane of all machine learning algorithms has two trainer modes: *Single Parameter* and *Parameter Range*.</span></span> <span data-ttu-id="b4ce9-123">選擇 [參數範圍] 模式。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-123">Choose Parameter Range mode.</span></span> <span data-ttu-id="b4ce9-124">在參數範圍模式中，您可以針對每個參數輸入多個值。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-124">In Parameter Range mode, you can enter multiple values for each parameter.</span></span> <span data-ttu-id="b4ce9-125">您可以在 hello] 文字方塊中輸入以逗號分隔值。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-125">You can enter comma-separated values in hello text box.</span></span>

![二元促進式決策樹，單一參數](./media/machine-learning-algorithm-parameters-optimize/fig2.png)

 <span data-ttu-id="b4ce9-127">或者，您可以定義 hello hello 格線和 hello 總數點 toobe 使用產生的最大和最小點**使用範圍產生器**。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-127">Alternately, you can define hello maximum and minimum points of hello grid and hello total number of points toobe generated with **Use Range Builder**.</span></span> <span data-ttu-id="b4ce9-128">根據預設，會產生線性標尺上的 hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-128">By default, hello parameter values are generated on a linear scale.</span></span> <span data-ttu-id="b4ce9-129">但是如果**對數刻度**勾選，hello 值會產生 hello 對數刻度 （也就是 hello 相鄰點的 hello 比例是常數，而不是差異）。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-129">But if **Log Scale** is checked, hello values are generated in hello log scale (that is, hello ratio of hello adjacent points is constant instead of their difference).</span></span> <span data-ttu-id="b4ce9-130">對於整數參數，您可以使用連字號來定義範圍。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-130">For integer parameters, you can define a range by using a hyphen.</span></span> <span data-ttu-id="b4ce9-131">例如，"1-10"表示，介於 1 到 10 之間的所有整數 （兩者內含） 形成 hello 參數集。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-131">For example, “1-10” means that all integers between 1 and 10 (both inclusive) form hello parameter set.</span></span> <span data-ttu-id="b4ce9-132">也支援使用混合的模式。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-132">A mixed mode is also supported.</span></span> <span data-ttu-id="b4ce9-133">比方說，hello 參數集"1-10、 20、 50"會加入整數 1-10、 20 到 50 個。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-133">For example, hello parameter set “1-10, 20, 50” would include integers 1-10, 20, and 50.</span></span>

![二元促進式決策樹，參數範圍](./media/machine-learning-algorithm-parameters-optimize/fig3.png)

## <a name="define-cross-validation-folds"></a><span data-ttu-id="b4ce9-135">定義交叉驗證折數</span><span class="sxs-lookup"><span data-stu-id="b4ce9-135">Define cross-validation folds</span></span>
<span data-ttu-id="b4ce9-136">hello[資料分割和取樣][ partition-and-sample]模組可以是使用的 toorandomly 指派摺疊 toohello 資料。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-136">hello [Partition and Sample][partition-and-sample] module can be used toorandomly assign folds toohello data.</span></span> <span data-ttu-id="b4ce9-137">在下列範例組態 hello 模組 hello，我們會定義五個摺疊，並隨機指派摺疊數字 toohello 範例執行個體。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-137">In hello following sample configuration for hello module, we define five folds and randomly assign a fold number toohello sample instances.</span></span>

![資料分割和取樣](./media/machine-learning-algorithm-parameters-optimize/fig4.png)

## <a name="define-hello-metric"></a><span data-ttu-id="b4ce9-139">定義 hello 度量</span><span class="sxs-lookup"><span data-stu-id="b4ce9-139">Define hello metric</span></span>
<span data-ttu-id="b4ce9-140">hello[微調模型超][ tune-model-hyperparameters]模組提供實證選擇 hello 參數指定的演算法和資料集的一組最佳的支援。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-140">hello [Tune Model Hyperparameters][tune-model-hyperparameters] module provides support for empirically choosing hello best set of parameters for a given algorithm and dataset.</span></span> <span data-ttu-id="b4ce9-141">此外訓練 hello tooother 資訊模型，hello**屬性**本單元的窗格包含決定最佳參數集 hello hello 度量。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-141">In addition tooother information regarding training hello model, hello **Properties** pane of this module includes hello metric for determining hello best parameter set.</span></span> <span data-ttu-id="b4ce9-142">分類和迴歸演算法分別有兩個不同的下拉式清單方塊。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-142">It has two different drop-down list boxes for classification and regression algorithms, respectively.</span></span> <span data-ttu-id="b4ce9-143">如果列入考量的 hello 演算法是一種分類演算法，就會忽略 hello 迴歸度量，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-143">If hello algorithm under consideration is a classification algorithm, hello regression metric is ignored and vice versa.</span></span> <span data-ttu-id="b4ce9-144">在此特定範例中，是 hello 度量**精確度**。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-144">In this specific example, hello metric is **Accuracy**.</span></span>   

![掃掠參數](./media/machine-learning-algorithm-parameters-optimize/fig5.png)

## <a name="train-evaluate-and-compare"></a><span data-ttu-id="b4ce9-146">訓練、評估和比較</span><span class="sxs-lookup"><span data-stu-id="b4ce9-146">Train, evaluate, and compare</span></span>
<span data-ttu-id="b4ce9-147">hello 相同[微調模型超][ tune-model-hyperparameters]模組來定型，對應 toohello 參數集，會評估各種標準，然後建立 hello 自動定型的模型，根據 hello 所有 hello 模型您選擇的度量。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-147">hello same [Tune Model Hyperparameters][tune-model-hyperparameters] module trains all hello models that correspond toohello parameter set, evaluates various metrics, and then creates hello best-trained model based on hello metric you choose.</span></span> <span data-ttu-id="b4ce9-148">此模組有兩個必要的輸入項：</span><span class="sxs-lookup"><span data-stu-id="b4ce9-148">This module has two mandatory inputs:</span></span>

* <span data-ttu-id="b4ce9-149">hello 未定型的學習模組</span><span class="sxs-lookup"><span data-stu-id="b4ce9-149">hello untrained learner</span></span>
* <span data-ttu-id="b4ce9-150">hello 資料集</span><span class="sxs-lookup"><span data-stu-id="b4ce9-150">hello dataset</span></span>

<span data-ttu-id="b4ce9-151">hello 模組也有選擇性輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-151">hello module also has an optional dataset input.</span></span> <span data-ttu-id="b4ce9-152">摺疊資訊 toohello 強制的資料集輸入具有連接 hello 資料集。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-152">Connect hello dataset with fold information toohello mandatory dataset input.</span></span> <span data-ttu-id="b4ce9-153">如果 hello 資料集未指派任何摺疊的資訊，然後 10 個摺疊的交叉驗證會自動執行的預設值。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-153">If hello dataset is not assigned any fold information, then a 10-fold cross-validation is automatically executed by default.</span></span> <span data-ttu-id="b4ce9-154">如果不是 hello 摺疊指派 hello 選擇性資料集連接埠所提供的驗證資料集，然後選擇定型測試模式並 hello 第一個資料集是使用的 tootrain hello 模型，每一個參數組合。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-154">If hello fold assignment is not done and a validation dataset is provided at hello optional dataset port, then a train-test mode is chosen and hello first dataset is used tootrain hello model for each parameter combination.</span></span>

![推進式決策樹分類器](./media/machine-learning-algorithm-parameters-optimize/fig6a.png)

<span data-ttu-id="b4ce9-156">hello 模型會再評估 hello 驗證資料集。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-156">hello model is then evaluated on hello validation dataset.</span></span> <span data-ttu-id="b4ce9-157">hello 留待 hello 模組顯示的輸出連接埠不同的度量資訊的參數值的函式。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-157">hello left output port of hello module shows different metrics as functions of parameter values.</span></span> <span data-ttu-id="b4ce9-158">hello 右輸出連接埠提供 hello 定型的模型對應 toohello 效能最佳的模型，根據 toohello 選擇公制 (**精確度**在此情況下)。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-158">hello right output port gives hello trained model that corresponds toohello best-performing model according toohello chosen metric (**Accuracy** in this case).</span></span>  

![驗證資料集](./media/machine-learning-algorithm-parameters-optimize/fig6b.png)

<span data-ttu-id="b4ce9-160">您可以看到 hello 精確參數選擇的視覺化 hello 右輸出連接埠。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-160">You can see hello exact parameters chosen by visualizing hello right output port.</span></span> <span data-ttu-id="b4ce9-161">此模型在儲存為訓練過的模型之後，可用來對測試集計分，或者用在可運作的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="b4ce9-161">This model can be used in scoring a test set or in an operationalized web service after saving as a trained model.</span></span>

<!-- Module References -->
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[tune-model-hyperparameters]: https://msdn.microsoft.com/library/azure/038d91b6-c2f2-42a1-9215-1f2c20ed1b40/
