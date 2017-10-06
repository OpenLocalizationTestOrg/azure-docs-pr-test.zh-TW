---
title: "Azure Active Directory B2C：內建原則 | Microsoft Docs"
description: "在 Azure Active Directory B2C 的 hello 可延伸原則架構和如何主題 toocreate 各種原則類型"
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
ms.openlocfilehash: 24bb85eba30f888c6ea7d0401e05235e8eb6ea79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a><span data-ttu-id="d1df0-103">Azure Active Directory B2C：內建原則</span><span class="sxs-lookup"><span data-stu-id="d1df0-103">Azure Active Directory B2C: Built-in policies</span></span>


<span data-ttu-id="d1df0-104">Azure Active Directory (Azure AD) B2C 的 hello 可延伸原則架構是 hello 服務 hello 核心強度。</span><span class="sxs-lookup"><span data-stu-id="d1df0-104">hello extensible policy framework of Azure Active Directory (Azure AD) B2C is hello core strength of hello service.</span></span> <span data-ttu-id="d1df0-105">原則可完整描述取用者身分識別體驗，例如註冊、登入或設定檔編輯。</span><span class="sxs-lookup"><span data-stu-id="d1df0-105">Policies fully describe consumer identity experiences such as sign-up, sign-in, or profile editing.</span></span> <span data-ttu-id="d1df0-106">比方說，註冊原則可讓您 toocontrol 行為藉由設定下列設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="d1df0-106">For instance, a sign-up policy allows you toocontrol behaviors by configuring hello following settings:</span></span>

* <span data-ttu-id="d1df0-107">帳戶類型 （例如 Facebook 社交帳戶） 或本機帳戶，例如電子郵件地址，取用者可以使用 toosign hello 應用程式註冊</span><span class="sxs-lookup"><span data-stu-id="d1df0-107">Account types (social accounts such as Facebook or local accounts such as email addresses) that consumers can use toosign up for hello application</span></span>
* <span data-ttu-id="d1df0-108">屬性 （例如，名字、 郵遞區號和鞋子尺寸） toobe hello 取用者從收集在註冊期間</span><span class="sxs-lookup"><span data-stu-id="d1df0-108">Attributes (for example, first name, postal code, and shoe size) toobe collected from hello consumer during sign-up</span></span>
* <span data-ttu-id="d1df0-109">Azure Multi-Factor Authentication 的使用</span><span class="sxs-lookup"><span data-stu-id="d1df0-109">Use of Azure Multi-Factor Authentication</span></span>
* <span data-ttu-id="d1df0-110">註冊的所有頁面的 hello 外觀與風格</span><span class="sxs-lookup"><span data-stu-id="d1df0-110">hello look and feel of all sign-up pages</span></span>
* <span data-ttu-id="d1df0-111">資訊 （資訊清單，以在權杖中宣告的形式） 的 hello 應用程式收到 hello 原則執行完成時</span><span class="sxs-lookup"><span data-stu-id="d1df0-111">Information (which manifests as claims in a token) that hello application receives when hello policy run finishes</span></span>

<span data-ttu-id="d1df0-112">您可以在租用戶中建立多個不同類型的原則，並視需要在您的應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="d1df0-112">You can create multiple policies of different types in your tenant and use them in your applications as needed.</span></span> <span data-ttu-id="d1df0-113">原則可以跨應用程式重複使用。</span><span class="sxs-lookup"><span data-stu-id="d1df0-113">Policies can be reused across applications.</span></span> <span data-ttu-id="d1df0-114">這種彈性可讓開發人員 toodefine 或並不修改取用者身分識別體驗，幾乎不需要任何變更 tootheir 程式碼。</span><span class="sxs-lookup"><span data-stu-id="d1df0-114">This flexibility enables developers toodefine and modify consumer identity experiences with minimal or no changes tootheir code.</span></span>

<span data-ttu-id="d1df0-115">透過簡單的開發人員介面就可使用原則。</span><span class="sxs-lookup"><span data-stu-id="d1df0-115">Policies are available for use via a simple developer interface.</span></span> <span data-ttu-id="d1df0-116">您的應用程式會使用標準 HTTP 驗證要求 （hello 要求中傳遞原則參數） 來觸發原則，並接收自訂的語彙基元為回應。</span><span class="sxs-lookup"><span data-stu-id="d1df0-116">Your application triggers a policy by using a standard HTTP authentication request (passing a policy parameter in hello request) and receives a customized token as response.</span></span> <span data-ttu-id="d1df0-117">比方說，hello 唯一的差別，可以叫用註冊的原則，以及要求叫用的登入原則是使用 hello"p"查詢字串參數中的 hello 原則名稱：</span><span class="sxs-lookup"><span data-stu-id="d1df0-117">For example, hello only difference between requests that invoke a sign-up policy and requests that invoke a sign-in policy is hello policy name that's used in hello "p" query string parameter:</span></span>

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

<span data-ttu-id="d1df0-118">如需 hello 原則架構的詳細資訊，請參閱[有關 Azure AD B2C 上 hello Enterprise Mobility and Security 部落格此部落格文章](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d1df0-118">For more information about hello policy framework, see [this blog post about Azure AD B2C on hello Enterprise Mobility and Security Blog](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span></span>

## <a name="create-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="d1df0-119">建立註冊或登入原則</span><span class="sxs-lookup"><span data-stu-id="d1df0-119">Create a sign-up or sign-in policy</span></span>

<span data-ttu-id="d1df0-120">此原則可使用單一組態處理取用者註冊和登入經驗。</span><span class="sxs-lookup"><span data-stu-id="d1df0-120">This policy handles both consumer sign-up & sign-in experiences with a single configuration.</span></span> <span data-ttu-id="d1df0-121">取用者會導致下 hello 正確的路徑 （註冊或登入） 視 hello 內容而定。</span><span class="sxs-lookup"><span data-stu-id="d1df0-121">Consumers are led down hello right path (sign-up or sign-in) depending on hello context.</span></span> <span data-ttu-id="d1df0-122">它也會說明 hello 內容 hello 應用程式將會收到在成功註冊或登入的語彙基元。Hello 註冊或登入原則的程式碼範例是[這裡](active-directory-b2c-devquickstarts-web-dotnet-susi.md)。</span><span class="sxs-lookup"><span data-stu-id="d1df0-122">It also describes hello contents of tokens that hello application will receive upon successful sign-ups or sign-ins.  A code sample for hello sign-up or sign-in policy is [available here](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>  <span data-ttu-id="d1df0-123">建議您使用這個原則，而不要使用註冊原則和登入原則。</span><span class="sxs-lookup"><span data-stu-id="d1df0-123">It is recommened that you use this policy over a sign-up policy and sign-in policy.</span></span>  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a><span data-ttu-id="d1df0-124">建立註冊原則</span><span class="sxs-lookup"><span data-stu-id="d1df0-124">Create a sign-up policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a><span data-ttu-id="d1df0-125">建立登入原則</span><span class="sxs-lookup"><span data-stu-id="d1df0-125">Create a sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a><span data-ttu-id="d1df0-126">建立設定檔編輯原則</span><span class="sxs-lookup"><span data-stu-id="d1df0-126">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a><span data-ttu-id="d1df0-127">建立密碼重設原則</span><span class="sxs-lookup"><span data-stu-id="d1df0-127">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a><span data-ttu-id="d1df0-128">常見問題集</span><span class="sxs-lookup"><span data-stu-id="d1df0-128">Frequently asked questions</span></span>

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a><span data-ttu-id="d1df0-129">如何將註冊或登入原則與密碼重設原則連結在一起？</span><span class="sxs-lookup"><span data-stu-id="d1df0-129">How do I link a sign-up or sign-in policy with a password reset policy?</span></span>
<span data-ttu-id="d1df0-130">當您建立的註冊或登入的原則 （使用本機帳戶） 時，您會看到**Forgot 密碼？** hello 經驗 hello 第一頁上的連結。</span><span class="sxs-lookup"><span data-stu-id="d1df0-130">When you create a sign-up or sign-in policy (with local accounts), you see a **Forgot password?** link on hello first page of hello experience.</span></span> <span data-ttu-id="d1df0-131">按一下此連結並不會自動觸發密碼重設原則。</span><span class="sxs-lookup"><span data-stu-id="d1df0-131">Clicking this link doesn't automatically trigger a password reset policy.</span></span> 

<span data-ttu-id="d1df0-132">相反地，hello 錯誤碼** `AADB2C90118` **傳回 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1df0-132">Instead, hello error code **`AADB2C90118`** is returned tooyour app.</span></span> <span data-ttu-id="d1df0-133">您的應用程式必須透過叫用特定的密碼重設原則 toohandle 此錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="d1df0-133">Your app needs toohandle this error code by invoking a specific password reset policy.</span></span> <span data-ttu-id="d1df0-134">如需詳細資訊，請參閱[示範 hello 方法將原則連結的範例](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI)。</span><span class="sxs-lookup"><span data-stu-id="d1df0-134">For more information, see a [sample that demonstrates hello approach of linking policies](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span></span>

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a><span data-ttu-id="d1df0-135">應該使用註冊原則、登入原則還是註冊原則加上登入原則？</span><span class="sxs-lookup"><span data-stu-id="d1df0-135">Should I use a sign-up or sign-in policy or a sign-up policy and a sign-in policy?</span></span>
<span data-ttu-id="d1df0-136">我們建議使用註冊原則或是登入原則，而不要使用註冊原則加上登入原則。</span><span class="sxs-lookup"><span data-stu-id="d1df0-136">We recommend that you use a sign-up or sign-in policy over a sign-up policy and a sign-in policy.</span></span>  

<span data-ttu-id="d1df0-137">hello 註冊或登入的原則都有更多能力比 hello 登入的原則。</span><span class="sxs-lookup"><span data-stu-id="d1df0-137">hello sign-up or sign-in policy has more capabilities than hello sign-in policy.</span></span> <span data-ttu-id="d1df0-138">它也可讓您自訂 toouse 頁面 UI，並有更佳的支援，以進行當地語系化。</span><span class="sxs-lookup"><span data-stu-id="d1df0-138">It also enables you toouse page UI customization and has better support for localization.</span></span> 

<span data-ttu-id="d1df0-139">hello 登入原則建議，如果您不需要 toolocalize 您的原則，只需要次要的自訂功能的商標，而且想密碼重設內建於它。</span><span class="sxs-lookup"><span data-stu-id="d1df0-139">hello sign-in policy is recommended if you don't need toolocalize your policies, only need minor customization capabilities for branding, and want password reset built into it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1df0-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d1df0-140">Next steps</span></span>
* [<span data-ttu-id="d1df0-141">權杖、工作階段及單一登入組態</span><span class="sxs-lookup"><span data-stu-id="d1df0-141">Token, session, and single sign-on configuration</span></span>](active-directory-b2c-token-session-sso.md)
* [<span data-ttu-id="d1df0-142">在取用者註冊期間停用電子郵件驗證</span><span class="sxs-lookup"><span data-stu-id="d1df0-142">Disable email verification during consumer sign-up</span></span>](active-directory-b2c-reference-disable-ev.md)

