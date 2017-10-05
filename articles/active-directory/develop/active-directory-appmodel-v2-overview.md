---
title: "Azure Active Directory v2.0 端點 | Microsoft Docs"
description: "建置具備 Microsoft 帳戶和 Azure Active Directory 登入之應用程式的簡介。"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 2dee579f-fdf6-474b-bc2c-016c931eaa27
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 1e286044fb1a1b367fcac2dc14c47f68d5ed120d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a><span data-ttu-id="e80db-103">以單一應用程式登入 Microsoft 帳戶和 Azure AD 使用者</span><span class="sxs-lookup"><span data-stu-id="e80db-103">Sign-in Microsoft Account & Azure AD users in a single app</span></span>
<span data-ttu-id="e80db-104">在過去，想要同時支援個人之 Microsoft 帳戶和得自 Azure Active Directory 之公司帳戶的應用程式開發人員必須整合這兩個不同的系統。</span><span class="sxs-lookup"><span data-stu-id="e80db-104">In the past, an app developer who wanted to support both personal Microsoft accounts and work accounts from Azure Active Directory was required to integrate with two separate systems.</span></span>  <span data-ttu-id="e80db-105">**Azure AD v2.0 端點**引進了新的驗證 API 版本，可讓您在進行過一次簡單的整合後，就能同時登入這兩種帳戶。</span><span class="sxs-lookup"><span data-stu-id="e80db-105">The **Azure AD v2.0 endpoint** introduces a new authentication API version that enables you to sign in both types of accounts using one simple integration.</span></span>  <span data-ttu-id="e80db-106">使用 v2.0 端點的應用程式也可以利用這其中一種帳戶，從 [Microsoft Graph](https://graph.microsoft.io) 取用 REST API。</span><span class="sxs-lookup"><span data-stu-id="e80db-106">Apps that use the v2.0 endpoint can also consume REST APIs from the [Microsoft Graph](https://graph.microsoft.io) using either type of account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="e80db-107">開始使用</span><span class="sxs-lookup"><span data-stu-id="e80db-107">Getting Started</span></span>
<span data-ttu-id="e80db-108">從下列清單選擇您最愛的平台，使用我們的開放原始碼程式庫與架構來建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="e80db-108">Choose your favorite platform from the following list to build an app using our open source libraries & frameworks.</span></span>  <span data-ttu-id="e80db-109">或者，您可以使用 OAuth 2.0 和 OpenID Connect 通訊協定文件，直接傳送及接收通訊協定訊息，而不使用驗證庫。</span><span class="sxs-lookup"><span data-stu-id="e80db-109">Alternatively, you can use our OAuth 2.0 & OpenID Connect protocol documentation to send & receive protocol messages directly without using an auth library.</span></span>

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a><span data-ttu-id="e80db-110">新功能</span><span class="sxs-lookup"><span data-stu-id="e80db-110">What's New</span></span>
<span data-ttu-id="e80db-111">當您想要了解 v2.0 端點可執行哪些動作以及不可執行哪些動作時，此處提供的資訊非常實用。</span><span class="sxs-lookup"><span data-stu-id="e80db-111">The information here will be useful in understanding what is & what isn't possible with the v2.0 endpoint.</span></span>

* <span data-ttu-id="e80db-112">了解 [您可以使用 v2.0 端點建置的應用程式類型](active-directory-v2-flows.md)。</span><span class="sxs-lookup"><span data-stu-id="e80db-112">Learn about the [types of apps you can build with the v2.0 endpoint](active-directory-v2-flows.md).</span></span>
* <span data-ttu-id="e80db-113">了解使用 v2.0 端點的 [限制和條件約束](active-directory-v2-limitations.md) 。</span><span class="sxs-lookup"><span data-stu-id="e80db-113">Understand the [limitations, restrictions, and constraints](active-directory-v2-limitations.md) with the v2.0 endpoint.</span></span>
* <span data-ttu-id="e80db-114">請觀賞這部關於 v2.0 端點的概觀影片︰</span><span class="sxs-lookup"><span data-stu-id="e80db-114">Check out this overview video for the v2.0 endpoint:</span></span>

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a><span data-ttu-id="e80db-115">參考</span><span class="sxs-lookup"><span data-stu-id="e80db-115">Reference</span></span>
<span data-ttu-id="e80db-116">下列連結有助於深入探索平台：</span><span class="sxs-lookup"><span data-stu-id="e80db-116">These links will be useful for exploring the platform in depth:</span></span>

* [<span data-ttu-id="e80db-117">v2.0 通訊協定參考</span><span class="sxs-lookup"><span data-stu-id="e80db-117">v2.0 Protocol Reference</span></span>](active-directory-v2-protocols.md)
* [<span data-ttu-id="e80db-118">v2.0 權杖參考</span><span class="sxs-lookup"><span data-stu-id="e80db-118">v2.0 Token Reference</span></span>](active-directory-v2-tokens.md)
* [<span data-ttu-id="e80db-119">v2.0 程式庫參考</span><span class="sxs-lookup"><span data-stu-id="e80db-119">v2.0 Library Reference</span></span>](active-directory-v2-libraries.md)
* [<span data-ttu-id="e80db-120">v2.0 端點的範圍和同意</span><span class="sxs-lookup"><span data-stu-id="e80db-120">Scopes and Consent in the v2.0 endpoint</span></span>](active-directory-v2-scopes.md)
* [<span data-ttu-id="e80db-121">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="e80db-121">The Microsoft Graph</span></span>](https://graph.microsoft.io)

## <a name="help--support"></a><span data-ttu-id="e80db-122">說明及支援</span><span class="sxs-lookup"><span data-stu-id="e80db-122">Help & Support</span></span>
<span data-ttu-id="e80db-123">以下是取得在 Azure Active Directory 開發之協助的最佳位置。</span><span class="sxs-lookup"><span data-stu-id="e80db-123">These are the best places to get help with developing on Azure Active Directory.</span></span>

* [<span data-ttu-id="e80db-124">Stack Overflow 的 `azure-active-directory` 和 `adal` 標籤</span><span class="sxs-lookup"><span data-stu-id="e80db-124">Stack Overflow's `azure-active-directory` and `adal` tags</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [<span data-ttu-id="e80db-125">Azure Active Directory 的意見反應</span><span class="sxs-lookup"><span data-stu-id="e80db-125">Feedback on Azure Active Directory</span></span>](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> <span data-ttu-id="e80db-126">如果您只需要從 Azure Active directory 登入公司及學校帳戶，則應該先閱讀我們的 [Azure AD 開發人員指南](active-directory-developers-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="e80db-126">If you only need to sign in work and school accounts from Azure Active Directory, you should start with our [Azure AD developer's guide](active-directory-developers-guide.md).</span></span>  <span data-ttu-id="e80db-127">v2.0 端點的適用對象是明確需要登入 Microsoft 個人帳戶的開發人員。</span><span class="sxs-lookup"><span data-stu-id="e80db-127">The v2.0 endpoint is intended for use by developers who explicitly need to sign in Microsoft personal accounts.</span></span>

