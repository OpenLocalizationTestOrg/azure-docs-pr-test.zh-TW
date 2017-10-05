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
ms.openlocfilehash: 6acbc347d7b187a6aac603dd05cf95c6aba54475
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="user-sign-in-with-azure-active-directory-pass-through-authentication"></a><span data-ttu-id="1af84-104">使用 Azure Active Directory 傳遞驗證來進行使用者登入</span><span class="sxs-lookup"><span data-stu-id="1af84-104">User sign-in with Azure Active Directory Pass-through Authentication</span></span>

## <a name="what-is-azure-active-directory-pass-through-authentication"></a><span data-ttu-id="1af84-105">什麼是 Azure Active Directory 傳遞驗證？</span><span class="sxs-lookup"><span data-stu-id="1af84-105">What is Azure Active Directory Pass-through Authentication?</span></span>

<span data-ttu-id="1af84-106">Azure Active Directory (Azure AD) 傳遞驗證可讓您的使用者以相同密碼登入內部部署和雲端式應用程式。</span><span class="sxs-lookup"><span data-stu-id="1af84-106">Azure Active Directory (Azure AD) Pass-through Authentication allows your users to sign in to both on-premises and cloud-based applications using the same passwords.</span></span> <span data-ttu-id="1af84-107">這項功能可讓您的使用者獲得更好的體驗，不僅少了一個要記住的密碼，還會因為使用者不太可能忘了如何登入而降低 IT 技術服務人員成本。</span><span class="sxs-lookup"><span data-stu-id="1af84-107">This feature provides your users a better experience - one less password to remember, and reduces IT helpdesk costs because your users are less likely to forget how to sign in.</span></span> <span data-ttu-id="1af84-108">當使用者使用 Azure AD 登入時，此功能會向您的內部部署 Active Directory 直接驗證使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="1af84-108">When users sign in using Azure AD, this feature validates users' passwords directly against your on-premises Active Directory.</span></span>

<span data-ttu-id="1af84-109">這是 [Azure AD 密碼雜湊同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)的替代功能，可為組織提供相同的雲端驗證好處。</span><span class="sxs-lookup"><span data-stu-id="1af84-109">This feature is an alternative to [Azure AD Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md), which provides the same benefit of cloud authentication to organizations.</span></span> <span data-ttu-id="1af84-110">不過，某些組織的安全性與合規性原則不會允許這些組織將使用者的密碼傳送到其內部界限之外，即使密碼採用雜湊格式也是如此。</span><span class="sxs-lookup"><span data-stu-id="1af84-110">However, security and compliance policies in certain organizations don't permit these organizations to send users' passwords, even in a hashed form, outside their internal boundaries.</span></span> <span data-ttu-id="1af84-111">傳遞驗證便是最適合這類組織的解決方案。</span><span class="sxs-lookup"><span data-stu-id="1af84-111">Pass-through Authentication is the right solution for such organizations.</span></span>

![Azure AD 傳遞驗證](./media/active-directory-aadconnect-pass-through-authentication/pta1.png)

<span data-ttu-id="1af84-113">您可以將傳遞驗證與[無縫單一登入](active-directory-aadconnect-sso.md)功能結合在一起。</span><span class="sxs-lookup"><span data-stu-id="1af84-113">You can combine Pass-through Authentication with the [Seamless Single Sign-On](active-directory-aadconnect-sso.md) feature.</span></span> <span data-ttu-id="1af84-114">如此一來，當使用者在公司網路內的公司電腦上存取應用程式時，就不需要輸入密碼來進行登入。</span><span class="sxs-lookup"><span data-stu-id="1af84-114">This way, when your users are accessing applications on their corporate machines inside your corporate network, they don't need to type in their passwords to sign in.</span></span>

>[!IMPORTANT]
><span data-ttu-id="1af84-115">Azure AD 傳遞驗證目前為預覽功能。</span><span class="sxs-lookup"><span data-stu-id="1af84-115">Azure AD Pass-through Authentication is currently in preview.</span></span>

## <a name="key-benefits-of-using-azure-ad-pass-through-authentication"></a><span data-ttu-id="1af84-116">使用 Azure AD 傳遞驗證的主要好處</span><span class="sxs-lookup"><span data-stu-id="1af84-116">Key benefits of using Azure AD Pass-through Authentication</span></span>

- <span data-ttu-id="1af84-117">良好的使用者體驗</span><span class="sxs-lookup"><span data-stu-id="1af84-117">*Great user experience*</span></span>
  - <span data-ttu-id="1af84-118">使用者使用相同的密碼來登入內部部署和雲端型的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1af84-118">Users use the same passwords to sign into both on-premises and cloud-based applications.</span></span>
  - <span data-ttu-id="1af84-119">使用者可以減少尋求 IT 技術服務人員解決密碼相關問題所耗費的對話時間。</span><span class="sxs-lookup"><span data-stu-id="1af84-119">Users spend less time talking to the IT helpdesk resolving password-related issues.</span></span>
  - <span data-ttu-id="1af84-120">使用者可以在雲端中完成[自助式密碼管理](../active-directory-passwords-overview.md)工作。</span><span class="sxs-lookup"><span data-stu-id="1af84-120">Users can complete [self-service password management](../active-directory-passwords-overview.md) tasks in the cloud.</span></span>
- <span data-ttu-id="1af84-121">容易部署和管理</span><span class="sxs-lookup"><span data-stu-id="1af84-121">*Easy to deploy & administer*</span></span>
  - <span data-ttu-id="1af84-122">不必再進行複雜的內部部署或網路設定。</span><span class="sxs-lookup"><span data-stu-id="1af84-122">No need for complex on-premises deployments or network configuration.</span></span>
  - <span data-ttu-id="1af84-123">只需要在內部部署環境安裝輕量型代理程式。</span><span class="sxs-lookup"><span data-stu-id="1af84-123">Needs just a lightweight agent to be installed on-premises.</span></span>
  - <span data-ttu-id="1af84-124">沒有任何額外的管理負荷。</span><span class="sxs-lookup"><span data-stu-id="1af84-124">No management overhead.</span></span> <span data-ttu-id="1af84-125">代理程式會自動收到改進和錯誤的修正。</span><span class="sxs-lookup"><span data-stu-id="1af84-125">The agent automatically receives improvements and bug fixes.</span></span>
- <span data-ttu-id="1af84-126">*安全*</span><span class="sxs-lookup"><span data-stu-id="1af84-126">*Secure*</span></span>
  - <span data-ttu-id="1af84-127">內部部署密碼絕對不會以任何形式儲存在雲端。</span><span class="sxs-lookup"><span data-stu-id="1af84-127">On-premises passwords are never stored in the cloud in any form.</span></span>
  - <span data-ttu-id="1af84-128">代理程式只會從您的網路內進行輸出連線。</span><span class="sxs-lookup"><span data-stu-id="1af84-128">The agent only makes outbound connections from within your network.</span></span> <span data-ttu-id="1af84-129">因此，不需要將代理程式安裝在周邊網路 (又稱做 DMZ) 中。</span><span class="sxs-lookup"><span data-stu-id="1af84-129">Therefore, there is no requirement to install the agent in a perimeter network, also known as a DMZ.</span></span>
  - <span data-ttu-id="1af84-130">與 [Azure AD 條件式存取原則](../active-directory-conditional-access-azure-portal.md) (包括 Multi-Factor Authentication (MFA)) 緊密配合，並[篩除暴力密碼破解攻擊](active-directory-aadconnect-pass-through-authentication-smart-lockout.md)，藉此保護您的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="1af84-130">Protects your user accounts by working seamlessly with [Azure AD Conditional Access policies](../active-directory-conditional-access-azure-portal.md), including Multi-Factor Authentication (MFA), and by [filtering out brute force password attacks](active-directory-aadconnect-pass-through-authentication-smart-lockout.md).</span></span>
- <span data-ttu-id="1af84-131">*高可用性*</span><span class="sxs-lookup"><span data-stu-id="1af84-131">*Highly available*</span></span>
  - <span data-ttu-id="1af84-132">可以在多部內部部署伺服器上安裝其他代理程式，以提供高可用性的登入要求。</span><span class="sxs-lookup"><span data-stu-id="1af84-132">Additional agents can be installed on multiple on-premises servers to provide high availability of sign-in requests.</span></span>

## <a name="feature-highlights"></a><span data-ttu-id="1af84-133">功能要點</span><span class="sxs-lookup"><span data-stu-id="1af84-133">Feature highlights</span></span>

- <span data-ttu-id="1af84-134">可讓使用者登入到使用[新式驗證](https://aka.ms/modernauthga)的所有 Web 瀏覽器型應用程式和 Microsoft Office 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="1af84-134">Supports user sign-in into all web browser-based applications and into Microsoft Office client applications that use [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="1af84-135">登入使用者名稱可以是內部部署的預設使用者名稱 (`userPrincipalName`)，或在 Azure AD Connect 中設定的另一個屬性 (又稱為 `Alternate ID`)。</span><span class="sxs-lookup"><span data-stu-id="1af84-135">Sign-in usernames can be either the on-premises default username (`userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
- <span data-ttu-id="1af84-136">此功能可與[條件式存取](../active-directory-conditional-access.md)功能 (例如，Multi-Factor Authentication (MFA)) 緊密配合，以協助保護您的使用者。</span><span class="sxs-lookup"><span data-stu-id="1af84-136">The feature works seamlessly with [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA) to help secure your users.</span></span>
- <span data-ttu-id="1af84-137">如果 AD 樹系之間有樹系信任且名稱尾碼路由已正確設定，就支援多樹系環境。</span><span class="sxs-lookup"><span data-stu-id="1af84-137">Multi-forest environments are supported if there are forest trusts between your AD forests and if name suffix routing is correctly configured.</span></span>
- <span data-ttu-id="1af84-138">這是免費功能，您不需要任何付費的 Azure AD 版本即可使用。</span><span class="sxs-lookup"><span data-stu-id="1af84-138">It is a free feature, and you don't need any paid editions of Azure AD to use it.</span></span>
- <span data-ttu-id="1af84-139">您可以透過 [Azure AD Connect](active-directory-aadconnect.md) 啟用它。</span><span class="sxs-lookup"><span data-stu-id="1af84-139">It can be enabled via [Azure AD Connect](active-directory-aadconnect.md).</span></span>
- <span data-ttu-id="1af84-140">它會使用輕量型內部部署代理程式來接聽並回應密碼驗證要求。</span><span class="sxs-lookup"><span data-stu-id="1af84-140">It uses a lightweight on-premises agent that listens for and responds to password validation requests.</span></span>
- <span data-ttu-id="1af84-141">安裝多個代理程式就能提供高可用性的登入要求。</span><span class="sxs-lookup"><span data-stu-id="1af84-141">Installing multiple agents provides high availability of sign-in requests.</span></span>
- <span data-ttu-id="1af84-142">它能[保護](active-directory-aadconnect-pass-through-authentication-smart-lockout.md)您的內部部署帳戶，不讓其遭到雲端暴力密碼破解攻擊的威脅。</span><span class="sxs-lookup"><span data-stu-id="1af84-142">It [protects](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) your on-premises accounts against brute force password attacks in the cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1af84-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1af84-143">Next steps</span></span>

- <span data-ttu-id="1af84-144">[**快速入門**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - 開始使用 Azure AD 傳遞驗證。</span><span class="sxs-lookup"><span data-stu-id="1af84-144">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="1af84-145">[**目前的限制**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - 此功能目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="1af84-145">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="1af84-146">了解支援的情節和不支援的情節。</span><span class="sxs-lookup"><span data-stu-id="1af84-146">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="1af84-147">[**技術性深入探討**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - 了解這項功能的運作方式。</span><span class="sxs-lookup"><span data-stu-id="1af84-147">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="1af84-148">[**常見問題集**](active-directory-aadconnect-pass-through-authentication-faq.md) - 常見問題集的答案。</span><span class="sxs-lookup"><span data-stu-id="1af84-148">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="1af84-149">[**疑難排解**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - 了解如何解決此功能的常見問題。</span><span class="sxs-lookup"><span data-stu-id="1af84-149">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="1af84-150">[**Azure AD 無縫 SSO**](active-directory-aadconnect-sso.md) - 深入了解此互補功能。</span><span class="sxs-lookup"><span data-stu-id="1af84-150">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="1af84-151">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。</span><span class="sxs-lookup"><span data-stu-id="1af84-151">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
