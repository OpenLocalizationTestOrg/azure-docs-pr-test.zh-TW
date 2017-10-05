---
title: "將虛擬機器提供給您的 Azure Stack 使用者| Microsoft Docs"
description: "此教學課程說明如何將虛擬機器提供給 Azure Stack"
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
ms.openlocfilehash: d2f38bc1c0b97e408f619f3ea2f704725e3bb460
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="make-virtual-machines-available-to-your-azure-stack-users"></a><span data-ttu-id="09e14-103">將虛擬機器提供給您的 Azure Stack 使用者</span><span class="sxs-lookup"><span data-stu-id="09e14-103">Make virtual machines available to your Azure Stack users</span></span>
<span data-ttu-id="09e14-104">身為 Azure Stack 雲端系統管理員，您可以建立供應項目，以供您的使用者 (有時稱為租用戶) 訂閱。</span><span class="sxs-lookup"><span data-stu-id="09e14-104">As an Azure Stack cloud administrator, you can create offers that your users (sometimes referred to as tenants) can subscribe to.</span></span> <span data-ttu-id="09e14-105">利用其訂用帳戶，使用者可以接著取用 Azure Stack 服務。</span><span class="sxs-lookup"><span data-stu-id="09e14-105">Using their subscription, users can then consume Azure Stack services.</span></span>

<span data-ttu-id="09e14-106">此文章說明如何建立供應項目並進行測試。</span><span class="sxs-lookup"><span data-stu-id="09e14-106">This article shows you how to create an offer, and then test it.</span></span> <span data-ttu-id="09e14-107">針對測試，您將必須以使用者身分登入入口網站，訂閱該供應項目，然後使用訂用帳戶建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="09e14-107">For the test, you will log in to the portal as a user, subscribe to the offer, and then create a virtual machine using the subscription.</span></span>

<span data-ttu-id="09e14-108">您將了解：</span><span class="sxs-lookup"><span data-stu-id="09e14-108">What you will learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="09e14-109">建立優惠</span><span class="sxs-lookup"><span data-stu-id="09e14-109">Create an offer</span></span>
> * <span data-ttu-id="09e14-110">新增映像</span><span class="sxs-lookup"><span data-stu-id="09e14-110">Add an image</span></span>
> * <span data-ttu-id="09e14-111">測試供應項目</span><span class="sxs-lookup"><span data-stu-id="09e14-111">Test the offer</span></span>


<span data-ttu-id="09e14-112">在 Azure Stack 中，能透過訂用帳戶、供應項目與方案，為使用者提供服務。</span><span class="sxs-lookup"><span data-stu-id="09e14-112">In Azure Stack, services are delivered to users using subscriptions, offers, and plans.</span></span> <span data-ttu-id="09e14-113">使用者可以訂閱多個供應項目。</span><span class="sxs-lookup"><span data-stu-id="09e14-113">Users can subscribe to multiple offers.</span></span> <span data-ttu-id="09e14-114">優惠可以有一個或多個方案，而方案則可有一或多項服務。</span><span class="sxs-lookup"><span data-stu-id="09e14-114">Offers can have one or more plans, and plans can have one or more services.</span></span>

![訂用帳戶、供應項目與方案](media/azure-stack-key-features/image4.png)

<span data-ttu-id="09e14-116">若要深入了解，請參閱 [Azure Stack 中的主要功能與概念](azure-stack-key-features.md)。</span><span class="sxs-lookup"><span data-stu-id="09e14-116">To learn more, see [Key features and concepts in Azure Stack](azure-stack-key-features.md).</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="09e14-117">建立優惠</span><span class="sxs-lookup"><span data-stu-id="09e14-117">Create an offer</span></span>

<span data-ttu-id="09e14-118">現在您可以為使用者準備項目。</span><span class="sxs-lookup"><span data-stu-id="09e14-118">Now you can get things ready for your users.</span></span> <span data-ttu-id="09e14-119">當您開始進行此程序時，系統會先提示您建立供應項目，然後建立方案，最後建立配額。</span><span class="sxs-lookup"><span data-stu-id="09e14-119">When you start the process, you are first prompted to create the offer, then a plan, and finally quotas.</span></span>

3. <span data-ttu-id="09e14-120">**建立優惠**</span><span class="sxs-lookup"><span data-stu-id="09e14-120">**Create an offer**</span></span>

   <span data-ttu-id="09e14-121">供應項目是一組提供者供使用者購買或訂閱的一或多個方案。</span><span class="sxs-lookup"><span data-stu-id="09e14-121">Offers are groups of one or more plans that providers present to users to purchase or subscribe to.</span></span>

   <span data-ttu-id="09e14-122">a.</span><span class="sxs-lookup"><span data-stu-id="09e14-122">a.</span></span> <span data-ttu-id="09e14-123">以系統管理員身分[登入](azure-stack-connect-azure-stack.md)入口網站，然後按一下 [新增] > [租用戶供應項目 + 方案] > [供應項目]。</span><span class="sxs-lookup"><span data-stu-id="09e14-123">[Sign in](azure-stack-connect-azure-stack.md) to the portal as a cloud administrator and then click **New** > **Tenant Offers + Plans** > **Offer**.</span></span>
   <span data-ttu-id="09e14-124">![新增供應項目](media/azure-stack-tutorial-tenant-vm/image01.png)</span><span class="sxs-lookup"><span data-stu-id="09e14-124">![New offer](media/azure-stack-tutorial-tenant-vm/image01.png)</span></span>

   <span data-ttu-id="09e14-125">b.</span><span class="sxs-lookup"><span data-stu-id="09e14-125">b.</span></span> <span data-ttu-id="09e14-126">在 [新增供應項目] 區段中，填寫 [顯示名稱] 與 [資源名稱]，然後選取新的或現有的 [資源群組]。</span><span class="sxs-lookup"><span data-stu-id="09e14-126">In the **New Offer** section, fill in **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span></span> <span data-ttu-id="09e14-127">[顯示名稱] 是供應項目的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="09e14-127">The Display Name is the offer's friendly name.</span></span> <span data-ttu-id="09e14-128">只有雲端操作員可以看到 [資源名稱]。</span><span class="sxs-lookup"><span data-stu-id="09e14-128">Only the cloud operator can see the Resource Name.</span></span> <span data-ttu-id="09e14-129">它是系統管理員用來處理其他供應項目 (以 Azure Resource Manager 資源方式) 的名稱。</span><span class="sxs-lookup"><span data-stu-id="09e14-129">It's the name that admins use to work with the offer as an Azure Resource Manager resource.</span></span>

   ![顯示名稱](media/azure-stack-tutorial-tenant-vm/image02.png)

   <span data-ttu-id="09e14-131">c.</span><span class="sxs-lookup"><span data-stu-id="09e14-131">c.</span></span> <span data-ttu-id="09e14-132">按一下 [基本方案]，然後在 [方案] 區段中，按一下 [新增] 以將新方案新增到供應項目中。</span><span class="sxs-lookup"><span data-stu-id="09e14-132">Click **Base plans**, and in the **Plan** section, click **Add** to add a new plan to the offer.</span></span>

   ![新增方案](media/azure-stack-tutorial-tenant-vm/image03.png)

   <span data-ttu-id="09e14-134">d.</span><span class="sxs-lookup"><span data-stu-id="09e14-134">d.</span></span> <span data-ttu-id="09e14-135">在 [新增方案] 區段中，填寫 [顯示名稱] 與 [資源名稱]。</span><span class="sxs-lookup"><span data-stu-id="09e14-135">In the **New Plan** section, fill in **Display Name** and **Resource Name**.</span></span> <span data-ttu-id="09e14-136">[顯示名稱] 是使用者看到的方案易記名稱。</span><span class="sxs-lookup"><span data-stu-id="09e14-136">The Display Name is the plan's friendly name that users see.</span></span> <span data-ttu-id="09e14-137">只有雲端操作員可以看到 [資源名稱]。</span><span class="sxs-lookup"><span data-stu-id="09e14-137">Only the cloud operator can see the Resource Name.</span></span> <span data-ttu-id="09e14-138">它是雲端操作員用來處理其他方案 (以 Azure Resource Manager 資源方式) 的名稱。</span><span class="sxs-lookup"><span data-stu-id="09e14-138">It's the name that cloud operators use to work with the plan as an Azure Resource Manager resource.</span></span>

   ![方案顯示名稱](media/azure-stack-tutorial-tenant-vm/image04.png)

   <span data-ttu-id="09e14-140">e.</span><span class="sxs-lookup"><span data-stu-id="09e14-140">e.</span></span> <span data-ttu-id="09e14-141">按一下 [服務]，選取 [Microsoft.Compute]、[Microsoft.Network] 及 [Microsoft.Storage]，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="09e14-141">Click **Services**, select **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**, and then click **Select**.</span></span>

   ![方案服務](media/azure-stack-tutorial-tenant-vm/image05.png)

   <span data-ttu-id="09e14-143">f.</span><span class="sxs-lookup"><span data-stu-id="09e14-143">f.</span></span> <span data-ttu-id="09e14-144">按一下 [配額]，然後選取您要建立配額的第一個服務。</span><span class="sxs-lookup"><span data-stu-id="09e14-144">Click **Quotas**, and then select the first service for which you want to create a quota.</span></span> <span data-ttu-id="09e14-145">針對 IaaS 配額，請針對計算、網路與儲存體服務依照這些步驟執行。</span><span class="sxs-lookup"><span data-stu-id="09e14-145">For an IaaS quota, follow these steps for the Compute, Network, and Storage services.</span></span>

   <span data-ttu-id="09e14-146">在此範例中，我們先為計算服務建立配額。</span><span class="sxs-lookup"><span data-stu-id="09e14-146">In this example, we first create a quota for the Compute service.</span></span> <span data-ttu-id="09e14-147">在命名空間清單中，選取 [Microsoft.Compute] 命名空間，然後按一下 [建立新的配額]。</span><span class="sxs-lookup"><span data-stu-id="09e14-147">In the namespace list, select the **Microsoft.Compute** namespace and then click **Create new quota**.</span></span>
   
   ![建立新的配額](media/azure-stack-tutorial-tenant-vm/image06.png)

   <span data-ttu-id="09e14-149">g.</span><span class="sxs-lookup"><span data-stu-id="09e14-149">g.</span></span> <span data-ttu-id="09e14-150">在 [建立配額] 區段中，輸入配額名稱並為配額設定想要的參數，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="09e14-150">On the **Create quota** section, type a name for the quota and set the desired parameters for the quota and click **OK**.</span></span>

   ![配額名稱](media/azure-stack-tutorial-tenant-vm/image07.png)

   <span data-ttu-id="09e14-152">h.</span><span class="sxs-lookup"><span data-stu-id="09e14-152">h.</span></span> <span data-ttu-id="09e14-153">現在，針對 **Microsoft.Compute**，選取您所建立的配額。</span><span class="sxs-lookup"><span data-stu-id="09e14-153">Now, for **Microsoft.Compute**, select the quota that you created.</span></span>

   ![選取配額](media/azure-stack-tutorial-tenant-vm/image08.png)

   <span data-ttu-id="09e14-155">針對網路與儲存體服務重複這些步驟，然後按一下 [配額] 區段中的 [確定]。</span><span class="sxs-lookup"><span data-stu-id="09e14-155">Repeat these steps for the Network and Storage services, and then click **OK** on the **Quotas** section.</span></span>

   <span data-ttu-id="09e14-156">i.</span><span class="sxs-lookup"><span data-stu-id="09e14-156">i.</span></span> <span data-ttu-id="09e14-157">按一下 [新的方案] 區段中的 [確定]。</span><span class="sxs-lookup"><span data-stu-id="09e14-157">Click **OK** on the **New plan** section.</span></span>

   <span data-ttu-id="09e14-158">j.</span><span class="sxs-lookup"><span data-stu-id="09e14-158">j.</span></span> <span data-ttu-id="09e14-159">在 [方案] 區段中，選取新方案並按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="09e14-159">On the **Plan** section, select the new plan and click **Select**.</span></span>

   <span data-ttu-id="09e14-160">k.</span><span class="sxs-lookup"><span data-stu-id="09e14-160">k.</span></span> <span data-ttu-id="09e14-161">在 [新增供應項目] 區段中，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="09e14-161">On the **New offer** section, click **Create**.</span></span> <span data-ttu-id="09e14-162">建立您的供應項目之後，您會看到通知。</span><span class="sxs-lookup"><span data-stu-id="09e14-162">You see a notification when the offer has been created.</span></span>

   <span data-ttu-id="09e14-163">l.</span><span class="sxs-lookup"><span data-stu-id="09e14-163">l.</span></span> <span data-ttu-id="09e14-164">在儀表板功能表上，按一下 [供應項目]，然後按一下您建立的供應項目。</span><span class="sxs-lookup"><span data-stu-id="09e14-164">On the dashboard menu, click **Offers** and then click the offer you created.</span></span>

   <span data-ttu-id="09e14-165">m.</span><span class="sxs-lookup"><span data-stu-id="09e14-165">m.</span></span> <span data-ttu-id="09e14-166">按一下 [變更狀態]，然後按一下 [公開]。</span><span class="sxs-lookup"><span data-stu-id="09e14-166">Click **Change State**, and then click **Public**.</span></span>

   ![公開映像](media/azure-stack-tutorial-tenant-vm/image09.png)

## <a name="add-an-image"></a><span data-ttu-id="09e14-168">新增映像</span><span class="sxs-lookup"><span data-stu-id="09e14-168">Add an image</span></span>

<span data-ttu-id="09e14-169">佈建虛擬機器之前，您必須新增一張影像到 Azure Stack 市集。</span><span class="sxs-lookup"><span data-stu-id="09e14-169">Before you can provision virtual machines, you must add an image to the Azure Stack marketplace.</span></span> <span data-ttu-id="09e14-170">您可以從 Azure Marketplace 新增您選擇的影像，包括 Linux 影像。</span><span class="sxs-lookup"><span data-stu-id="09e14-170">You can add the image of your choice, including Linux images, from the Azure Marketplace.</span></span>

<span data-ttu-id="09e14-171">若您是在已連結情節中作業，且您已向 Azure 註冊 Azure Stack 執行個體，您可以使用[從 Azure 下載 項目到 Azure Stack](azure-stack-download-azure-marketplace-item.md) 主題中所述的步驟，從 Azure Marketplace 下載 Windows Server 2016 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="09e14-171">If you are operating in a connected scenario and if you have registered your Azure Stack instance with Azure, then you can download the Windows Server 2016 VM image from the Azure Marketplace by using the steps described in the [Download marketplace items from Azure to Azure Stack](azure-stack-download-azure-marketplace-item.md) topic.</span></span>

<span data-ttu-id="09e14-172">如需有關將不同項目新增到 Marketplace 的資訊，請參閱 [Azure Stack Marketplace](azure-stack-marketplace.md)。</span><span class="sxs-lookup"><span data-stu-id="09e14-172">For information about adding different items to the marketplace, see [The Azure Stack Marketplace](azure-stack-marketplace.md).</span></span>

## <a name="test-the-offer"></a><span data-ttu-id="09e14-173">測試供應項目</span><span class="sxs-lookup"><span data-stu-id="09e14-173">Test the offer</span></span>

<span data-ttu-id="09e14-174">既然您已經建立供應項目，您可以進行測試。</span><span class="sxs-lookup"><span data-stu-id="09e14-174">Now that you’ve created an offer, you can test it.</span></span> <span data-ttu-id="09e14-175">以使用者身分登入並訂閱該供應項目，然後新增虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="09e14-175">Log in as a user and subscribe to the offer and then add a virtual machine.</span></span>

1. <span data-ttu-id="09e14-176">**訂閱提供項目**</span><span class="sxs-lookup"><span data-stu-id="09e14-176">**Subscribe to an offer**</span></span>

   <span data-ttu-id="09e14-177">現在您能以使用者身分登入到入口網站，以訂閱供應項目。</span><span class="sxs-lookup"><span data-stu-id="09e14-177">Now you can log in to the portal as a user to subscribe to an offer.</span></span>

   <span data-ttu-id="09e14-178">a.</span><span class="sxs-lookup"><span data-stu-id="09e14-178">a.</span></span> <span data-ttu-id="09e14-179">在 Azure Stack 開發套件電腦上，以使用者身分登入 `https://portal.local.azurestack.external`，然後按一下 [取得訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="09e14-179">On the Azure Stack Deployment Kit computer, log in to `https://portal.local.azurestack.external` as a user and click **Get a Subscription**.</span></span>

   ![取得訂用帳戶](media/azure-stack-subscribe-plan-provision-vm/image01.png)

   <span data-ttu-id="09e14-181">b.</span><span class="sxs-lookup"><span data-stu-id="09e14-181">b.</span></span> <span data-ttu-id="09e14-182">在 [顯示名稱] 欄位中，輸入您的訂閱名稱，按一下 [供應項目]，按一下 [選擇供應項目] 區段中的其中一個供應項目，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="09e14-182">In the **Display Name** field, type a name for your subscription, click **Offer**, click one of the offers in the **Choose an offer** section, and then click **Create**.</span></span>

   ![建立優惠](media/azure-stack-subscribe-plan-provision-vm/image02.png)

   <span data-ttu-id="09e14-184">c.</span><span class="sxs-lookup"><span data-stu-id="09e14-184">c.</span></span> <span data-ttu-id="09e14-185">若要檢視您建立的訂用帳戶，請按一下 [更多服務]、按一下 [訂用帳戶]，然後按一下您的新訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="09e14-185">To view the subscription you created, click **More services**, click **Subscriptions**, then click your new subscription.</span></span>  

   <span data-ttu-id="09e14-186">訂閱供應項目之後，請重新整理入口網站以查看哪些服務是新訂用帳戶的一部分。</span><span class="sxs-lookup"><span data-stu-id="09e14-186">After you subscribe to an offer, refresh the portal to see which services are part of the new subscription.</span></span>

2. <span data-ttu-id="09e14-187">**佈建虛擬機器**</span><span class="sxs-lookup"><span data-stu-id="09e14-187">**Provision a virtual machine**</span></span>

   <span data-ttu-id="09e14-188">現在您能以使用者身分登入入口網站，以使用訂用帳戶佈建虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="09e14-188">Now you can log in to the portal as a user to provision a virtual machine using the subscription.</span></span> 

   <span data-ttu-id="09e14-189">a.</span><span class="sxs-lookup"><span data-stu-id="09e14-189">a.</span></span> <span data-ttu-id="09e14-190">在 Azure Stack 開發套件電腦上，以使用者身分登入 `https://portal.local.azurestack.external`，然後按一下 [新增] > [計算] > [Windows Server 2016 Datacenter 評估版]。</span><span class="sxs-lookup"><span data-stu-id="09e14-190">On the Azure Stack Deployment Kit computer, log in to `https://portal.local.azurestack.external` as a user, and then click **New** > **Compute** > **Windows Server 2016 Datacenter Eval**.</span></span>  

   <span data-ttu-id="09e14-191">b.</span><span class="sxs-lookup"><span data-stu-id="09e14-191">b.</span></span> <span data-ttu-id="09e14-192">在 [基本] 區段中，輸入 [名稱][使用者名稱]與 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="09e14-192">In the **Basics** section, type a **Name**, **User name**, and **Password**.</span></span> <span data-ttu-id="09e14-193">針對 [VM 磁碟類型]，請選擇 [HDD]。</span><span class="sxs-lookup"><span data-stu-id="09e14-193">For **VM disk type**, choose **HDD**.</span></span> <span data-ttu-id="09e14-194">選擇 [訂用帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="09e14-194">Choose a **Subscription**.</span></span> <span data-ttu-id="09e14-195">建立 [資源群組]，或選取現有的資源群組，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="09e14-195">Create a **Resource group**, or select an existing one, and then click **OK**.</span></span>  

   <span data-ttu-id="09e14-196">c.</span><span class="sxs-lookup"><span data-stu-id="09e14-196">c.</span></span> <span data-ttu-id="09e14-197">在 [選擇大小] 區段中，按一下 [A1 基本]，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="09e14-197">In the **Choose a size** section, click **A1 Basic**, and then click **Select**.</span></span>  

   <span data-ttu-id="09e14-198">d.</span><span class="sxs-lookup"><span data-stu-id="09e14-198">d.</span></span> <span data-ttu-id="09e14-199">在 [設定] 區段中，按一下 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="09e14-199">In the **Settings** section, click **Virtual network**.</span></span> <span data-ttu-id="09e14-200">在 [選擇虛擬網路] 區段中，按一下 [建立新項目]。</span><span class="sxs-lookup"><span data-stu-id="09e14-200">In the **Choose virtual network** section, click **Create new**.</span></span> <span data-ttu-id="09e14-201">在 [建立虛擬網路] 區段中，接受所有預設值，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="09e14-201">In the **Create virtual network** section, accept all the defaults, and click **OK**.</span></span> <span data-ttu-id="09e14-202">在 [設定] 區段中，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="09e14-202">In the **Settings** section, click **OK**.</span></span>

   ![建立虛擬網路](media/azure-stack-provision-vm/image04.png)

   <span data-ttu-id="09e14-204">e.</span><span class="sxs-lookup"><span data-stu-id="09e14-204">e.</span></span> <span data-ttu-id="09e14-205">在 [摘要] 區段中，按一下 [確定] 以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="09e14-205">In the **Summary** section, click **OK** to create the virtual machine.</span></span>  

   <span data-ttu-id="09e14-206">f.</span><span class="sxs-lookup"><span data-stu-id="09e14-206">f.</span></span> <span data-ttu-id="09e14-207">若要查看您的新虛擬機器，請按一下 [所有資源]，然後搜尋虛擬機器並按一下其名稱。</span><span class="sxs-lookup"><span data-stu-id="09e14-207">To see your new virtual machine, click **All resources**, then search for the virtual machine and click its name.</span></span>

    ![所有資源](media/azure-stack-provision-vm/image06.png)

<span data-ttu-id="09e14-209">在本教學課程中，您已了解：</span><span class="sxs-lookup"><span data-stu-id="09e14-209">What you learned in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="09e14-210">建立優惠</span><span class="sxs-lookup"><span data-stu-id="09e14-210">Create an offer</span></span>
> * <span data-ttu-id="09e14-211">新增映像</span><span class="sxs-lookup"><span data-stu-id="09e14-211">Add an image</span></span>
> * <span data-ttu-id="09e14-212">測試供應項目</span><span class="sxs-lookup"><span data-stu-id="09e14-212">Test the offer</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="09e14-213">將 Web、行動裝置與 API 應用程式提供給您的 Azure Stack 使用者</span><span class="sxs-lookup"><span data-stu-id="09e14-213">Make web, mobile, and API apps available to your Azure Stack users</span></span>](azure-stack-tutorial-app-service.md)