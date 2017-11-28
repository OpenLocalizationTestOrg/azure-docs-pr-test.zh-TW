---
title: "Cortana Intelligence Gallery 自訂模組 | Microsoft Docs"
description: "探索 Cortana Intelligence Gallery 中的自訂機器學習服務模組。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 16037a84-dad0-4a8c-9874-a1d3bd551cf0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: roopalik;garye
ms.openlocfilehash: 56c308643ad6d20170174725f76f6ddbc76b3e22
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="discover-custom-machine-learning-modules-in-cortana-intelligence-gallery"></a><span data-ttu-id="bc1d8-103">探索 Cortana Intelligence Gallery 中的自訂機器學習服務模組</span><span class="sxs-lookup"><span data-stu-id="bc1d8-103">Discover custom machine learning modules in Cortana Intelligence Gallery</span></span>
[!INCLUDE [machine-learning-gallery-item-selector](../../includes/machine-learning-gallery-item-selector.md)]

## <a name="custom-modules-for-machine-learning-studio"></a><span data-ttu-id="bc1d8-104">Machine Learning studio 的自訂模組</span><span class="sxs-lookup"><span data-stu-id="bc1d8-104">Custom modules for Machine Learning Studio</span></span>
<span data-ttu-id="bc1d8-105">Cortana Intelligence Gallery 提供數個[自訂模組](https://gallery.cortanaintelligence.com/customModules)，可擴充 Azure Machine Learning Studio 的功能。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-105">Cortana Intelligence Gallery offers several [custom modules](https://gallery.cortanaintelligence.com/customModules) that expand the capabilities of Azure Machine Learning Studio.</span></span> <span data-ttu-id="bc1d8-106">您可以匯入這些模組用於您的實驗，以便開發更進階的預測性分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-106">You can import the modules to use in your experiments, so you can develop even more advanced predictive analytics solutions.</span></span>

<span data-ttu-id="bc1d8-107">目前，Gallery 提供*時間序列分析**關聯規則**叢集演算法*(k-means 除外) 和*視覺效果*，以及其他的主力公用程式模組。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-107">Currently, the Gallery offers modules on *time series analytics*, *association rules*, *clustering algorithms* (beyond k-means), and *visualizations*, and other workhorse utility modules.</span></span>


## <a name="discover"></a><span data-ttu-id="bc1d8-108">探索</span><span class="sxs-lookup"><span data-stu-id="bc1d8-108">Discover</span></span>
<span data-ttu-id="bc1d8-109">若要瀏覽 [Gallery 中的](http://gallery.cortanaintelligence.com)自訂模組，請在 [更多] 下方選取 [自訂模組]。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-109">To browse custom modules [in the Gallery](http://gallery.cortanaintelligence.com), under **More**, select **Custom Modules**.</span></span>

![選取 Gallery 首頁上的自訂模組](media/machine-learning-gallery-custom-modules/select-custom-modules-in-gallery.png)

<span data-ttu-id="bc1d8-111">**[自訂模組](https://gallery.cortanaintelligence.com/customModules)**頁面會顯示最近新增及熱門的模組清單。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-111">The **[Custom Modules](https://gallery.cortanaintelligence.com/customModules)** page displays a list of recently added and popular modules.</span></span> <span data-ttu-id="bc1d8-112">若要檢視所有的自訂模組，請選取 [查看全部] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-112">To view all custom modules, select the **See all** button.</span></span> <span data-ttu-id="bc1d8-113">若要搜尋特定的自訂模組，請選取 [查看全部]，然後選取篩選準則。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-113">To search for a specific custom module, select **See all**, and then select filter criteria.</span></span> <span data-ttu-id="bc1d8-114">您也可以在資源庫頁面頂端的 [搜尋] 方塊中輸入搜尋字詞。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-114">You also can enter search terms in the **Search** box at the top of the Gallery page.</span></span>

![選取 [查看全部] 可瀏覽所有的自訂模組](media/machine-learning-gallery-custom-modules/click-see-all-for-all-custom-modules.png)

### <a name="understand"></a><span data-ttu-id="bc1d8-116">了解</span><span class="sxs-lookup"><span data-stu-id="bc1d8-116">Understand</span></span>

<span data-ttu-id="bc1d8-117">若要了解已發佈的自訂模組如何運作，請選取自訂模組開啟模組詳細資料頁面。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-117">To understand how a published custom module works, select the custom module to open the module details page.</span></span> <span data-ttu-id="bc1d8-118">詳細資料頁面可提供一致且資訊豐富的學習經驗。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-118">The details page delivers a consistent and informative learning experience.</span></span> <span data-ttu-id="bc1d8-119">例如，詳細資料頁面會反白顯示模組目的，並列出預期的輸入、輸出和參數。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-119">For example, the details page highlights the purpose of the module, and it lists expected inputs, outputs, and parameters.</span></span> <span data-ttu-id="bc1d8-120">詳細資料頁面也提供基礎原始程式碼的連結，讓您可以檢查和自訂程式碼。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-120">The details page also has a link to the underlying source code, which you can examine and customize.</span></span>

### <a name="comment-and-share"></a><span data-ttu-id="bc1d8-121">註解和共用</span><span class="sxs-lookup"><span data-stu-id="bc1d8-121">Comment and share</span></span>
<span data-ttu-id="bc1d8-122">在自訂模組詳細資料頁面上的 [註解] 區段中，您可以留言、提供意見反應，或詢問有關模組的問題。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-122">On a custom module details page, in the **Comments** section, you can comment, provide feedback, or ask questions about the module.</span></span> <span data-ttu-id="bc1d8-123">您甚至可以在 Twitter 或 LinkedIn 上與朋友或同事分享模組。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-123">You can even share the module with friends or colleagues on Twitter or LinkedIn.</span></span> <span data-ttu-id="bc1d8-124">您也可以用電子郵件寄出模組詳細資料頁面連結，以邀請其他使用者檢視該頁面。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-124">You also can email a link to the module details page, to invite other users to view the page.</span></span>

![與朋友分享此項目](media/machine-learning-gallery-how-to-use-contribute-publish/share-links.png)

![新增您自己的留言](media/machine-learning-gallery-how-to-use-contribute-publish/comments.png)

## <a name="import"></a><span data-ttu-id="bc1d8-127">Import</span><span class="sxs-lookup"><span data-stu-id="bc1d8-127">Import</span></span>
<span data-ttu-id="bc1d8-128">您可以從 Gallery 將任何自訂模組匯入到您自己的實驗中。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-128">You can import any custom module from the Gallery to your own experiments.</span></span>

<span data-ttu-id="bc1d8-129">Cortana Intelligence Gallery 提供兩種匯入模組複本的方式：</span><span class="sxs-lookup"><span data-stu-id="bc1d8-129">Cortana Intelligence Gallery offers two ways to import a copy of the module:</span></span>

* <span data-ttu-id="bc1d8-130">**從 Gallery**。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-130">**From the Gallery**.</span></span> <span data-ttu-id="bc1d8-131">當您從 Gallery 匯入自訂模組，您也會獲得範例實驗，以舉例說明如何使用模組。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-131">When you import a custom module from the Gallery, you also get a sample experiment that gives you an example of how to use the module.</span></span>
* <span data-ttu-id="bc1d8-132">**從 Machine Learning Studio 內**。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-132">**From within Machine Learning Studio**.</span></span> <span data-ttu-id="bc1d8-133">您可以在使用 Machine Learning Studio 時，可以匯入任何自訂模組 (在此狀況下，您無法取得範例實驗)。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-133">You can import any custom module while you're working in Machine Learning Studio (in this case, you don't get the sample experiment).</span></span>

### <a name="from-the-gallery"></a><span data-ttu-id="bc1d8-134">從 Gallery</span><span class="sxs-lookup"><span data-stu-id="bc1d8-134">From the Gallery</span></span>

1. <span data-ttu-id="bc1d8-135">在 Gallery 中開啟模組詳細資料頁面。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-135">In the Gallery, open the module details page.</span></span> 
2. <span data-ttu-id="bc1d8-136">選取 [在 Studio 中開啟]。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-136">Select **Open in Studio**.</span></span>
   
    ![從 Gallery 開啟自訂模組](media/machine-learning-gallery-custom-modules/open-custom-module-from-gallery.png)
   
<span data-ttu-id="bc1d8-138">每個自訂模組都包含示範如何使用模組的範例實驗。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-138">Each custom module includes a sample experiment that demonstrates how to use the module.</span></span> <span data-ttu-id="bc1d8-139">當您選取 [在 Studio 中開啟]時，範例實驗會在 Machine Learning Studio 工作區中開啟。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-139">When you select **Open in Studio**, the sample experiment opens in your Machine Learning Studio workspace.</span></span> <span data-ttu-id="bc1d8-140">(如果您尚未登入 Studio，會提示您先使用您的 Microsoft 帳戶登入。)</span><span class="sxs-lookup"><span data-stu-id="bc1d8-140">(If you're not already signed in to Studio, you are prompted to first sign in by using your Microsoft account.)</span></span>

<span data-ttu-id="bc1d8-141">除了範例實驗外，自訂模組也會複製到您的工作區。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-141">In addition to the sample experiment, the custom module is copied to your workspace.</span></span> <span data-ttu-id="bc1d8-142">此外，自訂模組會連同所有內建或自訂 Machine Learning Studio 模組一起放在模組選擇區中。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-142">It's also placed in your module palette, with all your built-in or custom Machine Learning Studio modules.</span></span> <span data-ttu-id="bc1d8-143">現在，您可以將自訂模組用於您自己的實驗中，就如同工作區中任何其他的模組。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-143">You can now use it in your own experiments, like any other module in your workspace.</span></span>

### <a name="from-within-machine-learning-studio"></a><span data-ttu-id="bc1d8-144">從 Machine Learning Studio 內</span><span class="sxs-lookup"><span data-stu-id="bc1d8-144">From within Machine Learning Studio</span></span>

1. <span data-ttu-id="bc1d8-145">在 Machine Learning Studio 中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-145">In Machine Learning Studio, select **NEW**.</span></span>
2. <span data-ttu-id="bc1d8-146">選取 [模組]。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-146">Select **Module**.</span></span> <span data-ttu-id="bc1d8-147">您可以從 Gallery 模組清單中選擇，或使用 [搜尋] 方塊尋找特定模組。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-147">You can choose from a list of Gallery modules, or find a specific module by using the **Search** box.</span></span>
3. <span data-ttu-id="bc1d8-148">將滑鼠指向模組，然後選取 [匯入模組]。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-148">Point your mouse at a module, and then select **Import Module**.</span></span> <span data-ttu-id="bc1d8-149">(若要取得模組的相關資訊，請選取 [View in Gallery (在 Gallery 中檢視)]。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-149">(To get information about the module, select **View in Gallery**.</span></span> <span data-ttu-id="bc1d8-150">這會將您帶往 Gallery 中的模組詳細資料頁面。)</span><span class="sxs-lookup"><span data-stu-id="bc1d8-150">This takes you to the module details page in the Gallery.)</span></span>
   
    ![將自訂模組匯入 Machine Learning Studio](media/machine-learning-gallery-custom-modules/add-custom-module-in-studio.png)

<span data-ttu-id="bc1d8-152">自訂模組會複製到您的工作區，並連同內建或自訂的 Machine Learning 模組一起放在模組選擇區中。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-152">The custom module is copied to your workspace and placed in your module palette, with your built-in or custom Machine Learning Studio modules.</span></span> <span data-ttu-id="bc1d8-153">現在，您可以將自訂模組用於您自己的實驗中，就如同工作區中任何其他的模組。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-153">You can now use it in your own experiments, like any other module in your workspace.</span></span>

## <a name="use"></a><span data-ttu-id="bc1d8-154">使用</span><span class="sxs-lookup"><span data-stu-id="bc1d8-154">Use</span></span>

<span data-ttu-id="bc1d8-155">無論您選擇哪一種方式匯入自訂模組，當您匯入模組時，模組會放在 Machine Learning Studio 的模組選擇區中。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-155">Regardless of which method you choose to import a custom module, when you import the module, the module is placed in your module palette in Machine Learning Studio.</span></span> <span data-ttu-id="bc1d8-156">從模組選擇區中，您可以將自訂模組用於工作區中的任何實驗中，就如同任何其他模組一般。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-156">From your module palette, you can use the custom module in any experiment in your workspace, just like any other module.</span></span>

<span data-ttu-id="bc1d8-157">若要使用匯入的模組：</span><span class="sxs-lookup"><span data-stu-id="bc1d8-157">To use an imported module:</span></span>

1. <span data-ttu-id="bc1d8-158">建立實驗，或開啟現有的實驗。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-158">Create an experiment, or open an existing experiment.</span></span>
2. <span data-ttu-id="bc1d8-159">若要展開工作區中的自訂模組清單，在模組選擇區中 [自訂]。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-159">To expand the list of custom modules in your workspace, in the module palette, select **Custom**.</span></span> <span data-ttu-id="bc1d8-160">模組選擇區位在實驗畫布左側。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-160">The module palette is to the left of the experiment canvas.</span></span>
   
    ![Studio 調色盤中的自訂模組清單](media/machine-learning-gallery-custom-modules/custom-module-in-studio-palette.png)
3. <span data-ttu-id="bc1d8-162">選取您匯入的模組，並將它拖曳至您的實驗。</span><span class="sxs-lookup"><span data-stu-id="bc1d8-162">Select the module that you imported, and drag it to your experiment.</span></span>


<span data-ttu-id="bc1d8-163">**[移至資源庫](http://gallery.cortanaintelligence.com)**</span><span class="sxs-lookup"><span data-stu-id="bc1d8-163">**[Go to the Gallery](http://gallery.cortanaintelligence.com)**</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

