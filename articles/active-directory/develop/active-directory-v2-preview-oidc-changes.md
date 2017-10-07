---
title: "aaaChanges toohello Azure AD v2.0 端點 |Microsoft 文件"
description: "Toohello 應用程式模型 v2.0 公用預覽通訊協定所進行的變更的描述。"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e6c5b891-0b5d-47dc-8184-5d0ef6a1a006
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: d7b28a481e12d5dbbc4a10110193bdbd754f4929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="important-updates-toohello-v20-authentication-protocols"></a><span data-ttu-id="af0ad-103">重要的更新 toohello v2.0 驗證通訊協定</span><span class="sxs-lookup"><span data-stu-id="af0ad-103">Important Updates toohello v2.0 Authentication Protocols</span></span>
<span data-ttu-id="af0ad-104">開發人員請注意！</span><span class="sxs-lookup"><span data-stu-id="af0ad-104">Attention developers!</span></span> <span data-ttu-id="af0ad-105">透過 hello 接下來的兩週，我們會提出一些更新 tooour v2.0 驗證通訊協定，這可能表示重大我們預覽期間，您已撰寫的任何應用程式的變更。</span><span class="sxs-lookup"><span data-stu-id="af0ad-105">Over hello next two weeks, we will be making a few updates tooour v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="af0ad-106">那些人會受到影響？</span><span class="sxs-lookup"><span data-stu-id="af0ad-106">Who does this affect?</span></span>
<span data-ttu-id="af0ad-107">已寫入 toouse hello v2.0 任何應用程式建立聚合式驗證端點</span><span class="sxs-lookup"><span data-stu-id="af0ad-107">Any apps that have been written toouse hello v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="af0ad-108">可以找到更多資訊 hello v2.0 端點上的[這裡](active-directory-appmodel-v2-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="af0ad-108">More information on hello v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="af0ad-109">如果您已建立應用程式由撰寫程式碼直接 toohello v2.0 通訊協定，使用 hello v2.0 端點使用任何我們 OpenID Connect 或 OAuth web middlewares 或使用其他第 3 個合作對象文件庫 tooperform 驗證，您應該備妥 tootest 專案和產生如有必要的變更。</span><span class="sxs-lookup"><span data-stu-id="af0ad-109">If you have built an app using hello v2.0 endpoint by coding directly toohello v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries tooperform authentication, you should be prepared tootest your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="af0ad-110">那些人不會受到影響？</span><span class="sxs-lookup"><span data-stu-id="af0ad-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="af0ad-111">已寫入 hello 實際執行 Azure AD 驗證端點，針對任何應用程式</span><span class="sxs-lookup"><span data-stu-id="af0ad-111">Any apps that have been written against hello production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="af0ad-112">此通訊協定一定都是如此，並且不會發生任何變更。</span><span class="sxs-lookup"><span data-stu-id="af0ad-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="af0ad-113">此外，如果您的應用程式**只**使用我們的 ADAL 程式庫 tooperform 驗證，您將不會動用 toochange。</span><span class="sxs-lookup"><span data-stu-id="af0ad-113">Furthermore, if your app **only** uses our ADAL library tooperform authentication, you won\`t have toochange anything.</span></span>  <span data-ttu-id="af0ad-114">ADAL 具有受防護 hello 變更您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="af0ad-114">ADAL has shielded your app from hello changes.</span></span>  

## <a name="what-are-hello-changes"></a><span data-ttu-id="af0ad-115">Hello 變更有哪些？</span><span class="sxs-lookup"><span data-stu-id="af0ad-115">What are hello changes?</span></span>
### <a name="removing-hello-x5t-value-from-jwt-headers"></a><span data-ttu-id="af0ad-116">JWT 標頭中移除 hello x5t 值</span><span class="sxs-lookup"><span data-stu-id="af0ad-116">Removing hello x5t value from JWT headers</span></span>
<span data-ttu-id="af0ad-117">hello v2.0 端點會使用 JWT 權杖，其中包含相關 hello 語彙基元的相關中繼資料的標頭參數區段。</span><span class="sxs-lookup"><span data-stu-id="af0ad-117">hello v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about hello token.</span></span>  <span data-ttu-id="af0ad-118">如果解碼其中我們目前 Jwt 的 hello 標頭時，您會發現像這樣：</span><span class="sxs-lookup"><span data-stu-id="af0ad-118">If you decode hello header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="af0ad-119">這兩個 hello"x5t"和"限 kid"屬性，指定 hello 公開金鑰，應該使用的 toovalidate hello 權杖之簽章，因為從 hello OpenID Connect 的中繼資料端點擷取。</span><span class="sxs-lookup"><span data-stu-id="af0ad-119">Where both hello "x5t" and "kid" properties identify hello public key that should be used toovalidate hello token\`s signature, as retrieved from hello OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="af0ad-120">hello 這裡，我們正在進行的變更是 tooremove hello"x5t"屬性。</span><span class="sxs-lookup"><span data-stu-id="af0ad-120">hello change we are making here is tooremove hello "x5t" property.</span></span>  <span data-ttu-id="af0ad-121">您可以繼續 toouse hello 相同機制 toovalidate 語彙基元，但應該只信任 hello"限 kid"屬性 tooretrieve hello 正確公開金鑰，以指定在 hello OpenID Connect 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="af0ad-121">You may continue toouse hello same mechanisms toovalidate tokens, but should rely only on hello "kid" property tooretrieve hello correct public key, as specified in hello OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="af0ad-122">**您的工作： 請確定您的應用程式不相依於是否存在 hello hello x5t 值。**</span><span class="sxs-lookup"><span data-stu-id="af0ad-122">**Your job: Make sure your app does not depend on hello existence of hello x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="af0ad-123">移除 profile_info</span><span class="sxs-lookup"><span data-stu-id="af0ad-123">Removing profile_info</span></span>
<span data-ttu-id="af0ad-124">先前，hello v2.0 端點具有已傳回 base64 編碼的 JSON 物件中呼叫的權杖回應`profile_info`。</span><span class="sxs-lookup"><span data-stu-id="af0ad-124">Previously, hello v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="af0ad-125">當從 hello v2.0 端點要求存取權杖要求傳送到：</span><span class="sxs-lookup"><span data-stu-id="af0ad-125">When requesting an access token from hello v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="af0ad-126">hello 回應 hello 下列 JSON 物件的樣子：</span><span class="sxs-lookup"><span data-stu-id="af0ad-126">hello response would look like hello following JSON object:</span></span>

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

<span data-ttu-id="af0ad-127">hello `profile_info` hello 使用者登入 hello 應用程式的顯示名稱、 名字、 姓氏、 電子郵件地址、 識別碼和等等的值包含資訊。</span><span class="sxs-lookup"><span data-stu-id="af0ad-127">hello `profile_info` value contained information about hello user who signed into hello app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="af0ad-128">主要 hello`profile_info`用於權杖快取和顯示用途。</span><span class="sxs-lookup"><span data-stu-id="af0ad-128">Primarily, hello `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="af0ad-129">我們現在要移除 hello`profile_info`值-但別擔心，我們仍提供此資訊 toodevelopers，在稍有不同的地方。</span><span class="sxs-lookup"><span data-stu-id="af0ad-129">We are now removing hello `profile_info` value – but don't worry, we are still providing this information toodevelopers in a slightly different place.</span></span>  <span data-ttu-id="af0ad-130">而不是`profile_info`，現在會傳回 hello v2.0 端點`id_token`中每個權杖的回應：</span><span class="sxs-lookup"><span data-stu-id="af0ad-130">Instead of `profile_info`, hello v2.0 endpoint will now return an `id_token` in each token response:</span></span>

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

<span data-ttu-id="af0ad-131">您可以解碼並剖析 hello id_token tooretrieve hello profile_info 從收到的相同資訊。</span><span class="sxs-lookup"><span data-stu-id="af0ad-131">You may decode and parse hello id_token tooretrieve hello same information that you received from profile_info.</span></span>  <span data-ttu-id="af0ad-132">hello id_token 是 JSON Web Token (JWT)，與 OpenID Connect 所指定的內容。</span><span class="sxs-lookup"><span data-stu-id="af0ad-132">hello id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="af0ad-133">hello 這麼做的程式碼應該非常類似，您只需要 tooextract hello 中間區段 （hello 主體） 的 hello id_token 和 base64 解碼 tooaccess hello JSON 物件內。</span><span class="sxs-lookup"><span data-stu-id="af0ad-133">hello code for doing so should be very similar – you simply need tooextract hello middle segment (hello body) of hello id_token and base64 decode it tooaccess hello JSON object within.</span></span>

<span data-ttu-id="af0ad-134">透過 hello 接下來的兩週，您應撰寫您的應用程式 tooretrieve hello 的使用者資訊從任一 hello`id_token`或`profile_info`; 兩者中較存在。</span><span class="sxs-lookup"><span data-stu-id="af0ad-134">Over hello next two weeks, you should code your app tooretrieve hello user information from either hello `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="af0ad-135">如此一來當 hello 變更時，您的應用程式順暢地處理從 hello 轉換`profile_info`太`id_token`不中斷。</span><span class="sxs-lookup"><span data-stu-id="af0ad-135">That way when hello change is made, your app can seamlessly handle hello transition from `profile_info` too`id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af0ad-136">**您的工作： 請確定您的應用程式不相依於是否存在 hello hello`profile_info`值。**</span><span class="sxs-lookup"><span data-stu-id="af0ad-136">**Your job: Make sure your app does not depend on hello existence of hello `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="af0ad-137">移除 id_token_expires_in</span><span class="sxs-lookup"><span data-stu-id="af0ad-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="af0ad-138">類似太`profile_info`，我們也想要移除 hello`id_token_expires_in`回應中的參數。</span><span class="sxs-lookup"><span data-stu-id="af0ad-138">Similar too`profile_info`, we are also removing hello `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="af0ad-139">Hello v2.0 端點之前，會傳回的值`id_token_expires_in`以及每個 id_token 回應，例如在授權回應：</span><span class="sxs-lookup"><span data-stu-id="af0ad-139">Previously, hello v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="af0ad-140">或權杖回應中：</span><span class="sxs-lookup"><span data-stu-id="af0ad-140">Or in a token response:</span></span>

```
{ 
    "token_type": "Bearer",
    "id_token_expires_in": 3599,
    "scope": "openid",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

<span data-ttu-id="af0ad-141">hello`id_token_expires_in`值會指出 hello hello id_token 仍然為有效的秒數。</span><span class="sxs-lookup"><span data-stu-id="af0ad-141">hello `id_token_expires_in` value would indicate hello number of seconds hello id_token would remain valid for.</span></span>  <span data-ttu-id="af0ad-142">現在，我們會移除 hello`id_token_expires_in`完全值。</span><span class="sxs-lookup"><span data-stu-id="af0ad-142">Now, we are removing hello `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="af0ad-143">相反地，您可以使用 hello OpenID Connect 標準`nbf`和`exp`宣告 id_token tooexamine hello 有效性。</span><span class="sxs-lookup"><span data-stu-id="af0ad-143">Instead, you may use hello OpenID Connect standard `nbf` and `exp` claims tooexamine hello validity of an id_token.</span></span>  <span data-ttu-id="af0ad-144">請參閱 hello [v2.0 權杖參照](active-directory-v2-tokens.md)如需有關這些宣告。</span><span class="sxs-lookup"><span data-stu-id="af0ad-144">See hello [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af0ad-145">**您的工作： 請確定您的應用程式不相依於是否存在 hello hello`id_token_expires_in`值。**</span><span class="sxs-lookup"><span data-stu-id="af0ad-145">**Your job: Make sure your app does not depend on hello existence of hello `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-hello-claims-returned-by-scopeopenid"></a><span data-ttu-id="af0ad-146">變更 hello 宣告範圍傳回 = openid</span><span class="sxs-lookup"><span data-stu-id="af0ad-146">Changing hello claims returned by scope=openid</span></span>
<span data-ttu-id="af0ad-147">這項變更將最重要 – hello 事實上，它會影響使用 hello v2.0 端點幾乎每個應用程式。</span><span class="sxs-lookup"><span data-stu-id="af0ad-147">This change will be hello most significant – in fact, it will affect almost every app that uses hello v2.0 endpoint.</span></span>  <span data-ttu-id="af0ad-148">許多應用程式傳送要求 toohello v2.0 端點使用 hello`openid`範圍，例如：</span><span class="sxs-lookup"><span data-stu-id="af0ad-148">Many applications send requests toohello v2.0 endpoint using hello `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="af0ad-149">今天，當 hello 使用者授與同意，以便 hello`openid`範圍內，您的應用程式接收豐富的 hello 使用者資訊以產生 id_token hello。</span><span class="sxs-lookup"><span data-stu-id="af0ad-149">Today, when hello user grants consent for hello `openid` scope, your app receives a wealth of information about hello user in hello resulting id_token.</span></span>  <span data-ttu-id="af0ad-150">這些宣告可以包含其名稱、慣用的使用者名稱、電子郵件地址、物件識別碼等等。</span><span class="sxs-lookup"><span data-stu-id="af0ad-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="af0ad-151">在此更新中，我們會變更 hello 資訊時，該 hello`openid`範圍可以提供您的應用程式的存取權，toobetter comform 以 hello OpenID Connect 的規格。</span><span class="sxs-lookup"><span data-stu-id="af0ad-151">In this update, we are changing hello information that hello `openid` scope affords your app access to, toobetter comform with hello OpenID Connect specification.</span></span>  <span data-ttu-id="af0ad-152">hello`openid`範圍會只允許應用程式 toosign hello 使用者中，並在 hello 收到 hello 使用者應用程式特定識別項`sub`hello id_token 的宣告。</span><span class="sxs-lookup"><span data-stu-id="af0ad-152">hello `openid` scope will only allow your app toosign hello user in, and receive an app-specific identifier for hello user in hello `sub` claim of hello id_token.</span></span>  <span data-ttu-id="af0ad-153">hello id_token 中的宣告，以只 hello`openid`範圍授與將抹除任何個人識別資訊。</span><span class="sxs-lookup"><span data-stu-id="af0ad-153">hello claims in an id_token with only hello `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="af0ad-154">範例 id_token 宣告為：</span><span class="sxs-lookup"><span data-stu-id="af0ad-154">Example id_token claims are:</span></span>

```
{ 
    "aud": "580e250c-8f26-49d0-bee8-1c078add1609",
    "iss": "https://login.microsoftonline.com/b9410318-09af-49c2-b0c3-653adc1f376e/v2.0 ",
    "iat": 1449520283,
    "nbf": 1449520283,
    "exp": 1449524183,
    "nonce": "12345",
    "sub": "MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q",
    "tid": "b9410318-09af-49c2-b0c3-653adc1f376e",
    "ver": "2.0",
}
```

<span data-ttu-id="af0ad-155">如果您想 tooobtain 個人識別資訊 (PII) 有關 hello 使用者應用程式中，您的應用程式必須 toorequest hello 使用者從其他權限。</span><span class="sxs-lookup"><span data-stu-id="af0ad-155">If you want tooobtain personally identifiable information (PII) about hello user in your app, your app will need toorequest additional permissions from hello user.</span></span>  <span data-ttu-id="af0ad-156">我們採用兩個新領域的支援從 hello OpenID Connect 規格 – hello`email`和`profile`範圍 – 可讓您 toodo 因此。</span><span class="sxs-lookup"><span data-stu-id="af0ad-156">We are introducing support for two new scopes from hello OpenID Connect spec – hello `email` and `profile` scopes – which allow you toodo so.</span></span>

* <span data-ttu-id="af0ad-157">hello`email`範圍是非常簡單，因為它可讓您的應用程式存取 toohello 使用者的主要電子郵件地址，透過 hello `email` hello id_token 中宣告。</span><span class="sxs-lookup"><span data-stu-id="af0ad-157">hello `email` scope is very straightforward – it allows your app access toohello user's primary email address via hello `email` claim in hello id_token.</span></span>  <span data-ttu-id="af0ad-158">請注意該 hello`email`宣告不一定會出現在 id_tokens – 它將只會包含如果有的話，在 hello 使用者設定檔。</span><span class="sxs-lookup"><span data-stu-id="af0ad-158">Note that hello `email` claim will not always be present in id_tokens – it will only be included if available in hello user's profile.</span></span>
* <span data-ttu-id="af0ad-159">hello`profile`範圍可以提供您的應用程式存取 tooall hello 使用者 – 其名稱、 慣用的使用者名稱，其他基本資訊的物件識別碼，等等。</span><span class="sxs-lookup"><span data-stu-id="af0ad-159">hello `profile` scope affords your app access tooall other basic information about hello user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="af0ad-160">這可讓您 toocode 您的應用程式，以最少洩漏的方式 – 您可以要求 hello 使用者只要 hello 組的應用程式需要 toodo 其工作的資訊。</span><span class="sxs-lookup"><span data-stu-id="af0ad-160">This allows you toocode your app in a minimal-disclosure fashion – you can ask hello user for just hello set of information that your app requires toodo its job.</span></span>  <span data-ttu-id="af0ad-161">如果您想取得 hello 目前接收您的應用程式的使用者資訊的一組完整的 toocontinue，授權要求中應包含所有的三個範圍：</span><span class="sxs-lookup"><span data-stu-id="af0ad-161">If you want toocontinue getting hello full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="af0ad-162">您的應用程式可以開始傳送嗨`email`和`profile`立即範圍和 hello v2.0 端點會將接受這些兩個範圍，並開始視要求來自使用者的權限。</span><span class="sxs-lookup"><span data-stu-id="af0ad-162">Your app can begin sending hello `email` and `profile` scopes immediately, and hello v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="af0ad-163">但是 hello 變更中的 hello 的 hello 解譯`openid`範圍不會生效幾週。</span><span class="sxs-lookup"><span data-stu-id="af0ad-163">However, hello change in hello interpretation of hello `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af0ad-164">**您的工作： 新增 hello`profile`和`email`範圍，如果您的應用程式需要 hello 使用者的相關資訊。**</span><span class="sxs-lookup"><span data-stu-id="af0ad-164">**Your job: Add hello `profile` and `email` scopes if your app requires information about hello user.**</span></span>  <span data-ttu-id="af0ad-165">請注意，ADAL 預設會在要求中同時包含這些權限。</span><span class="sxs-lookup"><span data-stu-id="af0ad-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-hello-issuer-trailing-slash"></a><span data-ttu-id="af0ad-166">正在移除 hello 簽發者結尾斜線。</span><span class="sxs-lookup"><span data-stu-id="af0ad-166">Removing hello issuer trailing slash.</span></span>
<span data-ttu-id="af0ad-167">Hello 簽發者值，這個值會顯示在權杖中的 hello v2.0 端點之前，花費了 hello 表單</span><span class="sxs-lookup"><span data-stu-id="af0ad-167">Previously, hello issuer value that appears in tokens from hello v2.0 endpoint took hello form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="af0ad-168">其中 hello guid 為 hello 發行 hello 語彙基元的 hello Azure AD 租用戶的 tenantId。</span><span class="sxs-lookup"><span data-stu-id="af0ad-168">Where hello guid was hello tenantId of hello Azure AD tenant which issued hello token.</span></span>  <span data-ttu-id="af0ad-169">這些變更，變成 hello 簽發者值</span><span class="sxs-lookup"><span data-stu-id="af0ad-169">With these changes, hello issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="af0ad-170">在這兩個語彙基元和 hello OpenID Connect 探索文件中。</span><span class="sxs-lookup"><span data-stu-id="af0ad-170">in both tokens and in hello OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af0ad-171">**您的工作： 請確定您的應用程式簽發者驗證期間會接受 hello 簽發者值與並沒有尾端斜線。**</span><span class="sxs-lookup"><span data-stu-id="af0ad-171">**Your job: Make sure your app accepts hello issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="af0ad-172">為何變更？</span><span class="sxs-lookup"><span data-stu-id="af0ad-172">Why change?</span></span>
<span data-ttu-id="af0ad-173">hello 來介紹這些變更的主要動機是 toobe 與 hello OpenID Connect 標準規格相容。</span><span class="sxs-lookup"><span data-stu-id="af0ad-173">hello primary motivation for introducing these changes is toobe compliant with hello OpenID Connect standard specification.</span></span>  <span data-ttu-id="af0ad-174">透過 OpenID Connect 標準，我們希望 toominimize 差異整合 Microsoft 識別服務與 hello 產業中的其他身分識別服務。</span><span class="sxs-lookup"><span data-stu-id="af0ad-174">By being OpenID Connect compliant, we hope toominimize differences between integrating with Microsoft identity services and with other identity services in hello industry.</span></span>  <span data-ttu-id="af0ad-175">我們想要 tooenable 開發人員 toouse 他們最愛的開放原始碼的驗證程式庫而不需要 tooalter hello 文件庫 tooaccommodate Microsoft 差異。</span><span class="sxs-lookup"><span data-stu-id="af0ad-175">We want tooenable developers toouse their favorite open source authentication libraries without having tooalter hello libraries tooaccommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="af0ad-176">您該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="af0ad-176">What can you do?</span></span>
<span data-ttu-id="af0ad-177">目前，您可以開始進行所有的 hello 變更上面所述。</span><span class="sxs-lookup"><span data-stu-id="af0ad-177">As of today, you can begin making all of hello changes described above.</span></span>  <span data-ttu-id="af0ad-178">您應該立即：</span><span class="sxs-lookup"><span data-stu-id="af0ad-178">You should immediately:</span></span>

1. <span data-ttu-id="af0ad-179">**移除任何相依性 hello `x5t` header 參數。**</span><span class="sxs-lookup"><span data-stu-id="af0ad-179">**Remove any dependencies on hello `x5t` header parameter.**</span></span>
2. <span data-ttu-id="af0ad-180">**正常處理從 hello 轉換`profile_info`太`id_token`權杖回應中。**</span><span class="sxs-lookup"><span data-stu-id="af0ad-180">**Gracefully handle hello transition from `profile_info` too`id_token` in token responses.**</span></span>
3. <span data-ttu-id="af0ad-181">**移除任何相依性 hello`id_token_expires_in`回應參數。**</span><span class="sxs-lookup"><span data-stu-id="af0ad-181">**Remove any dependencies on hello `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="af0ad-182">**新增 hello`profile`和`email`範圍 tooyour 應用程式如果您的應用程式需要基本使用者的資訊。**</span><span class="sxs-lookup"><span data-stu-id="af0ad-182">**Add hello `profile` and `email` scopes tooyour app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="af0ad-183">**在權杖中接受包含或不含結尾斜線的簽發者值。**</span><span class="sxs-lookup"><span data-stu-id="af0ad-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="af0ad-184">我們[v2.0 通訊協定文件](active-directory-v2-protocols.md)已經過更新的 tooreflect 這些變更，因此您可以使用它做為參考，幫助您更新您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="af0ad-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated tooreflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="af0ad-185">如果您在 hello hello 變更範圍上有任何進一步的問題，請隨時可用 tooreach out toous 在 Twitter 上@AzureAD。</span><span class="sxs-lookup"><span data-stu-id="af0ad-185">If you have any further questions on hello scope of hello changes, please feel free tooreach out toous on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="af0ad-186">通訊協定變更發生頻率為何？</span><span class="sxs-lookup"><span data-stu-id="af0ad-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="af0ad-187">我們未預期任何進一步重大變更 toohello 驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="af0ad-187">We do not foresee any further breaking changes toohello authentication protocols.</span></span>  <span data-ttu-id="af0ad-188">我們會刻意結合在一起到一個發行這些變更，所以您不需要 toogo 透過這種類型的更新程序再次隨時推出。</span><span class="sxs-lookup"><span data-stu-id="af0ad-188">We are intentionally bundling these changes into one release so that you won\`t have toogo through this type of update process again any time soon.</span></span>  <span data-ttu-id="af0ad-189">當然，我們會繼續 tooadd 功能 toohello 交集 v2.0 驗證服務，您可以利用，但這些變更應該附加與中斷現有的程式碼。</span><span class="sxs-lookup"><span data-stu-id="af0ad-189">Of course, we will continue tooadd features toohello converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="af0ad-190">最後，我們希望 toosay 感謝您試用事項 hello 預覽期間。</span><span class="sxs-lookup"><span data-stu-id="af0ad-190">Lastly, we would like toosay thank you for trying things out during hello preview period.</span></span>  <span data-ttu-id="af0ad-191">hello 深入資訊和體驗的我們早期採用者一兩為止，而且我們希望您的意見與想法，您將會繼續 tooshare。</span><span class="sxs-lookup"><span data-stu-id="af0ad-191">hello insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue tooshare your opinions and ideas.</span></span>

<span data-ttu-id="af0ad-192">祝各位編碼程式愉快！</span><span class="sxs-lookup"><span data-stu-id="af0ad-192">Happy coding!</span></span>

<span data-ttu-id="af0ad-193">Microsoft 身分識別除法 hello</span><span class="sxs-lookup"><span data-stu-id="af0ad-193">hello Microsoft Identity Division</span></span>

