---
title: "Azure AD Connect：無縫單一登入 - 運作方式 | Microsoft Docs"
description: "本文說明 hello Azure Active Directory 無接縫單一登入功能的運作方式。"
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
ms.openlocfilehash: 17ce35b32832d241068ab878cf7aac42deab74ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a><span data-ttu-id="fac93-104">Azure Active Directory 無縫單一登入：技術性深入探討</span><span class="sxs-lookup"><span data-stu-id="fac93-104">Azure Active Directory Seamless Single Sign-On: Technical deep dive</span></span>

<span data-ttu-id="fac93-105">這篇文章提供您的技術詳細資料進入 hello Azure Active Directory 無接縫單一登入 (無縫式 SSO) 功能的運作方式。</span><span class="sxs-lookup"><span data-stu-id="fac93-105">This article gives you technical details into how hello Azure Active Directory Seamless Single Sign-On (Seamless SSO) feature works.</span></span>

>[!IMPORTANT]
><span data-ttu-id="fac93-106">hello 無縫式 SSO 的功能目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="fac93-106">hello Seamless SSO feature is currently in preview.</span></span>

## <a name="how-does-seamless-sso-work"></a><span data-ttu-id="fac93-107">順暢 SSO 如何運作？</span><span class="sxs-lookup"><span data-stu-id="fac93-107">How does Seamless SSO work?</span></span>

<span data-ttu-id="fac93-108">本節提供的兩個部分 tooit:</span><span class="sxs-lookup"><span data-stu-id="fac93-108">This section has two parts tooit:</span></span>
1. <span data-ttu-id="fac93-109">hello hello 無縫式 SSO 功能的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="fac93-109">hello setup of hello Seamless SSO feature.</span></span>
2. <span data-ttu-id="fac93-110">單一使用者登入交易如何與無縫 SSO 搭配運作。</span><span class="sxs-lookup"><span data-stu-id="fac93-110">How a single user sign-in transaction works with Seamless SSO.</span></span>

### <a name="how-does-set-up-work"></a><span data-ttu-id="fac93-111">設定如何運作？</span><span class="sxs-lookup"><span data-stu-id="fac93-111">How does set up work?</span></span>

<span data-ttu-id="fac93-112">無縫 SSO 是使用 Azure AD Connect 所啟用，如[這裏](active-directory-aadconnect-sso-quick-start.md)所示。</span><span class="sxs-lookup"><span data-stu-id="fac93-112">Seamless SSO is enabled using Azure AD Connect as shown [here](active-directory-aadconnect-sso-quick-start.md).</span></span> <span data-ttu-id="fac93-113">同時也可讓 hello 功能，就會發生 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fac93-113">While enabling hello feature, hello following steps occur:</span></span>
- <span data-ttu-id="fac93-114">名為 `AZUREADSSOACCT` 的電腦帳戶 (代表 Azure AD) 是在您的內部部署 Active Directory (AD) 中建立。</span><span class="sxs-lookup"><span data-stu-id="fac93-114">A computer account named `AZUREADSSOACCT` (which represents Azure AD) is created in your on-premises Active Directory (AD).</span></span>
- <span data-ttu-id="fac93-115">Azure AD 與安全地共用 hello 電腦帳戶的 Kerberos 解密金鑰。</span><span class="sxs-lookup"><span data-stu-id="fac93-115">hello computer account's Kerberos decryption key is shared securely with Azure AD.</span></span>
- <span data-ttu-id="fac93-116">此外，兩個 Kerberos 服務主要名稱 (Spn) 會建立 toorepresent Azure AD 登入期間所使用的兩個 Url。</span><span class="sxs-lookup"><span data-stu-id="fac93-116">In addition, two Kerberos service principal names (SPNs) are created toorepresent two URLs that are used during Azure AD sign-in.</span></span>

>[!NOTE]
> <span data-ttu-id="fac93-117">在每個 AD 樹系中建立 hello 電腦帳戶和 hello Kerberos Spn tooAzure AD 同步處理 （使用 Azure AD Connect），而且您想在其使用者的無縫式 SSO。</span><span class="sxs-lookup"><span data-stu-id="fac93-117">hello computer account and hello Kerberos SPNs are created in each AD forest you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want Seamless SSO.</span></span> <span data-ttu-id="fac93-118">移動 hello`AZUREADSSOACCT`電腦帳戶 tooan 組織單位 (OU) 中其他電腦帳戶的管理中的預存的 tooensure hello 相同的方式並不會刪除。</span><span class="sxs-lookup"><span data-stu-id="fac93-118">Move hello `AZUREADSSOACCT` computer account tooan Organization Unit (OU) where other computer accounts are stored tooensure that it is managed in hello same way and is not deleted.</span></span>

>[!IMPORTANT]
><span data-ttu-id="fac93-119">我們強烈建議您使用您[變換 hello Kerberos 解密金鑰](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account)的 hello`AZUREADSSOACCT`至少每隔 30 天內的電腦帳戶。</span><span class="sxs-lookup"><span data-stu-id="fac93-119">We highly recommend that you [roll over hello Kerberos decryption key](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) of hello `AZUREADSSOACCT` computer account at least every 30 days.</span></span>

### <a name="how-does-sign-in-with-seamless-sso-work"></a><span data-ttu-id="fac93-120">使用無縫 SSO 登入的運作方式？</span><span class="sxs-lookup"><span data-stu-id="fac93-120">How does sign-in with Seamless SSO work?</span></span>

<span data-ttu-id="fac93-121">Hello 安裝完成之後，無縫式 SSO 的運作方式相同方式與任何其他登入使用整合式 Windows 驗證 (IWA) 的 hello。</span><span class="sxs-lookup"><span data-stu-id="fac93-121">Once hello set-up is complete, Seamless SSO works hello same way as any other sign-in that uses Integrated Windows Authentication (IWA).</span></span> <span data-ttu-id="fac93-122">hello 流程如下所示：</span><span class="sxs-lookup"><span data-stu-id="fac93-122">hello flow is as follows:</span></span>

1. <span data-ttu-id="fac93-123">hello 的使用者嘗試 tooaccess 應用程式 (例如 hello Outlook Web 應用程式-https://outlook.office365.com/owa/) 從公司網路內，已加入網域的公司裝置。</span><span class="sxs-lookup"><span data-stu-id="fac93-123">hello user tries tooaccess an application (for example, hello Outlook Web App - https://outlook.office365.com/owa/) from a domain-joined corporate device inside your corporate network.</span></span>
2. <span data-ttu-id="fac93-124">Hello 使用者沒有已登入，hello 使用者登入頁面重新導向的 toohello Azure AD。</span><span class="sxs-lookup"><span data-stu-id="fac93-124">If hello user is not already signed in, hello user is redirected toohello Azure AD sign-in page.</span></span>

  >[!NOTE]
  ><span data-ttu-id="fac93-125">如果 hello Azure AD 登入要求中包含`domain_hint`識別您租用戶-例如 (contoso.onmicrosoft.com） 或`login_hint`(hello 使用者-例如，用來識別user@contoso.onmicrosoft.com或user@contoso.com) 參數，則步驟 2 則會略過。</span><span class="sxs-lookup"><span data-stu-id="fac93-125">If hello Azure AD sign-in request includes a `domain_hint` (identifying your tenant- for example, contoso.onmicrosoft.com) or `login_hint` (identifying hello user - for example, user@contoso.onmicrosoft.com or user@contoso.com) parameter, then step 2 is skipped.</span></span>

3. <span data-ttu-id="fac93-126">hello hello Azure AD 登入頁面使用者名稱中的使用者類型。</span><span class="sxs-lookup"><span data-stu-id="fac93-126">hello user types in their user name into hello Azure AD sign-in page.</span></span>
4. <span data-ttu-id="fac93-127">Azure AD 挑戰 hello 瀏覽器，透過 401 未授權回應，tooprovide hello 背景中使用 JavaScript，Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="fac93-127">Using JavaScript in hello background, Azure AD challenges hello browser, via a 401 Unauthorized response, tooprovide a Kerberos ticket.</span></span>
5. <span data-ttu-id="fac93-128">hello 瀏覽器中，依次要求票證從 Active Directory hello`AZUREADSSOACCT`電腦帳戶 （這表示 Azure AD）。</span><span class="sxs-lookup"><span data-stu-id="fac93-128">hello browser, in turn, requests a ticket from Active Directory for hello `AZUREADSSOACCT` computer account (which represents Azure AD).</span></span>
6. <span data-ttu-id="fac93-129">Active Directory 找出 hello 電腦帳戶，並傳回 hello 電腦帳戶的密碼以加密的 Kerberos 票證 toohello 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="fac93-129">Active Directory locates hello computer account and returns a Kerberos ticket toohello browser encrypted with hello computer account's secret.</span></span>
7. <span data-ttu-id="fac93-130">hello 瀏覽器會轉送它從 Active Directory tooAzure AD 取得 hello Kerberos 票證 (上一個 hello [Azure AD Url 先前加入 toohello 瀏覽器的內部網路區域設定](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature))。</span><span class="sxs-lookup"><span data-stu-id="fac93-130">hello browser forwards hello Kerberos ticket it acquired from Active Directory tooAzure AD (on one of hello [Azure AD URLs previously added toohello browser's Intranet zone settings](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span></span>
8. <span data-ttu-id="fac93-131">Azure AD 解密 hello Kerberos 票證，其中包括 hello 使用者登入 hello 公司裝置 hello 身分識別，先前使用 hello 共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="fac93-131">Azure AD decrypts hello Kerberos ticket, which includes hello identity of hello user signed into hello corporate device, using hello previously shared key.</span></span>
9. <span data-ttu-id="fac93-132">評估後，Azure AD 傳回的語彙基元後 toohello 應用程式或詢問 hello 使用者 tooperform 其他概念證明，例如 Multi-factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="fac93-132">After evaluation, Azure AD either returns a token back toohello application or asks hello user tooperform additional proofs, such as Multi-Factor Authentication.</span></span>
10. <span data-ttu-id="fac93-133">Hello 使用者登入成功時，hello 使用者能 tooaccess hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fac93-133">If hello user sign-in is successful, hello user is able tooaccess hello application.</span></span>

<span data-ttu-id="fac93-134">hello 下列圖表說明所有 hello 元件和 hello 所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="fac93-134">hello following diagram illustrates all hello components and hello steps involved.</span></span>

![順暢單一登入](./media/active-directory-aadconnect-sso/sso2.png)

<span data-ttu-id="fac93-136">無縫式 SSO 是隨機的這表示如果失敗，hello 登入體驗會回復 tooits 一般行為-也就是，hello 使用者需要 tooenter 中的其密碼 toosign。</span><span class="sxs-lookup"><span data-stu-id="fac93-136">Seamless SSO is opportunistic, which means if it fails, hello sign-in experience falls back tooits regular behavior - i.e, hello user needs tooenter their password toosign in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fac93-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fac93-137">Next steps</span></span>

- <span data-ttu-id="fac93-138">[**快速入門**](active-directory-aadconnect-sso-quick-start.md) - 開始使用 Azure AD 無縫 SSO。</span><span class="sxs-lookup"><span data-stu-id="fac93-138">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="fac93-139">[**常見問題集**](active-directory-aadconnect-sso-faq.md) -toofrequently 常見問題的答案。</span><span class="sxs-lookup"><span data-stu-id="fac93-139">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="fac93-140">[**疑難排解**](active-directory-aadconnect-troubleshoot-sso.md) -了解如何 tooresolve 常見問題與 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="fac93-140">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="fac93-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。</span><span class="sxs-lookup"><span data-stu-id="fac93-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
