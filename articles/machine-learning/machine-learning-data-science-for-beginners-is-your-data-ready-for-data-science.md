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
# <a name="is-your-data-ready-for-data-science"></a>已備妥資料來進行資料科學嗎？
## <a name="video-2-data-science-for-beginners-series"></a>影片 2：適用於初學者的資料科學系列
深入了解如何 tooevaluate 您資料 toomake 確定它符合基本的準則 toobe 準備用於資料科學。

充分利用 hello 數列 tooget hello 觀賞全部。 [前往影片 toohello 清單](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Shows/SupervisionNotRequired/9/player]
>
>

## <a name="other-videos-in-this-series"></a>系列中的其他影片
*為初學者所設計的資料科學*是快速介紹 toodata 科學中五個簡短的影片。

* 視訊 1: [hello 5 個問題的資料科學答案](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *（5 分鐘 14 秒）*
* 影片 2：您的資料已經可以進行資料科學了嗎？
* 影片 3：[詢問您可以使用資料回答的問題](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 分 17 秒)*
* 影片 4：[利用簡單模型預測答案](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 分 42 秒)*
* 視訊 5:[複製其他人工作 toodo 資料科學](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *（3 分 18 秒）*

## <a name="transcript-is-your-data-ready-for-data-science"></a>文字記錄：已備妥資料來進行資料科學嗎？
歡迎使用太 」 是您的資料準備用於資料科學？ 」 hello hello 數列中的第二個視訊*為初學者所設計的資料科學*。  

資料科學可以提供之前 hello 您想要的答案，您必須 toogive 它具有某些高品質原料 toowork。 就像進行披薩，hello 您開始使用，更好 hello 食材更 hello hello 最終產品。 

## <a name="criteria-for-data"></a>資料準則
因此，在資料科學的其中一個 hello 情況下，會有一些因素，我們需要 toopull 一起。

我們所需的資料是：

* 相關
* 連線
* 精確
* 具有足夠 toowork

## <a name="is-your-data-relevant"></a>您的資料有相關性嗎？
因此第一個因素 hello-我們需要的相關資料。

![相關的資料與無關的資料 - 評估資料](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/relevant-and-irrelevant-data.png)

查看 hello 資料表 hello 左側。 我們符合波士頓橫條外部的七個人員的測量其捐血酒精層級、 hello 紅襪隊打擊，在他們的最後一個遊戲和牛奶 hello 最接近的方便存放區中的 hello 價格。

這一切都是合法的資料。 唯一的缺點是它們並不相關。 這些數字之間沒有任何明顯的關聯性。 如果提供 hello 牛奶和 hello 紅襪隊打擊股票的現價，沒有任何方法，您無法猜測我捐血酒精內容。

現在查看 hello 資料表上 hello 右。 這次我們測量每個人的主體大型和計數的 hello 時會將它們過數目。  每個資料列中的 hello 數字現在為相關 tooeach 其他。 如果帶給您 Margaritas 我有我主體大型與 hello 號碼，您可以建立在我的捐血猜測酒精內容。

## <a name="do-you-have-connected-data"></a>是否有連貫的資料？
hello 下一個因素是連接的資料。

![連接的資料與中斷連接的資料 - 資料準則、備妥資料](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/connected-vs-disconnected-data.png)

以下是一些漢堡 hello 品質相關的資料： grill 溫度、 patty 加權和 hello 本機食物雜誌中的評等。 但請注意在 hello 左邊 hello 資料表中的 hello 間距。

大部分的資料集遺漏了某些值。 就像這樣的一般 toohave 漏洞而且沒有方法 toowork 周圍。 不過如果有太多遺失，您的資料開始 toolook 瑞士 cheese 類似。

Hello 左側查看 hello 資料表，如果沒有而遺失的資料量與任何一種之間的關聯性的硬式 toocome 向上 grill 溫度和 patty 權數。 這是連貫性中斷的資料範例。

雖然 hello hello 右側資料表中，已滿，而且完成-已連接資料的範例。

## <a name="is-your-data-accurate"></a>是您的資料精確嗎？
hello 我們需要的下一個因素是精確度。 以下是我們都希望 toohit 箭號的四個目標。

![準確的資料與不準確的資料 - 資料準則](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/inaccurate-vs-accurate-data.png)

查看 hello hello 右上角的目標。 我們必須要 hello 準星型的緊密群組。 當然這是精確的。 有，在資料科學的其中一個 hello 語言中，我們在其下的 hello 目標右邊的效能也會被視為正確。

如果您 toomap hello 中心的這些箭號，您會看到這是非常接近 toohello 準星型。 hello 箭號分布周圍 hello 目標，因此被視為不精確，但它們為主 hello 準星型，所以正在被視為正確。

現在查看 hello 左上方的目標。 此處，我們的箭射中得非常接近，是一個緊密的群組。 它們是精確，但因為 hello 中心是關閉 hello 準星型的方式不正確。 此外，當然 hello 左下方目標中的 hello 箭號會不正確且不精確。 這位弓箭手需要多加練習。

## <a name="do-you-have-enough-data-toowork-with"></a>您有足夠的資料 toowork 與嗎？
最後，成分 #4-toohave 我們需要足夠的資料。

![您是否有足夠資料可進行分析？ 資料評估](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/barely-enough-data.png)

將表格中的每一個資料點視為繪圖中的筆刷筆劃。 如果您有只有少數幾個、 hello 繪製可以是很模糊： 很難 tootell 它為何。

如果您加入一些其他的筆刷筆觸，您繪製啟動 tooget 小清晰。

當您擁有足夠幾乎筆劃時，您可以看到剛才足夠 toomake 一些廣泛的決策。 它是可以 toovisit 的地方嗎？ 它看起來很明亮，看起來像潔淨的水 – 沒錯，這就是我想要度假的地方。

當您加入更多資料，hello 圖片變得更清楚，您可以做出更詳細的決策。 現在我可以查看 hello hello 左銀行上的三個旅館。 好了，喜歡 hello 的 hello 前景 hello 一個架構的功能。 我將會留在那裡，hello 第三個樓層。

相關、 連線、 正確的資料並不夠，我們有所有的 hello 因素，我們需要 toodo 某些高品質資料科學。

在其他四個視訊是確定 toocheck 出 hello*為初學者所設計的資料科學*從 Microsoft Azure 機器學習。

## <a name="next-steps"></a>後續步驟
* [嘗試使用 Machine Learning Studio 進行您的第一個資料科學實驗](machine-learning-create-experiment.md)
* [取得簡介 tooMachine Microsoft Azure 上學習](machine-learning-what-is-machine-learning.md)
