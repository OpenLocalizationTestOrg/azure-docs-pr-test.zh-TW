---
title: "aaaHow Azure 機器學習模型會成為 web 服務 |Microsoft 文件"
description: "概觀 hello 機制的方式從開發您 Azure 機器學習模型進行試驗 tooan 實際運作 Web 服務。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 25e0c025-f8b0-44ab-beaf-d0f2d485eb91
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 2bbe09fa8fa22662cf8ec4a8b6249d23c87c8ddf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-a-machine-learning-model-progresses-from-an-experiment-tooan-operationalized-web-service"></a>如何在機器學習模型轉換時自動從實驗 tooan 實際運作 Web 服務
Azure Machine Learning Studio 提供可讓您 toodevelop，執行互動式畫布、 測試及逐一查看***實驗***代表預測分析模型。 有各種可用的模組可以︰

* 將資料輸入到實驗
* 操作 hello 資料
* 使用機器學習服務演算法來訓練模型
* 計分 hello 模型
* 評估 hello 結果
* 輸出最終值

一旦滿意實驗，您就可以將其部署為***傳統 Azure Machine Learning Web 服務***或***新式 Azure Machine Learning Web 服務***，讓使用者可以將新的資料傳送給它並接收結果。

在本文中，我們會產生 hello 機制的方式從開發實驗 tooan 您機器學習模型進行實際運作 Web 服務的概觀。

> [!NOTE]
> 有其他方式 toodevelop 和部署的機器學習模型，但這篇文章會著重於您如何使用 Machine Learning Studio。 例如，tooread 如何 toocreate 傳統預測的 Web 服務使用 R，請參閱 hello 部落格文章的描述[組建與部署預測 Web 應用程式使用 RStudio Azure ML](http://blogs.technet.com/b/machinelearning/archive/2015/09/25/build-and-deploy-a-predictive-web-app-using-rstudio-and-azure-ml.aspx)。
> 
> 

Azure Machine Learning Studio 時設計的 toohelp 您開發並部署*預測分析模型*，很可能 toouse Studio toodevelop 實驗不包含預測分析模型。 比方說，實驗可能只要輸入的資料、 處理它，並將結果輸出 hello。 就像是預測分析實驗中，您可以部署為 Web 服務時，此非預測實驗，但很簡單的程序因為 hello 實驗並不是定型或計分的機器學習模型。 雖然並非 hello 一般 toouse Studio，如此一來，我們將會包含在 hello 討論，讓我們可以提供 Studio 的運作方式的完整說明。

## <a name="developing-and-deploying-a-predictive-web-service"></a>開發及部署預測性 Web 服務
以下是典型的方案之後，當您開發並部署使用 Machine Learning Studio hello 階段：

![部署流程](media/machine-learning-model-progression-experiment-to-web-service/model-stages-from-experiment-to-web-service.png)

*圖 1 - 一般預測性分析模型的階段*

### <a name="hello-training-experiment"></a>hello 定型實驗
hello***定型實驗***是開發您的 Web 服務，Machine Learning Studio 中的 hello 初始階段。 hello 定型實驗 hello 用途是 toogive 位置 toodevelop，測試、 逐一查看，並最終訓練的機器學習模型。 您甚至定型多個模型同時您尋找 hello 最佳解決方案，但是一旦您完成實驗您將會選取單一定型模型，並消除從 hello 實驗 hello rest。 如需開發預測性分析實驗的範例，請參閱 [在 Azure Machine Learning 中為信用風險評估開發預測性分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)。

### <a name="hello-predictive-experiment"></a>hello 預測實驗
一旦已定型的模型定型實驗中，按一下**設定 Web 服務**選取**預測 Web 服務**在 Machine Learning Studio tooinitiate hello 轉換程序訓練實驗 tooa***預測實驗***。 hello hello 預測實驗的用途是 toouse 您定型的模型 tooscore 新的資料，以 hello 最後變得實際運作的 Azure Web 服務為目標。

這項轉換會為您完成透過 hello 下列步驟：

* 轉換 hello 組用於定型成單一模組的模組，並將它儲存為定型的模型
* 排除不相關的任何多餘模組 tooscoring
* 加入輸入和輸出 hello 最終的 Web 服務將使用的連接埠

可能有多個您想要 toomake tooget 您預測實驗準備 toodeploy 為 Web 服務的變更。 例如，如果您想 hello Web 服務 toooutput 結果的子集，您可以加入之前 hello 輸出連接埠的篩選模組。

此轉換程序中不會捨棄 hello 定型實驗。 Hello 程序完成時，在 Studio 中擁有兩個索引標籤： 一個用於 hello 定型實驗，一個 hello 預測實驗。 如此一來，您可以變更 toohello 定型實驗之前您部署您的 Web 服務，並重建 hello 預測實驗。 或您可以儲存一份 hello 定型實驗 toostart 另一行試驗。

> [!NOTE]
> 當您按一下**預測 Web 服務**您啟動自動偵測程序 tooconvert 定型實驗 tooa 預測實驗，而這都適用於大部分情況。 如果定型實驗複雜 （例如，具有您聯結在一起的訓練的多個路徑），您可能會偏好 toodo 這項轉換以手動方式。 如需詳細資訊，請參閱[如何 tooprepare Azure Machine Learning Studio 中的部署模型](machine-learning-convert-training-experiment-to-scoring-experiment.md)。
> 
> 

### <a name="hello-web-service"></a>hello Web 服務
一旦您認為您的預測實驗已經就緒，您就可以根據 Azure Resource Manager，將服務部署為傳統 Web 服務或新式 Web 服務。 toooperationalize 您將它做為部署的模型*傳統的機器學習 Web 服務*，按一下 **部署 Web 服務**選取**部署 Web 服務 [傳統]**。 做為 toodeploy*新的機器學習 Web 服務*，按一下**部署 Web 服務**選取**部署 Web 服務 [New]**。 使用者現在可以傳送資料 tooyour 模型使用 hello Web 服務 REST API，並收到 hello 後的結果。 如需詳細資訊，請參閱[如何 tooconsume Azure 機器學習 Web 服務](machine-learning-consume-web-services.md)。

## <a name="hello-non-typical-case-creating-a-non-predictive-web-service"></a>hello 非一般的情況下： 建立非預測的 Web 服務
如果您的經驗不訓練預測分析模型中，則您不需要 toocreate 定型實驗和計分實驗-有一個實驗，並將它部署為 Web 服務。 Machine Learning Studio 偵測到您的經驗是否包含藉由分析 hello 模組所使用的預測模型。

逐一查看實驗並滿足於該實驗之後：

1. 按一下 [設定 Web 服務]，並選取 [重新訓練 Web] - 自動會新增輸入和輸出節點
2. 按一下 [執行] 
3. 按一下**部署 Web 服務**選取**部署 Web 服務 [傳統]**或**部署 Web 服務 [New]**想根據 hello 環境 toowhich toodeploy。

現在已部署您的 Web 服務，而且您可以如同預測性 Web 服務一般存取及管理它。

## <a name="updating-your-web-service"></a>更新您的 Web 服務
既然您已部署為 Web 服務實驗，如果您需要 tooupdate 它嗎？

會視您的需要 tooupdate:

**您想 toochange hello 輸入或輸出，或者您想 toomodify hello Web 服務如何管理資料**

如果您不變更 hello 模型，但只變更 hello Web 服務處理資料的方式，您可以編輯 hello 預測實驗，然後按一下**部署 Web 服務**選取**部署 Web 服務 [傳統]**或**部署 Web 服務 [New]**一次。 hello Web 服務已停止、 hello 更新預測實驗部署，以及在 hello Web 服務重新啟動。

以下是範例： 假設您預測實驗傳回 hello 整個資料列的輸入資料以 hello 預測結果。 您可以決定您想 hello Web 服務 toojust hello 傳回結果。 讓您新增**投射資料行**hello 預測實驗模組，右 hello 輸出連接埠之前, tooexclude hello 以外的資料行產生。 當您按一下**部署 Web 服務**選取**部署 Web 服務 [傳統]**或**部署 Web 服務 [New]** hello Web 服務，會更新。

**您想要使用新的資料 tooretrain hello 模型**

如果您想 tookeep 您的機器學習模型，但您要 tooretrain 它與新的資料，您有兩個選擇：

1. **Hello Web 服務正在執行時重新定型模型 hello** -如果您想 tooretrain 模型 hello 預測 Web 服務執行時，您可以藉由一些修改 toohello 定型實驗 toomake 它***定型實驗***，則您可以將其部署為***訓練 web*服務**。 如需有關指示 toodo，請參閱[重新訓練機器學習模型以程式設計方式](machine-learning-retrain-models-programmatically.md)。
2. **請返回 toohello 原始定型實驗，並使用不同的訓練資料 toodevelop 模型**-預測實驗是連結的 toohello Web 服務，但這種方式中未直接連結 hello 定型實驗。 如果您修改 hello 原始定型實驗，並按一下**設定 Web 服務**，它會建立*新*預測進行實驗，部署時，將會建立*新*Web服務。 它不只會更新 hello 原始 Web 服務。
   
   如果您需要 toomodify hello 定型實驗，請開啟它，然後按一下**存**toomake 複本。 這會導致原始定型實驗保持不變的 hello、 預測的實驗和 Web 服務。 您現在可以利用您的變更建立新的 Web 服務。 一旦您已部署的 hello 新的 Web 服務然後您可以決定是否 toostop hello 先前的 Web 服務或讓它與 hello 新一起執行。

**您想要 tootrain 不同的模型**

如果您想要 toomake 變更 tooyour 原始預測實驗中，選取不同的機器學習演算法，例如嘗試不同的訓練方法，以此類推，則需要 toofollow hello 第二個上述程序重新訓練您的模型：開啟 hello 定型實驗中，按一下**存**toomake 複本，並再啟動開發您的模型、 建立 hello 預測實驗中，與部署的 hello 新路徑 hello web 服務。 這會建立新的 Web 服務不相關的 toohello 原始-您可以決定執行的其中一個，或兩者，tookeep。

## <a name="next-steps"></a>後續步驟
如需有關開發和實驗 hello 程序的詳細資訊，請參閱下列文章 hello:

* 轉換 hello 實驗-[如何 tooprepare Azure Machine Learning Studio 中的部署模型](machine-learning-convert-training-experiment-to-scoring-experiment.md)
* 部署 hello Web 服務-[部署 Azure Machine Learning web 服務](machine-learning-publish-a-machine-learning-web-service.md)
* 訓練 hello 模型-[重新訓練機器學習模型以程式設計的方式](machine-learning-retrain-models-programmatically.md)

如需 hello 整個程序的範例，請參閱：

* [機器學習教學課程：在 Azure Machine Learning Studio 中建立您的第一個實驗](machine-learning-create-experiment.md)
* [逐步解說：在 Azure Machine Learning 中為信用風險評估開發預測性分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)

