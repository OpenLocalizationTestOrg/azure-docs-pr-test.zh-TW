---
title: "aaaAzure Active Directory v2.0 端點 |Microsoft 文件"
description: "使用 Microsoft 帳戶和 Azure Active Directory 登入簡介 toobuilding 應用程式。"
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
ms.openlocfilehash: ae5946b02c50ae5a6137dc1decae66c96647e875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a><span data-ttu-id="c18e6-103">以單一應用程式登入 Microsoft 帳戶和 Azure AD 使用者</span><span class="sxs-lookup"><span data-stu-id="c18e6-103">Sign-in Microsoft Account & Azure AD users in a single app</span></span>
<span data-ttu-id="c18e6-104">在過去，應用程式開發人員想 toosupport 兩個人的 Microsoft 帳戶的 hello 從 Azure Active Directory 的工作帳戶但需要的 toointegrate 與兩個不同的系統。</span><span class="sxs-lookup"><span data-stu-id="c18e6-104">In hello past, an app developer who wanted toosupport both personal Microsoft accounts and work accounts from Azure Active Directory was required toointegrate with two separate systems.</span></span>  <span data-ttu-id="c18e6-105">hello **Azure AD v2.0 端點**導入了新的驗證 API 版本，可讓您在這兩種類型的帳戶使用一個簡單的整合 toosign。</span><span class="sxs-lookup"><span data-stu-id="c18e6-105">hello **Azure AD v2.0 endpoint** introduces a new authentication API version that enables you toosign in both types of accounts using one simple integration.</span></span>  <span data-ttu-id="c18e6-106">使用 hello v2.0 端點的應用程式也可以使用 REST Api 從 hello [Microsoft Graph](https://graph.microsoft.io)使用任一種帳戶。</span><span class="sxs-lookup"><span data-stu-id="c18e6-106">Apps that use hello v2.0 endpoint can also consume REST APIs from hello [Microsoft Graph](https://graph.microsoft.io) using either type of account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c18e6-107">開始使用</span><span class="sxs-lookup"><span data-stu-id="c18e6-107">Getting Started</span></span>
<span data-ttu-id="c18e6-108">選擇您最愛的平台從下列清單 toobuild hello 使用我們的開放原始碼程式庫 （& s） 架構的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c18e6-108">Choose your favorite platform from hello following list toobuild an app using our open source libraries & frameworks.</span></span>  <span data-ttu-id="c18e6-109">或者，您可以使用我們 OAuth 2.0 和 OpenID Connect 通訊協定文件 toosend & 直接不使用驗證程式庫接收通訊協定訊息。</span><span class="sxs-lookup"><span data-stu-id="c18e6-109">Alternatively, you can use our OAuth 2.0 & OpenID Connect protocol documentation toosend & receive protocol messages directly without using an auth library.</span></span>

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a><span data-ttu-id="c18e6-110">新功能</span><span class="sxs-lookup"><span data-stu-id="c18e6-110">What's New</span></span>
<span data-ttu-id="c18e6-111">這裡 hello 資訊將有助於了解為何 （& s） 與 hello v2.0 端點可能不是。</span><span class="sxs-lookup"><span data-stu-id="c18e6-111">hello information here will be useful in understanding what is & what isn't possible with hello v2.0 endpoint.</span></span>

* <span data-ttu-id="c18e6-112">深入了解 hello[類型的應用程式，您可以建立與 hello v2.0 端點](active-directory-v2-flows.md)。</span><span class="sxs-lookup"><span data-stu-id="c18e6-112">Learn about hello [types of apps you can build with hello v2.0 endpoint](active-directory-v2-flows.md).</span></span>
* <span data-ttu-id="c18e6-113">了解 hello[限制、 限制和條件約束](active-directory-v2-limitations.md)與 hello v2.0 端點。</span><span class="sxs-lookup"><span data-stu-id="c18e6-113">Understand hello [limitations, restrictions, and constraints](active-directory-v2-limitations.md) with hello v2.0 endpoint.</span></span>
* <span data-ttu-id="c18e6-114">請參閱本概觀視訊 hello v2.0 端點：</span><span class="sxs-lookup"><span data-stu-id="c18e6-114">Check out this overview video for hello v2.0 endpoint:</span></span>

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a><span data-ttu-id="c18e6-115">參考</span><span class="sxs-lookup"><span data-stu-id="c18e6-115">Reference</span></span>
<span data-ttu-id="c18e6-116">這些連結會是適合用來探索深度 hello 平台：</span><span class="sxs-lookup"><span data-stu-id="c18e6-116">These links will be useful for exploring hello platform in depth:</span></span>

* [<span data-ttu-id="c18e6-117">v2.0 通訊協定參考</span><span class="sxs-lookup"><span data-stu-id="c18e6-117">v2.0 Protocol Reference</span></span>](active-directory-v2-protocols.md)
* [<span data-ttu-id="c18e6-118">v2.0 權杖參考</span><span class="sxs-lookup"><span data-stu-id="c18e6-118">v2.0 Token Reference</span></span>](active-directory-v2-tokens.md)
* [<span data-ttu-id="c18e6-119">v2.0 程式庫參考</span><span class="sxs-lookup"><span data-stu-id="c18e6-119">v2.0 Library Reference</span></span>](active-directory-v2-libraries.md)
* [<span data-ttu-id="c18e6-120">範圍和同意 hello v2.0 端點中</span><span class="sxs-lookup"><span data-stu-id="c18e6-120">Scopes and Consent in hello v2.0 endpoint</span></span>](active-directory-v2-scopes.md)
* [<span data-ttu-id="c18e6-121">Microsoft Graph hello</span><span class="sxs-lookup"><span data-stu-id="c18e6-121">hello Microsoft Graph</span></span>](https://graph.microsoft.io)

## <a name="help--support"></a><span data-ttu-id="c18e6-122">說明及支援</span><span class="sxs-lookup"><span data-stu-id="c18e6-122">Help & Support</span></span>
<span data-ttu-id="c18e6-123">這些是 hello 最佳地方 tooget 說明與 Azure Active Directory 上進行開發。</span><span class="sxs-lookup"><span data-stu-id="c18e6-123">These are hello best places tooget help with developing on Azure Active Directory.</span></span>

* [<span data-ttu-id="c18e6-124">Stack Overflow 的 `azure-active-directory` 和 `adal` 標籤</span><span class="sxs-lookup"><span data-stu-id="c18e6-124">Stack Overflow's `azure-active-directory` and `adal` tags</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [<span data-ttu-id="c18e6-125">Azure Active Directory 的意見反應</span><span class="sxs-lookup"><span data-stu-id="c18e6-125">Feedback on Azure Active Directory</span></span>](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> <span data-ttu-id="c18e6-126">如果您只需要 toosign 公司及學校帳戶，從 Azure Active Directory 中的，您應該開始我們[Azure AD 開發人員手冊 》](active-directory-developers-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="c18e6-126">If you only need toosign in work and school accounts from Azure Active Directory, you should start with our [Azure AD developer's guide](active-directory-developers-guide.md).</span></span>  <span data-ttu-id="c18e6-127">hello v2.0 端點是用於開發人員明確 toosign 中 Microsoft 個人帳戶。</span><span class="sxs-lookup"><span data-stu-id="c18e6-127">hello v2.0 endpoint is intended for use by developers who explicitly need toosign in Microsoft personal accounts.</span></span>

