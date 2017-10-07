---
title: "aaaHow toochoose 機器學習演算法 |Microsoft 文件"
description: "如何 toochoose Azure 機器學習演算法在叢集中受監督和不受監督的學習、 分類或迴歸實驗。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: a3b23d7f-f083-49c4-b6b1-3911cd69f1b4
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/25/2017
ms.author: garye
ms.openlocfilehash: 367b2278acc2435f27f9d24ead8199db58aca283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-algorithms-for-microsoft-azure-machine-learning"></a>如何為 Microsoft Azure Machine Learning toochoose 演算法
hello 回答 toohello 問題 「 哪些機器學習演算法應該使用？ 」 」的答案永遠都是「視情況。 Hello 大小、 品質以及 hello 資料的本質而定。 這取決於您想要 toodo hello 的答案。 它相依於 hello 數學 hello 演算法的方式轉譯為您正在使用的 hello 電腦的指示。 而這又需視您有多少時間。 即使最發生 hello 資料科學家無法分辨哪一個演算法將會執行最佳之前嘗試它們。

## <a name="hello-machine-learning-algorithm-cheat-sheet"></a>hello 機器學習演算法小工作表
hello **Microsoft Azure 機器學習演算法小工作表**可協助您選擇 hello 右邊機器學習演算法，為從 hello Microsoft Azure 機器學習程式庫演算法的預測分析解決方案。
本文將逐步引導您 toouse 它。

> [!NOTE]
> toodownload hello 祕技與遵循這個發行項，請移過[機器的 Microsoft Azure Machine Learning Studio 學習演算法小祕技](machine-learning-algorithm-cheat-sheet.md)。
> 
> 

這個小祕技記住有非常特定的對象： 開頭資料科學家 charlie 層級的機器學習 」 中，以嘗試 toochoose Azure Machine Learning Studio 中使用的演算法 toostart。 這表示小祕技可能會比較概括且過於簡化，但它為您指引一個可靠的方向。 同時這也意味著還有許多演算法並未列入其中。 Azure Machine Learning 隨著 tooencompass 一組更完整的可用方法，我們會將其加入。

這些建議是收集許多資料科學家與機器學習專家的意見反應和提示所編撰而成。 我們未同意的任何項目，但我嘗試過 tooharmonize 意見到粗略共識。 大部分的 disagreement hello 陳述式的開頭為 「 它相依...」

### <a name="how-toouse-hello-cheat-sheet"></a>如何 toouse hello 速查表
讀取 hello 做為 hello 圖表上的路徑和演算法標籤 」 的*&lt;路徑標籤&gt;*，使用*&lt;演算法&gt;*。 」 例如「如果需要 *speed* (速度)，則使用 *two class logistic regression* (雙類別羅吉斯迴歸)。」 有時候適用於多個分支。
有時候則不完全適用。 它們是預定的 toobe 法則的建議，因此不要擔心正在確切。
談到具有數個資料科學家說只確定的方式來尋找 hello 非常最佳的演算法是 tootry 該 hello 它們全部。

以下是從 hello 範例[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com/)的實驗，並試著 hello 針對數種演算法相同的資料和比較 hello 結果：[比較多級分類器： 字母辨識](http://gallery.cortanaintelligence.com/Details/a635502fc98b402a890efe21cec65b92).

> [!TIP]
> toodownload 及列印的圖表，hello Machine Learning Studio 中，功能的概觀，請參閱[Azure Machine Learning Studio 功能的概觀圖表](machine-learning-studio-overview-diagram.md)。
> 
> 

## <a name="flavors-of-machine-learning"></a>機器學習的類型
### <a name="supervised"></a>監督式
監督式學習演算法會根據一組範例做出預測。 比方說，歷程記錄股票價格可以是使用的 toohazard 猜測，在未來的價格。 用於定型的每個範例會加上感興趣的 hello 值 — 在此情況下 hello 股票價格。 監督式學習演算法會在這些值標籤中尋找模式。 它可以使用任何可能相關的資訊 — hello 天數 hello 週 hello 季節、 hello 公司財務資料，hello 的產業、 類型 hello 干擾地理政治事件是否存在，及每一個演算法會尋找不同類型的模式。 Hello 演算法找到 hello 最佳的模式，它可以後，它會使用模式 toomake 預測未標記測試資料 — 明天的價格。

監督式學習是常見且實用的機器學習類型。 有一個例外狀況，在 Azure 機器學習所有 hello 模組是監督都式學習演算法。 Azure 機器學習中有幾個代表性的特定監督式學習類型：分類、迴歸和異常偵測。

* **分類**。 當 hello 資料正在使用的 toopredict 類別時，監督式的學習也稱為分類。 這是指派為 'cat' 或 'dog' 圖片影像 hello 情況。 如果只有兩個選擇，則稱作**雙類別**或**二項式分類**。 時有更多的類別，做為預測的 hello NCAA 年 3 月瘋狂聯賽 hello 成功者時，此問題稱為**多級分類**。
* **迴歸**。 如果要預測值，例如股價，這種監督式學習稱為迴歸。
* **異常偵測**。 有時 hello 的目標是只是不尋常的 tooidentify 資料點。 例如在偵測詐騙時，只要是極不尋常的信用卡消費模式都有嫌疑。 hello 可能變化這麼多和 hello 因此數，它是不可行 toolearn 詐騙活動看起來的定型範例。 異常偵測採用的方法是 toosimply 深入了解哪些活動正常看起來像 （使用歷程記錄非詐騙交易），並找出任何明顯不同的項目。

### <a name="unsupervised"></a>未監督式
在未監督的學習中，資料點沒有與其相關聯的標籤。 相反地，hello 目標不受監督的學習演算法組織中部分的方式或 toodescribe hello 資料結構。 這種方式可能是將資料劃分為叢集，或尋找各種查看複雜資料的方式，讓資料變得更簡單或更整齊。

### <a name="reinforcement-learning"></a>增強式學習
增援學習 hello 演算法取得 toochoose 動作以回應 tooeach 資料點。 hello 學習演算法也會收到一小段時間之後，指出妥當 hello 決策是報酬訊號。
根據這個 hello 演算法修改其策略中順序 tooachieve hello 最高的報酬。 Azure 機器學習中目前沒有增強式學習演算法模組。 增援學習中很常見機器人其中 hello 時間在一處的感應器讀數組是資料點，而 hello 演算法必須選擇 hello 機器人的下一個動作。 它的性質也很適合物聯網應用。

## <a name="considerations-when-choosing-an-algorithm"></a>選擇演算法時的考量
### <a name="accuracy"></a>精確度
取得 hello 最精確回應可能並不一定。
視您的用途而定，有時候近似值便已足夠。 在 hello 情形下，您可能無法 toocut 您處理時間大幅會繼續使用多個相近的方法。 近似法的另一項優點是，它們會自然傾向於避免 [過度學習](https://youtu.be/DQWI1kvmwRg)。

### <a name="training-time"></a>定型時間
hello 的分鐘數或小時必要 tootrain 模型而異划算演算法。 定型時間精確度與通常緊密相關-一個通常會伴隨其他 hello。 此外，某些演算法會更為敏感 toohello 資料點數目比其他。
時間限制時它資料表可以驅動 hello 演算法的選擇，尤其 hello 資料集很大。

### <a name="linearity"></a>線性
許多機器學習演算法都會使用線性。 線性分類演算法會假設可以直線 (或較高維度類比) 分隔類別。 這些演算法包括羅吉斯迴歸和支援向量機器 (如同 Azure 機器學習中所實作)。
線性迴歸演算法會假設資料趨勢依循著一條直線。 這類假設對某些問題而言還不錯，但在其他問題上會降低精確度。

![非線性類別界限][1]

***非線性類別界限*** *- 依賴線性分類演算法會造成低精確度的結果*

![具有非線性趨勢的資料][2]

***具有非線性趨勢的資料*** *：使用線性迴歸方法會產生較大且不必要的誤差*

儘管有風險，線性演算法對於首次攻擊而言仍是一種非常熱門的方式。 它們通常 toobe 以演算法簡單和快速定型。

### <a name="number-of-parameters"></a>參數數目
參數是 hello 參數設定的演算法時，資料科學家取得 tooturn。 它們是會影響 hello 演算法的行為，例如容錯或反覆項目或之間的 hello 演算法的運作方式的選項數目的數字。 hello 定型時間和精確度的 hello 演算法有時可能很容易受到 toogetting 只 hello 正確設定。 一般而言，大量參數的演算法需要最試用版的 hello 和錯誤 toofind 良好的組合。

或者，Azure 機器學習中有 [參數掃掠](machine-learning-algorithm-parameters-optimize.md) 模組區塊，會依照您選擇的細微性，自動嘗試所有參數組合。 雖然這是很好的方法 toomake 確定您已合併 hello 參數空間; hello 所需時間 tootrain 模型以等比級數增加 hello 參數數目。

hello 優點是，通常具有許多參數指出演算法是否有更大的彈性。 這通常可以達到很高的精確度。 提供您可以找到 hello 正確的參數設定的組合。

### <a name="number-of-features"></a>特徵數目
對於特定類型的資料，hello 的特徵數目可以是非常大的比較的 toohello 資料點數目。 這通常是 hello 跟 genetics 或文字資料。 hello 大量的功能可以陷入困境、 導致關閉某些學習演算法，進行訓練 unfeasibly 長的時間。 支援向量機器是特別適用於 toothis 案例 （請參閱下文）。

### <a name="special-cases"></a>特殊案例
某些學習演算法會做出特定假設 hello 結構 hello 資料或 hello 預期結果。 如果可以找到符合需求的假設，您就能獲得更實用的結果、更精確的預測或更快的定型時間。

| **演算法** | **精確度** | **定型時間** | **線性** | **參數** | **注意事項** |
| --- |:---:|:---:|:---:|:---:| --- |
| **雙類別分類** | | | | | |
| [羅吉斯迴歸](https://msdn.microsoft.com/library/azure/dn905994.aspx) | |● |● |5 | |
| [決策樹系](https://msdn.microsoft.com/library/azure/dn906008.aspx) |● |○ | |6 | |
| [決策叢林](https://msdn.microsoft.com/library/azure/dn905976.aspx) |● |○ | |6 |低記憶體使用量 |
| [促進式決策樹](https://msdn.microsoft.com/library/azure/dn906025.aspx) |● |○ | |6 |高記憶體使用量 |
| [類神經網路](https://msdn.microsoft.com/library/azure/dn905947.aspx) |● | | |9 |[支援其他自訂項目](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [平均感知器](https://msdn.microsoft.com/library/azure/dn906036.aspx) |○ |○ |● |4 | |
| [支援向量機器](https://msdn.microsoft.com/library/azure/dn905835.aspx) | |○ |● |5 |適用於大型特徵集 |
| [本機深度支援向量機器](https://msdn.microsoft.com/library/azure/dn913070.aspx) |○ | | |8 |適用於大型特徵集 |
| [貝氏點機器](https://msdn.microsoft.com/library/azure/dn905930.aspx) | |○ |● |3 | |
| **多類別分類** | | | | | |
| [羅吉斯迴歸](https://msdn.microsoft.com/library/azure/dn905853.aspx) | |● |● |5 | |
| [決策樹系](https://msdn.microsoft.com/library/azure/dn906015.aspx) |● |○ | |6 | |
| [決策叢林 ](https://msdn.microsoft.com/library/azure/dn905963.aspx) |● |○ | |6 |低記憶體使用量 |
| [類神經網路](https://msdn.microsoft.com/library/azure/dn906030.aspx) |● | | |9 |[支援其他自訂項目](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [one-v-all](https://msdn.microsoft.com/library/azure/dn905887.aspx) |- |- |- |- |請參閱 hello 選取兩個類別方法的屬性 |
| **迴歸** | | | | | |
| [線性](https://msdn.microsoft.com/library/azure/dn905978.aspx) | |● |● |4 | |
| [貝氏線性](https://msdn.microsoft.com/library/azure/dn906022.aspx) | |○ |● |2 | |
| [決策樹系](https://msdn.microsoft.com/library/azure/dn905862.aspx) |● |○ | |6 | |
| [促進式決策樹](https://msdn.microsoft.com/library/azure/dn905801.aspx) |● |○ | |5 |高記憶體使用量 |
| [快速樹系分量](https://msdn.microsoft.com/library/azure/dn913093.aspx) |● |○ | |9 |分佈而不是點預測 |
| [類神經網路](https://msdn.microsoft.com/library/azure/dn905924.aspx) |● | | |9 |[支援其他自訂項目](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [波氏](https://msdn.microsoft.com/library/azure/dn905988.aspx) | | |● |5 |技術上為對數線性。 針對預測計算 |
| [序數](https://msdn.microsoft.com/library/azure/dn906029.aspx) | | | |0 |針對預測順位排序 |
| **異常偵測** | | | | | |
| [支援向量機器](https://msdn.microsoft.com/library/azure/dn913103.aspx) |○ |○ | |2 |特別適用於大型特徵集 |
| [PCA 型異常偵測](https://msdn.microsoft.com/library/azure/dn913102.aspx) | |○ |● |3 | |
| [K-means](https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/) | |○ |● |4 |叢集演算法 |

**演算法屬性：**

**●** -顯示極佳的精確度、 快速的定型時間及和線性 hello 使用

**○** ：顯示不錯的精確度和適度的定型時間

## <a name="algorithm-notes"></a>演算法備註
### <a name="linear-regression"></a>線性迴歸
如前所述，[線性迴歸](https://msdn.microsoft.com/library/azure/dn905978.aspx)符合一行 （或平面或超平面） toohello 資料集。 它是常被使用的主力，簡單又快速，但可能會過度簡化某些問題。
請查看這裡的 [線性迴歸教學課程](machine-learning-linear-regression-in-azure.md)。

![具有線性趨勢的資料][3]

***具有線性趨勢的資料***

### <a name="logistic-regression"></a>羅吉斯迴歸
雖然困惑，它包含 '迴歸' hello 名稱中，羅吉斯迴歸是實際的強大工具[二級](https://msdn.microsoft.com/library/azure/dn905994.aspx)和[多級](https://msdn.microsoft.com/library/azure/dn905853.aspx)分類。 它既快速又簡單。 hello 事實，它所使用的 '-使得自然適合將資料分組造形的曲線而不是直線。 羅吉斯迴歸提供線性類別界限，因此使用它時，請確定線性近似值是您能接受的結果。

![只要其中一項功能與羅吉斯迴歸 tootwo 類別資料][4]

***只要其中一項功能與羅吉斯迴歸 tootwo 類別資料*** *-類別界限是 hello 點在哪一個 hello 羅吉斯曲線只要接近 tooboth 類別*

### <a name="trees-forests-and-jungles"></a>樹、樹系和叢林
決策樹系 ([迴歸](https://msdn.microsoft.com/library/azure/dn905862.aspx)、[雙類別](https://msdn.microsoft.com/library/azure/dn906008.aspx)和[多類別](https://msdn.microsoft.com/library/azure/dn906015.aspx))、決策叢林 ([雙類別](https://msdn.microsoft.com/library/azure/dn905976.aspx)和[多類別](https://msdn.microsoft.com/library/azure/dn905963.aspx)) 以及促進式決策樹 ([迴歸](https://msdn.microsoft.com/library/azure/dn905801.aspx)和[雙類別](https://msdn.microsoft.com/library/azure/dn906025.aspx))，都是以基本的機器學習概念「決策樹」做為基礎。 有許多變化的決策樹，但它們全都執行相同的動作： hello 特徵空間細分為區域大部分 hello 與相同的標籤。 根據您是執行分類或迴歸而定，這些區域可能會有一致的類別或常數值。

![細分特徵空間的決策樹][5]

***此決策樹將特徵空間細分為值大致統一的區域***

特徵空間可以再細分為很小的區域，因為它是簡單 tooimagine 拆解自助式足夠 toohave 一個資料點每個區域。 而這就是過度學習的極端範例。 在順序 tooavoid 樹狀結構的大型集合，這被建構小心特殊數學採取 hello 樹狀結構並沒有關聯。 這個 「 決策樹系 」 hello 平均是樹狀目錄中可避免過度配適。 決策樹系會使用大量記憶體。 決策叢林是會耗用較少的記憶體在 hello 費用的定型時間稍微長的 variant。

促進式決策樹可藉由限制細分的次數，以及每個區域中允許的最少資料點，來避免過度學習。 此演算法建構的一連串的樹狀結構，其中每個學習 hello 樹狀之前所留下的 hello 錯誤補償。 hello 結果會是記憶體的非常精確的學習因子，其中通常會 toouse 大量。 如 hello 完整技術說明，請參閱[Friedman 的原始紙張](http://www-stat.stanford.edu/~jhf/ftp/trebst.pdf)。

[快速樹系分量迴歸](https://msdn.microsoft.com/library/azure/dn913093.aspx)是您要知道不僅 hello 典型 （中間） 值 hello 中的資料區域，但也分量 hello 形式其散發 hello 特殊案例的決策樹的變化。

### <a name="neural-networks-and-perceptrons"></a>類神經網路和感知器
類神經網路是受大腦啟發的學習演算法，其中涵蓋[多類別](https://msdn.microsoft.com/library/azure/dn906030.aspx)、[雙類別](https://msdn.microsoft.com/library/azure/dn905947.aspx)和[迴歸](https://msdn.microsoft.com/library/azure/dn905924.aspx)問題。 它們有無限的各種不同，但在 Azure Machine Learning 中的 hello 類神經網路 hello 導向非循環圖形式的所有。 這表示輸入的特徵在轉換成輸出前，會在一連串的層中一直向前傳遞，且永遠不會向後。 在每個圖層中，輸入會在不同的組合，經過加總，並且傳入 hello 下一層加權。 這種簡單的計算能力 toolearn 導致組合魔術看似複雜類別界限和資料趨勢。 多層網路，這種執行 hello"深入學習 」 的 fuels 因此大多數時候有科技 reporting 和科幻。

可惜這種高效能並非隨手可得。 類神經網路可能需要很長的時間 tootrain，特別是針對大型資料集具有許多功能。 他們也擁有比大部分的演算法，這表示參數掃掠划算展開 hello 定型時間更多參數。
與這些使用者需要太 overachievers[指定自己的網路結構](http://go.microsoft.com/fwlink/?LinkId=402867)，這些可能是 inexhaustible。

![類神經網路學習界限][6]
***hello 界限所類神經網路學習很複雜，異常***

hello[二級平均感知器](https://msdn.microsoft.com/library/azure/dn906036.aspx)為類神經網路回應 tooskyrocketing 定型時間。 它使用的網路結構會提供線性類別界限。 幾乎基本今天的標準，但它已有悠久的歷史穩當地運作的而且夠小，toolearn 快速。

### <a name="svms"></a>SVM
支援向量機器 (Svm) 尋找 hello 界限分隔為盡可能寬的邊界的類別。 當無法清楚地分隔 hello 兩個類別時，hello 演算法會發現 hello 最佳的界限，他們可以。 如同 Azure Machine Learning 中的 hello[二級 SVM](https://msdn.microsoft.com/library/azure/dn905835.aspx)進行這項只有直線。 (但以 SVM 的說法，應該是使用線性核心)。因為這會讓此之線性近似值，就能 toorun 速度會相當快。 可以真正發揮它功效的地方是特徵密集的資料，例如文字或基因資料。 在這些情況下 Svm 是記憶體的無法 tooseparate 類別打字速度並減少過度配適比其他大部分的演算法，此外 toorequiring 只有少量數量。

![支援向量機器類別界限][7]

***典型的支援向量機器類別界限最大化 hello 邊界分隔兩個類別***

另一個產品的 Microsoft Research hello[二級局部深度 SVM](https://msdn.microsoft.com/library/azure/dn913070.aspx)是非線性 SVM 保留大部分的 hello hello 線性版本的速度和記憶體效率。 理想的情況下 hello 線性方法不會授與足夠精確回應。 hello 開發人員保持它快速分解成一堆線性的小型 SVM 問題 hello 問題。 讀取 hello[完整描述](http://research.microsoft.com/um/people/manik/pubs/Jose13.pdf)如 hello 它們提取關閉這個方法同樣的方式的詳細資訊。

使用的非線性 Svm 聰明的副檔名，hello[一級 SVM](https://msdn.microsoft.com/library/azure/dn913103.aspx)繪製緊密概述 hello 整個資料集的界限。 這適合用於異常偵測。 遠超出該界限任何新資料點是不尋常夠 toobe 值得注意。

### <a name="bayesian-methods"></a>貝氏方法
貝氏方法具有令人滿意的高品質：可避免過度學習。 他們這麼做，藉由一些假設事先 hello 回應 hello 可能分佈。 這種方法的另一個附加好處在於其參數非常少。 Azure 機器學習中的分類 ([雙類別貝氏點機器](https://msdn.microsoft.com/library/azure/dn905930.aspx)) 和迴歸 ([貝氏線性迴歸](https://msdn.microsoft.com/library/azure/dn906022.aspx)) 都各有貝氏演算法。
請注意，這些假設 hello 資料可以分割或配合一條直線。

在歷史記錄中，貝氏點機器是由 Microsoft Research 所開發。 它們有一些格外出色的理論做為後盾。 hello 興趣的學生會導向的 toohello [JMLR 中的原始文章](http://jmlr.org/papers/volume1/herbrich01a/herbrich01a.pdf)和[見解部落格，Chris Bishop](http://blogs.technet.com/b/machinelearning/archive/2014/10/30/embracing-uncertainty-probabilistic-inference.aspx)。

### <a name="specialized-algorithms"></a>專門的演算法
如果您有非常特定的目標，那麼您的可能運氣特別好。 Azure Machine Learning 集合 hello，有在特製化的演算法：

- 排名預測 ([序數迴歸](https://msdn.microsoft.com/library/azure/dn906029.aspx))、
- 計算預測 ([波氏迴歸](https://msdn.microsoft.com/library/azure/dn905988.aspx))、
- 異常偵測 (一個以[主體元件分析](https://msdn.microsoft.com/library/azure/dn913102.aspx)為基礎，一個以[支援向量機器](https://msdn.microsoft.com/library/azure/dn913103.aspx)為基礎)
- 叢集 ([K-means](https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/))

![PCA 型異常偵測][8]

***以 PCA 為基礎的異常偵測*** *-hello 的大部分 hello 資料分成 stereotypical 發佈; 大幅偏離該發佈點都有疑問*

![使用 K-means 分組的資料集][9]

***資料集使用 K-means 分為五個叢集***

另外還有一整團[一個 v 所有多級分類器](https://msdn.microsoft.com/library/azure/dn905887.aspx)，N-1 二級分類問題哪些符號 hello N 類別分類問題。 hello 精確度、 定型時間及線性屬性取決於使用 hello 二級分類器。

![二級分類器結合 tooform 三個類別分類器][10]

***二級分類器的一組結合 tooform 三個類別分類器***

Azure 機器學習也包含存取 tooa 功能強大的機器學習架構的 hello 標題底下[Vowpal Wabbit](https://msdn.microsoft.com/library/azure/8383eb49-c0a3-45db-95c8-eb56a1fef5bf)。
VW 背離這裡的歸納，因為它可以學習分類和迴歸問題，甚至還能從一些沒有標記的資料中學習。 您可以設定 toouse 學習演算法、 遺失函式，以及最佳化演算法的數字的任何一個。 此設計是從 hello 地面向上 toobe 有效率、 平行、 且非常快速。 它可以輕鬆處理大到不可思議的特徵集。
由創辦 Microsoft Research 的 John Langford 所發起及領導的 VW，可謂原裝賽車演算法領域中的一級方程式項目。 並非所有問題都適合 VW，但如果有的話，它可能是非常值得 tooclimb 其介面上的學習曲線。 它也有以數種語言提供 [獨立的開放原始程式碼](https://github.com/JohnLangford/vowpal_wabbit) 。

## <a name="more-help-with-algorithms"></a>更多演算法的詳細說明
* 如需描述演算法並提供範例的可下載資訊圖詳細資訊，請參閱[可下載的資訊圖：機器學習服務基本概念和演算法範例](machine-learning-basics-infographic-with-algorithm-examples.md)。
* 如需依類別目錄可用 Azure Machine Learning Studio 中的所有 hello 機器學習演算法的清單，請參閱[初始化模型][ initialize-model] hello 機器學習 Studio 演算法和模組說明。
* 如需 Azure Machine Learning Studio 中按字母順序排列的完整演算法和模組清單，請參閱＜Machine Learning Studio 演算法和模組說明＞中的 [Machine Learning Studio 模組的 A-Z 清單][a-z-list]。
* toodownload 及列印一張圖表，hello Azure Machine Learning Studio 中，功能的概觀，請參閱[Azure Machine Learning Studio 功能的概觀圖表](machine-learning-studio-overview-diagram.md)。


<!-- Reference links -->
[initialize-model]: https://msdn.microsoft.com/library/azure/dn905812.aspx
[a-z-list]: https://msdn.microsoft.com/library/azure/dn906033.aspx

<!-- Media -->

[1]: ./media/machine-learning-algorithm-choice/image1.png
[2]: ./media/machine-learning-algorithm-choice/image2.png
[3]: ./media/machine-learning-algorithm-choice/image3.png
[4]: ./media/machine-learning-algorithm-choice/image4.png
[5]: ./media/machine-learning-algorithm-choice/image5.png
[6]: ./media/machine-learning-algorithm-choice/image6.png
[7]: ./media/machine-learning-algorithm-choice/image7.png
[8]: ./media/machine-learning-algorithm-choice/image8.png
[9]: ./media/machine-learning-algorithm-choice/image9.png
[10]: ./media/machine-learning-algorithm-choice/image10.png
