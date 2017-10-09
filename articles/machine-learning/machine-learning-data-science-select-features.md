---
title: "aaaFeature hello 小組資料科學程序中的選取範圍 |Microsoft 文件"
description: "說明 hello 用途的特徵選取，並提供在機器學習的 hello 資料增強程序中的角色的範例。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 878541f5-1df8-4368-889a-ced6852aba47
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: zhangya;bradsev
ms.openlocfilehash: 54af93c83e4cc6a3670b3ad62490e0f74082b4ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="feature-selection-in-hello-team-data-science-process-tdsp"></a>Hello 小組資料科學程序 (TDSP) 中的特徵選取
本文說明 hello 用途的特徵選取，並提供其角色在機器學習的 hello 資料增強功能程序中的範例。 這些範例是根據 Azure Machine Learning Studio 繪製。 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

hello 工程和選取的功能是 hello 小組資料科學程序 (TDSP) 中所述的某一部分[hello 小組資料科學程序是什麼？](data-science-process-overview.md)。 功能工程及選取項目是部分 hello**開發功能**hello TDSP 的步驟。

* **功能工程**： 這個處理序嘗試 toocreate 其他相關的功能從 hello 現有未經處理的功能在 hello 資料和 tooincrease 預測檢定力 toohello 學習演算法。
* **特徵選取**： 此程序中 hello 訓練問題嘗試 tooreduce hello 維度性選取 hello 索引鍵子集的原始資料的功能。

通常**功能工程**套用第一個 toogenerate 額外的功能，然後在 hello**特徵選取**步驟是執行的 tooeliminate 無關、 備援性，或高度相關功能。

## <a name="filtering-features-from-your-data---feature-selection"></a>從您的資料篩選特性 - 特性選取
特徵選取是定型資料集的預測模型工作，例如分類或迴歸工作 hello 建構的通常會套用的處理序。 hello 目標是 tooselect hello 資料中使用的最少的功能 toorepresent hello 最大數量的變異數減少其維度的 hello 功能從 hello 原始資料集的子集。 這個子集的功能是，則唯一功能 toobe hello 包含 tootrain hello 模型。 特性選取有兩個主要目的。

* 第一，特性選取通常會排除不相關、多餘或高度相關的特性，進而提高分類正確性。
* 第二，也會降低 hello 數字的功能可讓模型定型程序更有效率。 這是特別重要，是高度耗費資源 tootrain 支援向量機器之類的學習模組。

雖然特徵選取，並搜尋 tooreduce hello 數目 hello 使用資料集 tootrain hello 模型中的功能，它通常不參考的 tooby hello 詞彙 「 縮減 」。 特徵選取方法會擷取 hello 資料中的原始功能的子集，而不變更它們。  維度性降低方法採用工程的功能，可以轉換 hello 原始功能，並因此能加以修改。 維度縮減方法的範例包含主成分分析、典型相關分析和奇異值分解。

監督環境中有一個廣泛應用的特性選取方法類別，稱之為「以篩選為基礎的特性選取」。 藉由評估每一個功能和 hello 目標屬性之間的 hello 相互關聯，這些方法會套用統計量值 tooassign 分數 tooeach 功能。 hello 功能，然後會 hello 分數，可能會使用的 toohelp hello 閾值或排除的特定功能的項目。 使用這些方法中的 hello 統計量值的範例包括人員相互關聯、 相互資訊和 hello 卡平方的測試。

Azure Machine Learning Studio 中有針對特性選取而提供的模組。 Hello 遵循圖所示，這些模組包括[篩選器為基礎的特徵選取][ filter-based-feature-selection]和[費雪線性判別分析][ fisher-linear-discriminant-analysis].

![特性選取範例](./media/machine-learning-data-science-select-features/feature-Selection.png)

請考慮，例如，使用 hello hello[篩選器為基礎的特徵選取][ filter-based-feature-selection]模組。 為了 hello 方便起見，我們將繼續 toouse hello 文字採礦範例以上所述。 假設我們想要透過 hello 建立迴歸模型之後的一組 256 功能 toobuild[特徵雜湊][ feature-hashing]模組，該 hello 回應變數 hello"Col1"且代表活頁簿檢閱 [評等範圍從 1 too5。 藉由設定 」 功能計分方法 」 toobe"皮耳森"，hello"的目標資料行 」 toobe"Col1"，」 和 「 hello 」 所需特徵數目 」 too50。 然後 hello 模組[篩選器為基礎的特徵選取][ filter-based-feature-selection]會產生包含 50 的功能與 hello 目標屬性"Col1"的資料集。 hello 以下圖顯示這項實驗 hello 流程，並 hello 我們剛剛所述的輸入的參數。

![特性選取範例](./media/machine-learning-data-science-select-features/feature-Selection1.png)

hello 下圖顯示 hello 產生資料集。 每個功能計分根據 hello 皮耳森相關之間本身上和 hello "Col1"的目標屬性。 具有高分的 hello 功能會保留。

![特性選取範例](./media/machine-learning-data-science-select-features/feature-Selection2.png)

hello 遵循圖會顯示 hello 對應分數的 hello 選取功能。

![特性選取範例](./media/machine-learning-data-science-select-features/feature-Selection3.png)

藉由套用這[篩選器為基礎的特徵選取][ filter-based-feature-selection]模組，50 超出 256，它們有 hello 最多的相互關聯的功能與 hello 目標變數"Col1"，因為選取的功能，會根據 hello 計分方法"皮耳森"。

## <a name="conclusion"></a>結論
特徵設計和特徵選取是 hello 的兩個通常工程和選取的功能會提高定型程序，從而試著 tooextract hello 金鑰資訊 hello 資料中包含 hello 效率。 它們也改善 hello 電源，這些模型 tooclassify hello 輸入資料的精確和 toopredict 結果感興趣多穩當地。 特徵設計和選取範圍也可以結合 toomake hello 學習更多計算容易處理。 它是藉由增強，則減少 hello 一些功能需要 toocalibrate 」 或 「 定型模型。 Hello 功能選取的 tootrain hello 模型數學上來說，是最基本的獨立變數說明 hello 資料中的 hello 模式，然後預測結果成功。

請注意，它不一定一定 tooperform 工程或功能特徵。 是否需要與否，取決於 hello 資料我們或者收集，我們挑選，hello 演算法，然後再 hello hello 實驗的目標。

<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/

