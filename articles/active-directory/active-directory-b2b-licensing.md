---
title: "Azure Active Directory B2B 共同作業授權指引 | Microsoft Docs"
description: "Azure Active Directory B2B 共同作業不需要 Azure AD 付費授權，但您也可以取得付費功能給 B2B 來賓使用者"
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
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: sasubram
ms.custom: it-pro
ms.openlocfilehash: dfef32c05af157ae8d3a5434016f87f488a35051
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2b-collaboration-licensing-guidance"></a><span data-ttu-id="0cb4b-103">Azure Active Directory B2B 共同作業授權指引</span><span class="sxs-lookup"><span data-stu-id="0cb4b-103">Azure Active Directory B2B collaboration licensing guidance</span></span>

<span data-ttu-id="0cb4b-104">您可以使用 Azure AD B2B 共同作業功能，將來賓使用者邀請至 Azure AD 租用戶，允許它們存取 Azure AD 服務和貴組織中的其他資源。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-104">You can use Azure AD B2B collaboration capabilities to invite guest users into your Azure AD tenant to allow them to access Azure AD services and other resources in your organization.</span></span> <span data-ttu-id="0cb4b-105">如果您不需要讓 B2B 共同作業來賓使用者存取 Azure AD 付費功能，他們就必須獲得適當的 Azure AD 授權。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-105">If you want to provide access to paid Azure AD features, B2B collaboration guest users must be licensed with appropriate Azure AD licenses.</span></span> 

<span data-ttu-id="0cb4b-106">具體而言：</span><span class="sxs-lookup"><span data-stu-id="0cb4b-106">Specifically:</span></span>
* <span data-ttu-id="0cb4b-107">Azure AD Free 功能可供來賓使用者使用，且無需額外的授權。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-107">Azure AD Free capabilities are available for guest users without additional licensing.</span></span>
* <span data-ttu-id="0cb4b-108">如果您需要讓 B2B 使用者存取 Azure AD 付費功能，就必須擁有足夠的授權，以支援這些 B2B 來賓使用者。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-108">If you want to provide access to paid Azure AD features to B2B users, you must have enough licenses to support those B2B guest users.</span></span>
* <span data-ttu-id="0cb4b-109">具有 Azure AD 付費授權的邀請方租用戶，擁有另外五位受邀加入租用戶之 B2B 來賓使用者的 B2B 共同作業使用權。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-109">An inviting tenant with an Azure AD paid license has B2B collaboration use rights to an additional five B2B guest users invited to the tenant.</span></span>
* <span data-ttu-id="0cb4b-110">擁有邀請方租用戶的客戶，必須決定多少位 B2B 共同作業使用者需要 Azure AD 付費功能。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-110">The customer who owns the inviting tenant must be the one to determine how many B2B collaboration users need paid Azure AD capabilities.</span></span> <span data-ttu-id="0cb4b-111">根據您需要取得給來賓使用者的 Azure AD 付費功能而定，您擁有的 Azure AD 付費授權必須足以涵蓋相同 5:1 比例的 B2B 共同作業使用者。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-111">Depending on the paid Azure AD features you want for your guest users, you must have enough Azure AD paid licenses to cover B2B collaboration users in the same 5:1 ratio.</span></span>

<span data-ttu-id="0cb4b-112">會從夥伴公司將 B2B 共同作業來賓使用者新增為使用者，而非貴組織的員工或貴企業集團中不同業務部門的員工。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-112">A B2B collaboration guest user is added as a user from a partner company, not an employee of your organization or an employee of a different business in your conglomerate.</span></span> <span data-ttu-id="0cb4b-113">B2B 來賓使用者可以使用外部認證或貴組織所擁有的認證來登入，如本文中所述。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-113">A B2B guest user can sign in with external credentials or credentials owned by your organization as described in this article.</span></span> 

<span data-ttu-id="0cb4b-114">換句話說，B2B 授權的設定方式並不是依使用者驗證，而是依貴組織使用者的關聯性。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-114">In other words, B2B licensing is set not by how the user authenticates but rather by the relationship of the user to your organization.</span></span> <span data-ttu-id="0cb4b-115">如果這些使用者並非夥伴，就會以不同的授權條款來處理。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-115">If these users are not partners, they are treated differently in licensing terms.</span></span> <span data-ttu-id="0cb4b-116">不會針對授權用途將它們視為 B2B 共同作業使用者，即使其 UserType 是標示為「來賓」。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-116">They are not considered to be a B2B collaboration user for licensing purposes even if their UserType is marked as “Guest.”</span></span> <span data-ttu-id="0cb4b-117">它們應以一般方式獲得授權，每個使用者獲得一項授權。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-117">They should be licensed normally, at one license per user.</span></span> <span data-ttu-id="0cb4b-118">這些使用者包括：</span><span class="sxs-lookup"><span data-stu-id="0cb4b-118">These users include:</span></span>
* <span data-ttu-id="0cb4b-119">您的員工</span><span class="sxs-lookup"><span data-stu-id="0cb4b-119">Your employees</span></span>
* <span data-ttu-id="0cb4b-120">使用外部身分識別登入的職員</span><span class="sxs-lookup"><span data-stu-id="0cb4b-120">Staff signing in using external identities</span></span>
* <span data-ttu-id="0cb4b-121">貴企業集團中不同業務部門的員工</span><span class="sxs-lookup"><span data-stu-id="0cb4b-121">An employee of a different business in your conglomerate</span></span>


## <a name="licensing-examples"></a><span data-ttu-id="0cb4b-122">授權範例</span><span class="sxs-lookup"><span data-stu-id="0cb4b-122">Licensing examples</span></span>
- <span data-ttu-id="0cb4b-123">客戶想要邀請 100 位 B2B 共同作業使用者加入其 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-123">A customer wants to invite 100 B2B collaboration users to its Azure AD tenant.</span></span> <span data-ttu-id="0cb4b-124">此客戶指派存取管理和佈建給所有使用者，但其中 50 位使用者還需要 MFA 和條件式存取。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-124">The customer assigns access management and provisioning for all users, but 50 users also require MFA and conditional access.</span></span> <span data-ttu-id="0cb4b-125">此客戶必須購買 10 個 Azure AD Basic 授權及 10 個 Azure AD Premium P1 授權，才能正確地涵蓋這些 B2B 使用者。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-125">This customer must purchase 10 Azure AD Basic licenses and 10 Azure AD Premium P1 licenses to cover these B2B users correctly.</span></span> <span data-ttu-id="0cb4b-126">如果客戶打算對 B2B 使用者使用「身分識別保護」功能，則他們必須有 Azure AD Premium P2 授權，才能涵蓋同樣 5:1 比例的受邀使用者。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-126">If the customer plans to use Identity Protection features with B2B users, they must have Azure AD Premium P2 licenses to cover the invited users in the same 5:1 ratio.</span></span>
- <span data-ttu-id="0cb4b-127">客戶有 10 位目前以 Azure AD「進階 P1」授權的員工。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-127">A customer has 10 employees who are all currently licensed with Azure AD Premium P1.</span></span> <span data-ttu-id="0cb4b-128">他們現在想邀請 60 位 B2B 使用者，而這些使用者全部都需多重要素驗證 (MFA)。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-128">They now want to invite 60 B2B users who all require multi-factor authentication (MFA).</span></span> <span data-ttu-id="0cb4b-129">依據 5:1 授權規則，此客戶必須至少有 12 個 Azure AD Premium P1 授權，才能涵蓋全部 60 位 B2B 共同作業使用者。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-129">Under the 5:1 licensing rule, the customer must have at least 12 Azure AD Premium P1 licenses to cover all 60 B2B collaboration users.</span></span> <span data-ttu-id="0cb4b-130">由於他們已經有 10 位員工的 10 個 Premium P1 授權，因此，他們有權使用 Premium P1 功能 (例如 MFA) 來邀請 50 位 B2B 使用者。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-130">Because they already have 10 Premium P1 licenses for their 10 employees, they have rights to invite 50 B2B users with Premium P1 features like MFA.</span></span> <span data-ttu-id="0cb4b-131">所以，在此範例中，他們必須再購買 2 個 Premium P1 授權，才能涵蓋剩餘的 10 位 B2B 共同作業使用者。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-131">In this example, then, they must purchase 2 additional Premium P1 licenses to cover the remaining 10 B2B collaboration users.</span></span>

> [!NOTE]
> <span data-ttu-id="0cb4b-132">尚無法直接將授權指派給 B2B 使用者，以啟用這些 B2B 共同作業使用者權限。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-132">There is no way yet to assign licenses directly to the B2B users to enable these B2B collaboration user rights.</span></span>

<span data-ttu-id="0cb4b-133">擁有邀請方租用戶的客戶，必須決定多少位 B2B 共同作業使用者需要 Azure AD 付費功能。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-133">The customer who owns the inviting tenant must be the one to determine how many B2B collaboration users need paid Azure AD capabilities.</span></span> <span data-ttu-id="0cb4b-134">根據您想要取得哪些 Azure AD 付費功能給來賓使用者而定，您擁有的 Azure AD 付費授權必須足以涵蓋 5:1 比例的 B2B 共同作業使用者。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-134">Depending on which paid Azure AD features you want for your guest users, you must have enough Azure AD paid licenses to cover B2B collaboration users in the 5:1 ratio.</span></span> 

## <a name="additional-licensing-details"></a><span data-ttu-id="0cb4b-135">其他授權詳細資料</span><span class="sxs-lookup"><span data-stu-id="0cb4b-135">Additional licensing details</span></span>
- <span data-ttu-id="0cb4b-136">並不需要將授權實際指派給 B2B 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-136">There is no need to actually assign licenses to B2B user accounts.</span></span> <span data-ttu-id="0cb4b-137">系統會根據 5:1 比例來自動計算和報告授權。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-137">Based on the 5:1 ratio, licensing is automatically calculated and reported.</span></span>
- <span data-ttu-id="0cb4b-138">如果租用戶中沒有 Azure AD 付費授權，則每位受邀使用者會獲得 Azure AD Free 版本所提供的權限。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-138">If no paid Azure AD license exists in the tenant, every invited user gets the rights that the Azure AD Free edition offers.</span></span>
- <span data-ttu-id="0cb4b-139">如果 B2B 共同作業使用者已從其組織獲得 Azure AD 付費授權，他就不會取用邀請方租用戶的其中一個 B2B 共同作業授權。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-139">If a B2B collaboration user already has a paid Azure AD license from their organization, they do not consume one of the B2B collaboration licenses of the inviting tenant.</span></span>

## <a name="advanced-discussion-what-are-the-licensing-considerations-when-we-add-users-from-a-conglomerate-organization-as-members-using-your-apis"></a><span data-ttu-id="0cb4b-140">進階討論：當我們使用您的 API 從某個集團組織新增使用者作為「成員」時，有什麼授權考量？</span><span class="sxs-lookup"><span data-stu-id="0cb4b-140">Advanced discussion: What are the licensing considerations when we add users from a conglomerate organization as “members” using your APIs?</span></span>
<span data-ttu-id="0cb4b-141">B2B 來賓使用者是從合作夥伴組織受邀來與主辦組織共同作業的使用者。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-141">A B2B guest user is one that is invited from a partner organization to work with the host organization.</span></span> <span data-ttu-id="0cb4b-142">一般而言，任何其他情況都不符合 B2B 資格，即使是使用 B2B 功能也一樣。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-142">Typically, any other case does not qualify as B2B even it uses B2B features.</span></span> <span data-ttu-id="0cb4b-143">讓我們來特別看看兩個案例：</span><span class="sxs-lookup"><span data-stu-id="0cb4b-143">Let’s look at two cases in particular:</span></span>

1. <span data-ttu-id="0cb4b-144">如果主辦組織使用取用者位址來邀請員工</span><span class="sxs-lookup"><span data-stu-id="0cb4b-144">If a host invites an employee using a consumer address</span></span>
  * <span data-ttu-id="0cb4b-145">此情節不符合我們的授權原則，不建議使用。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-145">This scenario is not compliant with our licensing policies and is not recommended.</span></span>

2. <span data-ttu-id="0cb4b-146">如果主辦組織從另一個集團組織新增使用者</span><span class="sxs-lookup"><span data-stu-id="0cb4b-146">If a host organization adds a user from another conglomerate organization</span></span>
  1. <span data-ttu-id="0cb4b-147">在此案例中是使用 B2B API 來邀請使用者，但此案例不是傳統的 B2B。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-147">In this case, the user is invited using B2B APIs, but this case is not traditionally B2B.</span></span> <span data-ttu-id="0cb4b-148">在理想情況下，我們應該讓這些組織邀請其他組織使用者作為成員 (我們的 API 允許這麼做)。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-148">Ideally, we should have these organizations invite the other orgs users as members (our API allows that).</span></span> <span data-ttu-id="0cb4b-149">在此情況下，必須將授權指派給這些成員，讓他們存取邀請組織中的資源。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-149">In this case, licenses have to be assigned to these members for them to access resources in the inviting organization.</span></span>

  2. <span data-ttu-id="0cb4b-150">有些組織可能會想要將另一個組織的使用者新增為「來賓」來作為一項原則。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-150">Some organizations may want to add the other org’s users to be added as “Guest” as a policy.</span></span> <span data-ttu-id="0cb4b-151">這裡有兩個案例：</span><span class="sxs-lookup"><span data-stu-id="0cb4b-151">There are two cases here:</span></span>
      * <span data-ttu-id="0cb4b-152">集團組織已經使用 Azure AD 且受邀的使用者已在另一個組織中獲得授權：在此情況下，我們不會預期受邀使用者需依循本文件稍早所配置的 1:5 公式。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-152">The conglomerate organization is already using Azure AD and the invited users are licensed in the other organization: in this case, we don’t expect invited users to need to follow the 1:5 formula laid out earlier in this document.</span></span> 

      * <span data-ttu-id="0cb4b-153">集團組織未使用 Azure AD 或沒有適當的授權：在此情況下，請依循本文件稍早所配置的 1:5 公式。</span><span class="sxs-lookup"><span data-stu-id="0cb4b-153">The conglomerate organization is not using Azure AD or doesn’t have adequate licenses: In this case, follow the 1:5 formula laid out earlier in this document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cb4b-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0cb4b-154">Next steps</span></span>

<span data-ttu-id="0cb4b-155">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="0cb4b-155">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="0cb4b-156">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="0cb4b-156">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="0cb4b-157">Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="0cb4b-157">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="0cb4b-158">資訊工作者如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="0cb4b-158">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="0cb4b-159">B2B 共同作業邀請電子郵件的元素</span><span class="sxs-lookup"><span data-stu-id="0cb4b-159">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="0cb4b-160">B2B 共同作業邀請兌換</span><span class="sxs-lookup"><span data-stu-id="0cb4b-160">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="0cb4b-161">針對 Azure Active Directory B2B 共同作業問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="0cb4b-161">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="0cb4b-162">Azure Active Directory B2B 共同作業常見問題 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="0cb4b-162">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="0cb4b-163">Azure Active Directory B2B 共同作業 API 和自訂</span><span class="sxs-lookup"><span data-stu-id="0cb4b-163">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="0cb4b-164">適用於 B2B 共同作業使用者的多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="0cb4b-164">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="0cb4b-165">在沒有邀請的情況下新增 B2B 共同作業使用者</span><span class="sxs-lookup"><span data-stu-id="0cb4b-165">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="0cb4b-166">Azure Active Directory 中應用程式管理的文章索引</span><span class="sxs-lookup"><span data-stu-id="0cb4b-166">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
