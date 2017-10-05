---
title: "變更為 Azure AD v2.0 端點 | Microsoft Docs"
description: "對應用程式模型 v2.0 公用預覽通訊協定所進行的變更的描述。"
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
ms.openlocfilehash: ae73833a68db14804dc40eaf07ff7d3effaa9052
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="important-updates-to-the-v20-authentication-protocols"></a><span data-ttu-id="b004a-103">v2.0 驗證通訊協定的重要更新</span><span class="sxs-lookup"><span data-stu-id="b004a-103">Important Updates to the v2.0 Authentication Protocols</span></span>
<span data-ttu-id="b004a-104">開發人員請注意！</span><span class="sxs-lookup"><span data-stu-id="b004a-104">Attention developers!</span></span> <span data-ttu-id="b004a-105">在接下來兩週，我們會對 v2.0 驗證通訊協定進行一些更新，這些更新對於您在我們的預覽期間撰寫的任何應用程式可能是重大變更。</span><span class="sxs-lookup"><span data-stu-id="b004a-105">Over the next two weeks, we will be making a few updates to our v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="b004a-106">那些人會受到影響？</span><span class="sxs-lookup"><span data-stu-id="b004a-106">Who does this affect?</span></span>
<span data-ttu-id="b004a-107">任何已撰寫使用 v2.0 整合驗證端點的任何應用程式，</span><span class="sxs-lookup"><span data-stu-id="b004a-107">Any apps that have been written to use the v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="b004a-108">更多關於 v2.0 端點的詳細資訊可以在 [這裡](active-directory-appmodel-v2-overview.md)找到。</span><span class="sxs-lookup"><span data-stu-id="b004a-108">More information on the v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="b004a-109">如果您已經藉由直接編碼至 v2.0 通訊協定，使用 v2.0 端點來建置應用程式，使用我們的任何 OpenID Connect 或 OAuth Web 中繼軟體，或使用其他協力廠商程式庫來執行驗證，您應該準備好測試您的專案，並且視需要進行變更。</span><span class="sxs-lookup"><span data-stu-id="b004a-109">If you have built an app using the v2.0 endpoint by coding directly to the v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries to perform authentication, you should be prepared to test your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="b004a-110">那些人不會受到影響？</span><span class="sxs-lookup"><span data-stu-id="b004a-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="b004a-111">任何已根據保護 Azure AD 驗證端點所撰寫的任何應用程式，</span><span class="sxs-lookup"><span data-stu-id="b004a-111">Any apps that have been written against the production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="b004a-112">此通訊協定一定都是如此，並且不會發生任何變更。</span><span class="sxs-lookup"><span data-stu-id="b004a-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="b004a-113">此外，如果您的應用程式 **只** 使用我們的 ADAL 程式庫來執行驗證，您不必變更任何項目。</span><span class="sxs-lookup"><span data-stu-id="b004a-113">Furthermore, if your app **only** uses our ADAL library to perform authentication, you won\`t have to change anything.</span></span>  <span data-ttu-id="b004a-114">ADAL 已防護您的應用程式免於變更。</span><span class="sxs-lookup"><span data-stu-id="b004a-114">ADAL has shielded your app from the changes.</span></span>  

## <a name="what-are-the-changes"></a><span data-ttu-id="b004a-115">所做的變更有哪些？</span><span class="sxs-lookup"><span data-stu-id="b004a-115">What are the changes?</span></span>
### <a name="removing-the-x5t-value-from-jwt-headers"></a><span data-ttu-id="b004a-116">從 JWT 標頭移除 x5t 值</span><span class="sxs-lookup"><span data-stu-id="b004a-116">Removing the x5t value from JWT headers</span></span>
<span data-ttu-id="b004a-117">V2.0 端點大量使用 JWT 權杖，其中包含標頭參數區段與權杖的相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="b004a-117">The v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about the token.</span></span>  <span data-ttu-id="b004a-118">如果您解碼其中一個目前 JWT 的標頭，您會發現類似以下的情形：</span><span class="sxs-lookup"><span data-stu-id="b004a-118">If you decode the header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="b004a-119">「x5t」和「kid」屬性都會識別從 OpenID Connect 中繼資料端點擷取，應該用於驗證權杖簽章的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="b004a-119">Where both the "x5t" and "kid" properties identify the public key that should be used to validate the token\`s signature, as retrieved from the OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="b004a-120">我們在這裡進行的變更是要移除「x5t」屬性。</span><span class="sxs-lookup"><span data-stu-id="b004a-120">The change we are making here is to remove the "x5t" property.</span></span>  <span data-ttu-id="b004a-121">您可以繼續使用相同的機制來驗證權杖，但應該只依賴「kid」屬性來擷取正確的公用金鑰，如 OpenID Connect 通訊協定中所指定。</span><span class="sxs-lookup"><span data-stu-id="b004a-121">You may continue to use the same mechanisms to validate tokens, but should rely only on the "kid" property to retrieve the correct public key, as specified in the OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b004a-122">**您的作業：請確定您的應用程式不依賴 x5t 值是否存在。**</span><span class="sxs-lookup"><span data-stu-id="b004a-122">**Your job: Make sure your app does not depend on the existence of the x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="b004a-123">移除 profile_info</span><span class="sxs-lookup"><span data-stu-id="b004a-123">Removing profile_info</span></span>
<span data-ttu-id="b004a-124">先前，v2.0 端點在稱為 `profile_info` 的權杖回應中已傳回 base64 編碼的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="b004a-124">Previously, the v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="b004a-125">藉由傳送要求至下列項目，從 v2.0 端點要求存取權杖時：</span><span class="sxs-lookup"><span data-stu-id="b004a-125">When requesting an access token from the v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="b004a-126">回應看起來類似下列 JSON 物件：</span><span class="sxs-lookup"><span data-stu-id="b004a-126">The response would look like the following JSON object:</span></span>

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

<span data-ttu-id="b004a-127">包含 `profile_info` 值的資訊是關於登入應用程式的使用者 - 其顯示名稱、名字、姓氏、電子郵件地址、 識別碼等等。</span><span class="sxs-lookup"><span data-stu-id="b004a-127">The `profile_info` value contained information about the user who signed into the app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="b004a-128">`profile_info` 主要是用於權杖快取和顯示用途。</span><span class="sxs-lookup"><span data-stu-id="b004a-128">Primarily, the `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="b004a-129">我們現在移除 `profile_info` 值 - 不過別擔心，我們仍然會在稍微不同的地方為開發人員提供這項資訊。</span><span class="sxs-lookup"><span data-stu-id="b004a-129">We are now removing the `profile_info` value – but don't worry, we are still providing this information to developers in a slightly different place.</span></span>  <span data-ttu-id="b004a-130">不是 `profile_info`，v2.0 端點現在會在每個權杖回應中傳回 `id_token`：</span><span class="sxs-lookup"><span data-stu-id="b004a-130">Instead of `profile_info`, the v2.0 endpoint will now return an `id_token` in each token response:</span></span>

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

<span data-ttu-id="b004a-131">您可以解碼並剖析的 id_token 以擷取您從 profile_info 所收到的相同資訊。</span><span class="sxs-lookup"><span data-stu-id="b004a-131">You may decode and parse the id_token to retrieve the same information that you received from profile_info.</span></span>  <span data-ttu-id="b004a-132">Id_token 是 JSON Web 權杖 (JWT)，其內容由 OpenID Connect 所指定。</span><span class="sxs-lookup"><span data-stu-id="b004a-132">The id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="b004a-133">要執行這項操作的程式碼應該非常類似 – 您只需要擷取 id_token 的中間區段 (主體)，而且 base64 會將其解碼以在 JSON 物件中存取。</span><span class="sxs-lookup"><span data-stu-id="b004a-133">The code for doing so should be very similar – you simply need to extract the middle segment (the body) of the id_token and base64 decode it to access the JSON object within.</span></span>

<span data-ttu-id="b004a-134">兩週過後，您應該撰寫程式碼以從 `id_token` 或 `profile_info` (存在的其中一個) 擷取使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="b004a-134">Over the next two weeks, you should code your app to retrieve the user information from either the `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="b004a-135">如此一來，當變更時，您的應用程式可以順暢地處理從 `profile_info` 至 `id_token` 的轉換而不會中斷。</span><span class="sxs-lookup"><span data-stu-id="b004a-135">That way when the change is made, your app can seamlessly handle the transition from `profile_info` to `id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b004a-136">**您的作業：請確定您的應用程式不倚賴 `profile_info` 值是否存在。**</span><span class="sxs-lookup"><span data-stu-id="b004a-136">**Your job: Make sure your app does not depend on the existence of the `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="b004a-137">移除 id_token_expires_in</span><span class="sxs-lookup"><span data-stu-id="b004a-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="b004a-138">類似於 `profile_info`，我們同時也從回應中移除 `id_token_expires_in` 參數。</span><span class="sxs-lookup"><span data-stu-id="b004a-138">Similar to `profile_info`, we are also removing the `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="b004a-139">先前，v2.0 端點會傳回 `id_token_expires_in` 的值以及每個 id_token 回應，例如在授權回應中：</span><span class="sxs-lookup"><span data-stu-id="b004a-139">Previously, the v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="b004a-140">或權杖回應中：</span><span class="sxs-lookup"><span data-stu-id="b004a-140">Or in a token response:</span></span>

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

<span data-ttu-id="b004a-141">`id_token_expires_in` 值會指出 id_token 保持有效的秒數。</span><span class="sxs-lookup"><span data-stu-id="b004a-141">The `id_token_expires_in` value would indicate the number of seconds the id_token would remain valid for.</span></span>  <span data-ttu-id="b004a-142">現在，我們完全移除 `id_token_expires_in` 值。</span><span class="sxs-lookup"><span data-stu-id="b004a-142">Now, we are removing the `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="b004a-143">相反地，您可以使用 OpenID Connect 標準 `nbf` 和 `exp` 宣告來檢查 id_token 的有效性。</span><span class="sxs-lookup"><span data-stu-id="b004a-143">Instead, you may use the OpenID Connect standard `nbf` and `exp` claims to examine the validity of an id_token.</span></span>  <span data-ttu-id="b004a-144">請參閱 [v2.0 權杖參考](active-directory-v2-tokens.md) 以取得這些宣告的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b004a-144">See the [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b004a-145">**您的作業：請確定您的應用程式不倚賴 `id_token_expires_in` 值是否存在。**</span><span class="sxs-lookup"><span data-stu-id="b004a-145">**Your job: Make sure your app does not depend on the existence of the `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-the-claims-returned-by-scopeopenid"></a><span data-ttu-id="b004a-146">變更 scope=openid 傳回的宣告</span><span class="sxs-lookup"><span data-stu-id="b004a-146">Changing the claims returned by scope=openid</span></span>
<span data-ttu-id="b004a-147">這項變更將是最重要的 – 事實上，它將會影響使用 v2.0 端點的幾乎每個應用程式。</span><span class="sxs-lookup"><span data-stu-id="b004a-147">This change will be the most significant – in fact, it will affect almost every app that uses the v2.0 endpoint.</span></span>  <span data-ttu-id="b004a-148">許多應用程式使用 `openid` 範圍將要求傳送至 v2.0 端點，例如：</span><span class="sxs-lookup"><span data-stu-id="b004a-148">Many applications send requests to the v2.0 endpoint using the `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="b004a-149">今天，當使用者同意 `openid` 範圍，您的應用程式會在產生的 id_token 中收到豐富的使用者相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b004a-149">Today, when the user grants consent for the `openid` scope, your app receives a wealth of information about the user in the resulting id_token.</span></span>  <span data-ttu-id="b004a-150">這些宣告可以包含其名稱、慣用的使用者名稱、電子郵件地址、物件識別碼等等。</span><span class="sxs-lookup"><span data-stu-id="b004a-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="b004a-151">在此更新中，我們會變更 `openid` 範圍給予您的應用程式存取權的資訊，使其更符合 OpenID Connect 規格。</span><span class="sxs-lookup"><span data-stu-id="b004a-151">In this update, we are changing the information that the `openid` scope affords your app access to, to better comform with the OpenID Connect specification.</span></span>  <span data-ttu-id="b004a-152">`openid` 範圍只允許您的應用程式將使用者登入，在 id_token 的 `sub` 宣告中接收應用程式特定識別碼。</span><span class="sxs-lookup"><span data-stu-id="b004a-152">The `openid` scope will only allow your app to sign the user in, and receive an app-specific identifier for the user in the `sub` claim of the id_token.</span></span>  <span data-ttu-id="b004a-153">只被授與 `openid` 範圍的 id_token 中的宣告會缺乏任何個人識別資訊。</span><span class="sxs-lookup"><span data-stu-id="b004a-153">The claims in an id_token with only the `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="b004a-154">範例 id_token 宣告為：</span><span class="sxs-lookup"><span data-stu-id="b004a-154">Example id_token claims are:</span></span>

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

<span data-ttu-id="b004a-155">如果您想要取得有關您的應用程式中的使用者的個人識別資訊 (PII)，您的應用程式必須向使用者要求其他權限。</span><span class="sxs-lookup"><span data-stu-id="b004a-155">If you want to obtain personally identifiable information (PII) about the user in your app, your app will need to request additional permissions from the user.</span></span>  <span data-ttu-id="b004a-156">我們從 OpenID Connect 規格引進兩個新領域的支援 – `email` 和 `profile` 範圍 – 可讓您執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="b004a-156">We are introducing support for two new scopes from the OpenID Connect spec – the `email` and `profile` scopes – which allow you to do so.</span></span>

* <span data-ttu-id="b004a-157">`email` 範圍非常簡單，它可讓您的應用程式透過 id_token 中的 `email` 宣告存取使用者的主要電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="b004a-157">The `email` scope is very straightforward – it allows your app access to the user's primary email address via the `email` claim in the id_token.</span></span>  <span data-ttu-id="b004a-158">請注意，`email` 宣告不一定會出現在 id_tokens 中 – 只有在使用者的設定檔中可用時才會包含。</span><span class="sxs-lookup"><span data-stu-id="b004a-158">Note that the `email` claim will not always be present in id_tokens – it will only be included if available in the user's profile.</span></span>
* <span data-ttu-id="b004a-159">`profile` 範圍可以讓您的應用程式存取使用者的所有其他基本資訊 – 其名稱、慣用的使用者名稱、物件識別碼等等。</span><span class="sxs-lookup"><span data-stu-id="b004a-159">The `profile` scope affords your app access to all other basic information about the user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="b004a-160">這可讓您以最低洩漏的方式編碼應用程式 – 您可以只向使用者要求應用程式執行其作業所需的資訊集。</span><span class="sxs-lookup"><span data-stu-id="b004a-160">This allows you to code your app in a minimal-disclosure fashion – you can ask the user for just the set of information that your app requires to do its job.</span></span>  <span data-ttu-id="b004a-161">如果您想要繼續取得您的應用程式目前接收的使用者資訊的完整集合，您應該在授權要求中包含所有三個範圍：</span><span class="sxs-lookup"><span data-stu-id="b004a-161">If you want to continue getting the full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="b004a-162">您的應用程式可以立即開始傳送 `email` 和 `profile`，v2.0 端點會接受這兩個範圍，並且視需要開始向使用者要求權限。</span><span class="sxs-lookup"><span data-stu-id="b004a-162">Your app can begin sending the `email` and `profile` scopes immediately, and the v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="b004a-163">不過， `openid` 範圍的轉譯中的變更幾週之後才會生效。</span><span class="sxs-lookup"><span data-stu-id="b004a-163">However, the change in the interpretation of the `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b004a-164">**您的作業：如果您的應用程式需要使用者的相關資訊，請新增 `profile` 和 `email` 範圍。**</span><span class="sxs-lookup"><span data-stu-id="b004a-164">**Your job: Add the `profile` and `email` scopes if your app requires information about the user.**</span></span>  <span data-ttu-id="b004a-165">請注意，ADAL 預設會在要求中同時包含這些權限。</span><span class="sxs-lookup"><span data-stu-id="b004a-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-the-issuer-trailing-slash"></a><span data-ttu-id="b004a-166">移除簽發者結尾斜線。</span><span class="sxs-lookup"><span data-stu-id="b004a-166">Removing the issuer trailing slash.</span></span>
<span data-ttu-id="b004a-167">先前，v2.0 端點的權杖中的簽發者值採用此格式</span><span class="sxs-lookup"><span data-stu-id="b004a-167">Previously, the issuer value that appears in tokens from the v2.0 endpoint took the form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="b004a-168">其中 guid 是發行權杖的 Azure AD 租用戶的 tenantId。</span><span class="sxs-lookup"><span data-stu-id="b004a-168">Where the guid was the tenantId of the Azure AD tenant which issued the token.</span></span>  <span data-ttu-id="b004a-169">進行這些變更之後，簽發者值會改變</span><span class="sxs-lookup"><span data-stu-id="b004a-169">With these changes, the issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="b004a-170">在這兩個權杖和 OpenID Connect 探索文件中。</span><span class="sxs-lookup"><span data-stu-id="b004a-170">in both tokens and in the OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b004a-171">**您的作業：確定您的應用程式在簽發者驗證期間接受包含或不含結尾斜線的簽發者值。**</span><span class="sxs-lookup"><span data-stu-id="b004a-171">**Your job: Make sure your app accepts the issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="b004a-172">為何變更？</span><span class="sxs-lookup"><span data-stu-id="b004a-172">Why change?</span></span>
<span data-ttu-id="b004a-173">導入這些變更的主要動機是要與 OpenID Connect 標準規格相容。</span><span class="sxs-lookup"><span data-stu-id="b004a-173">The primary motivation for introducing these changes is to be compliant with the OpenID Connect standard specification.</span></span>  <span data-ttu-id="b004a-174">與 OpenID Connect 相容，我們希望將與 Microsoft 識別服務以及業界其他識別服務整合的差異降到最低。</span><span class="sxs-lookup"><span data-stu-id="b004a-174">By being OpenID Connect compliant, we hope to minimize differences between integrating with Microsoft identity services and with other identity services in the industry.</span></span>  <span data-ttu-id="b004a-175">我們想要讓開發人員使用他們最愛的開放原始碼驗證程式庫而不必變更程式庫，以配合 Microsoft 的差異。</span><span class="sxs-lookup"><span data-stu-id="b004a-175">We want to enable developers to use their favorite open source authentication libraries without having to alter the libraries to accommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="b004a-176">您該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="b004a-176">What can you do?</span></span>
<span data-ttu-id="b004a-177">目前，您可以開始進行上述的所有變更。</span><span class="sxs-lookup"><span data-stu-id="b004a-177">As of today, you can begin making all of the changes described above.</span></span>  <span data-ttu-id="b004a-178">您應該立即：</span><span class="sxs-lookup"><span data-stu-id="b004a-178">You should immediately:</span></span>

1. <span data-ttu-id="b004a-179">**移除 `x5t` 標頭參數的任何相依性。**</span><span class="sxs-lookup"><span data-stu-id="b004a-179">**Remove any dependencies on the `x5t` header parameter.**</span></span>
2. <span data-ttu-id="b004a-180">**正常處理權杖回應中從 `profile_info` 至 `id_token` 的轉換。**</span><span class="sxs-lookup"><span data-stu-id="b004a-180">**Gracefully handle the transition from `profile_info` to `id_token` in token responses.**</span></span>
3. <span data-ttu-id="b004a-181">**移除 `id_token_expires_in` 回應參數的任何相依性。**</span><span class="sxs-lookup"><span data-stu-id="b004a-181">**Remove any dependencies on the `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="b004a-182">**如果您的應用程式需要基本使用者資訊，則將 `profile` 和 `email` 範圍新增至您的應用程式。**</span><span class="sxs-lookup"><span data-stu-id="b004a-182">**Add the `profile` and `email` scopes to your app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="b004a-183">**在權杖中接受包含或不含結尾斜線的簽發者值。**</span><span class="sxs-lookup"><span data-stu-id="b004a-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="b004a-184">我們的 [v2.0 通訊協定文件](active-directory-v2-protocols.md) 已更新以反映這些變更，因此您可能會使用它做為協助更新程式碼的參考。</span><span class="sxs-lookup"><span data-stu-id="b004a-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated to reflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="b004a-185">如果您對於變更的範圍有任何進一步的問題，歡迎在 Twitter 與我們連絡：@AzureAD。</span><span class="sxs-lookup"><span data-stu-id="b004a-185">If you have any further questions on the scope of the changes, please feel free to reach out to us on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="b004a-186">通訊協定變更發生頻率為何？</span><span class="sxs-lookup"><span data-stu-id="b004a-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="b004a-187">我們無法預見驗證通訊協定的任何進一步重大變更。</span><span class="sxs-lookup"><span data-stu-id="b004a-187">We do not foresee any further breaking changes to the authentication protocols.</span></span>  <span data-ttu-id="b004a-188">我們刻意將這些變更統合至一個發行版本，這樣，您就不需要馬上再經歷這種類型的更新程序。</span><span class="sxs-lookup"><span data-stu-id="b004a-188">We are intentionally bundling these changes into one release so that you won\`t have to go through this type of update process again any time soon.</span></span>  <span data-ttu-id="b004a-189">當然，我們將會繼續將功能新增至您可以充分利用的 v2.0 驗證服務，但是這些變更應該只是附加的，而不是中斷現有的程式碼。</span><span class="sxs-lookup"><span data-stu-id="b004a-189">Of course, we will continue to add features to the converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="b004a-190">最後，感謝您在預覽期間試用功能。</span><span class="sxs-lookup"><span data-stu-id="b004a-190">Lastly, we would like to say thank you for trying things out during the preview period.</span></span>  <span data-ttu-id="b004a-191">至此，我們早期採用者的深入資訊和體驗非常寶貴，而且我們希望您將會繼續共用您的意見與想法。</span><span class="sxs-lookup"><span data-stu-id="b004a-191">The insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue to share your opinions and ideas.</span></span>

<span data-ttu-id="b004a-192">祝各位編碼程式愉快！</span><span class="sxs-lookup"><span data-stu-id="b004a-192">Happy coding!</span></span>

<span data-ttu-id="b004a-193">Microsoft 身分識別部門</span><span class="sxs-lookup"><span data-stu-id="b004a-193">The Microsoft Identity Division</span></span>

