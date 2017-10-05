---
title: "Azure AD Connect：無縫單一登入 - 運作方式 | Microsoft Docs"
description: "本文描述 Azure Active Directory 無縫單一登入功能的運作方式。"
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
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: f0bcbdb03fbb70ff91ac3a56974a88eb1b26c245
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a><span data-ttu-id="0ca38-104">Azure Active Directory 無縫單一登入：技術性深入探討</span><span class="sxs-lookup"><span data-stu-id="0ca38-104">Azure Active Directory Seamless Single Sign-On: Technical deep dive</span></span>

<span data-ttu-id="0ca38-105">本文提供 Azure Active Directory 無縫單一登入 (無縫 SSO) 功能運作方式的技術詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0ca38-105">This article gives you technical details into how the Azure Active Directory Seamless Single Sign-On (Seamless SSO) feature works.</span></span>

>[!IMPORTANT]
><span data-ttu-id="0ca38-106">無縫 SSO 功能目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="0ca38-106">The Seamless SSO feature is currently in preview.</span></span>

## <a name="how-does-seamless-sso-work"></a><span data-ttu-id="0ca38-107">順暢 SSO 如何運作？</span><span class="sxs-lookup"><span data-stu-id="0ca38-107">How does Seamless SSO work?</span></span>

<span data-ttu-id="0ca38-108">本節有兩個部分：</span><span class="sxs-lookup"><span data-stu-id="0ca38-108">This section has two parts to it:</span></span>
1. <span data-ttu-id="0ca38-109">無縫 SSO 功能的設定。</span><span class="sxs-lookup"><span data-stu-id="0ca38-109">The setup of the Seamless SSO feature.</span></span>
2. <span data-ttu-id="0ca38-110">單一使用者登入交易如何與無縫 SSO 搭配運作。</span><span class="sxs-lookup"><span data-stu-id="0ca38-110">How a single user sign-in transaction works with Seamless SSO.</span></span>

### <a name="how-does-set-up-work"></a><span data-ttu-id="0ca38-111">設定如何運作？</span><span class="sxs-lookup"><span data-stu-id="0ca38-111">How does set up work?</span></span>

<span data-ttu-id="0ca38-112">無縫 SSO 是使用 Azure AD Connect 所啟用，如[這裏](active-directory-aadconnect-sso-quick-start.md)所示。</span><span class="sxs-lookup"><span data-stu-id="0ca38-112">Seamless SSO is enabled using Azure AD Connect as shown [here](active-directory-aadconnect-sso-quick-start.md).</span></span> <span data-ttu-id="0ca38-113">啟用此功能時，會執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0ca38-113">While enabling the feature, the following steps occur:</span></span>
- <span data-ttu-id="0ca38-114">名為 `AZUREADSSOACCT` 的電腦帳戶 (代表 Azure AD) 是在您的內部部署 Active Directory (AD) 中建立。</span><span class="sxs-lookup"><span data-stu-id="0ca38-114">A computer account named `AZUREADSSOACCT` (which represents Azure AD) is created in your on-premises Active Directory (AD).</span></span>
- <span data-ttu-id="0ca38-115">電腦帳戶的 Kerberos 解密金鑰可安全地與 Azure AD 共用。</span><span class="sxs-lookup"><span data-stu-id="0ca38-115">The computer account's Kerberos decryption key is shared securely with Azure AD.</span></span>
- <span data-ttu-id="0ca38-116">此外，系統會建立兩個 Kerberos 服務主體名稱 (SPN)，以代表 Azure AD 登入期間所使用的兩個 URL。</span><span class="sxs-lookup"><span data-stu-id="0ca38-116">In addition, two Kerberos service principal names (SPNs) are created to represent two URLs that are used during Azure AD sign-in.</span></span>

>[!NOTE]
> <span data-ttu-id="0ca38-117">在您同步處理至 Azure AD (使用 Azure AD Connect) 的每個 AD 樹系中，以及您想要為其使用者啟用無縫 SSO 者，建立電腦帳戶和 Kerberos SPN。</span><span class="sxs-lookup"><span data-stu-id="0ca38-117">The computer account and the Kerberos SPNs are created in each AD forest you synchronize to Azure AD (using Azure AD Connect) and for whose users you want Seamless SSO.</span></span> <span data-ttu-id="0ca38-118">將 `AZUREADSSOACCT` 電腦帳戶移至儲存其他電腦帳戶的組織單位 (OU)，確保它是透過相同方式進行管理，而且不會予以刪除。</span><span class="sxs-lookup"><span data-stu-id="0ca38-118">Move the `AZUREADSSOACCT` computer account to an Organization Unit (OU) where other computer accounts are stored to ensure that it is managed in the same way and is not deleted.</span></span>

>[!IMPORTANT]
><span data-ttu-id="0ca38-119">強烈建議您至少每隔 30 天變換一次 `AZUREADSSOACCT` 電腦帳戶的 [Kerberos 解密金鑰](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account)。</span><span class="sxs-lookup"><span data-stu-id="0ca38-119">We highly recommend that you [roll over the Kerberos decryption key](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) of the `AZUREADSSOACCT` computer account at least every 30 days.</span></span>

### <a name="how-does-sign-in-with-seamless-sso-work"></a><span data-ttu-id="0ca38-120">使用無縫 SSO 登入的運作方式？</span><span class="sxs-lookup"><span data-stu-id="0ca38-120">How does sign-in with Seamless SSO work?</span></span>

<span data-ttu-id="0ca38-121">設定完成之後，無縫 SSO 登入的運作方式與其他任何使用整合式 Windows 驗證 (IWA) 的登入相同。</span><span class="sxs-lookup"><span data-stu-id="0ca38-121">Once the set-up is complete, Seamless SSO works the same way as any other sign-in that uses Integrated Windows Authentication (IWA).</span></span> <span data-ttu-id="0ca38-122">流程如下︰</span><span class="sxs-lookup"><span data-stu-id="0ca38-122">The flow is as follows:</span></span>

1. <span data-ttu-id="0ca38-123">使用者嘗試從公司網路內加入網域的公司裝置存取應用程式 (例如 Outlook Web App - https://outlook.office365.com/owa/)。</span><span class="sxs-lookup"><span data-stu-id="0ca38-123">The user tries to access an application (for example, the Outlook Web App - https://outlook.office365.com/owa/) from a domain-joined corporate device inside your corporate network.</span></span>
2. <span data-ttu-id="0ca38-124">如果使用者尚未登入，則會將使用者重新導向至 Azure AD 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="0ca38-124">If the user is not already signed in, the user is redirected to the Azure AD sign-in page.</span></span>

  >[!NOTE]
  ><span data-ttu-id="0ca38-125">如果 Azure AD 登入要求包含 `domain_hint` (識別您的租用戶；例如 contoso.onmicrosoft.com) 或 `login_hint` (識別使用者；例如 user@contoso.onmicrosoft.com 或 user@contoso.com) 參數，則會跳過步驟 2。</span><span class="sxs-lookup"><span data-stu-id="0ca38-125">If the Azure AD sign-in request includes a `domain_hint` (identifying your tenant- for example, contoso.onmicrosoft.com) or `login_hint` (identifying the user - for example, user@contoso.onmicrosoft.com or user@contoso.com) parameter, then step 2 is skipped.</span></span>

3. <span data-ttu-id="0ca38-126">使用者將他們的使用者名稱鍵入 Azure AD 登入頁面中。</span><span class="sxs-lookup"><span data-stu-id="0ca38-126">The user types in their user name into the Azure AD sign-in page.</span></span>
4. <span data-ttu-id="0ca38-127">在背景中使用 JavaScript 時，Azure AD 會透過 401 未授權回應來挑戰瀏覽器，以提供 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="0ca38-127">Using JavaScript in the background, Azure AD challenges the browser, via a 401 Unauthorized response, to provide a Kerberos ticket.</span></span>
5. <span data-ttu-id="0ca38-128">瀏覽器接著會從 Active Directory 要求 `AZUREADSSOACCT` 電腦帳戶 (代表 Azure AD) 的票證。</span><span class="sxs-lookup"><span data-stu-id="0ca38-128">The browser, in turn, requests a ticket from Active Directory for the `AZUREADSSOACCT` computer account (which represents Azure AD).</span></span>
6. <span data-ttu-id="0ca38-129">Active Directory 會找出該電腦帳戶，並將 Kerberos 票證傳回給瀏覽器 (使用電腦帳戶的祕密加密)。</span><span class="sxs-lookup"><span data-stu-id="0ca38-129">Active Directory locates the computer account and returns a Kerberos ticket to the browser encrypted with the computer account's secret.</span></span>
7. <span data-ttu-id="0ca38-130">瀏覽器會將它需要的 Kerberos 票證從 Active Directory 轉送到 Azure AD (在其中一個[先前新增至瀏覽器內部網路區域設定的 Azure AD URL](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature) 上)。</span><span class="sxs-lookup"><span data-stu-id="0ca38-130">The browser forwards the Kerberos ticket it acquired from Active Directory to Azure AD (on one of the [Azure AD URLs previously added to the browser's Intranet zone settings](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span></span>
8. <span data-ttu-id="0ca38-131">Azure AD 會解密 Kerberos 票證，其中包含使用先前共用的金鑰登入公司裝置之使用者的身分識別。</span><span class="sxs-lookup"><span data-stu-id="0ca38-131">Azure AD decrypts the Kerberos ticket, which includes the identity of the user signed into the corporate device, using the previously shared key.</span></span>
9. <span data-ttu-id="0ca38-132">評估之後，Azure AD 會將權杖傳回給應用程式，或要求使用者執行其他證明，例如 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="0ca38-132">After evaluation, Azure AD either returns a token back to the application or asks the user to perform additional proofs, such as Multi-Factor Authentication.</span></span>
10. <span data-ttu-id="0ca38-133">如果使用者登入成功，則使用者可以存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ca38-133">If the user sign-in is successful, the user is able to access the application.</span></span>

<span data-ttu-id="0ca38-134">下圖說明所有元件和相關步驟。</span><span class="sxs-lookup"><span data-stu-id="0ca38-134">The following diagram illustrates all the components and the steps involved.</span></span>

![順暢單一登入](./media/active-directory-aadconnect-sso/sso2.png)

<span data-ttu-id="0ca38-136">無縫 SSO 是靈活變換的功能，這表示如果失敗，登入體驗會改回其一般行為； 也就是，使用者必須輸入密碼才能登入。</span><span class="sxs-lookup"><span data-stu-id="0ca38-136">Seamless SSO is opportunistic, which means if it fails, the sign-in experience falls back to its regular behavior - i.e, the user needs to enter their password to sign in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ca38-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0ca38-137">Next steps</span></span>

- <span data-ttu-id="0ca38-138">[**快速入門**](active-directory-aadconnect-sso-quick-start.md) - 開始使用 Azure AD 無縫 SSO。</span><span class="sxs-lookup"><span data-stu-id="0ca38-138">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="0ca38-139">[**常見問題集**](active-directory-aadconnect-sso-faq.md) - 常見問題集的答案。</span><span class="sxs-lookup"><span data-stu-id="0ca38-139">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="0ca38-140">[**疑難排解**](active-directory-aadconnect-troubleshoot-sso.md) - 了解如何解決此功能的常見問題。</span><span class="sxs-lookup"><span data-stu-id="0ca38-140">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="0ca38-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。</span><span class="sxs-lookup"><span data-stu-id="0ca38-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
