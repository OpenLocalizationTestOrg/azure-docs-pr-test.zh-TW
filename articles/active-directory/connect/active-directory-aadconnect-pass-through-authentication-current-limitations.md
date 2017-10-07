---
title: "Azure AD Connect：傳遞驗證 - 目前的限制 | Microsoft Docs"
description: "本文說明 hello 目前限制的 Azure Active Directory (Azure AD) 的傳遞驗證。"
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
ms.openlocfilehash: 2933745d071aae205c44659e6ea92697f390effb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a><span data-ttu-id="62ad4-104">Azure Active Directory 傳遞驗證：目前的限制</span><span class="sxs-lookup"><span data-stu-id="62ad4-104">Azure Active Directory Pass-through Authentication: Current limitations</span></span>

>[!IMPORTANT]
><span data-ttu-id="62ad4-105">Azure AD 傳遞驗證目前為預覽功能。</span><span class="sxs-lookup"><span data-stu-id="62ad4-105">Azure AD Pass-through Authentication is currently in preview.</span></span> <span data-ttu-id="62ad4-106">這是可用的功能，而且不需要任何付費的版本的 Azure AD toouse 它。</span><span class="sxs-lookup"><span data-stu-id="62ad4-106">It is a free feature, and you don't need any paid editions of Azure AD toouse it.</span></span> <span data-ttu-id="62ad4-107">傳遞驗證僅供以 hello 全球執行個體的 Azure AD 中，而不是在[Microsoft 雲端德國](http://www.microsoft.de/cloud-deutschland)和[Microsoft Azure 政府雲端](https://azure.microsoft.com/features/gov/)。</span><span class="sxs-lookup"><span data-stu-id="62ad4-107">Pass-through Authentication is only available in hello world-wide instance of Azure AD, and not on [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) and [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="62ad4-108">支援的案例</span><span class="sxs-lookup"><span data-stu-id="62ad4-108">Supported scenarios</span></span>

<span data-ttu-id="62ad4-109">在預覽期間完全支援下列案例的 hello:</span><span class="sxs-lookup"><span data-stu-id="62ad4-109">hello following scenarios are fully supported during preview:</span></span>

- <span data-ttu-id="62ad4-110">使用者登入所有網頁瀏覽器應用程式。</span><span class="sxs-lookup"><span data-stu-id="62ad4-110">User sign-ins into all web browser-based applications.</span></span>
- <span data-ttu-id="62ad4-111">使用者登入支援[新式驗證](https://aka.ms/modernauthga)的 Office 365 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="62ad4-111">User sign-ins into Office 365 client applications that support [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="62ad4-112">適用於 Windows 10 裝置的 Azure AD Join。</span><span class="sxs-lookup"><span data-stu-id="62ad4-112">Azure AD Join for Windows 10 devices.</span></span>
- <span data-ttu-id="62ad4-113">Exchange ActiveSync 支援。</span><span class="sxs-lookup"><span data-stu-id="62ad4-113">Exchange ActiveSync support.</span></span>

## <a name="unsupported-scenarios"></a><span data-ttu-id="62ad4-114">不支援的情節</span><span class="sxs-lookup"><span data-stu-id="62ad4-114">Unsupported scenarios</span></span>

<span data-ttu-id="62ad4-115">hello 案例如下_不_支援在預覽期間：</span><span class="sxs-lookup"><span data-stu-id="62ad4-115">hello following scenarios are _not_ supported during preview:</span></span>

- <span data-ttu-id="62ad4-116">使用者登入舊版 Office 用戶端應用程式c (Office 2013 或更早版本)。</span><span class="sxs-lookup"><span data-stu-id="62ad4-116">User sign-ins into legacy Office client applications (Office 2013 or earlier).</span></span> <span data-ttu-id="62ad4-117">組織可能的話會鼓勵的 tooswitch toomodern 驗證。</span><span class="sxs-lookup"><span data-stu-id="62ad4-117">Organizations are encouraged tooswitch toomodern authentication, if possible.</span></span> <span data-ttu-id="62ad4-118">新式驗證提供傳遞驗證支援，但也可使用 Multi-Factor Authentication (MFA) 等[條件式存取](../active-directory-conditional-access.md)功能，協助您保護使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="62ad4-118">Modern authentication allows for Pass-through Authentication support but also helps you secure your user accounts using [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA).</span></span>
- <span data-ttu-id="62ad4-119">使用者登入商務用 Skype 用戶端應用程式，包括商務用 Skype 2016。</span><span class="sxs-lookup"><span data-stu-id="62ad4-119">User sign-ins into Skype for Business client applications, including Skype for Business 2016.</span></span>
- <span data-ttu-id="62ad4-120">使用者登入 PowerShell 1.0 版。</span><span class="sxs-lookup"><span data-stu-id="62ad4-120">User sign-ins into PowerShell v1.0.</span></span> <span data-ttu-id="62ad4-121">建議您改為使用 PowerShell 2.0 版。</span><span class="sxs-lookup"><span data-stu-id="62ad4-121">It is recommended that you use PowerShell v2.0 instead.</span></span>

>[!IMPORTANT]
><span data-ttu-id="62ad4-122">不支援的案例的因應措施，以啟用密碼雜湊同步處理在 hello[選用功能](active-directory-aadconnect-get-started-custom.md#optional-features)hello Azure AD Connect 精靈 頁面。</span><span class="sxs-lookup"><span data-stu-id="62ad4-122">As a workaround for unsupported scenarios, enable Password Hash Synchronization on hello [Optional features](active-directory-aadconnect-get-started-custom.md#optional-features) page in hello Azure AD Connect wizard.</span></span> <span data-ttu-id="62ad4-123">密碼雜湊同步處理做為後援 hello 上述案例_只_(和_不_做為泛型後援 tooPass 透過驗證)。</span><span class="sxs-lookup"><span data-stu-id="62ad4-123">Password Hash Synchronization acts as a fallback for hello preceding scenarios _only_ (and _not_ as a generic fallback tooPass-through Authentication).</span></span> <span data-ttu-id="62ad4-124">如果您不需要這些情節，請關閉 [密碼雜湊同步處理]。</span><span class="sxs-lookup"><span data-stu-id="62ad4-124">If you don't need these scenarios, turn off Password Hash Synchronization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62ad4-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="62ad4-125">Next steps</span></span>
- <span data-ttu-id="62ad4-126">[**快速入門**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - 開始使用 Azure AD 傳遞驗證。</span><span class="sxs-lookup"><span data-stu-id="62ad4-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="62ad4-127">[**技術性深入探討**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - 了解這項功能的運作方式。</span><span class="sxs-lookup"><span data-stu-id="62ad4-127">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="62ad4-128">[**常見問題集**](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently 常見問題的答案。</span><span class="sxs-lookup"><span data-stu-id="62ad4-128">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="62ad4-129">[**疑難排解**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -了解如何 tooresolve 常見問題與 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="62ad4-129">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="62ad4-130">[**Azure AD 無縫 SSO**](active-directory-aadconnect-sso.md) - 深入了解此互補功能。</span><span class="sxs-lookup"><span data-stu-id="62ad4-130">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="62ad4-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。</span><span class="sxs-lookup"><span data-stu-id="62ad4-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
