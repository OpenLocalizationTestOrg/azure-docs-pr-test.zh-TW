---
title: "aaaManage 實驗 Machine Learning Studio 中的反覆項目 |Microsoft 文件"
description: "Toomanage 進行反覆項目，Azure Machine Learning Studio 中的實驗"
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
ms.openlocfilehash: bd30c048ce063811b1b2de8ce6d71e99ba975713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-experiment-iterations-in-azure-machine-learning-studio"></a><span data-ttu-id="c7210-103">在 Azure Machine Learning Studio 中管理實驗逐一查看</span><span class="sxs-lookup"><span data-stu-id="c7210-103">Manage experiment iterations in Azure Machine Learning Studio</span></span>
<span data-ttu-id="c7210-104">當您修改 hello 開發預測分析的模型是反覆的程序-您的結果不同的函式和參數的實驗，聚合直到您滿意您有定型、 有效率的模型。</span><span class="sxs-lookup"><span data-stu-id="c7210-104">Developing a predictive analysis model is an iterative process - as you modify hello various functions and parameters of your experiment, your results converge until you are satisfied that you have a trained, effective model.</span></span> <span data-ttu-id="c7210-105">索引鍵 toothis 程序為追蹤 hello 您實驗參數和組態的各個反覆項目。</span><span class="sxs-lookup"><span data-stu-id="c7210-105">Key toothis process is tracking hello various iterations of your experiment parameters and configurations.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="c7210-106">您可以檢閱先前執行的順序 toochallenge 中隨時將實驗，再次瀏覽，以及最終確認或精簡先前的假設。</span><span class="sxs-lookup"><span data-stu-id="c7210-106">You can review previous runs of your experiments at any time in order toochallenge, revisit, and ultimately either confirm or refine previous assumptions.</span></span> <span data-ttu-id="c7210-107">當您執行實驗時，Machine Learning Studio 就會保留記錄的 hello 執行，包括資料集、 模組和連接埠的連線和參數。</span><span class="sxs-lookup"><span data-stu-id="c7210-107">When you run an experiment, Machine Learning Studio keeps a history of hello run, including dataset, module, and port connections and parameters.</span></span> <span data-ttu-id="c7210-108">此歷程記錄也會擷取結果、執行階段資訊，例如開始和停止時間、記錄訊息及執行狀態。</span><span class="sxs-lookup"><span data-stu-id="c7210-108">This history also captures results, runtime information such as start and stop times, log messages, and execution status.</span></span> <span data-ttu-id="c7210-109">您可以回頭查看以前在任何這些就會在您的實驗和中繼結果的任何時間 tooreview hello 時序。</span><span class="sxs-lookup"><span data-stu-id="c7210-109">You can look back at any of these runs at any time tooreview hello chronology of your experiment and intermediate results.</span></span> <span data-ttu-id="c7210-110">您甚至可以使用到新的查詢和探索階段的先前執行的實驗 toolaunch 上您路徑 toocreating 簡單、 複雜或甚至集團模型方案。</span><span class="sxs-lookup"><span data-stu-id="c7210-110">You can even use a previous run of your experiment toolaunch into a new phase of inquiry and discovery on your path toocreating simple, complex, or even ensemble modeling solutions.</span></span>

> [!NOTE]
> <span data-ttu-id="c7210-111">當您檢視先前執行的實驗時，hello 實驗該版本已鎖定且無法編輯。</span><span class="sxs-lookup"><span data-stu-id="c7210-111">When you view a previous run of an experiment, that version of hello experiment is locked and can't be edited.</span></span> <span data-ttu-id="c7210-112">按一下，您可以不過，儲存一份**SAVE AS**並提供 hello 複製的新名稱。</span><span class="sxs-lookup"><span data-stu-id="c7210-112">You can, however, save a copy of it by clicking **SAVE AS** and providing a new name for hello copy.</span></span> <span data-ttu-id="c7210-113">Machine Learning Studio 中開啟 hello 新的複本，您可以編輯並執行。</span><span class="sxs-lookup"><span data-stu-id="c7210-113">Machine Learning Studio opens hello new copy, which you can then edit and run.</span></span> <span data-ttu-id="c7210-114">這份實驗位於 hello**實驗**清單以及所有您其他實驗。</span><span class="sxs-lookup"><span data-stu-id="c7210-114">This copy of your experiment is available in hello **EXPERIMENTS** list along with all your other experiments.</span></span>
> 
> 

## <a name="viewing-hello-prior-run"></a><span data-ttu-id="c7210-115">檢視先前執行的 hello</span><span class="sxs-lookup"><span data-stu-id="c7210-115">Viewing hello Prior Run</span></span>
<span data-ttu-id="c7210-116">當您有已開啟您已至少一次執行的實驗時，您可以檢視依序按一下之前執行 hello 實驗的 hello**先前執行**hello 屬性 窗格中。</span><span class="sxs-lookup"><span data-stu-id="c7210-116">When you have an experiment open that you have run at least once, you can view hello preceding run of hello experiment by clicking **Prior Run** in hello properties pane.</span></span>

<span data-ttu-id="c7210-117">例如，假設您建立實驗並且在下列時間執行其版本：11:23、11:42 及 11:55。</span><span class="sxs-lookup"><span data-stu-id="c7210-117">For example, suppose you create an experiment and run versions of it at 11:23, 11:42, and 11:55.</span></span> <span data-ttu-id="c7210-118">如果您開啟 hello 上次執行 hello 實驗 (11:55)，然後按一下**先前執行**，開啟您執行在 11:42 hello 版本。</span><span class="sxs-lookup"><span data-stu-id="c7210-118">If you open hello last run of hello experiment (11:55) and click **Prior Run**, hello version you ran at 11:42 is opened.</span></span>

## <a name="viewing-hello-run-history"></a><span data-ttu-id="c7210-119">檢視 hello 執行歷程記錄</span><span class="sxs-lookup"><span data-stu-id="c7210-119">Viewing hello Run History</span></span>
<span data-ttu-id="c7210-120">按一下即可檢視所有的 hello 先前執行的實驗**檢視執行記錄**開啟實驗中。</span><span class="sxs-lookup"><span data-stu-id="c7210-120">You can view all hello previous runs of an experiment by clicking **View Run History** in an open experiment.</span></span>

<span data-ttu-id="c7210-121">例如，假設您建立以 hello 的實驗[線性迴歸][ linear-regression]模組，而且您想要變更的 hello 值 tooobserve hello 影響**學習速率**上您的實驗結果。</span><span class="sxs-lookup"><span data-stu-id="c7210-121">For example, suppose you create an experiment with hello [Linear Regression][linear-regression] module and you want tooobserve hello effect of changing hello value of **Learning rate** on your experiment results.</span></span> <span data-ttu-id="c7210-122">Hello 實驗多次執行具有不同的值，這個參數，如，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c7210-122">You run hello experiment multiple times with different values for this parameter, as follows:</span></span>

| <span data-ttu-id="c7210-123">學習速度值</span><span class="sxs-lookup"><span data-stu-id="c7210-123">Learning Rate value</span></span> | <span data-ttu-id="c7210-124">執行開始時間</span><span class="sxs-lookup"><span data-stu-id="c7210-124">Run start time</span></span> |
| --- | --- |
| <span data-ttu-id="c7210-125">0.1</span><span class="sxs-lookup"><span data-stu-id="c7210-125">0.1</span></span> |<span data-ttu-id="c7210-126">2014/9/11 下午 4:18:58</span><span class="sxs-lookup"><span data-stu-id="c7210-126">9/11/2014 4:18:58 pm</span></span> |
| <span data-ttu-id="c7210-127">0.2</span><span class="sxs-lookup"><span data-stu-id="c7210-127">0.2</span></span> |<span data-ttu-id="c7210-128">2014/9/11 下午 4:24:33</span><span class="sxs-lookup"><span data-stu-id="c7210-128">9/11/2014 4:24:33 pm</span></span> |
| <span data-ttu-id="c7210-129">0.4</span><span class="sxs-lookup"><span data-stu-id="c7210-129">0.4</span></span> |<span data-ttu-id="c7210-130">2014/9/11 下午 4:28:36</span><span class="sxs-lookup"><span data-stu-id="c7210-130">9/11/2014 4:28:36 pm</span></span> |
| <span data-ttu-id="c7210-131">0.5</span><span class="sxs-lookup"><span data-stu-id="c7210-131">0.5</span></span> |<span data-ttu-id="c7210-132">2014/9/11 下午 4:33:31</span><span class="sxs-lookup"><span data-stu-id="c7210-132">9/11/2014 4:33:31 pm</span></span> |

<span data-ttu-id="c7210-133">如果您按一下 [ **檢視執行歷程記錄**]，您會看見所有執行的清單：</span><span class="sxs-lookup"><span data-stu-id="c7210-133">If you click **VIEW RUN HISTORY**, you see a list of all these runs:</span></span>

![範例執行歷程記錄][runhistory]

<span data-ttu-id="c7210-135">按一下任何這些執行 tooview，在您執行的 hello 階段實驗 hello 的快照集。</span><span class="sxs-lookup"><span data-stu-id="c7210-135">Click any of these runs tooview a snapshot of hello experiment at hello time you ran it.</span></span> <span data-ttu-id="c7210-136">hello 組態、 參數值、 註解，以及結果是所有保留的 toogive 您的實驗執行的完整記錄。</span><span class="sxs-lookup"><span data-stu-id="c7210-136">hello configuration, parameter values, comments, and results are all preserved toogive you a complete record of that run of your experiment.</span></span>

> [!TIP]
> <span data-ttu-id="c7210-137">toodocument hello 實驗的反覆項目，您可以修改 hello 標題每次執行它，您可以更新 hello**摘要**hello 的試驗 hello 屬性 窗格中，您可以新增或更新個別的模組上的註解toorecord 您的變更。</span><span class="sxs-lookup"><span data-stu-id="c7210-137">toodocument your iterations of hello experiment, you can modify hello title each time you run it, you can update hello **Summary** of hello experiment in hello properties pane, and you can add or update comments on individual modules toorecord your changes.</span></span> <span data-ttu-id="c7210-138">hello 標題、 摘要和模組註解會儲存與 hello 實驗每次執行。</span><span class="sxs-lookup"><span data-stu-id="c7210-138">hello title, summary, and module comments are saved with each run of hello experiment.</span></span>
> 
> 

<span data-ttu-id="c7210-139">hello 的實驗 hello 清單**實驗**Machine Learning Studio 中的索引標籤一律會顯示 hello 的實驗的最新版本。</span><span class="sxs-lookup"><span data-stu-id="c7210-139">hello list of experiments in hello **EXPERIMENTS** tab in Machine Learning Studio always displays hello latest version of an experiment.</span></span> <span data-ttu-id="c7210-140">如果您開啟先前 hello 實驗執行 (使用**先前執行**或**檢視執行記錄**)，您可以按一下傳回 toohello 草稿版本**檢視執行記錄**，然後選取hello 反覆項目具有**狀態**的**編輯**。</span><span class="sxs-lookup"><span data-stu-id="c7210-140">If you open a previous run of hello experiment (using **Prior Run** or **VIEW RUN HISTORY**), you can return toohello draft version by clicking **VIEW RUN HISTORY** and selecting hello iteration that has a **STATE** of **Editable**.</span></span>

## <a name="iterating-on-a-previous-run"></a><span data-ttu-id="c7210-141">逐一查看上一次執行</span><span class="sxs-lookup"><span data-stu-id="c7210-141">Iterating on a Previous Run</span></span>
<span data-ttu-id="c7210-142">當您按一下 [上一次執行] 或 [檢視執行歷程記錄]，並且開啟上一次執行時，您可以在唯讀模式中檢視完成的實驗。</span><span class="sxs-lookup"><span data-stu-id="c7210-142">When you click **Prior Run** or **VIEW RUN HISTORY** and open a previous run, you can view a finished experiment in read-only mode.</span></span>

<span data-ttu-id="c7210-143">如果您想 toobegin 實驗開頭 hello 方式針對先前執行的反覆項目，您可以開啟 hello 執行，然後按一下**SAVE AS**。</span><span class="sxs-lookup"><span data-stu-id="c7210-143">If you want toobegin an iteration of your experiment starting with hello way you configured it for a previous run, you can do this by opening hello run and clicking **SAVE AS**.</span></span> <span data-ttu-id="c7210-144">這會建立新的實驗中，新的標題、 空的執行歷程記錄，以及所有 hello 元件和執行先前的 hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="c7210-144">This creates a new experiment, with a new title, an empty run history, and all hello components and parameter values of hello previous run.</span></span> <span data-ttu-id="c7210-145">這個新的實驗會列在 hello**實驗** 索引標籤中 hello Machine Learning Studio 首頁上，而且您可以修改並執行它，初始化新執行實驗此反覆項目歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="c7210-145">This new experiment is listed in hello **EXPERIMENTS** tab in hello Machine Learning Studio home page, and you can modify and run it, initiating a new run history for this iteration of your experiment.</span></span> 

<span data-ttu-id="c7210-146">例如，假設您有執行歷程記錄顯示 hello 前一節中的 hello 實驗。</span><span class="sxs-lookup"><span data-stu-id="c7210-146">For example, suppose you have hello experiment run history shown in hello previous section.</span></span> <span data-ttu-id="c7210-147">要設定 hello 時，會發生什麼事 tooobserve**學習速率**參數 too0.4 和不同的值再試一次 hello**定型 epoch 的數目**參數。</span><span class="sxs-lookup"><span data-stu-id="c7210-147">You want tooobserve what happens when you set hello **Learning rate** parameter too0.4, and try different values for hello **Number of training epochs** parameter.</span></span>

1. <span data-ttu-id="c7210-148">按一下**檢視執行記錄**並開啟 hello 實驗下午 4:28:36 （您在其中設定 hello 參數值 too0.4） 執行您的 hello 反覆項目。</span><span class="sxs-lookup"><span data-stu-id="c7210-148">Click **VIEW RUN HISTORY** and open hello iteration of hello experiment that you ran at 4:28:36 pm (in which you set hello parameter value too0.4).</span></span>
2. <span data-ttu-id="c7210-149">按一下 [ **另存新檔**]。</span><span class="sxs-lookup"><span data-stu-id="c7210-149">Click **SAVE AS**.</span></span>
3. <span data-ttu-id="c7210-150">輸入新的標題，然後按一下 hello**確定**核取記號。</span><span class="sxs-lookup"><span data-stu-id="c7210-150">Enter a new title and click hello **OK** checkmark.</span></span> <span data-ttu-id="c7210-151">建立 hello 實驗的新複本。</span><span class="sxs-lookup"><span data-stu-id="c7210-151">A new copy of hello experiment is created.</span></span>
4. <span data-ttu-id="c7210-152">修改 hello**定型 epoch 的數目**參數。</span><span class="sxs-lookup"><span data-stu-id="c7210-152">Modify hello **Number of training epochs** parameter.</span></span>
5. <span data-ttu-id="c7210-153">按一下 [ **執行**]。</span><span class="sxs-lookup"><span data-stu-id="c7210-153">Click **RUN**.</span></span>

<span data-ttu-id="c7210-154">您現在可以繼續 toomodify 並執行您的經驗，此版本建立新的執行歷程記錄 toorecord 您的工作。</span><span class="sxs-lookup"><span data-stu-id="c7210-154">You can now continue toomodify and run this version of your experiment, building a new run history toorecord your work.</span></span>

<!-- Images -->
[runhistory]:./media/machine-learning-manage-experiment-iterations/viewrunhistory.jpg


<!-- Module References -->
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
