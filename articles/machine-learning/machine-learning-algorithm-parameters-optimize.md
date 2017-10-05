---
title: "最佳化 Azure Machine Learning 中的演算法 | Microsoft Docs"
description: "說明如何為 Azure Machine Learning 中的演算法選擇最佳的參數設定。"
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
ms.openlocfilehash: b3be7f31ac31c656744fb809e3972af0ac4ad4f1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="choose-parameters-to-optimize-your-algorithms-in-azure-machine-learning"></a><span data-ttu-id="e82f7-103">選擇參數來最佳化 Azure Machine Learning 中的演算法</span><span class="sxs-lookup"><span data-stu-id="e82f7-103">Choose parameters to optimize your algorithms in Azure Machine Learning</span></span>
<span data-ttu-id="e82f7-104">本主題說明如何為 Azure Machine Learning 中的演算法選擇正確的超參數 (hyperparameter) 集。</span><span class="sxs-lookup"><span data-stu-id="e82f7-104">This topic describes how to choose the right hyperparameter set for an algorithm in Azure Machine Learning.</span></span> <span data-ttu-id="e82f7-105">大部分的機器學習服務演算法都會有需要設定的參數。</span><span class="sxs-lookup"><span data-stu-id="e82f7-105">Most machine learning algorithms have parameters to set.</span></span> <span data-ttu-id="e82f7-106">當您訓練一個模型時，必須提供這些參數的值。</span><span class="sxs-lookup"><span data-stu-id="e82f7-106">When you train a model, you need to provide values for those parameters.</span></span> <span data-ttu-id="e82f7-107">訓練過的模型效率會依據所選擇的模型參數而定。</span><span class="sxs-lookup"><span data-stu-id="e82f7-107">The efficacy of the trained model depends on the model parameters that you choose.</span></span> <span data-ttu-id="e82f7-108">找出最佳參數集的過程稱為*模型選擇*。</span><span class="sxs-lookup"><span data-stu-id="e82f7-108">The process of finding the optimal set of parameters is known as *model selection*.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="e82f7-109">有各種方法可用來進行模型選擇。</span><span class="sxs-lookup"><span data-stu-id="e82f7-109">There are various ways to do model selection.</span></span> <span data-ttu-id="e82f7-110">在機器學習中，交叉驗證是其中一種最廣泛使用的模型選擇方法，在 Azure Machine Learning 中是預設的模型選擇機制。</span><span class="sxs-lookup"><span data-stu-id="e82f7-110">In machine learning, cross-validation is one of the most widely used methods for model selection, and it is the default model selection mechanism in Azure Machine Learning.</span></span> <span data-ttu-id="e82f7-111">由於 Azure Machine Learning 支援 R 和 Python 兩者，因此您一律可以使用 R 或 Python 來實作其自己的模型選擇機制。</span><span class="sxs-lookup"><span data-stu-id="e82f7-111">Because Azure Machine Learning supports both R and Python, you can always implement their own model selection mechanisms by using either R or Python.</span></span>

<span data-ttu-id="e82f7-112">找出最佳參數集的過程有四個步驟：</span><span class="sxs-lookup"><span data-stu-id="e82f7-112">There are four steps in the process of finding the best parameter set:</span></span>

1. <span data-ttu-id="e82f7-113">**定義參數空間**：對於演算法，先決定您想要考慮的確切參數值。</span><span class="sxs-lookup"><span data-stu-id="e82f7-113">**Define the parameter space**: For the algorithm, first decide the exact parameter values you want to consider.</span></span>
2. <span data-ttu-id="e82f7-114">**定義交叉驗證設定**：決定如何選擇資料集的交叉驗證折數。</span><span class="sxs-lookup"><span data-stu-id="e82f7-114">**Define the cross-validation settings**: Decide how to choose cross-validation folds for the dataset.</span></span>
3. <span data-ttu-id="e82f7-115">**定義計量**：決定要使用哪一種計量來判斷最佳的參數集，例如正確度、均方根誤差、精確度、召回率或 f 分數。</span><span class="sxs-lookup"><span data-stu-id="e82f7-115">**Define the metric**: Decide what metric to use for determining the best set of parameters, such as accuracy, root mean squared error, precision, recall, or f-score.</span></span>
4. <span data-ttu-id="e82f7-116">**訓練、評估和比較**：對於每個唯一的參數值組合，執行交叉驗證並根據您定義的錯誤計量。</span><span class="sxs-lookup"><span data-stu-id="e82f7-116">**Train, evaluate, and compare**: For each unique combination of the parameter values, cross-validation is carried out by and based on the error metric you define.</span></span> <span data-ttu-id="e82f7-117">評估和比較之後，您可以選擇最佳的模型。</span><span class="sxs-lookup"><span data-stu-id="e82f7-117">After evaluation and comparison, you can choose the best-performing model.</span></span>

<span data-ttu-id="e82f7-118">下列影像說明在 Azure Machine Learning 中如何達到這個目標。</span><span class="sxs-lookup"><span data-stu-id="e82f7-118">The following image illustrates shows how this can be achieved in Azure Machine Learning.</span></span>

![尋找最佳的參數集](./media/machine-learning-algorithm-parameters-optimize/fig1.png)

## <a name="define-the-parameter-space"></a><span data-ttu-id="e82f7-120">定義參數空間</span><span class="sxs-lookup"><span data-stu-id="e82f7-120">Define the parameter space</span></span>
<span data-ttu-id="e82f7-121">您可以在進行模型初始化步驟時定義參數集。</span><span class="sxs-lookup"><span data-stu-id="e82f7-121">You can define the parameter set at the model initialization step.</span></span> <span data-ttu-id="e82f7-122">所有機器學習演算法的參數窗格都有兩種訓練模式：[單一參數] 和 [參數範圍]。</span><span class="sxs-lookup"><span data-stu-id="e82f7-122">The parameter pane of all machine learning algorithms has two trainer modes: *Single Parameter* and *Parameter Range*.</span></span> <span data-ttu-id="e82f7-123">選擇 [參數範圍] 模式。</span><span class="sxs-lookup"><span data-stu-id="e82f7-123">Choose Parameter Range mode.</span></span> <span data-ttu-id="e82f7-124">在參數範圍模式中，您可以針對每個參數輸入多個值。</span><span class="sxs-lookup"><span data-stu-id="e82f7-124">In Parameter Range mode, you can enter multiple values for each parameter.</span></span> <span data-ttu-id="e82f7-125">您可以在文字方塊中輸入以逗號分隔的值。</span><span class="sxs-lookup"><span data-stu-id="e82f7-125">You can enter comma-separated values in the text box.</span></span>

![二元促進式決策樹，單一參數](./media/machine-learning-algorithm-parameters-optimize/fig2.png)

 <span data-ttu-id="e82f7-127">或者，您可以使用**使用範圍產生器**來定義網格的最大點數與最小點數，以及要產生的總點數。</span><span class="sxs-lookup"><span data-stu-id="e82f7-127">Alternately, you can define the maximum and minimum points of the grid and the total number of points to be generated with **Use Range Builder**.</span></span> <span data-ttu-id="e82f7-128">參數值預設會以線性刻度產生。</span><span class="sxs-lookup"><span data-stu-id="e82f7-128">By default, the parameter values are generated on a linear scale.</span></span> <span data-ttu-id="e82f7-129">但如果核取了 [對數刻度]，值會以對數刻度產生 (也就是相鄰兩點的比率而不是其差異為常數)。</span><span class="sxs-lookup"><span data-stu-id="e82f7-129">But if **Log Scale** is checked, the values are generated in the log scale (that is, the ratio of the adjacent points is constant instead of their difference).</span></span> <span data-ttu-id="e82f7-130">對於整數參數，您可以使用連字號來定義範圍。</span><span class="sxs-lookup"><span data-stu-id="e82f7-130">For integer parameters, you can define a range by using a hyphen.</span></span> <span data-ttu-id="e82f7-131">例如，"1-10" 表示介於 1 到 10 (兩者皆含) 之間的所有整數會構成參數集。</span><span class="sxs-lookup"><span data-stu-id="e82f7-131">For example, “1-10” means that all integers between 1 and 10 (both inclusive) form the parameter set.</span></span> <span data-ttu-id="e82f7-132">也支援使用混合的模式。</span><span class="sxs-lookup"><span data-stu-id="e82f7-132">A mixed mode is also supported.</span></span> <span data-ttu-id="e82f7-133">例如，此參數設定 "1-10, 20, 50" 會包括整數 1-10、20 和 50 個。</span><span class="sxs-lookup"><span data-stu-id="e82f7-133">For example, the parameter set “1-10, 20, 50” would include integers 1-10, 20, and 50.</span></span>

![二元促進式決策樹，參數範圍](./media/machine-learning-algorithm-parameters-optimize/fig3.png)

## <a name="define-cross-validation-folds"></a><span data-ttu-id="e82f7-135">定義交叉驗證折數</span><span class="sxs-lookup"><span data-stu-id="e82f7-135">Define cross-validation folds</span></span>
<span data-ttu-id="e82f7-136">[資料分割和取樣][partition-and-sample]模組可用來隨機指派資料的折數。</span><span class="sxs-lookup"><span data-stu-id="e82f7-136">The [Partition and Sample][partition-and-sample] module can be used to randomly assign folds to the data.</span></span> <span data-ttu-id="e82f7-137">在下圖模組的範例組態中，我們定義五個折數，並且對樣本實例隨機指派折疊數目。</span><span class="sxs-lookup"><span data-stu-id="e82f7-137">In the following sample configuration for the module, we define five folds and randomly assign a fold number to the sample instances.</span></span>

![資料分割和取樣](./media/machine-learning-algorithm-parameters-optimize/fig4.png)

## <a name="define-the-metric"></a><span data-ttu-id="e82f7-139">定義計量</span><span class="sxs-lookup"><span data-stu-id="e82f7-139">Define the metric</span></span>
<span data-ttu-id="e82f7-140">[微調模型超參數][tune-model-hyperparameters]模組支援依據經驗為指定的演算法和資料集選擇一組最佳參數。</span><span class="sxs-lookup"><span data-stu-id="e82f7-140">The [Tune Model Hyperparameters][tune-model-hyperparameters] module provides support for empirically choosing the best set of parameters for a given algorithm and dataset.</span></span> <span data-ttu-id="e82f7-141">除了有關訓練模型的其他資訊，此模組的 [屬性] 窗格還包括用來判斷最佳參數集的計量。</span><span class="sxs-lookup"><span data-stu-id="e82f7-141">In addition to other information regarding training the model, the **Properties** pane of this module includes the metric for determining the best parameter set.</span></span> <span data-ttu-id="e82f7-142">分類和迴歸演算法分別有兩個不同的下拉式清單方塊。</span><span class="sxs-lookup"><span data-stu-id="e82f7-142">It has two different drop-down list boxes for classification and regression algorithms, respectively.</span></span> <span data-ttu-id="e82f7-143">如果考慮使用分類演算法，則會忽略迴歸計量，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="e82f7-143">If the algorithm under consideration is a classification algorithm, the regression metric is ignored and vice versa.</span></span> <span data-ttu-id="e82f7-144">在此特定範例中，計量是**正確度**。</span><span class="sxs-lookup"><span data-stu-id="e82f7-144">In this specific example, the metric is **Accuracy**.</span></span>   

![掃掠參數](./media/machine-learning-algorithm-parameters-optimize/fig5.png)

## <a name="train-evaluate-and-compare"></a><span data-ttu-id="e82f7-146">訓練、評估和比較</span><span class="sxs-lookup"><span data-stu-id="e82f7-146">Train, evaluate, and compare</span></span>
<span data-ttu-id="e82f7-147">相同的[微調模型超參數][tune-model-hyperparameters]模組會訓練對應於參數集的所有模型、評估各種計量，然後根據您選擇的計量建立訓練最妥善的模型。</span><span class="sxs-lookup"><span data-stu-id="e82f7-147">The same [Tune Model Hyperparameters][tune-model-hyperparameters] module trains all the models that correspond to the parameter set, evaluates various metrics, and then creates the best-trained model based on the metric you choose.</span></span> <span data-ttu-id="e82f7-148">此模組有兩個必要的輸入項：</span><span class="sxs-lookup"><span data-stu-id="e82f7-148">This module has two mandatory inputs:</span></span>

* <span data-ttu-id="e82f7-149">未訓練過的學習者</span><span class="sxs-lookup"><span data-stu-id="e82f7-149">The untrained learner</span></span>
* <span data-ttu-id="e82f7-150">資料集</span><span class="sxs-lookup"><span data-stu-id="e82f7-150">The dataset</span></span>

<span data-ttu-id="e82f7-151">此模組也有一個選擇性資料集輸入項。</span><span class="sxs-lookup"><span data-stu-id="e82f7-151">The module also has an optional dataset input.</span></span> <span data-ttu-id="e82f7-152">將具有折疊資訊的資料集連接到必要的資料集輸入。</span><span class="sxs-lookup"><span data-stu-id="e82f7-152">Connect the dataset with fold information to the mandatory dataset input.</span></span> <span data-ttu-id="e82f7-153">如果資料集未被指派任何折疊資訊，則預設會自動執行 10 折交叉驗證。</span><span class="sxs-lookup"><span data-stu-id="e82f7-153">If the dataset is not assigned any fold information, then a 10-fold cross-validation is automatically executed by default.</span></span> <span data-ttu-id="e82f7-154">如果尚未進行折疊指派，且在選擇性資料集區域提供了驗證資料集，則會使用選擇的訓練-測試模式和第一個資料集針對每一個參數組合訓練模型。</span><span class="sxs-lookup"><span data-stu-id="e82f7-154">If the fold assignment is not done and a validation dataset is provided at the optional dataset port, then a train-test mode is chosen and the first dataset is used to train the model for each parameter combination.</span></span>

![推進式決策樹分類器](./media/machine-learning-algorithm-parameters-optimize/fig6a.png)

<span data-ttu-id="e82f7-156">接著，會針對驗證資料集評估模型。</span><span class="sxs-lookup"><span data-stu-id="e82f7-156">The model is then evaluated on the validation dataset.</span></span> <span data-ttu-id="e82f7-157">模組的左側輸出區域將不同的計量顯示為參數值的函數。</span><span class="sxs-lookup"><span data-stu-id="e82f7-157">The left output port of the module shows different metrics as functions of parameter values.</span></span> <span data-ttu-id="e82f7-158">右側的輸出區域提供訓練過的模型，根據選擇的計量 (在此案例中為**正確度**) 對應到最佳的執行模型。</span><span class="sxs-lookup"><span data-stu-id="e82f7-158">The right output port gives the trained model that corresponds to the best-performing model according to the chosen metric (**Accuracy** in this case).</span></span>  

![驗證資料集](./media/machine-learning-algorithm-parameters-optimize/fig6b.png)

<span data-ttu-id="e82f7-160">將右側輸出區域具體呈現之後，您可以看到所選擇的確切參數。</span><span class="sxs-lookup"><span data-stu-id="e82f7-160">You can see the exact parameters chosen by visualizing the right output port.</span></span> <span data-ttu-id="e82f7-161">此模型在儲存為訓練過的模型之後，可用來對測試集計分，或者用在可運作的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="e82f7-161">This model can be used in scoring a test set or in an operationalized web service after saving as a trained model.</span></span>

<!-- Module References -->
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[tune-model-hyperparameters]: https://msdn.microsoft.com/library/azure/038d91b6-c2f2-42a1-9215-1f2c20ed1b40/
