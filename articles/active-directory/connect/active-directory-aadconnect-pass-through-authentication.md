---
title: "Azure AD Connect：傳遞驗證 | Microsoft Docs"
description: "這篇文章說明 Azure Active Directory (Azure AD) 傳遞驗證，以及它如何向內部部署 Active Directory 驗證使用者的密碼以允許 Azure AD 登入。"
services: active-directory
keywords: "什麼是 Azure AD Connect 傳遞驗證、安裝 Active Directory，以及 Azure AD、SSO、單一登入的必要元件"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: 56cfb2c4f4afc7d46c926a392ae6ec01e96224d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="user-sign-in-with-azure-active-directory-pass-through-authentication"></a><span data-ttu-id="4d758-104">使用 Azure Active Directory 傳遞驗證來進行使用者登入</span><span class="sxs-lookup"><span data-stu-id="4d758-104">User sign-in with Azure Active Directory Pass-through Authentication</span></span>

## <a name="what-is-azure-active-directory-pass-through-authentication"></a><span data-ttu-id="4d758-105">什麼是 Azure Active Directory 傳遞驗證？</span><span class="sxs-lookup"><span data-stu-id="4d758-105">What is Azure Active Directory Pass-through Authentication?</span></span>

<span data-ttu-id="4d758-106">Azure Active Directory (Azure AD) 通過驗證可讓使用者 toosign tooboth 內部和雲端型應用程式使用 hello 相同密碼。</span><span class="sxs-lookup"><span data-stu-id="4d758-106">Azure Active Directory (Azure AD) Pass-through Authentication allows your users toosign in tooboth on-premises and cloud-based applications using hello same passwords.</span></span> <span data-ttu-id="4d758-107">這項功能提供您的使用者更好的體驗-一個較少的密碼 tooremember，並減少 IT 技術服務人員成本，因為使用者比較不可能 tooforget 如何 toosign 中的。</span><span class="sxs-lookup"><span data-stu-id="4d758-107">This feature provides your users a better experience - one less password tooremember, and reduces IT helpdesk costs because your users are less likely tooforget how toosign in.</span></span> <span data-ttu-id="4d758-108">當使用者使用 Azure AD 登入時，此功能會向您的內部部署 Active Directory 直接驗證使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="4d758-108">When users sign in using Azure AD, this feature validates users' passwords directly against your on-premises Active Directory.</span></span>

<span data-ttu-id="4d758-109">這項功能是替代太[Azure AD 密碼雜湊同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)，這樣會提供 hello 雲端驗證 tooorganizations 相同的優點。</span><span class="sxs-lookup"><span data-stu-id="4d758-109">This feature is an alternative too[Azure AD Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md), which provides hello same benefit of cloud authentication tooorganizations.</span></span> <span data-ttu-id="4d758-110">不過，某些組織中的安全性與相容性原則不允許這些組織 toosend 使用者的密碼，即使在雜湊的形式中，其內部的界限之外。</span><span class="sxs-lookup"><span data-stu-id="4d758-110">However, security and compliance policies in certain organizations don't permit these organizations toosend users' passwords, even in a hashed form, outside their internal boundaries.</span></span> <span data-ttu-id="4d758-111">Hello 解決方案這類組織通過驗證。</span><span class="sxs-lookup"><span data-stu-id="4d758-111">Pass-through Authentication is hello right solution for such organizations.</span></span>

![Azure AD 傳遞驗證](./media/active-directory-aadconnect-pass-through-authentication/pta1.png)

<span data-ttu-id="4d758-113">您可以結合通過驗證的 hello[無接縫單一登入](active-directory-aadconnect-sso.md)功能。</span><span class="sxs-lookup"><span data-stu-id="4d758-113">You can combine Pass-through Authentication with hello [Seamless Single Sign-On](active-directory-aadconnect-sso.md) feature.</span></span> <span data-ttu-id="4d758-114">如此一來，當您的使用者存取您公司網路內部其公司電腦上的應用程式時，它們不需要在其密碼 toosign 中的 tootype。</span><span class="sxs-lookup"><span data-stu-id="4d758-114">This way, when your users are accessing applications on their corporate machines inside your corporate network, they don't need tootype in their passwords toosign in.</span></span>

>[!IMPORTANT]
><span data-ttu-id="4d758-115">Azure AD 傳遞驗證目前為預覽功能。</span><span class="sxs-lookup"><span data-stu-id="4d758-115">Azure AD Pass-through Authentication is currently in preview.</span></span>

## <a name="key-benefits-of-using-azure-ad-pass-through-authentication"></a><span data-ttu-id="4d758-116">使用 Azure AD 傳遞驗證的主要好處</span><span class="sxs-lookup"><span data-stu-id="4d758-116">Key benefits of using Azure AD Pass-through Authentication</span></span>

- <span data-ttu-id="4d758-117">良好的使用者體驗</span><span class="sxs-lookup"><span data-stu-id="4d758-117">*Great user experience*</span></span>
  - <span data-ttu-id="4d758-118">使用者使用 hello 同時在內部部署和雲端型應用程式的相同密碼 toosign。</span><span class="sxs-lookup"><span data-stu-id="4d758-118">Users use hello same passwords toosign into both on-premises and cloud-based applications.</span></span>
  - <span data-ttu-id="4d758-119">使用者耗費較少的時間與對話 toohello IT 技術服務人員解決密碼相關的問題。</span><span class="sxs-lookup"><span data-stu-id="4d758-119">Users spend less time talking toohello IT helpdesk resolving password-related issues.</span></span>
  - <span data-ttu-id="4d758-120">使用者可以完成[自助密碼管理](../active-directory-passwords-overview.md)hello 雲端中的工作。</span><span class="sxs-lookup"><span data-stu-id="4d758-120">Users can complete [self-service password management](../active-directory-passwords-overview.md) tasks in hello cloud.</span></span>
- <span data-ttu-id="4d758-121">*輕鬆 toodeploy （& s) 管理*</span><span class="sxs-lookup"><span data-stu-id="4d758-121">*Easy toodeploy & administer*</span></span>
  - <span data-ttu-id="4d758-122">不必再進行複雜的內部部署或網路設定。</span><span class="sxs-lookup"><span data-stu-id="4d758-122">No need for complex on-premises deployments or network configuration.</span></span>
  - <span data-ttu-id="4d758-123">需要只輕量型的代理程式 toobe 安裝在內部部署。</span><span class="sxs-lookup"><span data-stu-id="4d758-123">Needs just a lightweight agent toobe installed on-premises.</span></span>
  - <span data-ttu-id="4d758-124">沒有任何額外的管理負荷。</span><span class="sxs-lookup"><span data-stu-id="4d758-124">No management overhead.</span></span> <span data-ttu-id="4d758-125">hello 代理程式會自動收到改進和 bug 修正。</span><span class="sxs-lookup"><span data-stu-id="4d758-125">hello agent automatically receives improvements and bug fixes.</span></span>
- <span data-ttu-id="4d758-126">*安全*</span><span class="sxs-lookup"><span data-stu-id="4d758-126">*Secure*</span></span>
  - <span data-ttu-id="4d758-127">以任何形式的 hello 雲端中永遠不會儲存在內部部署密碼。</span><span class="sxs-lookup"><span data-stu-id="4d758-127">On-premises passwords are never stored in hello cloud in any form.</span></span>
  - <span data-ttu-id="4d758-128">hello 代理程式只會從您的網路內的傳出連接。</span><span class="sxs-lookup"><span data-stu-id="4d758-128">hello agent only makes outbound connections from within your network.</span></span> <span data-ttu-id="4d758-129">因此，在周邊網路中，也稱為 DMZ 沒有需求 tooinstall hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="4d758-129">Therefore, there is no requirement tooinstall hello agent in a perimeter network, also known as a DMZ.</span></span>
  - <span data-ttu-id="4d758-130">與 [Azure AD 條件式存取原則](../active-directory-conditional-access-azure-portal.md) (包括 Multi-Factor Authentication (MFA)) 緊密配合，並[篩除暴力密碼破解攻擊](active-directory-aadconnect-pass-through-authentication-smart-lockout.md)，藉此保護您的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="4d758-130">Protects your user accounts by working seamlessly with [Azure AD Conditional Access policies](../active-directory-conditional-access-azure-portal.md), including Multi-Factor Authentication (MFA), and by [filtering out brute force password attacks](active-directory-aadconnect-pass-through-authentication-smart-lockout.md).</span></span>
- <span data-ttu-id="4d758-131">*高可用性*</span><span class="sxs-lookup"><span data-stu-id="4d758-131">*Highly available*</span></span>
  - <span data-ttu-id="4d758-132">其他代理程式可以安裝在多個內部部署伺服器 tooprovide 高可用性的登入要求。</span><span class="sxs-lookup"><span data-stu-id="4d758-132">Additional agents can be installed on multiple on-premises servers tooprovide high availability of sign-in requests.</span></span>

## <a name="feature-highlights"></a><span data-ttu-id="4d758-133">功能要點</span><span class="sxs-lookup"><span data-stu-id="4d758-133">Feature highlights</span></span>

- <span data-ttu-id="4d758-134">可讓使用者登入到使用[新式驗證](https://aka.ms/modernauthga)的所有 Web 瀏覽器型應用程式和 Microsoft Office 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d758-134">Supports user sign-in into all web browser-based applications and into Microsoft Office client applications that use [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="4d758-135">登入使用者名稱可以是任一個 hello 內部預設使用者名稱 (`userPrincipalName`) 或在 Azure AD Connect 中設定的另一個屬性 (又稱為`Alternate ID`)。</span><span class="sxs-lookup"><span data-stu-id="4d758-135">Sign-in usernames can be either hello on-premises default username (`userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
- <span data-ttu-id="4d758-136">hello 功能可以順暢地與[條件式存取](../active-directory-conditional-access.md)功能，例如 Multi-factor Authentication (MFA) toohelp 保護您的使用者。</span><span class="sxs-lookup"><span data-stu-id="4d758-136">hello feature works seamlessly with [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA) toohelp secure your users.</span></span>
- <span data-ttu-id="4d758-137">如果 AD 樹系之間有樹系信任且名稱尾碼路由已正確設定，就支援多樹系環境。</span><span class="sxs-lookup"><span data-stu-id="4d758-137">Multi-forest environments are supported if there are forest trusts between your AD forests and if name suffix routing is correctly configured.</span></span>
- <span data-ttu-id="4d758-138">這是可用的功能，而且不需要任何付費的版本的 Azure AD toouse 它。</span><span class="sxs-lookup"><span data-stu-id="4d758-138">It is a free feature, and you don't need any paid editions of Azure AD toouse it.</span></span>
- <span data-ttu-id="4d758-139">您可以透過 [Azure AD Connect](active-directory-aadconnect.md) 啟用它。</span><span class="sxs-lookup"><span data-stu-id="4d758-139">It can be enabled via [Azure AD Connect](active-directory-aadconnect.md).</span></span>
- <span data-ttu-id="4d758-140">它會使用輕量型在內部部署代理程式會接聽並回應 toopassword 驗證要求。</span><span class="sxs-lookup"><span data-stu-id="4d758-140">It uses a lightweight on-premises agent that listens for and responds toopassword validation requests.</span></span>
- <span data-ttu-id="4d758-141">安裝多個代理程式就能提供高可用性的登入要求。</span><span class="sxs-lookup"><span data-stu-id="4d758-141">Installing multiple agents provides high availability of sign-in requests.</span></span>
- <span data-ttu-id="4d758-142">它[保護](active-directory-aadconnect-pass-through-authentication-smart-lockout.md)暴力密碼破解針對您在內部部署帳戶強制執行密碼破解攻擊 hello 雲端中的。</span><span class="sxs-lookup"><span data-stu-id="4d758-142">It [protects](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) your on-premises accounts against brute force password attacks in hello cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d758-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4d758-143">Next steps</span></span>

- <span data-ttu-id="4d758-144">[**快速入門**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - 開始使用 Azure AD 傳遞驗證。</span><span class="sxs-lookup"><span data-stu-id="4d758-144">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="4d758-145">[**目前的限制**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - 此功能目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="4d758-145">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="4d758-146">了解支援的情節和不支援的情節。</span><span class="sxs-lookup"><span data-stu-id="4d758-146">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="4d758-147">[**技術性深入探討**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - 了解這項功能的運作方式。</span><span class="sxs-lookup"><span data-stu-id="4d758-147">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="4d758-148">[**常見問題集**](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently 常見問題的答案。</span><span class="sxs-lookup"><span data-stu-id="4d758-148">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="4d758-149">[**疑難排解**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -了解如何 tooresolve 常見問題與 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="4d758-149">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="4d758-150">[**Azure AD 無縫 SSO**](active-directory-aadconnect-sso.md) - 深入了解此互補功能。</span><span class="sxs-lookup"><span data-stu-id="4d758-150">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="4d758-151">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。</span><span class="sxs-lookup"><span data-stu-id="4d758-151">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
