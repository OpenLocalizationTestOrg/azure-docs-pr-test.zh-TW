---
title: "Azure Active Directory B2B 共同作業使用者的 aaaProperties |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業的使用者屬性可進行設定"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 78709f64430ed4c14eadf4dc257f175c24698c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="properties-of-an-azure-active-directory-b2b-collaboration-user"></a><span data-ttu-id="669e0-103">Azure Active Directory B2B 共同作業使用者的屬性</span><span class="sxs-lookup"><span data-stu-id="669e0-103">Properties of an Azure Active Directory B2B collaboration user</span></span>

<span data-ttu-id="669e0-104">Azure Active Directory (Azure AD) 企業對企業 (B2B) 共同作業使用者是 UserType = [來賓] 的使用者。</span><span class="sxs-lookup"><span data-stu-id="669e0-104">An Azure Active Directory (Azure AD) business-to-business (B2B) collaboration user is a user with UserType = Guest.</span></span> <span data-ttu-id="669e0-105">此 guest 使用者通常是來自夥伴組織，且 hello 邀請目錄中，預設的權限有限。</span><span class="sxs-lookup"><span data-stu-id="669e0-105">This guest user typically is from a partner organization and has limited privileges in hello inviting directory, by default.</span></span>

<span data-ttu-id="669e0-106">根據 hello 邀請組織的需求，Azure AD B2B 共同作業的使用者可以是其中一種 hello 下列帳戶狀態：</span><span class="sxs-lookup"><span data-stu-id="669e0-106">Depending on hello inviting organization's needs, an Azure AD B2B collaboration user can be in one of hello following account states:</span></span>

- <span data-ttu-id="669e0-107">狀態 1： 位於外部的 Azure AD 執行個體，並代表 hello 邀請組織中有 guest 使用者。</span><span class="sxs-lookup"><span data-stu-id="669e0-107">State 1: Homed in an external instance of Azure AD and represented as a guest user in hello inviting organization.</span></span> <span data-ttu-id="669e0-108">在此情況下，hello B2B 使用者登入使用所屬 toohello 受邀租用戶的 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="669e0-108">In this case, hello B2B user signs in by using an Azure AD account that belongs toohello invited tenant.</span></span> <span data-ttu-id="669e0-109">如果 hello 夥伴組織不使用 Azure AD，仍會建立在 Azure AD 中的 hello guest 使用者。</span><span class="sxs-lookup"><span data-stu-id="669e0-109">If hello partner organization doesn't use Azure AD, hello guest user in Azure AD is still created.</span></span> <span data-ttu-id="669e0-110">hello 需求是，它們兌換邀請其 Azure AD 會驗證電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="669e0-110">hello requirements are that they redeem their invitation and Azure AD verifies their email address.</span></span> <span data-ttu-id="669e0-111">此排列也稱為 Just-In-Time (JIT) 租用或「熱門」租用。</span><span class="sxs-lookup"><span data-stu-id="669e0-111">This arrangement is also called a just-in-time (JIT) tenancy or a "viral" tenancy.</span></span>

- <span data-ttu-id="669e0-112">狀態 2： 主目錄中的 Microsoft 帳戶，並代表 hello 主機組織中有 guest 使用者。</span><span class="sxs-lookup"><span data-stu-id="669e0-112">State 2: Homed in a Microsoft account and represented as a guest user in hello host organization.</span></span> <span data-ttu-id="669e0-113">在此情況下，hello guest 使用者帳戶登入 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="669e0-113">In this case, hello guest user signs in with a Microsoft account.</span></span> <span data-ttu-id="669e0-114">hello 受邀使用者的社交身分識別 (google.com 或類似)，提供兌換這不 Microsoft 帳戶，會建立為 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="669e0-114">hello invited user's social identity (google.com or similar), which is not a Microsoft account, is created as a Microsoft account during offer redemption.</span></span>

- <span data-ttu-id="669e0-115">狀態 3: Hello 主機組織的內部部署 Active Directory 中的主目錄和同步處理與 hello 主機組織的 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="669e0-115">State 3: Homed in hello host organization's on-premises Active Directory and synced with hello host organization's Azure AD.</span></span> <span data-ttu-id="669e0-116">在此版本中，您必須使用 PowerShell toomanually 變更 hello UserType 這類使用者的 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="669e0-116">During this release, you must use PowerShell toomanually change hello UserType of such users in hello cloud.</span></span>

- <span data-ttu-id="669e0-117">狀態 4： 位於主機組織的 Azure AD 與 UserType = 客體和主機 hello 的組織管理的認證。</span><span class="sxs-lookup"><span data-stu-id="669e0-117">State 4: Homed in host organization's Azure AD with UserType = Guest and credentials that hello host organization manages.</span></span>

  ![顯示 hello 邀請者縮寫](media/active-directory-b2b-user-properties/redemption-diagram.png)


<span data-ttu-id="669e0-119">現在，讓我們來看看狀態 1 中 Azure AD B2B 共同作業使用者在 Azure AD 中的外觀。</span><span class="sxs-lookup"><span data-stu-id="669e0-119">Now, let's see what an Azure AD B2B collaboration user in State 1 looks like in Azure AD.</span></span>

### <a name="before-invitation-redemption"></a><span data-ttu-id="669e0-120">邀請兌換之前</span><span class="sxs-lookup"><span data-stu-id="669e0-120">Before invitation redemption</span></span>

![優惠兌換之前](media/active-directory-b2b-user-properties/before-redemption.png)

### <a name="after-invitation-redemption"></a><span data-ttu-id="669e0-122">邀請兌換之後</span><span class="sxs-lookup"><span data-stu-id="669e0-122">After invitation redemption</span></span>

![優惠兌換之後](media/active-directory-b2b-user-properties/after-redemption.png)

## <a name="key-properties-of-hello-azure-ad-b2b-collaboration-user"></a><span data-ttu-id="669e0-124">Hello Azure AD B2B 共同作業的使用者之索引鍵屬性</span><span class="sxs-lookup"><span data-stu-id="669e0-124">Key properties of hello Azure AD B2B collaboration user</span></span>
### <a name="usertype"></a><span data-ttu-id="669e0-125">UserType</span><span class="sxs-lookup"><span data-stu-id="669e0-125">UserType</span></span>
<span data-ttu-id="669e0-126">這個屬性表示 hello 使用者 toohello 主機租用戶的 hello 關聯的性。</span><span class="sxs-lookup"><span data-stu-id="669e0-126">This property indicates hello relationship of hello user toohello host tenancy.</span></span> <span data-ttu-id="669e0-127">此屬性可以包含兩個值：</span><span class="sxs-lookup"><span data-stu-id="669e0-127">This property can have two values:</span></span>
- <span data-ttu-id="669e0-128">成員： 這個值表示 hello 主機組織的員工和 hello 公司的薪資中的使用者。</span><span class="sxs-lookup"><span data-stu-id="669e0-128">Member: This value indicates an employee of hello host organization and a user in hello organization's payroll.</span></span> <span data-ttu-id="669e0-129">比方說，這位使用者必須要有 toohave 存取僅限 toointernal 站台。</span><span class="sxs-lookup"><span data-stu-id="669e0-129">For example, this user expects toohave access toointernal-only sites.</span></span> <span data-ttu-id="669e0-130">這位使用者就不會被認為是外部共同作業人員。</span><span class="sxs-lookup"><span data-stu-id="669e0-130">This user would not be considered an external collaborator.</span></span>

- <span data-ttu-id="669e0-131">客體： 這個值表示不會被視為內部 toohello 公司，例如外部共同作業者、 夥伴、 客戶或類似使用者的使用者。</span><span class="sxs-lookup"><span data-stu-id="669e0-131">Guest: This value indicates a user who isn't considered internal toohello company, such as an external collaborator, partner, customer, or similar user.</span></span> <span data-ttu-id="669e0-132">這類使用者不是預期的 tooreceive 總裁的內部備忘或接收公司的好處，例如。</span><span class="sxs-lookup"><span data-stu-id="669e0-132">Such a user wouldn't be expected tooreceive a CEO's internal memo, or receive company benefits, for example.</span></span>

  > [!NOTE]
  > <span data-ttu-id="669e0-133">hello UserType 都有任何關聯 toohow hello 使用者登入時，hello 目錄角色的 hello 使用者等等。</span><span class="sxs-lookup"><span data-stu-id="669e0-133">hello UserType has no relation toohow hello user signs in, hello directory role of hello user, and so on.</span></span> <span data-ttu-id="669e0-134">這個屬性只是指出 hello 使用者的關聯性 toohello 主機組織，並允許 hello 組織 tooenforce 原則相依於這個屬性。</span><span class="sxs-lookup"><span data-stu-id="669e0-134">This property simply indicates hello user's relationship toohello host organization and allows hello organization tooenforce policies that depend on this property.</span></span>

### <a name="source"></a><span data-ttu-id="669e0-135">來源</span><span class="sxs-lookup"><span data-stu-id="669e0-135">Source</span></span>
<span data-ttu-id="669e0-136">這個屬性會指出 hello 使用者如何登入。</span><span class="sxs-lookup"><span data-stu-id="669e0-136">This property indicates how hello user signs in.</span></span>

- <span data-ttu-id="669e0-137">受邀使用者︰此使用者已受邀請，但尚未兌換邀請。</span><span class="sxs-lookup"><span data-stu-id="669e0-137">Invited User: This user has been invited but has not yet redeemed an invitation.</span></span>

- <span data-ttu-id="669e0-138">外部的 Active Directory： 此使用者位於外部組織，並使用所屬 toohello 另一個組織的 Azure AD 帳戶驗證。</span><span class="sxs-lookup"><span data-stu-id="669e0-138">External Active Directory: This user is homed in an external organization and authenticates by using an Azure AD account that belongs toohello other organization.</span></span> <span data-ttu-id="669e0-139">這種類型的登入對應 tooState 1。</span><span class="sxs-lookup"><span data-stu-id="669e0-139">This type of sign-in corresponds tooState 1.</span></span>

- <span data-ttu-id="669e0-140">Microsoft 帳戶：此使用者位於 Microsoft 帳戶，並使用 Microsoft 帳戶進行驗證。</span><span class="sxs-lookup"><span data-stu-id="669e0-140">Microsoft account: This user is homed in a Microsoft account and authenticates by using a Microsoft account.</span></span> <span data-ttu-id="669e0-141">這種類型的登入對應 tooState 2。</span><span class="sxs-lookup"><span data-stu-id="669e0-141">This type of sign-in corresponds tooState 2.</span></span>

- <span data-ttu-id="669e0-142">Windows Server Active Directory： 此使用者已登入從所屬 toothis 組織在內部部署 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="669e0-142">Windows Server Active Directory: This user is signed in from on-premises Active Directory that belongs toothis organization.</span></span> <span data-ttu-id="669e0-143">這種類型的登入對應 tooState 3。</span><span class="sxs-lookup"><span data-stu-id="669e0-143">This type of sign-in corresponds tooState 3.</span></span>

- <span data-ttu-id="669e0-144">Azure Active Directory： 使用所屬 toothis 組織的 Azure AD 帳戶來驗證此使用者。</span><span class="sxs-lookup"><span data-stu-id="669e0-144">Azure Active Directory: This user authenticates by using an Azure AD account that belongs toothis organization.</span></span> <span data-ttu-id="669e0-145">這種類型的登入對應 tooState 4。</span><span class="sxs-lookup"><span data-stu-id="669e0-145">This type of sign-in corresponds tooState 4.</span></span>
  > [!NOTE]
  > <span data-ttu-id="669e0-146">Source 和 UserType 是獨立的屬性。</span><span class="sxs-lookup"><span data-stu-id="669e0-146">Source and UserType are independent properties.</span></span> <span data-ttu-id="669e0-147">Source 的值不代表特定的 UserType 值。</span><span class="sxs-lookup"><span data-stu-id="669e0-147">A value of Source does not imply a particular value for UserType.</span></span>

## <a name="can-azure-ad-b2b-users-be-added-as-members-instead-of-guests"></a><span data-ttu-id="669e0-148">Azure AD B2B 使用者是否可新增為成員而非來賓？</span><span class="sxs-lookup"><span data-stu-id="669e0-148">Can Azure AD B2B users be added as members instead of guests?</span></span>
<span data-ttu-id="669e0-149">一般而言，Azure AD B2B 使用者和來賓使用者的意義相同。</span><span class="sxs-lookup"><span data-stu-id="669e0-149">Typically, an Azure AD B2B user and guest user are synonymous.</span></span> <span data-ttu-id="669e0-150">因此，Azure AD B2B 共同作業使用者依預設是新增為具有 UserType = [來賓] 的使用者。</span><span class="sxs-lookup"><span data-stu-id="669e0-150">Therefore, an Azure AD B2B collaboration user is added as a user with UserType = Guest by default.</span></span> <span data-ttu-id="669e0-151">不過，在某些情況下，hello 夥伴組織會也屬於較大的組織 toowhich hello 主機組織的成員。</span><span class="sxs-lookup"><span data-stu-id="669e0-151">However, in some cases, hello partner organization is a member of a larger organization toowhich hello host organization also belongs.</span></span> <span data-ttu-id="669e0-152">如果是這樣，hello 主機組織可能會想 tootreat hello 做為成員，而不是客體的夥伴組織中的使用者。</span><span class="sxs-lookup"><span data-stu-id="669e0-152">If so, hello host organization might want tootreat users in hello partner organization as members instead of guests.</span></span> <span data-ttu-id="669e0-153">使用 hello Azure AD B2B 邀請管理員 Api tooadd 或邀請 hello 夥伴組織 toohello 主機組織成員身分的使用者。</span><span class="sxs-lookup"><span data-stu-id="669e0-153">Use hello Azure AD B2B Invitation Manager APIs tooadd or invite a user from hello partner organization toohello host organization as a member.</span></span>

## <a name="filter-for-guest-users-in-hello-directory"></a><span data-ttu-id="669e0-154">Guest 使用者在 hello 目錄中的篩選條件</span><span class="sxs-lookup"><span data-stu-id="669e0-154">Filter for guest users in hello directory</span></span>

![篩選來賓使用者](media/active-directory-b2b-user-properties/filter-guest-users.png)

## <a name="convert-usertype"></a><span data-ttu-id="669e0-156">轉換 UserType</span><span class="sxs-lookup"><span data-stu-id="669e0-156">Convert UserType</span></span>
<span data-ttu-id="669e0-157">目前，它可能會從成員 tooGuest，反之亦然使用者 tooconvert UserType 使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="669e0-157">Currently, it is possible for users tooconvert UserType from Member tooGuest and vice-versa by using PowerShell.</span></span> <span data-ttu-id="669e0-158">不過，hello UserType 屬性應該 toorepresent hello 使用者的關聯性 toohello 組織。</span><span class="sxs-lookup"><span data-stu-id="669e0-158">However, hello UserType property is supposed toorepresent hello user's relationship toohello organization.</span></span> <span data-ttu-id="669e0-159">因此，只有在 hello 使用者 toohello 組織的 hello 性關聯有變化，應該變更 hello 這個屬性的值。</span><span class="sxs-lookup"><span data-stu-id="669e0-159">Therefore, hello value of this property should change only if hello relationship of hello user toohello organization changes.</span></span> <span data-ttu-id="669e0-160">如果 hello 的 hello 使用者的關聯性變更時，應該問題，例如是否應該變更 hello 使用者主要名稱 (UPN)，處理？</span><span class="sxs-lookup"><span data-stu-id="669e0-160">If hello relationship of hello user changes, should issues, like whether hello user principal name (UPN) should change, be addressed?</span></span> <span data-ttu-id="669e0-161">Hello 使用者應該繼續 toohave 存取 toohello 相同的資源嗎？</span><span class="sxs-lookup"><span data-stu-id="669e0-161">Should hello user continue toohave access toohello same resources?</span></span> <span data-ttu-id="669e0-162">是否應指派信箱？</span><span class="sxs-lookup"><span data-stu-id="669e0-162">Should a mailbox be assigned?</span></span> <span data-ttu-id="669e0-163">因此，我們不建議使用 PowerShell 為不可部分完成的活動變更 hello UserType。</span><span class="sxs-lookup"><span data-stu-id="669e0-163">Therefore, we do not recommend changing hello UserType by using PowerShell as an atomic activity.</span></span> <span data-ttu-id="669e0-164">此外，為免使用 PowerShell 讓這個屬性成為不可變屬性，我們不建議採用此值的相依性。</span><span class="sxs-lookup"><span data-stu-id="669e0-164">In addition, in case this property becomes immutable by using PowerShell, we do not recommend taking a dependency on this value.</span></span>

## <a name="remove-guest-user-limitations"></a><span data-ttu-id="669e0-165">移除來賓使用者限制</span><span class="sxs-lookup"><span data-stu-id="669e0-165">Remove guest user limitations</span></span>
<span data-ttu-id="669e0-166">可能有您希望 toogive 您來賓使用者的權限的情況。</span><span class="sxs-lookup"><span data-stu-id="669e0-166">There may be cases where you want toogive your guest users higher privileges.</span></span> <span data-ttu-id="669e0-167">您可以新增來賓使用者 tooany 角色並甚至移除 hello 預設來賓使用者限制中的 hello 目錄 toogive 相同權限做為成員的使用者 hello。</span><span class="sxs-lookup"><span data-stu-id="669e0-167">You can add a guest user tooany role and even remove hello default guest user restrictions in hello directory toogive a user hello same privileges as members.</span></span>

<span data-ttu-id="669e0-168">如此，來賓使用者 hello 公司目錄中的獲得便關閉 hello 預設來賓使用者限制可能 tooturn hello 相同成員使用者權限。</span><span class="sxs-lookup"><span data-stu-id="669e0-168">It is possible tooturn off hello default guest user limitations so that a guest user in hello company directory is given hello same permissions as a member user.</span></span>

![移除來賓使用者限制](media/active-directory-b2b-user-properties/remove-guest-limitations.png)

## <a name="next-steps"></a><span data-ttu-id="669e0-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="669e0-170">Next steps</span></span>

<span data-ttu-id="669e0-171">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="669e0-171">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="669e0-172">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="669e0-172">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="669e0-173">新增 B2B 共同作業使用者 tooa 角色</span><span class="sxs-lookup"><span data-stu-id="669e0-173">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="669e0-174">委派 B2B 共同作業邀請</span><span class="sxs-lookup"><span data-stu-id="669e0-174">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="669e0-175">B2B 共同作業使用者稽核和報告</span><span class="sxs-lookup"><span data-stu-id="669e0-175">B2B collaboration user auditing and reporting</span></span>](active-directory-b2b-auditing-and-reporting.md)
* [<span data-ttu-id="669e0-176">動態群組與 B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="669e0-176">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="669e0-177">B2B 共同作業程式碼與 PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="669e0-177">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="669e0-178">設定適用於 B2B 共同作業的 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="669e0-178">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="669e0-179">B2B 共同作業使用者權杖</span><span class="sxs-lookup"><span data-stu-id="669e0-179">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="669e0-180">B2B 共同作業使用者宣告對應</span><span class="sxs-lookup"><span data-stu-id="669e0-180">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="669e0-181">Office 365 外部共用</span><span class="sxs-lookup"><span data-stu-id="669e0-181">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="669e0-182">B2B 共同作業目前的限制</span><span class="sxs-lookup"><span data-stu-id="669e0-182">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
