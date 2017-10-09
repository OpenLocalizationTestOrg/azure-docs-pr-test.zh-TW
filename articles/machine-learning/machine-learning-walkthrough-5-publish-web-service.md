---
title: "步驟 5： 部署的 hello 機器學習 web 服務 |Microsoft 文件"
description: "步驟 5 的 hello 開發預測方案逐步解說： 部署為 web 服務 Machine Learning Studio 中的預測實驗。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 3fca74a3-c44b-4583-a218-c14c46ee5338
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 76391010972ed1450bbda8bfb2352c7b22b51ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-5-deploy-hello-azure-machine-learning-web-service"></a>逐步解說步驟 5： 部署的 hello Azure Machine Learning web 服務
這是 hello hello 逐步解說中，第五個步驟[開發 Azure Machine Learning 中的預測分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)

1. [建立機器學習服務工作區](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [上傳現有資料](machine-learning-walkthrough-2-upload-data.md)
3. [建立新實驗](machine-learning-walkthrough-3-create-new-experiment.md)
4. [來定型及評估 hello 模型](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. **部署 hello web 服務**
6. [存取 hello web 服務](machine-learning-walkthrough-6-access-web-service.md)

- - -
toogive 其他機率 toouse hello 我們已在本逐步解說中開發的預測模型，我們可以將其部署為 Azure 上的 web 服務。

向上 toothis 點我們已經已試驗訓練我們的模型。 但即將不再部署的 hello 服務 toodo 定型-它會執行 toogenerate 新預測計分根據我們的模型中的 hello 使用者的輸入。 讓我們 toodo 某些準備 tooconvert 這實驗從***訓練***實驗 tooa***預測***實驗。 

這是一個三步驟程序：  

1. 請移除其中一個 hello 模型
2. 轉換 hello*定型實驗*我們建立了成*預測實驗*
3. 部署為 web 服務的 hello 預測實驗

## <a name="remove-one-of-hello-models"></a>請移除其中一個 hello 模型

首先，我們需要 tootrim 此實驗向一點。 我們目前 hello 實驗中有兩個不同的模型，但我們只想 toouse 一個模型，我們將此部署為 web 服務。  

例如，假設我們已經決定該 hello 促進式樹狀模型的執行效能優於 hello SVM 模型。 因此第一件事 toodo hello 是移除 hello[二級支援向量機器][ two-class-support-vector-machine]模組和 hello 模組用於培訓。 您可以 toomake hello 實驗副本第一次按一下**另存新檔**底部 hello hello 實驗畫布。

我們需要 toodelete hello 下列模組：  

* [二元支援向量機器][two-class-support-vector-machine]
* [定型模型][ train-model]和[計分模型][ score-model]所連接的 tooit 模組
* [標準化資料][normalize-data] (兩者)
* [評估模型][ evaluate-model] （因為我們在完成評估 hello 模型）

選取每個模組並按下 hello Delete 鍵或以滑鼠右鍵按一下 hello 模組，然後選取**刪除**。 

![移除 hello SVM 模型][3a]

我們的模型現在看起來應該像這樣：

![移除 hello SVM 模型][3]

現在我們準備 toodeploy 此模型使用 hello[二級促進式決策樹][two-class-boosted-decision-tree]。

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a>轉換 hello 定型實驗 tooa 預測實驗

tooget 這模型備妥可進行部署，我們需要 tooconvert 這定型實驗 tooa 預測實驗。 這牽涉到三個步驟：

1. 儲存 hello 模型，我們已經定型，並取代我們定型模組
2. Trim 只所需的訓練的 hello 實驗 tooremove 模組
3. 定義 hello web 服務會接受輸入的位置，以及它會產生 hello 輸出

我們無法手動執行這項，但幸運的是所有三個步驟，可透過按一下**設定 Web 服務**在 hello hello 實驗畫布底部 (選取 hello**預測 Web 服務**選項）。

> [!TIP]
> 如果您想更多詳細資料上轉換定型實驗 tooa 預測時，會發生什麼情況進行實驗，請參閱[如何 tooprepare Azure Machine Learning Studio 中的部署模型](machine-learning-convert-training-experiment-to-scoring-experiment.md)。

當您按一下 [設定 Web 服務] ，會發生幾件事：

* hello 定型的模型為單一轉換的 tooa**定型的模型**模組，而儲存在 hello 模組調色盤 toohello 實驗畫布左邊的 hello (您可以找到在**定型的模型**)
* 用於定型的模組已遭到移除，尤其是：
  * [二元促進式決策樹][two-class-boosted-decision-tree]
  * [定型模型][train-model]
  * [資料分割][split]
  * 第二個 hello[執行 R 指令碼][ execute-r-script]用於測試資料的模組
* hello 儲存已定型的模型是已加回到 hello 實驗
* **Web 服務輸入**和**Web 服務輸出**加入模組 （這些識別 hello 使用者資料將在其中輸入 hello 模型，以及傳回的資料，存取 hello web 服務時）

> [!NOTE]
> 您可以看到 hello 實驗會儲存在已加入在 hello 實驗畫布 hello 最上方的索引標籤下的兩個部分。 hello 原始定型實驗是 hello 索引標籤下**定型實驗**，以及新建立的預測實驗 hello 低於**預測實驗**。 hello 預測實驗為 hello 我們將會部署為 web 服務的其中一個。

我們需要 tootake 一個額外的步驟與此特定實驗。
我們新增了兩個[執行 R 指令碼][ execute-r-script]模組 tooprovide 加權函式 toohello 資料。 因此，我們可以接受出 hello 最終模型中的那些模組時只會用於定型和測試，我們需要一墩。
Machine Learning Studio 移除其中一個[執行 R 指令碼][ execute-r-script]模組時移除它 hello[分割][ split]模組。 現在我們可以移除其他 hello 以及連接[中繼資料編輯器][ metadata-editor]直接太[計分模型][score-model]。    

實驗現在看起來如下：  

![計分的 hello 定型的模型][4]  

> [!NOTE]
> 您可能會想知道為什麼我們留 hello UCI 德文信用卡資料集在 hello 預測實驗中。 這樣會產生 tooscore hello 使用者的資料，不 hello 原始資料集，因此為什麼不要 hello 原始資料集 hello 模型中的 hello 服務？
> 
> 」 沒錯 hello 服務不需要 hello 原始信用卡資料。 但 hello 結構描述必須針對該資料，其中包括有多少資料行等資訊，以及哪些資料行是數值。 這個結構描述資訊是必要的 toointerpret hello 使用者的資料。 我們會保留這些連線，如此 hello 計分模組擁有 hello 資料集結構描述時 hello 服務正在執行的元件。 hello 資料不會使用，只要 hello 結構描述。  
> 
> 

執行 hello 實驗最後一次 (按一下**執行**。)如果您想 hello 模型的 tooverify 仍然可以運作，請按一下的 hello hello 輸出[計分模型][ score-model]模組，然後選取**檢視結果**。 您可以看到顯示 hello 原始資料，以及 hello 信用風險值 （「 計分標籤 」），並 hello 計分機率值 （「 計分機率 」。） 

## <a name="deploy-hello-web-service"></a>部署 hello web 服務
為其中一個傳統 web 服務，或為新的 web 服務為基礎的 Azure 資源管理員，您可以部署 hello 實驗。

### <a name="deploy-as-a-classic-web-service"></a>部署為傳統 Web 服務
按一下 toodeploy 傳統 web 服務實驗中，從衍生**部署 Web 服務**下方 hello 畫布，然後選取**部署 Web 服務 [傳統]**。 Machine Learning Studio 會部署為 web 服務的 hello 實驗，並引導您 toohello 儀表板的 web 服務。 從這個頁面中，您可以傳回 toohello 實驗 (**檢視快照集**或**檢視最新**) 並執行簡單的測試 hello web 服務 (請參閱**測試 hello web 服務**下方)。 另外還有這裡建立可以存取 hello web 服務 （更多的 hello 本逐步解說的下一個步驟中） 的應用程式的資訊。

![Web 服務儀表板][6]

您可以設定 hello 服務即可 hello**組態** 索引標籤。您可以在這裡修改 hello （它是預設的給定的 hello 實驗名稱） 的服務名稱並提供它的描述。 您也可以提供更多的易記標籤 hello 輸入和輸出資料。  

![設定 hello web 服務][5]  

### <a name="deploy-as-a-new-web-service"></a>部署為新式 Web 服務

> [!NOTE] 
> 新的 web 服務，您必須擁有足夠的權限，在您要部署的 hello 訂用帳戶 toowhich toodeploy hello web 服務。 如需詳細資訊，請參閱[管理 web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)。 

新的 web 服務 toodeploy 衍生自我們實驗：

1. 按一下**部署 Web 服務**下方 hello 畫布，然後選取**部署 Web 服務 [New]**。 Machine Learning Studio 會傳輸 toohello Azure Machine Learning web 服務**部署實驗**頁面。

2. 輸入 hello web 服務的名稱。 

3. 如**價格計劃**、 您可以選取現有的定價方案，或選取 「 建立新的 」 和授與 hello 新計劃的名稱和選取 hello 每月的計劃選項。 hello 計劃層預設 toohello 計劃您預設的地區和您的 web 服務是部署的 toothat 區域。

4. 按一下 [ **部署**]。

請稍候幾分鐘 hello**快速入門**web 服務 頁面隨即開啟。

您可以設定 hello 服務即可 hello**設定** 索引標籤。您可以在這裡修改 hello 服務標題，並提供它的描述。 

tootest hello web 服務，請按一下 hello**測試** 索引標籤 (請參閱**測試 hello web 服務**下方)。 建立可以存取 hello web 服務的應用程式的資訊，請按一下 hello**取用** 索引標籤 （在此逐步解說中的 hello 下一個步驟將移到更多詳細資料）。

> [!TIP]
> 已部署完成之後，您可以更新 hello web 服務。 例如，如果您想 toochange 您的模型，然後您可以編輯 hello 定型實驗、 調整 hello 模型參數，然後按一下**部署 Web 服務**、 選取**部署 Web 服務 [傳統]**或**部署 Web 服務 [New]**。 當您重新部署 hello 實驗時，它會取代 hello web 服務，現在使用更新的模型。  
> 
> 

## <a name="test-hello-web-service"></a>測試 hello web 服務

Hello 使用者資料存取 hello web 服務時，進入透過 hello **Web 服務輸入**模組，其中已通過 toohello[計分模型][ score-model]模組和計分。 我們設定 hello 預測實驗 hello 方式，hello 模型預期的 hello 相同格式化為 hello 原始信用風險資料集的資料。
hello 結果 toohello 使用者從 hello web 服務透過 hello **Web 服務輸出**模組。

> [!TIP]
> 我們有 hello 預測實驗設定，整個 hello hello 方法得到的 hello[計分模型][ score-model]模組會傳回。 這包括所有 hello 輸入的資料加上 hello 信用風險值和 hello 計分可能性。 但如果您想要傳回不同的項目-例如，您可能會傳回只 hello 信用風險的值。 toodo 此，插入[投射資料行][ project-columns]模組之間[計分模型][ score-model]和 hello **Web 服務輸出** tooeliminate 資料行，您不想 hello web 服務 tooreturn。 
> 
> 

您可以測試傳統 web 服務有兩種**Machine Learning Studio**或 hello **Azure 機器學習 Web 服務**入口網站。
您可以測試新的 web 服務只能在 hello**機器學習 Web 服務**入口網站。

> [!TIP]
> 測試時在 hello Azure 機器學習 Web 服務入口網站中，您可以建立範例資料，您可以使用 tootest hello 要求-回應服務的 hello 入口網站。 在 hello**設定**頁面上，選取 是**啟用範例資料嗎？**。 當您開啟 hello 要求-回應 索引標籤上 hello**測試** 頁面上，hello 入口網站會填入取自 hello 原始信用風險資料集的範例資料。

### <a name="test-a-classic-web-service"></a>測試傳統 Web 服務

Machine Learning Studio 中或 hello 機器學習 Web 服務入口網站中，您可以測試傳統 web 服務。 

#### <a name="test-in-machine-learning-studio"></a>在 Machine Learning Studio 中測試

1. 在 hello**儀表板**hello web 服務頁面上，按一下 hello**測試**按鈕底下**預設端點**。 對話方塊出現，並會要求您輸入 hello hello 服務的輸入資料。 這些是 hello 相同的資料行出現在 hello 原始信用風險資料集。  

2. 輸入一組資料，然後按一下確定 。 

#### <a name="test-in-hello-machine-learning-web-services-portal"></a>在 hello 機器學習 Web 服務入口網站中測試

1. 在 hello**儀表板**hello web 服務頁面上，按一下 hello**測試預覽**連結底下**預設端點**。 hello web 服務端點的 hello Azure 機器學習 Web 服務入口網站中的 hello 測試頁隨即開啟，並會要求您輸入 hello hello 服務的輸入資料。 這些是 hello 相同的資料行出現在 hello 原始信用風險資料集。

2. 按一下 [測試要求-回應]。 

### <a name="test-a-new-web-service"></a>測試新式 Web 服務

您可以只在 hello 機器學習 Web 服務入口網站中測試新的 web 服務。

1. 在 hello [Azure 機器學習 Web 服務](https://services.azureml.net/quickstart)入口網站中，按一下**測試**hello 頁面頂端的 hello。 hello**測試** 頁面隨即開啟，您可以輸入 hello 服務的資料。 hello 輸入所顯示的欄位對應 toohello 資料行出現在 hello 原始信用風險資料集。 

2. 輸入一組資料，然後按一下測試要求-回應 。

hello hello 測試的結果會顯示在 hello 右手邊的 hello 輸出資料行中的 hello 頁面。 


## <a name="manage-hello-web-service"></a>管理 hello web 服務

### <a name="manage-a-classic-web-service-in-hello-azure-classic-portal"></a>管理 hello Azure 傳統入口網站中的傳統 web 服務

一旦您部署了傳統 web 服務，您可以從管理 hello [Azure 傳統入口網站](https://manage.windowsazure.com)。

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)
2. 在 hello Microsoft Azure 服務面板中，按一下 **機器學習服務**
3. 按一下您的工作區
4. 按一下 hello **Web 服務** 索引標籤
5. 按一下 建立 hello web 服務
6. 按一下 hello 「 預設 」 端點

從這裡，您可以執行一些作業，例如監視 hello web 服務執行的動作，並變更多少同時呼叫 hello 服務可以處理，導致效能做調整。

如需詳細資訊，請參閱：

* [建立端點](machine-learning-create-endpoint.md)
* [調整 Web 服務](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-hello-azure-machine-learning-web-services-portal"></a>管理傳統或 hello Azure 機器學習 Web 服務入口網站中的新 web 服務

一旦您是否傳統或新部署您的 web 服務，您可以從管理 hello [Microsoft Azure 機器學習 Web 服務](https://services.azureml.net/quickstart)入口網站。

您的 web 服務的 toomonitor hello 效能：

1. 登入 toohello [Microsoft Azure 機器學習 Web 服務](https://services.azureml.net/quickstart)入口網站
2. 按一下 [Web 服務]
3. 按一下您的 Web 服務
4. 按一下 hello**儀表板**

- - -
**下一步:[存取 hello web 服務](machine-learning-walkthrough-6-access-web-service.md)**

[3]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3.png
[3a]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3a.png
[4]: ./media/machine-learning-walkthrough-5-publish-web-service/publish4.png
[5]: ./media/machine-learning-walkthrough-5-publish-web-service/publish5.png
[6]: ./media/machine-learning-walkthrough-5-publish-web-service/publish6.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[metadata-editor]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[project-columns]: https://msdn.microsoft.com/en-us/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
