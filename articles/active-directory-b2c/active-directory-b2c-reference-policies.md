---
title: "Azure Active Directory B2C：內建原則 | Microsoft Docs"
description: "關於 Azure Active Directory B2C 的可延伸原則架構及如何建立各種原則類型的主題"
services: active-directory-b2c
documentationcenter: 
author: sama
manager: mbaldwin
editor: PatAltimore
ms.assetid: 0d453e72-7f70-4aa2-953d-938d2814d5a9
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: sama
ms.openlocfilehash: daad3af089afdf76b930053728bb11a5cf4c2a92
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a><span data-ttu-id="4bd69-103">Azure Active Directory B2C：內建原則</span><span class="sxs-lookup"><span data-stu-id="4bd69-103">Azure Active Directory B2C: Built-in policies</span></span>


<span data-ttu-id="4bd69-104">Azure Active Directory (Azure AD) B2C 的可延伸原則架構是服務的核心力量。</span><span class="sxs-lookup"><span data-stu-id="4bd69-104">The extensible policy framework of Azure Active Directory (Azure AD) B2C is the core strength of the service.</span></span> <span data-ttu-id="4bd69-105">原則可完整描述取用者身分識別體驗，例如註冊、登入或設定檔編輯。</span><span class="sxs-lookup"><span data-stu-id="4bd69-105">Policies fully describe consumer identity experiences such as sign-up, sign-in, or profile editing.</span></span> <span data-ttu-id="4bd69-106">比方說，註冊原則可讓進行下列設定來控制行為：</span><span class="sxs-lookup"><span data-stu-id="4bd69-106">For instance, a sign-up policy allows you to control behaviors by configuring the following settings:</span></span>

* <span data-ttu-id="4bd69-107">可供取用者用來註冊應用程式的帳戶類型 (例如 Facebook 等社交帳戶，或像是電子郵件地址的本機帳戶)</span><span class="sxs-lookup"><span data-stu-id="4bd69-107">Account types (social accounts such as Facebook or local accounts such as email addresses) that consumers can use to sign up for the application</span></span>
* <span data-ttu-id="4bd69-108">註冊時向取用者收集的屬性 (例如名字、郵遞區號和鞋子尺寸)</span><span class="sxs-lookup"><span data-stu-id="4bd69-108">Attributes (for example, first name, postal code, and shoe size) to be collected from the consumer during sign-up</span></span>
* <span data-ttu-id="4bd69-109">Azure Multi-Factor Authentication 的使用</span><span class="sxs-lookup"><span data-stu-id="4bd69-109">Use of Azure Multi-Factor Authentication</span></span>
* <span data-ttu-id="4bd69-110">所有註冊頁面的外觀與風格</span><span class="sxs-lookup"><span data-stu-id="4bd69-110">The look and feel of all sign-up pages</span></span>
* <span data-ttu-id="4bd69-111">原則執行完成時應用程式所接收的資訊 (以權杖中的宣告表示)</span><span class="sxs-lookup"><span data-stu-id="4bd69-111">Information (which manifests as claims in a token) that the application receives when the policy run finishes</span></span>

<span data-ttu-id="4bd69-112">您可以在租用戶中建立多個不同類型的原則，並視需要在您的應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="4bd69-112">You can create multiple policies of different types in your tenant and use them in your applications as needed.</span></span> <span data-ttu-id="4bd69-113">原則可以跨應用程式重複使用。</span><span class="sxs-lookup"><span data-stu-id="4bd69-113">Policies can be reused across applications.</span></span> <span data-ttu-id="4bd69-114">此一彈性可讓開發人員在少量變更或完全不變更程式碼的情況，定義及修改取用者身分識別體驗。</span><span class="sxs-lookup"><span data-stu-id="4bd69-114">This flexibility enables developers to define and modify consumer identity experiences with minimal or no changes to their code.</span></span>

<span data-ttu-id="4bd69-115">透過簡單的開發人員介面就可使用原則。</span><span class="sxs-lookup"><span data-stu-id="4bd69-115">Policies are available for use via a simple developer interface.</span></span> <span data-ttu-id="4bd69-116">您的應用程式使用標準 HTTP 驗證要求來觸發原則 (在要求中傳遞原則參數)，並從回應中收到自訂的權杖。</span><span class="sxs-lookup"><span data-stu-id="4bd69-116">Your application triggers a policy by using a standard HTTP authentication request (passing a policy parameter in the request) and receives a customized token as response.</span></span> <span data-ttu-id="4bd69-117">例如，在叫用註冊原則的要求和叫用登入原則的要求之間，唯一的差別在於 "p" 查詢字串參數中使用的原則名稱：</span><span class="sxs-lookup"><span data-stu-id="4bd69-117">For example, the only difference between requests that invoke a sign-up policy and requests that invoke a sign-in policy is the policy name that's used in the "p" query string parameter:</span></span>

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siup                                       // Your sign-up policy

```

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siin                                       // Your sign-in policy

```

<span data-ttu-id="4bd69-118">如需原則架構的詳細資訊，請參閱 [Enterprise Mobility and Security 部落格上關於 Azure AD B2C 的這篇部落格文章](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4bd69-118">For more information about the policy framework, see [this blog post about Azure AD B2C on the Enterprise Mobility and Security Blog](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span></span>

## <a name="create-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="4bd69-119">建立註冊或登入原則</span><span class="sxs-lookup"><span data-stu-id="4bd69-119">Create a sign-up or sign-in policy</span></span>

<span data-ttu-id="4bd69-120">此原則可使用單一組態處理取用者註冊和登入經驗。</span><span class="sxs-lookup"><span data-stu-id="4bd69-120">This policy handles both consumer sign-up & sign-in experiences with a single configuration.</span></span> <span data-ttu-id="4bd69-121">視內容而定，取用者會被引導到正確的路徑 (註冊或登入)。</span><span class="sxs-lookup"><span data-stu-id="4bd69-121">Consumers are led down the right path (sign-up or sign-in) depending on the context.</span></span> <span data-ttu-id="4bd69-122">此原則也會描述在成功註冊或登入時，應用程式將收到的權杖內容。您可以 [在這裡找到](active-directory-b2c-devquickstarts-web-dotnet-susi.md)註冊或登入原則的代碼範例。</span><span class="sxs-lookup"><span data-stu-id="4bd69-122">It also describes the contents of tokens that the application will receive upon successful sign-ups or sign-ins.  A code sample for the sign-up or sign-in policy is [available here](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>  <span data-ttu-id="4bd69-123">建議您使用這個原則，而不要使用註冊原則和登入原則。</span><span class="sxs-lookup"><span data-stu-id="4bd69-123">It is recommened that you use this policy over a sign-up policy and sign-in policy.</span></span>  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a><span data-ttu-id="4bd69-124">建立註冊原則</span><span class="sxs-lookup"><span data-stu-id="4bd69-124">Create a sign-up policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a><span data-ttu-id="4bd69-125">建立登入原則</span><span class="sxs-lookup"><span data-stu-id="4bd69-125">Create a sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a><span data-ttu-id="4bd69-126">建立設定檔編輯原則</span><span class="sxs-lookup"><span data-stu-id="4bd69-126">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a><span data-ttu-id="4bd69-127">建立密碼重設原則</span><span class="sxs-lookup"><span data-stu-id="4bd69-127">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a><span data-ttu-id="4bd69-128">常見問題集</span><span class="sxs-lookup"><span data-stu-id="4bd69-128">Frequently asked questions</span></span>

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a><span data-ttu-id="4bd69-129">如何將註冊或登入原則與密碼重設原則連結在一起？</span><span class="sxs-lookup"><span data-stu-id="4bd69-129">How do I link a sign-up or sign-in policy with a password reset policy?</span></span>
<span data-ttu-id="4bd69-130">當您建立註冊或登入原則 (搭配本機帳戶) 時，您會在該體驗的第一個頁面上看到[忘記密碼?] 連結。</span><span class="sxs-lookup"><span data-stu-id="4bd69-130">When you create a sign-up or sign-in policy (with local accounts), you see a **Forgot password?** link on the first page of the experience.</span></span> <span data-ttu-id="4bd69-131">按一下此連結並不會自動觸發密碼重設原則。</span><span class="sxs-lookup"><span data-stu-id="4bd69-131">Clicking this link doesn't automatically trigger a password reset policy.</span></span> 

<span data-ttu-id="4bd69-132">相反地，系統會將錯誤碼 **`AADB2C90118`** 傳回您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4bd69-132">Instead, the error code **`AADB2C90118`** is returned to your app.</span></span> <span data-ttu-id="4bd69-133">您的應用程式必須叫用特定的密碼重設原則來處理此錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="4bd69-133">Your app needs to handle this error code by invoking a specific password reset policy.</span></span> <span data-ttu-id="4bd69-134">如需詳細資訊，請參閱[示範連結原則方法的範例](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI)。</span><span class="sxs-lookup"><span data-stu-id="4bd69-134">For more information, see a [sample that demonstrates the approach of linking policies](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span></span>

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a><span data-ttu-id="4bd69-135">應該使用註冊原則、登入原則還是註冊原則加上登入原則？</span><span class="sxs-lookup"><span data-stu-id="4bd69-135">Should I use a sign-up or sign-in policy or a sign-up policy and a sign-in policy?</span></span>
<span data-ttu-id="4bd69-136">我們建議使用註冊原則或是登入原則，而不要使用註冊原則加上登入原則。</span><span class="sxs-lookup"><span data-stu-id="4bd69-136">We recommend that you use a sign-up or sign-in policy over a sign-up policy and a sign-in policy.</span></span>  

<span data-ttu-id="4bd69-137">註冊原則或登入原則的功能比登入原則還多。</span><span class="sxs-lookup"><span data-stu-id="4bd69-137">The sign-up or sign-in policy has more capabilities than the sign-in policy.</span></span> <span data-ttu-id="4bd69-138">它也可讓您使用頁面 UI 自訂，並且對當地語系化有更強的支援。</span><span class="sxs-lookup"><span data-stu-id="4bd69-138">It also enables you to use page UI customization and has better support for localization.</span></span> 

<span data-ttu-id="4bd69-139">如果您不需要將原則當地語系化，只需要較少的自訂功能來設定商標，而且想要內建密碼重設功能，則建議您使用登入原則。</span><span class="sxs-lookup"><span data-stu-id="4bd69-139">The sign-in policy is recommended if you don't need to localize your policies, only need minor customization capabilities for branding, and want password reset built into it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bd69-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4bd69-140">Next steps</span></span>
* [<span data-ttu-id="4bd69-141">權杖、工作階段及單一登入組態</span><span class="sxs-lookup"><span data-stu-id="4bd69-141">Token, session, and single sign-on configuration</span></span>](active-directory-b2c-token-session-sso.md)
* [<span data-ttu-id="4bd69-142">在取用者註冊期間停用電子郵件驗證</span><span class="sxs-lookup"><span data-stu-id="4bd69-142">Disable email verification during consumer sign-up</span></span>](active-directory-b2c-reference-disable-ev.md)

