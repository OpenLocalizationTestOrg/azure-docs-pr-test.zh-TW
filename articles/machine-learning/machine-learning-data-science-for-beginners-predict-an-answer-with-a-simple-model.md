---
title: "利用簡單的迴歸模型預測答案 - Azure Machine Learning | Microsoft Docs"
description: "如何在「適用於初學者的資料科學」影片 4 中，建立簡單迴歸模型來預測價格。 包含線性迴歸以及目標資料。"
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
ms.openlocfilehash: 24df1823af2610a5111118f47e4cadbcfcc0eff1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="predict-an-answer-with-a-simple-model"></a><span data-ttu-id="48709-105">利用簡單模型預測答案</span><span class="sxs-lookup"><span data-stu-id="48709-105">Predict an answer with a simple model</span></span>
## <a name="video-4-data-science-for-beginners-series"></a><span data-ttu-id="48709-106">影片 4：適用於初學者的資料科學系列</span><span class="sxs-lookup"><span data-stu-id="48709-106">Video 4: Data Science for Beginners series</span></span>
<span data-ttu-id="48709-107">在「適用於初學者的資料科學」影片 4 中，了解如何建立簡單迴歸模型來預測鑽石價格。</span><span class="sxs-lookup"><span data-stu-id="48709-107">Learn how to create a simple regression model to predict the price of a diamond in Data Science for Beginners video 4.</span></span> <span data-ttu-id="48709-108">我們將利用目標資料來繪製迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="48709-108">We'll draw a regression model with target data.</span></span>

<span data-ttu-id="48709-109">若要充分運用這系列影片，請觀賞所有影片。</span><span class="sxs-lookup"><span data-stu-id="48709-109">To get the most out of the series, watch them all.</span></span> <span data-ttu-id="48709-110">[瀏覽影片清單](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="48709-110">[Go to the list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-predict-an-answer-with-a-simple-model/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="48709-111">系列中的其他影片</span><span class="sxs-lookup"><span data-stu-id="48709-111">Other videos in this series</span></span>
<span data-ttu-id="48709-112"> 是一個資料科學的快速簡介，包含五個簡短影片。</span><span class="sxs-lookup"><span data-stu-id="48709-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span></span>

* <span data-ttu-id="48709-113">影片 1：[資料科學可以回答的 5 個問題](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 分 14 秒)*</span><span class="sxs-lookup"><span data-stu-id="48709-113">Video 1: [The 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="48709-114">影片 2： [您的資料已經可以進行資料科學了嗎？](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span><span class="sxs-lookup"><span data-stu-id="48709-114">Video 2: [Is your data ready for data science?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span></span> <span data-ttu-id="48709-115">*(4 分 56 秒)*</span><span class="sxs-lookup"><span data-stu-id="48709-115">*(4 min 56 sec)*</span></span>
* <span data-ttu-id="48709-116">影片 3：[詢問您可以使用資料回答的問題](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 分 17 秒)*</span><span class="sxs-lookup"><span data-stu-id="48709-116">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="48709-117">影片 4：利用簡單模型預測答案</span><span class="sxs-lookup"><span data-stu-id="48709-117">Video 4: Predict an answer with a simple model</span></span>
* <span data-ttu-id="48709-118">影片 5：[複製其他人的工作進行資料科學](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 分 18 秒)*</span><span class="sxs-lookup"><span data-stu-id="48709-118">Video 5: [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-predict-an-answer-with-a-simple-model"></a><span data-ttu-id="48709-119">文字記錄：利用簡單模型預測答案</span><span class="sxs-lookup"><span data-stu-id="48709-119">Transcript: Predict an answer with a simple model</span></span>
<span data-ttu-id="48709-120">歡迎觀賞「適用於初學者的資料科學」系列的第四個影片。</span><span class="sxs-lookup"><span data-stu-id="48709-120">Welcome to the fourth video in the "Data Science for Beginners" series.</span></span> <span data-ttu-id="48709-121">在這個影片中，我們將建置簡單模型並進行預測。</span><span class="sxs-lookup"><span data-stu-id="48709-121">In this one, we'll build a simple model and make a prediction.</span></span>

<span data-ttu-id="48709-122">「模型」  是我們相關資料的簡化敘述。</span><span class="sxs-lookup"><span data-stu-id="48709-122">A *model* is a simplified story about our data.</span></span> <span data-ttu-id="48709-123">我將告訴您我的意思。</span><span class="sxs-lookup"><span data-stu-id="48709-123">I'll show you what I mean.</span></span>

## <a name="collect-relevant-accurate-connected-enough-data"></a><span data-ttu-id="48709-124">收集相關、精確、連貫、足夠的資料</span><span class="sxs-lookup"><span data-stu-id="48709-124">Collect relevant, accurate, connected, enough data</span></span>
<span data-ttu-id="48709-125">假設我想要購買鑽石。</span><span class="sxs-lookup"><span data-stu-id="48709-125">Say I want to shop for a diamond.</span></span> <span data-ttu-id="48709-126">我有一只戒指，它屬於我的祖母，其中鑲嵌了一個 1.35 克拉的鑽石，而我想要了解它的價值。</span><span class="sxs-lookup"><span data-stu-id="48709-126">I have a ring that belonged to my grandmother with a setting for a 1.35 carat diamond, and I want to get an idea of how much it will cost.</span></span> <span data-ttu-id="48709-127">我帶著筆記本和筆到珠寶店，並記下架上所有鑽石的價格，以及它們的重量有多少克拉數。</span><span class="sxs-lookup"><span data-stu-id="48709-127">I take a notepad and pen into the jewelry store, and I write down the price of all of the diamonds in the case and how much they weigh in carats.</span></span> <span data-ttu-id="48709-128">從第一顆鑽石開始 - 它是 1.01 克拉，美金 7,366 元。</span><span class="sxs-lookup"><span data-stu-id="48709-128">Starting with the first diamond - it's 1.01 carats and $7,366.</span></span>

<span data-ttu-id="48709-129">現在我已順利完成，並針對店內的所有其他鑽石執行此動作。</span><span class="sxs-lookup"><span data-stu-id="48709-129">Now I go through and do this for all the other diamonds in the store.</span></span>

![鑽石資料欄](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/diamond-data.png)

<span data-ttu-id="48709-131">請注意，我們的清單包含兩欄。</span><span class="sxs-lookup"><span data-stu-id="48709-131">Notice that our list has two columns.</span></span> <span data-ttu-id="48709-132">每欄都有不同的屬性 (克拉數的重量和價格)，而且每一行都是代表單一顆鑽石的單一資料點。</span><span class="sxs-lookup"><span data-stu-id="48709-132">Each column has a different attribute - weight in carats and price - and each row is a single data point that represents a single diamond.</span></span>

<span data-ttu-id="48709-133">我們實際上在此處建立了一個小型資料集 - 一個表格。</span><span class="sxs-lookup"><span data-stu-id="48709-133">We've actually created a small data set here - a table.</span></span> <span data-ttu-id="48709-134">請注意，它符合我們對於品質的準則：</span><span class="sxs-lookup"><span data-stu-id="48709-134">Notice that it meets our criteria for quality:</span></span>

* <span data-ttu-id="48709-135">資料是 **相關** 的 - 重量明確地與價格相關</span><span class="sxs-lookup"><span data-stu-id="48709-135">The data is **relevant** - weight is definitely related to price</span></span>
* <span data-ttu-id="48709-136">它是 **精確** 的 - 我們已再次檢查我們寫下的價格</span><span class="sxs-lookup"><span data-stu-id="48709-136">It's **accurate** - we double-checked the prices that we write down</span></span>
* <span data-ttu-id="48709-137">它是 **連貫** 的 - 在這些欄中沒有任何空格</span><span class="sxs-lookup"><span data-stu-id="48709-137">It's **connected** - there are no blank spaces in either of these columns</span></span>
* <span data-ttu-id="48709-138">此外，誠如所見，有 **足夠** 的資料可回答我們的問題</span><span class="sxs-lookup"><span data-stu-id="48709-138">And, as we'll see, it's **enough** data to answer our question</span></span>

## <a name="ask-a-sharp-question"></a><span data-ttu-id="48709-139">詢問明確的問題</span><span class="sxs-lookup"><span data-stu-id="48709-139">Ask a sharp question</span></span>
<span data-ttu-id="48709-140">現在我們將以明確的方式提出問題：「要花多少費用才能購買 1.35 克拉的鑽石？」</span><span class="sxs-lookup"><span data-stu-id="48709-140">Now we'll pose our question in a sharp way: "How much will it cost to buy a 1.35 carat diamond?"</span></span>

<span data-ttu-id="48709-141">我們的清單中沒有 1.35 克拉的鑽石，因此，必須使用剩餘的資料來取得問題的答案。</span><span class="sxs-lookup"><span data-stu-id="48709-141">Our list doesn't have a 1.35 carat diamond in it, so we'll have to use the rest of our data to get an answer to the question.</span></span>

## <a name="plot-the-existing-data"></a><span data-ttu-id="48709-142">繪製現有的資料</span><span class="sxs-lookup"><span data-stu-id="48709-142">Plot the existing data</span></span>
<span data-ttu-id="48709-143">我們要做的第一件事是繪製一條水平數線 (稱為軸) 來繪製重量的圖表。</span><span class="sxs-lookup"><span data-stu-id="48709-143">The first thing we'll do is draw a horizontal number line, called an axis, to chart the weights.</span></span> <span data-ttu-id="48709-144">重量的範圍從 0 到 2，因此，我們將繪製一條涵蓋此範圍的線，並針對每半克拉劃上刻度。</span><span class="sxs-lookup"><span data-stu-id="48709-144">The range of the weights is 0 to 2, so we'll draw a line that covers that range and put ticks for each half carat.</span></span>

<span data-ttu-id="48709-145">接下來，我們將繪製一條垂直軸來記錄價格，並將它連接到水平的重量軸。</span><span class="sxs-lookup"><span data-stu-id="48709-145">Next we'll draw a vertical axis to record the price and connect it to the horizontal weight axis.</span></span> <span data-ttu-id="48709-146">這將以美元為單位。</span><span class="sxs-lookup"><span data-stu-id="48709-146">This will be in units of dollars.</span></span> <span data-ttu-id="48709-147">現在我們有一組座標軸。</span><span class="sxs-lookup"><span data-stu-id="48709-147">Now we have a set of coordinate axes.</span></span>

![重量軸和價格軸](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/weight-and-price-axes.png)

<span data-ttu-id="48709-149">我們現在將利用這個資料，並將它變成「散佈圖」 。</span><span class="sxs-lookup"><span data-stu-id="48709-149">We're going to take this data now and turn it into a *scatter plot*.</span></span> <span data-ttu-id="48709-150">這是以視覺化方式檢視數值資料集的好方法。</span><span class="sxs-lookup"><span data-stu-id="48709-150">This is a great way to visualize numerical data sets.</span></span>

<span data-ttu-id="48709-151">針對第一個資料點，我們在 1.01 克拉處仔細打量出一條垂直線。</span><span class="sxs-lookup"><span data-stu-id="48709-151">For the first data point, we eyeball a vertical line at 1.01 carats.</span></span> <span data-ttu-id="48709-152">然後，在 7,366 美元處仔細打量出一條水平線。</span><span class="sxs-lookup"><span data-stu-id="48709-152">Then, we eyeball a horizontal line at $7,366.</span></span> <span data-ttu-id="48709-153">接著在它們的交會處畫上一點。</span><span class="sxs-lookup"><span data-stu-id="48709-153">Where they meet, we draw a dot.</span></span> <span data-ttu-id="48709-154">這代表我們的第一顆鑽石。</span><span class="sxs-lookup"><span data-stu-id="48709-154">This represents our first diamond.</span></span>

<span data-ttu-id="48709-155">現在逐一取得此清單上的每一顆鑽石，然後執行相同動作。</span><span class="sxs-lookup"><span data-stu-id="48709-155">Now we go through each diamond on this list and do the same thing.</span></span> <span data-ttu-id="48709-156">完成之後，這就是我們所得到的結果：一連串的點，每一個都代表一顆鑽石。</span><span class="sxs-lookup"><span data-stu-id="48709-156">When we're through, this is what we get: a bunch of dots, one for each diamond.</span></span>

![散佈圖](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/scatter-plot.png)

## <a name="draw-the-model-through-the-data-points"></a><span data-ttu-id="48709-158">通過資料點繪製模型</span><span class="sxs-lookup"><span data-stu-id="48709-158">Draw the model through the data points</span></span>
<span data-ttu-id="48709-159">現在如果您查看點與傾向，集合看起來就像一條很模糊的粗線。</span><span class="sxs-lookup"><span data-stu-id="48709-159">Now if you look at the dots and squint, the collection looks like a fat, fuzzy line.</span></span> <span data-ttu-id="48709-160">我們可以記上標記，並通過它繪製一條直線。</span><span class="sxs-lookup"><span data-stu-id="48709-160">We can take our marker and draw a straight line through it.</span></span>

<span data-ttu-id="48709-161">藉由繪製一條線，我們建立了一個「模型」 。</span><span class="sxs-lookup"><span data-stu-id="48709-161">By drawing a line, we created a *model*.</span></span> <span data-ttu-id="48709-162">將此想像為現實世界，並為它建立一個極度簡化的草圖版本。</span><span class="sxs-lookup"><span data-stu-id="48709-162">Think of this as taking the real world and making a simplistic cartoon version of it.</span></span> <span data-ttu-id="48709-163">現在草圖有誤 - 這條線並未通過所有資料點。</span><span class="sxs-lookup"><span data-stu-id="48709-163">Now the cartoon is wrong - the line doesn't go through all the data points.</span></span> <span data-ttu-id="48709-164">但它是非常實用的簡化。</span><span class="sxs-lookup"><span data-stu-id="48709-164">But, it's a useful simplification.</span></span>

![線性迴歸線](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/linear-regression-line.png)

<span data-ttu-id="48709-166">這條線不會完全通過所有點，事實上是沒問題。</span><span class="sxs-lookup"><span data-stu-id="48709-166">The fact that all the dots don't go exactly through the line is OK.</span></span> <span data-ttu-id="48709-167">資料科學家利用下列方式來說明這一點，假設有一個模型 (就是這條線)，接著每個點都有一些與它相關聯的「雜訊」或「變異數」。</span><span class="sxs-lookup"><span data-stu-id="48709-167">Data scientists explain this by saying that there's the model - that's the line - and then each dot has some *noise* or *variance* associated with it.</span></span> <span data-ttu-id="48709-168">有一個基本的完美關聯性，接著是加入了雜訊和不確定性的真實世界本質。</span><span class="sxs-lookup"><span data-stu-id="48709-168">There's the underlying perfect relationship, and then there's the gritty, real world that adds noise and uncertainty.</span></span>

<span data-ttu-id="48709-169">因為我們正試著回答「多少？」的問題，這就稱為「迴歸」。</span><span class="sxs-lookup"><span data-stu-id="48709-169">Because we're trying to answer the question *How much?* this is called a *regression*.</span></span> <span data-ttu-id="48709-170">而且由於我們使用直線，所以它是「線性迴歸」。</span><span class="sxs-lookup"><span data-stu-id="48709-170">And because we're using a straight line, it's a *linear regression*.</span></span>

## <a name="use-the-model-to-find-the-answer"></a><span data-ttu-id="48709-171">使用模型尋找答案</span><span class="sxs-lookup"><span data-stu-id="48709-171">Use the model to find the answer</span></span>
<span data-ttu-id="48709-172">現在我們已有模型，接著詢問它一個問題：1.35 克拉的鑽石價值多少？</span><span class="sxs-lookup"><span data-stu-id="48709-172">Now we have a model and we ask it our question: How much will a 1.35 carat diamond cost?</span></span>

<span data-ttu-id="48709-173">為了回答問題，我們仔細打量出 1.35 克拉的所在位置，並繪製一條垂直線。</span><span class="sxs-lookup"><span data-stu-id="48709-173">To answer our question, we eyeball 1.35 carats and draw a vertical line.</span></span> <span data-ttu-id="48709-174">在它與模型線交會的地方，我們繪製了一條垂直線到美元軸。</span><span class="sxs-lookup"><span data-stu-id="48709-174">Where it crosses the model line, we eyeball a horizontal line to the dollar axis.</span></span> <span data-ttu-id="48709-175">它正好命中 10,000。</span><span class="sxs-lookup"><span data-stu-id="48709-175">It hits right at 10,000.</span></span> <span data-ttu-id="48709-176">碰！</span><span class="sxs-lookup"><span data-stu-id="48709-176">Boom!</span></span> <span data-ttu-id="48709-177">這就是答案了︰一顆 1.35 克拉的鑽石價值約 10,000 美元。</span><span class="sxs-lookup"><span data-stu-id="48709-177">That's the answer: A 1.35 carat diamond costs about $10,000.</span></span>

![在模型中尋找答案](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/find-the-answer.png)

## <a name="create-a-confidence-interval"></a><span data-ttu-id="48709-179">建立信賴區間</span><span class="sxs-lookup"><span data-stu-id="48709-179">Create a confidence interval</span></span>
<span data-ttu-id="48709-180">很自然地就想要知道此預測的精確度為何。</span><span class="sxs-lookup"><span data-stu-id="48709-180">It's natural to wonder how precise this prediction is.</span></span> <span data-ttu-id="48709-181">了解 1.35 克拉的鑽石是否非常接近 10,000 美元，抑或高出許多或低很多，是非常實用的。</span><span class="sxs-lookup"><span data-stu-id="48709-181">It's useful to know whether the 1.35 carat diamond will be very close to $10,000, or a lot higher or lower.</span></span> <span data-ttu-id="48709-182">為了理解這一點，讓我們在迴歸線四周畫一條包絡線，其中包含大部分的點。</span><span class="sxs-lookup"><span data-stu-id="48709-182">To figure this out, let's draw an envelope around the regression line that includes most of the dots.</span></span> <span data-ttu-id="48709-183">這條包絡線就稱為「信賴區間」 ︰我們非常確信價格會落在此包絡線內，因為在過去它們大多數都是這樣。</span><span class="sxs-lookup"><span data-stu-id="48709-183">This envelope is called our *confidence interval*: We're pretty confident that prices fall within this envelope, because in the past most of them have.</span></span> <span data-ttu-id="48709-184">我們可以從 1.35 克拉線與此包絡線頂端和底部交會的地方繪製兩條以上的垂直線。</span><span class="sxs-lookup"><span data-stu-id="48709-184">We can draw two more horizontal lines from where the 1.35 carat line crosses the top and the bottom of that envelope.</span></span>

![信賴區間](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/confidence-interval.png)

<span data-ttu-id="48709-186">現在讓我們來談論關於信賴區間的資訊：我們可以很有自信地表示 1.35 克拉鑽石的價格大約是 10,000 美元，但它最低可能是 8,000 美元，最高可能是 12,000 美元。</span><span class="sxs-lookup"><span data-stu-id="48709-186">Now we can say something about our confidence interval:  We can say confidently that the price of a 1.35 carat diamond is about $10,000 - but it might be as low as $8,000 and it might be as high as $12,000.</span></span>

## <a name="were-done-with-no-math-or-computers"></a><span data-ttu-id="48709-187">我們不需用到任何數學或電腦就能完成</span><span class="sxs-lookup"><span data-stu-id="48709-187">We're done, with no math or computers</span></span>
<span data-ttu-id="48709-188">我們完成了資料科學家需要報酬才會進行的工作，而且只需繪製下列動作就能完成：</span><span class="sxs-lookup"><span data-stu-id="48709-188">We did what data scientists get paid to do, and we did it just by drawing:</span></span>

* <span data-ttu-id="48709-189">我們詢問可以使用資料回答的問題</span><span class="sxs-lookup"><span data-stu-id="48709-189">We asked a question that we could answer with data</span></span>
* <span data-ttu-id="48709-190">我們使用「線性迴歸」建立了「模型」</span><span class="sxs-lookup"><span data-stu-id="48709-190">We built a *model* using *linear regression*</span></span>
* <span data-ttu-id="48709-191">我們進行「預測」，並使用「信賴區間」來完成</span><span class="sxs-lookup"><span data-stu-id="48709-191">We made a *prediction*, complete with a *confidence interval*</span></span>

<span data-ttu-id="48709-192">而且並未使用數學或電腦來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="48709-192">And we didn't use math or computers to do it.</span></span>

<span data-ttu-id="48709-193">現在，如果我們當時有更多資訊，例如...</span><span class="sxs-lookup"><span data-stu-id="48709-193">Now if we'd had more information, like...</span></span>

* <span data-ttu-id="48709-194">鑽石切割</span><span class="sxs-lookup"><span data-stu-id="48709-194">the cut of the diamond</span></span>
* <span data-ttu-id="48709-195">色澤變化 (鑽石接近白色的程度)</span><span class="sxs-lookup"><span data-stu-id="48709-195">color variations (how close the diamond is to being white)</span></span>
* <span data-ttu-id="48709-196">鑽石中內含物的數目</span><span class="sxs-lookup"><span data-stu-id="48709-196">the number of inclusions in the diamond</span></span>

<span data-ttu-id="48709-197">...則會有更多欄。</span><span class="sxs-lookup"><span data-stu-id="48709-197">...then we would have had more columns.</span></span> <span data-ttu-id="48709-198">在此情況下，數學就會變得很有幫助。</span><span class="sxs-lookup"><span data-stu-id="48709-198">In that case, math becomes helpful.</span></span> <span data-ttu-id="48709-199">如果您有兩欄以上，就很難在紙張上繪製點。</span><span class="sxs-lookup"><span data-stu-id="48709-199">If you have more than two columns, it's hard to draw dots on paper.</span></span> <span data-ttu-id="48709-200">數學可使該條線或該平面非常準確地符合您的資料。</span><span class="sxs-lookup"><span data-stu-id="48709-200">The math lets you fit that line or that plane to your data very nicely.</span></span>

<span data-ttu-id="48709-201">此外，如果不是只有少數的鑽石，而是有兩千個或兩百萬個，則您可以使用電腦更快速地進行此動作。</span><span class="sxs-lookup"><span data-stu-id="48709-201">Also, if instead of just a handful of diamonds, we had two thousand or two million, then you can do that work much faster with a computer.</span></span>

<span data-ttu-id="48709-202">現在，我們已討論過如何進行線性迴歸，而且已使用資料進行預測。</span><span class="sxs-lookup"><span data-stu-id="48709-202">Today, we've talked about how to do linear regression, and we made a prediction using data.</span></span>

<span data-ttu-id="48709-203">請務必查看 Microsoft Azure Machine Learning 中「適用於初學者的資料科學」的其他影片。</span><span class="sxs-lookup"><span data-stu-id="48709-203">Be sure to check out the other videos in "Data Science for Beginners" from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48709-204">後續步驟</span><span class="sxs-lookup"><span data-stu-id="48709-204">Next steps</span></span>
* [<span data-ttu-id="48709-205">嘗試使用 Machine Learning Studio 進行您的第一個資料科學實驗</span><span class="sxs-lookup"><span data-stu-id="48709-205">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="48709-206">在 Microsoft Azure 上取得 Machine Learning 簡介</span><span class="sxs-lookup"><span data-stu-id="48709-206">Get an introduction to Machine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)
