---
title: "步驟 6： 存取 hello 機器學習 Web 服務 |Microsoft 文件"
description: "步驟 6 的 hello 開發預測方案逐步解說： 存取作用中的 Azure 機器學習 Web 服務。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a65c89a-40ab-4673-8dd8-8eee0a150e3b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 211de0294092c6a6b5e6eb608d5d3b88107674c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-6-access-hello-azure-machine-learning-web-service"></a>逐步解說步驟 6： 存取 hello Azure Machine Learning web 服務

這是 hello hello 逐步解說中，最後一個步驟[開發 Azure Machine Learning 中的預測分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)

1. [建立機器學習服務工作區](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [上傳現有資料](machine-learning-walkthrough-2-upload-data.md)
3. [建立新實驗](machine-learning-walkthrough-3-create-new-experiment.md)
4. [來定型及評估 hello 模型](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [部署 hello Web 服務](machine-learning-walkthrough-5-publish-web-service.md)
6. **存取 hello Web 服務**

- - -
在此逐步解說中的 hello 上一個步驟中部署的 web 服務，會使用我們的信用風險預測模型。 現在使用者可以 toosend 資料 tooit，並接收結果。 

hello Web 服務是一種 Azure web 服務，可接收並傳回在兩種方式之一使用 REST Api 的資料：  

* **要求/回應**-hello 使用者傳送一個或多個資料列的信用卡資料 toohello 服務透過 HTTP 通訊協定和 hello 服務回應一或多個結果集。
* **批次執行**-hello 使用者存放了一個或多個資料列，在 Azure 中的信用卡資料的 blob，然後將傳送 hello blob 位置 toohello 服務。 所有 hello 中的資料列的 hello 服務分數 hello 輸入的 blob、 存放區 hello 導致另一個 blob，並傳回 hello 該容器的 URL。  

hello 最快速且輕鬆的方式 tooaccess 傳統 web 服務是透過 hello [Azure ML 要求-回應服務 Web 應用程式](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)或[Azure ML 批次執行服務 Web 應用程式範本](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)。

這些 Web 應用程式範本可以建立自訂的 Web 應用程式，該應用程式知道您的 Web 服務輸入資料和將傳回的內容。 您只需要 toodo 提供存取 tooyour web 服務和資料，但 hello 範本沒有 hello rest。

如需有關使用 hello web 應用程式範本的詳細資訊，請參閱[取用的 Azure 機器學習 Web 服務與 web 應用程式範本](machine-learning-consume-web-service-with-web-app-template.md)。

您也可以開發自訂應用程式 tooaccess hello web 服務使用 R、 C# 和 Python 程式設計語言中，為您提供的起始程式碼。

您可以找到完整的詳細資料中[如何 tooconsume Azure 機器學習 Web 服務](machine-learning-consume-web-services.md)。

