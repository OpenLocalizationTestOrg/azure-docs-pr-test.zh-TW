---
title: "在 Azure Stack 中委派供應項目 | Microsoft Docs"
description: "了解如何讓其他人負責建立供應項目和為您註冊使用者。"
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
ms.openlocfilehash: c56c0669cbcd66fe1d7177846e02ba28838c0544
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="delegating-offers-in-azure-stack"></a><span data-ttu-id="95d72-103">在 Azure Stack 中委派提供項目</span><span class="sxs-lookup"><span data-stu-id="95d72-103">Delegating offers in Azure Stack</span></span>

<span data-ttu-id="95d72-104">身為 Azure Stack 雲端操作員，您往往想要了解如何讓其他人負責建立供應項目和為您註冊使用者。</span><span class="sxs-lookup"><span data-stu-id="95d72-104">As the Azure Stack cloud operator, you often want to put other people in charge of creating offers and signing up users for you.</span></span> <span data-ttu-id="95d72-105">例如，如果您是服務提供者，並且想要轉銷商註冊客戶並代表您管理客戶。</span><span class="sxs-lookup"><span data-stu-id="95d72-105">For example, if you are a service provider and you want resellers to sign up customers and manage them on your behalf.</span></span> <span data-ttu-id="95d72-106">如果您是中央 IT 群組的一部分，而且想要部門或子公司在不需要您介入的情況下註冊使用者，則在企業中也可能發生。</span><span class="sxs-lookup"><span data-stu-id="95d72-106">It can also happen in an enterprise if you are part of a central IT group and want divisions or subsidiaries to sign up users without your intervention.</span></span>

<span data-ttu-id="95d72-107">委派可協助您進行這些工作，協助您連接和管理超過您自己可直接管理數量的使用者。</span><span class="sxs-lookup"><span data-stu-id="95d72-107">Delegation helps you with these tasks, helping you to reach and manage more users than you would be able to do directly.</span></span> <span data-ttu-id="95d72-108">下圖顯示一個層級的委派，但 Azure Stack 支援多個層級。</span><span class="sxs-lookup"><span data-stu-id="95d72-108">The following illustration shows one level of delegation, but Azure Stack supports multiple levels.</span></span> <span data-ttu-id="95d72-109">委派的提供者可以依次委派給其他提供者，最多五個層級。</span><span class="sxs-lookup"><span data-stu-id="95d72-109">Delegated providers can in turn delegate to other providers, up to five levels.</span></span>

![](media/azure-stack-delegated-provider/image1.png)

<span data-ttu-id="95d72-110">Azure Stack 雲端操作員可以藉由使用委派功能，將供應項目和租用戶的建立委派給其他使用者。</span><span class="sxs-lookup"><span data-stu-id="95d72-110">Azure Stack cloud operators can delegate the creation of offers and tenants to other users by using the delegation functionality.</span></span>

## <a name="roles-and-steps-in-delegation"></a><span data-ttu-id="95d72-111">委派中的角色和步驟</span><span class="sxs-lookup"><span data-stu-id="95d72-111">Roles and steps in delegation</span></span>
<span data-ttu-id="95d72-112">若要了解委派，請記住，這牽涉到三個角色：</span><span class="sxs-lookup"><span data-stu-id="95d72-112">To understand delegation, keep in mind that there are three roles involved:</span></span>

* <span data-ttu-id="95d72-113">**雲端操作員**會管理 Azure Stack 基礎結構、建立供應項目範本，並委派其他人來提供給使用者。</span><span class="sxs-lookup"><span data-stu-id="95d72-113">The **cloud operator** manages the Azure Stack infrastructure, creates an offer template, and delegates others to offer it to their users.</span></span>
* <span data-ttu-id="95d72-114">委派的雲端系統管理員稱為**委派提供者**。</span><span class="sxs-lookup"><span data-stu-id="95d72-114">The delegated cloud administrators are called **delegated providers**.</span></span> <span data-ttu-id="95d72-115">他們可以隸屬於其他組織 (例如其他 Azure Active Directory 租用戶)。</span><span class="sxs-lookup"><span data-stu-id="95d72-115">They can belong to other organizations (such as other Azure Active Directory tenants).</span></span>
* <span data-ttu-id="95d72-116">**使用者**註冊使用供應項目，並用它們來管理其工作負載、建立 VM、儲存資料等等。</span><span class="sxs-lookup"><span data-stu-id="95d72-116">**Users** sign up for the offers and use them for managing their workloads, creating VMs, storing data, etc.</span></span>

<span data-ttu-id="95d72-117">如下圖所示，設定委派有兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="95d72-117">As shown in the following graphic, there are two steps in setting up delegation.</span></span>

1. <span data-ttu-id="95d72-118">**識別委派的提供者**：根據僅包含訂用帳戶服務的方案，讓委派的提供者訂閱供應項目。</span><span class="sxs-lookup"><span data-stu-id="95d72-118">**Identify the delegated providers** by subscribing them to an offer based on a plan that contains only the subscriptions service.</span></span>
   <span data-ttu-id="95d72-119">這項優惠訂閱的使用者取得部份雲端系統管理員的功能，包括擴充優惠和登入使用者註冊他們的能力。</span><span class="sxs-lookup"><span data-stu-id="95d72-119">Users who subscribe to this offer acquire some of the cloud administrator’s capabilities, including the ability to extend offers and sign users up for them.</span></span>
2. <span data-ttu-id="95d72-120">**向委派的提供者委派供應項目**：此供應項目可做為委派的提供者可提供項目的範本。</span><span class="sxs-lookup"><span data-stu-id="95d72-120">**Delegate an offer to the delegated provider**, this offer functions as a template for what the delegated provider can offer.</span></span> <span data-ttu-id="95d72-121">委派的提供者現在就可以取得供應項目、為其選擇名稱 (但不能變更其服務和配額)，並提供給客戶。</span><span class="sxs-lookup"><span data-stu-id="95d72-121">The delegated provider is now able to take the offer, choose a name for it (but not change its services and quotas), and offer it to customers.</span></span>

![](media/azure-stack-delegated-provider/image2.png)

<span data-ttu-id="95d72-122">若要做為委派的提供者，使用者必須與主要提供者建立關係；也就是說，他們必須建立訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="95d72-122">To act as delegated providers, users need to establish a relationship with the main provider; in other words, they need to create a subscription.</span></span> <span data-ttu-id="95d72-123">在此案例中，此訂用帳戶會將委派提供者識別為具有權限可代表主要提供者呈現供應項目。</span><span class="sxs-lookup"><span data-stu-id="95d72-123">In this scenario, this subscription identifies the delegated providers as having the right to present offers on behalf of the main provider.</span></span>

<span data-ttu-id="95d72-124">建立此關聯性之後，雲端操作員即可委派供應項目給委派的提供者。</span><span class="sxs-lookup"><span data-stu-id="95d72-124">Once this relationship is established, the cloud operator can delegate an offer to the delegated provider.</span></span> <span data-ttu-id="95d72-125">委派的提供者現在就可以取得供應項目、為其重新命名 (但不能變更其本質)，並提供給客戶。</span><span class="sxs-lookup"><span data-stu-id="95d72-125">The delegated provider is now able to take the offer, rename it (but not change its substance), and offer it to its customers.</span></span>

<span data-ttu-id="95d72-126">下列章節描述如何建立委派的提供者、委派供應項目，以及確認使用者可以註冊使用它。</span><span class="sxs-lookup"><span data-stu-id="95d72-126">The following sections describe how to establish a delegated provider, delegate an offer, and verify that users can sign up for it.</span></span>

## <a name="set-up-roles"></a><span data-ttu-id="95d72-127">設定角色</span><span class="sxs-lookup"><span data-stu-id="95d72-127">Set up roles</span></span>

<span data-ttu-id="95d72-128">若要查看工作的委派提供者，除了您的雲端操作員帳戶，您需要額外的 Azure Active Directory 帳戶。</span><span class="sxs-lookup"><span data-stu-id="95d72-128">To see a delegated provider at work, you need additional Azure Active Directory accounts in addition to your cloud operator account.</span></span> <span data-ttu-id="95d72-129">如果您沒有帳戶，請建立兩個帳戶。</span><span class="sxs-lookup"><span data-stu-id="95d72-129">If you do not have them, create the two accounts.</span></span> <span data-ttu-id="95d72-130">帳戶可以屬於任何 AAD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="95d72-130">The accounts can belong to any AAD tenant.</span></span> <span data-ttu-id="95d72-131">我們將它們稱為委派的提供者 (DP) 和使用者。</span><span class="sxs-lookup"><span data-stu-id="95d72-131">We refer to them as the delegated provider (DP) and the user.</span></span>

| <span data-ttu-id="95d72-132">**角色**</span><span class="sxs-lookup"><span data-stu-id="95d72-132">**Role**</span></span> | <span data-ttu-id="95d72-133">**組織的權限**</span><span class="sxs-lookup"><span data-stu-id="95d72-133">**Organizational rights**</span></span> |
| --- | --- |
| <span data-ttu-id="95d72-134">委派的提供者</span><span class="sxs-lookup"><span data-stu-id="95d72-134">Delegated Provider</span></span> |<span data-ttu-id="95d72-135">User</span><span class="sxs-lookup"><span data-stu-id="95d72-135">User</span></span> |
| <span data-ttu-id="95d72-136">User</span><span class="sxs-lookup"><span data-stu-id="95d72-136">User</span></span> |<span data-ttu-id="95d72-137">User</span><span class="sxs-lookup"><span data-stu-id="95d72-137">User</span></span> |

## <a name="identify-the-delegated-providers"></a><span data-ttu-id="95d72-138">識別委派的提供者</span><span class="sxs-lookup"><span data-stu-id="95d72-138">Identify the delegated providers</span></span>
1. <span data-ttu-id="95d72-139">以雲端操作員身分登入。</span><span class="sxs-lookup"><span data-stu-id="95d72-139">Sign in as cloud operator.</span></span>
2. <span data-ttu-id="95d72-140">建立可讓使用者成為委派提供者的供應項目。</span><span class="sxs-lookup"><span data-stu-id="95d72-140">Create the offer that enables users to become delegated providers.</span></span> <span data-ttu-id="95d72-141">這需要您根據它建立方案和供應項目：</span><span class="sxs-lookup"><span data-stu-id="95d72-141">This requires that you create a plan and an offer based on it:</span></span>
   
   <span data-ttu-id="95d72-142">a.</span><span class="sxs-lookup"><span data-stu-id="95d72-142">a.</span></span>  <span data-ttu-id="95d72-143">[建立方案](azure-stack-create-plan.md)。</span><span class="sxs-lookup"><span data-stu-id="95d72-143">[Create a plan](azure-stack-create-plan.md).</span></span>
       <span data-ttu-id="95d72-144">此方案應該僅包含訂閱服務。</span><span class="sxs-lookup"><span data-stu-id="95d72-144">This plan should include only the subscriptions service.</span></span> <span data-ttu-id="95d72-145">在本文章中，我們會使用名為 PlanForDelegation 的方案。</span><span class="sxs-lookup"><span data-stu-id="95d72-145">In this article, we use a plan called PlanForDelegation.</span></span>
   
   <span data-ttu-id="95d72-146">b.</span><span class="sxs-lookup"><span data-stu-id="95d72-146">b.</span></span>  <span data-ttu-id="95d72-147">根據此方案[建立供應項目](azure-stack-create-offer.md)。</span><span class="sxs-lookup"><span data-stu-id="95d72-147">[Create an offer](azure-stack-create-offer.md) based on this plan.</span></span> <span data-ttu-id="95d72-148">在本文章中，我們會使用名為 OfferToDP 的供應項目。</span><span class="sxs-lookup"><span data-stu-id="95d72-148">In this article, we use an offer called OfferToDP.</span></span>
   
   <span data-ttu-id="95d72-149">c.</span><span class="sxs-lookup"><span data-stu-id="95d72-149">c.</span></span>  <span data-ttu-id="95d72-150">供應項目的建立完成之後，請將委派的提供者新增為此供應項目的訂閱者，方法是依序按一下 [訂閱] &gt; [新增] &gt; [新的租用戶訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="95d72-150">Once the creation of the offer is complete, add the delegated provider as a subscriber to this offer by clicking **Subscriptions** &gt; **Add** &gt; **New Tenant Subscription**.</span></span>
   
   ![](media/azure-stack-delegated-provider/image3.png)

> [!NOTE]
> <span data-ttu-id="95d72-151">如同所有 Azure Stack 供應項目，您可以選擇讓供應項目公開並讓使用者註冊使用它，或是讓它保持在私人並由雲端操作員管理註冊。</span><span class="sxs-lookup"><span data-stu-id="95d72-151">As with all Azure Stack offers, you have the option of making the offer public and letting users sign up for it, or keeping it private and have the cloud operator manage the sign-up.</span></span> <span data-ttu-id="95d72-152">委派的提供者通常是一個小型群組，而且您想要控制可進入它的成員，所以在大部分情況下讓它保持為私人是有意義的。</span><span class="sxs-lookup"><span data-stu-id="95d72-152">Delegated providers are usually a small group and you want to control who is admitted to it, so keeping this offer private makes sense in most cases.</span></span>
> 
> 

## <a name="cloud-operator-creates-the-delegated-offer"></a><span data-ttu-id="95d72-153">雲端操作員建立委派的供應項目</span><span class="sxs-lookup"><span data-stu-id="95d72-153">Cloud operator creates the delegated offer</span></span>

<span data-ttu-id="95d72-154">您現在已建立您的委派提供者。</span><span class="sxs-lookup"><span data-stu-id="95d72-154">You have now established your delegated provider.</span></span> <span data-ttu-id="95d72-155">下一個步驟是建立您要委派以及您的客戶將會使用的方案和供應項目。</span><span class="sxs-lookup"><span data-stu-id="95d72-155">The next step is to create the plan and offer that you are going to delegate, and which your customers will use.</span></span> <span data-ttu-id="95d72-156">您應該完全依照要客戶看見它的方式定義此供應項目，因為委派的提供者將無法變更方案和它所包含的配額。</span><span class="sxs-lookup"><span data-stu-id="95d72-156">You should define this offer exactly as you want the customers to see it, because the delegated provider will not be able to change the plans and quotas it includes.</span></span>

1. <span data-ttu-id="95d72-157">身為雲端操作員，請根據它[建立方案](azure-stack-create-plan.md)和[供應項目](azure-stack-create-offer.md)。</span><span class="sxs-lookup"><span data-stu-id="95d72-157">As cloud operator, [create a plan](azure-stack-create-plan.md) and [an offer](azure-stack-create-offer.md) based on it.</span></span> <span data-ttu-id="95d72-158">在本文章中，我們會使用名為 DelegatedOffer 的供應項目。</span><span class="sxs-lookup"><span data-stu-id="95d72-158">For this article, we use an offer called DelegatedOffer.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="95d72-159">此供應項目不必是公用。</span><span class="sxs-lookup"><span data-stu-id="95d72-159">This offer does not have to be public.</span></span> <span data-ttu-id="95d72-160">如果您想要可以設為公用，但是在大部分情況下，您只會要委派的提供者可存取它。</span><span class="sxs-lookup"><span data-stu-id="95d72-160">It can be made public if you choose, but, in most cases, you only want delegated providers to have access to it.</span></span> <span data-ttu-id="95d72-161">一旦您如下列步驟所述委派私人供應項目，委派的提供者即可存取它。</span><span class="sxs-lookup"><span data-stu-id="95d72-161">Once you delegate a private offer as described in the following steps, the delegated provider has access to it.</span></span>
   > 
   > 
1. <span data-ttu-id="95d72-162">委派供應項目。</span><span class="sxs-lookup"><span data-stu-id="95d72-162">Delegate the offer.</span></span> <span data-ttu-id="95d72-163">移至 DelegatedOffer，並在 [設定] 窗格中，按一下 [委派的提供者] &gt; [新增]。</span><span class="sxs-lookup"><span data-stu-id="95d72-163">Go to DelegatedOffer, and in the Settings pane, click **Delegated Providers** &gt; **Add**.</span></span>
2. <span data-ttu-id="95d72-164">從下拉式清單方塊選取委派的提供者的訂用帳戶，然後按一下 [委派]。</span><span class="sxs-lookup"><span data-stu-id="95d72-164">Select the delegated provider’s subscription from the drop-down list box and click **Delegate**.</span></span>

> ![](media/azure-stack-delegated-provider/image4.png)
> 
> 

## <a name="delegated-provider-customizes-the-offer"></a><span data-ttu-id="95d72-165">委派的提供者會自訂供應項目</span><span class="sxs-lookup"><span data-stu-id="95d72-165">Delegated provider customizes the offer</span></span>

<span data-ttu-id="95d72-166">以委派的提供者身分登入**租用戶入口網站**，並使用委派的供應項目做為範本建立新的供應項目。</span><span class="sxs-lookup"><span data-stu-id="95d72-166">Sign in to the **tenant portal** as the delegated provider and create a new offer using the delegated offer as a template.</span></span>

1. <span data-ttu-id="95d72-167">按一下 [新增] &gt; [租用戶供應項目 + 方案] &gt; [提供]。</span><span class="sxs-lookup"><span data-stu-id="95d72-167">Click **New** &gt; **Tenant Offers + Plans** &gt; **Offer**.</span></span>

    ![](media/azure-stack-delegated-provider/image5.png)


1. <span data-ttu-id="95d72-168">將名稱指派給供應項目。</span><span class="sxs-lookup"><span data-stu-id="95d72-168">Assign a name to the offer.</span></span> <span data-ttu-id="95d72-169">這裡我們選擇 ResellerOffer。</span><span class="sxs-lookup"><span data-stu-id="95d72-169">Here we choose ResellerOffer.</span></span> <span data-ttu-id="95d72-170">選取要以其為基礎的委派供應項目，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="95d72-170">Select the delegated offer to base it on and then click **Create**.</span></span>
   
   ![](media/azure-stack-delegated-provider/image6.png)

    >[!NOTE] 
    > <span data-ttu-id="95d72-171">請注意相較於雲端操作員所遇到的供應項目建立的差異。</span><span class="sxs-lookup"><span data-stu-id="95d72-171">Note the difference compared to offer creation as experienced by the cloud operator.</span></span> <span data-ttu-id="95d72-172">委派的提供者不會從基礎方案和附加方案建構供應項目；他們只可以從已委派給他們的方案中選擇，並且無法對這些供應項目進行變更。</span><span class="sxs-lookup"><span data-stu-id="95d72-172">The delegated provider does not construct the offer from base plans and add-on plans; they can only choose from offers that have been delegated to them, and can't make changes to those offers.</span></span>

1. <span data-ttu-id="95d72-173">依序按一下[瀏覽] &gt; [供應項目]、選取供應項目，並按一下 [狀態變更] 來讓供應項目公開。</span><span class="sxs-lookup"><span data-stu-id="95d72-173">Make the offer public by clicking **Browse** &gt; **Offers**, selecting the offer, and clicking **Change State**.</span></span>
2. <span data-ttu-id="95d72-174">委派的提供者會透過自己的入口網站 URL 公開這些供應項目。</span><span class="sxs-lookup"><span data-stu-id="95d72-174">The delegated provider exposes these offers through their own portal URL.</span></span> <span data-ttu-id="95d72-175">這些供應項目只會透過委派入口網站顯示。</span><span class="sxs-lookup"><span data-stu-id="95d72-175">These offers are visible only through the delegated portal.</span></span> <span data-ttu-id="95d72-176">若要尋找並變更此 URL：</span><span class="sxs-lookup"><span data-stu-id="95d72-176">To find and change this URL:</span></span>
   
    <span data-ttu-id="95d72-177">a.</span><span class="sxs-lookup"><span data-stu-id="95d72-177">a.</span></span>  <span data-ttu-id="95d72-178">按一下 [瀏覽]&gt; [更多服務]&gt; [訂閱]&gt;選取委派的提供者的訂用帳戶，在我們的案例中，這是 [DPSubscription] &gt; [屬性]。</span><span class="sxs-lookup"><span data-stu-id="95d72-178">Click **Browse**&gt; **More services**&gt; **Subscriptions**&gt; Select the delegated provider subscription, in our case its *DPSubscription*&gt; **Properties**.</span></span>
   
    <span data-ttu-id="95d72-179">b.</span><span class="sxs-lookup"><span data-stu-id="95d72-179">b.</span></span>  <span data-ttu-id="95d72-180">將入口網站 URL 複製到不同的位置，例如：記事本。</span><span class="sxs-lookup"><span data-stu-id="95d72-180">Copy the portal URL to a separate location, such as Notepad.</span></span>
   
    ![](media/azure-stack-delegated-provider/dpportaluri.png)  
   
   <span data-ttu-id="95d72-181">您現在已完成以委派的提供者身分建立委派的供應項目。</span><span class="sxs-lookup"><span data-stu-id="95d72-181">You have now completed the creation of a delegated offer as a delegated provider.</span></span> <span data-ttu-id="95d72-182">以委派的提供者身分登出。</span><span class="sxs-lookup"><span data-stu-id="95d72-182">Sign out as the delegated provider.</span></span> <span data-ttu-id="95d72-183">關閉您已在使用的瀏覽器索引標籤。</span><span class="sxs-lookup"><span data-stu-id="95d72-183">Close the browser tab you have been using.</span></span>

## <a name="sign-up-for-the-offer"></a><span data-ttu-id="95d72-184">註冊取得供應項目</span><span class="sxs-lookup"><span data-stu-id="95d72-184">Sign up for the offer</span></span>
1. <span data-ttu-id="95d72-185">在新瀏覽器視窗中，移至您在上一個步驟中儲存的委派入口網站 URL。</span><span class="sxs-lookup"><span data-stu-id="95d72-185">In a new browser window, go to the delegated portal URL you saved in the previous step.</span></span> <span data-ttu-id="95d72-186">以使用者身分登入入口網站。</span><span class="sxs-lookup"><span data-stu-id="95d72-186">Sign in to the portal as user.</span></span> <span data-ttu-id="95d72-187">附註：對此步驟使用委派的入口網站。</span><span class="sxs-lookup"><span data-stu-id="95d72-187">Note: Use the delegated portal for this step.</span></span> <span data-ttu-id="95d72-188">否則，委派的供應項目會不可見。</span><span class="sxs-lookup"><span data-stu-id="95d72-188">The delegated offer are not visible otherwise.</span></span>
2. <span data-ttu-id="95d72-189">在儀表板中，按一下 [取得訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="95d72-189">In the dashboard, click **Get a subscription**.</span></span> <span data-ttu-id="95d72-190">您會看到只有委派的提供者所建立的委派供應項目才會呈現給使用者：</span><span class="sxs-lookup"><span data-stu-id="95d72-190">You will see that only the delegated offers created by the delegated provider are presented to the user:</span></span>

> ![](media/azure-stack-delegated-provider/image8.png)
> 
> 

<span data-ttu-id="95d72-191">這便完成了提供委派的程序。</span><span class="sxs-lookup"><span data-stu-id="95d72-191">This concludes the process of offer delegation.</span></span> <span data-ttu-id="95d72-192">使用者現在可以藉由為其取得訂用帳戶，立即註冊使用此供應項目。</span><span class="sxs-lookup"><span data-stu-id="95d72-192">The user can now sign up for this offer by getting a subscription for it.</span></span>

## <a name="multiple-tier-delegation"></a><span data-ttu-id="95d72-193">多層委派</span><span class="sxs-lookup"><span data-stu-id="95d72-193">Multiple-tier delegation</span></span>

<span data-ttu-id="95d72-194">多層委派可讓提供者將供應項目委派給其他實體。</span><span class="sxs-lookup"><span data-stu-id="95d72-194">Multiple-tier delegation allows the delegated provider to delegate the offer to other entities.</span></span> <span data-ttu-id="95d72-195">例如，這允許建立更深入的轉銷商通道，在當中，管理 Azure Stack 的提供者會將供應項目委派給散發者，然後依次委派給轉售商。</span><span class="sxs-lookup"><span data-stu-id="95d72-195">This allows, for example, the creation of deeper reseller channels, in which the provider managing Azure Stack delegates an offer to a distributor, who in turn delegates to reseller.</span></span>
<span data-ttu-id="95d72-196">Azure Stack 支援最多五個層級的委派。</span><span class="sxs-lookup"><span data-stu-id="95d72-196">Azure Stack supports up to five levels of delegation.</span></span>

<span data-ttu-id="95d72-197">若要建立多層供應項目委派，委派的提供者會依次將供應項目委派給下一個提供者。</span><span class="sxs-lookup"><span data-stu-id="95d72-197">To create multiple tiers of offer delegation, the delegated provider in turn delegates the offer to the next provider.</span></span> <span data-ttu-id="95d72-198">此處理程序對委派的提供者與對雲端操作員是相同的 (請參閱[雲端操作員建立委派的供應項目](#cloud-operator-creates-the-delegated-offer))。</span><span class="sxs-lookup"><span data-stu-id="95d72-198">The process is the same for the delegated provider as it was for the cloud operator (see [Cloud operator creates the delegated offer](#cloud-operator-creates-the-delegated-offer)).</span></span>

## <a name="next-steps"></a><span data-ttu-id="95d72-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="95d72-199">Next steps</span></span>
[<span data-ttu-id="95d72-200">佈建 VM</span><span class="sxs-lookup"><span data-stu-id="95d72-200">Provision a VM</span></span>](azure-stack-provision-vm.md)

