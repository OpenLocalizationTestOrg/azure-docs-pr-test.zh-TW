---
title: "aaaFeature 工程和 Azure Machine Learning 中的選取範圍 |Microsoft 文件"
description: "說明 hello 特徵選取和特徵設計目的，並提供在機器學習 hello 加強資料程序中的角色的範例。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ceb524d-842e-4f77-9eae-a18e599442d6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2017
ms.author: zhangya;bradsev
ROBOTS: NOINDEX
redirect_url: machine-learning-data-science-create-features
redirect_document_id: True
ms.openlocfilehash: e3e59329bf46f334396f5975b4e656137362d7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="feature-engineering-and-selection-in-azure-machine-learning"></a>Azure 機器學習中的特性工程設計和選取
本主題說明功能工程與 hello 加強資料程序中，特徵選取的機器學習的 hello 目的。 其使用 Azure Machine Learning Studio 提供的範例來解釋這些程序的相關事項。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

在機器學習中使用的 hello 定型資料可以通常增強 hello 選取範圍或擷取從 hello 未經處理資料收集功能。 學習如何 tooclassify hello 映像的手寫字元的 hello 內容的工程功能的範例元密度對應從 hello 未經處理的位元發佈資料所建構。 這個對應可協助找出 hello 邊緣 hello 字元比 hello 原始發佈更有效率。

工程與所選取的功能會提高 hello 效率 hello 定型程序，從而試著 hello 資料中包含 tooextract hello 金鑰資訊。 它們也改善 hello 電源，這些模型 tooclassify hello 輸入資料的精確和 toopredict 結果感興趣多穩當地。 特徵設計和選取範圍也可以結合 toomake hello 學習更多計算容易處理。 它是藉由增強，則減少 hello 一些功能需要 toocalibrate 」 或 「 定型模型。 Hello 功能選取的 tootrain hello 模型數學上來說，是最基本的獨立變數說明 hello 資料中的 hello 模式，然後預測結果成功。

hello 工程團隊以及的功能為一個較大的處理序，通常包含四個步驟：

* 資料收集
* 資料增強
* 模型建構
* 後處理

工程及選取項目組成的機器學習 hello 資料增強功能的步驟。 此程序的三個層面主要有四個目的：

* **資料前置處理**： 此程序會嘗試 tooensure hello 收集的資料，是全新且一致。 其中包含下列工作：例如整合多個資料集、處理不一致的資料，以及轉換資料類型。
* **功能工程**： 這個處理序嘗試 toocreate 其他相關的功能從 hello 現有未經處理的功能在 hello 資料和 tooincrease 預測檢定力 toohello 學習演算法。
* **特徵選取**： 此程序選取 hello 的原始資料功能 tooreduce hello 維度性 hello 訓練問題的索引鍵子集。

本主題只涵蓋 hello 功能工程及功能選取項目層面 hello 資料增強功能的程序。 如需有關 hello 資料前置處理步驟的詳細資訊，請參閱[前置處理 Azure Machine Learning Studio 中的資料](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/)。

## <a name="creating-features-from-your-data--feature-engineering"></a>從您的資料建立特性 - 特性工程設計
hello 定型資料包含的範例 （記錄或儲存在資料列的觀察值） 所組成的矩陣，每一個都有一組功能 （變數或資料行中儲存的欄位）。 預期的 toocharacterize hello 模式 hello 資料中會收到 hello hello 實驗設計中指定的功能。 雖然許多 hello 未經處理資料欄位包含可以直接在 hello 選取的功能集使用 tootrain 模型時，其他的工程的功能通常會需要 toobe hello 功能 hello 未經處理資料 toogenerate 增強的定型資料集從建構。

定型模型時，何種功能應該建立 tooenhance hello 資料集？ 增強 hello 訓練的工程的功能提供更好的差異 hello hello 資料模式的資訊。 您預期 hello 新功能 tooprovide 額外的資訊不清楚地擷取或原始 hello 輕鬆地呈現或現有的功能設定，但是此程序是一項藝術。 健全且有建設性的決策通常需要一些網域.專業知識。

從 Azure Machine Learning 開始，時，最簡單的 toograsp Machine Learning Studio 中提供具體的使用範例的這個程序。 以下呈現兩個範例：

* 迴歸範例 ([hello 自行車出租數目的預測](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4)) 在受監督的實驗稱為 hello 目標值
* 使用[特性雜湊][feature-hashing]的文字採礦分類範例

### <a name="example-1-adding-temporal-features-for-a-regression-model"></a>範例 1：新增迴歸模型的暫時特性
toodemonstrate 如何 tooengineer 功能的迴歸工作，讓我們使用 hello 實驗 」 需求預測自行車的 「 Azure Machine Learning Studio 中。 此實驗 hello 目標是 toopredict hello hello bikes，也就是 hello 自行車出租數目特定月、 日或小時內的要求。 hello 資料集**自行車以租用方式佔用 UCI 資料集**做 hello 未經處理的輸入資料。

此資料集根據從 hello 資本 Bikeshare 公司維護在 hello 美國華盛頓特區的自行車以租用方式佔用網路的實際資料。 hello 資料集代表，一天的某個特定時間內從 2011 too2012 hello 自行車出租數目，而且包含 17379 資料列和 17 的資料行。 hello 未經處理的功能集包含溫度、 溼度 （風速） 的天氣和 hello 類型 hello 天 （假日或工作日）。 hello 欄位 toopredict 是**cnt**，表示特定的一小時內 hello 自行車出租和，範圍從 1 too977 的計數。

tooconstruct 有效 hello 定型資料中的功能，使用 hello 建立四個迴歸模型相同的演算法，但包含四個不同的定型資料設定。 hello 四個資料集代表 hello 相同原始的輸入的資料，但有越來越多的功能設定。 這些特性可分為四類：

1. A = 天氣 + 假日 + 週間日 + 週末功能 hello 預測一天
2. B = bikes，先前的 12 小時內每個 hello 已出租數目
3. C = 已出租 hello 的每個先前的 12 天 hello 在相同的自行車的小時
4. D = 已出租 hello 的每個先前的 12 週，在 hello 相同的自行車的小時和 hello 同一天

功能集 A hello 原始未經處理資料中已存在，除了 hello 功能其他三組透過建立 hello 工程程序的功能。 設定 hello 的自行車的 B 擷取 hello 最近要求的功能。 功能設定的特定小時 C 擷取的自行車 hello 需求。 功能設定的自行車 D 擷取要求在特定小時與 hello 一週的特定天數。 每個 hello 四部訓練資料集包含的功能集 A、 A + B、 A + B + C 和 A + B + C + D、 分別。

在 hello Azure 機器學習實驗，這四個定型資料集格式透過 hello 預先處理輸入資料集的四個分支。 除了 hello 最左邊的分支，每個分支包含[執行 R 指令碼][ execute-r-script]分別建構及附加的模組中的一組衍生功能 （功能集 B、 C 以及 D）toohello 匯入資料集。 下列圖 hello 示範 hello R 指令碼會使用 toocreate 功能集 B hello 第二個左分支中。

![建立功能集](./media/machine-learning-feature-selection-and-engineering/addFeature-Rscripts.png)

hello 下表摘要說明 hello 比較 hello 效能結果的 hello 四種模型。 hello 獲得最佳結果會顯示功能 A + B + C。 請注意 hello 定型資料中包含額外的功能集，則會減少該 hello 錯誤率。 這可確認 hello B 和 C 提供 hello 迴歸工作的其他相關資訊的功能集我們假設結果。 加入 hello D 功能集似乎未 tooprovide 其他致使 hello 錯誤率。

![比較效能結果](./media/machine-learning-feature-selection-and-engineering/result1.png)

### <a name="example2"></a> 範例 2：在文字採礦中建立特性
在工作的相關 tootext 採礦，例如文件分類和情緒分析廣泛套用特徵設計。 比方說，當您想 tooclassify 文件分成數個類別，一般假設是 hello 單字或片語包含一份文件類別目錄中會比較不可能 toooccur 另一個文件類別目錄中。 換句話說，hello hello 單字或片語發佈頻率是無法 toocharacterize 不同的文件類別。 文字採礦應用程式，在 hello 功能工程程序會是需要的 toocreate hello 功能包含單字或片語的頻率，因為個別的文字內容片段通常做為 hello 輸入的資料。

tooachieve 這項工作，稱為技術*特徵雜湊*是套用的 tooefficiently 索引到任意文字功能。 而不是建立關聯，每個文字功能 （單字或片語） tooa 特定索引，此方法的功能藉由套用雜湊函式 toohello 功能，並為索引中直接使用其雜湊值。

Azure 機器學習中有一個[特性雜湊][feature-hashing]模組，會建立這些文字或片語特性。 hello 下圖顯示使用此模組的範例。 hello 輸入的資料集包含兩個資料行： hello 書籍評等範圍從 1 too5 和 hello 實際檢閱內容。 這個 hello 目標[特徵雜湊][ feature-hashing]模組是 tooretrieve 顯示 hello 出現頻率 hello 相對應的單字或片語 hello 特定書籍檢閱內的新功能。 toouse 這個模組，您需要下列步驟 toocomplete hello:

1. 包含 hello 輸入的文字的選取 hello 資料行 (**Col2**在此範例中)。
2. 設定*雜湊位元大小*too8，這表示 2 ^8 = 256 功能所建立。 hello 單字或片語中的 hello 文字就 too256 索引雜湊處理。 hello 參數*雜湊位元大小*範圍是從 1 too31。 如果 hello 參數設定 tooa 較大的數字，hello 單字或片語不太可能 toobe 雜湊成 hello 相同的索引。
3. 設定 hello 參數*N 字母組*too2。 這會從 hello 輸入文字擷取單字母組 （每個單字的功能） 和雙字母組 （每個單字相鄰的配對的功能） 的 hello 出現頻率。 hello 參數*N 字母組*範圍是從 0 too10，表示 hello 的循序字 toobe 功能中包含的最大數目。  

![特性雜湊模組](./media/machine-learning-feature-selection-and-engineering/feature-Hashing1.png)

hello 下圖顯示這些新功能的外觀。

![特性雜湊範例](./media/machine-learning-feature-selection-and-engineering/feature-Hashing2.png)

## <a name="filtering-features-from-your-data--feature-selection"></a>從您的資料篩選特性 - 特性選取
*特徵選取*是一般的程序套用 toohello 建構訓練資料集進行預測模型工作，例如分類或迴歸工作。 hello 目標是 tooselect hello hello 原始資料集，其維度減少 hello 資料中使用的最少的功能 toorepresent hello 最大數量的變異數的功能子集。 此功能子集包含 hello 唯一功能包含 toobe tootrain hello 模型。 特性選取有兩個主要目的：

* 特性選取通常會排除不相關、多餘或高度相關的特性，進而提高分類正確性。
* 功能選取項目會減少 hello 特徵數目，使得 hello 模型定型程序更有效率。 這是特別重要，是高度耗費資源 tootrain 支援向量機器之類的學習模組。

雖然特徵選取搜尋 tooreduce hello 數目 hello 資料集使用 tootrain hello 模型中的功能，但不是通常稱為 tooby hello 詞彙*維度縮減。* 特徵選取方法會擷取 hello 資料中的原始功能的子集，而不變更它們。  維度性降低方法採用工程的功能，可以轉換 hello 原始功能，並因此能加以修改。 維度縮減方法的範例包含主成分分析、典型相關分析和奇異值分解。

監督環境中有一個廣泛應用的特性選取方法類別為以篩選為基礎的特性選取。 藉由評估每一個功能和 hello 目標屬性之間的 hello 相互關聯，這些方法會套用統計量值 tooassign 分數 tooeach 功能。 hello 功能然後排序次序 hello 分數，您可以使用 tooset hello 臨界值或排除特定的功能。 使用這些方法中的 hello 統計量值的範例包括皮耳森相關、 相互資訊和 hello 卡方檢定。

Azure Machine Learning Studio 針對特性選取提供模組。 Hello 遵循圖所示，這些模組包括[篩選器為基礎的特徵選取][ filter-based-feature-selection]和[費雪線性判別分析][ fisher-linear-discriminant-analysis].

![特性選取範例](./media/machine-learning-feature-selection-and-engineering/feature-Selection.png)

例如，使用 hello[篩選器為基礎的特徵選取][ filter-based-feature-selection] hello 文字採礦範例先前所述的模組。 假設您想 toobuild 迴歸模型，建立一組 256 功能透過 hello 之後[特徵雜湊][ feature-hashing]模組，以及該 hello 回應變數是**Col1**表示活頁簿檢閱 [評等範圍從 1 too5。 設定**特徵計分法**太**皮耳森相關**，**目標資料行**太**Col1**，和**預期的數目功能**太**50**。 hello 模組[篩選器為基礎的特徵選取][ filter-based-feature-selection]然後產生資料集包含 50 的功能與 hello 目標屬性**Col1**。 hello 以下圖顯示這項實驗 hello 流程，並 hello 輸入的參數。

![特性選取範例](./media/machine-learning-feature-selection-and-engineering/feature-Selection1.png)

hello 下圖顯示 hello 產生資料集。 每項功能在 hello 皮耳森相關其本身之間 hello 計分根據目標屬性**Col1**。 具有高分的 hello 功能會保留。

![篩選器為基礎的特性選取資料集](./media/machine-learning-feature-selection-and-engineering/feature-Selection2.png)

下列圖顯示 hello hello hello 選取功能的相對應的分數。

![選取的特性分數](./media/machine-learning-feature-selection-and-engineering/feature-Selection3.png)

藉由套用這[篩選器為基礎的特徵選取][ filter-based-feature-selection]模組，50 超出 256，選取的功能，因為它們與 hello 目標變數的大部分功能相互關聯的 hello **Col1**根據計分方法的 hello**皮耳森相關**。

## <a name="conclusion"></a>結論
特徵設計與特徵選取是兩個步驟經常執行 tooprepare hello 定型資料，建立機器學習模型時。 一般而言，特徵設計會套用第一個 toogenerate 額外的功能，以及然後 hello 功能選取項目步驟是執行的 tooeliminate 無關、 備援性或在特徵高度相關。

它不一定一定 tooperform 工程或功能特徵。 是否需要取決於您擁有或收集您挑選，hello 演算法和 hello hello 實驗目標 hello 資料。

<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/
