---
title: "aaaAzure 常見問題集 (Faq) 的機器學習 |Microsoft 文件"
description: "Azure Machine Learning 簡介：常見問題集，涵蓋計費、功能，以及適用於簡化預測性模型化之雲端服務的限制。"
keywords: "機器學習服務簡介,建立預測模型,什麼是機器學習服務"
services: machine-learning
documentationcenter: 
author: garyericson
manager: paulettm
editor: cgronlun
ms.assetid: a4a32a06-dbed-4727-a857-c10da774ce66
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: 3af84451dde064c3c9520ee520b541128b1eef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-frequently-asked-questions-billing-capabilities-limitations-and-support"></a>Azure Machine Learning 常見問題集：計費、功能、限制及支援
以下是有關 Azure Machine Learning 的一些常見問題和對應解答，而 Azure Machine Learning 是適合透過 Web 服務開發預測性模型和運作方案的雲端服務。 這些常見問題集提供有關如何 toouse hello 服務，其中包括 hello 計費模型、 功能、 限制和支援問題。

**是否有您無法在這裡找到的問題？**

Azure Machine Learning 有其中 hello 資料科學社群的成員可以詢問有關 Azure Machine Learning 的 MSDN 上的論壇。 hello Azure Machine Learning 小組監視 hello 論壇。 移 toohello [Azure 機器學習論壇](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning)toosearch 答案或 toopost 您自己的新的問題。

## <a name="general-questions"></a>一般問題
**什麼是 Azure Machine Learning 服務？**

Azure Machine Learning 是完全受管理的服務，您可以使用 toocreate、 測試、 操作及管理 hello 雲端中的預測分析解決方案。 僅使用瀏覽器，您即可以登入、上傳資料，以及立即開始機器學習實驗。 拖放式預測性模型化、大型模組和用以啟動範本的程式庫，讓您得以簡便而快速地執行一般機器學習工作。 如需詳細資訊，請參閱 hello [Azure 機器學習服務概觀](https://azure.microsoft.com/services/machine-learning/)。 如簡介 toomachine 學習主要詞彙和概念的說明，請參閱[簡介 tooAzure 機器學習](machine-learning-what-is-machine-learning.md)。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**什麼是 Machine Learning Studio？**

Machine Learning Studio 是您利用網頁瀏覽器存取的工作區環境。 Machine Learning Studio 主控模組可協助您建立端對端視覺構圖介面中的，實驗的 hello 表單中的資料科學工作流程在棧的板。

如需 Machine Learning Studio 的詳細資訊，請參閱 [什麼是 Machine Learning Studio？](machine-learning-what-is-ml-studio.md)

**什麼是 hello 機器學習 API 服務？**

hello 機器學習 API 服務可讓您 toodeploy 預測模型，例如模型內建 Machine Learning Studio 中，為既可調整又容錯，web 服務。 建立 hello 機器學習 API 服務的 hello web 服務是 REST Api 可提供外部應用程式與您的預測分析的模型之間的通訊介面。

如需詳細資訊，請參閱[如何 tooconsume Azure 機器學習 Web 服務](machine-learning-consume-web-services.md)。

**傳統 Web 服務會在哪裡列出？新型 (Azure Resource Manager 架構) Web 服務會在哪裡列出？**

建立使用 hello 傳統部署模型和 web 服務使用 hello 新的 Azure Resource Manager 部署模型所建立的 web 服務會列在 hello [Microsoft Azure 機器學習 Web 服務](https://services.azureml.net/)入口網站。

傳統 web 服務也會列在[Machine Learning Studio](http://studio.azureml.net)上 hello **Web 服務** 索引標籤。

## <a name="azure-machine-learning-questions"></a>Azure Machine Learning 問題
**Azure Machine Learning Web 服務是什麼？**

Machine Learning Web 服務可在應用程式與機器學習服務工作流程計分模型之間提供介面。 外部應用程式可以使用 Azure Machine Learning toocommunicate 搭配即時的機器學習服務工作流程計分模型。 呼叫 tooa 機器學習 web 服務傳回預測結果 tooan 外部應用程式。 toomake 呼叫 tooa web 服務，您傳遞您部署的 hello web 服務時所建立的 API 金鑰。 Machine Learning Web 服務以 REST 為基礎，這是一種常見的 Web 程式設計專案架構。

Azure Machine Learning 有兩種 Web 服務類型：

* 要求-回應服務 (RR): 的低延遲、 高擴充性服務可提供介面 toohello 無狀態的模型建立和部署使用 Machine Learning Studio。
* 批次執行服務 (BES)：這是一種非同步的服務，為一批資料記錄進行計分。

有幾種方式 tooconsume hello REST API 及存取 hello web 服務。 例如，您可以使用部署 hello web 服務時，為您產生 hello 範例程式碼，在 C#、 R、 Python 撰寫應用程式。

hello 範例程式碼位於：
- hello hello Azure 機器學習 Web 服務入口網站中的 web 服務的 hello 取用頁面
- hello web 服務儀表板 Machine Learning Studio 中的 hello API 說明頁面

您也可以使用 hello 範例 Microsoft Excel 活頁簿會為您建立，且可供 hello web 服務儀表板 Machine Learning Studio 中使用。

**Hello 主要更新 tooAzure 機器學習服務有哪些？**

Hello 最新的更新，請參閱[Azure Machine Learning 中最新消息](machine-learning-whats-new.md)。

## <a name="machine-learning-studio-questions"></a>Machine Learning Studio 問題
### <a name="import-and-export-data-for-machine-learning"></a>匯入和匯出 Machine Learning 的資料
**機器學習服務支援何種資料來源？**

您可以下載資料 tooa Machine Learning Studio 實驗三種方式：

- 以資料集的形式上傳本機檔案
- 使用模組 tooimport 資料從雲端資料服務
- 匯入從另一個實驗儲存的資料集

toolearn 深入了解支援的檔案格式，請參閱[定型資料匯入至 Machine Learning Studio](machine-learning-data-science-import-data.md)。

#### <a id="ModuleLimit"></a>大小可以 hello 資料集是適用於我的模組？
Machine Learning Studio 中的模組支援常見使用案例的總 too10 GB 的密集的數值資料的資料集。 如果模組在多個輸入，hello 10 GB 的值為 hello 的所有輸入的大小總計。 您也可以使用 Hive 或 Azure SQL Database 查詢來取樣較大型資料集，或者在擷取前使用「以計數學習」前置處理。  

hello 下列類型的資料可以展開 toolarger 資料集特徵正規化期間而且會超過 10 GB 的限制的 tooless:

* 疏鬆
* 類別
* 字串
* 二進位資料

小於 10 GB 的限制的 toodatasets hello 下列模組︰

* Recommender 模組
* 合成少數類過採樣技術 (SMOTE) 模組
* 指令碼模組：R、Python SQL
* 模組 hello 輸出的資料大小可能大於輸入的資料大小，例如聯結 」 或 「 特徵雜湊
* 交叉驗證、 微調模型超、 序數迴歸和其中一個 vs 全部多級，hello 反覆項目數目很大時

#### <a id="UploadLimit"></a>上傳資料的 hello 限制為何？
對於大於幾個 Gb 的資料集上, 傳資料 tooAzure 儲存體或 Azure SQL Database，或使用 Azure HDInsight 而非直接從本機檔案上傳。

**可以從 Amazon S3 讀取資料嗎？**

如果您有小量的資料，並想 tooexpose 它透過 HTTP URL，則您可以使用 hello[匯入資料][ import-data]模組。 大量資料，將它傳輸 tooAzure 儲存體第一次，然後再使用 hello[匯入資料][ import-data]模組 toobring 到您的經驗。
<!--

<SEE CLOUD DS PROCESS>
-->

**有內建的影像輸入功能嗎？**

您可以了解映像輸入 hello 功能[匯入映像][ image-reader]參考。

### <a name="modules"></a>模組
**hello 演算法、 資料來源、 資料格式或我正在尋找的資料轉換作業不在 Azure Machine Learning Studio。我有哪些選擇？**

您可以移 toohello[使用者意見反應論壇](http://go.microsoft.com/fwlink/?LinkId=404231)toosee 功能會要求我們追蹤。 如果已經要求您要尋找的功能，請加入您投票 tooa 的要求。 如果您要尋找的 hello 功能不存在，請建立新的要求。 您可以在此論壇中太檢視 hello 要求的狀態。 我們會追蹤這份清單，並經常更新的功能可用性的 hello 狀態。 此外，您可以使用 hello 內建支援 R，並將 Python toocreate 自訂轉換時所需。

**是否可將我現有的程式碼放入 Machine Learning Studio 中？**

，您可以將現有的 R 或 Python 程式碼帶入 Machine Learning Studio 中，在 hello 相同試驗 Azure Machine Learning 學習模組，並將 hello 方案部署為 web 服務透過 Azure Machine Learning 中執行。 如需詳細資訊，請參閱[透過 R 擴展您的實驗](machine-learning-extend-your-experiment-with-r.md)和[在 Azure Machine Learning Studio 中執行 Python 機器學習服務指令碼](machine-learning-execute-python-scripts.md)。

**它是類似的可能 toouse [PMML](http://en.wikipedia.org/wiki/Predictive_Model_Markup_Language) toodefine 模型嗎？**

否，不支援預測模型標記語言 (PMML)。 您可以使用自訂 R 和 Python 程式碼 toodefine 模組。

**在我的實驗中可以平行執行多少個模組？**  

您可以執行 toofour 模組，以平行方式在實驗中。

### <a name="data-processing"></a>資料處理
**是否有能力 toovisualize 資料 （除了 R 視覺效果） 以互動方式在 hello 實驗？**

按一下 hello 輸出的模組 toovisualize hello 資料及取得統計資料。

**當在預覽結果或在瀏覽器中的資料，資料列和資料行的 hello 數目是限定的。原因為何？**

因為大量資料可能會傳送 tooa 瀏覽器，資料大小不受限的 tooprevent 減緩 Machine Learning Studio。 toovisualize 所有 hello 資料/結果中，它的較佳 toodownload hello 資料，並使用 Excel 或其他工具。

### <a name="algorithms"></a>演算法
**Machine Learning Studio 中支援哪些現有的演算法？**

Machine Learning Studio 提供頂級演算法，例如 Scalable Boosted Decision 樹、Bayesian Recommendation 系統、Deep Neural Networks 和 Decision Jungles (由 Microsoft Research 開發)。 此外也包含可調整的開放原始碼機器學習套件，例如 Vowpal Wabbit。 Machine Learning Studio 支援多類別與二進位分類、迴歸和叢集的機器學習演算法。 請參閱 hello 的完整清單[機器學習模組][machine-learning-modules]。

**您會自動建議 hello 右機器學習演算法 toouse 提供我的資料嗎？**

否，但 Machine Learning Studio 有的幾個 toocompare hello 結果的每個演算法 toodetermine hello 適合您的問題。

**您是否有任何一種演算法挑選透過另一個則針對提供的 hello 演算法的指導方針？**

請參閱[如何 toochoose 演算法](machine-learning-algorithm-choice.md)。

**提供的 hello 演算法或撰寫的 R Python 嗎？**

否，這些演算法通常會寫入編譯語言 tooprovide 較佳的效能。

**是任何 hello 所提供的演算法的詳細資料？**

hello 文件提供一些資訊 hello 演算法並進行微調的參數會描述的 toooptimize hello 演算法，您可以使用。  

**線上學習是否有任何支援？**

否，目前只支援以程式設計方式進行重新訓練。

**可以使用內建模組的 hello 視覺化 hello 圖層的類神經網路模型嗎？**

否。

**可以以 C# 或其他語言建立自己的模組嗎？**

目前，您可以只使用 R toocreate 新自訂模組。

### <a name="r-module"></a>R 模組
**Machine Learning Studio 中可使用什麼 R 套件？**

Machine Learning Studio 支援超過 400 CRAN R 封裝，並如下 hello[目前清單](http://az754797.vo.msecnd.net/docs/RPackages.xlsx)所有包含的封裝。 此外，請參閱[擴充以 R 實驗](machine-learning-extend-your-experiment-with-r.md)toolearn 如何 tooretrieve 這樣列出自己。 如果您想要的 hello 封裝不是這份清單中，提供在 hello hello 套件 hello 名稱[使用者意見反應論壇](http://go.microsoft.com/fwlink/?LinkId=404231)。

**它是可能 toobuild 自訂 R 模組嗎？**

是，如需詳細資訊，請參閱 [在 Azure Machine Learning 中撰寫自訂 R 模組](machine-learning-custom-r-modules.md) 。

**是否有 R 適用的 REPL 環境？**

否，沒有 hello studio 中的 R 的任何讀取 Eval-列印-迴圈 (REPL) 環境。

### <a name="python-module"></a>Python 模組
**它是可能 toobuild 自訂 Python 模組嗎？**

目前不可以，但是您可以使用一或多個[執行 Python 指令碼][ python]模組 tooget hello 相同的結果。

**是否有 Python 適用的 REPL 環境？**

您可以使用 hello Jupyter 筆記本 Machine Learning Studio 中。 如需詳細資訊，請參閱 [介紹 Azure Machine Learning Studio 中的 Jupyter Notebook](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx)。

## <a name="web-service"></a>Web 服務
### <a name="retrain"></a>重新訓練
**如何以程式設計方式重新訓練 Azure Machine Learning 模型？**

使用 hello 重新訓練應用程式開發介面。 如需詳細資訊，請參閱 [以程式設計方式重塑機器學習模型](machine-learning-retrain-models-programmatically.md)。 範例程式碼也會提供 hello [Microsoft Azure 機器學習重新訓練的示範](https://azuremlretrain.codeplex.com/)。

### <a name="create"></a>建立
**在本機或在沒有網際網路連線的應用程式可以部署 hello 模型嗎？**

否。

**所有 Web 服務是否有預期的基準延遲？**

請參閱 hello [Azure 訂用帳戶限制](../azure-subscription-service-limits.md)。

### <a name="use"></a>使用
**何時需要 toorun 我預測模型以批次執行的要求回應服務與服務？**

hello 的要求回應服務 (RR) 是低延遲、 高延展的 web 服務，使用的 tooprovide 介面 toostateless 模型所建立和部署從 hello 實驗環境。 hello 批次執行服務 (BES) 是一項服務，以非同步方式分數資料記錄的批次。 hello BES 為輸入，例如 RR 使用的資料輸入。 hello 主要差異是 BES 會從各種來源，例如 Azure Blob 儲存體、 Azure 資料表儲存體、 Azure SQL Database、 HDInsight （hive 查詢） 和 HTTP 的來源讀取之記錄區塊。 如需詳細資訊，請參閱[如何 tooconsume Azure 機器學習 Web 服務](machine-learning-consume-web-services.md)。

**如何更新部署的 hello web 服務的 hello 模型？**

tooupdate 預測模型已部署的服務，修改並重新執行您用 tooauthor hello 實驗，並儲存 hello 定型的模型。 您擁有 hello 定型的模型可用的新版本之後，Machine Learning Studio 詢問您是否 tooupdate web 服務。 如需詳細資訊，關於如何 tooupdate 已部署的 web 服務，請參閱[部署機器學習 web 服務](machine-learning-publish-a-machine-learning-web-service.md)。

您也可以使用 hello Retraining 應用程式開發介面。
如需詳細資訊，請參閱 [以程式設計方式重塑機器學習模型](machine-learning-retrain-models-programmatically.md)。 範例程式碼也會提供 hello [Microsoft Azure 機器學習重新訓練的示範](https://azuremlretrain.codeplex.com/)。

**如何監控部署在實際執行環境中的 Web 服務？**

部署的預測模型之後，您就可以監視從 hello Azure 傳統入口網站 （僅傳統 web 服務） 或 hello Azure 機器學習 Web 服務網站。 每個已部署的服務都有其本身的儀表板，您可以在此處檢視該服務的監控資訊。 如需有關如何 toomanage 已部署的 web 服務，請參閱[管理 Web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)和[管理 Azure Machine Learning 工作區](machine-learning-manage-workspace.md)。

**有我可以在其中看到我的 RR/BES hello 輸出的位置嗎？**

RR，如 hello web 服務回應通常是在您看到 hello 結果。 您也可以撰寫它 tooAzure Blob 儲存體。 BES，如 hello 輸出都會寫入 tooa blob，根據預設。 您也可以撰寫 hello 輸出 tooa 資料庫或資料表，使用 hello[匯出資料][ export-data]模組。

**只能從 Machine Learning Studio 中建立的模型來建立 Web 服務嗎？**

不，您也可以直接使用 Jupyter Notebook 和 RStudio 來建立 Web 服務。

**哪裡可以找到有關錯誤碼的詳細資訊？**

如需錯誤碼與說明的清單，請參閱 [Machine Learning 模組錯誤碼](https://msdn.microsoft.com/library/azure/dn905910.aspx) 。

## <a name="scalability"></a>延展性
**什麼是 hello 延展性 hello web 服務？**

目前，hello 預設端點的佈建 20 並行 RR 要求每個端點。 您可以調整每個端點，這個 too200 並行要求，而且您可以延展中所述的每個 web 服務 too10、 000 每個 web 服務端點[擴充 Web 服務](machine-learning-scaling-webservice.md)。 對於 BES，每個端點一次可以處理 40 個要求，超過 40 個的其他要求則會排入佇列。 這些佇列的要求會自動以 hello 佇列電量。

**R 作業會分散於節點嗎？**

編號  

**我可以將多少資料用於訓練？**

Machine Learning Studio 中的模組支援常見使用案例的總 too10 GB 的密集的數值資料的資料集。 如果模組需要一個以上的輸入，hello 總所有輸入的大小為 10 GB。 您也可以取樣較大型資料集，方法是透過 Hive 查詢或 Azure SQL Database 查詢，或在擷取前利用[以計數學習][counts]模組進行前置處理。  

hello 下列類型的資料可以展開 toolarger 資料集特徵正規化期間而且會超過 10 GB 的限制的 tooless:

* 疏鬆
* 類別
* 字串
* 二進位資料

小於 10 GB 的限制的 toodatasets hello 下列模組︰

* Recommender 模組
* 合成少數類過採樣技術 (SMOTE) 模組
* 指令碼模組：R、Python SQL
* 模組 hello 輸出的資料大小可能大於輸入的資料大小，例如聯結 」 或 「 特徵雜湊
* 當反覆運算數目非常大時的交叉驗證、微調模型超參數、序數迴歸和一對多的多類別

對於大於幾個 Gb 的資料集上, 傳資料 tooAzure 儲存體或 Azure SQL Database，或使用 HDInsight 而非直接從本機檔案上傳。

**是否有任何向量大小限制嗎？**

資料列和資料行是每個限制的 toohello.NET 的限制上限 Int: 2147483647。

**是否可以調整 hello hello 執行 hello web 服務的虛擬機器的大小？**

否。  

## <a name="security-and-availability"></a>安全性和可用性
**根據預設，誰可以存取 hello web 服務的 hello http 端點？我要如何限制存取 toohello 端點？**

部署 Web 服務之後，我們會建立該服務的預設端點。 使用其 API 金鑰，可以呼叫 hello 預設端點。 您可以加入多個端點，其中包含自己索引鍵從 hello Azure 傳統入口網站或以程式設計方式使用 hello Web 服務管理 Api。 存取金鑰都是必要的 toomake 呼叫 toohello web 服務。 如需詳細資訊，請參閱[如何 tooconsume Azure 機器學習 Web 服務](machine-learning-consume-web-services.md)。

**如果找不到我的 Azure 儲存體帳戶，會發生什麼情況？**

Machine Learning Studio 依賴使用者提供 Azure 儲存體帳戶 toosave 中繼資料時，它會執行 hello 工作流程。 在建立的工作區時，這個儲存體帳戶會提供 tooMachine Learning Studio。 Hello 後會建立工作區中，如果 hello 儲存體帳戶刪除不再找到、 hello 工作區將會停止運作，且所有實驗，區將會失敗。

如果您不小心刪除 hello 儲存體帳戶，來重新建立 hello 儲存體帳戶，以相同的名稱，在 hello hello hello 與相同的區域刪除儲存體帳戶。 在這之後，重新同步處理 hello 存取金鑰。

**如果我的儲存體帳戶存取金鑰未同步，會發生什麼情況？**

Machine Learning Studio 依賴使用者提供 Azure 儲存體帳戶 toostore 中繼資料時，它會執行 hello 工作流程。 建立工作區，以及與該工作區相關聯 hello 便捷鍵時，這個儲存體帳戶會提供 tooMachine Learning Studio。 如果 hello 工作區建立之後變更 hello 便捷鍵，hello 工作區就無法再存取 hello 儲存體帳戶。 它會停止運作，而該工作區中的所有實驗將會失敗。

如果您變更儲存體帳戶存取金鑰時，所使用的 hello 工作區中的重新同步處理 hello 便捷鍵 hello Azure 傳統入口網站。  

## <a name="support-and-training"></a>支援和訓練
**哪裡可以取得 Azure Machine Learning 的訓練？**

hello [Azure 機器學習服務文件中心](https://azure.microsoft.com/services/machine-learning/)影片教學課程和如何 tooguides 主機。 這些逐步指南介紹 hello 服務，並說明 hello 資料科學的匯入資料、 清除資料、 建立預測模型，以及將其部署在生產環境中使用 Azure Machine Learning 的生命週期。

我們持續加入新的材料 toohello 機器學習中心。 您可以送出要求 hello 在機器學習中心上的其他學習材料[使用者意見反應論壇](https://windowsazure.uservoice.com/forums/257792-machine-learning)。

您也可以在 [Microsoft Virtual Academy](http://www.microsoftvirtualacademy.com/training-courses/getting-started-with-microsoft-azure-machine-learning)尋找訓練。

**如何取得 Azure Machine Learning 的支援？**

tooget Azure 機器學習，技術支援人員移過[Azure 支援](/support/options/)，然後選取**Machine Learning**。

Azure Machine Learning 在 MSDN 上也設有社群論壇，可供您詢問 Azure Machine Learning 的相關問題。 hello Azure Machine Learning 小組監視 hello 論壇。 跳過[Azure 論壇](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning)。

## <a name="billing-questions"></a>計費問題
**機器學習服務如何計費？**

Azure Machine Learning 有兩個元件：Machine Learning Studio 與 Machine Learning Web 服務。

雖然您正在評估 Machine Learning Studio，您可以使用 hello 免費的計費層。 hello 免費層也可讓您部署的有限容量傳統 web 服務。

如果您決定 Azure Machine Learning 符合您的需求，您可以申請 hello Standard 價格區間。 向上 toosign，您必須有 Microsoft Azure 訂用帳戶。

在 hello 標準層次中，您所要支付每月在 Machine Learning Studio 中定義的每個工作區。 當您執行實驗 hello studio 中時，您所要支付計算資源時您所執行的實驗。 當您部署的傳統 web 服務交易，並計算小時的計費 hello 付制為基礎。

新型 (Resource Manager 架構) Web 服務引進了可提高成本可預測性的計費方案。 階層式定價提供折扣優惠 toocustomers 需要大量的容量。

當您建立計畫時，您就會認可 tooa 固定成本所隨附的應用程式開發介面運算時數和 API 交易內含數量。 如果您需要更包含的數量時，您可以加入執行個體 tooyour 計劃。 如果您需要非常多的包含數量，您可以選擇較高層級的方案，其可提供非常多的包含數量和更好的折扣費率。

Hello 中現有的執行個體包含的數量都用完之後，其他使用方式被收費 hello overage hello 計費方案層與相關聯。

> [!NOTE]
包含的數量重新配置每隔 30 天，並包含未使用的數量不會彙總 toohello 下一個週期。

如需其他計費和價格資訊，請參閱 [機器學習服務價格](https://azure.microsoft.com/pricing/details/machine-learning/)。

**機器學習服務是否有免費試用版？**

 Azure Machine Learning 有 [Machine Learning 價格](https://azure.microsoft.com/pricing/details/machine-learning/)中說明的免費訂用帳戶選項。 Machine Learning Studio 有八小時快速評估試用版，可在您登入太[Machine Learning Studio](https://studio.azureml.net/?selectAccess=true&o=2)。

 此外，註冊 Azure 免費試用版後，您可以試用任何 Azure 服務一個月。 toolearn 深入了解 hello Azure 免費試用版，請瀏覽[Azure 免費試用常見問題集](https://azure.microsoft.com/pricing/free-trial-faq/)。

**什麼是交易？**

交易代表 Azure Machine Learning 所回應的 API 呼叫。 來自要求回應服務 (RRS) 和批次執行服務 (BES) 呼叫的交易會彙總起來，並根據計費方案來收費。

**我可以使用包含 hello 交易數量計劃中 RR 和 BES 交易？**

是，來自 RRS 和 BES 的交易會彙總起來，並根據計費方案來收費。

**什麼是 API 計算時數？**

應用程式開發介面計算是 hello 計費單位 hello 次應用程式開發介面呼叫 take toorun 使用機器學習來計算資源。 系統會彙總所有呼叫以便計費。

**典型的生產 API 呼叫需要花費多久時間？**

實際執行應用程式開發介面呼叫時間變化相當大，通常介於數百個毫秒 tooa 幾秒鐘的時間。 有些應用程式開發介面呼叫可能需要分鐘視 hello hello 資料處理和機器學習模型的複雜度而定。 hello 最佳方式 tooestimate 生產應用程式開發介面呼叫時間不 toobenchmark hello 機器學習服務上的模型。

**什麼是 Studio 計算時數？**

Studio 計算小時是 hello 計費單位的 hello 彙總的時間，將實驗在 studio 中使用計算資源。

**在新的 （Azure 資源管理員為基礎） 的 web 服務中，是 hello 開發/測試層所謂的？**

資源管理員為基礎的 web 服務提供多個層，您可以使用 tooprovision 您的計費方案。 hello 開發/測試定價層提供有限且包含數量可讓您 tootest 實驗為 web 服務而不會產生成本。 您擁有 hello 機會 toosee 它的運作方式。

**儲存體需要另外付費嗎？**

hello 機器學習免費層次不需要或不允許不同的儲存體。 hello 機器學習標準層需要使用者 toohave Azure 儲存體帳戶。 Azure 儲存體是[另外收費](https://azure.microsoft.com/pricing/details/storage/)。

**Machine Learning 是否支援高可用性？**

是。 如需詳細資訊，請參閱[機器學習定價](https://azure.microsoft.com/en-us/pricing/details/machine-learning/)hello 服務等級協定 (SLA) 的描述。

**我的生產 API 呼叫將使用哪些特定種類的計算資源來執行？**

hello 機器學習服務是一個多租用戶的服務。 Hello 後端所使用的實際計算資源而有所不同，而且會針對效能和可預測性最佳化。

### <a name="management-of-new-resource-manager-based-web-services"></a>新型 (Resource Manager 架構) Web 服務的管理
**如果我刪除方案會發生什麼事？**

從您的訂用帳戶中，移除 hello 計畫，您所要支付計算按比例分配的使用方式。

> [!NOTE]
您無法刪除 Web 服務正在使用的方案。 toodelete hello 計劃，您必須指派新計劃 toohello web 服務，或者刪除 hello web 服務。

**什麼是方案執行個體？**

計劃的執行個體是您可以加入 tooyour 計費計劃包含數量的單位。 為計費方案選取計費層時，方案便會隨附一個執行個體。 如果您需要更包含的數量時，您可以加入 hello 選計費層 tooyour 計劃的執行個體。

**可以新增多少個方案執行個體？**

您可以訂用帳戶中有一個 hello 開發/測試定價層的執行個體。

在標準 S1、標準 S2 和標準 S3 層中，您可以視需要新增多個執行個體。

> [!NOTE]
根據您預期的使用方式，它可能是更符合成本效益更包含數量 tooupgrade tooa 層而非新增執行個體 toohello 目前層。

**變更方案層級 (升級/降級) 時會發生什麼事？**

hello 舊計劃已刪除，且 hello 目前使用量計費計算按比例分配的基礎。 與 hello 完整包含的數量 hello 升級/降級層的新計畫會建立 hello 期間 hello 其餘部分。

> [!NOTE]
包含的數量是針對每個期間來配置，未使用的數量不會展期。

**當我計劃中增加 hello 執行個體時，發生什麼事？**

數量則包含在計算按比例分配的基礎，而且可能需要 24 小時 toobe 有效。

**刪除方案執行個體時會發生什麼事？**

hello 實例會從您的訂用帳戶中，移除與您所要支付計算按比例分配的使用方式。

### <a name="sign-up-for-new-resource-manager-based-web-services-plans"></a>註冊新型 (Resource Manager 架構) Web 服務方案
**如何註冊方案？**

您有兩種方式 toocreate 計費方案。

當您第一次部署 Resource Manager 架構 Web 服務時，您可以選擇現有方案，或建立新方案。

您在這種方式中建立的計劃不會在您預設的地區，而且您的 web 服務部署的 toothat 區域。

如果您想 toodeploy 服務 tooregions 預設區域以外，您可能想 toodefine 計費的計劃之前部署您的服務。

在此情況下，您可以登入 toohello Azure 機器學習 Web 服務入口網站，並移 toohello 計劃 頁面。 您可以在該處新增方案、刪除方案，以及修改現有方案。

**哪一個計劃我應該選擇 toostart 關閉與？**

我們建議您您開始使用 hello 標準 S1 層和監視您的服務使用方式。 如果您發現您正在使用您包含的數量快速，您可以加入執行個體或移動 tooa 更高的層，並取得更好的折扣的率。 在整個計費週期內，您都可以視需要調整計費方案。

**哪些區域可用 hello 新計劃中？**

新的計費計畫 hello 可用 hello 三個生產區域中，我們支援 hello 新的 web 服務：

* 美國中南部
* 西歐
* 東南亞

**我在多個區域擁有 Web 服務。是否每個區域都需要一個方案？**

是。 不同區域有不同的方案價格。 當您部署的 web 服務 tooanother 區域時，您需要 tooassign 為特定 toothat 區域計劃。 如需詳細資訊，請參閱[不同區域提供的產品]( https://azure.microsoft.com/regions/services/)。

### <a name="new-web-services-overages"></a>新型 Web 服務：超額
**如何檢查 Web 服務使用量是否超額？**

您可以檢視 hello 使用量 hello Azure 機器學習 Web 服務入口網站中的 hello 計畫頁面上所有您計劃。 登入 toohello 入口網站，然後按一下hello**計劃**功能表選項。

在 hello**交易**和**計算**hello 資料表的資料行，您可以看到 hello 包含數量的 hello 計劃並使用 hello 百分比。

**使用向上 hello 時，會發生什麼事數量納入 hello 開發/測試定價層？**

下一個週期或移動 tooa 付費層之前，會停止直到 hello 具有定價層指派 toothem 開發/測試服務。

**針對傳統 Web 服務和超額的新 (Resource Manager 架構) Web 服務，如何計算要求回應 (RRS) 和批次 (BES) 工作負載的價格？**

針對 RR 工作負載，您負責確定每個 API 交易呼叫以及與這些要求相關聯的 hello 運算時間。 您的應用程式開發介面呼叫的 hello 總數乘以 hello 價格每 1000 （依比例由個別的交易） 的交易都會計算 RR 生產應用程式開發介面交易成本。 RR 應用程式開發介面實際執行應用程式開發介面計算小時成本會計算為 hello 數量乘以 hello API 交易總數，乘以 hello 單價生產應用程式開發介面計算小時每個應用程式開發介面呼叫 toorun 所需的時間。

比方說，標準 S1 超額部分，如 1000000 API 交易 0.72 秒的每個 toorun 會導致 (1000000 * $0.50/1k API 交易) 在 $500，實際執行應用程式開發介面交易成本和 (1000000 * 0.72 秒 * $2/hr) $400 生產應用程式開發介面計算中總計 $900 個小時。

BES 工作負載，您需要付費 hello 中相同的方式。 不過，hello API 交易成本表示您送出，批次作業的 hello 數目，而 hello 計算成本表示 hello 運算時間的批次作業相關聯。 提交的 hello 總數乘以 hello 價格每 1000 （依比例由個別的交易） 的交易都會計算 BES 生產應用程式開發介面交易成本。 BES 應用程式開發介面實際執行應用程式開發介面計算小時成本會以 hello 數量乘以 hello 資料列總數乘以 hello 總數乘以 hello 單價生產應用程式開發介面作業的工作中您工作 toorun 中每個資料列所需的時間計算計算小時。 當您使用 hello 機器學習 [小算盤] 時，hello 交易計量表代表 hello 的作業數目，您計劃 toosubmit，與 hello 每筆交易的時間欄位代表 hello 結合的所有資料列中每個作業 toorun 所需的時間。

例如，假設採用標準 S1 超額，而且您每天提交 100 個作業，每個作業包含 500 個資料列，且執行時間各為 0.72 秒。 您的每月超額費用會是 (每天 100 個作業 = 每月 3,100 個作業 * 0.50 美元/1,000 個 API 交易) 1.55 美元的生產 API 交易費用和 (500 個資料列 * 0.72 秒 * 3,100 個作業 * 2 美元/小時) 620 美元的生產 API 計算時數，總計 621.55 美元。

### <a name="azure-machine-learning-classic-web-services"></a>Azure Machine Learning 傳統 Web 服務
**是否還有提供隨用隨付？**

是，Azure Machine Learning 中仍然提供傳統的 Web 服務。  

### <a name="azure-machine-learning-free-and-standard-tier"></a>Azure Machine Learning 的免費層和標準層
**什麼包含在 hello Azure 機器學習免費層？**

hello Azure 機器學習免費層是預定的 tooprovide 深入了解簡介 toohello Azure Machine Learning Studio。 您只需要為 Microsoft 帳戶 toosign 註冊。 hello 免費層包含免費存取 tooone Azure Machine Learning Studio 工作區中的每個[Microsoft 帳戶](https://www.microsoft.com/account/default.aspx)。 在此層級，您可以使用向上 too10 GB 的儲存體，並實施模型做為暫存應用程式開發介面。 免費層工作負載不包含在 SLA 內，且僅供開發與個人使用。 

免費層次的工作區具有下列限制的 hello:

* 工作負載無法藉由連接 tooan 執行 SQL Server 的內部部署伺服器來存取資料。
* 您無法部署新的 Resource Manager 基底 Web 服務。


**什麼包含在 hello Azure 機器學習標準層和計劃？**

hello Azure 機器學習標準層是付費的實際執行版本的 Azure Machine Learning Studio。 hello Azure Machine Learning Studio 每月費用計費每個工作區中每個月為基礎和計算按比例分配的局部月數。 Azure Machine Learning Studio 實驗時數會依據進行中實驗的每個計算時數收費。 不足的時數會按比例收費。  

hello Azure 機器學習 API 服務為計費根據它是否傳統 web 服務或新的 （資源管理員為基礎） 的 web 服務。

hello 遵循費用會彙總每個訂用帳戶的工作區。

* 機器學習服務工作區訂用帳戶： hello Machine Learning 工作區的訂用帳戶會提供存取 tooa Machine Learning Studio 工作區是按月計價。 hello studio 和 tooutilize hello 在生產環境中應用程式開發介面需要的 toorun 實驗 hello 訂用帳戶。
* Studio 實驗小時： 這個計費表彙總累加的實驗執行 Machine Learning Studio 中的所有計算費用，並在預備環境的 hello 呼叫執行實際執行應用程式開發介面。
* 存取由 tooan 執行在程式訓練的模型中的 SQL Server 的內部部署伺服器連接和計分的資料。
* 傳統 Web 服務：
  * 生產 API 計算時數：此計量包含在生產環境中執行的 Web 服務所產生的計算費用。
  * 實際執行應用程式開發介面的交易 （1000): 這個計費表包括會累加的每個呼叫 tooyour 生產環境 web 服務的費用。

除了上述費用，在資源管理員為基礎的 web 服務的 hello 案例中的 hello 費用會彙總的 toohello 選取計劃：

* 這個計費表標準 S1/S2/S3 API 計劃 （單位）： 表示已選取的資源管理員為基礎的 web 服務的執行個體 hello 型別。
* 標準 S1/S2/S3 Overage API 運算時數： 這個計費表包括會累加的現有執行個體中的 hello 包含數量會用完後才在生產中執行的資源管理員為基礎的 web 服務的計算費用。 hello 額外使用量收費 hello overate S1/S2/S3 計劃層與相關聯的速率。
* 標準 S1/S2/S3 超額部分應用程式開發介面的交易 （1,000s): 這個計費表包含每個呼叫 tooyour 實際執行資源管理員為基礎的 web 服務 hello 納入現有的執行個體的數量之後用完會累算費用。 hello 額外使用量收費 hello overate S1/S2/S3 計劃層相關聯的速率。
* 包含數量的應用程式開發介面運算時數： 與資源管理員為基礎的 web 服務，這個計費表代表 hello 包含數量的應用程式開發介面運算時數。
* 納入數量 API 交易 （1,000s): 使用資源管理員為基礎的 web 服務，這個計費表代表 hello 包含 API 交易數量。

**如何註冊 Azure Machine Learning 免費層？**

您只需要 Microsoft 帳戶。 跳過[Azure Machine Learning 首頁](https://azure.microsoft.com/services/machine-learning/)，然後按一下**立即開始**。 使用 Microsoft 帳戶登入，系統便會為您建立免費層工作區。 您可以啟動 tooexplore，並立即建立機器學習實驗。

**如何註冊 Azure Machine Learning 標準層？**

您必須先存取 tooan Azure 訂用帳戶 toocreate 標準 Machine Learning 工作區。 您可以註冊 30 天免費試用 Azure 訂用帳戶和更新版本的升級 tooa 付費型 Azure 訂用帳戶，或者，您可以購買付費 Azure 訂用帳戶徹底。 然後您可以從 hello Microsoft Azure 傳統入口網站建立 Machine Learning 工作區之後您就可以存取 toohello 訂用帳戶。 檢視 hello[逐步指示](https://azure.microsoft.com/trial/get-started-machine-learning-b/)。

或者，您可以邀請由標準的機器學習服務工作區擁有者 tooaccess hello 擁有者的工作區。

**可以指定自己的 Azure Blob 儲存體帳戶 toouse 與 hello 免費層嗎？**

否，hello 標準層是 hello 機器學習服務層所導入的 hello 之前，對等 toohello 版本。

**可以部署我的機器學習模型做為應用程式開發介面，hello 免費層中嗎？**

是，您可以實施機器學習模型 toostaging API services hello 免費層的一部分。 tooput hello 接 API 服務移到實際執行環境和生產環境端點取得 hello 實際運作的服務，您必須使用 hello Standard 價格區間。

**Hello Azure 免費試用版與 Azure 機器學習免費層之間的差異為何？**

hello [Microsoft Azure 免費試用](https://azure.microsoft.com/free/)提供信用額度，您可以套用 tooany Azure 服務的一個月。 hello Azure 機器學習 Free 層提供連續存取特別 tooAzure Machine Learning 針對非生產工作負載。

**如何從 hello 免費層 toohello 標準層中移動實驗？**

toocopy hello 免費層 toohello 標準層將實驗：

1. 登入 tooAzure Machine Learning Studio 中，並請確定您可以看到 hello 免費工作區和 hello hello hello 上方導覽列中的工作區選取器中的 [標準] 工作區。
2. 如果您是在 hello 標準工作區，請切換 tooFree 工作區。
3. 在 hello 實驗清單檢視中，選取 實驗，您會想 toocopy，，然後按一下hello**複製**命令按鈕。
4. 從 hello 對話方塊中，開啟時，請選取 hello 標準工作區，然後按一下hello**複製** 按鈕。
   所有 hello 相關聯的資料集，定型的模型，會複製與 hello 實驗 hello 標準工作區。
5. 您需要 toorerun hello 實驗，並重新發佈 web 服務 hello 標準工作區中的。

### <a name="studio-workspace"></a>Studio 工作區
**不同的工作區會有不同的帳單嗎？**

一份帳單上，工作區費用會依每個適用的度量而個別細分。

**我的實驗作業會在何種特定類型的計算資源上進行？**

hello 機器學習服務是一個多租用戶的服務。 Hello 後端所使用的實際計算資源而有所不同，而且會針對效能和可預測性最佳化。

### <a name="guest-access"></a>來賓存取
**什麼是來賓存取 tooAzure Machine Learning Studio？**

「來賓存取」是有限制的試用經驗。 您可以在不經驗證的情況下，於 Azure Machine Learning Studio 中免費建立及執行實驗。 客體工作階段是在非持續性 （無法儲存），限制 tooeight 小時。 其他限制包括缺少 R 和 Python 支援、缺少預備 API，以及有限的資料集大小和儲存體容量。 相較之下，選擇 toosign 使用 Microsoft 帳戶的使用者擁有完整存取 toohello 免費層的機器學習 Studio 之前，描述其中包括持續性工作區和更完整的功能。 toochoose 免費的機器學習遇到按一下**開始**上[https://studio.azureml.net](https://studio.azureml.net)，然後選取**猜測存取**或使用 Microsoft 登入。帳戶。

<!-- Module References -->
[image-reader]: https://msdn.microsoft.com/library/azure/893f8c57-1d36-456d-a47b-d29ae67f5d84/
[join]: https://msdn.microsoft.com/library/azure/124865f7-e901-4656-adac-f4cb08248099/
[machine-learning-modules]: https://msdn.microsoft.com/library/azure/6d9e2516-1343-4859-a3dc-9673ccec9edc/
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[python]: https://msdn.microsoft.com/library/azure/CDB56F95-7F4C-404D-BDE7-5BB972E6F232
[counts]: https://msdn.microsoft.com/library/azure/dn913056.aspx
