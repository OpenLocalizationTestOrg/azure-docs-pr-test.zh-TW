---
title: "在機器學習中的 aaaInterpret 模型結果 |Microsoft 文件"
description: "如何 toochoose hello 最佳參數設定演算法使用，並以視覺化方式檢視計分模型輸出。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6230e5ab-a5c0-4c21-a061-47675ba3342c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52161b1aa5ff3e7a63fc4b1bfb7c5e354eabcc50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="interpret-model-results-in-azure-machine-learning"></a>在 Azure Machine Learning 中解譯模型結果
本主題說明如何 toovisualize 並解譯 Azure Machine Learning Studio 中的預測結果。 在培訓模型並進行預測頂端 （「 計分模型 hello"） 之後，您需要 toounderstand，並解譯 hello 預測結果。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Azure Machine Learning 中有四個主要的機器學習類型：

* 分類
* 叢集
* 迴歸
* 推薦系統

用來預測在這些模型之上的 hello 模組為：

* [評分模型][score-model]模組，用於分類和迴歸
* [指派 tooClusters] [ assign-to-clusters]適用於叢集模組
* [評分 Matchbox 推薦][score-matchbox-recommender]，用於推薦系統

本文件說明如何 toointerpret 預測結果的每一個這些模組。 如需這些模組的概觀，請參閱[如何 toochoose 參數 toooptimize 您在 Azure Machine Learning 中的演算法](machine-learning-algorithm-parameters-optimize.md)。

本主題說明預測解譯，但是未說明模型評估。 如需有關如何 tooevaluate 自己的模型，請參閱[tooevaluate 建立 Azure Machine Learning 中的效能的模型](machine-learning-evaluate-model-performance.md)。

如果您是新 tooAzure 機器學習，而且需要協助建立簡易實驗 tooget 啟動，請參閱[Azure Machine Learning Studio 中建立簡易實驗](machine-learning-create-experiment.md)Azure Machine Learning Studio 中。

## <a name="classification"></a>分類
分類問題方面有兩個子類別：

* 只有兩個分類的問題 (雙類別或二進位分類)
* 兩個以上分類的問題 (多類別分類)

Azure Machine Learning 具有不同的模組 toodeal 與每一個這些類型的分類，但解譯預測結果的 hello 方法很相似。

### <a name="two-class-classification"></a>雙類別分類
**範例實驗**

二級分類問題的範例是光圈花 hello 分類。 hello 工作是 tooclassify 光圈花在根據其功能。 hello Azure Machine Learning 中提供的光圈資料集是子集 hello 熱門[光圈資料集](http://en.wikipedia.org/wiki/Iris_flower_data_set)只有兩個花盆物種 （類別 0 和 1） 包含的執行個體。 每個花卉有四個特徵 (萼片長度、萼片寬度、花瓣長度及花瓣寬度)。

![鳶尾花實驗的螢幕擷取畫面](./media/machine-learning-interpret-model-results/1.png)

圖 1. 鳶尾花雙類別分類問題實驗

實驗已執行的 toosolve 這個問題，如圖 1 所示。 已訓練及評分雙類別促進式決策樹模型。 現在您可以視覺化 hello 預測結果從 hello[計分模型][ score-model]模組，依序按一下輸出連接埠 hello hello[計分模型][ score-model]模組，然後按一下**視覺化**。

![評分模型模組](./media/machine-learning-interpret-model-results/1_1.png)

這會顯示 hello 計分結果，如圖 2 所示。

![鳶尾花雙類別分類實驗的結果](./media/machine-learning-interpret-model-results/2.png)

圖 2. 視覺化雙類別分類中的評分模型結果

**結果解譯**

Hello 結果資料表中有六個資料行。 hello 左四個資料行是 hello 四個功能。 hello 右邊的兩個資料行計分標籤和計分機率是 hello 預測結果。 hello 計分機率資料行顯示 hello 機率花所屬 toohello 正數類別 (類別 1)。 例如，hello hello 資料行 (0.028571)，則表示 0.028571 hello 第一個正確的機率所屬 tooClass 1 中的第一個數字。 hello 計分標籤資料行顯示 hello 預測每個季節的類別。 這根據 hello 計分機率資料行。 如果 hello 計分的花牌機率大於 0.5，它被預測為類別 1。 否則會預測為類別 0。

**Web 服務發佈**

已了解並認定為音效 hello 預測結果之後，hello 實驗可以發佈為 web 服務，以便您可以將它部署在不同的應用程式，並呼叫它 tooobtain 類別預測任何新的 iris 花牌上。 toolearn 如何 toochange 訓練試驗為計分試驗，以及發佈為 web 服務，請參閱[發佈 hello Azure Machine Learning web 服務](machine-learning-walkthrough-5-publish-web-service.md)。 此程序可提供給您如圖 3 所示的評分實驗。

![評分實驗的螢幕擷取畫面](./media/machine-learning-interpret-model-results/3.png)

圖 3. 計分 hello 光圈二級分類問題實驗

現在您可以針對 hello web 服務需要 tooset hello 輸入和輸出。 hello 輸入是 hello 右輸入的連接埠[計分模型][score-model]，這是 hello 光圈花功能輸入。 您好的選擇 hello 輸出取決於您是否想要在 hello 預測類別 （計分標籤）、 hello 計分機率，或兩者。 此範例假設您對兩者都感到興趣。 tooselect hello 預期輸出資料行，使用[資料集內選取資料行][ select-columns]模組。 依序按一下 [選取資料集中的資料行][select-columns] 和 **啟動資料行選取器**，然後選取 [評分標籤] 和 [評分機率]。 設定 hello 輸出連接埠之後[資料集內選取資料行][ select-columns] ，再次執行，您應該準備好 toopublish hello 計分實驗為 web 服務，即可**發行 WEB服務**。 如圖 4 所示 hello 最終實驗。

![hello 光圈二級分類實驗](./media/machine-learning-interpret-model-results/4.png)

圖 4. 鳶尾花雙類別分類問題的最終評分實驗

在執行 hello web 服務，並輸入測試執行個體的某些功能值之後，hello 結果會傳回兩個數字。 hello 第一個數字為 hello 計分標籤，並 hello 第二種是 hello 計分可能性。 此花卉預測為類別 1，其機率為 0.9655。

![測試解譯評分模型](./media/machine-learning-interpret-model-results/4_1.png)

![測試結果評分](./media/machine-learning-interpret-model-results/5.png)

圖 5. 鳶尾花雙類別分類的 Web 服務結果

### <a name="multi-class-classification"></a>多類別分類
**範例實驗**

在此實驗中，您將執行字母辨識工作，做為多元分類的範例。 hello 分類嘗試 toopredict 特定字母 （類別） 會根據從 hello 手寫的映像擷取某些手寫的屬性值。

![字母辨識範例](./media/machine-learning-interpret-model-results/5_1.png)

Hello 定型資料，在有 16 手寫的字母映像從擷取的功能。 hello 26 字母形成 26 類別。 圖 6 顯示將定型的多級分類的實驗字母辨識的模型，而預測 hello 上相同的功能集上測試資料集。

![字母辨識多類別分類實驗](./media/machine-learning-interpret-model-results/6.png)

圖 6. 字母辨識多類別分類問題實驗

視覺化 hello hello 結果[計分模型][ score-model]模組，依序按一下 hello 輸出連接埠[計分模型][ score-model]模組，然後按一下**視覺化**，如圖 7 所示，您應該看到的內容。

![評分模型模組](./media/machine-learning-interpret-model-results/7.png)

圖 7. 視覺化多類別分類中的評分模型結果

**結果解譯**

hello 左邊 16 個資料行代表 hello 測試集的 hello 功能值。 hello 像計分機率類別"XX"hello 二級案例中就如同 hello 計分機率資料行的名稱的資料行。 它們會顯示 hello 機率 hello 對應的項目屬於特定類別。 例如，對於 hello 第一個項目沒有 0.003571 機率，則"A"0.000451 機率則是"B，"依此類推。 hello 最後一個資料行 （計分標籤） 是 hello 與計分標籤在 hello 二級案例相同。 它會選取 hello 類別以 hello 最大計分機率為 hello hello 對應項目的預測的類別。 例如，為 hello 第一個項目 hello 計分標籤是"F"因為它有最大機率 toobe hello"F"(0.916995)。

**Web 服務發佈**

您也可以取得 hello hello 計分標籤的每個項目和 hello 機率計分標籤。 hello 基本邏輯是之間所有 hello 計分機率 toofind hello 最大機率。 toodo，您需要 toouse hello[執行 R 指令碼][ execute-r-script]模組。 圖 8 顯示 hello R 程式碼，且圖 9 顯示 hello 實驗的 hello 結果。

![R 程式碼範例](./media/machine-learning-interpret-model-results/8.png)

圖 8. 解壓縮計分標籤和 hello 的 R 程式碼相關聯的機率的 hello 標籤

![實驗結果](./media/machine-learning-interpret-model-results/9.png)

圖 9. 最終的計分實驗的 hello 字母辨識多級分類問題

發行和執行 hello web 服務並輸入一些輸入的功能值之後，hello 會傳回結果看起來像是圖 10。 此手寫的代號，其擷取 16 的功能，與為 0.9715 機率的預測的 toobe"T"。

![測試解譯評分模組](./media/machine-learning-interpret-model-results/9_1.png)

![測試結果](./media/machine-learning-interpret-model-results/10.png)

圖 10. 多類別分類的 Web 服務結果

## <a name="regression"></a>迴歸
迴歸問題與分類問題不同。 在分類問題，您正嘗試 toopredict 離散類別，例如哪一種類別光圈花屬於。 但是，您可以看到 hello 下列範例的迴歸問題中，您正嘗試 toopredict 連續變數，例如 hello 汽車價格。

**範例實驗**

使用汽車價格預測做為您的迴歸範例。 您正嘗試根據其功能，包括產生、 燃料類型、 內文類型和磁碟機滾輪一輛車 toopredict hello 價格。 圖 11 顯示 hello 實驗。

![汽車價格迴歸實驗](./media/machine-learning-interpret-model-results/11.png)

圖 11. 汽車價格迴歸問題實驗

以視覺化方式檢視 hello[計分模型][ score-model]模組，hello 結果看起來像圖 12。

![汽車價格預測問題的評分結果](./media/machine-learning-interpret-model-results/12.png)

圖 12. 計分結果 hello 汽車價格預測問題

**結果解譯**

計分的標籤是此計分結果中的 hello 結果資料行。 hello 預測每輛汽車價格的 hello 數字。

**Web 服務發佈**

您可以發行到 web 服務的 hello 迴歸實驗，並呼叫它在 hello 汽車價格預測 hello 二級分類相同方式使用大小寫。

![汽車價格迴歸問題的評分實驗](./media/machine-learning-interpret-model-results/13.png)

圖 13. 汽車價格迴歸問題的評分實驗

執行 hello web 服務，hello 傳回結果看起來像是圖 14。 hello 預測這輛汽車價格為 $15,085.52。

![測試解譯評分模組](./media/machine-learning-interpret-model-results/13_1.png)

![評分模組結果](./media/machine-learning-interpret-model-results/14.png)

圖 14. 汽車價格迴歸問題的 Web 服務結果

## <a name="clustering"></a>叢集
**範例實驗**

我們將使用 hello 光圈資料集一次 toobuild 叢集實驗。 這裡您可以篩選掉 hello hello 資料集中的類別標籤，以便只具有的功能，並可用於叢集。 在此光圈使用案例，指定在 hello 定型過程中，這表示您將叢集 hello 花兩個類別中的兩個叢集 toobe 的 hello 數目。 hello 實驗 圖 15 所示。

![鳶尾花叢集問題實驗](./media/machine-learning-interpret-model-results/15.png)

圖 15. 鳶尾花叢集問題實驗

叢集與分類的 hello 定型資料集沒有的地真資料標籤本身。 叢集群組 hello 訓練資料集的執行個體到不同的叢集。 Hello 定型在處理期間，hello 模型標籤 hello 學習 hello 差異及其功能的項目。 在這之後，您可以使用 hello 定型的模型 toofurther 分類未來的項目。 有兩個部分的 hello 結果，我們有興趣內叢集問題。 hello 第一個部分標記 hello 定型資料集，和 hello 第二個會分類新的資料集與 hello 定型的模型。

hello hello 結果的第一個部分可以以視覺化方式檢視，即可保留輸出連接埠的 hello[定型群集模型][ train-clustering-model] ，然後按一下**視覺化**。 圖 16 顯示 hello 視覺效果。

![叢集結果](./media/machine-learning-interpret-model-results/16.png)

圖 16. 以視覺化方式檢視叢集 hello 定型資料集的結果

hello hello 第二個部分，叢集 hello 定型群集模型中，新的項目結果所示圖 17。

![視覺化叢集結果](./media/machine-learning-interpret-model-results/17.png)

圖 17. 視覺化新資料集的叢集結果

**結果解譯**

雖然 hello hello 兩個部分結果源自不同實驗階段，它們看起來 hello 相同，並解譯在 hello 相同的方式。 hello 前四個資料行的功能。 hello 最後一個資料行，指派方式，是 hello 預測結果。 hello 預測相同數目的項目指派的 hello toobe hello 相同叢集，也就是在共用相似之處，在某些方面 （這項實驗中使用 hello 預設歐幾里德距離公制）。 因為指定的叢集 toobe 2 的 hello 數目，0 或 1，分別標示為指派中的 hello 項目。

**Web 服務發佈**

您可以發行到 web 服務叢集實驗的 hello 並呼叫它的群集預測 hello 相同方式與 hello 二級分類中使用的大小寫。

![鳶尾花叢集問題的評分實驗](./media/machine-learning-interpret-model-results/18.png)

圖 18. 鳶尾花叢集問題的評分實驗

執行 hello web 服務之後，hello 傳回結果看起來像是圖 19。 此花牌是預測的 toobe 0 叢集中。

![測試解譯評分模組](./media/machine-learning-interpret-model-results/18_1.png)

![評分模組結果](./media/machine-learning-interpret-model-results/19.png)

圖 19. 鳶尾花雙類別分類的 Web 服務結果

## <a name="recommender-system"></a>推薦系統
**範例實驗**

適用於推薦系統，您可以使用 hello 餐廳建議問題，做為範例： 您可以根據分級記錄的客戶建議餐廳。 hello 輸入的資料包含三個部分：

* 來自客戶的餐廳評等
* 客戶特色資料
* 餐廳特色資料

有幾件事，我們可以與 hello[定型 Matchbox 推薦][ train-matchbox-recommender] Azure Machine Learning 中的模組：

* 為指定使用者和項目預測評等
* 建議您指定使用者的項目 tooa
* 尋找給定使用者的使用者相關的 tooa
* 尋找項目相關的 tooa 給定項目

您可以選擇您希望 toodo 從 hello 中的 hello 四個選項中選取**推薦預測種類**功能表。 您可以在這裡逐步完成這四個案例。

![Matchbox 推薦](./media/machine-learning-interpret-model-results/19_1.png)

典型的推薦系統 Azure Machine Learning 實驗如圖 20 所示。 如需有關如何 toouse 這些推薦系統模組，請參閱資訊[定型 matchbox 推薦][ train-matchbox-recommender]和[計分 matchbox 推薦][ score-matchbox-recommender].

![推薦系統實驗](./media/machine-learning-interpret-model-results/20.png)

圖 20. 推薦系統實驗

**結果解譯**

**為指定使用者和項目預測評等**

藉由選取**評等預測**下**推薦預測種類**，您要詢問 hello 推薦系統 toopredict hello 評等來指定的使用者和項目。 hello 視覺效果的 hello[計分 Matchbox 推薦][ score-matchbox-recommender]輸出看起來像圖 21。

![分數 hello 推薦系統-評比預測的結果](./media/machine-learning-interpret-model-results/21.png)

圖 21. 以視覺化方式檢視 hello 推薦系統-評等預測中的 hello 分數結果

hello 前兩個資料行是 hello hello 輸入資料所提供的使用者-項目組。 hello 第三個資料行是 hello 預測的評等的特定項目的使用者。 比方說，hello 第一個資料列中 U1048 是的客戶的預測做為 2 toorate 餐廳 135026。

**建議您指定使用者的項目 tooa**

藉由選取**項目建議**下**推薦預測種類**，您指定使用者的系統 toorecommend 項目 tooa 問 hello 推薦。 在此案例中 hello 最後一個參數 toochoose 是*建議的項目選取*。 hello 選項**從評等項目 （適用於模型評估）**主要是供 hello 定型程序期間的模型評估。 對於此預測階段，我們選擇 [從所有項目] 。 hello 視覺效果的 hello[計分 Matchbox 推薦][ score-matchbox-recommender]輸出看起來像圖 22。

![推薦系統的評分結果 - 項目推薦](./media/machine-learning-interpret-model-results/22.png)

圖 22. 以視覺化方式檢視 hello 推薦系統項目建議分數結果

所提供的輸入資料 hello hello hello 六個資料行代表 hello 指定使用者識別碼 toorecommend 項目，第的一個。 hello 其他五個資料行代表 hello 建議 toohello 使用者相關性的遞減順序的項目。 例如，hello 第一個資料列，在 hello 最建議的餐廳客戶 U1048 是 134986，後面接著 135018、 134975、 135021 和 132862。

**尋找給定使用者的使用者相關的 tooa**

藉由選取**相關使用者**下**推薦預測種類**，您會問 hello 推薦系統 toofind 相關的使用者 tooa 指定使用者。 相關的使用者是 hello 具有相似的偏好。 在此案例中 hello 最後一個參數 toochoose 是*相關使用者選取*。 hello 選項**從使用者的評等項目 （適用於模型評估）**主要是供 hello 定型程序期間的模型評估。 對於此預測階段選擇 [從所有使用者]。 hello 視覺效果的 hello[計分 Matchbox 推薦][ score-matchbox-recommender]輸出看起來像圖 23。

![推薦系統的評分結果 - 相關使用者](./media/machine-learning-interpret-model-results/23.png)

圖 23. 以視覺化方式檢視 hello 推薦系統相關使用者的分數結果

第一次 hello 給定使用者所需的 Id toofind hello 六個資料行顯示 hello 的相關使用者所提供的輸入資料。 hello 其他五個資料行存放區 hello 相關性的遞減順序中的 hello 使用者預測相關的使用者。 例如，在 hello 第一個資料列，hello 客戶 U1048 最相關的客戶是 U1051，後面接著 U1066、 U1044、 U1017 和 U1072。

**尋找項目相關的 tooa 給定項目**

藉由選取**相關項目**下**推薦預測種類**，您要詢問 hello 推薦系統 toofind 相關項目 tooa 給定項目。 相關項目是 hello 項目最有可能 toobe 喜歡 hello 由相同使用者。 在此案例中 hello 最後一個參數 toochoose 是*相關的項目選取*。 hello 選項**從評等項目 （適用於模型評估）**主要是供 hello 定型程序期間的模型評估。 對於此預測階段，我們選擇 [ **從所有項目** ]。 hello 視覺效果的 hello[計分 Matchbox 推薦][ score-matchbox-recommender]輸出看起來像圖 24。

![推薦系統的評分結果 - 相關項目](./media/machine-learning-interpret-model-results/24.png)

圖 24. 將相關項目-hello 推薦系統的分數結果視覺化

hello hello 六個資料行代表 hello 指定所需的項目 Id 中的第一個 toofind hello 輸入資料所提供，相關項目。 hello 其他五個資料行存放區 hello hello 項目以遞減的順序，根據關聯的預測相關的項目。 例如，在 hello 第一個資料列項目的 135026 hello 最相關的項目是 135074，後面接著 135035、 132875、 135055 和 134992。

**Web 服務發佈**

hello 程序發行為 web 服務 tooget 預測實驗是每個 hello 四種案例類似。 這裡我們採用 hello 第二個案例 (給定使用者建議項目 tooa) 做為範例。 您可以遵循與其他三個 hello hello 相同的程序。

儲存 hello 定型推薦系統為定型的模型，以及篩選 hello 輸入的資料 tooa 單一使用者識別碼資料行做為要求，您可以如同圖 25 hello 實驗相連結，並將其發行為 web 服務。

![計分實驗的 hello 餐廳建議問題](./media/machine-learning-interpret-model-results/25.png)

圖 25. 計分實驗的 hello 餐廳建議問題

執行 hello web 服務，hello 傳回結果看起來像是圖 26。 hello 五個建議的餐廳使用者 U1048 是 134986、 135018、 134975、 135021 和 132862。

![推薦系統服務的範例](./media/machine-learning-interpret-model-results/25_1.png)

![範例實驗結果](./media/machine-learning-interpret-model-results/26.png)

圖 26. 餐廳推薦問題的 Web 服務結果

<!-- Module References -->
[assign-to-clusters]: https://msdn.microsoft.com/library/azure/eed3ee76-e8aa-46e6-907c-9ca767f5c114/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-matchbox-recommender]: https://msdn.microsoft.com/library/azure/55544522-9a10-44bd-884f-9a91a9cec2cd/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-clustering-model]: https://msdn.microsoft.com/library/azure/bb43c744-f7fa-41d0-ae67-74ae75da3ffd/
[train-matchbox-recommender]: https://msdn.microsoft.com/library/azure/fa4aa69d-2f1c-4ba4-ad5f-90ea3a515b4c/
