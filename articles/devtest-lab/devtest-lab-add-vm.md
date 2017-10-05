---
title: "在 Azure DevTest Labs 中對實驗室新增 VM | Microsoft Docs"
description: "了解如何在 Azure DevTest Labs 中對實驗室新增虛擬機器"
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
ms.openlocfilehash: 449bffb040dafc8edd0b8b0afd80dbea35cd28ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="87284-103">在 Azure DevTest Labs 中對實驗室新增 VM</span><span class="sxs-lookup"><span data-stu-id="87284-103">Add a VM to a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="87284-104">如果您已經[建立您的第一個 VM](devtest-lab-create-first-vm.md)，您很有可能是透過預先載入的 [Marketplace 映像](devtest-lab-configure-marketplace-images.md)來完成的。</span><span class="sxs-lookup"><span data-stu-id="87284-104">If you have already [created your first VM](devtest-lab-create-first-vm.md), you likely did so from a pre-loaded [marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="87284-105">現在，如果您想要將後續的 VM 新增至您的實驗室，您也可以選擇一個「基底」，它可以是[自訂映像](devtest-lab-create-template.md)或[公式](devtest-lab-manage-formulas.md)。</span><span class="sxs-lookup"><span data-stu-id="87284-105">Now, if you want to add subsequent VMs to your lab, you can also choose a *base* that is either a [custom image](devtest-lab-create-template.md) or a [formula](devtest-lab-manage-formulas.md).</span></span> <span data-ttu-id="87284-106">本教學課程會逐步引導您使用 Azure 入口網站，在 DevTest Labs 中對實驗室新增 VM。</span><span class="sxs-lookup"><span data-stu-id="87284-106">This tutorial walks you through using the Azure portal to add a VM to a lab in DevTest Labs.</span></span>

<span data-ttu-id="87284-107">本文同時說明如何在實驗室中管理 VM 的構件。</span><span class="sxs-lookup"><span data-stu-id="87284-107">This article also shows you how to manage the artifacts for a VM in your lab.</span></span>

## <a name="steps-to-add-a-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="87284-108">在 Azure DevTest Labs 中對實驗室新增 VM 的步驟</span><span class="sxs-lookup"><span data-stu-id="87284-108">Steps to add a VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="87284-109">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="87284-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="87284-110">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="87284-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="87284-111">從實驗室清單中，選取您想要在其中建立 VM 的實驗室。</span><span class="sxs-lookup"><span data-stu-id="87284-111">From the list of labs, select the lab in which you want to create the VM.</span></span>  
1. <span data-ttu-id="87284-112">在實驗室的 [概觀] 刀鋒視窗中，選取 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="87284-112">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![加入 VM 按鈕](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="87284-114">在 [選擇基底]  刀鋒視窗中，選取 VM 的基底。</span><span class="sxs-lookup"><span data-stu-id="87284-114">On the **Choose a base** blade, select a base for the VM.</span></span>
1. <span data-ttu-id="87284-115">在 [虛擬機器] 刀鋒視窗的 [虛擬機器名稱] 文字方塊中，輸入新虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="87284-115">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![實驗室 VM 刀鋒視窗](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="87284-117">輸入**使用者名稱**，此名稱會被授與虛擬機器上的系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="87284-117">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="87284-118">如果您想使用儲存在[密碼存放區](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)中的密碼，請選取 [使用儲存的密碼]，並指定與密碼對應的金鑰值。</span><span class="sxs-lookup"><span data-stu-id="87284-118">If you want to use a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds to your secret (password).</span></span> <span data-ttu-id="87284-119">否則，請在標示為 [輸入值] 的文字欄位中輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="87284-119">Otherwise, enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="87284-120">[虛擬機器磁碟類型] 會決定實驗室中的虛擬機器所允許的儲存磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="87284-120">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="87284-121">選取 [虛擬機器大小]  ，然後選取其中一個預先定義的項目，這些項目可以指定處理器核心、RAM 大小，以及要建立的 VM 的硬碟大小。</span><span class="sxs-lookup"><span data-stu-id="87284-121">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="87284-122">選取 [構件]，然後從構件清單中，選取並設定您想要新增到基本映像中的構件。</span><span class="sxs-lookup"><span data-stu-id="87284-122">Select **Artifacts** and - from the list of artifacts - select and configure the artifacts that you want to add to the base image.</span></span>
    <span data-ttu-id="87284-123">**附註：**如果您對 DevTest Labs 或設定構件並不熟悉，請參閱[將現有的構件加入至 VM](#add-an-existing-artifact-to-a-vm) 一節，完成該節之後再返回此處。</span><span class="sxs-lookup"><span data-stu-id="87284-123">**Note:** If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="87284-124">選取 [進階設定] 以設定 VM 的網路選項和到期日選項。</span><span class="sxs-lookup"><span data-stu-id="87284-124">Select **Advanced settings** to configure the VM's network options and expiration options.</span></span> 

   <span data-ttu-id="87284-125">若要設定到期選項，選擇行事曆圖示，以指定 VM 將會自動刪除的日期。</span><span class="sxs-lookup"><span data-stu-id="87284-125">To set an expiration option, choose the calendar icon to specify a date on which the VM will be automatically deleted.</span></span>  <span data-ttu-id="87284-126">根據預設，VM 永遠不會到期。</span><span class="sxs-lookup"><span data-stu-id="87284-126">By default, the VM will never expire.</span></span> 
1. <span data-ttu-id="87284-127">如果您想要檢視或複製 Azure Resource Manager 範本，請參閱[儲存 Azure Resource Manager 範本](#save-azure-resource-manager-template)一節，然後在完成時回到這裡。</span><span class="sxs-lookup"><span data-stu-id="87284-127">If you want to view or copy the Azure Resource Manager template, refer to the [Save Azure Resource Manager template](#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="87284-128">選取 [建立]  ，將指定的 VM 加入實驗室。</span><span class="sxs-lookup"><span data-stu-id="87284-128">Select **Create** to add the specified VM to the lab.</span></span>
1. <span data-ttu-id="87284-129">實驗室刀鋒視窗會顯示 VM 的建立狀態，其狀態會先是 [正在建立]，在啟動該 VM 之後才會變成 [正在執行]。</span><span class="sxs-lookup"><span data-stu-id="87284-129">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>

> [!NOTE]
> <span data-ttu-id="87284-130">[新增可宣告 VM](devtest-lab-add-claimable-vm.md) 會示範如何允許宣告 VM，使它可供實驗室中的所有使用者使用。</span><span class="sxs-lookup"><span data-stu-id="87284-130">[Add a claimable VM](devtest-lab-add-claimable-vm.md) shows you how to make the VM claimable so that it is available for use by any user in the lab.</span></span>
>
>

## <a name="add-an-existing-artifact-to-a-vm"></a><span data-ttu-id="87284-131">將現有的構件加入至 VM</span><span class="sxs-lookup"><span data-stu-id="87284-131">Add an existing artifact to a VM</span></span>
<span data-ttu-id="87284-132">建立 VM 時，您可以加入現有的構件。</span><span class="sxs-lookup"><span data-stu-id="87284-132">While creating a VM, you can add existing artifacts.</span></span> <span data-ttu-id="87284-133">每個實驗室都會包括來自公用研發/測試實驗室構件儲存機制的構件，以及您已建立並加入至您自己之構件儲存機制的構件。</span><span class="sxs-lookup"><span data-stu-id="87284-133">Each lab includes artifacts from the Public DevTest Labs Artifact Repository as well as artifacts that you've created and added to your own Artifact Repository.</span></span>

* <span data-ttu-id="87284-134">Azure DevTest Labs「構件」可讓您指定會在 VM 佈建時執行的「動作」，例如執行 Windows PowerShell 指令碼、執行 Bash 命令，以及安裝軟體。</span><span class="sxs-lookup"><span data-stu-id="87284-134">Azure DevTest Labs *artifacts* let you specify *actions* that are performed when the VM is provisioned, such as running Windows PowerShell scripts, running Bash commands, and installing software.</span></span>
* <span data-ttu-id="87284-135">構件「參數」可讓您自訂適用於特定案例的構件</span><span class="sxs-lookup"><span data-stu-id="87284-135">Artifact *parameters* let you customize the artifact for your particular scenario</span></span>

<span data-ttu-id="87284-136">若要了解如何建立構件，請參閱 [了解如何撰寫您自己的構件以用於研發/測試實驗室](devtest-lab-artifact-author.md)文章。</span><span class="sxs-lookup"><span data-stu-id="87284-136">To discover how to create artifacts, see the article, [Learn how to author your own artifacts for use with DevTest Labs](devtest-lab-artifact-author.md).</span></span>

1. <span data-ttu-id="87284-137">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="87284-137">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="87284-138">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="87284-138">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="87284-139">從實驗室清單中，選取您想要使用之 VM 所在的實驗室。</span><span class="sxs-lookup"><span data-stu-id="87284-139">From the list of labs, select the lab containing the VM with which you want to work.</span></span>  
1. <span data-ttu-id="87284-140">選取 [我的虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="87284-140">Select **My virtual machines**.</span></span>
1. <span data-ttu-id="87284-141">選取所需的 VM。</span><span class="sxs-lookup"><span data-stu-id="87284-141">Select the desired VM.</span></span>
1. <span data-ttu-id="87284-142">選取 [構件]。</span><span class="sxs-lookup"><span data-stu-id="87284-142">Select **Artifacts**.</span></span> 
1. <span data-ttu-id="87284-143">選取 [套用構件]。</span><span class="sxs-lookup"><span data-stu-id="87284-143">Select **Apply artifacts**.</span></span>
1. <span data-ttu-id="87284-144">在 [套用構件] 刀鋒視窗中，選取您要新增到 VM 的構件。</span><span class="sxs-lookup"><span data-stu-id="87284-144">On the **Apply artifacts** blade, select the artifact you wish to add to the VM.</span></span>
1. <span data-ttu-id="87284-145">在 [新增構件] 刀鋒視窗中，輸入必要的參數值以及任何您所需的選用參數。</span><span class="sxs-lookup"><span data-stu-id="87284-145">On the **Add artifact** blade, enter the required parameter values and any optional parameters that you need.</span></span>  
1. <span data-ttu-id="87284-146">選取 [新增] 以新增構件，然後返回 [套用構件] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="87284-146">Select **Add** to add the artifact and return to the **Apply artifacts** blade.</span></span>
1. <span data-ttu-id="87284-147">視需要繼續為您的 VM 加入構件。</span><span class="sxs-lookup"><span data-stu-id="87284-147">Continue adding artifacts as needed for your VM.</span></span>
1. <span data-ttu-id="87284-148">加入構件之後，您可以 [變更構件的執行順序](#change-the-order-in-which-artifacts-are-run)。</span><span class="sxs-lookup"><span data-stu-id="87284-148">Once you've added your artifacts, you can [change the order in which the artifacts are run](#change-the-order-in-which-artifacts-are-run).</span></span> <span data-ttu-id="87284-149">您也可以返回來 [檢視或修改構件](#view-or-modify-an-artifact)。</span><span class="sxs-lookup"><span data-stu-id="87284-149">You can also go back to [view or modify an artifact](#view-or-modify-an-artifact).</span></span>
1. <span data-ttu-id="87284-150">當您新增好構件時，選取 [套用]</span><span class="sxs-lookup"><span data-stu-id="87284-150">When you're done adding artifacts, select **Apply**</span></span>

## <a name="change-the-order-in-which-artifacts-are-run"></a><span data-ttu-id="87284-151">變更構件的執行順序</span><span class="sxs-lookup"><span data-stu-id="87284-151">Change the order in which artifacts are run</span></span>
<span data-ttu-id="87284-152">根據預設，構件的動作是依照它們加入 VM 的順序來執行。</span><span class="sxs-lookup"><span data-stu-id="87284-152">By default, the actions of the artifacts are executed in the order in which they are added to the VM.</span></span> <span data-ttu-id="87284-153">下列步驟說明如何變更構件的執行順序。</span><span class="sxs-lookup"><span data-stu-id="87284-153">The following steps illustrate how to change the order in which the artifacts are run.</span></span>

1. <span data-ttu-id="87284-154">在 [套用構件] 刀鋒視窗頂端，選取會指出已新增至 VM 之構件數目的連結。</span><span class="sxs-lookup"><span data-stu-id="87284-154">At the top of the **Apply artifacts** blade, select the link indicating the number of artifacts that have been added to the VM.</span></span>
   
    ![新增至 VM 的構件數目](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. <span data-ttu-id="87284-156">在 [選取的構件] 刀鋒視窗中，將構件拖放到所需的順序。</span><span class="sxs-lookup"><span data-stu-id="87284-156">On the **Selected artifacts** blade, drag and drop the artifacts into the desired order.</span></span> <span data-ttu-id="87284-157">**附註︰**如果您在拖曳構件時發生問題，請確定您是從構件左側進行拖曳。</span><span class="sxs-lookup"><span data-stu-id="87284-157">**Note:** If you have trouble dragging the artifact, make sure that you are dragging from the left side of the artifact.</span></span> 
1. <span data-ttu-id="87284-158">完成時選取 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="87284-158">Select **OK** when done.</span></span>  

## <a name="view-or-modify-an-artifact"></a><span data-ttu-id="87284-159">檢視或修改構件</span><span class="sxs-lookup"><span data-stu-id="87284-159">View or modify an artifact</span></span>
<span data-ttu-id="87284-160">下列步驟說明如何檢視或修改構件的參數︰</span><span class="sxs-lookup"><span data-stu-id="87284-160">The following steps illustrate how to view or modify the parameters of an artifact:</span></span>

1. <span data-ttu-id="87284-161">在 [套用構件] 刀鋒視窗頂端，選取會指出已新增至 VM 之構件數目的連結。</span><span class="sxs-lookup"><span data-stu-id="87284-161">At the top of the **Apply artifacts** blade, select the link indicating the number of artifacts that have been added to the VM.</span></span>
   
    ![新增至 VM 的構件數目](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. <span data-ttu-id="87284-163">在 [選取的構件] 刀鋒視窗中，選取您想要檢視或編輯的構件。</span><span class="sxs-lookup"><span data-stu-id="87284-163">On the **Selected artifacts** blade, select the artifact that you want to view or edit.</span></span>  
1. <span data-ttu-id="87284-164">在 [新增構件] 刀鋒視窗中，進行任何所需的變更，然後選取 [確定] 以關閉 [新增構件] 刀鋒視窗 。</span><span class="sxs-lookup"><span data-stu-id="87284-164">On the **Add artifact** blade, make any needed changes, and select **OK** to close the **Add artifact** blade.</span></span>
1. <span data-ttu-id="87284-165">選取 [確定] 以關閉 [選取的構件] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="87284-165">Select **OK** to close the **Selected artifacts** blade.</span></span>

## <a name="save-azure-resource-manager-template"></a><span data-ttu-id="87284-166">儲存 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="87284-166">Save Azure Resource Manager template</span></span>
<span data-ttu-id="87284-167">Azure Resource Manager 範本提供宣告式方法來定義可重複的部署。</span><span class="sxs-lookup"><span data-stu-id="87284-167">An Azure Resource Manager template provides a declarative way to define a repeatable deployment.</span></span> <span data-ttu-id="87284-168">下列步驟說明如何為建立的 VM 儲存 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="87284-168">The following steps explain how to save the Azure Resource Manager template for the VM being created.</span></span>
<span data-ttu-id="87284-169">儲存之後，您便可以使用 Azure Resource Manager 範本[透過 Azure PowerShell 部署新的 VM](../azure-resource-manager/resource-group-overview.md#template-deployment)。</span><span class="sxs-lookup"><span data-stu-id="87284-169">Once saved, you can use the Azure Resource Manager template to [deploy new VMs with Azure PowerShell](../azure-resource-manager/resource-group-overview.md#template-deployment).</span></span>

1. <span data-ttu-id="87284-170">在 [虛擬機器] 刀鋒視窗上，選取 [檢視 ARM 範本]。</span><span class="sxs-lookup"><span data-stu-id="87284-170">On the **Virtual machine** blade, select **View ARM Template**.</span></span>
2. <span data-ttu-id="87284-171">在 [檢視 Azure Resource Manager 範本] 刀鋒視窗中，選取範本文字。</span><span class="sxs-lookup"><span data-stu-id="87284-171">On the **View Azure Resource Manager template** blade, select the template text.</span></span>
3. <span data-ttu-id="87284-172">將選取的文字複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="87284-172">Copy the selected text to the clipboard.</span></span>
4. <span data-ttu-id="87284-173">選取 [確定] 以關閉 [檢視 Azure Resource Manager 範本] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="87284-173">Select **OK** to close the **View Azure Resource Manager Template blade**.</span></span>
5. <span data-ttu-id="87284-174">開啟文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="87284-174">Open a text editor.</span></span>
6. <span data-ttu-id="87284-175">從剪貼簿貼上範本文字。</span><span class="sxs-lookup"><span data-stu-id="87284-175">Paste in the template text from the clipboard.</span></span>
7. <span data-ttu-id="87284-176">儲存檔案供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="87284-176">Save the file for later use.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="87284-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="87284-177">Next steps</span></span>
* <span data-ttu-id="87284-178">一旦建立 VM 之後，您可以選取 VM 刀鋒視窗上的 [連接]  來連接至 VM。</span><span class="sxs-lookup"><span data-stu-id="87284-178">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="87284-179">了解如何 [為您的 DevTest Labs VM 建立自訂構件](devtest-lab-artifact-author.md)。</span><span class="sxs-lookup"><span data-stu-id="87284-179">Learn how to [create custom artifacts for your DevTest Labs VM](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="87284-180">瀏覽 [DevTest Labs Azure Resource Manager 快速入門範本資源庫 (英文)](https://github.com/Azure/azure-devtestlab/tree/master/Samples)。</span><span class="sxs-lookup"><span data-stu-id="87284-180">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
