---
title: "Azure Active Directory B2B 共同作業的使用者存取 aaaConditional |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業的選擇性存取 tooyour 公司應用程式支援 multi-factor authentication (MFA)"
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
ms.openlocfilehash: 3a05be4393f74ff8e87f32432a222a5fbac9af62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="649c0-103">B2B 共同作業使用者的條件式存取</span><span class="sxs-lookup"><span data-stu-id="649c0-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="649c0-104">B2B 使用者的多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="649c0-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="649c0-105">在使用 Azure AD B2B 共同作業的情況下，組織會為 B2B 使用者強制執行 Multi-Factor Authentication (MFA) 原則。</span><span class="sxs-lookup"><span data-stu-id="649c0-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="649c0-106">這些原則可以強制執行在 hello 租用戶、 應用程式或個別使用者層級 hello 啟用這兩項全職員工和 hello 組織成員的方式相同。</span><span class="sxs-lookup"><span data-stu-id="649c0-106">These policies can be enforced at hello tenant, app, or individual user level, hello same way that they are enabled for full-time employees and members of hello organization.</span></span> <span data-ttu-id="649c0-107">在 hello 資源組織會強制執行 MFA 原則。</span><span class="sxs-lookup"><span data-stu-id="649c0-107">MFA policies are enforced at hello resource organization.</span></span>

<span data-ttu-id="649c0-108">範例：</span><span class="sxs-lookup"><span data-stu-id="649c0-108">Example:</span></span>
1. <span data-ttu-id="649c0-109">公司 A 中的系統管理員或資訊工作者邀請使用者從公司 B tooan 應用程式*Foo*公司 a。</span><span class="sxs-lookup"><span data-stu-id="649c0-109">Admin or information worker in Company A invites user from company B tooan application *Foo* in company A.</span></span>
2. <span data-ttu-id="649c0-110">應用程式*Foo*公司 A 是設定的 toorequire MFA 上存取。</span><span class="sxs-lookup"><span data-stu-id="649c0-110">Application *Foo* in company A is configured toorequire MFA on access.</span></span>
3. <span data-ttu-id="649c0-111">當從公司 B 的 hello 使用者嘗試 tooaccess 應用程式*Foo*在 hello 公司租用戶，它們是要求 toocomplete MFA 挑戰。</span><span class="sxs-lookup"><span data-stu-id="649c0-111">When hello user from company B attempts tooaccess app *Foo* in hello company A tenant, they are asked toocomplete an MFA challenge.</span></span>
4. <span data-ttu-id="649c0-112">hello 使用者可以設定其 MFA 搭配公司，並選擇其 MFA 選項。</span><span class="sxs-lookup"><span data-stu-id="649c0-112">hello user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="649c0-113">此案例對任何身分識別 (例如 Azure AD 或 MSA，若公司 B 的使用者使用社交識別碼來驗證) 都有效</span><span class="sxs-lookup"><span data-stu-id="649c0-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="649c0-114">公司 A 必須有足夠支援 MFA 的 Azure AD Premium 授權。</span><span class="sxs-lookup"><span data-stu-id="649c0-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="649c0-115">hello 使用者從公司 B 會消耗公司 a 本授權條款</span><span class="sxs-lookup"><span data-stu-id="649c0-115">hello user from company B consumes this license from company A.</span></span>

<span data-ttu-id="649c0-116">hello 邀請其他租用戶負責一律為 MFA hello 夥伴組織，使用者即使 hello 夥伴組織具有 MFA 功能。</span><span class="sxs-lookup"><span data-stu-id="649c0-116">hello inviting tenancy is always responsible for MFA for users from hello partner organization, even if hello partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="649c0-117">為 B2B 共同作業使用者設定 MFA</span><span class="sxs-lookup"><span data-stu-id="649c0-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="649c0-118">如何在 toodiscover 如何輕鬆是 tooset mfa B2B 共同作業的使用者，請參閱下列視訊 hello:</span><span class="sxs-lookup"><span data-stu-id="649c0-118">toodiscover how easy it is tooset up MFA for B2B collaboration users, see how in hello following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="649c0-119">方案兌換的 B2B 使用者 MFA 體驗</span><span class="sxs-lookup"><span data-stu-id="649c0-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="649c0-120">請參閱下列動畫 toosee hello 兌換經驗 hello:</span><span class="sxs-lookup"><span data-stu-id="649c0-120">Check out hello following animation toosee hello redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="649c0-121">B2B 共同作業使用者的 MFA 重設</span><span class="sxs-lookup"><span data-stu-id="649c0-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="649c0-122">目前，hello 系統管理員可以要求 B2B 共同作業的使用者 tooproof 向上一次只能藉由使用下列 PowerShell 指令程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="649c0-122">Currently, hello admin can require B2B collaboration users tooproof up again only by using hello following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="649c0-123">連接 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="649c0-123">Connect tooAzure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="649c0-124">取得具有證明方法的所有使用者</span><span class="sxs-lookup"><span data-stu-id="649c0-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="649c0-125">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="649c0-125">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="649c0-126">一次重設特定使用者 toorequire hello B2B 共同作業使用者 tooset 提升方法的 hello MFA 方法。</span><span class="sxs-lookup"><span data-stu-id="649c0-126">Reset hello MFA method for a specific user toorequire hello B2B collaboration user tooset proof-up methods again.</span></span> <span data-ttu-id="649c0-127">範例：</span><span class="sxs-lookup"><span data-stu-id="649c0-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-hello-resource-tenancy"></a><span data-ttu-id="649c0-128">我們要為什麼在 hello 資源的租用戶執行 MFA？</span><span class="sxs-lookup"><span data-stu-id="649c0-128">Why do we perform MFA at hello resource tenancy?</span></span>

<span data-ttu-id="649c0-129">在 hello 目前版本中，MFA 一定是在 hello 資源的租用戶，如可預測性的原因。</span><span class="sxs-lookup"><span data-stu-id="649c0-129">In hello current release, MFA is always in hello resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="649c0-130">例如，假設 Contoso 使用者 (Sally) 是受邀的 tooFabrikam 並 Fabrikam B2B 使用者啟用 MFA。</span><span class="sxs-lookup"><span data-stu-id="649c0-130">For example, let’s say a Contoso user (Sally) is invited tooFabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="649c0-131">如果 Contoso 啟用 App1 但不是 App2 的 MFA 原則，然後如果我們看一下 hello Contoso MFA 宣告在 hello 權杖中，我們可能會看到下列問題的 hello:</span><span class="sxs-lookup"><span data-stu-id="649c0-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at hello Contoso MFA claim in hello token, we might see hello following issue:</span></span>

* <span data-ttu-id="649c0-132">第 1 天：使用者有 Contoso 的 MFA 並存取 App1，Fabrikam 不顯示其他 MFA 提示。</span><span class="sxs-lookup"><span data-stu-id="649c0-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="649c0-133">第 2 天： hello 使用者存取應用程式 2，在 Contoso，因此，現在存取 Fabrikam 時，它們必須那里註冊 MFA。</span><span class="sxs-lookup"><span data-stu-id="649c0-133">Day 2: hello user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="649c0-134">此程序可能會造成混淆，並可能導致 toodrop 中登入完成。</span><span class="sxs-lookup"><span data-stu-id="649c0-134">This process can be confusing and could lead toodrop in sign-in completions.</span></span>

<span data-ttu-id="649c0-135">此外，即使 Contoso 的 MFA 功能，它不一定 hello 案例 hello Fabrikam 會信任 hello Contoso MFA 原則。</span><span class="sxs-lookup"><span data-stu-id="649c0-135">Moreover, even if Contoso has MFA capability, it is not always hello case hello Fabrikam would trust hello Contoso MFA policy.</span></span>

<span data-ttu-id="649c0-136">最後，資源租用戶 MFA 也適用於 MSA 和社交識別碼，以及未設定 MFA 的合作夥伴組織。</span><span class="sxs-lookup"><span data-stu-id="649c0-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="649c0-137">因此，MFA B2B 使用者 hello 建議是 tooalways hello 邀請租用戶中要求使用 MFA。</span><span class="sxs-lookup"><span data-stu-id="649c0-137">Therefore, hello recommendation for MFA for B2B users is tooalways require MFA in hello inviting tenant.</span></span> <span data-ttu-id="649c0-138">這項需求可能會導致 toodouble MFA，在某些情況下，但存取 hello 邀請其他租用戶，每當 hello 使用者體驗是可預測： Sally 必須與 hello 邀請其他租用戶註冊 MFA。</span><span class="sxs-lookup"><span data-stu-id="649c0-138">This requirement could lead toodouble MFA in some cases, but whenever accessing hello inviting tenant, hello end-users experience is predictable: Sally must register for MFA with hello inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="649c0-139">B2B 使用者的裝置型、位置型及風險型條件式存取。</span><span class="sxs-lookup"><span data-stu-id="649c0-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="649c0-140">當 Contoso 可讓其公司資料的裝置型條件式存取原則時，未受管理 Contoso 和與 hello Contoso 裝置原則不相容的裝置將無法存取。</span><span class="sxs-lookup"><span data-stu-id="649c0-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with hello Contoso device policies.</span></span>

<span data-ttu-id="649c0-141">如果 hello B2B 使用者的裝置不是由 Contoso 管理，B2B 使用者從 hello 夥伴組織的存取權會封鎖這些原則會強制執行任何內容中。</span><span class="sxs-lookup"><span data-stu-id="649c0-141">If hello B2B user’s device isn't managed by Contoso, access of B2B users from hello partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="649c0-142">不過，Contoso 可以建立排除清單包含特定的夥伴使用者 tooexclude 從 hello 裝置型條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="649c0-142">However, Contoso can create exclusion lists containing specific partner users tooexclude them from hello device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="649c0-143">B2B 的位置型條件式存取</span><span class="sxs-lookup"><span data-stu-id="649c0-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="649c0-144">以位置為基礎的條件式存取原則可以強制執行 B2B 使用者若 hello 邀請其他組織能夠 toocreate 受信任的 IP 位址範圍的定義夥伴組織。</span><span class="sxs-lookup"><span data-stu-id="649c0-144">Location-based conditional access policies can be enforced for B2B users if hello inviting organization is able toocreate a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="649c0-145">B2B 的風險型條件式存取</span><span class="sxs-lookup"><span data-stu-id="649c0-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="649c0-146">目前，風險依據登入的原則無法套用的 tooB2B 使用者因為 hello 風險評估在 hello B2B 使用者的主要組織中執行。</span><span class="sxs-lookup"><span data-stu-id="649c0-146">Currently, risk-based sign-in policies cannot be applied tooB2B users because hello risk evaluation is performed at hello B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="649c0-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="649c0-147">Next steps</span></span>

<span data-ttu-id="649c0-148">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="649c0-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="649c0-149">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="649c0-149">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="649c0-150">Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="649c0-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="649c0-151">資訊工作者如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="649c0-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="649c0-152">hello hello B2B 共同作業邀請電子郵件項目</span><span class="sxs-lookup"><span data-stu-id="649c0-152">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="649c0-153">B2B 共同作業邀請兌換</span><span class="sxs-lookup"><span data-stu-id="649c0-153">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="649c0-154">Azure AD B2B 共同作業授權</span><span class="sxs-lookup"><span data-stu-id="649c0-154">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="649c0-155">針對 Azure Active Directory B2B 共同作業問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="649c0-155">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="649c0-156">Azure Active Directory B2B 共同作業常見問題 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="649c0-156">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="649c0-157">Azure Active Directory B2B 共同作業 API 和自訂</span><span class="sxs-lookup"><span data-stu-id="649c0-157">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="649c0-158">在沒有邀請的情況下新增 B2B 共同作業使用者</span><span class="sxs-lookup"><span data-stu-id="649c0-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="649c0-159">Azure Active Directory 中應用程式管理的文章索引</span><span class="sxs-lookup"><span data-stu-id="649c0-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
