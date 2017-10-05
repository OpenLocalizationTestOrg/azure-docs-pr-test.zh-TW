---
title: "什麼是 Azure Active Directory B2B 共同作業？ | Microsoft Docs"
description: "Azure Active Directory B2B 共同作業讓企業合作夥伴選擇性地存取您的公司應用程式，以支援公司間的關係。"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 1464387b-ee8b-4c7c-94b3-2c5567224c27
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 06/27/2017
ms.author: curtand
ms.custom: aaddev
ms.reviewer: sasubram
ms.openlocfilehash: fbc12a52555b190d43b5e953fd4d19923a25b0ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-ad-b2b-collaboration"></a><span data-ttu-id="7264e-104">什麼是 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="7264e-104">What is Azure AD B2B collaboration?</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/AhwrweCBdsc" frameborder="0" allowfullscreen></iframe>

<span data-ttu-id="7264e-105">Azure AD 企業對企業 (B2B) 共同作業功能可讓任何使用 Azure AD 的組織 (不論規模大小)，安全地與來自任何其他組織的使用者共同作業。</span><span class="sxs-lookup"><span data-stu-id="7264e-105">Azure AD business-to-business (B2B) collaboration capabilities enable any organization using Azure AD to work safely and securely with users from any other organization, small or large.</span></span> <span data-ttu-id="7264e-106">這些組織可以有或沒有 Azure AD，或甚至可以有或沒有 IT 組織。</span><span class="sxs-lookup"><span data-stu-id="7264e-106">Those organizations can be with Azure AD or without, or even with an IT organization or without.</span></span> 

<span data-ttu-id="7264e-107">使用 Azure AD 的組織可以將文件、資源及應用程式的存取權提供給它們的合作夥伴，同時又保有其本身公司資料的完整控制權。</span><span class="sxs-lookup"><span data-stu-id="7264e-107">Organizations using Azure AD can provide access to documents, resources, and applications to their partners, while maintaining complete control over their own corporate data.</span></span> <span data-ttu-id="7264e-108">開發人員可以使用 Azure AD 企業對企業 API 來撰寫應用程式，以更安全的方式將兩個組織結合在一起。</span><span class="sxs-lookup"><span data-stu-id="7264e-108">Developers can use the Azure AD business-to-business APIs to write applications that bring two organizations together in more securely.</span></span> <span data-ttu-id="7264e-109">還可讓使用者相當輕鬆地瀏覽。</span><span class="sxs-lookup"><span data-stu-id="7264e-109">Also, it's pretty easy for end users to navigate.</span></span>

<span data-ttu-id="7264e-110">我們的客戶中有 97% 告訴我們，Azure AD B2B 共同作業對他們非常重要。</span><span class="sxs-lookup"><span data-stu-id="7264e-110">97% of our customers have told us Azure AD B2B collaboration is very important to them.</span></span>

![圓形圖](media/active-directory-b2b-what-is-azure-ad-b2b/97-percent-support.png)

<span data-ttu-id="7264e-112">截至 2017 年 4 月初為止，我們有大約三百萬個使用者已經使用 Azure AD B2B 共同作業功能。</span><span class="sxs-lookup"><span data-stu-id="7264e-112">As of early April 2017, we had about 3 million users already using Azure AD B2B collaboration capabilities.</span></span> <span data-ttu-id="7264e-113">而有超過 23% 有 10 個使用者以上的 Azure AD 組織已經從這些功能獲益。</span><span class="sxs-lookup"><span data-stu-id="7264e-113">And more than 23% of Azure AD organizations that have more than 10 users are already benefiting from these capabilities.</span></span>

## <a name="the-key-benefits-of-azure-ad-b2b-collaboration-to-your-organization"></a><span data-ttu-id="7264e-114">Azure AD B2B 共同作業可為您組織提供的主要優點</span><span class="sxs-lookup"><span data-stu-id="7264e-114">The key benefits of Azure AD B2B collaboration to your organization</span></span>

### <a name="work-with-any-user-from-any-partner"></a><span data-ttu-id="7264e-115">可與來自任何合作夥伴的任何使用者共同作業</span><span class="sxs-lookup"><span data-stu-id="7264e-115">Work with any user from any partner</span></span>

* <span data-ttu-id="7264e-116">合作夥伴可使用他們自己的認證</span><span class="sxs-lookup"><span data-stu-id="7264e-116">Partners use their own credentials</span></span>

* <span data-ttu-id="7264e-117">合作夥伴不一定要使用 Azure AD</span><span class="sxs-lookup"><span data-stu-id="7264e-117">No requirement for partners to use Azure AD</span></span>

* <span data-ttu-id="7264e-118">不需要外部目錄或複雜的設定</span><span class="sxs-lookup"><span data-stu-id="7264e-118">No external directories or complex set-up required</span></span>

### <a name="simple-and-secure-collaboration"></a><span data-ttu-id="7264e-119">簡單且安全的共同作業</span><span class="sxs-lookup"><span data-stu-id="7264e-119">Simple and secure collaboration</span></span>

* <span data-ttu-id="7264e-120">可提供對任何公司應用程式或資料的存取權，同時又套用精密、Azure AD 提供技術的授權原則</span><span class="sxs-lookup"><span data-stu-id="7264e-120">Provide access to any corporate app or data, while applying sophisticated, Azure AD-powered authorization policies</span></span>

* <span data-ttu-id="7264e-121">方便使用者</span><span class="sxs-lookup"><span data-stu-id="7264e-121">Easy for users</span></span>

* <span data-ttu-id="7264e-122">企業級的應用程式與資料安全性</span><span class="sxs-lookup"><span data-stu-id="7264e-122">Enterprise-grade security for apps and data</span></span>

### <a name="no-management-overhead"></a><span data-ttu-id="7264e-123">沒有任何額外的管理負荷</span><span class="sxs-lookup"><span data-stu-id="7264e-123">No management overhead</span></span>

* <span data-ttu-id="7264e-124">不需要進行任何外部帳戶或密碼管理</span><span class="sxs-lookup"><span data-stu-id="7264e-124">No external account or password management</span></span>

* <span data-ttu-id="7264e-125">不需要進行任何同步處理或手動帳戶生命週期管理</span><span class="sxs-lookup"><span data-stu-id="7264e-125">No sync or manual account lifecycle management</span></span>

* <span data-ttu-id="7264e-126">沒有任何額外的外部系統管理負荷</span><span class="sxs-lookup"><span data-stu-id="7264e-126">No external administrative overhead</span></span>

## <a name="you-can-easily-add-b2b-collaboration-users-to-your-organization"></a><span data-ttu-id="7264e-127">您可以將 B2B 共同作業使用者輕鬆地新增到您的組織</span><span class="sxs-lookup"><span data-stu-id="7264e-127">You can easily add B2B collaboration users to your organization</span></span>

<span data-ttu-id="7264e-128">系統管理員可以在 [Azure 入口網站](https://portal.azure.com)中新增 B2B 共同作業 (來賓) 使用者。</span><span class="sxs-lookup"><span data-stu-id="7264e-128">Admins can add B2B collaboration (guest) users in the [Azure portal](https://portal.azure.com).</span></span>

![新增來賓使用者](media/active-directory-b2b-what-is-azure-ad-b2b/adding-b2b-users-admin.png)

### <a name="enable-your-collaborators-to-bring-their-own-identity"></a><span data-ttu-id="7264e-130">讓您的共同作業者使用自己的身分識別</span><span class="sxs-lookup"><span data-stu-id="7264e-130">Enable your collaborators to bring their own identity</span></span>

<span data-ttu-id="7264e-131">B2B 共同作業者可以使用自己選擇的身分識別來登入。</span><span class="sxs-lookup"><span data-stu-id="7264e-131">B2B collaborators can sign in with an identity of their choice.</span></span> <span data-ttu-id="7264e-132">如果使用者沒有 Microsoft 帳戶或 Azure AD 帳戶 – 系統就會在他們兌換提供項目時為他們建立一個帳戶。</span><span class="sxs-lookup"><span data-stu-id="7264e-132">If the user doesn’t have a Microsoft account or an Azure AD account – one is created for them seamlessly at the time for offer redemption.</span></span>

![登入身分識別選項](media/active-directory-b2b-what-is-azure-ad-b2b/sign-in-identity-choice.png)

### <a name="delegate-to-application-and-group-owners"></a><span data-ttu-id="7264e-134">委派給應用程式和群組擁有者</span><span class="sxs-lookup"><span data-stu-id="7264e-134">Delegate to application and group owners</span></span> 
<span data-ttu-id="7264e-135">應用程式和群組擁有者可以將 B2B 使用者直接新增到您在意的任何應用程式，不論它是否為 Microsoft 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7264e-135">Application and group owners can add B2B users directly to any application that you care about, whether it is a Microsoft application or not.</span></span> <span data-ttu-id="7264e-136">系統管理員可以將新增 B2B 使用者的權限委派給非系統管理員。</span><span class="sxs-lookup"><span data-stu-id="7264e-136">Admins can delegate permission to add B2B users to non-admins.</span></span> <span data-ttu-id="7264e-137">非系統管理員可以使用 [Azure AD 應用程式存取面板](https://myapps.microsoft.com)，將 B2B 共同作業使用者新增到應用程式或群組。</span><span class="sxs-lookup"><span data-stu-id="7264e-137">Non-admins can use the [Azure AD Application Access Panel](https://myapps.microsoft.com) to add B2B collaboration users to applications or groups.</span></span>

![存取面板](media/active-directory-b2b-what-is-azure-ad-b2b/access-panel.png)

![新增成員](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="authorization-policies-protect-your-corporate-content"></a><span data-ttu-id="7264e-140">授權原則可保護您的公司內容</span><span class="sxs-lookup"><span data-stu-id="7264e-140">Authorization policies protect your corporate content</span></span>

<span data-ttu-id="7264e-141">可以強制執行條件式存取原則，例如多重要素驗證：</span><span class="sxs-lookup"><span data-stu-id="7264e-141">Conditional access policies, such as multi-factor authentication, can be enforced:</span></span>
- <span data-ttu-id="7264e-142">在租用戶層級</span><span class="sxs-lookup"><span data-stu-id="7264e-142">At the tenant level</span></span>
- <span data-ttu-id="7264e-143">在應用程式層級</span><span class="sxs-lookup"><span data-stu-id="7264e-143">At the application level</span></span>
- <span data-ttu-id="7264e-144">針對特定使用者來保護公司應用程式和資料</span><span class="sxs-lookup"><span data-stu-id="7264e-144">For specific users to protect corporate apps and data</span></span>

![新增成員](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="use-our-apis-and-sample-code-to-easily-build-applications-to-onboard"></a><span data-ttu-id="7264e-146">使用我們的 API 和範例程式碼來輕鬆建置要上線的應用程式</span><span class="sxs-lookup"><span data-stu-id="7264e-146">Use our APIs and sample code to easily build applications to onboard</span></span>
<span data-ttu-id="7264e-147">讓您的外部合作夥伴以針對您組織需求量身打造的方式上線使用</span><span class="sxs-lookup"><span data-stu-id="7264e-147">Bring your external partners on board in ways customized to your organization’s needs.</span></span>

<span data-ttu-id="7264e-148">您可以使用 [B2B 共同作業邀請 API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation) 來自訂入門訓練體驗，包括建立自助式註冊入口網站。</span><span class="sxs-lookup"><span data-stu-id="7264e-148">Using the [B2B collaboration invitation APIs](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), you can customize your onboarding experiences, including creating self-service sign-up portals.</span></span> <span data-ttu-id="7264e-149">我們[在 Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web) 提供自助式入口網站的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="7264e-149">We provide sample code for a self-service portal [on Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

![註冊入口網站](media/active-directory-b2b-what-is-azure-ad-b2b/sign-up-portal.png)

<span data-ttu-id="7264e-151">使用 Azure AD B2B 共同作業，您便可以運用 Azure AD 的完整強大功能，以使用者覺得簡單且直覺的方式來保護您的合作夥伴關係。</span><span class="sxs-lookup"><span data-stu-id="7264e-151">With Azure AD B2B collaboration, you can get the full power of Azure AD to protect your partner relationships in a way that end users find easy and intuitive.</span></span> <span data-ttu-id="7264e-152">因此，請不要猶豫，加入成為已使用 Azure AD B2B 進行其外部共同作業之數千個組織的一員吧！</span><span class="sxs-lookup"><span data-stu-id="7264e-152">So go ahead, join the thousands of organizations that are already using Azure AD B2B for their external collaboration!</span></span>

## <a name="next-steps"></a><span data-ttu-id="7264e-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7264e-153">Next steps</span></span>

* <span data-ttu-id="7264e-154">系統管理員體驗是在 [Azure 入口網站](https://portal.azure.com)中進行。</span><span class="sxs-lookup"><span data-stu-id="7264e-154">Administrator experiences are found in the [Azure portal](https://portal.azure.com).</span></span>

* <span data-ttu-id="7264e-155">資訊工作者體驗可在[存取面板](https://myapps.microsoft.com)中進行。</span><span class="sxs-lookup"><span data-stu-id="7264e-155">Information worker experiences are available in the [Access Panel](https://myapps.microsoft.com).</span></span>

* <span data-ttu-id="7264e-156">一如往常，如有任何意見反應、討論及建議，請透過我們的 [Microsoft 技術社群 (英文)](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b)，與產品小組聯繫。</span><span class="sxs-lookup"><span data-stu-id="7264e-156">And, as always, connect with the product team for any feedback, discussions, and suggestions through our [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).</span></span>

<span data-ttu-id="7264e-157">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="7264e-157">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="7264e-158">Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="7264e-158">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="7264e-159">資訊工作者如何新增 B2B 共同作業使用者？</span><span class="sxs-lookup"><span data-stu-id="7264e-159">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="7264e-160">B2B 共同作業邀請電子郵件的元素</span><span class="sxs-lookup"><span data-stu-id="7264e-160">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="7264e-161">B2B 共同作業邀請兌換</span><span class="sxs-lookup"><span data-stu-id="7264e-161">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="7264e-162">Azure AD B2B 共同作業授權</span><span class="sxs-lookup"><span data-stu-id="7264e-162">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="7264e-163">針對 Azure Active Directory B2B 共同作業問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="7264e-163">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="7264e-164">Azure Active Directory B2B 共同作業常見問題 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="7264e-164">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="7264e-165">Azure Active Directory B2B 共同作業 API 和自訂</span><span class="sxs-lookup"><span data-stu-id="7264e-165">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="7264e-166">適用於 B2B 共同作業使用者的多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="7264e-166">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="7264e-167">在沒有邀請的情況下新增 B2B 共同作業使用者</span><span class="sxs-lookup"><span data-stu-id="7264e-167">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="7264e-168">B2B 共同作業使用者稽核和報告</span><span class="sxs-lookup"><span data-stu-id="7264e-168">B2B collaboration user auditing and reporting</span></span>](active-directory-b2b-auditing-and-reporting.md)
* [<span data-ttu-id="7264e-169">Azure Active Directory 中應用程式管理的文章索引</span><span class="sxs-lookup"><span data-stu-id="7264e-169">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
