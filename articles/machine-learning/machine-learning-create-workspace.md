---
title: "aaaCreate Machine Learning 工作區 |Microsoft 文件"
description: "如何 toocreate Azure Machine Learning Studio 中的工作區"
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
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a><span data-ttu-id="11f67-103">建立和共用 Azure Machine Learning 工作區</span><span class="sxs-lookup"><span data-stu-id="11f67-103">Create and share an Azure Machine Learning workspace</span></span>
<span data-ttu-id="11f67-104">這個功能表連結描述如何設定 hello tooset 各種資料科學環境使用 hello Cortana 分析程序 (CAP) 的 tootopics。</span><span class="sxs-lookup"><span data-stu-id="11f67-104">This menu links tootopics that describe how tooset up hello various data science environments used by hello Cortana Analytics Process (CAPS).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="11f67-105">toouse Azure Machine Learning Studio 中，您需要 toohave Machine Learning 工作區。</span><span class="sxs-lookup"><span data-stu-id="11f67-105">toouse Azure Machine Learning Studio, you need toohave a Machine Learning workspace.</span></span> <span data-ttu-id="11f67-106">此工作區包含所需 toocreate hello 工具、 管理及發佈實驗。</span><span class="sxs-lookup"><span data-stu-id="11f67-106">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a><span data-ttu-id="11f67-107">toocreate 工作區</span><span class="sxs-lookup"><span data-stu-id="11f67-107">toocreate a workspace</span></span>
1. <span data-ttu-id="11f67-108">登入 toohello [Azure 入口網站](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="11f67-108">Sign in toohello [Azure portal](https://portal.azure.com/)</span></span>

    > [!NOTE]
    > <span data-ttu-id="11f67-109">toosign 中的和建立工作區，您需要 toobe Azure 訂用帳戶系統管理員。</span><span class="sxs-lookup"><span data-stu-id="11f67-109">toosign in and create a workspace, you need toobe an Azure subscription administrator.</span></span> 
    >
    > 

2. <span data-ttu-id="11f67-110">按一下 [+ 新增]</span><span class="sxs-lookup"><span data-stu-id="11f67-110">Click **+New**</span></span>

3. <span data-ttu-id="11f67-111">選取 [智慧 + 分析]按一下 [Machine Learning 工作區]，然後按一下 [建立]</span><span class="sxs-lookup"><span data-stu-id="11f67-111">Select **Intelligence + analytics**, click **Machine Learning Workspace**, then click **Create**</span></span>

4. <span data-ttu-id="11f67-112">輸入您的工作區資訊</span><span class="sxs-lookup"><span data-stu-id="11f67-112">Enter your workspace information</span></span>

    - <span data-ttu-id="11f67-113">hello*工作區名稱*too260 字元、 空格結尾不存在。</span><span class="sxs-lookup"><span data-stu-id="11f67-113">hello *workspace name* may be up too260 characters, not ending in a space.</span></span> <span data-ttu-id="11f67-114">hello 名稱不能包含下列字元：`< > * % & : \ ? + /`</span><span class="sxs-lookup"><span data-stu-id="11f67-114">hello name can't include these characters: `< > * % & : \ ? + /`</span></span>
    - <span data-ttu-id="11f67-115">hello *web 服務計劃*您選擇 （或建立），以及相關聯的 hello*定價層*您選取，如果您將部署此工作區的 web 服務使用。</span><span class="sxs-lookup"><span data-stu-id="11f67-115">hello *web service plan* you choose (or create), along with hello associated *pricing tier* you select, is used if you deploy web services from this workspace.</span></span>

    ![建立新的工作區](media/machine-learning-create-workspace/create-new-workspace.png)

5. <span data-ttu-id="11f67-117">按一下 [建立] </span><span class="sxs-lookup"><span data-stu-id="11f67-117">Click **Create**</span></span>

<span data-ttu-id="11f67-118">Hello 工作區部署之後，您可以在 Machine Learning Studio 中開啟它。</span><span class="sxs-lookup"><span data-stu-id="11f67-118">Once hello workspace is deployed, you can open it in Machine Learning Studio.</span></span>

1. <span data-ttu-id="11f67-119">瀏覽 tooMachine Learning Studio 在[https://studio.azureml.net/](https://studio.azureml.net/)。</span><span class="sxs-lookup"><span data-stu-id="11f67-119">Browse tooMachine Learning Studio at [https://studio.azureml.net/](https://studio.azureml.net/).</span></span>

2. <span data-ttu-id="11f67-120">選取您的工作區在 hello 上限右手邊角。</span><span class="sxs-lookup"><span data-stu-id="11f67-120">Select your workspace in hello upper-right-hand corner.</span></span>

    ![選取工作區](media/machine-learning-create-workspace/open-workspace.png)

3. <span data-ttu-id="11f67-122">按一下 [我的實驗]。</span><span class="sxs-lookup"><span data-stu-id="11f67-122">Click **my experiments**.</span></span>

    ![開啟實驗](media/machine-learning-create-workspace/my-experiments.png)

<span data-ttu-id="11f67-124">如需管理您的工作區的詳細資訊，請參閱 [管理 Azure Machine Learning 工作區](machine-learning-manage-workspace.md)。</span><span class="sxs-lookup"><span data-stu-id="11f67-124">For information about managing your workspace, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
<span data-ttu-id="11f67-125">如果您遇到問題，建立您的工作區，請參閱[疑難排解指南： 建立和連線 tooa Machine Learning 工作區](machine-learning-troubleshooting-creating-ml-workspace.md)。</span><span class="sxs-lookup"><span data-stu-id="11f67-125">If you encounter a problem creating your workspace, see [Troubleshooting guide: Create and connect tooa Machine Learning workspace](machine-learning-troubleshooting-creating-ml-workspace.md).</span></span>


## <a name="sharing-an-azure-machine-learning-workspace"></a><span data-ttu-id="11f67-126">共用 Azure 機器學習服務工作區</span><span class="sxs-lookup"><span data-stu-id="11f67-126">Sharing an Azure Machine Learning workspace</span></span>
<span data-ttu-id="11f67-127">一旦建立機器學習服務工作區，您可以邀請使用者 tooyour 工作區 tooshare 存取 tooyour 工作區和所有其實驗、 資料集、 筆記本等等。您可以將使用者新增至兩個角色之一︰</span><span class="sxs-lookup"><span data-stu-id="11f67-127">Once a Machine Learning workspace is created, you can invite users tooyour workspace tooshare access tooyour workspace and all its experiments, datasets, notebooks, etc. You can add users in one of two roles:</span></span>

* <span data-ttu-id="11f67-128">**使用者**-工作區中使用者可以建立、 開啟、 修改及刪除實驗、 資料集等 hello 工作區中。</span><span class="sxs-lookup"><span data-stu-id="11f67-128">**User** - A workspace user can create, open, modify, and delete experiments, datasets, etc. in hello workspace.</span></span>
* <span data-ttu-id="11f67-129">**擁有者**-擁有者可以邀請，並移除 hello 工作區中增加 toowhat 使用者的使用者可以執行。</span><span class="sxs-lookup"><span data-stu-id="11f67-129">**Owner** - An owner can invite and remove users in hello workspace, in addition toowhat a user can do.</span></span>

> [!NOTE]
> <span data-ttu-id="11f67-130">建立 hello 工作區中的 hello 系統管理員帳戶會自動加入 toohello 工作區中，為工作區擁有者。</span><span class="sxs-lookup"><span data-stu-id="11f67-130">hello administrator account that creates hello workspace is automatically added toohello workspace as workspace Owner.</span></span> <span data-ttu-id="11f67-131">不過，其他的系統管理員或使用者，因為訂用帳戶不會自動授與存取權 toohello 工作區-您需要 tooinvite 它們明確。</span><span class="sxs-lookup"><span data-stu-id="11f67-131">However, other administrators or users in that subscription are not automatically granted access toohello workspace - you need tooinvite them explicitly.</span></span>
> 
> 

### <a name="tooshare-a-workspace"></a><span data-ttu-id="11f67-132">tooshare 工作區</span><span class="sxs-lookup"><span data-stu-id="11f67-132">tooshare a workspace</span></span>

1. <span data-ttu-id="11f67-133">登入 tooMachine 學習 Studio 在[https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span><span class="sxs-lookup"><span data-stu-id="11f67-133">Sign in tooMachine Learning Studio at [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span></span>

2. <span data-ttu-id="11f67-134">在 hello 左面板中，按一下 **設定**</span><span class="sxs-lookup"><span data-stu-id="11f67-134">In hello left panel, click **SETTINGS**</span></span>

3. <span data-ttu-id="11f67-135">按一下 hello**使用者** 索引標籤</span><span class="sxs-lookup"><span data-stu-id="11f67-135">Click hello **USERS** tab</span></span>

4. <span data-ttu-id="11f67-136">按一下**更邀請使用者**hello hello 頁底端</span><span class="sxs-lookup"><span data-stu-id="11f67-136">Click **INVITE MORE USERS** at hello bottom of hello page</span></span>

    ![Studio 設定](media/machine-learning-create-workspace/settings.png)

5. <span data-ttu-id="11f67-138">輸入一或多個電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="11f67-138">Enter one or more email addresses.</span></span> <span data-ttu-id="11f67-139">hello 使用者需要有效的 Microsoft 帳戶或組織帳戶 （從 Azure Active Directory)。</span><span class="sxs-lookup"><span data-stu-id="11f67-139">hello users need a valid Microsoft account or an organizational account (from Azure Active Directory).</span></span>

6. <span data-ttu-id="11f67-140">選取是否要 tooadd hello 使用者作為擁有者或使用者。</span><span class="sxs-lookup"><span data-stu-id="11f67-140">Select whether you want tooadd hello users as Owner or User.</span></span>

7. <span data-ttu-id="11f67-141">按一下 hello**確定**核取記號按鈕。</span><span class="sxs-lookup"><span data-stu-id="11f67-141">Click hello **OK** checkmark button.</span></span>

<span data-ttu-id="11f67-142">您新增的每個使用者會收到一封電子郵件，說明如何在 toohello toosign 共用工作區。</span><span class="sxs-lookup"><span data-stu-id="11f67-142">Each user you add will receive an email with instructions on how toosign in toohello shared workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="11f67-143">針對使用者 toobe 無法 toodeploy 或管理 web 服務，此工作區中的，它們必須參與者或 hello Azure 訂用帳戶中的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="11f67-143">For users toobe able toodeploy or manage web services in this workspace, they must be a contributor or administrator in hello Azure subscription.</span></span> 



