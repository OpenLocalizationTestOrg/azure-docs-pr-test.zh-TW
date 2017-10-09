---
title: "在 Azure DevTest Labs toocreate Vm aaaManage 公式 |Microsoft 文件"
description: "深入了解如何 tooupdate 及移除 Azure DevTest Labs 公式"
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
ms.openlocfilehash: 855debe46f3b70cc45ea5d55869663b64e225124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a><span data-ttu-id="63c6a-103">管理 Azure DevTest Labs 公式</span><span class="sxs-lookup"><span data-stu-id="63c6a-103">Manage Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="63c6a-104">本文將說明如何 toocreate 基底 （自訂映像、 Marketplace 映像或另一個公式） 或現有 VM 的公式。</span><span class="sxs-lookup"><span data-stu-id="63c6a-104">This article illustrates how toocreate a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span></span> <span data-ttu-id="63c6a-105">本文也會引導您管理現有公式。</span><span class="sxs-lookup"><span data-stu-id="63c6a-105">This article also guides you through managing existing formulas.</span></span>

## <a name="create-a-formula"></a><span data-ttu-id="63c6a-106">建立公式</span><span class="sxs-lookup"><span data-stu-id="63c6a-106">Create a formula</span></span>
<span data-ttu-id="63c6a-107">任何人都 DevTest Labs*使用者*權限是可以 toocreate Vm 做為基底中使用公式。</span><span class="sxs-lookup"><span data-stu-id="63c6a-107">Anyone with DevTest Labs *Users* permissions is able toocreate VMs using a formula as a base.</span></span> <span data-ttu-id="63c6a-108">有兩種方式 toocreate 公式：</span><span class="sxs-lookup"><span data-stu-id="63c6a-108">There are two ways toocreate formulas:</span></span> 

* <span data-ttu-id="63c6a-109">基底-當您想使用 toodefine hello 公式的所有 hello 特性。</span><span class="sxs-lookup"><span data-stu-id="63c6a-109">From a base - Use when you want toodefine all hello characteristics of hello formula.</span></span>
* <span data-ttu-id="63c6a-110">從現有的實驗室 VM-當您想 toocreate 公式時使用 hello 以設定為基礎的現有 VM。</span><span class="sxs-lookup"><span data-stu-id="63c6a-110">From an existing lab VM - Use when you want toocreate a formula based on hello settings of an existing VM.</span></span>

<span data-ttu-id="63c6a-111">如需有關新增使用者和權限的詳細資訊，請參閱[在 Azure DevTest Labs 中新增擁有者和使用者](./devtest-lab-add-devtest-user.md)。</span><span class="sxs-lookup"><span data-stu-id="63c6a-111">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span></span>

### <a name="create-a-formula-from-a-base"></a><span data-ttu-id="63c6a-112">從基底建立公式</span><span class="sxs-lookup"><span data-stu-id="63c6a-112">Create a formula from a base</span></span>
<span data-ttu-id="63c6a-113">hello 步驟會引導您完成建立公式從自訂映像、 Marketplace 映像或另一個公式 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="63c6a-113">hello following steps guide you through hello process of creating a formula from a custom image, Marketplace image, or another formula.</span></span>

1. <span data-ttu-id="63c6a-114">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="63c6a-114">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

2. <span data-ttu-id="63c6a-115">選取**更服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="63c6a-115">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>

3. <span data-ttu-id="63c6a-116">從 hello 清單的實驗室中，選取 hello 所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="63c6a-116">From hello list of labs, select hello desired lab.</span></span>  

4. <span data-ttu-id="63c6a-117">在 hello 實驗室刀鋒視窗中，選取 **公式 （可重複使用基底）**。</span><span class="sxs-lookup"><span data-stu-id="63c6a-117">On hello lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![公式功能表](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. <span data-ttu-id="63c6a-119">在 hello**公式**刀鋒視窗中，選取**+ 加**。</span><span class="sxs-lookup"><span data-stu-id="63c6a-119">On hello **Formulas** blade, select **+ Add**.</span></span>
   
    ![加入公式](./media/devtest-lab-create-formulas/add-formula.png)

6. <span data-ttu-id="63c6a-121">在 hello**選擇基底**刀鋒視窗中，選取 hello 基底 （自訂映像、 Marketplace 映像或公式） 要從中 toocreate hello 公式。</span><span class="sxs-lookup"><span data-stu-id="63c6a-121">On hello **Choose a base** blade, select hello base (custom image, Marketplace image, or formula) from which you want toocreate hello formula.</span></span>
   
    ![基本清單](./media/devtest-lab-create-formulas/base-list.png)

7. <span data-ttu-id="63c6a-123">在 hello**建立公式**刀鋒視窗中，指定下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="63c6a-123">On hello **Create formula** blade, specify hello following values:</span></span>
   
    * <span data-ttu-id="63c6a-124">**公式名稱** - 輸入公式的名稱。</span><span class="sxs-lookup"><span data-stu-id="63c6a-124">**Formula name** - Enter a name for your formula.</span></span> <span data-ttu-id="63c6a-125">這個值會顯示 hello 的基底映像的清單中，當您建立 VM 時。</span><span class="sxs-lookup"><span data-stu-id="63c6a-125">This value is displayed in hello list of base images when you create a VM.</span></span> <span data-ttu-id="63c6a-126">當您輸入時，並不正確，如果訊息指出 hello 需求是有效的名稱，會驗證 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="63c6a-126">hello name is validated as you type it, and if not valid, a message indicates hello requirements for a valid name.</span></span>
    * <span data-ttu-id="63c6a-127">**描述** - 輸入公式的有意義描述。</span><span class="sxs-lookup"><span data-stu-id="63c6a-127">**Description** - Enter a meaningful description for your formula.</span></span> <span data-ttu-id="63c6a-128">當您建立 VM 時，這個值是可從 hello 公式的內容功能表。</span><span class="sxs-lookup"><span data-stu-id="63c6a-128">This value is available from hello formula's context menu when you create a VM.</span></span>
    * <span data-ttu-id="63c6a-129">**使用者名稱** - 輸入被授與系統管理員權限的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="63c6a-129">**User name** - Enter a user name that is granted administrator privileges.</span></span>
    * <span data-ttu-id="63c6a-130">**密碼**-輸入-或從 hello 下拉式清單中選取-hello 秘密 （密碼） 的 toouse hello 指定使用者相關聯的值。</span><span class="sxs-lookup"><span data-stu-id="63c6a-130">**Password** - Enter - or select from hello dropdown - a value that is associated with hello secret (password) that you want toouse for hello specified user.</span></span> <span data-ttu-id="63c6a-131">如需 hello 機密資料的詳細資訊，請參閱[Azure DevTest Labs： 密碼的個人存放區](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/)。</span><span class="sxs-lookup"><span data-stu-id="63c6a-131">For more information about hello secrets, see [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span></span>
    * <span data-ttu-id="63c6a-132">**虛擬機器磁碟類型**-指定任一個 （硬碟磁碟機） 的 HDD 或 SSD （固態硬碟） tooindicate 哪些儲存磁碟類型可供使用此基底映像來佈建 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="63c6a-132">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) tooindicate which storage disk type is allowed for hello virtual machines provisioned using this base image.</span></span>
    * <span data-ttu-id="63c6a-133">* * 虛擬機器大小 * *-選取其中一個指定 hello 處理器核心、 RAM 大小，以及 hello VM toocreate hello 硬碟大小的 hello 預先定義的項目。</span><span class="sxs-lookup"><span data-stu-id="63c6a-133">** Virtual machine size** - Select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span> 
    * <span data-ttu-id="63c6a-134">**成品**-選取 tooopen hello**新增成品**刀鋒視窗中，您選取並設定您想 tooadd toohello 基底映像的 hello 成品。</span><span class="sxs-lookup"><span data-stu-id="63c6a-134">**Artifacts** - Select tooopen hello **Add artifacts** blade, in which you select and configure hello artifacts that you want tooadd toohello base image.</span></span> <span data-ttu-id="63c6a-135">如需構件的詳細資訊，請參閱[在 Azure DevTest Labs 中管理 VM 構件](./devtest-lab-add-vm-with-artifacts.md)。</span><span class="sxs-lookup"><span data-stu-id="63c6a-135">For more information about artifacts, see [Manage VM artifacts in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span></span>
    * <span data-ttu-id="63c6a-136">**進階設定**-選取 tooopen hello**進階**刀鋒視窗中，您可以設定下列設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="63c6a-136">**Advanced settings** - Select tooopen hello **Advanced** blade where you configure hello following settings:</span></span>
        * <span data-ttu-id="63c6a-137">**虛擬網路**-指定 hello 所需的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="63c6a-137">**Virtual network** - Specify hello desired virtual network.</span></span>
        * <span data-ttu-id="63c6a-138">**子網路**-指定所需的 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="63c6a-138">**Subnet** - Specify hello desired subnet.</span></span>    
        * <span data-ttu-id="63c6a-139">**IP 位址設定**-指定是否要讓 hello 公用、 私人或共用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="63c6a-139">**IP address configuration** - Specify if you want hello Public, Private, or Shared IP addresses.</span></span> <span data-ttu-id="63c6a-140">如需共用 IP 位址的詳細資訊，請參閱[了解 Azure DevTest Labs 中的共用 IP 位址](./devtest-lab-shared-ip.md)。</span><span class="sxs-lookup"><span data-stu-id="63c6a-140">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span></span>
        * <span data-ttu-id="63c6a-141">**讓此機器 claimable** -進行機器"claimable"表示，它將不會指派擁有權時建立的 hello。</span><span class="sxs-lookup"><span data-stu-id="63c6a-141">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at hello time of creation.</span></span> <span data-ttu-id="63c6a-142">改為實驗室使用者都能 tootake 擁有權 （「 宣告 」） hello 機器 hello 實驗室刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="63c6a-142">Instead lab users will be able tootake ownership ("claim") hello machine in hello lab's blade.</span></span>     
    * <span data-ttu-id="63c6a-143">**映像**-這個欄位會顯示 hello 先前刀鋒視窗上的 hello 您選取的基底映像的名稱。</span><span class="sxs-lookup"><span data-stu-id="63c6a-143">**Image** - This field displays name of hello base image you selected on hello previous blade.</span></span> 
     
       ![建立公式](./media/devtest-lab-create-formulas/create-formula.png)

8. <span data-ttu-id="63c6a-145">選取**建立**toocreate hello 公式。</span><span class="sxs-lookup"><span data-stu-id="63c6a-145">Select **Create** toocreate hello formula.</span></span>

9. <span data-ttu-id="63c6a-146">當建立 hello 公式之後時，它會顯示在 hello 的 hello 清單中**公式**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="63c6a-146">When hello formula has been created, it displays in hello list on hello **Formulas** blade.</span></span>

### <a name="create-a-formula-from-a-vm"></a><span data-ttu-id="63c6a-147">從 VM 建立公式</span><span class="sxs-lookup"><span data-stu-id="63c6a-147">Create a formula from a VM</span></span>
<span data-ttu-id="63c6a-148">hello 下列步驟會引導您建立公式，根據現有的 VM 的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="63c6a-148">hello following steps guide you through hello process of creating a formula based on an existing VM.</span></span> 

> [!NOTE]
> <span data-ttu-id="63c6a-149">toocreate 從 VM 的公式，hello VM 必須已建立 2016 年 3 月 30 日之後。</span><span class="sxs-lookup"><span data-stu-id="63c6a-149">toocreate a formula from a VM, hello VM must have been created after March 30, 2016.</span></span> 
> 
> 

1. <span data-ttu-id="63c6a-150">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="63c6a-150">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="63c6a-151">選取**更服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="63c6a-151">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="63c6a-152">從 hello 清單的實驗室中，選取 hello 所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="63c6a-152">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="63c6a-153">在 hello 實驗室**概觀**刀鋒視窗中，選取 hello VM 希望 toocreate hello 公式。</span><span class="sxs-lookup"><span data-stu-id="63c6a-153">On hello lab's **Overview** blade, select hello VM from which you wish toocreate hello formula.</span></span>
   
    ![實驗室 VM](./media/devtest-lab-create-formulas/my-vms.png)
5. <span data-ttu-id="63c6a-155">在 hello VM 刀鋒視窗中，選取 **建立公式 （可重複使用基底）**。</span><span class="sxs-lookup"><span data-stu-id="63c6a-155">On hello VM's blade, select **Create formula (reusable base)**.</span></span>
   
    ![建立公式](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. <span data-ttu-id="63c6a-157">在 hello**建立公式**刀鋒視窗中，輸入**名稱**和**描述**新公式。</span><span class="sxs-lookup"><span data-stu-id="63c6a-157">On hello **Create formula** blade, enter a **Name** and **Description** for your new formula.</span></span>
   
    ![建立公式刀鋒視窗](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. <span data-ttu-id="63c6a-159">選取**確定**toocreate hello 公式。</span><span class="sxs-lookup"><span data-stu-id="63c6a-159">Select **OK** toocreate hello formula.</span></span>

## <a name="modify-a-formula"></a><span data-ttu-id="63c6a-160">修改公式</span><span class="sxs-lookup"><span data-stu-id="63c6a-160">Modify a formula</span></span>
<span data-ttu-id="63c6a-161">toomodify 公式，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="63c6a-161">toomodify a formula, follow these steps:</span></span>

1. <span data-ttu-id="63c6a-162">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="63c6a-162">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="63c6a-163">選取**更服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="63c6a-163">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="63c6a-164">從 hello 清單的實驗室中，選取 hello 所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="63c6a-164">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="63c6a-165">在 hello 實驗室刀鋒視窗中，選取 **公式 （可重複使用基底）**。</span><span class="sxs-lookup"><span data-stu-id="63c6a-165">On hello lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![公式功能表](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="63c6a-167">在 hello**實驗室公式**刀鋒視窗中，您想 toomodify 選取 hello 公式。</span><span class="sxs-lookup"><span data-stu-id="63c6a-167">On hello **Lab formulas** blade, select hello formula you wish toomodify.</span></span>
6. <span data-ttu-id="63c6a-168">在 hello**更新公式**刀鋒視窗中，進行所需的 hello 的編輯，然後選取**更新**。</span><span class="sxs-lookup"><span data-stu-id="63c6a-168">On hello **Update formula** blade, make hello desired edits, and select **Update**.</span></span>

## <a name="delete-a-formula"></a><span data-ttu-id="63c6a-169">刪除公式</span><span class="sxs-lookup"><span data-stu-id="63c6a-169">Delete a formula</span></span>
<span data-ttu-id="63c6a-170">toodelete 公式，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="63c6a-170">toodelete a formula, follow these steps:</span></span>

1. <span data-ttu-id="63c6a-171">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="63c6a-171">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="63c6a-172">選取**更服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="63c6a-172">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="63c6a-173">從 hello 清單的實驗室中，選取 hello 所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="63c6a-173">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="63c6a-174">在 hello 實驗室**設定**刀鋒視窗中，選取**公式**。</span><span class="sxs-lookup"><span data-stu-id="63c6a-174">On hello lab **Settings** blade, select **Formulas**.</span></span>
   
    ![公式功能表](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="63c6a-176">在 hello**實驗室公式**刀鋒視窗中，選取 hello hello 公式的右邊的省略符號 toohello 想 toodelete。</span><span class="sxs-lookup"><span data-stu-id="63c6a-176">On hello **Lab formulas** blade, select hello ellipsis toohello right of hello formula you wish toodelete.</span></span>
   
    ![公式功能表](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. <span data-ttu-id="63c6a-178">Hello 公式的內容功能表上，選取**刪除**。</span><span class="sxs-lookup"><span data-stu-id="63c6a-178">On hello formula's context menu, select **Delete**.</span></span>
   
    ![公式操作功能表](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. <span data-ttu-id="63c6a-180">選取**是**toohello 刪除確認 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="63c6a-180">Select **Yes** toohello deletion confirmation dialog.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="63c6a-181">相關部落格文章</span><span class="sxs-lookup"><span data-stu-id="63c6a-181">Related blog posts</span></span>
* [<span data-ttu-id="63c6a-182">自訂映像或公式？</span><span class="sxs-lookup"><span data-stu-id="63c6a-182">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="63c6a-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="63c6a-183">Next steps</span></span>
<span data-ttu-id="63c6a-184">一旦您已經建立的公式，建立 VM 時下, 一個步驟的 hello 太[加入 VM tooyour 實驗室](devtest-lab-add-vm-with-artifacts.md)。</span><span class="sxs-lookup"><span data-stu-id="63c6a-184">Once you have created a formula for use when creating a VM, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

