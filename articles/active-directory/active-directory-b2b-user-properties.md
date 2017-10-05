---
title: "Azure Active Directory B2B 共同作業使用者的屬性 | Microsoft Docs"
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
ms.openlocfilehash: 6e49cb202ed03bf50fb9ca34d34924cda434829c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="properties-of-an-azure-active-directory-b2b-collaboration-user"></a><span data-ttu-id="ab3dc-103">Azure Active Directory B2B 共同作業使用者的屬性</span><span class="sxs-lookup"><span data-stu-id="ab3dc-103">Properties of an Azure Active Directory B2B collaboration user</span></span>

<span data-ttu-id="ab3dc-104">Azure Active Directory (Azure AD) 企業對企業 (B2B) 共同作業使用者是 UserType = [來賓] 的使用者。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-104">An Azure Active Directory (Azure AD) business-to-business (B2B) collaboration user is a user with UserType = Guest.</span></span> <span data-ttu-id="ab3dc-105">此來賓使用者通常是來自合作夥伴組織的使用者，且依預設在邀請目錄中的權限有限。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-105">This guest user typically is from a partner organization and has limited privileges in the inviting directory, by default.</span></span>

<span data-ttu-id="ab3dc-106">根據邀請組織的需求，Azure AD B2B 共同作業使用者可以是下列帳戶狀態之一︰</span><span class="sxs-lookup"><span data-stu-id="ab3dc-106">Depending on the inviting organization's needs, an Azure AD B2B collaboration user can be in one of the following account states:</span></span>

- <span data-ttu-id="ab3dc-107">狀態 1：位於 Azure AD 的外部執行個體並表示為提出邀請之組織中的來賓使用者。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-107">State 1: Homed in an external instance of Azure AD and represented as a guest user in the inviting organization.</span></span> <span data-ttu-id="ab3dc-108">在此情況下，B2B 使用者會使用屬於受邀租用戶的 Azure AD 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-108">In this case, the B2B user signs in by using an Azure AD account that belongs to the invited tenant.</span></span> <span data-ttu-id="ab3dc-109">如果夥伴組織未使用 Azure AD，仍會在 Azure AD 中建立來賓使用者。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-109">If the partner organization doesn't use Azure AD, the guest user in Azure AD is still created.</span></span> <span data-ttu-id="ab3dc-110">他們必須兌換其邀請，而且 Azure AD 必須確認其電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-110">The requirements are that they redeem their invitation and Azure AD verifies their email address.</span></span> <span data-ttu-id="ab3dc-111">此排列也稱為 Just-In-Time (JIT) 租用或「熱門」租用。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-111">This arrangement is also called a just-in-time (JIT) tenancy or a "viral" tenancy.</span></span>

- <span data-ttu-id="ab3dc-112">狀態 2：位於 Microsoft 帳戶並表示為主機組織中的來賓使用者。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-112">State 2: Homed in a Microsoft account and represented as a guest user in the host organization.</span></span> <span data-ttu-id="ab3dc-113">在此情況下，來賓使用者會以 Microsoft 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-113">In this case, the guest user signs in with a Microsoft account.</span></span> <span data-ttu-id="ab3dc-114">受邀使用者的社交身分識別 (google.com 或類似項目，但不是 Microsoft 帳戶) 會在優惠兌換期間建立為 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-114">The invited user's social identity (google.com or similar), which is not a Microsoft account, is created as a Microsoft account during offer redemption.</span></span>

- <span data-ttu-id="ab3dc-115">狀態 3：位於主機組織的內部部署 Active Directory 並與主機組織的 Azure AD 同步處理。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-115">State 3: Homed in the host organization's on-premises Active Directory and synced with the host organization's Azure AD.</span></span> <span data-ttu-id="ab3dc-116">在此版本中，您必須使用 PowerShell 手動變更雲端中這類使用者的 UserType。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-116">During this release, you must use PowerShell to manually change the UserType of such users in the cloud.</span></span>

- <span data-ttu-id="ab3dc-117">狀態 4：位於主機組織的 AzureAD，其 UserType = [來賓] 並具備主機組織所管理的認證。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-117">State 4: Homed in host organization's Azure AD with UserType = Guest and credentials that the host organization manages.</span></span>

  ![顯示邀請者的姓名縮寫](media/active-directory-b2b-user-properties/redemption-diagram.png)


<span data-ttu-id="ab3dc-119">現在，讓我們來看看狀態 1 中 Azure AD B2B 共同作業使用者在 Azure AD 中的外觀。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-119">Now, let's see what an Azure AD B2B collaboration user in State 1 looks like in Azure AD.</span></span>

### <a name="before-invitation-redemption"></a><span data-ttu-id="ab3dc-120">邀請兌換之前</span><span class="sxs-lookup"><span data-stu-id="ab3dc-120">Before invitation redemption</span></span>

![優惠兌換之前](media/active-directory-b2b-user-properties/before-redemption.png)

### <a name="after-invitation-redemption"></a><span data-ttu-id="ab3dc-122">邀請兌換之後</span><span class="sxs-lookup"><span data-stu-id="ab3dc-122">After invitation redemption</span></span>

![優惠兌換之後](media/active-directory-b2b-user-properties/after-redemption.png)

## <a name="key-properties-of-the-azure-ad-b2b-collaboration-user"></a><span data-ttu-id="ab3dc-124">Azure AD B2B 共同作業使用者的金鑰屬性</span><span class="sxs-lookup"><span data-stu-id="ab3dc-124">Key properties of the Azure AD B2B collaboration user</span></span>
### <a name="usertype"></a><span data-ttu-id="ab3dc-125">UserType</span><span class="sxs-lookup"><span data-stu-id="ab3dc-125">UserType</span></span>
<span data-ttu-id="ab3dc-126">此屬性會指出使用者與主機租用的關聯性。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-126">This property indicates the relationship of the user to the host tenancy.</span></span> <span data-ttu-id="ab3dc-127">此屬性可以包含兩個值：</span><span class="sxs-lookup"><span data-stu-id="ab3dc-127">This property can have two values:</span></span>
- <span data-ttu-id="ab3dc-128">成員︰此值表示主機組織的員工，以及由組織支薪的使用者。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-128">Member: This value indicates an employee of the host organization and a user in the organization's payroll.</span></span> <span data-ttu-id="ab3dc-129">例如，這位使用者要能夠存取僅供內部使用的網站。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-129">For example, this user expects to have access to internal-only sites.</span></span> <span data-ttu-id="ab3dc-130">這位使用者就不會被認為是外部共同作業人員。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-130">This user would not be considered an external collaborator.</span></span>

- <span data-ttu-id="ab3dc-131">來賓：這個值表示非公司內部人員的使用者，例如外部共同作業者、合作夥伴、客戶或類似的使用者。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-131">Guest: This value indicates a user who isn't considered internal to the company, such as an external collaborator, partner, customer, or similar user.</span></span> <span data-ttu-id="ab3dc-132">這類使用者不會收到執行長的內部備忘，或收到公司權益。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-132">Such a user wouldn't be expected to receive a CEO's internal memo, or receive company benefits, for example.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ab3dc-133">UserType 與使用者登入的方式、使用者的目錄角色等等無關。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-133">The UserType has no relation to how the user signs in, the directory role of the user, and so on.</span></span> <span data-ttu-id="ab3dc-134">此屬性只是表示使用者與主機組織的關聯性，並可讓組織強制執行此屬性的相依原則。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-134">This property simply indicates the user's relationship to the host organization and allows the organization to enforce policies that depend on this property.</span></span>

### <a name="source"></a><span data-ttu-id="ab3dc-135">來源</span><span class="sxs-lookup"><span data-stu-id="ab3dc-135">Source</span></span>
<span data-ttu-id="ab3dc-136">此屬性指出使用者的登入方式。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-136">This property indicates how the user signs in.</span></span>

- <span data-ttu-id="ab3dc-137">受邀使用者︰此使用者已受邀請，但尚未兌換邀請。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-137">Invited User: This user has been invited but has not yet redeemed an invitation.</span></span>

- <span data-ttu-id="ab3dc-138">外部 Active Directory︰此使用者位於外部組織，並使用屬於其他組織的 Azure AD 帳戶進行驗證。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-138">External Active Directory: This user is homed in an external organization and authenticates by using an Azure AD account that belongs to the other organization.</span></span> <span data-ttu-id="ab3dc-139">這類型的登入對應於狀態 1。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-139">This type of sign-in corresponds to State 1.</span></span>

- <span data-ttu-id="ab3dc-140">Microsoft 帳戶：此使用者位於 Microsoft 帳戶，並使用 Microsoft 帳戶進行驗證。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-140">Microsoft account: This user is homed in a Microsoft account and authenticates by using a Microsoft account.</span></span> <span data-ttu-id="ab3dc-141">這類型的登入對應於狀態 2。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-141">This type of sign-in corresponds to State 2.</span></span>

- <span data-ttu-id="ab3dc-142">Windows Server Active Directory︰此使用者已從屬於此組織的內部部署 Active Directory 登入。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-142">Windows Server Active Directory: This user is signed in from on-premises Active Directory that belongs to this organization.</span></span> <span data-ttu-id="ab3dc-143">這類型的登入對應於狀態 3。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-143">This type of sign-in corresponds to State 3.</span></span>

- <span data-ttu-id="ab3dc-144">Azure Active Directory︰此使用者會使用屬於此組織的 Azure AD 帳戶進行驗證。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-144">Azure Active Directory: This user authenticates by using an Azure AD account that belongs to this organization.</span></span> <span data-ttu-id="ab3dc-145">這類型的登入對應於狀態 4。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-145">This type of sign-in corresponds to State 4.</span></span>
  > [!NOTE]
  > <span data-ttu-id="ab3dc-146">Source 和 UserType 是獨立的屬性。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-146">Source and UserType are independent properties.</span></span> <span data-ttu-id="ab3dc-147">Source 的值不代表特定的 UserType 值。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-147">A value of Source does not imply a particular value for UserType.</span></span>

## <a name="can-azure-ad-b2b-users-be-added-as-members-instead-of-guests"></a><span data-ttu-id="ab3dc-148">Azure AD B2B 使用者是否可新增為成員而非來賓？</span><span class="sxs-lookup"><span data-stu-id="ab3dc-148">Can Azure AD B2B users be added as members instead of guests?</span></span>
<span data-ttu-id="ab3dc-149">一般而言，Azure AD B2B 使用者和來賓使用者的意義相同。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-149">Typically, an Azure AD B2B user and guest user are synonymous.</span></span> <span data-ttu-id="ab3dc-150">因此，Azure AD B2B 共同作業使用者依預設是新增為具有 UserType = [來賓] 的使用者。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-150">Therefore, an Azure AD B2B collaboration user is added as a user with UserType = Guest by default.</span></span> <span data-ttu-id="ab3dc-151">不過，在某些情況下，合作夥伴組織是主機組織也所屬之較大組織的成員。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-151">However, in some cases, the partner organization is a member of a larger organization to which the host organization also belongs.</span></span> <span data-ttu-id="ab3dc-152">若是如此，主機組織可能會將合作夥伴組織中的使用者視為成員而非來賓。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-152">If so, the host organization might want to treat users in the partner organization as members instead of guests.</span></span> <span data-ttu-id="ab3dc-153">使用 Azure AD B2B 邀請管理員 API 來從夥伴組織新增或邀請使用者至主機組織作為成員。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-153">Use the Azure AD B2B Invitation Manager APIs to add or invite a user from the partner organization to the host organization as a member.</span></span>

## <a name="filter-for-guest-users-in-the-directory"></a><span data-ttu-id="ab3dc-154">篩選目錄中的來賓使用者</span><span class="sxs-lookup"><span data-stu-id="ab3dc-154">Filter for guest users in the directory</span></span>

![篩選來賓使用者](media/active-directory-b2b-user-properties/filter-guest-users.png)

## <a name="convert-usertype"></a><span data-ttu-id="ab3dc-156">轉換 UserType</span><span class="sxs-lookup"><span data-stu-id="ab3dc-156">Convert UserType</span></span>
<span data-ttu-id="ab3dc-157">目前，使用者可以使用 PowerShell 將 UserType 從 [成員] 轉換為 [來賓]，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-157">Currently, it is possible for users to convert UserType from Member to Guest and vice-versa by using PowerShell.</span></span> <span data-ttu-id="ab3dc-158">不過，UserType 屬性應該代表使用者與組織的關聯性。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-158">However, the UserType property is supposed to represent the user's relationship to the organization.</span></span> <span data-ttu-id="ab3dc-159">因此，只有在使用者與組織的關聯性變更時，才應該變更此屬性的值。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-159">Therefore, the value of this property should change only if the relationship of the user to the organization changes.</span></span> <span data-ttu-id="ab3dc-160">如果使用者的關聯性變更，是否應解決使用者主體名稱 (UPN) 是否應該變更等問題？</span><span class="sxs-lookup"><span data-stu-id="ab3dc-160">If the relationship of the user changes, should issues, like whether the user principal name (UPN) should change, be addressed?</span></span> <span data-ttu-id="ab3dc-161">使用者是否應該繼續存取相同的資源？</span><span class="sxs-lookup"><span data-stu-id="ab3dc-161">Should the user continue to have access to the same resources?</span></span> <span data-ttu-id="ab3dc-162">是否應指派信箱？</span><span class="sxs-lookup"><span data-stu-id="ab3dc-162">Should a mailbox be assigned?</span></span> <span data-ttu-id="ab3dc-163">因此，我們不建議以 PowerShell 做為不可部分完成的活動來變更 UserType 。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-163">Therefore, we do not recommend changing the UserType by using PowerShell as an atomic activity.</span></span> <span data-ttu-id="ab3dc-164">此外，為免使用 PowerShell 讓這個屬性成為不可變屬性，我們不建議採用此值的相依性。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-164">In addition, in case this property becomes immutable by using PowerShell, we do not recommend taking a dependency on this value.</span></span>

## <a name="remove-guest-user-limitations"></a><span data-ttu-id="ab3dc-165">移除來賓使用者限制</span><span class="sxs-lookup"><span data-stu-id="ab3dc-165">Remove guest user limitations</span></span>
<span data-ttu-id="ab3dc-166">在某些情況下，您要提供來賓使用者更高的權限。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-166">There may be cases where you want to give your guest users higher privileges.</span></span> <span data-ttu-id="ab3dc-167">您可以將來賓使用者新增至任何角色，甚至移除目錄中預設的來賓使用者限制，為使用者提供與成員相同的權限。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-167">You can add a guest user to any role and even remove the default guest user restrictions in the directory to give a user the same privileges as members.</span></span>

<span data-ttu-id="ab3dc-168">可以關閉預設來賓使用者限制，如此公司目錄中的來賓使用者便可獲得與成員使用者相同的權限。</span><span class="sxs-lookup"><span data-stu-id="ab3dc-168">It is possible to turn off the default guest user limitations so that a guest user in the company directory is given the same permissions as a member user.</span></span>

![移除來賓使用者限制](media/active-directory-b2b-user-properties/remove-guest-limitations.png)

## <a name="next-steps"></a><span data-ttu-id="ab3dc-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ab3dc-170">Next steps</span></span>

<span data-ttu-id="ab3dc-171">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="ab3dc-171">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="ab3dc-172">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="ab3dc-172">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="ab3dc-173">將 B2B 共同作業使用者新增至角色</span><span class="sxs-lookup"><span data-stu-id="ab3dc-173">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="ab3dc-174">委派 B2B 共同作業邀請</span><span class="sxs-lookup"><span data-stu-id="ab3dc-174">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="ab3dc-175">B2B 共同作業使用者稽核和報告</span><span class="sxs-lookup"><span data-stu-id="ab3dc-175">B2B collaboration user auditing and reporting</span></span>](active-directory-b2b-auditing-and-reporting.md)
* [<span data-ttu-id="ab3dc-176">動態群組與 B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="ab3dc-176">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="ab3dc-177">B2B 共同作業程式碼與 PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="ab3dc-177">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="ab3dc-178">設定適用於 B2B 共同作業的 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="ab3dc-178">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="ab3dc-179">B2B 共同作業使用者權杖</span><span class="sxs-lookup"><span data-stu-id="ab3dc-179">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="ab3dc-180">B2B 共同作業使用者宣告對應</span><span class="sxs-lookup"><span data-stu-id="ab3dc-180">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="ab3dc-181">Office 365 外部共用</span><span class="sxs-lookup"><span data-stu-id="ab3dc-181">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="ab3dc-182">B2B 共同作業目前的限制</span><span class="sxs-lookup"><span data-stu-id="ab3dc-182">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
