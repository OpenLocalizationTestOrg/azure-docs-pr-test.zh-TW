---
title: "Azure AD Connect：傳遞驗證 - 運作方式 | Microsoft Docs"
description: "本文描述 Azure Active Directory 傳遞驗證運作方式。"
services: active-directory
keywords: "Azure AD Connect 傳遞驗證, 安裝 Active Directory, Azure AD 的必要元件, SSO, 單一登入"
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
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a><span data-ttu-id="54631-105">Azure Active Directory 傳遞驗證：技術深入探討</span><span class="sxs-lookup"><span data-stu-id="54631-105">Azure Active Directory Pass-through Authentication: Technical deep dive</span></span>

>[!IMPORTANT]
><span data-ttu-id="54631-106">Azure AD 傳遞驗證目前為預覽功能。</span><span class="sxs-lookup"><span data-stu-id="54631-106">Azure AD Pass-through Authentication is currently in preview.</span></span> 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a><span data-ttu-id="54631-107">Azure Active Directory 傳遞驗證運作方式</span><span class="sxs-lookup"><span data-stu-id="54631-107">How does Azure Active Directory Pass-through Authentication work?</span></span>

<span data-ttu-id="54631-108">在使用者嘗試 toosign 到 Azure Active directory (Azure AD)，保護應用程式，而且如果 hello 租用戶，啟用傳遞驗證 hello 時就會發生下列步驟：</span><span class="sxs-lookup"><span data-stu-id="54631-108">When a user attempts toosign into an application secured by Azure Active Directory (Azure AD), and if Pass-through Authentication is enabled on hello tenant, hello following steps occur:</span></span>

1. <span data-ttu-id="54631-109">hello 的使用者嘗試 tooaccess 應用程式 (例如 hello Outlook Web 應用程式-https://outlook.office365.com/owa/)。</span><span class="sxs-lookup"><span data-stu-id="54631-109">hello user tries tooaccess an application (for example, hello Outlook Web App - https://outlook.office365.com/owa/).</span></span>
2. <span data-ttu-id="54631-110">Hello 使用者沒有已登入，hello 使用者登入頁面重新導向的 toohello Azure AD。</span><span class="sxs-lookup"><span data-stu-id="54631-110">If hello user is not already signed in, hello user is redirected toohello Azure AD sign-in page.</span></span>
3. <span data-ttu-id="54631-111">hello 使用者 hello Azure AD 登入頁面中輸入使用者名稱和密碼，然後按一下 hello 「 登入 」 按鈕。</span><span class="sxs-lookup"><span data-stu-id="54631-111">hello user enters their username and password into hello Azure AD sign-in page and clicks hello "Sign in" button.</span></span>
4. <span data-ttu-id="54631-112">收到 hello 登入要求的 azure AD 會將 hello 使用者名稱和密碼 （加密使用公開金鑰） 放在佇列上。</span><span class="sxs-lookup"><span data-stu-id="54631-112">Azure AD, on receiving hello sign-in request, places hello username and password (encrypted  using a public key) on a queue.</span></span>
5. <span data-ttu-id="54631-113">在內部部署的傳遞驗證代理程式可讓輸出呼叫 toohello 佇列，並擷取 hello 使用者名稱和加密的密碼。</span><span class="sxs-lookup"><span data-stu-id="54631-113">An on-premises Pass-through Authentication agent makes an outbound call toohello queue and retrieves hello username and encrypted password.</span></span>
6. <span data-ttu-id="54631-114">hello 代理程式會使用其私密金鑰的 hello 密碼解密。</span><span class="sxs-lookup"><span data-stu-id="54631-114">hello agent decrypts hello password using its private key.</span></span>
7. <span data-ttu-id="54631-115">hello 代理程式接著會驗證 hello 使用者名稱和密碼，對使用標準 Windows Api （類似的機制 toowhat 由 Active Directory Federation Services） 的 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="54631-115">hello agent then validates hello username and password against Active Directory using standard Windows APIs (a similar mechanism toowhat is used by Active Directory Federation Services).</span></span> <span data-ttu-id="54631-116">hello 使用者名稱可以是任一個 hello 內部預設使用者名稱 (通常`userPrincipalName`) 或在 Azure AD Connect 中設定的另一個屬性 (又稱為`Alternate ID`)。</span><span class="sxs-lookup"><span data-stu-id="54631-116">hello username can be either hello on-premises default username (usually `userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
8. <span data-ttu-id="54631-117">hello 在內部部署 Active Directory 網域控制站 (DC) 然後評估 hello 要求並傳回 hello 適當的回應 (成功、 失敗，密碼過期或鎖定使用者) toohello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="54631-117">hello on-premises Active Directory Domain Controller (DC) then evaluates hello request and returns hello appropriate response (success, failure, password expired or user locked out) toohello agent.</span></span>
9. <span data-ttu-id="54631-118">hello 代理程式，接著，會傳回此回應後 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="54631-118">hello agent, in turn, returns this response back tooAzure AD.</span></span>
10. <span data-ttu-id="54631-119">Azure AD 評估 hello 回應及回應視 toohello 使用者-例如，它立即 hello 使用者登入或要求的多重要素驗證 (MFA)。</span><span class="sxs-lookup"><span data-stu-id="54631-119">Azure AD evaluates hello response and responds toohello user as appropriate - for example, it either signs hello user in immediately or requests for Multi-Factor Authentication (MFA).</span></span>
11. <span data-ttu-id="54631-120">Hello 使用者登入成功時，hello 使用者能 tooaccess hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="54631-120">If hello user sign-in is successful, hello user is able tooaccess hello application.</span></span>

<span data-ttu-id="54631-121">hello 下列圖表說明所有 hello 元件和 hello 所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="54631-121">hello following diagram illustrates all hello components and hello steps involved.</span></span>

![傳遞驗證](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a><span data-ttu-id="54631-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="54631-123">Next steps</span></span>
- <span data-ttu-id="54631-124">[**目前的限制**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - 此功能目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="54631-124">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="54631-125">了解支援的情節和不支援的情節。</span><span class="sxs-lookup"><span data-stu-id="54631-125">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="54631-126">[**快速入門**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - 開始使用 Azure AD 傳遞驗證。</span><span class="sxs-lookup"><span data-stu-id="54631-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="54631-127">[**常見問題集**](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently 常見問題的答案。</span><span class="sxs-lookup"><span data-stu-id="54631-127">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="54631-128">[**疑難排解**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -了解如何 tooresolve 常見問題與 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="54631-128">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="54631-129">[**Azure AD 無縫 SSO**](active-directory-aadconnect-sso.md) - 深入了解此互補功能。</span><span class="sxs-lookup"><span data-stu-id="54631-129">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="54631-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。</span><span class="sxs-lookup"><span data-stu-id="54631-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
