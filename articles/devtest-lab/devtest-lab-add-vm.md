---
title: "aaaAdd VM tooa 實驗室中 Azure DevTest Labs |Microsoft 文件"
description: "深入了解如何在 Azure DevTest Labs 虛擬機器 tooa 實驗室 tooadd"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: tarcher
ms.openlocfilehash: 82838e4349550db56de311264c188140b9556b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="4c93c-103">新增 VM tooa 實驗室中 Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4c93c-103">Add a VM tooa lab in Azure DevTest Labs</span></span>
<span data-ttu-id="4c93c-104">如果您已經[建立您的第一個 VM](devtest-lab-create-first-vm.md)，您很有可能是透過預先載入的 [Marketplace 映像](devtest-lab-configure-marketplace-images.md)來完成的。</span><span class="sxs-lookup"><span data-stu-id="4c93c-104">If you have already [created your first VM](devtest-lab-create-first-vm.md), you likely did so from a pre-loaded [marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="4c93c-105">現在，如果您想 tooadd 後續 Vm tooyour 實驗室，您也可以選擇*基底*也就是 [自訂映像](devtest-lab-create-template.md)或[公式](devtest-lab-manage-formulas.md)。</span><span class="sxs-lookup"><span data-stu-id="4c93c-105">Now, if you want tooadd subsequent VMs tooyour lab, you can also choose a *base* that is either a [custom image](devtest-lab-create-template.md) or a [formula](devtest-lab-manage-formulas.md).</span></span> <span data-ttu-id="4c93c-106">本教學課程會引導您使用 Azure 入口網站 tooadd VM tooa 實驗室 hello DevTest 實驗室中。</span><span class="sxs-lookup"><span data-stu-id="4c93c-106">This tutorial walks you through using hello Azure portal tooadd a VM tooa lab in DevTest Labs.</span></span>

<span data-ttu-id="4c93c-107">本文也會顯示如何 toomanage hello 成品您的實驗室中的 VM。</span><span class="sxs-lookup"><span data-stu-id="4c93c-107">This article also shows you how toomanage hello artifacts for a VM in your lab.</span></span>

## <a name="steps-tooadd-a-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="4c93c-108">步驟 tooadd VM tooa 實驗室中 Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4c93c-108">Steps tooadd a VM tooa lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="4c93c-109">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="4c93c-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="4c93c-110">選取**更服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="4c93c-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="4c93c-111">從 hello 清單的實驗室中，選取您想在其中 toocreate hello VM hello 實驗室。</span><span class="sxs-lookup"><span data-stu-id="4c93c-111">From hello list of labs, select hello lab in which you want toocreate hello VM.</span></span>  
1. <span data-ttu-id="4c93c-112">在 hello 實驗室**概觀**刀鋒視窗中，選取**+ 加**。</span><span class="sxs-lookup"><span data-stu-id="4c93c-112">On hello lab's **Overview** blade, select **+ Add**.</span></span>  

    ![加入 VM 按鈕](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="4c93c-114">在 hello**選擇基底**刀鋒視窗中，選取一個 hello VM 的基底。</span><span class="sxs-lookup"><span data-stu-id="4c93c-114">On hello **Choose a base** blade, select a base for hello VM.</span></span>
1. <span data-ttu-id="4c93c-115">在 hello**虛擬機器**刀鋒視窗中，輸入 hello 新的虛擬機器的名稱在 hello**虛擬機器名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="4c93c-115">On hello **Virtual machine** blade, enter a name for hello new virtual machine in hello **Virtual machine name** text box.</span></span>

    ![實驗室 VM 刀鋒視窗](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="4c93c-117">輸入**使用者名**，授與 hello 虛擬機器上的系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="4c93c-117">Enter a **User Name** that is granted administrator privileges on hello virtual machine.</span></span>  
1. <span data-ttu-id="4c93c-118">如果您想要 toouse 密碼儲存在您[密碼存放區](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)，選取**使用已儲存的密碼**，並指定一個索引鍵的值，對應 tooyour 秘密 （密碼）。</span><span class="sxs-lookup"><span data-stu-id="4c93c-118">If you want toouse a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds tooyour secret (password).</span></span> <span data-ttu-id="4c93c-119">否則，標示為的 hello 文字欄位中輸入密碼**輸入值**。</span><span class="sxs-lookup"><span data-stu-id="4c93c-119">Otherwise, enter a password in hello text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="4c93c-120">hello**虛擬機器磁碟類型**會決定哪些儲存磁碟類型可供 hello hello 實驗室中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4c93c-120">hello **Virtual machine disk type** determines which storage disk type is allowed for hello virtual machines in hello lab.</span></span>
1. <span data-ttu-id="4c93c-121">選取**虛擬機器大小**和選取 hello 的其中一個預先定義的指定 hello 處理器核心、 RAM 大小，以及 hello VM toocreate hello 硬碟大小的項目。</span><span class="sxs-lookup"><span data-stu-id="4c93c-121">Select **Virtual machine size** and select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span>
1. <span data-ttu-id="4c93c-122">選取**成品**和-從成品-hello 清單選取，然後設定您想 tooadd toohello 基底映像的 hello 成品。</span><span class="sxs-lookup"><span data-stu-id="4c93c-122">Select **Artifacts** and - from hello list of artifacts - select and configure hello artifacts that you want tooadd toohello base image.</span></span>
    <span data-ttu-id="4c93c-123">**注意：**若您是新 tooDevTest 實驗室或設定成品，請參閱 toohello[加入現有的成品 tooa VM](#add-an-existing-artifact-to-a-vm)區段，然後再在完成時，返回此處。</span><span class="sxs-lookup"><span data-stu-id="4c93c-123">**Note:** If you're new tooDevTest Labs or configuring artifacts, refer toohello [Add an existing artifact tooa VM](#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="4c93c-124">選取**進階設定**tooconfigure hello VM 的網路選項和到期選項。</span><span class="sxs-lookup"><span data-stu-id="4c93c-124">Select **Advanced settings** tooconfigure hello VM's network options and expiration options.</span></span> 

   <span data-ttu-id="4c93c-125">tooset 到期選項，選擇 hello 行事曆圖示 toospecify 日期所在 hello VM 將會自動刪除。</span><span class="sxs-lookup"><span data-stu-id="4c93c-125">tooset an expiration option, choose hello calendar icon toospecify a date on which hello VM will be automatically deleted.</span></span>  <span data-ttu-id="4c93c-126">根據預設，永遠不會過期 hello VM。</span><span class="sxs-lookup"><span data-stu-id="4c93c-126">By default, hello VM will never expire.</span></span> 
1. <span data-ttu-id="4c93c-127">如果您想 tooview，或複製 hello Azure 資源管理員範本，請參閱 toohello[儲存 Azure Resource Manager 範本](#save-azure-resource-manager-template)區段，然後完成時，請回到這裡。</span><span class="sxs-lookup"><span data-stu-id="4c93c-127">If you want tooview or copy hello Azure Resource Manager template, refer toohello [Save Azure Resource Manager template](#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="4c93c-128">選取**建立**tooadd hello 指定 VM toohello 實驗室。</span><span class="sxs-lookup"><span data-stu-id="4c93c-128">Select **Create** tooadd hello specified VM toohello lab.</span></span>
1. <span data-ttu-id="4c93c-129">hello 實驗室刀鋒視窗會顯示 hello 狀態的 hello VM 建立-第一次為**建立**，然後為**執行**之後 hello VM 已啟動。</span><span class="sxs-lookup"><span data-stu-id="4c93c-129">hello lab blade displays hello status of hello VM's creation - first as **Creating**, then as **Running** after hello VM has been started.</span></span>

> [!NOTE]
> <span data-ttu-id="4c93c-130">[新增 claimable VM](devtest-lab-add-claimable-vm.md)顯示 toomake 如何 hello claimable VM，使其可供使用 hello 實驗室中的任何使用者。</span><span class="sxs-lookup"><span data-stu-id="4c93c-130">[Add a claimable VM](devtest-lab-add-claimable-vm.md) shows you how toomake hello VM claimable so that it is available for use by any user in hello lab.</span></span>
>
>

## <a name="add-an-existing-artifact-tooa-vm"></a><span data-ttu-id="4c93c-131">加入現有的成品 tooa VM</span><span class="sxs-lookup"><span data-stu-id="4c93c-131">Add an existing artifact tooa VM</span></span>
<span data-ttu-id="4c93c-132">建立 VM 時，您可以加入現有的構件。</span><span class="sxs-lookup"><span data-stu-id="4c93c-132">While creating a VM, you can add existing artifacts.</span></span> <span data-ttu-id="4c93c-133">每個實驗室包括了 hello 公用 DevTest 實驗室成品儲存機制的成品以及成品，您已建立和加入的 tooyour 擁有成品儲存機制。</span><span class="sxs-lookup"><span data-stu-id="4c93c-133">Each lab includes artifacts from hello Public DevTest Labs Artifact Repository as well as artifacts that you've created and added tooyour own Artifact Repository.</span></span>

* <span data-ttu-id="4c93c-134">Azure 的 DevTest Labs*成品*可讓您指定*動作*hello VM 已佈建時，例如執行 Windows PowerShell 指令碼、 執行 Bash 指令和安裝軟體會執行。</span><span class="sxs-lookup"><span data-stu-id="4c93c-134">Azure DevTest Labs *artifacts* let you specify *actions* that are performed when hello VM is provisioned, such as running Windows PowerShell scripts, running Bash commands, and installing software.</span></span>
* <span data-ttu-id="4c93c-135">成品*參數*可讓您自訂您的特定案例的 hello 成品</span><span class="sxs-lookup"><span data-stu-id="4c93c-135">Artifact *parameters* let you customize hello artifact for your particular scenario</span></span>

<span data-ttu-id="4c93c-136">如何 toocreate 成品，請參閱的 toodiscover hello 文件：[深入了解如何 tooauthor 您自己的成品以利使用的 DevTest Labs](devtest-lab-artifact-author.md)。</span><span class="sxs-lookup"><span data-stu-id="4c93c-136">toodiscover how toocreate artifacts, see hello article, [Learn how tooauthor your own artifacts for use with DevTest Labs](devtest-lab-artifact-author.md).</span></span>

1. <span data-ttu-id="4c93c-137">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="4c93c-137">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="4c93c-138">選取**更服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="4c93c-138">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="4c93c-139">從 hello 清單的實驗室中，選取包含您要與其 toowork hello VM hello 實驗室。</span><span class="sxs-lookup"><span data-stu-id="4c93c-139">From hello list of labs, select hello lab containing hello VM with which you want toowork.</span></span>  
1. <span data-ttu-id="4c93c-140">選取 [我的虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="4c93c-140">Select **My virtual machines**.</span></span>
1. <span data-ttu-id="4c93c-141">選取 hello 所需的 VM。</span><span class="sxs-lookup"><span data-stu-id="4c93c-141">Select hello desired VM.</span></span>
1. <span data-ttu-id="4c93c-142">選取 [構件]。</span><span class="sxs-lookup"><span data-stu-id="4c93c-142">Select **Artifacts**.</span></span> 
1. <span data-ttu-id="4c93c-143">選取 [套用構件]。</span><span class="sxs-lookup"><span data-stu-id="4c93c-143">Select **Apply artifacts**.</span></span>
1. <span data-ttu-id="4c93c-144">在 hello**套用成品**刀鋒視窗中，選取 hello 成品想 tooadd toohello VM。</span><span class="sxs-lookup"><span data-stu-id="4c93c-144">On hello **Apply artifacts** blade, select hello artifact you wish tooadd toohello VM.</span></span>
1. <span data-ttu-id="4c93c-145">在 hello**新增成品**刀鋒視窗中，輸入所需的 hello 參數值和任何您需要的選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="4c93c-145">On hello **Add artifact** blade, enter hello required parameter values and any optional parameters that you need.</span></span>  
1. <span data-ttu-id="4c93c-146">選取**新增**tooadd hello 成品，並傳回 toohello**套用成品**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="4c93c-146">Select **Add** tooadd hello artifact and return toohello **Apply artifacts** blade.</span></span>
1. <span data-ttu-id="4c93c-147">視需要繼續為您的 VM 加入構件。</span><span class="sxs-lookup"><span data-stu-id="4c93c-147">Continue adding artifacts as needed for your VM.</span></span>
1. <span data-ttu-id="4c93c-148">一旦您已經加入您的成品，您可以[變更執行哪些 hello 成品的 hello 順序](#change-the-order-in-which-artifacts-are-run)。</span><span class="sxs-lookup"><span data-stu-id="4c93c-148">Once you've added your artifacts, you can [change hello order in which hello artifacts are run](#change-the-order-in-which-artifacts-are-run).</span></span> <span data-ttu-id="4c93c-149">您也可以移回太[檢視或修改成品](#view-or-modify-an-artifact)。</span><span class="sxs-lookup"><span data-stu-id="4c93c-149">You can also go back too[view or modify an artifact](#view-or-modify-an-artifact).</span></span>
1. <span data-ttu-id="4c93c-150">當您新增好構件時，選取 [套用]</span><span class="sxs-lookup"><span data-stu-id="4c93c-150">When you're done adding artifacts, select **Apply**</span></span>

## <a name="change-hello-order-in-which-artifacts-are-run"></a><span data-ttu-id="4c93c-151">變更成品所執行的 hello 順序</span><span class="sxs-lookup"><span data-stu-id="4c93c-151">Change hello order in which artifacts are run</span></span>
<span data-ttu-id="4c93c-152">根據預設，會執行的 hello 成品的 hello 動作 hello 順序就加入 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="4c93c-152">By default, hello actions of hello artifacts are executed in hello order in which they are added toohello VM.</span></span> <span data-ttu-id="4c93c-153">hello 下列步驟說明如何 toochange hello 的 hello 成品執行的順序。</span><span class="sxs-lookup"><span data-stu-id="4c93c-153">hello following steps illustrate how toochange hello order in which hello artifacts are run.</span></span>

1. <span data-ttu-id="4c93c-154">頂端的 hello hello**套用成品**刀鋒視窗中，選取 hello 連結表示 hello toohello VM 已加入的成品數目。</span><span class="sxs-lookup"><span data-stu-id="4c93c-154">At hello top of hello **Apply artifacts** blade, select hello link indicating hello number of artifacts that have been added toohello VM.</span></span>
   
    ![加入 tooVM 數量的成品。](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. <span data-ttu-id="4c93c-156">在 hello**選取成品**hello 刀鋒視窗，拖曳和卸除 hello 成品所需的順序。</span><span class="sxs-lookup"><span data-stu-id="4c93c-156">On hello **Selected artifacts** blade, drag and drop hello artifacts into hello desired order.</span></span> <span data-ttu-id="4c93c-157">**注意：**如果您無法將拖曳 hello 成品，請確定您正在從 hello hello 成品的左方拖曳。</span><span class="sxs-lookup"><span data-stu-id="4c93c-157">**Note:** If you have trouble dragging hello artifact, make sure that you are dragging from hello left side of hello artifact.</span></span> 
1. <span data-ttu-id="4c93c-158">完成時選取 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="4c93c-158">Select **OK** when done.</span></span>  

## <a name="view-or-modify-an-artifact"></a><span data-ttu-id="4c93c-159">檢視或修改構件</span><span class="sxs-lookup"><span data-stu-id="4c93c-159">View or modify an artifact</span></span>
<span data-ttu-id="4c93c-160">hello 下列步驟說明如何 tooview 或修改成品的 hello 參數：</span><span class="sxs-lookup"><span data-stu-id="4c93c-160">hello following steps illustrate how tooview or modify hello parameters of an artifact:</span></span>

1. <span data-ttu-id="4c93c-161">頂端的 hello hello**套用成品**刀鋒視窗中，選取 hello 連結表示 hello toohello VM 已加入的成品數目。</span><span class="sxs-lookup"><span data-stu-id="4c93c-161">At hello top of hello **Apply artifacts** blade, select hello link indicating hello number of artifacts that have been added toohello VM.</span></span>
   
    ![加入 tooVM 數量的成品。](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. <span data-ttu-id="4c93c-163">在 hello**選取成品**刀鋒視窗中，您想 tooview 或編輯選取的 hello 成品。</span><span class="sxs-lookup"><span data-stu-id="4c93c-163">On hello **Selected artifacts** blade, select hello artifact that you want tooview or edit.</span></span>  
1. <span data-ttu-id="4c93c-164">在 hello**新增成品**刀鋒視窗中，任何所需的變更，且在選取**確定** tooclose hello**新增成品**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="4c93c-164">On hello **Add artifact** blade, make any needed changes, and select **OK** tooclose hello **Add artifact** blade.</span></span>
1. <span data-ttu-id="4c93c-165">選取**確定**tooclose hello**選取成品**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="4c93c-165">Select **OK** tooclose hello **Selected artifacts** blade.</span></span>

## <a name="save-azure-resource-manager-template"></a><span data-ttu-id="4c93c-166">儲存 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="4c93c-166">Save Azure Resource Manager template</span></span>
<span data-ttu-id="4c93c-167">Azure Resource Manager 範本提供的宣告方式 toodefine 可重複的部署。</span><span class="sxs-lookup"><span data-stu-id="4c93c-167">An Azure Resource Manager template provides a declarative way toodefine a repeatable deployment.</span></span> <span data-ttu-id="4c93c-168">hello 下列步驟說明如何 toosave hello hello VM 正在建立的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="4c93c-168">hello following steps explain how toosave hello Azure Resource Manager template for hello VM being created.</span></span>
<span data-ttu-id="4c93c-169">儲存之後，您也可以使用 hello Azure Resource Manager 範本[部署新的 Vm，使用 Azure PowerShell](../azure-resource-manager/resource-group-overview.md#template-deployment)。</span><span class="sxs-lookup"><span data-stu-id="4c93c-169">Once saved, you can use hello Azure Resource Manager template too[deploy new VMs with Azure PowerShell](../azure-resource-manager/resource-group-overview.md#template-deployment).</span></span>

1. <span data-ttu-id="4c93c-170">在 hello**虛擬機器**刀鋒視窗中，選取**檢視 ARM 範本**。</span><span class="sxs-lookup"><span data-stu-id="4c93c-170">On hello **Virtual machine** blade, select **View ARM Template**.</span></span>
2. <span data-ttu-id="4c93c-171">在 hello**檢視 Azure Resource Manager 範本**刀鋒視窗中，選取 hello 範本文字。</span><span class="sxs-lookup"><span data-stu-id="4c93c-171">On hello **View Azure Resource Manager template** blade, select hello template text.</span></span>
3. <span data-ttu-id="4c93c-172">將複製 hello 選取的文字 toohello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="4c93c-172">Copy hello selected text toohello clipboard.</span></span>
4. <span data-ttu-id="4c93c-173">選取**確定**tooclose hello**刀鋒視窗中檢視 Azure Resource Manager 範本**。</span><span class="sxs-lookup"><span data-stu-id="4c93c-173">Select **OK** tooclose hello **View Azure Resource Manager Template blade**.</span></span>
5. <span data-ttu-id="4c93c-174">開啟文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="4c93c-174">Open a text editor.</span></span>
6. <span data-ttu-id="4c93c-175">在 hello 剪貼簿中的 hello 範本文字中貼上。</span><span class="sxs-lookup"><span data-stu-id="4c93c-175">Paste in hello template text from hello clipboard.</span></span>
7. <span data-ttu-id="4c93c-176">儲存 hello 檔案供日後使用。</span><span class="sxs-lookup"><span data-stu-id="4c93c-176">Save hello file for later use.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="4c93c-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4c93c-177">Next steps</span></span>
* <span data-ttu-id="4c93c-178">一次 hello 在建立 VM，您可以連接 toohello VM 選取**連接**hello VM 刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="4c93c-178">Once hello VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="4c93c-179">了解如何太[DevTest Labs vm 建立自訂的成品](devtest-lab-artifact-author.md)。</span><span class="sxs-lookup"><span data-stu-id="4c93c-179">Learn how too[create custom artifacts for your DevTest Labs VM](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="4c93c-180">瀏覽 hello [DevTest Labs Azure 資源管理員的快速入門範本庫](https://github.com/Azure/azure-devtestlab/tree/master/Samples)。</span><span class="sxs-lookup"><span data-stu-id="4c93c-180">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
