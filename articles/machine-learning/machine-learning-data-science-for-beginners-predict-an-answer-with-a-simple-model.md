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
# <a name="predict-an-answer-with-a-simple-model"></a>利用簡單模型預測答案
## <a name="video-4-data-science-for-beginners-series"></a>影片 4：適用於初學者的資料科學系列
了解如何 toocreate 簡單的迴歸模型 toopredict hello 中適用於初學者視訊 4 的資料科學鑽石形的價格。 我們將利用目標資料來繪製迴歸模型。

充分利用 hello 數列 tooget hello 觀賞全部。 [前往影片 toohello 清單](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-predict-an-answer-with-a-simple-model/player]
>
>

## <a name="other-videos-in-this-series"></a>系列中的其他影片
*為初學者所設計的資料科學*是快速介紹 toodata 科學中五個簡短的影片。

* 視訊 1: [hello 5 個問題的資料科學答案](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *（5 分鐘 14 秒）*
* 影片 2： [您的資料已經可以進行資料科學了嗎？](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 分 56 秒)*
* 影片 3：[詢問您可以使用資料回答的問題](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 分 17 秒)*
* 影片 4：利用簡單模型預測答案
* 視訊 5:[複製其他人工作 toodo 資料科學](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *（3 分 18 秒）*

## <a name="transcript-predict-an-answer-with-a-simple-model"></a>文字記錄：利用簡單模型預測答案
歡迎使用 toohello hello 」 資料初學者科學"數列中第四個視訊。 在這個影片中，我們將建置簡單模型並進行預測。

「模型」  是我們相關資料的簡化敘述。 我將告訴您我的意思。

## <a name="collect-relevant-accurate-connected-enough-data"></a>收集相關、精確、連貫、足夠的資料
假設我想 tooshop 的菱形。 我有所屬 toomy 叫 1.35 克拉記號菱形設定信號，我想 tooget 了解它需要多少成本。 Hello 珠寶存放區，才能在 記事本 和 畫筆與我記下的所有在 hello 的案例和它們多少權衡 carats hello 菱形 hello 價格。 正在啟動 hello 第一個菱形-它的 1.01 carats 和 $7,366。

現在我瀏覽，這樣做的所有 hello hello 存放區中的其他菱形。

![鑽石資料欄](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/diamond-data.png)

請注意，我們的清單包含兩欄。 每欄都有不同的屬性 (克拉數的重量和價格)，而且每一行都是代表單一顆鑽石的單一資料點。

我們實際上在此處建立了一個小型資料集 - 一個表格。 請注意，它符合我們對於品質的準則：

* hello 資料**相關**-加權值是絕對相關的 tooprice
* 它有**精確**-我們重複檢查我們記下的 hello 價格
* 它是 **連貫** 的 - 在這些欄中沒有任何空格
* 而且，如我們所見，它有**足夠**資料 tooanswer 我們的問題

## <a name="ask-a-sharp-question"></a>詢問明確的問題
現在我們將會顯示我們的問題造成尖的方式:"多少成本 toobuy 1.35 克拉記號菱形？ 」

我們沒有 1.35 克拉記號菱形，因此我們必須我們資料 tooget 回應 toohello 問題 toouse hello 其餘部分。

## <a name="plot-hello-existing-data"></a>繪製 hello 的現有資料
hello 第一件事就是繪製水平的數字行，呼叫座標軸，toochart hello 加權。 hello 權數的 hello 範圍是 0 too2，因此我們會繪製一條線所涵蓋的範圍，並將每個半克拉記號的刻度。

接下來我們將會繪製垂直軸 toorecord hello 價格並將它連接 toohello 加權水平軸。 這將以美元為單位。 現在我們有一組座標軸。

![重量軸和價格軸](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/weight-and-price-axes.png)

我們現在已經準備進行 tootake 這項資料，並開啟它*散佈圖*。 這是很好的方法 toovisualize 數值的資料集。

針對第一個資料點 hello，我們可以看出 1.01 carats 在垂直線條。 然後，在 7,366 美元處仔細打量出一條水平線。 接著在它們的交會處畫上一點。 這代表我們的第一顆鑽石。

現在我們檢查每一個菱形此清單上，執行 hello 相同的動作。 完成之後，這就是我們所得到的結果：一連串的點，每一個都代表一顆鑽石。

![散佈圖](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/scatter-plot.png)

## <a name="draw-hello-model-through-hello-data-points"></a>Hello 資料點繪製 hello 模型
現在如果您看一下 hello 點與 squint，hello 集合就會像 fat、 模糊的行。 我們可以記上標記，並通過它繪製一條直線。

藉由繪製一條線，我們建立了一個「模型」 。 將此接受 hello 真實世界，且它的最簡單的卡通版本。 現在 hello 卡通錯誤-hello 列未通過所有 hello 資料點。 但它是非常實用的簡化。

![線性迴歸線](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/linear-regression-line.png)

所有的 hello 點不會經過完全 hello 線條的 hello 事實是 [確定]。 資料科學家所說 hello 模型-hello 列-說明這個，則每一個點不會有一些*雜訊*或*變異數*與其相關聯。 Hello 基礎完美的關聯性，而且沒有新增雜訊及不確定性的 hello 至今、 真實世界。

因為我們想 tooanswer hello 問題*多少？*這稱為*迴歸*。 而且由於我們使用直線，所以它是「線性迴歸」。

## <a name="use-hello-model-toofind-hello-answer"></a>使用 hello 模型 toofind hello 回應
現在我們已有模型，接著詢問它一個問題：1.35 克拉的鑽石價值多少？

tooanswer 我們的問題，我們可以看出 1.35 carats 並繪製垂直線條。 在每次跨越 hello 模型線條，我們可以看出水平線 toohello 貨幣軸。 它正好命中 10,000。 碰！ 這是 hello 回應： 1.35 克拉記號菱形的成本大約 $10,000。

![尋找 hello 回應 hello 模型](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/find-the-answer.png)

## <a name="create-a-confidence-interval"></a>建立信賴區間
自然 toowonder 如何精確此預測它。 它是有用的 tooknow 是否 hello 1.35 克拉記號菱形太將會非常接近 $10000 或很高或較低。 toofigure 這個 out，讓我們來繪製 hello 迴歸線，其中包含大部分的 hello 點周圍的信封。 此信封稱為我們*信賴區間*： 我們確信相當，價格會落在此信封，因為在過去的 hello 其中大部分都有。 我們可以繪製兩個多水平線條從 hello 1.35 克拉記號線交點 hello hello 的上下該信封。

![信賴區間](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/confidence-interval.png)

現在我們可以說一下我們信賴區間： 我們在 1.35 克拉記號鑽石形的 hello 價格是大約 $10000-，但是可能會為 $8000，而且可能是最高 $12000 可以很輕易地說。

## <a name="were-done-with-no-math-or-computers"></a>我們不需用到任何數學或電腦就能完成
我們所做的哪些資料科學家收款 toodo，和它所繪製的：

* 我們詢問可以使用資料回答的問題
* 我們使用「線性迴歸」建立了「模型」
* 我們進行「預測」，並使用「信賴區間」來完成

並沒有使用數學或電腦 toodo 它。

現在，如果我們當時有更多資訊，例如...

* hello 剪下 hello 鑽石形的
* 色彩變化 （如何關閉 hello 菱形是白色 toobeing）
* hello 的 hello 菱形中包含的數字

...則會有更多欄。 在此情況下，數學就會變得很有幫助。 如果您有兩個以上的資料行，則在紙張上的硬碟 toodraw 點。 hello 數學可讓您輕易符合該線條或平面 tooyour 資料。

此外，如果不是只有少數的鑽石，而是有兩千個或兩百萬個，則您可以使用電腦更快速地進行此動作。

今天，我們談論 toodo 線性迴歸，所以我們如何進行預測，使用資料。

為確定 toocheck 出 hello"的資料科學的初學者 」 從 Microsoft Azure Machine Learning 中的其他視訊。

## <a name="next-steps"></a>後續步驟
* [嘗試使用 Machine Learning Studio 進行您的第一個資料科學實驗](machine-learning-create-experiment.md)
* [取得簡介 tooMachine Microsoft Azure 上學習](machine-learning-what-is-machine-learning.md)
