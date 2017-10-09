---
title: "步驟 4： 來定型及評估 hello 預測分析模型 |Microsoft 文件"
description: "步驟 4 中的 hello 開發預測方案逐步解說： 定型，分數，並評估 Azure Machine Learning Studio 中的多個模型。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a>逐步解說步驟 4： 來定型及評估 hello 預測分析的模型
本主題包含 hello hello 逐步解說中，第四個步驟[開發 Azure Machine Learning 中的預測分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)

1. [建立機器學習服務工作區](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [上傳現有資料](machine-learning-walkthrough-2-upload-data.md)
3. [建立新實驗](machine-learning-walkthrough-3-create-new-experiment.md)
4. **來定型及評估 hello 模型**
5. [部署 hello Web 服務](machine-learning-walkthrough-5-publish-web-service.md)
6. [存取 hello Web 服務](machine-learning-walkthrough-6-access-web-service.md)

- - -
建立機器學習模型中使用 Azure Machine Learning Studio hello 優點的其中一個單一的實驗中一次是 hello 能力 tootry 多個模型類型，並比較 hello 結果。 這種類型的實驗，可協助您尋找 hello 最佳解決方案，針對您的問題。

在這個逐步解說中，我們正在開發 hello 實驗中，我們將建立兩個不同類型的模型，然後比較其計分結果 toodecide 哪一個演算法我們想 toouse 我們最後的實驗中。  

有各種不同的模型可供我們選擇。 toosee hello 模型，依序展開 hello **Machine Learning** hello 模組調色盤中的節點，然後展開 **初始化模型**和其下的 hello 節點。 基於 hello 這項實驗中，我們將選取 hello[二級支援向量機器][ two-class-support-vector-machine] (SVM) 和 hello[二級促進式決策樹][two-class-boosted-decision-tree]模組。    

> [!TIP]
> tooget 協助以決定哪一個機器學習演算法最適合您正嘗試 toosolve hello 特定問題，請參閱[如何 toochoose 演算法為 Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md)。
> 
> 

## <a name="train-hello-models"></a>定型的模型 hello

我們會將這兩個 hello[二級促進式決策樹][ two-class-boosted-decision-tree]模組和[二級支援向量機器][ two-class-support-vector-machine]模組在此實驗。

### <a name="two-class-boosted-decision-tree"></a>二元促進式決策樹

首先，接著要設定 hello 促進式決策樹模型。

1. 尋找 hello[二級促進式決策樹][ two-class-boosted-decision-tree] hello 模組調色盤中的模組並將它拖曳到畫布 hello。

2. 尋找 hello[定型模型][ train-model]模組，將它拖曳至 hello 畫布，然後 hello hello 輸出連接[二級促進式決策樹][ two-class-boosted-decision-tree]模組 toohello 左輸入的連接埠的 hello[定型模型][ train-model]模組。
   
   hello[二級促進式決策樹][ two-class-boosted-decision-tree]模組初始化 hello 通用模型 」 和[定型模型][ train-model]使用定型資料tootrain hello 模型。 

3. Hello hello 左邊的左邊的輸出連接[執行 R 指令碼][ execute-r-script]模組 toohello 直接輸入連接埠 hello[定型模型][ train-model] （我們的模組在決定[步驟 3](machine-learning-walkthrough-3-create-new-experiment.md)來自 hello 左邊 hello 分割資料模組來定型此逐步解說 toouse hello 資料)。
   
   > [!TIP]
   > 我們不需要兩個 hello 輸入以及其中一個 hello 輸出的 hello[執行 R 指令碼][ execute-r-script]此實驗，因此我們可以將它們保留未附加的模組。 
   > 
   > 

Hello 實驗的這個部分現在看起來像下面這樣：  

![Training a model][1]

現在，我們必須 tootell hello[定型模型][ train-model]我們想要 hello 模型 toopredict hello 信用風險值的模組。

1. 選取 hello[定型模型][ train-model]模組。 在 hello**屬性** 窗格中，按一下 **啟動資料行選取器**。

2. 在 hello**選取單一資料行** 對話方塊中，輸入 「 信用風險"hello 下搜尋 欄位中**可用的資料行**下方，選取 「 信用風險 」，按一下 hello 向右箭號按鈕 ( **>** ) toomove 「 信用風險 」 太**選取的資料行**。 

    ![選取 hello 定型模型 」 模組的 hello 信用風險資料行][0]

3. 按一下 hello**確定**核取記號。

### <a name="two-class-support-vector-machine"></a>二元支援向量機器

接下來，我們設定 hello SVM 模型。  

首先，簡單說明一下 SVM。 強化的決策樹適合處理任何類型的特性。 不過，由於 hello SVM 模組會產生線性分類器，hello 模型，它會產生有 hello 最佳測試錯誤時數字的所有功能都具有 hello 相同的標尺。 tooconvert 全都是數字相同擴充功能 toohello，我們使用 「 Tanh 」 轉換 (以 hello[標準化資料][ normalize-data]模組)。 這會將我們的數字轉換成 hello [0，1] 範圍中。 hello SVM 模組將轉換字串功能 toocategorical 功能，然後 toobinary 0/1 功能，因此我們不需要 toomanually 轉換字串的功能。 此外，我們不希望 tootransform hello 信用風險資料行 （21）： 它是數值，但它是我們要定型的 hello 值 hello 模型 toopredict，因此我們需要 tooleave 單獨它。  

tooset hello SVM 模型，請勿 hello 遵循：

1. 尋找 hello[二級支援向量機器][ two-class-support-vector-machine] hello 模組調色盤中的模組並將它拖曳到畫布 hello。

2. 以滑鼠右鍵按一下 hello[定型模型][ train-model]模組中，選取**複製**，然後以滑鼠右鍵按一下 hello 畫布，然後選取**貼上**。 hello 副本 hello[定型模型][ train-model]模組有 hello 相同的資料行選取項目為原始的 hello。

3. Hello hello 輸出連接[二級支援向量機器][ two-class-support-vector-machine]模組 toohello 會保留第二個輸入連接埠的 hello[定型模型][ train-model]模組。

4. 尋找 hello[標準化資料][ normalize-data]模組並將它拖曳到畫布 hello。

5. Hello hello 左邊的左邊的輸出連接[執行 R 指令碼][ execute-r-script]模組 toohello 輸入，此模組 （請注意模組 hello 輸出連接埠可能會比另一個模組的連接的 toomore）。

6. 連接保留 hello 輸出連接埠的 hello[標準化資料][ normalize-data]右模組 toohello 第二個輸入連接埠 hello[定型模型][ train-model]模組。

實驗的這部分目前看起來如下：  

![第二個模型的定型 hello][2]  

現在設定 hello[標準化資料][ normalize-data]模組：

1. 按一下 tooselect hello[標準化資料][ normalize-data]模組。 在 hello**屬性**窗格中，選取**Tanh** hello**轉換方法**參數。

2. 按一下**啟動資料行選取器**，選取 「 沒有資料行 」**使用 Begin With**，選取**Include** hello 第一個下拉式清單中選取**資料行類型**在 hello 第二個下拉式清單中，然後選取**數值**hello 第三個下拉式清單中。 這會指定所有 hello 數值資料行 （與唯一的數字） 會都轉換。

3. 按一下 hello 加號 （+） toohello 此資料列的權限-這會建立一個資料列的下拉式清單。 選取**排除**hello 第一個下拉式清單中選取**資料行名稱**在 hello 第二個下拉式清單中，然後輸入 hello 文字欄位中的 「 信用風險 」。 這會指定應該忽略該 hello 信用風險資料行 （我們需要的 toodo 這因為此資料行是數值，所以會轉換如果我們未排除它）。

4. 按一下 hello**確定**核取記號。  

    ![選取的資料行 hello 標準化資料模組][5]

hello[標準化資料][ normalize-data]模組現在會設定 tooperform Tanh 轉換 hello 信用風險資料行以外的所有數值資料行上。  

## <a name="score-and-evaluate-hello-models"></a>計分，並評估 hello 模型

我們使用測試資料的已隔開 hello hello[分割資料][ split]模組 tooscore 我們定型的模型。 然後，我們可以比較 hello 結果的 hello 兩個模型 toosee 產生更好的結果。  

### <a name="add-hello-score-model-modules"></a>加入 hello 分數模型模組

1. 尋找 hello[計分模型][ score-model]模組並將它拖曳到畫布 hello。

2. 連接 hello[定型模型][ train-model]模組已連接 toohello[二級促進式決策樹][ two-class-boosted-decision-tree]模組 toohello 左方的輸入連接埠 hello[計分模型][ score-model]模組。

3. 連接 hello 右邊[執行 R 指令碼][ execute-r-script]模組 （我們測試的資料） toohello 直接輸入連接埠 hello[計分模型][ score-model]模組。

    ![已連接評分模型模組][6]
   
   hello[計分模型][ score-model]模組現在能夠利用 hello 信用資訊從測試資料，執行透過 hello 模型 hello 和比較 hello 預測 hello 模型會產生以實際的 hello 信用風險hello 測試資料中的資料行。

4. 複製並貼上 hello[計分模型][ score-model]模組 toocreate 第二個副本。

5. Hello 輸出 hello SVM 模型連接 (也就是 hello 輸出連接埠的 hello[定型模型][ train-model]連接 toohello 的模組[二級支援向量機器][two-class-support-vector-machine]模組) toohello 第二個輸入連接埠 hello[計分模型][ score-model]模組。

6. Hello SVM 模型，我們有 toodo hello 相同轉換 toohello 測試資料，如同 toohello 定型資料。 因此複製並貼上 hello[標準化資料][ normalize-data]模組 toocreate 第二個複本並將它連接 toohello 右邊[執行 R 指令碼][ execute-r-script]模組。

7. 第二個連接的 hello hello 左的輸出[標準化資料][ normalize-data]右模組 toohello 第二個輸入連接埠 hello[計分模型][ score-model]模組。

    ![已連接兩個評分模型模組][7]

### <a name="add-hello-evaluate-model-module"></a>新增 hello 評估模型模組

tooevaluate hello 兩個計分結果並加以比較，我們使用[評估模型][ evaluate-model]模組。  

1. 尋找 hello[評估模型][ evaluate-model]模組並將它拖曳到畫布 hello。

2. 連接 hello hello 輸出連接埠[計分模型][ score-model] hello 與相關聯的模組促進式決策樹模型 toohello 左輸入連接埠 hello[評估模型][evaluate-model]模組。

3. 連接其他 hello[計分模型][ score-model]模組 toohello 直接輸入連接埠。  

    ![已連接評估模型模組][8]

### <a name="run-hello-experiment-and-check-hello-results"></a>執行 hello 實驗，並檢查 hello 結果

toorun hello 實驗中，按一下 hello**執行**hello 畫布下方的按鈕。 可能需要數分鐘的時間。 旋轉指標上每個模組會顯示正在執行，，和綠色的核取記號然後才顯示完成 hello 模組。 當所有 hello 模組都有核取記號時，hello 實驗已經完成執行。

hello 實驗現在看起來應該像下面這樣：  

![Evaluating both models][3]

toocheck hello 結果中按一下輸出連接埠 hello hello[評估模型][ evaluate-model]模組，然後選取**視覺化**。  

hello[評估模型][ evaluate-model]模組會產生一對曲線和 toocompare hello 結果的 hello 兩個計分模型可讓您的度量。 您可以檢視為接收者運算子特性 (ROC) 曲線、 重新叫用精確度/曲線或增益曲線 hello 結果。 顯示的其他資料包括混淆矩陣、 hello 曲線 (AUC)，底下的 hello 區域的累計值和其他度量。 您可以向左或向右移動的 hello 滑桿來變更 hello 臨界值，並查看它如何影響 hello 組度量。  

toohello hello 圖形的右邊按一下**評分資料集**或**計分資料集 toocompare** toohighlight hello 關聯的曲線和 toodisplay hello 相關聯的度量下方。 在 hello hello 曲線圖例，"評分資料集 」 對應 toohello 左輸入的連接埠的 hello[評估模型][ evaluate-model]模組-在此案例中，這是 hello 促進式決策樹模型。 「 計分資料集 toocompare 」 對應 toohello 右側輸入連接埠-hello SVM 模型，在我們的案例。 當您按一下其中一個這些標籤時，針對該模型的 hello 曲線會反白顯示，並且顯示 hello 對應度量，hello 下列圖片所示。  

![ROC curves for models][4]

您可以藉由檢查這些值，決定哪一個模型是最接近 toogiving hello 想要的結果。 您可以返回並變更 hello 不同模型中的參數值逐一查看您的經驗。 

hello 科學和解譯這些結果和微調 hello 模型效能的封面是本逐步解說的 hello 範圍外。 如需額外說明，您可能會讀取下列發行項的 hello:
- [Tooevaluate 建立 Azure Machine Learning 中的效能的模型](machine-learning-evaluate-model-performance.md)
- [Azure Machine Learning 中選擇您的演算法參數 toooptimize](machine-learning-algorithm-parameters-optimize.md)
- [在 Azure Machine Learning 中解讀模型結果](machine-learning-interpret-model-results.md)

> [!TIP]
> 每次執行 hello 實驗的該反覆項目記錄會保留在 hello 執行歷程記錄。 您可以檢視這些反覆項目，並傳回 tooany 項目，依序按一下**檢視執行記錄**hello 畫布下方。 您也可以按一下**先前執行**在 hello**屬性**窗格 tooreturn toohello 前面的反覆項目 hello 其中一個已開啟。
> 
> 您可以建立一份實驗任何反覆項目，依序按一下**SAVE AS** hello 畫布下方。 
> 使用 hello 實驗**摘要**和**描述**屬性 tookeep 記錄您已嘗試在您實驗反覆項目。
> 
> 如需詳細資訊，請參閱 [在 Azure Machine Learning Studio 中管理實驗逐一查看](machine-learning-manage-experiment-iterations.md)。  
> 
> 

- - -
**下一步:[部署 hello web 服務](machine-learning-walkthrough-5-publish-web-service.md)**

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
