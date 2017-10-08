---
title: "在資料科學 aaaFeature 工程 |Microsoft 文件"
description: "說明 hello 特徵設計的用途，並提供其角色在機器學習的 hello 資料增強功能程序中的範例。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 3fde69e8-5e7b-49ad-b3fb-ab8ef6503a4d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: zhangya;bradsev
ms.openlocfilehash: af40ea9cc9395bc87fe695eeaef26aa71e0ec9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="feature-engineering-in-data-science"></a>資料科學特徵工程設計
本主題說明 hello 特徵設計的用途，並提供其角色在機器學習的 hello 資料增強功能程序中的範例。 使用此程序會從 Azure Machine Learning Studio 繪製的 tooillustrate hello 範例。 

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

這**功能表**連結 tootopics 描述 toocreate 各種環境中的資料的功能。 這項工作是在 hello 步驟[小組資料科學程序 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)。

功能工程嘗試 tooincrease hello 預測檢定力的學習演算法，建立從原始資料，可協助進行 hello 學習程序的功能。 hello 工程和選取的功能是一個一部分 hello TDSP 述 hello [hello 小組資料科學程序生命週期是什麼？](data-science-process-overview.md) 功能工程及選取項目是部分 hello**開發功能**hello TDSP 的步驟。 

* **功能工程**： 這個處理序嘗試 toocreate 其他相關的功能從 hello 現有未經處理的功能在 hello 資料和 tooincrease hello hello 學習演算法的預測能力。
* **特徵選取**： 此程序中 hello 訓練問題嘗試 tooreduce hello 維度性選取 hello 索引鍵子集的原始資料的功能。

通常**功能工程**套用第一個 toogenerate 額外的功能，然後在 hello**特徵選取**步驟是執行的 tooeliminate 無關、 備援性，或高度相關功能。

擷取從 hello 未經處理資料收集功能通常可增進 hello 定型資料，在機器學習中使用。 學習如何 tooclassify hello 映像的手寫字元，就建立從 hello 未經處理的位元發佈資料所建構的位元密度地圖的 hello 內容的工程功能的範例。 這個對應可協助找出 hello 邊緣 hello 字元比只直接使用 hello 原始發佈更有效率。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="creating-features-from-your-data---feature-engineering"></a>從您的資料建立特性 - 特性工程設計
hello 定型資料包含的範例 （記錄或儲存在資料列的觀察值） 所組成的矩陣，每一個都有一組功能 （變數或資料行中儲存的欄位）。 預期的 toocharacterize hello 模式 hello 資料中會收到 hello hello 實驗設計中指定的功能。 雖然許多 hello 未經處理資料欄位包含可以直接在 hello 選取的功能集使用 tootrain 模型時，它通常是 toobe 建構自 hello hello 未經處理資料 toogenerate 增強功能不需要額外的 （工程） 功能的 hello 案例定型資料集。

定型模型時，何種功能應建立 tooenhance hello 資料集？ 增強 hello 訓練的工程的功能提供更好的差異 hello hello 資料模式的資訊。 我們預期 hello 新功能 tooprovide 額外的資訊不清楚地擷取或輕鬆地呈現 hello 原始的或現有的功能集。 但此程序是一種藝術。 健全且有建設性的決策通常需要一些網域.專業知識。

從 Azure Machine Learning 開始，時，最簡單的 toograsp hello Studio 中提供的具體使用範例的這個程序。 以下呈現兩個範例：

* 迴歸範例[hello 自行車出租數目的預測](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4)受監督的實驗稱為 hello 目標值
* 使用 [特性雜湊](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/)

## <a name="example-1-adding-temporal-features-for-regression-model"></a>範例 1：新增迴歸模型的暫時特性
讓我們使用 hello 實驗 」 需求預測自行車的 「 Azure Machine Learning Studio toodemonstrate tooengineer 功能如何在迴歸工作。 此實驗 hello 目標是 toopredict hello hello bikes，也就是 hello 自行車出租數目特定的月/日/一小時內的要求。 hello 資料集"Bike 以租用方式佔用 UCI 資料集 」 作為 hello 未經處理的輸入資料。 此資料集根據從 hello 資本 Bikeshare 公司維護在 hello 美國華盛頓特區的自行車以租用方式佔用網路的實際資料。 hello 資料集代表 hello 自行車出租數目 hello 2011 年和 2012 年中的一天的某個特定時間內，而且包含 17379 資料列和 17 的資料行。 hello 未經處理的功能集包含天氣 （溫度/溼度/風速） 和 hello 類型 hello 天 （假日/週間日）。 hello 欄位 toopredict 是"cnt"，表示特定的一小時內 hello 自行車出租和其範圍從 1 too977 範圍的計數。

建構有效的功能，hello 定型資料中的 hello 目標，四個迴歸模型會使用建立 hello 相同的演算法，但四個不同的訓練資料集。 hello 四個資料集代表 hello 相同原始的輸入的資料，但有越來越多的功能設定。 這些特性可分為四類：

1. A = 天氣 + 假日 + 週間日 + 週末功能 hello 預測一天
2. B = bikes，先前的 12 小時內每個 hello 已出租數目
3. C = 已出租 hello 的每個先前的 12 天 hello 在相同的自行車的小時
4. D = 已出租 hello 的每個先前的 12 週，在 hello 相同的自行車的小時和 hello 同一天

功能集 A 存在於 hello 原始未經處理資料，除了 hello 功能其他三組透過建立 hello 工程程序的功能。 功能設定 B 擷取最新的 hello 自行車需求。 功能設定的特定小時 C 擷取的自行車 hello 需求。 功能設定的自行車 D 擷取要求在特定小時與 hello 一週的特定天數。 hello 四個定型資料集每個包含功能 set A、 A + B、 A + B + C 和 A + B + C + D、 分別。

Hello Azure 機器學習實驗中，在這些四個定型資料集的格式透過 hello 預先處理輸入資料集的四個分支。 除了 hello 左大部分的分支，每個分支包含[執行 R 指令碼](https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/)模組中的一組衍生 （功能集 B、 C 以及 D） 的功能是分別建構和附加 toohello 匯入資料集。 下列圖 hello 示範 hello R 指令碼會使用 toocreate 功能集 B hello 第二個左分支中。

![建立特性](./media/machine-learning-data-science-create-features/addFeature-Rscripts.png)

hello hello 效能結果的 hello hello 下表中摘要說明四種模型的比較。 hello 獲得最佳結果會顯示功能 A + B + C。 請注意，hello 錯誤速率降低 hello 定型資料中包含額外的功能集。 它會確認我們假設，hello 功能集 B，C 提供 hello 迴歸工作的其他相關資訊的結果。 但是加入 hello D 功能似乎不 tooprovide 其他致使 hello 錯誤率。

![結果比較](./media/machine-learning-data-science-create-features/result1.png)

## <a name="example2"></a> 範例 2：在文字採礦中建立特性
在工作的相關 tootext 採礦，例如文件分類和情緒分析廣泛套用特徵設計。 比方說，當我們想 tooclassify 文件分成數個類別，一般假設是 hello 字/片語包含在一個文件類別目錄會比較不可能 toooccur 另一個文件類別目錄中。 換句話說，hello hello 文字/片語發佈頻率是無法 toocharacterize 不同的文件類別。 在文字採礦應用程式，因為文字內容的各個部分通常做為輸入資料 hello，工程程序的 hello 功能會是需要的 toocreate hello 功能涉及 word/片語頻率。

tooachieve 這項工作，稱為技術**特徵雜湊**是套用的 tooefficiently 索引到任意文字功能。 而不是建立關聯，每個文字功能 （單字/片語） tooa 特定的索引，此方法的功能套用雜湊函式 toohello 功能，並為索引中直接使用其雜湊值。

Azure 機器學習中有一個 [特性雜湊](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) 模組，方便建立這些文字/片語特性。 下圖顯示使用此模組的範例。 hello 輸入資料集包含兩個資料行： hello 書籍評等範圍從 1 too5，和 hello 實際的檢閱內容。 這個 hello 目標[特徵雜湊](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/)模組是 tooretrieve 顯示 hello 出現頻率的 hello 對應關鍵字的新功能的一大堆 / 離開 hello 特定書籍檢閱中。 toouse 本單元中，我們需要 toocomplete hello 下列步驟：

* 首先，選取 包含 hello 輸入的文字的 hello 資料行 (在此範例中為"Col2")。
* 接下來，設定 hello 「 雜湊位元大小 」 too8 表示 2 ^8 = 256 功能將會建立。 hello word/階段中所有的 hello 文字將 too256 雜湊的索引。 hello 參數 「 雜湊位元大小 」 的範圍從 1 too31。 hello 文字 / 離開會比較不可能 toobe 雜湊成 hello 相同索引如果要設定其 toobe 更大的數目。
* 第三，設定 hello 參數 」 N 字母組"too2。 這會取得 hello 出現頻率單字母組 （每個單字的功能） 和雙字母組 （每個單字相鄰的配對的功能） 從 hello 輸入文字。 hello"N 字母組 」 範圍是從 0 too10，指出 hello 最大數目循序字 toobe 包含在一項功能。  

![「特性雜湊」模組](./media/machine-learning-data-science-create-features/feature-Hashing1.png)

hello 如下圖所示什麼 hello 這些新功能的樣子。

![「特性雜湊」範例](./media/machine-learning-data-science-create-features/feature-Hashing2.png)

## <a name="conclusion"></a>結論
工程與所選取的功能會提高 hello 效率 hello 培訓程序，從而試著 hello 資料中包含 tooextract hello 金鑰資訊。 它們也改善 hello 電源，這些模型 tooclassify hello 輸入資料的精確和 toopredict 結果感興趣多穩當地。 特徵設計和選取範圍也可以結合 toomake hello 學習更多計算容易處理。 它是藉由增強，則減少 hello 一些功能需要 toocalibrate 」 或 「 定型模型。 Hello 功能選取的 tootrain hello 模型數學上來說，是最基本的獨立變數說明 hello 資料中的 hello 模式，然後預測結果成功。

請注意，它不一定一定 tooperform 工程或功能特徵。 是否需要與否，取決於 hello 資料我們或者收集，我們挑選，hello 演算法，然後再 hello hello 實驗的目標。

