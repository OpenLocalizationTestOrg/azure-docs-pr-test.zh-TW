---
title: "aaaCreate 的實驗室中 Azure DevTest Labs |Microsoft 文件"
description: "在 Azure DevTest Labs 中為虛擬機器建立實驗室"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="7e146-103">在 Azure 研測實驗室中建立實驗室</span><span class="sxs-lookup"><span data-stu-id="7e146-103">Create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="7e146-104">位於 Azure DevTest 實驗室的實驗室是 hello 基礎結構包含一組資源，例如可讓您更佳的虛擬機器 (Vm)，藉由指定限制和配額管理這些資源。</span><span class="sxs-lookup"><span data-stu-id="7e146-104">A lab in Azure DevTest Labs is hello infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span> <span data-ttu-id="7e146-105">這篇文章會引導您建立的實驗室使用 hello Azure 入口網站的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="7e146-105">This article walks you through hello process of creating a lab using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e146-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="7e146-106">Prerequisites</span></span>
<span data-ttu-id="7e146-107">toocreate 實驗室，您需要：</span><span class="sxs-lookup"><span data-stu-id="7e146-107">toocreate a lab, you need:</span></span>

* <span data-ttu-id="7e146-108">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7e146-108">An Azure subscription.</span></span> <span data-ttu-id="7e146-109">請參閱有關 Azure 購買選項 toolearn[如何 toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/)或[免費試用一個月](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="7e146-109">toolearn about Azure purchase options, see [How toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="7e146-110">您必須是 hello hello 訂用帳戶 toocreate hello 實驗室擁有者。</span><span class="sxs-lookup"><span data-stu-id="7e146-110">You must be hello owner of hello subscription toocreate hello lab.</span></span>

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="7e146-111">步驟 toocreate 的實驗室中 Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="7e146-111">Steps toocreate a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="7e146-112">hello 下列步驟說明如何 toouse 會 hello Azure 入口網站 toocreate Azure DevTest 實驗室中的實驗室。</span><span class="sxs-lookup"><span data-stu-id="7e146-112">hello following steps illustrate how toouse hello Azure portal toocreate a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="7e146-113">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="7e146-113">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="7e146-114">從左邊為 hello hello 主功能表上，選取**更服務**（位於 hello hello 清單底部）。</span><span class="sxs-lookup"><span data-stu-id="7e146-114">From hello main menu on hello left side, select **More Services** (at hello bottom of hello list).</span></span>

    ![[更多服務] 功能表選項](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. <span data-ttu-id="7e146-116">從可用服務清單中 hello **DevTest Labs**。</span><span class="sxs-lookup"><span data-stu-id="7e146-116">From hello list of available services, **DevTest Labs**.</span></span>
1. <span data-ttu-id="7e146-117">在 hello **DevTest Labs**刀鋒視窗中，選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="7e146-117">On hello **DevTest Labs** blade, select **Add**.</span></span>
   
    ![新增實驗室](./media/devtest-lab-create-lab/add-lab-button.png)

1. <span data-ttu-id="7e146-119">在 hello**建立 DevTest 實驗室**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="7e146-119">On hello **Create a DevTest Lab** blade:</span></span>
   
    1. <span data-ttu-id="7e146-120">輸入**實驗室名稱**hello 新實驗室。</span><span class="sxs-lookup"><span data-stu-id="7e146-120">Enter a **Lab Name** for hello new lab.</span></span>
    2. <span data-ttu-id="7e146-121">選取 hello**訂用帳戶**tooassociate 與 hello 實驗室。</span><span class="sxs-lookup"><span data-stu-id="7e146-121">Select hello **Subscription** tooassociate with hello lab.</span></span>
    3. <span data-ttu-id="7e146-122">選取**位置**哪些 toostore hello 實驗室中。</span><span class="sxs-lookup"><span data-stu-id="7e146-122">Select a **Location** in which toostore hello lab.</span></span>
    4. <span data-ttu-id="7e146-123">選取**自動關機**toospecify 如果您想 tooenable-定義-hello 參數 hello 自動關閉的所有 hello lab 的 Vm。</span><span class="sxs-lookup"><span data-stu-id="7e146-123">Select **Auto-shutdown** toospecify if you want tooenable - and define hello parameters for - hello automatic shutting down of all hello lab's VMs.</span></span> <span data-ttu-id="7e146-124">hello 自動關閉功能是主要是節省成本的功能，您可以指定當您想 hello VM tooautomatically 關機。</span><span class="sxs-lookup"><span data-stu-id="7e146-124">hello auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want hello VM tooautomatically be shut down.</span></span> <span data-ttu-id="7e146-125">您可以變更自動關閉設定 hello hello 文章所述的步驟建立 hello 實驗室之後[管理所有原則的實驗室中 Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown)。</span><span class="sxs-lookup"><span data-stu-id="7e146-125">You can change auto-shutdown settings after creating hello lab by following hello steps outlined in hello article, [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span></span>
    5. <span data-ttu-id="7e146-126">選取**Pin tooDashboard**如果您想要的 hello 實驗室 tooappear hello 入口網站儀表板上的捷徑。</span><span class="sxs-lookup"><span data-stu-id="7e146-126">Select **Pin tooDashboard** if you want a shortcut of hello lab tooappear on hello portal dashboard.</span></span>
    6. <span data-ttu-id="7e146-127">選取**自動化選項**tooget Azure 資源管理員範本組態自動化。</span><span class="sxs-lookup"><span data-stu-id="7e146-127">Select **Automation options** tooget Azure Resource Manager templates for configuration automation.</span></span> 
    7. <span data-ttu-id="7e146-128">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="7e146-128">Select **Create**.</span></span> <span data-ttu-id="7e146-129">選取之後**建立**，hello **DevTest Labs**刀鋒視窗會顯示。</span><span class="sxs-lookup"><span data-stu-id="7e146-129">After selecting **Create**, hello **DevTest Labs** blade displays.</span></span> <span data-ttu-id="7e146-130">您可以藉由監看 hello 監視 hello 實驗室建立程序的 hello 狀態**通知**區域。</span><span class="sxs-lookup"><span data-stu-id="7e146-130">You can monitor hello status of hello lab creation process by watching hello **Notifications** area.</span></span> <span data-ttu-id="7e146-131">完成後，重新整理 hello 頁面 toosee hello 新建立的實驗室的實驗室 hello 清單中。</span><span class="sxs-lookup"><span data-stu-id="7e146-131">Once completed, refresh hello page toosee hello newly created lab in hello list of labs.</span></span>  
    
    ![建立實驗室刀鋒視窗](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="7e146-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7e146-133">Next steps</span></span>
<span data-ttu-id="7e146-134">一旦您已建立您的實驗室，以下是一些下一個步驟 tooconsider:</span><span class="sxs-lookup"><span data-stu-id="7e146-134">Once you've created your lab, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="7e146-135">[安全存取 tooa 實驗室](devtest-lab-add-devtest-user.md)。</span><span class="sxs-lookup"><span data-stu-id="7e146-135">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="7e146-136">[設定實驗室原則](devtest-lab-set-lab-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="7e146-136">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="7e146-137">[建立實驗室範本](devtest-lab-create-template.md)。</span><span class="sxs-lookup"><span data-stu-id="7e146-137">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="7e146-138">[為您的 VM 建立自訂成品](devtest-lab-artifact-author.md)。</span><span class="sxs-lookup"><span data-stu-id="7e146-138">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="7e146-139">[加入具有成品 tooa 實驗室 VM](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/)。</span><span class="sxs-lookup"><span data-stu-id="7e146-139">[Add a VM with artifacts tooa lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span></span>

