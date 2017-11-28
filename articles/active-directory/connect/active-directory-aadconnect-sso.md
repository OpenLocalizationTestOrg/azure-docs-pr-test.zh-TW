---
title: "Azure AD Connect：無縫單一登入 | Microsoft Docs"
description: "本主題說明 Azure Active Directory (Azure AD) 無接縫單一登入，並且如何允許您 tooprovide true 單一登入您公司網路內部的企業桌面使用者。"
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
ms.openlocfilehash: 11c778c37ee39866dcc3a14ab648cfcd8e322e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on"></a><span data-ttu-id="59629-104">Azure Active Directory 無縫單一登入</span><span class="sxs-lookup"><span data-stu-id="59629-104">Azure Active Directory Seamless Single Sign-On</span></span>

## <a name="what-is-azure-active-directory-seamless-single-sign-on"></a><span data-ttu-id="59629-105">何謂 Azure Active Directory 無縫單一登入？</span><span class="sxs-lookup"><span data-stu-id="59629-105">What is Azure Active Directory Seamless Single Sign-On?</span></span>

<span data-ttu-id="59629-106">Azure Active Directory 無接縫單一登入 (Azure AD 無縫式 SSO) 自動簽署時其公司的裝置連線的 tooyour 公司網路上的使用者。</span><span class="sxs-lookup"><span data-stu-id="59629-106">Azure Active Directory Seamless Single Sign-On (Azure AD Seamless SSO) automatically signs users in when they are on their corporate devices connected tooyour corporate network.</span></span> <span data-ttu-id="59629-107">啟用時，使用者就不需要在 tooAzure AD 中, 其密碼 toosign tootype，並通常，即使輸入其使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="59629-107">When enabled, users don't need tootype in their passwords toosign in tooAzure AD, and usually, even type in their usernames.</span></span> <span data-ttu-id="59629-108">這項功能提供您的使用者方便存取 tooyour 雲端型應用程式而不需要任何額外的內部部署元件。</span><span class="sxs-lookup"><span data-stu-id="59629-108">This feature provides your users easy access tooyour cloud-based applications without needing any additional on-premises components.</span></span>

<span data-ttu-id="59629-109">無縫式 SSO 可以結合其中一個 hello[密碼雜湊同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)或[傳遞驗證](active-directory-aadconnect-pass-through-authentication.md)登入方法。</span><span class="sxs-lookup"><span data-stu-id="59629-109">Seamless SSO can be combined with either hello [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) or [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) sign-in methods.</span></span>

![無縫單一登入](./media/active-directory-aadconnect-sso/sso1.png)

>[!IMPORTANT]
><span data-ttu-id="59629-111">無縫 SSO 目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="59629-111">Seamless SSO is currently in preview.</span></span> <span data-ttu-id="59629-112">這項功能_不_適用 tooActive Directory Federation Services (ADFS)。</span><span class="sxs-lookup"><span data-stu-id="59629-112">This feature is _not_ applicable tooActive Directory Federation Services (ADFS).</span></span>

## <a name="key-benefits"></a><span data-ttu-id="59629-113">主要權益</span><span class="sxs-lookup"><span data-stu-id="59629-113">Key benefits</span></span>

- <span data-ttu-id="59629-114">良好的使用者體驗</span><span class="sxs-lookup"><span data-stu-id="59629-114">*Great user experience*</span></span>
  - <span data-ttu-id="59629-115">使用者會自動登入內部部署和雲端式應用程式。</span><span class="sxs-lookup"><span data-stu-id="59629-115">Users are automatically signed into both on-premises and cloud-based applications.</span></span>
  - <span data-ttu-id="59629-116">使用者沒有 tooenter 密碼重複。</span><span class="sxs-lookup"><span data-stu-id="59629-116">Users don't have tooenter their passwords repeatedly.</span></span>
- <span data-ttu-id="59629-117">*輕鬆 toodeploy （& s) 管理*</span><span class="sxs-lookup"><span data-stu-id="59629-117">*Easy toodeploy & administer*</span></span>
  - <span data-ttu-id="59629-118">沒有其他元件所需內部 toomake 這項工作。</span><span class="sxs-lookup"><span data-stu-id="59629-118">No additional components needed on-premises toomake this work.</span></span>
  - <span data-ttu-id="59629-119">與任何雲端驗證方法搭配運作：[密碼雜湊同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)或[傳遞驗證](active-directory-aadconnect-pass-through-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="59629-119">Works with any method of cloud authentication - [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) or [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md).</span></span>
  - <span data-ttu-id="59629-120">可以推出 toosome 或您使用群組原則的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="59629-120">Can be rolled out toosome or all your users using Group Policy.</span></span>
  - <span data-ttu-id="59629-121">非 Windows 10 裝置註冊而 hello 需要在任何 AD FS 基礎結構的 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="59629-121">Register non-Windows 10 devices with Azure AD without hello need for any AD FS infrastructure.</span></span> <span data-ttu-id="59629-122">這項功能需要您 toouse 版本 2.1 或更新版本的 hello[工作地方聯結用戶端](https://www.microsoft.com/download/details.aspx?id=53554)。</span><span class="sxs-lookup"><span data-stu-id="59629-122">This capability needs you toouse version 2.1 or later of hello [workplace-join client](https://www.microsoft.com/download/details.aspx?id=53554).</span></span>

## <a name="feature-highlights"></a><span data-ttu-id="59629-123">功能要點</span><span class="sxs-lookup"><span data-stu-id="59629-123">Feature highlights</span></span>

- <span data-ttu-id="59629-124">登入使用者名稱可以是任一個 hello 內部預設使用者名稱 (`userPrincipalName`) 或在 Azure AD Connect 中設定的另一個屬性 (`Alternate ID`)。</span><span class="sxs-lookup"><span data-stu-id="59629-124">Sign-in username can be either hello on-premises default username (`userPrincipalName`) or another attribute configured in Azure AD Connect (`Alternate ID`).</span></span> <span data-ttu-id="59629-125">同時使用的情況下工作，因為無縫式 SSO 使用 hello `securityIdentifier` hello Kerberos 票證 toolook hello 對應使用者物件在 Azure AD 中的宣告。</span><span class="sxs-lookup"><span data-stu-id="59629-125">Both use cases work because Seamless SSO uses hello `securityIdentifier` claim in hello Kerberos ticket toolook up hello corresponding user object in Azure AD.</span></span>
- <span data-ttu-id="59629-126">無縫 SSO 是一種靈活變換的功能。</span><span class="sxs-lookup"><span data-stu-id="59629-126">Seamless SSO is an opportunistic feature.</span></span> <span data-ttu-id="59629-127">如果因為任何原因失敗，hello 使用者登入經驗會回到 tooits 一般行為-也就是，hello 使用者需要 tooenter hello 登入頁面上的密碼。</span><span class="sxs-lookup"><span data-stu-id="59629-127">If it fails for any reason, hello user sign-in experience goes back tooits regular behavior - i.e, hello user needs tooenter their password on hello sign-in page.</span></span>
- <span data-ttu-id="59629-128">如果應用程式會將轉送`domain_hint`(OpenID Connect) 或`whr`(SAML) 參數-識別您的租用戶或`login_hint`參數-識別 hello 使用者在其 Azure AD 登入要求中，使用者會自動登入未加上輸入使用者名稱或密碼。</span><span class="sxs-lookup"><span data-stu-id="59629-128">If an application forwards a `domain_hint` (OpenID Connect) or `whr` (SAML) parameter - identifying your tenant, or `login_hint` parameter - identifying hello user, in its Azure AD sign-in request, users are automatically signed in without them entering usernames or passwords.</span></span>
- <span data-ttu-id="59629-129">您可以透過 Azure AD Connect 啟用它。</span><span class="sxs-lookup"><span data-stu-id="59629-129">It can be enabled via Azure AD Connect.</span></span>
- <span data-ttu-id="59629-130">這是可用的功能，而且不需要任何付費的版本的 Azure AD toouse 它。</span><span class="sxs-lookup"><span data-stu-id="59629-130">It is a free feature, and you don't need any paid editions of Azure AD toouse it.</span></span>
- <span data-ttu-id="59629-131">它是在能夠使用 Kerberos 驗證的平台和瀏覽器上，支援[新式驗證](https://aka.ms/modernauthga)的網頁瀏覽器型用戶端和 Office 用戶端來支援：</span><span class="sxs-lookup"><span data-stu-id="59629-131">It is supported on web browser-based clients and Office clients that support [modern authentication](https://aka.ms/modernauthga) on platforms and browsers capable of Kerberos authentication:</span></span>

| <span data-ttu-id="59629-132">作業系統\瀏覽器</span><span class="sxs-lookup"><span data-stu-id="59629-132">OS\Browser</span></span> |<span data-ttu-id="59629-133">Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="59629-133">Internet Explorer</span></span>|<span data-ttu-id="59629-134">Edge</span><span class="sxs-lookup"><span data-stu-id="59629-134">Edge</span></span>|<span data-ttu-id="59629-135">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="59629-135">Google Chrome</span></span>|<span data-ttu-id="59629-136">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="59629-136">Mozilla Firefox</span></span>|<span data-ttu-id="59629-137">Safari</span><span class="sxs-lookup"><span data-stu-id="59629-137">Safari</span></span>|
| --- | --- |--- | --- | --- | -- 
|<span data-ttu-id="59629-138">Windows 10</span><span class="sxs-lookup"><span data-stu-id="59629-138">Windows 10</span></span>|<span data-ttu-id="59629-139">是</span><span class="sxs-lookup"><span data-stu-id="59629-139">Yes</span></span>|<span data-ttu-id="59629-140">否</span><span class="sxs-lookup"><span data-stu-id="59629-140">No</span></span>|<span data-ttu-id="59629-141">是</span><span class="sxs-lookup"><span data-stu-id="59629-141">Yes</span></span>|<span data-ttu-id="59629-142">是\*</span><span class="sxs-lookup"><span data-stu-id="59629-142">Yes\*</span></span>|<span data-ttu-id="59629-143">N/A</span><span class="sxs-lookup"><span data-stu-id="59629-143">N/A</span></span>
|<span data-ttu-id="59629-144">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="59629-144">Windows 8.1</span></span>|<span data-ttu-id="59629-145">是</span><span class="sxs-lookup"><span data-stu-id="59629-145">Yes</span></span>|<span data-ttu-id="59629-146">N/A</span><span class="sxs-lookup"><span data-stu-id="59629-146">N/A</span></span>|<span data-ttu-id="59629-147">是</span><span class="sxs-lookup"><span data-stu-id="59629-147">Yes</span></span>|<span data-ttu-id="59629-148">是\*</span><span class="sxs-lookup"><span data-stu-id="59629-148">Yes\*</span></span>|<span data-ttu-id="59629-149">N/A</span><span class="sxs-lookup"><span data-stu-id="59629-149">N/A</span></span>
|<span data-ttu-id="59629-150">Windows 8</span><span class="sxs-lookup"><span data-stu-id="59629-150">Windows 8</span></span>|<span data-ttu-id="59629-151">是</span><span class="sxs-lookup"><span data-stu-id="59629-151">Yes</span></span>|<span data-ttu-id="59629-152">N/A</span><span class="sxs-lookup"><span data-stu-id="59629-152">N/A</span></span>|<span data-ttu-id="59629-153">是</span><span class="sxs-lookup"><span data-stu-id="59629-153">Yes</span></span>|<span data-ttu-id="59629-154">是\*</span><span class="sxs-lookup"><span data-stu-id="59629-154">Yes\*</span></span>|<span data-ttu-id="59629-155">N/A</span><span class="sxs-lookup"><span data-stu-id="59629-155">N/A</span></span>
|<span data-ttu-id="59629-156">Windows 7</span><span class="sxs-lookup"><span data-stu-id="59629-156">Windows 7</span></span>|<span data-ttu-id="59629-157">是</span><span class="sxs-lookup"><span data-stu-id="59629-157">Yes</span></span>|<span data-ttu-id="59629-158">N/A</span><span class="sxs-lookup"><span data-stu-id="59629-158">N/A</span></span>|<span data-ttu-id="59629-159">是</span><span class="sxs-lookup"><span data-stu-id="59629-159">Yes</span></span>|<span data-ttu-id="59629-160">是\*</span><span class="sxs-lookup"><span data-stu-id="59629-160">Yes\*</span></span>|<span data-ttu-id="59629-161">N/A</span><span class="sxs-lookup"><span data-stu-id="59629-161">N/A</span></span>
|<span data-ttu-id="59629-162">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="59629-162">Mac OS X</span></span>|<span data-ttu-id="59629-163">N/A</span><span class="sxs-lookup"><span data-stu-id="59629-163">N/A</span></span>|<span data-ttu-id="59629-164">N/A</span><span class="sxs-lookup"><span data-stu-id="59629-164">N/A</span></span>|<span data-ttu-id="59629-165">是\*</span><span class="sxs-lookup"><span data-stu-id="59629-165">Yes\*</span></span>|<span data-ttu-id="59629-166">是\*</span><span class="sxs-lookup"><span data-stu-id="59629-166">Yes\*</span></span>|<span data-ttu-id="59629-167">是\*</span><span class="sxs-lookup"><span data-stu-id="59629-167">Yes\*</span></span>

<span data-ttu-id="59629-168">\*需要[其他設定](active-directory-aadconnect-sso-quick-start.md#browser-considerations)</span><span class="sxs-lookup"><span data-stu-id="59629-168">\*Requires [additional configuration](active-directory-aadconnect-sso-quick-start.md#browser-considerations)</span></span>

>[!IMPORTANT]
><span data-ttu-id="59629-169">我們最近回復的邊緣 tooinvestigate 支援客戶回報的問題。</span><span class="sxs-lookup"><span data-stu-id="59629-169">We recently rolled back support for Edge tooinvestigate customer-reported issues.</span></span>

>[!NOTE]
><span data-ttu-id="59629-170">Windows 10 hello 建議的做法是 toouse [Azure AD Join](../active-directory-azureadjoin-overview.md) hello 最佳單一登入體驗與 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="59629-170">For Windows 10, hello recommendation is toouse [Azure AD Join](../active-directory-azureadjoin-overview.md) for hello optimal single sign-on experience with Azure AD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59629-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="59629-171">Next steps</span></span>

- <span data-ttu-id="59629-172">[**快速入門**](active-directory-aadconnect-sso-quick-start.md) - 開始使用 Azure AD 無縫 SSO。</span><span class="sxs-lookup"><span data-stu-id="59629-172">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="59629-173">[**技術性深入探討**](active-directory-aadconnect-sso-how-it-works.md) - 了解這項功能的運作方式。</span><span class="sxs-lookup"><span data-stu-id="59629-173">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="59629-174">[**常見問題集**](active-directory-aadconnect-sso-faq.md) -toofrequently 常見問題的答案。</span><span class="sxs-lookup"><span data-stu-id="59629-174">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="59629-175">[**疑難排解**](active-directory-aadconnect-troubleshoot-sso.md) -了解如何 tooresolve 常見問題與 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="59629-175">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="59629-176">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。</span><span class="sxs-lookup"><span data-stu-id="59629-176">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
