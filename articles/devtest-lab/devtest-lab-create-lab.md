---
title: "在 Azure DevTest Labs 中建立實驗室 | Microsoft Docs"
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
ms.openlocfilehash: 265a968f902f53c7561c8c7e937f8eacfdb37167
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="ca7a6-103">在 Azure 研測實驗室中建立實驗室</span><span class="sxs-lookup"><span data-stu-id="ca7a6-103">Create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="ca7a6-104">Azure DevTest Labs 中的實驗室是包含一組資源 (例如虛擬機器 (VM)) 的基礎結構，可讓您藉由指定限制和配額更好地管理這些資源。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-104">A lab in Azure DevTest Labs is the infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span> <span data-ttu-id="ca7a6-105">本文將逐步引導您完成使用 Azure 入口網站來建立實驗室的程序。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-105">This article walks you through the process of creating a lab using the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca7a6-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="ca7a6-106">Prerequisites</span></span>
<span data-ttu-id="ca7a6-107">若要建立實驗室，您需要：</span><span class="sxs-lookup"><span data-stu-id="ca7a6-107">To create a lab, you need:</span></span>

* <span data-ttu-id="ca7a6-108">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-108">An Azure subscription.</span></span> <span data-ttu-id="ca7a6-109">若要深入了解 Azure 購買選項，請參閱[如何購買 Azure](https://azure.microsoft.com/pricing/purchase-options/) 或[免費試用一個月](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-109">To learn about Azure purchase options, see [How to buy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="ca7a6-110">您必須是訂用帳戶的擁有者才能建立實驗室。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-110">You must be the owner of the subscription to create the lab.</span></span>

## <a name="steps-to-create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="ca7a6-111">在 Azure DevTest Labs 中建立實驗室的步驟</span><span class="sxs-lookup"><span data-stu-id="ca7a6-111">Steps to create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="ca7a6-112">下列步驟說明如何使用 Azure 入口網站在 Azure DevTest Labs 中建立實驗室。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-112">The following steps illustrate how to use the Azure portal to create a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="ca7a6-113">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-113">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="ca7a6-114">從左側的主要功能表中，選取 [更多服務] \(位於清單底部)。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-114">From the main menu on the left side, select **More Services** (at the bottom of the list).</span></span>

    ![[更多服務] 功能表選項](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. <span data-ttu-id="ca7a6-116">從可用服務清單中，選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-116">From the list of available services, **DevTest Labs**.</span></span>
1. <span data-ttu-id="ca7a6-117">在 [DevTest Labs] 刀鋒視窗上，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-117">On the **DevTest Labs** blade, select **Add**.</span></span>
   
    ![新增實驗室](./media/devtest-lab-create-lab/add-lab-button.png)

1. <span data-ttu-id="ca7a6-119">在 [建立 DevTest 實驗室]  刀鋒視窗上：</span><span class="sxs-lookup"><span data-stu-id="ca7a6-119">On the **Create a DevTest Lab** blade:</span></span>
   
    1. <span data-ttu-id="ca7a6-120">輸入新實驗室的 **實驗室名稱** 。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-120">Enter a **Lab Name** for the new lab.</span></span>
    2. <span data-ttu-id="ca7a6-121">選取要與實驗室關聯的 **訂用帳戶** 。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-121">Select the **Subscription** to associate with the lab.</span></span>
    3. <span data-ttu-id="ca7a6-122">選取用來儲存實驗室的 [位置]  。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-122">Select a **Location** in which to store the lab.</span></span>
    4. <span data-ttu-id="ca7a6-123">選取 [自動關機]  來指定是否要啟用所有實驗室 VM 的自動關閉，以及定義其參數。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-123">Select **Auto-shutdown** to specify if you want to enable - and define the parameters for - the automatic shutting down of all the lab's VMs.</span></span> <span data-ttu-id="ca7a6-124">自動關閉功能主要是用來節省成本的功能，若您想要讓 VM 自動關閉，便可指定此功能。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-124">The auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want the VM to automatically be shut down.</span></span> <span data-ttu-id="ca7a6-125">您可以按照[在 Azure DevTest Labs 中管理實驗室的所有原則](./devtest-lab-set-lab-policy.md#set-auto-shutdown)一文所述的步驟，在建立實驗室之後變更自動關閉設定。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-125">You can change auto-shutdown settings after creating the lab by following the steps outlined in the article, [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span></span>
    5. <span data-ttu-id="ca7a6-126">如果您希望在入口網站儀表板上顯示實驗室的捷徑，請選取 [釘選到儀表板]。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-126">Select **Pin to Dashboard** if you want a shortcut of the lab to appear on the portal dashboard.</span></span>
    6. <span data-ttu-id="ca7a6-127">選取 [自動化選項] 來取得可自動進行設定的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-127">Select **Automation options** to get Azure Resource Manager templates for configuration automation.</span></span> 
    7. <span data-ttu-id="ca7a6-128">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-128">Select **Create**.</span></span> <span data-ttu-id="ca7a6-129">在選取 [建立] 之後，[DevTest Labs] 刀鋒視窗便會隨即出現。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-129">After selecting **Create**, the **DevTest Labs** blade displays.</span></span> <span data-ttu-id="ca7a6-130">您可以監看 [通知] 區域，以監控實驗室建立程序的狀態。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-130">You can monitor the status of the lab creation process by watching the **Notifications** area.</span></span> <span data-ttu-id="ca7a6-131">程序完成之後，請重新整理頁面，以在實驗室清單中查看新建立的實驗室。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-131">Once completed, refresh the page to see the newly created lab in the list of labs.</span></span>  
    
    ![建立實驗室刀鋒視窗](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="ca7a6-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ca7a6-133">Next steps</span></span>
<span data-ttu-id="ca7a6-134">建立您的實驗室之後，以下是要考慮的一些後續步驟：</span><span class="sxs-lookup"><span data-stu-id="ca7a6-134">Once you've created your lab, here are some next steps to consider:</span></span>

* <span data-ttu-id="ca7a6-135">[安全存取實驗室](devtest-lab-add-devtest-user.md)。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-135">[Secure access to a lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="ca7a6-136">[設定實驗室原則](devtest-lab-set-lab-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-136">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="ca7a6-137">[建立實驗室範本](devtest-lab-create-template.md)。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-137">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="ca7a6-138">[為您的 VM 建立自訂成品](devtest-lab-artifact-author.md)。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-138">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="ca7a6-139">[將具有構件的 VM 新增至實驗室](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/)。</span><span class="sxs-lookup"><span data-stu-id="ca7a6-139">[Add a VM with artifacts to a lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span></span>

