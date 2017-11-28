---
title: "aaaAdd Azure DevTest Labs claimable VM tooa 實驗室 |Microsoft 文件"
description: "深入了解如何 tooadd claimable 虛擬機器 tooa 實驗室中 Azure DevTest Labs"
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
ms.openlocfilehash: fe6385ae2e59b9636b82aec250dc3a1f8a40ba5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="b4553-103">在 Azure DevTest Labs 中加入 claimable VM tooa 實驗室</span><span class="sxs-lookup"><span data-stu-id="b4553-103">Add a claimable VM tooa lab in Azure DevTest Labs</span></span>
<span data-ttu-id="b4553-104">您可以加入 claimable VM tooa 實驗室環境中類似的方式 toohow 您[加入標準 VM](devtest-lab-add-vm.md) – 從*基底*也就是 [自訂映像](devtest-lab-create-template.md)，[公式](devtest-lab-manage-formulas.md)，或[Marketplace 映像](devtest-lab-configure-marketplace-images.md)。</span><span class="sxs-lookup"><span data-stu-id="b4553-104">You add a claimable VM tooa lab in a similar manner toohow you [add a standard VM](devtest-lab-add-vm.md) – from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="b4553-105">本教學課程引導您使用 Azure 入口網站 tooadd hello DevTest Labs claimable VM tooa 實驗室，並顯示 hello 程序的使用者依照 tooclaim hello VM。</span><span class="sxs-lookup"><span data-stu-id="b4553-105">This tutorial walks you through using hello Azure portal tooadd a claimable VM tooa lab in DevTest Labs, and shows hello process a user follows tooclaim hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="b4553-106">如果您將部署到實驗室 Vm [Azure 資源管理員範本](devtest-lab-create-environment-from-arm.md)，您可以建立 claimable Vm 設定 hello **allowClaim**屬性 tootrue hello 屬性區段中的。</span><span class="sxs-lookup"><span data-stu-id="b4553-106">If you deploy lab VMs through [Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md), you can create claimable VMs by setting hello **allowClaim** property tootrue in hello properties section.</span></span>
>
>

## <a name="steps-tooadd-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="b4553-107">步驟 tooadd Azure DevTest Labs claimable VM tooa 實驗室</span><span class="sxs-lookup"><span data-stu-id="b4553-107">Steps tooadd a claimable VM tooa lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="b4553-108">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="b4553-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="b4553-109">選取**更服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="b4553-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="b4553-110">從 hello 清單的實驗室中，選取 hello 實驗室中您想要 toocreate hello claimable VM。</span><span class="sxs-lookup"><span data-stu-id="b4553-110">From hello list of labs, select hello lab in which you want toocreate hello claimable VM.</span></span>  
1. <span data-ttu-id="b4553-111">在 hello 實驗室**概觀**刀鋒視窗中，選取**+ 加**。</span><span class="sxs-lookup"><span data-stu-id="b4553-111">On hello lab's **Overview** blade, select **+ Add**.</span></span>  

    ![加入 VM 按鈕](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="b4553-113">在 hello**選擇基底**刀鋒視窗中，選取一個 hello VM 的基底。</span><span class="sxs-lookup"><span data-stu-id="b4553-113">On hello **Choose a base** blade, select a base for hello VM.</span></span>
1. <span data-ttu-id="b4553-114">在 hello**虛擬機器**刀鋒視窗中，輸入 hello 新的虛擬機器的名稱在 hello**虛擬機器名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="b4553-114">On hello **Virtual machine** blade, enter a name for hello new virtual machine in hello **Virtual machine name** text box.</span></span>

    ![實驗室 VM 刀鋒視窗](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="b4553-116">輸入**使用者名**，授與 hello 虛擬機器上的系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="b4553-116">Enter a **User Name** that is granted administrator privileges on hello virtual machine.</span></span>  
1. <span data-ttu-id="b4553-117">如果您想要 toouse 密碼儲存在您[密碼存放區](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)，選取**使用已儲存的密碼**，並指定一個索引鍵的值，對應 tooyour 秘密 （密碼）。</span><span class="sxs-lookup"><span data-stu-id="b4553-117">If you want toouse a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds tooyour secret (password).</span></span> <span data-ttu-id="b4553-118">否則，標示為的 hello 文字欄位中輸入密碼**輸入值**。</span><span class="sxs-lookup"><span data-stu-id="b4553-118">Otherwise, enter a password in hello text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="b4553-119">hello**虛擬機器磁碟類型**會決定哪些儲存磁碟類型可供 hello hello 實驗室中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b4553-119">hello **Virtual machine disk type** determines which storage disk type is allowed for hello virtual machines in hello lab.</span></span>
1. <span data-ttu-id="b4553-120">選取**虛擬機器大小**和選取 hello 的其中一個預先定義的指定 hello 處理器核心、 RAM 大小，以及 hello VM toocreate hello 硬碟大小的項目。</span><span class="sxs-lookup"><span data-stu-id="b4553-120">Select **Virtual machine size** and select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span>
1. <span data-ttu-id="b4553-121">選取**成品**及從 hello 成品的清單，選取並設定您想 tooadd toohello 基底映像的 hello 成品。</span><span class="sxs-lookup"><span data-stu-id="b4553-121">Select **Artifacts** and from hello list of artifacts, select and configure hello artifacts that you want tooadd toohello base image.</span></span> <span data-ttu-id="b4553-122">如果您是新 tooDevTest 實驗室或設定成品，請參閱 toohello[加入現有的成品 tooa VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm)區段，然後再在完成時，返回此處。</span><span class="sxs-lookup"><span data-stu-id="b4553-122">If you're new tooDevTest Labs or configuring artifacts, refer toohello [Add an existing artifact tooa VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="b4553-123">選取**進階設定**tooconfigure hello VM 的網路選項和到期選項。</span><span class="sxs-lookup"><span data-stu-id="b4553-123">Select **Advanced settings** tooconfigure hello VM's network options and expiration options.</span></span> <span data-ttu-id="b4553-124">在下**宣告選項**，選擇**是**claimable toomake hello 機器。</span><span class="sxs-lookup"><span data-stu-id="b4553-124">Under **Claim options**, choose **Yes** toomake hello machine claimable.</span></span>

  ![選擇 toomake hello claimable VM。](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. <span data-ttu-id="b4553-126">如果您想 tooview，或複製 hello Azure 資源管理員範本，請參閱 toohello[儲存 Azure Resource Manager 範本](devtest-lab-add-vm.md#save-azure-resource-manager-template)區段，然後完成時，請回到這裡。</span><span class="sxs-lookup"><span data-stu-id="b4553-126">If you want tooview or copy hello Azure Resource Manager template, refer toohello [Save Azure Resource Manager template](devtest-lab-add-vm.md#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="b4553-127">選取**建立**tooadd hello 指定 VM toohello 實驗室。</span><span class="sxs-lookup"><span data-stu-id="b4553-127">Select **Create** tooadd hello specified VM toohello lab.</span></span>
1. <span data-ttu-id="b4553-128">hello 實驗室刀鋒視窗會顯示 hello 狀態的 hello VM 建立-第一次為**建立**，然後為**執行**之後 hello VM 已啟動。</span><span class="sxs-lookup"><span data-stu-id="b4553-128">hello lab blade displays hello status of hello VM's creation - first as **Creating**, then as **Running** after hello VM has been started.</span></span>


## <a name="using-a-claimable-vm"></a><span data-ttu-id="b4553-129">使用可宣告 VM</span><span class="sxs-lookup"><span data-stu-id="b4553-129">Using a claimable VM</span></span>

<span data-ttu-id="b4553-130">使用者可以宣告任何 hello 清單中的 「 Claimable 虛擬機器 」 的 VM 執行這些步驟的其中一項：</span><span class="sxs-lookup"><span data-stu-id="b4553-130">A user can claim any VM from hello list of "Claimable virtual machines" by doing one of these steps:</span></span>

* <span data-ttu-id="b4553-131">從 hello 清單中的 「 Claimable 虛擬機器 」 在 hello hello 實驗室概觀刀鋒視窗的底部，以滑鼠右鍵按一下其中一個 hello 清單中的 hello Vm 上，然後選擇 **宣告機器**。</span><span class="sxs-lookup"><span data-stu-id="b4553-131">From hello list of "Claimable virtual machines" at hello bottom of hello lab's Overview blade, right-click on one of hello VMs in hello list and choose **Claim machine**.</span></span>

 ![要求特定可宣告 VM。](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* <span data-ttu-id="b4553-133">頂端的 hello hello**概觀**刀鋒視窗中，選擇**宣告任何**。</span><span class="sxs-lookup"><span data-stu-id="b4553-133">At hello top of hello **Overview** blade, choose **Claim any**.</span></span> <span data-ttu-id="b4553-134">隨機的虛擬機器指派的 hello claimable Vm 清單。</span><span class="sxs-lookup"><span data-stu-id="b4553-134">A random virtual machine is assigned from hello list of claimable VMs.</span></span>

 ![要求任何可宣告 VM。](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


<span data-ttu-id="b4553-136">在使用者宣告 VM 之後，該 VM 將會移至該使用者的 [我的虛擬機器] 清單，且其他使用者將無法宣告該 VM。</span><span class="sxs-lookup"><span data-stu-id="b4553-136">After a user claims a VM, it is moved up into their list of "My virtual machines" and is no longer claimable by any other user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4553-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b4553-137">Next steps</span></span>
* <span data-ttu-id="b4553-138">一次 hello 在建立 VM，您可以連接 toohello VM 選取**連接**hello VM 刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="b4553-138">Once hello VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="b4553-139">瀏覽 hello [DevTest Labs Azure 資源管理員的快速入門範本庫](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span><span class="sxs-lookup"><span data-stu-id="b4553-139">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span></span>
