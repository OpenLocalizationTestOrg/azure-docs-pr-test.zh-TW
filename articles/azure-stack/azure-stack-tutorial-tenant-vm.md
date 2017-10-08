---
title: "aaaMake 虛擬機器可用的 tooyour Azure 堆疊使用者 |Microsoft 文件"
description: "提供 Azure 堆疊上的教學課程 toomake 虛擬機器"
services: azure-stack
documentationcenter: 
author: vhorne
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/22/2017
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: 345206912f17662e51341c71175c5fe87b692ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="make-virtual-machines-available-tooyour-azure-stack-users"></a><span data-ttu-id="90408-103">讓虛擬機器可用 tooyour Azure 堆疊使用者</span><span class="sxs-lookup"><span data-stu-id="90408-103">Make virtual machines available tooyour Azure Stack users</span></span>
<span data-ttu-id="90408-104">Azure 堆疊的雲端系統管理員，您可以建立您的使用者 （有時參照的 tooas 租用戶） 可以訂閱的優惠。</span><span class="sxs-lookup"><span data-stu-id="90408-104">As an Azure Stack cloud administrator, you can create offers that your users (sometimes referred tooas tenants) can subscribe to.</span></span> <span data-ttu-id="90408-105">利用其訂用帳戶，使用者可以接著取用 Azure Stack 服務。</span><span class="sxs-lookup"><span data-stu-id="90408-105">Using their subscription, users can then consume Azure Stack services.</span></span>

<span data-ttu-id="90408-106">本文章將示範如何 toocreate 的供應項目，然後進行測試。</span><span class="sxs-lookup"><span data-stu-id="90408-106">This article shows you how toocreate an offer, and then test it.</span></span> <span data-ttu-id="90408-107">Hello 測試中，您將登入 toohello 入口網站的使用者身分，訂閱 toohello 供應項目，然後再建立虛擬機器使用 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="90408-107">For hello test, you will log in toohello portal as a user, subscribe toohello offer, and then create a virtual machine using hello subscription.</span></span>

<span data-ttu-id="90408-108">您將了解：</span><span class="sxs-lookup"><span data-stu-id="90408-108">What you will learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="90408-109">建立優惠</span><span class="sxs-lookup"><span data-stu-id="90408-109">Create an offer</span></span>
> * <span data-ttu-id="90408-110">新增映像</span><span class="sxs-lookup"><span data-stu-id="90408-110">Add an image</span></span>
> * <span data-ttu-id="90408-111">測試 hello 優惠</span><span class="sxs-lookup"><span data-stu-id="90408-111">Test hello offer</span></span>


<span data-ttu-id="90408-112">Azure 堆疊中的服務會傳遞 toousers 使用訂用帳戶、 提供項目，以及計劃。</span><span class="sxs-lookup"><span data-stu-id="90408-112">In Azure Stack, services are delivered toousers using subscriptions, offers, and plans.</span></span> <span data-ttu-id="90408-113">使用者可以訂閱 toomultiple 優惠。</span><span class="sxs-lookup"><span data-stu-id="90408-113">Users can subscribe toomultiple offers.</span></span> <span data-ttu-id="90408-114">優惠可以有一個或多個方案，而方案則可有一或多項服務。</span><span class="sxs-lookup"><span data-stu-id="90408-114">Offers can have one or more plans, and plans can have one or more services.</span></span>

![訂用帳戶、供應項目與方案](media/azure-stack-key-features/image4.png)

<span data-ttu-id="90408-116">詳細資訊，請參閱 toolearn[主要功能和 Azure 堆疊中的概念](azure-stack-key-features.md)。</span><span class="sxs-lookup"><span data-stu-id="90408-116">toolearn more, see [Key features and concepts in Azure Stack](azure-stack-key-features.md).</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="90408-117">建立優惠</span><span class="sxs-lookup"><span data-stu-id="90408-117">Create an offer</span></span>

<span data-ttu-id="90408-118">現在您可以為使用者準備項目。</span><span class="sxs-lookup"><span data-stu-id="90408-118">Now you can get things ready for your users.</span></span> <span data-ttu-id="90408-119">當您啟動 hello 程序時，您是第一個提示的 toocreate hello 優惠，計劃，然後按一下最後配額。</span><span class="sxs-lookup"><span data-stu-id="90408-119">When you start hello process, you are first prompted toocreate hello offer, then a plan, and finally quotas.</span></span>

3. <span data-ttu-id="90408-120">**建立優惠**</span><span class="sxs-lookup"><span data-stu-id="90408-120">**Create an offer**</span></span>

   <span data-ttu-id="90408-121">提供項目是一或多個計劃的群組有 toousers toopurchase 該提供者或訂閱。</span><span class="sxs-lookup"><span data-stu-id="90408-121">Offers are groups of one or more plans that providers present toousers toopurchase or subscribe to.</span></span>

   <span data-ttu-id="90408-122">a.</span><span class="sxs-lookup"><span data-stu-id="90408-122">a.</span></span> <span data-ttu-id="90408-123">[登入](azure-stack-connect-azure-stack.md)toohello 網站中的做為雲端系統管理員，然後按一下**新增** > **租用戶提供 + 計劃** > **提供**。</span><span class="sxs-lookup"><span data-stu-id="90408-123">[Sign in](azure-stack-connect-azure-stack.md) toohello portal as a cloud administrator and then click **New** > **Tenant Offers + Plans** > **Offer**.</span></span>
   <span data-ttu-id="90408-124">![新增供應項目](media/azure-stack-tutorial-tenant-vm/image01.png)</span><span class="sxs-lookup"><span data-stu-id="90408-124">![New offer](media/azure-stack-tutorial-tenant-vm/image01.png)</span></span>

   <span data-ttu-id="90408-125">b.</span><span class="sxs-lookup"><span data-stu-id="90408-125">b.</span></span> <span data-ttu-id="90408-126">在 hello**新提供**區段中，填寫**顯示名稱**和**資源名稱**，，然後選取新的或現有**資源群組**。</span><span class="sxs-lookup"><span data-stu-id="90408-126">In hello **New Offer** section, fill in **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span></span> <span data-ttu-id="90408-127">hello 顯示名稱會是 hello 供應項目的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="90408-127">hello Display Name is hello offer's friendly name.</span></span> <span data-ttu-id="90408-128">Hello 雲端操作員可以看到 hello 資源名稱。</span><span class="sxs-lookup"><span data-stu-id="90408-128">Only hello cloud operator can see hello Resource Name.</span></span> <span data-ttu-id="90408-129">它的 hello 名稱，系統管理員 」 搭配 toowork hello 供應項目做為 Azure 資源管理員資源。</span><span class="sxs-lookup"><span data-stu-id="90408-129">It's hello name that admins use toowork with hello offer as an Azure Resource Manager resource.</span></span>

   ![顯示名稱](media/azure-stack-tutorial-tenant-vm/image02.png)

   <span data-ttu-id="90408-131">c.</span><span class="sxs-lookup"><span data-stu-id="90408-131">c.</span></span> <span data-ttu-id="90408-132">按一下**基底計劃**，並在 hello**計劃**區段中，按一下**新增**tooadd 新的計劃 toohello 優惠。</span><span class="sxs-lookup"><span data-stu-id="90408-132">Click **Base plans**, and in hello **Plan** section, click **Add** tooadd a new plan toohello offer.</span></span>

   ![新增方案](media/azure-stack-tutorial-tenant-vm/image03.png)

   <span data-ttu-id="90408-134">d.</span><span class="sxs-lookup"><span data-stu-id="90408-134">d.</span></span> <span data-ttu-id="90408-135">在 hello**新增計劃**區段中，填寫**顯示名稱**和**資源名稱**。</span><span class="sxs-lookup"><span data-stu-id="90408-135">In hello **New Plan** section, fill in **Display Name** and **Resource Name**.</span></span> <span data-ttu-id="90408-136">hello 顯示名稱是使用者看到的 hello 計劃的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="90408-136">hello Display Name is hello plan's friendly name that users see.</span></span> <span data-ttu-id="90408-137">Hello 雲端操作員可以看到 hello 資源名稱。</span><span class="sxs-lookup"><span data-stu-id="90408-137">Only hello cloud operator can see hello Resource Name.</span></span> <span data-ttu-id="90408-138">它的 hello 名稱，雲端操作員搭配 toowork hello 計劃做為 Azure 資源管理員資源。</span><span class="sxs-lookup"><span data-stu-id="90408-138">It's hello name that cloud operators use toowork with hello plan as an Azure Resource Manager resource.</span></span>

   ![方案顯示名稱](media/azure-stack-tutorial-tenant-vm/image04.png)

   <span data-ttu-id="90408-140">e.</span><span class="sxs-lookup"><span data-stu-id="90408-140">e.</span></span> <span data-ttu-id="90408-141">按一下 服務，選取 Microsoft.Compute、Microsoft.Network 及 Microsoft.Storage，然後按一下選取。</span><span class="sxs-lookup"><span data-stu-id="90408-141">Click **Services**, select **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**, and then click **Select**.</span></span>

   ![方案服務](media/azure-stack-tutorial-tenant-vm/image05.png)

   <span data-ttu-id="90408-143">f.</span><span class="sxs-lookup"><span data-stu-id="90408-143">f.</span></span> <span data-ttu-id="90408-144">按一下**配額**，然後選取您想要的 toocreate 配額 hello 第一個服務。</span><span class="sxs-lookup"><span data-stu-id="90408-144">Click **Quotas**, and then select hello first service for which you want toocreate a quota.</span></span> <span data-ttu-id="90408-145">IaaS 配額，請遵循下列步驟 hello 運算、 網路和儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="90408-145">For an IaaS quota, follow these steps for hello Compute, Network, and Storage services.</span></span>

   <span data-ttu-id="90408-146">在此範例中，我們會先建立 hello 計算服務的配額。</span><span class="sxs-lookup"><span data-stu-id="90408-146">In this example, we first create a quota for hello Compute service.</span></span> <span data-ttu-id="90408-147">在 hello 命名空間清單中，選取 hello **Microsoft.Compute**命名空間，然後按一下**建立新的配額**。</span><span class="sxs-lookup"><span data-stu-id="90408-147">In hello namespace list, select hello **Microsoft.Compute** namespace and then click **Create new quota**.</span></span>
   
   ![建立新的配額](media/azure-stack-tutorial-tenant-vm/image06.png)

   <span data-ttu-id="90408-149">g.</span><span class="sxs-lookup"><span data-stu-id="90408-149">g.</span></span> <span data-ttu-id="90408-150">在 hello**建立配額**區段中，輸入 hello 配額以及組 hello hello 配額，然後按一下所需的參數名稱**確定**。</span><span class="sxs-lookup"><span data-stu-id="90408-150">On hello **Create quota** section, type a name for hello quota and set hello desired parameters for hello quota and click **OK**.</span></span>

   ![配額名稱](media/azure-stack-tutorial-tenant-vm/image07.png)

   <span data-ttu-id="90408-152">h.</span><span class="sxs-lookup"><span data-stu-id="90408-152">h.</span></span> <span data-ttu-id="90408-153">現在，如**Microsoft.Compute**，選取您建立的 hello 配額。</span><span class="sxs-lookup"><span data-stu-id="90408-153">Now, for **Microsoft.Compute**, select hello quota that you created.</span></span>

   ![選取配額](media/azure-stack-tutorial-tenant-vm/image08.png)

   <span data-ttu-id="90408-155">重複這些步驟 hello 網路和儲存體服務，然後再按一下**確定**上 hello**配額**> 一節。</span><span class="sxs-lookup"><span data-stu-id="90408-155">Repeat these steps for hello Network and Storage services, and then click **OK** on hello **Quotas** section.</span></span>

   <span data-ttu-id="90408-156">i.</span><span class="sxs-lookup"><span data-stu-id="90408-156">i.</span></span> <span data-ttu-id="90408-157">按一下**確定**上 hello**新計劃**> 一節。</span><span class="sxs-lookup"><span data-stu-id="90408-157">Click **OK** on hello **New plan** section.</span></span>

   <span data-ttu-id="90408-158">j.</span><span class="sxs-lookup"><span data-stu-id="90408-158">j.</span></span> <span data-ttu-id="90408-159">在 hello**計劃**區段中選取 hello 新計劃，然後按一下**選取**。</span><span class="sxs-lookup"><span data-stu-id="90408-159">On hello **Plan** section, select hello new plan and click **Select**.</span></span>

   <span data-ttu-id="90408-160">k.</span><span class="sxs-lookup"><span data-stu-id="90408-160">k.</span></span> <span data-ttu-id="90408-161">在 hello**新的優惠**區段中，按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="90408-161">On hello **New offer** section, click **Create**.</span></span> <span data-ttu-id="90408-162">在建立 hello 優惠時，您會看到通知。</span><span class="sxs-lookup"><span data-stu-id="90408-162">You see a notification when hello offer has been created.</span></span>

   <span data-ttu-id="90408-163">l.</span><span class="sxs-lookup"><span data-stu-id="90408-163">l.</span></span> <span data-ttu-id="90408-164">Hello 儀表板功能表上，按一下**提供**然後按一下您所建立的 hello 供應項目。</span><span class="sxs-lookup"><span data-stu-id="90408-164">On hello dashboard menu, click **Offers** and then click hello offer you created.</span></span>

   <span data-ttu-id="90408-165">m.</span><span class="sxs-lookup"><span data-stu-id="90408-165">m.</span></span> <span data-ttu-id="90408-166">按一下 變更狀態，然後按一下公開。</span><span class="sxs-lookup"><span data-stu-id="90408-166">Click **Change State**, and then click **Public**.</span></span>

   ![公開映像](media/azure-stack-tutorial-tenant-vm/image09.png)

## <a name="add-an-image"></a><span data-ttu-id="90408-168">新增映像</span><span class="sxs-lookup"><span data-stu-id="90408-168">Add an image</span></span>

<span data-ttu-id="90408-169">您可以佈建虛擬機器之前，您必須加入的映像 toohello 堆疊 Azure marketplace。</span><span class="sxs-lookup"><span data-stu-id="90408-169">Before you can provision virtual machines, you must add an image toohello Azure Stack marketplace.</span></span> <span data-ttu-id="90408-170">您可以加入您的選擇，包括 Linux 映像，從 hello Azure Marketplace 的 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="90408-170">You can add hello image of your choice, including Linux images, from hello Azure Marketplace.</span></span>

<span data-ttu-id="90408-171">如果您正在連線的案例中，而且如果您註冊 Azure 與您 Azure 堆疊的執行個體，然後您可以下載 hello Windows Server 2016 VM 映像從 hello Azure Marketplace 使用 hello hello 中所述的步驟[下載marketplace 項目，從 Azure tooAzure 堆疊](azure-stack-download-azure-marketplace-item.md)主題。</span><span class="sxs-lookup"><span data-stu-id="90408-171">If you are operating in a connected scenario and if you have registered your Azure Stack instance with Azure, then you can download hello Windows Server 2016 VM image from hello Azure Marketplace by using hello steps described in hello [Download marketplace items from Azure tooAzure Stack](azure-stack-download-azure-marketplace-item.md) topic.</span></span>

<span data-ttu-id="90408-172">如需新增不同的項目 toohello marketplace 資訊，請參閱[hello Marketplace</堆疊](azure-stack-marketplace.md)。</span><span class="sxs-lookup"><span data-stu-id="90408-172">For information about adding different items toohello marketplace, see [hello Azure Stack Marketplace](azure-stack-marketplace.md).</span></span>

## <a name="test-hello-offer"></a><span data-ttu-id="90408-173">測試 hello 優惠</span><span class="sxs-lookup"><span data-stu-id="90408-173">Test hello offer</span></span>

<span data-ttu-id="90408-174">既然您已經建立供應項目，您可以進行測試。</span><span class="sxs-lookup"><span data-stu-id="90408-174">Now that you’ve created an offer, you can test it.</span></span> <span data-ttu-id="90408-175">以使用者身分登入和訂閱 toohello 供應項目，然後將虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="90408-175">Log in as a user and subscribe toohello offer and then add a virtual machine.</span></span>

1. <span data-ttu-id="90408-176">**訂閱 tooan 供應項目**</span><span class="sxs-lookup"><span data-stu-id="90408-176">**Subscribe tooan offer**</span></span>

   <span data-ttu-id="90408-177">現在您可以登入 toohello 入口網站為使用者 toosubscribe tooan 供應項目。</span><span class="sxs-lookup"><span data-stu-id="90408-177">Now you can log in toohello portal as a user toosubscribe tooan offer.</span></span>

   <span data-ttu-id="90408-178">a.</span><span class="sxs-lookup"><span data-stu-id="90408-178">a.</span></span> <span data-ttu-id="90408-179">Hello Azure 堆疊部署套件在電腦上，登入太`https://portal.local.azurestack.external`作為使用者按一下**取得訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="90408-179">On hello Azure Stack Deployment Kit computer, log in too`https://portal.local.azurestack.external` as a user and click **Get a Subscription**.</span></span>

   ![取得訂用帳戶](media/azure-stack-subscribe-plan-provision-vm/image01.png)

   <span data-ttu-id="90408-181">b.</span><span class="sxs-lookup"><span data-stu-id="90408-181">b.</span></span> <span data-ttu-id="90408-182">在 hello**顯示名稱**欄位中，輸入您的訂用帳戶的名稱，按一下**提供**，按一下其中一個 hello hello 優惠**選擇優惠**區段，，然後按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="90408-182">In hello **Display Name** field, type a name for your subscription, click **Offer**, click one of hello offers in hello **Choose an offer** section, and then click **Create**.</span></span>

   ![建立優惠](media/azure-stack-subscribe-plan-provision-vm/image02.png)

   <span data-ttu-id="90408-184">c.</span><span class="sxs-lookup"><span data-stu-id="90408-184">c.</span></span> <span data-ttu-id="90408-185">建立 tooview hello 訂用帳戶中，按一下**更多服務**，按一下 **訂閱**，然後按一下 新的訂用。</span><span class="sxs-lookup"><span data-stu-id="90408-185">tooview hello subscription you created, click **More services**, click **Subscriptions**, then click your new subscription.</span></span>  

   <span data-ttu-id="90408-186">訂閱 tooan 供應項目之後，重新整理 hello 入口 toosee 哪些服務為 hello 新訂閱的一部分。</span><span class="sxs-lookup"><span data-stu-id="90408-186">After you subscribe tooan offer, refresh hello portal toosee which services are part of hello new subscription.</span></span>

2. <span data-ttu-id="90408-187">**佈建虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="90408-187">**Provision a virtual machine**</span></span>

   <span data-ttu-id="90408-188">現在您可以登入 toohello 入口網站為使用者 tooprovision 使用 hello 訂用帳戶在虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="90408-188">Now you can log in toohello portal as a user tooprovision a virtual machine using hello subscription.</span></span> 

   <span data-ttu-id="90408-189">a.</span><span class="sxs-lookup"><span data-stu-id="90408-189">a.</span></span> <span data-ttu-id="90408-190">Hello Azure 堆疊部署套件在電腦上，登入太`https://portal.local.azurestack.external`作為使用者，然後按一下**新增** > **計算** > **Windows Server 2016 DatacenterEval**。</span><span class="sxs-lookup"><span data-stu-id="90408-190">On hello Azure Stack Deployment Kit computer, log in too`https://portal.local.azurestack.external` as a user, and then click **New** > **Compute** > **Windows Server 2016 Datacenter Eval**.</span></span>  

   <span data-ttu-id="90408-191">b.</span><span class="sxs-lookup"><span data-stu-id="90408-191">b.</span></span> <span data-ttu-id="90408-192">在 hello**基本概念**區段中，輸入**名稱**，**使用者名**，和**密碼**。</span><span class="sxs-lookup"><span data-stu-id="90408-192">In hello **Basics** section, type a **Name**, **User name**, and **Password**.</span></span> <span data-ttu-id="90408-193">針對 [VM 磁碟類型]，請選擇 [HDD]。</span><span class="sxs-lookup"><span data-stu-id="90408-193">For **VM disk type**, choose **HDD**.</span></span> <span data-ttu-id="90408-194">選擇 [訂用帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="90408-194">Choose a **Subscription**.</span></span> <span data-ttu-id="90408-195">建立 資源群組，或選取現有的資源群組，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="90408-195">Create a **Resource group**, or select an existing one, and then click **OK**.</span></span>  

   <span data-ttu-id="90408-196">c.</span><span class="sxs-lookup"><span data-stu-id="90408-196">c.</span></span> <span data-ttu-id="90408-197">在 hello**大小選擇 「**區段中，按一下**A1 基本**，然後按一下**選取**。</span><span class="sxs-lookup"><span data-stu-id="90408-197">In hello **Choose a size** section, click **A1 Basic**, and then click **Select**.</span></span>  

   <span data-ttu-id="90408-198">d.</span><span class="sxs-lookup"><span data-stu-id="90408-198">d.</span></span> <span data-ttu-id="90408-199">在 hello**設定**區段中，按一下**虛擬網路**。</span><span class="sxs-lookup"><span data-stu-id="90408-199">In hello **Settings** section, click **Virtual network**.</span></span> <span data-ttu-id="90408-200">在 hello**選擇虛擬網路**區段中，按一下**建立新**。</span><span class="sxs-lookup"><span data-stu-id="90408-200">In hello **Choose virtual network** section, click **Create new**.</span></span> <span data-ttu-id="90408-201">在 hello**建立虛擬網路**區段中，接受所有的 hello 預設值，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="90408-201">In hello **Create virtual network** section, accept all hello defaults, and click **OK**.</span></span> <span data-ttu-id="90408-202">在 hello**設定**區段中，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="90408-202">In hello **Settings** section, click **OK**.</span></span>

   ![建立虛擬網路](media/azure-stack-provision-vm/image04.png)

   <span data-ttu-id="90408-204">e.</span><span class="sxs-lookup"><span data-stu-id="90408-204">e.</span></span> <span data-ttu-id="90408-205">在 hello**摘要**區段中，按一下**確定**toocreate hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="90408-205">In hello **Summary** section, click **OK** toocreate hello virtual machine.</span></span>  

   <span data-ttu-id="90408-206">f.</span><span class="sxs-lookup"><span data-stu-id="90408-206">f.</span></span> <span data-ttu-id="90408-207">toosee 新的虛擬機器，按一下 **所有資源**，然後搜尋 hello 虛擬機器，然後按一下其名稱。</span><span class="sxs-lookup"><span data-stu-id="90408-207">toosee your new virtual machine, click **All resources**, then search for hello virtual machine and click its name.</span></span>

    ![所有資源](media/azure-stack-provision-vm/image06.png)

<span data-ttu-id="90408-209">在本教學課程中，您已了解：</span><span class="sxs-lookup"><span data-stu-id="90408-209">What you learned in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="90408-210">建立優惠</span><span class="sxs-lookup"><span data-stu-id="90408-210">Create an offer</span></span>
> * <span data-ttu-id="90408-211">新增映像</span><span class="sxs-lookup"><span data-stu-id="90408-211">Add an image</span></span>
> * <span data-ttu-id="90408-212">測試 hello 優惠</span><span class="sxs-lookup"><span data-stu-id="90408-212">Test hello offer</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="90408-213">讓 web、 行動裝置、 應用程式開發介面應用程式可用 tooyour Azure 堆疊使用者</span><span class="sxs-lookup"><span data-stu-id="90408-213">Make web, mobile, and API apps available tooyour Azure Stack users</span></span>](azure-stack-tutorial-app-service.md)
