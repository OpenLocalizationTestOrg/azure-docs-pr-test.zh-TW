---
title: "Azure Machine Learning 自動化資料管線小密技 | Microsoft Docs"
description: "可列印的小祕技，可向您示範如何對您的 Azure Machine Learning Web 服務設定自動資料管線，無論您的資料是在內部部署、串流、Azure 中或協力廠商雲端服務中。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 22674d6b-4491-4805-a3ac-d423611177bb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: mithal;garye
ms.openlocfilehash: e212b2c935eb0ae64ed1cd2e6dc1564f8fcd503b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="cheat-sheet-for-an-automated-data-pipeline-for-azure-machine-learning-predictions"></a><span data-ttu-id="0cbec-103">適用於 Azure Machine Learning 預測之自動資料管線的小祕技</span><span class="sxs-lookup"><span data-stu-id="0cbec-103">Cheat sheet for an automated data pipeline for Azure Machine Learning predictions</span></span>
<span data-ttu-id="0cbec-104">「Microsoft Azure Machine Learning 自動資料管線小祕技」  可協助您瀏覽用於傳送資料至可由預測性分析模型評分之機器學習 Web 服務的技術。</span><span class="sxs-lookup"><span data-stu-id="0cbec-104">The **Microsoft Azure Machine Learning automated data pipeline cheat sheet** helps you navigate through the technology you can use to get your data to your Machine Learning web service where it can be scored by your predictive analytics model.</span></span>

<span data-ttu-id="0cbec-105">視您的資料是在內部部署、在雲端或以即時串流方式處理，會有不同機制用來將資料傳送至 Web 服務端點進行評分。</span><span class="sxs-lookup"><span data-stu-id="0cbec-105">Depending on whether your data is on-premises, in the cloud, or streaming real-time, there are different mechanisms available to move the data to your web service endpoint for scoring.</span></span>
<span data-ttu-id="0cbec-106">這份小祕技會逐步引導您做出各項決定，並提供可協助您開發方案之文章的連結。</span><span class="sxs-lookup"><span data-stu-id="0cbec-106">This cheat sheet walks you through the decisions you need to make, and it offers links to articles that can help you develop your solution.</span></span>

## <a name="download-the-machine-learning-automated-data-pipeline-cheat-sheet"></a><span data-ttu-id="0cbec-107">下載「Microsoft Azure Machine Learning 自動資料管線小祕技」</span><span class="sxs-lookup"><span data-stu-id="0cbec-107">Download the Machine Learning automated data pipeline cheat sheet</span></span>
<span data-ttu-id="0cbec-108">下載此這份小祕技之後，您可以將它列印成 Tabloid 大小 (11 x 17 英吋)。</span><span class="sxs-lookup"><span data-stu-id="0cbec-108">Once you download the cheat sheet, you can print it in tabloid size (11 x 17 in.).</span></span>

<span data-ttu-id="0cbec-109">在此下載小祕技： **[Microsoft Azure Machine Learning 自動資料管線小祕技](http://download.microsoft.com/download/C/C/7/CC726F8B-2E6F-4C20-9B6F-AFBEE8253023/microsoft-machine-learning-operationalization-cheat-sheet_v1.pdf)**</span><span class="sxs-lookup"><span data-stu-id="0cbec-109">Download the cheat sheet here: **[Microsoft Azure Machine Learning automated data pipeline cheat sheet](http://download.microsoft.com/download/C/C/7/CC726F8B-2E6F-4C20-9B6F-AFBEE8253023/microsoft-machine-learning-operationalization-cheat-sheet_v1.pdf)**</span></span>

![Microsoft Azure Machine Learning Studio 功能概觀][op-cheat-sheet]

[op-cheat-sheet]: ./media/machine-learning-automated-data-pipeline-cheat-sheet/machine-learning-automated-data-pipeline-cheat-sheet_v1.1.png


## <a name="more-help-with-machine-learning-studio"></a><span data-ttu-id="0cbec-111">Machine Learning Studio 的更多說明</span><span class="sxs-lookup"><span data-stu-id="0cbec-111">More help with Machine Learning Studio</span></span>
* <span data-ttu-id="0cbec-112">如需 Microsoft Azure Machine Learning 的概觀，請參閱 [Microsoft Azure 上的機器學習簡介](machine-learning-what-is-machine-learning.md)。</span><span class="sxs-lookup"><span data-stu-id="0cbec-112">For an overview of Microsoft Azure Machine Learning, see [Introduction to machine learning on Microsoft Azure](machine-learning-what-is-machine-learning.md).</span></span>
* <span data-ttu-id="0cbec-113">如需如何部署評分 Web 服務的說明，請參閱 [部署 Azure Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="0cbec-113">For an explanation of how to deploy a scoring web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="0cbec-114">如需如何使用評分 Web 服務的討論，請參閱[如何使用 Azure Machine Learning Web 服務](machine-learning-consume-web-services.md)。</span><span class="sxs-lookup"><span data-stu-id="0cbec-114">For a discussion of how to consume a scoring web service, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

