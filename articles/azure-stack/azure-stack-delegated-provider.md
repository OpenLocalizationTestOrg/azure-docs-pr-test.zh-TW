---
title: "Azure 堆疊中提供 aaaDelegating |Microsoft 文件"
description: "深入了解如何 tooput 其他人負責建立提供項目和註冊為您的使用者。"
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: 157f0207-bddc-42e5-8351-197ec23f9d46
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: alfredop
ms.openlocfilehash: d539cac3ed56f342338c830d95fbec7e93175929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="delegating-offers-in-azure-stack"></a><span data-ttu-id="3378b-103">在 Azure Stack 中委派提供項目</span><span class="sxs-lookup"><span data-stu-id="3378b-103">Delegating offers in Azure Stack</span></span>

<span data-ttu-id="3378b-104">Hello Azure 堆疊雲端操作員，您通常要 tooput 其他人負責建立提供項目和註冊為您的使用者。</span><span class="sxs-lookup"><span data-stu-id="3378b-104">As hello Azure Stack cloud operator, you often want tooput other people in charge of creating offers and signing up users for you.</span></span> <span data-ttu-id="3378b-105">比方說，如果您是服務提供者，而且您想要向上客戶轉銷商 toosign 和代替您管理它們。</span><span class="sxs-lookup"><span data-stu-id="3378b-105">For example, if you are a service provider and you want resellers toosign up customers and manage them on your behalf.</span></span> <span data-ttu-id="3378b-106">它也可以發生在企業中，如果您是一個中央 IT 群組的成員，而且想部門或分公司 toosign 使用者不需要您介入。</span><span class="sxs-lookup"><span data-stu-id="3378b-106">It can also happen in an enterprise if you are part of a central IT group and want divisions or subsidiaries toosign up users without your intervention.</span></span>

<span data-ttu-id="3378b-107">委派，協助您完成這些工作，可幫助您 tooreach 和管理多個使用者與您能 toodo 直接。</span><span class="sxs-lookup"><span data-stu-id="3378b-107">Delegation helps you with these tasks, helping you tooreach and manage more users than you would be able toodo directly.</span></span> <span data-ttu-id="3378b-108">hello 下圖顯示一個層級的委派，但 Azure 堆疊支援多個層級。</span><span class="sxs-lookup"><span data-stu-id="3378b-108">hello following illustration shows one level of delegation, but Azure Stack supports multiple levels.</span></span> <span data-ttu-id="3378b-109">委派的提供者接著可以委派 tooother 提供者，向上 toofive 層級。</span><span class="sxs-lookup"><span data-stu-id="3378b-109">Delegated providers can in turn delegate tooother providers, up toofive levels.</span></span>

![](media/azure-stack-delegated-provider/image1.png)

<span data-ttu-id="3378b-110">Azure 堆疊雲端操作員可以委派 hello 建立優惠和租用戶 tooother 使用者藉由使用 hello 委派功能。</span><span class="sxs-lookup"><span data-stu-id="3378b-110">Azure Stack cloud operators can delegate hello creation of offers and tenants tooother users by using hello delegation functionality.</span></span>

## <a name="roles-and-steps-in-delegation"></a><span data-ttu-id="3378b-111">委派中的角色和步驟</span><span class="sxs-lookup"><span data-stu-id="3378b-111">Roles and steps in delegation</span></span>
<span data-ttu-id="3378b-112">請記住，有三種角色涉及的 toounderstand 委派：</span><span class="sxs-lookup"><span data-stu-id="3378b-112">toounderstand delegation, keep in mind that there are three roles involved:</span></span>

* <span data-ttu-id="3378b-113">hello**雲端操作員**管理 hello Azure 堆疊基礎結構、 建立提供項目範本，並委派給其他人提供它 tootheir 使用者。</span><span class="sxs-lookup"><span data-stu-id="3378b-113">hello **cloud operator** manages hello Azure Stack infrastructure, creates an offer template, and delegates others to offer it tootheir users.</span></span>
* <span data-ttu-id="3378b-114">hello 委派的雲端系統管理員稱為**委派提供者**。</span><span class="sxs-lookup"><span data-stu-id="3378b-114">hello delegated cloud administrators are called **delegated providers**.</span></span> <span data-ttu-id="3378b-115">它們只能隸屬於 tooother 組織 （例如其他 Azure Active Directory 租用戶）。</span><span class="sxs-lookup"><span data-stu-id="3378b-115">They can belong tooother organizations (such as other Azure Active Directory tenants).</span></span>
* <span data-ttu-id="3378b-116">**使用者**申請 hello 優惠，用於管理其工作負載、 建立 Vm、 儲存的資料等。</span><span class="sxs-lookup"><span data-stu-id="3378b-116">**Users** sign up for hello offers and use them for managing their workloads, creating VMs, storing data, etc.</span></span>

<span data-ttu-id="3378b-117">Hello 下列圖片所示，有兩個步驟中設定委派。</span><span class="sxs-lookup"><span data-stu-id="3378b-117">As shown in hello following graphic, there are two steps in setting up delegation.</span></span>

1. <span data-ttu-id="3378b-118">**識別委派的 hello 提供者**訂閱它們 tooan 優惠根據包含 hello 訂用帳戶服務的計劃。</span><span class="sxs-lookup"><span data-stu-id="3378b-118">**Identify hello delegated providers** by subscribing them tooan offer based on a plan that contains only hello subscriptions service.</span></span>
   <span data-ttu-id="3378b-119">訂閱 toothis 優惠的使用者取得部份 hello 雲端系統管理員的功能，包括 hello 能力 tooextend 優惠和符號使用者註冊它們。</span><span class="sxs-lookup"><span data-stu-id="3378b-119">Users who subscribe toothis offer acquire some of hello cloud administrator’s capabilities, including hello ability tooextend offers and sign users up for them.</span></span>
2. <span data-ttu-id="3378b-120">**委派優惠 toohello 委派提供者**，這項優惠做為範本的可以提供什麼 hello 委派的提供者。</span><span class="sxs-lookup"><span data-stu-id="3378b-120">**Delegate an offer toohello delegated provider**, this offer functions as a template for what hello delegated provider can offer.</span></span> <span data-ttu-id="3378b-121">hello 委派的提供者就能 tootake hello 供應項目、 選擇的名稱 （但不是會變更其服務和配額），並提供它 toocustomers。</span><span class="sxs-lookup"><span data-stu-id="3378b-121">hello delegated provider is now able tootake hello offer, choose a name for it (but not change its services and quotas), and offer it toocustomers.</span></span>

![](media/azure-stack-delegated-provider/image2.png)

<span data-ttu-id="3378b-122">tooact 作為委派的提供者，使用者需要 tooestablish 關聯性與 hello 主要提供者。也就是說，它們需要 toocreate 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3378b-122">tooact as delegated providers, users need tooestablish a relationship with hello main provider; in other words, they need toocreate a subscription.</span></span> <span data-ttu-id="3378b-123">在此案例中，此訂用帳戶識別為具有 hello 右 toopresent 代表 hello 主要提供者所提供的委派提供者。</span><span class="sxs-lookup"><span data-stu-id="3378b-123">In this scenario, this subscription identifies the delegated providers as having hello right toopresent offers on behalf of hello main provider.</span></span>

<span data-ttu-id="3378b-124">一旦建立此關聯性，hello 雲端操作員可以委派提供 toohello 委派提供者。</span><span class="sxs-lookup"><span data-stu-id="3378b-124">Once this relationship is established, hello cloud operator can delegate an offer toohello delegated provider.</span></span> <span data-ttu-id="3378b-125">hello 委派的提供者就能 tootake hello 供應項目、 將它重新命名 （但不是會變更其內容），並提供它 tooits 客戶。</span><span class="sxs-lookup"><span data-stu-id="3378b-125">hello delegated provider is now able tootake hello offer, rename it (but not change its substance), and offer it tooits customers.</span></span>

<span data-ttu-id="3378b-126">hello 下列各節說明如何 tooestablish 委派的提供者，委派提供項目，並確認使用者可以註冊其。</span><span class="sxs-lookup"><span data-stu-id="3378b-126">hello following sections describe how tooestablish a delegated provider, delegate an offer, and verify that users can sign up for it.</span></span>

## <a name="set-up-roles"></a><span data-ttu-id="3378b-127">設定角色</span><span class="sxs-lookup"><span data-stu-id="3378b-127">Set up roles</span></span>

<span data-ttu-id="3378b-128">toosee 於工作的委派提供者，您需要新增 tooyour 雲端操作員帳戶中的其他 Azure Active Directory 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3378b-128">toosee a delegated provider at work, you need additional Azure Active Directory accounts in addition tooyour cloud operator account.</span></span> <span data-ttu-id="3378b-129">如果您沒有它們，請建立 hello 兩個帳戶。</span><span class="sxs-lookup"><span data-stu-id="3378b-129">If you do not have them, create hello two accounts.</span></span> <span data-ttu-id="3378b-130">hello 帳戶只能隸屬於 tooany AAD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="3378b-130">hello accounts can belong tooany AAD tenant.</span></span> <span data-ttu-id="3378b-131">我們會參考 toothem，如 hello 委派提供者 (DP) 和 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="3378b-131">We refer toothem as hello delegated provider (DP) and hello user.</span></span>

| <span data-ttu-id="3378b-132">**角色**</span><span class="sxs-lookup"><span data-stu-id="3378b-132">**Role**</span></span> | <span data-ttu-id="3378b-133">**組織的權限**</span><span class="sxs-lookup"><span data-stu-id="3378b-133">**Organizational rights**</span></span> |
| --- | --- |
| <span data-ttu-id="3378b-134">委派的提供者</span><span class="sxs-lookup"><span data-stu-id="3378b-134">Delegated Provider</span></span> |<span data-ttu-id="3378b-135">User</span><span class="sxs-lookup"><span data-stu-id="3378b-135">User</span></span> |
| <span data-ttu-id="3378b-136">User</span><span class="sxs-lookup"><span data-stu-id="3378b-136">User</span></span> |<span data-ttu-id="3378b-137">User</span><span class="sxs-lookup"><span data-stu-id="3378b-137">User</span></span> |

## <a name="identify-hello-delegated-providers"></a><span data-ttu-id="3378b-138">識別委派的 hello 提供者</span><span class="sxs-lookup"><span data-stu-id="3378b-138">Identify hello delegated providers</span></span>
1. <span data-ttu-id="3378b-139">以雲端操作員身分登入。</span><span class="sxs-lookup"><span data-stu-id="3378b-139">Sign in as cloud operator.</span></span>
2. <span data-ttu-id="3378b-140">建立 hello 供應項目可讓使用者委派 toobecome 提供者。</span><span class="sxs-lookup"><span data-stu-id="3378b-140">Create hello offer that enables users toobecome delegated providers.</span></span> <span data-ttu-id="3378b-141">這需要您根據它建立方案和供應項目：</span><span class="sxs-lookup"><span data-stu-id="3378b-141">This requires that you create a plan and an offer based on it:</span></span>
   
   <span data-ttu-id="3378b-142">a.</span><span class="sxs-lookup"><span data-stu-id="3378b-142">a.</span></span>  <span data-ttu-id="3378b-143">[建立方案](azure-stack-create-plan.md)。</span><span class="sxs-lookup"><span data-stu-id="3378b-143">[Create a plan](azure-stack-create-plan.md).</span></span>
       <span data-ttu-id="3378b-144">這個計畫應該包括 hello 訂閱服務。</span><span class="sxs-lookup"><span data-stu-id="3378b-144">This plan should include only hello subscriptions service.</span></span> <span data-ttu-id="3378b-145">在本文章中，我們會使用名為 PlanForDelegation 的方案。</span><span class="sxs-lookup"><span data-stu-id="3378b-145">In this article, we use a plan called PlanForDelegation.</span></span>
   
   <span data-ttu-id="3378b-146">b.</span><span class="sxs-lookup"><span data-stu-id="3378b-146">b.</span></span>  <span data-ttu-id="3378b-147">根據此方案[建立供應項目](azure-stack-create-offer.md)。</span><span class="sxs-lookup"><span data-stu-id="3378b-147">[Create an offer](azure-stack-create-offer.md) based on this plan.</span></span> <span data-ttu-id="3378b-148">在本文章中，我們會使用名為 OfferToDP 的供應項目。</span><span class="sxs-lookup"><span data-stu-id="3378b-148">In this article, we use an offer called OfferToDP.</span></span>
   
   <span data-ttu-id="3378b-149">c.</span><span class="sxs-lookup"><span data-stu-id="3378b-149">c.</span></span>  <span data-ttu-id="3378b-150">Hello 優惠 hello 建立完成之後，請加入 hello 委派提供者做訂閱者 toothis 供應項目，即可**訂閱** &gt; **新增** &gt; **新增租用戶訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="3378b-150">Once hello creation of hello offer is complete, add hello delegated provider as a subscriber toothis offer by clicking **Subscriptions** &gt; **Add** &gt; **New Tenant Subscription**.</span></span>
   
   ![](media/azure-stack-delegated-provider/image3.png)

> [!NOTE]
> <span data-ttu-id="3378b-151">因為所有 Azure 堆疊優惠，您都需要 hello 選項製作 hello 優惠公用，讓使用者註冊，或讓它維持在私用，而且都擁有 hello 雲端操作員管理 hello 註冊。</span><span class="sxs-lookup"><span data-stu-id="3378b-151">As with all Azure Stack offers, you have hello option of making hello offer public and letting users sign up for it, or keeping it private and have hello cloud operator manage hello sign-up.</span></span> <span data-ttu-id="3378b-152">委派的提供者通常是一小群，而且您想 toocontrol 人員就會准許 tooit，所以在大部分情況下保留這項優惠私人意義。</span><span class="sxs-lookup"><span data-stu-id="3378b-152">Delegated providers are usually a small group and you want toocontrol who is admitted tooit, so keeping this offer private makes sense in most cases.</span></span>
> 
> 

## <a name="cloud-operator-creates-hello-delegated-offer"></a><span data-ttu-id="3378b-153">雲端操作員建立 hello 委派的優惠</span><span class="sxs-lookup"><span data-stu-id="3378b-153">Cloud operator creates hello delegated offer</span></span>

<span data-ttu-id="3378b-154">您現在已建立您的委派提供者。</span><span class="sxs-lookup"><span data-stu-id="3378b-154">You have now established your delegated provider.</span></span> <span data-ttu-id="3378b-155">hello 下一個步驟是建立 hello 計劃，並提供您將 toodelegate，並將會使用您的客戶。</span><span class="sxs-lookup"><span data-stu-id="3378b-155">hello next step is to create hello plan and offer that you are going toodelegate, and which your customers will use.</span></span> <span data-ttu-id="3378b-156">您應該完全依照您想要客戶 toosee 定義這項優惠，因為 hello 委派提供者將無法變更 hello 計劃和它所包含的配額。</span><span class="sxs-lookup"><span data-stu-id="3378b-156">You should define this offer exactly as you want the customers toosee it, because hello delegated provider will not be able to change hello plans and quotas it includes.</span></span>

1. <span data-ttu-id="3378b-157">身為雲端操作員，請根據它[建立方案](azure-stack-create-plan.md)和[供應項目](azure-stack-create-offer.md)。</span><span class="sxs-lookup"><span data-stu-id="3378b-157">As cloud operator, [create a plan](azure-stack-create-plan.md) and [an offer](azure-stack-create-offer.md) based on it.</span></span> <span data-ttu-id="3378b-158">在本文章中，我們會使用名為 DelegatedOffer 的供應項目。</span><span class="sxs-lookup"><span data-stu-id="3378b-158">For this article, we use an offer called DelegatedOffer.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3378b-159">這項優惠沒有 toobe 公用。</span><span class="sxs-lookup"><span data-stu-id="3378b-159">This offer does not have toobe public.</span></span> <span data-ttu-id="3378b-160">可以設為公用，如果您選擇，但在大部分情況下，您只要委派提供者 toohave 存取 tooit。</span><span class="sxs-lookup"><span data-stu-id="3378b-160">It can be made public if you choose, but, in most cases, you only want delegated providers toohave access tooit.</span></span> <span data-ttu-id="3378b-161">一旦 hello 步驟中所述，您可以委派私人優惠，hello 委派提供者就會具有存取 tooit。</span><span class="sxs-lookup"><span data-stu-id="3378b-161">Once you delegate a private offer as described in hello following steps, hello delegated provider has access tooit.</span></span>
   > 
   > 
1. <span data-ttu-id="3378b-162">委派 hello 供應項目。</span><span class="sxs-lookup"><span data-stu-id="3378b-162">Delegate hello offer.</span></span> <span data-ttu-id="3378b-163">移 tooDelegatedOffer，然後在 hello 設定 窗格中，按一下**委派的提供者** &gt; **新增**。</span><span class="sxs-lookup"><span data-stu-id="3378b-163">Go tooDelegatedOffer, and in hello Settings pane, click **Delegated Providers** &gt; **Add**.</span></span>
2. <span data-ttu-id="3378b-164">從 [hello] 下拉式清單方塊選取 hello 委派提供者的訂用帳戶，然後按一下**委派**。</span><span class="sxs-lookup"><span data-stu-id="3378b-164">Select hello delegated provider’s subscription from hello drop-down list box and click **Delegate**.</span></span>

> ![](media/azure-stack-delegated-provider/image4.png)
> 
> 

## <a name="delegated-provider-customizes-hello-offer"></a><span data-ttu-id="3378b-165">委派的提供者會自訂 hello 供應項目</span><span class="sxs-lookup"><span data-stu-id="3378b-165">Delegated provider customizes hello offer</span></span>

<span data-ttu-id="3378b-166">登入 toohello**租用戶入口網站**為 hello 委派 提供者，並建立新的優惠使用 hello 委派供應項目做為範本。</span><span class="sxs-lookup"><span data-stu-id="3378b-166">Sign in toohello **tenant portal** as hello delegated provider and create a new offer using hello delegated offer as a template.</span></span>

1. <span data-ttu-id="3378b-167">按一下 [新增] &gt; [租用戶供應項目 + 方案] &gt; [提供]。</span><span class="sxs-lookup"><span data-stu-id="3378b-167">Click **New** &gt; **Tenant Offers + Plans** &gt; **Offer**.</span></span>

    ![](media/azure-stack-delegated-provider/image5.png)


1. <span data-ttu-id="3378b-168">指派名稱 toohello 供應項目。</span><span class="sxs-lookup"><span data-stu-id="3378b-168">Assign a name toohello offer.</span></span> <span data-ttu-id="3378b-169">這裡我們選擇 ResellerOffer。</span><span class="sxs-lookup"><span data-stu-id="3378b-169">Here we choose ResellerOffer.</span></span> <span data-ttu-id="3378b-170">它在然後按一下，選取 hello 委派優惠 toobase**建立**。</span><span class="sxs-lookup"><span data-stu-id="3378b-170">Select hello delegated offer toobase it on and then click **Create**.</span></span>
   
   ![](media/azure-stack-delegated-provider/image6.png)

    >[!NOTE] 
    > <span data-ttu-id="3378b-171">請注意 hello 差異比較 toooffer 建立為經驗豐富的 hello 雲端操作員。</span><span class="sxs-lookup"><span data-stu-id="3378b-171">Note hello difference compared toooffer creation as experienced by hello cloud operator.</span></span> <span data-ttu-id="3378b-172">hello 委派提供者不會建構基底的計劃和附加元件的計畫 hello 提供項目他們可以只選擇已被委派的 toothem，其供應項目，無法進行變更 toothose 優惠。</span><span class="sxs-lookup"><span data-stu-id="3378b-172">hello delegated provider does not construct hello offer from base plans and add-on plans; they can only choose from offers that have been delegated toothem, and can't make changes toothose offers.</span></span>

1. <span data-ttu-id="3378b-173">依序按一下公開提供的 hello**瀏覽** &gt; **提供**、 選取 hello 供應項目，並按一下**狀態變更**。</span><span class="sxs-lookup"><span data-stu-id="3378b-173">Make hello offer public by clicking **Browse** &gt; **Offers**, selecting hello offer, and clicking **Change State**.</span></span>
2. <span data-ttu-id="3378b-174">hello 委派提供者會公開這些提供項目透過自己的入口網站 URL。</span><span class="sxs-lookup"><span data-stu-id="3378b-174">hello delegated provider exposes these offers through their own portal URL.</span></span> <span data-ttu-id="3378b-175">這些提供項目是只能透過 hello 委派入口網站顯示。</span><span class="sxs-lookup"><span data-stu-id="3378b-175">These offers are visible only through hello delegated portal.</span></span> <span data-ttu-id="3378b-176">toofind 及變更此 URL:</span><span class="sxs-lookup"><span data-stu-id="3378b-176">toofind and change this URL:</span></span>
   
    <span data-ttu-id="3378b-177">a.</span><span class="sxs-lookup"><span data-stu-id="3378b-177">a.</span></span>  <span data-ttu-id="3378b-178">按一下**瀏覽**&gt; **更多服務**&gt; **訂閱**&gt;選取 hello 委派提供者的訂閱，在我們的案例其*DPSubscription* &gt; **屬性**。</span><span class="sxs-lookup"><span data-stu-id="3378b-178">Click **Browse**&gt; **More services**&gt; **Subscriptions**&gt; Select hello delegated provider subscription, in our case its *DPSubscription*&gt; **Properties**.</span></span>
   
    <span data-ttu-id="3378b-179">b.</span><span class="sxs-lookup"><span data-stu-id="3378b-179">b.</span></span>  <span data-ttu-id="3378b-180">將複製 hello 入口網站 URL tooa 不同的位置，例如 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="3378b-180">Copy hello portal URL tooa separate location, such as Notepad.</span></span>
   
    ![](media/azure-stack-delegated-provider/dpportaluri.png)  
   
   <span data-ttu-id="3378b-181">您現在已完成將建立的委派提供 hello 做為委派的提供者。</span><span class="sxs-lookup"><span data-stu-id="3378b-181">You have now completed hello creation of a delegated offer as a delegated provider.</span></span> <span data-ttu-id="3378b-182">因為 hello 委派的提供者，請先登出。</span><span class="sxs-lookup"><span data-stu-id="3378b-182">Sign out as hello delegated provider.</span></span> <span data-ttu-id="3378b-183">關閉已在使用您的 hello 瀏覽器索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3378b-183">Close hello browser tab you have been using.</span></span>

## <a name="sign-up-for-hello-offer"></a><span data-ttu-id="3378b-184">註冊 hello 優惠</span><span class="sxs-lookup"><span data-stu-id="3378b-184">Sign up for hello offer</span></span>
1. <span data-ttu-id="3378b-185">在新的瀏覽器視窗中，移 toohello 委派入口網站在 hello 先前步驟所儲存的 URL。</span><span class="sxs-lookup"><span data-stu-id="3378b-185">In a new browser window, go toohello delegated portal URL you saved in hello previous step.</span></span> <span data-ttu-id="3378b-186">使用者身分登入 toohello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="3378b-186">Sign in toohello portal as user.</span></span> <span data-ttu-id="3378b-187">注意： 使用 hello 委派此步驟中的入口網站。</span><span class="sxs-lookup"><span data-stu-id="3378b-187">Note: Use hello delegated portal for this step.</span></span> <span data-ttu-id="3378b-188">hello 委派的優惠否則不可見。</span><span class="sxs-lookup"><span data-stu-id="3378b-188">hello delegated offer are not visible otherwise.</span></span>
2. <span data-ttu-id="3378b-189">在 hello 儀表板中，按一下 **取得訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="3378b-189">In hello dashboard, click **Get a subscription**.</span></span> <span data-ttu-id="3378b-190">您會看到只 hello 委派提供者所建立的委派 hello 提供會呈現 toohello 使用者：</span><span class="sxs-lookup"><span data-stu-id="3378b-190">You will see that only hello delegated offers created by hello delegated provider are presented toohello user:</span></span>

> ![](media/azure-stack-delegated-provider/image8.png)
> 
> 

<span data-ttu-id="3378b-191">這總結 hello 程序的供應項目委派。</span><span class="sxs-lookup"><span data-stu-id="3378b-191">This concludes hello process of offer delegation.</span></span> <span data-ttu-id="3378b-192">hello 使用者可以立即註冊這項優惠的訂用帳戶取得。</span><span class="sxs-lookup"><span data-stu-id="3378b-192">hello user can now sign up for this offer by getting a subscription for it.</span></span>

## <a name="multiple-tier-delegation"></a><span data-ttu-id="3378b-193">多層委派</span><span class="sxs-lookup"><span data-stu-id="3378b-193">Multiple-tier delegation</span></span>

<span data-ttu-id="3378b-194">多層式委派可讓委派 hello 提供者 toodelegate 優惠 tooother 實體。</span><span class="sxs-lookup"><span data-stu-id="3378b-194">Multiple-tier delegation allows hello delegated provider toodelegate the offer tooother entities.</span></span> <span data-ttu-id="3378b-195">這可讓，比方說，更深入的轉售商通道中的 hello 管理 Azure 堆疊提供者委派優惠 tooa 散發者，後者會委派 tooreseller 人員 hello 建立。</span><span class="sxs-lookup"><span data-stu-id="3378b-195">This allows, for example, hello creation of deeper reseller channels, in which hello provider managing Azure Stack delegates an offer tooa distributor, who in turn delegates tooreseller.</span></span>
<span data-ttu-id="3378b-196">Azure 」 堆疊支援向上 toofive 層級的委派。</span><span class="sxs-lookup"><span data-stu-id="3378b-196">Azure Stack supports up toofive levels of delegation.</span></span>

<span data-ttu-id="3378b-197">toocreate 多個階層提供委派，後者會 hello 委派提供者委派 hello 提供 toohello 下一個提供者。</span><span class="sxs-lookup"><span data-stu-id="3378b-197">toocreate multiple tiers of offer delegation, hello delegated provider in turn delegates hello offer toohello next provider.</span></span> <span data-ttu-id="3378b-198">hello 程序是 hello 相同 hello 委派提供者而 hello 雲端操作員 (請參閱[雲端操作員建立 hello 委派的優惠](#cloud-operator-creates-the-delegated-offer))。</span><span class="sxs-lookup"><span data-stu-id="3378b-198">hello process is hello same for hello delegated provider as it was for hello cloud operator (see [Cloud operator creates hello delegated offer](#cloud-operator-creates-the-delegated-offer)).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3378b-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3378b-199">Next steps</span></span>
[<span data-ttu-id="3378b-200">佈建 VM</span><span class="sxs-lookup"><span data-stu-id="3378b-200">Provision a VM</span></span>](azure-stack-provision-vm.md)

