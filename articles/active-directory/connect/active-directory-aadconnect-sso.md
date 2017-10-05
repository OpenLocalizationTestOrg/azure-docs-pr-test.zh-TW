---
title: "Azure AD Connect：無縫單一登入 | Microsoft Docs"
description: "本主題描述 Azure Active Directory (Azure AD) 的無縫單一登入，以及它如何讓您為公司網路內部的公司桌面使用者，提供真正的單一登入。"
services: active-directory
keywords: "何謂 Azure AD Connect、安裝 Active Directory、Azure AD、SSO、單一登入的必要元件"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 5a390208f4b7c22e96d7888bcbbd14d8b27667eb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-seamless-single-sign-on"></a><span data-ttu-id="ead44-104">Azure Active Directory 無縫單一登入</span><span class="sxs-lookup"><span data-stu-id="ead44-104">Azure Active Directory Seamless Single Sign-On</span></span>

## <a name="what-is-azure-active-directory-seamless-single-sign-on"></a><span data-ttu-id="ead44-105">何謂 Azure Active Directory 無縫單一登入？</span><span class="sxs-lookup"><span data-stu-id="ead44-105">What is Azure Active Directory Seamless Single Sign-On?</span></span>

<span data-ttu-id="ead44-106">使用者位於連線到公司網路的公司裝置時，Azure Active Directory 無縫單一登入 (Azure AD 無縫 SSO) 就會自動將他們登入。</span><span class="sxs-lookup"><span data-stu-id="ead44-106">Azure Active Directory Seamless Single Sign-On (Azure AD Seamless SSO) automatically signs users in when they are on their corporate devices connected to your corporate network.</span></span> <span data-ttu-id="ead44-107">當此功能啟用時，使用者不需要輸入密碼就能登入 Azure AD，而且在大部分情況下，甚至也不用輸入其使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="ead44-107">When enabled, users don't need to type in their passwords to sign in to Azure AD, and usually, even type in their usernames.</span></span> <span data-ttu-id="ead44-108">這項功能可讓使用者輕鬆存取雲端式應用程式，而不需要任何額外的內部部署元件。</span><span class="sxs-lookup"><span data-stu-id="ead44-108">This feature provides your users easy access to your cloud-based applications without needing any additional on-premises components.</span></span>

<span data-ttu-id="ead44-109">無縫 SSO 可以與[密碼雜湊同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)或[傳遞驗證](active-directory-aadconnect-pass-through-authentication.md)登入方法合併使用。</span><span class="sxs-lookup"><span data-stu-id="ead44-109">Seamless SSO can be combined with either the [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) or [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) sign-in methods.</span></span>

![無縫單一登入](./media/active-directory-aadconnect-sso/sso1.png)

>[!IMPORTANT]
><span data-ttu-id="ead44-111">無縫 SSO 目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="ead44-111">Seamless SSO is currently in preview.</span></span> <span data-ttu-id="ead44-112">此功能_不_適用於 Active Directory 同盟服務 (ADFS)。</span><span class="sxs-lookup"><span data-stu-id="ead44-112">This feature is _not_ applicable to Active Directory Federation Services (ADFS).</span></span>

## <a name="key-benefits"></a><span data-ttu-id="ead44-113">主要權益</span><span class="sxs-lookup"><span data-stu-id="ead44-113">Key benefits</span></span>

- <span data-ttu-id="ead44-114">良好的使用者體驗</span><span class="sxs-lookup"><span data-stu-id="ead44-114">*Great user experience*</span></span>
  - <span data-ttu-id="ead44-115">使用者會自動登入內部部署和雲端式應用程式。</span><span class="sxs-lookup"><span data-stu-id="ead44-115">Users are automatically signed into both on-premises and cloud-based applications.</span></span>
  - <span data-ttu-id="ead44-116">使用者不需要重複輸入其密碼。</span><span class="sxs-lookup"><span data-stu-id="ead44-116">Users don't have to enter their passwords repeatedly.</span></span>
- <span data-ttu-id="ead44-117">容易部署和管理</span><span class="sxs-lookup"><span data-stu-id="ead44-117">*Easy to deploy & administer*</span></span>
  - <span data-ttu-id="ead44-118">在內部部署上不需要任何其他元件，即可進行這項工作。</span><span class="sxs-lookup"><span data-stu-id="ead44-118">No additional components needed on-premises to make this work.</span></span>
  - <span data-ttu-id="ead44-119">與任何雲端驗證方法搭配運作：[密碼雜湊同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)或[傳遞驗證](active-directory-aadconnect-pass-through-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="ead44-119">Works with any method of cloud authentication - [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) or [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md).</span></span>
  - <span data-ttu-id="ead44-120">可以推出給使用群組原則的一部分使用者或所有使用者。</span><span class="sxs-lookup"><span data-stu-id="ead44-120">Can be rolled out to some or all your users using Group Policy.</span></span>
  - <span data-ttu-id="ead44-121">可透過 Azure AD 註冊非 Windows 10 裝置，無需任何的 AD FS 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="ead44-121">Register non-Windows 10 devices with Azure AD without the need for any AD FS infrastructure.</span></span> <span data-ttu-id="ead44-122">此功能需要使用 2.1 版或更新版本的[加入工作場所用戶端](https://www.microsoft.com/download/details.aspx?id=53554)。</span><span class="sxs-lookup"><span data-stu-id="ead44-122">This capability needs you to use version 2.1 or later of the [workplace-join client](https://www.microsoft.com/download/details.aspx?id=53554).</span></span>

## <a name="feature-highlights"></a><span data-ttu-id="ead44-123">功能要點</span><span class="sxs-lookup"><span data-stu-id="ead44-123">Feature highlights</span></span>

- <span data-ttu-id="ead44-124">登入使用者名稱可以是內部部署的預設使用者名稱 (`userPrincipalName`)，或在 Azure AD Connect 中設定的另一個屬性 (`Alternate ID`)。</span><span class="sxs-lookup"><span data-stu-id="ead44-124">Sign-in username can be either the on-premises default username (`userPrincipalName`) or another attribute configured in Azure AD Connect (`Alternate ID`).</span></span> <span data-ttu-id="ead44-125">兩種使用案例均可行，因為無縫 SSO 在 Kerberos 票證中使用 `securityIdentifier` 宣告在 Azure AD 中查詢對應的使用者物件。</span><span class="sxs-lookup"><span data-stu-id="ead44-125">Both use cases work because Seamless SSO uses the `securityIdentifier` claim in the Kerberos ticket to look up the corresponding user object in Azure AD.</span></span>
- <span data-ttu-id="ead44-126">無縫 SSO 是一種靈活變換的功能。</span><span class="sxs-lookup"><span data-stu-id="ead44-126">Seamless SSO is an opportunistic feature.</span></span> <span data-ttu-id="ead44-127">如果因任何原因而失敗，使用者登入體驗會改回其一般行為；亦即，使用者必須在登入頁面上輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="ead44-127">If it fails for any reason, the user sign-in experience goes back to its regular behavior - i.e, the user needs to enter their password on the sign-in page.</span></span>
- <span data-ttu-id="ead44-128">如果應用程式在其 Azure AD 登入要求中轉送 `domain_hint` (OpenID Connect) 或 `whr` (SAML) 參數來識別您的租用戶，或是轉送 `login_hint` 參數來識別使用者，則會自動將使用者登入，而不需要輸入使用者名稱或密碼。</span><span class="sxs-lookup"><span data-stu-id="ead44-128">If an application forwards a `domain_hint` (OpenID Connect) or `whr` (SAML) parameter - identifying your tenant, or `login_hint` parameter - identifying the user, in its Azure AD sign-in request, users are automatically signed in without them entering usernames or passwords.</span></span>
- <span data-ttu-id="ead44-129">您可以透過 Azure AD Connect 啟用它。</span><span class="sxs-lookup"><span data-stu-id="ead44-129">It can be enabled via Azure AD Connect.</span></span>
- <span data-ttu-id="ead44-130">這是免費功能，您不需要任何付費的 Azure AD 版本即可使用。</span><span class="sxs-lookup"><span data-stu-id="ead44-130">It is a free feature, and you don't need any paid editions of Azure AD to use it.</span></span>
- <span data-ttu-id="ead44-131">它是在能夠使用 Kerberos 驗證的平台和瀏覽器上，支援[新式驗證](https://aka.ms/modernauthga)的網頁瀏覽器型用戶端和 Office 用戶端來支援：</span><span class="sxs-lookup"><span data-stu-id="ead44-131">It is supported on web browser-based clients and Office clients that support [modern authentication](https://aka.ms/modernauthga) on platforms and browsers capable of Kerberos authentication:</span></span>

| <span data-ttu-id="ead44-132">作業系統\瀏覽器</span><span class="sxs-lookup"><span data-stu-id="ead44-132">OS\Browser</span></span> |<span data-ttu-id="ead44-133">Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="ead44-133">Internet Explorer</span></span>|<span data-ttu-id="ead44-134">Edge</span><span class="sxs-lookup"><span data-stu-id="ead44-134">Edge</span></span>|<span data-ttu-id="ead44-135">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="ead44-135">Google Chrome</span></span>|<span data-ttu-id="ead44-136">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="ead44-136">Mozilla Firefox</span></span>|<span data-ttu-id="ead44-137">Safari</span><span class="sxs-lookup"><span data-stu-id="ead44-137">Safari</span></span>|
| --- | --- |--- | --- | --- | -- 
|<span data-ttu-id="ead44-138">Windows 10</span><span class="sxs-lookup"><span data-stu-id="ead44-138">Windows 10</span></span>|<span data-ttu-id="ead44-139">是</span><span class="sxs-lookup"><span data-stu-id="ead44-139">Yes</span></span>|<span data-ttu-id="ead44-140">否</span><span class="sxs-lookup"><span data-stu-id="ead44-140">No</span></span>|<span data-ttu-id="ead44-141">是</span><span class="sxs-lookup"><span data-stu-id="ead44-141">Yes</span></span>|<span data-ttu-id="ead44-142">是\*</span><span class="sxs-lookup"><span data-stu-id="ead44-142">Yes\*</span></span>|<span data-ttu-id="ead44-143">N/A</span><span class="sxs-lookup"><span data-stu-id="ead44-143">N/A</span></span>
|<span data-ttu-id="ead44-144">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="ead44-144">Windows 8.1</span></span>|<span data-ttu-id="ead44-145">是</span><span class="sxs-lookup"><span data-stu-id="ead44-145">Yes</span></span>|<span data-ttu-id="ead44-146">N/A</span><span class="sxs-lookup"><span data-stu-id="ead44-146">N/A</span></span>|<span data-ttu-id="ead44-147">是</span><span class="sxs-lookup"><span data-stu-id="ead44-147">Yes</span></span>|<span data-ttu-id="ead44-148">是\*</span><span class="sxs-lookup"><span data-stu-id="ead44-148">Yes\*</span></span>|<span data-ttu-id="ead44-149">N/A</span><span class="sxs-lookup"><span data-stu-id="ead44-149">N/A</span></span>
|<span data-ttu-id="ead44-150">Windows 8</span><span class="sxs-lookup"><span data-stu-id="ead44-150">Windows 8</span></span>|<span data-ttu-id="ead44-151">是</span><span class="sxs-lookup"><span data-stu-id="ead44-151">Yes</span></span>|<span data-ttu-id="ead44-152">N/A</span><span class="sxs-lookup"><span data-stu-id="ead44-152">N/A</span></span>|<span data-ttu-id="ead44-153">是</span><span class="sxs-lookup"><span data-stu-id="ead44-153">Yes</span></span>|<span data-ttu-id="ead44-154">是\*</span><span class="sxs-lookup"><span data-stu-id="ead44-154">Yes\*</span></span>|<span data-ttu-id="ead44-155">N/A</span><span class="sxs-lookup"><span data-stu-id="ead44-155">N/A</span></span>
|<span data-ttu-id="ead44-156">Windows 7</span><span class="sxs-lookup"><span data-stu-id="ead44-156">Windows 7</span></span>|<span data-ttu-id="ead44-157">是</span><span class="sxs-lookup"><span data-stu-id="ead44-157">Yes</span></span>|<span data-ttu-id="ead44-158">N/A</span><span class="sxs-lookup"><span data-stu-id="ead44-158">N/A</span></span>|<span data-ttu-id="ead44-159">是</span><span class="sxs-lookup"><span data-stu-id="ead44-159">Yes</span></span>|<span data-ttu-id="ead44-160">是\*</span><span class="sxs-lookup"><span data-stu-id="ead44-160">Yes\*</span></span>|<span data-ttu-id="ead44-161">N/A</span><span class="sxs-lookup"><span data-stu-id="ead44-161">N/A</span></span>
|<span data-ttu-id="ead44-162">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="ead44-162">Mac OS X</span></span>|<span data-ttu-id="ead44-163">N/A</span><span class="sxs-lookup"><span data-stu-id="ead44-163">N/A</span></span>|<span data-ttu-id="ead44-164">N/A</span><span class="sxs-lookup"><span data-stu-id="ead44-164">N/A</span></span>|<span data-ttu-id="ead44-165">是\*</span><span class="sxs-lookup"><span data-stu-id="ead44-165">Yes\*</span></span>|<span data-ttu-id="ead44-166">是\*</span><span class="sxs-lookup"><span data-stu-id="ead44-166">Yes\*</span></span>|<span data-ttu-id="ead44-167">是\*</span><span class="sxs-lookup"><span data-stu-id="ead44-167">Yes\*</span></span>

<span data-ttu-id="ead44-168">\*需要[其他設定](active-directory-aadconnect-sso-quick-start.md#browser-considerations)</span><span class="sxs-lookup"><span data-stu-id="ead44-168">\*Requires [additional configuration](active-directory-aadconnect-sso-quick-start.md#browser-considerations)</span></span>

>[!IMPORTANT]
><span data-ttu-id="ead44-169">我們最近已復原對 Edge 的支援，以調查客戶回報的問題。</span><span class="sxs-lookup"><span data-stu-id="ead44-169">We recently rolled back support for Edge to investigate customer-reported issues.</span></span>

>[!NOTE]
><span data-ttu-id="ead44-170">對於 Windows 10，建議使用 [Azure AD Join](../active-directory-azureadjoin-overview.md) 以獲得 Azure AD 最佳單一登入體驗。</span><span class="sxs-lookup"><span data-stu-id="ead44-170">For Windows 10, the recommendation is to use [Azure AD Join](../active-directory-azureadjoin-overview.md) for the optimal single sign-on experience with Azure AD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ead44-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ead44-171">Next steps</span></span>

- <span data-ttu-id="ead44-172">[**快速入門**](active-directory-aadconnect-sso-quick-start.md) - 開始使用 Azure AD 無縫 SSO。</span><span class="sxs-lookup"><span data-stu-id="ead44-172">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="ead44-173">[**技術性深入探討**](active-directory-aadconnect-sso-how-it-works.md) - 了解這項功能的運作方式。</span><span class="sxs-lookup"><span data-stu-id="ead44-173">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="ead44-174">[**常見問題集**](active-directory-aadconnect-sso-faq.md) - 常見問題集的答案。</span><span class="sxs-lookup"><span data-stu-id="ead44-174">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="ead44-175">[**疑難排解**](active-directory-aadconnect-troubleshoot-sso.md) - 了解如何解決此功能的常見問題。</span><span class="sxs-lookup"><span data-stu-id="ead44-175">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="ead44-176">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。</span><span class="sxs-lookup"><span data-stu-id="ead44-176">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
