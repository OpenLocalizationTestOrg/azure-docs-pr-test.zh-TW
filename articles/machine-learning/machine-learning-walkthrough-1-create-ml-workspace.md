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
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a><span data-ttu-id="4fb02-103">逐步解說步驟 1：建立 Machine Learning 工作區</span><span class="sxs-lookup"><span data-stu-id="4fb02-103">Walkthrough Step 1: Create a Machine Learning workspace</span></span>
<span data-ttu-id="4fb02-104">這是 hello hello 逐步解說中，第一個步驟[開發 Azure Machine Learning 中的預測分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)。</span><span class="sxs-lookup"><span data-stu-id="4fb02-104">This is hello first step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

1. <span data-ttu-id="4fb02-105">**建立機器學習服務工作區**</span><span class="sxs-lookup"><span data-stu-id="4fb02-105">**Create a Machine Learning workspace**</span></span>
2. [<span data-ttu-id="4fb02-106">上傳現有資料</span><span class="sxs-lookup"><span data-stu-id="4fb02-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="4fb02-107">建立新實驗</span><span class="sxs-lookup"><span data-stu-id="4fb02-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="4fb02-108">來定型及評估 hello 模型</span><span class="sxs-lookup"><span data-stu-id="4fb02-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="4fb02-109">部署 hello Web 服務</span><span class="sxs-lookup"><span data-stu-id="4fb02-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="4fb02-110">存取 hello Web 服務</span><span class="sxs-lookup"><span data-stu-id="4fb02-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs toobe updated toorefer toohello new way of creating workspaces in hello Ibiza portal -->

<span data-ttu-id="4fb02-111">toouse Machine Learning Studio 中，您需要 toohave Microsoft Azure Machine Learning 工作區。</span><span class="sxs-lookup"><span data-stu-id="4fb02-111">toouse Machine Learning Studio, you need toohave a Microsoft Azure Machine Learning workspace.</span></span> <span data-ttu-id="4fb02-112">此工作區包含所需 toocreate hello 工具、 管理及發佈實驗。</span><span class="sxs-lookup"><span data-stu-id="4fb02-112">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>  

<!--
## toocreate a workspace
1. Sign in toohello [Azure classic portal](https://manage.windowsazure.com).
2. In hello  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On hello **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

<span data-ttu-id="4fb02-113">hello Azure 訂用帳戶的系統管理員需要 toocreate hello 工作區，然後將您加入成為擁有者或參與者。</span><span class="sxs-lookup"><span data-stu-id="4fb02-113">hello administrator for your Azure subscription needs toocreate hello workspace and then add you as an owner or contributor.</span></span> <span data-ttu-id="4fb02-114">如需詳細資訊，請參閱[建立 Azure Machine Learning 工作區](machine-learning-create-workspace.md)。</span><span class="sxs-lookup"><span data-stu-id="4fb02-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="4fb02-115">建立您的工作區之後，開啟 Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home))。</span><span class="sxs-lookup"><span data-stu-id="4fb02-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span></span> <span data-ttu-id="4fb02-116">如果您有多個工作區，您可以在 hello hello 視窗右上角的 hello 工具列中選取 hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="4fb02-116">If you have more than one workspace, you can select hello workspace in hello toolbar in hello upper-right corner of hello window.</span></span>

![在 Studio 中選取工作區][2]

> [!TIP]
> <span data-ttu-id="4fb02-118">如果您所做的 hello 工作區的擁有者可以共用您的邀請其他人正在使用的 hello 實驗 toohello 工作區。</span><span class="sxs-lookup"><span data-stu-id="4fb02-118">If you were made an owner of hello workspace, you can share hello experiments you're working on by inviting others toohello workspace.</span></span> <span data-ttu-id="4fb02-119">您可以在 Machine Learning Studio 中的 hello**設定**頁面。</span><span class="sxs-lookup"><span data-stu-id="4fb02-119">You can do this in Machine Learning Studio on hello **SETTINGS** page.</span></span> <span data-ttu-id="4fb02-120">您為每個使用者只需要 hello Microsoft 帳戶或組織帳戶。</span><span class="sxs-lookup"><span data-stu-id="4fb02-120">You just need hello Microsoft account or organizational account for each user.</span></span>
> 
> <span data-ttu-id="4fb02-121">在 hello**設定**頁面上，按一下**使用者**，然後按一下 **更邀請使用者**在 hello hello 視窗的底部。</span><span class="sxs-lookup"><span data-stu-id="4fb02-121">On hello **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at hello bottom of hello window.</span></span>
> 
> 

- - -
<span data-ttu-id="4fb02-122">**下一步：[上傳現有資料](machine-learning-walkthrough-2-upload-data.md)**</span><span class="sxs-lookup"><span data-stu-id="4fb02-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span></span>

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
