---
title: "aaaDebug Azure 機器學習的模型 |Microsoft 文件"
description: "如何 toodebug 錯誤所產生的模型定型和計分模型 Azure Machine Learning 中的模組。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 629dc45e-ac1e-4b7d-b120-08813dc448be
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bradsev;garye
ms.openlocfilehash: ee38ca8ce38d4fc7add5ba70c80ab9bb2ceaf1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a>在 Azure Machine Learning 中為模型偵錯

本文說明原因是下列兩個失敗的 hello，可能會發生時執行模型的 hello 潛在原因：

* hello[定型模型][ train-model]模組產生的錯誤 
* hello[計分模型][ score-model]模組會產生不正確的結果 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a>定型模型模組產生錯誤

![image1](./media/machine-learning-debug-models/train_model-1.png)

hello[定型模型][ train-model]模組必須要有兩個輸入：

1. 機器學習模型提供的 Azure 機器學習模型 hello 集合中的 hello 型別。
2. hello 與指定的標籤資料行指定定型資料 hello 變數 toopredict （hello 其他資料行假定 toobe 功能）。

此模組可能會產生錯誤在下列情況下的 hello:

1. hello 標籤資料行指定不正確。 這種情況 hello 標籤以選取多個資料行或不正確的資料行索引。 例如，如果 30 的資料行索引搭配具有只有 25 的資料行的輸入資料集，會套用 hello 第二個案例。

2. hello dataset 不含任何特徵資料行。 例如，如果 hello 輸入資料集有一個資料行，已標示為 hello 標籤資料行，有哪些 toobuild hello 模型沒有功能。 在此情況下，hello[定型模型][ train-model]模組會產生錯誤。

3. hello 輸入資料集 （功能或標籤） 包含無限大值。

## <a name="score-model-module-produces-incorrect-results"></a>計分模型模組產生不正確的結果

![image2](./media/machine-learning-debug-models/train_test-2.png)

在受監督的學習一般定型/測試的實驗，hello[分割資料][ split]模組 hello 原始資料集分成兩個部分： 其中一個部分是使用的 tootrain hello 模型，而且是一個組件tooscore 程度 hello 定型的模型執行。 然後使用的 tooscore hello 測試資料，在其後 hello 結果會評估的 toodetermine hello 模型精確度的 hello hello 定型的模型。

hello[計分模型][ score-model]模組需要兩個輸入：

1. Hello 定型的模型輸出[定型模型][ train-model]模組。
2. 不同於 hello 資料集的計分資料集使用 tootrain hello 模型。

它的可能在即使 hello 試驗成功，hello[計分模型][ score-model]模組會產生不正確的結果。 幾個案例可能會造成這個 toohappen:

1. 如果 hello 指定標籤是類別，而的 hello 資料來定型迴歸模型，會產生不正確的輸出的 hello[計分模型][ score-model]模組。 這是因為迴歸需要持需回應變數。 在此情況下，將更適合 toouse 分類模型。 

2. 同樣地，如果分類模型已擁有 hello 標籤資料行中浮點數的資料集進行定型，它可能會產生非預期的結果。 這是因為分類需要離散回應變數，該變數僅允許涉及一組有限且通常比較小的類別的值。

3. 如果 hello 計分資料集不包含所有 hello 所使用的功能 tootrain hello 模型，hello[計分模型][ score-model]會產生錯誤。

4. 如果中 hello 計分資料集的資料列包含遺漏值或任何其功能的無限值，hello[計分模型][ score-model]將不會產生任何輸出對應 toothat 資料列。

5. hello[計分模型][ score-model]可能會產生相同的 hello 計分資料集的所有資料列的輸出。 這可能發生，例如，在嘗試使用決策樹系，如果選擇可用的定型範例的 toobe 多個 hello 數目，則 hello 的每個分葉節點的樣本數目下限的分類。

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

