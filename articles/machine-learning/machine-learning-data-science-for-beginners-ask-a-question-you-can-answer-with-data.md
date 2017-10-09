---
title: "aaaAsk 可以回答問題資料-資料科學問題 Azure Machine Learning |Microsoft 文件"
description: "了解如何 tooformulate 尖資料科學問題在資料科學中適用於初學者視訊 3。 包含分類和迴歸問題的比較。"
keywords: "資料科學問題, 資料科學問題, 制訂問題, 迴歸問題, 分類問題, 明確的問題"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: 5b9501e3-9964-417a-8ffc-8913103da77b
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: 00c328f51e6d9ff6654b5966eb97d6762582f7e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="ask-a-question-you-can-answer-with-data"></a>詢問您可以使用資料回答的問題
## <a name="video-3-data-science-for-beginners-series"></a>影片 3：適用於初學者的資料科學系列
深入了解如何 tooformulate 資料科學問題到適用於初學者視訊 3 的資料科學問題。 這個影片包含適用於分類和迴歸演算法的問題比較。

充分利用 hello 數列 tooget hello 觀賞全部。 [前往影片 toohello 清單](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Data-science-for-beginners-Ask-a-question-you-can-answer-with-data/player]
>
>

## <a name="other-videos-in-this-series"></a>系列中的其他影片
*為初學者所設計的資料科學*是快速介紹 toodata 科學中五個簡短的影片。

* 視訊 1: [hello 5 個問題的資料科學答案](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *（5 分鐘 14 秒）*
* 影片 2： [您的資料已經可以進行資料科學了嗎？](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 分 56 秒)*
* 影片 3：詢問您可以使用資料回答的問題
* 影片 4：[利用簡單模型預測答案](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 分 42 秒)*
* 視訊 5:[複製其他人工作 toodo 資料科學](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *（3 分 18 秒）*

## <a name="transcript-ask-a-question-you-can-answer-with-data"></a>文字記錄：詢問您可以使用資料回答的問題
歡迎使用 toohello hello 數列中的第三個視訊 」 為初學者所設計的資料科學 」。  

您可以從這個影片中獲得一些秘訣，在制訂可以使用資料回答的問題時使用。

您可能會收到多個跨這段影片中，如果您先觀察 hello 兩個先前的影片序列中:"hello 5 問題資料科學可以回答 「 和 」 是您的資料已準備好資料科學？ 」

## <a name="ask-a-sharp-question"></a>詢問明確的問題
我們談論資料科學是 hello 程序使用名稱 （也稱為 「 類別 」 或 「 標籤 」） 的方式，與數字 toopredict 回應 tooa 問題。 但不是能是任何問題。它有 toobe*尖的問題。*

含糊不清的問題沒有 toobe 回答名稱或數字。 必須是明確的問題。

假設您找到一個神燈，其中的精靈將如實回答您詢問的任何問題。 但惡作劇 genie，，他會嘗試 toomake 微積分和令人困惑為其回應因為他可以消除。 您想 toopin 他向下提出問題，所以他無法幫助，但會告訴您什麼 airtight 想 tooknow。

如果您 tooask 含糊不清的問題，像是 「 發生什麼事與我股票 toohappen？ 」、 hello genie 可能回應，「 hello 價格會變更 」。 這是如實的回答，但不是很有幫助。

但如果您選擇了 tooask 尖的問題，例如 「 我的股票銷售價格是什麼下週？"，hello genie 無法幫助，但提供您特定回應，並預測銷售價格。

## <a name="examples-of-your-answer-target-data"></a>您的答案範例︰目標資料
一旦您建立問題，請檢查 toosee，無論您擁有 hello 回應的範例資料中。

如果問題是「我的股票下週售價是多少？ 然後我們有 toomake 確定我們的資料包含 hello 股票價格記錄。

如果我們的問題是 「 在我的以及哪些汽車是進行 toofail 先？ 」 然後我們有 toomake 確定我們的資料包含先前失敗的相關資訊。

![目標資料 - 您的答案範例。 制訂資料科學問題。](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/target-data.png)

這些答案範例就稱為目標。 目標是我們的是類別或數字是否嘗試 toopredict 需未來的資料點。

如果您沒有任何目標資料，您將一些需要 tooget。 您不是您的問題，但它不能 tooanswer。

## <a name="reformulate-your-question"></a>重新制訂您的問題
有時候您可以改寫程式問題 tooget 更有用的解答。

hello 問題 」 是此資料點 A 或 B？ 」 預測 hello 類別 （或名稱或標籤） 的某個項目。 tooanswer，我們會使用*分類演算法*。

hello 問題 」 多少？ 」 」或「有多少？ 」這類問題會預測數量。 tooanswer 我們會使用它*迴歸演算法*。

toosee 如何我們可以轉換，讓我們看看 hello，"的新聞報導 hello 最有趣 toothis 讀取器？ 」 問題 」 它要求從多個可能性中預測單一選擇 (換句話說，就是「這是 A 或 B 或 C 或 D？ 」)，並會使用分類演算法。

但是，如果它當做重述您這個問題可能會更容易 tooanswer 「 有趣程度是在這個清單 toothis 讀取器上的每個劇本？ 」 現在您可以為每個發行項的數字的分數，則輕鬆 tooidentify hello 得分最高的發行項。 這是進而迴歸問題 hello 分類問題或多少？

![重新制訂您的問題。 分類問題與迴歸問題。](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/classification-question-vs-regression-question.png)

您如何詢問問題線索 toowhich 演算法可以為您解答。

您會發現特定系列的演算法-hello 的新聞報導在本例中為像是密切相關。 您可以重新編寫您的問題 toouse hello 的演算法，可讓您 hello 最有用的解答。

但是，最重要的詢問該尖的問題-hello 與資料，您可以回答的問題。 並確定您擁有 hello 正確的資料 tooanswer 它。

我們談論了一些基本原則，讓您在詢問可使用資料回答的問題時使用。

為確定 toocheck 出 hello"的資料科學的初學者 」 從 Microsoft Azure Machine Learning 中的其他視訊。

## <a name="next-steps"></a>後續步驟
* [嘗試使用 Machine Learning Studio 進行您的第一個資料科學實驗](machine-learning-create-experiment.md)
* [取得簡介 tooMachine Microsoft Azure 上學習](machine-learning-what-is-machine-learning.md)
