---
title: "管理 Azure DevTest Labs 中的公式來建立 VM | Microsoft Docs"
description: "了解如何更新和移除 Azure DevTest Labs 公式"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfdab5def50158f9b764bbb1e50c2624cc6d5fb3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a><span data-ttu-id="8feb0-103">管理 Azure DevTest Labs 公式</span><span class="sxs-lookup"><span data-stu-id="8feb0-103">Manage Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="8feb0-104">本文說明如何從基礎 (自訂映像、Marketplace 映像或另一個公式) 或現有的 VM 建立公式。</span><span class="sxs-lookup"><span data-stu-id="8feb0-104">This article illustrates how to create a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span></span> <span data-ttu-id="8feb0-105">本文也會引導您管理現有公式。</span><span class="sxs-lookup"><span data-stu-id="8feb0-105">This article also guides you through managing existing formulas.</span></span>

## <a name="create-a-formula"></a><span data-ttu-id="8feb0-106">建立公式</span><span class="sxs-lookup"><span data-stu-id="8feb0-106">Create a formula</span></span>
<span data-ttu-id="8feb0-107">具有 DevTest Labs「使用者」  權限的所有使用者，都可以使用公式作為基底來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="8feb0-107">Anyone with DevTest Labs *Users* permissions is able to create VMs using a formula as a base.</span></span> <span data-ttu-id="8feb0-108">有兩種方式可以建立公式：</span><span class="sxs-lookup"><span data-stu-id="8feb0-108">There are two ways to create formulas:</span></span> 

* <span data-ttu-id="8feb0-109">從基底開始 - 在您想要定義公式的所有特性時使用。</span><span class="sxs-lookup"><span data-stu-id="8feb0-109">From a base - Use when you want to define all the characteristics of the formula.</span></span>
* <span data-ttu-id="8feb0-110">從現有實驗室 VM - 在您想要根據現有 VM 的設定建立公式時使用。</span><span class="sxs-lookup"><span data-stu-id="8feb0-110">From an existing lab VM - Use when you want to create a formula based on the settings of an existing VM.</span></span>

<span data-ttu-id="8feb0-111">如需有關新增使用者和權限的詳細資訊，請參閱[在 Azure DevTest Labs 中新增擁有者和使用者](./devtest-lab-add-devtest-user.md)。</span><span class="sxs-lookup"><span data-stu-id="8feb0-111">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span></span>

### <a name="create-a-formula-from-a-base"></a><span data-ttu-id="8feb0-112">從基底建立公式</span><span class="sxs-lookup"><span data-stu-id="8feb0-112">Create a formula from a base</span></span>
<span data-ttu-id="8feb0-113">下列步驟會引導您完成從自訂映像、Marketplace 映像或其他公式建立公式的程序。</span><span class="sxs-lookup"><span data-stu-id="8feb0-113">The following steps guide you through the process of creating a formula from a custom image, Marketplace image, or another formula.</span></span>

1. <span data-ttu-id="8feb0-114">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="8feb0-114">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

2. <span data-ttu-id="8feb0-115">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="8feb0-115">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>

3. <span data-ttu-id="8feb0-116">從實驗室清單中，選取所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="8feb0-116">From the list of labs, select the desired lab.</span></span>  

4. <span data-ttu-id="8feb0-117">在實驗室的刀鋒視窗上，選取 [公式 (可重複使用的基底)] 。</span><span class="sxs-lookup"><span data-stu-id="8feb0-117">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![公式功能表](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. <span data-ttu-id="8feb0-119">在 [公式] 刀鋒視窗上，選取 [+新增]。</span><span class="sxs-lookup"><span data-stu-id="8feb0-119">On the **Formulas** blade, select **+ Add**.</span></span>
   
    ![加入公式](./media/devtest-lab-create-formulas/add-formula.png)

6. <span data-ttu-id="8feb0-121">在 [選擇基底]  刀鋒視窗上，選取您想要用來建立公式的基底 (自訂映像、Marketplace 映像或公式)。</span><span class="sxs-lookup"><span data-stu-id="8feb0-121">On the **Choose a base** blade, select the base (custom image, Marketplace image, or formula) from which you want to create the formula.</span></span>
   
    ![基本清單](./media/devtest-lab-create-formulas/base-list.png)

7. <span data-ttu-id="8feb0-123">在 [建立公式]  刀鋒視窗上，指定下列值：</span><span class="sxs-lookup"><span data-stu-id="8feb0-123">On the **Create formula** blade, specify the following values:</span></span>
   
    * <span data-ttu-id="8feb0-124">**公式名稱** - 輸入公式的名稱。</span><span class="sxs-lookup"><span data-stu-id="8feb0-124">**Formula name** - Enter a name for your formula.</span></span> <span data-ttu-id="8feb0-125">當您建立 VM 時，這個值會在顯示在基本映像清單中。</span><span class="sxs-lookup"><span data-stu-id="8feb0-125">This value is displayed in the list of base images when you create a VM.</span></span> <span data-ttu-id="8feb0-126">輸入名稱時會立即驗證，如果無效，則會出現訊息指出有效名稱的需求。</span><span class="sxs-lookup"><span data-stu-id="8feb0-126">The name is validated as you type it, and if not valid, a message indicates the requirements for a valid name.</span></span>
    * <span data-ttu-id="8feb0-127">**描述** - 輸入公式的有意義描述。</span><span class="sxs-lookup"><span data-stu-id="8feb0-127">**Description** - Enter a meaningful description for your formula.</span></span> <span data-ttu-id="8feb0-128">當您建立 VM 時，可以從公式的操作功能表使用這個值。</span><span class="sxs-lookup"><span data-stu-id="8feb0-128">This value is available from the formula's context menu when you create a VM.</span></span>
    * <span data-ttu-id="8feb0-129">**使用者名稱** - 輸入被授與系統管理員權限的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="8feb0-129">**User name** - Enter a user name that is granted administrator privileges.</span></span>
    * <span data-ttu-id="8feb0-130">**密碼** - 從下拉式清單中輸入或選取一個值，該值與您想用於指定使用者的密碼相關聯。</span><span class="sxs-lookup"><span data-stu-id="8feb0-130">**Password** - Enter - or select from the dropdown - a value that is associated with the secret (password) that you want to use for the specified user.</span></span> <span data-ttu-id="8feb0-131">如需密碼的詳細資訊，請參閱 [Azure DevTest Labs︰個人密碼存放區](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/)。</span><span class="sxs-lookup"><span data-stu-id="8feb0-131">For more information about the secrets, see [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span></span>
    * <span data-ttu-id="8feb0-132">**虛擬機器磁碟類型** - 指定 HDD (硬碟) 或 SSD (固態硬碟)，以表示使用此基本映像佈建的虛擬機器可使用哪種儲存磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="8feb0-132">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) to indicate which storage disk type is allowed for the virtual machines provisioned using this base image.</span></span>
    * <span data-ttu-id="8feb0-133">**虛擬機器大小** - 選取其中一個預先定義的項目，以指定要建立之 VM 的處理器核心、RAM 大小和硬碟大小。</span><span class="sxs-lookup"><span data-stu-id="8feb0-133">** Virtual machine size** - Select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span> 
    * <span data-ttu-id="8feb0-134">**構件** - 選取以開啟 [新增構件] 刀鋒視窗，以選取並設定您想要新增至基本映像的構件。</span><span class="sxs-lookup"><span data-stu-id="8feb0-134">**Artifacts** - Select to open the **Add artifacts** blade, in which you select and configure the artifacts that you want to add to the base image.</span></span> <span data-ttu-id="8feb0-135">如需構件的詳細資訊，請參閱[在 Azure DevTest Labs 中管理 VM 構件](./devtest-lab-add-vm-with-artifacts.md)。</span><span class="sxs-lookup"><span data-stu-id="8feb0-135">For more information about artifacts, see [Manage VM artifacts in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span></span>
    * <span data-ttu-id="8feb0-136">**進階設定** - 選取以開啟 [進階] 刀鋒視窗，以進行下列設定︰</span><span class="sxs-lookup"><span data-stu-id="8feb0-136">**Advanced settings** - Select to open the **Advanced** blade where you configure the following settings:</span></span>
        * <span data-ttu-id="8feb0-137">**虛擬網路** - 指定所需的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="8feb0-137">**Virtual network** - Specify the desired virtual network.</span></span>
        * <span data-ttu-id="8feb0-138">**子網路** - 指定所需的子網路。</span><span class="sxs-lookup"><span data-stu-id="8feb0-138">**Subnet** - Specify the desired subnet.</span></span>    
        * <span data-ttu-id="8feb0-139">**IP 位址組態** - 指定您想要公用、私人或共用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8feb0-139">**IP address configuration** - Specify if you want the Public, Private, or Shared IP addresses.</span></span> <span data-ttu-id="8feb0-140">如需共用 IP 位址的詳細資訊，請參閱[了解 Azure DevTest Labs 中的共用 IP 位址](./devtest-lab-shared-ip.md)。</span><span class="sxs-lookup"><span data-stu-id="8feb0-140">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span></span>
        * <span data-ttu-id="8feb0-141">**允許宣告此機器** -「允許宣告」機器表示建立機器時不會指派擁有權。</span><span class="sxs-lookup"><span data-stu-id="8feb0-141">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at the time of creation.</span></span> <span data-ttu-id="8feb0-142">實驗室使用者將能夠在實驗室的刀鋒視窗中，取得 (「宣告」) 機器的擁有權。</span><span class="sxs-lookup"><span data-stu-id="8feb0-142">Instead lab users will be able to take ownership ("claim") the machine in the lab's blade.</span></span>     
    * <span data-ttu-id="8feb0-143">**映像** - 這個欄位會顯示您在前一個刀鋒視窗上選取的基本映像名稱。</span><span class="sxs-lookup"><span data-stu-id="8feb0-143">**Image** - This field displays name of the base image you selected on the previous blade.</span></span> 
     
       ![建立公式](./media/devtest-lab-create-formulas/create-formula.png)

8. <span data-ttu-id="8feb0-145">選取 [建立]  以建立公式。</span><span class="sxs-lookup"><span data-stu-id="8feb0-145">Select **Create** to create the formula.</span></span>

9. <span data-ttu-id="8feb0-146">公式建立之後會顯示在 [公式] 刀鋒視窗的清單中。</span><span class="sxs-lookup"><span data-stu-id="8feb0-146">When the formula has been created, it displays in the list on the **Formulas** blade.</span></span>

### <a name="create-a-formula-from-a-vm"></a><span data-ttu-id="8feb0-147">從 VM 建立公式</span><span class="sxs-lookup"><span data-stu-id="8feb0-147">Create a formula from a VM</span></span>
<span data-ttu-id="8feb0-148">下列步驟會引導您完成根據現有 VM 建立公式的程序。</span><span class="sxs-lookup"><span data-stu-id="8feb0-148">The following steps guide you through the process of creating a formula based on an existing VM.</span></span> 

> [!NOTE]
> <span data-ttu-id="8feb0-149">VM 必須是在 2016 年 3 月 30 日以後建立的，才能從該 VM 建立公式。</span><span class="sxs-lookup"><span data-stu-id="8feb0-149">To create a formula from a VM, the VM must have been created after March 30, 2016.</span></span> 
> 
> 

1. <span data-ttu-id="8feb0-150">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="8feb0-150">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="8feb0-151">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="8feb0-151">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="8feb0-152">從實驗室清單中，選取所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="8feb0-152">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="8feb0-153">在實驗室的 [概觀]  刀鋒視窗中，選取要從中建立公式的 VM。</span><span class="sxs-lookup"><span data-stu-id="8feb0-153">On the lab's **Overview** blade, select the VM from which you wish to create the formula.</span></span>
   
    ![實驗室 VM](./media/devtest-lab-create-formulas/my-vms.png)
5. <span data-ttu-id="8feb0-155">在 VM 的刀鋒視窗上，選取 [建立公式 (可重複使用的基底)] 。</span><span class="sxs-lookup"><span data-stu-id="8feb0-155">On the VM's blade, select **Create formula (reusable base)**.</span></span>
   
    ![建立公式](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. <span data-ttu-id="8feb0-157">在 [建立公式] 刀鋒視窗上，輸入新公式的 [名稱] 和 [描述]。</span><span class="sxs-lookup"><span data-stu-id="8feb0-157">On the **Create formula** blade, enter a **Name** and **Description** for your new formula.</span></span>
   
    ![建立公式刀鋒視窗](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. <span data-ttu-id="8feb0-159">選取 [確定]  以建立公式。</span><span class="sxs-lookup"><span data-stu-id="8feb0-159">Select **OK** to create the formula.</span></span>

## <a name="modify-a-formula"></a><span data-ttu-id="8feb0-160">修改公式</span><span class="sxs-lookup"><span data-stu-id="8feb0-160">Modify a formula</span></span>
<span data-ttu-id="8feb0-161">若要修改公式，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="8feb0-161">To modify a formula, follow these steps:</span></span>

1. <span data-ttu-id="8feb0-162">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="8feb0-162">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="8feb0-163">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="8feb0-163">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="8feb0-164">從實驗室清單中，選取所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="8feb0-164">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="8feb0-165">在實驗室的刀鋒視窗上，選取 [公式 (可重複使用的基底)] 。</span><span class="sxs-lookup"><span data-stu-id="8feb0-165">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![公式功能表](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="8feb0-167">在 [Lab formulas] \(實驗室公式)  刀鋒視窗上，選取您想要修改的公式。</span><span class="sxs-lookup"><span data-stu-id="8feb0-167">On the **Lab formulas** blade, select the formula you wish to modify.</span></span>
6. <span data-ttu-id="8feb0-168">在 [更新公式] 刀鋒視窗上，進行所需的編輯，然後選取 [更新]。</span><span class="sxs-lookup"><span data-stu-id="8feb0-168">On the **Update formula** blade, make the desired edits, and select **Update**.</span></span>

## <a name="delete-a-formula"></a><span data-ttu-id="8feb0-169">刪除公式</span><span class="sxs-lookup"><span data-stu-id="8feb0-169">Delete a formula</span></span>
<span data-ttu-id="8feb0-170">若要刪除公式，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="8feb0-170">To delete a formula, follow these steps:</span></span>

1. <span data-ttu-id="8feb0-171">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="8feb0-171">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="8feb0-172">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="8feb0-172">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="8feb0-173">從實驗室清單中，選取所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="8feb0-173">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="8feb0-174">在實驗室的 [設定] 刀鋒視窗上，選取 [公式]。</span><span class="sxs-lookup"><span data-stu-id="8feb0-174">On the lab **Settings** blade, select **Formulas**.</span></span>
   
    ![公式功能表](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="8feb0-176">在 [Lab formulas] \(實驗室公式)  刀鋒視窗上，選取您想要刪除之公式右邊的省略符號。</span><span class="sxs-lookup"><span data-stu-id="8feb0-176">On the **Lab formulas** blade, select the ellipsis to the right of the formula you wish to delete.</span></span>
   
    ![公式功能表](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. <span data-ttu-id="8feb0-178">在公式的操作功能表上，選取 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="8feb0-178">On the formula's context menu, select **Delete**.</span></span>
   
    ![公式操作功能表](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. <span data-ttu-id="8feb0-180">在刪除確認對話方塊上，選取 [是]  。</span><span class="sxs-lookup"><span data-stu-id="8feb0-180">Select **Yes** to the deletion confirmation dialog.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="8feb0-181">相關部落格文章</span><span class="sxs-lookup"><span data-stu-id="8feb0-181">Related blog posts</span></span>
* [<span data-ttu-id="8feb0-182">自訂映像或公式？</span><span class="sxs-lookup"><span data-stu-id="8feb0-182">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="8feb0-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8feb0-183">Next steps</span></span>
<span data-ttu-id="8feb0-184">建立要在建立 VM 時使用的公式之後，下一個步驟就是[將 VM 新增實驗室](devtest-lab-add-vm-with-artifacts.md)。</span><span class="sxs-lookup"><span data-stu-id="8feb0-184">Once you have created a formula for use when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

