---
title: "aaaDeploy 機器學習 web 服務 |Microsoft 文件"
description: "如何 tooconvert 訓練試驗 tooa 預測實驗，準備進行部署，然後將其部署為 Azure Machine Learning web 服務。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 73a3e9c6-00d0-41d4-8cf1-2ec87713867e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9cb7af637632b2c3688c11483f29cf24df8fd065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-machine-learning-web-service"></a>部署 Azure Machine Learning Web 服務
Azure 機器學習可讓您 toobuild、 測試及部署預測分析解決方案。

從高階觀點而言，由下列三個步驟完成這個動作：

* **[建立定型實驗]** -Azure Machine Learning Studio 是共同作業視覺式開發環境，您使用 tootrain 及測試預測分析模型使用您提供的定型資料。
* **[將它轉換 tooa 預測實驗]** -一旦您的模型已定型使用現有的資料，您已經準備好 toouse 它 tooscore 新的資料，您準備和簡化您的經驗，用於預測。
* **[將其部署為 Web 服務]** - 您可以將預測實驗部署為[新式]或[傳統] Azure Web 服務。 使用者可以傳送資料 tooyour 模型及接收模型的預測。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="create-a-training-experiment"></a>建立訓練實驗
tootrain 預測分析模型，使用 Azure Machine Learning Studio toocreate 定型實驗，其中您包含各種模組 tooload 定型資料、 準備視 hello 資料、 套用機器學習演算法，以及評估 hello 結果. 您可以逐一查看實驗和不同的機器學習演算法 toocompare 再試一次並評估 hello 結果。

建立和管理定型實驗 hello 程序涵蓋更詳盡地其他位置。 如需詳細資訊，請參閱這些文章：

* [在 Azure Machine Learning Studio 中建立簡單實驗](machine-learning-create-experiment.md)
* [使用 Azure Machine Learning 開發預測解決方案](machine-learning-walkthrough-develop-predictive-solution.md)
* [將訓練資料匯入 Azure Machine Learning Studio](machine-learning-data-science-import-data.md)
* [在 Azure Machine Learning Studio 中管理實驗逐一查看](machine-learning-manage-experiment-iterations.md)

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a>轉換 hello 定型實驗 tooa 預測實驗
一旦您已經定型模型，您準備好 tooconvert 訓練試驗預測實驗 tooscore 新資料。

藉由轉換 tooa 預測進行實驗，您要取得您定型的模型就緒 toobe 部署為計分的 web 服務。 Hello web 服務的使用者可以傳送輸入的資料 tooyour 模型和您的模型會將傳送後 hello 預測結果。 當您轉換 tooa 預測實驗之後，請記住您希望其他人使用您模型 toobe 如何。

tooconvert 預測您定型實驗 tooa 實驗中，按一下**執行**在 hello hello 實驗畫布底部，按一下 **設定 Web 服務**，然後選取**預測 Web 服務**.

![轉換 tooscoring 實驗](./media/machine-learning-publish-a-machine-learning-web-service/figure-1.png)

如需有關如何 tooperform 這項轉換，請參閱[如何 tooprepare Azure Machine Learning Studio 中的部署模型](machine-learning-convert-training-experiment-to-scoring-experiment.md)。

hello 下列步驟描述部署為新的 web 服務的預測實驗。 您也可以部署 hello 實驗與傳統 web 服務。

## <a name="deploy-it-as-a-web-service"></a>將其部署為 Web 服務

為新的 web 服務或傳統 web 服務，您可以部署 hello 預測實驗。

### <a name="deploy-hello-predictive-experiment-as-a-new-web-service"></a>部署為新的 web 服務的 hello 預測實驗
既然 hello 預測實驗已備妥，您可以將其部署為新的 Azure web 服務。 使用 hello web 服務，使用者可以傳送資料 tooyour 模型和 hello 模型將會傳回預測。

toodeploy 您預測進行實驗，請按一下**執行**底部 hello hello 實驗畫布。 一旦 hello 實驗完成執行後，按一下 **部署 Web 服務**選取**部署 Web 服務[新增]**。  hello 部署的 hello Machine Learning Web 服務入口網站 頁面隨即開啟。

> [!NOTE] 
> toodeploy 新的 web 服務，您必須擁有足夠的權限 hello 訂用帳戶 toowhich 您部署 hello web 服務。 如需詳細資訊，請參閱[管理 Web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)。 

#### <a name="machine-learning-web-service-portal-deploy-experiment-page"></a>Machine Learning Web 服務入口網站 [部署實驗] 頁面
在 hello 部署實驗 頁面上，輸入 hello web 服務的名稱。
選取定價方案。 如果您有現有的定價方案，您可以選取它，否則您必須建立新的價格計劃 hello 服務。

1. 在 hello**價格計劃**下拉式清單中，選取現有的方案或選取 hello**選取新的計畫**選項。
2. 在**計劃名稱**，輸入會識別在帳單上的 hello 計劃的名稱。
3. 選取其中一個 hello**每月的計劃層**。 hello 計劃層預設 toohello 計劃您預設的地區和您的 web 服務是部署的 toothat 區域。

按一下**部署**和 hello**快速入門**web 服務 頁面隨即開啟。

hello web 服務快速入門 頁面可讓您存取和指引 hello 建立 web 服務之後，您將執行的最常見工作。 從這裡，您可以輕鬆地存取 hello 測試頁和取用的頁面。

<!-- ![Deploy hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)-->

#### <a name="test-your-new-web-service"></a>測試新式 Web 服務
tootest 新的 web 服務，按一下 **測試 web 服務**在一般工作。 您可以在 hello 測試頁面上，測試您的 web 服務做為要求-回應服務 (RR) 或批次執行服務 (BES)。

hello RR 測試頁面會顯示 hello 輸入、 輸出和 hello 實驗，您已定義任何全域參數。 tootest hello web 服務，您可以手動輸入適當的值 hello 輸入，或是提供逗號分隔值 (CSV) 格式的檔案包含 hello 測試值。

使用 RR，tootest 從 hello 清單檢視模式中，輸入適當的值為 hello 輸入，然後按一下**測試要求-回應**。 在左 hello 輸出資料行 toohello 中，顯示預測結果。

![部署 hello web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-5-test-request-response.png)

按一下 tootest 您 BES**批次**。 在 hello 批次測試頁面上，按一下 瀏覽在您的輸入，並選取包含適當的樣本值的 CSV 檔案。 如果您不需要為 CSV 檔，並且使用 Machine Learning Studio 預測實驗，您可以下載預測實驗 hello 資料集，並使用它。

toodownload hello 資料集，開啟 Machine Learning Studio。 開啟您預測的經驗，並以滑鼠右鍵按一下您的經驗的 hello 輸入。 Hello 內容功能表中選取**資料集**，然後選取 **下載**。

![部署 hello web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-7-mls-download.png)

按一下 [ **測試**]。 批次執行作業的 hello 狀態就會顯示下的 toohello 右邊**測試批次作業**。

![部署 hello web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-6-test-batch-execution.png)

<!--![Test hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)-->

在 [hello**組態**] 頁面上，您可以變更 hello 描述、 標題、 更新 hello 儲存體帳戶金鑰，並啟用您的 web 服務的範例資料。

![設定 hello web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-8-arm-configure.png)

一旦您已部署的 hello web 服務，您可以：

* **存取**透過 hello web 服務 API。
* **管理**透過 Azure Machine Learning web 服務入口網站或 hello Azure 傳統入口網站。
* **更新** 它。

#### <a name="access-your-new-web-service"></a>存取新式 Web 服務
一旦您部署您的 web 服務從 Machine Learning Studio 時，您可以傳送資料 toohello 服務和以程式設計的方式接收回應。

hello**取用**頁面會提供您的 web 服務需要 tooaccess 所有 hello 資訊。 例如，hello API 金鑰會提供 tooallow 獲授權存取 toohello 服務。

如需存取的機器學習 web 服務的詳細資訊，請參閱[如何 tooconsume Azure 機器學習 Web 服務](machine-learning-consume-web-services.md)。

#### <a name="manage-your-new-web-service"></a>管理新式 Web 服務
您可以在 Machine Learning Web 服務入口網站中管理新的 Web 服務。 從 hello[主要入口網站頁面](https://services.azureml-test.net/)，按一下  **Web 服務**。 從 hello web 服務 頁面上，您可以刪除或複製的服務。 toomonitor 特定服務中，按一下 hello 服務，然後按一下**儀表板**。 按一下 toomonitor hello web 服務，與相關聯的批次作業**批次要求記錄檔**。

### <a name="deploy-hello-predictive-experiment-as-a-classic-web-service"></a>與傳統 web 服務部署 hello 預測實驗

既然已充分備妥 hello 預測實驗，您可以將其部署為傳統 Azure web 服務。 使用 hello web 服務，使用者可以傳送資料 tooyour 模型和 hello 模型將會傳回預測。

toodeploy 您預測進行實驗，請按一下**執行**底部 hello hello 試驗畫布，然後按一下**部署 Web 服務**。 hello web 服務的設定，您會放置在 hello web 服務儀表板中。

![部署 hello web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)

#### <a name="test-your-classic-web-service"></a>測試傳統 Web 服務

您可以在 hello 機器學習 Web 服務入口網站或 Machine Learning Studio 中測試 hello web 服務。

tootest hello 的要求回應 web 服務，按一下 hello**測試**hello web 服務儀表板 按鈕。 對話方塊會出現 tooask 您 hello hello 服務的輸入資料。 這些是 hello hello 計分實驗所預期的資料行。 輸入一組資料，然後按一下確定 。 hello hello web 服務所產生的結果會顯示在 hello hello 儀表板底部。

您可以按一下 hello**測試**預覽連結 tootest 您 hello Azure 機器學習 Web 服務入口網站中的服務，如先前在 hello 新的 web 服務 > 一節中所示。

tootest hello 批次執行服務，按一下**測試**預覽連結。 在 hello 批次測試頁面上，按一下 瀏覽在您的輸入，並選取包含適當的樣本值的 CSV 檔案。 如果您不需要為 CSV 檔，並且使用 Machine Learning Studio 預測實驗，您可以下載預測實驗 hello 資料集，並使用它。

![測試 hello web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)

在 [hello**組態**] 頁面上，您可以變更 hello hello 服務顯示名稱，並提供它的描述。 hello 名稱和描述會顯示在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)您用來管理您的 web 服務。

您可以為輸入資料、輸出資料及 Web 服務參數提供描述，方法是在 [輸入結構描述]、[輸出結構描述] 及 [Web 服務參數] 底下的每個資料行輸入字串。 Hello web 服務所提供的 hello 範例程式碼文件中，會使用這些說明。

您可以啟用記錄 toodiagnose 存取您的 web 服務時看見任何失敗。 如需詳細資訊，請參閱 [為 Machine Learning Web 服務啟用記錄](machine-learning-web-services-logging.md)。

![設定 hello web 服務](./media/machine-learning-publish-a-machine-learning-web-service/figure-4.png)

您也可以在 hello Azure 機器學習 Web 服務入口網站類似 toohello 程序稍早顯示 hello 新的 web 服務區段中設定 hello hello web 服務端點。 hello 選項都不同，您可以新增或變更 hello 服務描述、 啟用記錄，以及啟用範例資料用於測試。

#### <a name="access-your-classic-web-service"></a>存取傳統 Web 服務
一旦您部署您的 web 服務從 Machine Learning Studio 時，您可以傳送資料 toohello 服務和以程式設計的方式接收回應。

hello 儀表板提供您的 web 服務需要 tooaccess 所有 hello 資訊。 例如，hello API 金鑰是提供 tooallow 獲授權存取 toohello 服務，以及 API 說明頁面會提供的 toohelp 開始撰寫您的程式碼。

如需存取的機器學習 web 服務的詳細資訊，請參閱[如何 tooconsume Azure 機器學習 Web 服務](machine-learning-consume-web-services.md)。

#### <a name="manage-your-classic-web-service"></a>管理傳統 Web 服務
有各種不同的動作，您可以執行 toomonitor web 服務。 您可以更新它和刪除它。 您也可以加入其他端點 tooa 傳統 web 服務加入 toohello 預設端點，當您在部署時建立。

如需詳細資訊，請參閱[管理 Azure Machine Learning 工作區](machine-learning-manage-workspace.md)和[管理 web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)。

<!-- When this article gets published, fix hello link and uncomment
For more information on how toomanage Azure Machine Learning web service endpoints using hello REST API, see **Azure machine learning web service endpoints**.
-->

## <a name="update-hello-web-service"></a>更新 hello web 服務
您可以變更 tooyour web 服務，例如更新 hello 模型額外的定型資料並部署一次，覆寫 hello 原始 web 服務。

tooupdate hello web 服務，開啟 hello 原始預測實驗用 toodeploy hello web 服務，並依序按一下中進行編輯的複製**SAVE AS**。 進行變更，然後按一下部署 Web 服務 。

因為您已部署此實驗之前，會要求您想 toooverwrite （傳統 Web 服務） 或更新 （新的 web 服務） hello 現有服務。 按一下**是**或**更新**停止 hello 現有 web 服務和部署 hello 新預測實驗部署在其位置。

> [!NOTE]
> 如果 hello 原始 web 服務中進行組態變更，例如，輸入新的顯示名稱或描述，您必須 tooenter 這些值一次。
> 
> 

更新您的 web 服務的其中一個選項以程式設計的方式是 tooretrain hello 模型。 如需詳細資訊，請參閱 [以程式設計方式重塑機器學習模型](machine-learning-retrain-models-programmatically.md)。

<!-- internal links -->
[建立定型實驗]: #create-a-training-experiment
[將它轉換 tooa 預測實驗]: #convert-the-training-experiment-to-a-predictive-experiment
[將其部署為 Web 服務]: #deploy-it-as-a-web-service
[新式]: #deploy-the-predictive-experiment-as-a-new-Web-service
[傳統]: #deploy-the-predictive-experiment-as-a-new-Web-service
[Access]: #access-the-Web-service
[Manage]: #manage-the-Web-service-in-the-azure-management-portal
[Update]: #update-the-Web-service
