---
title: "Azure AD Connect：傳遞驗證 - 目前的限制 | Microsoft Docs"
description: "本文說明 Azure Active Directory (Azure AD) 傳遞驗證目前的限制。"
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
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 37c0ea094d02208f2516a4a040f75894e046c670
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a><span data-ttu-id="f48a5-104">Azure Active Directory 傳遞驗證：目前的限制</span><span class="sxs-lookup"><span data-stu-id="f48a5-104">Azure Active Directory Pass-through Authentication: Current limitations</span></span>

>[!IMPORTANT]
><span data-ttu-id="f48a5-105">Azure AD 傳遞驗證目前為預覽功能。</span><span class="sxs-lookup"><span data-stu-id="f48a5-105">Azure AD Pass-through Authentication is currently in preview.</span></span> <span data-ttu-id="f48a5-106">這是免費功能，您不需要任何付費的 Azure AD 版本即可使用。</span><span class="sxs-lookup"><span data-stu-id="f48a5-106">It is a free feature, and you don't need any paid editions of Azure AD to use it.</span></span> <span data-ttu-id="f48a5-107">傳遞驗證僅適用於 Azure AD 的全球執行個體，不適用於 [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) 和 [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/)。</span><span class="sxs-lookup"><span data-stu-id="f48a5-107">Pass-through Authentication is only available in the world-wide instance of Azure AD, and not on [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) and [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="f48a5-108">支援的案例</span><span class="sxs-lookup"><span data-stu-id="f48a5-108">Supported scenarios</span></span>

<span data-ttu-id="f48a5-109">預覽期間完全支援的案例如下︰</span><span class="sxs-lookup"><span data-stu-id="f48a5-109">The following scenarios are fully supported during preview:</span></span>

- <span data-ttu-id="f48a5-110">使用者登入所有網頁瀏覽器應用程式。</span><span class="sxs-lookup"><span data-stu-id="f48a5-110">User sign-ins into all web browser-based applications.</span></span>
- <span data-ttu-id="f48a5-111">使用者登入支援[新式驗證](https://aka.ms/modernauthga)的 Office 365 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="f48a5-111">User sign-ins into Office 365 client applications that support [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="f48a5-112">適用於 Windows 10 裝置的 Azure AD Join。</span><span class="sxs-lookup"><span data-stu-id="f48a5-112">Azure AD Join for Windows 10 devices.</span></span>
- <span data-ttu-id="f48a5-113">Exchange ActiveSync 支援。</span><span class="sxs-lookup"><span data-stu-id="f48a5-113">Exchange ActiveSync support.</span></span>

## <a name="unsupported-scenarios"></a><span data-ttu-id="f48a5-114">不支援的情節</span><span class="sxs-lookup"><span data-stu-id="f48a5-114">Unsupported scenarios</span></span>

<span data-ttu-id="f48a5-115">預覽期間「不」支援的案例如下︰</span><span class="sxs-lookup"><span data-stu-id="f48a5-115">The following scenarios are _not_ supported during preview:</span></span>

- <span data-ttu-id="f48a5-116">使用者登入舊版 Office 用戶端應用程式c (Office 2013 或更早版本)。</span><span class="sxs-lookup"><span data-stu-id="f48a5-116">User sign-ins into legacy Office client applications (Office 2013 or earlier).</span></span> <span data-ttu-id="f48a5-117">組織應該盡可能切換到新式驗證。</span><span class="sxs-lookup"><span data-stu-id="f48a5-117">Organizations are encouraged to switch to modern authentication, if possible.</span></span> <span data-ttu-id="f48a5-118">新式驗證提供傳遞驗證支援，但也可使用 Multi-Factor Authentication (MFA) 等[條件式存取](../active-directory-conditional-access.md)功能，協助您保護使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="f48a5-118">Modern authentication allows for Pass-through Authentication support but also helps you secure your user accounts using [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA).</span></span>
- <span data-ttu-id="f48a5-119">使用者登入商務用 Skype 用戶端應用程式，包括商務用 Skype 2016。</span><span class="sxs-lookup"><span data-stu-id="f48a5-119">User sign-ins into Skype for Business client applications, including Skype for Business 2016.</span></span>
- <span data-ttu-id="f48a5-120">使用者登入 PowerShell 1.0 版。</span><span class="sxs-lookup"><span data-stu-id="f48a5-120">User sign-ins into PowerShell v1.0.</span></span> <span data-ttu-id="f48a5-121">建議您改為使用 PowerShell 2.0 版。</span><span class="sxs-lookup"><span data-stu-id="f48a5-121">It is recommended that you use PowerShell v2.0 instead.</span></span>

>[!IMPORTANT]
><span data-ttu-id="f48a5-122">對於不支援的情節，請在 Azure AD Connect 精靈的[選用功能](active-directory-aadconnect-get-started-custom.md#optional-features)頁面上，啟用 [密碼雜湊同步處理] 作為因應措施。</span><span class="sxs-lookup"><span data-stu-id="f48a5-122">As a workaround for unsupported scenarios, enable Password Hash Synchronization on the [Optional features](active-directory-aadconnect-get-started-custom.md#optional-features) page in the Azure AD Connect wizard.</span></span> <span data-ttu-id="f48a5-123">密碼雜湊同步處理「只是」作為先前情節的後援 (「不是」作為傳遞驗證的一般後援)。</span><span class="sxs-lookup"><span data-stu-id="f48a5-123">Password Hash Synchronization acts as a fallback for the preceding scenarios _only_ (and _not_ as a generic fallback to Pass-through Authentication).</span></span> <span data-ttu-id="f48a5-124">如果您不需要這些情節，請關閉 [密碼雜湊同步處理]。</span><span class="sxs-lookup"><span data-stu-id="f48a5-124">If you don't need these scenarios, turn off Password Hash Synchronization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f48a5-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f48a5-125">Next steps</span></span>
- <span data-ttu-id="f48a5-126">[**快速入門**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - 開始使用 Azure AD 傳遞驗證。</span><span class="sxs-lookup"><span data-stu-id="f48a5-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="f48a5-127">[**技術性深入探討**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - 了解這項功能的運作方式。</span><span class="sxs-lookup"><span data-stu-id="f48a5-127">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="f48a5-128">[**常見問題集**](active-directory-aadconnect-pass-through-authentication-faq.md) - 常見問題集的答案。</span><span class="sxs-lookup"><span data-stu-id="f48a5-128">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="f48a5-129">[**疑難排解**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - 了解如何解決此功能的常見問題。</span><span class="sxs-lookup"><span data-stu-id="f48a5-129">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="f48a5-130">[**Azure AD 無縫 SSO**](active-directory-aadconnect-sso.md) - 深入了解此互補功能。</span><span class="sxs-lookup"><span data-stu-id="f48a5-130">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="f48a5-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。</span><span class="sxs-lookup"><span data-stu-id="f48a5-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
