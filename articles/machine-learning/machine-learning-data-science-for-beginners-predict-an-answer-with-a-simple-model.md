---
title: "與簡單的迴歸模型-Azure Machine Learning 解答 aaaPredict |Microsoft 文件"
description: "如何 toocreate 簡單的迴歸模型 toopredict 中適用於初學者視訊 4 的資料科學的價格。 包含線性迴歸以及目標資料。"
keywords: "建立模型, 簡單模型, 價格預測, 簡單迴歸模型"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: a28f1fab-e2d8-4663-aa7d-ca3530c8b525
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: d4270c2237c33b7e898b78a08b292bc9d62e49ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="predict-an-answer-with-a-simple-model"></a><span data-ttu-id="fa74b-105">利用簡單模型預測答案</span><span class="sxs-lookup"><span data-stu-id="fa74b-105">Predict an answer with a simple model</span></span>
## <a name="video-4-data-science-for-beginners-series"></a><span data-ttu-id="fa74b-106">影片 4：適用於初學者的資料科學系列</span><span class="sxs-lookup"><span data-stu-id="fa74b-106">Video 4: Data Science for Beginners series</span></span>
<span data-ttu-id="fa74b-107">了解如何 toocreate 簡單的迴歸模型 toopredict hello 中適用於初學者視訊 4 的資料科學鑽石形的價格。</span><span class="sxs-lookup"><span data-stu-id="fa74b-107">Learn how toocreate a simple regression model toopredict hello price of a diamond in Data Science for Beginners video 4.</span></span> <span data-ttu-id="fa74b-108">我們將利用目標資料來繪製迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="fa74b-108">We'll draw a regression model with target data.</span></span>

<span data-ttu-id="fa74b-109">充分利用 hello 數列 tooget hello 觀賞全部。</span><span class="sxs-lookup"><span data-stu-id="fa74b-109">tooget hello most out of hello series, watch them all.</span></span> <span data-ttu-id="fa74b-110">[前往影片 toohello 清單](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="fa74b-110">[Go toohello list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-predict-an-answer-with-a-simple-model/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="fa74b-111">系列中的其他影片</span><span class="sxs-lookup"><span data-stu-id="fa74b-111">Other videos in this series</span></span>
<span data-ttu-id="fa74b-112">*為初學者所設計的資料科學*是快速介紹 toodata 科學中五個簡短的影片。</span><span class="sxs-lookup"><span data-stu-id="fa74b-112">*Data Science for Beginners* is a quick introduction toodata science in five short videos.</span></span>

* <span data-ttu-id="fa74b-113">視訊 1: [hello 5 個問題的資料科學答案](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *（5 分鐘 14 秒）*</span><span class="sxs-lookup"><span data-stu-id="fa74b-113">Video 1: [hello 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="fa74b-114">影片 2： [您的資料已經可以進行資料科學了嗎？](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span><span class="sxs-lookup"><span data-stu-id="fa74b-114">Video 2: [Is your data ready for data science?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span></span> <span data-ttu-id="fa74b-115">*(4 分 56 秒)*</span><span class="sxs-lookup"><span data-stu-id="fa74b-115">*(4 min 56 sec)*</span></span>
* <span data-ttu-id="fa74b-116">影片 3：[詢問您可以使用資料回答的問題](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 分 17 秒)*</span><span class="sxs-lookup"><span data-stu-id="fa74b-116">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="fa74b-117">影片 4：利用簡單模型預測答案</span><span class="sxs-lookup"><span data-stu-id="fa74b-117">Video 4: Predict an answer with a simple model</span></span>
* <span data-ttu-id="fa74b-118">視訊 5:[複製其他人工作 toodo 資料科學](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *（3 分 18 秒）*</span><span class="sxs-lookup"><span data-stu-id="fa74b-118">Video 5: [Copy other people's work toodo data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-predict-an-answer-with-a-simple-model"></a><span data-ttu-id="fa74b-119">文字記錄：利用簡單模型預測答案</span><span class="sxs-lookup"><span data-stu-id="fa74b-119">Transcript: Predict an answer with a simple model</span></span>
<span data-ttu-id="fa74b-120">歡迎使用 toohello hello 」 資料初學者科學"數列中第四個視訊。</span><span class="sxs-lookup"><span data-stu-id="fa74b-120">Welcome toohello fourth video in hello "Data Science for Beginners" series.</span></span> <span data-ttu-id="fa74b-121">在這個影片中，我們將建置簡單模型並進行預測。</span><span class="sxs-lookup"><span data-stu-id="fa74b-121">In this one, we'll build a simple model and make a prediction.</span></span>

<span data-ttu-id="fa74b-122">「模型」  是我們相關資料的簡化敘述。</span><span class="sxs-lookup"><span data-stu-id="fa74b-122">A *model* is a simplified story about our data.</span></span> <span data-ttu-id="fa74b-123">我將告訴您我的意思。</span><span class="sxs-lookup"><span data-stu-id="fa74b-123">I'll show you what I mean.</span></span>

## <a name="collect-relevant-accurate-connected-enough-data"></a><span data-ttu-id="fa74b-124">收集相關、精確、連貫、足夠的資料</span><span class="sxs-lookup"><span data-stu-id="fa74b-124">Collect relevant, accurate, connected, enough data</span></span>
<span data-ttu-id="fa74b-125">假設我想 tooshop 的菱形。</span><span class="sxs-lookup"><span data-stu-id="fa74b-125">Say I want tooshop for a diamond.</span></span> <span data-ttu-id="fa74b-126">我有所屬 toomy 叫 1.35 克拉記號菱形設定信號，我想 tooget 了解它需要多少成本。</span><span class="sxs-lookup"><span data-stu-id="fa74b-126">I have a ring that belonged toomy grandmother with a setting for a 1.35 carat diamond, and I want tooget an idea of how much it will cost.</span></span> <span data-ttu-id="fa74b-127">Hello 珠寶存放區，才能在 記事本 和 畫筆與我記下的所有在 hello 的案例和它們多少權衡 carats hello 菱形 hello 價格。</span><span class="sxs-lookup"><span data-stu-id="fa74b-127">I take a notepad and pen into hello jewelry store, and I write down hello price of all of hello diamonds in hello case and how much they weigh in carats.</span></span> <span data-ttu-id="fa74b-128">正在啟動 hello 第一個菱形-它的 1.01 carats 和 $7,366。</span><span class="sxs-lookup"><span data-stu-id="fa74b-128">Starting with hello first diamond - it's 1.01 carats and $7,366.</span></span>

<span data-ttu-id="fa74b-129">現在我瀏覽，這樣做的所有 hello hello 存放區中的其他菱形。</span><span class="sxs-lookup"><span data-stu-id="fa74b-129">Now I go through and do this for all hello other diamonds in hello store.</span></span>

![鑽石資料欄](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/diamond-data.png)

<span data-ttu-id="fa74b-131">請注意，我們的清單包含兩欄。</span><span class="sxs-lookup"><span data-stu-id="fa74b-131">Notice that our list has two columns.</span></span> <span data-ttu-id="fa74b-132">每欄都有不同的屬性 (克拉數的重量和價格)，而且每一行都是代表單一顆鑽石的單一資料點。</span><span class="sxs-lookup"><span data-stu-id="fa74b-132">Each column has a different attribute - weight in carats and price - and each row is a single data point that represents a single diamond.</span></span>

<span data-ttu-id="fa74b-133">我們實際上在此處建立了一個小型資料集 - 一個表格。</span><span class="sxs-lookup"><span data-stu-id="fa74b-133">We've actually created a small data set here - a table.</span></span> <span data-ttu-id="fa74b-134">請注意，它符合我們對於品質的準則：</span><span class="sxs-lookup"><span data-stu-id="fa74b-134">Notice that it meets our criteria for quality:</span></span>

* <span data-ttu-id="fa74b-135">hello 資料**相關**-加權值是絕對相關的 tooprice</span><span class="sxs-lookup"><span data-stu-id="fa74b-135">hello data is **relevant** - weight is definitely related tooprice</span></span>
* <span data-ttu-id="fa74b-136">它有**精確**-我們重複檢查我們記下的 hello 價格</span><span class="sxs-lookup"><span data-stu-id="fa74b-136">It's **accurate** - we double-checked hello prices that we write down</span></span>
* <span data-ttu-id="fa74b-137">它是 **連貫** 的 - 在這些欄中沒有任何空格</span><span class="sxs-lookup"><span data-stu-id="fa74b-137">It's **connected** - there are no blank spaces in either of these columns</span></span>
* <span data-ttu-id="fa74b-138">而且，如我們所見，它有**足夠**資料 tooanswer 我們的問題</span><span class="sxs-lookup"><span data-stu-id="fa74b-138">And, as we'll see, it's **enough** data tooanswer our question</span></span>

## <a name="ask-a-sharp-question"></a><span data-ttu-id="fa74b-139">詢問明確的問題</span><span class="sxs-lookup"><span data-stu-id="fa74b-139">Ask a sharp question</span></span>
<span data-ttu-id="fa74b-140">現在我們將會顯示我們的問題造成尖的方式:"多少成本 toobuy 1.35 克拉記號菱形？ 」</span><span class="sxs-lookup"><span data-stu-id="fa74b-140">Now we'll pose our question in a sharp way: "How much will it cost toobuy a 1.35 carat diamond?"</span></span>

<span data-ttu-id="fa74b-141">我們沒有 1.35 克拉記號菱形，因此我們必須我們資料 tooget 回應 toohello 問題 toouse hello 其餘部分。</span><span class="sxs-lookup"><span data-stu-id="fa74b-141">Our list doesn't have a 1.35 carat diamond in it, so we'll have toouse hello rest of our data tooget an answer toohello question.</span></span>

## <a name="plot-hello-existing-data"></a><span data-ttu-id="fa74b-142">繪製 hello 的現有資料</span><span class="sxs-lookup"><span data-stu-id="fa74b-142">Plot hello existing data</span></span>
<span data-ttu-id="fa74b-143">hello 第一件事就是繪製水平的數字行，呼叫座標軸，toochart hello 加權。</span><span class="sxs-lookup"><span data-stu-id="fa74b-143">hello first thing we'll do is draw a horizontal number line, called an axis, toochart hello weights.</span></span> <span data-ttu-id="fa74b-144">hello 權數的 hello 範圍是 0 too2，因此我們會繪製一條線所涵蓋的範圍，並將每個半克拉記號的刻度。</span><span class="sxs-lookup"><span data-stu-id="fa74b-144">hello range of hello weights is 0 too2, so we'll draw a line that covers that range and put ticks for each half carat.</span></span>

<span data-ttu-id="fa74b-145">接下來我們將會繪製垂直軸 toorecord hello 價格並將它連接 toohello 加權水平軸。</span><span class="sxs-lookup"><span data-stu-id="fa74b-145">Next we'll draw a vertical axis toorecord hello price and connect it toohello horizontal weight axis.</span></span> <span data-ttu-id="fa74b-146">這將以美元為單位。</span><span class="sxs-lookup"><span data-stu-id="fa74b-146">This will be in units of dollars.</span></span> <span data-ttu-id="fa74b-147">現在我們有一組座標軸。</span><span class="sxs-lookup"><span data-stu-id="fa74b-147">Now we have a set of coordinate axes.</span></span>

![重量軸和價格軸](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/weight-and-price-axes.png)

<span data-ttu-id="fa74b-149">我們現在已經準備進行 tootake 這項資料，並開啟它*散佈圖*。</span><span class="sxs-lookup"><span data-stu-id="fa74b-149">We're going tootake this data now and turn it into a *scatter plot*.</span></span> <span data-ttu-id="fa74b-150">這是很好的方法 toovisualize 數值的資料集。</span><span class="sxs-lookup"><span data-stu-id="fa74b-150">This is a great way toovisualize numerical data sets.</span></span>

<span data-ttu-id="fa74b-151">針對第一個資料點 hello，我們可以看出 1.01 carats 在垂直線條。</span><span class="sxs-lookup"><span data-stu-id="fa74b-151">For hello first data point, we eyeball a vertical line at 1.01 carats.</span></span> <span data-ttu-id="fa74b-152">然後，在 7,366 美元處仔細打量出一條水平線。</span><span class="sxs-lookup"><span data-stu-id="fa74b-152">Then, we eyeball a horizontal line at $7,366.</span></span> <span data-ttu-id="fa74b-153">接著在它們的交會處畫上一點。</span><span class="sxs-lookup"><span data-stu-id="fa74b-153">Where they meet, we draw a dot.</span></span> <span data-ttu-id="fa74b-154">這代表我們的第一顆鑽石。</span><span class="sxs-lookup"><span data-stu-id="fa74b-154">This represents our first diamond.</span></span>

<span data-ttu-id="fa74b-155">現在我們檢查每一個菱形此清單上，執行 hello 相同的動作。</span><span class="sxs-lookup"><span data-stu-id="fa74b-155">Now we go through each diamond on this list and do hello same thing.</span></span> <span data-ttu-id="fa74b-156">完成之後，這就是我們所得到的結果：一連串的點，每一個都代表一顆鑽石。</span><span class="sxs-lookup"><span data-stu-id="fa74b-156">When we're through, this is what we get: a bunch of dots, one for each diamond.</span></span>

![散佈圖](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/scatter-plot.png)

## <a name="draw-hello-model-through-hello-data-points"></a><span data-ttu-id="fa74b-158">Hello 資料點繪製 hello 模型</span><span class="sxs-lookup"><span data-stu-id="fa74b-158">Draw hello model through hello data points</span></span>
<span data-ttu-id="fa74b-159">現在如果您看一下 hello 點與 squint，hello 集合就會像 fat、 模糊的行。</span><span class="sxs-lookup"><span data-stu-id="fa74b-159">Now if you look at hello dots and squint, hello collection looks like a fat, fuzzy line.</span></span> <span data-ttu-id="fa74b-160">我們可以記上標記，並通過它繪製一條直線。</span><span class="sxs-lookup"><span data-stu-id="fa74b-160">We can take our marker and draw a straight line through it.</span></span>

<span data-ttu-id="fa74b-161">藉由繪製一條線，我們建立了一個「模型」 。</span><span class="sxs-lookup"><span data-stu-id="fa74b-161">By drawing a line, we created a *model*.</span></span> <span data-ttu-id="fa74b-162">將此接受 hello 真實世界，且它的最簡單的卡通版本。</span><span class="sxs-lookup"><span data-stu-id="fa74b-162">Think of this as taking hello real world and making a simplistic cartoon version of it.</span></span> <span data-ttu-id="fa74b-163">現在 hello 卡通錯誤-hello 列未通過所有 hello 資料點。</span><span class="sxs-lookup"><span data-stu-id="fa74b-163">Now hello cartoon is wrong - hello line doesn't go through all hello data points.</span></span> <span data-ttu-id="fa74b-164">但它是非常實用的簡化。</span><span class="sxs-lookup"><span data-stu-id="fa74b-164">But, it's a useful simplification.</span></span>

![線性迴歸線](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/linear-regression-line.png)

<span data-ttu-id="fa74b-166">所有的 hello 點不會經過完全 hello 線條的 hello 事實是 [確定]。</span><span class="sxs-lookup"><span data-stu-id="fa74b-166">hello fact that all hello dots don't go exactly through hello line is OK.</span></span> <span data-ttu-id="fa74b-167">資料科學家所說 hello 模型-hello 列-說明這個，則每一個點不會有一些*雜訊*或*變異數*與其相關聯。</span><span class="sxs-lookup"><span data-stu-id="fa74b-167">Data scientists explain this by saying that there's hello model - that's hello line - and then each dot has some *noise* or *variance* associated with it.</span></span> <span data-ttu-id="fa74b-168">Hello 基礎完美的關聯性，而且沒有新增雜訊及不確定性的 hello 至今、 真實世界。</span><span class="sxs-lookup"><span data-stu-id="fa74b-168">There's hello underlying perfect relationship, and then there's hello gritty, real world that adds noise and uncertainty.</span></span>

<span data-ttu-id="fa74b-169">因為我們想 tooanswer hello 問題*多少？*這稱為*迴歸*。</span><span class="sxs-lookup"><span data-stu-id="fa74b-169">Because we're trying tooanswer hello question *How much?* this is called a *regression*.</span></span> <span data-ttu-id="fa74b-170">而且由於我們使用直線，所以它是「線性迴歸」。</span><span class="sxs-lookup"><span data-stu-id="fa74b-170">And because we're using a straight line, it's a *linear regression*.</span></span>

## <a name="use-hello-model-toofind-hello-answer"></a><span data-ttu-id="fa74b-171">使用 hello 模型 toofind hello 回應</span><span class="sxs-lookup"><span data-stu-id="fa74b-171">Use hello model toofind hello answer</span></span>
<span data-ttu-id="fa74b-172">現在我們已有模型，接著詢問它一個問題：1.35 克拉的鑽石價值多少？</span><span class="sxs-lookup"><span data-stu-id="fa74b-172">Now we have a model and we ask it our question: How much will a 1.35 carat diamond cost?</span></span>

<span data-ttu-id="fa74b-173">tooanswer 我們的問題，我們可以看出 1.35 carats 並繪製垂直線條。</span><span class="sxs-lookup"><span data-stu-id="fa74b-173">tooanswer our question, we eyeball 1.35 carats and draw a vertical line.</span></span> <span data-ttu-id="fa74b-174">在每次跨越 hello 模型線條，我們可以看出水平線 toohello 貨幣軸。</span><span class="sxs-lookup"><span data-stu-id="fa74b-174">Where it crosses hello model line, we eyeball a horizontal line toohello dollar axis.</span></span> <span data-ttu-id="fa74b-175">它正好命中 10,000。</span><span class="sxs-lookup"><span data-stu-id="fa74b-175">It hits right at 10,000.</span></span> <span data-ttu-id="fa74b-176">碰！</span><span class="sxs-lookup"><span data-stu-id="fa74b-176">Boom!</span></span> <span data-ttu-id="fa74b-177">這是 hello 回應： 1.35 克拉記號菱形的成本大約 $10,000。</span><span class="sxs-lookup"><span data-stu-id="fa74b-177">That's hello answer: A 1.35 carat diamond costs about $10,000.</span></span>

![尋找 hello 回應 hello 模型](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/find-the-answer.png)

## <a name="create-a-confidence-interval"></a><span data-ttu-id="fa74b-179">建立信賴區間</span><span class="sxs-lookup"><span data-stu-id="fa74b-179">Create a confidence interval</span></span>
<span data-ttu-id="fa74b-180">自然 toowonder 如何精確此預測它。</span><span class="sxs-lookup"><span data-stu-id="fa74b-180">It's natural toowonder how precise this prediction is.</span></span> <span data-ttu-id="fa74b-181">它是有用的 tooknow 是否 hello 1.35 克拉記號菱形太將會非常接近 $10000 或很高或較低。</span><span class="sxs-lookup"><span data-stu-id="fa74b-181">It's useful tooknow whether hello 1.35 carat diamond will be very close too$10,000, or a lot higher or lower.</span></span> <span data-ttu-id="fa74b-182">toofigure 這個 out，讓我們來繪製 hello 迴歸線，其中包含大部分的 hello 點周圍的信封。</span><span class="sxs-lookup"><span data-stu-id="fa74b-182">toofigure this out, let's draw an envelope around hello regression line that includes most of hello dots.</span></span> <span data-ttu-id="fa74b-183">此信封稱為我們*信賴區間*： 我們確信相當，價格會落在此信封，因為在過去的 hello 其中大部分都有。</span><span class="sxs-lookup"><span data-stu-id="fa74b-183">This envelope is called our *confidence interval*: We're pretty confident that prices fall within this envelope, because in hello past most of them have.</span></span> <span data-ttu-id="fa74b-184">我們可以繪製兩個多水平線條從 hello 1.35 克拉記號線交點 hello hello 的上下該信封。</span><span class="sxs-lookup"><span data-stu-id="fa74b-184">We can draw two more horizontal lines from where hello 1.35 carat line crosses hello top and hello bottom of that envelope.</span></span>

![信賴區間](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/confidence-interval.png)

<span data-ttu-id="fa74b-186">現在我們可以說一下我們信賴區間： 我們在 1.35 克拉記號鑽石形的 hello 價格是大約 $10000-，但是可能會為 $8000，而且可能是最高 $12000 可以很輕易地說。</span><span class="sxs-lookup"><span data-stu-id="fa74b-186">Now we can say something about our confidence interval:  We can say confidently that hello price of a 1.35 carat diamond is about $10,000 - but it might be as low as $8,000 and it might be as high as $12,000.</span></span>

## <a name="were-done-with-no-math-or-computers"></a><span data-ttu-id="fa74b-187">我們不需用到任何數學或電腦就能完成</span><span class="sxs-lookup"><span data-stu-id="fa74b-187">We're done, with no math or computers</span></span>
<span data-ttu-id="fa74b-188">我們所做的哪些資料科學家收款 toodo，和它所繪製的：</span><span class="sxs-lookup"><span data-stu-id="fa74b-188">We did what data scientists get paid toodo, and we did it just by drawing:</span></span>

* <span data-ttu-id="fa74b-189">我們詢問可以使用資料回答的問題</span><span class="sxs-lookup"><span data-stu-id="fa74b-189">We asked a question that we could answer with data</span></span>
* <span data-ttu-id="fa74b-190">我們使用「線性迴歸」建立了「模型」</span><span class="sxs-lookup"><span data-stu-id="fa74b-190">We built a *model* using *linear regression*</span></span>
* <span data-ttu-id="fa74b-191">我們進行「預測」，並使用「信賴區間」來完成</span><span class="sxs-lookup"><span data-stu-id="fa74b-191">We made a *prediction*, complete with a *confidence interval*</span></span>

<span data-ttu-id="fa74b-192">並沒有使用數學或電腦 toodo 它。</span><span class="sxs-lookup"><span data-stu-id="fa74b-192">And we didn't use math or computers toodo it.</span></span>

<span data-ttu-id="fa74b-193">現在，如果我們當時有更多資訊，例如...</span><span class="sxs-lookup"><span data-stu-id="fa74b-193">Now if we'd had more information, like...</span></span>

* <span data-ttu-id="fa74b-194">hello 剪下 hello 鑽石形的</span><span class="sxs-lookup"><span data-stu-id="fa74b-194">hello cut of hello diamond</span></span>
* <span data-ttu-id="fa74b-195">色彩變化 （如何關閉 hello 菱形是白色 toobeing）</span><span class="sxs-lookup"><span data-stu-id="fa74b-195">color variations (how close hello diamond is toobeing white)</span></span>
* <span data-ttu-id="fa74b-196">hello 的 hello 菱形中包含的數字</span><span class="sxs-lookup"><span data-stu-id="fa74b-196">hello number of inclusions in hello diamond</span></span>

<span data-ttu-id="fa74b-197">...則會有更多欄。</span><span class="sxs-lookup"><span data-stu-id="fa74b-197">...then we would have had more columns.</span></span> <span data-ttu-id="fa74b-198">在此情況下，數學就會變得很有幫助。</span><span class="sxs-lookup"><span data-stu-id="fa74b-198">In that case, math becomes helpful.</span></span> <span data-ttu-id="fa74b-199">如果您有兩個以上的資料行，則在紙張上的硬碟 toodraw 點。</span><span class="sxs-lookup"><span data-stu-id="fa74b-199">If you have more than two columns, it's hard toodraw dots on paper.</span></span> <span data-ttu-id="fa74b-200">hello 數學可讓您輕易符合該線條或平面 tooyour 資料。</span><span class="sxs-lookup"><span data-stu-id="fa74b-200">hello math lets you fit that line or that plane tooyour data very nicely.</span></span>

<span data-ttu-id="fa74b-201">此外，如果不是只有少數的鑽石，而是有兩千個或兩百萬個，則您可以使用電腦更快速地進行此動作。</span><span class="sxs-lookup"><span data-stu-id="fa74b-201">Also, if instead of just a handful of diamonds, we had two thousand or two million, then you can do that work much faster with a computer.</span></span>

<span data-ttu-id="fa74b-202">今天，我們談論 toodo 線性迴歸，所以我們如何進行預測，使用資料。</span><span class="sxs-lookup"><span data-stu-id="fa74b-202">Today, we've talked about how toodo linear regression, and we made a prediction using data.</span></span>

<span data-ttu-id="fa74b-203">為確定 toocheck 出 hello"的資料科學的初學者 」 從 Microsoft Azure Machine Learning 中的其他視訊。</span><span class="sxs-lookup"><span data-stu-id="fa74b-203">Be sure toocheck out hello other videos in "Data Science for Beginners" from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa74b-204">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fa74b-204">Next steps</span></span>
* [<span data-ttu-id="fa74b-205">嘗試使用 Machine Learning Studio 進行您的第一個資料科學實驗</span><span class="sxs-lookup"><span data-stu-id="fa74b-205">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="fa74b-206">取得簡介 tooMachine Microsoft Azure 上學習</span><span class="sxs-lookup"><span data-stu-id="fa74b-206">Get an introduction tooMachine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)
