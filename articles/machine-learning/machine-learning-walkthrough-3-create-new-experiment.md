---
title: "步驟 3：建立新的 Machine Learning 實驗 | Microsoft Docs"
description: "步驟 3 中的 hello 開發預測方案逐步解說： 在 Azure Machine Learning Studio 中建立新的定型實驗。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 4697d461a205c50c8d2aa6a3bd56697840cb30f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a>逐步解說步驟 3：建立新的 Azure Machine Learning 實驗
這是 hello hello 逐步解說中，第三個步驟[開發 Azure Machine Learning 中的預測分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)

1. [建立機器學習服務工作區](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [上傳現有資料](machine-learning-walkthrough-2-upload-data.md)
3. **建立新實驗**
4. [來定型及評估 hello 模型](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [部署 hello Web 服務](machine-learning-walkthrough-5-publish-web-service.md)
6. [存取 hello Web 服務](machine-learning-walkthrough-6-access-web-service.md)

- - -
在此逐步解說中的 hello 下一個步驟是 toocreate 實驗中使用 hello 我們上傳的資料集的 Machine Learning Studio 中。  

1. 在 Studio 中，按一下  **+ 新增**在 hello hello 視窗的底部。
2. 選取 [實驗] ，然後選取 [空白實驗]。 

    ![建立新實驗][0]

2. 選取 hello 預設試驗頂端 hello hello 畫布的名稱，以及將它重新命名 toosomething 有意義。

    ![將實驗重新命名][5]
   
   > [!TIP]
   > 它是很好的作法 toofill**摘要**和**描述**hello 實驗中 hello**屬性**窗格。 這些屬性提供，以便稍後會查看它的任何人就可以了解您的目標和方法，hello 機會 toodocument hello 實驗。
   > 
   > ![實驗屬性][6]
   > 
3. 在 hello 模組調色盤 toohello 左邊 hello 實驗畫布上，依序展開**儲存的資料集**。
4. 尋找 hello 資料集下您建立**我的資料集**並將它拖曳到畫布 hello。 您也可以尋找 hello dataset 中 hello 輸入 hello 名稱**搜尋**hello 調色盤上的方塊。  

    ![新增 hello 資料集 toohello 實驗][7]

## <a name="prepare-hello-data"></a>準備 hello 資料
您可以檢視前 100 個資料列的 hello 和 hello 整個結果集的一些統計資訊 hello： 按一下 hello hello 資料集 （使用 hello 底部 hello 小圓形） 的輸出連接埠，然後選取**視覺化**。  

Studio hello 資料檔案並未隨附資料行標題，因為提供的泛型標題 (Col1，Col2，*等*)。 良好標題不是基本 toocreating 模型，但它們會 hello 資料更容易 toowork hello 實驗中。 此外，當我們最後發行此模型在 web 服務時，hello 標題將有助於識別 hello 服務的 hello 資料行 toohello 使用者。  

我們可以加入資料行標題使用 hello[編輯中繼資料][ edit-metadata]模組。
使用 hello[編輯中繼資料][ edit-metadata]模組 toochange 中繼資料與資料集相關聯。 在此情況下，將使用此值的更多的易記名稱的 tooprovide 針對資料行標題。 

toouse[編輯中繼資料][edit-metadata]，您首先要指定哪些資料行 toomodify，（在此情況下，它們全部。）接下來，您可以指定 hello 動作 toobe 對這些資料行 （在此情況下，變更資料行標題。）

1. Hello 模組調色盤上，輸入 「 中繼資料 」 中 hello**搜尋**方塊。 hello[編輯中繼資料][ edit-metadata] hello 模組清單中會出現。

2. 按一下並拖曳 hello[編輯中繼資料][ edit-metadata]模組 hello 到畫布，並將它放在下方 hello 我們先前加入的資料集。

3. 連接 hello 資料集 toohello[編輯中繼資料][edit-metadata]： 按一下 hello hello 資料集 （使用 hello 資料集的 hello 底部 hello 小圓形） 的輸出連接埠中，拖曳 toohello 的輸入連接埠[編輯中繼資料] [ edit-metadata] （hello 小圓圈 hello hello 模組頂端），然後放開 hello 滑鼠按鈕。 hello 資料集和模組保持連接，即使您移動其中 hello 畫布上。
   
   hello 實驗現在看起來應該像下面這樣：  
   
   ![新增編輯中繼資料][1]
   
   hello 紅色驚嘆號表示我們沒有尚未設定此模組的 hello 屬性。 我們接下來會這樣做。
   
   > [!TIP]
   > 您可以新增註解 tooa 模組按兩下 hello 模組和輸入的文字。 這可協助您快速地查看哪些 hello 模組負責在您實驗中。 在此情況下，按兩下 hello[編輯中繼資料][ edit-metadata]模組和類型 hello 註解"Add 資料行標題 」。 按一下任何其他地方 hello 畫布 tooclose hello 文字方塊。 toodisplay hello 註解，請按一下 hello 向下箭頭 hello 模組上。
   > 
   > ![編輯中繼資料模組並新增註解][8]
   > 
4. 選取[編輯中繼資料][edit-metadata]，並在 hello**屬性**窗格 toohello hello 畫布的右邊按一下**啟動資料行選取器**。

5. 在 hello**選取資料行**對話方塊中，選取所有 hello 中的資料列**可用的資料行**按一下 > toomove 它們太**選取的資料行**。
   hello 對話方塊看起來應該像這樣：

   ![已選取所有資料行的資料行選取器][2]

6. 按一下 hello**確定**核取記號。

7. 在 hello**屬性**窗格中，尋找 hello**新資料行名稱**參數。 在此欄位中，輸入 hello 21 hello 資料集，以逗點和資料行順序，以分隔資料行名稱的清單。 您可以從 hello 資料集的文件 hello UCI 在網站上，取得 hello 資料行名稱，或為了方便起見，您可以複製並貼上下列清單中的 hello:  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   hello 屬性 窗格看起來像這樣：
   
   ![編輯中繼資料的屬性][3]

> [!TIP]
> 如果您想 tooverify hello 資料行標題，請執行 hello 實驗 (按一下**執行**hello 實驗畫布下方)。 當它完成時執行 (綠色的核取記號會出現在[編輯中繼資料][edit-metadata])，按一下輸出連接埠 hello hello[編輯中繼資料][ edit-metadata]模組，並選取**視覺化**。 您可以檢視的任何模組的 hello 輸出中 hello hello 實驗中 hello 資料相同的方式 tooview hello 進度。
> 
> 

## <a name="create-training-and-test-datasets"></a>建立訓練和測試資料集
我們需要一些資料 tootrain hello 模型和一些 tootest 它。
因此在 hello 實驗 hello 下一步，分割 hello 資料集分成兩個不同的資料集： 一個用於培訓我們的模型，另一個用於測試。

toodo，我們使用 hello[分割資料][ split]模組。  

1. 尋找 hello[分割資料][ split]模組，將它拖曳至 hello 畫布，並將它連接 toohello[編輯中繼資料][ edit-metadata]模組。

2. 根據預設，hello 分割比例是 0.5 和 hello**隨機分割**參數設定。 這表示 hello 資料隨機半是透過一個連接埠的 hello 輸出[分割資料][ split]模組和半透過 hello 其他。 您可以調整這些參數，以及 hello**隨機種子**參數，toochange hello 分割成定型集和測試資料。 在此範例中，我們保持原狀。
   
   > [!TIP]
   > hello 屬性**hello 中的資料列的分數，第一次輸出資料集**決定多少 hello 資料是透過 hello 輸出*左*輸出連接埠。 比方說，如果您設定 hello 比率 too0.7，70%的 hello 資料則透過 hello 左連接埠和 30%，透過 hello 右連接埠的輸出。  
   > 
   > 

3. 按兩下 hello[分割資料][ split]模組和輸入 hello 註解、 「 定型/測試資料分割的 50%」。 

我們可以使用的 hello hello 輸出[分割資料][ split]我們喜歡，不過我們選擇 toouse hello 左的輸出做為定型資料，且右 hello 模組輸出為測試資料。  

Hello 中所述[上一個步驟](machine-learning-walkthrough-2-upload-data.md)，hello 高信用風險低為將錯誤分類成本高於五次 hello 為 high 低的信用風險將錯誤分類成本。 這個 tooaccount，我們會產生新的資料集，以反映此成本函式。 在 hello 新資料集中，每個高風險範例複寫五次，而不會複寫每個低風險範例。   

我們可以使用 R 程式碼來執行此複寫：  

1. 尋找並拖曳 hello[執行 R 指令碼][ execute-r-script] hello 實驗畫布的模組。 

2. 連接保留 hello 輸出連接埠的 hello[分割資料][ split]模組 toohello 的第一個輸入連接埠 (「 Dataset1") 的 hello[執行 R 指令碼][ execute-r-script]模組。

3. 按兩下 hello[執行 R 指令碼][ execute-r-script]模組，然後輸入 hello 註解，「 成本調整集 」。

4. 在 hello**屬性** 窗格中，刪除 hello 預設文字在 hello **R 指令碼**參數，並輸入此指令碼：
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![Hello 執行 R 指令碼模組中的 R 指令碼][9]

我們需要此相同的複寫作業每個輸出的 hello toodo[分割資料][ split]模組，因此該 hello 定型集和測試資料有 hello 相同成本的調整。 hello 最簡單的方式 toodo，這是透過複製 hello[執行 R 指令碼][ execute-r-script]模組我們剛才和其他連接 toohello 輸出連接埠 hello[分割資料][split]模組。

1. 以滑鼠右鍵按一下 hello[執行 R 指令碼][ execute-r-script]模組，然後選取**複製**。

2. 以滑鼠右鍵按一下 hello 實驗畫布，然後選取**貼上**。

3. 將 hello 新模組進入位置，然後再將連接 hello hello 右輸出連接埠[分割資料][ split]模組 toohello 的第一個輸入連接埠，這個新[執行 R 指令碼][execute-r-script]模組。 

4. 在 hello hello 畫布底部，按一下 **執行**。 

> [!TIP]
> hello 複本 hello 執行 R 指令碼模組包含的 hello 相同以 hello 原始模組的指令碼。 當您複製並貼上 hello 畫布上的模組時，hello 複製會保留原始 hello 所有 hello 屬性。  
> 
> 

實驗此時看起來會如下所示：

![Adding Split module and R scripts][4]

如需如何在您的實驗中使用 R 指令碼的詳細資訊，請參閱 [透過 R 擴充您的實驗](machine-learning-extend-your-experiment-with-r.md)。

**下一步:[定型和評估 hello 模型](machine-learning-walkthrough-4-train-and-evaluate-models.md)**

[0]: ./media/machine-learning-walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/machine-learning-walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/machine-learning-walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/machine-learning-walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/machine-learning-walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
