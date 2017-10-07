---
title: "aaaOptimize 您在 Azure Machine Learning 中的演算法 |Microsoft 文件"
description: "說明如何 toochoose hello 最佳參數設定的 Azure Machine Learning 中的演算法。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6717e30e-b8d8-4cc1-ad0b-1d4727928d32
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: fbf2f71abdbce19483fb048d67a39cbb368a928e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="choose-parameters-toooptimize-your-algorithms-in-azure-machine-learning"></a>Azure Machine Learning 中選擇您的演算法參數 toooptimize
本主題描述如何 toochoose hello 右 hyperparameter 設定 Azure 機器學習演算法。 大部分的機器學習演算法有參數 tooset。 當定型模型時，您會需要這些參數的 tooprovide 值。 hello 效用 hello 定型的模型取決於您選擇的 hello 模型參數。 hello 尋找 hello 最佳參數集的程序稱為*模型選取*。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

有各種方式 toodo 模型選取項目。 在 machine learning 中，交叉驗證是最常使用的 hello 方法的模型選取項目，而且 hello 預設模型在 Azure 機器學習的選取範圍機制。 由於 Azure Machine Learning 支援 R 和 Python 兩者，因此您一律可以使用 R 或 Python 來實作其自己的模型選擇機制。

尋找 hello 最佳參數集的 hello 程序有四個步驟：

1. **定義 hello 參數空間**: hello 的演算法，請先決定您希望 tooconsider hello 確切的參數值。
2. **定義 hello 交叉驗證設定**： 決定如何 toochoose 交叉驗證摺疊 hello 資料集。
3. **定義 hello 度量**： 決定哪些度量 toouse 判斷 hello 一組最佳的參數，例如精確度，均方根平方錯誤、 有效位數、 選出或 f 分數。
4. **定型、 評估並比較**: hello 參數值的每一個唯一組合，交叉驗證是由執行，並根據您定義的 hello 錯誤度量。 評估和比較之後, 您可以選擇 hello 效能最佳模型。

下列映像的 hello 說明如何達成這在 Azure Machine Learning 中的顯示。

![尋找 hello 最佳參數集](./media/machine-learning-algorithm-parameters-optimize/fig1.png)

## <a name="define-hello-parameter-space"></a>定義 hello 參數空間
您可以定義在 hello 模型初始化步驟設定 hello 參數。 hello 的所有機器學習演算法參數] 窗格有兩種定型模式：*單一參數*和*參數範圍*。 選擇 [參數範圍] 模式。 在參數範圍模式中，您可以針對每個參數輸入多個值。 您可以在 hello] 文字方塊中輸入以逗號分隔值。

![二元促進式決策樹，單一參數](./media/machine-learning-algorithm-parameters-optimize/fig2.png)

 或者，您可以定義 hello hello 格線和 hello 總數點 toobe 使用產生的最大和最小點**使用範圍產生器**。 根據預設，會產生線性標尺上的 hello 參數值。 但是如果**對數刻度**勾選，hello 值會產生 hello 對數刻度 （也就是 hello 相鄰點的 hello 比例是常數，而不是差異）。 對於整數參數，您可以使用連字號來定義範圍。 例如，"1-10"表示，介於 1 到 10 之間的所有整數 （兩者內含） 形成 hello 參數集。 也支援使用混合的模式。 比方說，hello 參數集"1-10、 20、 50"會加入整數 1-10、 20 到 50 個。

![二元促進式決策樹，參數範圍](./media/machine-learning-algorithm-parameters-optimize/fig3.png)

## <a name="define-cross-validation-folds"></a>定義交叉驗證折數
hello[資料分割和取樣][ partition-and-sample]模組可以是使用的 toorandomly 指派摺疊 toohello 資料。 在下列範例組態 hello 模組 hello，我們會定義五個摺疊，並隨機指派摺疊數字 toohello 範例執行個體。

![資料分割和取樣](./media/machine-learning-algorithm-parameters-optimize/fig4.png)

## <a name="define-hello-metric"></a>定義 hello 度量
hello[微調模型超][ tune-model-hyperparameters]模組提供實證選擇 hello 參數指定的演算法和資料集的一組最佳的支援。 此外訓練 hello tooother 資訊模型，hello**屬性**本單元的窗格包含決定最佳參數集 hello hello 度量。 分類和迴歸演算法分別有兩個不同的下拉式清單方塊。 如果列入考量的 hello 演算法是一種分類演算法，就會忽略 hello 迴歸度量，反之亦然。 在此特定範例中，是 hello 度量**精確度**。   

![掃掠參數](./media/machine-learning-algorithm-parameters-optimize/fig5.png)

## <a name="train-evaluate-and-compare"></a>訓練、評估和比較
hello 相同[微調模型超][ tune-model-hyperparameters]模組來定型，對應 toohello 參數集，會評估各種標準，然後建立 hello 自動定型的模型，根據 hello 所有 hello 模型您選擇的度量。 此模組有兩個必要的輸入項：

* hello 未定型的學習模組
* hello 資料集

hello 模組也有選擇性輸入資料集。 摺疊資訊 toohello 強制的資料集輸入具有連接 hello 資料集。 如果 hello 資料集未指派任何摺疊的資訊，然後 10 個摺疊的交叉驗證會自動執行的預設值。 如果不是 hello 摺疊指派 hello 選擇性資料集連接埠所提供的驗證資料集，然後選擇定型測試模式並 hello 第一個資料集是使用的 tootrain hello 模型，每一個參數組合。

![推進式決策樹分類器](./media/machine-learning-algorithm-parameters-optimize/fig6a.png)

hello 模型會再評估 hello 驗證資料集。 hello 留待 hello 模組顯示的輸出連接埠不同的度量資訊的參數值的函式。 hello 右輸出連接埠提供 hello 定型的模型對應 toohello 效能最佳的模型，根據 toohello 選擇公制 (**精確度**在此情況下)。  

![驗證資料集](./media/machine-learning-algorithm-parameters-optimize/fig6b.png)

您可以看到 hello 精確參數選擇的視覺化 hello 右輸出連接埠。 此模型在儲存為訓練過的模型之後，可用來對測試集計分，或者用在可運作的 Web 服務。

<!-- Module References -->
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[tune-model-hyperparameters]: https://msdn.microsoft.com/library/azure/038d91b6-c2f2-42a1-9215-1f2c20ed1b40/
