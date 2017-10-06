---
title: "aaaHow tooprepare Azure Machine Learning Studio 中的部署模型 |Microsoft 文件"
description: "如何 tooprepare 您定型的模型部署為 web 服務藉由轉換 Machine Learning Studio 定型實驗 tooa 預測實驗。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: eb943c45-541a-401d-844a-c3337de82da6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: garye
ms.openlocfilehash: d25bc68be63679a803bfc24a9e29e009a9263f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprepare-your-model-for-deployment-in-azure-machine-learning-studio"></a>如何 tooprepare Azure Machine Learning Studio 中的部署模型

Azure Machine Learning Studio 提供下列 hello 需要 toodevelop 預測性分析工具模型，並再將它部署為 Azure web 服務實施它。

toodo，使用 Studio toocreate 實驗-呼叫*定型實驗*-您訓練、 分數，並編輯您的模型。 一旦您滿意，您會取得您模型就緒 toodeploy 轉換您定型實驗 tooa*預測實驗*，已設定 tooscore 使用者資料。

如需此程序的範例，請參閱[逐步解說：在 Azure Machine Learning 中為信用風險評估開發預測分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)。

本文會深入探討如何定型實驗回轉換成預測實驗中，以及如何部署該預測實驗 hello 詳細資料。 了解這些詳細資料，您可以了解如何 tooconfigure 已部署的模型 toomake 它更有效率。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a>概觀 

轉換定型實驗 tooa 預測實驗的 hello 程序和三個步驟：

1. 取代 hello 機器學習演算法模組中使用定型的模型。
2. 修剪 hello 實驗 tooonly 計分所需的模組。 定型實驗包含之模組的所需的訓練，但不是需要用 hello 模型已定型之後的數字。
3. 定義模型如何接受資料的 hello web 服務使用者，而且不會傳回哪些資料。

> [!TIP]
> 在訓練實驗中，您曾考慮使用您自己的資料來訓練和評分模型。 但是，一旦部署之後，使用者會傳送新的資料 tooyour 模型，且會傳回預測結果。 因此，您將轉換它準備好要部署您定型實驗 tooa 預測實驗 tooget，請記住 hello 模型如何使用其他人。
> 
> 

## <a name="set-up-web-service-button"></a>設定 Web 服務按鈕
執行實驗之後 (按一下**執行**在 hello hello 實驗畫布底部)，按一下 hello**設定 Web 服務**按鈕 (選取 hello**預測 Web 服務**選項）。 **設定 Web 服務**的 hello 轉換定型實驗 tooa 預測實驗的三個步驟執行：

1. 它會將定型的模型儲存在 hello**定型的模型**hello 模組調色盤 （toohello hello 實驗畫布左邊） 一節。 然後它會取代 hello 機器學習演算法和[定型模型][ train-model]以 hello 儲存模組來定型模型。
2. 它會分析您的實驗，並移除已清楚僅用於定型且不再需要的模組。
3. 它會將 _Web 服務輸入_和_輸出_模組插入實驗中的預設位置 (這些模組會接受並傳回使用者資料)。

例如，下列 hello 體驗火車二級促進式的決策樹模型中使用範例人口普查資料：

![訓練實驗][figure1]

在這項實驗 hello 模組執行基本上四個不同的功能：

![模組功能][figure2]

當您轉換這個定型實驗 tooa 預測實驗時，不再需要這些模組的某些，或它們現在有不同用途：

* **資料**-在此範例資料集中的 hello 資料不用於計分-hello hello web 服務的使用者將會提供 hello 資料 toobe 計分。 不過，此資料集，例如資料類型中的 hello 中繼資料會使用 hello 定型的模型。 因此，讓它可提供此中繼資料，您必須在 hello 預測實驗 tookeep hello 資料集。

* **準備**-根據將立即送出計分，這些模組可能會或可能不是必要的 tooprocess hello 內送資料的 hello 使用者資料。 hello**設定 Web 服務**按鈕不會修改這些-您必須 toodecide 方式 toohandle 它們。
  
    比方說，在此範例中 hello 範例資料集可能會有遺漏的值，因此[清除遺漏資料][ clean-missing-data]模組已包含的 toodeal 它們。 此外，hello 範例資料集包含不需要的 tootrain hello 模型資料行。 因此[資料集中選取的資料行][ select-columns]模組已包含的 tooexclude 這些額外的資料行從 hello 資料流程。 如果您知道該 hello 資料會提交計分 hello 透過 web 服務並不會遺漏的值，則您可以移除 hello[清除遺漏資料][ clean-missing-data]模組。 不過，由於 hello[資料集中選取的資料行][ select-columns]模組可協助定義 hello 資料行的資料該 hello 定型的模型預期，該模組必須 tooremain。

* **定型**-這些模組會使用的 tootrain hello 模型。 當您按一下**設定 Web 服務**，這些模組都會取代成單一模組包含 hello 假設您在定型的模型。 這個新模組會儲存在 hello**定型的模型**hello 模組調色盤的區段。

* **分數**-在此範例中，hello[分割資料][ split]模組是使用的 toodivide hello 資料流到測試資料及定型資料。 在 hello 預測實驗中，我們正在不定型集失效，因此[分割資料][ split]可以移除。 同樣地，第二個 hello[計分模型][ score-model]模組和 hello[評估模型][ evaluate-model]模組會使用的 toocompare hello 測試結果資料，因此這些模組不需要在 hello 預測實驗。 hello 剩餘[計分模型][ score-model]模組，不過，是需要的 tooreturn 分數的結果，透過 hello web 服務。

以下是按一下 [設定 Web 服務] 之後，我們的範例外觀：

![已轉換的預測實驗][figure3]

hello 完成之工作**設定 Web 服務**可能是您部署為 web 服務的實驗 toobe 足夠 tooprepare。 不過，您可能想 toodo 某些額外的工作特定 tooyour 實驗。

### <a name="adjust-input-and-output-modules"></a>調整輸入和輸出模組
在定型實驗中，使用一組定型資料，有些處理 tooget 然後未 hello hello 機器學習演算法需要表單中的資料。 如果您預期 tooreceive 透過 hello web 服務的 hello 資料將不需要這項處理，您可以略過它： hello hello 輸出連接**Web 服務輸入的模組**tooa 不同的模組，在您實驗中。 hello 模型，在這個位置現在會到達 hello 使用者資料。

例如，根據預設**設定 Web 服務**置於 hello **Web 服務輸入**頂端 hello 資料流程，hello 上圖所示的模組。 但是我們可以手動將放 hello **Web 服務輸入**過去 hello 資料處理模組：

![移動 hello web 服務輸出][figure4]

提供透過 hello web 服務現在會傳遞直接在 hello 分數模型模組沒有任何前置處理資料輸入 hello。

同樣地，根據預設**設定 Web 服務**置於 hello 底部 hello 資料流量的 Web 服務輸出模組。 在此範例中，hello web 服務將傳回的 hello toohello 使用者 hello 輸出[計分模型][ score-model]模組，其包含 hello 完整的輸入的資料向量加上 hello 計分結果。
不過，如果您想使用 tooreturn 不同項目，然後您可以加入其他模組之前 hello **Web 服務輸出**模組。 

Tooreturn 只有 hello 計分結果不 hello 整個向量的輸入資料，例如，加入[資料集中選取的資料行][ select-columns]模組 tooexclude 以外的所有資料行 hello 計分結果。 然後移動 hello **Web 服務輸出**模組 toohello 輸出的 hello[資料集中選取的資料行][ select-columns]模組。 hello 實驗看起來像這樣：

![移動 hello web 服務輸出][figure5]

### <a name="add-or-remove-additional-data-processing-modules"></a>新增或移除其他資料處理模組
如果在您的實驗中還有您知道在評分期間不需要的模組，則可以移除這些模組。 例如，由於我們移動 hello **Web 服務輸入**模組 tooa 點之後 hello 資料處理模組，我們可以移除 hello[清除遺漏資料][ clean-missing-data]從模組hello 預測實驗。

我們的預測實驗現在看起來像這樣：

![移除額外的模組][figure6]


### <a name="add-optional-web-service-parameters"></a>新增選用的 Web 服務參數
在某些情況下，您可能想 tooallow hello 使用者的您的 web 服務 toochange hello 行為的模組存取 hello 服務時。 *Web 服務參數*toodo 可讓您這。

常見的範例設定[匯入資料][ import-data]模組，因此 hello hello 使用者部署 web 服務存取 hello web 服務時，可以指定不同的資料來源。 或者，設定[匯出資料][export-data]模組，以便能夠指定不同的目的地。

您可以定義 Web 服務參數，並使其與一個或多個模組參數產生關聯，而且您可以指定它們是必要還是選用參數。 hello web 服務的 hello 使用者在存取 hello 服務時，並據此修改 hello 模組動作時，會提供這些參數的值。

針對哪些 Web 服務參數的詳細資訊以及如何 toouse 它們，請參閱 <<c0> [ 使用 Azure 機器學習 Web 服務參數][webserviceparameters]。

[webserviceparameters]: machine-learning-web-service-parameters.md


## <a name="deploy-hello-predictive-experiment-as-a-web-service"></a>部署為 web 服務的 hello 預測實驗
既然已充分備妥 hello 預測實驗，您可以將其部署為 Azure web 服務。 使用 hello web 服務，使用者可以傳送資料 tooyour 模型和 hello 模型將會傳回預測。

如需有關 hello 完成部署程序的詳細資訊，請參閱[部署 Azure Machine Learning web 服務][deploy]

[deploy]: machine-learning-publish-a-machine-learning-web-service.md


<!-- Images -->
[figure1]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure1.png
[figure2]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure2.png
[figure3]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure3.png
[figure4]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure4.png
[figure5]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure5.png
[figure6]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure6.png


<!-- Module References -->
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[export-data]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/
