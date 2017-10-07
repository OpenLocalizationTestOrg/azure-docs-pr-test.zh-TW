---
title: "學習演算法小祕技 aaaMachine |Microsoft 文件"
description: "可列印的機器學習演算法小祕技可協助您在 Azure Machine Learning Studio 中選擇 hello 正確預測模型的演算法。"
keywords: "演算法小祕技,小祕技,機器學習演算法"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e1dc31ec-1acb-463f-ba77-de565d4ddf4d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: garye
ms.openlocfilehash: 2bedd77bfc65128a90c6128743016415dd8609d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-algorithm-cheat-sheet-for-microsoft-azure-machine-learning-studio"></a>適用於 Microsoft Azure Machine Learning Studio 的機器學習演算法小祕技
hello **Microsoft Azure 機器學習演算法小工作表**可協助您選擇 hello 正確的預測分析模型的演算法。

[Azure Machine Learning Studio](https://studio.azureml.net/)具有大型的程式庫的演算法從 hello***迴歸***，***分類***，***叢集***，和***異常偵測***系列。 每一個都是設計的 tooaddress 不同類型的機器學習問題。

## <a name="download-machine-learning-algorithm-cheat-sheet"></a>下載：機器學習服務演算法小祕技
**下載 hello 小祕技這裡：[機器學習演算法小工作表 (11 x 17 英)](http://download.microsoft.com/download/A/6/1/A613E11E-8F9C-424A-B99D-65344785C288/microsoft-machine-learning-algorithm-cheat-sheet-v6.pdf)**

![機器學習演算法祕技： 了解如何 toochoose 的機器學習演算法。][cheat-sheet]

[cheat-sheet]: ./media/machine-learning-algorithm-cheat-sheet/machine-learning-algorithm-cheat-sheet-small_v_0_6-01.png

下載並列印 hello 機器學習演算法小工作表中 tabloid 大小 tookeep 方便它並選擇演算法取得說明。

> [!NOTE]
> 請參閱 hello 文章[如何 toochoose 演算法為 Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md)的詳細的指引 toousing 這個小祕技。
> 
> 

## <a name="more-help-with-algorithms"></a>更多演算法的詳細說明
* 在使用這個小祕技選擇 hello 正確的演算法，加上 hello 不同類型的機器學習演算法和使用方式的深入討論的說明，請參閱[如何為 Microsoft Azure 機器學習toochoose演算法](machine-learning-algorithm-choice.md).
* 如需描述演算法並提供範例的可下載資訊圖詳細資訊，請參閱[可下載的資訊圖：機器學習服務基本概念和演算法範例](machine-learning-basics-infographic-with-algorithm-examples.md)。
* 如需依類別目錄的所有 hello 機器學習演算法 Machine Learning Studio 中可用的清單，請參閱[初始化模型][ initialize-model] hello 機器學習 Studio 演算法和模組說明。
* 如需 Machine Learning Studio 中按字母順序排列的完整演算法和模組清單，請參閱＜Machine Learning Studio 演算法和模組說明＞中的 [Machine Learning Studio 模組的 A-Z 清單][a-z-list]。
* toodownload 及列印的圖表，hello Machine Learning Studio 中，功能的概觀，請參閱[Azure Machine Learning Studio 功能的概觀圖表](machine-learning-studio-overview-diagram.md)。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="notes-and-terminology-definitions-for-hello-machine-learning-algorithm-cheat-sheet"></a>附註和 hello 機器學習演算法的詞彙定義速查表

* 此演算法小祕技中提供的 hello 建議會的 thumb 近似規則集。 您可以屈從有些建議，也可以公然違反有些建議。 這是預期的 toosuggest 的起始點。 不是恐怕 toorun 對資料的數種演算法之間為一對一競爭。 是只是了解每個演算法的 hello 原則及了解您的資料產生的 hello 系統沒有替代。

* 每個機器學習服務演算法都有自己的風格或*歸納偏差*。 對於特定問題，適合的演算法可能有數個，但其中一個演算法可能會比其他演算法更適合。 但它不一定可能 tooknow 事先即 hello 最適大小。 在這些情況下，有數種演算法會列在一起在 hello 小祕技。 適當的策略會 tootry 一種演算法，，如果 hello 結果尚不令人滿意，請嘗試其他 hello。 以下是從 hello 範例[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com/)的實驗，並試著 hello 針對數種演算法相同的資料和比較 hello 結果：[比較多級分類器： 字母辨識](http://gallery.cortanaintelligence.com/Details/a635502fc98b402a890efe21cec65b92).

* 機器學習有三個主要類別：**經過指導的學習**、**未經指導的學習**和**增強式學習**。

  * 在**經過指導的學習**中，每個資料點都會加上標籤或與感興趣的類別或值產生關聯。  分類標籤的範例就是將影像指派為「貓」或「狗」。  值標籤的範例是使用汽車相關聯的 hello 銷售價格。 hello 監督式學習的目的是 toostudy 許多標示為範例，然後再 toobe 無法 toomake 預測未來的資料點。 例如，以正確使用汽車的代表動物或指派正確的銷售價格 tooother hello 識別新相片。 這是常見且實用的機器學習服務類型。 所有在 Azure 機器學習的 hello 模組監督式學習演算法，除了[K-means 群集][k-means-clustering]。

  * 在**未監督的學習**中，資料點沒有與其相關聯的標籤。 相反地，hello 不受監督的學習演算法的目標是 tooorganize hello 資料，在某些方式或 toodescribe 其結構。 這可能表示將資料劃分為叢集 (如 K-Means 所為)，或尋找各種查看複雜資料的方式，使其變得更簡單。

  * 在**增援學習**，hello 演算法取得 toochoose 動作以回應 tooeach 資料點。 它是常見的方法中，其中 hello 時間在一處的感應器讀數組是資料點，而 hello 演算法必須選擇 hello 機器人的下一個動作。 它也很適合用於物聯網 (Internet of Things) 應用程式。 hello 學習演算法也會收到一小段時間之後，指出妥當 hello 決策是報酬訊號。 根據這個 hello 演算法修改其策略中順序 tooachieve hello 最高的報酬。 Azure ML 中目前沒有增強式學習演算法模組。

* **貝氏方法**進行 hello 假設統計無關的資料點。 Hello 不支援模型中一個資料點的變化性這表示它與其他人，也就是無法預測。 比方說，如果正在錄製的 hello 資料 hello 數分鐘，直到下一步捷運定型 hello 抵達時，兩個分開進行每日的測量是統計上獨立的。 不過，兩個度量單位一分鐘，不過不是統計上獨立-hello 值的其中一個高 hello hello 其他值的預測。

* **促進式決策樹迴歸**會利用特徵重疊或特徵間的互動。 表示，在任何給定的資料點，hello 的其中一項功能的值為 hello 值的另一個有點預測。 例如，在 [每日高/低溫度資料知道 hello 低溫度 hello 一天可讓您 toomake 合理猜測在 hello 高。 hello hello 兩個功能中所包含的資訊是多餘的。

* 使用原本就是多類別的分類器，或將一組雙類別的分類器合併成一個**整體** (Ensemble)，即可將資料分類成兩個以上的類別。 在 hello 集團方法中，沒有個別的二級分類器，為每個類別-每個資料加以區分 hello 分成兩個類別: 「 此類別 」 且 「 不此類別。" 然後 hello 正確 hello 資料點指派投票決定這些分類器。 這是背後的 hello 操作原則[其中一個 vs 全部多級][one-vs-all-multiclass]。

* 數個方法，包括羅吉斯迴歸和 hello 貝氏點機器，會假設**線性界限**。 也就是說，它們會假設該 hello 類別之間的界限是大約直線 （或在 hyperplanes hello 更常見的案例）。 通常這是特性 hello 後您嘗試過 tooseparate，但是它不知道您之前是通常可以透過視覺化事先取得的項目。 如果 hello 類別界限看起來非常異常，請盡可能使用決策樹、 決策叢林、 支援向量機器或類神經網路。

* 類神經網路可以搭配類別變數則會藉由建立**虛設變數**每個類別中將它設定 too1 在其中 hello 類別目錄會套用，0，不是其中的情況下。


<!-- This is how you can embed a link in an image in HTML. Don't know how toodo this in markdown.
<a href="http://download.microsoft.com/download/A/6/1/A613E11E-8F9C-424A-B99D-65344785C288/microsoft-machine-learning-algorithm-cheat-sheet.pdf">
<img src="C:\Users\garye\azure-docs-pr\articles\media\machine-learning-algorithm-cheat-sheet\cheat-sheet-small.png">
</a>
-->

<!-- Module References -->
[a-z-list]: https://msdn.microsoft.com/library/azure/dn906033.aspx
[initialize-model]: https://msdn.microsoft.com/library/azure/0c67013c-bfbc-428b-87f3-f552d8dd41f6/
[k-means-clustering]: https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/
[one-vs-all-multiclass]: https://msdn.microsoft.com/library/azure/7191efae-b4b1-4d03-a6f8-7205f87be664/
