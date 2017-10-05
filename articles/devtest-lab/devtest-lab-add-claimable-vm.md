---
title: "在 Azure DevTest Labs 中對實驗室新增可宣告 VM | Microsoft Docs"
description: "了解如何在 Azure DevTest Labs 中對實驗室新增可宣告的虛擬機器"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: 98950d72e90b0e178bae2fffa7644fd824a25eea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-claimable-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="05e68-103">在 Azure DevTest Labs 中對實驗室新增可宣告 VM</span><span class="sxs-lookup"><span data-stu-id="05e68-103">Add a claimable VM to a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="05e68-104">您可以從[自訂映像](devtest-lab-create-template.md)、[公式](devtest-lab-manage-formulas.md)或 [Marketplace 映像](devtest-lab-configure-marketplace-images.md)等「基底」，使用和[新增標準 VM](devtest-lab-add-vm.md) 相似的方法將可宣告 VM 新增至實驗室。</span><span class="sxs-lookup"><span data-stu-id="05e68-104">You add a claimable VM to a lab in a similar manner to how you [add a standard VM](devtest-lab-add-vm.md) – from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="05e68-105">本教學課程會逐步引導您使用 Azure 入口網站將可宣告 VM 新增至 DevTest Labs 中的實驗室，並示範宣告 VM 的程序。</span><span class="sxs-lookup"><span data-stu-id="05e68-105">This tutorial walks you through using the Azure portal to add a claimable VM to a lab in DevTest Labs, and shows the process a user follows to claim the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="05e68-106">如果您是透過 [Azure Resource Manager 範本](devtest-lab-create-environment-from-arm.md)部署實驗室 VM，您可以在 [屬性] 區段中將 **allowClaim** 屬性設定為 [true]，來建立可宣告 VM。</span><span class="sxs-lookup"><span data-stu-id="05e68-106">If you deploy lab VMs through [Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md), you can create claimable VMs by setting the **allowClaim** property to true in the properties section.</span></span>
>
>

## <a name="steps-to-add-a-claimable-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="05e68-107">將可宣告 VM 新增至 Azure DevTest Labs 中實驗室的步驟</span><span class="sxs-lookup"><span data-stu-id="05e68-107">Steps to add a claimable VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="05e68-108">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="05e68-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="05e68-109">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="05e68-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="05e68-110">從實驗室清單中，選取您想要在其中建立可宣告 VM 的實驗室。</span><span class="sxs-lookup"><span data-stu-id="05e68-110">From the list of labs, select the lab in which you want to create the claimable VM.</span></span>  
1. <span data-ttu-id="05e68-111">在實驗室的 [概觀] 刀鋒視窗中，選取 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="05e68-111">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![加入 VM 按鈕](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="05e68-113">在 [選擇基底]  刀鋒視窗中，選取 VM 的基底。</span><span class="sxs-lookup"><span data-stu-id="05e68-113">On the **Choose a base** blade, select a base for the VM.</span></span>
1. <span data-ttu-id="05e68-114">在 [虛擬機器] 刀鋒視窗的 [虛擬機器名稱] 文字方塊中，輸入新虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="05e68-114">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![實驗室 VM 刀鋒視窗](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="05e68-116">輸入**使用者名稱**，此名稱會被授與虛擬機器上的系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="05e68-116">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="05e68-117">如果您想使用儲存在[密碼存放區](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)中的密碼，請選取 [使用儲存的密碼]，並指定與密碼對應的金鑰值。</span><span class="sxs-lookup"><span data-stu-id="05e68-117">If you want to use a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds to your secret (password).</span></span> <span data-ttu-id="05e68-118">否則，請在標示為 [輸入值] 的文字欄位中輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="05e68-118">Otherwise, enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="05e68-119">[虛擬機器磁碟類型] 會決定實驗室中的虛擬機器所允許的儲存磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="05e68-119">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="05e68-120">選取 [虛擬機器大小]  ，然後選取其中一個預先定義的項目，這些項目可以指定處理器核心、RAM 大小，以及要建立的 VM 的硬碟大小。</span><span class="sxs-lookup"><span data-stu-id="05e68-120">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="05e68-121">選取 [構件]，然後從構件清單中，選取並設定您想要新增到基本映像中的構件。</span><span class="sxs-lookup"><span data-stu-id="05e68-121">Select **Artifacts** and from the list of artifacts, select and configure the artifacts that you want to add to the base image.</span></span> <span data-ttu-id="05e68-122">如果您對 DevTest Labs 或設定構件並不熟悉，請參閱[將現有的構件加入至 VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) 一節，完成該節之後再返回此處。</span><span class="sxs-lookup"><span data-stu-id="05e68-122">If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="05e68-123">選取 [進階設定] 以設定 VM 的網路選項和到期日選項。</span><span class="sxs-lookup"><span data-stu-id="05e68-123">Select **Advanced settings** to configure the VM's network options and expiration options.</span></span> <span data-ttu-id="05e68-124">在 [宣告選項] 底下，選擇 [是] 來允許宣告機器。</span><span class="sxs-lookup"><span data-stu-id="05e68-124">Under **Claim options**, choose **Yes** to make the machine claimable.</span></span>

  ![選擇以允許宣告 VM。](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. <span data-ttu-id="05e68-126">如果您想要檢視或複製 Azure Resource Manager 範本，請參閱[儲存 Azure Resource Manager 範本](devtest-lab-add-vm.md#save-azure-resource-manager-template)一節，然後在完成時回到這裡。</span><span class="sxs-lookup"><span data-stu-id="05e68-126">If you want to view or copy the Azure Resource Manager template, refer to the [Save Azure Resource Manager template](devtest-lab-add-vm.md#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="05e68-127">選取 [建立]  ，將指定的 VM 加入實驗室。</span><span class="sxs-lookup"><span data-stu-id="05e68-127">Select **Create** to add the specified VM to the lab.</span></span>
1. <span data-ttu-id="05e68-128">實驗室刀鋒視窗會顯示 VM 的建立狀態，其狀態會先是 [正在建立]，在啟動該 VM 之後才會變成 [正在執行]。</span><span class="sxs-lookup"><span data-stu-id="05e68-128">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>


## <a name="using-a-claimable-vm"></a><span data-ttu-id="05e68-129">使用可宣告 VM</span><span class="sxs-lookup"><span data-stu-id="05e68-129">Using a claimable VM</span></span>

<span data-ttu-id="05e68-130">使用者可以透過執行下列其中一項步驟，來宣告 [可宣告的虛擬機器] 清單上的任何 VM：</span><span class="sxs-lookup"><span data-stu-id="05e68-130">A user can claim any VM from the list of "Claimable virtual machines" by doing one of these steps:</span></span>

* <span data-ttu-id="05e68-131">在實驗室 [概觀] 刀鋒視窗底部的 [可宣告的虛擬機器] 清單上，以滑鼠右鍵按一下清單中的其中一個 VM，並選擇 [宣告機器]。</span><span class="sxs-lookup"><span data-stu-id="05e68-131">From the list of "Claimable virtual machines" at the bottom of the lab's Overview blade, right-click on one of the VMs in the list and choose **Claim machine**.</span></span>

 ![要求特定可宣告 VM。](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* <span data-ttu-id="05e68-133">在 [概觀] 刀鋒視窗的頂端，選擇 [宣告任何項目]。</span><span class="sxs-lookup"><span data-stu-id="05e68-133">At the top of the **Overview** blade, choose **Claim any**.</span></span> <span data-ttu-id="05e68-134">系統將會從可宣告 VM 清單中隨機指派虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="05e68-134">A random virtual machine is assigned from the list of claimable VMs.</span></span>

 ![要求任何可宣告 VM。](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


<span data-ttu-id="05e68-136">在使用者宣告 VM 之後，該 VM 將會移至該使用者的 [我的虛擬機器] 清單，且其他使用者將無法宣告該 VM。</span><span class="sxs-lookup"><span data-stu-id="05e68-136">After a user claims a VM, it is moved up into their list of "My virtual machines" and is no longer claimable by any other user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05e68-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="05e68-137">Next steps</span></span>
* <span data-ttu-id="05e68-138">一旦建立 VM 之後，您可以選取 VM 刀鋒視窗上的 [連接]  來連接至 VM。</span><span class="sxs-lookup"><span data-stu-id="05e68-138">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="05e68-139">瀏覽 [DevTest Labs Azure Resource Manager 快速入門範本資源庫](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span><span class="sxs-lookup"><span data-stu-id="05e68-139">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span></span>
