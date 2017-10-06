---
title: "aaaA Machine Learning Studio 中的簡易實驗 |Microsoft 文件"
description: "此機器學習服務教學課程會引導您輕鬆進行資料科學實驗。 我們會預測 hello 使用迴歸演算法的汽車價格。"
keywords: "實驗、線性迴歸、機器學習服務演算法、機器學習服務教學課程、預測性模型技術、資料科學實驗"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: fb215851d380acf7d0f4934a426283369f9c4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a>機器學習服務教學課程：在 Azure Machine Learning Studio 中建立您的第一個資料科學實驗

如果您從未使用過 **Azure Machine Learning Studio**，本教學課程很適合您。

在本教學課程中，我們將逐步引導 hello toouse Studio 第一次 toocreate 機器學習實驗。 hello 實驗會測試預測 hello 根據不同的變數，例如產生和技術規格汽車價格的分析模型。

> [!NOTE]
> 本教學課程會示範 hello 基本概念的方式 toodrag 放模組至您的經驗，連接在一起，請執行 hello 實驗，並查看 hello 結果。 我們不打算 toodiscuss hello 的機器學習的一般主題或 tooselect 並用 hello 100 + 內建演算法和資料操作已包含在 Studio 中。
>
>如果您是新 toomachine 學習，hello 影片系列[為初學者所設計的資料科學](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md)可能是很好的起點 toostart。 這一系列影片是絕佳的簡介 toomachine 學習使用日常用語和概念。
>
>如果您是熟悉 machine learning 中，但您想要尋求 Machine Learning Studio 和 hello 機器學習的演算法，它包含更多一般資訊，以下是一些實用的資源：
>
- [什麼是 Machine Learning Studio？](machine-learning-what-is-ml-studio.md) - 這是 Studio 的高階概觀。
- [機器學習演算法範例的基本概念](machine-learning-basics-infographic-with-algorithm-examples.md)-此資訊圖很有用，如果您想 toolearn 更多關於 hello 不同類型的機器學習 Studio 隨附的機器學習演算法。
- [機器學習指南](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1)-本指南涵蓋 hello 資訊圖上述項目，但以互動形式類似的資訊。
- [機器學習演算法小祕技](machine-learning-algorithm-cheat-sheet.md)和[如何 toochoose 演算法為 Microsoft Azure 機器學習](machine-learning-algorithm-choice.md)-此可下載海報和隨附的文章討論深度 hello Studio 演算法。
- [Machine Learning Studio： 演算法和模組說明](https://msdn.microsoft.com/library/azure/dn905974.aspx)-這是所有 Studio 模組，包括機器學習演算法，hello 完整的參考

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a>Machine Learning Studio 如何協助您？

Machine Learning Studio 可輕鬆 tooset 向上實驗中使用拖放模組預先排定使用預測模型的技巧。

使用互動式的視覺化工作區，可以拖放***資料集***和***分析***模組到互動式畫布。 連接在一起的 tooform***實驗***Machine Learning Studio 中執行。
您***建立模型***， ***hello 模型定型***，和***分數與測試 hello 模型***。

您可以在逐一查看您的模型設計，編輯 hello 實驗，並執行直到它可讓您 hello 想要的結果。 當您的模型就緒後，您可以將其發行為 ***Web 服務***，讓其他人可以傳送新資料到該服務，並取得預測結果。

## <a name="open-machine-learning-studio"></a>開啟 Machine Learning Studio

Studio 中，以啟動 tooget 移過[https://studio.azureml.net](https://studio.azureml.net)。 如果您之前已登入過 Machine Learning Studio，請按一下 [登入]。 否則，請按一下 [由此註冊] 並選擇免費或付費選項。

![登入 tooMachine Learning Studio][sign-in-to-studio]
<br/>
***登入 tooMachine Learning Studio***

## <a name="five-steps-toocreate-an-experiment"></a>五個步驟 toocreate 實驗

在此機器學習教學課程中，您將遵循五個基本步驟 toobuild Machine Learning Studio toocreate，定型，在實驗和計分模型：

- **建立模型**
    - [步驟 1：取得資料]
    - [步驟 2： 準備 hello 資料]
    - [步驟 3：定義功能]
- **定型 hello 模型**
    - [步驟 4：選擇及套用學習演算法]
- **分數與測試 hello 模型**
    - [步驟 5：預測新的汽車價格]

[步驟 1：取得資料]: #step-1-get-data
[步驟 2： 準備 hello 資料]: #step-2-prepare-the-data
[步驟 3：定義功能]: #step-3-define-features
[步驟 4：選擇及套用學習演算法]: #step-4-choose-and-apply-a-learning-algorithm
[步驟 5：預測新的汽車價格]: #step-5-predict-new-automobile-prices

> [!TIP] 
> 您可以找到 hello 的下列實驗中 hello [Cortana 智慧組件庫](https://gallery.cortanaintelligence.com)。 跳過**[第一次的資料科學實驗-汽車價格預測](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)**按一下**在 Studio 中開啟**toodownload hello 到機器學習的實驗的複本Studio 工作區。


## <a name="step-1-get-data"></a>步驟 1：取得資料

您需要 tooperform 機器學習 hello 第一件事是資料。
Machine Learning Studio 隨附多個範例資料集供您使用，或者，您可以從許多來源匯入資料。 此範例中，我們將使用 hello 範例資料集，**汽車價格資料 (Raw)**，被包含在您的工作區。
此資料集將包含許多個別汽車的項目，包括製造、模型、技術規格和價格等資訊。

以下是如何 tooget hello 到您的經驗的資料集。

1. 按一下 建立新的實驗**+ 新增**在 hello hello Machine Learning Studio 視窗底部，選取**實驗**，然後選取**空白實驗**。

2. hello 實驗會給予您可以查看 hello hello 畫布上方的預設名稱。 選取這段文字，並將它重新命名 toosomething 有意義，例如**汽車價格預測**。 hello 名稱不需要 toobe 唯一。

    ![重新命名 hello 實驗][rename-experiment]

2. toohello hello 實驗畫布左邊是資料集和模組的調色盤。 型別**汽車**在 hello 搜尋 方塊上方標示為此調色盤 toofind hello 資料集的 hello**汽車價格資料 (Raw)**。 將此資料集 toohello 實驗畫布。

    ![尋找 hello 汽車的資料集，並將它拖曳至 hello 實驗畫布][type-automobile]
    <br/>
    ***尋找 hello 汽車的資料集，並將它拖曳至 hello 實驗畫布***

toosee 什麼這項資料看來，按一下底端 hello hello 汽車的資料集，hello 輸出連接埠，然後選取**視覺化**。

![按一下 hello 輸出連接埠，然後選取 「 視覺化"][select-visualize]
<br/>
***按一下 hello 輸出連接埠，然後選取 「 視覺化"***

> [!TIP]
> 資料集和模組具有輸入和輸出連接埠由小圓形-在 hello 上方的輸入連接埠輸出 hello 底端的連接埠。
toocreate 透過實驗資料的流程，您連接的另一個模組 tooan 輸入埠的輸出連接埠。
在任何時候，您可以按一下資料集或模組 toosee hello 輸出連接埠 hello 資料看起來像此時 hello 資料流程中。

在此範例資料集中，汽車的每個執行個體顯示為一個資料列，並與每個汽車相關聯的 hello 變數顯示為資料行。 指定特定的汽車 hello 變數，我們 tootry toopredict hello 價格最右側資料行 (資料行 26，標題為"price") 中。

![在 hello 資料視覺效果視窗中檢視 hello 汽車資料][visualize-auto-data]
<br/>
***在 hello 資料視覺效果視窗中檢視 hello 汽車資料***

按一下 hello 關閉 hello 視覺效果視窗"**x**"hello 右上角。

## <a name="step-2-prepare-hello-data"></a>步驟 2： 準備 hello 資料

資料集通常必須先經過某些前置處理，才能進行分析。 例如，您可能已注意到 hello 遺漏 hello 的各種不同的資料列的資料行中存在的值。 Toobe 清除 hello 模型可以分析 hello 資料正確，因此需要這些遺漏的值。 在我們的案例中，我們將移除含有遺漏值的所有資料列。 此外，hello**正常化損失**資料行有大比例的遺漏值，因此我們將會排除該資料行 hello 模型完全。

> [!TIP]
> 清理 hello 遺漏值，從輸入資料是使用大多數 hello 模組的必要條件。

我們先新增移除 hello 模組**正常化損失**資料行完全，然後我們將會移除有遺漏資料的任何資料列的另一個模組。

1. 型別**選取資料行**在 hello 搜尋 方塊上方的 hello 模組調色盤 toofind hello hello[資料集中選取的資料行][ select-columns]模組，然後將它拖曳 toohello 實驗畫布. 此模組可讓我們 tooselect 我們想 tooinclude 中或排除的哪些資料行 hello 模型。

2. 連接 hello hello 輸出連接埠**汽車價格資料 (Raw)**資料集 toohello 輸入連接埠 hello[資料集中選取的資料行][ select-columns]模組。

    ![加入 hello 」 選取資料行中資料集 」 模組 toohello 實驗畫布，其連接][type-select-columns]
    <br/>
    ***加入 hello 」 選取資料行中資料集 」 模組 toohello 實驗畫布，其連接***

3. 按一下 hello[資料集中選取的資料行][ select-columns]模組，然後按一下**啟動資料行選取器**在 hello**屬性**窗格。

    - Hello 左側，按一下 **規則**
    - 在 [開始於] 下，按一下 [所有資料行]。 這樣便會指引[資料集中選取的資料行][ select-columns] toopass 透過所有的 hello 資料行 （除了我們 tooexclude 有關這些資料行）。
    - 從 [hello] 下拉式清單，選取 [**排除**和**資料行名稱**，然後按一下hello] 文字方塊內。 資料行清單隨即顯示。 選取**正常化損失**，而且它是加入的 toohello 文字方塊。
    - 按一下 hello （確定） 的核取記號按鈕 tooclose hello 資料行選取器 （在 hello 右下方)。

    ![啟動 hello 資料行選取器，並排除 hello"正常化損失 」 資料行][launch-column-selector]
    <br/>
    ***啟動 hello 資料行選取器，並排除 hello"正常化損失 」 資料行***

    現在 hello 屬性 窗格**資料集中選取的資料行**指出它將會傳遞通過所有資料行除了 hello 集中**正常化損失**。

    ![hello 屬性 窗格會顯示已排除該 hello"正常化損失 」 資料行][showing-excluded-column]
    <br/>
    ***hello 屬性 窗格會顯示已排除該 hello"正常化損失 」 資料行***

    > [!TIP]
    您可以新增註解 tooa 模組按兩下 hello 模組和輸入的文字。 這可協助您快速地查看哪些 hello 模組負責在您實驗中。 在此情況下按兩下 hello[資料集中選取的資料行][ select-columns]模組和類型 hello 註解 」"排除正常化損失。
    >
    >


    ![按兩下模組 tooadd 註解][add-comment]
    <br/>
    ***按兩下模組 tooadd 註解***

3. 拖曳 hello[清除遺漏資料][ clean-missing-data]模組 toohello 實驗畫布，並將它連接 toohello[資料集中選取的資料行][ select-columns]模組。 在 hello**屬性**窗格中，選取**移除整個資料列**下**清潔模式**。 這樣便會指引[清除遺漏資料][ clean-missing-data] tooclean hello 資料，藉由移除有任何遺漏值的資料列。 按兩下 hello 模組，然後輸入 hello 註解 [移除遺漏的值資料列]。

    ![設定 hello 清理模式太 」 移除整個資料列"hello"清除遺漏資料 」 模組][set-remove-entire-row]
    <br/>
    ***設定 hello 清理模式太 」 移除整個資料列"hello"清除遺漏資料 」 模組***

4. 按一下以執行 hello 實驗**執行**hello hello 頁底端。

    當 hello 實驗完成執行時，所有 hello 模組都有綠色核取記號 tooindicate 它們順利完成。 請注意也 hello**完成的執行**hello 右上角中的狀態。

![在執行 hello 實驗看起來應該像這樣][early-experiment-run]
<br/>
***在執行 hello 實驗看起來應該像這樣***

> [!TIP]
> 為什麼沒有我們 hello 實驗立即執行？ 所執行的 hello 實驗 hello 我們資料的資料行定義傳遞 hello 資料集，透過 hello[資料集中選取的資料行][ select-columns]模組，以及透過 hello[清除遺漏資料][ clean-missing-data]模組。 這表示我們太連接任何模組[清除遺漏資料][ clean-missing-data]也會有此相同資訊。

我們已完成設定 toothis 點 hello 實驗中所有是全新的 hello 資料。 如果您想 tooview hello 清除資料集時，按一下左 hello 輸出連接埠的 hello[清除遺漏資料][ clean-missing-data]模組，然後選取**視覺化**。 請注意該 hello**正常化損失**資料行已不再包含在內，，有沒有遺漏值。

現在 hello 資料是乾淨的我們已準備好 toospecify 功能我們要 toouse hello 預測模型中的。

## <a name="step-3-define-features"></a>步驟 3：定義功能

在機器學習中， *功能* 是您感興趣的某項目的個別可測量的屬性。 在我們的資料集中，每個資料列都代表一部汽車，而每個資料行是該汽車的功能。

您想 toosolve 尋找一組良好的功能來建立預測模型需要的試驗與 hello 問題的相關知識。 某些功能可更好預測比其他 hello 目標。 此外，某些功能與其他功能具有強相關性，而且可以移除。 例如，城市 mpg 和高速公路 mpg 密切相關因此我們可以保留其中一個，而不會大幅影響 hello 預測移除其他 hello。

我們來建置在我們的資料集使用 hello 功能子集的模型。 您可以於稍後回顧並選取不同的功能、 hello 實驗再次執行，並檢查是否可以取得更好的結果。 但 toostart，讓我們來試試 hello 下列功能：

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. 拖曳其他[資料集中選取的資料行][ select-columns]模組 toohello 實驗畫布。 連接保留 hello 輸出連接埠的 hello[清除遺漏資料][ clean-missing-data]模組 toohello 輸入的 hello[資料集中選取的資料行][ select-columns]模組。

    ![連接 hello 」 選取資料行中資料集 」 模組 toohello 」 清除遺漏資料 」 模組][connect-clean-to-select]
    <br/>
    ***連接 hello 」 選取資料行中資料集 」 模組 toohello 」 清除遺漏資料 」 模組***

2. 按兩下 hello 模組，然後輸入 [預測的選取功能。]

2. 按一下**啟動資料行選取器**在 hello**屬性**窗格。

3. 按一下 [套用規則] 。

4. 在 [開始於] 下，按一下 [無資料行]。 在 hello 篩選資料列，選取**Include**和**資料行名稱**hello 文字方塊中選取的資料行名稱清單。 除了 hello 我們在此指定的這會指示 hello 模組 toonot （功能） 的任何資料行傳遞。

5. 按一下 [hello] 核取記號 （確定） 按鈕。

    ![選取 hello （功能） 的資料行 tooinclude hello 預測中][select-columns-to-include]
    <br/>
    ***選取 hello （功能） 的資料行 tooinclude hello 預測中***

這會產生已篩選的資料集，其中包含我們想要學習的演算法 hello 下一個步驟中，我們將使用 toopass toohello hello 功能。 稍後您可以返回，並選取不同的功能重新嘗試。

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a>步驟 4：選擇及套用學習演算法

既然 hello 資料已就緒，建構預測的模型包含的定型和測試。 我們將使用我們資料 tootrain hello 的模型，並接著我們將測試 hello 模型 toosee 就能 toopredict 價格的程度。
<!-- For now, don't worry about *why* we need tootrain and then test a model.-->

*分類*和*迴歸*是兩種受監督的機器學習服務演算法。 「分類」可從一組已定義的類別預測答案，例如色彩 (紅色、藍色或綠色)。 迴歸是使用的 toopredict 數字。

因為我們想要 toopredict 價格是數字，我們會使用迴歸演算法。 在此範例中，我們將使用簡單*線性迴歸*模型。

> [!TIP]
> 如果您想要深入了解不同類型的機器學習演算法 toolearn toouse 它們，您可能會在 hello 資料科學初學者數列檢視 hello 第一個視訊[hello 五個問題的資料科學答案](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md)。 您也可以查看 hello 資訊圖[機器學習演算法範例的基本概念](machine-learning-basics-infographic-with-algorithm-examples.md)，或簽出 hello[機器學習演算法小祕技](machine-learning-algorithm-cheat-sheet.md)。

我們來定型 hello 模型提供一組包含 hello 價格的資料。 hello 模型掃描 hello 資料和外觀汽車的功能和其價格之間的關聯性。 然後，我們將測試 hello 模型-我們將提供我們很熟悉的汽車的一組功能，請參閱如何關閉 hello 模型就 toopredicting hello 已知的價格。

Hello 模型的定型和測試時將 hello 資料分割成個別的定型集和測試資料集，我們會使用我們的資料。

1. 選取並拖曳 hello[分割資料][ split]模組 toohello 實驗畫布並將它連接 toohello 上次[資料集中選取的資料行][ select-columns]模組。

2. 按一下 hello[分割資料][ split]模組 tooselect 它。 尋找 hello **hello 中的資料列的分數，第一次輸出資料集**(在 hello**屬性**hello 畫布的右窗格 toohello) 並將它設定 too0.75。 如此一來，我們將使用 75%的 hello 資料 tootrain hello 模型中，按住不放回 25%的測試 （更新版本中，您可以嘗試使用不同的百分比）。

    ![分割分數的 hello 「 分割資料 」 模組 too0.75 組 hello][set-split-data-percentage]
    <br/>
    ***分割分數的 hello 「 分割資料 」 模組 too0.75 組 hello***

    > [!TIP]
    > 藉由變更 hello**隨機種子**參數，您可以產生不同的隨機取樣，用於定型和測試。 此參數控制 hello 植入 hello 虛擬亂數產生器。

2. 執行 hello 實驗。 Hello 實驗執行時，hello[資料集中選取的資料行][ select-columns]和[分割資料][ split]模組傳遞的資料行定義 toohello接下來我們將持續加入的模組。  

3. 學習演算法，tooselect hello 展開 hello**機器學習**hello 模組調色盤 toohello 靠左 類別目錄的 hello 畫布，，然後展開**初始化模型**。 這會顯示數種類別可以使用的 tooinitialize 機器學習演算法的模組。 此實驗中，選取 hello[線性迴歸][ linear-regression]模組下 hello**迴歸**類別，並將它拖曳 toohello 實驗畫布。
（您也可以尋找 hello 模組 hello 調色盤搜尋方塊中輸入 「 線性迴歸 」。）

4. 尋找並拖曳 hello[定型模型][ train-model]模組 toohello 實驗畫布。 Hello hello 輸出連接[線性迴歸][ linear-regression]模組 toohello 左輸入的 hello[定型模型][ train-model]模組，並連接 hello定型資料 （由左連接埠） 的輸出 hello[分割資料][ split]模組 toohello 右邊輸入 hello[定型模型][ train-model]模組。

    ![連接 hello 「 定型模型 」 模組 tooboth hello 「 線性迴歸 」 和 「 分割資料 」 模組][connect-train-model]
    <br/>
    ***連接 hello 「 定型模型 」 模組 tooboth hello 「 線性迴歸 」 和 「 分割資料 」 模組***

5. 按一下 hello[定型模型][ train-model]模組中，按一下 [**啟動資料行選取器**在 hello**屬性**窗格中，然後再選取 hello **價格**資料行。 這是我們的模型會持續 toopredict hello 值。

    您選取 hello**價格**移動從 hello hello 資料行選取器中的資料行**可用的資料行**清單 toohello**選取的資料行**清單。

    ![選取 hello 「 定型模型 」 模組的 hello 價格資料行][select-price-column]
    <br/>
    ***選取 hello 「 定型模型 」 模組的 hello 價格資料行***

6. 執行 hello 實驗。

我們現在有可能是使用的 tooscore 新汽車資料 toomake 價格預測定型的迴歸模型。

![開始執行之後，hello 實驗現在看起來應該類似下面的][second-experiment-run]
<br/>
***開始執行之後，hello 實驗現在看起來應該類似下面的***

## <a name="step-5-predict-new-automobile-prices"></a>步驟 5：預測新的汽車價格

既然我們已經定型 hello 模型使用 75%的資料，我們可以使用 tooscore hello 其他的百分之 25 hello 資料 toosee 程度我們模型函式。

1. 尋找並拖曳 hello[計分模型][ score-model]模組 toohello 實驗畫布。 Hello hello 輸出連接[定型模型][ train-model]左輸入的連接埠的模組 toohello[計分模型][score-model]。 連接 hello 測試資料 （右連接埠） 的輸出 hello[分割資料][ split]模組 toohello 右輸入的連接埠[計分模型][score-model]。

    ![連接 hello 「 計分模型 」 模組 tooboth hello 「 定型模型 」 和 「 分割資料 」 模組][connect-score-model]
    <br/>
    ***連接 hello 「 計分模型 」 模組 tooboth hello 「 定型模型 」 和 「 分割資料 」 模組***

2. 執行 hello 實驗，並檢視 hello hello 輸出[計分模型][ score-model]模組 (按一下 hello 輸出連接埠[計分模型][ score-model]選取**視覺化**)。 hello 輸出顯示 hello 價格的預測的值，和 hello hello 測試資料的已知的值。  

    ![Hello 「 計分模型 」 模組的輸出][score-model-output]
    <br/>
    ***Hello 「 計分模型 」 模組的輸出***

3. 最後，我們測試 hello hello 結果的品質。 選取並拖曳 hello[評估模型][ evaluate-model]模組 toohello 實驗畫布與 hello hello 輸出連接[計分模型][ score-model]剩餘的輸入模組 toohello[評估模型][evaluate-model]。

    > [!TIP]
    > 有兩個輸入連接埠上 hello[評估模型][ evaluate-model]模組因為它可以是使用的 toocompare 兩個模型並存。 稍後，您可以加入另一個演算法 toohello 實驗，並使用[評估模型][ evaluate-model] toosee 哪一項提供更好的結果。

4. 執行 hello 實驗。

hello tooview hello 輸出[評估模型][ evaluate-model]模組中，按一下 hello 輸出連接埠]，然後選取**視覺化**。

![Hello 實驗的評估結果][evaluation-results]
<br/>
***Hello 實驗的評估結果***

hello 下列統計資料會顯示為我們的模型：

- **平均絕對誤差**(MAE): hello 的絕對錯誤平均值 (*錯誤*hello 差異 hello 預測值和 hello 實際值)。
- **根平均平方誤差**(RMSE): hello 的平方根 hello 平均平方錯誤 hello 測試資料集上所做的預測。
- **相對的絕對誤差**: hello 的絕對錯誤相對 toohello 絕對實際值與平均之間差異 hello 所有的實際值的平均值。
- **相對平方誤差**: hello 平均平方的錯誤相對 toohello 平方 hello 實際值與所有的實際值的平均值，hello 之間的差異。
- **判斷的係數**： 也稱為 hello **R 平方值**，這是統計度量，表示模型適合 hello 資料的程度。

Hello 錯誤的每個統計資料，較小，則更好。 較小的值會指出 hello 預測會更緊密符合 hello 實際值。 如**判斷的係數**，hello 接近其值是 tooone (1.0)，hello 較佳的 hello 預測。

## <a name="final-experiment"></a>最終實驗

hello 最終實驗看起來應該像這樣：

![hello 最終實驗][complete-linear-regression-experiment]
<br/>
***hello 最終實驗***

## <a name="next-steps"></a>後續步驟

既然您已經完成 hello 第一個機器學習教學課程，並以您的經驗設定，您可以繼續 tooimprove hello 模型，並再將其部署為在預測 web 服務。

- **逐一查看 tootry tooimprove hello 模型**-例如，您可以變更您預測中使用的 hello 功能。 您可以修改的 hello hello 屬性或者[線性迴歸][ linear-regression]演算法或完全嘗試不同的演算法。 您甚至可以加入多個機器學習演算法 tooyour 實驗一次並比較其中兩個使用 hello[評估模型][ evaluate-model]模組。
如需如何 toocompare 多個模型中單一實驗中，請參閱[比較迴歸輸入變數](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5)在 hello [Cortana 智慧組件庫](https://gallery.cortanaintelligence.com)。

    > [!TIP]
    > toocopy 您實驗中，使用 hello 任何反覆項目**SAVE AS**在 hello hello 頁面底部的按鈕。 您可以按一下來查看所有的 hello 反覆項目的實驗的**檢視執行記錄**hello hello 頁底端。 如需詳細資訊，請參閱[在 Azure Machine Learning Studio 中管理實驗逐一查看][runhistory]。

[runhistory]: machine-learning-manage-experiment-iterations.md

- **部署為預測的 web 服務的 hello 模型**-當您滿意您的模型，您可以將它部署為 web 服務 toobe 所使用新的資料使用 toopredict 汽車價格。 如需詳細資訊，請參閱[部署 Azure Machine Learning Web 服務][publish]。

[publish]: machine-learning-publish-a-machine-learning-web-service.md

想要更多的 toolearn 嗎？ 建立、 培訓、 計分，和部署模型 hello 程序的更廣泛且詳細逐步解說，請參閱[使用 Azure Machine Learning 開發預測解決方案][walkthrough]。

[walkthrough]: machine-learning-walkthrough-develop-predictive-solution.md

<!-- Images -->
[sign-in-to-studio]: ./media/machine-learning-create-experiment/sign-in-to-studio.png
[rename-experiment]: ./media/machine-learning-create-experiment/rename-experiment.png
[visualize-auto-data]:./media/machine-learning-create-experiment/visualize-auto-data.png
[select-visualize]: ./media/machine-learning-create-experiment/select-visualize.png
[showing-excluded-column]:./media/machine-learning-create-experiment/showing-excluded-column.png
[set-remove-entire-row]:./media/machine-learning-create-experiment/set-remove-entire-row.png
[early-experiment-run]:./media/machine-learning-create-experiment/early-experiment-run.png
[select-columns-to-include]:./media/machine-learning-create-experiment/select-columns-to-include.png
[second-experiment-run]:./media/machine-learning-create-experiment/second-experiment-run.png
[connect-score-model]:./media/machine-learning-create-experiment/connect-score-model.png
[evaluation-results]:./media/machine-learning-create-experiment/evaluation-results.png
[complete-linear-regression-experiment]:./media/machine-learning-create-experiment/complete-linear-regression-experiment.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[connect-train-model]:./media/machine-learning-create-experiment/connect-train-model.png
[select-price-column]:./media/machine-learning-create-experiment/select-price-column.png

[score-model-output]:./media/machine-learning-create-experiment/score-model-output.png

<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
