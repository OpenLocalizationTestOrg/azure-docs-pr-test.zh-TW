---
title: "aaaA 預測使用機器學習的信用風險解決方案 |Microsoft 文件"
description: "詳細的逐步解說，示範如何 toocreate 信用額度的預測分析解決方案將風險評定 Azure Machine Learning Studio 中。"
keywords: "信用風險, 預測性分析解決方案, 風險評估"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 43300854-a14e-4cd2-9bb1-c55c779e0e93
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 00ed39081e6952b8d03b37a8285d8dc3ddff2cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a>逐步解說：在 Azure Machine Learning 中為信用風險評估開發預測分析解決方案

在本逐步解說中，我們查看擴充開發預測分析解決方案 Machine Learning Studio 中的 hello 程序。 我們開發在機器學習 Studio 中，簡單的模型，然後將其部署為其中 hello 模型可以使用資料做出預測新的 Azure Machine Learning web 服務。 

本逐步解說會假設您之前已至少使用過一次 Machine Learning Studio，而且對機器學習服務概念有一些了解。 但不會假設您對上述任一方面有所專精。

如果您從未使用過**Azure Machine Learning Studio**您可能會想 toostart hello 教學課程中，使用之前，[建立 Azure Machine Learning Studio 中的第一次的資料科學實驗](machine-learning-create-experiment.md)。 該教學課程引導您完成 Machine Learning Studio hello 第一次。 它會顯示 hello 基本概念的方式 toodrag 放模組至您的經驗，連接在一起，請執行 hello 實驗，並查看 hello 結果。 可能會很有幫助使用者入門的另一個工具是 hello Machine Learning Studio 功能的概觀的圖表。 您可以從這裡下載並列印它：[Azure Machine Learning Studio 功能的概觀圖](machine-learning-studio-overview-diagram.md)。
 
如果您是新 toohello 欄位的機器學習的一般情況下，沒有可能會很有幫助 tooyou 影片系列。 它會呼叫[為初學者所設計的資料科學](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md)和它可以提供絕佳的簡介 toomachine 學習使用日常用語和概念。


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="hello-problem"></a>hello 問題

假設您需要的 toopredict hello 剩餘的信用應用程式所提供的資訊為基礎的個人的信用風險。  

信用風險評估是一個複雜的問題，但是我們可以針對這個逐步解說將它稍微簡化。 我們將使用它作為一個範例，以說明您如何使用 Microsoft Azure Machine Learning 來建立預測性分析解決方案。 toodo，我們使用 Azure Machine Learning Studio 和機器學習 web 服務。  

## <a name="hello-solution"></a>hello 方案

在這個詳細的逐步解說中，我們將從可公開取得的信用風險資料開始著手，然後根據該資料來開發並訓練預測性模型。 然後我們 hello 將模型部署為 web 服務，才能使用其他人所評估信用風險。

toocreate 這個信用風險評定解決方案中，我們遵循下列步驟：  

1. [建立機器學習服務工作區](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [上傳現有資料](machine-learning-walkthrough-2-upload-data.md)
3. [建立實驗](machine-learning-walkthrough-3-create-new-experiment.md)
4. [來定型及評估 hello 模型](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [部署 hello web 服務](machine-learning-walkthrough-5-publish-web-service.md)
6. [存取 hello web 服務](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> 您可以在本逐步解說中 hello 找到我們所開發的 hello 實驗的工作副本[Cortana 智慧組件庫](https://gallery.cortanaintelligence.com)。 跳過**[逐步解說-信用風險預測](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**按一下**在 Studio 中開啟**toodownload hello 實驗到 Machine Learning Studio 工作區的複本。
> 
> 本逐步解說根據 hello 範例實驗的簡化版本[二元分類： 信用風險預測](http://go.microsoft.com/fwlink/?LinkID=525270)，也可用於 hello[圖庫](http://gallery.cortanaintelligence.com/)。
