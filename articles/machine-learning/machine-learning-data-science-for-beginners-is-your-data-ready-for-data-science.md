---
title: "您的資料已準備用於資料科學 aaaIs 嗎？ 資料評估 - Azure Machine Learning | Microsoft Docs"
description: "了解準備好用於資料科學資料 toobe hello 4 準則。 適用於初學者視訊 2 的資料科學的具體範例 toohelp 基本資料評估。"
keywords: "相關的資料, 評估資料, 準備資料, 資料準則, 備妥資料"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: d502062c-da70-4b21-9054-0bfd9902612e
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: ef6bb680ace771537157dbdd50a4ccce0a3eb7ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="is-your-data-ready-for-data-science"></a><span data-ttu-id="491c2-106">已備妥資料來進行資料科學嗎？</span><span class="sxs-lookup"><span data-stu-id="491c2-106">Is your data ready for data science?</span></span>
## <a name="video-2-data-science-for-beginners-series"></a><span data-ttu-id="491c2-107">影片 2：適用於初學者的資料科學系列</span><span class="sxs-lookup"><span data-stu-id="491c2-107">Video 2: Data Science for Beginners series</span></span>
<span data-ttu-id="491c2-108">深入了解如何 tooevaluate 您資料 toomake 確定它符合基本的準則 toobe 準備用於資料科學。</span><span class="sxs-lookup"><span data-stu-id="491c2-108">Learn how tooevaluate your data toomake sure it meets basic criteria toobe ready for data science.</span></span>

<span data-ttu-id="491c2-109">充分利用 hello 數列 tooget hello 觀賞全部。</span><span class="sxs-lookup"><span data-stu-id="491c2-109">tooget hello most out of hello series, watch them all.</span></span> <span data-ttu-id="491c2-110">[前往影片 toohello 清單](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="491c2-110">[Go toohello list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Shows/SupervisionNotRequired/9/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="491c2-111">系列中的其他影片</span><span class="sxs-lookup"><span data-stu-id="491c2-111">Other videos in this series</span></span>
<span data-ttu-id="491c2-112">*為初學者所設計的資料科學*是快速介紹 toodata 科學中五個簡短的影片。</span><span class="sxs-lookup"><span data-stu-id="491c2-112">*Data Science for Beginners* is a quick introduction toodata science in five short videos.</span></span>

* <span data-ttu-id="491c2-113">視訊 1: [hello 5 個問題的資料科學答案](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *（5 分鐘 14 秒）*</span><span class="sxs-lookup"><span data-stu-id="491c2-113">Video 1: [hello 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="491c2-114">影片 2：您的資料已經可以進行資料科學了嗎？</span><span class="sxs-lookup"><span data-stu-id="491c2-114">Video 2: Is your data ready for data science?</span></span>
* <span data-ttu-id="491c2-115">影片 3：[詢問您可以使用資料回答的問題](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 分 17 秒)*</span><span class="sxs-lookup"><span data-stu-id="491c2-115">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="491c2-116">影片 4：[利用簡單模型預測答案](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 分 42 秒)*</span><span class="sxs-lookup"><span data-stu-id="491c2-116">Video 4: [Predict an answer with a simple model](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span></span>
* <span data-ttu-id="491c2-117">視訊 5:[複製其他人工作 toodo 資料科學](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *（3 分 18 秒）*</span><span class="sxs-lookup"><span data-stu-id="491c2-117">Video 5: [Copy other people's work toodo data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-is-your-data-ready-for-data-science"></a><span data-ttu-id="491c2-118">文字記錄：已備妥資料來進行資料科學嗎？</span><span class="sxs-lookup"><span data-stu-id="491c2-118">Transcript: Is your data ready for data science?</span></span>
<span data-ttu-id="491c2-119">歡迎使用太 」 是您的資料準備用於資料科學？ 」</span><span class="sxs-lookup"><span data-stu-id="491c2-119">Welcome too"Is your data ready for data science?"</span></span> <span data-ttu-id="491c2-120">hello hello 數列中的第二個視訊*為初學者所設計的資料科學*。</span><span class="sxs-lookup"><span data-stu-id="491c2-120">hello second video in hello series *Data Science for Beginners*.</span></span>  

<span data-ttu-id="491c2-121">資料科學可以提供之前 hello 您想要的答案，您必須 toogive 它具有某些高品質原料 toowork。</span><span class="sxs-lookup"><span data-stu-id="491c2-121">Before data science can give you hello answers you want, you have toogive it some high-quality raw materials toowork with.</span></span> <span data-ttu-id="491c2-122">就像進行披薩，hello 您開始使用，更好 hello 食材更 hello hello 最終產品。</span><span class="sxs-lookup"><span data-stu-id="491c2-122">Just like making a pizza, hello better hello ingredients you start with, hello better hello final product.</span></span> 

## <a name="criteria-for-data"></a><span data-ttu-id="491c2-123">資料準則</span><span class="sxs-lookup"><span data-stu-id="491c2-123">Criteria for data</span></span>
<span data-ttu-id="491c2-124">因此，在資料科學的其中一個 hello 情況下，會有一些因素，我們需要 toopull 一起。</span><span class="sxs-lookup"><span data-stu-id="491c2-124">So, in hello case of data science, there are some ingredients that we need toopull together.</span></span>

<span data-ttu-id="491c2-125">我們所需的資料是：</span><span class="sxs-lookup"><span data-stu-id="491c2-125">We need data that is:</span></span>

* <span data-ttu-id="491c2-126">相關</span><span class="sxs-lookup"><span data-stu-id="491c2-126">Relevant</span></span>
* <span data-ttu-id="491c2-127">連線</span><span class="sxs-lookup"><span data-stu-id="491c2-127">Connected</span></span>
* <span data-ttu-id="491c2-128">精確</span><span class="sxs-lookup"><span data-stu-id="491c2-128">Accurate</span></span>
* <span data-ttu-id="491c2-129">具有足夠 toowork</span><span class="sxs-lookup"><span data-stu-id="491c2-129">Enough toowork with</span></span>

## <a name="is-your-data-relevant"></a><span data-ttu-id="491c2-130">您的資料有相關性嗎？</span><span class="sxs-lookup"><span data-stu-id="491c2-130">Is your data relevant?</span></span>
<span data-ttu-id="491c2-131">因此第一個因素 hello-我們需要的相關資料。</span><span class="sxs-lookup"><span data-stu-id="491c2-131">So hello first ingredient - we need data that's relevant.</span></span>

![相關的資料與無關的資料 - 評估資料](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/relevant-and-irrelevant-data.png)

<span data-ttu-id="491c2-133">查看 hello 資料表 hello 左側。</span><span class="sxs-lookup"><span data-stu-id="491c2-133">Look at hello table on hello left.</span></span> <span data-ttu-id="491c2-134">我們符合波士頓橫條外部的七個人員的測量其捐血酒精層級、 hello 紅襪隊打擊，在他們的最後一個遊戲和牛奶 hello 最接近的方便存放區中的 hello 價格。</span><span class="sxs-lookup"><span data-stu-id="491c2-134">We met seven people outside of Boston bars, measured their blood alcohol level, hello Red Sox batting average in their last game, and hello price of milk in hello nearest convenience store.</span></span>

<span data-ttu-id="491c2-135">這一切都是合法的資料。</span><span class="sxs-lookup"><span data-stu-id="491c2-135">This is all perfectly legitimate data.</span></span> <span data-ttu-id="491c2-136">唯一的缺點是它們並不相關。</span><span class="sxs-lookup"><span data-stu-id="491c2-136">It’s only fault is that it isn’t relevant.</span></span> <span data-ttu-id="491c2-137">這些數字之間沒有任何明顯的關聯性。</span><span class="sxs-lookup"><span data-stu-id="491c2-137">There's no obvious relationship between these numbers.</span></span> <span data-ttu-id="491c2-138">如果提供 hello 牛奶和 hello 紅襪隊打擊股票的現價，沒有任何方法，您無法猜測我捐血酒精內容。</span><span class="sxs-lookup"><span data-stu-id="491c2-138">If I gave you hello current price of milk and hello Red Sox batting average, there's no way you could guess my blood alcohol content.</span></span>

<span data-ttu-id="491c2-139">現在查看 hello 資料表上 hello 右。</span><span class="sxs-lookup"><span data-stu-id="491c2-139">Now look at hello table on hello right.</span></span> <span data-ttu-id="491c2-140">這次我們測量每個人的主體大型和計數的 hello 時會將它們過數目。</span><span class="sxs-lookup"><span data-stu-id="491c2-140">This time we measured each person’s body mass and counted hello number of drinks they’ve had.</span></span>  <span data-ttu-id="491c2-141">每個資料列中的 hello 數字現在為相關 tooeach 其他。</span><span class="sxs-lookup"><span data-stu-id="491c2-141">hello numbers in each row are now relevant tooeach other.</span></span> <span data-ttu-id="491c2-142">如果帶給您 Margaritas 我有我主體大型與 hello 號碼，您可以建立在我的捐血猜測酒精內容。</span><span class="sxs-lookup"><span data-stu-id="491c2-142">If I gave you my body mass and hello number of Margaritas I've had, you could make a guess at my blood alcohol content.</span></span>

## <a name="do-you-have-connected-data"></a><span data-ttu-id="491c2-143">是否有連貫的資料？</span><span class="sxs-lookup"><span data-stu-id="491c2-143">Do you have connected data?</span></span>
<span data-ttu-id="491c2-144">hello 下一個因素是連接的資料。</span><span class="sxs-lookup"><span data-stu-id="491c2-144">hello next ingredient is connected data.</span></span>

![連接的資料與中斷連接的資料 - 資料準則、備妥資料](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/connected-vs-disconnected-data.png)

<span data-ttu-id="491c2-146">以下是一些漢堡 hello 品質相關的資料： grill 溫度、 patty 加權和 hello 本機食物雜誌中的評等。</span><span class="sxs-lookup"><span data-stu-id="491c2-146">Here is some relevant data on hello quality of hamburgers: grill temperature, patty weight, and rating in hello local food magazine.</span></span> <span data-ttu-id="491c2-147">但請注意在 hello 左邊 hello 資料表中的 hello 間距。</span><span class="sxs-lookup"><span data-stu-id="491c2-147">But notice hello gaps in hello table on hello left.</span></span>

<span data-ttu-id="491c2-148">大部分的資料集遺漏了某些值。</span><span class="sxs-lookup"><span data-stu-id="491c2-148">Most data sets are missing some values.</span></span> <span data-ttu-id="491c2-149">就像這樣的一般 toohave 漏洞而且沒有方法 toowork 周圍。</span><span class="sxs-lookup"><span data-stu-id="491c2-149">It's common toohave holes like this and there are ways toowork around them.</span></span> <span data-ttu-id="491c2-150">不過如果有太多遺失，您的資料開始 toolook 瑞士 cheese 類似。</span><span class="sxs-lookup"><span data-stu-id="491c2-150">But if there's too much missing, your data begins toolook like Swiss cheese.</span></span>

<span data-ttu-id="491c2-151">Hello 左側查看 hello 資料表，如果沒有而遺失的資料量與任何一種之間的關聯性的硬式 toocome 向上 grill 溫度和 patty 權數。</span><span class="sxs-lookup"><span data-stu-id="491c2-151">If you look at hello table on hello left, there's so much missing data, it's hard toocome up with any kind of relationship between grill temperature and patty weight.</span></span> <span data-ttu-id="491c2-152">這是連貫性中斷的資料範例。</span><span class="sxs-lookup"><span data-stu-id="491c2-152">This is an example of disconnected data.</span></span>

<span data-ttu-id="491c2-153">雖然 hello hello 右側資料表中，已滿，而且完成-已連接資料的範例。</span><span class="sxs-lookup"><span data-stu-id="491c2-153">hello table on hello right, though, is full and complete - an example of connected data.</span></span>

## <a name="is-your-data-accurate"></a><span data-ttu-id="491c2-154">是您的資料精確嗎？</span><span class="sxs-lookup"><span data-stu-id="491c2-154">Is your data accurate?</span></span>
<span data-ttu-id="491c2-155">hello 我們需要的下一個因素是精確度。</span><span class="sxs-lookup"><span data-stu-id="491c2-155">hello next ingredient we need is accuracy.</span></span> <span data-ttu-id="491c2-156">以下是我們都希望 toohit 箭號的四個目標。</span><span class="sxs-lookup"><span data-stu-id="491c2-156">Here are four targets that we’d like toohit with arrows.</span></span>

![準確的資料與不準確的資料 - 資料準則](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/inaccurate-vs-accurate-data.png)

<span data-ttu-id="491c2-158">查看 hello hello 右上角的目標。</span><span class="sxs-lookup"><span data-stu-id="491c2-158">Look at hello target in hello upper right.</span></span> <span data-ttu-id="491c2-159">我們必須要 hello 準星型的緊密群組。</span><span class="sxs-lookup"><span data-stu-id="491c2-159">We’ve got a tight grouping right around hello bullseye.</span></span> <span data-ttu-id="491c2-160">當然這是精確的。</span><span class="sxs-lookup"><span data-stu-id="491c2-160">That, of course, is accurate.</span></span> <span data-ttu-id="491c2-161">有，在資料科學的其中一個 hello 語言中，我們在其下的 hello 目標右邊的效能也會被視為正確。</span><span class="sxs-lookup"><span data-stu-id="491c2-161">Oddly, in hello language of data science, our performance on hello target right below it is also considered accurate.</span></span>

<span data-ttu-id="491c2-162">如果您 toomap hello 中心的這些箭號，您會看到這是非常接近 toohello 準星型。</span><span class="sxs-lookup"><span data-stu-id="491c2-162">If you were toomap out hello center of these arrows, you'd see that it's very close toohello bullseye.</span></span> <span data-ttu-id="491c2-163">hello 箭號分布周圍 hello 目標，因此被視為不精確，但它們為主 hello 準星型，所以正在被視為正確。</span><span class="sxs-lookup"><span data-stu-id="491c2-163">hello arrows are spread out all around hello target, so they're considered imprecise, but they're centered around hello bullseye, so they're considered accurate.</span></span>

<span data-ttu-id="491c2-164">現在查看 hello 左上方的目標。</span><span class="sxs-lookup"><span data-stu-id="491c2-164">Now look at hello upper-left target.</span></span> <span data-ttu-id="491c2-165">此處，我們的箭射中得非常接近，是一個緊密的群組。</span><span class="sxs-lookup"><span data-stu-id="491c2-165">Here our arrows hit very close together, a tight grouping.</span></span> <span data-ttu-id="491c2-166">它們是精確，但因為 hello 中心是關閉 hello 準星型的方式不正確。</span><span class="sxs-lookup"><span data-stu-id="491c2-166">They're precise, but they're inaccurate because hello center is way off hello bullseye.</span></span> <span data-ttu-id="491c2-167">此外，當然 hello 左下方目標中的 hello 箭號會不正確且不精確。</span><span class="sxs-lookup"><span data-stu-id="491c2-167">And, of course, hello arrows in hello bottom-left target are both inaccurate and imprecise.</span></span> <span data-ttu-id="491c2-168">這位弓箭手需要多加練習。</span><span class="sxs-lookup"><span data-stu-id="491c2-168">This archer needs more practice.</span></span>

## <a name="do-you-have-enough-data-toowork-with"></a><span data-ttu-id="491c2-169">您有足夠的資料 toowork 與嗎？</span><span class="sxs-lookup"><span data-stu-id="491c2-169">Do you have enough data toowork with?</span></span>
<span data-ttu-id="491c2-170">最後，成分 #4-toohave 我們需要足夠的資料。</span><span class="sxs-lookup"><span data-stu-id="491c2-170">Finally, ingredient #4 - we need toohave enough data.</span></span>

![您是否有足夠資料可進行分析？](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/barely-enough-data.png)

<span data-ttu-id="491c2-173">將表格中的每一個資料點視為繪圖中的筆刷筆劃。</span><span class="sxs-lookup"><span data-stu-id="491c2-173">Think of each data point in your table as being a brush stroke in a painting.</span></span> <span data-ttu-id="491c2-174">如果您有只有少數幾個、 hello 繪製可以是很模糊： 很難 tootell 它為何。</span><span class="sxs-lookup"><span data-stu-id="491c2-174">If you have only a few of them, hello painting can be pretty fuzzy - it's hard tootell what it is.</span></span>

<span data-ttu-id="491c2-175">如果您加入一些其他的筆刷筆觸，您繪製啟動 tooget 小清晰。</span><span class="sxs-lookup"><span data-stu-id="491c2-175">If you add some more brush strokes, then your painting starts tooget a little sharper.</span></span>

<span data-ttu-id="491c2-176">當您擁有足夠幾乎筆劃時，您可以看到剛才足夠 toomake 一些廣泛的決策。</span><span class="sxs-lookup"><span data-stu-id="491c2-176">When you have barely enough strokes, you can see just enough toomake some broad decisions.</span></span> <span data-ttu-id="491c2-177">它是可以 toovisit 的地方嗎？</span><span class="sxs-lookup"><span data-stu-id="491c2-177">Is it somewhere I might want toovisit?</span></span> <span data-ttu-id="491c2-178">它看起來很明亮，看起來像潔淨的水 – 沒錯，這就是我想要度假的地方。</span><span class="sxs-lookup"><span data-stu-id="491c2-178">It looks bright, that looks like clean water – yes, that’s where I’m going on vacation.</span></span>

<span data-ttu-id="491c2-179">當您加入更多資料，hello 圖片變得更清楚，您可以做出更詳細的決策。</span><span class="sxs-lookup"><span data-stu-id="491c2-179">As you add more data, hello picture becomes clearer and you can make more detailed decisions.</span></span> <span data-ttu-id="491c2-180">現在我可以查看 hello hello 左銀行上的三個旅館。</span><span class="sxs-lookup"><span data-stu-id="491c2-180">Now I can look at hello three hotels on hello left bank.</span></span> <span data-ttu-id="491c2-181">好了，喜歡 hello 的 hello 前景 hello 一個架構的功能。</span><span class="sxs-lookup"><span data-stu-id="491c2-181">You know, I really like hello architectural features of hello one in hello foreground.</span></span> <span data-ttu-id="491c2-182">我將會留在那裡，hello 第三個樓層。</span><span class="sxs-lookup"><span data-stu-id="491c2-182">I’ll stay there, on hello third floor.</span></span>

<span data-ttu-id="491c2-183">相關、 連線、 正確的資料並不夠，我們有所有的 hello 因素，我們需要 toodo 某些高品質資料科學。</span><span class="sxs-lookup"><span data-stu-id="491c2-183">With data that's relevant, connected, accurate, and enough, we have all hello ingredients we need toodo some high-quality data science.</span></span>

<span data-ttu-id="491c2-184">在其他四個視訊是確定 toocheck 出 hello*為初學者所設計的資料科學*從 Microsoft Azure 機器學習。</span><span class="sxs-lookup"><span data-stu-id="491c2-184">Be sure toocheck out hello other four videos in *Data Science for Beginners* from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="491c2-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="491c2-185">Next steps</span></span>
* [<span data-ttu-id="491c2-186">嘗試使用 Machine Learning Studio 進行您的第一個資料科學實驗</span><span class="sxs-lookup"><span data-stu-id="491c2-186">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="491c2-187">取得簡介 tooMachine Microsoft Azure 上學習</span><span class="sxs-lookup"><span data-stu-id="491c2-187">Get an introduction tooMachine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)
