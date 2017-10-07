---
title: "在 Azure Active Directory 群組個別的授權的使用者 tooa aaaHow toomigrate |Microsoft 文件"
description: "從個別使用者 tooswitch 授權 toogroup 授權使用 Azure Active Directory"
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
ms.openlocfilehash: 25e5c760b7e632ba71edde10d937fe580aa6ed35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-licensed-users-tooa-group-for-licensing-in-azure-active-directory"></a><span data-ttu-id="fa9c9-104">Tooadd 如何授權 Azure Active Directory 中的授權使用者 tooa 群組</span><span class="sxs-lookup"><span data-stu-id="fa9c9-104">How tooadd licensed users tooa group for licensing in Azure Active Directory</span></span>

<span data-ttu-id="fa9c9-105">透過 「 直接指派 」; hello 組織中可能有現有的授權部署 toousers也就使用 PowerShell 指令碼或其他工具 tooassign 個別使用者授權。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-105">You may have existing licenses deployed toousers in hello organizations via “direct assignment”; that is, using PowerShell scripts or other tools tooassign individual user licenses.</span></span> <span data-ttu-id="fa9c9-106">如果您想要 toostart 您組織中使用以群組為基礎的授權 toomanage 授權，您必須移轉計劃 tooseamlessly 取代現有的解決方案以群組為基礎的授權。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-106">If you would like toostart using group-based licensing toomanage licenses in your organization, you will need a migration plan tooseamlessly replace existing solutions with group-based licensing.</span></span>

<span data-ttu-id="fa9c9-107">請注意 hello 最重要事情 tookeep 是您應該避免在移轉 toogroup 為基礎的授權會導致使用者暫時遺失其目前指派的授權的情況。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-107">hello most important thing tookeep in mind is that you should avoid a situation where migrating toogroup-based licensing will result in users temporarily losing their currently assigned licenses.</span></span> <span data-ttu-id="fa9c9-108">移除授權可能會導致任何程序應該避免使用者存取 tooservices 和其資料會遺失 tooremove hello 風險。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-108">Any process that may result in removal of licenses should be avoided tooremove hello risk of users losing access tooservices and their data.</span></span>

## <a name="recommended-migration-process"></a><span data-ttu-id="fa9c9-109">建議的移轉程序</span><span class="sxs-lookup"><span data-stu-id="fa9c9-109">Recommended migration process</span></span>

1. <span data-ttu-id="fa9c9-110">您有現有的自動化 (例如，PowerShell) 管理使用者的授權指派及移除。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-110">You have existing automation (for example, PowerShell) managing license assignment and removal for users.</span></span> <span data-ttu-id="fa9c9-111">保留它的執行原樣。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-111">Leave it running as is.</span></span>

2. <span data-ttu-id="fa9c9-112">建立新的授權群組 （或決定哪些現有群組 toouse），並確定所有必要的使用者會新增為成員。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-112">Create a new licensing group (or decide which existing groups toouse) and make sure that all required users are added as members.</span></span>

3. <span data-ttu-id="fa9c9-113">將所需的 hello 授權指派 toothose 群組;您的目標應該是 tooreflect hello 相同授權狀態您現有的自動化 (例如 PowerShell) 會套用 toothose 使用者。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-113">Assign hello required licenses toothose groups; your goal should be tooreflect hello same licensing state your existing automation (for example, PowerShell) is applying toothose users.</span></span>

4. <span data-ttu-id="fa9c9-114">請確認使用權已經套用的 tooall 這些群組中的使用者。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-114">Verify that licenses have been applied tooall users in those groups.</span></span> <span data-ttu-id="fa9c9-115">作法是藉由檢查針對每個群組的 hello 處理狀態，以及檢查稽核記錄檔。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-115">This can be done by checking hello processing state on each group and by checking Audit Logs.</span></span>

  - <span data-ttu-id="fa9c9-116">您可以特別檢查個別使用者，方法是查看他們的授權詳細資料。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-116">You can spot check individual users by looking at their license details.</span></span> <span data-ttu-id="fa9c9-117">您會看到相同的授權指派給 「 直接 」 和 「 繼承 」 有 hello 的群組。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-117">You will see that they have hello same licenses assigned “directly” and “inherited” from groups.</span></span>

  - <span data-ttu-id="fa9c9-118">您可以執行 PowerShell 指令碼太[確認授權如何指派 toousers](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses)。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-118">You can run a PowerShell script too[verify how licenses are assigned toousers](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).</span></span>

  - <span data-ttu-id="fa9c9-119">當 hello 相同產品的授權指派 toohello 使用者同時以直接或透過群組時，hello 使用者會耗用一個授權。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-119">When hello same product license is assigned toohello user both directly and through a group, only one license is consumed by hello user.</span></span> <span data-ttu-id="fa9c9-120">因此沒有額外的授權是必要的 tooperform 移轉。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-120">Hence no additional licenses are required tooperform migration.</span></span>

5. <span data-ttu-id="fa9c9-121">確認沒有授權指派失敗，方法是檢查每個群組中是否有使用者處於錯誤狀態。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-121">Verify that no license assignments failed by checking each group for users in error state.</span></span> <span data-ttu-id="fa9c9-122">如需詳細資訊，請參閱[識別及解決群組的授權問題](active-directory-licensing-group-problem-resolution-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-122">For more information, see [Identifying and resolving license problems for a group](active-directory-licensing-group-problem-resolution-azure-portal.md).</span></span>

6. <span data-ttu-id="fa9c9-123">請考慮移除 hello 原始直接設定;您可能會想 toodo 逐漸增加，在 「 波浪"toomonitor hello 先在使用者的子集上的結果。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-123">Consider removing hello original direct assignments; you may want toodo it gradually, in “waves”, toomonitor hello outcome on a subset of users first.</span></span>

  <span data-ttu-id="fa9c9-124">您可能會離開 hello 原始直接指派的使用者，但當 hello 使用者讓它們仍然保留其授權的群組 hello 原始授權，可能不想要。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-124">You could leave hello original direct assignments on users, but when hello users leave their licensed groups they will still retain hello original license, which is possibly not want you want.</span></span>

## <a name="an-example"></a><span data-ttu-id="fa9c9-125">範例</span><span class="sxs-lookup"><span data-stu-id="fa9c9-125">An example</span></span>

<span data-ttu-id="fa9c9-126">我們的組織有 1,000 位使用者。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-126">We have an organization with 1,000 users.</span></span> <span data-ttu-id="fa9c9-127">所有使用者都需要 Enterprise Mobility + Security (EMS) 授權。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-127">All users require Enterprise Mobility + Security (EMS) licenses.</span></span> <span data-ttu-id="fa9c9-128">200 位使用者在 hello 財務部門中，但需要 Office 365 Enterprise E3 授權。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-128">200 users are in hello Finance Department and require Office 365 Enterprise E3 licenses.</span></span> <span data-ttu-id="fa9c9-129">我們有內部部署執行中的 PowerShell 指令碼，在使用者就職和離職時新增及移除授權。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-129">We have a PowerShell script running on premises adding and removing licenses from users as they come and go.</span></span> <span data-ttu-id="fa9c9-130">我們想要讓 Azure ad 授權會自動管理群組基礎授權的 tooreplace hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-130">We want tooreplace hello script with group-based licensing so licenses are managed automatically by Azure AD.</span></span>

<span data-ttu-id="fa9c9-131">以下是何種 hello 移轉程序可能看起來：</span><span class="sxs-lookup"><span data-stu-id="fa9c9-131">Here is what hello migration process could look like:</span></span>

1. <span data-ttu-id="fa9c9-132">使用 hello Azure 入口網站指派 hello EMS 授權 toohello**所有使用者**群組在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-132">Using hello Azure portal assign hello EMS license toohello **All users** group in Azure AD.</span></span> <span data-ttu-id="fa9c9-133">指派 hello E3 授權 toohello**財務部門**包含 hello 所需的所有使用者的群組。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-133">Assign hello E3 license toohello **Finance department** group that contains all hello required users.</span></span>

2. <span data-ttu-id="fa9c9-134">對於每個群組，確認針對所有使用者已完成授權指派。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-134">For each group, confirm that license assignment has completed for all users.</span></span> <span data-ttu-id="fa9c9-135">移 toohello 刀鋒視窗中的每個群組中，選取**授權**，並檢查 hello 處理狀態上方的 hello hello**授權**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-135">Go toohello blade for each group, select **Licenses**, and check hello processing status at hello top of hello **Licenses** blade.</span></span>

  - <span data-ttu-id="fa9c9-136">尋找 「 最新的授權變更已套用的 tooall 使用者 」 tooconfirm 處理已完成。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-136">Look for “Latest license changes have been applied tooall users" tooconfirm processing has completed.</span></span>

  - <span data-ttu-id="fa9c9-137">在最上層尋找任何使用者的授權可能尚未成功指派的相關通知。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-137">Look for a notification on top about any users for whom licenses may have not been successfully assigned.</span></span> <span data-ttu-id="fa9c9-138">我們對於某些使用者是否已用盡授權？</span><span class="sxs-lookup"><span data-stu-id="fa9c9-138">Did we run out of licenses for some users?</span></span> <span data-ttu-id="fa9c9-139">某些使用者是否有衝突的授權 SKU，使其無法繼承群組授權？</span><span class="sxs-lookup"><span data-stu-id="fa9c9-139">Do some users have conflicting license SKUs that prevent them from inheriting group licenses?</span></span>

3. <span data-ttu-id="fa9c9-140">特別檢查有直接的 hello 和套用的群組授權某些使用者 tooverify。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-140">Spot check some users tooverify that they have both hello direct and group licenses applied.</span></span> <span data-ttu-id="fa9c9-141">移 toohello 刀鋒視窗中的使用者，則選取**授權**，以及檢查 hello 狀態的授權。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-141">Go toohello blade for a user, select **Licenses**, and examine hello state of licenses.</span></span>

  - <span data-ttu-id="fa9c9-142">這是預期的 hello 使用者狀態移轉期間：</span><span class="sxs-lookup"><span data-stu-id="fa9c9-142">This is hello expected user state during migration:</span></span>

      ![預期的使用者狀態](media/active-directory-licensing-group-migration-azure-portal/expected-user-state.png)

  <span data-ttu-id="fa9c9-144">這可確認該 hello 使用者具有直接和繼承的授權。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-144">This confirms that hello user has both direct and inherited licenses.</span></span> <span data-ttu-id="fa9c9-145">我們看到同時指派 **EMS** 和 **E3**。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-145">We see that both **EMS** and **E3** are assigned.</span></span>

  - <span data-ttu-id="fa9c9-146">選取 hello 啟用服務的相關的每個授權 tooshow 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-146">Select each license tooshow details about hello enabled services.</span></span> <span data-ttu-id="fa9c9-147">如果直接 hello 和群組的授權啟用完全 hello hello 使用者相同的服務方案，這可能會使用的 toocheck。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-147">This can be used toocheck if hello direct and group licenses enable exactly hello same service plans for hello user.</span></span>

      ![檢查服務方案](media/active-directory-licensing-group-migration-azure-portal/check-service-plans.png)

4. <span data-ttu-id="fa9c9-149">在確認直接和群組授權是對等的之後，您可以開始從使用者移除直接授權。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-149">After confirming that both direct and group licenses are equivalent, you can start removing direct licenses from users.</span></span> <span data-ttu-id="fa9c9-150">您可以測試這種情況 hello 入口網站中的個別使用者移除它們，然後再執行自動化指令碼 toohave 大量加以移除。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-150">You can test this by removing them for individual users in hello portal and then run automation scripts toohave them removed in bulk.</span></span> <span data-ttu-id="fa9c9-151">以下是 hello 的範例與 hello 直接授權的同一個使用者透過 hello 入口網站來移除。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-151">Here is an example of hello same user with hello direct licenses removed through hello portal.</span></span> <span data-ttu-id="fa9c9-152">請注意 hello 授權狀態維持不變，但是我們不會再看見直接設定。</span><span class="sxs-lookup"><span data-stu-id="fa9c9-152">Notice that hello license state remains unchanged, but we no longer see direct assignments.</span></span>

  ![直接授權已移除](media/active-directory-licensing-group-migration-azure-portal/direct-licenses-removed.png)


## <a name="next-steps"></a><span data-ttu-id="fa9c9-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fa9c9-154">Next steps</span></span>

<span data-ttu-id="fa9c9-155">toolearn 深入了解其他透過群組，讀取授權管理案例</span><span class="sxs-lookup"><span data-stu-id="fa9c9-155">toolearn more about other scenarios for license management through groups, read</span></span>

* [<span data-ttu-id="fa9c9-156">Azure Active Directory 中指派的授權 tooa 群組</span><span class="sxs-lookup"><span data-stu-id="fa9c9-156">Assigning licenses tooa group in Azure Active Directory</span></span>](active-directory-licensing-group-assignment-azure-portal.md)
* [<span data-ttu-id="fa9c9-157">什麼是 Azure Active Directory 中以群組為基礎的授權？</span><span class="sxs-lookup"><span data-stu-id="fa9c9-157">What is group-based licensing in Azure Active Directory?</span></span>](active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="fa9c9-158">識別及解決 Azure Active Directory 中群組的授權問題</span><span class="sxs-lookup"><span data-stu-id="fa9c9-158">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [<span data-ttu-id="fa9c9-159">Azure Active Directory 群組型授權其他案例</span><span class="sxs-lookup"><span data-stu-id="fa9c9-159">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)
