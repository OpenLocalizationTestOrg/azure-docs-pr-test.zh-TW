---
title: "步驟 2：將資料上傳至 Machine Learning 實驗中 | Microsoft Docs"
description: "步驟 2 中的 hello 開發預測方案逐步解說： 上傳到 Azure Machine Learning Studio 中儲存公用資料。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 0ea21dcca2d0934ed06508560cf85cf31b48ce6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a>逐步解說步驟 2：將現有資料上傳至 Azure Machine Learning 實驗中
這是 hello hello 逐步解說中，第二個步驟[開發 Azure Machine Learning 中的預測分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)

1. [建立機器學習服務工作區](machine-learning-walkthrough-1-create-ml-workspace.md)
2. **上傳現有資料**
3. [建立新實驗](machine-learning-walkthrough-3-create-new-experiment.md)
4. [來定型及評估 hello 模型](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [部署 hello Web 服務](machine-learning-walkthrough-5-publish-web-service.md)
6. [存取 hello Web 服務](machine-learning-walkthrough-6-access-web-service.md)

- - -
toodevelop 信用風險的預測模型，我們需要的資料，我們可以使用 tootrain 並接著測試 hello 模型。 本逐步解說，我們將從 hello UC Irvine 機器學習儲存機制使用 hello 「 UCI Statlog （德文信用卡資料） 的資料集 」。 您可以在下列位置找到此儲存機制：  
<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a>

我們會使用名為 「 hello 檔案**german.data**。 下載這個檔案 tooyour 本機硬碟。  

hello **german.data**資料集包含資料列的 20 變數的信用額度 1000年過去的履歷表。 這些 20 變數代表 hello 資料集的功能 (hello*特徵向量*)，可提供每個剩餘的信用應徵者的識別特性。 每個資料列中的其他資料行代表 hello 申請者的導出的信用風險，700 低信用風險和 300 視為高風險的履歷表。

hello UCI 網站提供的這項資料的 hello 特徵向量 hello 屬性的描述。 包括財務資訊、信用歷史記錄、工作狀態、個人資訊。 每個申請者都會有一個二進位評等，指出他們屬於低信用風險還是高風險。 

我們將使用此資料 tootrain 預測分析模型。 當我們完成時，我們的模型中要能 tooaccept 特徵向量的新的人員，而且預測他或她是低或高信用風險。  

以下提供一個有趣的論點。 hello hello hello UCI 網站提及上的資料集的描述項目成本如果我們 misclassify 人員的信用風險。
如果 hello 模型預測高信用風險的實際低信用風險的人，hello 模型所做的錯誤分類。
但 hello 反向錯誤分類成本五次更高的 toohello 金融機構： 如果 hello 模型預測的人真的高信用風險低信用風險。

因此，我們想要 tootrain 我們的模型如此 hello 這個第二個類型的錯誤分類成本高於五次 hello 另一種方式將錯誤分類。
一個簡單的方式 toodo 這在我們的實驗中的 hello 模型定型時複製 （五次） 的項目代表具有高信用風險。 然後，如果 hello 模型利用人為低信用風險它們實際上是較高的風險時，hello 模型會該相同的錯誤分類五次，一次為每個重複項目。 這將會增加 hello 成本 hello 訓練結果中的這個錯誤。


## <a name="convert-hello-dataset-format"></a>轉換 hello 資料集格式
hello 原始資料集使用空白分隔的格式。 Machine Learning Studio 較適用於以逗號分隔值 (CSV) 檔案，所以我們會使用逗號來取代空格轉換 hello 資料集。  

有許多方式 tooconvert 這項資料。 其中一種方式是使用下列 Windows PowerShell 命令的 hello:   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

另一種方式是使用 hello Unix sed 命令：  

    sed 's/ /,/g' german.data > german.csv  

在任一情況下，我們建立了名為的檔案中的 hello 資料的逗號分隔版本**german.csv**我們可以在我們的實驗中使用。

## <a name="upload-hello-dataset-toomachine-learning-studio"></a>上傳 hello 資料集 tooMachine Learning Studio
一旦 hello 資料已轉換的 tooCSV 格式，我們需要 tooupload 到 Machine Learning Studio。 

1. 開啟 hello Machine Learning Studio 首頁 ([https://studio.azureml.net](https://studio.azureml.net))。 

2. 按一下 [hello] 功能表![功能表][1]在 hello hello 視窗的左上角，按一下**Azure Machine Learning**，選取**Studio**，並登入。

3. 按一下**+ 新增**在 hello hello 視窗的底部。

4. 選取 [ **資料集**]。

5. 選取 [ **從本機檔案**]。

    ![從本機檔案新增資料集][2]

6. 在 hello**上傳新的資料集**] 對話方塊中，按一下 [**瀏覽**並尋找 hello **german.csv**您建立的檔案。

7. 輸入 hello 資料集的名稱。 在此逐步解說中，將它稱為 "UCI German Credit Card Data"。

8. 針對資料類型，請選取 **不具標頭的一般 CSV 檔案 (.nh.csv)**。

9. 視需要新增說明。

10. 按一下 hello**確定**核取記號。  

    ![上傳 hello 資料集][3]

這將 hello 資料上傳至我們可以在實驗中使用的資料集模組。

您可以管理資料集，您已按一下 hello 上載 tooStudio**資料集** 索引標籤 toohello 方 hello Studio 視窗。

![管理資料集][4]

如需將其他種資料類型匯入實驗的詳細資訊，請參閱[將訓練資料匯入 Azure Machine Learning Studio](machine-learning-data-science-import-data.md)。

**下一步：[建立新實驗](machine-learning-walkthrough-3-create-new-experiment.md)**

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
