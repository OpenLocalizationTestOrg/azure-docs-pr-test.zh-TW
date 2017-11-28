---
title: "建立 Machine Learning 工作區 | Microsoft Docs"
description: "如何建立 Azure Machine Learning Studio 的工作區"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 182a34822e71d63f4d7229548ae3f59d9f195337
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a><span data-ttu-id="31673-103">建立和共用 Azure Machine Learning 工作區</span><span class="sxs-lookup"><span data-stu-id="31673-103">Create and share an Azure Machine Learning workspace</span></span>
<span data-ttu-id="31673-104">此功能表會連結至說明如何設定 Cortana Analytics 程序 (CAP) 所用的各種資料科學環境主題。</span><span class="sxs-lookup"><span data-stu-id="31673-104">This menu links to topics that describe how to set up the various data science environments used by the Cortana Analytics Process (CAPS).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="31673-105">若要使用 Azure Machine Learning Studio，您需要有機器學習服務工作區。</span><span class="sxs-lookup"><span data-stu-id="31673-105">To use Azure Machine Learning Studio, you need to have a Machine Learning workspace.</span></span> <span data-ttu-id="31673-106">此工作區包含您建立、管理及發行實驗所需的工具。</span><span class="sxs-lookup"><span data-stu-id="31673-106">This workspace contains the tools you need to create, manage, and publish experiments.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="to-create-a-workspace"></a><span data-ttu-id="31673-107">建立工作區</span><span class="sxs-lookup"><span data-stu-id="31673-107">To create a workspace</span></span>
1. <span data-ttu-id="31673-108">登入 [Azure 入口網站](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="31673-108">Sign in to the [Azure portal](https://portal.azure.com/)</span></span>

    > [!NOTE]
    > <span data-ttu-id="31673-109">若要登入並建立工作區，您必須是 Azure 訂用帳戶管理員。</span><span class="sxs-lookup"><span data-stu-id="31673-109">To sign in and create a workspace, you need to be an Azure subscription administrator.</span></span> 
    >
    > 

2. <span data-ttu-id="31673-110">按一下 [+ 新增]</span><span class="sxs-lookup"><span data-stu-id="31673-110">Click **+New**</span></span>

3. <span data-ttu-id="31673-111">選取 [智慧 + 分析]按一下 [Machine Learning 工作區]，然後按一下 [建立]</span><span class="sxs-lookup"><span data-stu-id="31673-111">Select **Intelligence + analytics**, click **Machine Learning Workspace**, then click **Create**</span></span>

4. <span data-ttu-id="31673-112">輸入您的工作區資訊</span><span class="sxs-lookup"><span data-stu-id="31673-112">Enter your workspace information</span></span>

    - <span data-ttu-id="31673-113">工作區名稱可能最多 260 個字元，結尾不可為空格。</span><span class="sxs-lookup"><span data-stu-id="31673-113">The *workspace name* may be up to 260 characters, not ending in a space.</span></span> <span data-ttu-id="31673-114">名稱不能包含下列字元︰`< > * % & : \ ? + /`</span><span class="sxs-lookup"><span data-stu-id="31673-114">The name can't include these characters: `< > * % & : \ ? + /`</span></span>
    - <span data-ttu-id="31673-115">會使用您選擇 (或建立) 的 Web 服務方案，以及您選取的相關聯定價層，如果您從此工作區中部署 web 服務。</span><span class="sxs-lookup"><span data-stu-id="31673-115">The *web service plan* you choose (or create), along with the associated *pricing tier* you select, is used if you deploy web services from this workspace.</span></span>

    ![建立新的工作區](media/machine-learning-create-workspace/create-new-workspace.png)

5. <span data-ttu-id="31673-117">按一下 [建立] </span><span class="sxs-lookup"><span data-stu-id="31673-117">Click **Create**</span></span>

<span data-ttu-id="31673-118">一旦部署工作區之後，您可以在 Machine Learning Studio 中開啟它。</span><span class="sxs-lookup"><span data-stu-id="31673-118">Once the workspace is deployed, you can open it in Machine Learning Studio.</span></span>

1. <span data-ttu-id="31673-119">瀏覽 Machine Learning Studio ([https://studio.azureml.net](https://studio.azureml.net/))。</span><span class="sxs-lookup"><span data-stu-id="31673-119">Browse to Machine Learning Studio at [https://studio.azureml.net/](https://studio.azureml.net/).</span></span>

2. <span data-ttu-id="31673-120">選取您右上角的工作區。</span><span class="sxs-lookup"><span data-stu-id="31673-120">Select your workspace in the upper-right-hand corner.</span></span>

    ![選取工作區](media/machine-learning-create-workspace/open-workspace.png)

3. <span data-ttu-id="31673-122">按一下 [我的實驗]。</span><span class="sxs-lookup"><span data-stu-id="31673-122">Click **my experiments**.</span></span>

    ![開啟實驗](media/machine-learning-create-workspace/my-experiments.png)

<span data-ttu-id="31673-124">如需管理您的工作區的詳細資訊，請參閱 [管理 Azure Machine Learning 工作區](machine-learning-manage-workspace.md)。</span><span class="sxs-lookup"><span data-stu-id="31673-124">For information about managing your workspace, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
<span data-ttu-id="31673-125">如果您對於建立您的工作區遇到問題，請參閱 [疑難排解指南：建立及連線至 Machine Learning 工作區](machine-learning-troubleshooting-creating-ml-workspace.md)。</span><span class="sxs-lookup"><span data-stu-id="31673-125">If you encounter a problem creating your workspace, see [Troubleshooting guide: Create and connect to a Machine Learning workspace](machine-learning-troubleshooting-creating-ml-workspace.md).</span></span>


## <a name="sharing-an-azure-machine-learning-workspace"></a><span data-ttu-id="31673-126">共用 Azure 機器學習服務工作區</span><span class="sxs-lookup"><span data-stu-id="31673-126">Sharing an Azure Machine Learning workspace</span></span>
<span data-ttu-id="31673-127">建立 Machine Learning 工作區 之後，您就可以邀請使用者加入您的工作區，並與您的工作區和其所有實驗、資料集、筆記型電腦等共用存取權。您可以將使用者新增至兩個角色之一︰</span><span class="sxs-lookup"><span data-stu-id="31673-127">Once a Machine Learning workspace is created, you can invite users to your workspace to share access to your workspace and all its experiments, datasets, notebooks, etc. You can add users in one of two roles:</span></span>

* <span data-ttu-id="31673-128">**使用者** - 工作區使用者可以在工作區中建立、開啟、修改和刪除實驗、資料集等。</span><span class="sxs-lookup"><span data-stu-id="31673-128">**User** - A workspace user can create, open, modify, and delete experiments, datasets, etc. in the workspace.</span></span>
* <span data-ttu-id="31673-129">**擁有者** - 除了使用者可以執行的動作以外，擁有者可以邀請和移除工作區中的使用者。</span><span class="sxs-lookup"><span data-stu-id="31673-129">**Owner** - An owner can invite and remove users in the workspace, in addition to what a user can do.</span></span>

> [!NOTE]
> <span data-ttu-id="31673-130">建立工作區的系統管理員帳戶會自動以工作區擁有者身分新增至工作區。</span><span class="sxs-lookup"><span data-stu-id="31673-130">The administrator account that creates the workspace is automatically added to the workspace as workspace Owner.</span></span> <span data-ttu-id="31673-131">不過，其他的系統管理員或該訂用帳戶中的使用者不會自動授與工作區的存取權 - 您必須先明確邀請他們。</span><span class="sxs-lookup"><span data-stu-id="31673-131">However, other administrators or users in that subscription are not automatically granted access to the workspace - you need to invite them explicitly.</span></span>
> 
> 

### <a name="to-share-a-workspace"></a><span data-ttu-id="31673-132">共用工作區</span><span class="sxs-lookup"><span data-stu-id="31673-132">To share a workspace</span></span>

1. <span data-ttu-id="31673-133">登入 Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home))</span><span class="sxs-lookup"><span data-stu-id="31673-133">Sign in to Machine Learning Studio at [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span></span>

2. <span data-ttu-id="31673-134">按一下左面板中的 [設定]</span><span class="sxs-lookup"><span data-stu-id="31673-134">In the left panel, click **SETTINGS**</span></span>

3. <span data-ttu-id="31673-135">按一下 [使用者] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="31673-135">Click the **USERS** tab</span></span>

4. <span data-ttu-id="31673-136">按一下頁面底部的 [邀請更多使用者]</span><span class="sxs-lookup"><span data-stu-id="31673-136">Click **INVITE MORE USERS** at the bottom of the page</span></span>

    ![Studio 設定](media/machine-learning-create-workspace/settings.png)

5. <span data-ttu-id="31673-138">輸入一或多個電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="31673-138">Enter one or more email addresses.</span></span> <span data-ttu-id="31673-139">使用者需要有效的 Microsoft 帳戶或組織帳戶 (來自 Azure Active Directory)。</span><span class="sxs-lookup"><span data-stu-id="31673-139">The users need a valid Microsoft account or an organizational account (from Azure Active Directory).</span></span>

6. <span data-ttu-id="31673-140">選取您是否想要將使用者新增為擁有者或使用者。</span><span class="sxs-lookup"><span data-stu-id="31673-140">Select whether you want to add the users as Owner or User.</span></span>

7. <span data-ttu-id="31673-141">按一下 [確定] 核取記號按鈕。</span><span class="sxs-lookup"><span data-stu-id="31673-141">Click the **OK** checkmark button.</span></span>

<span data-ttu-id="31673-142">您新增的每個使用者會收到一封電子郵件，其中含有如何登入共用工作區的指示。</span><span class="sxs-lookup"><span data-stu-id="31673-142">Each user you add will receive an email with instructions on how to sign in to the shared workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="31673-143">若要讓使用者能夠部署或管理此工作區中的 web 服務，它們必須為參與者或 Azure 訂用帳戶中的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="31673-143">For users to be able to deploy or manage web services in this workspace, they must be a contributor or administrator in the Azure subscription.</span></span> 



