---
title: "Azure Machine Learning 中的特徵設計和選取 | Microsoft Docs"
description: "說明機器學習的資料增強程序中特性選取和特性工程設計的目的，並提供其角色的範例。"
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
redirect_document_id: TRUE
ms.openlocfilehash: 51a5d8fed492cb9301e048c2b6a721e4573a47d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="feature-engineering-and-selection-in-azure-machine-learning"></a>Azure 機器學習中的特性工程設計和選取
本主題說明機器學習的資料增強程序中特徵工程設計和特徵選取的目的。 其使用 Azure Machine Learning Studio 提供的範例來解釋這些程序的相關事項。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

從收集的原始資料選取或擷取特性，通常可以增強機器學習中使用的定型資料。 在了解如何將手寫字元影像分類的內容中，有一個工程設計的特徵範例是建立從原始位元分配資料建構的位元密度對應。 相較於原始分配，此對應有助於更有效地找出字元的界限。

工程設計和選取的特徵可提高下列定型過程的效率：嘗試擷取資料中內含的重要資訊。 此外，還可改善這些模型的功效，正確地分類輸入資料以及更精確地預測感興趣的結果。 特性工程設計和選取也可結合起來，讓學習更易於以運算方式處理。 其作法是提高而後減少校正或定型模型所需的特性數量。 從數學的角度來看，選取用來定型模型的特性是極小的一組獨立變數，可供解釋資料中的模式，然後成功地預測結果。

特性的工程設計和選取屬於較大型程序的一部分，該程序通常包含下列四個步驟：

* 資料收集
* 資料增強
* 模型建構
* 後處理

工程設計和選取構成了機器學習服務的資料增強步驟。 此程序的三個層面主要有四個目的：

* **資料前處理**：此程序嘗試確保收集的資料乾淨而一致。 其中包含下列工作：例如整合多個資料集、處理不一致的資料，以及轉換資料類型。
* **特性工程設計**：此程序嘗試從資料中的現有原始特性建立其他相關特性，以及增加學習演算法的預測功效。
* **特性選取**：此程序選取主要的原始資料特性子集，以縮小定型問題的維度。

本主題僅涵蓋資料增強程序的特徵工程設計和特徵選取層面。 如需資料前處理步驟的其他資訊，請參閱 [在 Azure Machine Learning Studio 中進行資料前處理](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/) 影片。

## <a name="creating-features-from-your-data--feature-engineering"></a>從您的資料建立特性 - 特性工程設計
定型資料包含由範例所組成的矩陣 (資料列中儲存的記錄或 觀察)，而每個範例都有一組特性 (資料行中儲存的變數或欄位)。 在實驗設計中指定的特性預計會將資料中的模式特性化。 儘管許多原始資料欄位都可以直接包含在選取用來將模型定型的特性集中，但通常還是需要從原始資料中的特性建構其他 (經過工程設計的) 特性，才能產生增強的定型資料集。

應建立何種特性，才能在模型定型時增強資料集？ 經過工程設計的特性可增強定型，還會提供用以區分資料中模式的資訊。 您期望新特性可提供原始或現有特性集中未清楚擷取或顯而易見的其他資訊，但此程序是一種藝術。 健全且有建設性的決策通常需要一些網域.專業知識。

從 Azure 機器學習著手時，最簡單的方式是透過 Machine Learning Studio 中提供的範例具體地領會此程序。 以下呈現兩個範例：

* 在已知目標值的監督實驗中的 ([單車租用數量預測](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4)) 迴歸範例
* 使用[特性雜湊][feature-hashing]的文字採礦分類範例

### <a name="example-1-adding-temporal-features-for-a-regression-model"></a>範例 1：新增迴歸模型的暫時特性
為了示範如何為迴歸工作的特徵進行工程設計，讓我們在 Azure Machine Learning Studio 中使用「單車的需求預測」實驗。 這項實驗的目標在於預測單車需求，也就是再特定月份、日期或小時內單車租用的數量。 資料集**單車租用 UCI 資料集**作為原始輸入資料使用。

此資料集是以在美國華盛頓特區維護單車出租網路的 Capital Bikeshare 公司所提供的實際資料為基礎。 此資料集代表 2011 年到 2012 年間，一天中某個特定小時內的單車租用數量，總共包含 17379 個資料列和 17 個資料行。 原始特性集包含天氣條件 (溫度、溼度、風速) 和當天的類型 (假日或工作日)。 要預測的欄位為 **cnt**，代表特定小時內單位租用的計數，其範圍是 1 至 977。

為了在定型資料中建構有效特性，會使用相同的演算法建立四個各有不同定型資料集的迴歸模型， 這四個資料集代表相同的原始輸入資料，但設定的特性數量增加。 這些特性可分為四類：

1. A = 預測日的天氣 + 假日 + 工作日 + 週末特性
2. B = 過去的 12 小時以來，每小時租出的單車數量
3. C = 過去的 12 天以來，每天在同一個時間租出的單車數量
4. D = 過去的 12 週以來，在同一天同一個時間租出的單車數量

除了已存在於原先未經處理資料中的特徵集 A 以外，其他三個特徵集都是透過特徵工程設計程序來建立。 特徵集 B 會擷取最近的單車需求。 特性集 C 會擷取某一個小時的單車需求。 特性集 D 會擷取一週當中某一天某一個小時的單車需求。 四個定型資料集分別包含特性集 A、A+B、A+B+C 和 A+B+C+D。

在 Azure 機器學習實驗中，這四個定型資料集是透過預先處理的輸入資料集中的分支形成。 除了最左邊的分支以外，每個分支都包含[執行 R 指令碼][execute-r-script]模組，其中有一組衍生的特徵 (特徵集 B、C 和 D) 會分別建構並附加至匯入的資料集 。 下圖示範左邊第二個分支中用來建立特性集 B 的 R 指令碼。

![建立功能集](./media/machine-learning-feature-selection-and-engineering/addFeature-Rscripts.png)

下表彙總四個模型的效能結果比較。 特性 A+B+C 所呈現的結果最理想。 請注意，當定型資料中包含其他特性集時，錯誤率會降低。 這證實了我們的推測：特性集 B 和 C 會針對迴歸工作提供其他相關資訊。 新增 D 特性集似乎不會讓錯誤率降低。

![比較效能結果](./media/machine-learning-feature-selection-and-engineering/result1.png)

### <a name="example2"></a> 範例 2：在文字採礦中建立特性
特性工程設計廣泛運用於文字採礦的相關工作，例如文件分類和情感分析。 例如，當您想要將文件分為數個類別時，通常會假設包含在一個文件類別中的文字或片語比較不可能出現在其他文件類別中。 換言之，文字或片語分配的次數能夠描述不同文件類別的特徵。 在文字採礦應用程式，建立文字或片語次數相關特性時需要特性工程設計程序中，因為個別的文字內容通常可作為輸入資料。

為了達成此工作，會套用名為特性雜湊的技術，有效地將任意文字特性變成索引。 此方法不會將每個文字特性 (文字或片語) 關聯至特定索引，而是將雜湊函數套用至特性並直接使用其雜湊值作為索引。

Azure 機器學習中有一個[特性雜湊][feature-hashing]模組，會建立這些文字或片語特性。 下圖顯示使用此模組的範例。 輸入資料集包含兩個資料行：1 至 5 的書籍評比，以及實際評論內容。 此[特性雜湊][feature-hashing]模組的目標在於擷取新特性，以顯示特定書籍評論中對應文字或片語的發生次數。 若要使用此模組，您必須完成下列步驟：

1. 選取包含輸入文字的資料行 (此例中的 **Col2**)。
2. 將 Hashing bitsize 設定為 8，表示將建立 2^8=256 個特徵。 所有文字中的文字或片語接著會雜湊至 256 個索引。 Hashing bitsize 參數的範圍是 1 至 31。 如果參數設定為較大的數字，則單字或片語較不會雜湊至相同的索引。
3. 將 N-grams 參數設定為 2。 這麼做可從輸入文字中擷取 unigrams (適用於每一個文字的特性) 和 bigrams (適用於每一對相鄰文字的特性) 的發生次數。 N-grams 參數的範圍是 0 至 10，這表示要包含在一個特性中的循序文字數目上限。  

![特性雜湊模組](./media/machine-learning-feature-selection-and-engineering/feature-Hashing1.png)

下圖顯示這些新特徵的外觀。

![特性雜湊範例](./media/machine-learning-feature-selection-and-engineering/feature-Hashing2.png)

## <a name="filtering-features-from-your-data--feature-selection"></a>從您的資料篩選特性 - 特性選取
特性選取程序通常適用於定型資料集的建構，以便進行預測性建模工作，例如分類或迴歸工作。 其目的在於從原始資料集中選取一小組特性，使用極小一組的特性來代表資料中的最大變異量，藉此縮小其維度。 這個特徵的子集只會包含要用於訓練模型的特徵。 特性選取有兩個主要目的：

* 特性選取通常會排除不相關、多餘或高度相關的特性，進而提高分類正確性。
* 特性選取會減少特性數目，讓模型定型程序更有效率。 對於定型代價昂貴的學習者 (例如支援向量機器) 而言，這格外重要。

雖然特性選取設法要減少資料集中用於定型模型的特性數目，但通常不是指「維度縮減」。 特性選取方法會擷取資料中的原始特性子集，但不會加以變更。  維度縮減方法會運用經過工程設計的特性，轉換原始特性並加以修改。 維度縮減方法的範例包含主成分分析、典型相關分析和奇異值分解。

監督環境中有一個廣泛應用的特性選取方法類別為以篩選為基礎的特性選取。 這些方法會評估每個特性與目標屬性之間的相關性，套用統計量值以將評分指派給每個特性。 接著會依分數將特性排名，而分數可供您用來設定保留或排除特定特性的臨界值。 這些方法中使用的統計量值範例包含皮耳森相關、相互資訊和卡方檢定。

Azure Machine Learning Studio 針對特性選取提供模組。 如下圖所示，這些模組包含[以篩選為基礎的特性選取][filter-based-feature-selection]和[費雪線性判別分析][fisher-linear-discriminant-analysis]。

![特性選取範例](./media/machine-learning-feature-selection-and-engineering/feature-Selection.png)

例如，使用[篩選為基礎的特徵選取][filter-based-feature-selection]模組與先前所述的文字採礦範例。 假設在透過[特徵雜湊][feature-hashing]模組建立一組 256 個特性之後，您想要建立一個迴歸模型，其應變數為 **Col1** 並代表 1 至 5 的書籍評論評比。 將 [特性評分方法] 設定為 [皮耳森相關]，則 [目標欄] 會是 **Col1**，而 [所需的特性數] 會是 **50**。 然後，[以篩選器為基礎的特徵選取][filter-based-feature-selection]模組會產生一個包含 50 個特徵且目標屬性為 **Col1** 的資料集。 下圖顯示此實驗的流程以及輸入參數。

![特性選取範例](./media/machine-learning-feature-selection-and-engineering/feature-Selection1.png)

下圖顯示結果產生的資料集。 每個特性都是根據本身與目標屬性 **Col1** 之間的皮耳森相關進行評分。 系統會保留最高分的特性。

![篩選器為基礎的特性選取資料集](./media/machine-learning-feature-selection-and-engineering/feature-Selection2.png)

下圖顯示所選特性的對應評分。

![選取的特性分數](./media/machine-learning-feature-selection-and-engineering/feature-Selection3.png)

套用這個[以篩選為基礎的特性選取][filter-based-feature-selection]模組，則會選取 256 個特性中的 50 個特性，因為根據**皮耳森相關**評分方法，其具有最多個與目標變數 **Col1** 相互關聯的特性。

## <a name="conclusion"></a>結論
建立機器學習模型時，常會執行特性工程設計和特性選取這兩個步驟來預備定型資料。 通常會先套用特性工程設計以產生其他特定，然後執行特性選取步驟以排除不相關、多餘或高度相關的特性。

您不一定要執行特徵工程設計或特徵選取。 需要與否取決於您所擁有或收集的資料、您挑選的演算法，以及實驗的目標。

<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/
