---
title: "Machine Learning 中的線性迴歸 aaaUsing |Microsoft 文件"
description: "在 Excel 和 Azure Machine Learning Studio 中的線性迴歸模型的比較"
metakeywords: 
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 417ae6ab-de4f-4bdd-957a-d96133234656
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: kbaroni;garye
ms.openlocfilehash: 8716040ad296053a72fb06c7c9660a186123ac15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-linear-regression-in-azure-machine-learning"></a>在 Azure Machine Learning 中使用線性迴歸
> *Kate Baroni* 和 *Ben Boatman* 是 Microsoft 的 Data Insights Center of Excellence 的企業解決方案架構設計人員。 在本文中，這些主題說明移轉現有迴歸分析套件 tooa 以雲端為基礎的方案使用 Azure Machine Learning 經驗。 
> 
> 

&nbsp; 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="goal"></a>目標
我們的專案開始時有兩個目標： 

1. 使用我們的組織每月的營收預測的預測分析 tooimprove hello 精確度 
2. 使用 Azure Machine Learning tooconfirm、 最佳化、 增加的速度，和小數位數的結果。 

與許多企業一樣，我們的組織會每個月都會經歷營收預測程序。 商務分析師我們小組需要使用 Azure Machine Learning toosupport hello 程序，並改善預測的精確度。 hello 小組花費幾個月多個來源收集資料，並透過識別索引鍵屬性相關 tooservices 銷售預測的統計分析執行 hello 資料屬性。 hello 下一個步驟是在 Excel 中的 hello 資料 toobegin 原型統計的迴歸模型。 幾週後，我們必須其效果優於 hello 目前的欄位和財務預測程序，將 Excel 迴歸模型。 這會變成 hello 基準預測結果。 

然後把下一個步驟 toomoving hello 我們的預測分析透過 tooAzure Machine Learning toofind 出機器學習如何對預測的效能改進。

## <a name="achieving-predictive-performance-parity"></a>達成預測效能同位檢查
我們第一優先順序的機器學習和 Excel 迴歸模型之間的 tooachieve 同位檢查。 指定 hello 相同的資料，而且 hello 分割進行定型和測試資料相同，我們想 tooachieve 預測效能 Excel 和機器學習服務之間的同位檢查。 一開始我們失敗了。 hello Excel 模型的效能勝過 hello 機器學習模型。 hello 失敗是工具的由於 tooa 缺乏 hello 基底，在機器學習中設定了解。 與 hello Machine Learning 產品小組的同步處理之後, 我們將獲得更深入了解 hello 基底設定需要針對我們的資料集，並達成 hello 兩個模型之間的同位檢查。 

### <a name="create-regression-model-in-excel"></a>在 Excel 中建立迴歸模型
我們 Excel 迴歸用於 hello Excel 分析工具箱 中找到的 hello 標準的線性迴歸模型。 

我們計算*平均絕對 %錯誤*，當成 hello 模型 hello 效能量值。 花費在處理模型，使用 Excel 的 3 個月 tooarrive。 我們回到大部分 hello 學習到 hello Machine Learning Studio 的實驗，最終已了解需求有幫助。

### <a name="create-comparable-experiment-in-azure-machine-learning"></a>在 Azure Machine Learning 建立可比較的實驗
我們會遵循這些步驟 toocreate 我們 Machine Learning Studio 中的實驗： 

1. 上傳的 hello 做為 csv 檔案 tooMachine Learning Studio （非常小的檔案） 的資料集
2. 建立新的實驗，並使用 hello[資料集中選取的資料行][ select-columns]模組 tooselect hello Excel 中所使用的相同資料功能 
3. 使用的 hello[分割資料][ split]模組 (具有*相對運算式*模式) toodivide hello 資料 hello 相同訓練資料集，為 「 已在 Excel 中已完成 
4. 實驗 hello[線性迴歸][ linear-regression]模組 （只有預設選項），記載，並比較 hello 結果 tooour Excel 迴歸模型

### <a name="review-initial-results"></a>檢閱初步結果
首先，hello Excel 模型清楚的效能勝過 hello Machine Learning Studio 模型： 

|  | Excel | Studio |
| --- |:---:|:---:|
| 效能 | | |
| <ul style="list-style-type: none;"><li>調整 R 平方</li></ul> |0.96 |N/A |
| <ul style="list-style-type: none;"><li>決定 <br />係數</li></ul> |N/A |0.78<br />(低度精確度) |
| 平均絕對誤差 |$9.5M |$ 19.4M |
| 平均絕對誤差 (%) |6.03% |12.2% |

當我們執行我們的程序和結果的 hello 開發人員和資料科學家 hello Machine Learning 小組時，他們快速提供實用秘訣。 

* 當您使用 hello[線性迴歸][ linear-regression] Machine Learning Studio 中的模組，提供兩種方法：
  * 線上梯度下降：可能比較適合較大規模的問題
  * 普通最小平方： 這是當它們聽到線性迴歸大部分的人想到的 hello 方法。 對於小型資料集，一般最小平方是較佳的選擇。
* 請考慮調整 hello L2 正則化權數參數 tooimprove 效能。 依預設，它會設 too0.001 但我們的小型資料集我們設 too0.005 tooimprove 效能。 

### <a name="mystery-solved"></a>謎題解開了！
當我們套用 hello 建議時，我們所達成 hello 與 Excel 相同 Machine Learning Studio 中的基準效能： 

|  | Excel | Studio (最初) | Studio (最小平方法) |
| --- |:---:|:---:|:---:|
| 加上標籤的值 |實際值 (數值) |相同 |相同 |
| 學習模組 |Excel -> 資料分析 -> 迴歸 |線性迴歸。 |線性迴歸 |
| 學習模組選項 |N/A |預設值 |普通最小平方<br />L2 = 0.005 |
| 資料集 |26 個資料列，3 個功能，1 個標籤。 全部數值。 |相同 |相同 |
| 分割：訓練 |Excel hello 定型先 18 個資料列，測試 hello 最後 8 個資料列。 |相同 |相同 |
| 分割：測試 |Excel 迴歸公式套用 toohello 最後 8 個資料列 |相同 |相同 |
| **效能** | | | |
| 調整 R 平方 |0.96 |N/A | |
| 決定係數 |N/A |0.78 |0.952049 |
| 平均絕對誤差 |$9.5M |$ 19.4M |$9.5M |
| 平均絕對誤差 (%) |<span style="background-color: 00FF00;"> 6.03%</span> |12.2% |<span style="background-color: 00FF00;"> 6.03%</span> |

此外，hello Excel 係數也比較 toohello hello Azure 定型的模型中的特徵權數：

|  | Excel 係數 | Azure 功能加權 |
| --- |:---:|:---:|
| 截距/偏差 |19470209.88 |19328500 |
| 功能 A |0.832653063 |0.834156 |
| 功能 B |11071967.08 |11007300 |
| 功能 C |25383318.09 |25140800 |

## <a name="next-steps"></a>後續步驟
我們想在 Excel 內 tooconsume hello 機器學習 web 服務。 我們的商務分析師所需方式 toocall hello 機器學習 web 服務的 Excel 資料的資料列，並讓它傳回依賴 Excel 和我們 hello 預測值 tooExcel。 

我們也想 toooptimize 我們的模型中，使用 hello 選項和 Machine Learning Studio 中可用的演算法。

### <a name="integration-with-excel"></a>與 Excel 整合
我們的解決方案是的 toooperationalize 我們的機器學習迴歸模型所建立的 web 服務從 hello 定型的模型。 在幾分鐘的時間內建立 hello web 服務，我們可以呼叫它直接從 Excel tooreturn 營收預測的值。 

hello *Web Services 儀表板*區段包括可下載的 Excel 活頁簿。 hello 活頁簿隨附預先格式化 hello web 服務應用程式開發介面和結構描述資訊內嵌。 當您按一下*下載 Excel 活頁簿*hello 活頁簿隨即開啟，您可以將它儲存 tooyour 本機電腦。 

![][1]

與 hello 活頁簿開啟，請將預先定義的參數複製到藍色 hello 參數區段，如下所示。 輸入 hello 參數，一旦 toohello 機器學習 web 服務會呼叫 Excel 而且 hello 預測計分的標籤會顯示於 hello 綠色預測值 」 一節。 hello 活頁簿將會繼續 toocreate 預測參數根據定型模型的輸入參數的所有資料列項目。 如需有關如何 toouse 這項功能的詳細資訊，請參閱[取用 Azure Machine Learning Web 服務從 Excel](machine-learning-consuming-from-excel.md)。 

![][2]

### <a name="optimization-and-further-experiments"></a>最佳化及進一步實驗
既然我們已經基準與我們的 Excel 模型中，我們會將預先 toooptimize 移我們的機器學習線性迴歸模型。 我們使用 hello 模組[篩選器為基礎的特徵選取][ filter-based-feature-selection] tooimprove 我們選取初始資料元素，它可協助我們 4.6%的效能改善平均絕對誤差。 為未來的專案中，我們將使用這項功能可以儲存我們週在逐一查看資料屬性 toofind hello 的一組正確功能 toouse 的模型。 

接下來我們計劃 tooinclude 其他演算法，例如[Bayesian] [ bayesian-linear-regression]或[促進式決策樹][ boosted-decision-tree-regression]我們實驗 toocompare 中效能。 

如果您想與迴歸 tooexperiment，良好的資料集 tootry 是 hello 能源效率迴歸範例資料集，其中包含多個數值的屬性。 hello 資料集是依現狀 hello Machine Learning Studio 中的範例資料集的一部分。 您可以使用各種不同的學習模組 toopredict 加熱負載或冷卻負載。 hello 圖是針對 hello 電源效率的資料集預測的 hello 目標變數的冷卻負載的效能比較不同的迴歸學習： 

| 模型 | 平均絕對誤差 | 均方根誤差 | 相對絕對誤差 | 相對平方誤差 | 決定係數 |
| --- | --- | --- | --- | --- | --- |
| 推進式決策樹 |0.930113 |1.4239 |0.106647 |0.021662 |0.978338 |
| 線性迴歸 (梯度下降) |2.035693 |2.98006 |0.233414 |0.094881 |0.905119 |
| 類神經網路迴歸 |1.548195 |2.114617 |0.177517 |0.047774 |0.952226 |
| 線性迴歸 (一般最小平方) |1.428273 |1.984461 |0.163767 |0.042074 |0.957926 |

## <a name="key-takeaways"></a>重要心得
我們從並行執行 Excel 迴歸和 Azure Machine Learning 實驗中學到很多。 在 Excel 和比較 toomodels 使用機器學習中的建立 hello 基準模型[線性迴歸][ linear-regression]幫助我們了解 Azure Machine Learning 中，以及我們發現機會 tooimprove 資料選取項目和模型的效能。 

我們也會發現，則建議您 toouse[篩選器為基礎的特徵選取][ filter-based-feature-selection] tooaccelerate 未來的預測專案。 藉由套用功能選取項目 tooyour 資料，您可以建立在機器學習中改良的模型，整體效能更佳。 

hello 能力 tootransfer hello 預測分析 systemically 預測從 Machine Learning tooExcel 允許大幅增加在 hello 能力 toosuccessfully 中提供的結果 tooa 廣泛商務使用者對象。 

## <a name="resources"></a>資源
以下是一些可幫助您處理迴歸的資源： 

* Excel 中的迴歸。 如果您未曾使用 Excel 中的迴歸，本教學課程可讓它變得容易： [http://www.excel-easy.com/examples/regression.html](http://www.excel-easy.com/examples/regression.html)
* 迴歸與預測。 Tyler Chessman 撰寫部落格文章說明如何 toodo 時間序列預測在 Excel 中，其中包含的線性迴歸的良好初級開發人員描述。 [http://sqlmag.com/sql-server-analysis-services/understanding-time-series-forecasting-concepts](http://sqlmag.com/sql-server-analysis-services/understanding-time-series-forecasting-concepts) 
* 一般最小平方線性迴歸：缺點、問題和陷阱。 迴歸的簡介和討論： [http://www.clockbackward.com/2009/06/18/ordinary-least-squares-linear-regression-flaws-problems-and-pitfalls/ ](http://www.clockbackward.com/2009/06/18/ordinary-least-squares-linear-regression-flaws-problems-and-pitfalls/)

[1]: ./media/machine-learning-linear-regression-in-azure/machine-learning-linear-regression-in-azure-1.png
[2]: ./media/machine-learning-linear-regression-in-azure/machine-learning-linear-regression-in-azure-2.png


<!-- Module References -->
[bayesian-linear-regression]: https://msdn.microsoft.com/library/azure/ee12de50-2b34-4145-aec0-23e0485da308/
[boosted-decision-tree-regression]: https://msdn.microsoft.com/library/azure/0207d252-6c41-4c77-84c3-73bdf1ac5960/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

