---
title: "aaaEvaluate 機器學習模型效能 |Microsoft 文件"
description: "說明如何 tooevaluate 模型 Azure Machine Learning 中的效能。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 5dc5348a-4488-4536-99eb-ff105be9b160
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bradsev;garye
ms.openlocfilehash: 03477368758dbb13aa6f54c5d27fb215615d1f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooevaluate-model-performance-in-azure-machine-learning"></a>Tooevaluate 建立 Azure Machine Learning 中的效能的模型
本文示範如何 tooevaluate hello Azure Machine Learning Studio 中之模型的效能，並提供可用的 hello 度量的簡短說明這項工作。 提供三種常見的受監督的學習案例： 

* 迴歸
* 二進位分類 
* 多元分類

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

評估模型的 hello 效能是其中一個 hello 資料科學程序中的 hello 核心階段。 它會指出成功的 hello 計分 （預測） 的資料集已定型的模型。 

Azure Machine Learning 支援透過兩個主要的機器學習服務模組來評估模型：[評估模型][evaluate-model]和[交叉驗證模型][cross-validate-model]。 這些模組可讓您 toosee 模型方面的幾個常用在機器學習和統計資料的度量的執行。

## <a name="evaluation-vs-cross-validation"></a>評估與交叉驗證
評估和交叉驗證是模型的標準方式 toomeasure hello 效能。 它們都會產生您可以對照其他模型的度量檢查或比較的評估度量。

[評估模型][ evaluate-model]預期評分資料集做為輸入 （或您想要 2 的不同模型 toocompare hello 效能的在案例 2）。 這表示您需要 tootrain 模型使用 hello[定型模型][ train-model]模組，請使用 hello 某些資料集的預測[計分模型][ score-model]模組，您可以評估 hello 結果之前。 hello 評估根據 hello 計分標籤/機率 hello true 標籤，都是輸出的 hello[計分模型][ score-model]模組。

或者，您可以使用交叉驗證 tooperform 定型分數評估作業數目 （10 個摺疊） 會自動在不同的子集上的 hello 輸入資料。 hello 輸入的資料是分割成 10 個組件，其中一個保留供測試，及 hello 訓練其他 9。 此程序會重複 10 次，平均計算 hello 評估度量。 這有助於判斷模型會一般化 toonew 資料集的程度。 hello[交叉驗證模型][ cross-validate-model]模組會採用未定型的模型中某些標示為資料集和輸出 hello 評估結果的每個 hello 10 個摺疊，此外 toohello 平均結果。

在下列各節的 hello，我們將建立簡單的迴歸和分類模型和評估效能，使用這兩個 hello[評估模型][ evaluate-model]和 hello[交叉驗證模型][ cross-validate-model]模組。

## <a name="evaluating-a-regression-model"></a>評估迴歸模型
假設我們想 toopredict 使用某些功能，例如維度、 馬力、 引擎規格和等等的汽車的價格。 這是一般迴歸問題，其中 hello 目標變數 (*價格*) 是連續的數值。 我們可以放入指定的 hello 功能特定汽車的值可以預測 hello 該汽車價格簡單的線性迴歸模型。 可以使用此迴歸模型 tooscore hello 我們定型的相同資料集。 一旦我們有 hello 預測所有都 hello 汽車的價格，我們可以藉由查看多少都 hello 預測偏離都 hello 實際價格平均評估都 hello 模型的都 hello 效能。 tooillustrate，我們使用 hello*汽車價格資料 (Raw) 資料集*用於 hello**儲存的資料集**Azure Machine Learning Studio 中的區段。

### <a name="creating-hello-experiment"></a>建立 hello 實驗
新增下列模組 tooyour 工作區，在 Azure Machine Learning Studio 中的 hello:

* 汽車價格資料 (原始)
* [線性迴歸][linear-regression]
* [訓練模型][train-model]
* [計分模型][score-model]
* [評估模型][evaluate-model]

連接 hello 連接埠，如下所示的圖 1 和集 hello 標籤資料行的 hello[定型模型][ train-model]模組太*價格*。

![評估迴歸模型](media/machine-learning-evaluate-model-performance/1.png)

圖 1. 評估迴歸模型。

### <a name="inspecting-hello-evaluation-results"></a>檢查 hello 評估結果
之後執行 hello 實驗中，您可以按一下輸出連接埠 hello hello[評估模型][ evaluate-model]模組，然後選取*視覺化*toosee hello 評估結果。 迴歸模型的 hello 可用的評估度量：*平均絕對誤差*，*根平均絕對誤差*，*相對的絕對誤差*， *相對平方誤差*，和 hello*判斷的係數*。

「 錯誤 」 此處代表 hello 差異 hello 詞彙 hello 預測的值和 hello true 值。 hello 絕對值或 hello 方形的這項差異是通常計算的 toocapture hello 總 hello hello 差異為所有的執行個體錯誤的預測，則為 true 的值可以是負數，在某些情況下。 hello 誤差度量會測量 hello 方面 hello 標準差的 hello，則為 true 的值從其預測迴歸模型的預測的效能。 下限誤差值表示 hello 模型做預測更精確。 為 0 表示 hello 模型的整體錯誤公制完全符合 hello 資料。

決定，也就是也稱為 R hello 係數平方，也是標準的方式，測量 hello 模型符合 hello 資料的程度。 它可解譯為 hello 比例 hello 模型所說明的變化。 在此情況下，比例越高越好，其中 1 表示完全符合。

![線性迴歸評估度量](media/machine-learning-evaluate-model-performance/2.png)

圖 2. 線性迴歸評估度量。

### <a name="using-cross-validation"></a>使用交叉驗證
如先前所述，您可以執行重複的訓練、 評分和評估會自動使用 hello[交叉驗證模型][ cross-validate-model]模組。 在這種情況下，您只需要一個資料集、一個非定型模型，以及一個[交叉驗證模型][cross-validate-model]模組 (請參閱下圖)。 請注意，您需要 tooset hello 標籤資料行太*價格*在 hello[交叉驗證模型][ cross-validate-model]模組的屬性。

![交叉驗證迴歸模型](media/machine-learning-evaluate-model-performance/3.png)

圖 3. 交叉驗證迴歸模型。

之後執行 hello 實驗中，您可以檢查 hello 評估結果 hello hello 右輸出連接埠上的 [[交叉驗證模型][ cross-validate-model]模組。 這會針對每個反覆項目 （摺疊），提供 hello 度量的詳細的檢視與 hello 平均每個 hello 度量 (圖 4) 的結果。

![迴歸模型的交叉驗證結果](media/machine-learning-evaluate-model-performance/4.png)

圖 4. 迴歸模型的交叉驗證結果。

## <a name="evaluating-a-binary-classification-model"></a>評估二進位分類模型
在二進位分類案例中，hello 目標變數具有只有兩個可能的結果，例如: {0，1} 或 {false，則為 true}，{負數，正}。 假設您有一些成人員工的資料集人口統計和雇變數，並詢問 toopredict hello 收入層級，二進位變數與 hello 值 {"< = 50k"，"> 50k 個"}。 換句話說，hello 負類別代表 hello 的員工進行小於或等於每個年份和 hello 正數類別表示所有其他員工 too50K。 如同 hello 迴歸案例中，我們會為模型定型、 分數部分資料，並評估 hello 結果。 此處 hello 主要的差異在於 hello 選擇的 Azure Machine Learning 計算的度量和輸出。 tooillustrate hello 收入層級的預測案例中，我們將使用 hello[成人](http://archive.ics.uci.edu/ml/datasets/Adult)資料集 toocreate Azure 機器學習實驗和評估二級羅吉斯迴歸模型，常用的二進位檔的 hello 效能分類器。

### <a name="creating-hello-experiment"></a>建立 hello 實驗
新增下列模組 tooyour 工作區，在 Azure Machine Learning Studio 中的 hello:

* 成人收入普查二進位分類資料集
* [二元羅吉斯迴歸][two-class-logistic-regression]
* [訓練模型][train-model]
* [計分模型][score-model]
* [評估模型][evaluate-model]

圖 5 和集合的 hello hello 標籤資料行中，如下所示為 hello 連接埠的連接[定型模型][ train-model]模組太*收入*。

![評估二進位分類模型](media/machine-learning-evaluate-model-performance/5.png)

圖 5. 評估二進位分類模型。

### <a name="inspecting-hello-evaluation-results"></a>檢查 hello 評估結果
之後執行 hello 實驗中，您可以按一下輸出連接埠 hello hello[評估模型][ evaluate-model]模組，然後選取*視覺化*toosee hello 評估結果 (圖 7)。 二元分類模型的 hello 可用的評估度量：*精確度*，*精確度*，*回收*， *F1 分數*，和*AUC*。 此外，hello 模組會輸出混淆矩陣顯示 hello 數目以及真肯定、 誤否定、 誤判、 真否定、 以及*ROC*，*重新叫用精確度/*，和*提起*曲線。

精確度是只要 hello 比例的正確分類執行個體。 它通常是 hello 您查看評估分類器時的第一個公制。 不過，當 hello 測試資料是不對稱的 （大部分的 hello 執行個體所屬的 hello 類別 tooone），或您有興趣更 hello hello 類別的其中一個的效能，精確度不真的擷取 hello 有效性的分類器。 在 hello 收入層級分類案例中，假設您要測試某些資料，其中 99%的 hello 執行個體代表人贏得小於或等於 too50K 每年。 這是可能 tooachieve 0.99 精確度預測 hello 類別"< = 50k"所有執行個體。 hello 分類器在此情況下會出現 toobe 做得不錯整體，但事實上，它失敗時 tooclassify hello 收入個人 （hello 1%) 的正確。

因此，它是很有幫助 toocompute 擷取的 hello 評估更特定層面的其他度量。 移到這種衡量標準的 hello 詳細資料之前, 是二元分類評估的重要 toounderstand hello 混淆矩陣。 hello 類別只有 2 可能的值，哪個我們通常會採用 hello 定型集內的標籤，請參閱 tooas 正數或負數。 hello 正數和負數的執行個體正確預測分類器稱為真肯定 (TP) 和真否定 (TN)，分別。 同樣地，hello 分類錯誤執行個體稱為 (FP) 誤判和誤否定 (FN)。 hello 混淆矩陣是只要資料表顯示 hello 落在每個這些 4 種類別的執行個體數目。 Azure Machine Learning 會自動決定哪一個 hello hello 資料集中的兩個類別是 hello 正數類別。 如果 hello 類別標籤是布林值或整數，則 hello 'true' 或 '1' 標記的執行個體就會指派 hello 正數類別。 如果 hello 標籤是字串，如同 hello 情況 hello 收入資料集，hello 標籤依字母順序排序，然後 hello 第一個層級 hello 正數類別 hello 第二個層級時選擇 toobe hello 負類別。

![二元分類混淆矩陣](media/machine-learning-evaluate-model-performance/6a.png)

圖 6. 二進位分類混淆矩陣。

返回 toohello 收入分類問題，我們可能會想的 tooask 幾個評估問題，可協助我們了解 hello hello 分類器使用的效能。 很自然的問題是: ' hello 個人對 hello 超出模型預測的 toobe 贏得 > 50k 個 (TP + FP)、 多少已正確分類 (TP) 嗎？ ' 可以回答這個問題，藉由查看 hello**精確度**的 hello 模型，這是 hello 比例的正確分類的誤判： TP/(TP+FP)。 另一個常見的問題是"hello 高 earning 具有所有員工收入超出 > 多少未 hello 分類 50k 個 (TP + FN)、 正確分類 (TP) 」。 這是實際 hello**回收**，或 hello true positive 速率： TP/(TP+FN) hello 分類器。 您可能會注意到在精確度與回收之間有明顯的取捨。 比方說，假設相當對稱資料集，分類器，來預測大部分正執行個體，會有高回收，但會導致大量的誤判誤相當低的有效位數最大數量的 hello 負的執行個體的分類。 toosee 繪製這些度量的而有所不同，您可以按一下 hello 評估的結果輸出頁中的 hello '精確度/重新叫用' 曲線 （左上方圖 7 部分）。

![二元分類評估結果](media/machine-learning-evaluate-model-performance/7.png)

圖 7. 二進位分類評估結果。

另一個相關的常用的公制為 hello **F1 分數**，其可接受有效位數和回收列入考量。 它是這些 2 度量 hello 調和平均數，在這種情況的計算： F1 = 2 （有效位數 x 重新叫用） / （有效位數 + 重新叫用）。 hello F1 分數是很好的方式 toosummarize hello 評估中的單一數字，但它一定會是很好的作法 toolook 台有效位數和回收一起 toobetter 了解分類器的運作方式。

此外，其中一個可以檢查 hello true 正數的速率與 hello false positive 速率 hello**接收者 (ROC)**曲線和 hello 對應**區域底下 hello 曲線 (AUC)**值。 hello 接近此曲線 toohello 上方左上角，hello 更佳 hello 分類器的效能 （也就是而言，發揮最佳 hello true 正數頻率降至最低 hello false positive 速率）。 關閉 toohello 斜線曲線 hello 繪圖，分類器通常 toomake 預測的結果會關閉 toorandom 猜測。

### <a name="using-cross-validation"></a>使用交叉驗證
如同 hello 迴歸範例中，我們可以執行交叉驗證 toorepeatedly 定型、 評分和自動評估 hello 資料的不同子集。 同樣地，我們可以使用 hello[交叉驗證模型][ cross-validate-model]模組、 定型羅吉斯迴歸模型，與資料集。 hello 標籤資料行必須設定得*收入*在 hello[交叉驗證模型][ cross-validate-model]模組的屬性。 執行 hello 實驗，並按一下向右 hello 輸出連接埠的 hello 之後[交叉驗證模型][ cross-validate-model]模組中，我們可以看到 hello 二元分類度量值針對每個摺疊，此外 toohello平均和標準差的每個。 

![交叉驗證二元分類模型](media/machine-learning-evaluate-model-performance/8.png)

圖 8. 交叉驗證二進位分類模型。

![二元分類器的交叉驗證結果](media/machine-learning-evaluate-model-performance/9.png)

圖 9. 二進位分類器的交叉驗證結果。

## <a name="evaluating-a-multiclass-classification-model"></a>評估多元分類模型
在此實驗中，我們將使用熱門 hello[光圈](http://archive.ics.uci.edu/ml/datasets/Iris "光圈")資料集包含 3 種 hello 光圈工廠類型 （類別） 的執行個體。 每個案例有 4 個特性值 (萼片長度/寬度和花瓣長度/寬度)。 Hello 先前實驗定型和測試的 hello 模型使用 hello 相同的資料集。 在這裡，我們將使用 hello[分割資料][ split]模組 toocreate 2 hello 資料子集，首先，hello 來定型和計分，並評估 hello 上第二個。 hello 光圈資料集並公開用於 hello [UCI 機器學習儲存機制](http://archive.ics.uci.edu/ml/index.html)，而且可以使用下載[匯入資料][ import-data]模組。

### <a name="creating-hello-experiment"></a>建立 hello 實驗
新增下列模組 tooyour 工作區，在 Azure Machine Learning Studio 中的 hello:

* [匯入資料][import-data]
* [多元決策樹系][multiclass-decision-forest]
* [分割資料][split]
* [訓練模型][train-model]
* [計分模型][score-model]
* [評估模型][evaluate-model]

連接 hello 連接埠，如下所示，在圖 10。

設定 hello 標籤資料行索引的 hello[定型模型][ train-model]模組 too5。 hello 資料集則沒有標頭資料列，但我們了解該標籤是 hello 第五個資料行中的 hello 類別。

按一下 hello[匯入資料][ import-data]模組和組 hello*資料來源*屬性太*透過 HTTP 的 Web URL*，和 hello *URL* toohttp://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data。

執行個體 toobe 用於定型在 hello 組 hello 分數[分割資料][ split]模組 (例如 0.7)。

![評估多元分類器](media/machine-learning-evaluate-model-performance/10.png)

圖 10. 評估多元分類器

### <a name="inspecting-hello-evaluation-results"></a>檢查 hello 評估結果
執行 hello 實驗，然後按一下 hello 輸出連接埠上[評估模型][evaluate-model]。 hello 評估結果是 hello 形式呈現混淆矩陣，在此情況下。 hello 矩陣會顯示 hello 實際與預測所有 3 個類別執行個體。

![多元分類評估結果](media/machine-learning-evaluate-model-performance/11.png)

圖 11. 多元分類評估結果。

### <a name="using-cross-validation"></a>使用交叉驗證
如先前所述，您可以執行重複的訓練、 評分和評估會自動使用 hello[交叉驗證模型][ cross-validate-model]模組。 您需要一個資料集、一個非定型模型，以及一個[交叉驗證模型][cross-validate-model]模組 (請參閱下圖)。 您一次需要 tooset hello 標籤資料行的 hello[交叉驗證模型][ cross-validate-model]模組 （資料行索引 5 在此情況下）。 執行 hello 實驗，並按一下 hello 右邊的輸出連接埠的 hello 之後[交叉驗證模型][cross-validate-model]，針對每個摺疊與 hello 平均數和標準差，您可以檢查 hello 公制值。 此處顯示的 hello 度量資訊是 hello 類似 toohello hello 二元分類的案例中討論。 不過請注意，在多級分類中，運算 hello 真肯定/否定和 false 的誤判否定已完成，透過計算針對每個類別，因為沒有任何整體正或負的類別。 比方說，當運算 hello 有效位數或重新叫用的 hello ' 光圈 setosa' 類別，它會假設這是 hello 正數類別和其他所有項目做為負。

![交叉驗證多元分類模型](media/machine-learning-evaluate-model-performance/12.png)

圖 12. 交叉驗證多元分類模型。

![多元分類模型的交叉驗證結果](media/machine-learning-evaluate-model-performance/13.png)

圖 13. 多元分類模型的交叉驗證結果。

<!-- Module References -->
[cross-validate-model]: https://msdn.microsoft.com/library/azure/75fb875d-6b86-4d46-8bcc-74261ade5826/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[multiclass-decision-forest]: https://msdn.microsoft.com/library/azure/5e70108d-2e44-45d9-86e8-94f37c68fe86/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-logistic-regression]: https://msdn.microsoft.com/library/azure/b0fd7660-eeed-43c5-9487-20d9cc79ed5d/

