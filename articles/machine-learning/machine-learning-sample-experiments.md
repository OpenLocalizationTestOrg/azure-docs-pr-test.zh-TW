---
title: "複製機器學習服務範例實驗 - Azure | Microsoft Docs"
description: "了解如何透過 Cortana 智慧資源庫和 Microsoft Azure Machine Learning 使用範例機器學習服務實驗來建立新的實驗。"
keywords: "機器學習服務範例, 範例實驗, 機器學習服務範例"
services: machine-learning
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: 81e6c1d8-682c-4db3-bfd5-d7bfb1150ff3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: cgronlun
ms.openlocfilehash: 55f9bd2ed0d555a14d31bf3d262707d65bd70244
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="copy-example-experiments-to-create-new-machine-learning-experiments"></a>複製範例實驗來建立新的機器學習服務實驗
了解如何從 [Cortana 智慧資源庫](https://gallery.cortanaintelligence.com/) 的範例實驗開始，而不是從頭建立機器學習服務實驗。 您可以使用範例來建立自己的機器學習服務解決方案。

資源庫有 Microsoft Azure Machine Learning 小組的範例實驗，以及由 Machine Learning 社群共用的範例。 您也可以提出有關實驗的問題或張貼意見。

若要查看如何使用資源庫，請觀看[初學者的資料科學](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md)系列中的 3 分鐘影片[複製其他人的工作來進行資料科學](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md)。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="find-an-experiment-to-copy-in-cortana-intelligence-gallery"></a>在 Cortana 智慧資源庫中尋找要複製的實驗
若要查看有哪些可用的實驗，請移至[資源庫](https://gallery.cortanaintelligence.com/)，然後按一下頁面頂端的 [實驗]。

### <a name="find-the-newest-or-most-popular-experiments"></a>尋找最新或最受歡迎的實驗
在此頁面上，您可以查看 [最近新增] 實驗，或往下捲動查看 [熱門項目] 或最新的 [熱門的 Microsoft 實驗]。

### <a name="look-for-an-experiment-that-meets-specific-requirements"></a>尋找符合特定需求的實驗
若要瀏覽所有實驗︰

1. 按一下頁面頂端的 [全部瀏覽]  。
2. 在左側 [類別] 區段的 [精簡依據] 之下，選取 [實驗] 以查看資源庫中的所有實驗。
3. 有幾種不同方式可以找到符合您需求的實驗︰
   * **選取左邊的篩選。** 例如，若要瀏覽使用以 PCA 為基礎之異常偵測演算法的實驗，請選取 [類別] 之下的 [實驗]，然後按一下 [全部顯示]。 然後，在 [使用的演算法] 之下，選擇 [以 PCA 為基礎的異常偵測]。 <br></br>
     ![選取篩選器](./media/machine-learning-sample-experiments/refine-the-view.png)
   * **使用 [搜尋] 方塊。** 例如，若要尋找 Microsoft 所提出並使用二級支援向量機器演算法的數字辨識相關實驗，請在 [搜尋] 方塊中輸入「數字辨識」。 然後選取篩選器 [實驗]、[僅包含 Microsoft 內容] 和 [二級支援向量機器]：<br></br>
     ![使用搜尋方塊](./media/machine-learning-sample-experiments/search-for-experiments.png)
4. 按一下實驗，以深入了解相關資訊。
5. 若要執行和 (或) 修改實驗，請按一下實驗頁面上的 [在 Studio 中開啟]  。 <br></br>

    ![範例實驗](./media/machine-learning-sample-experiments/example-experiment.png)

    > [!NOTE]
    > 當您在 Machine Learning Studio 中第一次開啟實驗時，您可以免費試用或購買 Azure 訂用帳戶。 [了解 Machine Learning Studio 免費試用版與付費服務](https://azure.microsoft.com/pricing/details/machine-learning/)
    >
    >

## <a name="create-a-new-experiment-using-an-example-as-a-template"></a>使用範例作為範本來建立新實驗
您也可以使用資源庫範例作為範本，在 Machine Learning Studio 中建立新實驗。

1. 用您的 Microsoft 帳戶認證登入 [Studio](https://studio.azureml.net)，然後按一下 [新增] 以建立實驗。
2. 瀏覽範例內容，然後按一下其中一個。

隨即以範例實驗作為範本，在您的 Machine Learning Studio 工作區中建立新的實驗。

## <a name="next-steps"></a>後續步驟
* [從各種資源匯入資料](machine-learning-data-science-import-data.md)
* [Machine Learning 中的 R 語言所適用的快速入門教學課程](machine-learning-r-quickstart.md)
* [部署 Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)
