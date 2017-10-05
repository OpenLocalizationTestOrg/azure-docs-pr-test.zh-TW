---
title: "如何將個別授權的使用者移轉至 Azure Active Directory 中的群組 | Microsoft Docs"
description: "如何使用 Azure Active Directory 從個別使用者授權切換至以群組為基礎的授權"
services: active-directory
keywords: "Azure AD 授權"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6b77dd4e9a6d361a05382397e89b575896fdad84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-licensed-users-to-a-group-for-licensing-in-azure-active-directory"></a><span data-ttu-id="ba2a0-104">如何將已授權的使用者新增至群組以便在 Azure Active Directory 中授權</span><span class="sxs-lookup"><span data-stu-id="ba2a0-104">How to add licensed users to a group for licensing in Azure Active Directory</span></span>

<span data-ttu-id="ba2a0-105">您可能會透過「直接指派」將現有授權部署給組織中的使用者，也就是，使用 PowerShell 指令碼或其他工具來指派個別使用者授權。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-105">You may have existing licenses deployed to users in the organizations via “direct assignment”; that is, using PowerShell scripts or other tools to assign individual user licenses.</span></span> <span data-ttu-id="ba2a0-106">如果您想要開始使用以群組為基礎的授權來管理您組織中的授權，您需要移轉方案，以順暢地將現有的解決方案取代為以群組為基礎的授權。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-106">If you would like to start using group-based licensing to manage licenses in your organization, you will need a migration plan to seamlessly replace existing solutions with group-based licensing.</span></span>

<span data-ttu-id="ba2a0-107">要謹記在心最重要的事情是，您應該避免移轉到以群組為基礎的授權會導致使用者暫時遺失其目前獲得指派授權的情況。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-107">The most important thing to keep in mind is that you should avoid a situation where migrating to group-based licensing will result in users temporarily losing their currently assigned licenses.</span></span> <span data-ttu-id="ba2a0-108">應避免可能造成授權移除的任何處理，以便移除使用者失去服務及其資料存取權的風險。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-108">Any process that may result in removal of licenses should be avoided to remove the risk of users losing access to services and their data.</span></span>

## <a name="recommended-migration-process"></a><span data-ttu-id="ba2a0-109">建議的移轉程序</span><span class="sxs-lookup"><span data-stu-id="ba2a0-109">Recommended migration process</span></span>

1. <span data-ttu-id="ba2a0-110">您有現有的自動化 (例如，PowerShell) 管理使用者的授權指派及移除。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-110">You have existing automation (for example, PowerShell) managing license assignment and removal for users.</span></span> <span data-ttu-id="ba2a0-111">保留它的執行原樣。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-111">Leave it running as is.</span></span>

2. <span data-ttu-id="ba2a0-112">建立新的授權群組 (或決定要使用哪個現有群組)，並確定所有必要的使用者新增為成員。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-112">Create a new licensing group (or decide which existing groups to use) and make sure that all required users are added as members.</span></span>

3. <span data-ttu-id="ba2a0-113">將必要的授權指派給這些群組；您的目標應該是反映您現有的自動化 (例如，PowerShell) 的相同授權狀態會套用至這些使用者。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-113">Assign the required licenses to those groups; your goal should be to reflect the same licensing state your existing automation (for example, PowerShell) is applying to those users.</span></span>

4. <span data-ttu-id="ba2a0-114">確認授權已套用至這些群組中的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-114">Verify that licenses have been applied to all users in those groups.</span></span> <span data-ttu-id="ba2a0-115">這可以透過檢查每個群組上的處理狀態或檢查稽核記錄來完成。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-115">This can be done by checking the processing state on each group and by checking Audit Logs.</span></span>

  - <span data-ttu-id="ba2a0-116">您可以特別檢查個別使用者，方法是查看他們的授權詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-116">You can spot check individual users by looking at their license details.</span></span> <span data-ttu-id="ba2a0-117">您會看到他們具有從群組「直接」和「繼承」指派的相同授權。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-117">You will see that they have the same licenses assigned “directly” and “inherited” from groups.</span></span>

  - <span data-ttu-id="ba2a0-118">您可以執行 PowerShell 指令碼，以[確認授權指派給使用者的方式](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses)。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-118">You can run a PowerShell script to [verify how licenses are assigned to users](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).</span></span>

  - <span data-ttu-id="ba2a0-119">當相同的產品授權同時直接和透過群組指派給使用者時，只能有一個授權由使用者取用。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-119">When the same product license is assigned to the user both directly and through a group, only one license is consumed by the user.</span></span> <span data-ttu-id="ba2a0-120">因此不需要額外授權即可執行移轉。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-120">Hence no additional licenses are required to perform migration.</span></span>

5. <span data-ttu-id="ba2a0-121">確認沒有授權指派失敗，方法是檢查每個群組中是否有使用者處於錯誤狀態。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-121">Verify that no license assignments failed by checking each group for users in error state.</span></span> <span data-ttu-id="ba2a0-122">如需詳細資訊，請參閱[識別及解決群組的授權問題](active-directory-licensing-group-problem-resolution-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-122">For more information, see [Identifying and resolving license problems for a group](active-directory-licensing-group-problem-resolution-azure-portal.md).</span></span>

6. <span data-ttu-id="ba2a0-123">請考慮移除原始的直接指派；您可能想要「一波一波」逐漸地進行，以便先監視使用者子集上的結果。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-123">Consider removing the original direct assignments; you may want to do it gradually, in “waves”, to monitor the outcome on a subset of users first.</span></span>

  <span data-ttu-id="ba2a0-124">您可以離開使用者的原始直接指派，但是當使用者離開其授權群組時，仍會保留原始授權，這可能不是您想要的結果。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-124">You could leave the original direct assignments on users, but when the users leave their licensed groups they will still retain the original license, which is possibly not want you want.</span></span>

## <a name="an-example"></a><span data-ttu-id="ba2a0-125">範例</span><span class="sxs-lookup"><span data-stu-id="ba2a0-125">An example</span></span>

<span data-ttu-id="ba2a0-126">我們的組織有 1,000 位使用者。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-126">We have an organization with 1,000 users.</span></span> <span data-ttu-id="ba2a0-127">所有使用者都需要 Enterprise Mobility + Security (EMS) 授權。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-127">All users require Enterprise Mobility + Security (EMS) licenses.</span></span> <span data-ttu-id="ba2a0-128">200 位使用者是在財務部門，而且需要 Office 365 企業版 E3 授權。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-128">200 users are in the Finance Department and require Office 365 Enterprise E3 licenses.</span></span> <span data-ttu-id="ba2a0-129">我們有內部部署執行中的 PowerShell 指令碼，在使用者就職和離職時新增及移除授權。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-129">We have a PowerShell script running on premises adding and removing licenses from users as they come and go.</span></span> <span data-ttu-id="ba2a0-130">我們想要將指令碼取代為以群組為基礎的授權，這樣授權就會自動由 Azure AD 管理。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-130">We want to replace the script with group-based licensing so licenses are managed automatically by Azure AD.</span></span>

<span data-ttu-id="ba2a0-131">以下是移轉程序可能的情況︰</span><span class="sxs-lookup"><span data-stu-id="ba2a0-131">Here is what the migration process could look like:</span></span>

1. <span data-ttu-id="ba2a0-132">使用 Azure 入口網站將 EMS 授權指派給 Azure AD 中的**所有使用者**群組。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-132">Using the Azure portal assign the EMS license to the **All users** group in Azure AD.</span></span> <span data-ttu-id="ba2a0-133">將 E3 授權指派給**財務部門**群組，包含所有必要的使用者。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-133">Assign the E3 license to the **Finance department** group that contains all the required users.</span></span>

2. <span data-ttu-id="ba2a0-134">對於每個群組，確認針對所有使用者已完成授權指派。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-134">For each group, confirm that license assignment has completed for all users.</span></span> <span data-ttu-id="ba2a0-135">移至每個群組中的刀鋒視窗，選取 [授權]，然後在 [授權] 刀鋒視窗頂端檢查處理狀態。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-135">Go to the blade for each group, select **Licenses**, and check the processing status at the top of the **Licenses** blade.</span></span>

  - <span data-ttu-id="ba2a0-136">尋找「最新的授權變更已套用至所有使用者」以確認處理已完成。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-136">Look for “Latest license changes have been applied to all users" to confirm processing has completed.</span></span>

  - <span data-ttu-id="ba2a0-137">在最上層尋找任何使用者的授權可能尚未成功指派的相關通知。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-137">Look for a notification on top about any users for whom licenses may have not been successfully assigned.</span></span> <span data-ttu-id="ba2a0-138">我們對於某些使用者是否已用盡授權？</span><span class="sxs-lookup"><span data-stu-id="ba2a0-138">Did we run out of licenses for some users?</span></span> <span data-ttu-id="ba2a0-139">某些使用者是否有衝突的授權 SKU，使其無法繼承群組授權？</span><span class="sxs-lookup"><span data-stu-id="ba2a0-139">Do some users have conflicting license SKUs that prevent them from inheriting group licenses?</span></span>

3. <span data-ttu-id="ba2a0-140">特別檢查某些使用者，以確認其套用直接和群組授權。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-140">Spot check some users to verify that they have both the direct and group licenses applied.</span></span> <span data-ttu-id="ba2a0-141">移至使用者的刀鋒視窗，選取 [授權]，然後檢查授權狀態。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-141">Go to the blade for a user, select **Licenses**, and examine the state of licenses.</span></span>

  - <span data-ttu-id="ba2a0-142">這是移轉期間預期的使用者狀態︰</span><span class="sxs-lookup"><span data-stu-id="ba2a0-142">This is the expected user state during migration:</span></span>

      ![預期的使用者狀態](media/active-directory-licensing-group-migration-azure-portal/expected-user-state.png)

  <span data-ttu-id="ba2a0-144">這可確認使用者同時具有直接和繼承的授權。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-144">This confirms that the user has both direct and inherited licenses.</span></span> <span data-ttu-id="ba2a0-145">我們看到同時指派 **EMS** 和 **E3**。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-145">We see that both **EMS** and **E3** are assigned.</span></span>

  - <span data-ttu-id="ba2a0-146">選取每個授權，以顯示已啟用服務的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-146">Select each license to show details about the enabled services.</span></span> <span data-ttu-id="ba2a0-147">這可以用來檢查直接和群組授權是否針對使用者啟用完全相同的服務方案。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-147">This can be used to check if the direct and group licenses enable exactly the same service plans for the user.</span></span>

      ![檢查服務方案](media/active-directory-licensing-group-migration-azure-portal/check-service-plans.png)

4. <span data-ttu-id="ba2a0-149">在確認直接和群組授權是對等的之後，您可以開始從使用者移除直接授權。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-149">After confirming that both direct and group licenses are equivalent, you can start removing direct licenses from users.</span></span> <span data-ttu-id="ba2a0-150">您可以藉由在入口網站中移除個別使用者的直接授權來進行測試，然後再執行自動化指令碼，將它們大量移除。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-150">You can test this by removing them for individual users in the portal and then run automation scripts to have them removed in bulk.</span></span> <span data-ttu-id="ba2a0-151">以下是透過入口網站移除直接授權的相同使用者範例。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-151">Here is an example of the same user with the direct licenses removed through the portal.</span></span> <span data-ttu-id="ba2a0-152">請注意，授權狀態會維持不變，但是我們不會再看見直接指派。</span><span class="sxs-lookup"><span data-stu-id="ba2a0-152">Notice that the license state remains unchanged, but we no longer see direct assignments.</span></span>

  ![直接授權已移除](media/active-directory-licensing-group-migration-azure-portal/direct-licenses-removed.png)


## <a name="next-steps"></a><span data-ttu-id="ba2a0-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba2a0-154">Next steps</span></span>

<span data-ttu-id="ba2a0-155">若要深入了解透過群組管理授權的其他案例，請閱讀</span><span class="sxs-lookup"><span data-stu-id="ba2a0-155">To learn more about other scenarios for license management through groups, read</span></span>

* [<span data-ttu-id="ba2a0-156">將授權指派給 Azure Active Directory 中的群組</span><span class="sxs-lookup"><span data-stu-id="ba2a0-156">Assigning licenses to a group in Azure Active Directory</span></span>](active-directory-licensing-group-assignment-azure-portal.md)
* [<span data-ttu-id="ba2a0-157">什麼是 Azure Active Directory 中以群組為基礎的授權？</span><span class="sxs-lookup"><span data-stu-id="ba2a0-157">What is group-based licensing in Azure Active Directory?</span></span>](active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="ba2a0-158">識別及解決 Azure Active Directory 中群組的授權問題</span><span class="sxs-lookup"><span data-stu-id="ba2a0-158">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [<span data-ttu-id="ba2a0-159">Azure Active Directory 群組型授權其他案例</span><span class="sxs-lookup"><span data-stu-id="ba2a0-159">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)
