---
title: "步驟 1︰建立 Machine Learning 工作區 | Microsoft Docs"
description: "步驟 1 中的 hello 開發預測方案逐步解說： 了解如何註冊新的 Azure Machine Learning Studio 工作區 tooset。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b3c97e3d-16ba-4e42-9657-2562854a1e04
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 93d2e240826db9768e85b00cab0eb62510b4efb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a>逐步解說步驟 1：建立 Machine Learning 工作區
這是 hello hello 逐步解說中，第一個步驟[開發 Azure Machine Learning 中的預測分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)。

1. **建立機器學習服務工作區**
2. [上傳現有資料](machine-learning-walkthrough-2-upload-data.md)
3. [建立新實驗](machine-learning-walkthrough-3-create-new-experiment.md)
4. [來定型及評估 hello 模型](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [部署 hello Web 服務](machine-learning-walkthrough-5-publish-web-service.md)
6. [存取 hello Web 服務](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs toobe updated toorefer toohello new way of creating workspaces in hello Ibiza portal -->

toouse Machine Learning Studio 中，您需要 toohave Microsoft Azure Machine Learning 工作區。 此工作區包含所需 toocreate hello 工具、 管理及發佈實驗。  

<!--
## toocreate a workspace
1. Sign in toohello [Azure classic portal](https://manage.windowsazure.com).
2. In hello  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On hello **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

hello Azure 訂用帳戶的系統管理員需要 toocreate hello 工作區，然後將您加入成為擁有者或參與者。 如需詳細資訊，請參閱[建立 Azure Machine Learning 工作區](machine-learning-create-workspace.md)。

建立您的工作區之後，開啟 Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home))。 如果您有多個工作區，您可以在 hello hello 視窗右上角的 hello 工具列中選取 hello 工作區。

![在 Studio 中選取工作區][2]

> [!TIP]
> 如果您所做的 hello 工作區的擁有者可以共用您的邀請其他人正在使用的 hello 實驗 toohello 工作區。 您可以在 Machine Learning Studio 中的 hello**設定**頁面。 您為每個使用者只需要 hello Microsoft 帳戶或組織帳戶。
> 
> 在 hello**設定**頁面上，按一下**使用者**，然後按一下 **更邀請使用者**在 hello hello 視窗的底部。
> 
> 

- - -
**下一步：[上傳現有資料](machine-learning-walkthrough-2-upload-data.md)**

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
