---
title: "Azure Machine Learning Studio 中的 aaaCreate 文字分析模型 |Microsoft 文件"
description: "在 Azure Machine Learning Studio 模組對文字的前置處理、 N 字母組或使用特徵雜湊 toocreate 文字分析模型的方式"
services: machine-learning
documentationcenter: 
author: rastala
manager: jhubbard
editor: 
ms.assetid: 08cd6723-3ae6-4e99-a924-e650942e461b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: roastala
ms.openlocfilehash: e3799f37ba54bb2ec8815ecf5ed34e145ffb20e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-text-analytics-models-in-azure-machine-learning-studio"></a>在 Azure Machine Learning Studio 中建立文字分析模型
您可以使用 Azure Machine Learning toobuild 並實施文字分析模型。 這些模型可協助您解決問題，例如，文件分類或情緒分析問題。

在文字分析實驗中，您通常需要︰

1. 清理和前置處理文字資料集
2. 從已前置處理的文字擷取數值特徵向量
3. 定型分類或迴歸模型
4. 計分，並驗證 hello 模型
5. 部署 hello 模型 tooproduction

在此教學課程中，當我們使用「Amazon 書籍評論」資料集逐步解說情緒分析模型時，您會學到這些步驟 (請參閱研究報告 “Biographies, Bollywood, Boom-boxes and Blenders: Domain Adaptation for Sentiment Classification”，作者：Association of Computational Linguistics (ACL) 的 John Blitzer、Mark Dredze 和 Fernando Pereira，2007 年)。此資料集是由評論分數 (1-2 或 4-5) 和自由格式文字所組成。 hello 的目標是 toopredict hello 檢閱分數： 低 (1-2） 或 high (4-5)。

您可以在 Cortana Intelligence Gallery 找到本教學課程中涵蓋的實驗︰

[預測書籍評論](https://gallery.cortanaintelligence.com/Experiment/Predict-Book-Reviews-1)

[預測書籍評論 - 預測性實驗](https://gallery.cortanaintelligence.com/Experiment/Predict-Book-Reviews-Predictive-Experiment-1)

## <a name="step-1-clean-and-preprocess-text-dataset"></a>步驟 1：清理和前置處理文字資料集
我們先 hello 實驗將 hello 檢閱分數分割成兩個類別分類的類別低和高的值區 tooformulate hello 問題。 我們使用[編輯中繼資料](https://msdn.microsoft.com/library/azure/dn905986.aspx)和[群組類別值](https://msdn.microsoft.com/library/azure/dn906014.aspx)模組。

![建立標籤](./media/machine-learning-text-analytics-module-tutorial/create-label.png)

然後，我們可以清除 hello 文字使用[前置處理文字](https://msdn.microsoft.com/library/azure/mt762915.aspx)模組。 hello 清除可減少 hello 資料集中的 hello 雜訊，可協助您找出 hello 最重要的功能，並改善 hello hello 最終模型的精確度。 我們會移除停用字詞 (例如 "the" 或 "a" 等常見單字)、數字、特殊字元、重複字元、電子郵件地址和 URL。 我們也轉換 hello 文字 toolowercase、 lemmatize hello 文字的方式，以及偵測句子界限，然後以"| | |"符號，以預先處理過的文字。

![前置處理文字](./media/machine-learning-text-analytics-module-tutorial/preprocess-text.png)

如果您想 toouse 自訂停用字詞的清單？ 您可以將它傳入做為選擇性的輸入。 您也可以使用自訂 C# 語法規則運算式 tooreplace 子字串，並移除文字的一部份： 名詞、 動詞或形容詞。

Hello 前置處理完成之後，我們將 hello 資料分割成定型和測試集。

## <a name="step-2-extract-numeric-feature-vectors-from-pre-processed-text"></a>步驟 2：從已前置處理的文字擷取數值特徵向量
toobuild 文字資料的模型，您通常有 tooconvert 自由格式文字插入數字特徵向量。 在此範例中，我們使用[從文字擷取 N 字母組功能](https://msdn.microsoft.com/library/azure/mt762916.aspx)模組 tootransform hello 文字資料 toosuch 格式。 此模組會採用以空格分隔單字的資料行，並計算出現在您資料集中的單字字典或單字的 N-Gram。 然後，它會計算每個單字或 N-Gram 出現在每筆記錄的次數，並從這些計數建立特徵向量。 在本教學課程中，我們會設定 N 字母組大小 too2，因此我們特徵向量包括單字和句子的兩個後續。

![擷取 N-Gram](./media/machine-learning-text-analytics-module-tutorial/extract-ngrams.png)

我們套用 TF * 加權 tooN 字母組 IDF （詞彙頻率反向文件頻率） 計算。 這種方式新增之單字的單一記錄中經常出現，但 hello 整個資料集很少的權重。 其他選項包括二進位、TF 及圖形加權。

這類文字特徵通常具有高維度。 比方說，如果您的語言資料庫有 100,000 個唯一的單字，特徵空間會有 100,000 個維度，或使用更多的 N-Gram。 hello 擷取 N 字母組功能模組會提供一組選項 tooreduce hello 維度性。 您可以選擇 tooexclude 字詞是短或長或太常見或太頻繁 toohave 重要的預測值。 在本教學課程中，我們會排除出現在少於 5 筆記錄或超過 80% 的記錄的 N-Gram。

此外，您可以使用相互關聯的 hello 最這些功能的功能選取項目 tooselect 預測目標。 我們使用卡方功能選取項目 tooselect 1000 功能。 您可以檢視所選的字詞或 N 字母組的 hello 詞彙擷取 N 字母組模組 hello 正確輸出，即可。

替代方法 toousing 擷取 N 字母組功能，您可以使用特徵雜湊模組。 但請注意， [特徵雜湊](https://msdn.microsoft.com/library/azure/dn906018.aspx) 沒有內建的特徵選取功能或 TF*IDF 加權。

## <a name="step-3-train-classification-or-regression-model"></a>步驟 3：定型分類或迴歸模型
現在的 hello 文字已轉換的 toonumeric 特徵資料行。 hello 資料集仍然包含字串資料行，從上一個階段，因此我們使用選取的資料行中資料集 tooexclude 它們。

然後使用[二級羅吉斯迴歸](https://msdn.microsoft.com/library/azure/dn905994.aspx)toopredict 我們的目標： 高或過低的檢閱分數。 此時，hello 文字分析問題已轉換成一般分類問題。 您可以使用 Azure Machine Learning tooimprove hello 模型中可用的 hello 工具。 比方說，您可以試驗不同的分類器 toofind 出如何精確的結果所提供，或使用 hyperparameter 微調 tooimprove hello 精確度。

![定型和評分](./media/machine-learning-text-analytics-module-tutorial/scoring-text.png)

## <a name="step-4-score-and-validate-hello-model"></a>步驟 4： 計分，並驗證 hello 模型
如何驗證 hello 定型的模型？ 我們針對 hello 測試資料集評分它，並評估 hello 精確度。 不過，hello 模型學到 N 字母組和其加權 hello 定型資料集從 hello 的詞彙。 因此，我們應該使用該詞彙和這些加權時重新擷取功能，從 測試資料，做為相對於 toocreating hello 詞彙。 因此，我們加入擷取 N 字母組功能模組 toohello 計分實驗 hello 分支、 從定型分支連接 hello 輸出詞彙及 tooread 僅設定 hello 詞彙模式。 我們也會停用 hello 篩選 N 字母組頻率設定 hello too1 最小執行個體和最大 too100%並關閉 hello 特徵選取。

Hello 資料已經過的測試中的文字資料行轉換 toonumeric 特徵資料行之後，我們會排除資料行，從上一個階段喜歡訓練分支中的 hello 字串。 然後我們使用分數模型模組 toomake 預測和評估模型模組 tooevaluate hello 精確度。

## <a name="step-5-deploy-hello-model-tooproduction"></a>步驟 5： 部署的 hello 模型 tooproduction
部署就緒 toobe tooproduction hello 模型。 部署為 Web 服務時，它會採用自由格式的文字字串做為輸入，並傳回「高」或「低」的預測。 它使用學到的 hello N 字母組詞彙 tootransform hello 文字 toofeatures，，並訓練羅吉斯迴歸模型 toomake 從這些功能的預測。 

tooset 向上 hello 預測實驗，我們先儲存 hello N 字母組詞彙做為資料集，並 hello 定型 hello 訓練分支的 hello 實驗羅吉斯迴歸模型。 然後，我們將儲存 hello 實驗使用 另存新檔 」 toocreate 預測實驗實驗圖形。 我們從 hello 實驗移除 hello 分割資料的模組和 hello 訓練分支。 我們再連接先前儲存的 hello N 字母組詞彙和模型 tooExtract N 字母組功能分數模型模組分別。 我們也會移除 hello 評估模型 」 模組。

我們之前前置處理文字模組 tooremove hello 的標籤資料行的資料集模組中插入選取的資料行，並取消選取分數模組中的 「 附加分數資料行 toodataset 」 選項。 這樣一來，hello web 服務不要求它正嘗試 toopredict，並不回應 hello 輸入的功能，以回應 hello 標籤。

![預測性實驗](./media/machine-learning-text-analytics-module-tutorial/predictive-text.png)

現在我們有一個實驗可以發行為 Web 服務，並使用要求-回應或批次執行 API 進行呼叫。

## <a name="next-steps"></a>後續步驟
從 [MSDN 文件](https://msdn.microsoft.com/library/azure/dn905886.aspx)深入了解文字分析模組。

