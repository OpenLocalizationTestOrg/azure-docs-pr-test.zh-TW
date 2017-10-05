---
title: "在 Machine Learning Studio 中管理實驗逐一查看 | Microsoft Docs"
description: "如何在 Azure Machine Learning Studio 中管理實驗逐一查看"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a53530f-20d5-40ae-9b49-7b499ccb44b7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 0e32a02358d1901bb80f356b0289b02b8e98afdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-experiment-iterations-in-azure-machine-learning-studio"></a><span data-ttu-id="2b168-103">在 Azure Machine Learning Studio 中管理實驗逐一查看</span><span class="sxs-lookup"><span data-stu-id="2b168-103">Manage experiment iterations in Azure Machine Learning Studio</span></span>
<span data-ttu-id="2b168-104">開發預測分析模型是一種逐一查看過程 - 您修改實驗的各種函數及參數，結果會不斷收斂，直到您對已訓練的有效模型感到滿意為止。</span><span class="sxs-lookup"><span data-stu-id="2b168-104">Developing a predictive analysis model is an iterative process - as you modify the various functions and parameters of your experiment, your results converge until you are satisfied that you have a trained, effective model.</span></span> <span data-ttu-id="2b168-105">此程序的關鍵是追蹤實驗參數和組態的各種逐一查看。</span><span class="sxs-lookup"><span data-stu-id="2b168-105">Key to this process is tracking the various iterations of your experiment parameters and configurations.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="2b168-106">您可以隨時檢閱先前的實驗執行，以挑戰、重新瀏覽及最終確認或調整先前的假設。</span><span class="sxs-lookup"><span data-stu-id="2b168-106">You can review previous runs of your experiments at any time in order to challenge, revisit, and ultimately either confirm or refine previous assumptions.</span></span> <span data-ttu-id="2b168-107">當您執行實驗時，Machine Learning Studio 會保留執行歷程記錄，包括資料集、模組及連接埠連接和參數。</span><span class="sxs-lookup"><span data-stu-id="2b168-107">When you run an experiment, Machine Learning Studio keeps a history of the run, including dataset, module, and port connections and parameters.</span></span> <span data-ttu-id="2b168-108">此歷程記錄也會擷取結果、執行階段資訊，例如開始和停止時間、記錄訊息及執行狀態。</span><span class="sxs-lookup"><span data-stu-id="2b168-108">This history also captures results, runtime information such as start and stop times, log messages, and execution status.</span></span> <span data-ttu-id="2b168-109">您可以隨時回顧任何執行，以檢閱實驗和中繼結果的年表。</span><span class="sxs-lookup"><span data-stu-id="2b168-109">You can look back at any of these runs at any time to review the chronology of your experiment and intermediate results.</span></span> <span data-ttu-id="2b168-110">您甚至可以使用上一次的實驗執行，啟動到新的階段，在您的路徑上查詢和探索，以建立簡單、複雜或甚至集成模型解決方案。</span><span class="sxs-lookup"><span data-stu-id="2b168-110">You can even use a previous run of your experiment to launch into a new phase of inquiry and discovery on your path to creating simple, complex, or even ensemble modeling solutions.</span></span>

> [!NOTE]
> <span data-ttu-id="2b168-111">當您檢視上一次的實驗執行時，該版本的實驗已遭到鎖定，無法編輯。</span><span class="sxs-lookup"><span data-stu-id="2b168-111">When you view a previous run of an experiment, that version of the experiment is locked and can't be edited.</span></span> <span data-ttu-id="2b168-112">但是，您可以儲存複本，方法是按一下 [ **另存新檔** ] 並且為複本提供新名稱。</span><span class="sxs-lookup"><span data-stu-id="2b168-112">You can, however, save a copy of it by clicking **SAVE AS** and providing a new name for the copy.</span></span> <span data-ttu-id="2b168-113">Machine Learning Studio 會開啟新複本，然後您可以編輯及執行。</span><span class="sxs-lookup"><span data-stu-id="2b168-113">Machine Learning Studio opens the new copy, which you can then edit and run.</span></span> <span data-ttu-id="2b168-114">實驗的此複本可以在含有所有其他實驗的 [ **實驗** ] 清單中取得。</span><span class="sxs-lookup"><span data-stu-id="2b168-114">This copy of your experiment is available in the **EXPERIMENTS** list along with all your other experiments.</span></span>
> 
> 

## <a name="viewing-the-prior-run"></a><span data-ttu-id="2b168-115">檢視上一次執行</span><span class="sxs-lookup"><span data-stu-id="2b168-115">Viewing the Prior Run</span></span>
<span data-ttu-id="2b168-116">當您開啟已至少執行一次的實驗時，可以藉由按一下內容窗格的 [ **上一次執行** ] 以檢視先前的實驗執行。</span><span class="sxs-lookup"><span data-stu-id="2b168-116">When you have an experiment open that you have run at least once, you can view the preceding run of the experiment by clicking **Prior Run** in the properties pane.</span></span>

<span data-ttu-id="2b168-117">例如，假設您建立實驗並且在下列時間執行其版本：11:23、11:42 及 11:55。</span><span class="sxs-lookup"><span data-stu-id="2b168-117">For example, suppose you create an experiment and run versions of it at 11:23, 11:42, and 11:55.</span></span> <span data-ttu-id="2b168-118">如果您開啟最後實驗執行 (11:55) 並且按一下 [ **上一次執行**]，則會開啟您在 11:42 執行的版本。</span><span class="sxs-lookup"><span data-stu-id="2b168-118">If you open the last run of the experiment (11:55) and click **Prior Run**, the version you ran at 11:42 is opened.</span></span>

## <a name="viewing-the-run-history"></a><span data-ttu-id="2b168-119">檢視執行歷程記錄</span><span class="sxs-lookup"><span data-stu-id="2b168-119">Viewing the Run History</span></span>
<span data-ttu-id="2b168-120">您可以檢視所有先前的實驗執行，方法是在開啟的實驗中按一下 [ **檢視執行歷程記錄** ]。</span><span class="sxs-lookup"><span data-stu-id="2b168-120">You can view all the previous runs of an experiment by clicking **View Run History** in an open experiment.</span></span>

<span data-ttu-id="2b168-121">例如，假設您建立實驗，其具有[線性迴歸][linear-regression]模組，且您想要觀察在實驗結果中變更**學習速度**值的效果。</span><span class="sxs-lookup"><span data-stu-id="2b168-121">For example, suppose you create an experiment with the [Linear Regression][linear-regression] module and you want to observe the effect of changing the value of **Learning rate** on your experiment results.</span></span> <span data-ttu-id="2b168-122">您針對此參數以不同值執行實驗多次，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2b168-122">You run the experiment multiple times with different values for this parameter, as follows:</span></span>

| <span data-ttu-id="2b168-123">學習速度值</span><span class="sxs-lookup"><span data-stu-id="2b168-123">Learning Rate value</span></span> | <span data-ttu-id="2b168-124">執行開始時間</span><span class="sxs-lookup"><span data-stu-id="2b168-124">Run start time</span></span> |
| --- | --- |
| <span data-ttu-id="2b168-125">0.1</span><span class="sxs-lookup"><span data-stu-id="2b168-125">0.1</span></span> |<span data-ttu-id="2b168-126">2014/9/11 下午 4:18:58</span><span class="sxs-lookup"><span data-stu-id="2b168-126">9/11/2014 4:18:58 pm</span></span> |
| <span data-ttu-id="2b168-127">0.2</span><span class="sxs-lookup"><span data-stu-id="2b168-127">0.2</span></span> |<span data-ttu-id="2b168-128">2014/9/11 下午 4:24:33</span><span class="sxs-lookup"><span data-stu-id="2b168-128">9/11/2014 4:24:33 pm</span></span> |
| <span data-ttu-id="2b168-129">0.4</span><span class="sxs-lookup"><span data-stu-id="2b168-129">0.4</span></span> |<span data-ttu-id="2b168-130">2014/9/11 下午 4:28:36</span><span class="sxs-lookup"><span data-stu-id="2b168-130">9/11/2014 4:28:36 pm</span></span> |
| <span data-ttu-id="2b168-131">0.5</span><span class="sxs-lookup"><span data-stu-id="2b168-131">0.5</span></span> |<span data-ttu-id="2b168-132">2014/9/11 下午 4:33:31</span><span class="sxs-lookup"><span data-stu-id="2b168-132">9/11/2014 4:33:31 pm</span></span> |

<span data-ttu-id="2b168-133">如果您按一下 [ **檢視執行歷程記錄**]，您會看見所有執行的清單：</span><span class="sxs-lookup"><span data-stu-id="2b168-133">If you click **VIEW RUN HISTORY**, you see a list of all these runs:</span></span>

![範例執行歷程記錄][runhistory]

<span data-ttu-id="2b168-135">按一下任何執行以檢視您執行該實驗之時間的實驗快照。</span><span class="sxs-lookup"><span data-stu-id="2b168-135">Click any of these runs to view a snapshot of the experiment at the time you ran it.</span></span> <span data-ttu-id="2b168-136">保留組態、參數值、註解及結果，給予您該實驗執行的完整記錄。</span><span class="sxs-lookup"><span data-stu-id="2b168-136">The configuration, parameter values, comments, and results are all preserved to give you a complete record of that run of your experiment.</span></span>

> [!TIP]
> <span data-ttu-id="2b168-137">若要記載您的實驗逐一查看，您可以在每次執行時修改標題，可以更新內容窗格中實驗的 **摘要** ，以及可以在個別模組中新增或更新註解以記錄您的變更。</span><span class="sxs-lookup"><span data-stu-id="2b168-137">To document your iterations of the experiment, you can modify the title each time you run it, you can update the **Summary** of the experiment in the properties pane, and you can add or update comments on individual modules to record your changes.</span></span> <span data-ttu-id="2b168-138">標題、摘要及模組註解會在每一次執行實驗時儲存。</span><span class="sxs-lookup"><span data-stu-id="2b168-138">The title, summary, and module comments are saved with each run of the experiment.</span></span>
> 
> 

<span data-ttu-id="2b168-139">Machine Learning Studio 中 [實驗] 索引標籤的實驗清單一律會顯示最新版本的實驗。</span><span class="sxs-lookup"><span data-stu-id="2b168-139">The list of experiments in the **EXPERIMENTS** tab in Machine Learning Studio always displays the latest version of an experiment.</span></span> <span data-ttu-id="2b168-140">如果您開啟實驗的上一次執行 (使用 [上一次執行] 或 [檢視執行歷程記錄])，您可以返回草稿版本，方法是按一下 [檢視執行歷程記錄] 並且選取 [狀態] 為 [可編輯] 的逐一查看。</span><span class="sxs-lookup"><span data-stu-id="2b168-140">If you open a previous run of the experiment (using **Prior Run** or **VIEW RUN HISTORY**), you can return to the draft version by clicking **VIEW RUN HISTORY** and selecting the iteration that has a **STATE** of **Editable**.</span></span>

## <a name="iterating-on-a-previous-run"></a><span data-ttu-id="2b168-141">逐一查看上一次執行</span><span class="sxs-lookup"><span data-stu-id="2b168-141">Iterating on a Previous Run</span></span>
<span data-ttu-id="2b168-142">當您按一下 [上一次執行] 或 [檢視執行歷程記錄]，並且開啟上一次執行時，您可以在唯讀模式中檢視完成的實驗。</span><span class="sxs-lookup"><span data-stu-id="2b168-142">When you click **Prior Run** or **VIEW RUN HISTORY** and open a previous run, you can view a finished experiment in read-only mode.</span></span>

<span data-ttu-id="2b168-143">如果想要從您為上一次執行設定的方式開始實驗的逐一查看，您可以藉由開啟執行並且按一下 [ **另存新檔**] 來完成。</span><span class="sxs-lookup"><span data-stu-id="2b168-143">If you want to begin an iteration of your experiment starting with the way you configured it for a previous run, you can do this by opening the run and clicking **SAVE AS**.</span></span> <span data-ttu-id="2b168-144">這會建立新的實驗，具有新的標題、空白的執行歷程記錄及上一次執行的所有元件和參數值。</span><span class="sxs-lookup"><span data-stu-id="2b168-144">This creates a new experiment, with a new title, an empty run history, and all the components and parameter values of the previous run.</span></span> <span data-ttu-id="2b168-145">此新的實驗會列在 Machine Learning Studio 首頁的 [實驗]  索引標籤中，您可以修改及執行、為實驗的逐一查看起始新的執行歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="2b168-145">This new experiment is listed in the **EXPERIMENTS** tab in the Machine Learning Studio home page, and you can modify and run it, initiating a new run history for this iteration of your experiment.</span></span> 

<span data-ttu-id="2b168-146">例如，假設您有上一個章節顯示的實驗執行歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="2b168-146">For example, suppose you have the experiment run history shown in the previous section.</span></span> <span data-ttu-id="2b168-147">您想要觀察當您將 [學習速度] 參數設為 0.4，並且針對 [訓練 epoch 數目] 參數嘗試不同值時，會發生什麼狀況。</span><span class="sxs-lookup"><span data-stu-id="2b168-147">You want to observe what happens when you set the **Learning rate** parameter to 0.4, and try different values for the **Number of training epochs** parameter.</span></span>

1. <span data-ttu-id="2b168-148">按一下 [ **檢視執行歷程記錄** ] 並且開啟您在下午 4:28:36 執行的實驗逐一查看 (您在其中將參數值設為 0.4)。</span><span class="sxs-lookup"><span data-stu-id="2b168-148">Click **VIEW RUN HISTORY** and open the iteration of the experiment that you ran at 4:28:36 pm (in which you set the parameter value to 0.4).</span></span>
2. <span data-ttu-id="2b168-149">按一下 [ **另存新檔**]。</span><span class="sxs-lookup"><span data-stu-id="2b168-149">Click **SAVE AS**.</span></span>
3. <span data-ttu-id="2b168-150">輸入新標題，然後按一下 [ **確定** ] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="2b168-150">Enter a new title and click the **OK** checkmark.</span></span> <span data-ttu-id="2b168-151">實驗的新複本隨即建立。</span><span class="sxs-lookup"><span data-stu-id="2b168-151">A new copy of the experiment is created.</span></span>
4. <span data-ttu-id="2b168-152">修改 [ **訓練 epoch 數目** ] 參數。</span><span class="sxs-lookup"><span data-stu-id="2b168-152">Modify the **Number of training epochs** parameter.</span></span>
5. <span data-ttu-id="2b168-153">按一下 [ **執行**]。</span><span class="sxs-lookup"><span data-stu-id="2b168-153">Click **RUN**.</span></span>

<span data-ttu-id="2b168-154">您現在可以繼續修改及執行此實驗版本，建立新的執行歷程記錄以記錄您的工作。</span><span class="sxs-lookup"><span data-stu-id="2b168-154">You can now continue to modify and run this version of your experiment, building a new run history to record your work.</span></span>

<!-- Images -->
[runhistory]:./media/machine-learning-manage-experiment-iterations/viewrunhistory.jpg


<!-- Module References -->
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
