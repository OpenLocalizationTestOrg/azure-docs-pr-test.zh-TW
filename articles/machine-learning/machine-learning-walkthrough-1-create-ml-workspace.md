---
title: "步驟 1︰建立 Machine Learning 工作區 | Microsoft Docs"
description: "開發預測解決方案逐步解說的步驟 1：了解如何設定新的 Azure Machine Learning Studio 工作區。"
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
ms.openlocfilehash: 8ca42ef8f5314866301f5c9e93caa90dc837a66e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a><span data-ttu-id="e622e-103">逐步解說步驟 1：建立 Machine Learning 工作區</span><span class="sxs-lookup"><span data-stu-id="e622e-103">Walkthrough Step 1: Create a Machine Learning workspace</span></span>
<span data-ttu-id="e622e-104">這是 [在 Azure Machine Learning 中為信用風險評估開發預測性分析解決方案](machine-learning-walkthrough-develop-predictive-solution.md)逐步解說的第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="e622e-104">This is the first step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

1. <span data-ttu-id="e622e-105">**建立機器學習服務工作區**</span><span class="sxs-lookup"><span data-stu-id="e622e-105">**Create a Machine Learning workspace**</span></span>
2. [<span data-ttu-id="e622e-106">上傳現有資料</span><span class="sxs-lookup"><span data-stu-id="e622e-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="e622e-107">建立新實驗</span><span class="sxs-lookup"><span data-stu-id="e622e-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="e622e-108">訓練及評估模型</span><span class="sxs-lookup"><span data-stu-id="e622e-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="e622e-109">部署 Web 服務</span><span class="sxs-lookup"><span data-stu-id="e622e-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="e622e-110">存取 Web 服務</span><span class="sxs-lookup"><span data-stu-id="e622e-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs to be updated to refer to the new way of creating workspaces in the Ibiza portal -->

<span data-ttu-id="e622e-111">若要使用 Machine Learning Studio，您需要有 Microsoft Azure Machine Learning 工作區。</span><span class="sxs-lookup"><span data-stu-id="e622e-111">To use Machine Learning Studio, you need to have a Microsoft Azure Machine Learning workspace.</span></span> <span data-ttu-id="e622e-112">此工作區包含您建立、管理及發行實驗所需的工具。</span><span class="sxs-lookup"><span data-stu-id="e622e-112">This workspace contains the tools you need to create, manage, and publish experiments.</span></span>  

<!--
## To create a workspace
1. Sign in to the [Azure classic portal](https://manage.windowsazure.com).
2. In the  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On the **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

<span data-ttu-id="e622e-113">Azure 訂用帳戶的系統管理員必須建立工作區，然後將您新增為擁有者或參與者。</span><span class="sxs-lookup"><span data-stu-id="e622e-113">The administrator for your Azure subscription needs to create the workspace and then add you as an owner or contributor.</span></span> <span data-ttu-id="e622e-114">如需詳細資訊，請參閱[建立 Azure Machine Learning 工作區](machine-learning-create-workspace.md)。</span><span class="sxs-lookup"><span data-stu-id="e622e-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="e622e-115">建立您的工作區之後，開啟 Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home))。</span><span class="sxs-lookup"><span data-stu-id="e622e-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span></span> <span data-ttu-id="e622e-116">如果您具有多個工作區，您可以在視窗右上角的工具列中選取工作區。</span><span class="sxs-lookup"><span data-stu-id="e622e-116">If you have more than one workspace, you can select the workspace in the toolbar in the upper-right corner of the window.</span></span>

![在 Studio 中選取工作區][2]

> [!TIP]
> <span data-ttu-id="e622e-118">如果您是工作區的擁有者，您可以邀請他人到您的工作區，共用您正在執行的實驗。</span><span class="sxs-lookup"><span data-stu-id="e622e-118">If you were made an owner of the workspace, you can share the experiments you're working on by inviting others to the workspace.</span></span> <span data-ttu-id="e622e-119">您可以在 Machine Learning Studio 中的 [ **設定** ] 頁面上執行此動作。</span><span class="sxs-lookup"><span data-stu-id="e622e-119">You can do this in Machine Learning Studio on the **SETTINGS** page.</span></span> <span data-ttu-id="e622e-120">您只需要每個使用者的 Microsoft 帳戶或組織帳戶。</span><span class="sxs-lookup"><span data-stu-id="e622e-120">You just need the Microsoft account or organizational account for each user.</span></span>
> 
> <span data-ttu-id="e622e-121">在 [設定] 頁面上，按一下 [使用者]，然後按一下視窗底部的 [邀請使用者]。</span><span class="sxs-lookup"><span data-stu-id="e622e-121">On the **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at the bottom of the window.</span></span>
> 
> 

- - -
<span data-ttu-id="e622e-122">**下一步：[上傳現有資料](machine-learning-walkthrough-2-upload-data.md)**</span><span class="sxs-lookup"><span data-stu-id="e622e-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span></span>

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
