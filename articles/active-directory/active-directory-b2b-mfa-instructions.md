---
title: "Azure Active Directory B2B 共同作業使用者的條件式存取 | Microsoft Docs"
description: "Azure Active Directory B2B 共同作業支援多重要素驗證 (MFA) 以對您的公司應用程式進行選擇性存取"
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: d85f711d6551a68d1248ae8ec61e2ecc1ddc8ecd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="067c8-103">B2B 共同作業使用者的條件式存取</span><span class="sxs-lookup"><span data-stu-id="067c8-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="067c8-104">B2B 使用者的多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="067c8-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="067c8-105">在使用 Azure AD B2B 共同作業的情況下，組織會為 B2B 使用者強制執行 Multi-Factor Authentication (MFA) 原則。</span><span class="sxs-lookup"><span data-stu-id="067c8-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="067c8-106">這些原則可以在租用戶層級、應用程式或個別使用者層級強制執行，也同樣針對組織的全職員工和成員啟用。</span><span class="sxs-lookup"><span data-stu-id="067c8-106">These policies can be enforced at the tenant, app, or individual user level, the same way that they are enabled for full-time employees and members of the organization.</span></span> <span data-ttu-id="067c8-107">MFA 原則會在資源組織強制執行。</span><span class="sxs-lookup"><span data-stu-id="067c8-107">MFA policies are enforced at the resource organization.</span></span>

<span data-ttu-id="067c8-108">範例：</span><span class="sxs-lookup"><span data-stu-id="067c8-108">Example:</span></span>
1. <span data-ttu-id="067c8-109">公司 A 中的系統管理員或資訊工作者邀請公司 B 的使用者使用公司 A 的應用程式 *Foo*。</span><span class="sxs-lookup"><span data-stu-id="067c8-109">Admin or information worker in Company A invites user from company B to an application *Foo* in company A.</span></span>
2. <span data-ttu-id="067c8-110">公司 A 中的應用程式 *Foo* 是設定為要求在存取時使用 MFA。</span><span class="sxs-lookup"><span data-stu-id="067c8-110">Application *Foo* in company A is configured to require MFA on access.</span></span>
3. <span data-ttu-id="067c8-111">當公司 B 的使用者嘗試存取公司 A 租用戶的應用程式 *Foo* 時，系統會要求他們完成 MFA 查問。</span><span class="sxs-lookup"><span data-stu-id="067c8-111">When the user from company B attempts to access app *Foo* in the company A tenant, they are asked to complete an MFA challenge.</span></span>
4. <span data-ttu-id="067c8-112">使用者可以設定他們的公司 A MFA，選擇其 MFA 選項。</span><span class="sxs-lookup"><span data-stu-id="067c8-112">The user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="067c8-113">此案例對任何身分識別 (例如 Azure AD 或 MSA，若公司 B 的使用者使用社交識別碼來驗證) 都有效</span><span class="sxs-lookup"><span data-stu-id="067c8-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="067c8-114">公司 A 必須有足夠支援 MFA 的 Azure AD Premium 授權。</span><span class="sxs-lookup"><span data-stu-id="067c8-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="067c8-115">公司 B 的使用者會取用公司 A 的授權。</span><span class="sxs-lookup"><span data-stu-id="067c8-115">The user from company B consumes this license from company A.</span></span>

<span data-ttu-id="067c8-116">發出邀請的租用一律必須負責夥伴組織使用者的 MFA，即使夥伴組織本身具有 MFA 能力。</span><span class="sxs-lookup"><span data-stu-id="067c8-116">The inviting tenancy is always responsible for MFA for users from the partner organization, even if the partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="067c8-117">為 B2B 共同作業使用者設定 MFA</span><span class="sxs-lookup"><span data-stu-id="067c8-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="067c8-118">若要了解為 B2B 共同作業使用者設定 MFA 有多簡單，請觀看下列影片：</span><span class="sxs-lookup"><span data-stu-id="067c8-118">To discover how easy it is to set up MFA for B2B collaboration users, see how in the following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="067c8-119">方案兌換的 B2B 使用者 MFA 體驗</span><span class="sxs-lookup"><span data-stu-id="067c8-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="067c8-120">觀看下面的動畫以了解兌換體驗：</span><span class="sxs-lookup"><span data-stu-id="067c8-120">Check out the following animation to see the redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="067c8-121">B2B 共同作業使用者的 MFA 重設</span><span class="sxs-lookup"><span data-stu-id="067c8-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="067c8-122">目前，系統管理員只能使用 PowerShell Cmdlet 要求 B2B 共同作業使用者重新證明：</span><span class="sxs-lookup"><span data-stu-id="067c8-122">Currently, the admin can require B2B collaboration users to proof up again only by using the following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="067c8-123">連接至 Azure AD</span><span class="sxs-lookup"><span data-stu-id="067c8-123">Connect to Azure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="067c8-124">取得具有證明方法的所有使用者</span><span class="sxs-lookup"><span data-stu-id="067c8-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="067c8-125">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="067c8-125">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="067c8-126">重設特定使用者的 MFA 方法，要求 B2B 共同作業使用者再次設定證明方法。</span><span class="sxs-lookup"><span data-stu-id="067c8-126">Reset the MFA method for a specific user to require the B2B collaboration user to set proof-up methods again.</span></span> <span data-ttu-id="067c8-127">範例：</span><span class="sxs-lookup"><span data-stu-id="067c8-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-the-resource-tenancy"></a><span data-ttu-id="067c8-128">為什麼我們要在資源租用執行 MFA？</span><span class="sxs-lookup"><span data-stu-id="067c8-128">Why do we perform MFA at the resource tenancy?</span></span>

<span data-ttu-id="067c8-129">在目前的版本中，基於預測性的原因，MFA 一律位在資源租用中。</span><span class="sxs-lookup"><span data-stu-id="067c8-129">In the current release, MFA is always in the resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="067c8-130">例如，假設 Contoso 使用者 (Sally) 受邀到 Fabrikam，而且 Fabrikam 已經為 B2B 使用者啟用 MFA。</span><span class="sxs-lookup"><span data-stu-id="067c8-130">For example, let’s say a Contoso user (Sally) is invited to Fabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="067c8-131">如果 Contoso 為 App1 啟用了 MFA 原則，沒有為 App2 啟用，則若查閱權杖中的 Contoso MFA 宣告，可能會發現下列問題：</span><span class="sxs-lookup"><span data-stu-id="067c8-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at the Contoso MFA claim in the token, we might see the following issue:</span></span>

* <span data-ttu-id="067c8-132">第 1 天：使用者有 Contoso 的 MFA 並存取 App1，Fabrikam 不顯示其他 MFA 提示。</span><span class="sxs-lookup"><span data-stu-id="067c8-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="067c8-133">第 2 天：使用者存取了 Contoso 的 App2，而當他們要存取 Fabrikam 時，必須註冊那裡的 MFA。</span><span class="sxs-lookup"><span data-stu-id="067c8-133">Day 2: The user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="067c8-134">此程序令人混淆，而且可能會中斷登入作業。</span><span class="sxs-lookup"><span data-stu-id="067c8-134">This process can be confusing and could lead to drop in sign-in completions.</span></span>

<span data-ttu-id="067c8-135">此外，即使 Contoso 具有 MFA 功能，Fabrikam 也未必一定會信任 Contoso MFA 原則。</span><span class="sxs-lookup"><span data-stu-id="067c8-135">Moreover, even if Contoso has MFA capability, it is not always the case the Fabrikam would trust the Contoso MFA policy.</span></span>

<span data-ttu-id="067c8-136">最後，資源租用戶 MFA 也適用於 MSA 和社交識別碼，以及未設定 MFA 的合作夥伴組織。</span><span class="sxs-lookup"><span data-stu-id="067c8-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="067c8-137">因此，針對 B2B 使用者的 MFA 建議是一律要求使用邀請方租用戶的 MFA。</span><span class="sxs-lookup"><span data-stu-id="067c8-137">Therefore, the recommendation for MFA for B2B users is to always require MFA in the inviting tenant.</span></span> <span data-ttu-id="067c8-138">在某些情況下，此要求可能會導致雙重 MFA，但每次存取邀請方租用戶時的使用者體驗都會是可預測的：Sally 必須向邀請方租用戶註冊 MFA。</span><span class="sxs-lookup"><span data-stu-id="067c8-138">This requirement could lead to double MFA in some cases, but whenever accessing the inviting tenant, the end-users experience is predictable: Sally must register for MFA with the inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="067c8-139">B2B 使用者的裝置型、位置型及風險型條件式存取。</span><span class="sxs-lookup"><span data-stu-id="067c8-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="067c8-140">當 Contoso 為其公司資料啟用裝置型條件式存取原則時，系統會防止未受 Contoso 管理且不符合 Contoso 裝置原則的裝置進行存取。</span><span class="sxs-lookup"><span data-stu-id="067c8-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with the Contoso device policies.</span></span>

<span data-ttu-id="067c8-141">如果 B2B 使用者的裝置未受 Contoso 管理，當 B2B 使用者從夥伴組織進行存取時，只要是在強制執行這些原則的內容中，系統就會封鎖其存取。</span><span class="sxs-lookup"><span data-stu-id="067c8-141">If the B2B user’s device isn't managed by Contoso, access of B2B users from the partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="067c8-142">不過，Contoso 可以建立包含特定合作夥伴使用者的排除清單，將他們排除在裝置型條件式存取原則之外。</span><span class="sxs-lookup"><span data-stu-id="067c8-142">However, Contoso can create exclusion lists containing specific partner users to exclude them from the device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="067c8-143">B2B 的位置型條件式存取</span><span class="sxs-lookup"><span data-stu-id="067c8-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="067c8-144">如果邀請組織能夠建立定義其合作夥伴組織的受信任 IP 位址範圍，便可以針對 B2B 使用者強制執行位置型條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="067c8-144">Location-based conditional access policies can be enforced for B2B users if the inviting organization is able to create a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="067c8-145">B2B 的風險型條件式存取</span><span class="sxs-lookup"><span data-stu-id="067c8-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="067c8-146">目前，風險型登入原則無法套用至 B2B 使用者，因為風險評估是在 B2B 使用者的主要組織執行。</span><span class="sxs-lookup"><span data-stu-id="067c8-146">Currently, risk-based sign-in policies cannot be applied to B2B users because the risk evaluation is performed at the B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="067c8-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="067c8-147">Next steps</span></span>

<span data-ttu-id="067c8-148">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="067c8-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="067c8-149">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="067c8-149">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="067c8-150">Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="067c8-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="067c8-151">資訊工作者如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="067c8-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="067c8-152">B2B 共同作業邀請電子郵件的元素</span><span class="sxs-lookup"><span data-stu-id="067c8-152">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="067c8-153">B2B 共同作業邀請兌換</span><span class="sxs-lookup"><span data-stu-id="067c8-153">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="067c8-154">Azure AD B2B 共同作業授權</span><span class="sxs-lookup"><span data-stu-id="067c8-154">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="067c8-155">針對 Azure Active Directory B2B 共同作業問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="067c8-155">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="067c8-156">Azure Active Directory B2B 共同作業常見問題 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="067c8-156">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="067c8-157">Azure Active Directory B2B 共同作業 API 和自訂</span><span class="sxs-lookup"><span data-stu-id="067c8-157">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="067c8-158">在沒有邀請的情況下新增 B2B 共同作業使用者</span><span class="sxs-lookup"><span data-stu-id="067c8-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="067c8-159">Azure Active Directory 中應用程式管理的文章索引</span><span class="sxs-lookup"><span data-stu-id="067c8-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
