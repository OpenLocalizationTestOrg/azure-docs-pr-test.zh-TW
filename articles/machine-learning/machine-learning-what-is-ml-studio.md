---
title: "aaaWhat 是 Azure Machine Learning Studio？ | Microsoft Docs"
description: "從已準備就緒可供使用之演算法與模組的程式庫快速建置模型的拖放工具 - Azure ML Studio 概觀。"
keywords: azure machine learning,azure ml, ml studio
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e65c8fe1-7991-4a2a-86ef-fd80a7a06269
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: a25f2d9e75d088a37930de98240c6e14c9567fa4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-machine-learning-studio"></a>什麼是 Azure Machine Learning Studio？
Microsoft Azure Machine Learning Studio 是共同作業、 拖放的工具，您可以使用 toobuild、 測試及部署您的資料的預測分析解決方案。 Machine Learning Studio 會以 Web 服務方式發佈模型，讓自訂應用程式或 BI 工具 (例如 Excel) 都能夠很容易地使用。

Machine Learning Studio 讓資料科學、預測分析、雲端資源和您的資料齊聚一堂！

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-machine-learning-studio-interactive-workspace"></a>hello Machine Learning Studio 的互動式工作區
toodevelop 預測分析模型，您通常會使用資料從一個或多個來源、 轉換和分析透過各種不同的資料操作和統計函數，該資料，並產生的結果集。 開發此類模型是一種反覆式過程。 當您修改 hello 各種函式和其參數、 結果聚合，直到您滿意您有定型、 有效率的模型。

**Azure Machine Learning Studio**您互動、 視覺化工作區 tooeasily 建置，可讓測試及逐一查看預測分析模型。 您拖放***資料集***及分析***模組***畫布互動式，它們連接在一起的 tooform***實驗***，在機器學習中執行Studio。 在模型設計 tooiterate，編輯 hello 實驗中的，儲存複本，如有需要，再執行一次。 當您準備好時，您可以將轉換您***定型實驗***tooa***預測實驗***，然後將它做為發行***web 服務***以便可以存取您的模型其他人。

沒有不需要任何程式設計，只要以視覺化方式連接資料集和模組 tooconstruct 預測分析模型。

> [!TIP]
> toodownload 及列印的圖表，hello Machine Learning Studio 中，功能的概觀，請參閱[Azure Machine Learning Studio 功能的概觀圖表](machine-learning-studio-overview-diagram.md)。
> 
> 

![Azure ML Studio 圖表：建立實驗、讀取許多來源的資料、寫入評分的資料及寫入模型。][ml-studio-overview]

## <a name="get-started-with-machine-learning-studio"></a>開始使用 Machine Learning Studio
當您第一次輸入[Machine Learning Studio](https://studio.azureml.net)看到 hello**首頁**頁面。 您可以從這裡檢視文件、影片、網路研討會，以及尋找其他重要資源。

按一下左上方 hello 功能表 ![功能表](media/machine-learning-what-is-ml-studio/menu.png) 您會看到幾個選項。

### <a name="cortana-intelligence"></a>Cortana Intelligence
按一下**Cortana 智慧**和您將會進入 hello toohello 首頁[Cortana 智慧套件](https://www.microsoft.com/cloud-platform/cortana-intelligence-suite)。 hello Cortana 智慧套件是完全受管理的巨量資料，並為智慧型動作 advanced analytics suite tootransform 您的資料。 請參閱 hello 套件首頁，如完整的文件，包括客戶劇本。

### <a name="azure-machine-learning"></a>Azure Machine Learning
有兩個選項在這裡，**首頁**，在您啟動，hello 頁面和**Studio**。

按一下**Studio**和您將會進入 toohello **Azure Machine Learning Studio**。 第一次系統會詢問 toosign 中使用您的 Microsoft 帳戶或工作或學校帳戶。 一旦登入，您會看到下列索引標籤左側 hello hello:

* **專案** - 代表單一專案之實驗、資料集、Notebook 和其他資源的集合
* **實驗** - 已建立及執行或儲存為草稿的實驗
* **Web 服務** - 已從您的實驗部署的 Web 服務
* **Notebook** - 您已建立的 Jupyter Notebook
* **資料集** - 您已上傳到 Studio 的資料集
* **定型模型** - 您已在實驗中訓練並儲存在 Studio 中的模型
* **設定**-設定您的帳戶和資源，您可以使用 tooconfigure 的集合。

### <a name="gallery"></a>資源庫
按一下**圖庫**和您將會進入 toohello  **[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com/)**。 hello 圖庫是其中的資料科學家和開發人員社群分享使用 hello Cortana 智慧套件的元件建立方案的位置。

如需 hello 組件庫的詳細資訊，請參閱[共用及探索 hello Cortana 智慧組件庫中的方案](machine-learning-gallery-how-to-use-contribute-publish.md)。

## <a name="components-of-an-experiment"></a>實驗的元件
提供資料 tooanalytical 模組，您連接在一起的資料集包含實驗 tooconstruct 預測分析模型。 明確地說，有效的實驗有三個特性：

* hello 實驗具有至少一個資料集和一個模組
* 資料集可能是已連線的唯一 toomodules
* 模組可能連接的 tooeither 資料集或其他模組
* 所有模組的輸入連接埠必須有一些連接 toohello 資料流
* 必須設定每個模組的所有必要參數

您可以從頭建立實驗，或者使用現有的範例實驗做為範本。 如需詳細資訊，請參閱[複製範例實驗 toocreate 新機器學習實驗](machine-learning-sample-experiments.md)。

如需建立簡易實驗的範例，請參閱 [在 Azure Machine Learning Studio 中建立簡易實驗](machine-learning-create-experiment.md)。

如需建立預測性分析方案的更完整逐步解說，請參閱 [使用 Azure Machine Learning 開發預測方案](machine-learning-walkthrough-develop-predictive-solution.md)。

### <a name="datasets"></a>資料集
資料集是已經過的資料上傳 tooMachine Learning Studio 使用於 hello 模型程序。 範例資料集的數目隨附於 Machine Learning Studio tooexperiment，如，您可以上傳多個資料集，您需要的時候。 以下是隨附資料集的一些例子：

* **各種汽車的 MPG 資料** - 汽車的每加侖英里 (MPG) 值，以汽缸數、馬力等來識別。
* **乳癌資料** - 乳癌診斷資料。
* **森林火災資料** - 葡萄牙西北部的森林火災範圍

當您建立實驗可以從清單中選擇 hello 可用的資料集的 toohello 方 hello 畫布。

如需包含 Machine Learning Studio 中的範例資料集的清單，請參閱[使用 Azure Machine Learning Studio 中的 hello 取樣資料集](machine-learning-use-sample-datasets.md)。

### <a name="modules"></a>模組
模組是指您在資料上可執行的演算法。 Machine Learning Studio 即會從資料輸入函式 tootraining、 計分，以及驗證程序的模組數目。 以下是隨附模組的一些例子：

* [轉換 tooARFF] [ convert-to-arff] -將轉換.NET 序列化資料集 tooAttribute 關聯檔案格式 (ARFF)。
* [計算基本統計資料][elementary-statistics] - 計算基本統計資料，例如平均值、標準差等。
* [線性迴歸][linear-regression] - 建立線上梯度下降線性迴歸模型。
* [評分模型][score-model] - 給訓練的分類或迴歸模型評分。

當您建立實驗可以從清單中選擇 hello 可使用的模組 toohello 方 hello 畫布。  

模組可能會有一組您可以使用 tooconfigure hello 模組的內部演算法的參數。 當您選取 hello 畫布上的模組時，hello 模組參數會顯示在 hello**屬性**窗格 toohello hello 畫布的權限。 您可以修改您的模型中該窗格 tootune hello 參數。

某些說明瀏覽可用的機器學習演算法的 hello 大型的程式庫，請參閱[如何為 Microsoft Azure 機器學習 toochoose 演算法](machine-learning-algorithm-choice.md)。

## <a name="deploying-a-predictive-analytics-web-service"></a>部署預測性分析 Web 服務
當您的預測性分析模型準備好時，可以從 Machine Learning Studio 將它部署為 Web 服務。 如需此程序的詳細資訊，請參閱 [部署 Azure Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。

[ml-studio-overview]:./media/machine-learning-what-is-ml-studio/azure-ml-studio-diagram.jpg

<!-- Module References -->
[convert-to-arff]: https://msdn.microsoft.com/library/azure/62d2cece-d832-4a7a-a0bd-f01f03af0960/
[elementary-statistics]: https://msdn.microsoft.com/library/azure/3086b8d4-c895-45ba-8aa9-34f0c944d4d3/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
