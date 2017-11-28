---
title: "Azure Active Directory B2C：自訂原則 | 登陸頁面 | Microsoft Docs"
description: "使用自訂原則透過 Azure Active Directory B2C 開發取用者導向應用程式"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f2079f53-a637-4f2d-b3a0-61a9647ad433
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 5/06/2017
ms.author: parakhj
ms.openlocfilehash: 28a39f282488b81fc9e2ab7841b5f2cb4cd58715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-up-and-sign-in-consumers-in-your-applications-using-custom-policies"></a><span data-ttu-id="0007f-103">Azure Active Directory B2C：使用自訂原則在您的應用程式中註冊與登入取用者</span><span class="sxs-lookup"><span data-stu-id="0007f-103">Azure Active Directory B2C: Sign up and sign in consumers in your applications using custom policies</span></span>
<span data-ttu-id="0007f-104">自訂的原則是定義您的 Azure AD B2C 租用戶的 hello 行為的組態檔。</span><span class="sxs-lookup"><span data-stu-id="0007f-104">Custom policies are configuration files that define hello behavior of your Azure AD B2C tenant.</span></span> <span data-ttu-id="0007f-105">它們可以是完整的身分識別開發人員 toocomplete 編輯附近的無限制的工作數目。</span><span class="sxs-lookup"><span data-stu-id="0007f-105">They can be fully edited by an identity developer toocomplete a near unlimited number of tasks.</span></span>

## <a name="how-tooarticles"></a><span data-ttu-id="0007f-106">如何 tooarticles</span><span class="sxs-lookup"><span data-stu-id="0007f-106">How-tooarticles</span></span>
<span data-ttu-id="0007f-107">深入了解如何 toouse 特定 Azure Active Directory B2C 功能：</span><span class="sxs-lookup"><span data-stu-id="0007f-107">Learn how toouse specific Azure Active Directory B2C features:</span></span>

* [<span data-ttu-id="0007f-108">開始使用</span><span class="sxs-lookup"><span data-stu-id="0007f-108">Get Started</span></span>](active-directory-b2c-overview-custom.md)
* <span data-ttu-id="0007f-109">設定 OIDC 提供者，例如 [Azure AD](active-directory-b2c-setup-aad-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="0007f-109">Configure OIDC Providers such as [Azure AD](active-directory-b2c-setup-aad-custom.md).</span></span>
* <span data-ttu-id="0007f-110">設定 SAML 提供者，例如 [Salesforce](active-directory-b2c-setup-sf-app-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="0007f-110">Configure SAML Providers such as [Salesforce](active-directory-b2c-setup-sf-app-custom.md).</span></span>
* <span data-ttu-id="0007f-111">整合 RESTful API：</span><span class="sxs-lookup"><span data-stu-id="0007f-111">Integrate RESTful APIs:</span></span>
    * <span data-ttu-id="0007f-112">[取得額外宣告](active-directory-b2c-rest-api-step-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="0007f-112">[Obtain additional claims](active-directory-b2c-rest-api-step-custom.md).</span></span>
    * <span data-ttu-id="0007f-113">[驗證使用者輸入](active-directory-b2c-rest-api-validation-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="0007f-113">[Validate user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>
* <span data-ttu-id="0007f-114">自訂登入：</span><span class="sxs-lookup"><span data-stu-id="0007f-114">Customize Login:</span></span>
    * [<span data-ttu-id="0007f-115">設定使用者輸入</span><span class="sxs-lookup"><span data-stu-id="0007f-115">Configure User Input</span></span>](active-directory-b2c-configure-signup-self-asserted-custom.md)
    * [<span data-ttu-id="0007f-116">自訂 UI</span><span class="sxs-lookup"><span data-stu-id="0007f-116">Customize UI</span></span>](active-directory-b2c-ui-customization-custom.md)
    * [<span data-ttu-id="0007f-117">自訂權杖</span><span class="sxs-lookup"><span data-stu-id="0007f-117">Customize Token</span></span>](active-directory-b2c-reference-manage-sso-and-token-configuration.md)
* <span data-ttu-id="0007f-118">[使用 Application Insights 收集記錄](active-directory-b2c-troubleshoot-custom.md)以進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="0007f-118">Troubleshoot by [collecting logs using Application Insights](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="whats-new"></a><span data-ttu-id="0007f-119">新功能</span><span class="sxs-lookup"><span data-stu-id="0007f-119">What's new</span></span>
<span data-ttu-id="0007f-120">回到這裡查看通常需未來變更 toohello Azure Active Directory B2C toolearn。</span><span class="sxs-lookup"><span data-stu-id="0007f-120">Check back here often toolearn about future changes toohello Azure Active Directory B2C.</span></span> <span data-ttu-id="0007f-121">我們也會使用 @AzureAD 發佈任何更新的相關推文。</span><span class="sxs-lookup"><span data-stu-id="0007f-121">We'll also tweet about any updates by using @AzureAD.</span></span>



