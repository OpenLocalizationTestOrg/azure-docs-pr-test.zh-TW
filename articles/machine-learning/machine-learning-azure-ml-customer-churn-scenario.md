---
title: "客戶變換使用機器學習 aaaAnalyzing |Microsoft 文件"
description: "開發整合式模型以分析及評分客戶流失的案例研究"
services: machine-learning
documentationcenter: 
author: jeannt
manager: jhubbard
editor: cgronlun
ms.assetid: 1333ffe2-59b8-4f40-9be7-3bf1173fc38d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeannt
ms.openlocfilehash: 070e6a2ebe4f2fe439a42ffe1a3fa9d6d3788d62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-customer-churn-by-using-azure-machine-learning"></a>使用 Azure Machine Learning 分析客戶流失
## <a name="overview"></a>概觀
本文提供使用 Azure Machine Learning 建置客戶流失分析專案的參考實作。 在本文中，我們會討論而加以進行歷程解決的工業客戶變換的 hello 問題的相關聯的一般模型。 我們也會測量 hello 建立使用機器學習模型的精確度，我們評估進一步開發之用的說明。  

### <a name="acknowledgements"></a>通知
這項實驗是由 Microsoft 的首席資料科學家 Serge Berger 和 Microsoft Azure Machine Learning 的前產品經理 Roger Barga 共同開發和測試。 hello Azure 文件小組非常感謝認可其專業知識，並感謝共用這份技術白皮書。

> [!NOTE]
> 使用此實驗的 hello 資料不公開可用。 如 toobuild 機器學習的變換分析模型的方式範例，請參閱：[零售變換模型範本](https://gallery.cortanaintelligence.com/Collection/Retail-Customer-Churn-Prediction-Template-1)中[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com/)
> 
> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-problem-of-customer-churn"></a>客戶變換的 hello 問題
企業和所有的企業磁區 hello 消費者市場中有 toodeal 與變換。 有時，客戶流失太多會影響政策決定。 hello 傳統方案 toopredict 高傾向 churners 並解決透過指引服務，行銷活動，或藉由套用特殊 dispensations 其需求。 從業界 tooindustry 和甚至特定取用者叢集 tooanother 一個產業 （例如，電信） 內，這些方法可能會不同。

hello 共同因素是企業需要 toominimize 這些特殊的客戶保留投入時間。 因此，自然方法會 tooscore hello 機率變換每位客戶，解決 hello 前 n 個項目。 hello 最佳客戶可能 hello 最有利潤的;例如，在更複雜的情況下，收益函式會採用在 hello 選取特殊 dispensation 候選項目期間。 不過，這些考量是只包含 hello 變換處理的整體策略的一部分。 企業也有到帳戶風險 （和相關聯的風險承受度） tootake hello 層級和 hello 介入和擬真客戶區隔的成本。  

## <a name="industry-outlook-and-approaches"></a>產業展望和作法
駕輕就熟地處理客戶流失是成熟產業的一項特徵。 hello 典型的範例 hello 電信業界位置是 「 訂閱者 」 從一個提供者 tooanother 已知的 toofrequently 交換器。 這種志願性流失是最主要問題所在。 此外，提供者已經累積相當了解有關*變換驅動程式*，而該磁碟機客戶 tooswitch 是 hello 因素。

比方說，手持式裝置選擇會是已知的 hello 行動電話公司中變換驅動程式。 如此一來，熱門原則是新的 「 訂閱者 」 和充電完整價格 tooexisting 升級客戶話筒 toosubsidize hello 價格。 在過去，此原則導致 toocustomers 跳動從一個提供者 tooanother tooget 新折扣，亦有提示您提供者 toorefine 其策略。

手機產品日新月異，是造成以最新手機款式為主的客戶流失模型迅速失效的一項因素。 此外，行動電話不是只有電信裝置。它們也方式陳述式 （請考慮 hello iPhone），而且這些社交預測量是一般的電信資料集的 hello 範圍外。

hello 用於模型化的最後結果就是您無法只藉由消除變換的已知的原因設計音效的原則。 事實上，持續性的模型建構策略是 **必要的**，包括量化類別變項的傳統模型 (例如決策樹)。

客戶使用大型資料集，組織執行巨量資料分析 （尤其是，根據巨量資料變換偵測） 為有效的方法 toohello 問題。 您可以找到更多關於變換 hello 建議 ETL > 一節中的 hello 巨量資料方法 toohello 問題。  

## <a name="methodology-toomodel-customer-churn"></a>方法 toomodel 客戶變換
常見解決問題的程序 toosolve 客戶變換描繪數字 1-3:  

1. 風險模型可讓您 tooconsider 動作如何影響機率和風險。
2. 操作模型可讓您 tooconsider hello 介入的程度可能會影響 hello 機率變換 hello 數量及客戶存留時間值 (CLV) 的方式。
3. 這項分析本身是擴大的 tooa 主動式行銷活動的目標客戶區段 toodeliver hello 最佳優惠的 tooa 質化分析。  

![][1]

這種預視的方法是最佳方式 tootreat 變換 hello，但它隨附複雜度： 我們有 toodevelop hello 模型之間多模型原型和追蹤相依性。 可以封裝 hello 模型間的互動，hello 下列圖表所示：  

![][2]

*圖 4：多模型整合原型*  

Hello 模型之間的互動是索引鍵，如果我們 toodeliver 全面性方法 toocustomer 保留。 每一個模型一定隨著時間逐漸降低。因此，hello 架構是隱含的迴圈 (類似 toohello 原型 hello CRISP-DM 資料採礦的標準，來設定 [***3***])。  

hello 風險決策行銷分割/分解的整個週期仍然是通用的結構，也就是適用的 toomany 商務問題。 變換分析是只是這個群組的問題是強式代表值，因為它所表現的簡化預測方案不允許有複雜的商務問題的所有 hello 特性。 hello 社交 hello 現代方法 toochurn 層面不特別以反白顯示 hello 方法，但 hello 社交層面封裝在 hello 模型原型，因為它們可以在任何模型。  

此處增添的一項重要部分是巨量資料分析。 現今的電信和零售企業收集徹底瞭解他們的客戶的資料和我們可以輕鬆地預測該 hello 需要針對多模型連線將會變成一般趨勢，指定新趨勢，例如 hello 物聯網和無所不在的裝置，可讓多個層級 tooemploy 商務智慧方案。  

 

## <a name="implementing-hello-modeling-archetype-in-machine-learning-studio"></a>實作模型原型，Machine Learning Studio 中的 hello
指定 hello 剛剛所述的問題，什麼是最佳方式 tooimplement hello 整合式的模型及計分方法？ 在本節中，我們將示範如何利用 Azure Machine Learning Studio 來達成這項目的。  

hello 多模型方法時，必須設計全域變換的原型。 即使 hello 計分 hello 方法 （預測） 的一部分應該多模型。  

hello 下列圖表顯示 hello 原型建立，其採用 Machine Learning Studio toopredict 變換量的四個計分演算法。 hello 原因使用多模型的方式是不僅 toocreate 集團分類 tooincrease 精確度，而且還 tooprotect 防止過度配度與 tooimprove 精準的特徵選取。  

![][3]

*圖 5：客戶流失模型建構方法的原型*  

hello 下列各節提供更多詳細 hello 原型計分我們實作是利用 Machine Learning Studio 中的模型。  

### <a name="data-selection-and-preparation"></a>選擇和準備資料
使用 toobuild hello 模型 hello 資料和分數客戶已經 CRM 垂直方案中，從取得的 hello 資料模糊化 tooprotect 客戶隱私權。 hello 資料包含在 hello 美國、 8000 訂用帳戶資訊，而且它會結合三個來源： 佈建資料 （訂用帳戶中繼資料），活動資料 （hello 系統的使用方式），以及客戶支援的資料。 hello 資料不包含任何商務相關 hello 客戶; 的相關資訊例如，它不包含忠誠度中繼資料或參與名單的分數。  

為了簡單起見，ETL 和資料淨化處理不在討論範圍內，因為我們假設資料準備已在別處完成。   

模型的特徵選取根據 hello 組預測值，包含使用 hello 隨機樹系模組的 hello 程序中的計分初步的重要性。 Machine Learning Studio 中的 hello 實作，我們可以計算 hello 平均、 中間值和具代表性的功能範圍。 例如，我們加入 hello 質化資料，例如使用者活動的最小和最大值的彙總。    

我們也會擷取暫時資訊 hello 最近六個月。 一年的分析資料，我們建立，即使沒有統計上明顯的趨勢，變換 hello 影響會大為降低六個月後。  

hello 最重要的一點是 hello 整個程序，包括 ETL，特徵選取，而且模型已實作在機器學習 Studio 中，使用 Microsoft Azure 中的資料來源。   

hello 下列圖表說明 hello 所使用的資料。  

![][4]

*圖 6：資料來源摘錄 (經過模糊處理)*  

![][5]

*圖 7：從資料來源擷取的特徵*
 

> 請注意，這項資料是私用，因此無法共用 hello 模型和資料。
> 不過，類似的模型，使用可公開可用的資料，請參閱下列範例實驗中 hello [Cortana 智慧組件庫](http://gallery.cortanaintelligence.com/):[電信公司客戶變換](http://gallery.cortanaintelligence.com/Experiment/31c19425ee874f628c847f7e2d93e383)。
> 
> 深入了解如何實作使用 Cortana 智慧套件的變換分析模型 toolearn，我們也建議[這段影片](https://info.microsoft.com/Webinar-Harness-Predictive-Customer-Churn-Model.html)由資深方案經理 Wee Wee-hyong Tok。 
> 
> 

### <a name="algorithms-used-in-hello-prototype"></a>Hello 原型中使用的演算法
我們使用下列四個機器學習演算法的 hello toobuild hello 原型 （沒有任何自訂）：  

1. 邏輯式迴歸 (LR)
2. 推進式決策樹 (BT)
3. 平均感知器 (AP)
4. 支援向量機器 (SVM)  

hello 下列圖表說明 hello 實驗設計介面，表示哪些 hello 模型所建立的 hello 順序的一部分：  

![][6]  

*圖 8：在 Machine Learning Studio 中建立模型*  

### <a name="scoring-methods"></a>評分方法
我們使用標籤的定型資料集評分 hello 四個模型。  

我們也送出 hello 計分的 SAS Enterprise 器 12 hello 桌面版本來建立資料集 tooa 比較模型。 我們會測量 hello hello SAS 模型和所有的四種 Machine Learning Studio 模型的精確度。  

## <a name="results"></a>結果
在本節中，我們提供我們的發現有關 hello hello 計分資料集為基礎的 hello 模型精確度。  

### <a name="accuracy-and-precision-of-scoring"></a>評分的正確性和準確度
一般而言，Azure Machine Learning 中的 hello 實作位於 SAS 中大約 10-15%（在曲線區域或 AUC） 的精確度。  

不過，hello 變換中最重要的度量是 hello 錯誤分類速率： 也就是的 hello 前 n 個 churners 做為預測 hello 分類，其中實際執行**不**變換，，和在尚未收到特殊的處理方式？ hello下列圖表比較所有 hello 模型此錯誤分類率：  

![][7]

*圖 9：Passau 原型曲線下面積*

### <a name="using-auc-toocompare-results"></a>使用 AUC toocompare 結果
在曲線區域 (AUC) 是代表全域的量值的標準*separability*之間的正數和負數的母體擴展的分數的 hello 散發。 它類似 toohello 傳統接收者運算子特性 (ROC) 圖形中，但是有一個重要差異是該 hello AUC 度量不需要您 toochoose 臨界值。 相反地，它摘述 hello 結果透過**所有**可能的選項。 相反地，hello 傳統 ROC 圖表顯示 hello 正數速率的 hello 垂直軸和 hello false 正數的速率 hello 水平軸上和 hello 分類臨界值而有所不同。   

AUC 通常作為值得的量值不同的演算法 （或不同的系統） 因為它可讓模型 toobe 透過其 AUC 值進行比較。 這在如氣象和生物科學等領域是常用的方法。 因此，AUC 是一種評估分類器表現的普遍工具。  

### <a name="comparing-misclassification-rates"></a>比較分類誤判率
我們使用的大約每 8,000 個訂閱 hello CRM 資料比較 hello hello 資料集有問題的錯誤分類比率。  

* hello SAS 錯誤分類速率為 10-15%。
* hello Machine Learning Studio 錯誤分類成本是 hello top 200-300 churners 15 20%。  

在 hello 電信產業、 很重要的 tooaddress 僅具有這些客戶 hello 最高風險 toochurn 藉由提供它們指引服務或其他特殊的處理。 在這方面，hello Machine Learning Studio 實作達成與 hello SAS 模型同等的結果。  

Hello 的相同語彙基元，精確度為有效位數比更重要因為我們最感興趣正確分類潛在 churners。  

hello 維基百科中的下列圖表描述熱烈、 容易瞭解圖形中的 hello 關聯性：  

![][8]

*圖 10：正確性和準確度之間的取捨*

### <a name="accuracy-and-precision-results-for-boosted-decision-tree-model"></a>推進式決策樹模型的正確性與準確度結果
下列圖表顯示 hello 未經處理的 hello 得到的計分 hello 促進式決策樹模型，這種 toobe hello 最精確 hello 四種模型之間使用 hello Machine Learning 原型：  

![][9]

*圖 11：推進式決策樹模型的特性*

## <a name="performance-comparison"></a>表現比較
我們比較 hello 速度資料已計分使用 hello Machine Learning Studio 模型和建立 hello 桌面版本的 SAS 企業器 12.1 來比較模型。  

hello 下表摘要說明 hello 演算法 hello 的效能：  

*表 1.一般效能 （精確度） 的 hello 演算法*

| LR | BT | AP | SVM |
| --- | --- | --- | --- |
| 平均模型 |hello 最佳模型 |表現不佳 |平均模型 |

裝載的效能勝過 SAS 15-25%的執行，但精確度的速度是主要在長條上方，Machine Learning Studio 中的 hello 模型。  

## <a name="discussion-and-recommendations"></a>討論與建議
在 hello 電信產業、 幾個作法應有 tooanalyze 變換，包括：  

* 導出四個基本類別的度量：
  * **實體 (例如訂用帳戶)**。 佈建 hello 訂用帳戶及/或變換 hello 主體的客戶的基本資訊。
  * **活動**。 取得是相關的 toohello 實體，例如 hello 登入數目的所有可能的使用方式資訊。
  * **客戶支援**。 蒐集資訊從客戶支援記錄 tooindicate，是否 hello 訂閱有問題或互動與客戶支援。
  * **競爭性和商務資料**。 取得 hello 客戶有關的任何可能的資訊 （例如，可以是無法使用或硬 tootrack）。
* 使用重要性 toodrive 特徵選取。 這表示該 hello 促進式決策樹模型中永遠是我們的方法。  

hello 這四種類型的使用會建立 hello 假象簡單*決定性*索引於合理的因素，每個類別，格式為基礎的方法，應該可以滿足 tooidentify 客戶變換的風險。 可惜，雖然這種想法看似可行，但卻是一種誤解。 hello 原因是變換是暫時的效果，而且 hello 因素造成 toochurn 通常是暫時性的狀態。 導致客戶 tooconsider 離開目前可能是不同明天，而它一定會是不同六個月從現在。 因此，有必要使用「機率」  模型。  

商務，通常慣用 business intelligence 導向方法 tooanalytics 經常忽略這個重要的觀察，大部分，因為它更容易銷售接受簡單的自動化。  

不過，hello 承諾的自助式分析使用 Machine Learning Studio 是資訊的 hello 四種分類，來評分依部門，變成變換的機器學習的重要來源。  

另一個有趣的功能即將在 Azure Machine Learning 中是 hello 能力 tooadd 已有的預先定義之模組的自訂模組 toohello 儲存機制。 這項功能，基本上，建立商機 tooselect 文件庫，並建立市場都有的範本。 它是 Azure Machine Learning hello 服務商場中的重要差異。  

我們希望 toocontinue hello 未來，特別相關 toobig 資料分析中的這個主題。
  

## <a name="conclusion"></a>結論
這份文件使用一般架構，可用來描述客戶變換的實用方法 tootackling hello 一般問題。 我們採用原型來給模型評分，並使用 Azure Machine Learning 來實作。 最後，我們會評估 hello 精確度和 hello 原型方案中使用 SAS 而考慮 toocomparable 演算法的效能。  

**其他資訊：**  

本文對您有幫助嗎？ 請提供意見給我們。 小數位數為 1 （很差） too5 （很好） 上告訴我們您會如何對這份文件，為什麼您打此分級？ 例如：  

* 評分很高的到期 toohaving 很好的例子，絕佳的螢幕擷取畫面，清楚明確或因為其他原因？
* 評分很低的到期 toopoor 範例、 模糊的螢幕擷取畫面或不清楚撰寫？  

這份回函將協助我們改善 hello 發行我們的技術白皮書品質。   

[傳送意見](mailto:sqlfback@microsoft.com)。
 

## <a name="references"></a>參考
[1] predictive Analytics: hello 預測，W McKnight，Information Management 年 7 月/年 8 月 2011，p.18 20 之外。  

[2] 維基百科文章：[正確性與準確度](http://en.wikipedia.org/wiki/Accuracy_and_precision)

[3] [CRISP-DM 1.0：資料採礦逐步指南](http://www.the-modeling-agency.com/crisp-dm.pdf)   

[4] [巨量資料行銷：更有效地吸引您的客戶和促進價值](http://www.amazon.com/Big-Data-Marketing-Customers-Effectively/dp/1118733894/ref=sr_1_12?ie=UTF8&qid=1387541531&sr=8-12&keywords=customer+churn)

[5] [Cortana Intelligence 資源庫](http://gallery.cortanaintelligence.com/)中的[電信公司客戶流失模型範本](http://gallery.cortanaintelligence.com/Experiment/Telco-Customer-Churn-5) 
 

## <a name="appendix"></a>附錄
![][10]

*圖 12：客戶流失原型的簡報擷取畫面*

[1]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-1.png
[2]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-2.png
[3]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-3.png
[4]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-4.png
[5]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-5.png
[6]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-6.png
[7]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-7.png
[8]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-8.png
[9]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-9.png
[10]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-10.png
