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
ms.openlocfilehash: d34ccd40082edbe036d963ad548bff648119bdd4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a><span data-ttu-id="e2f56-105">Azure Active Directory 傳遞驗證：技術深入探討</span><span class="sxs-lookup"><span data-stu-id="e2f56-105">Azure Active Directory Pass-through Authentication: Technical deep dive</span></span>

>[!IMPORTANT]
><span data-ttu-id="e2f56-106">Azure AD 傳遞驗證目前為預覽功能。</span><span class="sxs-lookup"><span data-stu-id="e2f56-106">Azure AD Pass-through Authentication is currently in preview.</span></span> 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a><span data-ttu-id="e2f56-107">Azure Active Directory 傳遞驗證運作方式</span><span class="sxs-lookup"><span data-stu-id="e2f56-107">How does Azure Active Directory Pass-through Authentication work?</span></span>

<span data-ttu-id="e2f56-108">如果使用者嘗試登入 Azure Active Directory (Azure AD) 所保護的應用程式，並且在租用戶上啟用傳遞驗證，則會執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e2f56-108">When a user attempts to sign into an application secured by Azure Active Directory (Azure AD), and if Pass-through Authentication is enabled on the tenant, the following steps occur:</span></span>

1. <span data-ttu-id="e2f56-109">使用者嘗試存取應用程式 (例如，Outlook Web App - https://outlook.office365.com/owa/)。</span><span class="sxs-lookup"><span data-stu-id="e2f56-109">The user tries to access an application (for example, the Outlook Web App - https://outlook.office365.com/owa/).</span></span>
2. <span data-ttu-id="e2f56-110">如果使用者尚未登入，則會將使用者重新導向至 Azure AD 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="e2f56-110">If the user is not already signed in, the user is redirected to the Azure AD sign-in page.</span></span>
3. <span data-ttu-id="e2f56-111">使用者將其使用者名稱和密碼輸入 Azure AD 登入頁面，然後按一下 [登入] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e2f56-111">The user enters their username and password into the Azure AD sign-in page and clicks the "Sign in" button.</span></span>
4. <span data-ttu-id="e2f56-112">接收登入要求時的 Azure AD 會將使用者名稱和密碼 (使用公開金鑰加密) 置於佇列。</span><span class="sxs-lookup"><span data-stu-id="e2f56-112">Azure AD, on receiving the sign-in request, places the username and password (encrypted  using a public key) on a queue.</span></span>
5. <span data-ttu-id="e2f56-113">內部部署傳遞驗證代理程式會對佇列進行輸出呼叫，並擷取使用者名稱和加密密碼。</span><span class="sxs-lookup"><span data-stu-id="e2f56-113">An on-premises Pass-through Authentication agent makes an outbound call to the queue and retrieves the username and encrypted password.</span></span>
6. <span data-ttu-id="e2f56-114">代理程式會使用其私密金鑰將密碼解密。</span><span class="sxs-lookup"><span data-stu-id="e2f56-114">The agent decrypts the password using its private key.</span></span>
7. <span data-ttu-id="e2f56-115">代理程式接著會使用標準 Windows API (和 Active Directory 同盟服務所使用的類似機制)，向 Active Directory 驗證使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="e2f56-115">The agent then validates the username and password against Active Directory using standard Windows APIs (a similar mechanism to what is used by Active Directory Federation Services).</span></span> <span data-ttu-id="e2f56-116">使用者名稱可以是內部部署的預設使用者名稱 (通常是 `userPrincipalName`)，或可在 Azure AD Connect 中設定的另一個屬性 (又稱為 `Alternate ID`)。</span><span class="sxs-lookup"><span data-stu-id="e2f56-116">The username can be either the on-premises default username (usually `userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
8. <span data-ttu-id="e2f56-117">內部部署 Active Directory 網域控制站 (DC) 接著會評估要求，並將適當的回應 (成功、失敗、密碼過期或鎖定使用者) 傳回給代理程式。</span><span class="sxs-lookup"><span data-stu-id="e2f56-117">The on-premises Active Directory Domain Controller (DC) then evaluates the request and returns the appropriate response (success, failure, password expired or user locked out) to the agent.</span></span>
9. <span data-ttu-id="e2f56-118">代理程式再將此回應傳回給 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="e2f56-118">The agent, in turn, returns this response back to Azure AD.</span></span>
10. <span data-ttu-id="e2f56-119">Azure AD 會評估回應，並適當地回應使用者；例如，它會立即將使用者登入，或要求 Multi-Factor Authentication (MFA)。</span><span class="sxs-lookup"><span data-stu-id="e2f56-119">Azure AD evaluates the response and responds to the user as appropriate - for example, it either signs the user in immediately or requests for Multi-Factor Authentication (MFA).</span></span>
11. <span data-ttu-id="e2f56-120">如果使用者登入成功，則使用者可以存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="e2f56-120">If the user sign-in is successful, the user is able to access the application.</span></span>

<span data-ttu-id="e2f56-121">下圖說明所有元件和相關步驟。</span><span class="sxs-lookup"><span data-stu-id="e2f56-121">The following diagram illustrates all the components and the steps involved.</span></span>

![傳遞驗證](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a><span data-ttu-id="e2f56-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e2f56-123">Next steps</span></span>
- <span data-ttu-id="e2f56-124">[**目前的限制**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - 此功能目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="e2f56-124">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="e2f56-125">了解支援的情節和不支援的情節。</span><span class="sxs-lookup"><span data-stu-id="e2f56-125">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="e2f56-126">[**快速入門**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - 開始使用 Azure AD 傳遞驗證。</span><span class="sxs-lookup"><span data-stu-id="e2f56-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="e2f56-127">[**常見問題集**](active-directory-aadconnect-pass-through-authentication-faq.md) - 常見問題集的答案。</span><span class="sxs-lookup"><span data-stu-id="e2f56-127">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="e2f56-128">[**疑難排解**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - 了解如何解決此功能的常見問題。</span><span class="sxs-lookup"><span data-stu-id="e2f56-128">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="e2f56-129">[**Azure AD 無縫 SSO**](active-directory-aadconnect-sso.md) - 深入了解此互補功能。</span><span class="sxs-lookup"><span data-stu-id="e2f56-129">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="e2f56-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。</span><span class="sxs-lookup"><span data-stu-id="e2f56-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
