---
title: "Active Directory aaaAzure v2.0 範圍、 權限和同意 |Microsoft 文件"
description: "在 Azure AD hello v2.0 端點使用，包括領域、 權限和同意授權的描述。"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 8f98cbf0-a71d-4e34-babf-e644ad9ff423
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 5721d368c435868bfb4ae91cff7fbb9bc4a79b66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scopes-permissions-and-consent-in-hello-azure-active-directory-v20-endpoint"></a><span data-ttu-id="010c5-103">範圍、 權限，以及在 hello Azure Active Directory v2.0 端點中同意</span><span class="sxs-lookup"><span data-stu-id="010c5-103">Scopes, permissions, and consent in hello Azure Active Directory v2.0 endpoint</span></span>
<span data-ttu-id="010c5-104">與 Azure Active Directory (Azure AD) 整合的應用程式會遵循一種授權模型，可讓使用者控制應用程式存取他們資料的方式。</span><span class="sxs-lookup"><span data-stu-id="010c5-104">Apps that integrate with Azure Active Directory (Azure AD) follow an authorization model that gives users control over how an app can access their data.</span></span> <span data-ttu-id="010c5-105">已更新 hello v2.0 實作 hello 的授權模型，並在應用程式必須與 Azure AD 互動的方式變更。</span><span class="sxs-lookup"><span data-stu-id="010c5-105">hello v2.0 implementation of hello authorization model has been updated, and it changes how an app must interact with Azure AD.</span></span> <span data-ttu-id="010c5-106">本文涵蓋 hello 基本概念，這個授權模型，包括領域、 權限和同意。</span><span class="sxs-lookup"><span data-stu-id="010c5-106">This article covers hello basic concepts of this authorization model, including scopes, permissions, and consent.</span></span>

> [!NOTE]
> <span data-ttu-id="010c5-107">hello v2.0 端點不支援所有的 Azure Active Directory 的案例和功能。</span><span class="sxs-lookup"><span data-stu-id="010c5-107">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span> <span data-ttu-id="010c5-108">toodetermine 是否應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="010c5-108">toodetermine whether you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

## <a name="scopes-and-permissions"></a><span data-ttu-id="010c5-109">範圍和權限</span><span class="sxs-lookup"><span data-stu-id="010c5-109">Scopes and permissions</span></span>
<span data-ttu-id="010c5-110">Azure AD 實作 hello [OAuth 2.0](active-directory-v2-protocols.md)授權通訊協定。</span><span class="sxs-lookup"><span data-stu-id="010c5-110">Azure AD implements hello [OAuth 2.0](active-directory-v2-protocols.md) authorization protocol.</span></span> <span data-ttu-id="010c5-111">OAuth 2.0 是一種可讓協力廠商應用程式代表使用者存取 Web 主控資源的方法。</span><span class="sxs-lookup"><span data-stu-id="010c5-111">OAuth 2.0 is a method through which a third-party app can access web-hosted resources on behalf of a user.</span></span> <span data-ttu-id="010c5-112">任何與 Azure AD 整合的 Web 主控資源都具有資源識別碼 (或稱「應用程式識別碼 URI」)。</span><span class="sxs-lookup"><span data-stu-id="010c5-112">Any web-hosted resource that integrates with Azure AD has a resource identifier, or *Application ID URI*.</span></span> <span data-ttu-id="010c5-113">例如，Microsoft 的 Web 主控資源包括：</span><span class="sxs-lookup"><span data-stu-id="010c5-113">For example, some of Microsoft's web-hosted resources include:</span></span>

* <span data-ttu-id="010c5-114">hello Office 365 整合 Mail API:`https://outlook.office.com`</span><span class="sxs-lookup"><span data-stu-id="010c5-114">hello Office 365 Unified Mail API: `https://outlook.office.com`</span></span>
* <span data-ttu-id="010c5-115">hello Azure AD Graph API:`https://graph.windows.net`</span><span class="sxs-lookup"><span data-stu-id="010c5-115">hello Azure AD Graph API: `https://graph.windows.net`</span></span>
* <span data-ttu-id="010c5-116">Microsoft Graph：`https://graph.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="010c5-116">Microsoft Graph: `https://graph.microsoft.com`</span></span>

<span data-ttu-id="010c5-117">hello 也適用於已整合 Azure AD 與任何第三方資源。</span><span class="sxs-lookup"><span data-stu-id="010c5-117">hello same is true for any third-party resources that have integrated with Azure AD.</span></span> <span data-ttu-id="010c5-118">下列任何資源也可以定義一組權限可以使用的 toodivide hello 功能，該資源為較小區塊。</span><span class="sxs-lookup"><span data-stu-id="010c5-118">Any of these resources also can define a set of permissions that can be used toodivide hello functionality of that resource into smaller chunks.</span></span> <span data-ttu-id="010c5-119">例如， [Microsoft Graph](https://graph.microsoft.io)已定義的權限 toodo hello 下列工作，和其他項目：</span><span class="sxs-lookup"><span data-stu-id="010c5-119">As an example, [Microsoft Graph](https://graph.microsoft.io) has defined permissions toodo hello following tasks, among others:</span></span>

* <span data-ttu-id="010c5-120">讀取使用者的行事曆</span><span class="sxs-lookup"><span data-stu-id="010c5-120">Read a user's calendar</span></span>
* <span data-ttu-id="010c5-121">寫入 tooa 使用者的行事曆</span><span class="sxs-lookup"><span data-stu-id="010c5-121">Write tooa user's calendar</span></span>
* <span data-ttu-id="010c5-122">以使用者身分傳送郵件</span><span class="sxs-lookup"><span data-stu-id="010c5-122">Send mail as a user</span></span>

<span data-ttu-id="010c5-123">藉由定義這些類型的權限，hello 資源都有其資料和 hello 資料會公開方式更細微的控制。</span><span class="sxs-lookup"><span data-stu-id="010c5-123">By defining these types of permissions, hello resource has fine-grained control over its data and how hello data is exposed.</span></span> <span data-ttu-id="010c5-124">協力廠商應用程式可以向應用程式使用者要求這些權限。</span><span class="sxs-lookup"><span data-stu-id="010c5-124">A third-party app can request these permissions from an app user.</span></span> <span data-ttu-id="010c5-125">hello 應用程式使用者必須核准 hello 權限，才能代表 hello 使用者可採取動作 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="010c5-125">hello app user must approve hello permissions before hello app can act on hello user's behalf.</span></span> <span data-ttu-id="010c5-126">切割成較小的權限集的 hello 資源的功能，由協力廠商應用程式可以是內建的 toorequest 只有 hello 特定權限所需 tooperform 其函式。</span><span class="sxs-lookup"><span data-stu-id="010c5-126">By chunking hello resource's functionality into smaller permission sets, third-party apps can be built toorequest only hello specific permissions that they need tooperform their function.</span></span> <span data-ttu-id="010c5-127">應用程式使用者可以知道應用程式將使用的確切方式其資料，並且可更確信該 hello 應用程式的行為不被用於惡意用途使用。</span><span class="sxs-lookup"><span data-stu-id="010c5-127">App users can know exactly how an app will use their data, and they can be more confident that hello app is not behaving with malicious intent.</span></span>

<span data-ttu-id="010c5-128">在 Azure AD 和 OAuth 中，這些類型的權限也稱為「範圍」。</span><span class="sxs-lookup"><span data-stu-id="010c5-128">In Azure AD and OAuth, these types of permissions are called *scopes*.</span></span> <span data-ttu-id="010c5-129">它們有時也會參照的 tooas *oAuth2Permissions*。</span><span class="sxs-lookup"><span data-stu-id="010c5-129">They also sometimes are referred tooas *oAuth2Permissions*.</span></span> <span data-ttu-id="010c5-130">在 Azure AD 中範圍會以字串值表示。</span><span class="sxs-lookup"><span data-stu-id="010c5-130">A scope is represented in Azure AD as a string value.</span></span> <span data-ttu-id="010c5-131">繼續 hello Microsoft Graph 範例，每個權限的 hello 範圍值是：</span><span class="sxs-lookup"><span data-stu-id="010c5-131">Continuing with hello Microsoft Graph example, hello scope value for each permission is:</span></span>

* <span data-ttu-id="010c5-132">使用 `Calendar.Read` 來讀取使用者的行事曆</span><span class="sxs-lookup"><span data-stu-id="010c5-132">Read a user's calendar by using `Calendar.Read`</span></span>
* <span data-ttu-id="010c5-133">您可以使用撰寫 tooa 使用者的行事曆`Mail.ReadWrite`</span><span class="sxs-lookup"><span data-stu-id="010c5-133">Write tooa user's calendar by using `Mail.ReadWrite`</span></span>
* <span data-ttu-id="010c5-134">使用 `Mail.Send` 來以使用者身分傳送郵件</span><span class="sxs-lookup"><span data-stu-id="010c5-134">Send mail as a user using by `Mail.Send`</span></span>

<span data-ttu-id="010c5-135">應用程式可以藉由指定要求 toohello v2.0 端點中的 hello 範圍要求這些權限。</span><span class="sxs-lookup"><span data-stu-id="010c5-135">An app can request these permissions by specifying hello scopes in requests toohello v2.0 endpoint.</span></span>

## <a name="openid-connect-scopes"></a><span data-ttu-id="010c5-136">OpenId Connect 範圍</span><span class="sxs-lookup"><span data-stu-id="010c5-136">OpenID Connect scopes</span></span>
<span data-ttu-id="010c5-137">OpenID Connect hello v2.0 實作具有少數妥善定義的範圍，不會套用 tooa 特定資源： `openid`， `email`， `profile`，和`offline_access`。</span><span class="sxs-lookup"><span data-stu-id="010c5-137">hello v2.0 implementation of OpenID Connect has a few well-defined scopes that do not apply tooa specific resource: `openid`, `email`, `profile`, and `offline_access`.</span></span>

### <a name="openid"></a><span data-ttu-id="010c5-138">openid</span><span class="sxs-lookup"><span data-stu-id="010c5-138">openid</span></span>
<span data-ttu-id="010c5-139">如果應用程式執行登入使用[OpenID Connect](active-directory-v2-protocols.md)，則必須要求 hello`openid`範圍。</span><span class="sxs-lookup"><span data-stu-id="010c5-139">If an app performs sign-in by using [OpenID Connect](active-directory-v2-protocols.md), it must request hello `openid` scope.</span></span> <span data-ttu-id="010c5-140">hello `openid` hello 工作帳戶的範圍顯示 hello 「 將您登入 」 權限的同意頁面和 hello 個人 Microsoft 帳戶的同意頁面為 hello"檢視您的設定檔及連接 tooapps 和使用您的 Microsoft 帳戶的服務 」 的權限。</span><span class="sxs-lookup"><span data-stu-id="010c5-140">hello `openid` scope shows on hello work account consent page as hello "Sign you in" permission, and on hello personal Microsoft account consent page as hello "View your profile and connect tooapps and services using your Microsoft account" permission.</span></span> <span data-ttu-id="010c5-141">這個權限，應用程式可以接收 hello 使用者的唯一識別碼 hello hello 形式`sub`宣告。</span><span class="sxs-lookup"><span data-stu-id="010c5-141">With this permission, an app can receive a unique identifier for hello user in hello form of hello `sub` claim.</span></span> <span data-ttu-id="010c5-142">同時也提供 hello 應用程式存取 toohello 使用者資訊端點。</span><span class="sxs-lookup"><span data-stu-id="010c5-142">It also gives hello app access toohello UserInfo endpoint.</span></span> <span data-ttu-id="010c5-143">hello`openid`在 hello v2.0 權杖端點 tooacquire ID 語彙基元，它可以是使用的 toosecure HTTP 呼叫的應用程式的不同元件之間，就可以使用範圍。</span><span class="sxs-lookup"><span data-stu-id="010c5-143">hello `openid` scope can be used at hello v2.0 token endpoint tooacquire ID tokens, which can be used toosecure HTTP calls between different components of an app.</span></span>

### <a name="email"></a><span data-ttu-id="010c5-144">電子郵件</span><span class="sxs-lookup"><span data-stu-id="010c5-144">email</span></span>
<span data-ttu-id="010c5-145">hello`email`範圍可以搭配 hello`openid`領域和任何其他項目。</span><span class="sxs-lookup"><span data-stu-id="010c5-145">hello `email` scope can be used with hello `openid` scope and any others.</span></span> <span data-ttu-id="010c5-146">它提供 hello 應用程式存取 toohello 使用者的主要電子郵件地址 hello hello 形式`email`宣告。</span><span class="sxs-lookup"><span data-stu-id="010c5-146">It gives hello app access toohello user's primary email address in hello form of hello `email` claim.</span></span> <span data-ttu-id="010c5-147">hello`email`宣告已包含在權杖中，只有電子郵件地址是 hello 使用者帳戶，但不一定 hello 案例相關聯。</span><span class="sxs-lookup"><span data-stu-id="010c5-147">hello `email` claim is included in a token only if an email address is associated with hello user account, which is not always hello case.</span></span> <span data-ttu-id="010c5-148">如果它使用 hello`email`範圍內，您的應用程式應該準備 toohandle 的案例中的 hello`email`宣告不存在於 hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="010c5-148">If it uses hello `email` scope, your app should be prepared toohandle a case in which hello `email` claim does not exist in hello token.</span></span>

### <a name="profile"></a><span data-ttu-id="010c5-149">設定檔</span><span class="sxs-lookup"><span data-stu-id="010c5-149">profile</span></span>
<span data-ttu-id="010c5-150">hello`profile`範圍可以搭配 hello`openid`領域和任何其他項目。</span><span class="sxs-lookup"><span data-stu-id="010c5-150">hello `profile` scope can be used with hello `openid` scope and any others.</span></span> <span data-ttu-id="010c5-151">它提供 hello 應用程式存取 tooa 大量的 hello 使用者的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="010c5-151">It gives hello app access tooa substantial amount of information about hello user.</span></span> <span data-ttu-id="010c5-152">它可以存取的 hello 資訊包括但不是會受限於至 hello 使用者的名字、 姓氏、 慣用的使用者名稱和物件識別碼。</span><span class="sxs-lookup"><span data-stu-id="010c5-152">hello information it can access includes, but is not limited to, hello user's given name, surname, preferred username, and object ID.</span></span> <span data-ttu-id="010c5-153">Hello 設定檔宣告 hello id_tokens 參數中使用特定使用者的完整清單，請參閱 hello [v2.0 權杖參考](active-directory-v2-tokens.md)。</span><span class="sxs-lookup"><span data-stu-id="010c5-153">For a complete list of hello profile claims available in hello id_tokens parameter for a specific user, see hello [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

### <a name="offlineaccess"></a><span data-ttu-id="010c5-154">offline_access</span><span class="sxs-lookup"><span data-stu-id="010c5-154">offline_access</span></span>
<span data-ttu-id="010c5-155">hello [ `offline_access`範圍](http://openid.net/specs/openid-connect-core-1_0.html#OfflineAccess)代表 hello 使用者提供您的應用程式存取 tooresources 相當長的時間。</span><span class="sxs-lookup"><span data-stu-id="010c5-155">hello [`offline_access` scope](http://openid.net/specs/openid-connect-core-1_0.html#OfflineAccess) gives your app access tooresources on behalf of hello user for an extended time.</span></span> <span data-ttu-id="010c5-156">在 hello 工作帳戶的同意頁面上，此範圍會顯示為 hello 「 隨時存取您的資料 」 的權限。</span><span class="sxs-lookup"><span data-stu-id="010c5-156">On hello work account consent page, this scope appears as hello "Access your data anytime" permission.</span></span> <span data-ttu-id="010c5-157">在 hello 個人 Microsoft 帳戶的同意頁面上，它會出現如下 hello 「 隨時存取您的資訊 」 權限。</span><span class="sxs-lookup"><span data-stu-id="010c5-157">On hello personal Microsoft account consent page, it appears as hello "Access your info anytime" permission.</span></span> <span data-ttu-id="010c5-158">當使用者核准 hello`offline_access`範圍內，您的應用程式可以接收來自 hello v2.0 權杖端點的重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="010c5-158">When a user approves hello `offline_access` scope, your app can receive refresh tokens from hello v2.0 token endpoint.</span></span> <span data-ttu-id="010c5-159">重新整理權杖是長期權杖。</span><span class="sxs-lookup"><span data-stu-id="010c5-159">Refresh tokens are long-lived.</span></span> <span data-ttu-id="010c5-160">您的應用程式可以在舊存取權杖到期時取得新的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="010c5-160">Your app can get new access tokens as older ones expire.</span></span>

<span data-ttu-id="010c5-161">如果您的應用程式沒有要求 hello`offline_access`範圍，它不會收到重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="010c5-161">If your app does not request hello `offline_access` scope, it won't receive refresh tokens.</span></span> <span data-ttu-id="010c5-162">這表示當兌換授權碼中 hello [OAuth 2.0 授權碼流程](active-directory-v2-protocols.md)，您將會收到只存取權杖來自 hello`/token`端點。</span><span class="sxs-lookup"><span data-stu-id="010c5-162">This means that when you redeem an authorization code in hello [OAuth 2.0 authorization code flow](active-directory-v2-protocols.md), you'll receive only an access token from hello `/token` endpoint.</span></span> <span data-ttu-id="010c5-163">hello 存取權杖是有效的短時間。</span><span class="sxs-lookup"><span data-stu-id="010c5-163">hello access token is valid for a short time.</span></span> <span data-ttu-id="010c5-164">hello 存取權杖通常會在一小時後到期。</span><span class="sxs-lookup"><span data-stu-id="010c5-164">hello access token usually expires in one hour.</span></span> <span data-ttu-id="010c5-165">此時，您的應用程式需要 tooredirect hello 使用者回復 toohello`/authorize`端點 tooget 新的授權碼。</span><span class="sxs-lookup"><span data-stu-id="010c5-165">At that point, your app needs tooredirect hello user back toohello `/authorize` endpoint tooget a new authorization code.</span></span> <span data-ttu-id="010c5-166">這個重新導向，根據 hello 類型的應用程式，在 hello 使用者可能會再次需要 tooenter 他們的認證，或再次同意 toopermissions。</span><span class="sxs-lookup"><span data-stu-id="010c5-166">During this redirect, depending on hello type of app, hello user might need tooenter their credentials again or consent again toopermissions.</span></span>

<span data-ttu-id="010c5-167">如需有關如何在 tooget 並使用重新整理權杖的詳細資訊，請參閱 hello [v2.0 通訊協定參考](active-directory-v2-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="010c5-167">For more information about how tooget and use refresh tokens, see hello [v2.0 protocol reference](active-directory-v2-protocols.md).</span></span>

## <a name="requesting-individual-user-consent"></a><span data-ttu-id="010c5-168">要求個別使用者同意</span><span class="sxs-lookup"><span data-stu-id="010c5-168">Requesting individual user consent</span></span>
<span data-ttu-id="010c5-169">在[OpenID Connect 或 OAuth 2.0](active-directory-v2-protocols.md)授權要求時，應用程式可以要求 hello 權限需要使用 hello`scope`查詢參數。</span><span class="sxs-lookup"><span data-stu-id="010c5-169">In an [OpenID Connect or OAuth 2.0](active-directory-v2-protocols.md) authorization request, an app can request hello permissions it needs by using hello `scope` query parameter.</span></span> <span data-ttu-id="010c5-170">例如，當使用者登入時 tooan 應用程式，hello 應用程式將要求傳送 hello （使用加上換行以利閱讀） 下列範例類似：</span><span class="sxs-lookup"><span data-stu-id="010c5-170">For example, when a user signs in tooan app, hello app sends a request like hello following example (with line breaks added for legibility):</span></span>

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=
https%3A%2F%2Fgraph.microsoft.com%2Fcalendar.read%20
https%3A%2F%2Fgraph.microsoft.com%2Fmail.send
&state=12345
```

<span data-ttu-id="010c5-171">hello`scope`參數是以空格分隔清單的範圍 hello 應用程式的要求。</span><span class="sxs-lookup"><span data-stu-id="010c5-171">hello `scope` parameter is a space-separated list of scopes that hello app is requesting.</span></span> <span data-ttu-id="010c5-172">每個範圍會以附加 hello 範圍值 toohello 資源的識別項 (hello 應用程式識別碼 URI)。</span><span class="sxs-lookup"><span data-stu-id="010c5-172">Each scope is indicated by appending hello scope value toohello resource's identifier (hello Application ID URI).</span></span> <span data-ttu-id="010c5-173">在 hello 要求範例中，hello 應用程式需要使用權限 tooread hello 使用者的行事曆和 hello 使用者的身分傳送郵件。</span><span class="sxs-lookup"><span data-stu-id="010c5-173">In hello request example, hello app needs permission tooread hello user's calendar and send mail as hello user.</span></span>

<span data-ttu-id="010c5-174">Hello v2.0 端點 hello 使用者輸入其認證之後，會檢查的相符記錄*使用者同意*。</span><span class="sxs-lookup"><span data-stu-id="010c5-174">After hello user enters their credentials, hello v2.0 endpoint checks for a matching record of *user consent*.</span></span> <span data-ttu-id="010c5-175">如果不同意 hello 使用者的 hello tooany 要求的權限在過去，hello hello v2.0 端點要求 hello 使用者 toogrant hello 要求的權限。</span><span class="sxs-lookup"><span data-stu-id="010c5-175">If hello user has not consented tooany of hello requested permissions in hello past, hello v2.0 endpoint asks hello user toogrant hello requested permissions.</span></span>

![工作帳戶同意](../../media/active-directory-v2-flows/work_account_consent.png)

<span data-ttu-id="010c5-177">當 hello 使用者核准 hello 權限時，如此 hello 使用者不需要 tooconsent 再次在後續的帳戶登入記錄 hello 同意。</span><span class="sxs-lookup"><span data-stu-id="010c5-177">When hello user approves hello permission, hello consent is recorded so that hello user doesn't have tooconsent again on subsequent account sign-ins.</span></span>

## <a name="requesting-consent-for-an-entire-tenant"></a><span data-ttu-id="010c5-178">要求整個租用戶的同意</span><span class="sxs-lookup"><span data-stu-id="010c5-178">Requesting consent for an entire tenant</span></span>
<span data-ttu-id="010c5-179">通常，在組織購買的授權或訂用帳戶的應用程式，hello 組織會想為其員工 toofully 佈建 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="010c5-179">Often, when an organization purchases a license or subscription for an application, hello organization wants toofully provision hello application for its employees.</span></span> <span data-ttu-id="010c5-180">此程序的一部分，系統管理員可以將同意授與 hello 應用程式 tooact 代表任何員工。</span><span class="sxs-lookup"><span data-stu-id="010c5-180">As part of this process, an administrator can grant consent for hello application tooact on behalf of any employee.</span></span> <span data-ttu-id="010c5-181">如果 hello 系統管理員授與 hello 整個租用戶的同意，hello 組織的員工就不會看見 hello 應用程式的同意頁面。</span><span class="sxs-lookup"><span data-stu-id="010c5-181">If hello admin grants consent for hello entire tenant, hello organization's employees won't see a consent page for hello application.</span></span>

<span data-ttu-id="010c5-182">toorequest 同意的租用戶，您的應用程式中的所有使用者都可以使用 hello 系統管理員同意端點。</span><span class="sxs-lookup"><span data-stu-id="010c5-182">toorequest consent for all users in a tenant, your app can use hello admin consent endpoint.</span></span>

## <a name="admin-restricted-scopes"></a><span data-ttu-id="010c5-183">受系統管理員限制的範圍</span><span class="sxs-lookup"><span data-stu-id="010c5-183">Admin-restricted scopes</span></span>
<span data-ttu-id="010c5-184">可以設定 hello Microsoft 生態系統中的某些高權限得*管理員限制*。</span><span class="sxs-lookup"><span data-stu-id="010c5-184">Some high-privilege permissions in hello Microsoft ecosystem can be set too*admin-restricted*.</span></span> <span data-ttu-id="010c5-185">這類的範圍的範例包括下列權限的 hello:</span><span class="sxs-lookup"><span data-stu-id="010c5-185">Examples of these kinds of scopes include hello following permissions:</span></span>

* <span data-ttu-id="010c5-186">使用 `Directory.Read` 來讀取組織的目錄資料</span><span class="sxs-lookup"><span data-stu-id="010c5-186">Read an organization's directory data by using `Directory.Read`</span></span>
* <span data-ttu-id="010c5-187">您可以使用撰寫資料 tooan 組織的目錄`Directory.ReadWrite`</span><span class="sxs-lookup"><span data-stu-id="010c5-187">Write data tooan organization's directory by using `Directory.ReadWrite`</span></span>
* <span data-ttu-id="010c5-188">使用 `Groups.Read.All` 來讀取組織目錄中的安全性群組</span><span class="sxs-lookup"><span data-stu-id="010c5-188">Read security groups in an organization's directory by using `Groups.Read.All`</span></span>

<span data-ttu-id="010c5-189">雖然取用者使用者集可能會授與應用程式存取 toothis 種類的資料，組織的使用者權限授與存取 toohello 相同設定的公司的機密資料。</span><span class="sxs-lookup"><span data-stu-id="010c5-189">Although a consumer user might grant an application access toothis kind of data, organizational users are restricted from granting access toohello same set of sensitive company data.</span></span> <span data-ttu-id="010c5-190">如果您的應用程式會要求這些權限的存取 tooone 從組織的使用者，hello 使用者會收到錯誤訊息，指出它們不是授權的 tooconsent tooyour 應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="010c5-190">If your application requests access tooone of these permissions from an organizational user, hello user receives an error message that says they are not authorized tooconsent tooyour app's permissions.</span></span>

<span data-ttu-id="010c5-191">如果您的應用程式需要存取組織 tooadmin 限制領域，您應該要求它們直接從公司系統管理員，也使用 hello 系統管理員同意端點一節所說明。</span><span class="sxs-lookup"><span data-stu-id="010c5-191">If your app requires access tooadmin-restricted scopes for organizations, you should request them directly from a company administrator, also by using hello admin consent endpoint, described next.</span></span>

<span data-ttu-id="010c5-192">當系統管理員授與這些權限透過 hello 系統管理員同意端點時，授與同意 hello 租用戶中的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="010c5-192">When an administrator grants these permissions via hello admin consent endpoint, consent is granted for all users in hello tenant.</span></span>

## <a name="using-hello-admin-consent-endpoint"></a><span data-ttu-id="010c5-193">使用 hello 系統管理員同意端點</span><span class="sxs-lookup"><span data-stu-id="010c5-193">Using hello admin consent endpoint</span></span>
<span data-ttu-id="010c5-194">如果您依照這些步驟，您的應用程式便能針對租用戶中所有的使用者收集權限，包括受系統管理員限制的範圍。</span><span class="sxs-lookup"><span data-stu-id="010c5-194">If you follow these steps, your app can gather permissions for all users in a tenant, including admin-restricted scopes.</span></span> <span data-ttu-id="010c5-195">toosee 實作 hello 步驟的程式碼範例，請參閱 「 hello[管理員限制範圍範例](https://github.com/Azure-Samples/active-directory-dotnet-admin-restricted-scopes-v2)。</span><span class="sxs-lookup"><span data-stu-id="010c5-195">toosee a code sample that implements hello steps, see hello [admin-restricted scopes sample](https://github.com/Azure-Samples/active-directory-dotnet-admin-restricted-scopes-v2).</span></span>

### <a name="request-hello-permissions-in-hello-app-registration-portal"></a><span data-ttu-id="010c5-196">要求在 hello 應用程式註冊入口網站中的 hello 權限</span><span class="sxs-lookup"><span data-stu-id="010c5-196">Request hello permissions in hello app registration portal</span></span>
1. <span data-ttu-id="010c5-197">移 tooyour 應用程式在 hello[應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)，或[建立應用程式](active-directory-v2-app-registration.md)如果尚未這麼做。</span><span class="sxs-lookup"><span data-stu-id="010c5-197">Go tooyour application in hello [Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or [create an app](active-directory-v2-app-registration.md) if you haven't already.</span></span>
2. <span data-ttu-id="010c5-198">找出 hello **Microsoft Graph 權限**區段，然後再新增您的應用程式所需的 hello 權限。</span><span class="sxs-lookup"><span data-stu-id="010c5-198">Locate hello **Microsoft Graph Permissions** section, and then add hello permissions that your app requires.</span></span>
3. <span data-ttu-id="010c5-199">請確定您**儲存**hello 應用程式註冊。</span><span class="sxs-lookup"><span data-stu-id="010c5-199">Make sure you **Save** hello app registration.</span></span>

### <a name="recommended-sign-hello-user-in-tooyour-app"></a><span data-ttu-id="010c5-200">建議使用： 號 hello 使用者 tooyour 應用程式中</span><span class="sxs-lookup"><span data-stu-id="010c5-200">Recommended: Sign hello user in tooyour app</span></span>
<span data-ttu-id="010c5-201">一般而言，當您建置應用程式時，會使用 hello 系統管理員同意端點，hello 應用程式所需的頁面或檢視中的 hello 系統管理員可以核准 hello 應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="010c5-201">Typically, when you build an application that uses hello admin consent endpoint, hello app needs a page or view in which hello admin can approve hello app's permissions.</span></span> <span data-ttu-id="010c5-202">此頁面可以是 hello 應用程式註冊流程的一部分，一部分 hello 應用程式的設定，或它可以是專用，「 連接 」 流程。</span><span class="sxs-lookup"><span data-stu-id="010c5-202">This page can be part of hello app's sign-up flow, part of hello app's settings, or it can be a dedicated "connect" flow.</span></span> <span data-ttu-id="010c5-203">在許多情況下，是合理的 hello 應用程式 tooshow 這 「 連接 」 檢視只能在使用者登入工作或學校的 Microsoft 帳戶之後。</span><span class="sxs-lookup"><span data-stu-id="010c5-203">In many cases, it makes sense for hello app tooshow this "connect" view only after a user has signed in with a work or school Microsoft account.</span></span>

<span data-ttu-id="010c5-204">當您登入時 hello tooyour 應用程式中的使用者時，您可以識別 hello 組織 toowhich hello 管理員所屬之前要求他們 tooapprove hello 必要的權限。</span><span class="sxs-lookup"><span data-stu-id="010c5-204">When you sign hello user in tooyour app, you can identify hello organization toowhich hello admin belongs before asking them tooapprove hello necessary permissions.</span></span> <span data-ttu-id="010c5-205">雖然這並非絕對必要，但這麼做可協助您為組織使用者建立更直覺式的體驗。</span><span class="sxs-lookup"><span data-stu-id="010c5-205">Although not strictly necessary, it can help you create a more intuitive experience for your organizational users.</span></span> <span data-ttu-id="010c5-206">在後續的 toosign hello 使用者我們[v2.0 通訊協定教學課程](active-directory-v2-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="010c5-206">toosign hello user in, follow our [v2.0 protocol tutorials](active-directory-v2-protocols.md).</span></span>

### <a name="request-hello-permissions-from-a-directory-admin"></a><span data-ttu-id="010c5-207">從目錄管理員要求 hello 權限</span><span class="sxs-lookup"><span data-stu-id="010c5-207">Request hello permissions from a directory admin</span></span>
<span data-ttu-id="010c5-208">當您準備好 toorequest 貴組織的管理員權限時，您可以重新導向 hello 使用者 toohello v2.0*系統管理員同意端點*。</span><span class="sxs-lookup"><span data-stu-id="010c5-208">When you're ready toorequest permissions from your organization's admin, you can redirect hello user toohello v2.0 *admin consent endpoint*.</span></span>

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting hello below request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| <span data-ttu-id="010c5-209">參數</span><span class="sxs-lookup"><span data-stu-id="010c5-209">Parameter</span></span> | <span data-ttu-id="010c5-210">條件</span><span class="sxs-lookup"><span data-stu-id="010c5-210">Condition</span></span> | <span data-ttu-id="010c5-211">說明</span><span class="sxs-lookup"><span data-stu-id="010c5-211">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010c5-212">tenant</span><span class="sxs-lookup"><span data-stu-id="010c5-212">tenant</span></span> |<span data-ttu-id="010c5-213">必要</span><span class="sxs-lookup"><span data-stu-id="010c5-213">Required</span></span> |<span data-ttu-id="010c5-214">您想要從 toorequest 權限 hello 目錄租用戶。</span><span class="sxs-lookup"><span data-stu-id="010c5-214">hello directory tenant that you want toorequest permission from.</span></span> <span data-ttu-id="010c5-215">可以採用 GUID 或易記名稱格式。</span><span class="sxs-lookup"><span data-stu-id="010c5-215">Can be provided in GUID or friendly name format.</span></span> |
| <span data-ttu-id="010c5-216">client_id</span><span class="sxs-lookup"><span data-stu-id="010c5-216">client_id</span></span> |<span data-ttu-id="010c5-217">必要</span><span class="sxs-lookup"><span data-stu-id="010c5-217">Required</span></span> |<span data-ttu-id="010c5-218">hello 應用程式識別碼的 hello[應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)指派 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="010c5-218">hello Application ID that hello [Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) assigned tooyour app.</span></span> |
| <span data-ttu-id="010c5-219">redirect_uri</span><span class="sxs-lookup"><span data-stu-id="010c5-219">redirect_uri</span></span> |<span data-ttu-id="010c5-220">必要</span><span class="sxs-lookup"><span data-stu-id="010c5-220">Required</span></span> |<span data-ttu-id="010c5-221">hello 重新導向您想要針對應用程式 toohandle 傳送 hello 回應 toobe 的 URI。</span><span class="sxs-lookup"><span data-stu-id="010c5-221">hello redirect URI where you want hello response toobe sent for your app toohandle.</span></span> <span data-ttu-id="010c5-222">它必須完全符合其中一個 hello 重新導向您 hello 應用程式註冊入口網站中註冊的 Uri。</span><span class="sxs-lookup"><span data-stu-id="010c5-222">It must exactly match one of hello redirect URIs that you registered in hello app registration portal.</span></span> |
| <span data-ttu-id="010c5-223">state</span><span class="sxs-lookup"><span data-stu-id="010c5-223">state</span></span> |<span data-ttu-id="010c5-224">建議</span><span class="sxs-lookup"><span data-stu-id="010c5-224">Recommended</span></span> |<span data-ttu-id="010c5-225">Hello 權杖回應中也會傳回的 hello 要求中包含一個值。</span><span class="sxs-lookup"><span data-stu-id="010c5-225">A value included in hello request that will also be returned in hello token response.</span></span> <span data-ttu-id="010c5-226">它可以是您想要的任何內容的字串。</span><span class="sxs-lookup"><span data-stu-id="010c5-226">It can be a string of any content you want.</span></span> <span data-ttu-id="010c5-227">發生 hello 驗證要求，例如 hello 頁面或檢視上之前，請使用 hello 應用程式中的 hello 使用者的狀態相關的 hello 狀態 tooencode 資訊。</span><span class="sxs-lookup"><span data-stu-id="010c5-227">Use hello state tooencode information about hello user's state in hello app before hello authentication request occurred, such as hello page or view they were on.</span></span> |

<span data-ttu-id="010c5-228">此時，Azure AD 需要租用戶系統管理員 toosign toocomplete hello 要求中。</span><span class="sxs-lookup"><span data-stu-id="010c5-228">At this point, Azure AD requires a tenant administrator toosign in toocomplete hello request.</span></span> <span data-ttu-id="010c5-229">hello 系統管理員要求的 tooapprove 所有 hello 您要求的 hello 應用程式註冊入口網站中的應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="010c5-229">hello administrator is asked tooapprove all hello permissions that you have requested for your app in hello app registration portal.</span></span>

#### <a name="successful-response"></a><span data-ttu-id="010c5-230">成功回應</span><span class="sxs-lookup"><span data-stu-id="010c5-230">Successful response</span></span>
<span data-ttu-id="010c5-231">如果 hello 系統管理員核准 hello 應用程式的權限，成功的回應 hello 看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="010c5-231">If hello admin approves hello permissions for your app, hello successful response looks like this:</span></span>

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| <span data-ttu-id="010c5-232">參數</span><span class="sxs-lookup"><span data-stu-id="010c5-232">Parameter</span></span> | <span data-ttu-id="010c5-233">說明</span><span class="sxs-lookup"><span data-stu-id="010c5-233">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010c5-234">tenant</span><span class="sxs-lookup"><span data-stu-id="010c5-234">tenant</span></span> |<span data-ttu-id="010c5-235">hello 目錄租用戶授與您的應用程式 hello 權限要求，GUID 格式。</span><span class="sxs-lookup"><span data-stu-id="010c5-235">hello directory tenant that granted your application hello permissions it requested, in GUID format.</span></span> |
| <span data-ttu-id="010c5-236">state</span><span class="sxs-lookup"><span data-stu-id="010c5-236">state</span></span> |<span data-ttu-id="010c5-237">將傳回 hello 權杖回應中的 hello 要求中包含一個值。</span><span class="sxs-lookup"><span data-stu-id="010c5-237">A value included in hello request that also will be returned in hello token response.</span></span> <span data-ttu-id="010c5-238">它可以是您想要的任何內容的字串。</span><span class="sxs-lookup"><span data-stu-id="010c5-238">It can be a string of any content you want.</span></span> <span data-ttu-id="010c5-239">hello 狀態是使用的 tooencode hello 應用程式中的 hello 使用者狀態資訊之前發生 hello 驗證要求，例如 hello 頁面或檢視上。</span><span class="sxs-lookup"><span data-stu-id="010c5-239">hello state is used tooencode information about hello user's state in hello app before hello authentication request occurred, such as hello page or view they were on.</span></span> |
| <span data-ttu-id="010c5-240">admin_consent</span><span class="sxs-lookup"><span data-stu-id="010c5-240">admin_consent</span></span> |<span data-ttu-id="010c5-241">將太**true**。</span><span class="sxs-lookup"><span data-stu-id="010c5-241">Will be set too**true**.</span></span> |

#### <a name="error-response"></a><span data-ttu-id="010c5-242">錯誤回應</span><span class="sxs-lookup"><span data-stu-id="010c5-242">Error response</span></span>
<span data-ttu-id="010c5-243">如果 hello 系統管理員不會核准 hello 應用程式的權限，hello 失敗回應看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="010c5-243">If hello admin does not approve hello permissions for your app, hello failed response looks like this:</span></span>

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| <span data-ttu-id="010c5-244">參數</span><span class="sxs-lookup"><span data-stu-id="010c5-244">Parameter</span></span> | <span data-ttu-id="010c5-245">說明</span><span class="sxs-lookup"><span data-stu-id="010c5-245">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="010c5-246">錯誤</span><span class="sxs-lookup"><span data-stu-id="010c5-246">error</span></span> |<span data-ttu-id="010c5-247">錯誤的程式碼字串是使用的 tooclassify 類型之錯誤的發生，且可以使用的 tooreact tooerrors。</span><span class="sxs-lookup"><span data-stu-id="010c5-247">An error code string that can be used tooclassify types of errors that occur, and can be used tooreact tooerrors.</span></span> |
| <span data-ttu-id="010c5-248">error_description</span><span class="sxs-lookup"><span data-stu-id="010c5-248">error_description</span></span> |<span data-ttu-id="010c5-249">特定的錯誤訊息，可協助開發人員識別 hello 根本原因的錯誤。</span><span class="sxs-lookup"><span data-stu-id="010c5-249">A specific error message that can help a developer identify hello root cause of an error.</span></span> |

<span data-ttu-id="010c5-250">收到 hello 系統管理員同意端點的成功回應之後，您的應用程式已取得它所要求的 hello 權限。</span><span class="sxs-lookup"><span data-stu-id="010c5-250">After you've received a successful response from hello admin consent endpoint, your app has gained hello permissions it requested.</span></span> <span data-ttu-id="010c5-251">接下來，您可以要求您想要的 hello 資源語彙基元。</span><span class="sxs-lookup"><span data-stu-id="010c5-251">Next, you can request a token for hello resource you want.</span></span>

## <a name="using-permissions"></a><span data-ttu-id="010c5-252">使用權限</span><span class="sxs-lookup"><span data-stu-id="010c5-252">Using permissions</span></span>
<span data-ttu-id="010c5-253">Hello 使用者同意 toopermissions 應用程式之後，您的應用程式可以取得存取權杖，代表您的應用程式的權限 tooaccess 某些容量中的資源。</span><span class="sxs-lookup"><span data-stu-id="010c5-253">After hello user consents toopermissions for your app, your app can acquire access tokens that represent your app's permission tooaccess a resource in some capacity.</span></span> <span data-ttu-id="010c5-254">存取權杖可僅針對單一資源，但編碼 hello 存取權杖內為您的應用程式已被授與該資源的每個權限。</span><span class="sxs-lookup"><span data-stu-id="010c5-254">An access token can be used only for a single resource, but encoded inside hello access token is every permission that your app has been granted for that resource.</span></span> <span data-ttu-id="010c5-255">tooacquire 存取權杖，您的應用程式可以進行要求 toohello v2.0 權杖端點，就像這樣：</span><span class="sxs-lookup"><span data-stu-id="010c5-255">tooacquire an access token, your app can make a request toohello v2.0 token endpoint, like this:</span></span>

```
POST common/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/json

{
    "grant_type": "authorization_code",
    "client_id": "6731de76-14a6-49ae-97bc-6eba6914391e",
    "scope": "https://outlook.office.com/mail.read https://outlook.office.com/mail.send",
    "code": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq..."
    "redirect_uri": "https://localhost/myapp",
    "client_secret": "zc53fwe80980293klaj9823"  // NOTE: Only required for web apps
}
```

<span data-ttu-id="010c5-256">您可以使用 hello 產生的存取權杖中 HTTP 要求 toohello 資源。</span><span class="sxs-lookup"><span data-stu-id="010c5-256">You can use hello resulting access token in HTTP requests toohello resource.</span></span> <span data-ttu-id="010c5-257">它會可靠地指出 toohello 資源應用程式有 hello 適當的權限 tooperform 特定工作。</span><span class="sxs-lookup"><span data-stu-id="010c5-257">It reliably indicates toohello resource that your app has hello proper permission tooperform a specific task.</span></span>  

<span data-ttu-id="010c5-258">如需有關 hello OAuth 2.0 通訊協定，以及如何 tooget 存取權杖，請參閱 hello [v2.0 端點通訊協定參考](active-directory-v2-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="010c5-258">For more information about hello OAuth 2.0 protocol and how tooget access tokens, see hello [v2.0 endpoint protocol reference](active-directory-v2-protocols.md).</span></span>
